---
title: "aaaRelease anotações para o Application Insights | Microsoft Docs"
description: "Adicionar implantação ou compilação marcadores de gráficos de explorer tooyour métricas no Application Insights."
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
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="3258d-103">Anotações sobre gráficos de métricas no Application Insights</span><span class="sxs-lookup"><span data-stu-id="3258d-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="3258d-104">As anotações de versão nos gráficos do [Metrics Explorer](app-insights-metrics-explorer.md) mostram onde você implantou uma nova compilação ou outro evento relevante.</span><span class="sxs-lookup"><span data-stu-id="3258d-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="3258d-105">Elas facilitam toosee fácil se suas alterações tinham efeito no desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3258d-105">They make it easy toosee whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="3258d-106">Eles podem ser criados automaticamente pelo Olá [sistema de compilação do Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="3258d-106">They can be automatically created by hello [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="3258d-107">Você também pode criar anotações tooflag qualquer evento que você deseja por [criá-las do PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="3258d-107">You can also create annotations tooflag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Exemplo de anotações com correlação visível com tempo de resposta do servidor](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="3258d-109">Anotações de versão com a compilação VSTS</span><span class="sxs-lookup"><span data-stu-id="3258d-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="3258d-110">Anotações de versão são um recurso de compilação de baseado em nuvem hello e versão de serviço do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3258d-110">Release annotations are a feature of hello cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-hello-annotations-extension-one-time"></a><span data-ttu-id="3258d-111">Instalar a extensão de anotações da saudação (uma vez)</span><span class="sxs-lookup"><span data-stu-id="3258d-111">Install hello Annotations extension (one time)</span></span>
<span data-ttu-id="3258d-112">toobe toocreate capaz de versão anotações, você precisará tooinstall um de saudação muitas extensões de serviços de equipe disponíveis no hello Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3258d-112">toobe able toocreate release annotations, you'll need tooinstall one of hello many Team Service extensions available in hello Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="3258d-113">Entrar tooyour [do Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projeto.</span><span class="sxs-lookup"><span data-stu-id="3258d-113">Sign in tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="3258d-114">No Visual Studio Marketplace, [obter Olá versão anotações extensão](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)e adicione-a conta de Team Services tooyour.</span><span class="sxs-lookup"><span data-stu-id="3258d-114">In Visual Studio Marketplace, [get hello Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it tooyour Team Services account.</span></span>

