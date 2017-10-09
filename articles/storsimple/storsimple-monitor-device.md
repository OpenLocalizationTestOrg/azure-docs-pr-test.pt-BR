---
title: aaaMonitor seu dispositivo StorSimple | Microsoft Docs
description: "Descreve como toouse Olá desempenho de e/s de toomonitor do serviço StorSimple Manager, utilização da capacidade, taxa de transferência de rede e desempenho do dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>Usar toomonitor de serviço do StorSimple Manager Olá seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
Você pode usar dispositivos específicos de toomonitor Olá de serviço StorSimple Manager em sua solução StorSimple. Você pode criar gráficos personalizados com base no desempenho de E/S, utilização da capacidade, taxa de transferência de rede e métricas de desempenho do dispositivo. 

Olá tooview informações para um dispositivo específico, em Olá portal clássico do Azure, o serviço StorSimple Manager Olá select de monitoramento. Clique em Olá **Monitor** guia e, em seguida, selecione na lista de saudação de dispositivos. Olá **Monitor** página contém Olá informações a seguir.

## <a name="io-performance"></a>Desempenho de E/S
**Desempenho de e/s** acompanha as métricas relacionadas toohello número de leitura e gravação operações entre iSCSI Olá interfaces do iniciador no servidor de host de saudação e dispositivo hello ou dispositivo hello e nuvem hello. Esse desempenho pode ser medido para um volume específico, um contêiner de volume específico ou todos os contêineres de volume.

gráfico de saudação abaixo mostra hello e/s de dispositivo de tooyour de iniciador Olá para todos os volumes de saudação para um dispositivo de produção. métricas de saudação plotadas são lidas e gravar bytes por segundo, ler e gravar operações de e/s por segundo e leitura e gravação latências.

