---
title: "Solução de problemas: criar e conectar-se a um Espaço de Trabalho do Machine Learning | Microsoft Docs"
description: "Soluções para problemas comuns na criação e conexão a um espaço de trabalho de Azure Machine Learning"
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
ms.openlocfilehash: 398ac3d9c9d32a1ab10413ce0d7ce8d448890409
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="24528-103">Guia de solução de problemas: criar e conectar-se a um espaço de trabalho do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="24528-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="24528-104">Este guia fornece soluções para alguns desafios encontrados com frequência quando você configura espaços de trabalho do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="24528-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="24528-105">Proprietário do espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="24528-105">Workspace owner</span></span>
<span data-ttu-id="24528-106">Para abrir um espaço de trabalho no Machine Learning Studio, você deve estar conectado à Conta da Microsoft usada para criar o espaço de trabalho, ou receber um convite do proprietário para ingressar no espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="24528-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="24528-107">No portal do Azure você pode gerenciar o espaço de trabalho, que inclui a capacidade de alterar o proprietário e configurar o acesso.</span><span class="sxs-lookup"><span data-stu-id="24528-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="24528-108">Para obter mais informações sobre como gerenciar um espaço de trabalho, consulte [Gerenciar um espaço de trabalho do Azure Machine Learning].</span><span class="sxs-lookup"><span data-stu-id="24528-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

<span data-ttu-id="24528-109">
            [Gerenciar um espaço de trabalho do Azure Machine Learning]: machine-learning-manage-workspace.md</span><span class="sxs-lookup"><span data-stu-id="24528-109">[Manage an Azure Machine Learning workspace]: machine-learning-manage-workspace.md</span></span>

## <a name="allowed-regions"></a><span data-ttu-id="24528-110">Regiões permitidas</span><span class="sxs-lookup"><span data-stu-id="24528-110">Allowed regions</span></span>
<span data-ttu-id="24528-111">No momento, o Machine Learning está disponível em um número limitado de regiões.</span><span class="sxs-lookup"><span data-stu-id="24528-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="24528-112">Se sua assinatura não incluir uma dessas regiões, talvez você receba a mensagem de erro "Você não tem assinaturas nas regiões permitidas".</span><span class="sxs-lookup"><span data-stu-id="24528-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="24528-113">Para solicitar a adição de uma região à sua assinatura, crie uma nova solicitação de suporte da Microsoft no portal do Azure, escolha o tipo de problema **Cobrança** e siga os prompts para enviar sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="24528-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="24528-114">Conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="24528-114">Storage account</span></span>
<span data-ttu-id="24528-115">O serviço de Machine Learning precisa de uma conta de armazenamento para armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="24528-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="24528-116">Você pode usar uma conta de armazenamento existente, ou pode criar uma nova conta de armazenamento ao criar o novo espaço de trabalho de Machine Learning (se você tiver cota para criar uma nova conta de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="24528-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="24528-117">Criado o novo espaço de trabalho do Machine Learning, você pode entrar no Machine Learning Studio com a conta da Microsoft usada para criar o espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="24528-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="24528-118">Se você encontrar a mensagem de erro "Espaço de Trabalho Não Encontrado" (semelhante à captura de tela a seguir), use as etapas a seguir para excluir os cookies do navegador.</span><span class="sxs-lookup"><span data-stu-id="24528-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![Espaço de trabalho não encontrado][screen3]

<span data-ttu-id="24528-120">**Para excluir cookies do navegador**</span><span class="sxs-lookup"><span data-stu-id="24528-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="24528-121">Se você usa o Internet Explorer, clique no botão **Ferramentas** no canto superior direito e selecione **Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="24528-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![Opções da Internet][screen4]

2. <span data-ttu-id="24528-123">Na guia **Geral**, clique em **Excluir…**</span><span class="sxs-lookup"><span data-stu-id="24528-123">Under the **General** tab, click **Delete…**</span></span>

![Guia Geral][screen5]

3. <span data-ttu-id="24528-125">Na caixa de diálogo **Excluir Histórico de Navegação**, selecione **Cookies e dados de sites** e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="24528-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Excluir cookies][screen6]

<span data-ttu-id="24528-127">Depois que os cookies forem excluídos, reinicie o navegador e vá para a página [Microsoft Azure Machine Learning](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="24528-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="24528-128">Quando forem solicitados nome de usuário e senha, insira os dados da mesma conta da Microsoft usada para criar o espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="24528-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="24528-129">Comentários</span><span class="sxs-lookup"><span data-stu-id="24528-129">Comments</span></span>

<span data-ttu-id="24528-130">Nosso objetivo é tornar a experiência do Machine Learning o mais simples possível.</span><span class="sxs-lookup"><span data-stu-id="24528-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="24528-131">Poste comentários e problemas no [Fórum do Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) para nos ajudar a atendê-lo melhor.</span><span class="sxs-lookup"><span data-stu-id="24528-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
