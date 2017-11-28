---
title: "aaaPermissions na Central de segurança do Azure | Microsoft Docs"
description: "Este artigo explica como a Central de segurança do Azure usa toousers de permissões de tooassign de controle de acesso baseado em função e identifica Olá permitido ações para cada função."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="01f70-103">Permissões na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="01f70-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="01f70-104">Central de segurança do Azure usa [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md), que fornece [funções internas](../active-directory/role-based-access-built-in-roles.md) que podem ser atribuídos toousers, grupos e serviços no Azure.</span><span class="sxs-lookup"><span data-stu-id="01f70-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="01f70-105">Central de segurança avalia a configuração de saudação de vulnerabilidades e problemas de segurança de tooidentify de recursos.</span><span class="sxs-lookup"><span data-stu-id="01f70-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="01f70-106">Na Central de segurança, você ver apenas as informações relacionadas tooa recurso quando foi atribuída a função de saudação do leitor, colaborador ou proprietário para Olá assinatura ou grupo de recursos que o recurso pertence.</span><span class="sxs-lookup"><span data-stu-id="01f70-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="01f70-107">Funções de toothese adição, há duas funções específicas da Central de segurança:</span><span class="sxs-lookup"><span data-stu-id="01f70-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="01f70-108">**Leitor de segurança**: um usuário que pertence a função toothis tem direitos tooSecurity Centro de exibição.</span><span class="sxs-lookup"><span data-stu-id="01f70-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="01f70-109">usuário Olá pode exibir as recomendações, alertas, uma política de segurança e estados de segurança, mas não é possível fazer alterações.</span><span class="sxs-lookup"><span data-stu-id="01f70-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="01f70-110">**Administrador de segurança**: um usuário que pertence a função toothis Olá mesmo direitos como Olá leitor de segurança e pode também atualizar a política de segurança hello e ignorar alertas e recomendações.</span><span class="sxs-lookup"><span data-stu-id="01f70-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="01f70-111">funções de segurança Hello, leitor de segurança e o administrador de segurança, tem acesso somente na Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="01f70-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="01f70-112">funções de segurança de saudação não tem acesso tooother áreas de serviço do Azure como armazenamento, Web e móveis ou Internet das coisas.</span><span class="sxs-lookup"><span data-stu-id="01f70-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="01f70-113">Funções e ações permitidas</span><span class="sxs-lookup"><span data-stu-id="01f70-113">Roles and allowed actions</span></span>

