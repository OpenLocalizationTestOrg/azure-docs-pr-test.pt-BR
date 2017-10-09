---
title: "replicação aaaEnable para VMs VMware replicando tooAzure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooenable tooAzure de replicação para VMs VMware usando o serviço do Azure Site Recovery Olá"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a>Etapa 11: Habilitar a replicação para tooAzure de máquinas virtuais VMware


Este artigo descreve como replicação tooenable para local VMware virtual máquinas tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

- Máquinas virtuais do VMware devem ter Olá [componente de serviço de mobilidade instalado](vmware-walkthrough-install-mobility.md). -Se uma VM está preparada para a instalação por push, servidor de processo Olá instala automaticamente o serviço de mobilidade hello quando você habilitar a replicação.
- Sua conta de usuário do Azure precisa específico [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de uma VM tooAzure
- Quando você adiciona ou modifica máquinas virtuais, pode levar a too15 minutos ou mais para efeito de tootake de alterações e, para que eles tooappear no portal de saudação.
- Você pode verificar o tempo de saudação do último descoberto para VMs no **servidores de configuração** > **último contato em**.
- tooadd VMs sem aguardar a descoberta agendada hello, servidor de configuração de saudação do realce (não clique nele) e clique em **atualizar**.



## <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por padrão, todos os discos em um computador são replicados. Você pode excluir discos da replicação. Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que foi atualizada cada vez que uma máquina ou aplicativo reinicia (por exemplo, pagefile.sys ou tempdb do SQL Server). [Saiba mais](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Replicar VMs

Antes de começar, assista a uma rápida visão geral em vídeo

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Clique em **Etapa 2: replicar aplicativo** > **Origem**.
2. Em **fonte**, selecione o servidor de configuração hello.
3. Em **Tipo de máquina**, selecione **Máquinas Virtuais**.
4. Em **vCenter/vSphere hipervisor**, selecione o servidor do vCenter Olá que gerencia o host do vSphere hello, ou selecione host hello.
5. Selecione o servidor de processo hello. Se você não criou nenhum servidor de processo adicional esse será o servidor de configuração de saudação. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. Em **destino**, selecione a assinatura hello e Olá no qual você deseja Olá toocreate failover de máquinas virtuais do grupo de recursos. Escolha o modelo de implantação de saudação que você deseja toouse no Azure (clássico ou o recurso de gerenciamento), para Olá failover VMs.


7. Selecione conta de armazenamento do Azure Olá que desejar toouse para replicação de dados. Se você não quiser toouse uma conta que você já tenha configurado o, você pode criar um novo.

8. Selecione Olá toowhich de rede e sub-rede do Azure VMs do Azure conectará quando eles são criados após o failover. Selecione **configurar agora para os computadores selecionados**, tooapply Olá rede configuração tooall máquinas selecionadas para proteção. Selecione **configurar posteriormente** tooselect Olá rede do Azure por máquina. Se você não quiser toouse uma rede existente, você pode criar um.

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. Em **máquinas virtuais** > **selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate. Você só pode selecionar computadores para os quais a replicação pode ser habilitada. Em seguida, clique em **OK**.

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. Em **propriedades** > **configurar propriedades**, selecione conta Olá que será usada por tooautomatically de servidor de processo Olá instalar serviço de mobilidade de saudação na máquina de saudação.
11. Por padrão, todos os discos são replicados. Clique em **todos os discos** e desmarque os discos que você não deseja tooreplicate. Em seguida, clique em **OK**. Você pode definir propriedades de VM adicionais posteriormente.

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. Em **as configurações de replicação** > **definir configurações de replicação**, verifique se esse Olá correto de política de replicação está selecionada. Se você modificar uma política, as alterações serão aplicadas tooreplicating máquina e toonew máquinas.
12. Habilitar **consistência de várias VMs** toogather máquinas em um grupo de replicação, e especifique um nome para o grupo de saudação. Em seguida, clique em **OK**. Observe que:

    * Os computadores nos grupos de replicação são replicados em conjunto e têm pontos de recuperação consistentes compartilhados com o aplicativo e com falhas quando executam failover.
    * É recomendável que você colete VMs e servidores físicos para que espelhem suas cargas de trabalho. Habilitar a consistência de várias VMs pode afetar o desempenho da carga de trabalho e só deve ser usado se as máquinas estão executando Olá mesma carga de trabalho e você precisa de consistência.

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. Clique em **Habilitar a Replicação**. Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **configurações** > **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** execuções de trabalho máquina hello está pronta para failover.

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 12: executar um failover de teste](vmware-walkthrough-test-failover.md)
