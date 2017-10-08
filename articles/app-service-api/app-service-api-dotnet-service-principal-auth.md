---
title: "a autenticação principal aaaService para aplicativos de API no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como aplicativo tooprotect uma API no serviço de aplicativo do Azure para cenários de serviços."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Autenticação de entidade de serviço para Aplicativos de API no Serviço de Aplicativo do Azure
## <a name="overview"></a>Visão geral
Este artigo explica como autenticação de serviço de aplicativo toouse para *interno* acessar aplicativos tooAPI. Um cenário interno é onde você tem um aplicativo de API que você deseja toobe consumível somente por seu próprio código de aplicativo. Olá recomendado tooimplement de maneira esse cenário no serviço de aplicativo é toouse AD do Azure tooprotect Olá chamado aplicativo de API. Chamar o aplicativo de API Olá protegido com um token de portador que você obtém do AD do Azure, fornecendo credenciais (entidade de serviço) a identidade do aplicativo. Para alternativas toousing AD do Azure, consulte Olá **autenticação de serviço a serviço** seção Olá [visão geral da autenticação do serviço de aplicativo do Azure](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

Neste artigo, você aprenderá o seguinte:

* Como toouse aplicativo de tooprotect uma API do Azure Active Directory (AD do Azure) de acesso não autenticado.
* Como aplicativo tooconsume uma API protegida de um aplicativo de API, aplicativo web ou aplicativo móvel usando credenciais de entidade de segurança (identidade de aplicativo) de serviço do AD do Azure. Para obter informações sobre como tooconsume de um aplicativo de lógica, consulte [usando sua API personalizada hospedado no serviço de aplicativo com aplicativos lógicos](../logic-apps/logic-apps-custom-hosted-api.md).
* Como toomake-se de que Olá protegido do aplicativo de API não pode ser chamado em um navegador, usuários conectados.
* Como toomake-se de que Olá protegido do aplicativo de API só pode ser chamado por uma determinada entidade de serviço do AD do Azure.

artigo Olá contém duas seções:

* Olá [como tooconfigure serviço principal autenticação no serviço de aplicativo do Azure](#authconfig) seção explica como geral tooconfigure autenticação para qualquer aplicativo de API e como tooconsume Olá protegido do aplicativo de API. Esta seção se aplica igualmente tooall estruturas com suporte pelo serviço de aplicativo, incluindo .NET, Node.js e Java.
* Começando com hello [continuar tutoriais de Introdução .NET de saudação](#tutorialstart) seção, Olá tutorial orienta você pela configuração de um cenário de "acesso interno" para um aplicativo de exemplo .NET em execução no serviço de aplicativo. 

## <a id="authconfig"></a>Como tooconfigure serviço principal autenticação no serviço de aplicativo do Azure
Esta seção fornece instruções gerais que se aplicam a tooany do aplicativo de API. Para etapas específicas toohello tooDo aplicativo de exemplo .NET de lista, vá muito[continuar a série de tutoriais de aplicativos de API .NET Olá](#tutorialstart).

1. Em Olá [portal do Azure](https://portal.azure.com/), navegar toohello **configurações** folha do aplicativo hello API que você deseja tooprotect e, em seguida, localize Olá **recursos** seção e clique em **Autenticação / autorização**.
   
    ![Autenticação/Autorização no portal do Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Em Olá **autenticação / autorização** folha, clique em **em**.
3. Em Olá **tootake de ação quando a solicitação não está autenticada** lista suspensa, selecione **fazer logon com Active Directory do Azure** .
4. Em **Provedores de Autenticação**, selecione **Azure Active Directory**.
   
    ![Folha Autenticação/Autorização no portal do Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Configurar Olá **configurações do Active Directory do Azure** toocreate folha Azure um novo aplicativo do AD, ou usar um aplicativo existente do AD do Azure se você já tiver um que você deseja toouse.
   
    Cenários internos normalmente envolvem um aplicativo de API que chama um aplicativo de API. Você pode usar aplicativos do Azure AD separados para cada aplicativo de API ou apenas um aplicativo Azure AD.
   
    Para obter instruções detalhadas sobre esta folha, consulte [como tooconfigure seu logon de Active Directory do Azure do serviço de aplicativo aplicativo toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Quando tiver terminado com folha de configuração do provedor de autenticação de saudação, clique em **Okey**.
7. Em Olá **autenticação / autorização** folha, clique em **salvar**.
   
    ![Clique em Salvar](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Quando isso for feito, o serviço de aplicativo só permite solicitações de chamadores em locatário do AD do Azure Olá configurado. Nenhum código de autorização ou autenticação é necessária no aplicativo de API Olá protegido. Olá token de portador é passada toohello API aplicativo junto com as declarações usadas em cabeçalhos HTTP, e você pode ler as informações no código toovalidate que solicitações são de um chamador específico, como uma entidade de serviço.

Essa funcionalidade de autenticação funciona Olá mesma maneira para todos os idiomas do serviço de aplicativo que oferece suporte, incluindo .NET, Node.js e Java. 

#### <a name="how-tooconsume-hello-protected-api-app"></a>Como tooconsume Olá protegido do aplicativo de API
chamador Olá deve fornecer um token de portador do AD do Azure com chamadas de API. tooget um token de portador usando credenciais de serviço principal, o chamador de saudação usa a biblioteca de autenticação do Active Directory (ADAL para [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), ou [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). tooget um token, código de saudação que chama o ADAL fornece Olá tooADAL informações a seguir:

* nome de saudação do seu locatário do AD do Azure.
* Olá ID e o cliente segredo do cliente (chave de aplicativo) do aplicativo de saudação do AD do Azure associado chamador hello.
* Olá ID do cliente de aplicativo do AD do Azure associado à saudação do hello protegido do aplicativo de API. (Se apenas um aplicativo do AD do Azure for usado, isso é Olá mesma ID de cliente como Olá um chamador hello.)

Esses valores estão disponíveis nas páginas de saudação do AD do Azure do hello [portal clássico do Azure](https://manage.windowsazure.com/).

Depois que o token Olá foi adquirido, chamador Olá inclui com solicitações HTTP no cabeçalho de autorização de saudação.  Serviço de aplicativo valida o token hello e permite Olá Olá de tooreach solicitações protegido do aplicativo de API.

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>Como tooprotect Olá API aplicativo contra o acesso por usuários em Olá mesmo locatário
Os tokens de portador para usuários em Olá mesmo locatário são considerados válidos para Olá protegido do aplicativo de API.  Se você quiser tooensure apenas uma entidade de serviço pode chamar hello protegido do aplicativo de API, adicione o código em Olá protegido saudação de toovalidate de aplicativo de API declarações do token Olá a seguir:

* `appid`deve ser o ID de cliente de saudação do aplicativo do AD do Azure Olá que está associado ao chamador hello. 
* `oid`(`objectidentifier`) deve ser o ID principal do serviço de saudação do chamador hello. 

Serviço de aplicativo também fornece Olá `objectidentifier` declaração no cabeçalho X-MS-CLIENT--ID do PRINCIPAL de saudação.

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>Como tooprotect Olá aplicativo de API de acesso do navegador
Se você não validar declarações em código no aplicativo de API Olá protegido e se você usar um separado aplicativo AD do Azure para Olá protegido aplicativo de API, certifique-se de que Olá URL de resposta do aplicativo do AD do Azure é não Olá mesmo Olá URL base do aplicativo de API. Se Olá URL de resposta aponta diretamente do aplicativo de API toohello protegido, um usuário no locatário Olá mesmo Azure AD pode procurar o aplicativo de API toohello, logon e chamar com êxito Olá API.

## <a id="tutorialstart"></a>Continuando a série de tutoriais Olá aplicativos de API do .NET
Se você estiver seguindo Olá Node. js ou Java série de tutoriais para aplicativos de API, ignorar toohello [próximas etapas](#next-steps) seção. 

Olá restante deste artigo continua a série de tutoriais Olá aplicativos de API do .NET e pressupõe que você tenha concluído Olá [tutorial de autenticação de usuário](app-service-api-dotnet-user-principal-auth.md) e ter o aplicativo de exemplo hello em execução no Azure com autenticação do usuário habilitado.

## <a name="set-up-authentication-in-azure"></a>Configurar a autenticação no Azure
Nesta seção você configurar o serviço de aplicativo para que solicitações de HTTP só permite que o aplicativo de API do tooreach Olá dados da camada de saudação são Olá aqueles que têm válida do Azure tokens de portador de AD. 

Em Olá seção a seguir, você configurar credenciais Olá camada intermediária API aplicativo toosend aplicativo tooAzure AD, obter um token de portador e envia portador Olá token toohello aplicativo de API de camada de dados. Esse processo é ilustrado no diagrama de saudação.

![Diagrama do serviço de autenticação](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Se você tiver problemas ao tutorial instruções a seguir hello, consulte Olá [solução de problemas](#troubleshooting) seção final Olá tutorial hello. 

1. Em Olá [portal do Azure](https://portal.azure.com/), navegar toohello **configurações** folha Olá API do aplicativo de que você criou para o aplicativo de API do hello ToDoListDataAPI (camada de dados) e, em seguida, clique em **configurações**.
2. Em Olá **configurações** folha, localizar Olá **recursos** seção e, em seguida, clique em **autenticação / autorização**.
   
    ![Autenticação/Autorização no portal do Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. Em Olá **autenticação / autorização** folha, clique em **em**.
4. Em Olá **tootake de ação quando a solicitação não está autenticada** lista suspensa, selecione **fazer logon com Active Directory do Azure**.
   
    Essa é a configuração de saudação que faz com que o serviço de aplicativo tooensure que autenticou somente solicitações alcance saudação do aplicativo de API. Para solicitações com tokens de portador válido, o serviço de aplicativo passa tokens Olá ao longo do aplicativo toohello API e preenche os cabeçalhos HTTP com declarações usadas toomake essas informações código tooyour mais facilmente disponíveis.
5. Em **Provedores de Autenticação**, clique em **Azure Active Directory**.
   
    ![Folha Autenticação/Autorização no portal do Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. Em Olá **configurações do Active Directory do Azure** folha, clique em **Express**.
   
    Com hello **Express** opção Azure pode criar um aplicativo AAD automaticamente no AD do Azure [locatário](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    Você não tem toocreate um locatário, porque cada conta do Azure tem uma automaticamente.
7. Em **Modo de gerenciamento**, clique em **Criar novo aplicativo do AD** se ainda não estiver selecionado.
   
    conecta-se portal Olá Olá **criar aplicativo** caixa de entrada com um valor padrão. Por padrão, Olá aplicativo AD do Azure é denominado hello mesmo como o aplicativo hello API. Se preferir, você pode inserir um nome diferente.
   
    ![Configurações do Azure AD](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Observação**: como alternativa, você pode usar o Azure AD um único aplicativo para ambos Olá chamado aplicativo de API e Olá protegido do aplicativo de API. Se você escolher essa alternativa, você não precisará Olá **criar novo aplicativo AD** opção aqui porque você já criou um aplicativo do AD do Azure anteriormente no tutorial de autenticação de usuário hello. Para este tutorial, você usará separar aplicativos do Azure AD para Olá chamando o aplicativo de API e hello protegido do aplicativo de API.
8. Anote Olá valor Olá **criar aplicativo** caixa de entrada; você verá esse aplicativo AAD no hello portal clássico do Azure posteriormente.
9. Clique em **OK**.
10. Em Olá **autenticação / autorização** folha, clique em **salvar**.
    
    ![Clique em Salvar](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    Serviço de aplicativo cria um aplicativo do Active Directory do Azure com **URL de logon** e **URL de resposta** definir automaticamente a URL de toohello do seu aplicativo de API. último valor de saudação permite aos usuários em sua toolog de locatário do AAD no e aplicativo de API de saudação do access.

### <a name="verify-that-hello-api-app-is-protected"></a>Verifique se que o aplicativo hello API está protegido
1. Em um navegador, vá toohello URL do aplicativo hello API: no hello **aplicativo de API** folha em Olá portal do Azure, clique o link de saudação em **URL**. 
   
    Você está a tela de login tooa redirecionado porque as solicitações não autenticadas não são permitidas tooreach saudação do aplicativo de API. 
   
    Se seu navegador vá toohello Swagger da interface do usuário, seu navegador já pode estar conectado – nesse caso, abra uma janela InPrivate ou Incognito e vá toohello URL Swagger de interface do usuário.
2. Faça logon com as credenciais de um usuário em seu locatário do AAD.
   
   Quando você fizer logon, Olá "criado com êxito" página aparece no navegador de saudação.

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Configurar Olá ToDoListAPI projeto tooacquire e enviar o token do AD do Azure Olá
Nesta seção você Olá seguintes tarefas:

* Adicione o código no aplicativo de API de camada intermediária Olá que usa o AD do Azure aplicativo credenciais tooacquire um token e enviar solicitações com HTTP toohello aplicativo de API de camada de dados.
* Obtenha as credenciais de saudação que precisar do AD do Azure.
* Insira as credenciais de saudação em configurações de ambiente de tempo de execução do serviço de aplicativo do Azure na camada intermediária de saudação do aplicativo de API. 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Configurar Olá ToDoListAPI projeto tooacquire e enviar o token do AD do Azure Olá
Verifique Olá após as alterações no projeto de ToDoListAPI Olá no Visual Studio.

1. Remova todo o código de saudação em Olá *ServicePrincipal.cs* arquivo.
   
    Esse é o código de saudação que usa ADAL para o token de portador .NET tooacquire Olá AD do Azure.  Ele usa vários valores de configuração que você definir no ambiente de tempo de execução do Azure hello mais tarde. Aqui está o código de saudação: 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **Observação:** esse código requer Olá ADAL para o pacote do NuGet do .NET (ActiveDirectory), que já está instalado no projeto de saudação. Se você criar este projeto do zero, você teria tooinstall este pacote. Este pacote não é instalado automaticamente pelo modelo de novo projeto de aplicativo de API de saudação.
2. Em *controladores/ToDoListController*, remova os comentários de código Olá Olá `NewDataAPIClient` método que adiciona solicitações de token tooHTTP Olá no cabeçalho de autorização de saudação.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Implante Olá ToDoListAPI projeto. (Clique com botão direito hello, clique em **publicar > publicar**.)
   
    Visual Studio implanta o projeto hello e abre URL de base de um navegador toohello aplicativo web. Isso mostrará uma página de 403 erro, que é normal para uma URL base de tentativa toogo tooa API da Web em um navegador.
4. Navegador de saudação fechar.

### <a name="get-azure-ad-configuration-values"></a>Obter valores de configuração do Azure AD
1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), ir muito**Active Directory do Azure**.
2. Em Olá **diretório** , clique em seu locatário do AAD.
3. Clique em **aplicativos > aplicativos que minha empresa possui**e, em seguida, clique em marca de seleção de saudação.
4. Na lista de Olá de aplicativos, clique em nome de saudação do hello que Azure criado para você quando você habilitou a autenticação para aplicativo de API do hello ToDoListDataAPI (camada de dados).
5. Clique em Olá **configurar** guia.
6. Saudação de cópia **ID do cliente** valor e salve-o em algum ponto, você poderá obtê-lo de mais tarde. 
7. No portal clássico do Azure de saudação volte lista toohello de **aplicativos que minha empresa possui**e clique em aplicativo AAD hello que você criou para o aplicativo ToDoListAPI API de camada intermediária hello (Olá um criado no tutorial anterior de saudação, não Olá um criado por você neste tutorial).
8. Clique em Olá **configurar** guia.
9. Saudação de cópia **ID do cliente** valor e salve-o em algum ponto, você poderá obtê-lo de mais tarde.
10. Em **chaves**, selecione **1 ano** de saudação **selecionar duração** lista suspensa.
11. Clique em **Salvar**.
    
     ![Gerar chave do aplicativo](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Copie o valor da chave hello e salve-o em algum ponto, que você poderá obtê-lo de mais tarde.
    
     ![Copiar a nova chave do aplicativo](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>Configurar o AD do Azure no ambiente de tempo de execução do aplicativo de camada intermediária API Olá
1. Vá toohello [portal do Azure](https://portal.azure.com/)e, em seguida, navegue toohello **API App** folha para o aplicativo hello API que hospeda o projeto do hello TodoListAPI (camada intermediária).
2. Clique em **Configurações > Configurações do Aplicativo**.
3. Em Olá **configurações do aplicativo** seção, adicione Olá seguindo as chaves e valores:
   
   | **Chave** | ida:Authority |
   | --- | --- |
   | **Valor** |https://login.microsoftonline.com/{your Azure AD tenant name} |
   | **Exemplo** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Chave** | ida:ClientId |
   | --- | --- |
   | **Valor** |ID do cliente da saudação (camada intermediária - ToDoListAPI) do aplicativo de chamada |
   | **Exemplo** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Chave** | ida:ClientSecret |
   | --- | --- |
   | **Valor** |Chave de aplicativo da saudação (camada intermediária - ToDoListAPI) do aplicativo de chamada |
   | **Exemplo** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Chave** | ida:Resource |
   | --- | --- |
   | **Valor** |ID do cliente do hello chamado de aplicativo (camada de dados - ToDoListDataAPI) |
   | **Exemplo** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Observação**: para `ida:Resource`, certifique-se de usar o hello chamado do aplicativo **ID do cliente** e não seu **URI da ID do aplicativo**.
   
    `ida:ClientId`e `ida:Resource` são diferentes valores para este tutorial, porque você está usando, separe applicaations do AD do Azure para a camada intermediária hello e camada de dados. Se você estiver usando um único aplicativo do AD do Azure para Olá chamando o aplicativo de API e hello protegido do aplicativo de API, você usaria Olá mesmo valor em ambos os `ida:ClientId` e `ida:Resource`.
   
    código de Olá usa ConfigurationManager tooget esses valores, portanto pode ser armazenados no arquivo de Web. config do projeto hello ou no ambiente de tempo de execução do Azure hello. Enquanto um aplicativo do ASP.NET é executado no Serviço de Aplicativo do Azure, as configurações de ambiente automaticamente substituem as configurações de Web.config. Configurações de ambiente são geralmente uma [mais seguras informações confidenciais toostore de maneira com tooa. config](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Clique em **Salvar**.
   
    ![Clique em Salvar](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>Testar o aplicativo hello
1. Em um navegador, vá toohello HTTPS URL do aplicativo de web de front-end Olá AngularJS.
2. Clique em Olá **tooDo lista** guia e faça logon com credenciais de um usuário no seu locatário do AD do Azure. 
3. Adicione tooverify de itens de tarefas que o aplicativo hello está funcionando.
   
    ![página de lista de tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Se o aplicativo hello não funcionar conforme o esperado, verifique novamente todas as configurações de saudação inserido no hello portal do Azure. Se todas as configurações de saudação aparecem toobe correto, consulte Olá [solução de problemas](#troubleshooting) seção mais adiante neste tutorial.

## <a name="protect-hello-api-app-from-browser-access"></a>Proteger a saudação do aplicativo de API de acesso do navegador
Para este tutorial, você criou um separado aplicativo AD do Azure para o aplicativo hello API ToDoListDataAPI (camada de dados). Como você viu, quando o serviço de aplicativo cria um aplicativo AAD, ele configura o aplicativo de AAD saudação de forma que permite que URL de um usuário toogo toohello aplicativo de API em um navegador e o log em. Isso significa que é possível que um usuário final em seu locatário do AD do Azure, não apenas uma entidade de serviço, tooaccess Olá API. 

Se você quiser acesso do navegador tooprevent sem gravar qualquer código no hello protegidos do aplicativo de API, você pode alterar Olá **URL de resposta** em Olá aplicativo AAD para que seja diferente do aplicativo hello API URL de base. 

### <a name="disable-browser-access"></a>Desabilitar o acesso do navegador
1. No portal clássico hello **configurar** para aplicativo AAD hello que foi criado para Olá TodoListService, altere o valor Olá Olá **URL de resposta** campo para que seja uma URL válida, mas não Olá API do aplicativo URL.
2. Clique em **Salvar**.

### <a name="verify-browser-access-no-longer-works"></a>Verificar se o acesso de navegador não funciona mais
Anteriormente, você verificou que você pode ir toohello URL do aplicativo de API de um navegador, faça logon com credenciais de um usuário individual. Nesta seção, você verá que isso não é mais possível. 

1. Em uma nova janela do navegador, vá toohello URL do aplicativo de API Olá novamente.
2. Log quando for solicitado para toodo.
3. Logon for bem-sucedido, mas leva tooan página de erro.
   
    Você configurou o aplicativo do AAD Olá para que os usuários no locatário do AAD Olá não podem entrar e acessar Olá API em um navegador. Você ainda pode acessar o aplicativo de API Olá usando um token da entidade do serviço, que você pode verificar indo URL do aplicativo da web toohello e adicionar mais itens de tarefas pendentes.

## <a name="restrict-access-tooa-particular-service-principal"></a>Restringir a entidade de serviço específico de tooa de acesso
Agora, qualquer chamador que pode obter um token para um usuário ou entidade de serviço em seu locatário do AD do Azure pode chamar o aplicativo hello API TodoListDataAPI (camada de dados). Talvez você queira toomake-se de que aplicativo de API Olá da camada de dados só aceita chamadas de aplicativo de API do hello TodoListAPI (camada intermediária) e somente de uma entidade de serviço específico. 

Você pode adicionar essas restrições com a adição de saudação do código toovalidate `appid` e `objectidentifier` declarações em chamadas de entrada.

Neste tutorial você colocar o código de saudação que valida a ID do aplicativo e a ID principal serviço diretamente em suas ações do controlador.  Alternativas são toouse um personalizado `Authorize` atributo ou toodo essa validação nas sequências de inicialização (por exemplo, o middleware OWIN). Para obter um exemplo de hello último, consulte [este aplicativo de exemplo](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Verifique Olá projeto de TodoListDataAPI toohello alterações a seguir.

1. Olá abrir *Controllers/TodoListController.cs* arquivo.
2. Descomente as linhas de saudação que definam `trustedCallerClientId` e `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Remova os comentários de código Olá Olá CheckCallerId método. Este método é chamado no início de saudação de cada método de ação no controlador de saudação. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. Reimplante Olá ToDoListDataAPI projeto tooAzure do serviço de aplicativo.
5. Em seu navegador, vá HTTPS URL do aplicativo do toohello AngularJS front-end da web e clique em Ajuda na home page do hello Olá **tooDo lista** guia.
   
    aplicativo Hello não funciona porque falha em chamadas toohello volta terminar. novo código de saudação está verificando appid real e objectidentifier mas ele ainda não tem Olá valores corretos toocheck-las com. navegador de saudação Console de ferramentas de desenvolvedor relata que servidor hello está retornando um erro HTTP 401.
   
    ![Erro no Console de Ferramentas de Desenvolvedor](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    Olá etapas a seguir, você configura valores esperados de saudação.
6. Usando o PowerShell do AD do Azure, obter valor de saudação do serviço de saudação principal Olá aplicativo AD do Azure que você criou para o projeto de TodoListWebApp hello.
   
    a. Para obter instruções sobre como tooinstall PowerShell do Azure e conecte-se a assinatura de tooyour, consulte [usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md).
   
    b. tooget uma lista de entidades de serviço, execute Olá `Login-AzureRmAccount` de comando e, em seguida, Olá `Get-AzureRmADServicePrincipal` comando.
   
    c. Localizar objectid Olá para Olá entidade de serviço de aplicativo de TodoListAPI hello e salvá-lo em um local que você pode copiar de mais tarde.
7. No portal do Azure de Olá, navegue toohello folha de API do aplicativo para o aplicativo de API Olá que você implantou o projeto ToDoListDataAPI Olá.
8. Clique em **Configurações > Configurações do Aplicativo**.
9. Em Olá **configurações do aplicativo** seção, adicione Olá seguindo as chaves e valores:
   
   | **Chave** | todo:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Valor** |Id da entidade de serviço do aplicativo de chamada |
   | **Exemplo** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Chave** | todo:TrustedCallerClientId |
   | --- | --- |
   | **Valor** |ID do cliente da chamada de aplicativo - copiado do aplicativo do hello TodoListAPI AD do Azure |
   | **Exemplo** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Clique em **Salvar**.
    
     ![Clique em Salvar](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. No navegador, retornar o URL do aplicativo da web de toohello e, em seguida, clique em Ajuda na home page do Olá Olá **tooDo lista** guia.
    
     Este aplicativo de saudação do tempo funciona conforme o esperado porque Olá chamador confiável app ID e a ID de entidade de serviço Olá esperado de valores.
    
     ![página de lista de tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>Compilando projetos de saudação do zero
projetos de API da Web Hello dois foram criados usando Olá **aplicativo de API do Azure** modelo e substituindo controlador de valores padrão de saudação com um controlador de lista de tarefas do projeto. Para aquisição de tokens de entidade de serviço do AD do Azure no projeto de ToDoListAPI Olá, Olá [autenticação biblioteca ADAL (Active Directory) para .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet package foi instalado.

Para obter informações sobre como criar muito um aplicativo de página única AngularJS com um back-end de API da Web como ToDoListAngular, consulte [mãos no laboratório: criar um aplicativo de página única (SPA) com a API da Web do ASP.NET e Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Para obter informações sobre como tooadd código de autenticação do AD do Azure, consulte [protegendo AngularJS única página de aplicativos com o Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Solucionar problemas
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Não confunda ToDoListAPI (camada intermediária) e ToDoListDataAPI (camada de dados). Por exemplo, neste tutorial, você adicionar autenticação toohello dados da camada aplicativo de API, **mas chave do aplicativo hello deve vir do hello aplicativo AD do Azure que você criou para o aplicativo de camada intermediária API Olá**.

## <a name="next-steps"></a>Próximas etapas
Este é o último tutorial Olá Olá série de aplicativos de API. 

Para obter mais informações sobre o Active Directory do Azure, consulte Olá recursos a seguir.

* [Guia dos desenvolvedores do AD do Azure](http://aka.ms/aaddev)
* [Cenários do AD do Azure](http://aka.ms/aadscenarios)
* [Exemplos do AD do Azure](http://aka.ms/aadsamples)
  
    Olá [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) exemplo é semelhante toowhat é mostrado neste tutorial, mas sem usar autenticação do serviço de aplicativo.

Para obter informações sobre outras maneiras toodeploy Visual Studio projetos tooAPI aplicativos, usando o Visual Studio ou [automatizar a implantação](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) de um [sistema de controle de origem](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), consulte [como toodeploy um Aplicativo de serviço de aplicativo do Azure](../app-service-web/web-sites-deploy.md).

