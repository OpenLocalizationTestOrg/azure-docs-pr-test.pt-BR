---
title: Usando aplicativos do App-V com o Azure RemoteApp| Microsoft Docs
description: Saiba como usar os aplicativos App-V no Azure RemoteApp.
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
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="5b697-103">Usando os aplicativos App-V no Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5b697-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5b697-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="5b697-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5b697-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5b697-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5b697-106">Você pode usar os aplicativos do App-V em uma coleção híbrida do Azure RemoteApp, o que requer o ingresso no domínio.</span><span class="sxs-lookup"><span data-stu-id="5b697-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="5b697-107">Antes de começar, instale o cliente do App-V 5.1 com as atualizações mais recentes.</span><span class="sxs-lookup"><span data-stu-id="5b697-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span></span> <span data-ttu-id="5b697-108">Você precisará criar uma [imagem personalizada](remoteapp-create-custom-image.md) que inclua o cliente de App-V.</span><span class="sxs-lookup"><span data-stu-id="5b697-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span></span>  

<span data-ttu-id="5b697-109">É fácil usar sua infraestrutura existente do App-V com o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5b697-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="5b697-110">Como uma coleção híbrida é implantada em uma Rede Virtual do Azure com acesso ao controlador de domínio e as VMs são ingressadas no domínio, você poderá aproveitar a infraestrutura existente do App-V e os métodos de implantação para hospedar com facilidade o aplicativo App-V no Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5b697-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="5b697-111">Veja algumas considerações que você deve fazer com base no tipo de implantação do App-V que possui no momento:</span><span class="sxs-lookup"><span data-stu-id="5b697-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="5b697-112">Opções de configuração</span><span class="sxs-lookup"><span data-stu-id="5b697-112">Configuration options</span></span> |  | <span data-ttu-id="5b697-113">Positivo</span><span class="sxs-lookup"><span data-stu-id="5b697-113">Positive</span></span> | <span data-ttu-id="5b697-114">Negativo</span><span class="sxs-lookup"><span data-stu-id="5b697-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b697-115">Método de entrega</span><span class="sxs-lookup"><span data-stu-id="5b697-115">Delivery method</span></span> |<span data-ttu-id="5b697-116">Streaming (por demanda)</span><span class="sxs-lookup"><span data-stu-id="5b697-116">Streaming (on-demand)</span></span> |<span data-ttu-id="5b697-117">O aplicativo é sempre a versão mais recente e está sempre atualizado</span><span class="sxs-lookup"><span data-stu-id="5b697-117">App is always the latest and fresh</span></span> |<span data-ttu-id="5b697-118">Latência da primeira vez</span><span class="sxs-lookup"><span data-stu-id="5b697-118">First time latency</span></span> |
| <span data-ttu-id="5b697-119">Montado</span><span class="sxs-lookup"><span data-stu-id="5b697-119">Mounted</span></span> |<span data-ttu-id="5b697-120">Mais rápido; o aplicativo já está presente na VM</span><span class="sxs-lookup"><span data-stu-id="5b697-120">Fastest; app is already present on the VM</span></span> |<span data-ttu-id="5b697-121">Inchaço - ocupa o espaço da imagem (limite de 127 GB)</span><span class="sxs-lookup"><span data-stu-id="5b697-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="5b697-122">Armazenamento de local de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5b697-122">App location storage</span></span> |<span data-ttu-id="5b697-123">Conteúdo compartilhado</span><span class="sxs-lookup"><span data-stu-id="5b697-123">Shared content</span></span> |<span data-ttu-id="5b697-124">O aplicativo é executado na memória da instância do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5b697-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="5b697-125">Consome memória e a conexão com o servidor de streaming (arquivo) em que o aplicativo reside</span><span class="sxs-lookup"><span data-stu-id="5b697-125">Eats memory and good connection to streaming (file) server where the app resides</span></span> |
| <span data-ttu-id="5b697-126">Disco (em cache)</span><span class="sxs-lookup"><span data-stu-id="5b697-126">Disk (Cached)</span></span> |<span data-ttu-id="5b697-127">Execução rápida.</span><span class="sxs-lookup"><span data-stu-id="5b697-127">Fast execution.</span></span> <span data-ttu-id="5b697-128">O aplicativo não depende de disponibilidade da Fonte de Conteúdo</span><span class="sxs-lookup"><span data-stu-id="5b697-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="5b697-129">Inchaço - ocupa o espaço da imagem (limite de 127 GB)</span><span class="sxs-lookup"><span data-stu-id="5b697-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="5b697-130">Direcionamento</span><span class="sxs-lookup"><span data-stu-id="5b697-130">Targeting</span></span> |<span data-ttu-id="5b697-131">Usuário</span><span class="sxs-lookup"><span data-stu-id="5b697-131">User</span></span> |<span data-ttu-id="5b697-132">Exige a infraestrutura completa do App-V autônomo</span><span class="sxs-lookup"><span data-stu-id="5b697-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="5b697-133">Global (máquina)</span><span class="sxs-lookup"><span data-stu-id="5b697-133">Global (machine)</span></span> |<span data-ttu-id="5b697-134">Pré-publicar ou destinar usando o servidor de Publicação</span><span class="sxs-lookup"><span data-stu-id="5b697-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="5b697-135">Você precisará atualizar a imagem do Azure se quiser atualizar o aplicativo (enorme).</span><span class="sxs-lookup"><span data-stu-id="5b697-135">Need to update your Azure image if you want to update the app (huge).</span></span> <span data-ttu-id="5b697-136">Ocupa algum espaço na imagem.</span><span class="sxs-lookup"><span data-stu-id="5b697-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="5b697-137">Depois de criar sua imagem personalizada e sua coleção híbrida, publique seu aplicativo, atribua usuários e aproveite seus aplicativos existentes do App-V hospedados no Azure RemoteApp entregues a qualquer dispositivo em qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="5b697-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span></span>

