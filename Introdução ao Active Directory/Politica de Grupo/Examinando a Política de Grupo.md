# Examinando a Política de Grupo
1. **O que é a Política de Grupo**: A Política de Grupo é uma ferramenta poderosa para gerenciar configurações em ambientes Windows, permitindo aos administradores definir políticas para usuários e computadores.
    
2. **Objetos de Política de Grupo (GPOs)**: São coleções virtuais de configurações de política que podem ser aplicadas a usuários ou computadores. Cada GPO tem um nome exclusivo e um identificador único.
    
3. **Exemplos de configurações de GPO**: Isso inclui estabelecer políticas de senha, restringir dispositivos de mídia removíveis, aplicar protetores de tela com senha, restringir acesso a aplicativos, entre outros.
    
4. **Hierarquia e Precedência de GPOs**: As configurações de GPOs são processadas de acordo com uma hierarquia específica, com GPOs de nível mais alto tendo precedência sobre os de nível inferior. O "Default Domain Policy" tem a precedência mais alta. Objeto de política de grupo é criado quando o domínio é criado.
    
5. **Atualização de Política de Grupo**: As configurações de GPO são atualizadas periodicamente pelos clientes do Windows, geralmente a cada 90 minutos (com um intervalo aleatório de +/- 30 minutos). Isso pode ser alterado, se necessário.
    
6. **Considerações de Segurança**: Os GPOs podem ser usados para realizar ataques se um usuário mal-intencionado ganhar acesso para modificá-los. Isso pode levar a movimentos laterais, escalonamento de privilégios e comprometimento do domínio.
