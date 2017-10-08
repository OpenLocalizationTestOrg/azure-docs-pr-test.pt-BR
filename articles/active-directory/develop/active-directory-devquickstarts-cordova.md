---
title: "aaaAzure AD Cordova Introdução | Microsoft Docs"
description: Como toobuild um aplicativo Cordova que se integra ao AD do Azure para entrar e chama as APIs de protegidos pelo AD do Azure usando o OAuth.
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Integrar o AD do Azure com um aplicativo Apache Cordova
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Você pode usar o Apache Cordova toodevelop HTML5/JavaScript aplicativos que podem ser executados em dispositivos móveis, como aplicativos nativos completos. Com o Azure Active Directory (AD do Azure), você pode adicionar empresariais autenticação recursos tooyour Cordova de aplicativos.

Um plug-in do Cordova encapsula os SDKs nativos do Azure AD em iOS, Android, Windows Store e Windows Phone. Usando o que plug-in, você pode aprimorar seu aplicativo toosupport entrar com contas do Active Directory do Windows Server de seus usuários, obter acesso tooOffice 365 e APIs do Azure e até mesmo ajudar a proteger chamadas tooyour próprio personalizado API da web.

Neste tutorial, usaremos Olá Apache Cordova plug-in para a biblioteca de autenticação do Active Directory (ADAL) tooimprove um aplicativo simples adicionando Olá recursos a seguir:

* Com apenas algumas linhas de código, autenticar um usuário e obter um token.
* Use esse tooquery de API do Graph Olá token tooinvoke diretório e exibir resultados de saudação.  
* Usar autenticação de toominimize do cache de token ADAL Olá solicita usuário hello.

toomake esses melhorias, você precisa:

1. Registrar um aplicativo com o Azure AD.
2. Adicione tokens do código tooyour aplicativo toorequest.
3. Adicionar código toouse Olá token para consultar Olá Graph API e exibir os resultados.
4. Criar o projeto de implantação do Cordova Olá com todas as plataformas de saudação desejado tootarget, adicionar Olá plug-in Cordova ADAL e testar a solução de saudação em emuladores.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa:

* Um locatário do Azure AD onde você pode ter uma conta com direitos de desenvolvimento de aplicativo.
* Um ambiente de desenvolvimento que configurou toouse Apache Cordova.  

Se você já tiver configurado, vá diretamente toostep 1.

Se você não tiver um locatário Azure AD, use Olá [obter instruções sobre como tooget uma](active-directory-howto-tenant.md).

