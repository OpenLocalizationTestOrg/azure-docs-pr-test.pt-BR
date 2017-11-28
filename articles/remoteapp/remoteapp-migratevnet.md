---
title: "Como migrar de uma coleção híbrida de uma VNET RemoteApp para uma VNET do Azure | Microsoft Docs"
description: "Aprenda como migrar de uma coleção híbrida de uma VNET RemoteApp para uma VNET do Azure"
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
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a><span data-ttu-id="3aa3e-103">Como migrar uma coleção híbrida de um VNET RemoteApp para uma VNET do Azure</span><span class="sxs-lookup"><span data-stu-id="3aa3e-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3aa3e-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3aa3e-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3aa3e-106">Boas notícias!</span><span class="sxs-lookup"><span data-stu-id="3aa3e-106">Good news!</span></span> <span data-ttu-id="3aa3e-107">Habilitamos você para implantar as coleções híbridas de RemoteApp diretamente para as redes virtuais (VNETs) do Azure existentes em vez de criar VNETs específicas do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="3aa3e-108">Isso permite a você aproveitar os recursos mais recentes do VNET (como ExpressRoute) e dar a suas coleções híbridas acesso direto de rede a outros serviços do Azure e máquinas virtuais implantadas nessa VNET.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span></span>  <span data-ttu-id="3aa3e-109">(Isso apresenta um desempenho melhor e mais fácil instalação que configurações de VNET para VNET).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="3aa3e-110">Digamos que você já criou uma coleção híbrida de RemoteApp chamada *ColeçãoOriginal* com uma VNET do RemoteApp chamada *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="3aa3e-111">Aqui estão as etapas para migrá-la para uma nova VNET do Azure chamada *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="3aa3e-112">Na guia **Redes** do [Portal de Gerenciamento](http://manage.windowsazure.com/), crie uma VNET chamada *AzureVNET*, usando o mesmo local, a configuração do DNS e espaço de endereço (para pelo menos uma das sub-redes do *AzureVNET*) que você usou para a *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="3aa3e-113">Configure *AzureVNET* para hospedar ou ter conectividade de rede para a implantação do Active Directory ao qual o domínio *ColeçãoOriginal* é integrado.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="3aa3e-114">Na guia **RemoteApps** , crie uma nova coleção de RemoteApp chamada *NovaColeção*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="3aa3e-115">(Use a opção **Criar com VNET**, e não **Criação rápida**.)</span><span class="sxs-lookup"><span data-stu-id="3aa3e-115">(Use the **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="3aa3e-116">Configure *NovaColeção* para ser implantada em uma sub-rede em *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="3aa3e-117">Configure *NovaColeção* para usar as mesmas informações de imagem e ingresso no domínio que as usadas para *ColeçãoOriginal*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="3aa3e-118">Após algumas horas, *NovaColeção* aparecerá na sua lista de coleções com um estado Ativo.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="3aa3e-119">Agora, se você NÃO precisa migrar informações do usuário da coleção original para a nova coleção, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="3aa3e-120">Exclua *ColeçãoOriginal*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="3aa3e-121">Exclua *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="3aa3e-122">E pronto!</span><span class="sxs-lookup"><span data-stu-id="3aa3e-122">And, you’re done!</span></span>

<span data-ttu-id="3aa3e-123">Alternativamente, se você PRECISA migrar informações do usuário da coleção original para a nova coleção, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3aa3e-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="3aa3e-124">Envie um email para [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) com sua ID de assinatura do Azure, o nome de sua coleção original e o nome da nova coleção e peça-lhes para migrarem suas informações de usuário.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span></span>
2. <span data-ttu-id="3aa3e-125">Em 2 dias úteis a equipe RemoteApp moverá a lista de acesso de usuário e todos os documentos e configurações de usuário da coleção original para a nova coleção.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span></span>
3. <span data-ttu-id="3aa3e-126">Exclua *ColeçãoOriginal*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="3aa3e-127">Exclua *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="3aa3e-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="3aa3e-128">E pronto!</span><span class="sxs-lookup"><span data-stu-id="3aa3e-128">And now, you’re done!</span></span>

<span data-ttu-id="3aa3e-129">Se você tiver dúvidas ou precisar de ajuda especial, envie um email para [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="3aa3e-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

