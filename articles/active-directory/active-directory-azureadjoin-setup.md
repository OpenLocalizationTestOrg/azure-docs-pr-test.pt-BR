---
title: "Configurando a Junção do Azure AD para seus usuários | Microsoft Docs"
description: "Explica como os administradores podem configurar a Junção do Azure AD para o diretório local e o registro de dispositivos."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: c37adc2654f7e931fdda22627e4a6ece2789fd86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="d6df3-103">Configuração da Junção do Azure AD na sua organização</span><span class="sxs-lookup"><span data-stu-id="d6df3-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="d6df3-104">Antes de configurar a Junção do Azure AD (Junção do Azure Active Directory), é necessário sincronizar seu diretório local de usuários com a nuvem ou criar manualmente as contas gerenciadas no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6df3-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="d6df3-105">Instruções detalhadas para sincronizar seus usuários locais com o Azure AD são fornecidas em [Integrando suas identidades locais com o Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d6df3-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="d6df3-106">Para criar e gerenciar usuários manualmente no Azure AD, consulte [Gerenciamento de usuários no Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6df3-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="d6df3-107">Configure o registro de dispositivos</span><span class="sxs-lookup"><span data-stu-id="d6df3-107">Set up device registration</span></span>
1. <span data-ttu-id="d6df3-108">Faça logon no Portal do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="d6df3-108">Log on to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="d6df3-109">No painel esquerdo, selecione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6df3-109">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="d6df3-110">Na guia **Diretório** , selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="d6df3-110">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="d6df3-111">Selecione a guia **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="d6df3-111">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="d6df3-112">Vá para a seção **Dispositivos** .</span><span class="sxs-lookup"><span data-stu-id="d6df3-112">Go to the **Devices** section.</span></span>
6. <span data-ttu-id="d6df3-113">Na guia **dispositivos** , defina o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d6df3-113">On the **devices** tab, set the following:</span></span>  
   * <span data-ttu-id="d6df3-114">**NÚMERO MÁXIMP DE DISPOSITIVOS POR USUÁRIO**: selecione o número máximo de dispositivos que um usuário pode ter no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6df3-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="d6df3-115">Se um usuário atingir esta cota, ele não poderá adicionar mais dispositivos até que um ou mais dos seus dispositivos existentes sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="d6df3-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="d6df3-116">**EXIGIR MULTI-FACTOR AUTH PARA UNIR DISPOSITIVOS**: defina se os usuários devem precisar fornecer um segundo fator de autenticação para unir seu dispositivo ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6df3-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="d6df3-117">Para saber mais sobre a Autenticação Multifator do Azure, confira [Introdução à Autenticação Multifator do Azure na nuvem](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="d6df3-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="d6df3-118">**USUÁRIOS PODEM UNIR DISPOSITIVOS AO AZURE AD**: selecione os usuários e grupos que têm permissão para unir dispositivos ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6df3-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span></span>
   * <span data-ttu-id="d6df3-119">**ADMINISTRADORES ADICIONAIS EM DISPOSITIVOS UNIDOS AO AZURE**: com o Azure AD Premium ou a EMS (Enterprise Mobility Suite), você pode escolher quais usuários recebem direitos de administrador local no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d6df3-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span></span> <span data-ttu-id="d6df3-120">Os administradores globais e os proprietários do dispositivo recebem direitos de administrador local por padrão.</span><span class="sxs-lookup"><span data-stu-id="d6df3-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="d6df3-121"><center>![Configure o registro de dispositivos](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="d6df3-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="d6df3-122">Após você configurar a Junção do Azure AD para seus usuários, eles podem se conectar ao Azure AD por meio de seus dispositivos pessoais ou corporativos.</span><span class="sxs-lookup"><span data-stu-id="d6df3-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="d6df3-123">A seguir estão os três cenários que você pode usar para habilitar seus usuários para configurarem a Junção do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d6df3-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span></span>

* <span data-ttu-id="d6df3-124">Os usuários unem um dispositivo da empresa diretamente ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6df3-124">Users join a company-owned device directly to Azure AD.</span></span>
* <span data-ttu-id="d6df3-125">Os usuários unem um dispositivo de empresa ao domínio no Active Directory local e o estendem para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6df3-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span></span>
* <span data-ttu-id="d6df3-126">Os usuários adicionam contas corporativas e de estudante ao Windows em um dispositivo pessoal</span><span class="sxs-lookup"><span data-stu-id="d6df3-126">Users add work or school accounts to Windows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="d6df3-127">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="d6df3-127">Additional information</span></span>
* [<span data-ttu-id="d6df3-128">Windows 10 para a empresa: maneiras de usar dispositivos para o trabalho</span><span class="sxs-lookup"><span data-stu-id="d6df3-128">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="d6df3-129">Estendendo os recursos de nuvem para dispositivos Windows 10 por meio da Junção do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d6df3-129">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="d6df3-130">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6df3-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="d6df3-131">Conectar dispositivos ingressados no domínio ao AD do Azure para experiências com o Windows 10</span><span class="sxs-lookup"><span data-stu-id="d6df3-131">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="d6df3-132">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6df3-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