Se você não tiver o Apache Cordova configurado no seu computador, instale o seguinte hello:

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org/download/)
* [Cordova CLI](https://cordova.apache.org/) (pode ser facilmente instalado por meio do gerenciador de pacotes NPM: `npm install -g cordova`)

Olá anterior instalações deve funcionar no hello PC e no hello Mac.

Cada plataforma de destino tem pré-requisitos diferentes:

* toobuild e execute um aplicativo Tablet/PC Windows ou Windows Phone:
  * Instale o [Visual Studio 2013 para Windows com Atualização 2 ou superior](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express ou outra versão) ou [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).

* toobuild e executar um aplicativo para iOS:

  * Instale o Xcode 6.x ou posterior. Baixá-lo do hello [site do desenvolvedor Apple](http://developer.apple.com/downloads) ou hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).
  * Instale o [ios-sim](https://www.npmjs.org/package/ios-sim). Você pode usá-lo toostart iOS aplicativos no simulador de iOS da linha de comando hello. (Você pode instalá-lo facilmente por meio de saudação terminal: `npm install -g ios-sim`.)
* toobuild e executar um aplicativo para Android:

  * Instale [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior. Certifique-se de `JAVA_HOME` (variável de ambiente) está configurado corretamente de acordo com o caminho de instalação do JDK toohello (por exemplo, C:\Program Files\Java\jdk1.7.0_75).
  * Instalar [SDK do Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) e adicione Olá `<android-sdk-location>\tools` tooyour local (por exemplo, C:\tools\Android\android-sdk\tools) `PATH` variável de ambiente.
  * Abra o Gerenciador de SDK do Android (por exemplo, via Olá terminal: `android`) e instalar:
    * *Android 5.0.1 (API 21)* SDK de plataforma
    * *Android SDK Build-tools* versão 19.1.0 ou superior
    * *Repositório de suporte do Android* (Extras)

  Olá SDK do Android não fornece qualquer instância do emulador padrão. Criar um executando `android avd` de saudação terminal e, em seguida, selecionando **criar**, se você quiser que o aplicativo do Android Olá toorun em um emulador. Recomendamos um nível de API de 19 ou superior. Para obter mais informações sobre opções de emulador e a criação da Android hello, consulte [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) no site de saudação Android.

## <a name="step-1-register-an-application-with-azure-ad"></a>Etapa 1: registrar um aplicativo com o Azure AD
Esta etapa é opcional. Este tutorial fornece pré-provisionado valores que você pode usar toosee Olá exemplo em ação sem fazer qualquer provisionamento em seu próprio locatário. No entanto, é recomendável que você execute esta etapa e se familiarizar com o processo de Olá, pois ela será necessária quando você cria seus próprios aplicativos.

O Azure AD emite tokens tooonly conhecido de aplicativos. Antes de usar o AD do Azure do seu aplicativo, você precisa toocreate uma entrada para ele no seu locatário. tooregister um novo aplicativo no seu locatário:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta. Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.
5. Siga os prompts de saudação e criar um **aplicativo cliente nativo**. (Embora os aplicativos Cordova sejam baseados em HTML, estamos criando um aplicativo cliente nativo aqui. Olá **aplicativo cliente nativo** opção deve ser selecionada ou aplicativo hello não funcionará.)
  * **Nome** descreve toousers seu aplicativo.
  * **URI de redirecionamento** é hello URI que usou tooreturn tokens tooyour aplicativo. Digite **http://MyDirectorySearcherApp**.

Depois de concluir o registro, o Azure AD atribui a um aplicativo de tooyour de ID de aplicativo único. Você precisará desse valor nas seções próximos hello. Você pode encontrá-lo na guia do aplicativo de saudação do hello aplicativo criado recentemente.

toorun `DirSearchClient Sample`, conceder Olá recém-criado aplicativo permissão tooquery hello Azure AD Graph API:

1. De saudação **configurações** página, selecione **permissões necessárias**e, em seguida, selecione **adicionar**.  
2. Olá aplicativo do Active Directory do Azure, selecione **Microsoft Graph** como Olá API e adicione Olá **acessar o diretório de hello como o usuário conectado Olá** permissão em **delegados Permissões**.  Isso permite que seu Olá tooquery do aplicativo Graph API para os usuários.

## <a name="step-2-clone-hello-sample-app-repository"></a>Etapa 2: Clonar o repositório de aplicativo de exemplo hello
O shell ou a linha de comando, digite Olá comando a seguir:

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>Etapa 3: Criar um aplicativo Cordova de saudação
Há várias maneiras toocreate Cordova aplicativos. Neste tutorial, vamos usar interface de linha de comando Cordova hello (CLI).

1. O shell ou a linha de comando, digite Olá comando a seguir:

        cordova create DirSearchClient

   Esse comando cria a estrutura de pasta de saudação e scaffolding de projeto do Cordova hello.

2. Mova a nova pasta de DirSearchClient toohello:

        cd .\DirSearchClient

3. Copie o conteúdo de saudação do projeto de starter Olá na subpasta de www hello usando um Gerenciador de arquivos ou Olá seguinte comando no shell:

  * Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Adicione lista branca de saudação plug-in. Isso é necessário para chamar hello API do Graph.

        cordova plugin add cordova-plugin-whitelist

5. Adicione todas as plataformas de saudação que você deseja toosupport. toohave um exemplo de funcionamento, você precisa tooexecute pelo menos um dos comandos a seguir de saudação. Observe que você não ser capaz de tooemulate iOS no Windows ou emular Windows em um Mac.

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Adicione hello ADAL para o projeto do Cordova tooyour plug-in:

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>Etapa 4: Adicionar código tooauthenticate usuários e obter tokens do AD do Azure
aplicativo Hello que você está desenvolvendo neste tutorial fornecerá um recurso de pesquisa de diretório simples. usuário Olá pode, em seguida, digite o alias de saudação de qualquer usuário no diretório hello e visualizar alguns atributos básicos. projeto de starter Olá contém a definição de saudação da interface de usuário básica de saudação do aplicativo hello (em www/index.html) e scaffolding Olá que conecta os eventos de aplicativo básico ciclos, associações de interface do usuário e resultados de lógica de exibição (em www/js/index.js). Olá única tarefa para você é tooadd lógica de saudação que implementa as tarefas de identidade.

Olá primeira coisa toodo em seu código é apresentar valores de protocolo de saudação do AD do Azure usa para identificar seu aplicativo e Olá recursos de destino. Esses valores serão usados tooconstruct Olá solicitações de token posteriormente. Inserir saudação seguindo o trecho de código na parte superior de saudação do arquivo de js hello:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

Olá `redirectUri` e `clientId` valores devem corresponder a valores de saudação que descrevem seu aplicativo no AD do Azure. Você pode encontrar os da saudação **configurar** guia Olá portal do Azure, conforme descrito na etapa 1, anteriormente neste tutorial.

> [!NOTE]
> Se você tiver optado por não registrar um novo aplicativo no seu próprio locatário, você pode colar apenas valores hello pré-configurado como está. Você pode ver executando o exemplo hello, embora você sempre deve criar sua própria entrada para os aplicativos que são destinados a produção.

Em seguida, adicione o código de solicitação de token hello. Inserir saudação trecho de código a seguir entre hello `search` e `renderData` definições:

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
Vamos examinar essa função, separando-a em suas duas partes principais.
Este exemplo é projetado toowork com qualquer locatário, conforme toobeing contrário vinculado tooa um determinado. Ele usa hello "/ comum" ponto de extremidade, que permite que Olá usuário tooenter qualquer conta no momento da autenticação e direciona o locatário do hello solicitação toohello qual ele pertence.

Esta primeira parte do método hello inspeciona Olá cache ADAL toosee se um token já está armazenado. Nesse caso, o método hello usa locatários Olá onde token Olá veio para reinicializar ADAL. Isso é necessário tooavoid prompts extras, porque Olá uso de "/ comum" sempre resulta em perguntando Olá usuário tooenter uma nova conta.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
a segunda parte saudação do método hello executa Olá solicitação de token adequado. Olá `acquireTokenSilentAsync` método solicita tooreturn ADAL um token Olá especificado recursos sem mostrar qualquer UX. Que pode acontecer se o cache Olá já tem um token de acesso adequado armazenado, ou se um token de atualização pode ser usado tooget um novo token de acesso sem mostrar qualquer prompt. Se essa tentativa falhar, podemos voltar aos `acquireTokenAsync`– que solicitará visivelmente Olá tooauthenticate de usuário.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
Agora que temos token hello, podemos finalmente invocar Olá API do Graph e executar a consulta de pesquisa de saudação que queremos. Inserir saudação seguindo o trecho abaixo Olá `authenticate` definição:

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
arquivos de ponto inicial de saudação fornecido um simple UX para inserir o alias do usuário na caixa de texto. Esse método usará esse valor tooconstruct uma consulta, combiná-lo com o token de acesso do hello, enviá-lo tooMicrosoft gráfico e analisar os resultados de saudação. Olá `renderData` método, já está presente no arquivo de ponto inicial de hello, cuida de visualizar os resultados de saudação.

## <a name="step-5-run-hello-app"></a>Etapa 5: Executar aplicativo hello
Seu aplicativo é toorun finalmente pronto. Operacional ele é simple: quando o aplicativo hello é iniciado, insira o alias de saudação do usuário Olá desejar toolook e clique em botão de saudação. Será solicitada a sua autenticação. Após a autenticação bem-sucedida e pesquisa bem-sucedida, atributos de saudação do usuário Olá pesquisado são exibidos.

As execuções subsequentes executará Olá pesquisa sem mostrar qualquer prompt, graças toohello presença Olá anteriormente adquirido token em cache.

etapas de concreto Olá para executar o aplicativo hello variam por plataforma.

### <a name="windows-10"></a>Windows 10
   Tablet/computador: `cordova run windows --archs=x64 -- --appx=uap`

   Dispositivos móveis (requer um dispositivo conectado de Windows 10 Mobile tooa PC):`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > Durante a saudação executado pela primeira vez, você pode ser solicitado toosign em uma licença de desenvolvedor. Para mais informações, consulte [Licença de desenvolvedor](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-81-tabletpc"></a>Tablet/computador Windows 8.1
   `cordova run windows`

   > [!NOTE]
   > Durante a saudação executado pela primeira vez, você pode ser solicitado toosign em uma licença de desenvolvedor. Para mais informações, consulte [Licença de desenvolvedor](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-phone-81"></a>Windows Phone 8,1
   toorun em um dispositivo conectado:`cordova run windows --device -- --phone`

   toorun no emulador do saudação padrão:`cordova emulate windows -- --phone`

   Use `cordova run windows --list -- --phone` toosee todos os destinos disponíveis e `cordova run windows --target=<target_name> -- --phone` toorun aplicativo de hello em um determinado dispositivo ou emulador (por exemplo, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   toorun em um dispositivo conectado:`cordova run android --device`

   toorun no emulador do saudação padrão:`cordova emulate android`

   Verifique se que você criou uma instância do emulador usando o Gerenciador de AVD, conforme descrito anteriormente na seção "Pré-requisitos" de saudação.

   Use `cordova run android --list` toosee todos os destinos disponíveis e `cordova run android --target=<target_name>` toorun aplicativo de hello em um determinado dispositivo ou emulador (por exemplo, `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   toorun em um dispositivo conectado:`cordova run ios --device`

   toorun no emulador do saudação padrão:`cordova emulate ios`

   > [!NOTE]
   > Verifique se você tem Olá `ios-sim` toorun pacote instalado no emulador de saudação. Para obter mais informações, consulte hello "pré-requisitos" seção.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>Próximas etapas
Para referência, o exemplo hello concluída (sem os valores de configuração) está disponível em [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).

Você pode agora cenários de movimentação em toomore avançado (e mais interessante). Talvez você queira tootry: [proteger uma API da Web Node. js com o Azure AD](active-directory-devquickstarts-webapi-nodejs.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
