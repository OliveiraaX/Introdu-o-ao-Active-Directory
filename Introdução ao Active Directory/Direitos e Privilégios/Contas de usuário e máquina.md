# User and Machine Accounts
As contas de usuário são criadas tanto em sistemas locais quanto em Active Directory (AD) para permitir que indivíduos ou programas façam login em um computador e acessem recursos de acordo com seus direitos. Quando um usuário faz login, o sistema verifica sua senha e cria um **token de acesso**. Este token descreve o contexto de segurança de um processo ou thread e inclui a identidade de segurança do usuário e sua associação a grupos. O token é apresentado sempre que o usuário interage com um processo, permitindo acesso controlado a recursos.

#### Grupos e Privilégios

- **Grupos de Usuários**: Usuários podem ser atribuídos a grupos, que podem conter um ou mais membros. Grupos são usados para controlar o acesso a recursos.
- **Facilidade de Administração**: Administradores atribuem privilégios a grupos ao invés de individualmente a cada usuário, simplificando a administração e facilitando a concessão e revogação de direitos.

### Contas de Usuário no Active Directory

O AD permite a provisão e gestão de contas de usuário, normalmente com pelo menos uma conta AD por usuário. Algumas organizações podem ter usuários com múltiplas contas, como administradores de TI ou membros do Help Desk. Além das contas de usuário e administrador padrão, também há contas de serviço para execução de aplicativos ou serviços específicos.

#### Quantidade de Contas

- **Contas Ativas**: Uma organização com 1.000 funcionários pode ter 1.200 contas de usuário ativas ou mais.
- **Contas Desativadas**: Organizações frequentemente mantêm contas desativadas de ex-funcionários para fins de auditoria, armazenadas em Unidades Organizacionais (UOs) específicas como "FORMER EMPLOYEES".

#### Permissões e Segurança

- **Variedade de Direitos**: Contas de usuário podem ter desde permissões de leitura básica até controle total como "Enterprise Admin".
- **Riscos e Erros**: Configurações incorretas podem conceder direitos não intencionais, oferecendo uma superfície de ataque significativa para invasores.

### Contas Locais

As contas locais são armazenadas em um servidor ou estação de trabalho específico e só possuem direitos naquele host. Existem várias contas padrão em um sistema Windows:

1. **Administrator**: esta conta possui o SID `S-1-5-domain-500`e é a primeira conta criada com uma nova instalação do Windows, com controle total sobre quase todos os recursos do sistema.
2. **Guest**: Desabilitada por padrão, permite login temporário com direitos limitados.
3. **SYSTEM**: Conta usada pelo sistema operacional para funções internas, com permissões sobre quase tudo no host.
4. **Network Service**: Conta usada para executar serviços do Windows com credenciais apresentadas aos serviços remotos.
5. **Local Service**: Conta usada para executar serviços do Windows com privilégios mínimos no computador e credenciais anônimas na rede.

### Usuários de Domínio

Os usuários de domínio recebem direitos para acessar recursos como servidores de arquivos, impressoras, e outros objetos no domínio. Diferentemente dos usuários locais, eles podem fazer login em qualquer host do domínio.

#### Tipos de Contas no AD

- **UserPrincipalName (UPN)**: Nome de logon principal do usuário, geralmente o endereço de email.
- **ObjectGUID**: Identificador único do usuário e permanecerá assim mesmo se a conta for excluída.
- **SAMAccountName**: Nome de logon compatível com versões anteriores de Windows.
- **objectSID**: Identificador de segurança (SID) do usuário.
- **sIDHistory**: Contém SIDs anteriores para o usuário, usado em migrações de domínio.

#### Contas de Máquina e Permissões

- **Máquinas Ingressadas no Domínio**: Facilita o compartilhamento de informações e gerenciamento centralizado via Política de Grupo.
- **Máquinas Não Ingressadas no Domínio**: Adequado para uso doméstico ou pequenas empresas, com gerenciamento individual das alterações do host.

### Considerações de Segurança

Entender os diferentes tipos de contas e suas permissões é crucial para proteger um ambiente AD. Configurações incorretas podem ser exploradas por invasores, e a segurança deve ser reforçada com políticas adequadas e defesa em profundidade para mitigar os riscos associados às contas de usuário.

### Resumo

- **Contas de Usuário**: Facilita login e acesso a recursos.
- **Grupos e Privilégios**: Simplifica administração e gerenciamento de direitos.
- **Active Directory**: Provisão e gestão centralizada de contas de usuário.
- **Contas Locais**: Direitos e gerenciamento limitados ao host específico.
- **Usuários de Domínio**: Acesso amplo a recursos do domínio.
- **Segurança**: Crucial para proteger contra configurações incorretas e ataques.

#### Atributos comuns do usuário

  Contas de usuário e máquina

```powershell-session
PS C:\htb Get-ADUser -Identity artgh-student

DistinguishedName : CN=htb student,CN=Users,DC=exemplo,DC=LOCAL
Enabled           : True
GivenName         : artgh
Name              : artgh student
ObjectClass       : user
ObjectGUID        : aa799587-c641-4c23-a2f7-75850b4dd7e3
SamAccountName    : artgh-student
SID               : S-1-5-21-3842939050-3880317879-2865463114-1111
Surname           : student
UserPrincipalName : artgh-student@exemplo.LOCAL
```
