
1. <span data-ttu-id="f4d0b-101">No arquivo de projeto MainPage.xaml.cs hello, adicione o seguinte de saudação **usando** instruções:</span><span class="sxs-lookup"><span data-stu-id="f4d0b-101">In hello MainPage.xaml.cs project file, add hello following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="f4d0b-102">Substituir saudação **AuthenticateAsync** método com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f4d0b-102">Replace hello **AuthenticateAsync** method with hello following code:</span></span>
   
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
   
    <span data-ttu-id="f4d0b-103">Nesta versão do **AuthenticateAsync**, Olá aplicativo tenta toouse credenciais armazenadas no hello **PasswordVault** tooaccess Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="f4d0b-103">In this version of **AuthenticateAsync**, hello app tries toouse credentials stored in hello **PasswordVault** tooaccess hello service.</span></span> <span data-ttu-id="f4d0b-104">Também é realizado um registro normal quando não há uma credencial armazenada.</span><span class="sxs-lookup"><span data-stu-id="f4d0b-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f4d0b-105">Um token em cache pode ser expirado e expiração do token também pode ocorrer após a autenticação quando o aplicativo hello está em uso.</span><span class="sxs-lookup"><span data-stu-id="f4d0b-105">A cached token may be expired, and token expiration can also occur after authentication when hello app is in use.</span></span> <span data-ttu-id="f4d0b-106">toolearn como toodetermine se um token tiver expirado, consulte [verificar tokens de autenticação expirou](http://aka.ms/jww5vp).</span><span class="sxs-lookup"><span data-stu-id="f4d0b-106">toolearn how toodetermine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="f4d0b-107">Para erros de autorização de toohandling uma solução tokens tooexpiring relacionados, consulte Olá postagem [cache e a manipulação de tokens expirados em serviços móveis do Azure gerenciados SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4d0b-107">For a solution toohandling authorization errors related tooexpiring tokens, see hello post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="f4d0b-108">Reinicie o aplicativo hello duas vezes.</span><span class="sxs-lookup"><span data-stu-id="f4d0b-108">Restart hello app twice.</span></span>
   
    <span data-ttu-id="f4d0b-109">Observe que no início da primeira hello, entrar com o provedor de saudação novamente é necessária.</span><span class="sxs-lookup"><span data-stu-id="f4d0b-109">Notice that on hello first start-up, sign-in with hello provider is again required.</span></span> <span data-ttu-id="f4d0b-110">No entanto, na segunda reinicialização depois Olá credenciais Olá armazenados em cache são usadas e entrada será ignorada.</span><span class="sxs-lookup"><span data-stu-id="f4d0b-110">However, on hello second restart hello cached credentials are used and sign-in is bypassed.</span></span> 

