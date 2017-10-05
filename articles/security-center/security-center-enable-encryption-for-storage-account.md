---
title: "Habilitar criptografia para conta de armazenamento na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar as recomendações da Central de Segurança do Azure **Habilitar criptografia para Conta de Armazenamento do Azure**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: b7b2e8a12cbab68da9c8fcc348e8e3c543607007
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="e6c46-103">Habilitar criptografia para conta de armazenamento do Azure na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="e6c46-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="e6c46-104">A Central de Segurança do Azure pode aconselhar você a habilitar a Criptografia do Serviço de Armazenamento do Azure para dados em repouso.</span><span class="sxs-lookup"><span data-stu-id="e6c46-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="e6c46-105">A SSE (Criptografia do Serviço de Armazenamento) funciona criptografando os dados quando eles são gravados no armazenamento do Azure e descriptografando-os antes da recuperação.</span><span class="sxs-lookup"><span data-stu-id="e6c46-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span></span>  <span data-ttu-id="e6c46-106">Atualmente, a SSE está disponível somente para o serviço Blob do Azure e pode ser usada para blobs de blocos, blobs de páginas e blobs de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="e6c46-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="e6c46-107">Para saber mais, confira [Criptografia do Serviço de Armazenamento para dados em repouso](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="e6c46-107">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="e6c46-108">Depois de habilitar a criptografia, somente dados novos serão criptografados.</span><span class="sxs-lookup"><span data-stu-id="e6c46-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="e6c46-109">Todos os blobs existentes em sua conta de armazenamento permanecem descriptografados.</span><span class="sxs-lookup"><span data-stu-id="e6c46-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="e6c46-110">Para criptografar os blobs existentes, confira as [perguntas frequentes sobre a Criptografia do Serviço de Armazenamento](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="e6c46-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="e6c46-111">A Criptografia do Serviço de Armazenamento é compatível apenas com contas de armazenamento do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6c46-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="e6c46-112">Atualmente, não há suporte para contas de armazenamento clássicas.</span><span class="sxs-lookup"><span data-stu-id="e6c46-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="e6c46-113">Para entender os modelos de implantação clássicos e do Resource Manager, confira [Modelos de implantação do Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="e6c46-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e6c46-114">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e6c46-114">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="e6c46-115">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="e6c46-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="e6c46-116">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="e6c46-116">Implement the recommendation</span></span>
1. <span data-ttu-id="e6c46-117">Na folha **Recomendações**, escolha **Habilitar criptografia para Conta de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="e6c46-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="e6c46-118">![Habilitar a criptografia para a conta de armazenamento][1]</span><span class="sxs-lookup"><span data-stu-id="e6c46-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="e6c46-119">A folha **Habilitar criptografia de armazenamento** é aberta.</span><span class="sxs-lookup"><span data-stu-id="e6c46-119">The **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="e6c46-120">Essa folha lista as contas de armazenamento do Azure em que a criptografia de armazenamento está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="e6c46-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="e6c46-121">Neste exemplo, vamos selecionar **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="e6c46-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="e6c46-122">![Habilitar criptografia de armazenamento][2]</span><span class="sxs-lookup"><span data-stu-id="e6c46-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="e6c46-123">A folha **Criptografia** de **storageacct1** é aberta.</span><span class="sxs-lookup"><span data-stu-id="e6c46-123">The **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="e6c46-124">Selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="e6c46-124">Select **Enabled**.</span></span>
   <span data-ttu-id="e6c46-125">![Folha Criptografia][3]</span><span class="sxs-lookup"><span data-stu-id="e6c46-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="e6c46-126">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e6c46-126">Select **Save**.</span></span>

<span data-ttu-id="e6c46-127">Agora, você habilitou a criptografia de armazenamento para **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="e6c46-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="e6c46-128">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e6c46-128">See also</span></span>
<span data-ttu-id="e6c46-129">Este documento mostrou como implementar a recomendação da Central de Segurança do Azure "Habilitar criptografia para Conta de Armazenamento do Azure".</span><span class="sxs-lookup"><span data-stu-id="e6c46-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="e6c46-130">Para saber mais sobre a Criptografia do Serviço de Armazenamento do Azure, confira:</span><span class="sxs-lookup"><span data-stu-id="e6c46-130">To learn more about Azure Storage Service Encryption, see the following:</span></span>

* [<span data-ttu-id="e6c46-131">Criptografia do Serviço de Armazenamento do Azure para dados em repouso</span><span class="sxs-lookup"><span data-stu-id="e6c46-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="e6c46-132">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e6c46-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="e6c46-133">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md): saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6c46-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e6c46-134">[Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md): saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6c46-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="e6c46-135">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md): aprenda a gerenciar e responder aos alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="e6c46-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="e6c46-136">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6c46-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e6c46-137">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md): encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="e6c46-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="e6c46-138">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6c46-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
