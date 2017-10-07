---
title: "dispositivo da série aaaUse StorSimple 8000 resumo | Microsoft Docs"
description: "Descreve o dispositivo de serviço de Gerenciador de dispositivos de StorSimple Olá resumo e como toouse-tooview as métricas de armazenamento e iniciadores conectados e localizar Olá número de série e o IQN."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a>Usar Olá dispositivo resumo no serviço do Gerenciador de dispositivos de StorSimple

## <a name="overview"></a>Visão geral
folha de resumo Olá StorSimple dispositivo fornece uma visão geral das informações de um dispositivo StorSimple específico, em contraste toohello serviço folha resumida, que fornece informações sobre todos os dispositivos de saudação incluídos em sua solução do Microsoft Azure StorSimple.

folha de resumo de dispositivo Olá fornece uma exibição resumida de um dispositivo da série StorSimple 8000 que está registrado com um determinado StorSimple Gerenciador de dispositivos, realçando os problemas de dispositivos que precisam de atenção do administrador do sistema. Este tutorial apresenta a folha de resumo de dispositivo hello, explica a função e o conteúdo de saudação e descreve Olá tarefas que você pode executar com esta folha.

folha de resumo de dispositivo Olá exibe Olá informações a seguir:

![Folha de resumo do dispositivo](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a>Barra de comandos de gerenciamento

Na folha de dispositivo do StorSimple Olá, você verá opções de saudação para gerenciar seu dispositivo StorSimple. Você ver os comandos de gerenciamento de saudação na superior de saudação da folha de saudação e no lado esquerdo da saudação. Use essas opções tooadd compartilhamentos ou volumes, ou atualizar ou failover de seu dispositivo.

![Barra de comandos de gerenciamento](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a>Conceitos básicos

área do essentials Olá captura algumas das propriedades de saudação importantes, como, status hello, modelo, IQN de destino e versão do software hello. 

![Conceitos básicos do dispositivo](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a>Monitoramento

* Olá **alertas** lado a lado fornece um instantâneo de todos os alertas ativos de saudação do seu dispositivo, agrupado por severidade do alerta.

    ![Bloco de alerta](./media/storsimple-8000-device-dashboard/device-summary4.png)

    Clique em Olá bloco tooopen Olá **alertas** folha e depois clique em um indivíduo alerta tooview mais detalhes sobre esse alerta, incluindo as ações recomendadas. Você também pode limpar o alerta de saudação se Olá problema foi resolvido.

    ![Clique no bloco de alerta](./media/storsimple-8000-device-dashboard/device-summary10.png)

* Olá **Status e integridade** lado a lado fornece ideias sobre a integridade dos componentes de hardware Olá para um dispositivo, incluindo status de saudação do dispositivo. status de saudação do dispositivo pode ser tooset offline, online, desativado ou pronto para cima.

    ![Bloco de status e integridade](./media/storsimple-8000-device-dashboard/device-summary5.png)

* Olá **Volumes** lado a lado fornece um resumo do número de saudação de volumes no seu dispositivo agrupados por status.

    ![Bloco Volumes](./media/storsimple-8000-device-dashboard/device-summary6.png)

    Clique em Olá bloco tooopen Olá **Volumes** folha e, em seguida, clique em um volume individual tooview ou modificar suas propriedades.
    
    ![Clique no bloco Volumes](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    Para obter mais informações, consulte como muito[gerenciar volumes](storsimple-8000-manage-volumes-u2.md).

* Em Olá **uso** gráfico, você pode exibir o armazenamento primário de saudação usado em seu dispositivo e o armazenamento em nuvem Olá consumida durante saudação últimos 7 dias, o padrão de saudação período de tempo.

     ![Bloco Uso](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     toochoose uma escala de tempo diferentes, use Olá **editar** opção no canto superior direito de saudação do gráfico de saudação.

     ![Editar gráfico de uso](./media/storsimple-8000-device-dashboard/device-summary12.png)

     Neste gráfico, você pode exibir métricas para armazenamento primário total hello (quantidade Olá dos dados gravados pelo dispositivo de tooyour hosts) e Olá total consumido por seu dispositivo em um período de tempo de armazenamento em nuvem.
  
     Nesse contexto, *armazenamento primário* refere-se a quantidade total de toohello dos dados gravados pelo host hello e podem ser divididos por tipo de volume: *armazenamento hierárquico primário* inclui tanto armazenadas localmente os dados e dados nuvem toohello em camadas. O *armazenamento primário fixado localmente* inclui apenas os dados armazenados localmente. *Armazenamento em nuvem*, em Olá outro lado, é uma medida da quantidade total de saudação dos dados armazenados na nuvem hello. Esse armazenamento inclui dados em camadas e backups. Olá dados armazenados na nuvem Olá com eliminação de duplicação e compactados, enquanto o armazenamento primário indica a quantidade de saudação do armazenamento usado antes de dados saudação está com eliminação de duplicação e compactados. (Você pode comparar esses dois números tooget uma ideia da taxa de compactação de saudação). Para o principal e o armazenamento na nuvem, Olá valores mostrados se baseiam no hello frequência de configuração de rastreamento. Por exemplo, se você escolher uma frequência de uma semana, Olá gráfico mostra dados de cada dia em Olá semana anterior.

     quantidade de saudação toosee de armazenamento em nuvem consumido por tempo, selecione Olá **armazenamento de nuvem usado** opção. toosee Olá total de armazenamento que foi gravado pelo host hello, selecione Olá **armazenamento primário em camadas, usado** e **LOCALMENTE FIXADOS armazenamento primário usado** opções. 
     Para obter mais informações, consulte [Use Olá toomonitor de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-monitor-device.md).


* Olá **capacidade** Olá lado a lado exibe Olá armazenamento primário provisionado e o restante em Olá dispositivo toohello relativo armazenamento total disponível para a mesma. **Provisionado** refere-se a quantidade de toohello de armazenamento preparado e alocado para uso, **restante** refere-se toohello capacidade que pode ser provisionada por este dispositivo restante. 

    ![Bloco Uso](./media/storsimple-8000-device-dashboard/device-summary8.png)

    Clique neste tooview lado a lado como capacidade Olá é provisionada em volumes fixados localmente e em camadas. Olá **camadas restantes** capacidade é a capacidade disponível de saudação que pode ser provisionada incluindo nuvem durante a saudação **restantes Local** é toothis dispositivo conectado à capacidade restante em discos de saudação de saudação.

    ![Clique no gráfico de uso](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre Olá [folha de resumo de serviço do StorSimple](storsimple-8000-service-dashboard.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

