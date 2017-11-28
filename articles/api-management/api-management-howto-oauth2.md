---
title: contas de desenvolvedor aaaAuthorize usando OAuth 2.0 no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como usuários tooauthorize usando OAuth 2.0 no gerenciamento de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="d5147-103">Como desenvolvedor de tooauthorize contas usando OAuth 2.0 no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="d5147-103">How tooauthorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="d5147-104">Suportam a várias APIs [OAuth 2.0](http://oauth.net/2/) toosecure Olá API e certifique-se de que apenas usuários válidos tenham acesso, e eles podem acessar apenas os recursos toowhich que estão qualificado.</span><span class="sxs-lookup"><span data-stu-id="d5147-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) toosecure hello API and ensure that only valid users have access, and they can only access resources toowhich they're entitled.</span></span> <span data-ttu-id="d5147-105">No Console de desenvolvedor de interativo do gerenciamento de API do Azure toouse ordem, com essas APIs, Olá serviço permite que você tooconfigure sua toowork de instância de serviço com o OAuth 2.0 habilitado API.</span><span class="sxs-lookup"><span data-stu-id="d5147-105">In order toouse Azure API Management's interactive Developer Console with such APIs, hello service allows you tooconfigure your service instance toowork with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="d5147-106"><a name="prerequisites"> </a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d5147-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="d5147-107">Este guia mostra como tooconfigure seu toouse de instância de serviço de gerenciamento de API autorização do OAuth 2.0 para desenvolvedor de contas, mas não mostram como provedor tooconfigure an OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d5147-107">This guide shows you how tooconfigure your API Management service instance toouse OAuth 2.0 authorization for developer accounts, but does not show you how tooconfigure an OAuth 2.0 provider.</span></span> <span data-ttu-id="d5147-108">configuração de saudação para cada provedor é diferente, embora Olá etapas são semelhantes, e Olá necessárias informações usadas na configuração OAuth 2.0 em sua instância de serviço de gerenciamento de API do OAuth 2.0 Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="d5147-108">hello configuration for each OAuth 2.0 provider is different, although hello steps are similar, and hello required pieces of information used in configuring OAuth 2.0 in your API Management service instance are hello same.</span></span> <span data-ttu-id="d5147-109">Este tópico mostra exemplos ao usar o Active Directory do Azure como um provedor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d5147-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="d5147-110">Para obter mais informações sobre como configurar o OAuth 2.0 usando o Active Directory do Azure, consulte Olá [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] exemplo.</span><span class="sxs-lookup"><span data-stu-id="d5147-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see hello [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="d5147-111"><a name="step1"> </a>Configurar um servidor de autorização do OAuth 2.0 no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="d5147-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="d5147-112">tooget iniciado, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="d5147-112">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal do editor][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="d5147-114">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="d5147-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="d5147-115">Clique em **segurança** de saudação **gerenciamento de API** menu da esquerda, clique em de saudação **OAuth 2.0**e, em seguida, clique em **Adicionar servidor de autorização**.</span><span class="sxs-lookup"><span data-stu-id="d5147-115">Click **Security** from hello **API Management** menu on hello left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="d5147-117">Depois de clicar em **Adicionar servidor de autorização**, Olá novo formulário de servidor de autorização é exibido.</span><span class="sxs-lookup"><span data-stu-id="d5147-117">After clicking **Add authorization server**, hello new authorization server form is displayed.</span></span>

![Novo servidor][api-management-oauth2-server-1]

<span data-ttu-id="d5147-119">Insira um nome e uma descrição opcional na Olá **nome** e **descrição** campos.</span><span class="sxs-lookup"><span data-stu-id="d5147-119">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="d5147-120">Esses campos são o servidor de autorização de saudação OAuth 2.0 tooidentify usado na instância de serviço de gerenciamento de API atual hello e seus valores não vêm do servidor de saudação OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d5147-120">These fields are used tooidentify hello OAuth 2.0 authorization server within hello current API Management service instance and their values do not come from hello OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="d5147-121">Digite hello **URL de página de registro de cliente**.</span><span class="sxs-lookup"><span data-stu-id="d5147-121">Enter hello **Client registration page URL**.</span></span> <span data-ttu-id="d5147-122">Esta página é onde os usuários podem criar e gerenciar suas contas e varia de acordo com o provedor de saudação OAuth 2.0 usado.</span><span class="sxs-lookup"><span data-stu-id="d5147-122">This page is where users can create and manage their accounts, and varies depending on hello OAuth 2.0 provider used.</span></span> <span data-ttu-id="d5147-123">Olá **URL de página de registro de cliente** pontos toohello página que os usuários podem usar toocreate e configurar suas próprias contas para provedores OAuth 2.0 que dão suporte ao gerenciamento de contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="d5147-123">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="d5147-124">Algumas organizações não configurar ou usar essa funcionalidade, mesmo se o provedor de saudação OAuth 2.0 dá suporte a ele.</span><span class="sxs-lookup"><span data-stu-id="d5147-124">Some organizations do not configure or use this functionality even if hello OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="d5147-125">Se seu provedor OAuth 2.0 não tem gerenciamento de usuários de contas configuradas, insira uma URL de espaço reservado como Olá URL da sua empresa ou uma URL como `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d5147-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as hello URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="d5147-126">a próxima seção saudação do formulário Olá contém Olá **tipos de concessão de código de autorização**, **URL de ponto de extremidade de autorização**, e **método de solicitação de autorização** configurações.</span><span class="sxs-lookup"><span data-stu-id="d5147-126">hello next section of hello form contains hello **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Novo servidor][api-management-oauth2-server-2]

<span data-ttu-id="d5147-128">Especifique a saudação **tipos de concessão de código de autorização** verificando tipos Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="d5147-128">Specify hello **Authorization code grant types** by checking hello desired types.</span></span> <span data-ttu-id="d5147-129">**código de autorização** é especificado por padrão.</span><span class="sxs-lookup"><span data-stu-id="d5147-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="d5147-130">Digite hello **URL de ponto de extremidade de autorização**.</span><span class="sxs-lookup"><span data-stu-id="d5147-130">Enter hello **Authorization endpoint URL**.</span></span> <span data-ttu-id="d5147-131">Active Directory do Azure, essa URL será semelhante toohello seguinte URL, onde `<client_id>` é substituído por id do cliente Olá que identifica o servidor de aplicativos toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d5147-131">For Azure Active Directory, this URL will be similar toohello following URL, where `<client_id>` is replaced with hello client id that identifies your application toohello OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="d5147-132">Olá **método de solicitação de autorização** Especifica como a solicitação de autorização de saudação será enviada server toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d5147-132">hello **Authorization request method** specifies how hello authorization request is sent toohello OAuth 2.0 server.</span></span> <span data-ttu-id="d5147-133">O **GET** é selecionado por padrão.</span><span class="sxs-lookup"><span data-stu-id="d5147-133">By default **GET** is selected.</span></span>

<span data-ttu-id="d5147-134">Olá próxima seção é onde hello **URL de ponto de extremidade de Token**, **métodos de autenticação de cliente**, **token de acesso de envio de método**, e **escopopadrão** especificados.</span><span class="sxs-lookup"><span data-stu-id="d5147-134">hello next section is where hello **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Novo servidor][api-management-oauth2-server-3]

