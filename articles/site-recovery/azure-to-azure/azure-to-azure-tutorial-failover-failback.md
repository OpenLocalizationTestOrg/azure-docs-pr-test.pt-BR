---
title: "Fazer failover e failback de VMs do Azure replicadas para uma região do Azure secundária com o Azure Site Recovery (versão prévia)"
description: "Saiba como fazer failover e failback da replicação de VMs do Azure para uma região do Azure secundária com o Azure Site Recovery"
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 11/01/2017
ms.author: raynew
ms.custom: mvc
ms.openlocfilehash: 5f37a7b3534102a06f6d5dc6fb91d3abee7c0522
ms.sourcegitcommit: cfd1ea99922329b3d5fab26b71ca2882df33f6c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2017
---
# <a name="fail-over-and-fail-back-azure-vms-between-azure-regions-preview"></a>Fazer failover e failback de VMs do Azure entre regiões do Azure (versão prévia)

O serviço [Azure Site Recovery](../site-recovery-overview.md) contribui para sua estratégia de recuperação de desastre ao gerenciar e orquestrar a replicação, o failover e o failback de computadores locais e de VMs (máquinas virtuais) do Azure.

Este tutorial descreve como fazer failover de uma única VM do Azure para uma região secundária do Azure. Depois de fazer failover, você fará failback para a região primária quando ela estiver disponível. Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Fazer failover da VM do Azure
> * Proteger novamente a VM do Azure secundária para que ela seja replicada para a região primária
> * Fazer failback da VM secundária
> * Proteger novamente a VM primária de volta para a região secundária

## <a name="prerequisites"></a>Pré-requisitos

- É importante realizar uma [simulação de recuperação de desastre](azure-to-azure-tutorial-dr-drill.md) para verificar se tudo está funcionando conforme o esperado.
- Verifique as propriedades da VM antes de executar o failover de teste. A VM deve atender aos [requisitos do Azure](../site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="run-a-failover-to-the-secondary-region"></a>Executar um failover para a região secundária

1. Em **Itens replicados**, selecione a VM cujo failover você deseja fazer > **Failover**

   ![Failover](./media/azure-to-azure-tutorial-failover-failback/failover.png)

2. Em **Failover**, selecione um **Ponto de Recuperação** para o qual fazer o failover. Você pode usar uma das seguintes opções:

   * **Último** (padrão): essa opção processa todos os dados no serviço Site Recovery e fornece o RPO (Objetivo de Ponto de Recuperação) mais baixo.
   * **Último processado**: essa opção reverte a máquina virtual para o último ponto de recuperação que já foi processado pelo serviço Site Recovery.
   * **Personalizado**: use essa opção para fazer failover para um ponto de recuperação específico. Essa opção é útil para fazer um failover de teste.

3. Selecione **Desligue o computador antes do início do failover** se quiser que o Site Recovery tente realizar um desligamento das máquinas virtuais de origem antes de disparar o failover. O failover continuará mesmo o desligamento falhar.

4. Acompanhe o progresso do failover na página **Trabalhos**.

5. Após o failover, valide a máquina virtual, efetuando logon nela. Se desejar ir a outro ponto de recuperação para a máquina virtual, você pode usar a opção **Alterar ponto de recuperação**.

6. Quando estiver satisfeito com a máquina virtual que passou por failover, você pode **Confirmar** o failover.
   Confirmar exclui todos os pontos de recuperação disponíveis com o serviço. A opção **Alterar ponto de recuperação** não está mais disponível.

## <a name="reprotect-the-secondary-vm"></a>Proteger novamente a VM secundária

Após o failover da VM, você precisa protegê-la novamente para que ela seja replicada de volta para a região primária.

1. Verifique se a VM está no estado **Failover confirmado** e verifique se a região primária está disponível e se você é capaz de criar e acessar novos recursos nela.
2. Em **Cofre** > **Itens replicados**, clique com o botão direito do mouse na VM em que o failover foi executado e, em seguida, selecione **Proteger Novamente**.

   ![Clicar com o botão direito do mouse para proteger novamente](./media/azure-to-azure-tutorial-failover-failback/reprotect.png)

2. Observe que a direção da proteção, da região secundária para a primária, já está selecionada.
3. Examine as informações de **Grupo de recursos, Rede, Armazenamento e Conjuntos de disponibilidade**. Quaisquer recursos marcados (novos) serão criados como parte da operação de proteger novamente.
4. Clique em **OK** para disparar um trabalho de proteger novamente. Esse trabalho propaga os dados mais recentes para o site de destino. Em seguida, ele replica os deltas para a região primária. A VM agora está em um estado protegido.

## <a name="fail-back-to-the-primary-region"></a>Failback para a região primária

Depois que as VMs são protegidas novamente, você pode fazer failback para a região primária conforme necessário. Para fazer isso, siga as instruções de [failover](#run-a-failover).
