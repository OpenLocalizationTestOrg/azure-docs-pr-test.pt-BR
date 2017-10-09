---
title: "aaaDeploy, chamar e autenticar as APIs da web e APIs REST para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Implantar, autenticar e chamar APIs Web e APIs REST em fluxos de trabalho para integrações do sistema com o Aplicativo Lógico do Azure"
keywords: "APIs Web, APIs REST, conectores, fluxos de trabalho, integrações do sistema, autenticar"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="931bc-104">Implantar, chamar e autenticar as APIs personalizadas como conectores para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="931bc-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="931bc-105">Depois que você [criar APIs personalizadas](./logic-apps-create-api-app.md) que fornecem toouse ações ou disparadores na lógica de fluxos de trabalho de aplicativos, você deve implantar suas APIs antes de você pode chamá-los.</span><span class="sxs-lookup"><span data-stu-id="931bc-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="931bc-106">E embora você possa chamar qualquer API de um aplicativo lógico, para obter melhor experiência hello, adicione [Swagger metadados](http://swagger.io/specification/) que descreve as operações e os parâmetros de sua API.</span><span class="sxs-lookup"><span data-stu-id="931bc-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="931bc-107">Este arquivo Swagger ajuda sua API a funcionar melhor e se integrar aos aplicativos lógicos mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="931bc-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="931bc-108">Você pode implantar suas APIs como [aplicativos web](../app-service-web/app-service-web-overview.md), mas considere a implantação de suas APIs como [aplicativos de API](../app-service-api/app-service-api-apps-why-best-platform.md), que pode facilitar o trabalho quando você criar, hospeda e consumir APIs na nuvem hello e no local.</span><span class="sxs-lookup"><span data-stu-id="931bc-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="931bc-109">Você não tem qualquer código de toochange em suas APIs - apenas implantar seu aplicativo de API de tooan de código.</span><span class="sxs-lookup"><span data-stu-id="931bc-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="931bc-110">Você pode hospedar suas APIs em [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md), um plataforma-como-um-serviço (PaaS) que oferece uma das maneiras de saudação melhores, mais fácil e mais escalonáveis para API de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="931bc-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="931bc-111">chamadas de tooauthenticate de lógica aplicativos tooyour APIs, você pode definir o Azure Active Directory no hello portal do Azure para que você não tenha tooupdate seu código.</span><span class="sxs-lookup"><span data-stu-id="931bc-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="931bc-112">Ou você pode exigir e aplicar a autenticação por meio do seu código da API.</span><span class="sxs-lookup"><span data-stu-id="931bc-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="931bc-113">Implantar sua API como um aplicativo Web ou aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="931bc-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="931bc-114">Antes de chamar sua API personalizada de um aplicativo lógico, implante sua API como um aplicativo web ou tooAzure do aplicativo de API do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="931bc-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="931bc-115">Além disso, a toomake Swagger documento legível por Olá lógica de aplicativo Designer, defina as propriedades de definição de saudação API e ativar [recursos entre origens (CORS) de compartilhamento](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) para seu aplicativo web ou aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="931bc-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="931bc-116">No hello portal do Azure, selecione o aplicativo web ou aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="931bc-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="931bc-117">Na folha de saudação que é aberta, em **API**, escolha **de definição de API**.</span><span class="sxs-lookup"><span data-stu-id="931bc-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="931bc-118">Saudação de conjunto **local da definição de API** toohello URL para o arquivo swagger. JSON.</span><span class="sxs-lookup"><span data-stu-id="931bc-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="931bc-119">Geralmente, Olá URL aparece neste formato:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="931bc-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Arquivo de tooSwagger link para sua API personalizada](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="931bc-121">Em **API**, escolha **CORS**.</span><span class="sxs-lookup"><span data-stu-id="931bc-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="931bc-122">Definir a diretiva de CORS Olá **permitido origens** muito**'*'** (permitir todos os).</span><span class="sxs-lookup"><span data-stu-id="931bc-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="931bc-123">Essa configuração permite solicitações do Designer de Aplicativo Lógico.</span><span class="sxs-lookup"><span data-stu-id="931bc-123">This setting permits requests from Logic App Designer.</span></span>

   ![Permitir solicitações de API personalizada do Designer de lógica do aplicativo tooyour](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="931bc-125">Para obter mais informações, consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="931bc-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="931bc-126">Adicionar metadados do Swagger para APIs Web do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="931bc-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="931bc-127">Implantar tooAzure APIs da web ASP.NET do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="931bc-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="931bc-128">Chamar sua API personalizada de fluxos de trabalho de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="931bc-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="931bc-129">Depois de configurar propriedades de definição de saudação API e CORS, gatilhos e ações de sua API personalizada deverá ficar disponíveis para você tooinclude no seu fluxo de trabalho do aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="931bc-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="931bc-130">tooview Olá sites que tenham URLs Swagger, você pode procurar seus sites de assinatura em Olá lógica do Designer de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="931bc-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="931bc-131">ações disponíveis tooview e entradas apontando para um documento de Swagger, use Olá [HTTP + Swagger ação](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="931bc-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="931bc-132">toocall qualquer API, incluindo aquelas que não têm ou expor um documento de Swagger, você sempre pode criar uma solicitação com hello [ação HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="931bc-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="931bc-133">Autenticar chamadas tooyour personalizado API</span><span class="sxs-lookup"><span data-stu-id="931bc-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="931bc-134">Você pode proteger chamadas API personalizada do tooyour das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="931bc-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="931bc-135">[Nenhuma alteração de código](#no-code): proteger sua API com [do Azure Active Directory (AD do Azure)](../active-directory/active-directory-whatis.md) por meio de Olá portal do Azure, portanto não tiver tooupdate seu código ou reimplantar sua API.</span><span class="sxs-lookup"><span data-stu-id="931bc-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="931bc-136">Por padrão, a autenticação do AD do Azure Olá que ativar Olá portal do Azure não fornece autorização refinada.</span><span class="sxs-lookup"><span data-stu-id="931bc-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="931bc-137">Por exemplo, essa autenticação bloqueios toojust sua API um locatário específico, não tooa usuário específico ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="931bc-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="931bc-138">[Atualizar o código da API](#update-code): proteja sua API impondo a [autenticação de certificado](#certificate), a [autenticação básica](#basic) ou a [autenticação do Azure AD](#azure-ad-code) por meio de código.</span><span class="sxs-lookup"><span data-stu-id="931bc-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="931bc-139">Autenticar chamadas tooyour API sem alterar o código</span><span class="sxs-lookup"><span data-stu-id="931bc-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="931bc-140">Eis as etapas gerais para este método hello:</span><span class="sxs-lookup"><span data-stu-id="931bc-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="931bc-141">Crie duas [identidades de aplicativo do Azure AD (Azure Active Directory)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): uma para seu aplicativo lógico e um para seu aplicativo Web (ou aplicativo de API).</span><span class="sxs-lookup"><span data-stu-id="931bc-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="931bc-142">tooauthenticate tooyour de chamadas API, use credenciais de saudação (ID do cliente e segredo) para Olá [entidade de serviço](../app-service-api/app-service-api-dotnet-service-principal-auth.md) associado Olá identidade de aplicativo do AD do Azure para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="931bc-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="931bc-143">Inclua o aplicativo hello IDs em sua definição de aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="931bc-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="931bc-144">Parte 1: Criar uma identidade do aplicativo do Azure AD para seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="931bc-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="931bc-145">Sua lógica de aplicativo usa esse tooauthenticate de identidade de aplicativo do AD do Azure no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="931bc-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="931bc-146">Você só tem tooset a essa identidade de uma vez para seu diretório.</span><span class="sxs-lookup"><span data-stu-id="931bc-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="931bc-147">Por exemplo, você pode escolher toouse Olá identidade mesmo para todos os seus aplicativos lógicos, mesmo que você pode criar identidades exclusivas para cada aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="931bc-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="931bc-148">Você pode configurar essas identidades no hello portal do Azure, [portal clássico do Azure](#app-identity-logic-classic), ou use [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="931bc-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="931bc-149">**Criar identidade de aplicativo hello para seu aplicativo lógica no hello portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="931bc-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="931bc-150">Em Olá [portal do Azure](https://portal.azure.com "https://portal.azure.com"), escolha **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="931bc-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="931bc-151">Confirme que você está no hello mesmo diretório que o aplicativo web ou aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="931bc-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="931bc-152">tooswitch diretórios, clique em seu perfil e selecione outro diretório.</span><span class="sxs-lookup"><span data-stu-id="931bc-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="931bc-153">Ou escolha **Visão Geral** > **Mudar diretório**.</span><span class="sxs-lookup"><span data-stu-id="931bc-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="931bc-154">No menu de diretório hello, em **gerenciar**, escolha **registros do aplicativo** > **novo registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="931bc-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="931bc-155">Por padrão, a lista de registros do aplicativo hello mostra todos os registros do aplicativo em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="931bc-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="931bc-156">tooview somente seus registros do aplicativo, próxima toohello caixa de pesquisa, selecione **meus aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="931bc-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![Criar novo registro de aplicativo](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="931bc-158">Dê um nome de sua identidade de aplicativo, deixe **tipo de aplicativo** definido muito**aplicativo Web / API**, fornecer uma única cadeia de caracteres formatada como um domínio para **URL de logon**e escolha  **Criar**.</span><span class="sxs-lookup"><span data-stu-id="931bc-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Forneça o nome e a URL de entrada para a identidade do aplicativo](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="931bc-160">identidade de aplicativo Hello que você criou para seu aplicativo lógico agora aparece na lista de registros do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="931bc-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![Identidade do aplicativo para seu aplicativo lógico](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="931bc-162">Na lista de registros do aplicativo hello, selecione sua nova identidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="931bc-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="931bc-163">Copie e salve Olá **ID do aplicativo** toouse como hello "ID do cliente" para seu aplicativo lógica na parte 3.</span><span class="sxs-lookup"><span data-stu-id="931bc-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![Copie e salve a ID do aplicativo para o aplicativo lógico](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="931bc-165">Se as configurações de identidade do aplicativo não estiverem visíveis, escolha **Configurações** ou **Todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="931bc-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="931bc-166">Em **Acesso à API**, escolha **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="931bc-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="931bc-167">Em **Descrição**, forneça um nome para sua chave.</span><span class="sxs-lookup"><span data-stu-id="931bc-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="931bc-168">Em **Expira**, selecione uma duração para a chave.</span><span class="sxs-lookup"><span data-stu-id="931bc-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="931bc-169">chave de saudação que você está criando atua como da identidade do aplicativo hello "segredo" ou a senha para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="931bc-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![Criar chave para identidade de aplicativo lógico](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="931bc-171">Na barra de ferramentas hello, escolha **salvar**.</span><span class="sxs-lookup"><span data-stu-id="931bc-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="931bc-172">Em **Valor**, agora sua chave aparece.</span><span class="sxs-lookup"><span data-stu-id="931bc-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="931bc-173">**Certifique-se de que toocopy e salvar sua chave** para uso posterior porque está oculta chave hello quando você deixa folha chave hello.</span><span class="sxs-lookup"><span data-stu-id="931bc-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="931bc-174">Quando você configura seu aplicativo lógico na parte 3, você especificar essa chave hello "segredo" ou a senha.</span><span class="sxs-lookup"><span data-stu-id="931bc-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![Copiar e salvar a chave para mais tarde](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="931bc-176">**Criar identidade de aplicativo hello para seu aplicativo lógica no hello portal clássico do Azure**</span><span class="sxs-lookup"><span data-stu-id="931bc-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="931bc-177">Nas Olá portal clássico do Azure, escolha [ **do Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="931bc-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="931bc-178">Selecione Olá mesmo diretório que você pode usar para seu aplicativo web ou aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="931bc-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="931bc-179">Em Olá **aplicativos** guia, escolha **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="931bc-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="931bc-180">Dê um nome à identidade do aplicativo e escolha **Avançar** (seta para a direita).</span><span class="sxs-lookup"><span data-stu-id="931bc-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="931bc-181">Em **Propriedades do aplicativo**, forneça uma única cadeia de caracteres formatada como um domínio para **URL de Entrada** e **URI da ID do Aplicativo** e escolha **Concluir** (marca de seleção).</span><span class="sxs-lookup"><span data-stu-id="931bc-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="931bc-182">Em Olá **configurar** guia, copiar e salvar Olá **ID do cliente** para toouse de aplicativo sua lógica na parte 3.</span><span class="sxs-lookup"><span data-stu-id="931bc-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="931bc-183">Em **chaves**, abra Olá **selecionar duração** lista.</span><span class="sxs-lookup"><span data-stu-id="931bc-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="931bc-184">Selecione uma duração para a chave.</span><span class="sxs-lookup"><span data-stu-id="931bc-184">Select a duration for your key.</span></span>

   <span data-ttu-id="931bc-185">chave de saudação que você está criando atua como da identidade do aplicativo hello "segredo" ou a senha para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="931bc-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="931bc-186">Final Olá Olá página, escolha **salvar**.</span><span class="sxs-lookup"><span data-stu-id="931bc-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="931bc-187">Você pode ter toowait alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="931bc-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="931bc-188">Em **chaves**, certifique-se de que toocopy e salvar chave de saudação agora aparece.</span><span class="sxs-lookup"><span data-stu-id="931bc-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="931bc-189">Quando você configura seu aplicativo lógico na parte 3, você especificar essa chave hello "segredo" ou a senha.</span><span class="sxs-lookup"><span data-stu-id="931bc-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="931bc-190">Para obter mais informações, saiba como muito [configurar seu aplicativo de serviço de aplicativo toouse Active Directory do Azure logon](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="931bc-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="931bc-191">**Criar identidade de aplicativo de saudação para seu aplicativo lógico no PowerShell**</span><span class="sxs-lookup"><span data-stu-id="931bc-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="931bc-192">Você pode executar essa tarefa por meio do Azure Resource Manager com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="931bc-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="931bc-193">No PowerShell, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="931bc-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="931bc-194">Verifique se Olá de toocopy **ID de locatário** hello (GUID para seu locatário do AD do Azure), **ID do aplicativo**e a senha de saudação que você usou.</span><span class="sxs-lookup"><span data-stu-id="931bc-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="931bc-195">Para obter mais informações, saiba como muito [criar uma entidade de serviço com recursos do PowerShell tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="931bc-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="931bc-196">Parte 2: Criar uma identidade do aplicativo do Azure AD para seu aplicativo Web ou aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="931bc-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="931bc-197">Se seu aplicativo de API ou um aplicativo web já estiver implantado, pode ativar a autenticação e criar a identidade do aplicativo hello no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="931bc-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="931bc-198">Caso contrário, você pode [ativar a autenticação quando implantar com um modelo do Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="931bc-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="931bc-199">**Criar identidade de aplicativo hello e ativar a autenticação no portal do Azure para aplicativos implantados de saudação**</span><span class="sxs-lookup"><span data-stu-id="931bc-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="931bc-200">Em Olá [portal do Azure](https://portal.azure.com "https://portal.azure.com"), localize e selecione o aplicativo web ou aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="931bc-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="931bc-201">Em **Configurações**, escolha **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="931bc-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="931bc-202">Em **Autenticação do Serviço de Aplicativo**, **Ative** a autenticação.</span><span class="sxs-lookup"><span data-stu-id="931bc-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="931bc-203">Em **Provedores de Autenticação**, escolha **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="931bc-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Ativar a autenticação](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="931bc-205">Agora crie uma identidade do aplicativo para seu aplicativo Web ou aplicativo de API conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="931bc-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="931bc-206">Em Olá **configurações do Active Directory do Azure** folha, defina **modo de gerenciamento** muito**Express**.</span><span class="sxs-lookup"><span data-stu-id="931bc-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="931bc-207">Escolha **Criar novo aplicativo do AD**.</span><span class="sxs-lookup"><span data-stu-id="931bc-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="931bc-208">Dê um nome à identidade do aplicativo e escolha **OK**.</span><span class="sxs-lookup"><span data-stu-id="931bc-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Criar identidade do aplicativo para seu aplicativo Web ou aplicativo de API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="931bc-210">Em Olá **autenticação / folha de autorização**, escolha **salvar**.</span><span class="sxs-lookup"><span data-stu-id="931bc-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="931bc-211">Agora você deve localizar a ID do cliente hello e ID de locatário para a identidade de aplicativo hello associada com o aplicativo web ou aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="931bc-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="931bc-212">Você usará essas IDs na Parte 3.</span><span class="sxs-lookup"><span data-stu-id="931bc-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="931bc-213">Para continuar com estas etapas para Olá portal do Azure ou [portal clássico do Azure](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="931bc-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="931bc-214">**Localizar a ID do cliente da identidade do aplicativo e a ID do locatário para seu aplicativo web ou aplicativo de API no hello portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="931bc-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="931bc-215">Em **Provedores de Autenticação**, escolha **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="931bc-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Escolha "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="931bc-217">Em Olá **configurações do Active Directory do Azure** folha, defina **modo de gerenciamento** muito**avançado**.</span><span class="sxs-lookup"><span data-stu-id="931bc-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="931bc-218">Saudação de cópia **ID do cliente**e salve o GUID para uso na parte 3.</span><span class="sxs-lookup"><span data-stu-id="931bc-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="931bc-219">Se **ID do cliente** e **Url do emissor** não aparecer, tente atualizar Olá portal do Azure e repita a etapa 1.</span><span class="sxs-lookup"><span data-stu-id="931bc-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="931bc-220">Em **Url do emissor**, copiar e salvar apenas hello GUID para a parte 3.</span><span class="sxs-lookup"><span data-stu-id="931bc-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="931bc-221">Você também pode usar esse GUID no modelo de implantação do aplicativo Web ou aplicativo de API, se necessário.</span><span class="sxs-lookup"><span data-stu-id="931bc-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="931bc-222">Esse GUID é GUID específico do locatário ("ID de locatário") e deve aparecer nessa URL: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="931bc-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="931bc-223">Sem salvar as alterações, fechar Olá **configurações do Active Directory do Azure** folha.</span><span class="sxs-lookup"><span data-stu-id="931bc-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="931bc-224">**Localizar a ID do cliente da identidade do aplicativo e ID de locatário para seu aplicativo web ou aplicativo de API no hello portal clássico do Azure**</span><span class="sxs-lookup"><span data-stu-id="931bc-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="931bc-225">Nas Olá portal clássico do Azure, escolha [ **do Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="931bc-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="931bc-226">Selecione o diretório de saudação que você pode usar para seu aplicativo web ou aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="931bc-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="931bc-227">Em Olá **pesquisa** , localize e selecione a identidade de aplicativo hello para seu aplicativo web ou aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="931bc-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="931bc-228">Em Olá **configurar** guia, Olá cópia **ID do cliente**e salve o GUID para uso na parte 3.</span><span class="sxs-lookup"><span data-stu-id="931bc-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="931bc-229">Depois de obter a ID do cliente hello, na parte inferior de saudação do hello **configurar** guia, escolha **exibir pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="931bc-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="931bc-230">Copiar URL Olá **documento de metadados de Federação**e procurar toothat URL.</span><span class="sxs-lookup"><span data-stu-id="931bc-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="931bc-231">No documento de metadados de saudação é aberto, localize a raiz de saudação **EntityDescriptor ID** elemento que tem um **entityID** atributo neste formulário:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="931bc-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="931bc-232">Olá GUID nesse atributo é GUID específico do locatário (ID do Locatário).</span><span class="sxs-lookup"><span data-stu-id="931bc-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="931bc-233">Copie a ID de locatário hello e salve essa ID para uso na parte 3 e também toouse em seu aplicativo web ou o modelo de implantação do aplicativo de API, se necessário.</span><span class="sxs-lookup"><span data-stu-id="931bc-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="931bc-234">Para saber mais, consulte esses tópicos:</span><span class="sxs-lookup"><span data-stu-id="931bc-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="931bc-235">Autenticação de usuário para Aplicativos de API no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="931bc-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="931bc-236">Autenticação e autorização no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="931bc-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="931bc-237">**Ativar a autenticação quando implantar com um modelo do Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="931bc-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="931bc-238">Você ainda deve criar uma identidade de aplicativo do AD do Azure para seu aplicativo web ou aplicativo de API que é diferente de identidade de aplicativo hello para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="931bc-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="931bc-239">identidade do aplicativo hello toocreate, siga Olá anterior etapas na parte 2 para Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="931bc-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="931bc-240">Você também pode siga etapas Olá na parte 1, mas verifique toouse-se de que seu aplicativo web ou aplicativo de API real `https://{URL}` para **URL de logon** e **URI da ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="931bc-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="931bc-241">Essas etapas, você tem toosave ambos os computadores cliente Olá ID e a ID de locatário para uso no modelo de implantação do aplicativo e também para a parte 3.</span><span class="sxs-lookup"><span data-stu-id="931bc-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="931bc-242">Quando você cria a identidade de aplicativo de saudação do AD do Azure para seu aplicativo web ou aplicativo de API, você deve usar o hello portal do Azure ou portal clássico do Azure, em vez de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="931bc-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="931bc-243">Olá PowerShell commandlet não configurar permissões de saudação necessária toosign usuários em um site.</span><span class="sxs-lookup"><span data-stu-id="931bc-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="931bc-244">Depois de obter a ID do cliente hello e ID de locatário, inclua essas IDs como um subresource do seu aplicativo web ou aplicativo de API em seu modelo de implantação:</span><span class="sxs-lookup"><span data-stu-id="931bc-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="931bc-245">tooautomatically implantar um aplicativo da web em branco e um aplicativo de lógica junto com a autenticação do Active Directory do Azure, [exibição Olá modelo completa aqui](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), ou clique em **implantar tooAzure** aqui:</span><span class="sxs-lookup"><span data-stu-id="931bc-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="931bc-246">[![Implantar tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="931bc-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="931bc-247">Parte 3: Preencher a seção de autorização de saudação em seu aplicativo de lógica</span><span class="sxs-lookup"><span data-stu-id="931bc-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="931bc-248">modelo anterior Olá já tem essa seção de autorização configurar, mas se estiver criando Olá lógica aplicativo diretamente, você deve incluir a seção de autorização total de saudação.</span><span class="sxs-lookup"><span data-stu-id="931bc-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="931bc-249">Abrir sua definição lógica do aplicativo no modo de exibição de código, vá toohello **HTTP** seção de ação, localizar Olá **autorização** seção e inclua esta linha:</span><span class="sxs-lookup"><span data-stu-id="931bc-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="931bc-250">Elemento</span><span class="sxs-lookup"><span data-stu-id="931bc-250">Element</span></span> | <span data-ttu-id="931bc-251">Descrição</span><span class="sxs-lookup"><span data-stu-id="931bc-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="931bc-252">locatário</span><span class="sxs-lookup"><span data-stu-id="931bc-252">tenant</span></span> |<span data-ttu-id="931bc-253">Olá GUID para o locatário de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="931bc-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="931bc-254">audiência</span><span class="sxs-lookup"><span data-stu-id="931bc-254">audience</span></span> |<span data-ttu-id="931bc-255">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="931bc-255">Required.</span></span> <span data-ttu-id="931bc-256">Olá GUID do recurso de destino Olá que você deseja tooaccess - Olá ID do cliente de identidade de aplicativo hello para seu aplicativo web ou aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="931bc-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="931bc-257">clientId</span><span class="sxs-lookup"><span data-stu-id="931bc-257">clientId</span></span> |<span data-ttu-id="931bc-258">Olá GUID para o cliente Olá solicitando acesso - Olá ID do cliente de identidade de aplicativo hello para seu aplicativo de lógica</span><span class="sxs-lookup"><span data-stu-id="931bc-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="931bc-259">segredo</span><span class="sxs-lookup"><span data-stu-id="931bc-259">secret</span></span> |<span data-ttu-id="931bc-260">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="931bc-260">Required.</span></span> <span data-ttu-id="931bc-261">chave de saudação ou a senha de identidade de aplicativo hello para cliente Olá que está solicitando o token de acesso de saudação</span><span class="sxs-lookup"><span data-stu-id="931bc-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="931bc-262">type</span><span class="sxs-lookup"><span data-stu-id="931bc-262">type</span></span> |<span data-ttu-id="931bc-263">tipo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="931bc-263">hello authentication type.</span></span> <span data-ttu-id="931bc-264">Para autenticação do ActiveDirectoryOAuth, o valor de saudação é `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="931bc-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="931bc-265">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="931bc-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="931bc-266">Proteger chamadas à API por meio de código</span><span class="sxs-lookup"><span data-stu-id="931bc-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="931bc-267">Autenticação de certificado</span><span class="sxs-lookup"><span data-stu-id="931bc-267">Certificate authentication</span></span>

<span data-ttu-id="931bc-268">toovalidate Olá solicitações de entrada do seu aplicativo de lógica de tooyour aplicativo web ou aplicativo de API, você pode usar certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="931bc-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="931bc-269">Saiba tooset seu código, [como autenticação mútua de TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="931bc-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="931bc-270">Em Olá **autorização** seção, inclua esta linha:</span><span class="sxs-lookup"><span data-stu-id="931bc-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="931bc-271">Elemento</span><span class="sxs-lookup"><span data-stu-id="931bc-271">Element</span></span> | <span data-ttu-id="931bc-272">Descrição</span><span class="sxs-lookup"><span data-stu-id="931bc-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="931bc-273">type</span><span class="sxs-lookup"><span data-stu-id="931bc-273">type</span></span> |<span data-ttu-id="931bc-274">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="931bc-274">Required.</span></span> <span data-ttu-id="931bc-275">tipo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="931bc-275">hello authentication type.</span></span> <span data-ttu-id="931bc-276">Para certificados de cliente SSL, o valor de saudação deve ser `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="931bc-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="931bc-277">Senha</span><span class="sxs-lookup"><span data-stu-id="931bc-277">password</span></span> |<span data-ttu-id="931bc-278">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="931bc-278">Required.</span></span> <span data-ttu-id="931bc-279">senha de saudação para acessar o certificado de cliente da saudação (arquivo PFX)</span><span class="sxs-lookup"><span data-stu-id="931bc-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="931bc-280">pfx</span><span class="sxs-lookup"><span data-stu-id="931bc-280">pfx</span></span> |<span data-ttu-id="931bc-281">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="931bc-281">Required.</span></span> <span data-ttu-id="931bc-282">Conteúdo codificado com base64 do certificado de cliente da saudação (arquivo PFX)</span><span class="sxs-lookup"><span data-stu-id="931bc-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="931bc-283">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="931bc-283">Basic authentication</span></span>

<span data-ttu-id="931bc-284">solicitações de entrada toovalidate do seu aplicativo de lógica de tooyour aplicativo web ou aplicativo de API, você pode usar a autenticação básica, como um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="931bc-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="931bc-285">A autenticação básica é um padrão comum, e você pode usar essa autenticação em qualquer idioma usado toobuild seu aplicativo web ou aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="931bc-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="931bc-286">Em Olá **autorização** seção, inclua esta linha:</span><span class="sxs-lookup"><span data-stu-id="931bc-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="931bc-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="931bc-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="931bc-288">Elemento</span><span class="sxs-lookup"><span data-stu-id="931bc-288">Element</span></span> | <span data-ttu-id="931bc-289">Descrição</span><span class="sxs-lookup"><span data-stu-id="931bc-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="931bc-290">type</span><span class="sxs-lookup"><span data-stu-id="931bc-290">type</span></span> |<span data-ttu-id="931bc-291">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="931bc-291">Required.</span></span> <span data-ttu-id="931bc-292">tipo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="931bc-292">hello authentication type.</span></span> <span data-ttu-id="931bc-293">Para a autenticação básica, o valor de saudação deve ser `Basic`.</span><span class="sxs-lookup"><span data-stu-id="931bc-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="931bc-294">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="931bc-294">username</span></span> |<span data-ttu-id="931bc-295">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="931bc-295">Required.</span></span> <span data-ttu-id="931bc-296">saudação de nome de usuário para autenticação</span><span class="sxs-lookup"><span data-stu-id="931bc-296">hello username for authentication</span></span> |
| <span data-ttu-id="931bc-297">Senha</span><span class="sxs-lookup"><span data-stu-id="931bc-297">password</span></span> |<span data-ttu-id="931bc-298">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="931bc-298">Required.</span></span> <span data-ttu-id="931bc-299">senha de saudação para autenticação</span><span class="sxs-lookup"><span data-stu-id="931bc-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="931bc-300">Autenticação do Azure Active Directory pelo código</span><span class="sxs-lookup"><span data-stu-id="931bc-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="931bc-301">Por padrão, a autenticação do AD do Azure Olá que ativar Olá portal do Azure não fornece autorização refinada.</span><span class="sxs-lookup"><span data-stu-id="931bc-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="931bc-302">Por exemplo, essa autenticação bloqueios toojust sua API um locatário específico, não tooa usuário específico ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="931bc-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="931bc-303">aplicativo de lógica de tooyour toorestrict API access por meio de código, extrair cabeçalho Olá que tem Olá JSON web token (JWT).</span><span class="sxs-lookup"><span data-stu-id="931bc-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="931bc-304">Verificar a identidade do chamador hello e rejeitar as solicitações que não correspondem.</span><span class="sxs-lookup"><span data-stu-id="931bc-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="931bc-305">Continuar, tooimplement essa autenticação inteiramente em seu próprio código e não use Olá portal do Azure, Aprenda como muito [autenticar com o Active Directory local em seu aplicativo do Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="931bc-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="931bc-306">toocreate uma identidade de aplicativo para seu aplicativo lógico e usar essa identidade toocall sua API, você deve seguir as etapas anteriores hello.</span><span class="sxs-lookup"><span data-stu-id="931bc-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="931bc-307">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="931bc-307">Next steps</span></span>

* [<span data-ttu-id="931bc-308">Verificar o desempenho do aplicativo lógico com alertas e logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="931bc-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)