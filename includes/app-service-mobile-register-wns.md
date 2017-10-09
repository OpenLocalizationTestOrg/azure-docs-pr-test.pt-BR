
1. No Gerenciador de soluções do Visual Studio, clique o projeto de aplicativo da Windows Store hello e clique em **repositório** > **associar aplicativo hello repositório**.

    ![Associar aplicativo com a Windows Store](./media/app-service-mobile-register-wns/notification-hub-associate-win8-app.png)
2. No Assistente de saudação, clique em **próximo**e entre com sua conta da Microsoft. Digite um nome para o seu aplicativo em **Reservar nome do aplicativo** e clique em **Reservar**.
3. Após o registro do aplicativo hello novo nome de aplicativo criado com êxito, selecione hello, clique em **próximo**e, em seguida, clique em **associar**. Isso adiciona o manifesto do aplicativo hello necessárias da Windows Store registro informações toohello.
4. Repita as etapas 1 e 3 para o projeto de aplicativo do Windows Phone Store hello usando Olá mesmo registro que você criou anteriormente para o aplicativo da Windows Store hello.  
5. Procurar toohello [Centro de desenvolvimento do Windows](https://dev.windows.com/en-us/overview)e entre com sua conta da Microsoft. Clique em novo registro de aplicativo hello em **meus aplicativos**e, em seguida, expanda **serviços** > **notificações por Push**.
6. Em Olá **notificações por Push** , clique em **site de serviços do Live** em **Windows Push Notification Services (WNS) e aplicativos móveis do Microsoft Azure**. Anote os valores de saudação do hello **SID do pacote** e hello *atual* valor em **segredo do aplicativo**. 

    ![Configuração do aplicativo no Centro de desenvolvedores Olá](./media/app-service-mobile-register-wns/mobile-services-win8-app-push-auth.png)

   > [!IMPORTANT]
   > SID de pacote e segredo do aplicativo Hello são credenciais de segurança importantes. Não compartilhe esses valores com ninguém nem os distribua com seu aplicativo.
   >
   >
