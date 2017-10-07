---
title: "latências de relatório de Active Directory aaaAzure | Microsoft Docs"
description: "Saiba mais sobre a quantidade de saudação de tempo que leva para relatar eventos tooshow backup no portal do Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="e0631-103">Latências de relatórios do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0631-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="e0631-104">Com [reporting](active-directory-preview-explainer.md) em Olá Active Directory do Azure, você obter todas as informações de saudação necessário toodetermine como seu ambiente está fazendo.</span><span class="sxs-lookup"><span data-stu-id="e0631-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="e0631-105">quantidade de saudação de tempo que leva para tooshow de dados para cima em Olá portal do Azure também é conhecido como latência de relatório.</span><span class="sxs-lookup"><span data-stu-id="e0631-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="e0631-106">Este tópico lista informações de latência de saudação para Olá todas as categorias de relatório no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0631-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="e0631-107">Relatórios de atividades</span><span class="sxs-lookup"><span data-stu-id="e0631-107">Activity reports</span></span>

<span data-ttu-id="e0631-108">Há duas áreas de relatórios de atividade:</span><span class="sxs-lookup"><span data-stu-id="e0631-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="e0631-109">**Atividades de entrada** – informações sobre o uso de saudação de aplicativos gerenciados e atividades de entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="e0631-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="e0631-110">**Logs de auditoria** - informações de auditoria sobre o gerenciamento de usuários e de grupos, os aplicativos gerenciados e as atividades de diretório</span><span class="sxs-lookup"><span data-stu-id="e0631-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="e0631-111">Olá a tabela a seguir lista as informações de latência de saudação para relatórios de atividade.</span><span class="sxs-lookup"><span data-stu-id="e0631-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="e0631-112">Relatório</span><span class="sxs-lookup"><span data-stu-id="e0631-112">Report</span></span> | <span data-ttu-id="e0631-113">Mínimo</span><span class="sxs-lookup"><span data-stu-id="e0631-113">Minimum</span></span> | <span data-ttu-id="e0631-114">Média</span><span class="sxs-lookup"><span data-stu-id="e0631-114">Average</span></span> | <span data-ttu-id="e0631-115">Máximo</span><span class="sxs-lookup"><span data-stu-id="e0631-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="e0631-116">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="e0631-116">Audit logs</span></span>             | <span data-ttu-id="e0631-117">30 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-117">30 minutes</span></span>  | <span data-ttu-id="e0631-118">45 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-118">45 Minutes</span></span> | <span data-ttu-id="e0631-119">1 hora</span><span class="sxs-lookup"><span data-stu-id="e0631-119">1 hour</span></span>     |
| <span data-ttu-id="e0631-120">Entradas</span><span class="sxs-lookup"><span data-stu-id="e0631-120">Sign-ins</span></span>               | <span data-ttu-id="e0631-121">15 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-121">15 minutes</span></span>  | <span data-ttu-id="e0631-122">15 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-122">15 minutes</span></span> | <span data-ttu-id="e0631-123">2 horas*</span><span class="sxs-lookup"><span data-stu-id="e0631-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="e0631-124">Para alguns dados de atividade de entradas provenientes de aplicativos do office herdado, pode levar horas too8 Olá comunicando tooshow de dados.</span><span class="sxs-lookup"><span data-stu-id="e0631-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="e0631-125">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="e0631-125">Security reports</span></span>

<span data-ttu-id="e0631-126">Há duas áreas de relatórios de segurança:</span><span class="sxs-lookup"><span data-stu-id="e0631-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="e0631-127">**Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="e0631-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="e0631-128">**Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="e0631-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="e0631-129">Olá a tabela a seguir lista as informações de latência de saudação para relatórios de segurança.</span><span class="sxs-lookup"><span data-stu-id="e0631-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="e0631-130">Relatório</span><span class="sxs-lookup"><span data-stu-id="e0631-130">Report</span></span> | <span data-ttu-id="e0631-131">Mínimo</span><span class="sxs-lookup"><span data-stu-id="e0631-131">Minimum</span></span> | <span data-ttu-id="e0631-132">Média</span><span class="sxs-lookup"><span data-stu-id="e0631-132">Average</span></span> | <span data-ttu-id="e0631-133">Máximo</span><span class="sxs-lookup"><span data-stu-id="e0631-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="e0631-134">Usuários em risco</span><span class="sxs-lookup"><span data-stu-id="e0631-134">Users at risk</span></span>          | <span data-ttu-id="e0631-135">5 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-135">5 minutes</span></span>   | <span data-ttu-id="e0631-136">15 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-136">15 minutes</span></span>  | <span data-ttu-id="e0631-137">2 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-137">2 hours</span></span>  |
| <span data-ttu-id="e0631-138">Entradas de risco</span><span class="sxs-lookup"><span data-stu-id="e0631-138">Risky sign-ins</span></span>         | <span data-ttu-id="e0631-139">5 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-139">5 minutes</span></span>   | <span data-ttu-id="e0631-140">15 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-140">15 minutes</span></span>  | <span data-ttu-id="e0631-141">2 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="e0631-142">Eventos de risco</span><span class="sxs-lookup"><span data-stu-id="e0631-142">Risk events</span></span>

