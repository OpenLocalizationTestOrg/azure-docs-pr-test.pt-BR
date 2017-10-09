### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>Conceder acesso tooyour Push certificado tooMobile contrato
tooallow Mobile Engagement toosend notificações por Push em seu nome, será necessário toogrant-lo acessar o certificado de tooyour. Isso é feito configurando e inserindo seu certificado no portal do Mobile Engagement hello. Certifique-se de ter o certificado .p12, conforme explicado na [documentação da Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

1. Navegue tooyour portal do compromisso de mobilidade. Verifique se você está no hello correto e, em seguida, clique em Olá **Engage** botão na parte inferior da saudação:
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Clique em Olá **configurações** página no Portal do compromisso. De lá, clique em Olá **Push nativo** seção tooupload seu certificado p12:
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. Selecione seu p12, carregue-o e digite sua senha:
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>Enviar um aplicativo de tooyour de notificação
Agora, vamos criar uma campanha de notificação por Push simple que enviará um aplicativo de tooour por push:

1. Navegue toohello **alcançar** no seu portal do compromisso de mobilidade.
2. Clique em **novo comunicado** toocreate sua campanha de push
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. Campos de primeira Olá da sua campanha de configuração:
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * Forneça um **Nome** para sua campanha. 
   * Selecione Olá **tempo de entrega** como **somente fora do aplicativo**: isso é Olá Apple push notificação tipo simples que apresenta um texto.
   * Texto de notificação hello, digite hello primeiro **título** que será a primeira linha hello push hello.
   * Em seguida, digite sua **mensagem** qual será a segunda linha de saudação
4. Role para baixo e em Olá seção conteúda selecione **somente notificação**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. Você concluiu a campanha mais básica de saudação de configuração. Agora, role para baixo e clique em **criar** botão toosave sua campanha de notificação por push. 
6. Por fim - clique em **ativar** toosend notificação de envio. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. Você poderá receber a notificação de saudação em seu dispositivo iOS no Centro de notificação hello como Olá a seguir:
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. Se você tiver um Apple Watch emparelhado com este dispositivo iOS, em seguida, você verá Olá notificação em seu Apple Watch:
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

