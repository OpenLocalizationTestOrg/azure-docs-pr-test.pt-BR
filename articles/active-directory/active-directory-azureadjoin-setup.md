---
title: "aaaSetting a junção do Azure AD para seus usuários | Microsoft Docs"
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
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="1eced-103">Configuração da Junção do Azure AD na sua organização</span><span class="sxs-lookup"><span data-stu-id="1eced-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="1eced-104">Antes de configurar a junção do Azure Active Directory (junção do Azure AD), você precisar de sincronização de tooeither até seu diretório local da nuvem de toohello de usuários ou criar manualmente as contas gerenciadas no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1eced-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="1eced-105">Instruções detalhadas para sincronizar seu tooAzure de usuários local AD é abordado em [integrando suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="1eced-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="1eced-106">toomanually criar e gerenciar os usuários no AD do Azure, consulte muito[gerenciamento de usuário no AD do Azure](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="1eced-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="1eced-107">Configure o registro de dispositivos</span><span class="sxs-lookup"><span data-stu-id="1eced-107">Set up device registration</span></span>
1. <span data-ttu-id="1eced-108">Faça logon no toohello portal do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="1eced-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="1eced-109">No painel esquerdo do hello, selecione **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eced-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="1eced-110">Em Olá **diretório** , selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="1eced-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="1eced-111">Selecione Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="1eced-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="1eced-112">Vá toohello **dispositivos** seção.</span><span class="sxs-lookup"><span data-stu-id="1eced-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="1eced-113">Em Olá **dispositivos** guia, defina Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="1eced-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="1eced-114">**MÁXIMO número de dispositivos por usuário**: selecione Olá o número máximo de dispositivos que um usuário pode ter no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1eced-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="1eced-115">Se um usuário atingir essa cota, eles não estarão dispositivos adicionais capaz de tooadd até que um ou mais dos seus dispositivos existentes são removidos.</span><span class="sxs-lookup"><span data-stu-id="1eced-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="1eced-116">**EXIGIR autenticação MULTIFATOR tooJOIN dispositivos**: definir se os usuários são necessária tooprovide uma autenticação de segundo fator toojoin tooAzure seu dispositivo AD.</span><span class="sxs-lookup"><span data-stu-id="1eced-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="1eced-117">Para obter mais informações sobre o Azure multi-Factor Authentication, consulte [guia de Introdução ao Azure multi-Factor Authentication na nuvem Olá](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="1eced-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="1eced-118">**Os usuários podem dispositivos de junção do AZURE AD**: selecione Olá usuários e grupos são permitidos toojoin dispositivos tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="1eced-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="1eced-119">**DISPOSITIVOS que ingressaram no AD do AZURE ON de administradores adicionais**: com o Azure AD Premium ou Olá Enterprise Mobility Suite (EMS), você pode escolher quais usuários são concedidos direitos de administrador local toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1eced-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="1eced-120">Os administradores globais e os proprietários do dispositivo recebem direitos de administrador local por padrão.</span><span class="sxs-lookup"><span data-stu-id="1eced-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="1eced-121"><center>![Configure o registro de dispositivos](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="1eced-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="1eced-122">Depois de configurar junção do Azure AD para seus usuários, eles podem se conectar dispositivos pessoais ou tooAzure AD por meio de sua empresa.</span><span class="sxs-lookup"><span data-stu-id="1eced-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="1eced-123">A seguir estão os três cenários de saudação você pode usar tooenable tooset seus usuários a junção do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1eced-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="1eced-124">Os usuários se associar a um dispositivo da empresa diretamente tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="1eced-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="1eced-125">Usuários toohello de dispositivo de uma empresa de associação de domínio do Active Directory local e estende Olá dispositivo tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="1eced-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="1eced-126">Adicionarem usuários ou contas de estudante tooWindows em um dispositivo pessoal</span><span class="sxs-lookup"><span data-stu-id="1eced-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="1eced-127">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="1eced-127">Additional information</span></span>
* [<span data-ttu-id="1eced-128">Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho</span><span class="sxs-lookup"><span data-stu-id="1eced-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="1eced-129">Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1eced-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="1eced-130">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eced-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="1eced-131">Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10</span><span class="sxs-lookup"><span data-stu-id="1eced-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="1eced-132">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eced-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

