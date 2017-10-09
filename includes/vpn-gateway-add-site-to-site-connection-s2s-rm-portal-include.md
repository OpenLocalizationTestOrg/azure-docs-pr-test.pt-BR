1. Navegue tooand folha de saudação aberta para o gateway de rede virtual. Há toonavigate de várias maneiras. Em nosso exemplo, podemos navegou gateway toohello 'VNet1GW' indo muito**TestVNet1 -> Visão geral -> conectado dispositivos -> VNet1GW**.
2. Na folha de saudação para VNet1GW, clique em **conexões**. Na parte superior de saudação da folha de conexões de saudação, clique em **+ adicionar** tooopen Olá **Adicionar conexão** folha.

    ![Criar uma conexão site a site](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. Em Olá **Adicionar conexão** folha, preencha Olá valores toocreate sua conexão.

  - **Nome:** nomeie sua conexão. Nós usamos **VNet1toSite2** em nosso exemplo.
  - **Tipo de conexão:** selecione **Site a site (IPSec)**.
  - **Gateway de rede virtual:** valor Olá é fixo porque você está se conectando deste gateway.
  - **Gateway de rede local:** clique **escolher um gateway de rede local** e selecione Olá gateway de rede local que você deseja toouse. Em nosso exemplo, nós usamos **Site2**.
  - **Chave compartilhada:** valor Olá aqui deve corresponder o valor de saudação que você está usando para o dispositivo VPN local no local. No exemplo hello, usamos 'abc123', mas você pode (e deve) usar algo mais complexas. Olá importante é esse valor de saudação que você especificar aqui deve ser Olá que mesmo valor que você especificou ao configurar seu dispositivo VPN.
  - Olá valores restante para **assinatura**, **grupo de recursos**, e **local** corrigidos.

4. Clique em **Okey** toocreate sua conexão. Você verá *criar Conexão* flash na tela hello.
5. Você pode exibir conexão Olá no hello **conexões** folha Olá virtual do gateway de rede. Olá Status será alterado de *desconhecido* muito*conectando*e, em seguida, muito*êxito*.
