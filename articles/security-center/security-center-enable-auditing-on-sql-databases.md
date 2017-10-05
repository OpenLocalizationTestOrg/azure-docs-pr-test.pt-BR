---
title: "Habilitar a auditoria e detecção de ameaças em bancos de dados SQL na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de segurança do Azure * * habilitar a detecção de ameaças e auditoria em bancos de dados SQL * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 8f4febdaa4497fee0dc690b59cd6eaa415c5e5cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="14c82-103">Habilitar a auditoria e detecção de ameaças em bancos de dados SQL na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="14c82-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="14c82-104">A Central de Segurança do Azure recomendará que você ative a auditoria e detecção de ameaças para todos os bancos de dados SQL se isso ainda não tiver sido habilitado.</span><span class="sxs-lookup"><span data-stu-id="14c82-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="14c82-105">A auditoria e a detecção de ameaças podem ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar preocupações de negócios ou suspeitas de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="14c82-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="14c82-106">Depois de ativar a auditoria, você poderá definir as configurações de Detecção de Ameaças e emails para receber alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="14c82-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="14c82-107">A Detecção de Ameaças detecta as atividades anormais do banco de dados que indicam possíveis ameaças de segurança ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="14c82-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="14c82-108">Isso permite que você detecte e reaja a possíveis ameaças à medida que elas ocorrem.</span><span class="sxs-lookup"><span data-stu-id="14c82-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="14c82-109">Essa recomendação se aplica apenas ao serviço do SQL Azure, não incluindo o SQL em execução nas suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="14c82-109">This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="14c82-110">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="14c82-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="14c82-111">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="14c82-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="14c82-112">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="14c82-112">Implement the recommendation</span></span>
1. <span data-ttu-id="14c82-113">Na folha **Recomendações**, selecione **Habilitar Auditoria e Detecção de ameaças em bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="14c82-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="14c82-114">Isso abre a folha **Habilitar Auditoria e Detecção de ameaças em bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="14c82-114">This opens the **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Habilitar auditoria em bancos de dados SQL][1]
2. <span data-ttu-id="14c82-116">Selecione um Banco de Dados SQL no qual você deseja habilitar a auditoria.</span><span class="sxs-lookup"><span data-stu-id="14c82-116">Select a SQL database to enable auditing on.</span></span> <span data-ttu-id="14c82-117">Isso abre a folha **Auditoria e Detecção de Ameaças**.</span><span class="sxs-lookup"><span data-stu-id="14c82-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="14c82-118">Na folha **Auditoria e Detecção de Ameaças**, selecione **ATIVAR** em **Auditoria**.</span><span class="sxs-lookup"><span data-stu-id="14c82-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Ativar a auditoria e detecção de ameaças][2]
4. <span data-ttu-id="14c82-120">Execute as etapas em [Detecção de ameaças do Banco de Dados SQL no Portal do Azure](../sql-database/sql-database-threat-detection-portal.md) para ativar e configurar a detecção de ameaças e configurar a lista de emails que receberá alertas de segurança após a detecção de atividades anormais.</span><span class="sxs-lookup"><span data-stu-id="14c82-120">Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="14c82-121">Consulte também</span><span class="sxs-lookup"><span data-stu-id="14c82-121">See also</span></span>
<span data-ttu-id="14c82-122">Este artigo mostrou como implementar a recomendação "Habilitar auditoria e detecção de ameaças em bancos de dados SQL" da Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="14c82-122">This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="14c82-123">Para saber mais sobre como proteger seu Banco de Dados SQL, consulte:</span><span class="sxs-lookup"><span data-stu-id="14c82-123">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="14c82-124">Protegendo o Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="14c82-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="14c82-125">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="14c82-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="14c82-126">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="14c82-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="14c82-127">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="14c82-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="14c82-128">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="14c82-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="14c82-129">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="14c82-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="14c82-130">[Monitoramento de soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="14c82-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="14c82-131">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço de localização.</span><span class="sxs-lookup"><span data-stu-id="14c82-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="14c82-132">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="14c82-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
