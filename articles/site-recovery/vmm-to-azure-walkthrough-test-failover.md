---
title: "um failover de teste para tooAzure de replicação (com o System Center VMM) do Hyper-V de aaaRun | Microsoft Docs"
description: "Resume as etapas de saudação que é necessário para executar um failover de teste para VMs do Hyper-V nas nuvens do VMM, replicando tooAzure usando o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7b562a23-7ba7-48ee-905d-c22b4b5d6466
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: fc60e536f2eeb6f95dde3d347f364f3bf8bfdf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-with-vmm-tooazure"></a>Etapa 11: Executar um failover de teste para tooAzure de replicação (com o VMM) do Hyper-V

Depois que você [habilitar a replicação para máquinas virtuais do Hyper-V](vmm-to-azure-walkthrough-enable-replication.md), use este toorun artigo um failover de teste do local máquinas de virtuais de Hyper-V gerenciado no tooAzure de nuvens do System Center Virtual Machine Manager (VMM), usando Olá [ O Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Antes de começar

Antes de executar um failover de teste, que é recomendável que você verifique Olá propriedades da VM e faça as alterações você precisa. Você pode acessar propriedades da VM Olá no **replicadas itens**. Olá **Essentials** folha mostra informações sobre configurações de máquinas e status.

## <a name="managed-disk-considerations"></a>Considerações sobre discos gerenciados

[Discos gerenciado](../virtual-machines/windows/managed-disks-overview.md) simplificar o gerenciamento de disco para máquinas virtuais do Azure, por meio do gerenciamento de contas de armazenamento Olá associadas Olá discos VM. 

- Discos gerenciados são criados e anexados toohello VM somente quando ocorre um failover tooAzure. Quando você habilita a proteção, dados de local VMs replicam toostorage contas.
- Discos gerenciados podem ser criados apenas para VMs que são implantados usando o modelo de implantação do Gerenciador de recursos de hello.
- Failback do Azure tooan local ambiente Hyper-V não é suportado atualmente para computadores com discos gerenciados. Você só deve definir **usar gerenciada discos** muito**Sim** se você estiver fazendo uma migração única (failover tooAzure sem failback)
- Com essa configuração habilitada, apenas os conjuntos de disponibilidade nos Grupos de Recursos que tenham a configuração **Utilizar discos gerenciados** habilitados poderão ser selecionados. Máquinas virtuais com discos gerenciados devem ser em conjuntos de disponibilidade com **usar gerenciada discos** definido muito**Sim**. Se a configuração de saudação não está habilitada para máquinas virtuais, apenas conjuntos de disponibilidade em grupos de recursos sem discos gerenciados habilitados podem ser selecionados. [Saiba mais](../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).
- - Se você usar para replicação de conta de armazenamento Olá tiver sido criptografada com criptografia do serviço de armazenamento, discos gerenciados não podem ser criados durante o failover. Nesse caso o não habilitar o uso de discos gerenciados, ou desabilite a proteção de saudação VM e reabilitá-la toouse uma conta de armazenamento que não tem a criptografia habilitada. [Saiba mais](../virtual-machines/windows/managed-disks-overview.md#managed-disks-and-encryption).

 
## <a name="network-considerations"></a>Considerações sobre rede
    
- Você pode definir o endereço IP do hello destino toobe usado para hello Azure VM após o failover. Se você não fornecer um endereço, Olá failover máquina usará o DHCP. Se você definir um endereço que não está disponível em failover, Olá failover falhará. saudação do mesmo endereço IP de destino pode ser usado para failover de teste se o endereço de saudação está disponível na rede de failover de teste de saudação.
- número de saudação de adaptadores de rede é determinado pelo tamanho de saudação especificado para a máquina de virtual de destino Olá, da seguinte maneira:
    - Se Olá vários adaptadores de rede no computador de origem de saudação é menor ou igual toohello número de adaptadores permitido para o tamanho de máquina de destino Olá, então terá destino Olá Olá o mesmo número de adaptadores de fonte de saudação.
    - Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino hello e tamanho máximo da saudação destino será usado.
    - Por exemplo, se um computador de origem tem dois adaptadores de rede e tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um computador de destino Olá terá apenas um adaptador.     
- Se Olá VM tem vários adaptadores de rede conectará todos toohello mesma rede.
- Se a máquina virtual de saudação tem vários adaptadores de rede, Olá primeiro mostrada na lista de saudação se torna Olá *padrão* adaptador de rede na máquina virtual do Azure de saudação.


## <a name="view-and-manage-vm-settings"></a>Exibir e gerenciar as configurações da VM

É recomendável que você verifique as propriedades Olá Olá computador de origem antes de executar um failover.

1. Em **itens protegidos**, clique em **itens replicados**e clique em Olá VM.

    ![Habilitar a replicação](./media/vmm-to-azure-walkthrough-test-failover/test-failover1.png)
2. Em Olá **item replicadas** painel, você pode ver um resumo das informações de VM, o status de integridade e pontos de recuperação disponível mais recentes do hello. Clique em **propriedades** tooview mais detalhes.

    ![Habilitar a replicação](./media/vmm-to-azure-walkthrough-test-failover/test-failover2.png)
3. Em **Computador e Rede**, é possível:
    - Modificar o nome de VM do Azure Olá. nome da saudação deve atender aos [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Especificar um failover de postagem [grupo de recursos].
    - Especifique um tamanho de destino para Olá VM do Azure
    - Selecione um [conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md).
    - Especifique se toouse [discos gerenciado](#managed-disk-considerations). Selecione **Sim**, se você quiser tooattach discos gerenciado tooyour máquina em tooAzure de migração.
    - Exibir ou modificar as configurações de rede, incluindo Olá/sub-rede na qual Olá VM do Azure serão localizado após o failover e o endereço IP de saudação que será atribuído tooit.

    ![Habilitar a replicação](./media/vmm-to-azure-walkthrough-test-failover/test-failover4.png)
4. Em **discos**, você pode ver informações sobre o sistema operacional de saudação e discos de dados Olá VM.


## <a name="run-a-test-failover"></a>Execute um teste de failover

Agora, execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.

- Se você quiser tooconnect tooAzure VMs usando o RDP após o failover, [preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - teste de toofully necessário toocopy do Active Directory e DNS em seu ambiente de teste. [Saiba mais](site-recovery-active-directory.md#test-failover-considerations).
 - Para obter informações completas sobre failover de teste, leia [este artigo](site-recovery-test-failover-to-azure.md).
 
 Agora, execute um failover:

1. toofail em um único computador, em **itens replicados**, clique em Olá VM > **+ Failover de teste** ícone.
2. Planejar toofail sobre a recuperação, em **planos de recuperação**, plano de saudação do botão direito do mouse > **Failover de teste**. um plano de recuperação de toocreate [, siga estas instruções](site-recovery-create-recovery-plans.md).
3. Em **Failover de teste**, selecione toowhich de rede do Azure Olá VMs do Azure será conectada após o failover.
4. Clique em **Okey** toobegin Olá failover. Você pode acompanhar o progresso clicando no hello VM tooopen suas propriedades, ou em Olá **Failover de teste** trabalho em nome do cofre > **trabalhos** > **trabalhos de recuperação de Site**.
5. Após a conclusão do failover hello, você também deve ser capaz de réplica de saudação toosee máquina do Azure aparecem no hello portal do Azure > **máquinas virtuais**. Você deve garantir que Olá VM é o tamanho apropriado hello, que tenha se conectado toohello apropriado, e rede que está sendo executado.
6. Se você preparou para conexões após o failover, deve ser capaz de tooconnect toohello VM do Azure.
7. Depois de concluir, clique em **failover de teste de limpeza** no plano de recuperação de saudação. Em **notas** registrar e salvar todas as observações associadas Olá failover de teste. Isso excluirá as máquinas virtuais Olá que foram criadas durante o failover de teste.



## <a name="next-steps"></a>Próximas etapas

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.
- [Leia sobre failback](site-recovery-failback-from-azure-to-hyper-v.md), toofail back e replicação de máquinas virtuais do Azure novamente toohello nuvem da máquina local primário.

