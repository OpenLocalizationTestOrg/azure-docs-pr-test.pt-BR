---
title: "aaaMonitor seu dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Descreve como Olá toouse Gerenciador de dispositivos do StorSimple serviço toomonitor uso, desempenho de e/s e utilização da capacidade."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a>Usar toomonitor de serviço do Gerenciador de dispositivos de StorSimple Olá seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
Você pode usar o hello Gerenciador de dispositivos do StorSimple service toomonitor específicos a dispositivos em sua solução StorSimple. Você pode criar gráficos personalizados com base no desempenho de e/s, utilização da capacidade, taxa de transferência de rede e métricas de desempenho do dispositivo e fixar o dashboard esses toohello. Para obter mais informações, vá muito[personalizar seu painel do portal](/articles/azure-portal/azure-portal-dashboards.md).

tooview Olá informações para um dispositivo específico, em Olá portal do Azure, selecione Serviço de Gerenciador de dispositivos de StorSimple hello. Na lista de saudação de dispositivos, selecione seu dispositivo e, em seguida, vá muito**Monitor**. Em seguida, você pode ver Olá **capacidade**, **uso**, e **desempenho** gráficos para o dispositivo selecionado hello.

## <a name="capacity"></a>Capacity
**Capacidade** rastreia Olá espaço provisionado e Olá restante no dispositivo de saudação. Olá capacidade restante é exibido como fixado localmente ou em camadas.

Olá provisionada e a capacidade restante é divididos por volumes fixados localmente e em camadas. Para cada volume, Olá provisionado capacidade e Olá capacidade em dispositivo Olá restante é exibida.

