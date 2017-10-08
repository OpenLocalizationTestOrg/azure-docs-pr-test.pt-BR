---
title: "aaaAzure AD Android Introdução | Microsoft Docs"
description: Como toobuild um aplicativo do Android que se integra ao AD do Azure para entrar e chamadas de AD do Azure APIs protegidas usando OAuth.
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Integração do Azure AD a um aplicativo Android
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Experimentar a visualização de saudação do nosso novo [portal do desenvolvedor](https://identity.microsoft.com/Docs/Android), que irá ajudá-lo a colocar em funcionamento com o Azure AD em apenas alguns minutos. portal do desenvolvedor Olá irá orientá-lo pelo processo de saudação do registro de um aplicativo e a integração do AD do Azure em seu código. Quando terminar, você terá um aplicativo simples que pode autenticar os usuários em seu locatário e um back-end que pode aceitar tokens e executar a validação.
>
>

Se você estiver desenvolvendo um aplicativo de desktop, Azure Active Directory (AD do Azure) torna simples e direta para você tooauthenticate os usuários com suas contas do Active Directory local. Ele também permite que seu aplicativo toosecurely consumir qualquer web API protegida pelo AD do Azure, como Olá APIs do Office 365 ou Olá API do Azure.

Para clientes do Android que necessitam de recursos tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory (ADAL). Olá única finalidade ADAL é toomake fácil para seus tokens de acesso do aplicativo tooget. toodemonstrate fácil é, criaremos um aplicativo do Android lista de tarefas que:

* Obtém acesso tokens para chamar uma API da lista de tarefas usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Obtém a lista de tarefas pendentes de um usuário.
* Desconecta usuários.

tooget iniciado, você precisa de um locatário do AD do Azure, na qual você pode criar usuários e registrar um aplicativo. Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>Etapa 1: Baixar e executar o servidor de exemplo hello Node. js REST API TODO
exemplo de Node. js REST API TODO Hello é gravado especificamente toowork em nosso exemplo existente para a criação de um API de REST de tarefas pendentes de único locatário do AD do Azure. Este é um pré-requisito para Olá início rápido.

Para obter informações sobre como tooset isso, consulte nossos exemplos existentes em [Microsoft Azure exemplo REST API de serviço do Active Directory para Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>Etapa 2: Registre sua API da Web com seu locatário do Azure AD
O Active Directory dá suporte à adição de dois tipos de aplicativos:

- APIs da Web que oferecem serviços toousers
- Aplicativos (executando em Olá web ou em um dispositivo) que acessam as APIs de web

Nesta etapa, você está registrando Olá web API que você está executando localmente para testar este exemplo. Normalmente, essa API da web é um serviço REST que é a funcionalidade de oferta que você deseja que um aplicativo tooaccess. O Azure AD pode ajudar a proteger qualquer ponto de extremidade.

Estamos supondo que você está registrando Olá TODO REST API mencionado anteriormente. Mas isso funciona para qualquer API da web que você deseja proteger toohelp Active Directory do Azure.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta. Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.
5. Insira um nome amigável para o aplicativo hello (por exemplo, **TodoListService**), selecione **aplicativo Web e/ou API da Web**e clique em **próximo**.
6. Para Olá URL de logon, insira a URL base Olá para exemplo hello. Por padrão, ela é `https://localhost:8080`.
7. Clique em **Okey** toocomplete registro de saudação.
8. Ainda no hello portal do Azure, acesse a página de aplicativo tooyour, localizar o valor de ID de aplicativo hello e copiá-lo. Você precisará dele mais tarde ao configurar o aplicativo.
9. De saudação **configurações** -> **propriedades** página, atualize o URI da ID do aplicativo hello - digite `https://<your_tenant_name>/TodoListService`. Substituir `<your_tenant_name>` com nome de saudação do seu locatário do AD do Azure.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>Etapa 3: Registrar o aplicativo de Android Native Client do exemplo hello
Registre seu aplicativo da Web neste exemplo. Isso permite que toocommunicate seu aplicativo com hello registrados apenas API da web. O AD do Azure recusará tooeven permitir tooask seu aplicativo para entrar, a menos que ele está registrado. Que faz parte da segurança de saudação do modelo de saudação.

Estamos supondo que você está registrando o aplicativo de exemplo hello mencionado anteriormente. Porém, este procedimento funciona para qualquer aplicativo que você esteja desenvolvendo.

> [!NOTE]
> Talvez você se pergunte por que está colocando um aplicativo e uma API da Web em um locatário. Como você deve ter adivinhado, é possível compilar um aplicativo que acessa uma API externa que é registrada no Azure AD de outro locatário. Se você fizer isso, os clientes serão solicitados tooconsent toohello uso Olá API no aplicativo hello. A biblioteca de autenticação do Active Directory para iOS se encarrega desse consentimento por você. Como podemos explorar recursos mais avançados, você verá que se trata de uma parte importante do conjunto de saudação do hello trabalho tooaccess necessárias de APIs do Office e do Azure, bem como qualquer outro provedor de serviço do Microsoft. Por enquanto, como você se registrou sua API da web e o aplicativo hello mesmo locatário, você não verá quaisquer solicitações de consentimento. Isso geralmente é o caso de Olá se você estiver desenvolvendo um aplicativo apenas para seu próprio toouse da empresa.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta. Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.
5. Insira um nome amigável para o aplicativo hello (por exemplo, **TodoListClient Android**), selecione **aplicativo cliente nativo**e clique em **próximo**.
6. URI de redirecionamento para hello, digite `http://TodoListClient`. Clique em **Concluir**.
7. Na página de aplicativo hello, localizar o valor de ID de aplicativo hello e copiá-lo. Você precisará dele mais tarde ao configurar o aplicativo.
8. De saudação **configurações** página, selecione **permissões necessárias** e selecione **adicionar**.  Localize e selecione TodoListService, adicionar Olá **acesso TodoListService** permissão em **permissões delegadas**e clique em **feito**.

toobuild com o Maven, você pode usar pom.xml no nível superior da saudação:

1. Clone esse repositório em um diretório de sua escolha:

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Siga as etapas de Olá Olá [tooset pré-requisitos seu ambiente Maven para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Configure o emulador Olá 19 SDK.
4. Acesse a pasta raiz de toohello onde você clonou repositório hello.
5. Execute este comando: `mvn clean install`
6. Alterar o exemplo de início rápido do hello diretório toohello:`cd samples\hello`
7. Execute este comando: `mvn android:deploy android:run`

   Você deve ver a saudação inicial de aplicativo.
8. Insira tootry de credenciais de usuário de teste.

JAR pacotes serão enviados ao lado do pacote do hello AAR.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>Etapa 4: Baixar Olá Android ADAL e adicioná-lo tooyour espaço de trabalho do Eclipse
Tornamos fácil para você toohave várias opções toouse ADAL em seu projeto Android:

* Você pode usar o hello tooimport de código de origem nesta biblioteca no aplicativo de tooyour Eclipse e link.
* Se você estiver usando o Android Studio, você pode usar o hello AAR pacote referência e formato Olá binários.

### <a name="option-1-source-zip"></a>Opção 1: zip de origem
toodownload uma cópia do código-fonte hello, clique em **baixar ZIP** Olá direita da página de saudação. Ou [baixe do GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Opção 2: Origem via Git
código-fonte tooget saudação do hello SDK por meio de Git, digite:

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Opção 3: Binários via Gradle
Você pode obter os binários de saudação do repositório central de Maven hello. pacote de AAR Olá pode ser incluído em seu projeto no Android Studio da seguinte maneira:

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>Opção 4: AAR via Maven
Se você estiver usando Olá M2Eclipse plug-in, você pode especificar a dependência de saudação em seu arquivo pom.xml:

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>Opção 5: Pacote JAR dentro da pasta de bibliotecas de saudação
Você pode obter o arquivo JAR de saudação do repositório de Maven hello e inseri-la em Olá **bibliotecas** pasta em seu projeto. Você precisa toocopy Olá recursos necessários tooyour projeto, porque os pacotes JAR Olá não incluem-los.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>Etapa 5: Adicionar um projeto ADAL tooyour tooAndroid referências
1. Adicione uma referência de projeto do tooyour e especificá-la como uma biblioteca Android. Se não tiver certeza como toodo isso, você pode obter mais informações sobre Olá [site Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Adicione dependência de projeto Olá para depuração em suas configurações de projeto.
3. Atualize tooinclude de arquivo AndroidManifest.xml do projeto:

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. Crie uma instância de AuthenticationContext na atividade principal. Olá detalhes desta chamada além do escopo deste tópico hello, mas você pode obter um bom começo examinando Olá [exemplo do Android Native Client](https://github.com/AzureADSamples/NativeClient-Android). Em Olá exemplo a seguir, SharedPreferences é cache padrão de saudação e autoridade está na forma de saudação do `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Copie esta final do código bloco toohandle Olá de AuthenticationActivity depois insere as credenciais de usuário de saudação e recebe um código de autorização:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask para um token, defina um retorno de chamada:

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. Por fim, solicite um token usando esse retorno de chamada:

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Aqui está uma explicação sobre os parâmetros de saudação:

* *recurso* é necessária e recurso Olá estiver tentando tooaccess.
* *clientid* é obrigatório e é proveniente do Azure AD.
* *RedirectUri* não é necessário toobe fornecido para a chamada de acquireToken hello. Configure-o como o nome de seu pacote.
* *PromptBehavior* ajuda tooask para cache de saudação tooskip credenciais e o cookie.
* *retorno de chamada* é chamado depois que o código de autorização de saudação é trocado por um token. Ele possui um objeto AuthenticationResult, que tem informações sobre o token de acesso, a data de vencimento e o token de ID.
* *acquireTokenSilent* é opcional. Você pode chamá-lo toohandle cache e atualização do token. Ele também fornece a versão de sincronização de saudação. Ele aceita *userid* como parâmetro.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

Usando este passo a passo, você deve ter o que você precisa toosuccessfully integrar com o Active Directory do Azure. Para obter mais exemplos disso funcionar, visite Olá AzureADSamples / repositório no GitHub.

## <a name="important-information"></a>Informações importantes
### <a name="customization"></a>Personalização
Os recursos de seu aplicativo podem substituir os recursos de projeto da biblioteca. Isso acontece quando seu aplicativo está sendo compilado. Por esse motivo, você pode personalizar o modo de saudação do autenticação atividade layout desejado. ID de Olá tookeep-se de controles de saudação que ADAL usa (exibição da Web).

### <a name="broker"></a>Agente
aplicativo de Portal da empresa do Microsoft Intune Olá fornece o componente de agente do hello. Olá conta é criada no AccountManager. tipo de conta de saudação é "workaccount". AccountManager permite apenas uma única conta SSO. Ele cria um cookie SSO para o usuário Olá depois de concluir o desafio de dispositivo Olá para um dos aplicativos de saudação.

ADAL usa a conta de agente de saudação se uma conta de usuário é criada nesse autenticador e você escolher não tooskip-lo. Você pode ignorar o usuário de agente Olá com:

   `AuthenticationSettings.Instance.setSkipBroker(true);`

Você precisa tooregister um RedirectUri especial para uso do agente. RedirectUri está no formato de saudação do `msauth://packagename/Base64UrlencodedSignature`. Você pode obter o RedirectUri para seu aplicativo usando Olá script brokerRedirectPrint.ps1 ou Olá API chamada mContext.getBrokerRedirectUri. assinatura de saudação é tooyour relacionado certificados de assinatura.

modelo de broker atual Olá é para um usuário. AuthenticationContext fornece um usuário de agente de Olá Olá API método tooget.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

O manifesto do aplicativo deve ter Olá contas de AccountManager toouse permissões a seguir. Para obter detalhes, consulte Olá [AccountManager informações no site Android Olá](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>URL da Autoridade e AD FS
Os serviços de Federação do Active Directory (AD FS) não é reconhecido como produção STS, para que você precisa tooturn de descoberta da instância e passe false no construtor de AuthenticationContext hello.

Olá autoridade URL precisa de uma instância de STS e um [nome do locatário](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Consultar itens do cache
A ADAL fornece um cache padrão em SharedPreferences com algumas funções de consulta de cache simples. Você pode obter cache atual de saudação do AuthenticationContext usando:

    ITokenCacheStore cache = mContext.getCache();

Você também pode fornecer a implementação do cache, se você quiser toocustomize-lo.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Comportamento da solicitação
O ADAL fornece um comportamento do prompt toospecify opção. PromptBehavior.Auto mostrará a saudação da interface do usuário se o token de atualização de saudação é inválido e são necessárias credenciais de usuário. PromptBehavior.Always irá ignorar o uso de cache de saudação e sempre mostrar Olá da interface do usuário.

### <a name="silent-token-request-from-cache-and-refresh"></a>Solicitação de token silenciosa do cache e atualização
Uma solicitação de token silenciosa não usa Olá pop-up de interface do usuário e não requer uma atividade. Ele retorna um token de cache hello, se disponível. Se o token Olá tiver expirado, esse método tentará toorefresh-lo. Se o token de atualização de saudação expirou ou falha, ele retornará AuthenticationException.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

Você também pode fazer uma chamada de sincronização com esse método. Você pode definir toocallback nulo ou use acquireTokenSilentSync.

### <a name="diagnostics"></a>Diagnostics
Estas são as Olá principais fontes de informações para diagnosticar problemas:

* Exceções
* Logs
* Rastreamentos de rede

Observe que as IDs de correlação são diagnóstico toohello central na biblioteca de saudação. Você pode definir suas IDs de correlação em uma base por solicitação, se você quiser toocorrelate solicitar uma ADAL com outras operações em seu código. Se você não definir uma ID de correlação, a ADAL gerará uma senha aleatória. Todas as mensagens de log e, em seguida, chamadas de rede serão carimbadas com ID de correlação de saudação. Olá gerado automaticamente ID as alterações em cada solicitação.

#### <a name="exceptions"></a>Exceções
Exceções são Olá primeiro diagnóstico. Tentamos tooprovide mensagens de erro úteis. Se você encontrar uma que não é útil, registre um problema e nos informe. Inclua informações do dispositivo, como modelo e número do SDK.

#### <a name="logs"></a>Logs
Você pode configurar Olá biblioteca toogenerate mensagens de log que você pode usar toohelp diagnosticar problemas. Configurar o log fazendo o seguinte Olá chamar tooconfigure um retorno de chamada que ADAL usará toohand cada mensagem de log gerado.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

As mensagens podem ser gravadas tooa o arquivo de log personalizado, como mostrado na saudação de código a seguir. Infelizmente, não há um modo padrão de obter os logs de um dispositivo. Há alguns serviços que podem ajudá-lo. Você pode também crie seu próprios, como servidor de tooa arquivo hello envio.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Estes são os níveis de log hello:
* Erro (exceções)
* Aviso (aviso)
* Informações (fins informativos)
* Detalhado (mais detalhes)

Você definir o nível de log de saudação assim:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Todas as mensagens de log são enviadas toologcat, em retornos de chamada adição tooany log personalizado.
Você pode obter um arquivo de log tooa de logcat da seguinte maneira:

    adb logcat > "C:\logmsg\logfile.txt"

 Para obter detalhes sobre comandos adb, consulte Olá [logcat informações no site Android Olá](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Rastreamentos de rede
Você pode usar várias ferramentas toocapture Olá tráfego HTTP que gera ADAL.  Isso é mais útil se você estiver familiarizado com hello protocolo OAuth ou se você precisar tooprovide tooMicrosoft de informações de diagnóstico ou outros canais de suporte.

O Fiddler é uma ferramenta de rastreamento de HTTP mais fácil hello. A seguir use Olá links tooset-toocorrectly registro ADAL tráfego de rede. Para uma ferramenta de rastreamento como o Fiddler ou Charles toobe útil, você deve configurá-lo toorecord sem criptografia SSL tráfego.  

> [!NOTE]
> Rastreamentos gerados desta forma podem conter informações altamente privilegiadas como tokens de acesso, nomes de usuário e senhas. Se você estiver usando contas de produção, não compartilhe esses rastreamentos com terceiros. Se você precisar toosupply toosomeone um rastreamento no suporte a ordem tooget, reproduza o problema de saudação usando uma conta temporária com nomes de usuário e senhas que você não se importar de compartilhamento.

* Do site de Telerik Olá: [configuração o Fiddler para Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* Do GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler) (Configurar regras do Fiddler para ADAL)

### <a name="dialog-mode"></a>Modo de caixa de diálogo
método de acquireToken Hello sem atividade dá suporte a um prompt da caixa de diálogo.

### <a name="encryption"></a>Criptografia
ADAL criptografa tokens hello e armazenamento em SharedPreferences por padrão. Você pode ver detalhes de Olá Olá StorageHelper classe toosee. O Android introduziu o Armazenamento de chaves privadas Android KeyStore 4.3 (API 18). A ADAL o utiliza para API18 e superior. Se você quiser toouse ADAL para versões anteriores do SDK, você precisa tooprovide uma chave de segredo AuthenticationSettings.INSTANCE.setSecretKey.

### <a name="oauth2-bearer-challenge"></a>Desafio de portador do Oauth2
Olá AuthenticationParameters classe fornece funcionalidade tooget authorization_uri de saudação desafio de portador de OAuth2.

### <a name="session-cookies-in-webview"></a>Cookies de sessão no Webview
WebView Android não limpar cookies de sessão depois que o aplicativo hello está fechado. Você pode tratar disso usando este exemplo de código:

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Para obter detalhes sobre os cookies, consulte Olá [CookieSyncManager informações no site Android Olá](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Substituições de recurso
Biblioteca da ADAL Olá inclui cadeias de caracteres em inglês de ProgressDialog. Seu aplicativo deve substituí-las se você quiser cadeias de caracteres localizadas.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>Caixa de diálogo NTLM
Versão da ADAL 1.1.0 dá suporte a uma caixa de diálogo NTLM que é processada por meio do evento de onReceivedHttpAuthRequest de saudação do WebViewClient. Você pode personalizar o layout de saudação e cadeias de caracteres para a caixa de diálogo de saudação.

### <a name="cross-app-sso"></a>SSO entre aplicativos
Saiba [como tooenable SSO entre aplicativo no Android usando o ADAL](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