<span data-ttu-id="01f70-114">Olá tabela a seguir exibe as funções e ações permitidas na Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="01f70-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="01f70-115">Um X indica que a ação de saudação é permitida para essa função.</span><span class="sxs-lookup"><span data-stu-id="01f70-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="01f70-116">Função</span><span class="sxs-lookup"><span data-stu-id="01f70-116">Role</span></span> | <span data-ttu-id="01f70-117">Editar política de segurança</span><span class="sxs-lookup"><span data-stu-id="01f70-117">Edit security policy</span></span> | <span data-ttu-id="01f70-118">Aplicar as recomendações de segurança a um recurso</span><span class="sxs-lookup"><span data-stu-id="01f70-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="01f70-119">Ignorar alertas e recomendações</span><span class="sxs-lookup"><span data-stu-id="01f70-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="01f70-120">Exibir alertas e recomendações</span><span class="sxs-lookup"><span data-stu-id="01f70-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="01f70-121">Proprietário da assinatura</span><span class="sxs-lookup"><span data-stu-id="01f70-121">Subscription Owner</span></span> | <span data-ttu-id="01f70-122">X</span><span class="sxs-lookup"><span data-stu-id="01f70-122">X</span></span> | <span data-ttu-id="01f70-123">X</span><span class="sxs-lookup"><span data-stu-id="01f70-123">X</span></span> | <span data-ttu-id="01f70-124">X</span><span class="sxs-lookup"><span data-stu-id="01f70-124">X</span></span> | <span data-ttu-id="01f70-125">X</span><span class="sxs-lookup"><span data-stu-id="01f70-125">X</span></span> |
| <span data-ttu-id="01f70-126">Colaborador da assinatura</span><span class="sxs-lookup"><span data-stu-id="01f70-126">Subscription Contributor</span></span> | <span data-ttu-id="01f70-127">X</span><span class="sxs-lookup"><span data-stu-id="01f70-127">X</span></span> | <span data-ttu-id="01f70-128">X</span><span class="sxs-lookup"><span data-stu-id="01f70-128">X</span></span> | <span data-ttu-id="01f70-129">X</span><span class="sxs-lookup"><span data-stu-id="01f70-129">X</span></span> | <span data-ttu-id="01f70-130">X</span><span class="sxs-lookup"><span data-stu-id="01f70-130">X</span></span> |
| <span data-ttu-id="01f70-131">Proprietário do Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="01f70-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="01f70-132">X</span><span class="sxs-lookup"><span data-stu-id="01f70-132">X</span></span> | -- | <span data-ttu-id="01f70-133">X</span><span class="sxs-lookup"><span data-stu-id="01f70-133">X</span></span> |
| <span data-ttu-id="01f70-134">Colaborador do Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="01f70-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="01f70-135">X</span><span class="sxs-lookup"><span data-stu-id="01f70-135">X</span></span> | -- | <span data-ttu-id="01f70-136">X</span><span class="sxs-lookup"><span data-stu-id="01f70-136">X</span></span> |
| <span data-ttu-id="01f70-137">Leitor</span><span class="sxs-lookup"><span data-stu-id="01f70-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="01f70-138">X</span><span class="sxs-lookup"><span data-stu-id="01f70-138">X</span></span> |
| <span data-ttu-id="01f70-139">Administrador de segurança</span><span class="sxs-lookup"><span data-stu-id="01f70-139">Security Administrator</span></span> | <span data-ttu-id="01f70-140">X</span><span class="sxs-lookup"><span data-stu-id="01f70-140">X</span></span> | -- | <span data-ttu-id="01f70-141">X</span><span class="sxs-lookup"><span data-stu-id="01f70-141">X</span></span> | <span data-ttu-id="01f70-142">X</span><span class="sxs-lookup"><span data-stu-id="01f70-142">X</span></span> |
| <span data-ttu-id="01f70-143">Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="01f70-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="01f70-144">X</span><span class="sxs-lookup"><span data-stu-id="01f70-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="01f70-145">É recomendável que você atribua Olá função menos permissiva necessários para os usuários toocomplete suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="01f70-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="01f70-146">Por exemplo, atribua Olá leitor função toousers que precisam apenas informações de tooview sobre a integridade da segurança Olá de um recurso, mas não tome uma ação, como aplicar recomendações ou edição de políticas.</span><span class="sxs-lookup"><span data-stu-id="01f70-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="01f70-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01f70-147">Next steps</span></span>
<span data-ttu-id="01f70-148">Este artigo explicou como a Central de segurança usa RBAC tooassign permissões toousers e identificado Olá permitido ações para cada função.</span><span class="sxs-lookup"><span data-stu-id="01f70-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="01f70-149">Agora que você está familiarizado com as atribuições de função hello necessário toomonitor Olá estado de segurança de sua assinatura, editar políticas de segurança e aplicar recomendações, saiba como:</span><span class="sxs-lookup"><span data-stu-id="01f70-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="01f70-150">Configurar políticas de segurança na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="01f70-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="01f70-151">Gerenciando recomendações de segurança na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="01f70-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="01f70-152">Monitorar a integridade da segurança Olá de seus recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="01f70-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="01f70-153">Gerenciar e responder a alertas toosecurity na Central de segurança</span><span class="sxs-lookup"><span data-stu-id="01f70-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- <span data-ttu-id="01f70-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) (Monitorando soluções de parceiros com a Central de Segurança do Azure)</span><span class="sxs-lookup"><span data-stu-id="01f70-154">[Monitor partner security solutions](security-center-partner-solutions.md)</span></span>
