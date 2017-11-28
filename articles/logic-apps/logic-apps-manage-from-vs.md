---
title: "aplicativos de lógica de aaaManage no Visual Studio - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Gerenciar aplicativos lógicos e outros ativos do Azure com o Visual Studio Cloud Explorer"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="0f0ba-103">Gerenciar os aplicativos lógicos com o Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0f0ba-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="0f0ba-104">Embora hello [portal do Azure](https://portal.azure.com/) oferece uma ótima maneira de você toodesign e gerenciar os aplicativos lógicos do Azure, você pode usar o Gerenciador de nuvem do Visual Studio para o gerenciamento de vários ativos do Azure, incluindo aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="0f0ba-105">O Visual Studio Cloud Explorer lhe permite procurar, gerenciar, editar e baixar aplicativos lógicos publicados.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="0f0ba-106">As tarefas de gerenciamento incluem habilitar, desabilitar e visualizar o histórico de execução.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="0f0ba-107">Antes de acessar e gerenciar seus aplicativos lógicos no Visual Studio, instale e configure essas ferramentas do Visual Studio para Aplicativos Lógicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0f0ba-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0f0ba-108">Prerequisites</span></span>

* [<span data-ttu-id="0f0ba-109">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0f0ba-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="0f0ba-110">[SDK mais recente do Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou superior)</span><span class="sxs-lookup"><span data-stu-id="0f0ba-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="0f0ba-111">Gerenciador de Nuvem do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f0ba-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="0f0ba-112">Web toohello de acesso ao usar o designer incorporado Olá</span><span class="sxs-lookup"><span data-stu-id="0f0ba-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="0f0ba-113">Instalar ferramentas do Visual Studio para Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="0f0ba-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="0f0ba-114">Depois de instalar os pré-requisitos do hello, baixar e instalar as ferramentas de aplicativos do hello Azure lógica para o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="0f0ba-115">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-115">Open Visual Studio.</span></span> <span data-ttu-id="0f0ba-116">Em Olá **ferramentas** menu, selecione **extensões e atualizações**.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="0f0ba-117">Expanda Olá **Online** categoria para que você pode pesquisar online na Olá Galeria do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="0f0ba-118">Procure por **Aplicativos Lógicos** até encontrar as **Ferramentas de Aplicativos Lógicos do Azure para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="0f0ba-119">toodownload e extensão de saudação de instalação, clique em **baixar**.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="0f0ba-120">Reinicie o Visual Studio após a instalação.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="0f0ba-121">Olá toodownload ferramentas de aplicativos de lógica do Azure para Visual Studio ir diretamente, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="0f0ba-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="0f0ba-122">Procurar aplicativos lógicos no Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0f0ba-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="0f0ba-123">tooopen Cloud Explorer no hello **exibição** menu, escolha **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="0f0ba-124">Navegue para o aplicativo lógico, por grupo de recursos ou tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="0f0ba-125">Se você procurar pelo tipo de recurso, selecione sua assinatura do Azure, expanda Olá **aplicativos lógicos** seção e, em seguida, selecione o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="0f0ba-126">Se você procurar pelo grupo de recursos, expanda Olá grupo de recursos que tem sua lógica de aplicativo e selecione o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="0f0ba-127">tooview comandos para seu aplicativo de lógica, com o botão direito seu aplicativo lógico tanto na parte inferior de saudação do Cloud Explorer, escolha Olá **ações** menu.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![Navegar para o aplicativo lógico](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="0f0ba-129">Editar o aplicativo lógico com o Designer de Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="0f0ba-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="0f0ba-130">Do Pesquisador de objetos de nuvem, você pode abrir um aplicativo implantado no momento de lógica de Olá designer mesmo que você usa no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="0f0ba-131">tooedit seu aplicativo lógico, no Pesquisador de objetos de nuvem, seu aplicativo de lógica e selecione **abrir com o Editor de lógica de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="0f0ba-132">toopublish seu toohello atualizações de nuvem, escolha **publicar**.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="0f0ba-133">toostart uma nova execução, escolha **disparador executar**.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-133">toostart a new run, choose **Run Trigger**.</span></span>

![Designer de Aplicativos Lógicos](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="0f0ba-135">No designer de hello, você também pode **baixar** um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="0f0ba-136">Essa ação automaticamente parametriza definição de aplicativo hello lógica e salva a definição de saudação como um modelo de implantação do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="0f0ba-137">Você pode adicionar este projeto de grupo de recursos do Azure de tooyour de modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="0f0ba-138">Procurar o histórico de execução do aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="0f0ba-138">Browse your logic app run history</span></span>

<span data-ttu-id="0f0ba-139">Olá tooview executar histórico para seu aplicativo lógico, seu aplicativo de lógica e selecione **histórico de execução de abrir**.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="0f0ba-140">tooreorder seu histórico de execução com base em qualquer cabeçalho de coluna Olá propriedades Olá mostrado, selecione.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![Histórico da execução](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="0f0ba-142">Olá tooshow histórico para uma instância de execução para que você pode rever Olá executar resultados, inclusive entradas hello e saídas de cada etapa, clique duas vezes em uma saudação executar instâncias.</span><span class="sxs-lookup"><span data-stu-id="0f0ba-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![Resultados do histórico de execução, entradas e saídas de etapas](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="0f0ba-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f0ba-144">Next steps</span></span>

* [<span data-ttu-id="0f0ba-145">Criar seu primeiro aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="0f0ba-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="0f0ba-146">Criar, compilar e implantar aplicativos lógicos no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f0ba-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="0f0ba-147">Veja exemplos e cenários comuns</span><span class="sxs-lookup"><span data-stu-id="0f0ba-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="0f0ba-148">Vídeo: Automatizar processos de negócios com os Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="0f0ba-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="0f0ba-149">Vídeo: integrar seus sistemas com os Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="0f0ba-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
