---
title: "resultados de aaaTest para replicação do Hyper-V entre sites com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo fornece informações sobre o teste de desempenho para replicação de tooon local no local de VMs Hyper-V usando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 96ff404f-0d88-43fa-a00b-2dffde93d192
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 3b37542fc88e0af05e05cee78183983667618816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test-results-for-on-premises-tooon-premises-hyper-v-replication-with-site-recovery"></a>Resultados de teste para replicação de Hyper-V local tooon local com a recuperação de Site

Você pode usar o Microsoft Azure Site Recovery tooorchestrate e gerenciar a replicação de máquinas virtuais e servidores físicos tooAzure ou datacenter secundário tooa. Este artigo fornece resultados de saudação do teste de desempenho que fizemos ao replicar máquinas virtuais Hyper-V entre dois locais datacenters.

## <a name="test-goals"></a>Objetivos do teste

meta de saudação do teste foi tooexamine como o Azure Site Recovery executa durante a replicação de estado estacionário. A replicação em estado estável ocorre após a conclusão da replicação inicial das máquinas virtuais e durante a sincronizando das alterações delta. É importante toomeasure desempenho usando o estado constante porque é Olá o estado em que a maioria das máquinas virtuais permanecem a menos que ocorram interrupções inesperadas.

implantação de teste Olá consistia em dois sites locais com um servidor VMM em cada site. Esta implantação de teste é típica de uma implantação de escritório de sede/filial, com sede agindo como o site primário hello e filial hello como o site secundário ou de recuperação de saudação.

## <a name="what-we-did"></a>O que fizemos

Aqui está o que no teste de saudação passamos:

1. Criação de máquinas virtuais usando modelos do VMM.
2. Inicialização das máquinas virtuais e captura das métricas de desempenho de linha de base durante 12 horas.
3. Criação de nuvens em servidores VMM primário e de recuperação.
4. Configuração da proteção da nuvem no Azure Site Recovery, incluindo o mapeamento de nuvens de origem e de recuperação.
5. Habilitar a proteção para máquinas virtuais e permitir que eles toocomplete a replicação inicial.
6. Espera de algumas horas para a estabilização do sistema.
7. Captura de métricas de desempenho durante 12 horas, garantindo que todas as máquinas virtuais permaneçam em um estado de replicação esperado durante essas 12 horas.
8. Medir delta Olá entre métricas de desempenho de linha de base de saudação e Olá métricas de desempenho de replicação.


## <a name="primary-server-performance"></a>Desempenho do servidor primário

* Réplica do Hyper-V arquivo de log de tooa alterações com sobrecarga mínima de armazenamento no servidor primário Olá controla de forma assíncrona.
* Réplica do Hyper-V utiliza memória automantido cache toominimize IOPS sobrecarga para o rastreamento. Ele armazena gravações toohello VHDX em memória e liberações-los para o arquivo de log Olá Olá antes de tempo que o log Olá é enviado toohello site de recuperação. Uma limpeza de disco também acontecerá se Olá gravações atingirem um limite predeterminado.
* gráfico de saudação abaixo mostra a sobrecarga IOPS de estado estacionário Olá para replicação. Podemos ver que Olá tooreplication vencimento sobrecarga de IOPS é aproximadamente 5% que é muito baixa.

![Resultados primários](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

Réplica do Hyper-V utiliza memória no desempenho do disco de toooptimize Olá servidor primário. Conforme mostrado na Olá gráfico a seguir, a sobrecarga de memória em todos os servidores no cluster primário Olá é marginal. Olá sobrecarga de memória mostrada é a porcentagem de saudação de memória usada pela replicação em comparação comparada memória de toohello total instalada no servidor do Hyper-V hello.

![Resultados primários](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

A Réplica do Hyper-V tem uma sobrecarga mínima de CPU. Conforme mostrado no gráfico de hello, sobrecarga de replicação está no intervalo de saudação do % 2 a 3.

![Resultados primários](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>Desempenho do servidor secundário (recuperação)

Réplica do Hyper-V usa uma pequena quantidade de memória no número de Olá Olá recuperação servidor toooptimize de operações de armazenamento. gráfico de Olá resume o uso de memória Olá no servidor de recuperação de saudação. Olá sobrecarga de memória mostrada é a porcentagem de saudação de memória usada pela replicação em comparação comparada memória de toohello total instalada no servidor do Hyper-V hello.

![Resultados secundários](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

quantidade de saudação de operações de e/s no site de recuperação de saudação é uma função do número de saudação de operações de gravação no site primário hello. Vamos examinar a operações de e/s total Olá no site de recuperação de saudação em comparação com operações de e/s total hello e operações de gravação em um site primário hello. gráficos de saudação mostram esse total de Olá que IOPS no site de recuperação de saudação é

* Saudação de cerca de 1,5 vezes IOPS de gravação em Olá primário.
* Em torno 37% da saudação total de IOPS no site primário hello.

![Resultados secundários](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![Resultados secundários](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>Efeito na utilização da rede

Uma média de 275 Mb por segundo de largura de banda de rede foi usada entre hello primário e nós de recuperação (com compactação habilitada) em relação a uma largura de banda existente de 5 Gb por segundo.

![Resultados da utilização da rede](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>Efeito no desempenho da VM

Uma consideração importante é o impacto de saudação da replicação nas cargas de trabalho de produção em execução em máquinas virtuais de saudação. Se o site primário hello está configurado adequadamente para replicação, não deve haver qualquer impacto em cargas de trabalho de saudação. Mecanismo de controle de leve da réplica do Hyper-V garante que as cargas de trabalho em execução em máquinas virtuais de saudação não sejam afetadas durante a replicação de estado estacionário. Isso é ilustrado no hello gráficos a seguir.

Este gráfico mostra o IOPS realizado por máquinas virtuais executando cargas de trabalho diferentes, antes e depois da habilitação da replicação. Você pode observar que não há nenhuma diferença entre hello dois.

![Resultados do efeito de réplica](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

Olá gráfico a seguir mostra taxa de transferência de saudação de máquinas virtuais executando cargas de trabalho diferentes antes e depois que a replicação foi habilitada. Você pode observar que a replicação não tem impacto significativo.

![Efeitos da réplica dos resultados](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>Conclusão

resultados de saudação mostram claramente a Azure Site Recovery, juntamente com a réplica do Hyper-V, pode ser dimensionado com sobrecarga mínima para um cluster grande.  O Azure Site Recovery oferece implantação, replicação, gerenciamento e monitoramento simplificado. Réplica do Hyper-V fornece infraestrutura necessária Olá para dimensionamento de replicação com êxito. Para planejar uma implantação ideal, sugerimos que você baixe Olá [Planejador de capacidade de réplica do Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057).

## <a name="test-environment-details"></a>Detalhes do ambiente de teste

### <a name="primary-site"></a>Site primário

* site primário Olá tem um cluster com cinco servidores Hyper-V executando 470 máquinas virtuais.
* máquinas virtuais de saudação executar cargas de trabalho diferentes, e todos têm a proteção do Azure Site Recovery habilitada.
* O armazenamento para o nó de cluster Olá é fornecido por uma SAN iSCSI. Modelo – Hitachi HUS130.
* Cada servidor de cluster tem quatro placas de rede (NICs) de um Gbps cada.
* Duas das placas de rede Olá são rede privada de iSCSI conectado tooan e dois são rede empresarial externa de tooan conectado. Uma das redes externas Olá é reservada para comunicações de cluster apenas.

![Principais requisitos de hardware](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| Servidor | RAM | Modelo | Processador | Número de processadores | NIC | Software |
| --- | --- | --- | --- | --- | --- | --- |
| Servidores Hyper-V no cluster:  <br />ESTLAB-HOST11<br />ESTLAB-HOST12<br />ESTLAB-HOST13<br />ESTLAB-HOST14<br />ESTLAB-HOST25 |128ESTLAB-HOST25 tem 256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 a 2.20GHz |4 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + função Hyper-V |
| Servidor VMM |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>Site secundário (recuperação)

* site secundário Olá tem um cluster de failover de seis nós.
* O armazenamento para o nó de cluster Olá é fornecido por uma SAN iSCSI. Modelo – Hitachi HUS130.

![Principais especificações de hardware](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| Servidor | RAM | Modelo | Processador | Número de processadores | NIC | Software |
| --- | --- | --- | --- | --- | --- | --- |
| Servidores Hyper-V no cluster:  <br />ESTLAB-HOST07<br />ESTLAB-HOST08<br />ESTLAB-HOST09<br />ESTLAB-HOST10 |96 |Dell ™ PowerEdge ™ R720 |Intel(R) Xeon(R) CPU E5-2630 0 a 2.30GHz |2 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + função Hyper-V |
| ESTLAB-HOST17 |128 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 a 2.20GHz |4 | |Windows Server Datacenter 2012 R2 (x64) + função Hyper-V |
| ESTLAB-HOST24 |256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 a 2.20GHz |2 | |Windows Server Datacenter 2012 R2 (x64) + função Hyper-V |
| Servidor VMM |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="server-workloads"></a>Cargas de trabalho do servidor

* Para fins de teste, escolhemos as cargas de trabalho normalmente usadas em cenários de clientes empresariais.
* Usamos [IOMeter](http://www.iometer.org) com característica de carga de trabalho Olá resumida na tabela Olá para simulação.
* Todos os perfis do IOMeter são definidos padrões de gravação do pior caso de toosimulate toowrite bytes aleatórios para cargas de trabalho.

| Carga de trabalho | Tamanho de E/S (KB) | % de acesso | % de leitura | E/Ss pendentes | Padrão de E/S |
| --- | --- | --- | --- | --- | --- |
| Servidor de arquivos |48163264 |60%20%5%5%10% |80%80%80%80%80% |88888 |Todos 100% aleatórios |
| SQL Server (volume 1) SQL Server (volume 2) |864 |100%100% |70%0% |88 |100% aleatório 100% sequencial |
| Exchange |32 |100% |67% |8 |100% aleatório |
| Estação de trabalho/VDI |464 |66%34% |70%95% |11 |Ambos 100% aleatórios |
| Servidor de arquivos da Web |4864 |33%34%33% |95%95%95% |888 |Todos 75% aleatórios |

### <a name="vm-configuration"></a>Configuração da VM

* 470 máquinas virtuais no cluster primário hello.
* Todas as máquinas virtuais com disco VHDX.
* Máquinas virtuais executando cargas de trabalho resumidas na tabela de saudação. Todas foram criadas com modelos do VMM.

| Carga de trabalho | Nº de VMs | RAM mínima (GB) | RAM máxima (GB) | Tamanho de disco lógico (GB) por VM | IOPS máximo |
| --- | --- | --- | --- | --- | --- |
| SQL Server |51 |1 |4 |167 |10 |
| Exchange Server |71 |1 |4 |552 |10 |
| Servidor de arquivos |50 |1 |2 |552 |22 |
| VDI |149 |.5 |1 |80 |6 |
| Servidor Web |149 |.5 |1 |80 |6 |
| TOTAL |470 | | |96,83 TB |4108 |

### <a name="site-recovery-settings"></a>Configurações do Site Recovery

* O Azure Site Recovery foi configurado para proteção local tooon de local
* servidor do VMM Olá tem quatro nuvens configuradas, que contém servidores de cluster do Hyper-V hello e suas máquinas virtuais.

| Nuvem VMM primária | Máquinas virtuais na nuvem Olá protegidas | Frequência de replicação | Pontos de recuperação adicionais |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15 min |Nenhum |
| PrimaryCloudRpo30s |47 |30 segundos |Nenhum |
| PrimaryCloudRpo30sArp1 |47 |30 segundos |1 |
| PrimaryCloudRpo5m |235 |5 min |Nenhum |

### <a name="performance-metrics"></a>Métricas de desempenho

tabela Olá resume as métricas de desempenho de saudação e contadores que foram medidos na implantação de saudação.

| Métrica | Contador |
| --- | --- |
| CPU |\Processador(_Total)\% Tempo do processador |
| Memória disponível |\Memória\MBytes disponíveis |
| IOPS |\Disco físico(_Total)\Transferências do disco/seg |
| Operações de leitura da VM (IOPS)/seg |\Dispositivo de armazenamento virtual do Hyper-V (<VHD>)\Operações de leitura/Seg |
| Operações de gravação da VM (IOPS)/seg |\Dispositivo de armazenamento virtual do Hyper-V (<VHD>)\Operações de gravação/S |
| Taxa de transferência de leitura da VM |\Dispositivo de armazenamento virtual do Hyper-V (<VHD>)\Bytes de leitura/seg |
| Taxa de transferência de gravação da VM |\Dispositivo de armazenamento virtual do Hyper-V (<VHD>)\Bytes de gravação/seg |

## <a name="next-steps"></a>Próximas etapas

[Configurar a replicação entre dois sites locais VMM](site-recovery-vmm-to-vmm.md)
