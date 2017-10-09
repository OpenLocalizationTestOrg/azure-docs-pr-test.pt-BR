
<span data-ttu-id="8b0a7-101">exemplo de Hello anterior mostrou um padrão entrar, que exige Olá cliente toocontact ambos Olá identidade provedor e hello serviço back-end do Azure sempre que o aplicativo hello iniciado.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="8b0a7-102">Esse método é ineficiente e você pode ter problemas de uso se muitos clientes toostart seu aplicativo simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="8b0a7-103">Uma abordagem melhor é o token de autorização de saudação toocache retornado por saudação do serviço do Azure e tente toouse isso antes de usar um provedor com base em entrar.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="8b0a7-104">Você pode armazenar em cache token Olá emitido por Olá back-end do serviço do Azure, independentemente de se você estiver usando autenticação de cliente gerenciado ou o serviço gerenciado.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="8b0a7-105">Este tutorial usa a autenticação gerenciada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="8b0a7-106">Abra o arquivo de ToDoActivity.java hello e adicione Olá seguindo as instruções de importação:</span><span class="sxs-lookup"><span data-stu-id="8b0a7-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="8b0a7-107">Adicionar Olá toohello membros a seguir `ToDoActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="8b0a7-108">No arquivo de ToDoActivity.java de saudação, adicione Olá após a definição de saudação `cacheUserToken` método.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="8b0a7-109">Esse método armazena Olá ID de usuário e token em um arquivo de preferência que está marcado como privado.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="8b0a7-110">Isso deve proteger o acesso toohello cache para que outros aplicativos no dispositivo de saudação não tem o token de acesso de toohello.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="8b0a7-111">preferência de saudação está na área restrita para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="8b0a7-112">No entanto, se alguém obtiver toohello acessar o dispositivo, é possível que eles podem obter o cache de token de acesso toohello por outros meios.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8b0a7-113">Você pode proteger ainda mais o token Olá com criptografia, se o token de acesso tooyour os dados serão considerados altamente confidenciais e alguém pode obter toohello acessar o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="8b0a7-114">Uma solução totalmente segura está além do escopo deste tutorial, Olá no entanto e depende de seus requisitos de segurança.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="8b0a7-115">No arquivo de ToDoActivity.java de saudação, adicione Olá após a definição de saudação `loadUserTokenCache` método.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

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
5. <span data-ttu-id="8b0a7-116">Em Olá *ToDoActivity.java* de arquivo, substitua Olá `authenticate` método com hello seguinte método, que usa um cache de token.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="8b0a7-117">Altere o provedor de logon Olá toouse uma conta diferente do Google.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-117">Change hello login provider if you want toouse an account other than Google.</span></span>

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
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
6. <span data-ttu-id="8b0a7-118">Crie hello aplicativo e teste a autenticação usando uma conta válida.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="8b0a7-119">Execute pelo menos uma vez.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-119">Run it at least twice.</span></span> <span data-ttu-id="8b0a7-120">Durante a saudação executado pela primeira vez, você deve receber um prompt toosign em e criar o cache de token de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="8b0a7-121">Depois disso, cada execução tentativas de cache de token tooload Olá para autenticação.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="8b0a7-122">Você não deve ser necessário toosign no.</span><span class="sxs-lookup"><span data-stu-id="8b0a7-122">You should not be required toosign in.</span></span>
