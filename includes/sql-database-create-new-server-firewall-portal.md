
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, the following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="61c6c-101">Criar uma regra de firewall de nível de servidor no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="61c6c-101">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="61c6c-102">Na folha do SQL server, em Configurações, clique em **Firewall** para abrir a folha de Firewall para o SQL server.</span><span class="sxs-lookup"><span data-stu-id="61c6c-102">On the SQL server blade, under Settings, click **Firewall** to open the Firewall blade for the SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="61c6c-103">Examine o endereço IP do cliente exibido e confirme se esse é o endereço IP na Internet usando um navegador de sua escolha (perguntar "o que é meu endereço IP).</span><span class="sxs-lookup"><span data-stu-id="61c6c-103">Review the client IP address displayed and validate that this is your IP address on the Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="61c6c-104">Ocasionalmente, eles não coincidem por vários motivos.</span><span class="sxs-lookup"><span data-stu-id="61c6c-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="61c6c-105">Supondo que os endereços IP têm correspondência, clique em **Adicionar IP do cliente** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="61c6c-105">Assuming that the IP addresses match, click **Add client IP** on the toolbar.</span></span>

    ![adicionar IP do cliente](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="61c6c-107">Você pode abrir o firewall do Banco de dados SQL no servidor para um único endereço IP ou um intervalo inteiro de endereços.</span><span class="sxs-lookup"><span data-stu-id="61c6c-107">You can open the SQL Database firewall on the server to a single IP address or an entire range of addresses.</span></span> <span data-ttu-id="61c6c-108">Abrir o firewall permite que os administradores do SQL e os usuários façam logon em qualquer banco de dados no servidor ao qual eles têm credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="61c6c-108">Opening the firewall enables SQL administrators and users to login to any database on the server to which they have valid credentials.</span></span>
    >

4. <span data-ttu-id="61c6c-109">Clique em **Salvar** na barra de ferramentas para salvar essa regra de firewall de nível de servidor e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="61c6c-109">Click **Save** on the toolbar to save this server-level firewall rule and then click **OK**.</span></span>

    ![adicionar IP do cliente](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="61c6c-111">Para obter um tutorial, confira [Tutorial do banco de dados SQL: criar um servidor, uma regra de firewall de nível de servidor, um banco de dados de exemplo, uma regra de firewall de nível de banco de dados e conectar-se com o SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="61c6c-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
