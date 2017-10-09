
1. Clique em Olá **serviços de aplicativos** botão, selecione seu back-end de aplicativos móveis, selecione **Quickstart**e, em seguida, selecione a plataforma de cliente (iOS, Android, Xamarin, Cordova).

    ![Portal do Azure com Início Rápido de Aplicativos Móveis realçado][quickstart]

2. Se uma conexão de banco de dados não estiver configurado, crie um fazendo Olá seguinte:

    ![Portal do Azure com conexão de aplicativos móveis toodatabase][connect]

    a. Crie um novo servidor e Banco de Dados SQL.

    ![O portal do Azure com Aplicativos Móveis cria novo banco de dados e servidor][server]

    b. Aguarde até que a conexão de dados de saudação é criado com êxito.

    ![Notificação no portal do Azure sobre a criação bem-sucedida da conexão de dados][notification]

    c. A conexão de dados deve ser bem-sucedida.

    ![Notificação no portal do Azure, "Você já tem uma conexão de dados"][already-connection]

3. Em **2. Crie uma API de tabela**, selecione Node.js como **Linguagem de back-end**. 
 
4. Aceite a confirmação de saudação e, em seguida, selecione **tabela TodoItem criar**.  
    Essa ação cria uma nova tabela de item de tarefas pendentes no banco de dados. 

    >[!IMPORTANT]
    > Alternar um tooNode.js de back-end existente substituirá todo o conteúdo. toocreate um back-end do .NET em vez disso, consulte [trabalhar com o servidor de saudação back-end .NET SDK para aplicativos móveis][instructions].

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
