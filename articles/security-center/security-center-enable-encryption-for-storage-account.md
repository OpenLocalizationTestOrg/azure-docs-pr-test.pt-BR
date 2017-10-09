---
title: "criptografia aaaEnable conta de armazenamento no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendações da Central de segurança do Azure * * habilitar a criptografia para o Azure Storage conta * *."
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
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="3c2b4-103">Habilitar criptografia para conta de armazenamento do Azure na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="3c2b4-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="3c2b4-104">A Central de Segurança do Azure pode aconselhar você a habilitar a Criptografia do Serviço de Armazenamento do Azure para dados em repouso.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="3c2b4-105">Criptografia de serviço de armazenamento (SSE) funciona criptografando dados saudação quando ele está escrito tooAzure armazenamento e descriptografando dados Olá antes da recuperação.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="3c2b4-106">SSE está disponível somente para Olá serviço Blob do Azure e pode ser usado para blobs de bloco, blobs de página e blobs de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="3c2b4-107">mais, consulte toolearn [criptografia do serviço de armazenamento de dados em repouso](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="3c2b4-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="3c2b4-108">Depois de habilitar a criptografia, somente dados novos serão criptografados.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="3c2b4-109">Todos os blobs existentes em sua conta de armazenamento permanecem descriptografados.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="3c2b4-110">tooencrypt de blobs existentes, consulte Olá [perguntas frequentes sobre a criptografia de serviços de armazenamento](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="3c2b4-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="3c2b4-111">A Criptografia do Serviço de Armazenamento é compatível apenas com contas de armazenamento do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="3c2b4-112">Atualmente, não há suporte para contas de armazenamento clássicas.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="3c2b4-113">saudação de toounderstand clássica e modelos de implantação do Gerenciador de recursos, consulte [modelos de implantação do Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="3c2b4-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3c2b4-114">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="3c2b4-115">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="3c2b4-116">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="3c2b4-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="3c2b4-117">Em Olá **recomendações** folha, selecione **habilitar a criptografia para a conta de armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="3c2b4-118">![Habilitar a criptografia para a conta de armazenamento][1]</span><span class="sxs-lookup"><span data-stu-id="3c2b4-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="3c2b4-119">Olá **habilitar a criptografia de armazenamento** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="3c2b4-120">Esta folha lista de contas de armazenamento do Azure Olá em que a criptografia de armazenamento está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="3c2b4-121">Neste exemplo, vamos selecionar **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="3c2b4-122">![Habilitar criptografia de armazenamento][2]</span><span class="sxs-lookup"><span data-stu-id="3c2b4-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="3c2b4-123">Olá **criptografia** folha para **storageacct1** abre.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="3c2b4-124">Selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-124">Select **Enabled**.</span></span>
   <span data-ttu-id="3c2b4-125">![Folha Criptografia][3]</span><span class="sxs-lookup"><span data-stu-id="3c2b4-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="3c2b4-126">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-126">Select **Save**.</span></span>

<span data-ttu-id="3c2b4-127">Agora, você habilitou a criptografia de armazenamento para **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="3c2b4-128">Consulte também</span><span class="sxs-lookup"><span data-stu-id="3c2b4-128">See also</span></span>
<span data-ttu-id="3c2b4-129">Este documento lhe mostrou como tooimplement Olá Central de segurança recomendação "Habilitar criptografia para a conta de armazenamento do Azure".</span><span class="sxs-lookup"><span data-stu-id="3c2b4-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="3c2b4-130">toolearn mais informações sobre criptografia de serviço de armazenamento do Azure, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="3c2b4-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="3c2b4-131">Criptografia do Serviço de Armazenamento do Azure para dados em repouso</span><span class="sxs-lookup"><span data-stu-id="3c2b4-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="3c2b4-132">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="3c2b4-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="3c2b4-133">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) -Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="3c2b4-134">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) -Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="3c2b4-135">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) -Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="3c2b4-136">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="3c2b4-137">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) -perguntas frequentes sobre como usar o serviço de saudação de localizar.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="3c2b4-138">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2b4-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
