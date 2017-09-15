### <a name="create-a-new-logical-sql-server-in-the-azure-portal"></a><span data-ttu-id="20196-101">Criar um novo servidor lógico do SQL no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="20196-101">Create a new logical SQL server in the Azure portal</span></span>

1. <span data-ttu-id="20196-102">Clique em **Novo**, pesquise **servidor lógico** e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="20196-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![pesquisar servidor lógico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="20196-104">Selecione **SQL server (servidor lógico)**</span><span class="sxs-lookup"><span data-stu-id="20196-104">Select **SQL server (logical server)**</span></span> 

    ![selecionar servidor lógico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="20196-106">Clique em **Criar** para abrir a nova folha do SQL Server (servidor lógico).</span><span class="sxs-lookup"><span data-stu-id="20196-106">Click **Create** to open the new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="20196-107"><kbd>![abrir a folha de servidor lógico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![folha de servidor lógico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="20196-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="20196-108">Na caixa de texto do nome do servidor da folha SQL Server (servidor lógico), forneça um nome válido para o novo servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="20196-108">In the SQL Server (logical server) blade's server name text box, provide a valid name for the new logical server.</span></span> <span data-ttu-id="20196-109">Uma marca de seleção verde indica que você forneceu um nome válido.</span><span class="sxs-lookup"><span data-stu-id="20196-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![novo nome do servidor](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="20196-111">O nome totalmente qualificado para o novo servidor será <nome_do_servidor>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="20196-111">The fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="20196-112">Na caixa de texto de logon do administrador de servidor, forneça um nome de usuário para o logon de autenticação do SQL para este servidor.</span><span class="sxs-lookup"><span data-stu-id="20196-112">In the Server admin login text box, provide a user name for the SQL authentication login for this server.</span></span> <span data-ttu-id="20196-113">Esse logon é conhecido como o logon principal do servidor.</span><span class="sxs-lookup"><span data-stu-id="20196-113">This login is known as the server principal login.</span></span> <span data-ttu-id="20196-114">Uma marca de seleção verde indica que você forneceu um nome válido.</span><span class="sxs-lookup"><span data-stu-id="20196-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![Logon de administrador do SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="20196-116">Nas caixas de texto **Senha** e **Confirmar senha**, forneça uma senha para a conta de logon da entidade de segurança.</span><span class="sxs-lookup"><span data-stu-id="20196-116">In the **Password** and **Confirm password** text boxes, provide a password for the server principal login account.</span></span> <span data-ttu-id="20196-117">Uma marca de seleção verde indica que você forneceu uma senha válida.</span><span class="sxs-lookup"><span data-stu-id="20196-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![Senha de administrador do SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="20196-119">Selecione uma assinatura em que você tenha permissão para criar objetos.</span><span class="sxs-lookup"><span data-stu-id="20196-119">Select a subscription in which you have permission to create objects.</span></span>

    ![subscription](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="20196-121">Na caixa de texto Grupo de recursos, selecione **Criar novo** e, na caixa de texto grupo de recursos, forneça um nome válido para o novo grupo de recursos (você também pode usar um grupo de recursos existente, caso já tenha criado um).</span><span class="sxs-lookup"><span data-stu-id="20196-121">In the Resource group text box, select **Create new** and then, in the resource group text box, provide a valid name for the new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="20196-122">Uma marca de seleção verde indica que você forneceu um nome válido.</span><span class="sxs-lookup"><span data-stu-id="20196-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![novo grupo de recursos](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="20196-124">Na caixa de texto **Local**, selecione um data center apropriado para seu local, como "Leste da Austrália".</span><span class="sxs-lookup"><span data-stu-id="20196-124">In the **Location** text box, select a data center appropriate to your location - such as "Australia East".</span></span>
    
    ![local do servidor](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="20196-126">A caixa de seleção para **Permitir que os serviços do Azure acessem o servidor** não pode ser alterado nessa folha.</span><span class="sxs-lookup"><span data-stu-id="20196-126">The checkbox for **Allow azure services to access server** cannot be changed on this blade.</span></span> <span data-ttu-id="20196-127">Você pode alterar essa configuração na folha de firewall do servidor.</span><span class="sxs-lookup"><span data-stu-id="20196-127">You can change this setting on the server firewall blade.</span></span> <span data-ttu-id="20196-128">Para obter mais informações, confira [Introdução à segurança](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="20196-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="20196-129">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="20196-129">Click **Create**.</span></span>

    ![botão criar](./media/sql-data-warehouse-create-logical-server/create.png)

