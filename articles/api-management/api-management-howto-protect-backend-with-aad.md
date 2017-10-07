---
title: aaaProtect um back-end de API da Web com o Active Directory do Azure e o gerenciamento de API | Microsoft Docs
description: Saiba como tooprotect um back-end de API da Web com o Active Directory do Azure e o gerenciamento de API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="8ae0e-103">Como tooprotect um back-end de API da Web com o Active Directory do Azure e o gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="8ae0e-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="8ae0e-104">Olá seguindo o vídeo mostra como toobuild um back-end de API da Web e protegê-los usando o protocolo OAuth 2.0 com o Active Directory do Azure e o gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="8ae0e-105">Este artigo fornece uma visão geral e informações adicionais para Olá etapas vídeo hello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="8ae0e-106">Este vídeo de 24 minutos mostra como:</span><span class="sxs-lookup"><span data-stu-id="8ae0e-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="8ae0e-107">Criar um back-end de API da Web e protegê-lo com o AAD - iniciando em 1:30</span><span class="sxs-lookup"><span data-stu-id="8ae0e-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="8ae0e-108">Importar Olá API para gerenciamento de API - começando em 7:10</span><span class="sxs-lookup"><span data-stu-id="8ae0e-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="8ae0e-109">Configurar Olá Developer portal toocall Olá API - começando em 9:09</span><span class="sxs-lookup"><span data-stu-id="8ae0e-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="8ae0e-110">Configurar uma saudação do aplicativo de desktop toocall API - começando em 18:08</span><span class="sxs-lookup"><span data-stu-id="8ae0e-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="8ae0e-111">Configurar um toopre de política de validação de JWT-autorizar solicitações - começando em 20:47</span><span class="sxs-lookup"><span data-stu-id="8ae0e-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="8ae0e-112">Criar um diretório do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8ae0e-112">Create an Azure AD directory</span></span>
<span data-ttu-id="8ae0e-113">toosecure API da Web do seu backup usando o Azure Active Directory, primeiro você deve ter um um locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="8ae0e-114">Neste vídeo, um locatário chamado **APIMDemo** é usado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="8ae0e-115">toocreate um locatário do AAD, entrar toohello [Portal clássico do Azure](https://manage.windowsazure.com) e clique em **novo**->**serviços de aplicativos**->**ativa Diretório**->**diretório**->**criação personalizada**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="8ae0e-117">Neste exemplo, um diretório chamado **APIMDemo** é criado com um domínio padrão chamado **DemoAPIM.onmicrosoft.com**. Esse diretório é usado em todo o vídeo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="8ae0e-119">Criar um serviço de API da Web protegido pelo Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8ae0e-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="8ae0e-120">Nesta etapa, um back-end de API da Web é criado usando o Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="8ae0e-121">Esta etapa do hello vídeo começa em 1:30.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="8ae0e-122">projeto de back-end de API da Web toocreate no, clique em Visual Studio **arquivo**->**novo**->**projeto**e escolha **da Web do ASP.NET Aplicativo** de saudação **Web** lista de modelos.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="8ae0e-123">Este vídeo Olá projeto é denominado **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="8ae0e-124">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="8ae0e-126">Clique em **API da Web** de saudação **selecionar uma lista de modelos** toocreate um projeto de API da Web.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="8ae0e-127">Clique em tooconfigure autenticação de diretório do Azure **alterar autenticação**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![Novo Projeto][api-management-new-project]

<span data-ttu-id="8ae0e-129">Clique em **contas organizacionais**e especifique Olá **domínio** do seu locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="8ae0e-130">Olá Este exemplo domínio é **DemoAPIM.onmicrosoft.com**. domínio saudação do seu diretório pode ser obtido Olá **domínios** guia de seu diretório.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![Domínios][api-management-aad-domains]

<span data-ttu-id="8ae0e-132">Definir configurações de saudação desejada no hello **alterar autenticação** caixa de diálogo e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![Alterar Autenticação][api-management-change-authentication]

<span data-ttu-id="8ae0e-134">Quando você clica em **Okey** Visual Studio tentará tooregister seu aplicativo com o diretório do AD do Azure e pode ser solicitado toosign no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="8ae0e-135">Entre usando uma conta administrativa para seu diretório.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-135">Sign in using an administrative account for your directory.</span></span>

![Entrar tooVisual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="8ae0e-137">tooconfigure este projeto como uma saudação de seleção de API da Web do Azure caixa **Host na nuvem Olá** e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![Novo Projeto][api-management-new-project-cloud]

<span data-ttu-id="8ae0e-139">Pode ser solicitado toosign em tooAzure e, em seguida, você pode configurar Olá aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![Configurar][api-management-configure-web-app]

<span data-ttu-id="8ae0e-141">Neste exemplo, um novo **Plano do Serviço de Aplicativo** chamado **APIMAADDemo** é especificado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="8ae0e-142">Clique em **Okey** tooconfigure Olá Web App e crie o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="8ae0e-143">Adicionar projeto de API da Web do hello código toohello</span><span class="sxs-lookup"><span data-stu-id="8ae0e-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="8ae0e-144">a próxima etapa Olá vídeo Olá adiciona o projeto de API da Web do hello código toohello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="8ae0e-145">Esta etapa começa em 4:35.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-145">This step starts at 4:35.</span></span>

<span data-ttu-id="8ae0e-146">Olá API da Web neste exemplo implementa um serviço de calculadora básica usando um modelo e um controlador.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="8ae0e-147">modelo de saudação tooadd para serviço hello, clique **modelos** na **Solution Explorer** e escolha **adicionar**, **classe**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="8ae0e-148">Nome de classe Olá `CalcInput` e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="8ae0e-149">Adicione o seguinte Olá `using` superior de toohello de instrução de saudação `CalcInput.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="8ae0e-150">Substitua classe Olá gerado pelo Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="8ae0e-151">Clique com o botão direito em **Controladores** no **Gerenciador de Soluções** e escolha **Adicionar**->**Controlador**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="8ae0e-152">Clique em **Controlador de API da Web 2 - Vazio**, depois clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="8ae0e-153">Tipo **CalcController** para Olá controlador nome e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![Adicionar controlador][api-management-add-controller]

<span data-ttu-id="8ae0e-155">Adicione o seguinte Olá `using` superior de toohello de instrução de saudação `CalcController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="8ae0e-156">Saudação de substituição gerado classe do controlador com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="8ae0e-157">Esse código implementa Olá `Add`, `Subtract`, `Multiply`, e `Divide` operações de saudação básica API de calculadora.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="8ae0e-158">Pressione **F6** toobuild e verifique se a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="8ae0e-159">Publicar Olá projeto tooAzure</span><span class="sxs-lookup"><span data-stu-id="8ae0e-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="8ae0e-160">Olá essa etapa Visual Studio project é tooAzure publicado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="8ae0e-161">Esta etapa do hello vídeo começa em 5:45.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="8ae0e-162">toopublish Olá tooAzure do projeto, clique com botão direito Olá **APIMAADDemo** do projeto no Visual Studio e escolha **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="8ae0e-163">Manter as configurações padrão de saudação em Olá **Publicar Web** caixa de diálogo e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![Publicar na Web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="8ae0e-165">Conceder permissões de aplicativo de serviço de back-end toohello AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8ae0e-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="8ae0e-166">Um novo aplicativo de serviço de back-end de saudação é criado no diretório do AD do Azure como parte da configuração de saudação e o processo de publicação do seu projeto de API da Web.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="8ae0e-167">Nesta etapa do hello vídeo, começando em 6:13, permissões são concedidas back-end do toohello API da Web.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![Aplicativo][api-management-aad-backend-app]

<span data-ttu-id="8ae0e-169">Clique em nome Olá Olá tooconfigure Olá necessário de permissões de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="8ae0e-170">Navegue toohello **configurar** guia e role para baixo toohello **permissões tooother aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="8ae0e-171">Clique Olá **permissões de aplicativo** lista suspensa ao lado de **Windows** **Active Directory do Azure**, marque caixa Olá **ler dados do diretório**e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![Adicionar permissões][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="8ae0e-173">Se **Windows** **Active Directory do Azure** não é listado em aplicativos de tooother de permissões, clique em **Adicionar aplicativo** e adicioná-lo da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="8ae0e-174">Anote Olá **URI da Id do aplicativo** para uso em uma etapa posterior, quando um aplicativo do AD do Azure está configurado para o portal do desenvolvedor de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![URI da Id do aplicativo][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="8ae0e-176">Importar Olá API da Web para gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="8ae0e-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="8ae0e-177">APIs são configurados da saudação API portal do publicador, que pode é acessada por meio de saudação Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="8ae0e-178">tooreach-la, clique em **portal do publicador** na barra de ferramentas de saudação do seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="8ae0e-179">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [gerenciar sua primeira API] [ Manage your first API] tutorial.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="8ae0e-181">Operações podem ser [adicionado tooAPIs manualmente](api-management-howto-add-operations.md), ou eles podem ser importados.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="8ae0e-182">Neste vídeo, as operações são importadas no formato Swagger começando em 6:40.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="8ae0e-183">Crie um arquivo chamado `calcapi.json` com conteúdo a seguir e salve-o computador tooyour.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="8ae0e-184">Certifique-se de que Olá `host` atributo aponta back-end do tooyour API da Web.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="8ae0e-185">Neste exemplo, `"host": "apimaaddemo.azurewebsites.net"` é usado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="8ae0e-186">Calculadora de saudação tooimport API, clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **importação API**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Botão Importar API][api-management-import-api]

<span data-ttu-id="8ae0e-188">Execute Olá etapas tooconfigure Olá Calculadora API a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="8ae0e-189">Clique em **do arquivo**, procurar toohello `calculator.json` arquivo que você salvou e clique em Olá **Swagger** botão de opção.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="8ae0e-190">Tipo **calc** em Olá **sufixo de URL da API da Web** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="8ae0e-191">Clique em Olá **produtos (opcionais)** caixa e escolha **Starter**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="8ae0e-192">Clique em **salvar** tooimport Olá API.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-192">Click **Save** tooimport hello API.</span></span>

![Adicionar nova API][api-management-import-new-api]

<span data-ttu-id="8ae0e-194">Depois que Olá API é importado, hello página Resumo para a API de saudação é exibida no portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="8ae0e-195">Chamar API Olá com êxito do portal do desenvolvedor Olá</span><span class="sxs-lookup"><span data-stu-id="8ae0e-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="8ae0e-196">Neste ponto, Olá API foi importado para o gerenciamento de API, mas não pode ainda ser chamado com êxito do portal do desenvolvedor Olá porque o serviço de back-end de saudação é protegido com a autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="8ae0e-197">Isso é demonstrado no vídeo Olá começando com 7:40 usando Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="8ae0e-198">Clique em **portal do desenvolvedor** Olá superior-direita do portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-menu]

<span data-ttu-id="8ae0e-200">Clique em **APIs** e clique em Olá **Calculadora** API.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-200">Click **APIs** and click hello **Calculator** API.</span></span>

![Portal do desenvolvedor][api-management-dev-portal-apis]

<span data-ttu-id="8ae0e-202">Clique em **Experimentar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-202">Click **Try it**.</span></span>

![Experimente][api-management-dev-portal-try-it]

<span data-ttu-id="8ae0e-204">Clique em **enviar** e observe o status de resposta de saudação do **401 não autorizado**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![Enviar][api-management-dev-portal-send-401]

<span data-ttu-id="8ae0e-206">solicitação de saudação não está autorizada porque Olá API back-end está protegido pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="8ae0e-207">Antes de chamar com êxito a API de saudação portal do desenvolvedor Olá deve ser configurado tooauthorize desenvolvedores usando OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="8ae0e-208">Esse processo é descrito nas seções a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="8ae0e-209">Registrar o portal do desenvolvedor hello como um aplicativo AAD</span><span class="sxs-lookup"><span data-stu-id="8ae0e-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="8ae0e-210">Olá primeira etapa na configuração de desenvolvedores de tooauthorize portal do desenvolvedor hello usando OAuth 2.0 é o portal do desenvolvedor Olá tooregister como um aplicativo AAD.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="8ae0e-211">Isso é demonstrado começando em 8:27 vídeo hello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="8ae0e-212">Navegue toohello AD do Azure locatário da primeira etapa Olá neste vídeo, neste exemplo **APIMDemo** e navegue toohello **aplicativos** guia.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![Novo aplicativo][api-management-aad-new-application-devportal]

<span data-ttu-id="8ae0e-214">Clique em Olá **adicionar** botão toocreate um novo aplicativo do Active Directory do Azure e escolha **adicionar um aplicativo que minha organização esteja desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Novo aplicativo][api-management-new-aad-application-menu]

<span data-ttu-id="8ae0e-216">Escolha **Web aplicativo e/ou API da Web**, insira um nome e clique em seta Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="8ae0e-217">Neste exemplo, **APIMDeveloperPortal** é usado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-217">In this example **APIMDeveloperPortal** is used.</span></span>

![Novo aplicativo][api-management-aad-new-application-devportal-1]

<span data-ttu-id="8ae0e-219">Para **URL de logon** digite Olá URL de seu serviço de gerenciamento de API e acrescente `/signin`.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="8ae0e-220">Neste exemplo, `https://contoso5.portal.azure-api.net/signin` é usado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="8ae0e-221">Para **URL de Id do aplicativo** digite Olá URL de seu serviço de gerenciamento de API e acrescenta alguns caracteres exclusivos.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="8ae0e-222">Eles podem ser qualquer caractere desejado e, neste exemplo, `https://contoso5.portal.azure-api.net/dp` é usado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="8ae0e-223">Quando a saudação desejado **propriedades do aplicativo** são configuradas, clique em aplicativo de saudação de toocreate hello marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![Novo aplicativo][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="8ae0e-225">Configurar um servidor de autorização do OAuth 2.0 no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="8ae0e-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="8ae0e-226">Olá próxima etapa é tooconfigure um servidor de autorização OAuth 2.0 no gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="8ae0e-227">Esta etapa é demonstrada no hello vídeo começando em 9:43.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="8ae0e-228">Clique em **segurança** no menu de gerenciamento de API Olá Olá esquerda, clique em **OAuth 2.0**e, em seguida, clique em **adicionar autorização** server.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server]

<span data-ttu-id="8ae0e-230">Insira um nome e uma descrição opcional na Olá **nome** e **descrição** campos.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="8ae0e-231">Esses campos são do servidor de autorização de saudação OAuth 2.0 tooidentify usado na instância do serviço de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="8ae0e-232">Neste exemplo, **Demonstração de servidor de autorização** é usado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="8ae0e-233">Mais tarde quando você especificar um toobe de servidor OAuth 2.0 usado para autenticação de uma API, você selecionará esse nome.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="8ae0e-234">Para Olá **URL de página de registro de cliente** Insira um valor de espaço reservado como `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="8ae0e-235">Olá **URL de página de registro de cliente** pontos toohello página que os usuários podem usar toocreate e configurar suas próprias contas para provedores OAuth 2.0 que dão suporte ao gerenciamento de contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="8ae0e-236">Neste exemplo os usuários não criam e configuram suas próprias contas, é usado um espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server-1]

<span data-ttu-id="8ae0e-238">Em seguida, especifique a **URL de ponto de extremidade de autorização** e a **URL de ponto de extremidade de Token**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Servidor de autorização][api-management-add-authorization-server-1a]

<span data-ttu-id="8ae0e-240">Esses valores podem ser recuperados de saudação **pontos de extremidade do aplicativo** página do aplicativo AAD que você criou para o portal do desenvolvedor de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="8ae0e-241">Navegue de pontos de extremidade de saudação tooaccess toohello **configurar** guia para o aplicativo do AAD hello e clique em **exibir pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![Aplicativo][api-management-aad-devportal-application]

![Exibir pontos de extremidade][api-management-aad-view-endpoints]

<span data-ttu-id="8ae0e-244">Saudação de cópia **ponto de extremidade de autorização OAuth 2.0** e cole-a saudação **URL de ponto de extremidade de autorização** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server-2]

<span data-ttu-id="8ae0e-246">Saudação de cópia **ponto de extremidade de token OAuth 2.0** e cole-a saudação **URL de ponto de extremidade de Token** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server-2a]

<span data-ttu-id="8ae0e-248">Além disso toopasting no ponto de extremidade token hello, adicionar um parâmetro de corpo adicional denominado **recurso** e valor Olá use Olá **URI da Id do aplicativo** de saudação aplicativo AAD para o serviço de back-end de saudação foi criado quando o projeto do Visual Studio Olá foi publicado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![URI da Id do aplicativo][api-management-aad-sso-uri]

<span data-ttu-id="8ae0e-250">Em seguida, especifique as credenciais do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="8ae0e-251">Essas são as credenciais de saudação para o recurso de saudação desejado tooaccess, nesse caso Olá portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![Credenciais do cliente][api-management-client-credentials]

<span data-ttu-id="8ae0e-253">Olá tooget **Id do cliente**, navegar toohello **configurar** guia do aplicativo AAD para Olá Olá de portal e a cópia do desenvolvedor de saudação **Id do cliente**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="8ae0e-254">Olá tooget **segredo do cliente** clique Olá **selecionar duração** suspensa no hello **chaves** seção e especificar um intervalo.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="8ae0e-255">Neste exemplo, 1 ano é usado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-255">In this example 1 year is used.</span></span>

![ID do cliente][api-management-aad-client-id]

<span data-ttu-id="8ae0e-257">Clique em **salvar** toosave Olá configuração e exibição Olá a chave.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8ae0e-258">Anote esta chave.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-258">Make a note of this key.</span></span> <span data-ttu-id="8ae0e-259">Quando você fechar a janela de configuração do Active Directory do Azure hello, chave de saudação não pode ser exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="8ae0e-260">Copiar Olá chave toohello área de transferência, switch back toohello portal do publicador, cole a chave de saudação na Olá **segredo do cliente** caixa de texto e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server-3]

<span data-ttu-id="8ae0e-262">Imediatamente após as credenciais do cliente Olá é uma concessão de código de autorização.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="8ae0e-263">Copie esse código de autorização e switch back tooyour aplicativo de portal de desenvolvedor do AD do Azure para Configurar página e cole a concessão de autorização Olá Olá **URL de resposta** campo e, em seguida, clique em **salvar** novamente.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![URL de resposta][api-management-aad-reply-url]

<span data-ttu-id="8ae0e-265">Olá próxima etapa é tooconfigure permissões de saudação para o portal do desenvolvedor Olá aplicativo AAD.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="8ae0e-266">Clique em **permissões de aplicativo** e marque caixa Olá **ler dados do diretório**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="8ae0e-267">Clique em **salvar** toosave isso alterar e, em seguida, clique em **Adicionar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![Adicionar permissões][api-management-add-devportal-permissions]

<span data-ttu-id="8ae0e-269">Clique ícone de pesquisa hello, tipo **APIM** em hello a partir da caixa, selecione **APIMAADDemo**e clique em Olá toosave de marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![Adicionar permissões][api-management-aad-add-app-permissions]

<span data-ttu-id="8ae0e-271">Clique em **permissões delegadas** para **APIMAADDemo** e marque caixa Olá **acesso APIMAADDemo**e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="8ae0e-272">Isso permite que o desenvolvedor de saudação serviço de back-end do aplicativo de portal tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![Adicionar permissões][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="8ae0e-274">Ativar a autorização de usuário OAuth 2.0 para Olá API de Calculadora</span><span class="sxs-lookup"><span data-stu-id="8ae0e-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="8ae0e-275">Olá servidor OAuth 2.0 já está configurado, você pode especificá-lo nas configurações de segurança de saudação para sua API.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="8ae0e-276">Esta etapa é demonstrada no hello vídeo começando na 14:30.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="8ae0e-277">Clique em **APIs** no hello menus à esquerda e clique em **Calculadora** tooview e definir suas configurações.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![API de Calculadora][api-management-calc-api]

<span data-ttu-id="8ae0e-279">Navegue toohello **segurança** guia, verifique Olá **OAuth 2.0** caixa de seleção servidor de autorização desejado Olá select de saudação **servidor de autorização** lista suspensa e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![API de Calculadora][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="8ae0e-281">Chame com sucesso Olá API de Calculadora do portal do desenvolvedor Olá</span><span class="sxs-lookup"><span data-stu-id="8ae0e-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="8ae0e-282">Autorização Olá OAuth 2.0 já está configurado no hello API, suas operações podem ser chamadas com êxito do Centro de desenvolvedores de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="8ae0e-283">Esta etapa é demonstrada no hello vídeo iniciando às 15:00.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="8ae0e-284">Navegue back toohello **adicionar dois inteiros** operação do serviço de calculadora Olá no portal do desenvolvedor hello e clique em **Experimente**.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="8ae0e-285">Observação Olá novo item no hello **autorização** seção servidor de autorização toohello correspondente que acabou de adicionar.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![API de Calculadora][api-management-calc-authorization-server]

<span data-ttu-id="8ae0e-287">Selecione **código de autorização** da autorização Olá suspensa lista e digite as credenciais de saudação do hello conta toouse.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="8ae0e-288">Se você já tiver entrado com conta Olá que não pode ser solicitado.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-288">If you are already signed in with hello account you may not be prompted.</span></span>

![API de Calculadora][api-management-devportal-authorization-code]

<span data-ttu-id="8ae0e-290">Clique em **enviar** e observe hello **status da resposta** de **200 Okey** e resultados de saudação da operação de saudação no conteúdo de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![API de Calculadora][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="8ae0e-292">Configurar uma saudação do aplicativo de desktop toocall API</span><span class="sxs-lookup"><span data-stu-id="8ae0e-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="8ae0e-293">próximo procedimento Olá Olá vídeo inicia às 16:30 e configura uma saudação do aplicativo de área de trabalho simples toocall API.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="8ae0e-294">Olá primeira etapa é um aplicativo de área de trabalho tooregister hello no AD do Azure e dê a ele serviço de back-end acesso toohello diretório e toohello.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="8ae0e-295">18:25 há uma demonstração do aplicativo de área de trabalho hello chamar uma operação em Calculadora Olá API.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="8ae0e-296">Configurar um toopre de política de validação de JWT-autorizar solicitações</span><span class="sxs-lookup"><span data-stu-id="8ae0e-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="8ae0e-297">Olá procedimento final vídeo Olá inicia às 20:48 e mostra como Olá toouse [validar JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) política toopre-autorizar solicitações, validando tokens de acesso de saudação de cada solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="8ae0e-298">Se a solicitação de saudação não for validada pelo Olá política validar JWT, solicitação de Olá está bloqueada pela API de gerenciamento e não é passada toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="8ae0e-299">Para outra demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: recursos de gerenciamento de API mais](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too13:50.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="8ae0e-300">Avanço too15:00 toosee políticas de saudação configuradas no editor de diretiva de saudação e, em seguida, too18:50 para ver uma demonstração de como chamar uma operação do portal do desenvolvedor do hello com e sem Olá necessário token de autorização.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ae0e-301">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ae0e-301">Next steps</span></span>
* <span data-ttu-id="8ae0e-302">Confira mais [vídeos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) sobre o Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="8ae0e-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="8ae0e-303">Para outra maneiras toosecure seu serviço de back-end, consulte [autenticação mútua de certificado](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="8ae0e-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
