---
title: "Azure AD Connect: Selecionar o tipo de instalação | Microsoft Docs"
description: "Este tópico explica como selecionar o tipo de instalação para o Azure AD Connect"
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
ms.openlocfilehash: a5697686bd1f41d581554b27ce78897963e38c74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a><span data-ttu-id="9fb67-103">Selecione o tipo de instalação para o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="9fb67-103">Select which installation type to use for Azure AD Connect</span></span>
<span data-ttu-id="9fb67-104">O Azure AD Connect oferece dois tipos de instalação para uma nova instalação: Expressa e personalizado.</span><span class="sxs-lookup"><span data-stu-id="9fb67-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="9fb67-105">Este tópico ajuda você a decidir qual opção usar durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="9fb67-105">This topic helps you to decide which option to use during installation.</span></span>

## <a name="express"></a><span data-ttu-id="9fb67-106">Express</span><span class="sxs-lookup"><span data-stu-id="9fb67-106">Express</span></span>
<span data-ttu-id="9fb67-107">Expressa é a opção mais comum e é usada por cerca de 90% de todas as novas instalações.</span><span class="sxs-lookup"><span data-stu-id="9fb67-107">Express is the most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="9fb67-108">Ela foi projetada para fornecer uma configuração que funcione para os cenários mais comuns dos clientes.</span><span class="sxs-lookup"><span data-stu-id="9fb67-108">It was designed to provide a configuration that works for the most common customer scenarios.</span></span>

<span data-ttu-id="9fb67-109">Ela pressupõe que:</span><span class="sxs-lookup"><span data-stu-id="9fb67-109">It assumes:</span></span>

- <span data-ttu-id="9fb67-110">Você tem uma única floresta local do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9fb67-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="9fb67-111">Você tem uma conta de administrador corporativo que pode usar para a instalação.</span><span class="sxs-lookup"><span data-stu-id="9fb67-111">You have an enterprise administrator account you can use for the installation.</span></span>
- <span data-ttu-id="9fb67-112">Há menos de 100.000 objetos em seu Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="9fb67-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="9fb67-113">Você recebe:</span><span class="sxs-lookup"><span data-stu-id="9fb67-113">You get:</span></span>

