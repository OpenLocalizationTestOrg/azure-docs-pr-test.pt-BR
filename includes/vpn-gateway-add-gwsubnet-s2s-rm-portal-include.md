1. No portal, navegue até a rede virtual para a qual você deseja criar um gateway de rede virtual.
2. Na seção **Configurações** da página VNet, clique em **Sub-redes** para expandir a página Sub-redes.
3. Na página **Sub-redes**, clique em **+Sub-rede de gateway** no topo para abrir a página **Adicionar sub-rede**.

  ![Adicionar a sub-rede de gateway](./media/vpn-gateway-add-gwsubnet-s2s-rm-portal-include/addgwsub.png "Adicionar a sub-rede de gateway")
4. O **Nome** da sua sub-rede será automaticamente preenchido com o valor 'GatewaySubnet'. O valor GatewaySubnet é necessário para que o Azure reconheça a sub-rede como a sub-rede do gateway. Ajuste os valores preenchidos automaticamente de **Intervalo de endereços** para corresponder aos seus requisitos de configuração.

  ![Adição da sub-rede de gateway](./media/vpn-gateway-add-gwsubnet-s2s-rm-portal-include/addsub2.png "Adição da sub-rede de gateway")
5. Para criar a sub-rede, clique em **OK** na parte inferior da página.