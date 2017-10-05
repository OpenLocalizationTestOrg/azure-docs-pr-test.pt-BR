---
title: "Adicionar um usuário à sua coleção do Azure RemoteApp | Microsoft Docs"
description: "Saiba como adicionar usuários à sua coleção do RemoteApp do Azure"
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
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="908c1-103">Como adicionar um usuário à sua coleção do RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="908c1-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="908c1-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="908c1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="908c1-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="908c1-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="908c1-106">Antes que os usuários possam ver e usar seus aplicativos no RemoteApp do Azure, você precisa conceder acesso à sua coleção a eles.</span><span class="sxs-lookup"><span data-stu-id="908c1-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="908c1-107">Essa é a parte fácil: na guia **Acesso de Usuário** , insira as informações da conta para o usuário e depois clique na marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="908c1-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="908c1-108">Quais informações da conta são necessárias?</span><span class="sxs-lookup"><span data-stu-id="908c1-108">What account information do you need?</span></span> <span data-ttu-id="908c1-109">Isso depende do tipo de coleção criada (nuvem ou híbrida) e se você estiver usando Office 365 ProPlus nessa coleção.</span><span class="sxs-lookup"><span data-stu-id="908c1-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="908c1-110">Identidades de usuário com suporte</span><span class="sxs-lookup"><span data-stu-id="908c1-110">Supported user identities</span></span>
<span data-ttu-id="908c1-111">Os tipos de coleção diferentes (nuvem versus híbridos) são compatíveis com o uso de identidades de usuário diferentes para acesso aos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="908c1-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="908c1-112">Para obter uma coleção híbrida do RemoteApp, você precisa configurar uma infraestrutura de domínio do Active Directory local e um locatário do Active Directory do Azure com a Integração de diretório (e opcionalmente logon único).</span><span class="sxs-lookup"><span data-stu-id="908c1-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="908c1-113">Além disso, você precisa criar alguns objetos do Active Directory no diretório local.</span><span class="sxs-lookup"><span data-stu-id="908c1-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="908c1-114">Para uma coleção de nuvem do RemoteApp, qualquer usuário que tenha o Active Directory do Azure que dá suporte a identidades pode receber acesso de usuário para o RemoteApp para incluir as Contas da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="908c1-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="908c1-115">Consulte a tabela abaixo.</span><span class="sxs-lookup"><span data-stu-id="908c1-115">See the table below.</span></span>

<span data-ttu-id="908c1-116">Os usuários do Office 365 são usuários do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="908c1-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="908c1-117">Se eles tiverem o Active Directory do Azure híbrido, as contas sincronizadas do diretório, eles poderão receber acesso de usuário em uma implantação híbrida do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="908c1-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="908c1-118">Você pode usar essa tabela como uma referência rápida sobre qual identidade tem suporte em sua coleção e quais são os requisitos do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="908c1-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="908c1-119">Contas de usuário</span><span class="sxs-lookup"><span data-stu-id="908c1-119">User accounts</span></span> | <span data-ttu-id="908c1-120">Nuvem</span><span class="sxs-lookup"><span data-stu-id="908c1-120">Cloud</span></span> | <span data-ttu-id="908c1-121">Híbrido</span><span class="sxs-lookup"><span data-stu-id="908c1-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="908c1-122">Conta da Microsoft</span><span class="sxs-lookup"><span data-stu-id="908c1-122">Microsoft Account</span></span> |<span data-ttu-id="908c1-123">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-123">Yes</span></span> |<span data-ttu-id="908c1-124">Não</span><span class="sxs-lookup"><span data-stu-id="908c1-124">No</span></span> |
| <span data-ttu-id="908c1-125">Active Directory do Azure (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="908c1-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="908c1-126">Somente nuvem do Azure AD</span><span class="sxs-lookup"><span data-stu-id="908c1-126">Azure AD cloud only</span></span> |<span data-ttu-id="908c1-127">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-127">Yes</span></span> |<span data-ttu-id="908c1-128">Não</span><span class="sxs-lookup"><span data-stu-id="908c1-128">No</span></span> |
| <span data-ttu-id="908c1-129">ADsync com sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="908c1-129">ADsync with password sync</span></span> |<span data-ttu-id="908c1-130">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-130">Yes</span></span> |<span data-ttu-id="908c1-131">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-131">Yes</span></span> |
| <span data-ttu-id="908c1-132">ADsync sem sincronização de senha</span><span class="sxs-lookup"><span data-stu-id="908c1-132">ADsync without password sync</span></span> |<span data-ttu-id="908c1-133">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-133">Yes</span></span> |<span data-ttu-id="908c1-134">Não</span><span class="sxs-lookup"><span data-stu-id="908c1-134">No</span></span> |
| <span data-ttu-id="908c1-135">ADsync com o AD FS</span><span class="sxs-lookup"><span data-stu-id="908c1-135">ADsync with AD FS</span></span> |<span data-ttu-id="908c1-136">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-136">Yes</span></span> |<span data-ttu-id="908c1-137">sim</span><span class="sxs-lookup"><span data-stu-id="908c1-137">Yes</span></span> |
| <span data-ttu-id="908c1-138">[Provedores de identidade de terceiros com suporte do Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (por exemplo, Ping)</span><span class="sxs-lookup"><span data-stu-id="908c1-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="908c1-139">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-139">Yes</span></span> |<span data-ttu-id="908c1-140">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-140">Yes</span></span> |
| <span data-ttu-id="908c1-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="908c1-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="908c1-142">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-142">Yes</span></span> |<span data-ttu-id="908c1-143">Sim</span><span class="sxs-lookup"><span data-stu-id="908c1-143">Yes</span></span> |

<span data-ttu-id="908c1-144">Verifique [obter mais informações](remoteapp-ad.md) sobre a configuração do Active Directory para o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="908c1-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="908c1-145">Os usuários do Azure Active Directory devem ser do locatário que está associado à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="908c1-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="908c1-146">(Você pode exibir e modificar a sua assinatura na guia **Configurações** no portal.</span><span class="sxs-lookup"><span data-stu-id="908c1-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="908c1-147">Consulte [Alterar o locatário do Active Directory do Azure usado pelo RemoteApp](remoteapp-changetenant.md) para obter mais informações.)</span><span class="sxs-lookup"><span data-stu-id="908c1-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="908c1-148">Informações de conta de usuário do Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="908c1-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="908c1-149">Se você estiver usando a imagem do modelo do Office 365 ProPlus em sua coleção *ou* se você criou uma imagem personalizada que usa o Office 365, será possível adicionar apenas usuários do Azure Active Directory que têm assinaturas do Office 365 para o domínio padrão da sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="908c1-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="908c1-150">Consulte [Usando o Office 365 com o Azure RemoteApp](remoteapp-o365.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="908c1-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

