1. No portal de saudação do **todos os recursos**, clique em **+ adicionar**. 
2. Em Olá **tudo** caixa de pesquisa de folha, digite **gateway de rede Local**, em seguida, clique em toosearch. Isso retornará uma lista. Clique em **gateway de rede Local** tooopen Olá folha, clique em **criar** tooopen Olá **criar gateway de rede local** folha.

  ![criar gateway de rede local](./media/vpn-gateway-add-lng-s2s-rm-portal-include/createlng.png)

3. Em Olá **criar folha de gateway de rede local**, especifique valores de saudação do seu gateway de rede local.

  - **Nome:** especifique um nome para seu objeto de gateway de rede local.
  - **Endereço IP:** este é o endereço IP público de saudação do dispositivo VPN Olá que você deseja tooconnect do Azure para. Especifique um endereço IP público válido. endereço IP de saudação não pode estar atrás de NAT e tem toobe acessível pelo Azure. Se você não tem endereço IP hello agora, você pode usar valores hello mostrados na captura de tela hello, mas você precisa fazer toogo e substitua o seu endereço IP de espaço reservado com o endereço IP público de saudação do seu dispositivo VPN. Caso contrário, o Azure não será capaz de tooconnect.
  - **Espaço de endereço** refere-se toohello intervalos de endereços de rede Olá que representa esta rede local. Você pode adicionar vários intervalos de espaço de endereço. Certifique-se de que os intervalos de saudação especificado aqui não se sobreponham com intervalos de outras redes que você deseja tooconnect para. Azure roteará o intervalo de endereços de saudação que você especifique o endereço IP do dispositivo VPN de local do toohello. *Usar seus próprios valores aqui, não Olá valores mostrados na captura de tela de saudação*.
  - **Assinatura:** verificar que Olá correto de assinatura está mostrando.
  - **Grupo de recursos:** grupo de recursos de saudação selecione que você deseja toouse. Você pode criar um novo grupo de recursos ou selecionar um que você já criou.
  - **Local:** selecione Olá local que esse objeto será criado no. Talvez você queira tooselect Olá sua rede virtual reside no mesmo local, mas não é necessário toodo assim.

4. Quando tiver terminado de especificar os valores hello, clique em **criar** na parte inferior de Olá Olá folha toocreate Olá local do gateway de rede.
