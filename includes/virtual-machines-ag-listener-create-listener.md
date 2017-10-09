Nesta etapa, você criar manualmente o ouvinte do grupo de disponibilidade Olá no Gerenciador de Cluster de Failover e o SQL Server Management Studio.

1. Abra o Gerenciador de Cluster de Failover de nó de saudação que hospeda a réplica primária hello.

2. Selecione Olá **redes** nó e, em seguida, nome de rede de cluster de saudação de observação. Esse nome é usado na variável de saudação $ClusterNetworkName em Olá script do PowerShell.

3. Expanda o nome do cluster hello e, em seguida, clique em **funções**.

4. Em Olá **funções** painel, o grupo de disponibilidade do botão direito do mouse Olá nome e, em seguida, selecione **adicionar recurso** > **ponto de acesso para cliente**.
   
    ![Adicionar ponto de acesso para cliente para o grupo de disponibilidade](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. Em Olá **nome** , crie um nome para este novo ouvinte, clique em **próximo** duas vezes e, em seguida, clique em **concluir**.  
    Não coloque Olá ouvinte ou recurso online neste momento.

6. Clique em Olá **recursos** guia e, em seguida, expanda o ponto de acesso de cliente Olá você acabou de criar. 
    recurso de endereço IP Olá para cada rede de cluster no cluster é exibido. Se essa é uma solução somente no Azure, somente um recurso de endereço IP é exibido.

7. Siga um destes procedimentos hello:
   
   * tooconfigure uma solução híbrida:
     
        a. Recurso de endereço IP de saudação que corresponde a tooyour subrede local e, em seguida, selecione **propriedades**. Observe o nome do endereço IP hello e o nome de rede.
   
        b. Selecione o **Endereço IP estático**, atribua um endereço IP não utilizado e clique em **OK**.
 
   * tooconfigure uma solução somente no Azure:

        a. Recurso de endereço IP de saudação que corresponde a tooyour sub-rede do Azure e, em seguida, selecione **propriedades**.
       
       > [!NOTE]
       > Se mais tarde, o ouvinte de saudação não toocome online devido a um endereço IP conflitante selecionado pelo DHCP, você pode configurar um endereço IP estático válido nessa janela de propriedades.
       > 
       > 

       b. Em Olá mesmo **endereço IP** janela Propriedades, alteração Olá **nome do endereço IP**.  
        Esse nome é usado na variável Olá $IPResourceName de saudação script do PowerShell. Se sua solução abrange diversas VNets do Azure, repita essa etapa para cada recurso IP.

