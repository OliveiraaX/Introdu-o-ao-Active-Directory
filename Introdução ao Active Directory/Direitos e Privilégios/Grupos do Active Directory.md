# Active Directory Groups
Os grupos no Active Directory (AD) são essenciais para a administração de permissões e gerenciamento de recursos. Eles facilitam a concessão e a revogação de acesso de maneira eficiente, reduzindo a complexidade administrativa e aumentando a segurança quando configurados corretamente.

### Tipos de Grupos

**1. Grupos de Segurança:**

- **Propósito:** Usados para atribuir permissões a recursos em uma rede AD (melhor utilizado para atribuir permissões e direitos aos usuários).
- **Função:** Facilitar a gestão de permissões para recursos como arquivos, pastas, impressoras, etc.
- **Benefícios:** Simplificam a atribuição de permissões e podem ser usados em conjunto com listas de controle de acesso (ACLs) para controlar o acesso a recursos.

**2. Grupos de Distribuição:**

- **Propósito:** Usados principalmente para distribuir e-mails para uma coleção de usuários.
- **Função:** Atuar como listas de distribuição em aplicativos de e-mail, como Microsoft Exchange.
- **Limitação:** Não podem ser usados para atribuir permissões de segurança a recursos.

### Escopos de Grupo

**1. Grupo Local de Domínio:**

- **Uso:** Atribuir permissões para recursos no domínio onde o grupo foi criado.
- **Características:** Pode conter usuários de outros domínios, mas não pode ser usado em outros domínios.

**2. Grupo Global:**

- **Uso:** Gerenciar permissões em qualquer domínio da floresta AD.
- **Características:** Só pode conter usuários do mesmo domínio onde foi criado, mas pode ser usado em outros domínios.

**3. Grupo Universal:**

- **Uso:** Gerenciar permissões em qualquer domínio dentro da floresta AD.
- **Características:** Pode conter usuários de qualquer domínio e a associação a esses grupos é replicada pelo Catálogo Global.
- Pode ser convertido em um grupo de domínio local.

### Diferença entre Grupos e Unidades Organizacionais (OUs)

**Unidades Organizacionais (OUs):**

- **Propósito:** Agrupar usuários, grupos e computadores para facilitar a administração.
- **Uso:** Delegar tarefas administrativas e aplicar Políticas de Grupo (GPOs).
- **Características:** Não são usadas para atribuir permissões diretamente a recursos.

**Grupos:**

- **Propósito:** Atribuir permissões a recursos.
- **Uso:** Gerenciar o acesso a recursos como arquivos, pastas e impressoras.
- **Características:** Podem ser usados em conjunto com ACLs para definir permissões de segurança.

### Grupos Integrados vs. Grupos Personalizados

**Grupos Integrados:**

- **Descrição:** Grupos criados automaticamente pelo AD durante a configuração inicial do domínio.
- **Uso:** Facilitar a administração e segurança do domínio.
- **Exemplos:** Domain Admins, Administrators, Users, Guests, etc.

**Grupos Personalizados:**

- **Descrição:** Grupos criados por administradores para atender necessidades específicas da organização.
- **Uso:** Adaptar a estrutura de permissões às necessidades específicas de acesso e segurança da organização.

### Associação de Grupo Aninhado

A associação de grupo aninhado permite que um grupo seja membro de outro grupo, permitindo que usuários herdem permissões de grupos pai. Isso pode simplificar a administração, mas também pode levar a atribuições de permissões não intencionais e excessivas.

**Exemplo:** Um grupo "Helpdesk Level 1" pode ser membro do grupo "Help Desk", que por sua vez pode ter permissões para realizar certas tarefas administrativas. Um usuário que é membro do "Helpdesk Level 1" herda as permissões do "Help Desk".

### Ferramentas de Auditoria e Segurança

**Ferramentas como BloodHound:**

- **Uso:** Analisar e visualizar a relação entre grupos, usuários e permissões no AD.
- **Benefício:** Identificar possíveis configurações incorretas e caminhos de ataque que podem ser explorados por invasores.

### Atributos Importantes do Grupo

- **cn (Common-Name):** Nome do grupo nos Serviços de Domínio Active Directory.
- **member:** Objetos de usuário, grupo e contato que são membros do grupo.
- **groupType:** Número inteiro que especifica o tipo e o escopo do grupo.
- **memberOf:** Listagem de grupos dos quais o grupo é membro (associação de grupo aninhado).
- **objectSid:** Identificador de segurança (SID) do grupo, usado para identificar o grupo como uma entidade de segurança.

### Conclusão

Os grupos são ferramentas poderosas no AD para gerenciar permissões e acessos, mas requerem configuração cuidadosa para evitar atribuições de permissões excessivas ou não intencionais. Compreender os diferentes tipos de grupos, seus escopos e como aninhá-los corretamente é essencial para uma administração eficaz e segura do AD. Auditorias regulares e o uso de ferramentas como BloodHound ajudam a manter a segurança e a integridade da estrutura de permissões no AD.
