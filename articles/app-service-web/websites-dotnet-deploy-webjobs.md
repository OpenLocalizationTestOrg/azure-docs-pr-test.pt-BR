---
title: Implantar Trabalhos Web usando o Visual Studio
description: "Aprenda como implantar Trabalhos Web do Azure para Aplicativos Web do Serviço de Aplicativo do Azure usando o Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="6a021-103">Implantar Trabalhos Web usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6a021-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="6a021-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6a021-104">Overview</span></span>
<span data-ttu-id="6a021-105">Esse tópico explica como usar o Visual Studio para implantar um projeto de Aplicativo de Console para um aplicativo Web do [Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) como um [Trabalho Web do Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="6a021-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="6a021-106">Para obter informações sobre como implantar Trabalhos Web usando o [Portal do Azure](https://portal.azure.com), consulte [Executar tarefas em segundo plano com Trabalhos Web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="6a021-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="6a021-107">Ao implantar um projeto do Aplicativo de Console habilitado para Trabalhos Web, o Visual Studio realiza duas tarefas:</span><span class="sxs-lookup"><span data-stu-id="6a021-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="6a021-108">Copia arquivos de tempo de execução para a pasta apropriada no aplicativo Web (*App_Data/jobs/continuous* para Trabalhos Web contínuos, *App_Data/jobs/triggered* para Trabalhos Web agendados e sob demanda).</span><span class="sxs-lookup"><span data-stu-id="6a021-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="6a021-109">Configura [Trabalhos do Agendador do Azure](#scheduler) para Trabalhos Web agendados a serem executados em determinados horários.</span><span class="sxs-lookup"><span data-stu-id="6a021-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="6a021-110">(Isso não é necessário para Trabalhos Web contínuos.)</span><span class="sxs-lookup"><span data-stu-id="6a021-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="6a021-111">Um projeto habilitado para Trabalhos Web tem os seguintes itens adicionados:</span><span class="sxs-lookup"><span data-stu-id="6a021-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="6a021-112">O pacote NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) .</span><span class="sxs-lookup"><span data-stu-id="6a021-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="6a021-113">Um arquivo [webjob-publish-settings.json](#publishsettings) que contém configurações de implantação e agendador.</span><span class="sxs-lookup"><span data-stu-id="6a021-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagrama que mostra o que é adicionado a um Aplicativo de Console para habilitar implantação como um Trabalho Web](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="6a021-115">É possível adicionar esses itens a um projeto do Aplicativo de Console existente ou usar um modelo para criar um novo projeto do Aplicativo de Console habilitado para Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="6a021-116">É possível implantar um projeto como um Trabalho Web propriamente dito ou vinculá-lo a um projeto Web de forma que ele seja implantado automaticamente sempre que você implanta o projeto Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="6a021-117">Para vincular projetos, o Visual Studio inclui o nome do projeto habilitado para Trabalhos Web em um arquivo [webjobs-list.json](#webjobslist) no projeto Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Diagrama que mostra o projeto de Trabalho Web sendo vinculado ao projeto Web](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="6a021-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a021-119">Prerequisites</span></span>
<span data-ttu-id="6a021-120">Os recursos de implantação do WebJobs estão disponíveis no Visual Studio quando você instala o SDK do Azure para .NET:</span><span class="sxs-lookup"><span data-stu-id="6a021-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="6a021-121">[SDK do Azure para .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6a021-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="6a021-122"><a id="convert"></a>Habilitar a implantação de Trabalhos Web para um projeto do Aplicativo de Console existente</span><span class="sxs-lookup"><span data-stu-id="6a021-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="6a021-123">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="6a021-123">You have two options:</span></span>

* <span data-ttu-id="6a021-124">[Habilitar implantação automática com um projeto Web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="6a021-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="6a021-125">Configure um projeto do Aplicativo de Console existente de forma que ele seja implantado automaticamente como um Trabalho Web quando você implanta o projeto Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="6a021-126">Use esta opção quando quiser executar o Trabalho Web no mesmo aplicativo Web em que você executa o aplicativo Web relacionado.</span><span class="sxs-lookup"><span data-stu-id="6a021-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="6a021-127">[Habilitar implantação sem um projeto Web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="6a021-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="6a021-128">Configure um projeto do Aplicativo de Console existente a ser implantado como um Trabalho Web propriamente dito, sem link para um projeto Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="6a021-129">Use esta opção quando você quiser executar um Trabalho Web em um aplicativo Web por si só, sem nenhum aplicativo Web em execução no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="6a021-130">Você talvez queira fazer isso para ser capaz de dimensionar os recursos de Trabalho Web independentemente dos recursos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="6a021-131"><a id="convertlink"></a> Habilitar a implantação de Trabalhos Web automática com um projeto Web</span><span class="sxs-lookup"><span data-stu-id="6a021-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="6a021-132">Clique com o botão direito do mouse no projeto Web no **Gerenciador de Soluções** e clique em **Adicionar** > **Projeto Existente como Trabalho Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="6a021-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Projeto Existente como Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="6a021-134">A caixa de diálogo [Adicionar Trabalho Web do Azure](#configure) é exibida.</span><span class="sxs-lookup"><span data-stu-id="6a021-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="6a021-135">Na lista suspensa **Nome do projeto** , selecione o projeto do Aplicativo de Console a ser adicionado como um Trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Selecionando projeto na caixa de diálogo Adicionar Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="6a021-137">Complete a caixa de diálogo [Adicionar Trabalho Web do Azure](#configure) e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a021-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="6a021-138"><a id="convertnolink"></a> Habilitar a implantação de Trabalhos Web sem um projeto Web</span><span class="sxs-lookup"><span data-stu-id="6a021-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="6a021-139">Clique com o botão direito do mouse no projeto do Aplicativo de Console no **Gerenciador de Soluções** e, depois, clique em **Publicar como Azure WebJob...**.</span><span class="sxs-lookup"><span data-stu-id="6a021-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publicar como Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="6a021-141">A caixa de diálogo [Adicionar Trabalho Web do Azure](#configure) é exibida, com o projeto selecionado na caixa **Nome do projeto** .</span><span class="sxs-lookup"><span data-stu-id="6a021-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="6a021-142">Complete a caixa de diálogo [Adicionar Trabalho Web do Azure](#configure) e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a021-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="6a021-143">O assistente **Publicar Web** é exibido.</span><span class="sxs-lookup"><span data-stu-id="6a021-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="6a021-144">Se você não desejar publicar imediatamente, feche o assistente.</span><span class="sxs-lookup"><span data-stu-id="6a021-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="6a021-145">As configurações inseridas por você são salvas para quando quiser [implantar o projeto](#deploy).</span><span class="sxs-lookup"><span data-stu-id="6a021-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="6a021-146"><a id="create"></a>Criar um novo projeto habilitado para Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="6a021-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="6a021-147">Para criar um projeto habilitado para Trabalhos Web, é possível usar o modelo de projeto do Aplicativo de Console e habilitar a implantação de Trabalhos Web conforme explicado na [seção anterior](#convert).</span><span class="sxs-lookup"><span data-stu-id="6a021-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="6a021-148">Também é possível usar o modelo do novo projeto de Trabalhos Web:</span><span class="sxs-lookup"><span data-stu-id="6a021-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="6a021-149">Usar o novo modelo de projeto de Trabalhos Web para um Trabalho Web independente</span><span class="sxs-lookup"><span data-stu-id="6a021-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="6a021-150">Crie um projeto e o configure para ser implantado propriamente dito como um Trabalho Web, sem link para um projeto Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="6a021-151">Use esta opção quando você quiser executar um Trabalho Web em um aplicativo Web por si só, sem nenhum aplicativo Web em execução no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="6a021-152">Você talvez queira fazer isso para ser capaz de dimensionar os recursos de Trabalho Web independentemente dos recursos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="6a021-153">Usar o novo modelo de projeto de Trabalhos Web para um Trabalho Web vinculado a um projeto Web</span><span class="sxs-lookup"><span data-stu-id="6a021-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="6a021-154">Crie um projeto que seja configurado para ser implantado automaticamente como um Trabalho Web quando um projeto Web na mesma solução for implantado.</span><span class="sxs-lookup"><span data-stu-id="6a021-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="6a021-155">Use esta opção quando quiser executar o Trabalho Web no mesmo aplicativo Web em que você executa o aplicativo Web relacionado.</span><span class="sxs-lookup"><span data-stu-id="6a021-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="6a021-156">O modelo new-project do WebJobs instala automaticamente pacotes NuGet e inclui o código em *Program.cs* para o [SDK do WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="6a021-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="6a021-157">Se você não desejar usar o SDK do WebJobs, remova ou altere a instrução `host.RunAndBlock` em *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="6a021-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="6a021-158"><a id="createnolink"></a> Usar o novo modelo de projeto de Trabalhos Web para um Trabalho Web independente</span><span class="sxs-lookup"><span data-stu-id="6a021-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="6a021-159">Clique em **Arquivo** > **Novo Projeto** e, depois, na caixa de diálogo **Novo Projeto**, clique em **Nuvem** > **Azure WebJob (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6a021-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Caixa de diálogo Novo Projeto mostrando o modelo de Trabalho Web](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="6a021-161">Siga as direções mostradas anteriormente para [tornar o projeto do Aplicativo de Console um projeto de Trabalhos Web independente](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="6a021-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="6a021-162"><a id="createlink"></a> Usar o novo modelo de projeto de Trabalhos Web para um Trabalho Web vinculado a um projeto Web</span><span class="sxs-lookup"><span data-stu-id="6a021-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="6a021-163">Clique com o botão direito do mouse no projeto Web no **Gerenciador de Soluções** e clique em **Adicionar** > **Novo Projeto de Trabalho Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="6a021-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Entrada de menu de Novo Projeto de Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="6a021-165">A caixa de diálogo [Adicionar Trabalho Web do Azure](#configure) é exibida.</span><span class="sxs-lookup"><span data-stu-id="6a021-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="6a021-166">Complete a caixa de diálogo [Adicionar Trabalho Web do Azure](#configure) e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a021-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="6a021-167"><a id="configure"></a>A caixa de diálogo Adicionar Trabalho Web do Azure</span><span class="sxs-lookup"><span data-stu-id="6a021-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="6a021-168">A caixa de diálogo **Adicionar Azure WebJob** permite inserir o nome do WebJob e executar a configuração de modo do WebJob.</span><span class="sxs-lookup"><span data-stu-id="6a021-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Caixa de diálogo Adicionar Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="6a021-170">Os campos nessa caixa de diálogo correspondem aos campos na caixa de diálogo **Novo Trabalho** do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a021-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="6a021-171">Para obter mais informações, consulte [Executar tarefas em segundo plano com o Trabalhos Web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="6a021-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="6a021-172">Para obter informações sobre a implantação de linha de comando, consulte [Habilitando a entrega de linha de comando ou contínua de Trabalhos Web do Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="6a021-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="6a021-173">Se você implantar um Trabalho Web e, em seguida, decidir que deseja alterar o tipo de Trabalho Web e implantá-lo novamente, você precisará excluir o arquivo webjobs-publish-settings.json.</span><span class="sxs-lookup"><span data-stu-id="6a021-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="6a021-174">Isso fará com que o Visual Studio exiba novamente as opções de publicação para que você possa alterar o tipo de Trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="6a021-175">Se você implantar um Trabalho Web e depois alterar o modo de execução de contínuo para não contínuo ou vice-versa, o Visual Studio criará um novo Trabalho Web no Azure quando você o reimplantar.</span><span class="sxs-lookup"><span data-stu-id="6a021-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="6a021-176">Se você alterar outras configurações de agendamento, mas deixar o modo de execução igual ou alternar Agendado e Sob Demanda, o Visual Studio atualizará o trabalho existente, em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="6a021-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="6a021-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="6a021-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="6a021-178">Quando você configura um Aplicativo de Console para implantação de Trabalhos Web, o Visual Studio instala o pacote NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) e armazena informações de agendamento em um arquivo *webjob-publish-settings.json* na pasta *Propriedades* do projeto dos Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="6a021-179">Aqui está um exemplo desse arquivo:</span><span class="sxs-lookup"><span data-stu-id="6a021-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="6a021-180">É possível editar esse arquivo diretamente, e o Visual Studio fornece o IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="6a021-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="6a021-181">O esquema de arquivo é armazenado em [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) e pode ser exibido aqui.</span><span class="sxs-lookup"><span data-stu-id="6a021-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="6a021-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="6a021-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="6a021-183">Quando você vincula um projeto habilitado para Trabalhos Web a um projeto Web, o Visual Studio armazena o nome do projeto de Trabalhos Web em um arquivo *webjobs-list.json* na pasta *Propriedades* do projeto Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="6a021-184">A lista pode conter vários projetos do WebJobs, conforme mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="6a021-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="6a021-185">É possível editar esse arquivo diretamente, e o Visual Studio fornece o IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="6a021-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="6a021-186">O esquema de arquivo é armazenado em [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) e pode ser exibido aqui.</span><span class="sxs-lookup"><span data-stu-id="6a021-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="6a021-187"><a id="deploy"></a>Implantar um projeto de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="6a021-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="6a021-188">Um projeto de Trabalhos Web vinculado a um projeto Web é implantado automaticamente com o projeto Web.</span><span class="sxs-lookup"><span data-stu-id="6a021-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="6a021-189">Para obter informações sobre a implantação de projetos Web, consulte [Como implantar Aplicativos Web](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6a021-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="6a021-190">Para implantar um projeto do WebJobs sozinho, clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e clique em **Publicar como Azure WebJob...**.</span><span class="sxs-lookup"><span data-stu-id="6a021-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publicar como Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="6a021-192">Para um Trabalho Web independente, o mesmo assistente **Publicar Web** usado em projetos Web é exibido, mas com menos configurações disponíveis para serem alteradas.</span><span class="sxs-lookup"><span data-stu-id="6a021-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="6a021-193"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6a021-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="6a021-194">Este artigo explicou como implantar WebJobs usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a021-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="6a021-195">Para obter mais informações sobre como implantar o Azure WebJobs, consulte [Azure WebJobs – Recursos recomendados - Implantação](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="6a021-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

