---
title: "Etapa 1: Criar um Espaço de Trabalho do Machine Learning | Microsoft Docs"
description: "Etapa 1 de saudação desenvolver um passo a passo de solução de previsão: Saiba como tooset um novo espaço de trabalho do estúdio de aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="f1ed5-103">Etapa 1 do passo a passo: Criar um espaço de trabalho de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f1ed5-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="f1ed5-104">Essa é a primeira etapa Olá Olá explicação passo a passo, [desenvolver uma solução de análise preditiva em aprendizado de máquina do Azure](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="f1ed5-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="f1ed5-105">
            **Criar um espaço de trabalho do Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="f1ed5-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="f1ed5-106">Carregar dados existentes</span><span class="sxs-lookup"><span data-stu-id="f1ed5-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="f1ed5-107">Criar um novo teste</span><span class="sxs-lookup"><span data-stu-id="f1ed5-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="f1ed5-108">Treinar e avaliar modelos Olá</span><span class="sxs-lookup"><span data-stu-id="f1ed5-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="f1ed5-109">Implantar o serviço Web de saudação</span><span class="sxs-lookup"><span data-stu-id="f1ed5-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="f1ed5-110">Acessar o serviço Web Olá</span><span class="sxs-lookup"><span data-stu-id="f1ed5-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="f1ed5-111">toouse estúdio de aprendizado de máquina, você precisa toohave um espaço de trabalho do aprendizado de máquina do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f1ed5-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="f1ed5-112">Este espaço de trabalho contém ferramentas Olá necessárias toocreate, gerenciar e publicar experiências.</span><span class="sxs-lookup"><span data-stu-id="f1ed5-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="f1ed5-113">administrador de saudação para sua assinatura do Azure precisa de espaço de trabalho do toocreate hello e, em seguida, adicioná-lo como um proprietário ou colaborador.</span><span class="sxs-lookup"><span data-stu-id="f1ed5-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="f1ed5-114">Para obter mais detalhes, consulte [Criar e compartilhar um espaço de trabalho do Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f1ed5-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="f1ed5-115">Após a criação do espaço de trabalho, abra o Machine Learning Studio:[https://studio.azureml.net/Home](https://studio.azureml.net/Home).</span><span class="sxs-lookup"><span data-stu-id="f1ed5-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="f1ed5-116">Se você tiver mais de um espaço de trabalho, você pode selecionar o espaço de trabalho de saudação na barra de ferramentas Olá no canto superior direito de saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1ed5-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Selecionar o espaço de trabalho no estúdio][2]

> [!TIP]
> <span data-ttu-id="f1ed5-118">Se você tiver sido feita um proprietário do espaço de trabalho Olá, você pode compartilhar experiências Olá você está trabalhando, por convidar outras pessoas toohello espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f1ed5-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="f1ed5-119">Você pode fazer isso no estúdio de aprendizado de máquina em Olá **configurações** página.</span><span class="sxs-lookup"><span data-stu-id="f1ed5-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="f1ed5-120">Basta conta da Microsoft hello ou conta organizacional para cada usuário.</span><span class="sxs-lookup"><span data-stu-id="f1ed5-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="f1ed5-121">Em Olá **configurações** , clique em **usuários**, em seguida, clique em **CONVIDAR usuários mais** na parte inferior da saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1ed5-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="f1ed5-122">**Em seguida:[ Carregar dados existentes](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="f1ed5-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
