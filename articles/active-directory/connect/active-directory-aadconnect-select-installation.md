---
title: "Azure AD Connect: Selecionar o tipo de instalação | Microsoft Docs"
description: "Este tópico o orienta como instalação de saudação tooselect digite toouse para conexão do AD do Azure"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="33cb1-103">Selecione quais toouse do tipo de instalação para o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="33cb1-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="33cb1-104">O Azure AD Connect oferece dois tipos de instalação para uma nova instalação: Expressa e personalizado.</span><span class="sxs-lookup"><span data-stu-id="33cb1-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="33cb1-105">Este tópico Ajuda toodecide qual opção toouse durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="33cb1-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="33cb1-106">Express</span><span class="sxs-lookup"><span data-stu-id="33cb1-106">Express</span></span>
<span data-ttu-id="33cb1-107">Express é a opção mais comum de saudação e é usado por cerca de 90% de todas as novas instalações.</span><span class="sxs-lookup"><span data-stu-id="33cb1-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="33cb1-108">Foi projetado tooprovide uma configuração que funciona para cenários mais comuns de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="33cb1-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="33cb1-109">Ela pressupõe que:</span><span class="sxs-lookup"><span data-stu-id="33cb1-109">It assumes:</span></span>

- <span data-ttu-id="33cb1-110">Você tem uma única floresta local do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="33cb1-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="33cb1-111">Você tem uma conta de administrador corporativo que você pode usar para a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="33cb1-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="33cb1-112">Há menos de 100.000 objetos em seu Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="33cb1-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="33cb1-113">Você recebe:</span><span class="sxs-lookup"><span data-stu-id="33cb1-113">You get:</span></span>

- <span data-ttu-id="33cb1-114">[Sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md) do local tooAzure AD para logon único.</span><span class="sxs-lookup"><span data-stu-id="33cb1-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="33cb1-115">Uma configuração que sincroniza [usuários, grupos, contatos e computadores com Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="33cb1-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="33cb1-116">Sincronização de todos os objetos qualificados em todos os domínios e em todas as UOs.</span><span class="sxs-lookup"><span data-stu-id="33cb1-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="33cb1-117">[A atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md) é habilitado toomake-se de que você sempre use a versão mais recente disponível de saudação.</span><span class="sxs-lookup"><span data-stu-id="33cb1-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="33cb1-118">Opções onde ainda é possível usar a Expressa:</span><span class="sxs-lookup"><span data-stu-id="33cb1-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="33cb1-119">Se você não quiser toosynchronize todas as UOs, você ainda pode usar o Express e na última página de hello, desmarque **iniciar o processo de sincronização hello...** *.</span><span class="sxs-lookup"><span data-stu-id="33cb1-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="33cb1-120">Em seguida, execute novamente o Assistente de instalação de saudação e alterar Olá OUs [opções de configuração](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) e habilitar a sincronização agendada.</span><span class="sxs-lookup"><span data-stu-id="33cb1-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="33cb1-121">Você deseja tooenable um dos recursos de saudação do Azure AD Premium, como write-back de senha.</span><span class="sxs-lookup"><span data-stu-id="33cb1-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="33cb1-122">Passam primeiro pelo tooget express saudação inicial a instalação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="33cb1-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="33cb1-123">Em seguida, execute novamente o Assistente de instalação hello e alterar Olá [opções de configuração](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="33cb1-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="33cb1-124">Personalizado</span><span class="sxs-lookup"><span data-stu-id="33cb1-124">Custom</span></span>
<span data-ttu-id="33cb1-125">caminho personalizado Olá permite que muitos mais opções do express.</span><span class="sxs-lookup"><span data-stu-id="33cb1-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="33cb1-126">Ele deve ser usado em todos os casos em que a configuração de saudação descrita na seção anterior para express não é representativa para sua organização.</span><span class="sxs-lookup"><span data-stu-id="33cb1-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="33cb1-127">Use quando:</span><span class="sxs-lookup"><span data-stu-id="33cb1-127">Use when:</span></span>

- <span data-ttu-id="33cb1-128">Você não tem a conta de administrador do acesso tooan enterprise no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="33cb1-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="33cb1-129">Você tem mais de uma floresta ou planejar toosynchronize mais de uma floresta em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="33cb1-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="33cb1-130">Você tiver domínios na floresta não pode ser acessada do servidor de conectar hello.</span><span class="sxs-lookup"><span data-stu-id="33cb1-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="33cb1-131">Planejar toouse federação ou autenticação de passagem de entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="33cb1-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="33cb1-132">Você tem mais de 100.000 objetos e precisa toouse um completo do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="33cb1-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="33cb1-133">Planejar toouse a filtragem baseada em grupo e não apenas domínio ou filtragem baseada em unidade Organizacional.</span><span class="sxs-lookup"><span data-stu-id="33cb1-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="33cb1-134">Atualização do DirSync</span><span class="sxs-lookup"><span data-stu-id="33cb1-134">Upgrade from DirSync</span></span>
<span data-ttu-id="33cb1-135">Se você estiver usando o DirSync, siga etapas Olá [atualizar do DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade sua configuração existente.</span><span class="sxs-lookup"><span data-stu-id="33cb1-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="33cb1-136">Há duas opções de atualização diferentes:</span><span class="sxs-lookup"><span data-stu-id="33cb1-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="33cb1-137">Tooinstall atualização in-loco se conectar em Olá mesmo servidor.</span><span class="sxs-lookup"><span data-stu-id="33cb1-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="33cb1-138">Paralelo implantação tooinstall conectar em um novo servidor, enquanto o servidor DirSync existente de saudação ainda está operacional.</span><span class="sxs-lookup"><span data-stu-id="33cb1-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="33cb1-139">Atualização do Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="33cb1-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="33cb1-140">Se você estiver usando sincronização do AD do Azure, você pode seguir Olá [mesmas etapas](active-directory-aadconnect-upgrade-previous-version.md) como quando você atualiza de uma conexão versão tooa mais recente.</span><span class="sxs-lookup"><span data-stu-id="33cb1-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="33cb1-141">Há duas opções de atualização diferentes:</span><span class="sxs-lookup"><span data-stu-id="33cb1-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="33cb1-142">Tooinstall atualização in-loco se conectar em Olá mesmo servidor.</span><span class="sxs-lookup"><span data-stu-id="33cb1-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="33cb1-143">Migração de giro tooinstall conectar em um novo servidor ao servidor de sincronização do AD do Azure existente Olá ainda está operacional.</span><span class="sxs-lookup"><span data-stu-id="33cb1-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="33cb1-144">Migrar do FIM2010 ou MIM2016</span><span class="sxs-lookup"><span data-stu-id="33cb1-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="33cb1-145">Se atualmente você estiver usando o Forefront Identity Manager 2010 ou o Microsoft Identity Manager 2016 com hello conector AD do Azure, sua única opção é uma migração.</span><span class="sxs-lookup"><span data-stu-id="33cb1-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="33cb1-146">Execute as etapas de saudação descritas em [movimento migração](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="33cb1-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="33cb1-147">Nas etapas hello, substitua mencionar do Azure AD Sync FIM2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="33cb1-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33cb1-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33cb1-148">Next steps</span></span>
<span data-ttu-id="33cb1-149">Dependendo da opção de saudação selecionado toouse, use a tabela de saudação do toofind esquerdo toohello conteúdo seu artigo com hello etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="33cb1-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
