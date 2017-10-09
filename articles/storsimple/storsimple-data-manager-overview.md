---
title: "Visão geral do Gerenciador de dados do Azure StorSimple aaaMicrosoft | Microsoft Docs"
description: "Fornece uma visão geral da saudação serviço StorSimple Manager de dados (visualização particular)"
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
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="d5ad0-103">Visão geral do Gerenciador de Dados do StorSimple (Visualização particular)</span><span class="sxs-lookup"><span data-stu-id="d5ad0-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="d5ad0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d5ad0-104">Overview</span></span>

<span data-ttu-id="d5ad0-105">Microsoft Azure StorSimple é uma solução de armazenamento de nuvem híbrida endereços Olá complexidades de comumente associadas a compartilhamentos de arquivos de dados não estruturados.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="d5ad0-106">StorSimple usa armazenamento em nuvem como uma extensão da saudação solução local e automaticamente dados de camadas de armazenamento de local de saudação e armazenamento em nuvem.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="d5ad0-107">Integra a proteção de dados local e instantâneos em nuvem, que elimina a necessidade de saudação de uma infraestrutura de armazenamento amplas.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="d5ad0-108">Arquivamento e recuperação de desastres também é consistente com a nuvem Olá atuando como um local externo.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="d5ad0-109">Olá data transformation Services que estamos introduzindo neste documento, permite que você tooseamlessly acesso Olá StorSimple dados na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="d5ad0-110">Esse serviço fornece dados de tooextract APIs do StorSimple e apresentá-lo tooother Azure serviços em formatos que podem ser consumidos imediatamente.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="d5ad0-111">formatos de saudação com suporte nesta visualização são blobs do Azure e ativos de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="d5ad0-112">Essa transformação permite que você tooeasily durante a transmissão os serviços, como serviços de mídia do Azure, HDInsight do Azure, aprendizado de máquina do Azure e pesquisa do Azure dados toooperate no dispositivo de local de série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="d5ad0-113">Veja abaixo um diagrama de bloco de alto nível que ilustra isso.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagrama de alto nível](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="d5ad0-115">Este documento explica como você pode se inscrever para uma visualização particular desse serviço.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="d5ad0-116">Ele também explica como você pode usar estes aplicativos de toowrite de serviço que usam dados do StorSimple e outros serviços do Azure na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="d5ad0-117">Inscrever-se para a visualização do Gerenciador de Dados</span><span class="sxs-lookup"><span data-stu-id="d5ad0-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="d5ad0-118">Antes de se inscrever para o serviço de Gerenciador de dados hello, examine Olá pré-requisitos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d5ad0-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d5ad0-119">Prerequisites</span></span>

<span data-ttu-id="d5ad0-120">Este exercício supõe que você tem</span><span class="sxs-lookup"><span data-stu-id="d5ad0-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="d5ad0-121">uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-121">an active Azure subscription.</span></span>
* <span data-ttu-id="d5ad0-122">acesso tooa registrado o dispositivo da série 8000 StorSimple</span><span class="sxs-lookup"><span data-stu-id="d5ad0-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="d5ad0-123">todos os Olá chaves associadas ao dispositivo da série StorSimple 8000 do hello.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="d5ad0-124">Inscrição</span><span class="sxs-lookup"><span data-stu-id="d5ad0-124">Sign up</span></span>

<span data-ttu-id="d5ad0-125">Olá StorSimple Data Manager está no modo de visualização particular.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="d5ad0-126">Execute Olá toosign etapas para uma visualização privada do serviço a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5ad0-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="d5ad0-127">Faça logon no hello portal do Azure com extensão de Gerenciador de dados StorSimple Olá em: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="d5ad0-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="d5ad0-128">Use o toolog as credenciais do Azure no.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="d5ad0-129">Clique em Olá  **+**  ícone toocreate um serviço.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="d5ad0-130">Clique em **armazenamento** e, em seguida, clique em **consulte todos os** na folha de saudação que é aberta.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![Ícone Pesquisar no Gerenciador de Dados do StorSimple](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="d5ad0-132">Você verá o ícone do Gerenciador de dados StorSimple Olá.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-132">You see hello StorSimple Data Manager icon.</span></span>

    ![Ícone Selecionar Gerenciador de Dados do StorSimple](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="d5ad0-134">Clique no ícone Gerenciador de Dados do StorSimple e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="d5ad0-135">Escolha a assinatura de saudação que você deseja tooenable para visualização privada hello e, em seguida, clique em **me inscrever!**</span><span class="sxs-lookup"><span data-stu-id="d5ad0-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![Inscrever-me](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="d5ad0-137">Isso envia uma solicitação tooonboard você.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="d5ad0-138">Realizaremos sua integração assim que possível.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="d5ad0-139">Após a habilitação de sua assinatura, você poderá criar um serviço de Gerenciador de Dados do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="d5ad0-140">tooeasily acessar o serviço de Gerenciador de dados StorSimple hello, clique em Olá ícone de estrela toopin-tooyour Favoritos.</span><span class="sxs-lookup"><span data-stu-id="d5ad0-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![Acessar o Gerenciador de Dados do StorSimple](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="d5ad0-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d5ad0-142">Next steps</span></span>

<span data-ttu-id="d5ad0-143">[Usar os dados de interface de usuário de Gerenciador de dados StorSimple tootransform](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="d5ad0-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
