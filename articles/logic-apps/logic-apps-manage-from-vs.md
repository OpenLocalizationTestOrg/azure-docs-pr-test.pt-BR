---
title: "Gerenciar aplicativos lógicos no Visual Studio – Aplicativo Lógico do Azure | Microsoft Docs"
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
ms.openlocfilehash: a5bf24de1a7a2b6d4c1ae6416c95d83ef7506da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="a62d2-103">Gerenciar os aplicativos lógicos com o Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="a62d2-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="a62d2-104">Embora o [Portal do Azure](https://portal.azure.com/) ofereça uma excelente maneira para criar e gerenciar Aplicativo Lógico do Azure, é possível usar o Visual Studio Cloud Explorer para gerenciar vários ativos do Azure, incluindo aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="a62d2-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="a62d2-105">O Visual Studio Cloud Explorer lhe permite procurar, gerenciar, editar e baixar aplicativos lógicos publicados.</span><span class="sxs-lookup"><span data-stu-id="a62d2-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="a62d2-106">As tarefas de gerenciamento incluem habilitar, desabilitar e visualizar o histórico de execução.</span><span class="sxs-lookup"><span data-stu-id="a62d2-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="a62d2-107">Antes de acessar e gerenciar seus aplicativos lógicos no Visual Studio, instale e configure essas ferramentas do Visual Studio para Aplicativos Lógicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a62d2-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a62d2-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a62d2-108">Prerequisites</span></span>

* [<span data-ttu-id="a62d2-109">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a62d2-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="a62d2-110">[SDK mais recente do Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou superior)</span><span class="sxs-lookup"><span data-stu-id="a62d2-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="a62d2-111">Gerenciador de Nuvem do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a62d2-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="a62d2-112">Acesso à Web ao usar o designer incorporado</span><span class="sxs-lookup"><span data-stu-id="a62d2-112">Access to the web when using the embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="a62d2-113">Instalar ferramentas do Visual Studio para Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="a62d2-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="a62d2-114">Depois de instalar os pré-requisitos, baixe e instale as Ferramentas de Aplicativos Lógicos do Azure para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a62d2-114">After you install the prerequisites, download and install the Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="a62d2-115">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a62d2-115">Open Visual Studio.</span></span> <span data-ttu-id="a62d2-116">No menu **Ferramentas**, selecione **Extensões e Atualizações**.</span><span class="sxs-lookup"><span data-stu-id="a62d2-116">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="a62d2-117">Expanda a categoria **Online** para que você possa pesquisar online na Galeria do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a62d2-117">Expand the **Online** category so you can search online in the Visual Studio Gallery.</span></span>
3. <span data-ttu-id="a62d2-118">Procure por **Aplicativos Lógicos** até encontrar as **Ferramentas de Aplicativos Lógicos do Azure para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="a62d2-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="a62d2-119">Clique em **Baixar** para baixar e instalar a extensão.</span><span class="sxs-lookup"><span data-stu-id="a62d2-119">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="a62d2-120">Reinicie o Visual Studio após a instalação.</span><span class="sxs-lookup"><span data-stu-id="a62d2-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="a62d2-121">Para baixar diretamente as Ferramentas de Aplicativos Lógicos do Azure para Visual Studio no [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="a62d2-121">To download the Azure Logic Apps Tools for Visual Studio directly, go to the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="a62d2-122">Procurar aplicativos lógicos no Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="a62d2-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="a62d2-123">Para abrir o Cloud Explorer, no menu **Exibir**, escolha **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="a62d2-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="a62d2-124">Navegue para o aplicativo lógico, por grupo de recursos ou tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a62d2-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="a62d2-125">Se você procurar por tipo de recurso, selecione sua assinatura do Azure e, em seguida, expanda a seção **Aplicativos Lógicos** e selecione seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a62d2-125">If you browse by resource type, select your Azure subscription, expand the **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="a62d2-126">Se você procurar por grupo de recursos, expanda o grupo de recursos que tem seu aplicativo lógico e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="a62d2-126">If you browse by resource group, expand the resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="a62d2-127">Para exibir comandos para seu aplicativo lógico, clique com o botão direito em seu aplicativo lógico, ou na parte inferior do Cloud Explorer, escolha no menu **Ações**.</span><span class="sxs-lookup"><span data-stu-id="a62d2-127">To view commands for your logic app, either right-click your logic app, or at the bottom of Cloud Explorer, choose from the **Actions** menu.</span></span>

    ![Navegar para o aplicativo lógico](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="a62d2-129">Editar o aplicativo lógico com o Designer de Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="a62d2-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="a62d2-130">Do Cloud Explorer, você pode abrir um aplicativo lógico implantado no momento no mesmo designer que você usa no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a62d2-130">From Cloud Explorer, you can open a currently deployed logic app in the same designer that you use in the Azure portal.</span></span> 

* <span data-ttu-id="a62d2-131">Para editar seu aplicativo lógico, no Cloud Explorer, clique com o botão direito em seu aplicativo lógico e selecione **Abrir com o Editor de Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="a62d2-131">To edit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="a62d2-132">Para publicar suas atualizações na nuvem, escolha **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a62d2-132">To publish your updates to the cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="a62d2-133">Para iniciar uma nova execução, escolha **Executar Gatilho**.</span><span class="sxs-lookup"><span data-stu-id="a62d2-133">To start a new run, choose **Run Trigger**.</span></span>

![Designer de Aplicativos Lógicos](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="a62d2-135">No designer, você também pode **Baixar** um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a62d2-135">From the designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="a62d2-136">Essa ação parametriza automaticamente a definição do aplicativo lógico, e salva a definição como um modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a62d2-136">This action automatically parameterizes the logic app definition, and saves the definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="a62d2-137">Você pode adicionar esse modelo de implantação ao seu projeto de Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a62d2-137">You can add this deployment template to your Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="a62d2-138">Procurar o histórico de execução do aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="a62d2-138">Browse your logic app run history</span></span>

<span data-ttu-id="a62d2-139">Para exibir o histórico de execução do aplicativo lógico, clique com o botão direito do mouse no aplicativo lógico e selecione **Abrir histórico de execução**.</span><span class="sxs-lookup"><span data-stu-id="a62d2-139">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="a62d2-140">Para reordenar o histórico de execução de acordo com uma das propriedades mostradas, selecione o cabeçalho de coluna.</span><span class="sxs-lookup"><span data-stu-id="a62d2-140">To reorder your run history based on any of the properties shown, select the column header.</span></span>

![Histórico da execução](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="a62d2-142">Para mostrar o histórico de execução de uma instância para poder ver os resultados da execução, incluindo as entradas e saídas de cada etapa, clique duas vezes em uma das instâncias de execução.</span><span class="sxs-lookup"><span data-stu-id="a62d2-142">To show the run history for an instance so you can review the run results, including the inputs and outputs from each step, double-click one of the run instances.</span></span>

![Resultados do histórico de execução, entradas e saídas de etapas](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="a62d2-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a62d2-144">Next steps</span></span>

* [<span data-ttu-id="a62d2-145">Criar seu primeiro aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="a62d2-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="a62d2-146">Criar, compilar e implantar aplicativos lógicos no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a62d2-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="a62d2-147">Veja exemplos e cenários comuns</span><span class="sxs-lookup"><span data-stu-id="a62d2-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="a62d2-148">Vídeo: Automatizar processos de negócios com os Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="a62d2-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="a62d2-149">Vídeo: integrar seus sistemas com os Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="a62d2-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
