---
title: "Habilitar a auditoria e detecção de ameaças em servidores SQL na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de segurança do Azure * * detecção de ameaça e habilitar a auditoria em servidores SQL * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 660b537aef8d175a478ff93d60b8391d55fc92ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="ecaa6-103">Habilitar a auditoria e detecção de ameaças em servidores SQL na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="ecaa6-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="ecaa6-104">A Central de Segurança do Azure recomendará que você ative a auditoria e detecção de ameaças para todos os bancos de dados em seus servidores SQL do Azure se isso não tiver sido habilitado.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="ecaa6-105">A auditoria e a detecção de ameaças podem ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar preocupações de negócios ou suspeitas de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="ecaa6-106">Depois de ativar a auditoria, você poderá definir as configurações de Detecção de Ameaças e emails para receber alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="ecaa6-107">A Detecção de Ameaças detecta as atividades anormais do banco de dados que indicam possíveis ameaças de segurança ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="ecaa6-108">Isso permite que você detecte e reaja a possíveis ameaças à medida que elas ocorrem.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="ecaa6-109">Essa recomendação se aplica apenas ao serviço do SQL do Azure. Ela não inclui o servidor SQL em execução nas máquinas virtuais nos Serviços de Infraestrutura do Azure (Azure IaaS).</span><span class="sxs-lookup"><span data-stu-id="ecaa6-109">This recommendation applies to the Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="ecaa6-110">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="ecaa6-111">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="ecaa6-112">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="ecaa6-112">Implement the recommendation</span></span>
1. <span data-ttu-id="ecaa6-113">Na folha **Recomendações**, selecione **Habilitar Auditoria e Detecção de ameaças em servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="ecaa6-114">Isso abre a folha **Habilitar Auditoria e Detecção de ameaças em servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-114">This opens the **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Habilitar auditoria em servidores SQL][1]
2. <span data-ttu-id="ecaa6-116">Selecione um SQL Server no qual habilitar a auditoria e detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-116">Select a SQL server to enable auditing and threat detection on.</span></span> <span data-ttu-id="ecaa6-117">Isso abre a folha **Auditoria e Detecção de Ameaças**.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="ecaa6-118">Na folha **Auditoria e Detecção de Ameaças**, selecione **ATIVAR** em **Auditoria**.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Ativar configurações de auditoria][2]
4. <span data-ttu-id="ecaa6-120">Siga as etapas em [Auditoria do Banco de Dados SQL no Portal do Azure](../sql-database/sql-database-auditing-portal.md) para configurar o armazenamento em que os logs de auditoria serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-120">Follow the steps in [SQL database auditing in the Azure portal](../sql-database/sql-database-auditing-portal.md) to configure storage where your audit logs will be stored.</span></span> <span data-ttu-id="ecaa6-121">A conta de armazenamento da assinatura para coleta de dados é a padrão.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-121">The subscription's storage account for data collection is the default storage account.</span></span>
5. <span data-ttu-id="ecaa6-122">Siga as etapas em [Introdução à Detecção de Ameaças do Banco de Dados SQL](../sql-database/sql-database-threat-detection.md) para ativar e configurar a Detecção de Ameaças e configurar a lista de emails que receberá alertas de segurança após a detecção de atividades anormais.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-122">Follow the steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="ecaa6-123">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ecaa6-123">See also</span></span>
<span data-ttu-id="ecaa6-124">Este artigo mostrou como implementar a recomendação "Habilitar auditoria e detecção de ameaças em servidores SQL" da Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-124">This article showed you how to implement the Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="ecaa6-125">Para saber mais sobre como proteger seu Banco de Dados SQL, consulte:</span><span class="sxs-lookup"><span data-stu-id="ecaa6-125">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="ecaa6-126">Protegendo o Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="ecaa6-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="ecaa6-127">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ecaa6-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="ecaa6-128">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ecaa6-129">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ecaa6-130">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ecaa6-131">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ecaa6-132">[Monitoramento de soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="ecaa6-133">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço de localização.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ecaa6-134">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecaa6-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
