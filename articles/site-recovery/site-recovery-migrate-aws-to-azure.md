---
title: aaaMigrate VMs do AWS tooAzure | Microsoft Docs
description: "Este artigo descreve como toomigrate virtual máquinas em execução no tooAzure serviços AWS (Amazon Web) usando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>Migrar máquinas virtuais em tooAzure AWS Amazon Web Services () com o Azure Site Recovery

Este artigo descreve como toomigrate Windows AWS instâncias de máquinas virtuais de tooAzure com hello [do Azure Site Recovery](site-recovery-overview.md) serviço.

A migração é efetivamente um failover do AWS tooAzure. Não é possível failback máquinas tooAWS e não há nenhuma replicação em andamento. Este artigo descreve etapas Olá para migração em Olá portal do Azure e são baseados em instruções Olá para [replicar uma máquina física tooAzure](site-recovery-vmware-to-azure.md).

Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

Recuperação de site pode ser usado toomigrate EC2 instâncias executando qualquer um dos Olá sistemas operacionais a seguir:

- Windows (somente 64 bits)
    - Windows Server 2008 R2 SP1+ (drivers Citrix PV ou somente drivers AWS PV. **Não há suporte para instâncias executando drivers RedHat PV**) Windows Server 2012 Windows Server 2012 R2
- Linux (somente 64 bits)
    - Red Hat Enterprise Linux 6.7 (apenas instâncias de HVM virtualizadas)

## <a name="prerequisites"></a>Pré-requisitos

Aqui está o que você precisa para essa implantação:

* **Servidor de configuração**: uma VM de EC2 Amazon executando o Windows Server 2012 R2 é implantado como servidor de configuração de saudação. Por padrão, hello outros componentes do Azure Site Recovery (servidor de processo e servidor de destino mestre) são instalados quando você implanta o servidor de configuração de saudação. Este artigo descreve etapas Olá para migração em Olá portal do Azure e são baseados em instruções Olá para [Saiba mais](site-recovery-components.md)

* **Instâncias de EC2**: Olá Amazon EC2 instâncias de máquinas virtuais que você deseja toomigrate.

## <a name="deployment-steps"></a>Etapas de implantação.

1. Crie um cofre dos Serviços de Recuperação.
2. saudação de grupo de segurança de suas instâncias de EC2 deve ter regras configuradas tooallow comunicação entre Olá EC2 a instância que você toomigrate e instância de saudação em que planeje Olá toodeploy servidor de configuração.

3. Em Olá mesmo Amazon Virtual nuvem privada que suas instâncias de EC2, implantar um servidor de configuração de ASR. Consulte Olá VMware / físicos tooAzure pré-requisitos para requisitos de implantação de servidor de configuração.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Depois que o servidor de configuração é implantado em AWS e registrado com o Cofre de serviços de recuperação, você deve ver o servidor de configuração hello e servidor de processo na infraestrutura de recuperação de Site conforme mostrado abaixo:

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. Depois que você implantou o servidor de configuração de saudação (pode levar até too15 minustes para ele tooappear), valide que ele possa se comunicar com VMs Olá que você deseja toomigrate.

6. [Defina as configurações de replicação](site-recovery-setup-replication-settings-vmware.md).

7. Habilitar a replicação: habilitar a replicação para Olá VMs que você deseja toomigrate. Você pode descobrir instâncias de EC2 hello usando Olá endereços IP privados, que pode ser obtido do console de EC2 hello.

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. Depois de instâncias de saudação EC2 foram protegidas e Olá replicação tooAzure estiver concluída, [executar um Failover de teste](site-recovery-test-failover-to-azure.md) toovalidate o desempenho do aplicativo no Azure.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. Execute um Failover de AWS tooAzure para cada VM. Opcionalmente, você pode criar um plano de recuperação e executar um Failover, toomigrate várias máquinas virtuais do AWS tooAzure. [Saiba mais](site-recovery-create-recovery-plans.md) sobre planos de recuperação.

10. Para a migração, você não precisa toocommit um failover. Em vez disso, você selecionar a opção de concluir a migração de saudação para cada máquina que você deseja toomigrate. Olá ação concluir a migração termina o processo de migração de hello, remove a replicação para máquina hello e interrompe a recuperação de Site de cobrança para a máquina de saudação.

    ![Migrar](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>Próximas etapas

- [Preparar máquinas migradas tooenable replicação](site-recovery-azure-to-azure-after-migration.md) tooanother região para necessidades de recuperação de desastres.
- Inicie a proteção de suas cargas de trabalho ao [replicar máquinas virtuais do Azure.](site-recovery-azure-to-azure.md)
