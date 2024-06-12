### Objetos no Active Directory (AD)

No ambiente do Active Directory (AD), um objeto refere-se a qualquer recurso, como unidades organizacionais, usuários, grupos e impressoras. Cada objeto possui atributos associados que o descrevem em detalhes.

#### Usuários

Os usuários são objetos de segurança no AD, cada um com um identificador de segurança (SID) e um identificador exclusivo global (GUID). Eles possuem vários atributos, como nome de exibição, endereço de email e data da última alteração de senha.

#### Contatos

Os contatos são usados para representar usuários externos e contêm informações como nome, sobrenome, endereço de email e número de telefone. Eles não possuem um SID, apenas um GUID.

#### Impressoras

Objetos de impressora apontam para impressoras acessíveis na rede AD. Eles são entidades de segurança e possuem apenas um GUID, com atributos como nome da impressora e informações do driver.

#### Computadores

Objetos de computador são alvos cruciais para invasores, pois o acesso administrativo total a um computador concede direitos semelhantes a uma conta de usuário de domínio padrão. Eles são objetos de segurança com um SID e um GUID.

#### Pastas Compartilhadas

Apontam para pastas compartilhadas em um computador específico e podem ter controles de acesso aplicados a eles para restringir o acesso.

#### Grupos

Os grupos são contêineres de objetos que podem conter usuários, computadores e outros grupos. Eles são objetos de segurança com um SID e um GUID e são usados para gerenciar permissões de usuários e acesso a outros objetos protegidos.

#### Unidades Organizacionais (OUs)

As OUs são contêineres usados para armazenar objetos semelhantes e facilitar a administração. Elas permitem a delegação administrativa de tarefas e podem ter permissões específicas aplicadas a elas.
