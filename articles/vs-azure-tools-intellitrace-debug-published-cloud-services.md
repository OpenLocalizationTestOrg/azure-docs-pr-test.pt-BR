---
title: "serviço com o Visual Studio e o IntelliTrace em nuvem aaaDebugging publicado um Azure | Microsoft Docs"
description: "Saiba como toodebug uma nuvem de serviço com o Visual Studio e o IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="dc0c7-103">Depurando um serviço de nuvem do Azure publicado com o Visual Studio e o IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="dc0c7-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="dc0c7-104">Com o IntelliTrace, você pode registrar em log informações extensas de depuração sobre uma instância de função quando ela é executada no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="dc0c7-105">Se você precisar toofind causa de saudação de um problema, você pode usar toostep de logs do IntelliTrace Olá pelo código do Visual Studio como se ele estivesse sendo executado no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="dc0c7-106">Em vigor, IntelliTrace registra código ambiente e da execução os dados quando o aplicativo do Azure está sendo executado como um serviço de nuvem no Azure e permite que você reproduza os dados de saudação registrado do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="dc0c7-107">Você poderá usar o IntelliTrace se tiver o Visual Studio Enterprise instalado e seu aplicativo Azure se destinar ao .NET Framework 4 ou uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="dc0c7-108">O IntelliTrace coleta informações sobre suas funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="dc0c7-109">máquinas virtuais de saudação para essas funções sempre executadas sistemas operacionais de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="dc0c7-110">Como alternativa, você pode usar [depuração remota](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach diretamente tooa serviço de nuvem está em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc0c7-111">O IntelliTrace destina-se apenas aos cenários de depuração e não deve ser usado para uma implantação de produção.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="dc0c7-112">Configurar o IntelliTrace em um aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="dc0c7-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="dc0c7-113">tooenable IntelliTrace para um aplicativo do Azure, você deve criar e publicar o aplicativo hello de um projeto do Azure do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="dc0c7-114">Você deve configurar o IntelliTrace para seu aplicativo do Azure antes de publicá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="dc0c7-115">Se você publicar seu aplicativo sem configurar o IntelliTrace, é necessário o projeto de saudação toorepublish.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="dc0c7-116">Para obter mais informações, consulte [Publicando projetos de serviços de nuvem do Azure usando o Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="dc0c7-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="dc0c7-117">Quando estiver pronto toodeploy seu aplicativo do Azure, verifique se seus destinos de compilação do projeto são definidos muito**depurar**.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="dc0c7-118">Em **Solution Explorer**, clique com botão direito e, no menu de contexto hello, selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="dc0c7-119">Em Olá **publicar aplicativo do Azure** caixa de diálogo, selecione Olá assinatura do Azure e selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="dc0c7-120">Em Olá **configurações** página, selecione Olá **configurações avançadas** guia.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="dc0c7-121">Ativar Olá **habilitar IntelliTrace** opção toocollect os logs do IntelliTrace para seu aplicativo quando ele é publicado na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="dc0c7-122">toocustomize Olá IntelliTrace configuração básica, selecione **configurações** Avançar muito**habilitar IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![Link de configurações do IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="dc0c7-124">Em Olá **configurações do IntelliTrace** caixa de diálogo, você pode especificar quais eventos toolog, se toocollect chamar informações, toocollect quais módulos e processos de logs para e gravação de toohello de tooallocate quanto espaço.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="dc0c7-125">Para saber mais sobre o IntelliTrace, consulte [Depurando com o IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="dc0c7-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![Configurações do IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="dc0c7-127">o log do IntelliTrace Olá é um arquivo de log circular de tamanho máximo de saudação especificado nas configurações do IntelliTrace hello (tamanho da saudação padrão é 250 MB).</span><span class="sxs-lookup"><span data-stu-id="dc0c7-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="dc0c7-128">Os logs do IntelliTrace são coletados tooa arquivo no sistema de arquivos de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="dc0c7-129">Quando você solicitar logs Olá, um instantâneo é obtido no momento e baixado o computador local tooyour.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="dc0c7-130">Olá serviço de nuvem do Azure foi tooAzure publicado, você pode determinar se o IntelliTrace foi habilitado de saudação do Azure nó **Server Explorer**, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc0c7-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![Gerenciador de Servidores – IntelliTrace habilitado](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="dc0c7-132">Baixar logs do IntelliTrace de uma instância de função</span><span class="sxs-lookup"><span data-stu-id="dc0c7-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="dc0c7-133">Com o Visual Studio, é possível baixar os logs do IntelliTrace de uma instância de função seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="dc0c7-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="dc0c7-134">Em **Server Explorer**, expanda Olá **serviços de nuvem** nó e localize a instância de função cujos logs que você deseja toodownload.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="dc0c7-135">Instância de função hello e Olá s no menu de contexto, selecione **Exibir Logs do IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![Opção de menu Exibir logs do IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="dc0c7-137">os logs do IntelliTrace Olá são arquivo tooa baixado em um diretório no computador local.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="dc0c7-138">Cada vez que você solicitar os logs do IntelliTrace hello, um novo instantâneo é criado.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="dc0c7-139">Enquanto Olá logs estão sendo baixadas, Visual Studio exibe o andamento de saudação da operação de saudação em hello **o Log de atividades do Azure** janela.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="dc0c7-140">Conforme mostrado na figura a seguir de saudação, você pode expandir item de linha de saudação de saudação operação toosee mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="dc0c7-142">Você pode continuar toowork no Visual Studio enquanto os logs do IntelliTrace Olá são baixadas.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="dc0c7-143">Quando o log de saudação download for concluído, ele é aberto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="dc0c7-144">Olá logs do IntelliTrace podem conter as exceções framework hello gera e gerencia posteriormente.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="dc0c7-145">O código interno da estrutura gera essas exceções como uma parte normal de iniciar uma função, de modo que você pode ignorá-las com segurança.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="dc0c7-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc0c7-146">Next steps</span></span>
- [<span data-ttu-id="dc0c7-147">Opções de depuração dos serviços de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="dc0c7-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="dc0c7-148">Publicando um serviço de nuvem do Azure usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc0c7-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)