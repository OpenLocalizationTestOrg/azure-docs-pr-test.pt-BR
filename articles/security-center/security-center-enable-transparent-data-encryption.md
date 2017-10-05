---
title: "Habilitar Transparent Data Encryption na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de Segurança do Azure para **Habilitar Transparent Data Encryption**."
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
ms.openlocfilehash: 2a2963affdbff3710ad08f86c6ed4e6304335559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="fb667-103">Habilitar Transparent Data Encryption na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="fb667-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="fb667-104">A Central de Segurança do Azure recomendará habilitar a TDE (Transparent Data Encryption) em bancos de dados SQL se já não estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="fb667-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="fb667-105">A TDE protege seus dados e ajuda a cumprir os requisitos de conformidade, criptografando seu banco de dados, backups associados e arquivos de log de transações em repouso, sem exigir alterações no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb667-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span></span> <span data-ttu-id="fb667-106">Para saber mais, consulte [Transparent Data Encryption com o Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="fb667-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="fb667-107">Essa recomendação se aplica apenas ao serviço do SQL Azure, não incluindo o SQL em execução em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="fb667-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="fb667-108">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="fb667-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="fb667-109">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="fb667-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="fb667-110">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="fb667-110">Implement the recommendation</span></span>
1. <span data-ttu-id="fb667-111">Na folha **Recomendações**, selecione **Habilitar Transparent Data Encryption**.</span><span class="sxs-lookup"><span data-stu-id="fb667-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="fb667-112">![Habilitar Transparent Data Encryption][1]</span><span class="sxs-lookup"><span data-stu-id="fb667-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="fb667-113">Isso abre a folha **Habilitar Transparent Data Encryption em bancos de dados SQL** .</span><span class="sxs-lookup"><span data-stu-id="fb667-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="fb667-114">Selecione um banco de dados SQL no qual você deseja habilitar a TDE.</span><span class="sxs-lookup"><span data-stu-id="fb667-114">Select a SQL database to enable TDE on.</span></span>
   <span data-ttu-id="fb667-115">![Selecionar o banco de dados SQL no qual habilitar a TDE][2]</span><span class="sxs-lookup"><span data-stu-id="fb667-115">![Select SQL DB to enable TDE on][2]</span></span>
3. <span data-ttu-id="fb667-116">Na folha **Criptografia de dados transparentes**, selecione **ATIVAR** em Criptografia de dados e selecione **Salvar** na faixa de opções superior da folha.</span><span class="sxs-lookup"><span data-stu-id="fb667-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span></span>
   <span data-ttu-id="fb667-117">![Ativar TDE][3]</span><span class="sxs-lookup"><span data-stu-id="fb667-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="fb667-118">Quando a TDE for habilitada no banco de dados SQL selecionado, o **Status da criptografia** será alterado para **Criptografado**.</span><span class="sxs-lookup"><span data-stu-id="fb667-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span></span>    

   ![Status de criptografia][4]

## <a name="see-also"></a><span data-ttu-id="fb667-120">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fb667-120">See also</span></span>
<span data-ttu-id="fb667-121">Este artigo mostrou como implementar a recomendação da Central de Segurança "Habilitar a Transparent Data Encryption".</span><span class="sxs-lookup"><span data-stu-id="fb667-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="fb667-122">Para saber mais sobre a TDE do SQL, consulte o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fb667-122">To learn more about SQL TDE, see the following:</span></span>

* [<span data-ttu-id="fb667-123">Transparent Data Encryption com o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="fb667-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="fb667-124">Introdução ao Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="fb667-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="fb667-125">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fb667-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="fb667-126">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb667-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="fb667-127">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb667-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="fb667-128">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb667-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="fb667-129">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="fb667-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="fb667-130">[Monitoramento de soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="fb667-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="fb667-131">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço de localização.</span><span class="sxs-lookup"><span data-stu-id="fb667-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="fb667-132">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb667-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
