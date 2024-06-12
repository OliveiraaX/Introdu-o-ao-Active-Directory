#NTLM Authentication
Além do Kerberos e do LDAP, o Active Directory usa vários outros métodos de autenticação que podem ser usados ​ por aplicativos e serviços no AD. 
*Isso inclui LM, NTLM, NTLMv1 e NTLMv2. LM e NTLM* aqui são os nomes de hash, **e NTLMv1 e NTLMv2 são protocolos de autenticação que utilizam o hash LM ou NT**. Abaixo está uma rápida comparação entre esses hashes e protocolos, o que nos mostra que, embora não seja perfeito de forma alguma, o Kerberos costuma ser o protocolo de autenticação preferido sempre que possível. É essencial entender a diferença entre os tipos de hash e os protocolos que os utilizam.

#### Comparação de protocolo Hash

| **Hash/Protocolo** | **Técnica criptográfica**                                  | **Autenticação Mútua** | **Tipo de mensagem**                  | **Terceiro confiável**                                        |
| ------------------ | ---------------------------------------------------------- | ---------------------- | ------------------------------------- | ------------------------------------------------------------- |
| `NTLM`             | Criptografia de chave simétrica                            | Não                    | Número aleatório                      | Controlador de Domínio                                        |
| `NTLMv1`           | Criptografia de chave simétrica                            | Não                    | Hash MD4, número aleatório            | Controlador de Domínio                                        |
| `NTLMv2`           | Criptografia de chave simétrica                            | Não                    | Hash MD4, número aleatório            | Controlador de Domínio                                        |
| `Kerberos`         | Criptografia de chave simétrica e criptografia assimétrica | Sim                    | Bilhete criptografado usando DES, MD5 | Controlador de Domínio/Centro de Distribuição de Chaves (KDC) |

---

## LM

#### O que são Hashes LM?
- **Definição**: São um método antigo de armazenamento de senhas usado no sistema operacional Windows, estreado em 1987 no OS/2.
- **Local de Armazenamento**: Encontrados no banco de dados SAM em hosts Windows e no banco de dados NTDS.DIT em Controladores de Domínio.

#### Problemas e Status Atual

- **Falhas de Segurança**: O algoritmo de hash LM possui vulnerabilidades significativas.
- **Status Atual**: Desativado por padrão desde o Windows Vista/Server 2008, mas ainda pode ser encontrado em sistemas antigos, especialmente em grandes ambientes corporativos.

#### Características dos Hashes LM

- **Comprimento da Senha**: Limitada a um máximo de 14 caracteres.
- **Case Insensitive**: Senhas convertidas para letras maiúsculas, limitando o espaço de chave a 69 caracteres.
- **Facilidade de Quebra**: Relativamente fácil de quebrar usando ferramentas como o Hashcat.

#### Processo de Hashing

1. **Divisão da Senha**: Senha de 14 caracteres dividida em dois blocos de sete caracteres.
2. **Preenchimento com NULL**: Senhas com menos de 14 caracteres são preenchidas com caracteres NULL.
3. **Criação de Chaves DES**: Cada bloco de 7 caracteres é transformado em uma chave DES.
4. **Criptografia**: Blocos criptografados usando a string `KGS!@#$%`, criando dois valores cifrados de 8 bytes.
5. **Concatenação**: Os dois valores são concatenados para formar o hash LM.

#### Vulnerabilidade Adicional

- **Força Bruta Facilitada**: Ataque de força bruta precisa ser aplicado em dois blocos de sete caracteres, em vez de em uma senha inteira de 14 caracteres, acelerando o processo de quebra.
- **Hash de Metade Fixa**: Para senhas de 7 caracteres ou menos, a segunda metade do hash LM é sempre a mesma e pode ser identificada visualmente.

#### Exemplo de Hash LM

- Forma típica: `299bd128c1101fd6`.

#### Prevenção

- **Política de Grupo**: O uso de hashes LM pode ser proibido através de configurações de Política de Grupo.
**Observação:** os sistemas operacionais Windows anteriores ao Windows Vista e ao Windows Server 2008 (Windows NT4, Windows 2000, Windows 2003, Windows XP) armazenavam o hash LM e o hash NTLM da senha de um usuário por padrão.

