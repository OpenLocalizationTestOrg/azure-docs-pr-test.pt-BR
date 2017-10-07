---
title: "aaaHow toodeploy um serviço Web regiões toomultiple | Microsoft Docs"
description: "Etapas toodeploy (cópia) regiões de tooother um novo serviço da Web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="fc030-103">Como um serviço Web de toodeploy toomultiple regiões</span><span class="sxs-lookup"><span data-stu-id="fc030-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="fc030-104">Olá serviços Web do Azure nova permitem tooeasily implantar um regiões de toomultiple de serviço web sem a necessidade de várias assinaturas ou espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fc030-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="fc030-105">Os preços são região específica, que portanto, você deve definir um plano de cobrança para cada região na qual você implantará o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc030-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="fc030-106">toocreate um plano em outra região</span><span class="sxs-lookup"><span data-stu-id="fc030-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="fc030-107">Entre nos [serviços Web de Microsoft Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="fc030-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="fc030-108">Clique em Olá **planos** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="fc030-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="fc030-109">Em planos de saudação pela página de exibição, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="fc030-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="fc030-110">De saudação **assinatura** suspenso, assinatura Olá selecione em quais Olá novo plano residirá.</span><span class="sxs-lookup"><span data-stu-id="fc030-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="fc030-111">De saudação **região** lista suspensa, selecione uma região para um novo plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc030-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="fc030-112">Olá opções do plano para a região selecionada hello serão exibidos no hello **opções do plano de** seção da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc030-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="fc030-113">De saudação **grupo de recursos** lista suspensa, selecione um recurso de grupo para o plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc030-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="fc030-114">Em mais informações sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc030-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="fc030-115">Em **nome do plano de** nome de saudação do tipo de plano de hello.</span><span class="sxs-lookup"><span data-stu-id="fc030-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="fc030-116">Em **opções do plano de**, clique no nível de cobrança Olá para o novo plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc030-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="fc030-117">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fc030-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="fc030-118">Implantação de região de tooanother Olá web service</span><span class="sxs-lookup"><span data-stu-id="fc030-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="fc030-119">Clique em Olá **serviços Web** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="fc030-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="fc030-120">Selecione Olá serviço Web que você está implantando tooa nova região.</span><span class="sxs-lookup"><span data-stu-id="fc030-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="fc030-121">Clique em **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="fc030-121">Click **Copy**.</span></span>
4. <span data-ttu-id="fc030-122">Em **nome do serviço Web**, digite um novo nome para o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc030-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="fc030-123">Em **Web descrição do serviço**, digite uma descrição para o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc030-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="fc030-124">De saudação **assinatura** suspenso, assinatura Olá selecione em quais Olá novo serviço da web residirá.</span><span class="sxs-lookup"><span data-stu-id="fc030-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="fc030-125">De saudação **grupo de recursos** lista suspensa, selecione um recurso de grupo do serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc030-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="fc030-126">Em mais informações sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc030-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="fc030-127">De saudação **região** suspenso, região Olá selecione quais toodeploy Olá no serviço na web.</span><span class="sxs-lookup"><span data-stu-id="fc030-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="fc030-128">De saudação **conta de armazenamento** lista suspensa, selecione uma conta de armazenamento no qual Olá toostore de serviço da web.</span><span class="sxs-lookup"><span data-stu-id="fc030-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="fc030-129">De saudação **plano de preço** lista suspensa, selecione um plano na região de saudação selecionado na etapa 8.</span><span class="sxs-lookup"><span data-stu-id="fc030-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="fc030-130">Clique em **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="fc030-130">Click **Copy**.</span></span>

