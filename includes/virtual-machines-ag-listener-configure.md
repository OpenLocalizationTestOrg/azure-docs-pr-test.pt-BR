ouvinte do grupo de disponibilidade de saudação é um nome de rede e o endereço IP que Olá ouve o grupo de disponibilidade do SQL Server. ouvinte de grupo de disponibilidade do toocreate hello, Olá a seguir:

1. <a name="getnet"></a>Obter nome Olá Olá rede do recurso de cluster.

    a. Use RDP tooconnect toohello máquina virtual do Azure que hospeda a réplica primária hello. 

    b. Abra o Gerenciador de Cluster de Failover.

    c. Selecione Olá **redes** nó e o nome de rede de cluster de saudação de observação. Use o nome da saudação `$ClusterNetworkName` variável Olá script do PowerShell. Olá nome de rede de cluster de saudação de imagem a seguir é **rede de Cluster 1**:

   ![Nome da rede de clusters](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Adicione ponto de acesso para cliente hello.  
    ponto de acesso para cliente Olá é o nome de rede de saudação que os aplicativos usem tooconnect toohello os bancos de dados em um grupo de disponibilidade. Crie ponto de acesso para cliente Olá no Gerenciador de Cluster de Failover.

    a. Expanda o nome do cluster hello e, em seguida, clique em **funções**.

    b. Em Olá **funções** painel, o grupo de disponibilidade do botão direito do mouse Olá nome e, em seguida, selecione **adicionar recurso** > **ponto de acesso para cliente**.

   ![Ponto de acesso para cliente](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. Em Olá **nome** caixa, crie um nome para este novo ouvinte. 
   Olá nome novo ouvinte de saudação é o nome de rede de saudação que os aplicativos usem tooconnect toodatabases no grupo de disponibilidade do SQL Server hello.
   
    d. toofinish criando Olá ouvinte, clique em **próximo** duas vezes e, em seguida, clique em **concluir**. Não coloque Olá ouvinte ou recurso online neste momento.

3. <a name="congroup"></a>Configure o recurso IP Olá Olá grupo de disponibilidade.

    a. Clique em Olá **recursos** guia e em seguida, expanda o ponto de acesso de cliente Olá criado por você.  
    ponto de acesso para cliente Hello está offline.

   ![Ponto de acesso para cliente](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Clique o recurso IP hello e, em seguida, clique em Propriedades. Observe o nome de saudação do endereço IP de saudação e usá-lo em Olá `$IPResourceName` variável Olá script do PowerShell.

    c. Em **Endereço IP**, clique em **Endereço IP Estático**. Definir o endereço IP de saudação como hello mesmo endereço que você usou ao definir o endereço do balanceador de carga de saudação em Olá portal do Azure.

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Torne o recurso de grupo de disponibilidade do SQL Server Olá dependente no ponto de acesso de cliente hello.

    a. No Gerenciador de Cluster de Failover, clique em **Funções** e em seu grupo de disponibilidade.

    b. Em Olá **recursos** guia em **outros recursos**, clique o grupo de recursos de disponibilidade hello e, em seguida, clique em **propriedades**. 

    c. Na guia de dependências de hello, adicione o nome de saudação do recurso de ponto (ouvinte Olá) de acesso de cliente hello.

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. Clique em **OK**.

5. <a name="listname"></a>Verifique o acesso para cliente Olá recursos dependentes no endereço IP de saudação do ponto.

    a. No Gerenciador de Cluster de Failover, clique em **Funções** e em seu grupo de disponibilidade. 

    b. Em Olá **recursos** guia, clique no recurso de ponto de acesso de cliente de saudação em **nome do servidor**e, em seguida, clique em **propriedades**. 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Clique em Olá **dependências** guia. Verifique se o endereço IP de saudação é uma dependência. Se não estiver, defina uma dependência no endereço IP hello. Se houver vários recursos listados, verifique se os endereços IP hello tem ou não e dependências. Clique em **OK**. 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Clique no nome do ouvinte Olá e clique **colocar Online**. 

    >[!TIP]
    >Você pode validar que Olá as dependências estão corretamente configuradas. No Gerenciador de Cluster de Failover, vá tooRoles, grupo de disponibilidade hello, clique **mais ações**e, em seguida, clique em **Mostrar relatório de dependências**. Quando dependências Olá estão configuradas corretamente, o grupo de disponibilidade Olá é dependente de nome de rede hello e nome de rede de saudação é dependente de endereço IP de saudação. 


6. <a name="setparam"></a>Definir parâmetros de cluster de saudação do PowerShell.
    
    a. Saudação de cópia tooone de script do PowerShell de suas instâncias do SQL Server a seguir. Atualize as variáveis de saudação para seu ambiente.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Definir parâmetros de cluster de saudação executando Olá script do PowerShell em um de nós de cluster de saudação.  

    > [!NOTE]
    > Se suas instâncias do SQL Server estiverem em regiões separadas, você precisa de script do PowerShell Olá toorun duas vezes. Olá primeira vez, use Olá `$ILBIP` e `$ProbePort` da região de saudação primeiro. Olá pela segunda vez, use Olá `$ILBIP` e `$ProbePort` da região segundo hello. nome de rede de cluster Hello e nome de recurso de IP de cluster Olá são Olá mesmo. 
