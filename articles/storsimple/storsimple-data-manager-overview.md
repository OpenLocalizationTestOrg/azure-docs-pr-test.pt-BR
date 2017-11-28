---
title: "Visão geral do Gerenciador de Dados do Microsoft Azure StorSimple | Microsoft Docs"
description: "Fornece uma visão geral do serviço Gerenciador de Dados do StorSimple (visualização particular)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: aedb44610fe57055851538b9dbdb810e66e58d73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="16702-103">Visão geral do Gerenciador de Dados do StorSimple (Visualização particular)</span><span class="sxs-lookup"><span data-stu-id="16702-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="16702-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="16702-104">Overview</span></span>

<span data-ttu-id="16702-105">O Microsoft Azure StorSimple é uma solução de armazenamento de nuvem híbrida que resolve as complexidades de dados não estruturados comumente associados aos compartilhamentos de arquivos.</span><span class="sxs-lookup"><span data-stu-id="16702-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses the complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="16702-106">O StorSimple usa o armazenamento em nuvem como uma extensão da solução local e dispõe os dados em camadas automaticamente no armazenamento local e no armazenamento em nuvem.</span><span class="sxs-lookup"><span data-stu-id="16702-106">StorSimple uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="16702-107">A proteção de dados integrada, com instantâneos locais e de nuvem, elimina a necessidade de uma infraestrutura de armazenamento ampla.</span><span class="sxs-lookup"><span data-stu-id="16702-107">Integrated data protection, with local and cloud snapshots, eliminates the need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="16702-108">O arquivamento e a recuperação de desastres também são perfeitos com a nuvem agindo como um local externo.</span><span class="sxs-lookup"><span data-stu-id="16702-108">Archival and disaster recovery is also seamless with the cloud acting as an offsite location.</span></span>

<span data-ttu-id="16702-109">O serviço de transformação de dados que estamos apresentando neste documento, permite o acesso direto aos dados do StorSimple na nuvem.</span><span class="sxs-lookup"><span data-stu-id="16702-109">The data transformation service that we are introducing in this document, allows you to seamlessly access the StorSimple data in the cloud.</span></span> <span data-ttu-id="16702-110">Esse serviço fornece APIs para extração de dados do StorSimple e os apresenta a outros serviços do Azure em formatos que podem ser facilmente consumidos.</span><span class="sxs-lookup"><span data-stu-id="16702-110">This service provides APIs to extract data from StorSimple and present it to other Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="16702-111">Os formatos com suporte nesta visualização são Blobs do Azure e ativos dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="16702-111">The formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="16702-112">Essa transformação permite que você conecte facilmente os serviços, como os Serviços de Mídia do Azure, o Azure HDInsight, o Azure Machine Learning e o Azure Search, a fim de operar os dados no dispositivo local da série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="16702-112">This transformation enables you to easily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search to operate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="16702-113">Veja abaixo um diagrama de bloco de alto nível que ilustra isso.</span><span class="sxs-lookup"><span data-stu-id="16702-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagrama de alto nível](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="16702-115">Este documento explica como você pode se inscrever para uma visualização particular desse serviço.</span><span class="sxs-lookup"><span data-stu-id="16702-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="16702-116">Também explica como você pode usar esse serviço para escrever aplicativos que usam dados do StorSimple e outros serviços do Azure na nuvem.</span><span class="sxs-lookup"><span data-stu-id="16702-116">It also explains how you can use this service to write applications that use StorSimple data and other Azure services in the cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="16702-117">Inscrever-se para a visualização do Gerenciador de Dados</span><span class="sxs-lookup"><span data-stu-id="16702-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="16702-118">Antes de se inscrever no serviço do Gerenciador de Gados, consulte os seguintes pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="16702-118">Before you sign up for the Data Manager service, review the following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="16702-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="16702-119">Prerequisites</span></span>

<span data-ttu-id="16702-120">Este exercício supõe que você tem</span><span class="sxs-lookup"><span data-stu-id="16702-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="16702-121">uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="16702-121">an active Azure subscription.</span></span>
* <span data-ttu-id="16702-122">acesso a um dispositivo da série StorSimple 8000 registrado</span><span class="sxs-lookup"><span data-stu-id="16702-122">access to a registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="16702-123">todas as chaves associadas ao dispositivo da série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="16702-123">all the keys associated with the StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="16702-124">Inscrição</span><span class="sxs-lookup"><span data-stu-id="16702-124">Sign up</span></span>

<span data-ttu-id="16702-125">O Gerenciador de Dados do StorSimple está em visualização particular.</span><span class="sxs-lookup"><span data-stu-id="16702-125">The StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="16702-126">Execute as etapas a seguir para se inscrever para uma visualização particular desse serviço:</span><span class="sxs-lookup"><span data-stu-id="16702-126">Perform the following steps to sign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="16702-127">Faça logon no Portal do Azure com a extensão do Gerenciador de Dados do StorSimple no: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="16702-127">Log into the Azure portal with the StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="16702-128">Use suas credenciais do Azure AD para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="16702-128">Use your Azure credentials to log in.</span></span>

2.  <span data-ttu-id="16702-129">Clique no ícone **+** para criar um serviço.</span><span class="sxs-lookup"><span data-stu-id="16702-129">Click the **+** icon to create a service.</span></span> <span data-ttu-id="16702-130">Clique em **Armazenamento** e depois em **Ver Tudo** na folha exibida.</span><span class="sxs-lookup"><span data-stu-id="16702-130">Click **Storage** and then click **See All** in the blade that opens up.</span></span>

    ![Ícone Pesquisar no Gerenciador de Dados do StorSimple](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="16702-132">Você verá o ícone do Gerenciador de Dados do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="16702-132">You see the StorSimple Data Manager icon.</span></span>

    ![Ícone Selecionar Gerenciador de Dados do StorSimple](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="16702-134">Clique no ícone Gerenciador de Dados do StorSimple e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="16702-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="16702-135">Escolha a assinatura que você deseja habilitar para a visualização particular e, em seguida, clique em **Inscrever-me!**</span><span class="sxs-lookup"><span data-stu-id="16702-135">Pick the subscription that you want to enable for the private preview and then click **Sign me up!**</span></span>

    ![Inscrever-me](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="16702-137">Isso envia uma solicitação para sua integração.</span><span class="sxs-lookup"><span data-stu-id="16702-137">This sends a request to onboard you.</span></span> <span data-ttu-id="16702-138">Realizaremos sua integração assim que possível.</span><span class="sxs-lookup"><span data-stu-id="16702-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="16702-139">Após a habilitação de sua assinatura, você poderá criar um serviço de Gerenciador de Dados do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="16702-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="16702-140">Para acessar facilmente o serviço do Gerenciador de Dados do StorSimple, clique no ícone de estrela para fixá-lo aos seus favoritos.</span><span class="sxs-lookup"><span data-stu-id="16702-140">To easily access the StorSimple Data Manager service, click the star icon to pin it to your favorites.</span></span>

    ![Acessar o Gerenciador de Dados do StorSimple](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="16702-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16702-142">Next steps</span></span>

<span data-ttu-id="16702-143">[Use a interface do usuário do Gerenciador de Dados StorSimple para transformar seus dados](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="16702-143">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>