---
title: toomigrate aaaHow de tooan uma VNET do RemoteApp VNET do Azure | Microsoft Docs
description: Saiba como toomigrate de tooan uma VNET do RemoteApp VNET do Azure
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a><span data-ttu-id="55197-103">Como toomigrate uma coleção híbrida de tooan uma VNET do RemoteApp VNET do Azure</span><span class="sxs-lookup"><span data-stu-id="55197-103">How toomigrate a hybrid collection from a RemoteApp VNET tooan Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="55197-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="55197-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="55197-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="55197-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="55197-106">Boas notícias!</span><span class="sxs-lookup"><span data-stu-id="55197-106">Good news!</span></span> <span data-ttu-id="55197-107">Habilitamos coleções do RemoteApp híbrida toodeploy diretamente no seu existente do Azure redes virtuais (VNETs) em vez de criar VNETs RemoteApp específicos.</span><span class="sxs-lookup"><span data-stu-id="55197-107">We have enabled you toodeploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="55197-108">Isso permite que você tire proveito de hello mais recentes recursos de rede virtual (como a rota expressa) e dê sua tooother de acesso direto rede híbrida coleções serviços do Azure e máquinas virtuais implantadas toothat VNET.</span><span class="sxs-lookup"><span data-stu-id="55197-108">This lets you take advantage of hello latest VNET features (like ExpressRoute) and give your hybrid collections direct network access tooother Azure services and virtual machines deployed toothat VNET.</span></span>  <span data-ttu-id="55197-109">(Isso apresenta um desempenho melhor e mais fácil instalação que configurações de VNET para VNET).</span><span class="sxs-lookup"><span data-stu-id="55197-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="55197-110">Digamos que você já criou uma coleção híbrida de RemoteApp chamada *ColeçãoOriginal* com uma VNET do RemoteApp chamada *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="55197-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="55197-111">Aqui estão Olá etapas toomigrate-tooa nova rede virtual do Azure chamado *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="55197-111">Here are hello steps toomigrate it tooa new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="55197-112">Em Olá **redes** guia Olá [portal de gerenciamento](http://manage.windowsazure.com/), crie uma rede virtual chamada *AzureVNET*usando hello mesmo local, a configuração de DNS e o espaço de endereço (para pelo menos um de saudação *AzureVNET* sub-redes) que você usou para *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="55197-112">On hello **Networks** tab in hello [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using hello same location, DNS configuration, and address space (for at least one of hello *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="55197-113">Configurar *AzureVNET* tooeither de host ou tem conectividade de rede toohello implantação de Active Directory que *OriginalCollection* é integrado ao domínio.</span><span class="sxs-lookup"><span data-stu-id="55197-113">Configure *AzureVNET* tooeither host or have network connectivity toohello Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="55197-114">Em Olá **RemoteApps** guia, crie uma nova coleção do RemoteApp chamada *nova coleção*.</span><span class="sxs-lookup"><span data-stu-id="55197-114">On hello **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="55197-115">(Olá use **criar com uma rede virtual** opção, não **criação rápida**.)</span><span class="sxs-lookup"><span data-stu-id="55197-115">(Use hello **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="55197-116">Configurar *NewCollection* toobe implantado sub-rede tooa *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="55197-116">Configure *NewCollection* toobe deployed tooa subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="55197-117">Configurar *NewCollection* toouse Olá a mesma imagem e informações de associação de domínio que você usou para *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="55197-117">Configure *NewCollection* toouse hello same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="55197-118">Após algumas horas, *NovaColeção* aparecerá na sua lista de coleções com um estado Ativo.</span><span class="sxs-lookup"><span data-stu-id="55197-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="55197-119">Agora, se você não precisa toomigrate qualquer informação de usuário do hello original toohello nova coleção, segue estas etapas:</span><span class="sxs-lookup"><span data-stu-id="55197-119">Now, if you DON’T need toomigrate any user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="55197-120">Exclua *ColeçãoOriginal*.</span><span class="sxs-lookup"><span data-stu-id="55197-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="55197-121">Exclua *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="55197-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="55197-122">E pronto!</span><span class="sxs-lookup"><span data-stu-id="55197-122">And, you’re done!</span></span>

<span data-ttu-id="55197-123">Como alternativa, se você precisar de informações de usuário de toomigrate de saudação original toohello nova coleção, segue estas etapas:</span><span class="sxs-lookup"><span data-stu-id="55197-123">Alternately, if you DO need toomigrate user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="55197-124">Enviar um email muito[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) com sua ID de assinatura do Azure, Olá nome de sua coleção original e o nome de saudação da nova coleção e peça-lhes toomigrate as informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="55197-124">Send an email too[remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, hello name of your original collection, and hello name of your new collection, and ask them toomigrate your user information.</span></span>
2. <span data-ttu-id="55197-125">Dentro de 2 dias úteis o equipe do RemoteApp Olá moverá lista de acesso de usuário hello e todos os documentos do usuário e configurações de usuário do hello original toohello nova coleção.</span><span class="sxs-lookup"><span data-stu-id="55197-125">Within 2 business days hello RemoteApp team will move hello user access list and all user documents and user settings from hello original collection toohello new collection.</span></span>
3. <span data-ttu-id="55197-126">Exclua *ColeçãoOriginal*.</span><span class="sxs-lookup"><span data-stu-id="55197-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="55197-127">Exclua *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="55197-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="55197-128">E pronto!</span><span class="sxs-lookup"><span data-stu-id="55197-128">And now, you’re done!</span></span>

<span data-ttu-id="55197-129">Se você tiver dúvidas ou precisar de ajuda especial, envie um email para [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="55197-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

