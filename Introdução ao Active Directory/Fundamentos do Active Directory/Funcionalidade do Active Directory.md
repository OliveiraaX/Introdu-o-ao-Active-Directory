## Funções de Operação Mestre Única Flexível (FSMO)

As funções FSMO no Active Directory (AD) incluem:

| Funções          | Descrição                                                                                                                                 |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Schema Master    | Gerencia a cópia de leitura/gravação do esquema do AD, que define todos os atributos que podem ser aplicados a um objeto no AD.         |
| Domain Naming Master | Gerencia nomes de domínio e garante que dois domínios com o mesmo nome não sejam criados na mesma floresta.                            |
| Relative ID (RID) Master | Atribui blocos de RIDs a outros DCs dentro do domínio, ajudando a garantir que vários objetos não recebam o mesmo SID.               |
| PDC Emulator     | Controla autenticação, alterações de senha, gerenciamento de objetos de política de grupo (GPOs) e mantém a hora dentro do domínio.     |
| Infrastructure Master | Traduz GUIDs, SIDs e DNs entre domínios em organizações com vários domínios em uma única floresta.                                      |

## Níveis Funcionais de Domínio e Floresta

Os níveis funcionais determinam os recursos e capacidades disponíveis no AD DS. Veja uma comparação entre o Windows 2000 nativo e o Windows Server 2016:

| Nível funcional de domínio | Recursos disponíveis                                                                                                              |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Nativo do Windows 2000      | Grupos universais, aninhamento de grupos, histórico de SID.                                                                       |
| Servidor Windows 2003       | Ferramenta Netdom.exe, atributo lastLogonTimestamp, autenticação seletiva.                                                       |
| Servidor Windows 2008       | Suporte para DFS, AES para Kerberos, políticas de senha refinadas.                                                                |
| Servidor Windows 2008 R2    | Garantia de autenticação, contas de serviço gerenciadas.                                                                          |
| Servidor Windows 2012       | Suporte KDC para declarações, autenticação composta.                                                                              |
| Servidor Windows 2012 R2    | Proteções extras para membros do grupo Usuários Protegidos, Silos de Política de Autenticação.                                     |
| Servidor Windows 2016       | Necessidade de cartão inteligente para logon interativo, novos recursos do Kerberos, proteção de credenciais adicionais.          |

## Confianças

As relações de confiança estabelecem a autenticação entre domínios. Existem vários tipos de confiança, como parent-child, external e forest trust. Essas relações podem ser transitivas ou não transitivas e unidirecionais ou bidirecionais.
