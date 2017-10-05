---
title: Publicar aplicativos cliente nativos - Azure AD | Microsoft Docs
description: Aborda como habilitar aplicativos clientes nativos para se comunicar com o Conector de Proxy do aplicativo Azure AD para fornecer acesso remoto seguro aos seus aplicativos locais.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: bdaa5af6ff5331bc310499586615b48a864c3c5e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="71e74-103">Como habilitar aplicativos clientes nativos para interagir com aplicativos de proxy</span><span class="sxs-lookup"><span data-stu-id="71e74-103">How to enable native client apps to interact with proxy Applications</span></span>

<span data-ttu-id="71e74-104">Além dos aplicativos Web, o Proxy de Aplicativo do Azure Active Directory também pode ser usado para publicar aplicativos cliente nativos.</span><span class="sxs-lookup"><span data-stu-id="71e74-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps.</span></span> <span data-ttu-id="71e74-105">Os aplicativos cliente nativos diferem dos aplicativos Web porque eles são instalados em um dispositivo, enquanto os aplicativos Web são acessados por meio de um navegador.</span><span class="sxs-lookup"><span data-stu-id="71e74-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="71e74-106">O Proxy de Aplicativo dá suporte a aplicativos cliente nativos aceitando os tokens emitidos pelo Azure AD que são enviados nos cabeçalhos padrão Autorizar HTTP.</span><span class="sxs-lookup"><span data-stu-id="71e74-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relação entre os usuários finais, o Active Directory do Azure e os aplicativos publicados](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="71e74-108">Use a Biblioteca de Autenticação do Azure AD, que trata da autenticação e dá suporte a vários ambientes de cliente, para publicar aplicativos nativos.</span><span class="sxs-lookup"><span data-stu-id="71e74-108">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="71e74-109">O Proxy de Aplicativo se encaixa no [cenário de Aplicativo Nativo para API Web](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="71e74-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="71e74-110">Este artigo explica as quatro etapas para publicar um aplicativo nativo com o Proxy de Aplicativo e a Biblioteca de Autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71e74-110">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="71e74-111">Etapa 1: publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="71e74-111">Step 1: Publish your application</span></span>
<span data-ttu-id="71e74-112">Publique seu aplicativo de proxy como faria com qualquer outro aplicativo e atribua aos usuários acesso a ele.</span><span class="sxs-lookup"><span data-stu-id="71e74-112">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="71e74-113">Para saber mais, consulte [Publicar aplicativos com o Proxy de Aplicativo](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="71e74-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="71e74-114">Etapa 2: configurar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="71e74-114">Step 2: Configure your application</span></span>
<span data-ttu-id="71e74-115">Configure seu aplicativo nativo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="71e74-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="71e74-116">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="71e74-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="71e74-117">Navegue até **Azure Active Directory** > **Registros de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="71e74-117">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="71e74-118">Selecione **Novo registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="71e74-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="71e74-119">Especifique um nome para o aplicativo, selecione **Nativo** como o tipo de aplicativo e forneça o URI de Redirecionamento para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71e74-119">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![Criar um novo registro de aplicativo](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="71e74-121">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="71e74-121">Select **Create**.</span></span>

<span data-ttu-id="71e74-122">Para obter informações mais detalhadas sobre como criar um novo registro de aplicativo, confira [Integrando aplicativos ao Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="71e74-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="71e74-123">Etapa 3: conceder acesso a outros aplicativos</span><span class="sxs-lookup"><span data-stu-id="71e74-123">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="71e74-124">Habilite o aplicativo nativo para ser exposto a outros aplicativos no seu diretório:</span><span class="sxs-lookup"><span data-stu-id="71e74-124">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="71e74-125">Ainda nos **Registros de aplicativo**, selecione o novo aplicativo nativo que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="71e74-125">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="71e74-126">Selecione **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="71e74-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="71e74-127">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="71e74-127">Select **Add**.</span></span>
4. <span data-ttu-id="71e74-128">Abra a primeira etapa, **Selecionar uma API**.</span><span class="sxs-lookup"><span data-stu-id="71e74-128">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="71e74-129">Use a barra de pesquisa para encontrar o aplicativo Proxy de Aplicativo que você publicou na primeira seção.</span><span class="sxs-lookup"><span data-stu-id="71e74-129">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="71e74-130">Escolha esse aplicativo e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="71e74-130">Choose that app, then click **Select**.</span></span> 

   ![Procurar o aplicativo de proxy](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="71e74-132">Abra a segunda etapa, **Selecionar permissões**.</span><span class="sxs-lookup"><span data-stu-id="71e74-132">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="71e74-133">Use a caixa de seleção para conceder ao aplicativo nativo acesso ao aplicativo de proxy e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="71e74-133">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![Conceder acesso ao aplicativo de proxy](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="71e74-135">Selecione **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="71e74-135">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="71e74-136">Etapa 4: Edite a Biblioteca de Autenticação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="71e74-136">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="71e74-137">Edite o código de aplicativo nativo no contexto de autenticação da ADAL (Biblioteca de Autenticação do Active Directory) para incluir o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="71e74-137">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="71e74-138">As variáveis no exemplo de código devem ser substituídas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="71e74-138">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="71e74-139">A **ID do locatário** pode ser encontrada no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="71e74-139">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="71e74-140">Navegue até **Azure Active Directory** > **Propriedades** e copie a ID de Diretório.</span><span class="sxs-lookup"><span data-stu-id="71e74-140">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="71e74-141">A **URL externa** é a URL de front-end que você inseriu no Aplicativo de Proxy.</span><span class="sxs-lookup"><span data-stu-id="71e74-141">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="71e74-142">Para encontrar esse valor, navegue até a seção **Proxy de aplicativo** do aplicativo de proxy.</span><span class="sxs-lookup"><span data-stu-id="71e74-142">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="71e74-143">A **ID do aplicativo** do aplicativo nativo pode ser encontrada na página **Propriedades** do aplicativo nativo.</span><span class="sxs-lookup"><span data-stu-id="71e74-143">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="71e74-144">O **URI de Redirecionamento do aplicativo nativo** pode ser encontrado na página **URIs de Redirecionamento** do aplicativo nativo.</span><span class="sxs-lookup"><span data-stu-id="71e74-144">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="71e74-145">Consulte também</span><span class="sxs-lookup"><span data-stu-id="71e74-145">See also</span></span>

<span data-ttu-id="71e74-146">Para saber mais sobre o fluxo do aplicativo nativo, confira [Aplicativo nativo para API Web](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="71e74-146">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="71e74-147">Para obter as últimas notícias e atualizações, confira o [blog do Proxy de Aplicativo](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="71e74-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
