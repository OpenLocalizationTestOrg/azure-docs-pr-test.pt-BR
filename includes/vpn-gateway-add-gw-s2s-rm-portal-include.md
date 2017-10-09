1. No hello lado esquerdo da página do portal hello, clique em  **+**  e digite 'Gateway de rede Virtual' na pesquisa. Em **Resultados**, localize e clique em **Gateway de rede virtual**.
2. Na parte inferior de saudação da folha de 'Gateway de rede Virtual' hello, clique em **criar**. Isso abre o hello **criar gateway de rede virtual** folha.

    ![Campos da folha Criar gateway de rede virtual](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "Novo gateway")

3. Em Olá **criar gateway de rede virtual** folha, especifique valores de saudação do seu gateway de rede virtual.

  - **Nome**: nomeie o seu gateway. Isso não é Olá igual ao nomear uma sub-rede de gateway. Nome de saudação do objeto de gateway Olá que você está criando-lo do.
  - **Tipo de gateway**: selecione **VPN**. Gateways VPN usam o tipo de gateway de rede virtual Olá **VPN**. 
  - **Tipo de VPN**: Selecionar tipo VPN Olá especificado para a sua configuração. A maioria das configurações exige um tipo de VPN baseado em rota.
  - **SKU**: SKU do gateway Olá selecione na lista suspensa de saudação. Olá SKUs listadas na lista suspensa de saudação dependem Olá tipo VPN que você selecionar. Para saber mais sobre os SKUs de gateway, consulte [SKUs de Gateway](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).
  - **Local**: talvez seja necessário tooscroll toosee local. Ajustar Olá **local** campo toopoint toohello local onde sua rede virtual está localizada. Se o local de saudação não está apontando para toohello região onde reside a sua rede virtual, rede virtual Olá não aparecerá na próxima etapa do hello suspensa 'Escolher uma rede virtual'.
  - **Rede virtual**: escolha Olá rede virtual toowhich deseja tooadd este gateway. Clique em **rede Virtual** 'Escolher uma rede virtual' folha de saudação tooopen. Selecione Olá VNet. Se você não vir a sua rede virtual, certifique-se de campo de local de saudação está apontando toohello região na qual sua rede virtual está localizada.
  - **Endereço IP público**: folha de 'Criar endereço IP público' hello cria um objeto de endereço IP público. endereço IP público de saudação é atribuído dinamicamente quando o gateway de VPN Olá é criado. O gateway de VPN atualmente suporta apenas alocação de endereços IP público *Dinâmico*. No entanto, isso não significa que o endereço IP de saudação alterado depois que ele foi atribuído tooyour gateway VPN. somente tempo de saudação alterações de endereço IP público hello quando é Olá gateway é excluído e criado novamente. Isso não altera o redimensionamento, a redefinição ou outras manutenções/atualizações internas do seu gateway de VPN.

    - Primeiro, clique em **endereço IP público** tooopen Olá 'Escolher endereço IP público' folha, clique em **+ criar novos** 'Criar endereço IP público' folha de saudação tooopen.
    - Em seguida, insira um **nome** para seu endereço IP público, em seguida, clique em **Okey** em Olá inferior do toosave folha suas alterações.

      ![Criar o IP público](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "Criar PIP")

4. Verifique as configurações de saudação. Você pode selecionar **toodashboard Pin** na parte inferior da saudação da folha de saudação se você quiser tooappear seu gateway no painel de saudação. 
5. Clique em **criar** toobegin criar gateway VPN hello. Olá configurações serão validadas e você verá hello "Gateway de rede Virtual de implantação" bloco no painel de saudação. Criar um gateway pode demorar até too45 minutos. Talvez seja necessário toorefresh o status da página do portal toosee Olá concluída.

Depois de criar o gateway de hello, exiba o endereço IP de saudação que foi atribuído tooit examinando a rede virtual Olá no portal de saudação. gateway Hello serão exibidos como um dispositivo conectado. Você pode clicar Olá conectado (seu gateway de rede virtual) do dispositivo tooview obter mais informações.
