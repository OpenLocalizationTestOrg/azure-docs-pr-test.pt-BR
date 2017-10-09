
1. Navegue toohello [Google nuvem Console](https://console.developers.google.com/project), entre com suas credenciais de conta do Google. 
2. Clique em **Criar Projeto**, digite um nome de projeto, então clique em **Criar**. Se solicitado, realizar Olá verificação de SMS e clique em **criar** novamente.
   
    ![Criar um novo projeto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     Digite o novo **Nome do projeto** e clique em **Criar projeto**.
3. Clique em Olá **utilitários e muito mais** botão e, em seguida, clique em **informações sobre o projeto**. Anote Olá **projeto número**. Você precisará tooset esse valor como Olá `SenderId` variável no aplicativo de cliente hello.
   
    ![Utilitários e mais](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. Em Olá projeto dashboard, em **Mobile APIs**, clique em **Google Cloud Messaging**, em seguida, na próxima página do hello, clique em **Habilitar API** e aceite os termos de saudação do serviço. 
   
    ![Habilitar o GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Habilitar o GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. No painel de projeto hello, clique em **credenciais** > **Create Credential** > **chave API**. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. Em **Criar uma nova chave**, clique em **Chave do servidor**, digite um nome para a chave, clique em **Criar**.
7. Anote Olá **chave API** valor.
   
    Você irá usar esse valor de chave de API tooenable tooauthenticate do Azure com GCM e enviar notificações por push em nome do seu aplicativo.

