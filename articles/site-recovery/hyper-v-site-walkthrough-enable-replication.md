---
title: "a replicação para máquinas virtuais do Hyper-V replicando tooAzure (sem o System Center VMM) com o Azure Site Recovery aaaEnable | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooenable tooAzure de replicação para máquinas virtuais do Hyper-V usando o serviço do Azure Site Recovery Olá"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>Etapa 10: Habilitar a replicação para máquinas virtuais do Hyper-V replicando tooAzure


Este artigo descreve como replicação tooenable para local máquinas virtuais de Hyper-V (não gerenciados pelo System Center VMM) tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="before-you-start"></a>Antes de começar

Antes de começar, certifique-se de que sua conta de usuário do Azure tem Olá necessário [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de um novo tooAzure de máquina virtual.

## <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por padrão, todos os discos em um computador são replicados. Você pode excluir discos da replicação. Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que foi atualizada cada vez que uma máquina ou aplicativo reinicia (por exemplo, pagefile.sys ou tempdb do SQL Server). [Saiba mais](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>Replicar VMs

Habilite a replicação para VMs conforme demonstrado a seguir:          

1. Clique em **Replicar aplicativo** > **Origem**. Depois de configurar a replicação para Olá primeira vez, você pode clicar em **+ replicar** tooenable replicação para máquinas adicionais.

    ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. Em **fonte**, selecione site Olá Hyper-V. Em seguida, clique em **OK**.
3. Em **destino**, selecione a assinatura do cofre hello e Olá failover modelo toouse no Azure (clássico ou o recurso de gerenciamento) após o failover.
4. Selecione a conta de armazenamento de saudação que toouse desejado. Se você não tiver uma conta que você deseja toouse, você pode [criar um](#set-up-an-azure-storage-account). Em seguida, clique em **OK**.
5. Selecione Olá toowhich de rede e sub-rede do Azure VMs do Azure se conectará quando eles são criados o failover.

    - Selecione tooapply Olá configurações tooall máquinas de rede habilitar para replicação, **configurar agora para os computadores selecionados**.
    - Selecione **configurar posteriormente** tooselect Olá rede do Azure por máquina.
    - Se você não tiver uma rede que você deseja toouse, você pode [criar um](#set-up-an-azure-network). Selecione uma sub-rede, se aplicável. Em seguida, clique em **OK**.

   ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. Em **máquinas virtuais** > **selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate. Você só pode selecionar computadores para os quais a replicação pode ser habilitada. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. Em **propriedades** > **configurar propriedades**, selecione o sistema operacional de saudação para VMs Olá selecionado e Olá disco do sistema operacional.
8. Verifique se esse nome de VM do Azure hello (nome de destino) está em conformidade com [requisitos da máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Por padrão, todos os discos de saudação da saudação VM são selecionados para replicação. Limpar discos tooexclude-los.
10. Clique em **Okey** toosave alterações. Você pode definir propriedades adicionais posteriormente.

    ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. Em **as configurações de replicação** > **definir configurações de replicação**, selecione Olá política de replicação você deseja tooapply para Olá protegido VMs. Em seguida, clique em **OK**. Você pode modificar a política de replicação de saudação em **políticas de replicação** > nome da política > **editar configurações de**. As alterações aplicadas serão usadas para computadores que já estejam replicando e para novas máquinas.


   ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** execuções de trabalho máquina hello está pronta para failover.


## <a name="next-steps"></a>Próximas etapas


Vá muito[etapa 11: executar um failover de teste](hyper-v-site-walkthrough-test-failover.md)
