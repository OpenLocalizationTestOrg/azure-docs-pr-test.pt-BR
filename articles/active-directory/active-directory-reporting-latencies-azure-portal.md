---
title: "Latências de relatórios do Azure Active Directory | Microsoft Docs"
description: "Saiba quanto tempo leva para que os eventos de relatório sejam exibidos no seu portal do Azure"
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
ms.openlocfilehash: 93cb0baeab8f13f81257ed1bd32ed08561c54b72
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="0f90d-103">Latências de relatórios do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f90d-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="0f90d-104">Com o [relatório](active-directory-preview-explainer.md) no Azure Active Directory, você obtém todas as informações necessárias para determinar como seu ambiente está se comportando.</span><span class="sxs-lookup"><span data-stu-id="0f90d-104">With [reporting](active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="0f90d-105">A quantidade de tempo que leva para que os dados de relatório sejam exibidos no portal do Azure também é conhecida como latência.</span><span class="sxs-lookup"><span data-stu-id="0f90d-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="0f90d-106">Este tópico lista as informações de latência para todas as categorias de relatórios no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f90d-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="0f90d-107">Relatórios de atividades</span><span class="sxs-lookup"><span data-stu-id="0f90d-107">Activity reports</span></span>

<span data-ttu-id="0f90d-108">Há duas áreas de relatórios de atividade:</span><span class="sxs-lookup"><span data-stu-id="0f90d-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="0f90d-109">**Atividades de entrada** – informações sobre o uso de aplicativos gerenciados e de atividades de entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="0f90d-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="0f90d-110">**Logs de auditoria** - informações de auditoria sobre o gerenciamento de usuários e de grupos, os aplicativos gerenciados e as atividades de diretório</span><span class="sxs-lookup"><span data-stu-id="0f90d-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="0f90d-111">A tabela a seguir lista as informações de latência para relatórios de atividade.</span><span class="sxs-lookup"><span data-stu-id="0f90d-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="0f90d-112">Relatório</span><span class="sxs-lookup"><span data-stu-id="0f90d-112">Report</span></span> | <span data-ttu-id="0f90d-113">Mínimo</span><span class="sxs-lookup"><span data-stu-id="0f90d-113">Minimum</span></span> | <span data-ttu-id="0f90d-114">Média</span><span class="sxs-lookup"><span data-stu-id="0f90d-114">Average</span></span> | <span data-ttu-id="0f90d-115">Máximo</span><span class="sxs-lookup"><span data-stu-id="0f90d-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="0f90d-116">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="0f90d-116">Audit logs</span></span>             | <span data-ttu-id="0f90d-117">30 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-117">30 minutes</span></span>  | <span data-ttu-id="0f90d-118">45 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-118">45 Minutes</span></span> | <span data-ttu-id="0f90d-119">1 hora</span><span class="sxs-lookup"><span data-stu-id="0f90d-119">1 hour</span></span>     |
| <span data-ttu-id="0f90d-120">Entradas</span><span class="sxs-lookup"><span data-stu-id="0f90d-120">Sign-ins</span></span>               | <span data-ttu-id="0f90d-121">15 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-121">15 minutes</span></span>  | <span data-ttu-id="0f90d-122">15 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-122">15 minutes</span></span> | <span data-ttu-id="0f90d-123">2 horas*</span><span class="sxs-lookup"><span data-stu-id="0f90d-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="0f90d-124">Para alguns dados de atividade de entrada provenientes de aplicativos do Office herdados, pode levar até 8 horas para que os dados de relatório sejam exibidos.</span><span class="sxs-lookup"><span data-stu-id="0f90d-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="0f90d-125">Relatórios de segurança</span><span class="sxs-lookup"><span data-stu-id="0f90d-125">Security reports</span></span>

<span data-ttu-id="0f90d-126">Há duas áreas de relatórios de segurança:</span><span class="sxs-lookup"><span data-stu-id="0f90d-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="0f90d-127">**Entradas arriscadas** - uma entrada arriscada é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é o proprietário legítimo de uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="0f90d-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="0f90d-128">**Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="0f90d-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="0f90d-129">A tabela a seguir lista as informações de latência para relatórios de segurança.</span><span class="sxs-lookup"><span data-stu-id="0f90d-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="0f90d-130">Relatório</span><span class="sxs-lookup"><span data-stu-id="0f90d-130">Report</span></span> | <span data-ttu-id="0f90d-131">Mínimo</span><span class="sxs-lookup"><span data-stu-id="0f90d-131">Minimum</span></span> | <span data-ttu-id="0f90d-132">Média</span><span class="sxs-lookup"><span data-stu-id="0f90d-132">Average</span></span> | <span data-ttu-id="0f90d-133">Máximo</span><span class="sxs-lookup"><span data-stu-id="0f90d-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="0f90d-134">Usuários em risco</span><span class="sxs-lookup"><span data-stu-id="0f90d-134">Users at risk</span></span>          | <span data-ttu-id="0f90d-135">5 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-135">5 minutes</span></span>   | <span data-ttu-id="0f90d-136">15 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-136">15 minutes</span></span>  | <span data-ttu-id="0f90d-137">2 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-137">2 hours</span></span>  |
| <span data-ttu-id="0f90d-138">Entradas de risco</span><span class="sxs-lookup"><span data-stu-id="0f90d-138">Risky sign-ins</span></span>         | <span data-ttu-id="0f90d-139">5 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-139">5 minutes</span></span>   | <span data-ttu-id="0f90d-140">15 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-140">15 minutes</span></span>  | <span data-ttu-id="0f90d-141">2 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="0f90d-142">Eventos de risco</span><span class="sxs-lookup"><span data-stu-id="0f90d-142">Risk events</span></span>

<span data-ttu-id="0f90d-143">O Azure Active Directory usa algoritmos de aprendizado de máquina e heurística adaptáveis para detectar ações suspeitas relacionadas às contas do usuário.</span><span class="sxs-lookup"><span data-stu-id="0f90d-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="0f90d-144">Cada ação suspeita detectada é armazenada em um registro chamado evento de risco.</span><span class="sxs-lookup"><span data-stu-id="0f90d-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="0f90d-145">A tabela a seguir lista as informações de latência para eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="0f90d-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="0f90d-146">Relatório</span><span class="sxs-lookup"><span data-stu-id="0f90d-146">Report</span></span> | <span data-ttu-id="0f90d-147">Mínimo</span><span class="sxs-lookup"><span data-stu-id="0f90d-147">Minimum</span></span> | <span data-ttu-id="0f90d-148">Média</span><span class="sxs-lookup"><span data-stu-id="0f90d-148">Average</span></span> | <span data-ttu-id="0f90d-149">Máximo</span><span class="sxs-lookup"><span data-stu-id="0f90d-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="0f90d-150">Entradas de endereços IP anônimos</span><span class="sxs-lookup"><span data-stu-id="0f90d-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="0f90d-151">5 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-151">5 minutes</span></span> |<span data-ttu-id="0f90d-152">15 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-152">15 Minutes</span></span> |<span data-ttu-id="0f90d-153">2 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-153">2 hours</span></span> |
| <span data-ttu-id="0f90d-154">Entradas de locais desconhecidos</span><span class="sxs-lookup"><span data-stu-id="0f90d-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="0f90d-155">5 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-155">5 minutes</span></span> |<span data-ttu-id="0f90d-156">15 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-156">15 Minutes</span></span> |<span data-ttu-id="0f90d-157">2 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-157">2 hours</span></span> |
| <span data-ttu-id="0f90d-158">Usuários com credenciais vazadas</span><span class="sxs-lookup"><span data-stu-id="0f90d-158">Users with leaked credentials</span></span> |<span data-ttu-id="0f90d-159">2 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-159">2 hours</span></span> |<span data-ttu-id="0f90d-160">4 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-160">4 hours</span></span> |<span data-ttu-id="0f90d-161">8 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-161">8 hours</span></span> |
| <span data-ttu-id="0f90d-162">Viagem impossível a locais atípicos</span><span class="sxs-lookup"><span data-stu-id="0f90d-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="0f90d-163">5 minutos</span><span class="sxs-lookup"><span data-stu-id="0f90d-163">5 minutes</span></span> |<span data-ttu-id="0f90d-164">1 hora</span><span class="sxs-lookup"><span data-stu-id="0f90d-164">1 hour</span></span> |<span data-ttu-id="0f90d-165">8 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-165">8 hours</span></span>  |
| <span data-ttu-id="0f90d-166">Entradas de dispositivos infectados</span><span class="sxs-lookup"><span data-stu-id="0f90d-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="0f90d-167">2 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-167">2 hours</span></span> |<span data-ttu-id="0f90d-168">4 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-168">4 hours</span></span> |<span data-ttu-id="0f90d-169">8 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-169">8 hours</span></span>  |
| <span data-ttu-id="0f90d-170">Entradas de endereços IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="0f90d-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="0f90d-171">2 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-171">2 hours</span></span> |<span data-ttu-id="0f90d-172">4 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-172">4 hours</span></span> |<span data-ttu-id="0f90d-173">8 horas</span><span class="sxs-lookup"><span data-stu-id="0f90d-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="0f90d-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f90d-174">Next steps</span></span>

<span data-ttu-id="0f90d-175">Se você quiser saber mais sobre os relatórios de atividade no portal do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="0f90d-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="0f90d-176">Relatórios de atividades de entrada no portal do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f90d-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="0f90d-177">Audit activity reports in the Azure Active Directory portal (Relatórios de atividades de auditoria no portal do Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="0f90d-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="0f90d-178">Se você quiser saber mais sobre os relatórios de segurança no portal do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="0f90d-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="0f90d-179">Relatório de segurança de usuários em risco no portal do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f90d-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="0f90d-180">Relatório de entradas de risco no portal do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f90d-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="0f90d-181">Se você quiser saber mais sobre eventos de risco, consulte [Eventos de risco do Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="0f90d-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
