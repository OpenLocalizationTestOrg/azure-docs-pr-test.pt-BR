---
title: "aaaPrepare Hyper-V hospeda (sem o System Center VMM) para a replicação tooAzure | Microsoft Docs"
description: "Descreve como tooprepare Hyper-V hospeda para tooAzure de replicação usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a>Etapa 6: Preparar hosts Hyper-V para replicação tooAzure

Use instruções Olá tooprepare este artigo toointeract de hosts do Hyper-V com o Azure Site Recovery no local.

Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hosts"></a>Preparar os hosts

- Verifique se os hosts Hyper-V de saudação atendem Olá [pré-requisitos](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).
- Certifique-se de que os hosts de saudação podem acessar Olá necessário URLs:

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.
- Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).
- Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).

Durante a implantação da recuperação de Site, você deve adicionar hosts Hyper-V que contêm máquinas virtuais que você deseja tooreplicate tooa Hyper-V site. Olá provedor de recuperação de Site e o agente de serviços de recuperação são instalados em cada host. site Olá Hyper-V é registrado no cofre de serviços de recuperação de saudação.

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 7: criar um cofre](hyper-v-site-walkthrough-create-vault.md)

