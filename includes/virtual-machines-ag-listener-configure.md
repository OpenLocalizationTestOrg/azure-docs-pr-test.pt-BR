<span data-ttu-id="3e865-101">ouvinte do grupo de disponibilidade de saudação é um nome de rede e o endereço IP que Olá ouve o grupo de disponibilidade do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3e865-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="3e865-102">ouvinte de grupo de disponibilidade do toocreate hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e865-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="3e865-103"><a name="getnet"></a>Obter nome Olá Olá rede do recurso de cluster.</span><span class="sxs-lookup"><span data-stu-id="3e865-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="3e865-104">a.</span><span class="sxs-lookup"><span data-stu-id="3e865-104">a.</span></span> <span data-ttu-id="3e865-105">Use RDP tooconnect toohello máquina virtual do Azure que hospeda a réplica primária hello.</span><span class="sxs-lookup"><span data-stu-id="3e865-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="3e865-106">b.</span><span class="sxs-lookup"><span data-stu-id="3e865-106">b.</span></span> <span data-ttu-id="3e865-107">Abra o Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="3e865-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="3e865-108">c.</span><span class="sxs-lookup"><span data-stu-id="3e865-108">c.</span></span> <span data-ttu-id="3e865-109">Selecione Olá **redes** nó e o nome de rede de cluster de saudação de observação.</span><span class="sxs-lookup"><span data-stu-id="3e865-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="3e865-110">Use o nome da saudação `$ClusterNetworkName` variável Olá script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e865-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="3e865-111">Olá nome de rede de cluster de saudação de imagem a seguir é **rede de Cluster 1**:</span><span class="sxs-lookup"><span data-stu-id="3e865-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![Nome da rede de clusters](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="3e865-113"><a name="addcap"></a>Adicione ponto de acesso para cliente hello.</span><span class="sxs-lookup"><span data-stu-id="3e865-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="3e865-114">ponto de acesso para cliente Olá é o nome de rede de saudação que os aplicativos usem tooconnect toohello os bancos de dados em um grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3e865-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="3e865-115">Crie ponto de acesso para cliente Olá no Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="3e865-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="3e865-116">a.</span><span class="sxs-lookup"><span data-stu-id="3e865-116">a.</span></span> <span data-ttu-id="3e865-117">Expanda o nome do cluster hello e, em seguida, clique em **funções**.</span><span class="sxs-lookup"><span data-stu-id="3e865-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="3e865-118">b.</span><span class="sxs-lookup"><span data-stu-id="3e865-118">b.</span></span> <span data-ttu-id="3e865-119">Em Olá **funções** painel, o grupo de disponibilidade do botão direito do mouse Olá nome e, em seguida, selecione **adicionar recurso** > **ponto de acesso para cliente**.</span><span class="sxs-lookup"><span data-stu-id="3e865-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Ponto de acesso para cliente](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="3e865-121">c.</span><span class="sxs-lookup"><span data-stu-id="3e865-121">c.</span></span> <span data-ttu-id="3e865-122">Em Olá **nome** caixa, crie um nome para este novo ouvinte.</span><span class="sxs-lookup"><span data-stu-id="3e865-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="3e865-123">Olá nome novo ouvinte de saudação é o nome de rede de saudação que os aplicativos usem tooconnect toodatabases no grupo de disponibilidade do SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="3e865-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="3e865-124">d.</span><span class="sxs-lookup"><span data-stu-id="3e865-124">d.</span></span> <span data-ttu-id="3e865-125">toofinish criando Olá ouvinte, clique em **próximo** duas vezes e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="3e865-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="3e865-126">Não coloque Olá ouvinte ou recurso online neste momento.</span><span class="sxs-lookup"><span data-stu-id="3e865-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="3e865-127"><a name="congroup"></a>Configure o recurso IP Olá Olá grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3e865-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="3e865-128">a.</span><span class="sxs-lookup"><span data-stu-id="3e865-128">a.</span></span> <span data-ttu-id="3e865-129">Clique em Olá **recursos** guia e em seguida, expanda o ponto de acesso de cliente Olá criado por você.</span><span class="sxs-lookup"><span data-stu-id="3e865-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="3e865-130">ponto de acesso para cliente Hello está offline.</span><span class="sxs-lookup"><span data-stu-id="3e865-130">hello client access point is offline.</span></span>

   ![Ponto de acesso para cliente](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="3e865-132">b.</span><span class="sxs-lookup"><span data-stu-id="3e865-132">b.</span></span> <span data-ttu-id="3e865-133">Clique o recurso IP hello e, em seguida, clique em Propriedades.</span><span class="sxs-lookup"><span data-stu-id="3e865-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="3e865-134">Observe o nome de saudação do endereço IP de saudação e usá-lo em Olá `$IPResourceName` variável Olá script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e865-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="3e865-135">c.</span><span class="sxs-lookup"><span data-stu-id="3e865-135">c.</span></span> <span data-ttu-id="3e865-136">Em **Endereço IP**, clique em **Endereço IP Estático**.</span><span class="sxs-lookup"><span data-stu-id="3e865-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="3e865-137">Definir o endereço IP de saudação como hello mesmo endereço que você usou ao definir o endereço do balanceador de carga de saudação em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e865-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="3e865-139"><a name = "dependencyGroup"></a>Torne o recurso de grupo de disponibilidade do SQL Server Olá dependente no ponto de acesso de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="3e865-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="3e865-140">a.</span><span class="sxs-lookup"><span data-stu-id="3e865-140">a.</span></span> <span data-ttu-id="3e865-141">No Gerenciador de Cluster de Failover, clique em **Funções** e em seu grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3e865-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="3e865-142">b.</span><span class="sxs-lookup"><span data-stu-id="3e865-142">b.</span></span> <span data-ttu-id="3e865-143">Em Olá **recursos** guia em **outros recursos**, clique o grupo de recursos de disponibilidade hello e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="3e865-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="3e865-144">c.</span><span class="sxs-lookup"><span data-stu-id="3e865-144">c.</span></span> <span data-ttu-id="3e865-145">Na guia de dependências de hello, adicione o nome de saudação do recurso de ponto (ouvinte Olá) de acesso de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="3e865-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="3e865-147">d.</span><span class="sxs-lookup"><span data-stu-id="3e865-147">d.</span></span> <span data-ttu-id="3e865-148">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e865-148">Click **OK**.</span></span>

5. <span data-ttu-id="3e865-149"><a name="listname"></a>Verifique o acesso para cliente Olá recursos dependentes no endereço IP de saudação do ponto.</span><span class="sxs-lookup"><span data-stu-id="3e865-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="3e865-150">a.</span><span class="sxs-lookup"><span data-stu-id="3e865-150">a.</span></span> <span data-ttu-id="3e865-151">No Gerenciador de Cluster de Failover, clique em **Funções** e em seu grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3e865-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="3e865-152">b.</span><span class="sxs-lookup"><span data-stu-id="3e865-152">b.</span></span> <span data-ttu-id="3e865-153">Em Olá **recursos** guia, clique no recurso de ponto de acesso de cliente de saudação em **nome do servidor**e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="3e865-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="3e865-155">c.</span><span class="sxs-lookup"><span data-stu-id="3e865-155">c.</span></span> <span data-ttu-id="3e865-156">Clique em Olá **dependências** guia. Verifique se o endereço IP de saudação é uma dependência.</span><span class="sxs-lookup"><span data-stu-id="3e865-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="3e865-157">Se não estiver, defina uma dependência no endereço IP hello.</span><span class="sxs-lookup"><span data-stu-id="3e865-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="3e865-158">Se houver vários recursos listados, verifique se os endereços IP hello tem ou não e dependências.</span><span class="sxs-lookup"><span data-stu-id="3e865-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="3e865-159">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e865-159">Click **OK**.</span></span> 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="3e865-161">d.</span><span class="sxs-lookup"><span data-stu-id="3e865-161">d.</span></span> <span data-ttu-id="3e865-162">Clique no nome do ouvinte Olá e clique **colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="3e865-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="3e865-163">Você pode validar que Olá as dependências estão corretamente configuradas.</span><span class="sxs-lookup"><span data-stu-id="3e865-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="3e865-164">No Gerenciador de Cluster de Failover, vá tooRoles, grupo de disponibilidade hello, clique **mais ações**e, em seguida, clique em **Mostrar relatório de dependências**.</span><span class="sxs-lookup"><span data-stu-id="3e865-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="3e865-165">Quando dependências Olá estão configuradas corretamente, o grupo de disponibilidade Olá é dependente de nome de rede hello e nome de rede de saudação é dependente de endereço IP de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e865-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="3e865-166"><a name="setparam"></a>Definir parâmetros de cluster de saudação do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e865-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="3e865-167">a.</span><span class="sxs-lookup"><span data-stu-id="3e865-167">a.</span></span> <span data-ttu-id="3e865-168">Saudação de cópia tooone de script do PowerShell de suas instâncias do SQL Server a seguir.</span><span class="sxs-lookup"><span data-stu-id="3e865-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="3e865-169">Atualize as variáveis de saudação para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="3e865-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="3e865-170">b.</span><span class="sxs-lookup"><span data-stu-id="3e865-170">b.</span></span> <span data-ttu-id="3e865-171">Definir parâmetros de cluster de saudação executando Olá script do PowerShell em um de nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e865-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="3e865-172">Se suas instâncias do SQL Server estiverem em regiões separadas, você precisa de script do PowerShell Olá toorun duas vezes.</span><span class="sxs-lookup"><span data-stu-id="3e865-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="3e865-173">Olá primeira vez, use Olá `$ILBIP` e `$ProbePort` da região de saudação primeiro.</span><span class="sxs-lookup"><span data-stu-id="3e865-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="3e865-174">Olá pela segunda vez, use Olá `$ILBIP` e `$ProbePort` da região segundo hello.</span><span class="sxs-lookup"><span data-stu-id="3e865-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="3e865-175">nome de rede de cluster Hello e nome de recurso de IP de cluster Olá são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="3e865-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
