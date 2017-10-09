
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="d2b1b-101">Criar uma regra de firewall de nível de servidor no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2b1b-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="d2b1b-102">Na folha de servidor SQL hello, em configurações, clique em **Firewall** tooopen folha de Firewall Olá para o SQL server de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2b1b-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="d2b1b-103">Examine o endereço IP do cliente Olá exibido e confirme se esse é o endereço IP na Internet usando um navegador de sua escolha de saudação (perguntar "qual é o endereço IP).</span><span class="sxs-lookup"><span data-stu-id="d2b1b-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="d2b1b-104">Ocasionalmente, eles não coincidem por vários motivos.</span><span class="sxs-lookup"><span data-stu-id="d2b1b-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="d2b1b-105">Supondo que os endereços IP hello corresponderem, clique em **Adicionar IP do cliente** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2b1b-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![adicionar IP do cliente](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="d2b1b-107">Você pode abrir o firewall do banco de dados SQL Olá em Olá tooa único endereço IP de servidor ou todo um intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="d2b1b-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="d2b1b-108">Abertura Olá firewall permite os administradores do SQL e os usuários toologin tooany banco de dados Olá toowhich servidor tiverem credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="d2b1b-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="d2b1b-109">Clique em **salvar** em Olá barra de ferramentas toosave essa regra de firewall de nível de servidor e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d2b1b-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![adicionar IP do cliente](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="d2b1b-111">Para obter um tutorial, confira [Tutorial do banco de dados SQL: criar um servidor, uma regra de firewall de nível de servidor, um banco de dados de exemplo, uma regra de firewall de nível de banco de dados e conectar-se com o SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2b1b-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