- <span data-ttu-id="9fb67-114">[Sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md) do local para o Azure AD para logon único.</span><span class="sxs-lookup"><span data-stu-id="9fb67-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span></span>
- <span data-ttu-id="9fb67-115">Uma configuração que sincroniza [usuários, grupos, contatos e computadores com Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="9fb67-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="9fb67-116">Sincronização de todos os objetos qualificados em todos os domínios e em todas as UOs.</span><span class="sxs-lookup"><span data-stu-id="9fb67-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="9fb67-117">A [Atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md) está habilitada para garantir que você use sempre a versão mais recente disponível.</span><span class="sxs-lookup"><span data-stu-id="9fb67-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span></span>

<span data-ttu-id="9fb67-118">Opções onde ainda é possível usar a Expressa:</span><span class="sxs-lookup"><span data-stu-id="9fb67-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="9fb67-119">Se você não quiser sincronizar todas as UOs, ainda será possível usar a Expressa e, na última página, desmarcar **Iniciar o processo de sincronização...** .</span><span class="sxs-lookup"><span data-stu-id="9fb67-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect **Start the synchronization process...***.</span></span> <span data-ttu-id="9fb67-120">Em seguida, execute novamente o assistente de instalação e altere as UOs em [opções de configuração](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) e habilite a sincronização agendada.</span><span class="sxs-lookup"><span data-stu-id="9fb67-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="9fb67-121">Convém habilitar um dos recursos no Azure AD Premium, como Write-back de Senha.</span><span class="sxs-lookup"><span data-stu-id="9fb67-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="9fb67-122">Primeiro, use Expressa para concluir a instalação inicial.</span><span class="sxs-lookup"><span data-stu-id="9fb67-122">First go through express to get the initial installation completed.</span></span> <span data-ttu-id="9fb67-123">Em seguida, execute novamente o assistente de instalação e altere as [opções de configuração](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="9fb67-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="9fb67-124">Personalizado</span><span class="sxs-lookup"><span data-stu-id="9fb67-124">Custom</span></span>
<span data-ttu-id="9fb67-125">O caminho personalizado permite muito mais opções do que a Expressa.</span><span class="sxs-lookup"><span data-stu-id="9fb67-125">The customized path allows many more options than express.</span></span> <span data-ttu-id="9fb67-126">Ele deve ser usado em todos os casos nos quais a configuração descrita na seção anterior para Expressa não é representativa para sua organização.</span><span class="sxs-lookup"><span data-stu-id="9fb67-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="9fb67-127">Use quando:</span><span class="sxs-lookup"><span data-stu-id="9fb67-127">Use when:</span></span>

- <span data-ttu-id="9fb67-128">Você não tiver acesso a uma conta de administrador de empresa no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9fb67-128">You do not have access to an enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="9fb67-129">Você tiver mais de uma floresta, ou planejar sincronizar mais de uma floresta no futuro.</span><span class="sxs-lookup"><span data-stu-id="9fb67-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span></span>
- <span data-ttu-id="9fb67-130">Houver domínios em sua floresta que não podem ser acessados pelo servidor do Connect.</span><span class="sxs-lookup"><span data-stu-id="9fb67-130">You have domains in your forest not reachable from the Connect server.</span></span>
- <span data-ttu-id="9fb67-131">Você planejar usar a federação ou autenticação de passagem para entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="9fb67-131">You plan to use federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="9fb67-132">Houver mais de 100.000 objetos e você precisar usar um SQL Server completo.</span><span class="sxs-lookup"><span data-stu-id="9fb67-132">You have more than 100,000 objects and need to use a full SQL Server.</span></span>
- <span data-ttu-id="9fb67-133">Você planeja usar a filtragem baseada em grupo e não apenas a filtragem baseada em domínio ou unidade organizacional.</span><span class="sxs-lookup"><span data-stu-id="9fb67-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="9fb67-134">Atualizar do DirSync</span><span class="sxs-lookup"><span data-stu-id="9fb67-134">Upgrade from DirSync</span></span>
<span data-ttu-id="9fb67-135">Se você estiver usando o DirSync, execute as etapas em [Atualizar do DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) para atualizar sua configuração existente.</span><span class="sxs-lookup"><span data-stu-id="9fb67-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span></span> <span data-ttu-id="9fb67-136">Há duas opções de atualização diferentes:</span><span class="sxs-lookup"><span data-stu-id="9fb67-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="9fb67-137">Atualização in-loco para instalação do Connect no mesmo servidor.</span><span class="sxs-lookup"><span data-stu-id="9fb67-137">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="9fb67-138">Implantação paralela para instalação do Connect em um novo servidor, enquanto o servidor DirSync existente ainda está em operação.</span><span class="sxs-lookup"><span data-stu-id="9fb67-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="9fb67-139">Atualização do Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="9fb67-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="9fb67-140">Se você estiver usando o Azure AD Sync, poderá executar as [mesmas etapas](active-directory-aadconnect-upgrade-previous-version.md) usadas durante a atualização de uma versão do Connect para uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="9fb67-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span></span> <span data-ttu-id="9fb67-141">Há duas opções de atualização diferentes:</span><span class="sxs-lookup"><span data-stu-id="9fb67-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="9fb67-142">Atualização in-loco para instalação do Connect no mesmo servidor.</span><span class="sxs-lookup"><span data-stu-id="9fb67-142">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="9fb67-143">Migração de balanço (Swing-migration) para instalação do Connect em um novo servidor, enquanto o servidor Azure AD Sync existente ainda está em operação.</span><span class="sxs-lookup"><span data-stu-id="9fb67-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="9fb67-144">Migrar do FIM2010 ou MIM2016</span><span class="sxs-lookup"><span data-stu-id="9fb67-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="9fb67-145">Se você estiver usando o Forefront Identity Manager 2010 ou o Microsoft Identity Manager 2016 com o Azure AD Connector, sua única opção será uma migração.</span><span class="sxs-lookup"><span data-stu-id="9fb67-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="9fb67-146">Execute as etapas descritas em [migração de balanço (swing-migration)](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="9fb67-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="9fb67-147">Nas etapas, substitua qualquer menção ao Azure AD Sync por FIM2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="9fb67-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fb67-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9fb67-148">Next steps</span></span>
<span data-ttu-id="9fb67-149">Dependendo da opção selecionada, use o índice à esquerda para localizar o artigo com as etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="9fb67-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span></span>