<span data-ttu-id="d5147-136">Para um servidor do Azure Active Directory OAuth 2.0, Olá **URL de ponto de extremidade de Token** terá Olá seguinte formato, onde `<APPID>` tem o formato de saudação do `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="d5147-136">For an Azure Active Directory OAuth 2.0 server, hello **Token endpoint URL** will have hello following format, where `<APPID>`  has hello format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="d5147-137">Olá a configuração padrão para **métodos de autenticação de cliente** é **básica**, e **token de acesso de envio de método** é **cabeçalho de autorização**.</span><span class="sxs-lookup"><span data-stu-id="d5147-137">hello default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="d5147-138">Esses valores são configurados nessa seção do formulário hello, juntamente com hello **escopo padrão**.</span><span class="sxs-lookup"><span data-stu-id="d5147-138">These values are configured on this section of hello form, along with hello **Default scope**.</span></span>

<span data-ttu-id="d5147-139">Olá **as credenciais do cliente** seção contém Olá **ID do cliente** e **segredo do cliente**, que é obtido durante o processo de criação e configuração de saudação do seu OAuth 2.0 servidor.</span><span class="sxs-lookup"><span data-stu-id="d5147-139">hello **Client credentials** section contains hello **Client ID** and **Client secret**, which are obtained during hello creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="d5147-140">Uma vez Olá **ID do cliente** e **segredo do cliente** forem especificados, hello **redirect_uri** para Olá **código de autorização** é gerado.</span><span class="sxs-lookup"><span data-stu-id="d5147-140">Once hello **Client ID** and **Client secret** are specified, hello **redirect_uri** for hello **authorization code** is generated.</span></span> <span data-ttu-id="d5147-141">Esse URI é a URL de resposta de saudação tooconfigure usado na configuração de servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d5147-141">This URI is used tooconfigure hello reply URL in your OAuth 2.0 server configuration.</span></span>

![Novo servidor][api-management-oauth2-server-4]

<span data-ttu-id="d5147-143">Se **tipos de concessão de código de autorização** está definido muito**senha do proprietário do recurso**, Olá **as credenciais de senha de proprietário do recurso** seção é toospecify usada as credenciais; Caso contrário, você pode deixar em branco.</span><span class="sxs-lookup"><span data-stu-id="d5147-143">If **Authorization code grant types** is set too**Resource owner password**, hello **Resource owner password credentials** section is used toospecify those credentials; otherwise you can leave it blank.</span></span>

![Novo servidor][api-management-oauth2-server-5]

<span data-ttu-id="d5147-145">Depois que o formulário de saudação for concluído, clique em **salvar** configuração do servidor de autorização toosave Olá OAuth 2.0 do API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="d5147-145">Once hello form is complete, click **Save** toosave hello API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="d5147-146">Depois que a configuração do servidor de saudação for salvo, você pode configurar APIs toouse essa configuração, conforme mostrado na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="d5147-146">Once hello server configuration is saved, you can configure APIs toouse this configuration, as shown in hello next section.</span></span>

## <span data-ttu-id="d5147-147"><a name="step2"></a>Configurar toouse uma API autorização do usuário OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="d5147-147"><a name="step2"> </a>Configure an API toouse OAuth 2.0 user authorization</span></span>
<span data-ttu-id="d5147-148">Clique em **APIs** de saudação **gerenciamento de API** Olá menu à esquerda, clique em nome de saudação da API de saudação desejada **segurança**e, em seguida, marque caixa Olá **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="d5147-148">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, click **Security**, and then check hello box for **OAuth 2.0**.</span></span>

![Autorização do usuário][api-management-user-authorization]

<span data-ttu-id="d5147-150">Selecione Olá desejado **servidor de autorização** na lista suspensa de saudação e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="d5147-150">Select hello desired **Authorization server** from hello drop-down list, and click **Save**.</span></span>

![Autorização do usuário][api-management-user-authorization-save]

## <span data-ttu-id="d5147-152"><a name="step3"></a>Teste autorização do usuário Olá OAuth 2.0 no Portal do desenvolvedor da saudação</span><span class="sxs-lookup"><span data-stu-id="d5147-152"><a name="step3"> </a>Test hello OAuth 2.0 user authorization in hello Developer Portal</span></span>
<span data-ttu-id="d5147-153">Depois que você configurou o servidor de autorização OAuth 2.0 e configurou sua API toouse nesse servidor, você pode testá-lo indo toohello Portal do desenvolvedor e chamar uma API.</span><span class="sxs-lookup"><span data-stu-id="d5147-153">Once you have configured your OAuth 2.0 authorization server and configured your API toouse that server, you can test it by going toohello Developer Portal and calling an API.</span></span>  <span data-ttu-id="d5147-154">Clique em **portal do desenvolvedor** no menu superior direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="d5147-154">Click **Developer portal** in hello top right menu.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-menu]

<span data-ttu-id="d5147-156">Clique em **APIs** no menu superior hello e selecione **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="d5147-156">Click **APIs** in hello top menu and select **Echo API**.</span></span>

![API de Eco][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="d5147-158">Se você tiver apenas uma API configurada ou conta tooyour visível, clique em APIs leva você diretamente toohello operações para essa API.</span><span class="sxs-lookup"><span data-stu-id="d5147-158">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="d5147-159">Selecione Olá **obter recursos** operação, clique em **abrir o Console**e, em seguida, selecione **código de autorização** Olá suspenso.</span><span class="sxs-lookup"><span data-stu-id="d5147-159">Select hello **GET Resource** operation, click **Open Console**, and then select **Authorization code** from hello drop-down.</span></span>

![Abrir console][api-management-open-console]

<span data-ttu-id="d5147-161">Quando **código de autorização** é selecionada, uma janela pop-up será exibida com hello formulário de inscrição do provedor de saudação OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d5147-161">When **Authorization code** is selected, a pop-up window is displayed with hello sign-in form of hello OAuth 2.0 provider.</span></span> <span data-ttu-id="d5147-162">Neste exemplo, formulário de entrada hello é fornecido pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5147-162">In this example hello sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="d5147-163">Se você tiver pop-ups desabilitado, você será solicitado a tooenable-los pelo navegador hello.</span><span class="sxs-lookup"><span data-stu-id="d5147-163">If you have pop-ups disabled you will be prompted tooenable them by hello browser.</span></span> <span data-ttu-id="d5147-164">Depois que você ativá-los, selecione **código de autorização** novamente e hello formulário de entrada será exibido.</span><span class="sxs-lookup"><span data-stu-id="d5147-164">After you enable them, select **Authorization code** again and hello sign-in form will be displayed.</span></span>
> 
> 

![Entrar][api-management-oauth2-signin]

<span data-ttu-id="d5147-166">Depois de ter entrado, Olá **cabeçalhos de solicitação** são preenchidas com um `Authorization : Bearer` cabeçalho que autoriza a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5147-166">Once you have signed in, hello **Request headers** are populated with an `Authorization : Bearer` header that authorizes hello request.</span></span>

![Token do cabeçalho da solicitação][api-management-request-header-token]

<span data-ttu-id="d5147-168">Agora você pode configurar valores de saudação desejado para Olá restantes parâmetros e enviar solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5147-168">At this point you can configure hello desired values for hello remaining parameters, and submit hello request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d5147-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d5147-169">Next steps</span></span>
<span data-ttu-id="d5147-170">Para obter mais informações sobre como usar o OAuth 2.0 e o gerenciamento de API, consulte o seguinte de saudação vídeo e acompanha [artigo](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="d5147-170">For more information about using OAuth 2.0 and API Management, see hello following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

