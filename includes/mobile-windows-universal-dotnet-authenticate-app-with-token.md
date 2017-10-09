
1. No arquivo de projeto MainPage.xaml.cs hello, adicione o seguinte de saudação **usando** instruções:
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. Substituir saudação **AuthenticateAsync** método com hello código a seguir:
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    Nesta versão do **AuthenticateAsync**, Olá aplicativo tenta toouse credenciais armazenadas no hello **PasswordVault** tooaccess Olá serviço. Também é realizado um registro normal quando não há uma credencial armazenada.
   
   > [!NOTE]
   > Um token em cache pode ser expirado e expiração do token também pode ocorrer após a autenticação quando o aplicativo hello está em uso. toolearn como toodetermine se um token tiver expirado, consulte [verificar tokens de autenticação expirou](http://aka.ms/jww5vp). Para erros de autorização de toohandling uma solução tokens tooexpiring relacionados, consulte Olá postagem [cache e a manipulação de tokens expirados em serviços móveis do Azure gerenciados SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx). 
   > 
   > 
3. Reinicie o aplicativo hello duas vezes.
   
    Observe que no início da primeira hello, entrar com o provedor de saudação novamente é necessária. No entanto, na segunda reinicialização depois Olá credenciais Olá armazenados em cache são usadas e entrada será ignorada. 

