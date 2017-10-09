---
title: "um espaço de trabalho do aprendizado de máquina do aaaCreate | Microsoft Docs"
description: "Como toocreate um espaço de trabalho para o estúdio de aprendizado de máquina do Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="fe126-103">Criar e compartilhar um espaço de trabalho de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fe126-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="fe126-104">Esse menu links tootopics que descrevem como tooset backup Olá vários ambientes de ciência de dados usado pelo Olá processo de análise da Cortana (CAPS).</span><span class="sxs-lookup"><span data-stu-id="fe126-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="fe126-105">toouse estúdio de aprendizado de máquina do Azure, você precisa toohave um espaço de trabalho do aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="fe126-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="fe126-106">Este espaço de trabalho contém ferramentas Olá necessárias toocreate, gerenciar e publicar experiências.</span><span class="sxs-lookup"><span data-stu-id="fe126-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="fe126-107">toocreate um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="fe126-107">toocreate a workspace</span></span>
1. <span data-ttu-id="fe126-108">Entrar toohello [portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="fe126-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe126-109">toosign em e criar um espaço de trabalho, você precisa toobe um administrador de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe126-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="fe126-110">Clique em **+Novo**</span><span class="sxs-lookup"><span data-stu-id="fe126-110">Click **+New**</span></span>

3. <span data-ttu-id="fe126-111">Selecione **Inteligência + análise**, clique em **Espaço de Trabalho do Machine Learning**, e clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="fe126-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="fe126-112">Insira suas informações de espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="fe126-112">Enter your workspace information</span></span>

    - <span data-ttu-id="fe126-113">Olá *nome do espaço de trabalho* pode ser too260 caracteres, não termine em um espaço.</span><span class="sxs-lookup"><span data-stu-id="fe126-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="fe126-114">nome de saudação não pode incluir estes caracteres:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="fe126-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="fe126-115">Olá *plano do serviço web* você escolher (ou criar), juntamente com hello associado *preço* você selecionar, será usado se você implantar serviços web deste espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fe126-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Criar um novo espaço de trabalho](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="fe126-117">Clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="fe126-117">Click **Create**</span></span>

<span data-ttu-id="fe126-118">Depois que o espaço de trabalho de saudação é implantado, você pode abri-lo no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="fe126-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="fe126-119">Procurar tooMachine estúdio de aprendizado em [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="fe126-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="fe126-120">Selecione o espaço de trabalho no canto de superior direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="fe126-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![Selecione o espaço de trabalho](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="fe126-122">Clique em **meus experimentos**.</span><span class="sxs-lookup"><span data-stu-id="fe126-122">Click **my experiments**.</span></span>

    ![Experimentos abertos](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="fe126-124">Para saber mais sobre como gerenciar seu espaço de trabalho, consulte [Gerenciar um espaço de trabalho do Azure Machine Learning](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="fe126-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="fe126-125">Se você encontrar um problema ao criar seu espaço de trabalho, consulte [guia de solução de problemas: criar e conectar-se o espaço de trabalho de aprendizado de máquina tooa](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="fe126-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="fe126-126">Compartilhar um espaço de trabalho do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fe126-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="fe126-127">Depois de criar um espaço de trabalho do aprendizado de máquina, você pode convidar usuários tooyour espaço de trabalho tooshare acesso tooyour espaço de trabalho e todas as suas experiências, conjuntos de dados, anotações, etc. Você pode adicionar usuários em uma das duas funções:</span><span class="sxs-lookup"><span data-stu-id="fe126-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="fe126-128">**Usuário** -um usuário do espaço de trabalho pode criar, abrir, modificar e excluir experiências, conjuntos de dados, etc. no espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe126-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="fe126-129">**Proprietário** - um proprietário pode convidar e remover usuários no espaço de trabalho hello, na inclusão toowhat um usuário podem fazer.</span><span class="sxs-lookup"><span data-stu-id="fe126-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="fe126-130">conta de administrador de saudação que cria o espaço de trabalho de saudação é automaticamente adicionada toohello espaço de trabalho como proprietário do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fe126-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="fe126-131">No entanto, outros administradores ou usuários de assinatura não são automaticamente concedido acesso toohello espaço de trabalho - você precisa tooinvite-los explicitamente.</span><span class="sxs-lookup"><span data-stu-id="fe126-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="fe126-132">tooshare um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="fe126-132">tooshare a workspace</span></span>

1. <span data-ttu-id="fe126-133">Entrar tooMachine estúdio de aprendizado em [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="fe126-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="fe126-134">No painel esquerdo do hello, clique em **configurações**</span><span class="sxs-lookup"><span data-stu-id="fe126-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="fe126-135">Clique em Olá **usuários** guia</span><span class="sxs-lookup"><span data-stu-id="fe126-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="fe126-136">Clique em **CONVIDAR usuários mais** final Olá Olá página</span><span class="sxs-lookup"><span data-stu-id="fe126-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Configurações do Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="fe126-138">Insira um ou mais endereços de email.</span><span class="sxs-lookup"><span data-stu-id="fe126-138">Enter one or more email addresses.</span></span> <span data-ttu-id="fe126-139">usuários de saudação precisam de uma conta da Microsoft válida ou uma conta organizacional (a partir do Active Directory do Azure).</span><span class="sxs-lookup"><span data-stu-id="fe126-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="fe126-140">Selecione se deseja que os usuários de saudação do tooadd como proprietário ou usuário.</span><span class="sxs-lookup"><span data-stu-id="fe126-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="fe126-141">Clique em Olá **Okey** botão de marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="fe126-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="fe126-142">Cada usuário que você adicionar receberá um email com instruções sobre como toosign no toohello compartilhados espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fe126-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="fe126-143">Para usuários toobe capaz de toodeploy ou gerenciar os serviços web neste espaço de trabalho, eles devem ser um administrador no hello assinatura do Azure ou colaborador.</span><span class="sxs-lookup"><span data-stu-id="fe126-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



