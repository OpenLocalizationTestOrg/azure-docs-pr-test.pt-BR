---
title: "nuvens de aaaEnable tooAzure de replicação para máquinas virtuais do Hyper-V no VMM com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como nuvens tooenable tooAzure de replicação para máquinas virtuais do Hyper-V no VMM, com hello serviço Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>Etapa 11: Habilitar replicação tooAzure para máquinas virtuais do Hyper-V nas nuvens do VMM

Depois de configurar uma política de replicação, use essa replicação artigo tooenable para máquinas virtuais de Hyper-V no local (VMs) gerenciada em nuvens do System Center Virtual Machine Manager (VMM)), tooAzure, usando Olá [Azure Site Recovery](site-recovery-overview.md)serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

Verifique se sua conta do Azure tem Olá correto [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate VMs do Azure. [Saiba mais](../active-directory/role-based-access-built-in-roles.md) sobre o controle de acesso baseado em função do Azure.

## <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por padrão, todos os discos em um computador são replicados. Você pode excluir discos da replicação. Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que foi atualizada cada vez que uma máquina ou aplicativo reinicia (por exemplo, pagefile.sys ou tempdb do SQL Server). [Saiba mais](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Replicar VMs

Habilite a replicação para VMs conforme demonstrado a seguir:  

1. Clique em **Etapa 2: replicar aplicativo** > **Origem**. Depois de habilitar a replicação para Olá primeira vez, clique em **+ replicar** em replicação de tooenable Olá cofre para outras máquinas.

    ![Habilitar a replicação](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. Em Olá **fonte** folha, selecione Olá servidor do VMM e nuvem Olá no qual Olá Hyper-V hosts estão localizados. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. Em **destino**, selecione a assinatura hello, o modelo de implantação após o failover, e Olá conta de armazenamento que você está usando para os dados replicados.

    ![Habilitar a replicação](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. Selecione a conta de armazenamento de saudação que toouse desejado. Se você quiser toouse uma conta de armazenamento diferentes daquelas que você tem, você pode [criar um](#set-up-an-azure-storage-account). Se você estiver usando uma conta de armazenamento premium para os dados replicados, você precisa tooselect um logs de replicação de toostore conta de armazenamento padrão adicionais que captura alterações contínuas local tooon data.toocreate uma conta de armazenamento usando o modelo do Gerenciador de recursos de saudação Clique em **criar novo**. Se você quiser toocreate uma conta de armazenamento usando o modelo clássico hello, isso [no portal do Azure de saudação](../storage/common/storage-create-storage-account.md). Em seguida, clique em **OK**.
5. Selecione Olá toowhich de rede e sub-rede do Azure VMs do Azure conectará quando eles são criados após o failover. Selecione **configurar agora para os computadores selecionados**, tooapply Olá rede configuração tooall máquinas selecionadas para proteção. Selecione **configurar posteriormente**, Olá tooselect rede do Azure por máquina. Se você quiser toouse uma rede diferente daquelas que você tem, você pode [criar um](#set-up-an-azure-network). Gerenciador de recursos, clique em modelo de Olá toocreate usando uma rede **criar novo**. Se você quiser toocreate uma rede usando o modelo clássico hello, isso [no portal do Azure de saudação](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selecione uma sub-rede, se aplicável. Em seguida, clique em **OK**.
6. Em **máquinas virtuais** > **selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate. Você só pode selecionar computadores para os quais a replicação pode ser habilitada. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. Em **propriedades** > **configurar propriedades**, selecione o sistema operacional de saudação para VMs Olá selecionado e Olá disco do sistema operacional.

    - Verifique se esse nome de VM do Azure hello (nome de destino) está em conformidade com [requisitos da máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Por padrão, todos os discos de saudação da saudação VM são selecionados para replicação, mas você pode desmarcar discos tooexclude-los.

        - Talvez você queira largura de banda de replicação tooreduce tooexclude discos. Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que tem atualizados sempre que um computador ou aplicativos reinicia (como pagefile.sys ou tempdb do Microsoft SQL Server). Você pode excluir o disco de saudação da replicação por disco de saudação desmarque.
        - Apenas discos básicos podem ser excluídos. Você não pode excluir discos do sistema operacional.
        - É recomendável que você não exclua discos dinâmicos. O Site Recovery não pode identificar se um disco rígido virtual dentro de uma VM convidada é básico ou dinâmico. Se todos os discos de volume dinâmico dependentes não são excluídos, disco dinâmico protegido de saudação será mostrado como um disco com falha quando hello VM failover, e os dados no disco Olá não poderão ser acessados.
        - Depois que a replicação estiver habilitada, você não poderá adicionar ou remover discos para replicação. Se você quiser tooadd ou excluir um disco, é necessário toodisable proteção para Olá VM e reabilitá-la.
        - Discos que você criar manualmente no Azure não sofrerão failback. Por exemplo, se você falha em três discos e cria duas diretamente na VM do Azure, somente Olá três discos que sofreram failover serão falhou da tooHyper-V do Azure. Você não pode incluir discos criados manualmente no failback ou na replicação inversa do Hyper-V tooAzure.
        - Se você excluir um disco que é necessário para um aplicativo toooperate, após o failover tooAzure é necessário toocreate-lo manualmente no Azure, portanto esse Olá replicadas aplicativo pode executar. Como alternativa, você pode integrar a automação do Azure em um plano de recuperação, o disco de saudação toocreate durante o failover da máquina de saudação.

    Clique em **Okey** toosave alterações. Você pode definir propriedades adicionais posteriormente.

    ![Habilitar a replicação](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. Em **as configurações de replicação** > **definir configurações de replicação**, selecione Olá política de replicação você deseja tooapply para Olá protegido VMs. Em seguida, clique em **OK**. Você pode modificar a política de replicação de saudação em **políticas de replicação** > nome da política > **editar configurações de**. As alterações aplicadas são usadas para computadores que já estejam replicando e para novas máquinas.

   ![Habilitar a replicação](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** trabalho é executado, a máquina de saudação está pronta para failover.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 12: executar um failover de teste](vmm-to-azure-walkthrough-test-failover.md)
