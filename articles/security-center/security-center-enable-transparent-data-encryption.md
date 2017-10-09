---
title: "aaaEnable criptografia transparente de dados na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * habilitar Transparent Data Encryption * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="4c1eb-103">Habilitar Transparent Data Encryption na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="4c1eb-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="4c1eb-104">A Central de Segurança do Azure recomendará habilitar a TDE (Transparent Data Encryption) em bancos de dados SQL se já não estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="4c1eb-105">A TDE protege seus dados e ajuda a atender aos requisitos de conformidade por meio da criptografia de banco de dados, backups associados e arquivos de log de transações em descanso, sem a necessidade de alterações tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="4c1eb-106">toolearn mais ver [Transparent Data Encryption com o banco de dados do Azure SQL](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="4c1eb-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="4c1eb-107">Essa recomendação se aplica a toohello serviço do SQL Azure. não inclui o SQL em execução em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="4c1eb-108">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="4c1eb-109">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="4c1eb-110">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="4c1eb-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="4c1eb-111">Em Olá **recomendações** folha, selecione **habilitar a criptografia transparente de dados**.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="4c1eb-112">![Habilitar Transparent Data Encryption][1]</span><span class="sxs-lookup"><span data-stu-id="4c1eb-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="4c1eb-113">Isso abre o hello **habilitar a criptografia transparente de dados em bancos de dados SQL** folha.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="4c1eb-114">Selecione um banco de dados SQL tooenable TDE.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="4c1eb-115">![Selecione o banco de dados SQL tooenable TDE no][2]</span><span class="sxs-lookup"><span data-stu-id="4c1eb-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="4c1eb-116">Em Olá **criptografia transparente de dados** folha, selecione **ON** em criptografia de dados e selecione **salvar** na faixa de opções superior da folha de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="4c1eb-117">![Ativar TDE][3]</span><span class="sxs-lookup"><span data-stu-id="4c1eb-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="4c1eb-118">Quando a TDE está habilitada em Olá selecionados banco de dados SQL, hello **status de criptografia** alterará muito**criptografado**.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![Status de criptografia][4]

## <a name="see-also"></a><span data-ttu-id="4c1eb-120">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4c1eb-120">See also</span></span>
<span data-ttu-id="4c1eb-121">Este artigo lhe mostrou como tooimplement Olá recomendação da Central de segurança "Habilitar criptografia transparente de dados".</span><span class="sxs-lookup"><span data-stu-id="4c1eb-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="4c1eb-122">toolearn mais sobre o SQL TDE, consulte a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="4c1eb-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="4c1eb-123">Transparent Data Encryption com o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="4c1eb-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="4c1eb-124">Introdução ao Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="4c1eb-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="4c1eb-125">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4c1eb-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="4c1eb-126">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4c1eb-127">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4c1eb-128">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="4c1eb-129">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="4c1eb-130">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="4c1eb-131">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="4c1eb-132">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – obter notícias mais recentes de segurança do Azure hello e informações.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
