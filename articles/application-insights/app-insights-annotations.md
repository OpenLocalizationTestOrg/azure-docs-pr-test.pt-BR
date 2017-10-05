---
title: "Anotações de versão para o Application Insights | Microsoft Docs"
description: "Adicione uma implantação ou compile marcadores para seus gráficos do gerenciador de métricas no Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="d3e6c-103">Anotações sobre gráficos de métricas no Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3e6c-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="d3e6c-104">As anotações de versão nos gráficos do [Metrics Explorer](app-insights-metrics-explorer.md) mostram onde você implantou uma nova compilação ou outro evento relevante.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="d3e6c-105">Elas facilitam ver se suas alterações tinham qualquer efeito sobre o desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="d3e6c-106">Elas podem ser criadas automaticamente pelo [sistema de compilação do Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="d3e6c-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="d3e6c-107">Você também pode criar anotações para sinalizar eventos desejados [criando-as no PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="d3e6c-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Exemplo de anotações com correlação visível com tempo de resposta do servidor](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="d3e6c-109">Anotações de versão com a compilação VSTS</span><span class="sxs-lookup"><span data-stu-id="d3e6c-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="d3e6c-110">As anotações de versão são um recurso de compilação baseado em nuvem e serviço de versão do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="d3e6c-111">Instalar a extensão Annotations (uma vez)</span><span class="sxs-lookup"><span data-stu-id="d3e6c-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="d3e6c-112">Para poder criar anotações de versão, você precisará instalar uma das muitas extensões de Team Service disponíveis no Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="d3e6c-113">Entre no seu projeto do [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online).</span><span class="sxs-lookup"><span data-stu-id="d3e6c-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="d3e6c-114">No Visual Studio Marketplace, [obtenha a extensão Anotações de Versão](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)e adicione-a à sua conta do Team Services.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![Na parte superior direita da página da Web do Team Services, abra o Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="d3e6c-117">Você só precisa fazer isso uma vez em sua conta de serviços de equipe do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="d3e6c-118">As anotações de versão agora podem ser configuradas para qualquer projeto na sua conta.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="d3e6c-119">Criar anotações de versão</span><span class="sxs-lookup"><span data-stu-id="d3e6c-119">Configure release annotations</span></span>

<span data-ttu-id="d3e6c-120">Você precisa obter uma chave de API separada para cada modelo de versão do VSTS.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="d3e6c-121">Entre no [Portal do Microsoft Azure](https://portal.azure.com) e abra o recurso Application Insights que monitora seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="d3e6c-122">(Ou [crie um agora](app-insights-overview.md), se você ainda não fez isso.)</span><span class="sxs-lookup"><span data-stu-id="d3e6c-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="d3e6c-123">Abra **Acesso à API**, **ID do Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Em portal.azure.com, abra o recurso do Application Insights e escolha Configurações.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="d3e6c-127">Em um janela de navegador separada, abra (ou crie) o modelo de versão que gerencia suas implantações do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="d3e6c-128">Adicione uma tarefa e selecione a tarefa de anotação de versão do Application Insights do menu.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="d3e6c-129">Cole a **ID do Aplicativo** que você copiou da folha Acesso à API.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![No Visual Studio Team Services, abra Versão, selecione uma definição de versão e escolha Editar.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="d3e6c-133">Defina o campo **APIKey** como uma variável `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="d3e6c-134">De volta à janela do Azure, crie uma nova chave de API e faça uma cópia dela.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Na folha de Acesso à API na janela do Azure, clique em Criar Chave de API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="d3e6c-138">Abra a guia Configuração do modelo de versão.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="d3e6c-139">Crie uma definição de variável para `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="d3e6c-140">Cole sua chave de API para a definição da variável ApiKey.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![Na janela Team Services, selecione a guia Configuração e clique em Adicionar Variável.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="d3e6c-143">Por fim, **Salve** a definição da versão.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="d3e6c-144">Exibir anotações</span><span class="sxs-lookup"><span data-stu-id="d3e6c-144">View annotations</span></span>
<span data-ttu-id="d3e6c-145">Agora, sempre que você usar o modelo de versão para implantar uma nova versão, uma anotação será enviada ao Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="d3e6c-146">As anotações aparecerão em gráficos no Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="d3e6c-147">Clique em qualquer marcador de anotação para abrir os detalhes sobre a versão, incluindo o solicitante, a ramificação de controle do código-fonte, a definição da versão, o ambiente e muito mais.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Clique em qualquer marcador de anotação de versão.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="d3e6c-149">Criar anotações personalizadas no PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3e6c-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="d3e6c-150">Você também pode criar anotações de qualquer processo que desejar (sem usar o VS Team System).</span><span class="sxs-lookup"><span data-stu-id="d3e6c-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="d3e6c-151">Faça uma cópia local do [script do Powershell do GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="d3e6c-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="d3e6c-152">Obtenha a ID do aplicativo e crie uma chave de API na folha Acesso à API.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="d3e6c-153">Chame o script assim:</span><span class="sxs-lookup"><span data-stu-id="d3e6c-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="d3e6c-154">É fácil modificar o script, por exemplo, para criar as anotações para o que já passou.</span><span class="sxs-lookup"><span data-stu-id="d3e6c-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3e6c-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3e6c-155">Next steps</span></span>

* [<span data-ttu-id="d3e6c-156">Criar um item de trabalho</span><span class="sxs-lookup"><span data-stu-id="d3e6c-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="d3e6c-157">Automação com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3e6c-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
