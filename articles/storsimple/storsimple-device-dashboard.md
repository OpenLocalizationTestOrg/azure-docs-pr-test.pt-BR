---
title: "painel do dispositivo aaaUse Olá StorSimple Manager | Microsoft Docs"
description: "Descreve o painel de dispositivo de serviço do StorSimple Manager hello e como toouse-tooview as métricas de armazenamento e iniciadores conectados e localizar Olá número de série e o IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c213969-a385-461f-b698-78ef5b8a79cc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e213fc0a081c21b9d6b408a3dd845cc93a31e250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-dashboard-in-storsimple-manager-service"></a>Use o painel do dispositivo Olá no serviço StorSimple Manager  

## <a name="overview"></a>Visão geral
painel do dispositivo StorSimple Manager Olá fornece uma visão geral das informações de um dispositivo StorSimple específico, em contraste toohello serviço painel, que fornece informações sobre todos os dispositivos de saudação incluídos em sua solução do Microsoft Azure StorSimple.

![Página Painel de dispositivo](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

painel Olá contém Olá informações a seguir:

* **Área do gráfico** – você pode ver as métricas de armazenamento relevantes de saudação na área de gráfico de saudação na parte superior de saudação do painel de saudação. Neste gráfico, você pode exibir métricas para armazenamento primário total hello (quantidade Olá dos dados gravados pelo dispositivo de tooyour hosts) e Olá total consumido por seu dispositivo em um período de tempo de armazenamento em nuvem.
  
     Nesse contexto, *armazenamento primário* refere-se a quantidade total de toohello dos dados gravados pelo host hello e podem ser divididos por tipo de volume: *armazenamento hierárquico primário* inclui tanto armazenadas localmente os dados e dados nuvem em camadas toohello; *primário localmente afixado armazenamento* inclui apenas os dados armazenados localmente. *Armazenamento em nuvem*, em Olá outro lado, é uma medida da quantidade total de saudação dos dados armazenados na nuvem hello. Isso inclui backups e dados em camadas. Observe que os dados armazenados na nuvem Olá com eliminação de duplicação e compactados, enquanto o armazenamento primário indica a quantidade de saudação do armazenamento usado antes da data de saudação é eliminação de duplicação e compactado. (Você pode comparar esses dois números tooget uma ideia da taxa de compactação de saudação). Para o principal e o armazenamento na nuvem, Olá valores mostrados se baseará Olá frequência de configuração de rastreamento. Por exemplo, se você escolher uma frequência de uma semana, em seguida, Olá gráfico mostrará dados para cada dia em Olá semana anterior.
  
     Você pode configurar o gráfico de saudação da seguinte maneira:
  
  * quantidade de saudação toosee de armazenamento em nuvem consumido por tempo, selecione Olá **armazenamento de nuvem usado** opção. toosee Olá total de armazenamento que foi gravado pelo host hello, selecione Olá **armazenamento primário em camadas, usado** e **LOCALMENTE FIXADOS armazenamento primário usado** opções. Na ilustração hello, ambas as opções são selecionadas; Portanto, o gráfico de saudação mostra valores de armazenamento para armazenamento primário e de nuvem. Observe que qualquer armazenamento primário usado tooinstalling anterior atualização 2 é representado por Olá **armazenamento primário em camadas, usado** linha.
  * Use o menu suspenso de saudação no canto superior direito Olá Olá gráfico toospecify um período de tempo de 1 semana, 1 mês, 3 meses ou 1 ano. Observe que Olá gráfico de nível superior é atualizado apenas uma vez por dia e, portanto, refletirá Olá totais do dia anterior.
    
    Para obter mais informações, consulte [Use Olá toomonitor do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-monitor-device.md).
* **Visão geral de uso** – Olá **visão geral de uso** área, você pode ver quantidade Olá de armazenamento primário usado, quantidade de saudação do armazenamento provisionado e capacidade de armazenamento máximo Olá para seu dispositivo. Ao comparar esses uso números toohello máximo de armazenamento que está disponível, você pode ver rapidamente se você precisar de armazenamento adicionais tooobtain. Observe que esta visão geral é atualizado a cada 15 minutos e, por causa da diferença de saudação na frequência de atualização, pode mostrar números diferentes daqueles mostrados na Olá área do gráfico acima, que é atualizada diariamente. Para obter mais informações, consulte [Use Olá toomonitor do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-monitor-device.md).
* **Alertas** – hello **alertas** área contém uma visão geral de alertas de saudação para seu dispositivo. Alertas são agrupados por severidade e é fornecida uma contagem do número de saudação de alertas em cada nível de severidade. Clicando em alerta Olá gravidade abre uma exibição em escopo de saudação alertas tooshow guia que você Olá apenas alertas desse nível de gravidade para este dispositivo.
* **Trabalhos** – hello **trabalhos** área mostra Olá resultado da atividade de trabalho recente. Isso pode lhe garantir que o sistema hello está funcionando conforme o esperado ou pode permitir que você sabe que precisa de uma ação corretiva tootake. toosee obter mais informações sobre trabalhos concluídos recentemente, clique **trabalhos bem-sucedidos nas Olá últimas 24 horas**.
* Olá **visão rápida** área Olá direita do painel Olá fornece informações úteis como modelo do dispositivo, número de série, status, descrição e o número de volumes.

Você também pode configurar failover e exibir iniciadores conectados do painel do dispositivo hello.

Olá tarefas comuns que podem ser executadas nesta página são:

* Exibir iniciadores conectados
* Localizar o número de série do dispositivo Olá
* Localizar o IQN de destino do dispositivo Olá

## <a name="view-connected-initiators"></a>Exibir iniciadores conectados
Você pode exibir os iniciadores iSCSI Olá que estão conectados tooyour dispositivo clicando Olá **Exibir iniciadores conectados** link fornecido na Olá **visão rápida** área do painel do dispositivo. Esta página fornece uma listagem tabular de iniciadores Olá que se conectou com êxito o dispositivo tooyour. Para cada iniciador, você pode ver:

* Olá iSCSI IQN (nome qualificado) do hello conectado iniciador.
* nome de saudação do registro de controle de acesso hello (ACR) que permite esse iniciador conectado.
* endereço IP de saudação do hello conectado iniciador.
* Olá interfaces de rede que iniciador Olá é conectado tooon seu dispositivo de armazenamento. Elas podem variar de dados 0 tooDATA 5.
* Todos os volumes Olá Olá iniciador conectado é permitido tooaccess de acordo com a configuração de ACR atual toohello.

Se você vir iniciadores inesperados nessa lista ou não vir Olá esperado aqueles, examine a configuração de ACR. Um máximo de 512 iniciadores pode conectar o dispositivo tooyour.

## <a name="find-hello-device-serial-number"></a>Localizar o número de série do dispositivo Olá
Número de série do dispositivo Olá talvez seja necessário quando você configura o Microsoft Multipath i/o (MPIO) no dispositivo de saudação. Execute Olá após o número de série do dispositivo do etapas toofind hello.

#### <a name="toofind-hello-device-serial-number"></a>número de série do dispositivo toofind Olá
1. Navegue muito**dispositivos** > **painel**.
2. No painel direito de saudação do painel Olá, localize Olá **visão rápida** área.
3. Role para baixo e localize o número de série de saudação.

## <a name="find-hello-device-target-iqn"></a>Localizar o IQN de destino do dispositivo Olá
Talvez seja necessário IQN de destino do dispositivo hello quando você configura Olá Challenge Handshake Authentication Protocol (CHAP) no seu dispositivo StorSimple. Execute Olá etapas IQN de destino do dispositivo toofind Olá a seguir.

### <a name="toofind-hello-device-target-iqn"></a>IQN de destino do dispositivo do toofind Olá
1. Navegue muito**dispositivos** > **painel**.
2. No painel direito de saudação do painel Olá, localize Olá **visão rápida** área.
3. Role para baixo e localize o IQN de destino hello.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre Olá [painel de serviço do Gerenciador de StorSimple](storsimple-service-dashboard.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).

