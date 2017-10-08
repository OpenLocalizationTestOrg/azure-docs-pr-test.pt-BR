---
title: "aaaUser autenticação para aplicativos de API no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como tooprotect um aplicativo de API no serviço de aplicativo do Azure, permitindo acesso tooauthenticated somente usuários."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Autenticação de usuário para Aplicativos de API no Serviço de Aplicativo do Azure
## <a name="overview"></a>Visão geral
Este artigo mostra como um aplicativo de API do Azure para que somente usuários autenticados do tooprotect pode chamá-lo. Olá artigo pressupõe que você leu Olá [visão geral da autenticação do serviço de aplicativo do Azure](../app-service/app-service-authentication-overview.md).

Você aprenderá a:

* Como tooconfigure um provedor de autenticação, com detalhes para o Azure Active Directory (AD do Azure).
* Como tooconsume um aplicativo de API protegido usando Olá [autenticação biblioteca ADAL (Active Directory) para JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

artigo Olá contém duas seções:

* Olá [como tooconfigure de autenticação de usuário no serviço de aplicativo do Azure](#authconfig) seção explica como geral tooconfigure de autenticação de usuário para qualquer aplicativo de API e se aplica igualmente tooall estruturas com suporte pelo serviço de aplicativo, incluindo .NET, Node.js e Java.
* Começando com hello [continuar tutoriais de aplicativos de API .NET Olá](#tutorialstart) seção, Olá guias artigo você pela configuração de um aplicativo de exemplo com um .NET fazer final e um front-end do AngularJS para que ele usa o Active Directory do Azure para usuário autenticação. 

## <a id="authconfig"></a>Como tooconfigure de autenticação de usuário no serviço de aplicativo do Azure
Esta seção fornece instruções gerais que se aplicam a tooany do aplicativo de API. Para etapas específicas toohello tooDo aplicativo de exemplo .NET de lista, vá muito[continuar tutoriais de Introdução .NET de saudação](#tutorialstart).

1. Em Olá [portal do Azure](https://portal.azure.com/), navegar toohello **configurações** folha do aplicativo hello API que você deseja tooprotect, localizar Olá **recursos** seção e, em seguida, clique em  **Autenticação / autorização**.
   
    ![Autenticação/Autorização do portal do Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Em Olá **autenticação / autorização** folha, clique em **em**.
3. Selecione uma das opções de saudação do hello **tootake de ação quando a solicitação não está autenticada** lista suspensa.
   
   * Se você quiser apenas chamadas autenticadas tooreach seu aplicativo de API, escolha uma saudação **fazer login...**  opções. Essa opção permite que você tooprotect Olá API aplicativo sem gravar qualquer código que é executado nele.
   * Se você desejar que todas as chamadas tooreach seu aplicativo de API, escolha **Permitir solicitação (nenhuma ação)**. Você pode usar essa opção de tooa opção toodirect não autenticado chamadores de provedores de autenticação. Com essa opção, você tem autorização de toohandle toowrite código.
     
     Para saber mais, confira [Autenticação e autorização para Aplicativos de API no Serviço de Aplicativo do Azure](app-service-api-authentication.md#multiple-protection-options).
4. Selecione um ou mais Olá **provedores de autenticação**.
   
    imagem de saudação mostra opções que exigem todos os toobe chamadores autenticadas pelo AD do Azure.
   
    ![Folha Autenticação/Autorização do portal do Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Quando você escolher um provedor de autenticação, o portal de saudação exibe uma folha de configuração para o provedor. 
   
    Para obter instruções que explicam como tooconfigure Olá folhas de configuração do provedor de autenticação, consulte [como tooconfigure seu logon de Active Directory do Azure do serviço de aplicativo aplicativo toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (link Olá vai tooan artigo sobre o AD do Azure, mas artigo Olá próprio contém guias que vinculam tooarticles para Olá outros provedores de autenticação).
5. Quando tiver terminado com folha de configuração do provedor de autenticação de saudação, clique em **Okey**.
6. Em Olá **autenticação / autorização** folha, clique em **salvar**.

Quando isso for feito, o serviço de aplicativo autentica todas as chamadas de API antes que elas atinjam o aplicativo de API de saudação. trabalho de serviços de autenticação Olá Olá mesmo para todos os idiomas com suporte do serviço de aplicativo, incluindo .NET, Node.js e Java. 

toomake autenticado chamadas de API, chamador Olá inclui o token de portador OAuth 2.0 do provedor de autenticação Olá no cabeçalho de autorização de saudação de solicitações HTTP. token de saudação pode ser adquirida por meio SDK do provedor de autenticação Olá.

## <a id="tutorialstart"></a>Tutoriais de aplicativos de API .NET Olá continuando
Se você estiver seguindo os tutoriais de saudação Node. js ou Java para aplicativos de API, ignorar toohello próximo artigo, [autenticação principal do serviço para aplicativos de API](app-service-api-dotnet-service-principal-auth.md). 

Se você estiver seguindo a série de tutoriais Olá .NET para aplicativos de API e já implantou o aplicativo de exemplo hello conforme indicado na Olá [primeiro](app-service-api-dotnet-get-started.md) e [segundo](app-service-api-cors-consume-javascript.md) tutoriais, ignorar toohello [configurar autenticação no serviço de aplicativo e o Azure AD](#azureauth) seção.

Se você quiser toofollow neste tutorial, sem passar pelo tutoriais de primeiro e segundo Olá, Olá seguindo as etapas que explicam como tooget iniciado usando um aplicativo de exemplo do processo automatizado toodeploy hello.

> [!NOTE]
> Olá etapas a seguir que você toohello ponto inicial mesmo que você Olá dois primeiros tutoriais, com uma exceção: Visual Studio já não saberá qual aplicativo web ou aplicativo de API que cada projeto é implantado. Isso significa que você não terá as instruções exatas neste tutorial que explicam como toodeploy toohello direita destinos. Se você não estiver familiarizado com a descobrir como as etapas de implantação de saudação toodo por conta própria, é melhor toofollow Olá série de tutoriais de saudação [primeiro tutorial](app-service-api-dotnet-get-started.md) que toostart com essa automatizada o processo de implantação.
> 
> 

1. Certifique-se de que você tem todos os pré-requisitos de saudação listados no hello [primeiro tutorial](app-service-api-dotnet-get-started.md). Adição toohello os pré-requisitos listados, esses tutoriais de autenticação supõem que você tenha trabalhado com aplicativos do serviço de aplicativo web e aplicativos de API no Visual Studio e Olá portal do Azure.
2. Clique em Olá **implantar tooAzure** botão Olá [arquivo Leiame de repositório de exemplo do tooDo lista](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) toodeploy Olá API aplicativos e hello de aplicativo da web. Faça uma anotação hello Azure do grupo de recursos que é criado, porque você pode usar este posterior toolook o aplicativo web e nomes de aplicativo de API.
3. Download ou o clone hello [repositório de exemplo lista tooDo](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) código de saudação tooget que você trabalhará com localmente no Visual Studio.

## <a id="azureauth"></a> Configurar a autenticação no Serviço de Aplicativo e no Azure AD
Agora, você tem um aplicativo hello em execução no serviço de aplicativo do Azure sem a necessidade de que os usuários autenticados. Nesta seção você pode adicionar autenticação fazendo Olá tarefas a seguir:

* Configure a autenticação do serviço de aplicativo toorequire Azure Active Directory (AD do Azure) para chamar o aplicativo de camada intermediária API hello.
* Criar um aplicativo Azure AD.
* Configure o token de portador de Olá Olá AD do Azure aplicativo toosend após logon toohello AngularJS front-end. 

Se você tiver problemas ao tutorial instruções a seguir hello, consulte Olá [solução de problemas](#troubleshooting) seção final Olá tutorial hello. 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>Configurar a autenticação para a camada intermediária de saudação do aplicativo de API
1. Em Olá [portal do Azure](https://portal.azure.com/), navegar toohello **configurações** folha do aplicativo hello API que você criou para o projeto de ToDoListAPI hello, localize Olá **recursos** seção e, em seguida, Clique em **autenticação / autorização**.
   
    ![Autenticação/Autorização do portal do Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Em Olá **autenticação / autorização** folha, clique em **em**.
3. Em Olá **tootake de ação quando a solicitação não está autenticada** lista suspensa, selecione **fazer logon com Active Directory do Azure**.
   
    Essa opção garante que nenhuma solicitação unauathenticated alcançará saudação do aplicativo de API. 
4. Em **Provedores de Autenticação**, clique em **Azure Active Directory**.
   
    ![Folha Autenticação/Autorização do portal do Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Em Olá **configurações do Active Directory do Azure** folha, clique em **Express**
   
    ![Opção Autenticação/Autorização Expressa do portal do Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Com hello **Express** opção, o serviço de aplicativo pode criar automaticamente um aplicativo do AD do Azure no AD do Azure [locatário](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Você não tem toocreate um locatário, porque cada conta do Azure tem uma automaticamente.
6. Em **modo de gerenciamento**, clique em **criar novo aplicativo AD** se ainda não estiver selecionado e observe o valor Olá no hello **criar aplicativo** caixa de texto; você procurará esse AAD aplicativo em Olá portal clássico do Azure posteriormente.
   
    ![Configurações do Azure AD no portal do Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure criará automaticamente um aplicativo do AD do Azure com o nome de saudação indicada em seu locatário do AD do Azure. Por padrão, Olá aplicativo AD do Azure é denominado hello mesmo como o aplicativo hello API. Se preferir, você pode inserir um nome diferente.
7. Clique em **OK**.
8. Em Olá **autenticação / autorização** folha, clique em **salvar**.
   
    ![Clique em Salvar](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Agora apenas os usuários em seu locatário do AD do Azure podem chamar o aplicativo de API de saudação.

### <a name="optional-test-hello-api-app"></a>Opcional: Testar o aplicativo hello API
1. Em um navegador, vá toohello URL do aplicativo hello API: no hello **aplicativo de API** folha em Olá portal do Azure, clique o link de saudação em **URL**.  
   
    Você está a tela de login tooa redirecionado porque as solicitações não autenticadas não são permitidas tooreach saudação do aplicativo de API.
   
    Se seu navegador der página toohello "criado com êxito", já pode estar conectado navegador hello – nesse caso, abra uma janela InPrivate ou Incognito e acesse a URL do aplicativo toohello API.
2. Faça logon usando as credenciais de um usuário no locatário do Azure AD.
   
    Quando você fizer logon, Olá "criado com êxito" página aparece no navegador de saudação.
3. Navegador de saudação fechar.

### <a name="configure-hello-azure-ad-application"></a>Configurar o aplicativo hello AD do Azure
Quando você configurou a autenticação do Azure AD, o Serviço de Aplicativo criou um aplicativo Azure AD para você. Por padrão o aplicativo hello novo AD do Azure foi URL do aplicativo de API toohello token portador tooprovide configurado hello. Nesta seção você configurar Olá AD do Azure aplicativo tooprovide Olá portador token toohello AngularJS front-end em vez de aplicativo de camada intermediária API toohello diretamente. front-end de AngularJS Olá enviará Olá token toohello API do aplicativo quando ele chama o aplicativo de API de saudação.

> [!NOTE]
> processo de saudação tookeep tão simple quanto possível, este tutorial usa um único AD do Azure para o front-end hello e o aplicativo de camada intermediária API hello. Outra opção é toouse dois aplicativos do AD do Azure. Nesse caso, você teria do toogive Olá front-end AD do Azure aplicativo permissão toocall Olá intermediária aplicativo da camada AD do Azure. Essa abordagem de vários aplicativo oferecem maior controle granular sobre a camada de tooeach de permissões.
> 
> 

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), ir muito**Active Directory do Azure**.
   
   Você tem o portal clássico do toouse Olá porque algumas configurações do Active Directory do Azure que você precisa acessar tooare ainda não está disponível no portal do Azure atual de saudação.
2. Em Olá **diretório** , clique em seu locatário do AAD.
   
   ![Azure AD no portal clássico](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Clique em **aplicativos > aplicativos que minha empresa possui**e, em seguida, clique em marca de seleção de saudação.
   
   Você também pode ter toorefresh Olá página toosee Olá novo aplicativo.
4. Na lista de Olá de aplicativos, clique em nome de saudação do hello que Azure criado para você quando você habilitou a autenticação para seu aplicativo de API.
   
   ![Guia Aplicativos Azure AD](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Clique em **Configurar**.
   
   ![Guia Configurar Azure AD](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Definir **URL de logon** toohello URL para seu aplicativo da web do AngularJS, nenhuma barra à direita.
   
   Por exemplo: https://todolistangular.azurewebsites.net
   
   ![URL de logon](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Definir **URL de resposta** toohello URL para seu aplicativo web, nenhuma barra à direita.
   
   Por exemplo: https://todolistsangular.azurewebsites.net
8. Clique em **Salvar**.
   
   ![URL de resposta](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. Final Olá Olá página, clique em **gerenciar manifesto > Download manifesto**.
   
   ![Baixar manifesto](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Baixe tooa local do arquivo de saudação onde você pode editá-lo.
11. No arquivo de manifesto Olá baixado, procure Olá `oauth2AllowImplicitFlow` propriedade. Alterar valor Olá dessa propriedade de `false` muito`true`e, em seguida, salve o arquivo hello.
    
    Essa configuração é necessária para o acesso de um aplicativo de página única de JavaScript. Ele permite Olá Oauth 2.0 portador token toobe retornado no fragmento de URL hello.
12. Clique em **gerenciar manifesto > carregar manifesto**e carregar arquivo hello que você atualizou no hello anterior da etapa.
    
    ![Carregar manifesto](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Saudação de cópia **ID do cliente** valor e salve-o em algum lugar, você poderá obtê-lo de mais tarde.

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>Configurar a autenticação de toouse Olá ToDoListAngular projeto
Nesta seção, você alterar front-end de AngularJS Olá para que ele usa a biblioteca de autenticação do Active Directory (ADAL) para tooacquire JS um token de portador Olá logon do usuário do AD do Azure. código de saudação incluirá token Olá em solicitações HTTP enviadas toohello de camada intermediária, conforme mostrado no diagrama a seguir de saudação. 

![Diagrama de autenticação de usuário](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Verifique Olá toofiles alterações no projeto de ToDoListAngular Olá a seguir.

1. Olá abrir *cshtml* arquivo.
2. Descomente as linhas de saudação que fazem referência a saudação biblioteca de autenticação do Active Directory (ADAL) para scripts JS.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Olá abrir *app/scripts/app.js* arquivo.
4. Comente o bloco de saudação de código marcado para "sem autenticação" e remova o bloco de saudação de código marcado para "autenticação com".
   
    Essa alteração referencia o provedor de autenticação de ADAL JS hello e fornece tooit de valores de configuração. Olá etapas você define valores de configuração Olá para o aplicativo de API e o aplicativo do AD do Azure.
5. No código de saudação que define Olá `endpoints` Olá variável, defina URL da API toohello URL do aplicativo hello API que você criou para o projeto de ToDoListAPI Olá e defina Olá AD do Azure ID toohello cliente ID do aplicativo que você copiou da saudação portal clássico do Azure.
   
    código de saudação agora é semelhante toohello exemplo a seguir.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. Olá chamar muito`adalProvider.init`, defina `tenant` tooyour o nome do locatário e `clientId` toosame valor usado na etapa anterior hello.
   
    código de saudação agora é semelhante toohello exemplo a seguir.
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    Essas alterações muito`app.js` especificar que o código de chamada hello e Olá chamado API estão no aplicativo hello mesmo Azure AD.
7. Olá abrir *app/scripts/homeCtrl.js* arquivo.
8. Comente o bloco de saudação de código marcado para "sem autenticação" e remova o bloco de saudação de código marcado para "autenticação com".
9. Olá abrir *app/scripts/indexCtrl.js* arquivo.
10. Comente o bloco de saudação de código marcado para "sem autenticação" e remova o bloco de saudação de código marcado para "autenticação com".

### <a name="deploy-hello-todolistangular-project-tooazure"></a>Implantar Olá ToDoListAngular projeto tooAzure
1. Em **Solution Explorer**, clique com botão direito Olá ToDoListAngular e, em seguida, clique em **publicar**.
2. Clique em **Publicar**.
   
    Visual Studio implanta o projeto hello e abre URL de base de um navegador toohello aplicativo web. Isso mostrará uma página de 403 erro, que é normal para uma URL base de tentativa toogo tooa API da Web em um navegador.
   
    Você ainda terá toomake uma alteração toohello intermediária do aplicativo de API antes de testar o aplicativo hello.
3. Navegador de saudação fechar.

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>Configurar a autenticação de toouse Olá ToDoListAPI projeto
Olá atualmente envios de projeto ToDoListAPI "*" como Olá `owner` tooToDoListDataAPI de valor. Nesta seção, você alterar Olá código toosend Olá ID de usuário com logon hello.

Verifique Olá após as alterações no projeto de ToDoListAPI hello.

1. Olá abrir *Controllers/ToDoListController.cs* de arquivo e remova os comentários de linha de saudação em cada método de ação que define `owner` toohello AD do Azure `NameIdentifier` valor de declaração. Por exemplo:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Importante**: não remova o código no hello `ToDoListDataAPI` método; você fará isso mais tarde para tutorial de autenticação principal do serviço hello.

### <a name="deploy-hello-todolistapi-project-tooazure"></a>Implantar Olá ToDoListAPI projeto tooAzure
1. Em **Solution Explorer**, clique com botão direito Olá ToDoListAPI e, em seguida, clique em **publicar**.
2. Clique em **Publicar**.
   
    Visual Studio implanta o projeto hello e abre URL de base de um navegador toohello aplicativo de API.
3. Navegador de saudação fechar.

### <a name="test-hello-application"></a>Testar o aplicativo hello
1. Vá toohello URL do aplicativo web de hello, **usando HTTPS, não HTTP**.
2. Clique em Olá **tooDo lista** guia.
   
    Você está toolog solicitada no.
3. Faça logon com credenciais de saudação de um usuário em seu locatário do AAD.
4. Olá **tooDo lista** página será exibida.
   
   ![página de lista de tooDo](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Não são exibidos itens pendentes porque, até agora, todos eles eram para o proprietário "*". Agora camada intermediária hello está solicitando itens para Olá logon do usuário e nenhum foi criado.
5. Adicione novo tooverify de itens de tarefas que o aplicativo hello está funcionando.
6. Em outra janela do navegador, vá toohello URL Swagger de interface do usuário para o aplicativo de API ToDoListDataAPI hello e clique em **ToDoList > obter**. Insira um asterisco para Olá `owner` parâmetro e clique **Experimente**.
   
   resposta de saudação mostra que o novos itens de tarefas pendentes Olá têm ID de usuário Olá real do AD do Azure na propriedade do proprietário hello.
   
   ![ID do proprietário na resposta JSON](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>Compilando projetos de saudação do zero
projetos de API da Web Hello dois foram criados usando Olá **aplicativo de API do Azure** modelo e substituindo controlador de valores padrão de saudação com um controlador de lista de tarefas do projeto. 

Para obter informações sobre como criar também um aplicativo de página única AngularJS com um back-end da Web API 2, consulte [mãos no laboratório: criar um aplicativo de página única (SPA) com a API da Web do ASP.NET e Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Para obter informações sobre como tooadd código de autenticação do AD do Azure, consulte Olá recursos a seguir:

* [Como proteger aplicativos de página única AngularJS com o Azure AD](../active-directory/active-directory-devquickstarts-angular.md).
* [Apresentação da ADAL JS v1](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Solução de problemas
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Não confunda ToDoListAPI (camada intermediária) e ToDoListDataAPI (camada de dados). Por exemplo, verifique se você adicionou o aplicativo de API do autenticação toohello camada intermediária, camada de dados do hello. 
* Certifique-se de que a URL do aplicativo hello API de camada intermediária Olá do referências de código de origem AngularJS (ToDoListAPI, não ToDoListDataAPI) e hello corrigir ID de cliente do AD do Azure. 

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toouse autenticação de serviço de aplicativo para um aplicativo de API e como toocall Olá aplicativo de API usando Olá biblioteca ADAL JS. Olá Avançar tutorial você aprenderá como muito[acesso seguro tooyour API do aplicativo para cenários de serviço a serviço](app-service-api-dotnet-service-principal-auth.md).