---

## NTHash (NTLM)
#### O que é o NTLM?

- **Definição**: NT LAN Manager (NTLM) é um protocolo de autenticação desafio-resposta utilizado em sistemas Windows modernos.
- **Armazenamento**: Os hashes NTLM são armazenados localmente no banco de dados SAM ou no banco de dados NTDS.DIT em um Controlador de Domínio.

#### Processo de Autenticação NTLM

- **Protocolo Desafio-Resposta**:
    1. **NEGOTIATE_MESSAGE**: O cliente envia uma mensagem de negociação para o servidor.
    2. **CHALLENGE_MESSAGE**: O servidor responde com um desafio para verificar a identidade do cliente.
    3. **AUTHENTICATE_MESSAGE**: O cliente responde com uma mensagem de autenticação.

#### Detalhes Técnicos

- **Tipos de Hash**:
    - **Hash LM**: Utilizado em sistemas antigos (menos seguro).
    - **Hash NT**: Utilizado para autenticação em sistemas modernos.
        - **Algoritmo**: O hash NT é o resultado do hash MD4 do valor da senha codificada em UTF-16 little-endian.
        - **Formulação**: `MD4(UTF-16-LE(password))`.

#### Segurança

- **Força e Vulnerabilidades**:
    - **Hash NT**: Consideravelmente mais forte que o hash LM, suportando todo o conjunto de caracteres Unicode de 65.536 caracteres.
    - **Quebra de Hash**: Apesar da segurança, hashes NTLM podem ser quebrados offline com ferramentas como Hashcat. Um hash NTLM de 8 caracteres pode ser quebrado por força bruta em menos de 3 horas usando GPUs.
    - **Ataque Pass-the-Hash**: Um invasor pode usar o hash NTLM diretamente para autenticação em sistemas de destino onde o usuário é um administrador local, sem precisar conhecer a senha em texto claro.

#### Estrutura de um Hash NTLM

- **Exemplo**: `Rachel:500:aad3c435b514a4eeaad3b935b51304fe:e46b9e548fa0d122de7f59fb6d48eaa2:::`
    - `Rachel`: Nome de usuário.
    - `500`: Identificador Relativo (RID), 500 é o RID conhecido para a conta `administrator`.
    - `aad3c435b514a4eeaad3b935b51304fe`: Hash LM (não utilizado se os hashes LM estiverem desativados).
    - `e46b9e548fa0d122de7f59fb6d48eaa2`: Hash NT (pode ser quebrado offline ou usado para ataques pass-the-hash).

#### Exemplo de Ataque Pass-the-Hash

- **Ferramenta CrackMapExec**:
    `crackmapexec smb 10.129.41.19 -u rachel -H e46b9e548fa0d122de7f59fb6d48eaa2 
    
    `SMB 10.129.43.9 445 DC01 [*] Windows 10.0 Build 17763 (name:DC01) (domain:exemplo.LOCAL) (signing:True) (SMBv1:False)
	
    `SMB 10.129.43.9 445 DC01 [+] exemplo.LOCAL\rachel:e46b9e548fa0d122de7f59fb6d48eaa2 (Pwn3d!)`
    

#### NTLMv1 e NTLMv2

- **Progressão do Protocolo**: O NTLM evoluiu de NTLMv1 para NTLMv2 para melhorar a segurança. Nem LANMAN nem NTLM usam salt, o que os torna vulneráveis a certos tipos de ataques.

#### Conclusão

- **Utilização**: NTLM continua sendo amplamente utilizado devido à sua compatibilidade com versões anteriores e integração com o Active Directory, apesar de suas vulnerabilidades conhecidas. É essencial estar ciente das suas fraquezas e tomar medidas para proteger as credenciais armazenadas e transmitidas.

---

## NTLMv1 (Rede-NTLMv1)
#### Funcionamento

