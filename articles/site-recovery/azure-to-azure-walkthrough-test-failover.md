---
title: "aaaRun um failover de teste para replicação de VM do Azure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação que você precisa para executar um failover de teste para máquinas virtuais do Azure replica tooanother região do Azure usando hello Azure Site Recovery service."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a>Etapa 6: executar um failover de teste para replicação de VM do Azure

Depois de habilitar a replicação da máquina virtual do Azure (VMs), execute as etapas de saudação neste artigo, o failover de teste de toorun de tooanother de uma região do Azure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

- Quando você terminar de artigo hello, você deve ter verificado com um failover de teste que pelo menos uma VM do Azure pode fazer failover tooyour região secundária do Azure. 
- Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Atualmente, a replicação de VM do Azure está em versão prévia.


## <a name="before-you-start"></a>Antes de começar

- Antes de executar um failover de teste, é recomendável que você verifique Olá propriedades da VM e faça as alterações que você precisa. Você pode acessar propriedades da VM Olá no **replicadas itens**. Olá **Essentials** folha mostra informações sobre configurações de máquinas e status.
- É recomendável usar uma rede separada da VM do Azure para failover de teste Olá e não rede de saudação (padrão ou personalizado) que foi configurada para failover de produção.
- Olá teste failover failover de máquinas virtuais do Azure (e seu armazenamento) toohello região secundária do Azure. Não replica quaisquer aplicativos ou recursos dependentes. Se os aplicativos executados em falha em VMs dependem de outros recursos, como o Active Directory ou DNS, você precisa tooreplicate dessas também, se eles não ainda estiver disponíveis em sua região secundária. [Saiba mais](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- Se você quiser tooaccess replicadas VMs após o failover de um site local, você precisa muito[preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese VMs.

## <a name="run-a-test-failover"></a>Execute um teste de failover

1. Em **configurações** > **itens replicados**, clique em Olá VM **+ Failover de teste** ícone. 

2. Em **Failover de teste**, selecione um toouse de ponto de recuperação para failover de saudação:

    - **Mais recentes processados**: falha Olá VM sobre toohello último ponto de recuperação que foi processado pelo serviço de recuperação de Site hello. carimbo de data / hora de saudação é mostrado. Com essa opção, nenhum tempo é gasto em processamento de dados, portanto, fornece um RTO (Objetivo do Tempo de Recuperação) baixo.
    - **Mais recente consistente de aplicativo**: essa opção Falha em todas as VMs toohello ponto mais recente recuperação consistentes com o aplicativo. carimbo de data / hora de saudação é mostrado. 
    - **Personalizar**: selecione qualquer ponto de recuperação.
 
3. Selecione Olá destino rede virtual do Azure toowhich VMs do Azure na região secundária hello será conectada após o failover de saudação.
4. toostart Olá failover, clique em **Okey**. tootrack de andamento, clique em Olá VM tooopen suas propriedades. Ou, você pode clicar em Olá **Failover de teste** trabalho em nome do cofre hello > **configurações** > **trabalhos** > **ostrabalhosderecuperaçãodeSite**.
5. Depois de saudação failover for concluído, réplica hello Azure VM aparece no hello portal do Azure > **máquinas virtuais**. Certifique-se de que Olá VM é o tamanho apropriado hello, que tenha se conectado toohello apropriado, e rede que está sendo executado.
6. Olá toodelete VMs que foram criados durante a saudação failover de teste, clique em **failover de teste de limpeza** em Olá replicadas item ou hello plano de recuperação. Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste. 

[Saiba mais](site-recovery-test-failover-to-azure.md) sobre failovers de teste.

## <a name="next-steps"></a>Próximas etapas

Depois de testar o failover, esse passo a passo estará concluído. Agora, saiba mais sobre a execução de failovers em produção:

- [Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.
- Saiba mais sobre a falha em várias VMs[utilizando um plano de recuperação](site-recovery-create-recovery-plans.md).
- Saiba mais sobre [utilizar planos de recuperação](site-recovery-create-recovery-plans.md).
- Saiba mais sobre [proteger novamente as VMs do Azure](site-recovery-how-to-reprotect.md) após o failover.

