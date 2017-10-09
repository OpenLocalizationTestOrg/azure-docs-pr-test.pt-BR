1. Faça logon em Olá [Portal do Azure].
2. Clique em **+NOVO** > **Web + Móvel** > **Aplicativo Móvel**, então forneça um nome para o back-end do Aplicativo Móvel.
3. Para Olá **grupo de recursos**, selecione um grupo de recursos existente ou criar um novo (usando Olá o mesmo nome de seu aplicativo). 
   
    Você pode selecionar outro plano de Serviço de Aplicativo ou criar um novo. Para obter mais informações sobre planos de serviços de aplicativos e como toocreate um novo plano em um preço diferente de camada e no local desejado, consulte [visão geral detalhada de planos de serviço de aplicativo do Azure](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Para Olá **plano de serviço de aplicativo**, plano de padrão de saudação (em hello [camada padrão](https://azure.microsoft.com/pricing/details/app-service/)) está selecionado. Você também pode selecionar um plano diferente ou [criar um novo](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). configurações do plano do serviço de aplicativo Hello determinam Olá [local, recursos, custo e os recursos de computação](https://azure.microsoft.com/pricing/details/app-service/) associados ao seu aplicativo. 
   
    Depois de decidir plano hello, clique em **criar**. Isso cria um back-end de aplicativo móvel hello. 
5. Em Olá **configurações** folha para Olá novo aplicativo móvel back-end, clique em **início rápido** > sua plataforma de aplicativo do cliente > **se conectar a um banco de dados**. 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. Em Olá **Adicionar conexão de dados** folha, clique em **banco de dados SQL** > **criar um novo banco de dados**, o banco de dados do tipo hello **nome**, Escolha um tipo de preço, clique em **Server**.  Você pode reutilizar este novo banco de dados. Se você já tiver um banco de dados em Olá mesmo local, você pode optar por **usar um banco de dados**. uso de saudação de um banco de dados em um local diferente não é recomendado devido a custos de toobandwidth e latência mais alta.
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. Em Olá **novo servidor** folha, digite um nome de servidor exclusivo Olá **nome do servidor** campo, forneça um logon e uma senha, verifique **permitir servidor de tooaccess de serviços do azure**e clique em **Okey**. Isso cria um novo banco de dados de saudação.
8. Em Olá **Adicionar conexão de dados** folha, clique em **cadeia de caracteres de Conexão**, digite Olá os valores de logon e senha para seu banco de dados e clique em **Okey**. Aguarde alguns minutos para Olá toobe de banco de dados implantado com êxito antes de continuar.

<!-- URLs. -->
[Portal do Azure]: https://portal.azure.com/
