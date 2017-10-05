---
title: Proteger um back-end de API da Web com o Azure Active Directory e o Gerenciamento de API | Microsoft Docs
description: Saiba como proteger um back-end de API da Web com o Active Directory do Azure e Gerenciamento de API
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
ms.openlocfilehash: 0dfb4102904c2e972e6617fd3851fb1c50147357
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-protect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="bbbd1-103">Como proteger um back-end de API da Web com o Active Directory do Azure e Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="bbbd1-103">How to protect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="bbbd1-104">O vídeo a seguir mostra como criar um back-end de API da Web e protegê-lo usando o protocolo OAuth 2.0 com o Active Directory do Azure e Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-104">The following video shows how to build a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="bbbd1-105">Este artigo fornece uma visão geral e informações adicionais sobre as etapas no vídeo.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-105">This article provides an overview and additional information for the steps in the video.</span></span> <span data-ttu-id="bbbd1-106">Este vídeo de 24 minutos mostra como:</span><span class="sxs-lookup"><span data-stu-id="bbbd1-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="bbbd1-107">Criar um back-end de API da Web e protegê-lo com o AAD - iniciando em 1:30</span><span class="sxs-lookup"><span data-stu-id="bbbd1-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="bbbd1-108">Importar a API para o Gerenciamento de APIs - iniciando em 7:10</span><span class="sxs-lookup"><span data-stu-id="bbbd1-108">Import the API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="bbbd1-109">Configurar o portal do Desenvolvedor para chamar a API - iniciando em 9:09</span><span class="sxs-lookup"><span data-stu-id="bbbd1-109">Configure the Developer portal to call the API - starting at 9:09</span></span>
* <span data-ttu-id="bbbd1-110">Configurar um aplicativo de área de trabalho para chamar a API - iniciando em 18:08</span><span class="sxs-lookup"><span data-stu-id="bbbd1-110">Configure a desktop application to call the API - starting at 18:08</span></span>
* <span data-ttu-id="bbbd1-111">Configurar uma política de validação de JWT para pré-autorizar solicitações - iniciando em 20:47</span><span class="sxs-lookup"><span data-stu-id="bbbd1-111">Configure a JWT validation policy to pre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="bbbd1-112">Criar um diretório do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bbbd1-112">Create an Azure AD directory</span></span>
<span data-ttu-id="bbbd1-113">Para proteger sua API da Web usando o Active Directory do Azure, você deve primeiramente ter um locatário AAD.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-113">To secure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="bbbd1-114">Neste vídeo, um locatário chamado **APIMDemo** é usado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="bbbd1-115">Para criar um locatário do AAD, entre no [Portal Clássico do Azure](https://manage.windowsazure.com) e clique em **Novo**->**Serviço de Aplicativos**->**Active Directory**->**Diretório**->**Criação Personalizada**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-115">To create an AAD tenant, sign-in to the [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="bbbd1-117">Neste exemplo, um diretório chamado **APIMDemo** é criado com um domínio padrão chamado **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="bbbd1-118">Esse diretório é usado em todo o vídeo.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-118">This directory is used throughout the video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="bbbd1-120">Criar um serviço de API da Web protegido pelo Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="bbbd1-120">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="bbbd1-121">Nesta etapa, um back-end de API da Web é criado usando o Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-121">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="bbbd1-122">Esta etapa do vídeo começa em 1:30.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-122">This step of the video starts at 1:30.</span></span> <span data-ttu-id="bbbd1-123">Para criar o projeto de back-end de API da Web no Visual Studio clique em **Arquivo**->**Novo**->**Projeto** e escolha **Aplicativo Web ASP.NET** na lista de modelos da **Web**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-123">To create Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from the **Web** templates list.</span></span> <span data-ttu-id="bbbd1-124">Neste vídeo, o projeto é denominado **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-124">In this video the project is named **APIMAADDemo**.</span></span> <span data-ttu-id="bbbd1-125">Clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-125">Click **OK** to create the project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="bbbd1-127">Clique em **API Web** em **Selecionar uma lista de modelos** para criar um projeto de API da Web.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-127">Click **Web API** from the **Select a template list** to create a Web API project.</span></span> <span data-ttu-id="bbbd1-128">Para configurar a Autenticação do Azure Directory clique em **Alterar Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-128">To configure Azure Directory Authentication click **Change Authentication**.</span></span>

![Novo Projeto][api-management-new-project]

<span data-ttu-id="bbbd1-130">Clique em **Contas Organizacionais** e especifique o **Domínio** do seu locatário AAD.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-130">Click **Organizational Accounts**, and specify the **Domain** of your AAD tenant.</span></span> <span data-ttu-id="bbbd1-131">Neste exemplo é o domínio **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-131">In this example the domain is **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="bbbd1-132">O domínio do seu diretório pode ser obtido a partir da guia **Domínios** do seu diretório.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-132">The domain of your directory can be obtained from the **Domains** tab of your directory.</span></span>

![Domínios][api-management-aad-domains]

<span data-ttu-id="bbbd1-134">Defina as configurações desejadas na caixa de diálogo **Alterar Autenticação** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-134">Configure the desired settings in the **Change Authentication** dialog box and click **OK**.</span></span>

![Alterar Autenticação][api-management-change-authentication]

<span data-ttu-id="bbbd1-136">Quando você clica em **OK** o Visual Studio tenta registrar seu aplicativo com o diretório do AD do Azure e você talvez precise entrar pelo Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-136">When you click **OK** Visual Studio will attempt to register your application with your Azure AD directory and you may be prompted to sign in by Visual Studio.</span></span> <span data-ttu-id="bbbd1-137">Entre usando uma conta administrativa para seu diretório.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-137">Sign in using an administrative account for your directory.</span></span>

![Entrar no Visual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="bbbd1-139">Para configurar esse projeto como uma API da Web do Azure marque a caixa de **Host na nuvem** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-139">To configure this project as an Azure Web API check the box for **Host in the cloud** and then click **OK**.</span></span>

![Novo Projeto][api-management-new-project-cloud]

<span data-ttu-id="bbbd1-141">Você pode ser solicitado a entrar no Azure e, em seguida, você pode configurar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-141">You may be prompted to sign in to Azure, and then you can configure the Web App.</span></span>

![Configurar][api-management-configure-web-app]

<span data-ttu-id="bbbd1-143">Neste exemplo, um novo **Plano do Serviço de Aplicativo** chamado **APIMAADDemo** é especificado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-143">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="bbbd1-144">Clique em **OK** para configurar o aplicativo Web e criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-144">Click **OK** to configure the Web App and create the project.</span></span>

## <a name="add-the-code-to-the-web-api-project"></a><span data-ttu-id="bbbd1-145">Adicione o código ao projeto de API da Web</span><span class="sxs-lookup"><span data-stu-id="bbbd1-145">Add the code to the Web API project</span></span>
<span data-ttu-id="bbbd1-146">A próxima etapa no vídeo adiciona o código no projeto de API da Web.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-146">The next step in the video adds the code to the Web API project.</span></span> <span data-ttu-id="bbbd1-147">Esta etapa começa em 4:35.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-147">This step starts at 4:35.</span></span>

<span data-ttu-id="bbbd1-148">A API da Web neste exemplo implementa um serviço de calculadora básica usando um modelo e um controlador.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-148">The Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="bbbd1-149">Para adicionar o modelo para o serviço, clique com botão direito em **Modelos** no **Gerenciador de Soluções** e escolha **Adicionar**, **Classe**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-149">To add the model for the service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="bbbd1-150">Nomeie a classe como `CalcInput` e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-150">Name the class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="bbbd1-151">Adicione a seguinte declaração `using` no topo do arquivo `CalcInput.cs`.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-151">Add the following `using` statement to the top of the `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="bbbd1-152">Substitua a classe gerada pelo seguinte código.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-152">Replace the generated class with the following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="bbbd1-153">Clique com o botão direito em **Controladores** no **Gerenciador de Soluções** e escolha **Adicionar**->**Controlador**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-153">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="bbbd1-154">Clique em **Controlador de API da Web 2 - Vazio**, depois clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-154">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="bbbd1-155">Digite **CalcController** para o nome do controlador e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-155">Type **CalcController** for the Controller name and click **Add**.</span></span>

![Adicionar controlador][api-management-add-controller]

<span data-ttu-id="bbbd1-157">Adicione a seguinte declaração `using` no topo do arquivo `CalcController.cs`.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-157">Add the following `using` statement to the top of the `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="bbbd1-158">Substitua a classe do controlador gerado pelo seguinte código.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-158">Replace the generated controller class with the following code.</span></span> <span data-ttu-id="bbbd1-159">Esse código implementa as operações `Add`, `Subtract`, `Multiply` e `Divide` da API básica de calculadora.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-159">This code implements the `Add`, `Subtract`, `Multiply`, and `Divide` operations of the Basic Calculator API.</span></span>

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

<span data-ttu-id="bbbd1-160">Pressione **F6** para compilar e verificar a solução.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-160">Press **F6** to build and verify the solution.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="bbbd1-161">Publicar o projeto no Azure</span><span class="sxs-lookup"><span data-stu-id="bbbd1-161">Publish the project to Azure</span></span>
<span data-ttu-id="bbbd1-162">Nesta etapa o projeto do Visual Studio é publicado no Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-162">In this step the Visual Studio project is published to Azure.</span></span> <span data-ttu-id="bbbd1-163">Esta etapa do vídeo começa em 5:45.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-163">This step of the video starts at 5:45.</span></span>

<span data-ttu-id="bbbd1-164">Para publicar o projeto no Azure, clique com o botão direito no projeto **APIMAADDemo** no Visual Studio e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-164">To publish the project to Azure, right-click the **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="bbbd1-165">Mantenha as configurações padrão na caixa de diálogo **Publicar Web** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-165">Keep the default settings in the **Publish Web** dialog box and click **Publish**.</span></span>

![Publicar na Web][api-management-web-publish]

## <a name="grant-permissions-to-the-azure-ad-backend-service-application"></a><span data-ttu-id="bbbd1-167">Concessão de permissões para o aplicativo de serviço de back-end do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bbbd1-167">Grant permissions to the Azure AD backend service application</span></span>
<span data-ttu-id="bbbd1-168">Um novo aplicativo do serviço de back-end é criado no diretório do AD do Azure como parte do processo de publicação e configuração do seu projeto de API da Web.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-168">A new application for the backend service is created in your Azure AD directory as part of the configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="bbbd1-169">Nesta etapa do vídeo, começando em 6:13, as permissões são concedidas no back-end de API da Web.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-169">In this step of the video, starting at 6:13, permissions are granted to the Web API backend.</span></span>

![Aplicativo][api-management-aad-backend-app]

<span data-ttu-id="bbbd1-171">Clique no nome do aplicativo para configurar as permissões necessárias.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-171">Click the name of the application to configure the required permissions.</span></span> <span data-ttu-id="bbbd1-172">Navegue até a guia **Configurar** e role para baixo até a seção **permissões para outros aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-172">Navigate to the **Configure** tab and scroll down to the **permissions to other applications** section.</span></span> <span data-ttu-id="bbbd1-173">Clique na lista suspensa **Permissões de Aplicativo** ao lado do **Microsoft** **Azure Active Directory**, marque a caixa **Ler dados do diretório** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-173">Click the **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check the box for **Read directory data**, and click **Save**.</span></span>

![Adicionar permissões][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="bbbd1-175">Se o **Microsoft** **Azure Active Directory** não estiver listado em permissões para outros aplicativos, clique em **Adicionar aplicativo** e adicione-o da lista.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-175">If **Windows** **Azure Active Directory** is not listed under permissions to other applications, click **Add application** and add it from the list.</span></span>
> 
> 

<span data-ttu-id="bbbd1-176">Anote a **URI da Id do aplicativo** para uso em uma etapa posterior, quando um aplicativo do AD do Azure é configurado para o portal do desenvolvedor de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-176">Make a note of the **App Id URI** for use in a subsequent step when an Azure AD application is configured for the API Management developer portal.</span></span>

![URI da Id do aplicativo][api-management-aad-sso-uri]

## <a name="import-the-web-api-into-api-management"></a><span data-ttu-id="bbbd1-178">Importar a API da Web para o Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="bbbd1-178">Import the Web API into API Management</span></span>
<span data-ttu-id="bbbd1-179">APIs são configuradas no portal do publicador da API, que pode ser acessado no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-179">APIs are configured from the API publisher portal, which is accessed through the Azure Portal.</span></span> <span data-ttu-id="bbbd1-180">Para acessá-lo, clique em **Portal do publicador** na barra de ferramentas do seu serviço Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-180">To reach it, click **Publisher portal** from the toolbar of your API Management service.</span></span> <span data-ttu-id="bbbd1-181">Se você ainda não tiver criado uma instância de serviço de Gerenciamento de API, veja [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Gerenciar sua primeira API][Manage your first API].</span><span class="sxs-lookup"><span data-stu-id="bbbd1-181">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API][Manage your first API] tutorial.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="bbbd1-183">As operações podem ser [adicionadas manualmente às APIs](api-management-howto-add-operations.md)ou podem ser importadas.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-183">Operations can be [added to APIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="bbbd1-184">Neste vídeo, as operações são importadas no formato Swagger começando em 6:40.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-184">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="bbbd1-185">Crie um arquivo chamado `calcapi.json` com o conteúdo a seguir e salve-o em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-185">Create a file named `calcapi.json` with following contents and save it to your computer.</span></span> <span data-ttu-id="bbbd1-186">Verifique os pontos do atributo `host` para o back-end da API da Web.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-186">Ensure that the `host` attribute points to your Web API backend.</span></span> <span data-ttu-id="bbbd1-187">Neste exemplo, `"host": "apimaaddemo.azurewebsites.net"` é usado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-187">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

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

<span data-ttu-id="bbbd1-188">Para importar a API de calculadora, clique em **APIs** no menu **Gerenciamento de API** à esquerda e depois clique em **Importar API**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-188">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Botão Importar API][api-management-import-api]

<span data-ttu-id="bbbd1-190">Execute as seguintes etapas para configurar a API de calculadora.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-190">Perform the following steps to configure the calculator API.</span></span>

1. <span data-ttu-id="bbbd1-191">Clique em **Do arquivo**, navegue até arquivo `calculator.json` que foi salvo e clique no botão de opção **Swagger**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-191">Click **From file**, browse to the `calculator.json` file you saved, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="bbbd1-192">Digite **calc** na caixa de texto **Sufixo da URL da API Web**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-192">Type **calc** into the **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="bbbd1-193">Clique na caixa **Produtos (opcional)** e escolha **Inicial**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-193">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="bbbd1-194">Clique em **Salvar** para importar a API.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-194">Click **Save** to import the API.</span></span>

![Adicionar nova API][api-management-import-new-api]

<span data-ttu-id="bbbd1-196">Depois que a API é importada, a página de resumo para a API é exibida no portal do editor.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-196">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

## <a name="call-the-api-unsuccessfully-from-the-developer-portal"></a><span data-ttu-id="bbbd1-197">Chamar a API sem êxito a partir do portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="bbbd1-197">Call the API unsuccessfully from the developer portal</span></span>
<span data-ttu-id="bbbd1-198">Neste ponto, a API foi importada para o Gerenciamento de API, mas não pode ainda ser chamada com êxito a partir do portal do desenvolvedor porque o serviço de back-end é protegido com a autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-198">At this point, the API has been imported into API Management, but cannot yet be called successfully from the developer portal because the backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="bbbd1-199">Isso é demonstrado no vídeo começando em 7:40 usando as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-199">This is demonstrated in the video starting at 7:40 using the following steps.</span></span>

<span data-ttu-id="bbbd1-200">Clique em **Portal do desenvolvedor** do lado superior direito do portal do publicador.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-200">Click **Developer portal** from the top-right side of the publisher portal.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-menu]

<span data-ttu-id="bbbd1-202">Clique em **APIs** e clique na API **Calculadora**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-202">Click **APIs** and click the **Calculator** API.</span></span>

![Portal do desenvolvedor][api-management-dev-portal-apis]

<span data-ttu-id="bbbd1-204">Clique em **Experimentar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-204">Click **Try it**.</span></span>

![Experimente][api-management-dev-portal-try-it]

<span data-ttu-id="bbbd1-206">Clique em **Enviar** e observe o status de resposta **401 não autorizado**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-206">Click **Send** and note the response status of **401 Unauthorized**.</span></span>

![Enviar][api-management-dev-portal-send-401]

<span data-ttu-id="bbbd1-208">A solicitação é não autorizada porque a API de back-end é protegida pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-208">The request is unauthorized because the backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="bbbd1-209">Antes de chamar a API com êxito o portal do desenvolvedor deve ser configurado para autorizar os desenvolvedores que usam OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-209">Before successfully calling the API the developer portal must be configured to authorize developers using OAuth 2.0.</span></span> <span data-ttu-id="bbbd1-210">Cada atributo é descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-210">This process is described in the following sections.</span></span>

## <a name="register-the-developer-portal-as-an-aad-application"></a><span data-ttu-id="bbbd1-211">Registrar o portal do desenvolvedor como um aplicativo AAD</span><span class="sxs-lookup"><span data-stu-id="bbbd1-211">Register the developer portal as an AAD application</span></span>
<span data-ttu-id="bbbd1-212">A primeira etapa na configuração do portal do desenvolvedor para autorizar os desenvolvedores que usam o OAuth 2.0 é registrar o portal do desenvolvedor como um aplicativo AAD.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-212">The first step in configuring the developer portal to authorize developers using OAuth 2.0 is to register the developer portal as an AAD application.</span></span> <span data-ttu-id="bbbd1-213">Isso é demonstrado começando em 8:27 no vídeo.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-213">This is demonstrated starting at 8:27 in the video.</span></span>

<span data-ttu-id="bbbd1-214">Navegue até o locatário do Azure AD da primeira etapa deste vídeo, neste exemplo **APIMDemo** e navegue até a guia **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-214">Navigate to the Azure AD tenant from the first step of this video, in this example **APIMDemo** and navigate to the **Applications** tab.</span></span>

![Novo aplicativo][api-management-aad-new-application-devportal]

<span data-ttu-id="bbbd1-216">Clique no botão **Adicionar** para criar um novo aplicativo do Azure Active Directory e escolha **Adicionar um aplicativo que minha organização está desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-216">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Novo aplicativo][api-management-new-aad-application-menu]

<span data-ttu-id="bbbd1-218">Escolha **Aplicativo Web e/ou API Web**, insira um nome e clique na seta Próximo.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-218">Choose **Web application and/or Web API**, enter a name, and click the next arrow.</span></span> <span data-ttu-id="bbbd1-219">Neste exemplo, **APIMDeveloperPortal** é usado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-219">In this example **APIMDeveloperPortal** is used.</span></span>

![Novo aplicativo][api-management-aad-new-application-devportal-1]

<span data-ttu-id="bbbd1-221">Para a **URL de Entrada**, insira a URL do seu serviço de Gerenciamento de API e acrescente `/signin`.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-221">For **Sign-on URL** enter the URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="bbbd1-222">Neste exemplo, `https://contoso5.portal.azure-api.net/signin` é usado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-222">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="bbbd1-223">Para a **URL da Id do aplicativo** insira a URL do seu serviço de Gerenciamento de API e acrescente alguns caracteres exclusivos.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-223">For **App Id URL** enter the URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="bbbd1-224">Eles podem ser qualquer caractere desejado e, neste exemplo, `https://contoso5.portal.azure-api.net/dp` é usado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-224">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="bbbd1-225">Quando as **Propriedades do aplicativo** desejadas forem configuradas, clique na marca de seleção para criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-225">When the  desired **App properties** are configured, click the check mark to create the application.</span></span>

![Novo aplicativo][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="bbbd1-227">Configurar um servidor de autorização do OAuth 2.0 no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="bbbd1-227">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="bbbd1-228">A próxima etapa é configurar um servidor de autorização OAuth 2.0 no gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-228">The next step is to configure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="bbbd1-229">Esta etapa é demonstrada no vídeo, começando em 9:43.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-229">This step is demonstrated in the video starting at 9:43.</span></span>

<span data-ttu-id="bbbd1-230">Clique em **Segurança** no menu de Gerenciamento de API à esquerda, clique em **OAuth 2.0** e em **Adicionar servidor de autorização**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-230">Click **Security** from the API Management menu on the left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server]

<span data-ttu-id="bbbd1-232">Insira um nome e uma descrição opcional nos campos **Nome** e **Descrição**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-232">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> <span data-ttu-id="bbbd1-233">Esses campos são usados para identificar o servidor de autorização OAuth 2.0 dentro da instância do serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-233">These fields are used to identify the OAuth 2.0 authorization server within the API Management service instance.</span></span> <span data-ttu-id="bbbd1-234">Neste exemplo, **Demonstração de servidor de autorização** é usado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-234">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="bbbd1-235">Posteriormente quando você especificar um servidor OAuth 2.0 para ser usado para autenticação para uma API, você selecionará esse nome.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-235">Later when you specify an OAuth 2.0 server to be used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="bbbd1-236">Para a **URL de página de registro do cliente**, insira um valor de espaço reservado como `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-236">For the **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="bbbd1-237">A **URL de página de registro do cliente** aponta para a página que os usuários podem usar para criar e configurar suas próprias contas para provedores OAuth 2.0 que dão suporte a gerenciamento de contas por usuários.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-237">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="bbbd1-238">Neste exemplo os usuários não criam e configuram suas próprias contas, é usado um espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-238">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server-1]

<span data-ttu-id="bbbd1-240">Em seguida, especifique a **URL de ponto de extremidade de autorização** e a **URL de ponto de extremidade de Token**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-240">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Servidor de autorização][api-management-add-authorization-server-1a]

<span data-ttu-id="bbbd1-242">Esses valores podem ser recuperados na página **Pontos de extremidade do aplicativo** do aplicativo AAD criado para o portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-242">These values can be retrieved from the **App Endpoints** page of the AAD application you created for the developer portal.</span></span> <span data-ttu-id="bbbd1-243">Para acessar os pontos de extremidade navegue até a guia **Configurar** para o aplicativo AAD e clique em **Exibir pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-243">To access the endpoints navigate to the **Configure** tab for the AAD application and click **View endpoints**.</span></span>

![Aplicativo][api-management-aad-devportal-application]

![Exibir pontos de extremidade][api-management-aad-view-endpoints]

<span data-ttu-id="bbbd1-246">Copie o **ponto de extremidade da autorização OAuth 2.0** e cole-o na caixa de texto **URL de ponto de extremidade de autorização**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-246">Copy the **OAuth 2.0 authorization endpoint** and paste it into the **Authorization endpoint URL** textbox.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server-2]

<span data-ttu-id="bbbd1-248">Copie o **ponto de extremidade do token OAuth 2.0** e cole-o na caixa de texto **URL de ponto de extremidade de token**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-248">Copy the **OAuth 2.0 token endpoint** and paste it into the **Token endpoint URL** textbox.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server-2a]

<span data-ttu-id="bbbd1-250">Além de colá-lo no ponto de extremidade de token, adicione um parâmetro de corpo adicional chamado **recurso** e para o valor use a **URI da Id do aplicativo** AAD do serviço de back-end criado quando o projeto do Visual Studio foi publicado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-250">In addition to pasting in the token endpoint, add an additional body parameter named **resource** and for the value use the **App Id URI** from the AAD application for the backend service that was created when the Visual Studio project was published.</span></span>

![URI da Id do aplicativo][api-management-aad-sso-uri]

<span data-ttu-id="bbbd1-252">Em seguida, especifique as credenciais do cliente.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-252">Next, specify the client credentials.</span></span> <span data-ttu-id="bbbd1-253">Essas são as credenciais para o recurso que você quer acessar, nesse caso, o portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-253">These are the credentials for the resource you want to access, in this case the developer portal.</span></span>

![Credenciais do cliente][api-management-client-credentials]

<span data-ttu-id="bbbd1-255">Para obter a **Id do Cliente**, navegue até a guia **Configurar** do aplicativo AAD para o portal de desenvolvedor e copie a **Id do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-255">To get the **Client Id**, navigate to the **Configure** tab of the AAD application for the developer portal and copy the **Client Id**.</span></span>

<span data-ttu-id="bbbd1-256">Para obter o **Segredo do Cliente** clique em **Selecionar duração** na seção **Chaves** e especifique um intervalo.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-256">To get the **Client Secret** click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="bbbd1-257">Neste exemplo, 1 ano é usado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-257">In this example 1 year is used.</span></span>

![Id do Cliente][api-management-aad-client-id]

<span data-ttu-id="bbbd1-259">Clique em **Salvar** para salvar a configuração e exibir a chave.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-259">Click **Save** to save the configuration and display the key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bbbd1-260">Anote esta chave.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-260">Make a note of this key.</span></span> <span data-ttu-id="bbbd1-261">Depois que você fechar a janela de configuração do Active Directory do Azure, a chave não pode ser exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-261">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="bbbd1-262">Copie a chave para a área de transferência, alterne de volta para o portal do publicador, cole a chave na caixa de texto **Segredo do Cliente** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-262">Copy the key to the clipboard, switch back to the publisher portal, paste the key into the **Client Secret** textbox, and click **Save**.</span></span>

![Adicionar servidor de autorização][api-management-add-authorization-server-3]

<span data-ttu-id="bbbd1-264">Imediatamente após as credenciais do cliente está uma concessão de código de autorização.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-264">Immediately following the client credentials is an authorization code grant.</span></span> <span data-ttu-id="bbbd1-265">Copie esse código de autorização e volte para a página de configuração do seu aplicativo de portal do desenvolvedor do Azure AD e cole a concessão de autorização no campo **URL de Resposta** e clique em **Salvar** novamente.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-265">Copy this authorization code and switch back to your Azure AD developer portal application configure page, and paste the authorization grant into the **Reply URL** field, and click **Save** again.</span></span>

![URL de resposta][api-management-aad-reply-url]

<span data-ttu-id="bbbd1-267">A próxima etapa é configurar as permissões para o aplicativo AAD do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-267">The next step is to configure the permissions for the developer portal AAD application.</span></span> <span data-ttu-id="bbbd1-268">Clique em **Permissões de Aplicativo** e marque a caixa **Ler dados do diretório**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-268">Click **Application Permissions** and check the box for **Read directory data**.</span></span> <span data-ttu-id="bbbd1-269">Clique em **Salvar** para salvar essa alteração e, em seguida, clique em **Adicionar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-269">Click **Save** to save this change, and then click **Add application**.</span></span>

![Adicionar permissões][api-management-add-devportal-permissions]

<span data-ttu-id="bbbd1-271">Clique no ícone de pesquisa, digite **APIM** na caixa Iniciando com, selecione **APIMAADDemo** e clique na marca de seleção para salvar.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-271">Click the search icon, type **APIM** into the Starting with box, select **APIMAADDemo**, and click the check mark to save.</span></span>

![Adicionar permissões][api-management-aad-add-app-permissions]

<span data-ttu-id="bbbd1-273">Clique em **Permissões Delegadas** para **APIMAADDemo** e marque a caixa Acessar **APIMAADDemo** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-273">Click **Delegated Permissions** for **APIMAADDemo** and check the box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="bbbd1-274">Isso permite que o aplicativo do portal do desenvolvedor acesse o serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-274">This allows the developer portal application to access the backend service.</span></span>

![Adicionar permissões][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-the-calculator-api"></a><span data-ttu-id="bbbd1-276">Habilitar autorização do usuário OAuth 2.0 para a API de Calculadora</span><span class="sxs-lookup"><span data-stu-id="bbbd1-276">Enable OAuth 2.0 user authorization for the Calculator API</span></span>
<span data-ttu-id="bbbd1-277">Agora que o servidor OAuth 2.0 está configurado, você pode especificá-lo nas configurações de segurança para sua API.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-277">Now that the OAuth 2.0 server is configured, you can specify it in the security settings for your API.</span></span> <span data-ttu-id="bbbd1-278">Esta etapa é demonstrada no vídeo, começando em 14:30.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-278">This step is demonstrated in the video starting at 14:30.</span></span>

<span data-ttu-id="bbbd1-279">Clique em **APIs** no menu à esquerda e clique em **Calculadora** para exibir e definir suas configurações.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-279">Click **APIs** in the left menu, and click  **Calculator** to view and configure its settings.</span></span>

![API de Calculadora][api-management-calc-api]

<span data-ttu-id="bbbd1-281">Navegue até a guia **Segurança**, marque a caixa de seleção **OAuth 2.0**, selecione o servidor de autorização desejado na lista suspensa **Servidor de autorização** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-281">Navigate to the **Security** tab, check the **OAuth 2.0** checkbox, select the desired authorization server from the **Authorization server** drop-down, and click **Save**.</span></span>

![API de Calculadora][api-management-enable-aad-calculator]

## <a name="successfully-call-the-calculator-api-from-the-developer-portal"></a><span data-ttu-id="bbbd1-283">Chamar com êxito a API de Calculadora do portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="bbbd1-283">Successfully call the Calculator API from the developer portal</span></span>
<span data-ttu-id="bbbd1-284">A autorização do OAuth 2.0 já está configurado na API, suas operações podem ser chamadas com êxito no centro do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-284">Now that the OAuth 2.0 authorization is configured on the API, its operations can be successfully called from the developer center.</span></span> <span data-ttu-id="bbbd1-285">Esta etapa é demonstrada no vídeo, começando em 15:00.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-285">THis step is demonstrated in the video starting at 15:00.</span></span>

<span data-ttu-id="bbbd1-286">Navegue de volta para a operação **Adicionar dois inteiros** do serviço da calculadora no portal do desenvolvedor e clique em **Experimente**.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-286">Navigate back to the **Add two integers** operation of the calculator service in the developer portal and click **Try it**.</span></span> <span data-ttu-id="bbbd1-287">Observe o novo item na seção **Autorização** correspondente ao servidor de autorização que você acabou de adicionar.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-287">Note the new item in the **Authorization** section corresponding to the authorization server you just added.</span></span>

![API de Calculadora][api-management-calc-authorization-server]

<span data-ttu-id="bbbd1-289">Selecione **Código de autorização** na lista suspensa de autorização e insira as credenciais da conta a ser usada.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-289">Select **Authorization code** from the authorization drop-down list and enter the credentials of the account to use.</span></span> <span data-ttu-id="bbbd1-290">Se você já estiver conectado com a conta pode ser que você não seja solicitado.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-290">If you are already signed in with the account you may not be prompted.</span></span>

![API de Calculadora][api-management-devportal-authorization-code]

<span data-ttu-id="bbbd1-292">Clique em **Enviar** e observe o **Status da resposta** **200 OK** e os resultados da operação no conteúdo da resposta.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-292">Click **Send** and note the **Response status** of **200 OK** and the results of the operation in the response content.</span></span>

![API de Calculadora][api-management-devportal-response]

## <a name="configure-a-desktop-application-to-call-the-api"></a><span data-ttu-id="bbbd1-294">Configurar um aplicativo de área de trabalho para chamar a API</span><span class="sxs-lookup"><span data-stu-id="bbbd1-294">Configure a desktop application to call the API</span></span>
<span data-ttu-id="bbbd1-295">O próximo procedimento no vídeo começa em 16:30 e configura um aplicativo de área de trabalho simples para chamar a API.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-295">The next procedure in the video starts at 16:30 and configures a simple desktop application to call the API.</span></span> <span data-ttu-id="bbbd1-296">A primeira etapa é registrar o aplicativo de área de trabalho no AD do Azure e fornecer acesso ao diretório e ao serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-296">The first step is to register the desktop application in Azure AD and give it access to the directory and to the backend service.</span></span> <span data-ttu-id="bbbd1-297">Em 18:25 há uma demonstração do aplicativo da área de trabalho chamando uma operação na API da calculadora.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-297">At 18:25 there is a demonstration of the desktop application calling an operation on the calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-to-pre-authorize-requests"></a><span data-ttu-id="bbbd1-298">Configurar uma diretiva de validação de JWT para pré-autorizar solicitações</span><span class="sxs-lookup"><span data-stu-id="bbbd1-298">Configure a JWT validation policy to pre-authorize requests</span></span>
<span data-ttu-id="bbbd1-299">O procedimento final no vídeo começa em 20:48 e mostra como usar a diretiva [Validar JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) para pré-autorizar solicitações validando os tokens de acesso de cada solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-299">The final procedure in the video starts at 20:48 and shows you how to use the [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy to pre-authorize requests by validating the access tokens of each incoming request.</span></span> <span data-ttu-id="bbbd1-300">Se a solicitação não é validada pela política Validar JWT, a solicitação é bloqueada pelo Gerenciamento de API e não é passada para o back-end.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-300">If the request is not validated by the Validate JWT policy, the request is blocked by API Management and is not passed along to the backend.</span></span>

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

<span data-ttu-id="bbbd1-301">Para outra demonstração de configuração e uso dessa diretiva, consulte [Abordagem da nuvem Episódio 177: Mais recursos de Gerenciamento de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e avance para 13:50.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-301">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="bbbd1-302">Avance para 15:00 para ver as diretivas configuradas no editor de diretiva e, em seguida, 18:50 para uma demonstração de como chamar uma operação do portal do desenvolvedor com e sem o token de autorização necessário.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-302">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbbd1-303">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bbbd1-303">Next steps</span></span>
* <span data-ttu-id="bbbd1-304">Confira mais [vídeos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) sobre o Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="bbbd1-304">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="bbbd1-305">Para outras maneiras de proteger seu serviço de back-end, confira [Autenticação de certificado mútuo](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="bbbd1-305">For other ways to secure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

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
