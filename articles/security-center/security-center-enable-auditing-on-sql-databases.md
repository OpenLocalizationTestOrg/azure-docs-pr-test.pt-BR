---
title: "bancos de dados de detecção de ameaças e auditoria aaaEnable no SQL na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * habilitar a detecção de ameaças e auditoria em bancos de dados SQL * *."
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
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="9bec2-103">Habilitar a auditoria e detecção de ameaças em bancos de dados SQL na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="9bec2-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="9bec2-104">A Central de Segurança do Azure recomendará que você ative a auditoria e detecção de ameaças para todos os bancos de dados SQL se isso ainda não tiver sido habilitado.</span><span class="sxs-lookup"><span data-stu-id="9bec2-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="9bec2-105">A auditoria e a detecção de ameaças podem ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar preocupações de negócios ou suspeitas de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="9bec2-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="9bec2-106">Depois que você ativou a auditoria, você pode configurar alertas de segurança de tooreceive de configurações e emails de detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="9bec2-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="9bec2-107">Detecção de ameaças detecta atividades anormais de banco de dados indicando banco dados potencial toohello de ameaças de segurança.</span><span class="sxs-lookup"><span data-stu-id="9bec2-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="9bec2-108">Isso permite que você toodetect e responde a ameaças de toopotential conforme elas ocorrem.</span><span class="sxs-lookup"><span data-stu-id="9bec2-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="9bec2-109">Essa recomendação se aplica a toohello serviço do SQL Azure. não inclui o SQL em execução em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9bec2-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="9bec2-110">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="9bec2-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="9bec2-111">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="9bec2-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="9bec2-112">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="9bec2-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="9bec2-113">Em Olá **recomendações** folha, selecione **detecção de ameaça e habilitar a auditoria em bancos de dados do SQL**.</span><span class="sxs-lookup"><span data-stu-id="9bec2-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="9bec2-114">Isso abre o hello **detecção de ameaça e habilitar a auditoria em bancos de dados SQL** folha.</span><span class="sxs-lookup"><span data-stu-id="9bec2-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Habilitar auditoria em bancos de dados SQL][1]
2. <span data-ttu-id="9bec2-116">Selecione um banco de dados tooenable a auditoria do SQL no.</span><span class="sxs-lookup"><span data-stu-id="9bec2-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="9bec2-117">Isso abre o hello **auditoria e detecção de ameaças** folha.</span><span class="sxs-lookup"><span data-stu-id="9bec2-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="9bec2-118">Em Olá **auditoria e detecção de ameaças** folha, selecione **ON** em **auditoria**.</span><span class="sxs-lookup"><span data-stu-id="9bec2-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Ativar a auditoria e detecção de ameaças][2]
4. <span data-ttu-id="9bec2-120">Siga as etapas de saudação em [detecção de ameaças do banco de dados SQL no portal do Azure de saudação](../sql-database/sql-database-threat-detection-portal.md) tooturn em e configurar a detecção de ameaças e a lista de saudação tooconfigure de endereços de email que receberão alertas de segurança após a detecção de atividades anormais.</span><span class="sxs-lookup"><span data-stu-id="9bec2-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="9bec2-121">Consulte também</span><span class="sxs-lookup"><span data-stu-id="9bec2-121">See also</span></span>
<span data-ttu-id="9bec2-122">Este artigo lhe mostrou como tooimplement Olá Central de segurança recomendação "Habilitar auditoria & ameaça detecção em bancos de dados SQL."</span><span class="sxs-lookup"><span data-stu-id="9bec2-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="9bec2-123">toolearn mais sobre como proteger seu banco de dados SQL, consulte a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="9bec2-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="9bec2-124">Protegendo o Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="9bec2-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="9bec2-125">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9bec2-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="9bec2-126">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="9bec2-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9bec2-127">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bec2-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9bec2-128">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bec2-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="9bec2-129">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="9bec2-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="9bec2-130">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="9bec2-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="9bec2-131">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="9bec2-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="9bec2-132">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – obter notícias mais recentes de segurança do Azure hello e informações.</span><span class="sxs-lookup"><span data-stu-id="9bec2-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
