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
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Habilitar criptografia para conta de armazenamento do Azure na Central de Segurança do Azure
A Central de Segurança do Azure pode aconselhar você a habilitar a Criptografia do Serviço de Armazenamento do Azure para dados em repouso.

Criptografia de serviço de armazenamento (SSE) funciona criptografando dados saudação quando ele está escrito tooAzure armazenamento e descriptografando dados Olá antes da recuperação.  SSE está disponível somente para Olá serviço Blob do Azure e pode ser usado para blobs de bloco, blobs de página e blobs de acréscimo.  mais, consulte toolearn [criptografia do serviço de armazenamento de dados em repouso](../storage/common/storage-service-encryption.md).


> [!Note]
> Depois de habilitar a criptografia, somente dados novos serão criptografados. Todos os blobs existentes em sua conta de armazenamento permanecem descriptografados. tooencrypt de blobs existentes, consulte Olá [perguntas frequentes sobre a criptografia de serviços de armazenamento](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

A Criptografia do Serviço de Armazenamento é compatível apenas com contas de armazenamento do Resource Manager. Atualmente, não há suporte para contas de armazenamento clássicas. saudação de toounderstand clássica e modelos de implantação do Gerenciador de recursos, consulte [modelos de implantação do Azure](../azure-classic-rm.md).

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Este documento não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **recomendações** folha, selecione **habilitar a criptografia para a conta de armazenamento do Azure**.
   ![Habilitar a criptografia para a conta de armazenamento][1]
2. Olá **habilitar a criptografia de armazenamento** folha é aberta. Esta folha lista de contas de armazenamento do Azure Olá em que a criptografia de armazenamento está desabilitada. Neste exemplo, vamos selecionar **storageacct1**.
   ![Habilitar criptografia de armazenamento][2]
3. Olá **criptografia** folha para **storageacct1** abre. Selecione **Habilitado**.
   ![Folha Criptografia][3]
4. Selecione **Salvar**.

Agora, você habilitou a criptografia de armazenamento para **storageacct1**.


## <a name="see-also"></a>Consulte também
Este documento lhe mostrou como tooimplement Olá Central de segurança recomendação "Habilitar criptografia para a conta de armazenamento do Azure". toolearn mais informações sobre criptografia de serviço de armazenamento do Azure, consulte o seguinte hello:

* [Criptografia do Serviço de Armazenamento do Azure para dados em repouso](../storage/common/storage-service-encryption.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) -Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) -Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) -Saiba como alertas de toosecurity toomanage e responder.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) -perguntas frequentes sobre como usar o serviço de saudação de localizar.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
