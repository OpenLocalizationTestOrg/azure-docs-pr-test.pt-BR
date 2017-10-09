
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Criar uma regra de firewall de nível de servidor no hello portal do Azure

1. Na folha de servidor SQL hello, em configurações, clique em **Firewall** tooopen folha de Firewall Olá para o SQL server de saudação.

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. Examine o endereço IP do cliente Olá exibido e confirme se esse é o endereço IP na Internet usando um navegador de sua escolha de saudação (perguntar "qual é o endereço IP). Ocasionalmente, eles não coincidem por vários motivos.

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. Supondo que os endereços IP hello corresponderem, clique em **Adicionar IP do cliente** na barra de ferramentas de saudação.

    ![adicionar IP do cliente](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > Você pode abrir o firewall do banco de dados SQL Olá em Olá tooa único endereço IP de servidor ou todo um intervalo de endereços. Abertura Olá firewall permite os administradores do SQL e os usuários toologin tooany banco de dados Olá toowhich servidor tiverem credenciais válidas.
    >

4. Clique em **salvar** em Olá barra de ferramentas toosave essa regra de firewall de nível de servidor e, em seguida, clique em **Okey**.

    ![adicionar IP do cliente](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> Para obter um tutorial, confira [Tutorial do banco de dados SQL: criar um servidor, uma regra de firewall de nível de servidor, um banco de dados de exemplo, uma regra de firewall de nível de banco de dados e conectar-se com o SQL Server](../articles/sql-database/sql-database-get-started.md).    
>
