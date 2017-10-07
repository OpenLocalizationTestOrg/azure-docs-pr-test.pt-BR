---
title: "aaaFailover na recuperação de Site | Microsoft Docs"
description: "O Azure Site Recovery coordena a replicação hello, failover e recuperação de máquinas virtuais e servidores físicos. Saiba mais sobre tooAzure de failover ou um datacenter secundário."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>Failover na Recuperação de Site
Este artigo descreve como os servidores físicos e máquinas virtuais de toofailover protegido pela recuperação de Site.

## <a name="prerequisites"></a>Pré-requisitos
1. Antes de realizar um failover, fazer uma [failover de teste](site-recovery-test-failover-to-azure.md) tooensure que tudo está funcionando conforme o esperado.
1. [Preparar a rede Olá](site-recovery-network-design.md) no local de destino antes de realizar um failover.  


## <a name="run-a-failover"></a>Executar um failover
Este procedimento descreve como toorun um failover para um [plano de recuperação](site-recovery-create-recovery-plans.md). Alternativamente, você pode executar failover Olá para uma única máquina virtual ou o servidor físico do hello **replicadas itens** página


![Failover](./media/site-recovery-failover/Failover.png)

1. Selecione **Planos de Recuperação** > *recoveryplan_name*. Clique em **Failover**.
2. Em Olá **Failover** tela, selecione um **ponto de recuperação** toofailover para. Você pode usar uma saudação as opções a seguir:
    1.  **Última** (padrão): essa opção primeiro processa todos os dados de saudação que tem sido enviada tooSite recuperação serviço toocreate um ponto de recuperação para cada máquina virtual antes de eles failover tooit. Essa opção fornece Olá menor RPO (objetivo de ponto de recuperação) como máquina de virtual de saudação criado após o failover tem todos os dados de saudação que tenha sido replicada tooSite o serviço de recuperação quando Olá failover foi disparado.
    1.  **Mais recentes processados**: essa opção Falha em todas as máquinas virtuais Olá recuperação plano toohello mais recente do ponto de recuperação que já foi processado pelo serviço de recuperação de Site. Quando você estiver realizando failover de teste de uma máquina virtual, o carimbo de hora do último ponto de recuperação processados Olá também é mostrado. Se você estiver fazendo o failover de um plano de recuperação, você pode ir de máquina virtual de tooindividual e examinar **pontos de recuperação mais recente** bloco tooget essas informações. Como não há tempo é gasto tooprocess Olá dados não processados, essa opção fornece uma opção de failover baixo RTO (objetivo de tempo de recuperação).
    1.  **Mais recente consistente de aplicativo**: essa opção Falha em todas as máquinas virtuais de Olá plano toohello mais recente aplicativo recuperação consistentes com o ponto de recuperação que já foi processado pelo serviço de recuperação de Site. Quando você estiver realizando failover de teste de uma máquina virtual, o carimbo de data / hora do último ponto de recuperação consistentes com o aplicativo hello também é mostrado. Se você estiver fazendo o failover de um plano de recuperação, você pode ir de máquina virtual de tooindividual e examinar **pontos de recuperação mais recente** bloco tooget essas informações.
    1.  **Várias VMs processadas mais recentemente**: essa opção só está disponível para os planos de recuperação que têm pelo menos uma máquina virtual com consistência de várias VMs ativada. Ponto de máquinas virtuais que fazem parte de uma grupo failover toohello mais recente comuns várias VMs consistente recuperação da replicação. Outro máquinas virtuais failover tootheir mais recentes processados ponto de recuperação.  
    1.  **Várias VMs mais recentes consistentes com aplicativo**: essa opção só está disponível para os planos de recuperação que têm pelo menos uma máquina virtual com consistência de várias VMs ativada. Máquinas virtuais que fazem parte de uma replicação de grupo failover toohello mais recente várias VMs consistente com o aplicativo de ponto de recuperação comum. Outra máquinas virtuais failover tootheir mais recente consistente com o aplicativo de ponto de recuperação.
    1.  **Personalizar**: se você estiver fazendo o failover de teste de uma máquina virtual, você pode usar essa opção toofailover tooa determinado ponto de recuperação.

    > [!NOTE]
    > Olá opção toochoose um ponto de recuperação só está disponível quando você estiver realizando o failover tooAzure.
    >
    >


1. Se algumas das máquinas virtuais de saudação no plano de recuperação de saudação sofreram failover em uma execução anterior e agora Olá máquinas de virtuais estão ativas no local de origem e destino, você pode usar **alterar direção** opção direção Olá toodecide qual o failover Olá deve ocorrer.
1. Se você estiver realizando o failover tooAzure e criptografia de dados está habilitada para nuvem hello (aplica-se somente quando você protegeu máquinas virtuais Hyper-v de um servidor VMM), em **chave de criptografia** certificado Olá select que foi emitido quando você criptografia de dados durante a instalação no servidor do VMM Olá habilitada.
1. Selecione **desligar a máquina antes de iniciar o failover** se você quiser que o Site Recovery tooattempt toodo um desligamento de máquinas virtuais de origem antes de disparar Olá failover. O failover continuará mesmo o desligamento falhar.  

    > [!NOTE]
    > No caso de máquinas virtuais Hyper-v, essa opção também tenta toosynchronize Olá de dados locais que ainda não foi enviados toohello serviço antes de disparar um failover de saudação.
    >
    >

