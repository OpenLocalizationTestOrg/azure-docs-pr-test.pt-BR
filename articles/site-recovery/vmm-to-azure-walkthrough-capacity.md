---
title: "aaaPlan capacidade e dimensionamento para tooAzure de replicação (com o VMM) de VM do Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Usar essa capacidade do artigo tooplan e escala quando a replicação de máquinas virtuais do Hyper-V no VMM nuvens tooAzure, com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a>Etapa 3: Planejar a capacidade e dimensionamento para a replicação do Hyper-V (com o VMM) tooAzure

Depois que você tiver examinado Olá [os pré-requisitos de implantação](vmm-to-azure-walkthrough-prerequisites.md), use toofigure este artigo planejamento de capacidade e dimensionamento, durante a replicação local em VMs Hyper-V tooAzure de nuvens do System Center Virtual Machine Manager (VMM), com [Azure Site Recovery](site-recovery-overview.md).

Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="how-do-i-start-capacity-planning"></a>Como iniciar o planejamento de capacidade?


Você coletar informações sobre o ambiente de replicação e capacidade de plano usando dados hello, junto com as considerações de saudação realçados neste artigo.


## <a name="gather-information"></a>Coletar informações

1. Reunir informações sobre seu ambiente de replicação, inclusive VMs, discos por VMs e armazenamento por disco.
2. Identifique sua taxa de alteração (variação) diária de dados replicados. Baixar Olá [ferramenta de planejamento de capacidade de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) tooget taxa de alteração de saudação. Recomendamos que você execute essa ferramenta em uma semana toocapture médias.
 

## <a name="figure-out-capacity"></a>Descobrir a capacidade

Com base nas informações de saudação que você colete, executar Olá [ferramenta de Planejador de capacidade de recuperação de Site](http://aka.ms/asr-capacity-planner-excel) tooanalyze seu ambiente de origem e cargas de trabalho, estimar as necessidades de largura de banda e recursos do servidor para o local de origem hello e Olá recursos (máquinas virtuais e armazenamento etc), que é necessário no local de destino hello. Você pode executar a ferramenta de saudação em dois modos:

- Planejando rápida: executar ferramenta Olá nesse modo tooget projeções de rede e servidor com base em um número médio de VMs, discos, armazenamento e a taxa de alteração.
- Planejamento detalhado: execute a ferramenta de saudação nesse modo e fornecer detalhes de cada carga de trabalho no nível da VM. Analise a compatibilidade da VM e obtenha as projeções de rede e de servidor.

Agora execute a ferramenta de saudação:

1. Baixar Olá [ferramenta](http://aka.ms/asr-capacity-planner-excel)
2. Planejador rápida do toorun hello, siga [estas instruções](site-recovery-capacity-planner.md#run-the-quick-planner)e selecione Olá cenário **tooAzure Hyper-V**.
3. toorun Olá Planejador detalhada, execute [estas instruções](site-recovery-capacity-planner.md#run-the-detailed-planner)e selecione Olá cenário **tooAzure Hyper-V**.

## <a name="control-network-bandwidth"></a>Controlar largura de banda da rede

Depois que você tenha largura de banda Olá calculado que é necessário, você tem duas opções para controlar quantidade de saudação de largura de banda usada para replicação:

* **Limitação da largura de banda**: tráfego Hyper-V que replica tooAzure passa por um host Hyper-V específico. Você pode reduzir a largura de banda no servidor de host de saudação.
* **Influenciam a largura de banda**: você pode influenciar a largura de banda de saudação usada para replicação usando duas chaves do registro.

### <a name="throttle-bandwidth"></a>Restringir a largura de banda
1. Abra o snap-in MMC do Backup do Microsoft Azure de saudação no servidor de host do Hyper-V hello. Por padrão um atalho para o Backup do Microsoft Azure está disponível na área de trabalho hello, ou em C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. No snap-in Olá clique **alterar propriedades**.
3. Em Olá **limitação** guia **habilitar limitação para operações de backup do uso de largura de banda de internet**e definir limites de saudação do trabalho e folga horas. Intervalos válidos são de 512 Mbps de too102 Kbps por segundo.

    ![Restringir a largura de banda](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

Você também pode usar o hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação. Veja um exemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que nenhuma limitação é necessária.

### <a name="influence-network-bandwidth"></a>Influência da largura de banda de rede
1. No registro de saudação navegue muito**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tráfego de largura de banda de saudação tooinfluence em um disco de replicação, modificar Olá Olá do valor **UploadThreadsPerVM**, ou criar a chave de saudação se ele não existir.
   * largura de banda tooinfluence Olá para o tráfego de failback do Azure, modifique o valor de saudação **DownloadThreadsPerVM**.
2. valor padrão de saudação é 4. Em uma rede de "sobreprovisionada", essas chaves do registro devem ser diferente dos valores padrão de saudação. Olá máximo é 32. Monitorar o tráfego toooptimize Olá valor.

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 4: planejar a rede](vmm-to-azure-walkthrough-network.md).
