---
title: Autorizar contas de desenvolvedor usando o OAuth 2.0 no Gerenciamento de API do Azure | Microsoft Docs
description: "Aprenda a autorizar os usuários usando o OAuth 2.0 no Gerenciamento de API."
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
ms.openlocfilehash: a19c453bb3271374b587f3d0b35adad55863b490
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-authorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="54942-103">Como autorizar contas de desenvolvedor usando o OAuth 2.0 no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="54942-103">How to authorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="54942-104">Muitas APIs dão suporte ao [OAuth 2.0](http://oauth.net/2/) para proteger a API e garantir que apenas usuários válidos tenham acesso e possam acessar apenas os recursos para os quais eles estão qualificados.</span><span class="sxs-lookup"><span data-stu-id="54942-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) to secure the API and ensure that only valid users have access, and they can only access resources to which they're entitled.</span></span> <span data-ttu-id="54942-105">Para usar o Console de desenvolvedor interativo do Gerenciamento de API do Azure com essas APIs, o serviço permite que você configure sua instância de serviço para funcionar com sua API habilitada para o OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="54942-105">In order to use Azure API Management's interactive Developer Console with such APIs, the service allows you to configure your service instance to work with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="54942-106"><a name="prerequisites"> </a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="54942-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="54942-107">Este guia mostra como configurar sua instância de serviço de Gerenciamento de API para usar a autorização OAuth 2.0 para contas do desenvolvedor, mas não mostra como configurar um provedor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="54942-107">This guide shows you how to configure your API Management service instance to use OAuth 2.0 authorization for developer accounts, but does not show you how to configure an OAuth 2.0 provider.</span></span> <span data-ttu-id="54942-108">A configuração para cada provedor OAuth 2.0 é diferente, embora as etapas sejam semelhantes e as peças de informações necessárias usadas ao configurar o OAuth 2.0 na sua instância de serviço de Gerenciamento de API sejam as mesmas.</span><span class="sxs-lookup"><span data-stu-id="54942-108">The configuration for each OAuth 2.0 provider is different, although the steps are similar, and the required pieces of information used in configuring OAuth 2.0 in your API Management service instance are the same.</span></span> <span data-ttu-id="54942-109">Este tópico mostra exemplos ao usar o Active Directory do Azure como um provedor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="54942-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="54942-110">Para obter mais informações sobre a configuração do OAuth 2.0 usando o Azure Active Directory, consulte a amostra [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet].</span><span class="sxs-lookup"><span data-stu-id="54942-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see the [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="54942-111"><a name="step1"> </a>Configurar um servidor de autorização do OAuth 2.0 no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="54942-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="54942-112">Para começar, clique em **Portal do Editor** no Portal do Azure para acessar o serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="54942-112">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal do editor][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="54942-114">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="54942-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="54942-115">Clique em **Segurança** no menu de **Gerenciamento da API** à esquerda, clique em **OAuth 2.0** e em **Adicionar servidor de autorização**.</span><span class="sxs-lookup"><span data-stu-id="54942-115">Click **Security** from the **API Management** menu on the left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="54942-117">Após clicar em **Adicionar servidor de autorização**, a nova forma do servidor de autorização é exibida.</span><span class="sxs-lookup"><span data-stu-id="54942-117">After clicking **Add authorization server**, the new authorization server form is displayed.</span></span>

![Novo servidor][api-management-oauth2-server-1]

<span data-ttu-id="54942-119">Insira um nome e uma descrição opcional nos campos **Nome** e **Descrição**.</span><span class="sxs-lookup"><span data-stu-id="54942-119">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="54942-120">Esses campos são usados para identificar o servidor de autorização OAuth 2.0 dentro da instância do serviço de Gerenciamento de API atual e seus valores não vêm do servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="54942-120">These fields are used to identify the OAuth 2.0 authorization server within the current API Management service instance and their values do not come from the OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="54942-121">Digite a **URL da página de registro do cliente**.</span><span class="sxs-lookup"><span data-stu-id="54942-121">Enter the **Client registration page URL**.</span></span> <span data-ttu-id="54942-122">Essa página é onde os usuários podem criar e gerenciar suas contas e varia de acordo com o provedor OAuth 2.0 usado.</span><span class="sxs-lookup"><span data-stu-id="54942-122">This page is where users can create and manage their accounts, and varies depending on the OAuth 2.0 provider used.</span></span> <span data-ttu-id="54942-123">A **URL de página de registro do cliente** aponta para a página que os usuários podem usar para criar e configurar suas próprias contas para provedores OAuth 2.0 que dão suporte a gerenciamento de contas por usuários.</span><span class="sxs-lookup"><span data-stu-id="54942-123">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="54942-124">Algumas organizações não configuram nem usam essa funcionalidade, mesmo se o provedor OAuth 2.0 dá suporte a ele.</span><span class="sxs-lookup"><span data-stu-id="54942-124">Some organizations do not configure or use this functionality even if the OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="54942-125">Se seu provedor OAuth 2.0 não tem o gerenciamento de contas por usuários configurado, insira uma URL de espaço reservado aqui, como a URL da sua empresa, ou uma URL como `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="54942-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as the URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="54942-126">A seção seguinte da forma contém as configurações dos **tipos de concessão do código de autorização**, da **URL do ponto de extremidade de autorização** e do **método de solicitação de autorização**.</span><span class="sxs-lookup"><span data-stu-id="54942-126">The next section of the form contains the **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Novo servidor][api-management-oauth2-server-2]

<span data-ttu-id="54942-128">Especifique os **tipos de concessão do código de autorização** ao verificar os tipos desejados.</span><span class="sxs-lookup"><span data-stu-id="54942-128">Specify the **Authorization code grant types** by checking the desired types.</span></span> <span data-ttu-id="54942-129">**código de autorização** é especificado por padrão.</span><span class="sxs-lookup"><span data-stu-id="54942-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="54942-130">Digite a **URL do ponto de extremidade de autorização**.</span><span class="sxs-lookup"><span data-stu-id="54942-130">Enter the **Authorization endpoint URL**.</span></span> <span data-ttu-id="54942-131">Para o Active Directory do Azure, essa URL será semelhante à URL seguinte, em que `<client_id>` é substituído pela ID do cliente que identifica seu aplicativo para o servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="54942-131">For Azure Active Directory, this URL will be similar to the following URL, where `<client_id>` is replaced with the client id that identifies your application to the OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="54942-132">O **método de solicitação de autorização** especifica como a solicitação de autorização é enviada para o servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="54942-132">The **Authorization request method** specifies how the authorization request is sent to the OAuth 2.0 server.</span></span> <span data-ttu-id="54942-133">O **GET** é selecionado por padrão.</span><span class="sxs-lookup"><span data-stu-id="54942-133">By default **GET** is selected.</span></span>

<span data-ttu-id="54942-134">A seção seguinte está onde a **URL de ponto de extremidade do token**, os **métodos de autenticação do cliente**, **o método de envio de token de acesso** e o **escopo padrão** são especificados.</span><span class="sxs-lookup"><span data-stu-id="54942-134">The next section is where the **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Novo servidor][api-management-oauth2-server-3]

<span data-ttu-id="54942-136">Para o servidor OAuth 2.0 do Azure Active Directory, a **URL do ponto de extremidade do token** terá o seguinte formato, em que `<APPID>` tem o formato de `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="54942-136">For an Azure Active Directory OAuth 2.0 server, the **Token endpoint URL** will have the following format, where `<APPID>`  has the format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="54942-137">A configuração padrão para os **métodos de autenticação do cliente** é **Básica** e o **método de envio do token de acesso** é **Cabeçalho de autorização**.</span><span class="sxs-lookup"><span data-stu-id="54942-137">The default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="54942-138">Esses valores são configurados nesta seção da forma, junto com o **Escopo padrão**.</span><span class="sxs-lookup"><span data-stu-id="54942-138">These values are configured on this section of the form, along with the **Default scope**.</span></span>

<span data-ttu-id="54942-139">A seção **Credenciais do cliente** contém a **ID do cliente** e a **Senha do cliente**, que são obtidas durante o processo de criação e de configuração do seu servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="54942-139">The **Client credentials** section contains the **Client ID** and **Client secret**, which are obtained during the creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="54942-140">Uma vez que a **ID do cliente** e a **Senha do cliente** são especificadas, o **redirect_uri** para o **código de autorização** é gerado.</span><span class="sxs-lookup"><span data-stu-id="54942-140">Once the **Client ID** and **Client secret** are specified, the **redirect_uri** for the **authorization code** is generated.</span></span> <span data-ttu-id="54942-141">Essa URI é usada para configurar a URL de resposta em sua configuração do servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="54942-141">This URI is used to configure the reply URL in your OAuth 2.0 server configuration.</span></span>

![Novo servidor][api-management-oauth2-server-4]

<span data-ttu-id="54942-143">Se os **Tipos de concessão do código de autorização** são definidos como **Senha do proprietário do recurso**, a seção **Credenciais de senha do proprietário de recurso** é usada para especificar estas credenciais; não sendo o caso, você pode deixá-la em branco.</span><span class="sxs-lookup"><span data-stu-id="54942-143">If **Authorization code grant types** is set to **Resource owner password**, the **Resource owner password credentials** section is used to specify those credentials; otherwise you can leave it blank.</span></span>

![Novo servidor][api-management-oauth2-server-5]

<span data-ttu-id="54942-145">Uma vez que o formulário está concluído, clique em **Salvar** para salvar a configuração do servidor de autorização do OAuth 2.0 de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="54942-145">Once the form is complete, click **Save** to save the API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="54942-146">Quando a configuração do servidor for salva, você pode configurar as APIs para usar esta configuração, conforme mostrado na seção seguinte.</span><span class="sxs-lookup"><span data-stu-id="54942-146">Once the server configuration is saved, you can configure APIs to use this configuration, as shown in the next section.</span></span>

## <span data-ttu-id="54942-147"><a name="step2"> </a>Configurar uma API para usar a autorização do usuário do OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="54942-147"><a name="step2"> </a>Configure an API to use OAuth 2.0 user authorization</span></span>
<span data-ttu-id="54942-148">Clique nas **APIs** no menu **Gerenciamento de API** à esquerda, clique no nome da API desejada, clique na guia **Segurança** e marque a caixa para **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="54942-148">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, click **Security**, and then check the box for **OAuth 2.0**.</span></span>

![Autorização do usuário][api-management-user-authorization]

<span data-ttu-id="54942-150">Selecione o **Servidor de autorização** desejado a partir da lista suspensa e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="54942-150">Select the desired **Authorization server** from the drop-down list, and click **Save**.</span></span>

![Autorização do usuário][api-management-user-authorization-save]

## <span data-ttu-id="54942-152"><a name="step3"> </a>Testar a autorização do usuário do OAuth 2.0 no Portal do Desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="54942-152"><a name="step3"> </a>Test the OAuth 2.0 user authorization in the Developer Portal</span></span>
<span data-ttu-id="54942-153">Depois de configurar seu servidor de autorização OAuth 2.0 e configurar sua API para usar esse servidor, você pode testá-lo indo para o Portal do Desenvolvedor e chamando a API.</span><span class="sxs-lookup"><span data-stu-id="54942-153">Once you have configured your OAuth 2.0 authorization server and configured your API to use that server, you can test it by going to the Developer Portal and calling an API.</span></span>  <span data-ttu-id="54942-154">Clique em **Portal do desenvolvedor** no menu superior direito.</span><span class="sxs-lookup"><span data-stu-id="54942-154">Click **Developer portal** in the top right menu.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-menu]

