### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Compromisso de mobilidade de conceder acesso tooyour chave API do GCM
notificações de push tooallow Mobile Engagement toosend em seu nome, é necessário toogrant ele acessar tooyour chave de API. Isso é feito configurando e digitar a chave no portal do Mobile Engagement hello.

1. Do seu Portal clássico do Azure, certifique-se você estiver no aplicativo hello que está usando para este projeto e clique em hello **Engage** botão na parte inferior da saudação:
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. Em seguida, clique em Olá **configurações** -> **Push nativo** seção tooenter sua chave GCM:
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Clique em hello **editar** ícone na frente do **chave API** em hello **configurações do GCM** seção conforme mostrado abaixo:
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. No pop-up hello, cole Olá GCM chave de servidor obtido antes e, em seguida, clique em **Okey**.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>Enviar um aplicativo de tooyour de notificação
Agora, vamos criar uma campanha de notificação por push simples que envia um aplicativo de tooour de notificação por push.

1. Navegue toohello **alcançar** no seu portal do compromisso de mobilidade.
2. Clique em **novo comunicado** toocreate sua campanha de notificação por push.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. Configure o primeiro campo de saudação da campanha por meio de saudação etapas a seguir:
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. Nome de sua campanha.
   
    b. Selecione Olá **tipo de entrega** como *notificação do sistema -> simples*: Este é o tipo de notificação de push Android simples Olá que apresenta um título e uma linha pequena de texto.
   
    c. Selecione **tempo de entrega** como *sempre* tooallow Olá aplicativo tooreceive uma notificação se o aplicativo hello é iniciado ou não.
   
    d. Em Olá Olá de tipo de texto de notificação **título** que será em negrito no envio de saudação.
   
    e. Em seguida, digite sua **Mensagem**
4. Role para baixo e em Olá **conteúdo** seção, selecione **somente notificação**.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. Você concluiu possíveis de campanha configuração hello mais básica. Agora, role para baixo novamente e clique em Olá **criar** botão toosave sua campanha.
6. Última etapa: clique em **ativar** tooactivate suas notificações de push de toosend da campanha.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

