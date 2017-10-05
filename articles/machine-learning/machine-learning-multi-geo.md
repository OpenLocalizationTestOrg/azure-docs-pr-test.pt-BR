---
title: "Documentação de ajuda de várias áreas geográficas | Microsoft Docs"
description: "Saiba como criar um espaço de trabalho e publicar um serviço Web em uma região do Azure diferente do Centro-Sul dos Estados Unidos (SCUS)."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="db912-103">Documentação da Ajuda para diversas áreas geográficas</span><span class="sxs-lookup"><span data-stu-id="db912-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="db912-104">Este artigo descreve como você pode criar um espaço de trabalho e publicar um serviço Web em diferentes regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="db912-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="db912-105">A página [Produtos do Azure por região](https://azure.microsoft.com/en-us/regions/services/) lista regiões em que o Azure Machine Learning está disponível.</span><span class="sxs-lookup"><span data-stu-id="db912-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="db912-106">Criar um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="db912-106">Create a workspace</span></span>
1. <span data-ttu-id="db912-107">Entre no Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="db912-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="db912-108">Clique em **+ NOVO** > **SERVIÇOS DE DADOS** > **ACHINE LEARNING** > **CRIAÇÃO RÁPIDA**.</span><span class="sxs-lookup"><span data-stu-id="db912-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="db912-109">Em **LOCAL**, selecione outra região, como **Sudeste Asiático**.</span><span class="sxs-lookup"><span data-stu-id="db912-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="db912-110">![Imagem de Ajuda de várias áreas geográficas 1][1]</span><span class="sxs-lookup"><span data-stu-id="db912-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="db912-111">Selecione o espaço de trabalho e, em seguida, clique em **Entrar no Estúdio AM**.</span><span class="sxs-lookup"><span data-stu-id="db912-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="db912-112">![Imagem de Ajuda de várias áreas geográficas 2][2]</span><span class="sxs-lookup"><span data-stu-id="db912-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="db912-113">Agora você tem um espaço de trabalho em outra região que pode usar como qualquer outro espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="db912-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="db912-114">Para alternar entre seus espaços de trabalho, veja o canto superior direito da tela.</span><span class="sxs-lookup"><span data-stu-id="db912-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="db912-115">Clique na lista suspensa, selecione a região e, em seguida, selecione o espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="db912-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="db912-116">Tudo é local para a região do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="db912-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="db912-117">Por exemplo, todos os serviços Web criados por meio de um espaço de trabalho estarão na mesma região em que o espaço de trabalho está localizado.</span><span class="sxs-lookup"><span data-stu-id="db912-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="db912-118">![Imagem de Ajuda de várias áreas geográficas 3][3]</span><span class="sxs-lookup"><span data-stu-id="db912-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="db912-119">Abrir um experimento da Galeria</span><span class="sxs-lookup"><span data-stu-id="db912-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="db912-120">Se você abrir um experimento da galeria, também pode selecionar a região para a qual deseja copiar o experimento.</span><span class="sxs-lookup"><span data-stu-id="db912-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Imagem de Ajuda de várias áreas geográficas 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="db912-122">Gerenciamento de serviço Web</span><span class="sxs-lookup"><span data-stu-id="db912-122">Web service management</span></span>
<span data-ttu-id="db912-123">Para gerenciar os serviços Web de forma programática, como um novo treinamento, use o endereço específico da região:</span><span class="sxs-lookup"><span data-stu-id="db912-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="db912-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="db912-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="db912-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="db912-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="db912-126">Elementos a serem observados</span><span class="sxs-lookup"><span data-stu-id="db912-126">Things to note</span></span>
1. <span data-ttu-id="db912-127">Dessa maneira, você só pode copiar experimentos entre espaços de trabalho que pertençam à mesma região.</span><span class="sxs-lookup"><span data-stu-id="db912-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="db912-128">Se precisar copiar experimentos entre espaços de trabalho em regiões diferentes, você poderá usar o cmdlet do [PowerShell](http://aka.ms/amlps), [*Copy-AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="db912-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="db912-129">Outra solução alternativa é publicar o experimento na Galeria no modo não listado e depois abri-lo no espaço de trabalho da outra região.</span><span class="sxs-lookup"><span data-stu-id="db912-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="db912-130">O seletor de região mostrará apenas os espaços de trabalho para uma região por vez.</span><span class="sxs-lookup"><span data-stu-id="db912-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="db912-131">Um espaço de trabalho livre ou de acesso de convidado (anônimo) será criado e hospedado no Centro-Sul dos EUA</span><span class="sxs-lookup"><span data-stu-id="db912-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="db912-132">Os serviços Web implantados por meio de um espaço de trabalho no Sudeste Asiático também serão hospedados no Sudeste Asiático.</span><span class="sxs-lookup"><span data-stu-id="db912-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="db912-133">Mais informações</span><span class="sxs-lookup"><span data-stu-id="db912-133">More information</span></span>
<span data-ttu-id="db912-134">Fazer uma pergunta no [fórum de Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="db912-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