![Capacidade de E/S](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a>Uso
**Uso** quantidade de toohello relacionados rastreia as métricas de espaço de armazenamento de dados que é usado pelo Olá volumes, contêineres de volume ou dispositivo. Você pode criar relatórios com base na utilização da capacidade de saudação do seu armazenamento primário, o armazenamento em nuvem ou o armazenamento do dispositivo. A utilização da capacidade pode ser medida em um volume específico, um contêiner de volume específico ou todos os contêineres de volume.
Por padrão, o uso de saudação nas últimas 24 horas é relatado. Você pode editar sobre quais Olá uso é relatado selecionando de duração de Olá Olá gráfico toochange:
* Últimas 24 horas
* Últimos 7 dias
* Últimos 30 dias
* Últimos 90 dias
* Ano passado


Olá primário, nuvem e armazenamento local usado podem ser descritas como se segue:

### <a name="primary-storage-usage"></a>Uso de armazenamento primário
Esses gráficos mostram a quantidade de saudação de dados gravados tooStorSimple volumes antes de dados saudação está com eliminação de duplicação e compactados. Você pode exibir o armazenamento primário de saudação usado por todos os volumes em um contêiner de volume ou para um único volume. armazenamento primário de saudação usado é dividido por hierárquico armazenamento primário usado e primário armazenamento localmente afixado usado.

Olá gráficos a seguir mostram armazenamento primário hello, usado para um dispositivo StorSimple antes e depois de um instantâneo de nuvem foi criado. Como esse é apenas dados de volume, um instantâneo de nuvem não deve alterar o armazenamento primário hello. Como você pode ver, o gráfico de saudação não mostra nenhuma diferença no hello em camadas ou localmente afixado armazenamento primário usado como resultado de tirar um instantâneo de nuvem. instantâneo em nuvem Olá iniciado em aproximadamente 11:50 pm nesse dispositivo.

![Utilização da capacidade primária após o instantâneo da nuvem](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

Se executar e/s no dispositivo StorSimple do hello host conectado tooyour agora, você verá um aumento no armazenamento em camadas principal ou primário localmente fixados dependendo do armazenamento usado após quais volumes (em camadas ou localmente afixado) você gravar dados hello. Aqui estão os gráficos de uso de armazenamento primário Olá para um dispositivo StorSimple. Neste dispositivo, host de StorSimple Olá iniciado atendendo grava em cerca de 2:30 pm em um volume em camadas no dispositivo de saudação. Você pode ver o pico de saudação em Olá bytes/s de gravação correspondente toohello e/s em execução no host de saudação.

![Desempenho quando a E/S está em execução em volumes em camadas](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

Se você observar Olá hierárquico armazenamento primário usado, que tem sido ativado enquanto uso localmente afixado Olá primário permanece inalterado, pois há nenhuma gravação atendidas volumes toohello fixado localmente no dispositivo de saudação.

![Utilização da capacidade primária quando a E/S está em execução nos volumes em camada](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

Se você estiver executando a atualização 3 ou superior, você pode dividir utilização da capacidade de armazenamento principal Olá por um volume individual, todos os volumes, todos os volumes em camadas e todos os volumes localmente afixados conforme mostrado abaixo. Dividindo por todos os localmente volumes afixados permitirá que você tooquickly verificar quanto da camada de saudação local é usado para cima.

![Utilização da capacidade primária para todos os volumes em camadas](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![Utilização da capacidade principal para todos os volumes fixados localmente](./media/storsimple-8000-monitor-device/monitor-usage4.png)

Ainda mais, você pode clicar em cada um dos volumes de saudação na lista de saudação e ver o uso correspondente de saudação.

![Utilização da capacidade principal para todos os volumes fixados localmente](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a>Uso do armazenamento em nuvem
Esses gráficos mostram a quantidade de saudação do armazenamento em nuvem usado. Esses dados passam pela eliminação de duplicação e são compactados. O valor inclui instantâneos de nuvem que podem conter dados que não serão refletidos em nenhum volume primário e são mantidos para fins de retenção obrigatória ou herança. Você pode comparar hello primário e o consumo de armazenamento de nuvem figuras tooget uma ideia Olá de redução de dados de taxa, embora Olá número não ser exato.

Olá gráficos a seguir mostram utilização do armazenamento de nuvem de saudação de um dispositivo StorSimple quando um instantâneo foi tirado.

* instantâneo em nuvem Olá iniciado em aproximadamente 11:50 e no dispositivo e você pode ver que antes de instantâneo de nuvem hello, não havia nenhum armazenamento em nuvem usado. 
* Uma vez instantâneo em nuvem Olá concluído, utilização de armazenamento de nuvem Olá captura a 0.89 GB. 
* Enquanto o instantâneo em nuvem Olá estava em andamento, também há um pico correspondente no hello e/s do dispositivo toocloud.

    ![Utilização do armazenamento em nuvem antes do instantâneo de nuvem](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![Utilização do armazenamento em nuvem depois do instantâneo de nuvem](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![E/s de dispositivo toocloud durante um instantâneo de nuvem](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a>Uso do armazenamento local
Esses gráficos mostram a utilização total da saudação para dispositivo hello, que será mais do que o uso de armazenamento principal porque ela inclui a camada do hello SSD linear. Essa camada contém uma quantidade de dados que já existe na Olá outras camadas do dispositivo. capacidade de saudação na camada do hello SSD linear é alternada para que quando novos dados chega, Olá antigo dados toohello movidos da camada de unidade de disco rígido (que é eliminação de duplicação e compactado) e subsequentemente toohello nuvem.

Ao longo do tempo, o armazenamento primário usado e local de armazenamento usado provavelmente aumentará juntos até dados saudação começam toobe hierárquico toohello nuvem. Nesse ponto, o armazenamento local de saudação usado provavelmente começará tooplateau, mas o armazenamento primário de saudação usado aumentará à medida que mais dados são gravados.

Olá gráficos a seguir mostram armazenamento primário hello, usado para um dispositivo StorSimple quando um instantâneo foi tirado. instantâneo em nuvem Olá iniciada às 11:50 e armazenamento local Olá iniciadas diminuindo nesse momento. armazenamento local de saudação usado foi desativado de 1.445 GB too1.09 GB. Isso indica que provavelmente hello dados não compactados na camada SSD linear de saudação foi com eliminação de duplicação, compactados e movidos para a camada HDD hello. Observe que, se o dispositivo de saudação já tem uma grande quantidade de dados em Olá SSD e níveis de unidade de disco rígido, você poderá não ver essa diminuição. Neste exemplo, o dispositivo Olá tem uma pequena quantidade de dados.

![Utilização do armazenamento local depois do instantâneo de nuvem](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a>Desempenho
**Desempenho** acompanha as métricas relacionadas toohello número de leitura e gravação operações entre iSCSI Olá interfaces do iniciador no servidor de host de saudação e dispositivo hello ou dispositivo hello e nuvem hello. Esse desempenho pode ser medido para um volume específico, um contêiner de volume específico ou todos os contêineres de volume. Desempenho também inclui a utilização da CPU e a taxa de transferência de rede para Olá várias interfaces de rede em seu dispositivo.

### <a name="io-performance-for-initiator-toodevice"></a>Desempenho de e/s para o iniciador toodevice
gráfico de saudação abaixo mostra hello e/s de dispositivo de tooyour de iniciador Olá para todos os volumes de saudação para um dispositivo de produção. métricas de saudação plotadas são ler e gravar bytes por segundo. Também é possível elaborar um gráfico de E/S de leitura, gravação e pendente ou latências de leitura e de gravação.

![Desempenho de e/s para o iniciador toodevice](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a>Desempenho de e/s do dispositivo toocloud
Para Olá mesmo dispositivo, as operações de e/s de saudação são plotadas para dados Olá Olá dispositivo toohello nuvem para todos os contêineres de volume de hello. Neste dispositivo, dados saudação estão apenas na camada linear hello e nada tem vazados toohello nuvem. Não há nenhuma operação de leitura / gravação que ocorrem por dispositivo toohello nuvem. Portanto, picos Olá no gráfico de saudação estão em um intervalo de 5 minutos que corresponde a frequência de toohello no qual pulsação Olá é verificada entre dispositivos hello e serviço de saudação.

Para hello mesmo dispositivo, um instantâneo de nuvem foi obtido para dados de volume iniciando às 11:50. Isso resultou em dados que fluem da saudação dispositivo toohello nuvem. Gravações foram atendidas nuvem toohello durante esse período. gráfico de e/s de Olá mostra um pico em Olá Bytes/s de gravação correspondente toohello horário quando Olá instantâneo foi tirado.

![E/s de dispositivo toocloud durante um instantâneo de nuvem](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a>Taxa de transferência de rede para adaptadores de rede do dispositivo
**Taxa de transferência de rede** quantidade de toohello relacionados de métricas de faixas de dados transferidos de saudação rede interfaces do iniciador iSCSI no servidor de host de saudação e dispositivo hello e entre o dispositivo hello e nuvem hello. Você pode monitorar esta métrica para cada uma das interfaces de rede iSCSI Olá em seu dispositivo.

Olá seguintes gráficos Mostrar Olá rede taxa de transferência para Olá Data 0, 1 1 rede GbE em seu dispositivo, que era ambos nuvem habilitada (padrão) e o iSCSI habilitado. Neste dispositivo na 14 de junho em torno de 21: 00, dados foi em camadas para a nuvem de saudação (nenhuma nuvem instantâneos foram criados em que o tempo que tootiering de pontos, que está sendo Olá dados de saudação do mecanismo toomove em nuvem Olá) que resultou em e/s seja servido toohello nuvem. Há um pico correspondente no gráfico de taxa de transferência de rede Olá para hello mesmo tempo e a maioria do tráfego de rede de saudação é saída toohello nuvem.

![Taxa de transferência de rede para Data 0](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

Se observarmos o gráfico de taxa de transferência de interface Olá Data 1, interface que só foi habilitada com iSCSI de rede de 1 GbE outro, não houve praticamente nenhum tráfego de rede durante esse período.

![Taxa de transferência de rede para Data 1](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a>Utilização da CPU do dispositivo
**Utilização da CPU** acompanha as métricas relacionadas a CPU de toohello utilizada em seu dispositivo. Olá gráfico a seguir mostra estatísticas de utilização de CPU Olá para um dispositivo em produção.

![Utilização da CPU do dispositivo](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar o painel de dispositivo de serviço do Gerenciador de dispositivos de StorSimple Olá](storsimple-device-dashboard.md).
* Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-manager-service-administration.md).

