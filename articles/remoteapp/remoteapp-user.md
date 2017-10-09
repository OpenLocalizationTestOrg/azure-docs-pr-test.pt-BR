---
title: "aaaAdd tooyour um usuário coleção do RemoteApp do Azure | Microsoft Docs"
description: "Saiba como tooadd usuários tooyour coleção do RemoteApp do Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="600c9-103">Como tooadd tooyour um usuário coleção do RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="600c9-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="600c9-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="600c9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="600c9-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="600c9-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="600c9-106">Antes dos usuários podem ver e usar seus aplicativos no Azure RemoteApp, você tem toogrant tooyour coleção a eles acesso.</span><span class="sxs-lookup"><span data-stu-id="600c9-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="600c9-107">Isso faz parte de fácil Olá: em Olá **acesso de usuário** guia, insira informações de conta de saudação do usuário Olá e, em seguida, clique em marca de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="600c9-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="600c9-108">Quais informações da conta são necessárias?</span><span class="sxs-lookup"><span data-stu-id="600c9-108">What account information do you need?</span></span> <span data-ttu-id="600c9-109">Isso depende Olá tipo de coleção criado por você (nuvem ou híbrida) e se você estiver usando Office 365 ProPlus nessa coleção.</span><span class="sxs-lookup"><span data-stu-id="600c9-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="600c9-110">Identidades de usuário com suporte</span><span class="sxs-lookup"><span data-stu-id="600c9-110">Supported user identities</span></span>
<span data-ttu-id="600c9-111">tipos de coleção diferente de saudação (nuvem versus híbrido) suportam o uso de diferentes identidades de usuário para acesso tooapplications.</span><span class="sxs-lookup"><span data-stu-id="600c9-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="600c9-112">Para uma coleção híbrida do RemoteApp, você precisa tooset backup de uma infraestrutura de domínio do Active Directory local e um locatário do Active Directory do Azure com a integração de diretório (e opcionalmente o logon único).</span><span class="sxs-lookup"><span data-stu-id="600c9-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="600c9-113">Além disso, você precisa toocreate alguns objetos do Active Directory no diretório local de saudação.</span><span class="sxs-lookup"><span data-stu-id="600c9-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="600c9-114">Para uma coleção de nuvem do RemoteApp, qualquer usuário que tenha o Active Directory do Azure suporta identidades pode ser concedido usuário acesso tooRemoteApp tooinclude Accounts da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="600c9-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="600c9-115">Consulte a tabela de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="600c9-115">See hello table below.</span></span>

<span data-ttu-id="600c9-116">Os usuários do Office 365 são usuários do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="600c9-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="600c9-117">Se eles tiverem o Active Directory do Azure híbrido, as contas sincronizadas do diretório, eles poderão receber acesso de usuário em uma implantação híbrida do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="600c9-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="600c9-118">Você pode usar essa tabela como uma referência rápida para o qual há suporte para em sua coleção e quais são os requisitos de Active Directory Olá identidade.</span><span class="sxs-lookup"><span data-stu-id="600c9-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="600c9-119">Contas de usuário</span><span class="sxs-lookup"><span data-stu-id="600c9-119">User accounts</span></span> | <span data-ttu-id="600c9-120">Nuvem</span><span class="sxs-lookup"><span data-stu-id="600c9-120">Cloud</span></span> | <span data-ttu-id="600c9-121">Híbrido</span><span class="sxs-lookup"><span data-stu-id="600c9-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="600c9-122">Conta da Microsoft</span><span class="sxs-lookup"><span data-stu-id="600c9-122">Microsoft Account</span></span> |<span data-ttu-id="600c9-123">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-123">Yes</span></span> |<span data-ttu-id="600c9-124">Não</span><span class="sxs-lookup"><span data-stu-id="600c9-124">No</span></span> |
| <span data-ttu-id="600c9-125">Active Directory do Azure (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="600c9-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="600c9-126">Somente nuvem do Azure AD</span><span class="sxs-lookup"><span data-stu-id="600c9-126">Azure AD cloud only</span></span> |<span data-ttu-id="600c9-127">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-127">Yes</span></span> |<span data-ttu-id="600c9-128">Não</span><span class="sxs-lookup"><span data-stu-id="600c9-128">No</span></span> |
| <span data-ttu-id="600c9-129">ADsync com sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="600c9-129">ADsync with password sync</span></span> |<span data-ttu-id="600c9-130">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-130">Yes</span></span> |<span data-ttu-id="600c9-131">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-131">Yes</span></span> |
| <span data-ttu-id="600c9-132">ADsync sem sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="600c9-132">ADsync without password sync</span></span> |<span data-ttu-id="600c9-133">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-133">Yes</span></span> |<span data-ttu-id="600c9-134">Não</span><span class="sxs-lookup"><span data-stu-id="600c9-134">No</span></span> |
| <span data-ttu-id="600c9-135">ADsync com o AD FS</span><span class="sxs-lookup"><span data-stu-id="600c9-135">ADsync with AD FS</span></span> |<span data-ttu-id="600c9-136">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-136">Yes</span></span> |<span data-ttu-id="600c9-137">sim</span><span class="sxs-lookup"><span data-stu-id="600c9-137">Yes</span></span> |
| <span data-ttu-id="600c9-138">[Provedores de identidade de terceiros com suporte do Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (por exemplo, Ping)</span><span class="sxs-lookup"><span data-stu-id="600c9-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="600c9-139">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-139">Yes</span></span> |<span data-ttu-id="600c9-140">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-140">Yes</span></span> |
| <span data-ttu-id="600c9-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="600c9-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="600c9-142">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-142">Yes</span></span> |<span data-ttu-id="600c9-143">Sim</span><span class="sxs-lookup"><span data-stu-id="600c9-143">Yes</span></span> |

<span data-ttu-id="600c9-144">Verifique [obter mais informações](remoteapp-ad.md) sobre a configuração do Active Directory para o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="600c9-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="600c9-145">os usuários do Active Directory do Azure Olá devem ser do locatário Olá associado à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="600c9-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="600c9-146">(Você pode exibir e modificar sua assinatura do hello **configurações** no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="600c9-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="600c9-147">Consulte [locatário de Active Directory do Azure Olá alteração usado pelo RemoteApp](remoteapp-changetenant.md) para obter mais informações.)</span><span class="sxs-lookup"><span data-stu-id="600c9-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="600c9-148">Informações de conta de usuário do Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="600c9-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="600c9-149">Se você estiver usando a imagem de modelo Olá Office 365 ProPlus em sua coleção *ou* se você tiver criado uma imagem personalizada que usa o Office 365, são permitidos apenas os usuários tooadd do Active Directory do Azure que têm assinaturas do Office 365 para Olá domínio padrão da sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="600c9-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="600c9-150">Consulte [Usando o Office 365 com o Azure RemoteApp](remoteapp-o365.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="600c9-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

