---
title: Preparar o destino (VMware tooAzure) | Microsoft Docs
description: "Este artigo descreve como tooprepare toostart seu ambiente do Azure que replicando tooAzure de máquinas virtuais VMware."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>Preparar o destino (tooAzure VMware)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [TooAzure físico](./site-recovery-prepare-target-physical-to-azure.md)

Este artigo descreve como tooprepare toostart seu ambiente do Azure que replicando tooAzure de máquinas virtuais VMware.

## <a name="prerequisites"></a>Pré-requisitos

artigo de saudação pressupõe seguinte hello:
- Você criou um cofre de serviços de recuperação tooprotect máquinas virtuais VMware. Você pode criar um cofre de serviços de recuperação de saudação [portal do Azure](http://portal.azure.com "portal do Azure").
- Você tem [configurar seu ambiente local](./site-recovery-set-up-vmware-to-azure.md) tooAzure de máquinas virtuais VMware tooreplicate.

## <a name="prepare-target"></a>Preparar o destino

Depois de concluir a saudação **objetivo de proteção etapa 1: selecione** e **etapa 2: preparar fonte**, você será direcionado muito**etapa 3: destino**

![Preparar o destino](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. **Assinatura:** de saudação menu suspenso, selecione Olá assinatura que você deseja tooreplicate máquinas virtuais.
2. **Modelo de implantação:** modelo de implantação de saudação Select (clássico ou Gerenciador de recursos)

Com base em Olá escolhida o modelo de implantação, uma validação é executada tooensure que você tem pelo menos uma conta de armazenamento e rede virtual em Olá tooreplicate de assinatura de destino e o failover sua máquina virtual para.

Depois que as validações de saudação concluída com êxito, clique em toogo Okey toohello próxima etapa.

Se você não tiver uma conta de armazenamento compatível com o Gerenciador de recursos ou a rede virtual, ou gostaria tooadd mais, você pode fazer isso clicando Olá **+ conta de armazenamento** ou **+ rede** botões na parte superior de saudação do hello folha.

## <a name="next-steps"></a>Próximas etapas
[Definir configurações de replicação](./site-recovery-setup-replication-settings-vmware.md).
