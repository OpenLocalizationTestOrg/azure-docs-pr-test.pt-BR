## <a name="obtain-an-azure-resource-manager-token"></a>Obter um token do Azure Resource Manager
Active Directory do Azure deve autenticar todas as tarefas de saudação que podem ser executadas em recursos usando hello Azure Resource Manager. Olá exemplo mostrado aqui usa autenticação de senha, para outras abordagens, consulte [solicitações de autenticação do Azure Resource Manager][lnk-authenticate-arm].

1. Adicionar Olá toohello de código a seguir **principal** método em Program.cs tooretrieve um token do AD do Azure usando a id de aplicativo hello e a senha.
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. Criar um **ResourceManagementClient** que usa Olá token adicionando Olá após o final do código toohello de saudação do objeto **principal** método:
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. Criar ou obter uma referência ao grupo de recursos de saudação que você está usando:
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx