---
title: "aaaPlan capacidade e dimensionamento para VMware tooAzure de replicação com o Azure Site Recovery | Microsoft Docs"
description: "Usar essa capacidade de tooplan de artigo e o dimensionamento ao replicar máquinas virtuais do VMware tooAzure com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 551533ab7090d85c216be242ea92781deb8287ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-vmware-tooazure-replication"></a>Etapa 3: Planejar a capacidade e dimensionamento de replicação do VMware tooAzure

Use este toofigure artigo planejamento de capacidade e dimensionamento, quando a replicação de máquinas virtuais do VMware no local e tooAzure de servidores físicos com [do Azure Site Recovery](site-recovery-overview.md).

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="how-do-i-start-capacity-planning"></a>Como iniciar o planejamento de capacidade?

Coletar informações sobre seu ambiente de replicação e em seguida, planeje a capacidade usando essas informações, junto com as considerações de saudação realçados neste artigo.


## <a name="gather-information"></a>Coletar informações

1. Baixar Olá [ferramenta de implantação Planejador](https://aka.ms/asr-deployment-planner) para replicação de VMware.
2. [Leia este artigo](site-recovery-deployment-planner.md) toounderstand como toorun Olá ferramenta.
3. Usando a ferramenta Olá você coletar informações sobre VMs compatíveis e incompatíveis, discos por máquina virtual, e rotatividade de dados por disco. ferramenta Olá também aborda os requisitos de largura de banda de rede e hello Azure infraestrutura necessária para failover de teste e de replicação com êxito.

## <a name="replication-considerations"></a>Considerações sobre a replicação

Observe essas considerações antes de iniciar a implantação:

**Componente** | **Detalhes** |
--- | --- | ---
**Replicação** | **Taxa de alteração diária máxima:** um computador protegido só pode usar um servidor de processo e um servidor de processo único pode lidar com uma taxa de alteração diária até too2 TB. Portanto, 2 TB é máxima de dados diário Olá alterar taxa em que há suporte para um computador protegido.<br/><br/> **Taxa de transferência máxima:** um computador replicado pode pertencer tooone conta de armazenamento do Azure. Uma conta de armazenamento padrão pode lidar com um máximo de 20.000 solicitações por segundo, e é recomendável que você mantenha o número de saudação de operações de entrada/saída por segundo (IOPS) em um too20 da máquina de origem, 000. Por exemplo, se você tiver uma máquina de origem com 5 discos, e cada disco gera 120 IOPS (tamanho de 8K) no computador de origem hello, em seguida, ele será em hello Azure por limite de IOPS de disco de 500. (o número de saudação de contas de armazenamento necessária é máquina de origem total toohello igual IOPS, dividida por 20.000.)

## <a name="configuration-server-capacity"></a>Capacidade do servidor de configuração

servidor de configuração de saudação deve ser capacidade taxa de alteração diária toohandle capaz de saudação em todas as cargas de trabalho em execução em computadores protegidos e precisa toocontinuously de largura de banda suficiente replicar dados tooAzure armazenamento.

Como uma prática recomendada, localize o servidor de configuração de saudação no hello mesma rede e o segmento de LAN Olá máquinas que você deseja tooprotect. Ela pode estar localizada em uma rede diferente, mas as máquinas que você deseja tooprotect devem ter tooit de visibilidade de rede 3 de camada.

## <a name="sizing-recommendations"></a>Recomendações de dimensionamento

tabela de saudação resume as recomendações de dimensionamento com base na CPU.

**CPU** | **Memória** | **Tamanho do disco de cache** | **Taxa de alteração de dados** | **Computadores protegidos**
--- | --- | --- | --- | ---
8 vCPUs (2 soquetes * 4 núcleos a 2,5 GHz) | 16 GB | 300 GB | 500 GB ou menos | Replique menos de 100 computadores.
12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz) | 18 GB | 600 GB | 500 GB too1 TB | Replique entre 100 e 150 computadores.
16 vCPUs (2 soquetes * 8 núcleos @ 2,5 GHz) | 32 GB | 1 TB | 1 TB too2 TB | Replique entre 150 e 200 computadores.
Implantar outro servidor de processo | | | > 2 TB | Implante servidores de processo adicional se você estiver replicando mais de 200 máquinas, ou se alterar dados diários Olá taxa excede 2 TB.

Em que:

* Cada computador de origem é configurado com 3 discos de 100 GB.
* Usamos armazenamento de benchmark de 8 unidades SAS de 10 K de RPM, com RAID 10, para as medidas do disco de cache.

## <a name="process-server-capacity"></a>Capacidade do servidor em processo


servidor de processo Olá recebe dados de replicação de computadores protegidos e otimiza o com o cache, a compactação e criptografia. Em seguida, ele envia Olá dados tooAzure.

- máquina de servidor de processo Olá deve ter tooperform de recursos suficientes essas tarefas.
- primeiro servidor de processo Olá é instalado por padrão no servidor de configuração de saudação. Você pode implantar tooscale de servidores de processo adicional em seu ambiente.
- servidor de processo Olá usa um cache com base em disco. Use um disco de cache separado de 600 GB ou mais alterações de dados de toohandle armazenadas no evento de saudação de um afunilamento de rede ou uma interrupção.
- Se você precisa de mais de 200 máquinas tooprotect ou taxa de alteração diária Olá é maior que 2 TB, você pode adicionar carga do processo servidores toohandle Olá replicação. tooscale-out, você pode:
    - Aumente o número de saudação de servidores de configuração. Por exemplo, você pode proteger as máquinas too400 com dois servidores de configuração.
    - Adicionar mais servidores de processo e usar esse servidor de configuração Olá toohandle tráfego em vez de (ou além).


### <a name="example-process-server-scaling"></a>Dimensionamento de exemplo do servidor em processo

Olá, a tabela a seguir descreve um cenário em que:

* Você não estiver planejando o servidor de configuração de saudação toouse como um servidor de processo.
* Você configurou um servidor de processo adicional.
* Você configurou o servidor em processo adicionais de máquinas virtuais protegidas toouse hello.
* Cada computador de origem protegido é configurado com três discos de 100 GB cada.

**Servidor de configuração** | **Servidor de processo adicional** | **Tamanho do disco de cache** | **Taxa de alteração de dados** | **Computadores protegidos**
--- | --- | --- | --- | ---
8 vCPUs (2 soquetes * 4 núcleos a 2,5 GHz), 16 GB de memória | 4 vCPUs (2 soquetes * 2 núcleos a 2,5 GHz), 8 GB de memória | 300 GB | 250 GB ou menos | Replicar 85 computadores ou menos.
8 vCPUs (2 soquetes * 4 núcleos a 2,5 GHz), 16 GB de memória | 8 vCPUs (2 soquetes * 4 núcleos a 2,5 GHz), 12 GB de memória | 600 GB | 250 GB too1 TB | Replique entre 85 e 150 computadores.
12 vCPUs (2 soquetes * 6 núcleos a 2,5 GHz), 18 GB de memória | 12 vCPUs (2 soquetes * 6 núcleos a 2,5 GHz), 24 GB de memória | 1 TB | 1 TB too2 TB | Replique entre 150 e 225 computadores.

forma Olá no qual você dimensionar seus servidores depende de sua preferência para um modelo de escala vertical ou expansão.  Você pode escalar verticalmente implantando alguns servidores de processo e de configuração de alto nível ou escalar horizontalmente implantando mais servidores com poucos recursos. Por exemplo, se você precisar 220 máquinas tooprotect, você pode fazer Olá seguinte:

* Configure o servidor de configuração de saudação com 12 vCPU, 18 GB de memória e um servidor de processo adicional com 12 vCPU, 24 GB de memória. Configure servidor de processo adicional do máquinas protegidas toouse Olá somente.
* Configure dois servidores de configuração (2 x 8 de vCPU, 16 GB de RAM) e dois servidores de processo adicional (1x8 vCPU e máquinas [220] do 4 vCPU x 1 toohandle 135 + 85). Configure computadores protegidos toouse Olá processo adicional somente os servidores.

## <a name="deploy-additional-process-servers"></a>Implantar servidores de processo adicionais

Siga essas tooset instruções um servidor de processo adicional. Depois de configurar o servidor de saudação, migrar fonte máquinas toouse-lo.

1. Em **servidores de recuperação de Site**, clique em servidor de configuração de hello > **+ servidor de processo**.
2. Em **Tipo de servidor**, clique em **Servidor de processo (local)**.

    ![Servidor de processo](./media/vmware-walkthrough-capacity/migrate-ps2.png)
3. Baixe arquivo de configuração do Site Recovery unificado hello.
4. Executar o servidor de processo do programa de instalação tooinstall hello e registrá-lo no cofre hello.
5. Em **antes de começar a**, selecione **adicionar tooscale de servidores de processo adicional implantação**.
6. Em **detalhes do servidor de configuração**, especifique o endereço IP hello saudação do servidor de configuração e Olá frase secreta. Se você não tem senha hello, obtenha executando **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** no servidor de configuração de saudação.

    ![Servidor de configuração](./media/vmware-walkthrough-capacity/add-ps2.png)
7. Conclua o restante da saudação da instalação de saudação do mesmo modo que você fez quando você configura o servidor de configuração de saudação.

### <a name="migrate-machines-toouse-hello-process-server"></a>Migrar o servidor de processo máquinas toouse Olá

1. Em **configurações** > **servidores de recuperação de Site**, clique em servidor de configuração de hello > **processar servidores**.
2. Servidor de processo Olá com o botão direito em uso no momento > **comutador**.

    ![Alternar o servidor de processo](./media/vmware-walkthrough-capacity/migrate-ps3.png)
3. Em **selecione servidor de processo**, selecione o servidor de processo Olá desejado toouse e selecione Olá VMs nesse servidor de saudação tratará.
4. Clique o ícone de informações de saudação. toohelp você fazer as decisões de carga, Olá médio espaço que é necessário tooreplicate cada VM toohello novo servidor de processo selecionado é exibido.
5. Clique em Olá marca de seleção toostart replicação toohello novo servidor de processo.

## <a name="control-network-bandwidth"></a>Controlar largura de banda da rede

Depois de executar [ferramenta de implantação Planejador Olá](site-recovery-deployment-planner.md) largura de banda de saudação toocalculate é necessário para replicação (a replicação inicial hello e, em seguida, delta), você pode controlar a quantidade de saudação de largura de banda usada para replicação usando duas opções:

* **Limitação da largura de banda**: tráfego VMware que replica tooAzure passa por um servidor de processo específico. Você pode reduzir a largura de banda em computadores de saudação em execução como servidores de processo.
* **Influenciam a largura de banda**: você pode influenciar a largura de banda de saudação usada para replicação usando duas chaves do registro:
  * Olá **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** valor de registro Especifica o número de saudação de threads que são usados para a transferência de dados (replicação inicial ou delta) de um disco. Um valor mais alto aumenta a largura de banda de rede Olá usada para replicação.
  * Olá **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** Especifica o número de saudação de threads usados para transferência de dados durante o failback.

### <a name="throttle-bandwidth"></a>Restringir a largura de banda

1. Abra Olá snap-in de MMC de Backup do Azure em atuar de máquina hello como servidor de processo hello. Por padrão, um atalho para o Backup está disponível na área de trabalho hello, ou em Olá pasta a seguir: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Olá snap-in, clique em **alterar propriedades**.
3. Em Olá **limitação** guia, selecione **habilitar limitação para operações de backup do uso de largura de banda de internet**.
4. Definir limites de Olá de trabalho e de folga horas. Intervalos válidos são de 512 Mbps de too102 Kbps por segundo.

    ![Restrição](./media/vmware-walkthrough-capacity/throttle2.png)

Você também pode usar o hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação. Veja um exemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que nenhuma limitação é necessária.

### <a name="influence-network-bandwidth-for-a-vm"></a>Influenciar largura de banda da rede para uma VM

1. No registro de saudação VM, vá muito**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tráfego de largura de banda de saudação tooinfluence em um disco de replicação, modifique o valor de saudação do **UploadThreadsPerVM**, ou criar a chave de saudação se ele não existir.
   * largura de banda tooinfluence Olá para o tráfego de failback do Azure, modifique o valor de saudação do **DownloadThreadsPerVM**.
2. valor padrão de saudação é 4. Em uma rede sobreprovisionada, essas chaves do Registro devem ser modificadas. Olá máximo é 32. Monitorar o tráfego toooptimize Olá valor.




## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 4: planejar a rede](vmware-walkthrough-network.md).
