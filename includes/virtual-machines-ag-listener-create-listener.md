<span data-ttu-id="60d27-101">Nesta etapa, você criar manualmente o ouvinte do grupo de disponibilidade Olá no Gerenciador de Cluster de Failover e o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="60d27-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="60d27-102">Abra o Gerenciador de Cluster de Failover de nó de saudação que hospeda a réplica primária hello.</span><span class="sxs-lookup"><span data-stu-id="60d27-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="60d27-103">Selecione Olá **redes** nó e, em seguida, nome de rede de cluster de saudação de observação.</span><span class="sxs-lookup"><span data-stu-id="60d27-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="60d27-104">Esse nome é usado na variável de saudação $ClusterNetworkName em Olá script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60d27-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="60d27-105">Expanda o nome do cluster hello e, em seguida, clique em **funções**.</span><span class="sxs-lookup"><span data-stu-id="60d27-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="60d27-106">Em Olá **funções** painel, o grupo de disponibilidade do botão direito do mouse Olá nome e, em seguida, selecione **adicionar recurso** > **ponto de acesso para cliente**.</span><span class="sxs-lookup"><span data-stu-id="60d27-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Adicionar ponto de acesso para cliente para o grupo de disponibilidade](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="60d27-108">Em Olá **nome** , crie um nome para este novo ouvinte, clique em **próximo** duas vezes e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="60d27-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="60d27-109">Não coloque Olá ouvinte ou recurso online neste momento.</span><span class="sxs-lookup"><span data-stu-id="60d27-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="60d27-110">Clique em Olá **recursos** guia e, em seguida, expanda o ponto de acesso de cliente Olá você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="60d27-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="60d27-111">recurso de endereço IP Olá para cada rede de cluster no cluster é exibido.</span><span class="sxs-lookup"><span data-stu-id="60d27-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="60d27-112">Se essa é uma solução somente no Azure, somente um recurso de endereço IP é exibido.</span><span class="sxs-lookup"><span data-stu-id="60d27-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="60d27-113">Siga um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="60d27-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="60d27-114">tooconfigure uma solução híbrida:</span><span class="sxs-lookup"><span data-stu-id="60d27-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="60d27-115">a.</span><span class="sxs-lookup"><span data-stu-id="60d27-115">a.</span></span> <span data-ttu-id="60d27-116">Recurso de endereço IP de saudação que corresponde a tooyour subrede local e, em seguida, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="60d27-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="60d27-117">Observe o nome do endereço IP hello e o nome de rede.</span><span class="sxs-lookup"><span data-stu-id="60d27-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="60d27-118">b.</span><span class="sxs-lookup"><span data-stu-id="60d27-118">b.</span></span> <span data-ttu-id="60d27-119">Selecione o **Endereço IP estático**, atribua um endereço IP não utilizado e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="60d27-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="60d27-120">tooconfigure uma solução somente no Azure:</span><span class="sxs-lookup"><span data-stu-id="60d27-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="60d27-121">a.</span><span class="sxs-lookup"><span data-stu-id="60d27-121">a.</span></span> <span data-ttu-id="60d27-122">Recurso de endereço IP de saudação que corresponde a tooyour sub-rede do Azure e, em seguida, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="60d27-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="60d27-123">Se mais tarde, o ouvinte de saudação não toocome online devido a um endereço IP conflitante selecionado pelo DHCP, você pode configurar um endereço IP estático válido nessa janela de propriedades.</span><span class="sxs-lookup"><span data-stu-id="60d27-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="60d27-124">b.</span><span class="sxs-lookup"><span data-stu-id="60d27-124">b.</span></span> <span data-ttu-id="60d27-125">Em Olá mesmo **endereço IP** janela Propriedades, alteração Olá **nome do endereço IP**.</span><span class="sxs-lookup"><span data-stu-id="60d27-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="60d27-126">Esse nome é usado na variável Olá $IPResourceName de saudação script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60d27-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="60d27-127">Se sua solução abrange diversas VNets do Azure, repita essa etapa para cada recurso IP.</span><span class="sxs-lookup"><span data-stu-id="60d27-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

