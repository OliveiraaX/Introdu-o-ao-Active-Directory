# Funções FSMO no Active Directory

O Active Directory do Windows Server possui funções mestre única flexíveis (FSMO). Essas funções são essenciais para a operação e gerenciamento do domínio. Elas incluem:

| Função                | Descrição                                                                                                      |
|-----------------------|----------------------------------------------------------------------------------------------------------------|
| `Schema Master`       | Gerencia a cópia de leitura/gravação do esquema do AD, que define todos os atributos aplicáveis a um objeto.   |
| `Domain Naming Master`| Gerencia nomes de domínio e evita a criação de domínios com o mesmo nome na mesma floresta.                   |
| `RID Master`          | Atribui blocos de RIDs a outros DCs dentro do domínio, garantindo a exclusividade dos SIDs dos objetos.        |
| `PDC Emulator`        | Controlador de domínio autoritativo para autenticação, alterações de senha e gerenciamento de GPOs.            |
| `Infrastructure Master`| Traduz GUIDs, SIDs e DNs entre domínios em uma floresta multi-domínio.                                         |

Problemas com funções FSMO podem levar a dificuldades de autenticação e autorização dentro de um domínio.

## Níveis Funcionais de Domínio e Floresta

A Microsoft introduziu níveis funcionais para determinar os recursos disponíveis nos Serviços de Domínio Active Directory (AD DS). Abaixo está uma comparação entre os níveis funcionais do Windows 2000 nativo e o Windows Server 2016:

| Nível funcional de domínio | Recursos disponíveis | Sistemas operacionais suportados |
|-----------------------------|----------------------|----------------------------------|
| Nativo do Windows 2000      | Grupos universais, histórico de SID, etc. | Windows Server 2008 R2, Windows Server 2008, Windows Server 2003, Windows 2000 |
| Servidor Windows 2016       | Recursos de proteção de credenciais, Kerberos aprimorado, etc. | Servidor Windows 2019, Servidor Windows 2016 |

Não houve adição de novo nível funcional com o Windows Server 2019.

## Confianças

As relações de confiança no Active Directory permitem a autenticação e o acesso a recursos entre diferentes domínios. Existem vários tipos de confiança, como parent-child, cross-link, external, tree-root e forest. As relações de confiança podem ser transitivas ou não transitivas, e bidirecionais ou unidirecionais.

### Exemplo de confiança

As relações de confiança são fundamentais para a interoperabilidade entre domínios e florestas no Active Directory.

# Kerberos

O **Kerberos** é o protocolo de autenticação padrão no Active Directory. Ele é usado para autenticar usuários e serviços em um ambiente de domínio. O Kerberos é um protocolo baseado em tickets que evita a transmissão de senhas pela rede.

## Processo de autenticação Kerberos

1. O usuário solicita um ticket de autenticação (TGT) ao KDC.
2. O KDC valida as credenciais do usuário e emite um TGT.
3. O usuário solicita um ticket de serviço (TGS) para acessar um recurso específico.
4. O KDC emite um TGS criptografado com a chave do serviço.
5. O usuário apresenta o TGS ao serviço para acessar o recurso.

O **Kerberos** usa a **porta 88** (TCP e UDP).

# DNS

O **DNS** é fundamental para o funcionamento do Active Directory. Ele é usado para resolver nomes de host em endereços IP e vice-versa. O DNS dinâmico é usado para atualizar automaticamente o banco de dados DNS conforme os endereços IP dos sistemas são alterados.

## Exemplo de pesquisa de DNS
O DNS usa a porta TCP e UDP 53.

```bash
nslookup Local.LOCAL
```
#LDAP
O LDAP é usado para pesquisas de diretório no Active Directory. Ele fornece um método de comunicação entre aplicativos e servidores que hospedam serviços de diretório. O LDAP usa a porta 389 e o LDAPS usa a porta 636 para comunicação segura.

#MSRPC
O MSRPC é a implementação da Chamada de Procedimento Remoto (RPC) da Microsoft. Ele é usado para acessar sistemas no Active Directory por meio de quatro interfaces RPC principais: lsarpc, netlogon, samr e drsuapi.






