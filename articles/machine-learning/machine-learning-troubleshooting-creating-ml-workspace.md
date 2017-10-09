---
title: "Solução de problemas: Criar e conectar-se o espaço de trabalho de aprendizado de máquina tooa | Microsoft Docs"
description: "Soluções para problemas comuns na criação e conectar-se o espaço de trabalho de aprendizado de máquina do Azure tooan"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="bfeb6-103">Guia de solução de problemas: criar e conectar-se o espaço de trabalho de aprendizado de máquina tooan</span><span class="sxs-lookup"><span data-stu-id="bfeb6-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="bfeb6-104">Este guia fornece soluções para alguns desafios encontrados com frequência quando você configura espaços de trabalho do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="bfeb6-105">Proprietário do espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="bfeb6-105">Workspace owner</span></span>
<span data-ttu-id="bfeb6-106">tooopen um espaço de trabalho no estúdio de aprendizado de máquina, você deve ser conectado toohello Account da Microsoft que você usou o espaço de trabalho do toocreate hello, ou será necessário tooreceive um convite de espaço de trabalho da saudação toojoin Olá proprietário.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="bfeb6-107">Olá portal do Azure, você pode gerenciar espaço de trabalho de saudação, que inclui Olá capacidade tooconfigure acesso.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="bfeb6-108">Para obter mais informações sobre como gerenciar um espaço de trabalho, consulte [Gerenciar um espaço de trabalho do Azure Machine Learning].</span><span class="sxs-lookup"><span data-stu-id="bfeb6-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>


            [Gerenciar um espaço de trabalho do Azure Machine Learning]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="bfeb6-110">Regiões permitidas</span><span class="sxs-lookup"><span data-stu-id="bfeb6-110">Allowed regions</span></span>
<span data-ttu-id="bfeb6-111">No momento, o Machine Learning está disponível em um número limitado de regiões.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="bfeb6-112">Se sua assinatura não tem uma dessas regiões, você poderá ver a mensagem de erro hello, "Você não tem assinaturas em Olá permitido regiões."</span><span class="sxs-lookup"><span data-stu-id="bfeb6-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="bfeb6-113">toorequest uma região de ser adicionado tooyour assinatura, crie uma nova solicitação de suporte da Microsoft da saudação portal do Azure, escolha **cobrança** como o tipo de problema hello e siga Olá solicita toosubmit sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="bfeb6-114">Conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="bfeb6-114">Storage account</span></span>
<span data-ttu-id="bfeb6-115">Olá service de aprendizado de máquina precisa de um toostore dados da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="bfeb6-116">Você pode usar uma conta de armazenamento existente, ou você pode criar uma nova conta de armazenamento ao criar o espaço de trabalho de aprendizado de máquina de novo hello (se você tiver cota toocreate uma nova conta de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="bfeb6-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="bfeb6-117">Após a criação do espaço de trabalho de aprendizado de máquina de novo Olá, entrar tooMachine estúdio de aprendizado usando a conta da Microsoft hello usado o espaço de trabalho do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="bfeb6-118">Se você receber a mensagem de erro de hello, "Espaço de trabalho não encontrado" (semelhante toohello captura de tela a seguir), use Olá toodelete as etapas a seguir os cookies do seu navegador.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![Espaço de trabalho não encontrado][screen3]

<span data-ttu-id="bfeb6-120">**cookies do navegador toodelete**</span><span class="sxs-lookup"><span data-stu-id="bfeb6-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="bfeb6-121">Se você usar o Internet Explorer, clique em Olá **ferramentas** botão no canto superior direito de saudação e selecione **opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![Opções da Internet][screen4]

2. <span data-ttu-id="bfeb6-123">Em Olá **geral** , clique em **excluir...**</span><span class="sxs-lookup"><span data-stu-id="bfeb6-123">Under hello **General** tab, click **Delete…**</span></span>

![Guia Geral][screen5]

3. <span data-ttu-id="bfeb6-125">Em Olá **Excluir histórico de navegação** caixa de diálogo caixa, certifique-se de **Cookies e dados de site** está selecionado e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Excluir cookies][screen6]

<span data-ttu-id="bfeb6-127">Após Olá cookies são excluídos, reinicie o navegador hello e vá toohello [aprendizado de máquina do Microsoft Azure](https://studio.azureml.net) página.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="bfeb6-128">Quando você for solicitado, insira um nome de usuário e senha, Olá mesma conta da Microsoft usado o espaço de trabalho do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="bfeb6-129">Comentários</span><span class="sxs-lookup"><span data-stu-id="bfeb6-129">Comments</span></span>

<span data-ttu-id="bfeb6-130">Nosso objetivo é toomake Olá experiência de aprendizado de máquina uniforme possível.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="bfeb6-131">Poste quaisquer problemas e comentários no hello [Fórum de aprendizado de máquina do Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp nos servi-lo melhor.</span><span class="sxs-lookup"><span data-stu-id="bfeb6-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
