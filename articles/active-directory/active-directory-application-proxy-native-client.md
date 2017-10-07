---
title: aplicativos cliente nativos de aaaPublish - AD do Azure | Microsoft Docs
description: Aborda como tooenable toocommunicate de aplicativos cliente nativo com o conector de Proxy de aplicativo do AD do Azure tooprovide acesso remoto seguro tooyour local aplicativos.
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
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="d87fa-103">Como tooenable toointeract de aplicativos cliente nativo com o proxy de aplicativos</span><span class="sxs-lookup"><span data-stu-id="d87fa-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="d87fa-104">Em aplicativos de tooweb de adição, Proxy de aplicativo do Azure Active Directory também podem ser usados toopublish aplicativos de cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="d87fa-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="d87fa-105">Os aplicativos cliente nativos diferem dos aplicativos Web porque eles são instalados em um dispositivo, enquanto os aplicativos Web são acessados por meio de um navegador.</span><span class="sxs-lookup"><span data-stu-id="d87fa-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="d87fa-106">O Proxy de Aplicativo dá suporte a aplicativos cliente nativos aceitando os tokens emitidos pelo Azure AD que são enviados nos cabeçalhos padrão Autorizar HTTP.</span><span class="sxs-lookup"><span data-stu-id="d87fa-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relação entre os usuários finais, o Active Directory do Azure e os aplicativos publicados](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="d87fa-108">Use Olá biblioteca de autenticação do AD do Azure, que cuida da autenticação e dá suporte a muitos ambientes de cliente, aplicativos nativos toopublish.</span><span class="sxs-lookup"><span data-stu-id="d87fa-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="d87fa-109">Proxy de aplicativo se encaixa Olá [cenário do aplicativo nativo tooWeb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="d87fa-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="d87fa-110">Este artigo orienta Olá quatro etapas toopublish um aplicativo nativo com o Proxy de aplicativo e hello biblioteca de autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d87fa-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="d87fa-111">Etapa 1: publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d87fa-111">Step 1: Publish your application</span></span>
<span data-ttu-id="d87fa-112">Publicar seu aplicativo proxy como faria com qualquer outro aplicativo e atribuir usuários tooaccess seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d87fa-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="d87fa-113">Para saber mais, consulte [Publicar aplicativos com o Proxy de Aplicativo](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d87fa-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="d87fa-114">Etapa 2: configurar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d87fa-114">Step 2: Configure your application</span></span>
<span data-ttu-id="d87fa-115">Configure seu aplicativo nativo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d87fa-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="d87fa-116">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d87fa-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d87fa-117">Navegue muito**Active Directory do Azure** > **registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="d87fa-118">Selecione **Novo registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="d87fa-119">Especifique um nome para seu aplicativo, selecione **nativo** como tipo de aplicativo hello e fornecem Olá URI de redirecionamento para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d87fa-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![Criar um novo registro de aplicativo](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="d87fa-121">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-121">Select **Create**.</span></span>

<span data-ttu-id="d87fa-122">Para obter informações mais detalhadas sobre como criar um novo registro de aplicativo, confira [Integrando aplicativos ao Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d87fa-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="d87fa-123">Etapa 3: Acesso tooother candidaturas</span><span class="sxs-lookup"><span data-stu-id="d87fa-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="d87fa-124">Habilite Olá aplicativo nativo toobe exposto tooother aplicativos em seu diretório:</span><span class="sxs-lookup"><span data-stu-id="d87fa-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="d87fa-125">Ainda no **registros do aplicativo**, selecione Olá novo aplicativo nativo que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="d87fa-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="d87fa-126">Selecione **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="d87fa-127">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-127">Select **Add**.</span></span>
4. <span data-ttu-id="d87fa-128">Olá abrir a primeira etapa **selecionar uma API**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="d87fa-129">Use Olá barra toofind Olá Proxy de aplicativo aplicativo de pesquisa que você publicou na primeira seção do hello.</span><span class="sxs-lookup"><span data-stu-id="d87fa-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="d87fa-130">Escolha esse aplicativo e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-130">Choose that app, then click **Select**.</span></span> 

   ![Procure Olá proxy aplicativo](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="d87fa-132">Segunda etapa de saudação aberto, **selecionar permissões**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="d87fa-133">Olá caixa de seleção toogrant seu aplicativo de proxy do aplicativo nativo acesso tooyour e clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![Conceder acesso tooproxy aplicativo](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="d87fa-135">Selecione **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="d87fa-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="d87fa-136">Etapa 4: Editar Olá biblioteca de autenticação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="d87fa-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="d87fa-137">Edite o código do aplicativo nativo Olá no contexto de autenticação de saudação do Olá biblioteca de autenticação do Active Directory (ADAL) tooinclude Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d87fa-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="d87fa-138">variáveis de saudação no código de exemplo hello devem ser substituídos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d87fa-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="d87fa-139">**ID do locatário** pode ser encontrado na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d87fa-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="d87fa-140">Navegue muito**Active Directory do Azure** > **propriedades** e cópia hello ID de diretório.</span><span class="sxs-lookup"><span data-stu-id="d87fa-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="d87fa-141">**URL externa** é Olá URL de front-end inserida no hello Proxy de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d87fa-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="d87fa-142">toofind este valor, navegar toohello **proxy de aplicativo** seção do aplicativo de proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="d87fa-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="d87fa-143">**ID do aplicativo** de saudação aplicativo nativo pode ser encontrado no hello **propriedades** página do aplicativo nativo hello.</span><span class="sxs-lookup"><span data-stu-id="d87fa-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="d87fa-144">**Redirecionar URI do aplicativo nativo Olá** podem ser encontradas no hello **URIs de redirecionamento** página do aplicativo nativo hello.</span><span class="sxs-lookup"><span data-stu-id="d87fa-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="d87fa-145">Consulte também</span><span class="sxs-lookup"><span data-stu-id="d87fa-145">See also</span></span>

<span data-ttu-id="d87fa-146">Para obter mais informações sobre o fluxo do aplicativo nativo hello, consulte [tooweb aplicativo nativo API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="d87fa-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="d87fa-147">Para Olá últimas notícias e atualizações, confira Olá [blog de Proxy de aplicativo](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="d87fa-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
