# Direitos e privilégios do Active Directory
No contexto do gerenciamento de AD, é crucial distinguir entre "direitos" e "privilégios". Embora esses termos sejam frequentemente usados de forma intercambiável, eles possuem significados distintos que impactam a segurança e a administração do sistema.

**whoami /priv** comando do Windows pode nos mostrar todos os direitos de usuário atribuídos ao usuário atual.

- **Direitos** são permissões atribuídas a usuários ou grupos que definem o acesso a objetos específicos, como arquivos ou pastas. Por exemplo, um direito pode permitir que um usuário leia ou modifique um arquivo.
- **Privilégios** são permissões que concedem a um usuário a capacidade de realizar ações específicas no sistema, como executar programas, desligar o sistema ou redefinir senhas. Privilégios são atribuídos por meio de grupos integrados ou personalizados.

### Atribuição de Direitos de Usuário no Windows

A atribuição de direitos de usuário pode ter um grande impacto na segurança do sistema. Dependendo dos direitos concedidos, um usuário pode ter a capacidade de realizar ações que vão desde fazer login remotamente até manipular processos críticos do sistema. Alguns exemplos de privilégios perigosos incluem:

- **SeRemoteInteractiveLogonRight:** Permite que um usuário faça login remotamente via RDP, o que pode levar à obtenção de dados confidenciais ou ao aumento de privilégios.
- **SeBackupPrivilege:** Concede ao usuário a capacidade de fazer backups do sistema, o que pode ser usado para acessar arquivos confidenciais e até mesmo recuperar senhas.
- **SeDebugPrivilege:** Permite que um usuário depure e ajuste a memória de um processo, facilitando a obtenção de credenciais armazenadas na memória.
- **SeImpersonatePrivilege:** Permite representar um token de uma conta privilegiada, possibilitando o aumento de privilégios em um sistema.
- **SeLoadDriverPrivilege:** Permite carregar e descarregar drivers de dispositivos, o que pode ser usado para aumentar privilégios ou comprometer um sistema.
- **SeTakeOwnershipPrivilege:** Permite que um processo assuma a propriedade de um objeto, o que pode conceder acesso a recursos normalmente inacessíveis.

É crucial entender o impacto de conceder privilégios inadequados a uma conta, pois um pequeno erro administrativo pode levar ao comprometimento completo do sistema ou da empresa.

### Grupos Integrados no Active Directory

O AD possui vários grupos de segurança integrados, cada um com direitos e privilégios específicos. A participação nesses grupos deve ser gerenciada com rigor para evitar abusos, seja por invasores ou por erros administrativos. Abaixo estão alguns dos grupos mais comuns e suas descrições:

#### Descrição dos Grupos Integrados

1. **Account Operators**: Podem criar e modificar a maioria dos tipos de contas, exceto as contas administrativas principais. Podem fazer login localmente em controladores de domínio.
2. **Administrators**: Têm acesso total a um computador ou a um domínio inteiro. Devem ser geridos com extrema cautela. Grupo interno concederá ao usuário acesso total e irrestrito a um computador
3. **Backup Operators**: Podem fazer backup e restaurar todos os arquivos de um computador, ignorando permissões. Podem fazer login localmente em controladores de domínio.
4. **DnsAdmins**: Acesso a informações de DNS da rede.
5. **Domain Admins**: Acesso total para administrar o domínio, incluindo membros locais em todas as máquinas do domínio.
6. **Enterprise Admins**: Acesso completo à configuração do domínio, com capacidade de fazer alterações em toda a floresta AD.
7. **Server Operators**: Podem modificar serviços, acessar compartilhamentos SMB e fazer backup de arquivos em controladores de domínio.

### Visualizando Privilégios de um Usuário

Para visualizar os privilégios de um usuário no Windows, pode-se utilizar o comando `whoami /priv`. Abaixo está um exemplo dos privilégios padrão de um usuário de domínio:

**PRIVILEGES INFORMATION**

| Privilege Name                | Description                    | State    |
| ----------------------------- | ------------------------------ | -------- |
| SeChangeNotifyPrivilege       | Bypass traverse checking       | Enabled  |
| SeIncreaseWorkingSetPrivilege | Increase a process working set | Disabled |

Usuários administrativos, quando logados em uma sessão elevada, têm acesso a uma gama mais ampla de privilégios:
`PS C:\htb> whoami /priv  

| Privilege Name                            | Description                                                        | State    |
| -----------------------------------------| ------------------------------------------------------------------ | -------- |
| SeIncreaseQuotaPrivilege                  | Adjust memory quotas for a process                                 | Disabled |
| SeMachineAccountPrivilege                 | Add workstations to domain                                         | Disabled |
| SeSecurityPrivilege                       | Manage auditing and security log                                   | Disabled |
| SeTakeOwnershipPrivilege                  | Take ownership of files or other objects                           | Disabled |
| SeLoadDriverPrivilege                     | Load and unload device drivers                                     | Disabled |
| SeSystemProfilePrivilege                  | Profile system performance                                         | Disabled |
| SeSystemtimePrivilege                     | Change the system time                                             | Disabled |
| SeProfileSingleProcessPrivilege           | Profile single process                                             | Disabled |
| SeIncreaseBasePriorityPrivilege           | Increase scheduling priority                                       | Disabled |
| SeCreatePagefilePrivilege                 | Create a pagefile                                                  | Disabled |
| SeBackupPrivilege                         | Back up files and directories                                      | Disabled |
| SeRestorePrivilege                        | Restore files and directories                                      | Disabled |
| SeShutdownPrivilege                       | Shut down the system                                               | Disabled |
| SeDebugPrivilege                          | Debug programs                                                     | Enabled  |
| SeSystemEnvironmentPrivilege              | Modify firmware environment values                                 | Disabled |
| SeChangeNotifyPrivilege                   | Bypass traverse checking                                           | Enabled  |
| SeRemoteShutdownPrivilege                 | Force shutdown from a remote system                                | Disabled |
| SeUndockPrivilege                         | Remove computer from docking station                               | Disabled |
| SeEnableDelegationPrivilege               | Enable computer and user accounts to be trusted for delegation     | Disabled |
| SeManageVolumePrivilege                   | Perform volume maintenance tasks                                   | Disabled |
| SeImpersonatePrivilege                    | Impersonate a client after authentication                          | Enabled  |
| SeCreateGlobalPrivilege                   | Create global objects                                              | Enabled  |
| SeIncreaseWorkingSetPrivilege             | Increase a process working set                                     | Disabled |
| SeTimeZonePrivilege                       | Change the time zone                                               | Disabled |
| SeCreateSymbolicLinkPrivilege             | Create symbolic links                                              | Disabled |
| SeDelegateSessionUserImpersonatePrivilege | Obtain an impersonation token for another user in the same session | Disabled |


### Considerações de Segurança no AD

- **Gerenciamento de Grupos**: Manter a adesão a grupos integrados estritamente controlada e monitorada. Idealmente, grupos poderosos devem permanecer vazios a menos que necessário.
- **Segurança de Privilégios**: Atribuir privilégios apenas quando absolutamente necessário e monitorar o uso desses privilégios.
- **Separação de Funções**: Garantir que contas administrativas e de usuário sejam separadas para minimizar riscos.
- **Monitoramento Contínuo**: Utilizar ferramentas e políticas de monitoramento para detectar e responder rapidamente a atividades suspeitas ou não autorizadas.

Com uma gestão cuidadosa dos direitos e privilégios no AD, é possível minimizar riscos e manter a segurança do ambiente de TI.
