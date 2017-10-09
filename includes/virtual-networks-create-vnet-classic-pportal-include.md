## <a name="how-toocreate-a-classic-vnet-in-hello-azure-portal"></a>Como toocreate uma VNet clássico no hello portal do Azure
toocreate uma VNet clássica com base no cenário de saudação acima, siga as etapas de saudação abaixo.

1. Em um navegador, navegue toohttp://portal.azure.com e, se necessário, entre com sua conta do Azure.
2. Clique em **novo** > **rede** > **rede Virtual**, observe que Olá **selecionar um modelo de implantação** lista já mostra **clássico**e, em seguida, clique em **criar**, como mostrado na figura de saudação abaixo.
   
    ![Criar rede virtual no portal do Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. Em Olá **rede Virtual** folha, Olá tipo **nome** de saudação VNet e clique **espaço de endereço**. Defina as configurações de espaço de endereço para hello rede virtual e sua primeira sub-rede, clique **Okey**. Olá figura a seguir mostra as configurações do bloco de CIDR Olá para o nosso cenário.
   
    ![Folha Espaço de endereço](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. Clique em **grupo de recursos** e selecione Olá VNet para um tooadd do grupo de recursos, ou clique em **criar novo grupo de recursos** tooadd Olá VNet tooa novo grupo de recursos. Hello figura abaixo mostra Olá recurso configurações de grupo para um novo grupo de recursos chamado **TestRG**. Para saber mais sobre grupos de recursos, visite [Visão geral do Gerenciador de Recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
   
    ![Folha Criar grupo de recursos](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. Se necessário, altere Olá **assinatura** e **local** configurações para sua rede virtual. 
6. Se não desejar Olá toosee VNet como um bloco em Olá **quadro inicial**, desabilitar **tooStartboard Pin**. 
7. Clique em **criar** e observe Olá bloco nomeado **Virtual criando rede** conforme mostrado na figura abaixo a saudação.
   
    ![Criar rede virtual no portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. Aguarde Olá toobe VNet criado e quando você vir Olá bloco abaixo, clique em tooadd mais sub-redes.
   
    ![Criar rede virtual no portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. Você deve ver Olá **configuração** para sua VNet, conforme mostrado abaixo. 
   
    ![Criar rede virtual no portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. Clique em **Sub-redes** > **Adicionar**. Em seguida, digite um **Nome** e especifique um **Intervalo de endereços (bloco CIDR)** para a sub-rede e clique em **OK**. Olá figura a seguir mostra as configurações de saudação em nosso cenário atual.
    
    ![Criar rede virtual no portal do Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)

