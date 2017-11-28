<span data-ttu-id="b2a20-101">O ouvinte do grupo de disponibilidade é um nome de rede e endereço IP que o grupo de disponibilidade do SQL Server escuta.</span><span class="sxs-lookup"><span data-stu-id="b2a20-101">The availability group listener is an IP address and network name that the SQL Server availability group listens on.</span></span> <span data-ttu-id="b2a20-102">Para criar o ouvinte do grupo de disponibilidade, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b2a20-102">To create the availability group listener, do the following:</span></span>

1. <span data-ttu-id="b2a20-103"><a name="getnet"></a>Obtenha o nome do recurso de rede de cluster.</span><span class="sxs-lookup"><span data-stu-id="b2a20-103"><a name="getnet"></a>Get the name of the cluster network resource.</span></span>

    <span data-ttu-id="b2a20-104">a.</span><span class="sxs-lookup"><span data-stu-id="b2a20-104">a.</span></span> <span data-ttu-id="b2a20-105">Use o RDP para se conectar à máquina virtual do Azure que hospeda a réplica primária.</span><span class="sxs-lookup"><span data-stu-id="b2a20-105">Use RDP to connect to the Azure virtual machine that hosts the primary replica.</span></span> 

    <span data-ttu-id="b2a20-106">b.</span><span class="sxs-lookup"><span data-stu-id="b2a20-106">b.</span></span> <span data-ttu-id="b2a20-107">Abra o Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="b2a20-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="b2a20-108">c.</span><span class="sxs-lookup"><span data-stu-id="b2a20-108">c.</span></span> <span data-ttu-id="b2a20-109">Selecione o nó **Redes** e observe o nome da rede do cluster.</span><span class="sxs-lookup"><span data-stu-id="b2a20-109">Select the **Networks** node, and note the cluster network name.</span></span> <span data-ttu-id="b2a20-110">Use esse nome na variável `$ClusterNetworkName` no script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2a20-110">Use this name in the `$ClusterNetworkName` variable in the PowerShell script.</span></span> <span data-ttu-id="b2a20-111">Na imagem a seguir, o nome da rede de clusters é **Rede de Cluster 1**:</span><span class="sxs-lookup"><span data-stu-id="b2a20-111">In the following image the cluster network name is **Cluster Network 1**:</span></span>

   ![Nome da rede de clusters](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="b2a20-113"><a name="addcap"></a>Adicionar o ponto de acesso para cliente.</span><span class="sxs-lookup"><span data-stu-id="b2a20-113"><a name="addcap"></a>Add the client access point.</span></span>  
    <span data-ttu-id="b2a20-114">O ponto de acesso do cliente é o nome da rede que os aplicativos usam para se conectar aos bancos de dados em um grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b2a20-114">The client access point is the network name that applications use to connect to the databases in an availability group.</span></span> <span data-ttu-id="b2a20-115">Crie o ponto de acesso de cliente no Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="b2a20-115">Create the client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="b2a20-116">a.</span><span class="sxs-lookup"><span data-stu-id="b2a20-116">a.</span></span> <span data-ttu-id="b2a20-117">Expanda o nome do cluster e, em seguida, clique em **Funções**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-117">Expand the cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="b2a20-118">b.</span><span class="sxs-lookup"><span data-stu-id="b2a20-118">b.</span></span> <span data-ttu-id="b2a20-119">No painel **Funções**, clique com o botão direito do mouse no nome do grupo de disponibilidade e, em seguida, selecione **Adicionar recurso** > **Ponto de acesso para o cliente**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-119">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Ponto de acesso para cliente](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="b2a20-121">c.</span><span class="sxs-lookup"><span data-stu-id="b2a20-121">c.</span></span> <span data-ttu-id="b2a20-122">Na caixa **Nome**, crie um nome para o novo ouvinte.</span><span class="sxs-lookup"><span data-stu-id="b2a20-122">In the **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="b2a20-123">O nome para o novo ouvinte é o nome da rede que o aplicativo usará para se conectar aos bancos de dados no grupo de disponibilidade do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b2a20-123">The name for the new listener is the network name that applications use to connect to databases in the SQL Server availability group.</span></span>
   
    <span data-ttu-id="b2a20-124">d.</span><span class="sxs-lookup"><span data-stu-id="b2a20-124">d.</span></span> <span data-ttu-id="b2a20-125">Para concluir a criação do ouvinte, clique em **Avançar** duas vezes e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-125">To finish creating the listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="b2a20-126">Não coloque o ouvinte ou o recurso online neste momento.</span><span class="sxs-lookup"><span data-stu-id="b2a20-126">Do not bring the listener or resource online at this point.</span></span>

3. <span data-ttu-id="b2a20-127"><a name="congroup"></a>Configurar o recurso de IP do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b2a20-127"><a name="congroup"></a>Configure the IP resource for the availability group.</span></span>

    <span data-ttu-id="b2a20-128">a.</span><span class="sxs-lookup"><span data-stu-id="b2a20-128">a.</span></span> <span data-ttu-id="b2a20-129">Clique na guia **Recursos**e expanda o ponto de acesso para cliente que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="b2a20-129">Click the **Resources** tab, and then expand the client access point you created.</span></span>  
    <span data-ttu-id="b2a20-130">O ponto de acesso para cliente está offline.</span><span class="sxs-lookup"><span data-stu-id="b2a20-130">The client access point is offline.</span></span>

   ![Ponto de acesso para cliente](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="b2a20-132">b.</span><span class="sxs-lookup"><span data-stu-id="b2a20-132">b.</span></span> <span data-ttu-id="b2a20-133">Clique com o botão direito do mouse no recurso de IP e clique em Propriedades.</span><span class="sxs-lookup"><span data-stu-id="b2a20-133">Right-click the IP resource, and then click properties.</span></span> <span data-ttu-id="b2a20-134">Anote o nome do endereço IP e use-o na variável `$IPResourceName` no script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2a20-134">Note the name of the IP address, and use it in the `$IPResourceName` variable in the PowerShell script.</span></span>

    <span data-ttu-id="b2a20-135">c.</span><span class="sxs-lookup"><span data-stu-id="b2a20-135">c.</span></span> <span data-ttu-id="b2a20-136">Em **Endereço IP**, clique em **Endereço IP Estático**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="b2a20-137">Defina o endereço IP como o mesmo endereço que você usou quando definiu o endereço do balanceador de carga no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2a20-137">Set the IP address as the same address that you used when you set the load balancer address on the Azure portal.</span></span>

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="b2a20-139"><a name = "dependencyGroup"></a>Torne o recurso de grupo de disponibilidade do SQL Server dependente do ponto de acesso para cliente.</span><span class="sxs-lookup"><span data-stu-id="b2a20-139"><a name = "dependencyGroup"></a>Make the SQL Server availability group resource dependent on the client access point.</span></span>

    <span data-ttu-id="b2a20-140">a.</span><span class="sxs-lookup"><span data-stu-id="b2a20-140">a.</span></span> <span data-ttu-id="b2a20-141">No Gerenciador de Cluster de Failover, clique em **Funções** e em seu grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b2a20-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="b2a20-142">b.</span><span class="sxs-lookup"><span data-stu-id="b2a20-142">b.</span></span> <span data-ttu-id="b2a20-143">Na guia **Recursos** em **Outros Recursos**, com o botão direito do mouse no grupo de recursos de disponibilidade e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-143">On the **Resources** tab, under **Other Resources**, right-click the availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="b2a20-144">c.</span><span class="sxs-lookup"><span data-stu-id="b2a20-144">c.</span></span> <span data-ttu-id="b2a20-145">Na guia dependências, adicione o nome do recurso de ponto de acesso ao cliente (o ouvinte).</span><span class="sxs-lookup"><span data-stu-id="b2a20-145">On the dependencies tab, add the name of the client access point (the listener) resource.</span></span>

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="b2a20-147">d.</span><span class="sxs-lookup"><span data-stu-id="b2a20-147">d.</span></span> <span data-ttu-id="b2a20-148">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-148">Click **OK**.</span></span>

5. <span data-ttu-id="b2a20-149"><a name="listname"></a>Torne o recurso de ponto de acesso de cliente dependente do endereço IP.</span><span class="sxs-lookup"><span data-stu-id="b2a20-149"><a name="listname"></a>Make the client access point resource dependent on the IP address.</span></span>

    <span data-ttu-id="b2a20-150">a.</span><span class="sxs-lookup"><span data-stu-id="b2a20-150">a.</span></span> <span data-ttu-id="b2a20-151">No Gerenciador de Cluster de Failover, clique em **Funções** e em seu grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b2a20-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="b2a20-152">b.</span><span class="sxs-lookup"><span data-stu-id="b2a20-152">b.</span></span> <span data-ttu-id="b2a20-153">Na guia **Recursos**, clique com o botão direito do mouse no recurso do ponto de acesso no **Nome do Servidor** e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-153">On the **Resources** tab, right-click the client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="b2a20-155">c.</span><span class="sxs-lookup"><span data-stu-id="b2a20-155">c.</span></span> <span data-ttu-id="b2a20-156">Selecione a guia **Dependências** .</span><span class="sxs-lookup"><span data-stu-id="b2a20-156">Click the **Dependencies** tab.</span></span> <span data-ttu-id="b2a20-157">Verifique se o endereço IP é uma dependência.</span><span class="sxs-lookup"><span data-stu-id="b2a20-157">Verify that the IP address is a dependency.</span></span> <span data-ttu-id="b2a20-158">Se não for, defina uma dependência no endereço IP.</span><span class="sxs-lookup"><span data-stu-id="b2a20-158">If it is not, set a dependency on the IP address.</span></span> <span data-ttu-id="b2a20-159">Se houver vários recursos listados, verifique se os endereços IP têm dependências OR, e não AND.</span><span class="sxs-lookup"><span data-stu-id="b2a20-159">If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="b2a20-160">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-160">Click **OK**.</span></span> 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="b2a20-162">d.</span><span class="sxs-lookup"><span data-stu-id="b2a20-162">d.</span></span> <span data-ttu-id="b2a20-163">Clique com o botão direito do mouse no nome do ouvinte e, em seguida, clique em **Colocar online**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-163">Right-click the listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="b2a20-164">Você pode validar se as dependências estão configuradas corretamente.</span><span class="sxs-lookup"><span data-stu-id="b2a20-164">You can validate that the dependencies are correctly configured.</span></span> <span data-ttu-id="b2a20-165">No Gerenciador de Cluster de Failover, vá para funções, clique no grupo de disponibilidade, clique em **Mais Ações**e clique em **Mostrar Relatório de Dependências**.</span><span class="sxs-lookup"><span data-stu-id="b2a20-165">In Failover Cluster Manager, go to Roles, right-click the availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="b2a20-166">Quando as dependências são configuradas corretamente, o grupo de disponibilidade é dependente do nome da rede e o nome da rede depende do endereço IP.</span><span class="sxs-lookup"><span data-stu-id="b2a20-166">When the dependencies are correctly configured, the availability group is dependent on the network name, and the network name is dependent on the IP address.</span></span> 


6. <span data-ttu-id="b2a20-167"><a name="setparam"></a>Definir os parâmetros do cluster no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2a20-167"><a name="setparam"></a>Set the cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="b2a20-168">a.</span><span class="sxs-lookup"><span data-stu-id="b2a20-168">a.</span></span> <span data-ttu-id="b2a20-169">Copie o script do PowerShell a seguir em uma de suas instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b2a20-169">Copy the following PowerShell script to one of your SQL Server instances.</span></span> <span data-ttu-id="b2a20-170">Atualize as variáveis para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="b2a20-170">Update the variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
    $IPResourceName = "<IPResourceName>" # the IP Address resource name
    $ILBIP = “<n.n.n.n>” # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="b2a20-171">b.</span><span class="sxs-lookup"><span data-stu-id="b2a20-171">b.</span></span> <span data-ttu-id="b2a20-172">Defina os parâmetros de cluster executando o script do PowerShell em um dos nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="b2a20-172">Set the cluster parameters by running the PowerShell script on one of the cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="b2a20-173">Se suas instâncias do SQL Server estiverem em regiões separadas, você precisará executar o script do PowerShell duas vezes.</span><span class="sxs-lookup"><span data-stu-id="b2a20-173">If your SQL Server instances are in separate regions, you need to run the PowerShell script twice.</span></span> <span data-ttu-id="b2a20-174">Na primeira vez, use o `$ILBIP` e `$ProbePort` da primeira região.</span><span class="sxs-lookup"><span data-stu-id="b2a20-174">The first time, use the `$ILBIP` and `$ProbePort` from the first region.</span></span> <span data-ttu-id="b2a20-175">Na segunda vez, use o `$ILBIP` e `$ProbePort` da segunda região.</span><span class="sxs-lookup"><span data-stu-id="b2a20-175">The second time, use the `$ILBIP` and `$ProbePort` from the second region.</span></span> <span data-ttu-id="b2a20-176">O nome da rede de cluster e o nome do recurso de IP do cluster são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="b2a20-176">The cluster network name and the cluster IP resource name are the same.</span></span> 
