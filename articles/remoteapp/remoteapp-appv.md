---
title: aplicativos aaaUsing App-V com o Azure RemoteApp | Microsoft Docs
description: Saiba como aplicativos toouse App-V no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="cfe1b-103">Usando os aplicativos App-V no Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cfe1b-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cfe1b-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cfe1b-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cfe1b-106">Você pode usar os aplicativos do App-V em uma coleção híbrida do Azure RemoteApp, o que requer o ingresso no domínio.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="cfe1b-107">Antes de começar, certifique-se de cliente de App-V 5.1 Olá tooinstall com atualizações mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="cfe1b-108">Você precisará toocreate um [imagem personalizada](remoteapp-create-custom-image.md) que inclui o cliente Olá App-V.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="cfe1b-109">É fácil toouse sua infraestrutura existente do App-V com o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="cfe1b-110">Como uma coleção híbrida é implantada em uma rede virtual do Azure com o controlador de domínio do acesso tooyour e VMs Olá são ingressados no domínio, você pode aproveitar seu existente aplicativo App-v infraestrutura e a implantação de métodos tooeasyily host App-V no Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="cfe1b-111">Aqui estão algumas considerações que você deve estar atento, com base no tipo de saudação da implantação do App-V que no momento:</span><span class="sxs-lookup"><span data-stu-id="cfe1b-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="cfe1b-112">Opções de configuração</span><span class="sxs-lookup"><span data-stu-id="cfe1b-112">Configuration options</span></span> |  | <span data-ttu-id="cfe1b-113">Positivo</span><span class="sxs-lookup"><span data-stu-id="cfe1b-113">Positive</span></span> | <span data-ttu-id="cfe1b-114">Negativo</span><span class="sxs-lookup"><span data-stu-id="cfe1b-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cfe1b-115">Método de entrega</span><span class="sxs-lookup"><span data-stu-id="cfe1b-115">Delivery method</span></span> |<span data-ttu-id="cfe1b-116">Streaming (por demanda)</span><span class="sxs-lookup"><span data-stu-id="cfe1b-116">Streaming (on-demand)</span></span> |<span data-ttu-id="cfe1b-117">Aplicativo é sempre Olá nova e mais recente</span><span class="sxs-lookup"><span data-stu-id="cfe1b-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="cfe1b-118">Latência da primeira vez</span><span class="sxs-lookup"><span data-stu-id="cfe1b-118">First time latency</span></span> |
| <span data-ttu-id="cfe1b-119">Montado</span><span class="sxs-lookup"><span data-stu-id="cfe1b-119">Mounted</span></span> |<span data-ttu-id="cfe1b-120">Mais rápido; aplicativo já está presente no hello VM</span><span class="sxs-lookup"><span data-stu-id="cfe1b-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="cfe1b-121">Inchaço - ocupa o espaço da imagem (limite de 127 GB)</span><span class="sxs-lookup"><span data-stu-id="cfe1b-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="cfe1b-122">Armazenamento de local de aplicativo</span><span class="sxs-lookup"><span data-stu-id="cfe1b-122">App location storage</span></span> |<span data-ttu-id="cfe1b-123">Conteúdo compartilhado</span><span class="sxs-lookup"><span data-stu-id="cfe1b-123">Shared content</span></span> |<span data-ttu-id="cfe1b-124">O aplicativo é executado na memória da instância do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cfe1b-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="cfe1b-125">Consome memória e boa conexão toostreaming (arquivo) servidor em que reside o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="cfe1b-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="cfe1b-126">Disco (em cache)</span><span class="sxs-lookup"><span data-stu-id="cfe1b-126">Disk (Cached)</span></span> |<span data-ttu-id="cfe1b-127">Execução rápida.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-127">Fast execution.</span></span> <span data-ttu-id="cfe1b-128">O aplicativo não depende de disponibilidade da Fonte de Conteúdo</span><span class="sxs-lookup"><span data-stu-id="cfe1b-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="cfe1b-129">Inchaço - ocupa o espaço da imagem (limite de 127 GB)</span><span class="sxs-lookup"><span data-stu-id="cfe1b-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="cfe1b-130">Direcionamento</span><span class="sxs-lookup"><span data-stu-id="cfe1b-130">Targeting</span></span> |<span data-ttu-id="cfe1b-131">Usuário</span><span class="sxs-lookup"><span data-stu-id="cfe1b-131">User</span></span> |<span data-ttu-id="cfe1b-132">Exige a infraestrutura completa do App-V autônomo</span><span class="sxs-lookup"><span data-stu-id="cfe1b-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="cfe1b-133">Global (máquina)</span><span class="sxs-lookup"><span data-stu-id="cfe1b-133">Global (machine)</span></span> |<span data-ttu-id="cfe1b-134">Pré-publicar ou destinar usando o servidor de Publicação</span><span class="sxs-lookup"><span data-stu-id="cfe1b-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="cfe1b-135">Necessário tooupdate sua imagem do Azure se você quiser tooupdate Olá aplicativo (grande).</span><span class="sxs-lookup"><span data-stu-id="cfe1b-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="cfe1b-136">Ocupa algum espaço na imagem.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="cfe1b-137">Depois de criar sua imagem personalizada e sua coleção híbrida, publique seu aplicativo, atribuir usuários e aproveitar seus aplicativos existentes do App-V hospedados no Azure RemoteApp entregues tooany dispositivo em qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="cfe1b-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

