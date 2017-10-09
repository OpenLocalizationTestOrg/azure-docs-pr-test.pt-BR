### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="3032b-101">Criar um novo servidor SQL lógico no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3032b-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="3032b-102">Clique em **Novo**, pesquise **servidor lógico** e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3032b-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![pesquisar servidor lógico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="3032b-104">Selecione **SQL server (servidor lógico)**</span><span class="sxs-lookup"><span data-stu-id="3032b-104">Select **SQL server (logical server)**</span></span> 

    ![selecionar servidor lógico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="3032b-106">Clique em **criar** tooopen Olá nova do SQL Server (servidor lógico) folha.</span><span class="sxs-lookup"><span data-stu-id="3032b-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="3032b-107"><kbd>![abrir a folha de servidor lógico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![folha de servidor lógico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="3032b-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="3032b-108">Na caixa de texto Nome do servidor da folha do SQL Server (servidor lógico) hello, forneça um nome válido para o novo servidor lógico de saudação.</span><span class="sxs-lookup"><span data-stu-id="3032b-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="3032b-109">Uma marca de seleção verde indica que você forneceu um nome válido.</span><span class="sxs-lookup"><span data-stu-id="3032b-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![novo nome do servidor](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="3032b-111">Olá nome totalmente qualificado para o novo servidor será < your_server_name >. t.</span><span class="sxs-lookup"><span data-stu-id="3032b-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="3032b-112">Na caixa de texto do logon de administrador de servidor hello, forneça um nome de usuário para logon de autenticação de SQL Olá para este servidor.</span><span class="sxs-lookup"><span data-stu-id="3032b-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="3032b-113">Esse logon é conhecido como logon principal do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="3032b-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="3032b-114">Uma marca de seleção verde indica que você forneceu um nome válido.</span><span class="sxs-lookup"><span data-stu-id="3032b-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![Logon de administrador do SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="3032b-116">Em Olá **senha** e **Confirmar senha** caixas de texto, forneça uma senha para a conta de logon principal do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="3032b-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="3032b-117">Uma marca de seleção verde indica que você forneceu uma senha válida.</span><span class="sxs-lookup"><span data-stu-id="3032b-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![Senha de administrador do SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="3032b-119">Selecione uma assinatura em que você tenha objetos toocreate de permissão.</span><span class="sxs-lookup"><span data-stu-id="3032b-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![subscription](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="3032b-121">Na caixa de texto de grupo de recursos de saudação, selecione **criar novo** e, em seguida, na caixa de texto de grupo de recursos hello, forneça um nome válido para Olá novo grupo de recursos (você também pode usar um grupo de recursos existente se você já tiver criado um).</span><span class="sxs-lookup"><span data-stu-id="3032b-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="3032b-122">Uma marca de seleção verde indica que você forneceu um nome válido.</span><span class="sxs-lookup"><span data-stu-id="3032b-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![novo grupo de recursos](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="3032b-124">Em Olá **local** caixa de texto, selecione um data center local apropriado tooyour - como "Leste da Austrália".</span><span class="sxs-lookup"><span data-stu-id="3032b-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![local do servidor](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="3032b-126">Olá a caixa de seleção **permitir servidor de tooaccess de serviços do azure** não pode ser alterado nesta folha.</span><span class="sxs-lookup"><span data-stu-id="3032b-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="3032b-127">Você pode alterar essa configuração na folha de firewall de servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="3032b-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="3032b-128">Para obter mais informações, confira [Introdução à segurança](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3032b-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="3032b-129">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3032b-129">Click **Create**.</span></span>

    ![botão criar](./media/sql-data-warehouse-create-logical-server/create.png)

