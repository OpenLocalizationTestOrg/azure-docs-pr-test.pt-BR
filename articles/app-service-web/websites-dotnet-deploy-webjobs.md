---
title: aaaDeploy WebJobs usando o Visual Studio
description: "Saiba como toodeploy do Azure WebJobs tooAzure aplicativos de Web do serviço do aplicativo usando o Visual Studio."
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
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="221c9-103">Implantar Trabalhos Web usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="221c9-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="221c9-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="221c9-104">Overview</span></span>
<span data-ttu-id="221c9-105">Este tópico explica como toouse Visual Studio toodeploy um aplicativo de Console projeto aplicativo web de tooa [do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) como um [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="221c9-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="221c9-106">Para obter informações sobre como toodeploy WebJobs usando Olá [Portal do Azure](https://portal.azure.com), consulte [tarefas de execução em segundo plano com o WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="221c9-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="221c9-107">Ao implantar um projeto do Aplicativo de Console habilitado para Trabalhos Web, o Visual Studio realiza duas tarefas:</span><span class="sxs-lookup"><span data-stu-id="221c9-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="221c9-108">Tempo de execução de cópias de arquivos toohello a pasta apropriada no aplicativo web de saudação (*App_Data/trabalhos/contínua* para trabalhos Web contínuos, *App_Data/trabalhos/disparado* para trabalhos Web agendados e sob demanda).</span><span class="sxs-lookup"><span data-stu-id="221c9-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="221c9-109">Configura [trabalhos do Agendador do Azure](#scheduler) para WebJobs são agendado toorun em momentos específicos.</span><span class="sxs-lookup"><span data-stu-id="221c9-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="221c9-110">(Isso não é necessário para Trabalhos Web contínuos.)</span><span class="sxs-lookup"><span data-stu-id="221c9-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="221c9-111">Um projeto habilitadas WebJobs tem Olá tooit adicionados itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="221c9-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="221c9-112">Olá [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="221c9-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="221c9-113">Um arquivo [webjob-publish-settings.json](#publishsettings) que contém configurações de implantação e agendador.</span><span class="sxs-lookup"><span data-stu-id="221c9-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagrama mostrando o que é adicionado tooa implantação de tooenable de aplicativo de Console como um trabalho Web](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="221c9-115">Você pode adicionar esses tooan itens existentes do projeto de aplicativo de Console ou usar um modelo toocreate um novo projeto de aplicativo de Console WebJobs habilitado.</span><span class="sxs-lookup"><span data-stu-id="221c9-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="221c9-116">Você pode implantar um projeto como um trabalho Web por si só ou vincular projeto da web de tooa para que ele implanta automaticamente sempre que você implantar o projeto da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="221c9-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="221c9-117">projetos toolink, Visual Studio inclui o nome de saudação do projeto de saudação trabalhos Web habilitados em um [webjobs list.json](#webjobslist) arquivo no projeto da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="221c9-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![Diagrama mostrando o projeto do WebJob tooweb projeto de vinculação](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="221c9-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="221c9-119">Prerequisites</span></span>
<span data-ttu-id="221c9-120">Recursos de implantação de trabalhos Web estão disponíveis no Visual Studio quando você instala o hello Azure SDK para .NET:</span><span class="sxs-lookup"><span data-stu-id="221c9-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="221c9-121">[SDK do Azure para .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="221c9-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="221c9-122"><a id="convert"></a>Habilitar a implantação de Trabalhos Web para um projeto do Aplicativo de Console existente</span><span class="sxs-lookup"><span data-stu-id="221c9-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="221c9-123">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="221c9-123">You have two options:</span></span>

* <span data-ttu-id="221c9-124">[Habilitar implantação automática com um projeto Web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="221c9-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="221c9-125">Configure um projeto do Aplicativo de Console existente de forma que ele seja implantado automaticamente como um Trabalho Web quando você implanta o projeto Web.</span><span class="sxs-lookup"><span data-stu-id="221c9-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="221c9-126">Use essa opção quando desejar toorun seu trabalho Web em Olá mesmo aplicativo da web em que você executar Olá relacionados ao aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="221c9-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="221c9-127">[Habilitar implantação sem um projeto Web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="221c9-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="221c9-128">Configure um toodeploy de projeto de aplicativo de Console existente como um trabalho Web por si só, com nenhum projeto da web do link tooa.</span><span class="sxs-lookup"><span data-stu-id="221c9-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="221c9-129">Use essa opção quando quiser toorun um trabalho Web em um aplicativo web por si só, com nenhum aplicativo web em execução no aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="221c9-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="221c9-130">Talvez você queira toodo isso na ordem tooscale capaz de toobe seus recursos de trabalho Web independentemente dos recursos do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="221c9-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="221c9-131"><a id="convertlink"></a> Habilitar a implantação de Trabalhos Web automática com um projeto Web</span><span class="sxs-lookup"><span data-stu-id="221c9-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="221c9-132">Projeto de web hello com o botão direito em **Solution Explorer**e, em seguida, clique em **adicionar** > **projeto existente como Azure WebJob**.</span><span class="sxs-lookup"><span data-stu-id="221c9-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Projeto Existente como Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="221c9-134">Olá [adicionar Azure WebJob](#configure) caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="221c9-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="221c9-135">Em Olá **nome do projeto** lista suspensa, selecione Olá tooadd de projeto de aplicativo de Console como um trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="221c9-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Selecionando projeto na caixa de diálogo Adicionar Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="221c9-137">Olá completa [adicionar Azure WebJob](#configure) caixa de diálogo e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="221c9-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="221c9-138"><a id="convertnolink"></a> Habilitar a implantação de Trabalhos Web sem um projeto Web</span><span class="sxs-lookup"><span data-stu-id="221c9-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="221c9-139">Projeto de aplicativo de Console Olá com o botão direito no **Solution Explorer**e, em seguida, clique em **Publicar como Azure WebJob...** .</span><span class="sxs-lookup"><span data-stu-id="221c9-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publicar como Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="221c9-141">Olá [adicionar Azure WebJob](#configure) caixa de diálogo é exibida com hello projeto selecionado no hello **nome do projeto** caixa.</span><span class="sxs-lookup"><span data-stu-id="221c9-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="221c9-142">Olá completa [adicionar Azure WebJob](#configure) caixa de diálogo e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="221c9-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="221c9-143">Olá **Publicar Web** assistente é exibido.</span><span class="sxs-lookup"><span data-stu-id="221c9-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="221c9-144">Se você não quiser toopublish imediatamente, feche o Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="221c9-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="221c9-145">configurações de saudação que você inseriu são salvos para quando você quiser muito[implantar projeto Olá](#deploy).</span><span class="sxs-lookup"><span data-stu-id="221c9-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="221c9-146"><a id="create"></a>Criar um novo projeto habilitado para Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="221c9-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="221c9-147">toocreate um novo projeto de trabalhos Web habilitados, você pode usar Olá Console projeto modelo e habilitar trabalhos Web implantação do aplicativo conforme explicado em [Olá seção anterior](#convert).</span><span class="sxs-lookup"><span data-stu-id="221c9-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="221c9-148">Como alternativa, você pode usar o modelo de novo projeto de trabalhos Web hello:</span><span class="sxs-lookup"><span data-stu-id="221c9-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="221c9-149">Use o modelo de novo projeto de WebJobs de saudação para um trabalho Web independente</span><span class="sxs-lookup"><span data-stu-id="221c9-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="221c9-150">Criar um projeto e configurá-lo toodeploy por si próprio como um trabalho Web com nenhum projeto da web do link tooa.</span><span class="sxs-lookup"><span data-stu-id="221c9-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="221c9-151">Use essa opção quando quiser toorun um trabalho Web em um aplicativo web por si só, com nenhum aplicativo web em execução no aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="221c9-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="221c9-152">Talvez você queira toodo isso na ordem tooscale capaz de toobe seus recursos de trabalho Web independentemente dos recursos do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="221c9-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="221c9-153">Use o modelo de novo projeto de WebJobs de saudação para um projeto do WebJob tooa vinculado web</span><span class="sxs-lookup"><span data-stu-id="221c9-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="221c9-154">Crie um projeto que é configurado toodeploy automaticamente como um trabalho Web quando um projeto da web em Olá mesma solução é implantada.</span><span class="sxs-lookup"><span data-stu-id="221c9-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="221c9-155">Use essa opção quando desejar toorun seu trabalho Web em Olá mesmo aplicativo da web em que você executar Olá relacionados ao aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="221c9-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="221c9-156">modelo de novo projeto de trabalhos Web Hello automaticamente instala pacotes NuGet e inclui o código em *Program.cs* para Olá [SDK do WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="221c9-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="221c9-157">Se você não quiser toouse Olá SDK do WebJobs, remover ou alterar Olá `host.RunAndBlock` instrução em *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="221c9-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="221c9-158"><a id="createnolink"></a>Use o modelo de novo projeto de WebJobs de saudação para um trabalho Web independente</span><span class="sxs-lookup"><span data-stu-id="221c9-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="221c9-159">Clique em **arquivo** > **novo projeto**e, em seguida, em Olá **novo projeto** clique da caixa de diálogo **nuvem**  >   **Azure WebJob (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="221c9-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Caixa de diálogo Novo Projeto mostrando o modelo de Trabalho Web](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="221c9-161">Siga as direções Olá mostradas anteriormente muito[fazer Olá projeto de aplicativo de Console em um projeto de trabalhos Web independente](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="221c9-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="221c9-162"><a id="createlink"></a>Use o modelo de novo projeto de WebJobs de saudação para um projeto do WebJob tooa vinculado web</span><span class="sxs-lookup"><span data-stu-id="221c9-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="221c9-163">Projeto de web hello com o botão direito em **Solution Explorer**e, em seguida, clique em **adicionar** > **novo projeto do Azure WebJob**.</span><span class="sxs-lookup"><span data-stu-id="221c9-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Entrada de menu de Novo Projeto de Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="221c9-165">Olá [adicionar Azure WebJob](#configure) caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="221c9-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="221c9-166">Olá completa [adicionar Azure WebJob](#configure) caixa de diálogo e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="221c9-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="221c9-167"><a id="configure"></a>caixa de diálogo Olá adicionar Azure WebJob</span><span class="sxs-lookup"><span data-stu-id="221c9-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="221c9-168">Olá **adicionar Azure WebJob** caixa de diálogo permite que você insira o nome do trabalho Web hello e execute a configuração do modo de seu trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="221c9-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Caixa de diálogo Adicionar Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="221c9-170">campos de saudação nesta caixa de diálogo correspondem toofields em Olá **novo trabalho** caixa de diálogo de saudação Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="221c9-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="221c9-171">Para obter mais informações, consulte [Executar tarefas em segundo plano com o Trabalhos Web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="221c9-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="221c9-172">Para obter informações sobre a implantação de linha de comando, consulte [Habilitando a entrega de linha de comando ou contínua de Trabalhos Web do Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="221c9-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="221c9-173">Se você implantar um trabalho Web e, em seguida, decide toochange tipo de saudação do trabalho Web e reimplantação, você precisará de arquivo do toodelete Olá settings.json publicar webjobs.</span><span class="sxs-lookup"><span data-stu-id="221c9-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="221c9-174">Isso fará com que o Visual Studio Mostrar Olá opções de publicação novamente, para que você pode alterar o tipo de saudação do WebJob.</span><span class="sxs-lookup"><span data-stu-id="221c9-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="221c9-175">Se você implantar um trabalho Web e depois altera Olá modo de execução de contínuo toonon contínua ou vice-versa, o Visual Studio cria um novo trabalho de Web no Azure ao reimplantar.</span><span class="sxs-lookup"><span data-stu-id="221c9-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="221c9-176">Se você alterar outras configurações de agendamento, mas deixe executar modo Olá mesmo ou alternar entre programada e sob demanda, atualizações do Visual Studio Olá trabalho existente em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="221c9-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="221c9-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="221c9-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="221c9-178">Quando você configura um aplicativo de Console para a implantação de trabalhos Web, o Visual Studio instala Olá [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet pacote e armazena informações de agendamento um *settings.json publicar webjob*  arquivo no projeto Olá *propriedades* pasta do projeto de trabalhos Web hello.</span><span class="sxs-lookup"><span data-stu-id="221c9-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="221c9-179">Aqui está um exemplo desse arquivo:</span><span class="sxs-lookup"><span data-stu-id="221c9-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="221c9-180">É possível editar esse arquivo diretamente, e o Visual Studio fornece o IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="221c9-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="221c9-181">esquema de arquivo Hello é armazenada em [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) e pode ser exibido lá.</span><span class="sxs-lookup"><span data-stu-id="221c9-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="221c9-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="221c9-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="221c9-183">Quando você vincula um projeto do projeto habilitadas WebJobs tooa da web, Visual Studio armazena o nome de saudação do projeto de trabalhos Web hello em um *webjobs list.json* arquivo do projeto da web hello *propriedades* pasta.</span><span class="sxs-lookup"><span data-stu-id="221c9-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="221c9-184">lista de saudação pode conter vários projetos de trabalhos Web, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="221c9-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

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

<span data-ttu-id="221c9-185">É possível editar esse arquivo diretamente, e o Visual Studio fornece o IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="221c9-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="221c9-186">esquema de arquivo Hello é armazenada em [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) e pode ser exibido lá.</span><span class="sxs-lookup"><span data-stu-id="221c9-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="221c9-187"><a id="deploy"></a>Implantar um projeto de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="221c9-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="221c9-188">Um projeto de WebJobs que você vinculou projeto da web de tooa implanta automaticamente com o projeto da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="221c9-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="221c9-189">Para obter informações sobre a implantação de projeto da web, consulte [como toodeploy tooWeb aplicativos](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="221c9-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="221c9-190">toodeploy um projeto de trabalhos Web por si só, clique com botão direito Olá em **Solution Explorer** e clique em **Publicar como Azure WebJob...** .</span><span class="sxs-lookup"><span data-stu-id="221c9-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publicar como Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="221c9-192">Para um trabalho Web independente, Olá mesmo **Publicar Web** assistente que é usado para projetos da web é exibido, mas com menos toochange disponíveis de configurações.</span><span class="sxs-lookup"><span data-stu-id="221c9-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="221c9-193"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="221c9-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="221c9-194">Este artigo explicou como toodeploy trabalhos Web usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="221c9-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="221c9-195">Para obter mais informações sobre como toodeploy WebJobs do Azure, consulte [WebJobs do Azure - recomendado recursos - implantação](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="221c9-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

