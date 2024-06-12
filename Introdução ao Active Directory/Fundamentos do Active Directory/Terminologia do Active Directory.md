**Objeto** — Em um ambiente do Active Directory, um objeto refere-se a qualquer recurso que pode ser representado e gerenciado pelo AD. Isso inclui usuários, grupos, computadores, impressoras, pastas compartilhadas e muito mais.

**Atributos** — Todo objeto em um ambiente do Active Directory possui atributos, que são propriedades que descrevem o objeto. Por exemplo, um usuário pode ter atributos como nome, endereço de email, senha, grupo de pertença, etc.

**Schema** - O schema define a estrutura dos objetos que podem existir em um ambiente do Active Directory e os atributos associados a esses objetos. É como um plano mestre que especifica os tipos de objetos que podem ser armazenados no AD e quais informações eles podem conter.

**Domínio** — Em termos de Active Directory, um domínio é uma unidade lógica de organização para objetos, como usuários, grupos e computadores. Os domínios operam de forma independente uns dos outros e geralmente são vinculados por relações de confiança.

**Floresta** — Uma floresta é uma coleção de um ou mais domínios que compartilham um namespace comum, políticas e relações de confiança. Ela permite a centralização e a administração unificada de múltiplos domínios em uma única estrutura.

**Árvore** — No contexto do Active Directory, uma árvore é uma hierarquia de domínios relacionados em que cada domínio é conectado a um domínio pai.

**Container** – Em um ambiente do Active Directory, um container é um tipo de objeto que pode armazenar outros objetos. Por exemplo, as unidades organizacionais (OUs) são containers que podem conter usuários, grupos e outros objetos.

**Folha** — Uma folha é um domínio sem subdomínios na hierarquia do Active Directory. Geralmente, é o último nível de uma árvore de domínio.

**GUID (Identificador Único Global)** — É um valor exclusivo de 128 bits atribuído a cada objeto no Active Directory quando é criado. É usado para identificar exclusivamente o objeto em toda a floresta.

**Princípios de segurança** — São objetos de segurança em um ambiente do Active Directory que controlam o acesso a recursos, como arquivos, pastas e impressoras.

**SID (Identificador de Segurança)** — É um identificador exclusivo usado para representar uma entidade de segurança no Windows, como um usuário, grupo ou processo.

**DN (Nome Distinto)** — É uma forma de nomear um objeto no Active Directory que descreve seu caminho completo na hierarquia do diretório.

**sAMAccountName** — É o nome de logon de um usuário em um domínio do Active Directory.

**userPrincipleName** — É outra forma de identificar usuários no Active Directory, no formato "nome@domínio".

**Funções FSMO (Funções Flexíveis de Operador Mestre Único)** — São funções no Active Directory que são atribuídas a um único controlador de domínio e são responsáveis por operações críticas de gerenciamento de domínio.

**GC (Catálogo Global)** — É um controlador de domínio no Active Directory que armazena cópias de todos os objetos em uma floresta e permite pesquisas globais em toda a floresta.

**RODC (Controlador de Domínio Somente Leitura)** — É um tipo de controlador de domínio no Active Directory que não permite alterações no diretório e é especialmente projetado para implantações em locais remotos ou de baixa segurança.

**SPN (Nome Principal de Serviço)** — É um identificador único para uma instância de serviço usado pela autenticação Kerberos.

**Objetos de Política de Grupo (GPO)** — São coleções de configurações de políticas que podem ser aplicadas a usuários e computadores em um ambiente do Active Directory.

**ACLs (Listas de Controle de Acesso)** — São coleções ordenadas de entradas que determinam permissões de acesso a objetos em um ambiente do Active Directory.

**ACEs (Entradas de Controle de Acesso)** — Identifica um administrador e especifica os direitos de acesso a um objeto.

**FQDN (Nome de Domínio Totalmente Qualificado)** — É o nome completo de um computador ou host, incluindo o nome do domínio.

**Tombstone** — É um objeto contêiner no Active Directory que contém objetos excluídos temporariamente.

**SYSVOL** — É uma pasta compartilhada no Active Directory que armazena arquivos públicos, como políticas de sistema e scripts de logon.

**dsHeuristics** — É um atributo usado para definir configurações em toda a floresta do Active Directory.

**NTDS.DIT** ​​— É o banco de dados do Active Directory que armazena dados do AD, incluindo informações sobre usuários e grupos.

**Lápide** — É um objeto contêiner no Active Directory que contém objetos excluídos temporariamente antes da exclusão permanente.