![Na parte superior direita da página da Web do Team Services, abra o Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="3258d-117">Você só precisa toodo desta vez para a sua conta do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3258d-117">You only need toodo this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="3258d-118">As anotações de versão agora podem ser configuradas para qualquer projeto na sua conta.</span><span class="sxs-lookup"><span data-stu-id="3258d-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="3258d-119">Criar anotações de versão</span><span class="sxs-lookup"><span data-stu-id="3258d-119">Configure release annotations</span></span>

<span data-ttu-id="3258d-120">Você precisa de chave de tooget uma API diferente para cada modelo de versão do VSTS.</span><span class="sxs-lookup"><span data-stu-id="3258d-120">You need tooget a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="3258d-121">Entrar toohello [Portal do Microsoft Azure](https://portal.azure.com) e abrir o recurso do Application Insights Olá que monitora o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3258d-121">Sign in toohello [Microsoft Azure Portal](https://portal.azure.com) and open hello Application Insights resource that monitors your application.</span></span> <span data-ttu-id="3258d-122">(Ou [crie um agora](app-insights-overview.md), se você ainda não fez isso.)</span><span class="sxs-lookup"><span data-stu-id="3258d-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="3258d-123">Abra **Acesso à API**, **ID do Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="3258d-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Em portal.azure.com, abra o recurso do Application Insights e escolha Configurações.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="3258d-127">Em uma janela separada do navegador, abra (ou crie) em modelo de liberação de saudação que gerencia as implantações do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3258d-127">In a separate browser window, open (or create) hello release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="3258d-128">Adicionar uma tarefa e selecione a tarefa de anotação de versão do aplicativo Insights de Olá menu hello.</span><span class="sxs-lookup"><span data-stu-id="3258d-128">Add a task, and select hello Application Insights Release Annotation task from hello menu.</span></span>
   
    <span data-ttu-id="3258d-129">Saudação de colar **Id do aplicativo** que você copiou da saudação folha de acesso à API.</span><span class="sxs-lookup"><span data-stu-id="3258d-129">Paste hello **Application Id** that you copied from hello API Access blade.</span></span>
   
    ![No Visual Studio Team Services, abra Versão, selecione uma definição de versão e escolha Editar.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="3258d-133">Saudação de conjunto **APIKey** variável do campo tooa `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="3258d-133">Set hello **APIKey** field tooa variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="3258d-134">Na Olá janela do Azure, crie uma nova chave de API e faça uma cópia dele.</span><span class="sxs-lookup"><span data-stu-id="3258d-134">Back in hello Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![No hello folha de acesso à API no hello janela do Azure, clique em criar chave de API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="3258d-138">Abra o guia de configuração de saudação do modelo de versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3258d-138">Open hello Configuration tab of hello release template.</span></span>
   
    <span data-ttu-id="3258d-139">Crie uma definição de variável para `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="3258d-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="3258d-140">Cole seu toohello de chave de API ApiKey definição da variável.</span><span class="sxs-lookup"><span data-stu-id="3258d-140">Paste your API key toohello ApiKey variable definition.</span></span>
   
    ![Na janela do Team Services hello, selecione a guia de configuração de saudação e clique em Adicionar variável.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="3258d-143">Por fim, **salvar** Olá definição de versão.</span><span class="sxs-lookup"><span data-stu-id="3258d-143">Finally, **Save** hello release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="3258d-144">Exibir anotações</span><span class="sxs-lookup"><span data-stu-id="3258d-144">View annotations</span></span>
<span data-ttu-id="3258d-145">Agora, sempre que usar Olá versão modelo toodeploy uma nova versão, uma anotação será enviada tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="3258d-145">Now, whenever you use hello release template toodeploy a new release, an annotation will be sent tooApplication Insights.</span></span> <span data-ttu-id="3258d-146">anotações de saudação serão exibido nos gráficos do Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="3258d-146">hello annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="3258d-147">Clique no qualquer anotação marcador tooopen detalhes sobre a versão de hello, incluindo o solicitante, branch de controle de origem, definição de versão, ambiente e muito mais.</span><span class="sxs-lookup"><span data-stu-id="3258d-147">Click on any annotation marker tooopen details about hello release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Clique em qualquer marcador de anotação de versão.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="3258d-149">Criar anotações personalizadas no PowerShell</span><span class="sxs-lookup"><span data-stu-id="3258d-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="3258d-150">Você também pode criar anotações de qualquer processo que desejar (sem usar o VS Team System).</span><span class="sxs-lookup"><span data-stu-id="3258d-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="3258d-151">Faça uma cópia local do hello [script do Powershell do GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="3258d-151">Make a local copy of hello [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="3258d-152">Obter Olá ID do aplicativo e criar uma chave de API de saudação folha de acesso à API.</span><span class="sxs-lookup"><span data-stu-id="3258d-152">Get hello Application ID and create an API key from hello API Access blade.</span></span>

3. <span data-ttu-id="3258d-153">Chame o script hello como este:</span><span class="sxs-lookup"><span data-stu-id="3258d-153">Call hello script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="3258d-154">É fácil toomodify script de hello, por exemplo toocreate anotações para Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="3258d-154">It's easy toomodify hello script, for example toocreate annotations for hello past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3258d-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3258d-155">Next steps</span></span>

* [<span data-ttu-id="3258d-156">Criar um item de trabalho</span><span class="sxs-lookup"><span data-stu-id="3258d-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="3258d-157">Automação com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="3258d-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
