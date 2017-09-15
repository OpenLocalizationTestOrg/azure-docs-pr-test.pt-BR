
1. <span data-ttu-id="b74ef-101">Abra o projeto no Android Studio.</span><span class="sxs-lookup"><span data-stu-id="b74ef-101">Open the project in Android Studio.</span></span>

2. <span data-ttu-id="b74ef-102">No **Gerenciador de projetos** , no Android Studio, abra o arquivo ToDoActivity.java e adicione as seguintes instruções de importação:</span><span class="sxs-lookup"><span data-stu-id="b74ef-102">In **Project Explorer** in Android Studio, open the ToDoActivity.java file and add the following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="b74ef-103">Adicione o método a seguir à classe **ToDoActivity** :</span><span class="sxs-lookup"><span data-stu-id="b74ef-103">Add the following method to the **ToDoActivity** class:</span></span>

        // You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using the Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check the request code matches the one we send in the login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check the error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="b74ef-104">Esse código cria um novo método para manipular o processo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="b74ef-104">This code creates a method to handle the Google authentication process.</span></span> <span data-ttu-id="b74ef-105">Um diálogo exibe a ID do usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="b74ef-105">A dialog displays the ID of the authenticated user.</span></span> <span data-ttu-id="b74ef-106">Você só pode continuar em uma autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="b74ef-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b74ef-107">Se você estiver usando um provedor de identidade diferente do Google, altere o valor passado ao método **login** para um dos valores a seguir: _MicrosoftAccount_, _Facebook_, _Twitter_ ou _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="b74ef-107">If you are using an identity provider other than Google, change the value passed to the **login** method to one of the following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="b74ef-108">No método **OnCreate**, adicione a linha de código a seguir após o código que cria uma instância do objeto `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="b74ef-108">In the **onCreate** method, add the following line of code after the code that instantiates the `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="b74ef-109">Essa chamada inicia o processo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="b74ef-109">This call starts the authentication process.</span></span>

5. <span data-ttu-id="b74ef-110">Mova o código restante após `authenticate();` no método **OnCreate** para um novo método **CreateTable**:</span><span class="sxs-lookup"><span data-stu-id="b74ef-110">Move the remaining code after `authenticate();` in the **onCreate** method to a new **createTable** method:</span></span>

        private void createTable() {

            // Get the table instance to use.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter to bind the items with the view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load the items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="b74ef-111">Para garantir que o redirecionamento funcione conforme o esperado, adicione o seguinte trecho de _RedirectUrlActivity_ a _AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="b74ef-111">To ensure redirection works as expected, add the following snippet of _RedirectUrlActivity_ to _AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="b74ef-112">Adicione redirectUriScheme a _build.gradle_ de seu aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="b74ef-112">Add redirectUriScheme to _build.gradle_ of your Android application.</span></span>

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. <span data-ttu-id="b74ef-113">Adicione com.android.support:customtabs:23.0.1 às dependências em seu build.gradle:</span><span class="sxs-lookup"><span data-stu-id="b74ef-113">Add com.android.support:customtabs:23.0.1 to the dependencies in your build.gradle:</span></span>

      <span data-ttu-id="b74ef-114">dependências {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span><span class="sxs-lookup"><span data-stu-id="b74ef-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="b74ef-115">No menu **Executar**, clique em **Executar aplicativo** para iniciar o aplicativo e entrar com seu provedor de identidade escolhido.</span><span class="sxs-lookup"><span data-stu-id="b74ef-115">From the **Run** menu, click **Run app** to start the app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="b74ef-116">O esquema de URL mencionado diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b74ef-116">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="b74ef-117">Certifique-se de que todas as ocorrências de `{url_scheme_of_you_app}` a mesma formatação, maiúsculas ou minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b74ef-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use the same case.</span></span>

<span data-ttu-id="b74ef-118">Ao entrar com êxito, o aplicativo deve ser executado sem erros e você deve ser capaz de consultar o serviço de back-end e fazer atualizações nos dados.</span><span class="sxs-lookup"><span data-stu-id="b74ef-118">When you are successfully signed in, the app should run without errors, and you should be able to query the back-end service and make updates to data.</span></span>
