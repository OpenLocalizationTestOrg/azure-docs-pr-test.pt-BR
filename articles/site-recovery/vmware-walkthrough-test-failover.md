---
title: "aaaRun um failover de teste para VMware replicação tooAzure | Microsoft Docs"
description: "Resume as etapas de saudação que é necessário para executar um failover de teste para VMs VMware replicando tooAzure usando o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bed934446f0c6940089bfae24a13de4fb1556a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-12-run-a-test-failover-tooazure-for-vmware-vms"></a>Etapa 12: Executar um tooAzure de failover de teste para VMs VMware

Este artigo descreve como toorun um failover de teste do local VMware virtual máquinas tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

Antes de executar um failover de teste, que é recomendável que você verifique Olá propriedades da VM e faça as alterações você precisa. Você pode acessar propriedades da VM Olá no **replicadas itens**. Olá **Essentials** folha mostra informações sobre configurações de máquinas e status.

## <a name="managed-disk-considerations"></a>Considerações sobre discos gerenciados

[Discos gerenciado](../virtual-machines/windows/managed-disks-overview.md) simplificar o gerenciamento de disco para máquinas virtuais do Azure, por meio do gerenciamento de contas de armazenamento Olá associadas Olá discos VM. 

- Quando você habilita a proteção para uma VM, dados da VM replicam tooa conta de armazenamento. Discos gerenciados são criados e anexados toohello VM somente quando ocorrer failover.
- Discos gerenciados podem ser criados somente para as VMs implantadas usando o modelo do Gerenciador de recursos de saudação.  
- Com essa configuração habilitada, apenas os conjuntos de disponibilidade nos Grupos de Recursos que tenham a configuração **Utilizar discos gerenciados** habilitados poderão ser selecionados. Máquinas virtuais com discos gerenciados devem ser em conjuntos de disponibilidade com **usar gerenciada discos** definido muito**Sim**. Se a configuração de saudação não está habilitada para máquinas virtuais, apenas conjuntos de disponibilidade em grupos de recursos sem discos gerenciados habilitados podem ser selecionados.
- [Saiba mais](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) sobre discos gerenciados e conjuntos de disponibilidade.
- Se você usar para replicação de conta de armazenamento Olá tiver sido criptografada com criptografia do serviço de armazenamento, discos gerenciados não podem ser criados durante o failover. Nesse caso o não habilitar o uso de discos gerenciados, ou desabilite a proteção de saudação VM e reabilitá-la toouse uma conta de armazenamento que não tem a criptografia habilitada. [Saiba mais](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="network-considerations"></a>Considerações sobre rede

Você pode definir o endereço IP de destino Olá para uma VM do Azure criado após o failover.

- Se você não fornecer um endereço, Olá failover máquina usará o DHCP.
- Se definir um endereço que não esteja disponível no failover, o failover não funcionará.
- saudação do mesmo endereço IP de destino pode ser usado para failover de teste, se o endereço de saudação está disponível na rede de failover de teste de saudação.
- número de saudação de adaptadores de rede é determinado pelo tamanho Olá especificado para a máquina de virtual de destino hello:

     - Se Olá vários adaptadores de rede no computador de origem de saudação é hello igual ou menor, número de saudação de adaptadores permitido para o tamanho de máquina de destino hello, destino Olá terá Olá o mesmo número de adaptadores de fonte de saudação.
     - Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino Olá, tamanho máximo da saudação destino será usado.
     - Por exemplo, se um computador de origem tem dois adaptadores de rede e o tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores. Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um computador de destino Olá terá apenas um adaptador.     
   - Se a máquina virtual de saudação tem vários adaptadores de rede conectará todos toohello mesma rede.
   - Se a máquina virtual de saudação tem vários adaptadores de rede, Olá primeiro mostrada na lista de saudação se torna Olá *padrão* adaptador de rede na máquina virtual do Azure de saudação.
 - [Saiba mais](vmware-walkthrough-network.md) sobre o endereçamento IP.



## <a name="view-and-modify-vm-settings"></a>Exibir e modificar as configurações da VM

É recomendável que você verifique as propriedades Olá Olá computador de origem antes de executar um failover.

1. Em **itens protegidos**, clique em **itens replicados**e clique em Olá VM.
2. Em Olá **item replicadas** painel, você pode ver um resumo das informações de VM, o status de integridade e pontos de recuperação disponível mais recentes do hello. Clique em **propriedades** tooview mais detalhes.
3. Em **Computador e Rede**, é possível:
    - Modificar o nome de VM do Azure Olá. nome da saudação deve atender aos [requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Especificar um failover de postagem [grupo de recursos].
    - Especifique um tamanho de destino para Olá VM do Azure
    - Selecione um [conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md).
    - Especifique se toouse [discos gerenciado](#managed-disk-considerations). Selecione **Sim**, se você quiser tooattach discos gerenciado tooyour máquina em tooAzure de migração.
    - Exibir ou modificar as configurações de rede, incluindo Olá/sub-rede na qual Olá VM do Azure serão localizado após o failover e o endereço IP de saudação que será atribuído tooit.
4. Em **discos**, você pode ver informações sobre o sistema operacional de saudação e discos de dados Olá VM.

## <a name="run-a-test-failover"></a>Execute um teste de failover

Depois que você configurou tudo, execute um toomake de failover de teste se que tudo está funcionando conforme o esperado.

- Se você quiser tooconnect tooAzure VMs usando o RDP após o failover, [preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - teste de toofully necessário toocopy do Active Directory e DNS em seu ambiente de teste. [Saiba mais](site-recovery-active-directory.md#test-failover-considerations).
 - Para obter informações completas sobre failover de teste, leia [este artigo](site-recovery-test-failover-to-azure.md).
- Obtenha uma rápida visão geral em vídeo antes de começar:


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


Agora, execute um failover:

1. toofail em um único computador, em **configurações** > **itens duplicados**, clique em Olá VM > **+ Failover de teste** ícone.

    ![Failover de Teste](./media/vmware-walkthrough-test-failover/test-failover.png)

2. Planejar toofail sobre a recuperação, em **configurações** > **planos de recuperação**, plano de saudação do botão direito do mouse > **Failover de teste**. um plano de recuperação de toocreate [, siga estas instruções](site-recovery-create-recovery-plans.md).  

3. Em **Failover de teste**, selecione toowhich de rede do Azure Olá VMs do Azure será conectada após o failover.

4. Clique em **Okey** toobegin Olá failover. Você pode acompanhar o progresso clicando no hello VM tooopen suas propriedades, ou em Olá **Failover de teste** trabalho em nome do cofre > **configurações** > **trabalhos**  >  **Trabalhos de recuperação de site**.

5. Após a conclusão do failover hello, você também deve ser capaz de réplica de saudação toosee máquina do Azure aparecem no hello portal do Azure > **máquinas virtuais**. Você deve garantir que Olá VM é o tamanho apropriado hello, que tenha se conectado toohello apropriado, e rede que está sendo executado.

6. Se você preparou para conexões após o failover, deve ser capaz de tooconnect toohello VM do Azure.

7. Depois de concluir, clique em **failover de teste de limpeza** no plano de recuperação de saudação. Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste. Isso excluirá Olá VMs que foram criados durante o failover de teste.



## <a name="next-steps"></a>Próximas etapas

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.
- Se estiver migrando máquinas em vez de replicar e fazer failback, [leia mais](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Leia sobre failback](site-recovery-failback-azure-to-vmware.md), toofail back e replicação de máquinas virtuais do Azure novamente toohello principal no site local.