- **Autenticação Desafio/Resposta**: NTLMv1 usa um processo de desafio/resposta para autenticar o cliente.
- **Hash Utilizado**: Utiliza o hash NT e o hash LM.
- **Uso**: Utilizado para autenticação de rede.
- **Insegurança**: Facilita o "crack" off-line após a captura do hash usando ferramentas como o [Responder](https://github.com/lgandx/Responder) ou por meio de um [ataque de retransmissão NTLM](https://byt3bl33d3r.github.io/practical-guide-to-ntlm-relaying-in-2017-aka-getting-a-foothold-in-under-5-minutes.html).

#### Algoritmo de Desafio/Resposta NTLMv1

`C = 8-byte server challenge, random K1 | K2 | K3 = LM/NT-hash | 5-bytes-0 response = DES(K1,C) | DES(K2,C) | DES(K3,C)`

- **Desafio**: O servidor envia um desafio aleatório de 8 bytes para o cliente.
- **Resposta**: O cliente retorna uma resposta de 24 bytes.

#### Exemplo de Hash NTLMv1
`u4-netntlm::kNS:338d08f8e26de93300000000000000000000000000000000:9526fb8c23a90751cdd619b6cea564742e1e4bf33006ba41:cb8086049ec4736c`

- Este exemplo mostra como o hash NTLMv1 é estruturado, destacando a separação entre os componentes do desafio e da resposta.

### NTLMv2 (Network NTLMv2)

#### Introdução

- **Lançamento**: Introduzido no Windows NT 4.0 SP4, e padrão desde o Windows Server 2000.
- **Segurança Aprimorada**: Mais resistente a ataques de falsificação em comparação com o NTLMv1.

#### Algoritmo de Desafio/Resposta NTLMv2

`SC = 8-byte server challenge, random CC = 8-byte client challenge, random CC* = (X, time, CC2, domain name) v2-Hash = HMAC-MD5(NT-Hash, user name, domain name) LMv2 = HMAC-MD5(v2-Hash, SC, CC) NTv2 = HMAC-MD5(v2-Hash, SC, CC*) response = LMv2 | CC | NTv2 | CC*`

- **Desafios**: O servidor envia um desafio de 8 bytes. O cliente responde com dois desafios: um desafio simples e um desafio com informações adicionais (tempo, domínio, etc.).
- **Respostas**: O cliente envia duas respostas ao desafio do servidor. Essas respostas contêm hashes HMAC-MD5 de 16 bytes.

#### Exemplo de Hash NTLMv2
`admin::N46iSNekpT:08ca45b7d7ea58ee:88dcbe4446168966a153a0064958dac6:5c7830315c7830310000000000000b45c67103d07d7b95acd12ffa11230e0000000052920b85f78d013c31cdb3b92f5d765c783030`

- Mostra a complexidade e os vários componentes que constituem um hash NTLMv2, tornando-o mais robusto.

### Credenciais Armazenadas em Cache de Domínio (MSCache2)

#### Finalidade

- **Uso em Ambientes AD**: Criado para permitir que hosts se autentiquem mesmo sem comunicação com um Controlador de Domínio.
- **Armazenamento**: Os últimos dez hashes de qualquer usuário do domínio que tenha efetuado login com sucesso são armazenados em `HKEY_LOCAL_MACHINE\SECURITY\Cache`.

#### Características

- **Resistência**: Os hashes são muito lentos para quebrar com ferramentas como o Hashcat, exigindo ataques extremamente direcionados ou o uso de senhas fracas.
- **Formato do Hash**:
	`$DCC2$10240#bjones#e4e938d12fe5974dc42a90120bd9c90f`

- **Importância**: Essencial para entender os diversos tipos de hashes em um ambiente AD, seus pontos fortes e fracos, e a eficácia de ataques como pass-the-hash ou cracking.

### Conclusão

- **Compreensão dos Hashes**: Fundamental para testadores de penetração entenderem os diferentes tipos de hashes, como eles podem ser explorados e quando os ataques podem ser fúteis.
- **Segurança**: Importante para identificar e mitigar as vulnerabilidades em um ambiente de rede, garantindo que as credenciais e métodos de autenticação estejam adequadamente protegidos.