1. Você pode acompanhar o progresso de failover de saudação em Olá **trabalhos** página. Mesmo se ocorrerem erros durante um failover não planejado, o plano de recuperação de saudação executa até que ela seja concluída.
1. Após o failover hello, valide máquina virtual de saudação fazendo logon em tooit. Se você deseja toogo outro ponto de recuperação para a máquina virtual de saudação, você pode usar **alterar ponto de recuperação** opção.
1. Quando estiver satisfeito com hello failover da máquina virtual, você pode **confirmar** Olá failover. Isso exclui todos os pontos de recuperação Olá disponíveis com o serviço de saudação e **alterar ponto de recuperação** opção não estará disponível.

## <a name="planned-failover"></a>Failover planejado
Além do failover, as máquinas virtuais Hyper-V protegidas usando o Site Recovery também suportam **Failover planejado**. Essa é uma opção de failover com perda de dados zero. Quando um failover planejado é disparado, primeiro Olá fonte máquinas virtuais são desligadas, dados saudação ainda toobe sincronizada é sincronizado e, em seguida, um failover é disparado.

> [!NOTE]
> Quando você máquinas virtuais de Hyper-v de failover de um local tooanother site local site, toocome toohello back local primário tiver toofirst **replicação inversa** site de backup tooprimary máquina virtual hello e em seguida, dispare um failover. Se a máquina virtual primária de saudação não estiver disponível, em seguida, antes de iniciar muito**replicação inversa** ter toorestore Olá máquina de virtual de um backup.   
>
>

## <a name="failover-job"></a>Trabalho de failover

![Failover](./media/site-recovery-failover/FailoverJob.png)

Quando é disparado, um failover envolve as seguintes etapas:

1. Verificação de pré-requisitos: Essa etapa garante que todas as condições necessárias para o failover sejam atendidas
1. Failover: Essa etapa processa dados hello e torna pronto para que uma máquina virtual do Azure pode ser criada fora dele. Se você tiver escolhido **mais recente** ponto de recuperação, esta etapa cria um ponto de recuperação de dados de saudação que enviou toohello serviço.
1. Início: Essa etapa cria uma máquina virtual do Azure usando dados Olá processados na etapa anterior hello.

> [!WARNING]
> **Não cancelar uma em andamento failover**: antes de iniciar o failover, a replicação da máquina virtual de saudação é interrompida. Se você **Cancelar** um trabalho em andamento, paradas de failover, mas Olá VM não será iniciado tooreplicate. A replicação não pode ser iniciada novamente.
>
>

## <a name="time-taken-for-failover-tooazure"></a>Tempo levado para tooAzure de failover

Em certos casos, o failover de máquinas virtuais requer uma etapa intermediária extra que geralmente leva aproximadamente 8 toocomplete de minutos too10. Esses casos são os seguintes:

* Máquinas virtuais VMware usando o serviço de mobilidade da versão anterior a 9.8
* Servidores físicos 
* Máquinas virtuais VMware Linux
* Máquinas virtuais Hyper-V protegidas como servidores físicos
* Máquinas virtuais VMware em que os drivers a seguir não estão presentes como drivers de inicialização 
    * storvsc 
    * vmbus 
    * storflt 
    * intelide 
    * atapi
* Máquinas virtuais VMware que não têm o serviço DHCP habilitado, independentemente de estarem usando endereços DHCP ou IP estáticos

Em Olá todos os outros casos essa etapa intermediária não é necessária e tempo Olá Olá failover é significativamente mais baixo. 





## <a name="using-scripts-in-failover"></a>Utilizar scripts no Failover
Talvez você queira tooautomate determinadas ações ao realizar um failover. Você pode usar scripts ou [runbooks de automação do Azure](site-recovery-runbook-automation.md) na [planos de recuperação](site-recovery-create-recovery-plans.md) toodo que.

## <a name="other-considerations"></a>Outras considerações
* **Letra da unidade** — letra da unidade tooretain Olá em máquinas virtuais após o failover, você pode definir Olá **diretiva SAN** para Olá virtual da máquina muito**OnlineAll**. [Leia mais](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>Próximas etapas
Depois de fazer failover em máquinas virtuais e Olá local data center está disponível, você deve [ **proteger novamente** ](site-recovery-how-to-reprotect.md) toohello Centro de dados de local de volta de máquinas virtuais VMware.

Use [ **failover planejado** ](site-recovery-failback-from-azure-to-hyper-v.md) opção muito**Failback** máquinas virtuais Hyper-v fazer tooon locais do Azure.

Se a falha em um dados locais de tooanother de máquina virtual de Hyper-v center gerenciado pelo VMM server e hello data center principal estiver disponível, em seguida, use **a replicação inversa** toohello voltar a opção toostart Olá para replicação data center primário.