<span data-ttu-id="e0631-143">Active Directory do Azure usa algoritmos e heurística toodetect suspeitas ações relacionadas tooyour contas de usuário de aprendizado de máquina adaptável.</span><span class="sxs-lookup"><span data-stu-id="e0631-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="e0631-144">Cada ação suspeita detectada é armazenada em um registro chamado evento de risco.</span><span class="sxs-lookup"><span data-stu-id="e0631-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="e0631-145">Olá a tabela a seguir lista as informações de latência de saudação para eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="e0631-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="e0631-146">Relatório</span><span class="sxs-lookup"><span data-stu-id="e0631-146">Report</span></span> | <span data-ttu-id="e0631-147">Mínimo</span><span class="sxs-lookup"><span data-stu-id="e0631-147">Minimum</span></span> | <span data-ttu-id="e0631-148">Média</span><span class="sxs-lookup"><span data-stu-id="e0631-148">Average</span></span> | <span data-ttu-id="e0631-149">Máximo</span><span class="sxs-lookup"><span data-stu-id="e0631-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="e0631-150">Entradas de endereços IP anônimos</span><span class="sxs-lookup"><span data-stu-id="e0631-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="e0631-151">5 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-151">5 minutes</span></span> |<span data-ttu-id="e0631-152">15 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-152">15 Minutes</span></span> |<span data-ttu-id="e0631-153">2 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-153">2 hours</span></span> |
| <span data-ttu-id="e0631-154">Entradas de locais desconhecidos</span><span class="sxs-lookup"><span data-stu-id="e0631-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="e0631-155">5 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-155">5 minutes</span></span> |<span data-ttu-id="e0631-156">15 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-156">15 Minutes</span></span> |<span data-ttu-id="e0631-157">2 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-157">2 hours</span></span> |
| <span data-ttu-id="e0631-158">Usuários com credenciais vazadas</span><span class="sxs-lookup"><span data-stu-id="e0631-158">Users with leaked credentials</span></span> |<span data-ttu-id="e0631-159">2 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-159">2 hours</span></span> |<span data-ttu-id="e0631-160">4 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-160">4 hours</span></span> |<span data-ttu-id="e0631-161">8 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-161">8 hours</span></span> |
| <span data-ttu-id="e0631-162">Viagem impossível tooatypical locais</span><span class="sxs-lookup"><span data-stu-id="e0631-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="e0631-163">5 minutos</span><span class="sxs-lookup"><span data-stu-id="e0631-163">5 minutes</span></span> |<span data-ttu-id="e0631-164">1 hora</span><span class="sxs-lookup"><span data-stu-id="e0631-164">1 hour</span></span> |<span data-ttu-id="e0631-165">8 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-165">8 hours</span></span>  |
| <span data-ttu-id="e0631-166">Entradas de dispositivos infectados</span><span class="sxs-lookup"><span data-stu-id="e0631-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="e0631-167">2 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-167">2 hours</span></span> |<span data-ttu-id="e0631-168">4 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-168">4 hours</span></span> |<span data-ttu-id="e0631-169">8 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-169">8 hours</span></span>  |
| <span data-ttu-id="e0631-170">Entradas de endereços IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="e0631-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="e0631-171">2 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-171">2 hours</span></span> |<span data-ttu-id="e0631-172">4 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-172">4 hours</span></span> |<span data-ttu-id="e0631-173">8 horas</span><span class="sxs-lookup"><span data-stu-id="e0631-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="e0631-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0631-174">Next steps</span></span>

<span data-ttu-id="e0631-175">Se você quiser tooknow mais sobre relatórios de atividades de Olá Olá portal do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="e0631-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="e0631-176">Relatórios de atividade de entrada no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="e0631-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="e0631-177">Relatórios de atividade no portal do Azure Active Directory Olá de auditoria</span><span class="sxs-lookup"><span data-stu-id="e0631-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="e0631-178">Se você quiser tooknow mais sobre relatórios de segurança de Olá Olá portal do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="e0631-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="e0631-179">Usuários no relatório de riscos de segurança no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="e0631-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="e0631-180">Relatório de entradas arriscados no portal do Azure Active Directory Olá</span><span class="sxs-lookup"><span data-stu-id="e0631-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="e0631-181">Se você quiser tooknow mais informações sobre eventos de risco, consulte [eventos de risco do Active Directory do Azure](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="e0631-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