![Desempenho de e/s de iniciador toodevice](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Para Olá mesmo dispositivo, as operações de e/s de saudação são plotadas para dados Olá Olá dispositivo toohello nuvem para todos os contêineres de volume de hello. Neste dispositivo, dados saudação estão apenas na camada linear hello e nada tem vazados toohello nuvem. Não há nenhuma operação de leitura / gravação que ocorrem por dispositivo toohello nuvem. Portanto, picos Olá no gráfico de saudação estão em um intervalo de 5 minutos que corresponde a frequência de toohello no qual pulsação Olá é verificada entre dispositivos hello e serviço de saudação. 

![Desempenho de e/s do dispositivo toocloud](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Para hello mesmo dispositivo, um instantâneo de nuvem foi obtido para dados de volume, começando às 2:00. Isso resultou em dados que fluem da saudação dispositivo toohello nuvem. Leituras gravações foram atendidas nuvem toohello durante esse período. Olá gráfico de e/s mostra um pico em Olá várias métricas correspondente toohello tempo quando o instantâneo de saudação foi criado. 

![Desempenho de e/s de dispositivo toocloud depois que o instantâneo de nuvem](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>Utilização da capacidade
**A utilização de capacidade** quantidade de toohello relacionados rastreia as métricas de espaço de armazenamento de dados que é usado pelo Olá volumes, contêineres de volume ou dispositivo. Você pode criar relatórios com base na utilização da capacidade de saudação do seu armazenamento primário, o armazenamento em nuvem ou o armazenamento do dispositivo. A utilização da capacidade pode ser medida em um volume específico, um contêiner de volume específico ou todos os contêineres de volume.

Olá primário, a nuvem e a capacidade de armazenamento do dispositivo podem ser descritas como se segue:

### <a name="primary-storage-capacity-utilization"></a>Utilização da capacidade de armazenamento primário
Esses gráficos mostram a quantidade de saudação de dados gravados tooStorSimple volumes antes de dados saudação está com eliminação de duplicação e compactados. Você pode exibir a utilização de armazenamento principal Olá por todos os volumes ou para um único volume.

Quando você exibir gráficos de utilização de capacidade Olá armazenamento primário volume para todos os volumes em relação a cada um dos volumes individuais hello e soma de backup de dados primário Olá ambos nesses casos, pode haver uma incompatibilidade entre dois números de saudação. Olá total principal de dados em todos os volumes podem não somar toohello soma total dos dados primários de saudação de volumes individuais hello. Isso pode ser devido tooone seguinte hello:

* **Dados de instantâneo incluídos para todos os volumes**: esse comportamento será visto somente se você estiver executando uma versão anterior à Atualização 3. dados primários de saudação mostrados para todos os volumes de saudação são a soma de saudação de dados primário de saudação para cada volume e dados de instantâneo de saudação. mostrado para um determinado volume de dados primário do Hello corresponde a quantidade de saudação do tooonly de dados alocados no volume de saudação (e não incluem dados de instantâneo de volume correspondente saudação).
  
    Isso também pode ser explicado por Olá equação a seguir:
  
    *Dados primários (todos os volumes) = Soma de (Dados primários (volume i) + Tamanho dos dados de instantâneo (volume i))*
  
    *onde, dados primário (volume i) = tamanho de dados primários alocados toovolume i*
  
    Se Olá instantâneos são excluídos por meio do serviço hello, exclusão Olá é feito assincronamente no plano de fundo de saudação. Ele pode levar algum tempo para Olá volume dados tamanho toobe atualizada após a exclusão do instantâneo hello. 
  
    Se executar o Update 3 ou posterior, dados de instantâneo de saudação não estão incluídos nos dados de volume hello. E utilização de saudação principal é calculada da seguinte maneira:
  
    *Dados primários (todos os volumes) = Soma de (Dados primários (volume i))
  
    *onde, dados primário (volume i) = tamanho de dados primários alocados toovolume i*
* **Volumes com monitoramento desabilitado incluídos em todos os volumes**: se você tiver volumes em seu dispositivo para o qual monitoramento está desativado, Olá dados para esses volumes individuais de monitoramento não estarão disponível em gráficos de saudação. No entanto, dados Olá para todos os volumes no gráfico de saudação incluem volumes Olá para o qual monitoramento está desativado. 
* **Excluir volumes com backups associados ao vivo que incluídas para todos os volumes**: se volumes que contêm dados de instantâneo são excluídos mas instantâneos Olá associado ainda existem, você poderá ver uma incompatibilidade.
* **Excluído volumes incluídos em todos os volumes**: em alguns casos, os volumes antigos podem existir mesmo que eles tenham sido excluídos. efeito de saudação de exclusão não é visto e dispositivo Olá pode mostrar menos capacidade disponível. É necessário toocontact Microsoft Support tooremove esses volumes.

Olá gráficos a seguir mostram utilização da capacidade de armazenamento principal de saudação de um dispositivo StorSimple antes e depois de um instantâneo de nuvem foi criado. Como esse é apenas dados de volume, um instantâneo de nuvem não deve alterar o armazenamento primário hello. Como você pode ver, o gráfico de saudação não mostra nenhuma diferença na utilização de capacidade principal hello como resultado de tirar um instantâneo de nuvem. instantâneo em nuvem Olá iniciado em aproximadamente 2:00 pm nesse dispositivo.

![Utilização da capacidade primária antes do instantâneo da nuvem](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![Utilização da capacidade primária após o instantâneo da nuvem](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

Se você estiver executando a atualização 2 ou superior, você pode dividir utilização da capacidade de armazenamento principal Olá por um volume individual, todos os volumes, todos os volumes em camadas e todos os volumes localmente afixados conforme mostrado abaixo. Dividindo por todos os localmente volumes afixados permitirá que você tooquickly verificar quanto da camada de saudação local é usado para cima.

![Utilização da capacidade principal para todos os volumes fixados localmente](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>Utilização da capacidade de armazenamento em nuvem
Esses gráficos mostram a quantidade de saudação do armazenamento em nuvem usado. Esses dados passam pela eliminação de duplicação e são compactados. O valor inclui instantâneos de nuvem que podem conter dados que não serão refletidos em nenhum volume primário e são mantidos para fins de retenção obrigatória ou herança. Você pode comparar hello primário e o consumo de armazenamento de nuvem figuras tooget uma ideia Olá de redução de dados de taxa, embora Olá número não ser exato. Olá gráficos a seguir mostram Olá nuvem armazenamento utilização da capacidade de um dispositivo StorSimple antes e depois de um instantâneo de nuvem foi criado. Hello instantâneo em nuvem iniciado em aproximadamente 2:00 pm no dispositivo e você pode ver a utilização da capacidade de nuvem Olá melhor o Olá mesmo tempo, aumentando de MB 5,73 too4.04 GB.

![Utilização da capacidade da nuvem antes do instantâneo da nuvem](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![Utilização da capacidade da nuvem após o instantâneo da nuvem](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>Utilização da capacidade de armazenamento do dispositivo
Esses gráficos mostram a utilização total da saudação para dispositivo hello, que será maior utilização de armazenamento principal porque ela inclui a camada do hello SSD linear. Essa camada contém uma quantidade de dados que já existe na Olá outras camadas do dispositivo. capacidade de saudação na camada do hello SSD linear é alternada para que quando novos dados chega, Olá antigo dados toohello movidos da camada de unidade de disco rígido (que é eliminação de duplicação e compactado) e subsequentemente toohello nuvem.

Ao longo do tempo, utilização da capacidade principal e a utilização da capacidade de dispositivo provavelmente aumentará juntos até dados saudação começam toobe hierárquico toohello nuvem. Nesse ponto, utilização da capacidade de dispositivo Olá provavelmente começará tooplateau, mas a utilização da capacidade principal de saudação aumentará à medida que mais dados são gravados.

Olá gráficos a seguir mostram utilização da capacidade de armazenamento principal de saudação de um dispositivo StorSimple antes e depois de um instantâneo de nuvem foi criado. instantâneo em nuvem Olá iniciada às 2:00 e utilização da capacidade de dispositivo Olá iniciadas diminuindo nesse momento. utilização da capacidade de armazenamento de dispositivo Olá desligou do GB 11.58 too7.48 GB. Isso indica que provavelmente hello dados não compactados na camada SSD linear de saudação foi com eliminação de duplicação, compactados e movidos para a camada HDD hello. Observe que, se o dispositivo de saudação já tem uma grande quantidade de dados em Olá SSD e níveis de unidade de disco rígido, você poderá não ver essa diminuição. Neste exemplo, o dispositivo Olá tem uma pequena quantidade de dados.

![Utilização da capacidade do dispositivo antes do instantâneo da nuvem](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![Utilização da capacidade do dispositivo após o instantâneo da nuvem](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>Taxa de transferência de rede
**Taxa de transferência de rede** quantidade de toohello relacionados de métricas de faixas de dados transferidos de saudação rede interfaces do iniciador iSCSI no servidor de host de saudação e dispositivo hello e entre o dispositivo hello e nuvem hello. Você pode monitorar esta métrica para cada uma das interfaces de rede iSCSI Olá em seu dispositivo.

Olá gráficos Mostrar Olá rede taxa de transferência para hello Data 0 e 4 de dados, ambas as interfaces de rede 1 GbE em seu dispositivo a seguir. Neste exemplo, Dado 0 estava habilitado para nuvem, enquanto Dado 4 estava habilitado para iSCSI. Você pode ver dois Olá de entrada e Olá o tráfego de saída para seu dispositivo StorSimple. a linha reta Olá no gráfico de saudação inicial de 3:24 pm é devido toohello fatos que podemos coletar dados somente a cada 5 minutos e deve ser ignorados. 

![Taxa de transferência de rede para Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Taxa de transferência de rede para Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>Desempenho do dispositivo
**Desempenho do dispositivo** acompanha as métricas relacionadas toohello o desempenho do seu dispositivo. Olá gráfico a seguir mostra estatísticas de utilização de CPU Olá para um dispositivo em produção.

![Utilização da CPU do dispositivo](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar o painel de dispositivo de serviço do StorSimple Manager Olá](storsimple-device-dashboard.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

