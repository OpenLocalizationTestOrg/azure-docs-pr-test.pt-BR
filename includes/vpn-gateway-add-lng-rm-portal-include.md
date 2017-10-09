1. No portal de saudação do **todos os recursos**, clique em **+ adicionar**. Em Olá **tudo** caixa de pesquisa de folha, digite **gateway de rede Local**, em seguida, clique em tooreturn uma lista de recursos. Clique em **gateway de rede Local** tooopen Olá folha, clique em **criar** tooopen Olá **criar gateway de rede local** folha.
   
    ![criar gateway de rede local](./media/vpn-gateway-add-lng-rm-portal-include/lng.png)

2. Em Olá **criar folha de gateway de rede local**, especifique um **nome** para seu objeto de gateway de rede local. Se possível, use algo intuitivo, como **ClassicVNetLocal** ou **TestVNet1Local**. Isso torna mais fácil para você tooidentify Olá gateway de rede local no portal de saudação.
3. Especifique um público válido **endereço IP** para o dispositivo VPN hello ou toowhich de gateway de rede virtual você deseja tooconnect.<br>**Se esta rede local representa um local:** especificar o endereço IP público de saudação do dispositivo VPN Olá que você deseja tooconnect para. Ele não pode estar atrás de NAT e tem toobe acessível pelo Azure.<br>**Se esta rede local representa outro VNet:** especificar o endereço IP público Olá que foi atribuído o gateway de rede virtual toohello para essa rede virtual.<br>**Se você ainda não possui endereço IP hello:** você pode fazer backup de um endereço IP de espaço reservado válido e, em seguida, voltar e modificar essa configuração antes de se conectar.
4. **Espaço de endereço** refere-se toohello intervalos de endereços de rede Olá que representa esta rede local. Você pode adicionar vários intervalos de espaço de endereço. Certifique-se de que os intervalos de saudação especificado aqui não sobrepor intervalos de toowhich outras redes que você se conectar.
5. Para **assinatura**, verifique se esse Olá correto de assinatura está mostrando.
6. Para **grupo de recursos**, selecione grupo de recursos de saudação que você deseja toouse. Você pode criar um novo grupo de recursos ou selecionar um que você já criou.
7. Para **local**, selecione Olá local em que esse recurso será criado. Talvez você queira tooselect Olá sua rede virtual reside no mesmo local, mas não é necessário toodo assim.
8. Clique em **criar** gateway de rede local toocreate hello.

