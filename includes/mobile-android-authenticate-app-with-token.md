
<span data-ttu-id="66241-101">O exemplo anterior mostrou um logon padrão, que requer que o cliente contate o provedor de identidade e o serviço de back-end do Azure sempre que o aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="66241-101">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the back-end Azure service every time the app starts.</span></span> <span data-ttu-id="66241-102">Esse método é ineficiente e você pode ter problemas relacionados ao uso caso muitos clientes tentem iniciar o aplicativo simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="66241-102">This method is inefficient, and you can have usage-related issues if many customers try to start your app simultaneously.</span></span> <span data-ttu-id="66241-103">Uma abordagem melhor é armazenar em cache o token de autorização retornado pelo serviço do Azure e tentar usá-lo antes de usar um logon baseado em provedor.</span><span class="sxs-lookup"><span data-stu-id="66241-103">A better approach is to cache the authorization token returned by the Azure service, and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="66241-104">Você pode armazenar em cache o token emitido pelo serviço de back-end do Azure usando tanto a autenticação gerenciada pelo cliente quanto a autenticação gerenciada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="66241-104">You can cache the token issued by the back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="66241-105">Este tutorial usa a autenticação gerenciada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="66241-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="66241-106">Abra o arquivo ToDoActivity.java e adicione as seguintes instruções de importação:</span><span class="sxs-lookup"><span data-stu-id="66241-106">Open the ToDoActivity.java file and add the following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="66241-107">Adicione os seguintes membros à classe `ToDoActivity` :</span><span class="sxs-lookup"><span data-stu-id="66241-107">Add the following members to the `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="66241-108">No arquivo ToDoActivity.java, adicione a seguinte definição para o método `cacheUserToken`.</span><span class="sxs-lookup"><span data-stu-id="66241-108">In the ToDoActivity.java file, add the following definition for the `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="66241-109">Este método armazena a ID e o token do usuário em um arquivo preferencial marcado como privado.</span><span class="sxs-lookup"><span data-stu-id="66241-109">This method stores the user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="66241-110">Isto deve proteger o acesso ao cache para que os outros aplicativos do dispositivo não tenham acesso ao token.</span><span class="sxs-lookup"><span data-stu-id="66241-110">This should protect access to the cache so that other apps on the device do not have access to the token.</span></span> <span data-ttu-id="66241-111">A preferência é uma área restrita para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66241-111">The preference is sandboxed for the app.</span></span> <span data-ttu-id="66241-112">No entanto, se alguém obtiver acesso ao dispositivo, é possível que a pessoa ganhe acesso ao cache de token de outras formas.</span><span class="sxs-lookup"><span data-stu-id="66241-112">However, if someone gains access to the device, it is possible that they may gain access to the token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="66241-113">Você pode proteger ainda mais o token com criptografia se o acesso do token a seus dados for considerado altamente confidencial e alguém puder acessar o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="66241-113">You can further protect the token with encryption, if token access to your data is considered highly sensitive and someone may gain access to the device.</span></span> <span data-ttu-id="66241-114">No entanto, uma solução completamente segura está além do escopo deste tutorial e depende dos seus requisitos de segurança.</span><span class="sxs-lookup"><span data-stu-id="66241-114">A completely secure solution is beyond the scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="66241-115">No arquivo ToDoActivity.java, adicione a seguinte definição para o método `loadUserTokenCache`.</span><span class="sxs-lookup"><span data-stu-id="66241-115">In the ToDoActivity.java file, add the following definition for the `loadUserTokenCache` method.</span></span>

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. <span data-ttu-id="66241-116">No arquivo *ToDoActivity.java*, substitua o método `authenticate` pelo seguinte método, que usa um cache de token.</span><span class="sxs-lookup"><span data-stu-id="66241-116">In the *ToDoActivity.java* file, replace the `authenticate` method with the following method, which uses a token cache.</span></span> <span data-ttu-id="66241-117">Altere o provedor de logon se quiser usar uma conta que não seja do Google.</span><span class="sxs-lookup"><span data-stu-id="66241-117">Change the login provider if you want to use an account other than Google.</span></span>

        private void authenticate() {
            // We first try to load a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed to load a token cache, login and create a token cache
            else
            {
                // Login using the Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. <span data-ttu-id="66241-118">Compile o aplicativo e teste a autenticação usando uma conta válida.</span><span class="sxs-lookup"><span data-stu-id="66241-118">Build the app and test authentication using a valid account.</span></span> <span data-ttu-id="66241-119">Execute pelo menos uma vez.</span><span class="sxs-lookup"><span data-stu-id="66241-119">Run it at least twice.</span></span> <span data-ttu-id="66241-120">Durante a primeira execução, você deverá ser solicitado a iniciar uma sessão e criar o cache do token.</span><span class="sxs-lookup"><span data-stu-id="66241-120">During the first run, you should receive a prompt to sign in and create the token cache.</span></span> <span data-ttu-id="66241-121">Depois disso, cada execução tentará carregar o cache de token para autenticação.</span><span class="sxs-lookup"><span data-stu-id="66241-121">After that, each run attempts to load the token cache for authentication.</span></span> <span data-ttu-id="66241-122">Não deve ser solicitado que você inicie uma sessão.</span><span class="sxs-lookup"><span data-stu-id="66241-122">You should not be required to sign in.</span></span>
