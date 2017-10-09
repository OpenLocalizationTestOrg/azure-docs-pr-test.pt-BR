
1. Abra o projeto de saudação no Android Studio.

2. Em **Explorador de projeto** no Android Studio, abra o arquivo de ToDoActivity.java de saudação e adicione Olá seguindo as instruções de importação:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Adicionar Olá após o método toohello **ToDoActivity** classe:

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    Esse código cria uma saudação do método toohandle processo de autenticação do Google. Uma caixa de diálogo exibe a ID de saudação do usuário Olá autenticado. Você só pode continuar em uma autenticação bem-sucedida.

    > [!NOTE]
    > Se você estiver usando um provedor de identidade que não seja o Google, altere o valor de saudação passado toohello **logon** tooone de método de saudação valores a seguir: _MicrosoftAccount_, _Facebook_, _Twitter_, ou _windowsazureactivedirectory_.

4. Em Olá **onCreate** método, adicionar Olá a seguinte linha de código após código Olá que instancia Olá `MobileServiceClient` objeto.

        authenticate();

    Essa chamada inicia o processo de autenticação de saudação.

5. Olá restantes código depois de mover `authenticate();` em Olá **onCreate** método tooa novo **createTable** método:

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. tooensure redirecionamento funciona conforme o esperado, adicionar Olá seguindo o trecho de _RedirectUrlActivity_ too_AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. Adicione too_build.gradle_ redirectUriScheme do seu aplicativo Android.

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

8. Adicione o gradle com.android.support:customtabs:23.0.1 toohello dependências:

      dependências {        // ...        compile 'com.android.support:customtabs:23.0.1'    }

9. De saudação **executar** menu, clique em **executar aplicativo** toostart Olá aplicativo e entre com seu provedor de identidade escolhido.

> [!WARNING]
> Olá mencionado o esquema de URL diferencia maiusculas de minúsculas.  Certifique-se de que todas as ocorrências de `{url_scheme_of_you_app}` uso Olá mesmo caso.

Quando você estiver entrado com êxito, Olá aplicativo deve ser executado sem erros, e você deve ser capaz de tooquery serviço de back-end de saudação e fazer atualizações toodata.
