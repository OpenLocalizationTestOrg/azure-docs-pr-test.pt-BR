---
title: "aaaPrepare System Center VMM para tooAzure de replicação do Hyper-V | Microsoft Docs"
description: "Descreve como servidor do System Center VMM tooprepare para tooAzure de replicação do Hyper-V, usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>Etapa 6: Preparar os servidores do VMM e hosts Hyper-V para tooAzure de replicação do Hyper-V

Depois de configurar o [componentes do Azure](vmm-to-azure-walkthrough-prepare-azure.md) para implantação de hello, use instruções Olá nesse toointeract de hosts do Hyper-V e servidores do artigo tooprepare locais do VMM com o Azure Site Recovery.

Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-vmm-servers"></a>Preparar servidores VMM

- É necessário pelo menos um servidor do VMM que atendem aos requisitos de suporte de saudação para replicação de recuperação de Site (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- Certifique-se que você preparou o servidor do VMM Olá para [mapeamento de rede](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- Verifique se o que servidor VMM Olá pode acessar essas URLs

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.
- Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).
- Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).

Durante a implantação da recuperação de Site, você baixar Olá provedor de recuperação de Site e instale-o em cada servidor do VMM. servidor do VMM Hello está registrado no cofre de serviços de recuperação de saudação.




## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 7: criar um cofre](vmm-to-azure-walkthrough-create-vault.md)

