
exemplo de Hello anterior mostrou um padrão entrar, que exige Olá cliente toocontact ambos Olá identidade provedor e hello serviço back-end do Azure sempre que o aplicativo hello iniciado. Esse método é ineficiente e você pode ter problemas de uso se muitos clientes toostart seu aplicativo simultaneamente. Uma abordagem melhor é o token de autorização de saudação toocache retornado por saudação do serviço do Azure e tente toouse isso antes de usar um provedor com base em entrar.

> [!NOTE]
> Você pode armazenar em cache token Olá emitido por Olá back-end do serviço do Azure, independentemente de se você estiver usando autenticação de cliente gerenciado ou o serviço gerenciado. Este tutorial usa a autenticação gerenciada pelo serviço.
>
>

1. Abra o arquivo de ToDoActivity.java hello e adicione Olá seguindo as instruções de importação:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Adicionar Olá toohello membros a seguir `ToDoActivity` classe.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. No arquivo de ToDoActivity.java de saudação, adicione Olá após a definição de saudação `cacheUserToken` método.

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Esse método armazena Olá ID de usuário e token em um arquivo de preferência que está marcado como privado. Isso deve proteger o acesso toohello cache para que outros aplicativos no dispositivo de saudação não tem o token de acesso de toohello. preferência de saudação está na área restrita para o aplicativo hello. No entanto, se alguém obtiver toohello acessar o dispositivo, é possível que eles podem obter o cache de token de acesso toohello por outros meios.

   > [!NOTE]
   > Você pode proteger ainda mais o token Olá com criptografia, se o token de acesso tooyour os dados serão considerados altamente confidenciais e alguém pode obter toohello acessar o dispositivo. Uma solução totalmente segura está além do escopo deste tutorial, Olá no entanto e depende de seus requisitos de segurança.
   >
   >
4. No arquivo de ToDoActivity.java de saudação, adicione Olá após a definição de saudação `loadUserTokenCache` método.

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
5. Em Olá *ToDoActivity.java* de arquivo, substitua Olá `authenticate` método com hello seguinte método, que usa um cache de token. Altere o provedor de logon Olá toouse uma conta diferente do Google.

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
6. Crie hello aplicativo e teste a autenticação usando uma conta válida. Execute pelo menos uma vez. Durante a saudação executado pela primeira vez, você deve receber um prompt toosign em e criar o cache de token de saudação. Depois disso, cada execução tentativas de cache de token tooload Olá para autenticação. Você não deve ser necessário toosign no.
