---
title: "a replicação de servidores físicos replicando tooAzure com o Azure Site Recovery aaaEnable | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooenable tooAzure de replicação de servidores físicos, usando o serviço do Azure Site Recovery Olá"
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
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a>Etapa 10: Habilitar a replicação de servidores físicos tooAzure


Este artigo descreve como replicação tooenable para local Windows/Linux tooAzure de servidores físicos, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

- Os servidores devem ter Olá [componente de serviço de mobilidade instalado](physical-walkthrough-install-mobility.md).
- Se uma VM está preparada para a instalação por push, servidor de processo Olá instala automaticamente o serviço de mobilidade hello quando você habilitar a replicação.
- Quando você habilita uma máquina para replicação, precisa de sua conta de usuário do Azure específico [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure você está toouse capaz de armazenamento do Azure e criar máquinas virtuais do Azure.
- Quando você adicionar ou modificar os endereços IP para servidores, pode levar too15 minutos ou mais para efeito de tootake de alterações e, para que eles tooappear no portal de saudação.


## <a name="exclude-disks-from-replication"></a>Excluir discos da replicação

Por padrão, todos os discos em um computador são replicados. Você pode excluir discos da replicação. Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que foi atualizada cada vez que uma máquina ou aplicativo reinicia (por exemplo, pagefile.sys ou tempdb do SQL Server). [Saiba mais](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a>Replicar servidores

1. Clique em **Etapa 2: replicar aplicativo** > **Origem**.
2. Em **fonte**, selecione o servidor de configuração hello.
3. Em **Tipo de máquina**, selecione **Máquinas Físicas**.
4. Selecione o servidor de processo hello. Se você não criou nenhum servidor de processo adicional esse será o servidor de configuração de saudação. Em seguida, clique em **OK**.
5. Em **destino**, selecione a assinatura hello e Olá no qual você deseja Olá toocreate failover de máquinas virtuais do grupo de recursos. Escolha o modelo de implantação de saudação que você deseja toouse no Azure (clássico ou o recurso de gerenciamento), para Olá failover VMs.
6. Selecione conta de armazenamento do Azure Olá que desejar toouse para replicação de dados. Se você não quiser toouse uma conta que você já tenha configurado o, você pode criar um novo.
7. Selecione Olá **rede Azure** e **sub-rede** toowhich VMs do Azure se conectar após o failover. Selecione **configurar agora para os computadores selecionados** tooapply Olá rede configuração tooall máquinas selecionadas para proteção. Selecione **configurar posteriormente** tooselect Olá rede do Azure por máquina. Se você não quiser toouse uma rede existente, você pode criar um.

    ![Habilitar a replicação](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. Em **máquinas físicas**, clique em **+ máquina física** e digite Olá **nome** e **endereço IP**. Escolha o sistema operacional de saudação da máquina Olá deseja tooreplicate. Leva alguns minutos até que os computadores são descobertos e mostrados na lista de saudação.
9. Em **propriedades** > **configurar propriedades**, selecione conta Olá que será usada por tooautomatically de servidor de processo Olá instalar serviço de mobilidade de saudação na máquina de saudação.
10. Por padrão, todos os discos são replicados. Clique em **todos os discos** e desmarque os discos que você não deseja tooreplicate. Em seguida, clique em **OK**. Você pode definir propriedades de VM adicionais posteriormente.

    ![Habilitar a replicação](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. Em **as configurações de replicação** > **definir configurações de replicação**, verifique se esse Olá correto de política de replicação está selecionada. Se você modificar uma política, as alterações serão aplicadas tooreplicating máquina e toonew máquinas.
12. Habilitar **consistência de várias VMs** toogather máquinas em um grupo de replicação, e especifique um nome para o grupo de saudação. Em seguida, clique em **OK**. Observe que:

    * Os computadores nos grupos de replicação são replicados em conjunto e têm pontos de recuperação consistentes compartilhados com o aplicativo e com falhas quando executam failover.
    * Recomendamos que você reúna os servidores físicos, de forma que eles espelhem as cargas de trabalho. Habilitar a consistência de várias VMs pode afetar o desempenho da carga de trabalho e só deve ser usado se as máquinas estão executando Olá mesma carga de trabalho e você precisa de consistência.

13. Clique em **Habilitar a Replicação**. Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **configurações** > **trabalhos** > **trabalhos de recuperação de Site**. Depois de saudação **finalizar proteção** execuções de trabalho máquina hello está pronta para failover.

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 11: executar um failover de teste](physical-walkthrough-test-failover.md)