<span data-ttu-id="54942-156">Clique em **APIs** no menu superior e selecione **API de Eco**.</span><span class="sxs-lookup"><span data-stu-id="54942-156">Click **APIs** in the top menu and select **Echo API**.</span></span>

![API de Eco][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="54942-158">Se você tem apenas uma API configurada ou visível na conta, clicar em APIs levará você diretamente às operações dessa API.</span><span class="sxs-lookup"><span data-stu-id="54942-158">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="54942-159">Selecione a operação **Recurso GET**, clique em **Abrir Console** e selecione **Código de autorização** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="54942-159">Select the **GET Resource** operation, click **Open Console**, and then select **Authorization code** from the drop-down.</span></span>

![Abrir console][api-management-open-console]

<span data-ttu-id="54942-161">Quando o **Código de autorização** está selecionado, uma janela pop-up é exibida com a forma de entrada do provedor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="54942-161">When **Authorization code** is selected, a pop-up window is displayed with the sign-in form of the OAuth 2.0 provider.</span></span> <span data-ttu-id="54942-162">Neste exemplo, o formulário de inscrição é fornecido pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="54942-162">In this example the sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="54942-163">Se você tiver pop-ups desativados, será solicitado a habilitá-los pelo navegador.</span><span class="sxs-lookup"><span data-stu-id="54942-163">If you have pop-ups disabled you will be prompted to enable them by the browser.</span></span> <span data-ttu-id="54942-164">Depois de habilitar, selecione **Código de autorização** novamente e a forma de entrada será exibida.</span><span class="sxs-lookup"><span data-stu-id="54942-164">After you enable them, select **Authorization code** again and the sign-in form will be displayed.</span></span>
> 
> 

![Entrar][api-management-oauth2-signin]

<span data-ttu-id="54942-166">Depois de entrar, os **Cabeçalhos de solicitação** serão preenchidos com um cabeçalho `Authorization : Bearer` que autoriza a solicitação.</span><span class="sxs-lookup"><span data-stu-id="54942-166">Once you have signed in, the **Request headers** are populated with an `Authorization : Bearer` header that authorizes the request.</span></span>

![Token do cabeçalho da solicitação][api-management-request-header-token]

<span data-ttu-id="54942-168">Nesse momento, você pode configurar os valores desejados para os parâmetros restantes e enviar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="54942-168">At this point you can configure the desired values for the remaining parameters, and submit the request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="54942-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54942-169">Next steps</span></span>
<span data-ttu-id="54942-170">Para obter mais informações sobre como usar OAuth 2.0 e Gerenciamento de API, consulte o vídeo a seguir e o [artigo](api-management-howto-protect-backend-with-aad.md)que o acompanha.</span><span class="sxs-lookup"><span data-stu-id="54942-170">For more information about using OAuth 2.0 and API Management, see the following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

