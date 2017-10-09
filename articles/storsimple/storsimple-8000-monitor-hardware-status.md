---
title: aaaStorSimple 8000 series componentes de hardware e status | Microsoft Docs
description: "Saiba como toomonitor Olá componentes de hardware do seu dispositivo StorSimple por meio do serviço do Gerenciador de dispositivos de StorSimple hello."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 85b398e4b1a6b8921792b8945331325940082eb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-hardware-components-and-status"></a>Usar componentes de hardware toomonitor do serviço de Gerenciador de dispositivos de StorSimple hello e status
## <a name="overview"></a>Visão geral
Este artigo descreve Olá vários componentes físicos e lógicos em seu dispositivo da série 8000 StorSimple local. Ele também explica como toomonitor Olá status do componente de dispositivo usando Olá **hardware e Status de integridade** folha em Olá serviço do Gerenciador de dispositivos do StorSimple.

Olá **hardware e Status de integridade** folha mostra o status do hardware Olá de todos os componentes de dispositivo do StorSimple Olá.

Na lista de saudação de componentes para 8100, há três seções descrevem:

* **Componentes compartilhados** – não fazem parte dos controladores hello, como unidades de disco, compartimento, componentes de PCM e temperatura de PCM, voltagem de linha e sensores de voltagem de linha.
* **Componentes do controlador 0** – componentes Olá que residem no controlador 0, como controlador, expansor SAS e o conector, sensores de temperatura do controlador e Olá várias interfaces de rede.
* **Componentes do controlador 1** – Olá componentes que constituem o controlador 1, similar toothose detalhado para o controlador 0.

Um dispositivo 8600 tem componentes adicionais que correspondem a toohello Extended Bunch de discos (compartimento EBOD). Na lista de saudação de componentes, há cinco seções. Desses, há três seções que contêm componentes Olá no compartimento primário hello e são idêntico toohello descritos para 8100. Há duas seções adicionais para Olá compartimento EBOD que descrevem:

* **Componentes do controlador EBOD 0** – Olá componentes que residem no compartimento do EBOD 0, como o controlador do EBOD hello, sensores de temperatura do controlador e conector e Expansor SAS.
* **Componentes de 1 do controlador EBOD** – Olá componentes que constituem o compartimento EBOD 1, similar toothose detalhados para o compartimento do EBOD 0.
* **Componentes compartilhados do compartimento do EBOD** – componentes de saudação presentes no compartimento do EBOD hello e PCM que não fazem parte de saudação do controlador do EBOD.

> [!NOTE]
> **status do hardware Olá não está disponível para um dispositivo de nuvem do StorSimple (8010/8020).**


## <a name="monitor-hello-hardware-status"></a>Monitorar o status do hardware Olá
Execute Olá status do hardware Olá etapas tooview de um componente de dispositivo a seguir:

1. Navegue muito**dispositivos**, selecione um dispositivo StorSimple específico. Vá muito**Monitor > integridade do Hardware**.

    ![](./media/storsimple-8000-monitor-hardware-status/hw-health1.png)

2. Localizar Olá **componentes de Hardware** seção e escolha entre componentes disponíveis hello. Simplesmente clique Olá componente Rótulo tooexpand Olá lista e exibir o status de saudação de saudação vários componentes do dispositivo. Consulte Olá [lista de componente detalhado para o compartimento principal Olá](#component-list-for-primary-enclosure-of-storsimple-device) e hello [lista de componente detalhado para Olá compartimento EBOD](#component-list-for-ebod-enclosure-of-storsimple-device).

    ![](./media/storsimple-8000-monitor-hardware-status/hw-health2.png)

3. Use Olá status do componente Olá toointerpret do esquema de codificação de cores a seguir:
   
   * **Marca verde** – Indica um componente íntegro com status **OK**.
   * **Amarelo** – Indica um componente degradado no estado de **Aviso**.
   * **Ponto de exclamação vermelho** – Indica um componente falho que tem um status de **Falha**.
   * **Branco com texto preto** – Indica um componente que não está presente.
   
   Olá, seguinte captura de tela mostra um dispositivo que tenha componentes no **Okey**, **aviso**, e **falha** estado.
       
   ![](./media/storsimple-8000-monitor-hardware-status/hw-health3.png)

   Olá expansão **lista de componentes compartilhados**, podemos ver esse cluster NVRAM e Olá Olá estão degradados.

   ![](./media/storsimple-8000-monitor-hardware-status/hw-health5.png)

   Olá expansão **componentes do controlador 1** lista, podemos ver esse nó de cluster Olá falhou.  

   ![](./media/storsimple-8000-monitor-hardware-status/hw-health4.png)  

4. Se você encontrar um componente que não está em um estado **Íntegro** , entre em contato com o Suporte da Microsoft. Se os alertas forem habilitados no seu dispositivo, você receberá um alerta por email. Se você precisar tooreplace um componente de hardware com falha, consulte [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>Lista de componentes para o compartimento primário do dispositivo StorSimple
Olá, a tabela a seguir descreve Olá componentes físicos e lógicos contidos no compartimento Olá principal (presente em 8100 e 8600) do dispositivo StorSimple local.

| Componente | Módulo | Tipo | Local | Unidade renovável (FRU)? | Descrição |
| --- | --- | --- | --- | --- | --- |
| Unidade no slot [0-11] |Unidades de disco |Físico |Compartilhado |Sim |É apresentada uma linha para cada Olá SSD ou Olá HDD unidades no compartimento primário hello. |
| Sensor de temperatura ambiente |Compartimento |Físico |Compartilhado |Não |Medidas Olá temperatura dentro do chassi hello. |
| Sensor de temperatura do plano intermediário |Compartimento |Físico |Compartilhado |Não |Medidas Olá temperatura do plano intermediário hello. |
| Alarme audível |Compartimento |Físico |Compartilhado |Não |Indica se o subsistema de alarme audível hello dentro do chassi Olá é funcional. |
| Compartimento |Compartimento |Físico |Compartilhado |Sim |Indica a presença de saudação do gabinete. |
| Configurações de compartimento |Compartimento |Físico |Compartilhado |Não |Refere-se do painel frontal do chassi Olá toohello. |
| Sensores de tensão de linha |PCM |Físico |Compartilhado |Não |Vários sensores de voltagem de linha têm seu estado exibido, que indica se a medida Olá tensão está dentro da tolerância. |
| Sensores de corrente de linha |PCM |Físico |Compartilhado |Não |Vários sensores de voltagem de linha têm seu estado exibido, que indica se hello medida atual está dentro da tolerância. |
| Sensores de temperatura em PCM |PCM |Físico |Compartilhado |Não |Vários sensores de temperatura, como sensores de entrada e o ponto de acesso tem seu estado exibido, indicando se Olá medido temperatura está dentro da tolerância. |
| Fonte de alimentação [0-1] |PCM |Físico |Compartilhado |Sim |É apresentada uma linha para cada uma das fontes de alimentação Olá no hello dois PCMs localizados em Olá parte posterior do dispositivo hello. |
| Resfriamento [0-1] |PCM |Físico |Compartilhado |Sim |É apresentada uma linha para cada Olá quatro ventiladores que residem em Olá dois PCMs. |
| Bateria [0-1] |PCM |Físico |Compartilhado |Sim |É apresentada uma linha para cada um dos módulos de bateria de backup Olá que estão encaixados no hello PCM. |
| Metis |N/D |Lógico |Compartilhado |N/D |Exibe o estado de saudação de baterias Olá: se eles precisam de ser carregadas e estão se aproximando do fim da vida útil. |
| HDInsight |N/D |Lógico |Compartilhado |N/D |Exibe Olá estado do cluster Olá criado entre dois módulos de controlador integrado hello. |
| Nó de cluster |N/D |Lógico |Compartilhado |N/D |Indica o estado de saudação do controlador hello como parte do cluster hello. |
| Quorum de cluster |N/D |Lógico | |N/D |Indica a presença de saudação da associação de disco de maioria de saudação ao Olá pool de armazenamento HDD. |
| Espaço de dados do HDD |N/D |Lógico |Compartilhado |N/D |espaço de armazenamento de saudação que é usado para dados no pool de armazenamento de disco rígido (HDD) hello. |
| Espaço de gerenciamento de HDD |N/D |Lógico |Compartilhado |N/D |espaço de saudação reservado no hello pool de armazenamento HDD para tarefas de gerenciamento. |
| Espaço de quorum do HDD |N/D |Lógico |Compartilhado |N/D |espaço de saudação reservado no hello pool de armazenamento HDD para quorum do cluster. |
| Espaço de substituição do HDD |N/D |Lógico |Compartilhado |N/D |espaço de saudação reservado no hello pool de armazenamento HDD para substituição do controlador. |
| Espaço de dados do SSD |N/D |Lógico |Compartilhado |N/D |espaço de armazenamento Olá usado para os dados no pool de armazenamento do hello estado sólido (SSD) da unidade. |
| Espaço SSD NVRAM |N/D |Lógico |Compartilhado |N/D |espaço de armazenamento Olá no hello pool de armazenamento SSD dedicado a lógica NVRAM. |
| Pool de armazenamento do HDD |N/D |Lógico |Compartilhado |N/D |Exibe Olá estado Olá lógica do pool de armazenamento que é criado a partir de HDDs do dispositivo. |
| Pool de armazenamento do SSD |N/D |Lógico |Compartilhado |N/D |Exibe Olá estado Olá lógica do pool de armazenamento que é criado a partir de SSDs do dispositivo. |
| Controller [0-1] [estado] |E/S |Físico |Controller |Sim |Exibe o estado de saudação do controlador Olá, e se ele está no modo ativo ou em espera no chassi hello. |
| Sensores de temperatura no controlador |E/S |Físico |Controller |Não |Vários sensores de temperatura, como o módulo de e/s, temperatura da CPU, sensores DIMM e PCIe tem seu estado exibido, que indica se é ou não temperatura Olá encontrada dentro da tolerância. |
| Expansor SAS |E/S |Físico |Controller |Não |Indica o estado de saudação do hello serial anexado SCSI (SAS) expansor, que é usado tooconnect Olá armazenamento integrado toohello controlador. |
| Conector SAS [0-1] |E/S |Físico |Controller |Não |Indica o estado de saudação de cada conector SAS, que é usado tooconnect integrado armazenamento toohello SAS expansor. |
| Interconexão de plano intermediário de SBB |E/S |Físico |Controller |Não |Indica o estado de saudação do conector intermediário hello, o que é usado tooconnect cada intermediário de toohello controlador. |
| Núcleo do processador |E/S |Físico |Controller |Não |Indica o estado de Olá Olá de núcleos de processador em cada controlador. |
| Energia de eletrônicos do compartimento |E/S |Físico |Controller |Não |Indica o estado de saudação do sistema de energia de Olá usado pelo compartimento hello. |
| Diagnósticos de eletrônicos do compartimento |E/S |Físico |Controller |Não |Indica o estado de saudação de subsistemas de diagnóstico Olá fornecidos pelo controlador de saudação. |
| Controlador de Gerenciamento de Placa-base (BMC) |E/S |Físico |Controller |Não |Indica o estado de saudação do hello controlador BMC, que é um processador de serviço especializado que monitora o dispositivo de hardware Olá por meio de sensores e se comunica com o administrador do sistema Olá por meio de uma conexão independente. |
| Ethernet |E/S |Físico |Controller |Não |Indica o estado de saudação de cada uma das interfaces de rede hello, ou seja, o gerenciamento de saudação e portas de dados fornecidas no controlador de saudação. |
| NVRAM |E/S |Físico |Controller |Não |Indica o estado de saudação da NVRAM, uma memória de acesso aleatório não volátil com bateria de reserva de saudação que serve informações críticas de aplicativos tooretain na saudação de falha de energia. |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>Lista de componentes para o compartimento EBOD do dispositivo StorSimple
Olá, a tabela a seguir descreve Olá componentes físicos e lógicos contidos no hello compartimento EBOD (só está presente no modelo 8600) do dispositivo StorSimple local.

| Componente | Módulo | Tipo | Local | FRU? | Descrição |
| --- | --- | --- | --- | --- | --- |
| Unidade no slot [0-11] |Unidades de disco |Físico |Compartilhado |Sim |É apresentada uma linha para cada Olá que unidades HDD na frente de saudação do hello compartimento EBOD. |
| Sensor de temperatura ambiente |Compartimento |Físico |Compartilhado |Não |Medidas Olá temperatura dentro do chassi hello. |
| Sensor de temperatura do plano intermediário |Compartimento |Físico |Compartilhado |Não |Medidas Olá temperatura do plano intermediário hello. |
| Alarme audível |Compartimento |Físico |Compartilhado |Não |Indica se o subsistema de alarme audível hello dentro do chassi Olá é funcional. |
| Compartimento |Compartimento |Físico |Compartilhado |Sim |Indica a presença de saudação do gabinete. |
| Configurações de compartimento |Compartimento |Físico |Compartilhado |Não |Refere-se toohello OPS ou do painel frontal do chassi Olá Olá. |
| Sensores de tensão de linha |PCM |Físico |Compartilhado |Não |Vários sensores de voltagem de linha têm seu estado exibido, que indica se a medida Olá tensão está dentro da tolerância. |
| Sensores de corrente de linha |PCM |Físico |Compartilhado |Não |Vários sensores de voltagem de linha têm seu estado exibido, que indica se hello medida atual está dentro da tolerância. |
| Sensores de temperatura em PCM |PCM |Físico |Compartilhado |Não |Vários sensores de temperatura, como sensores de entrada e o ponto de acesso tem seu estado exibido, que indica se Olá medido temperatura está dentro da tolerância. |
| Fonte de alimentação [0-1] |PCM |Físico |Compartilhado |Sim |É apresentada uma linha para cada uma das fontes de alimentação Olá no hello dois PCMs localizados em Olá parte posterior do dispositivo hello. |
| Resfriamento [0-1] |PCM |Físico |Compartilhado |Sim |É apresentada uma linha para cada Olá quatro ventiladores que residem em Olá dois PCMs. |
| Armazenamento local [HDD] |N/D |Lógico |Compartilhado |N/D |Exibe Olá estado Olá lógica do pool de armazenamento que é criado a partir de HDDs do dispositivo. |
| Controller [0-1] [estado] |E/S |Físico |Controller |Sim |Exibe Olá estado dos controladores de saudação no módulo EBOD de saudação. |
| Sensores de temperatura no EBOD |E/S |Físico |Controller |Não |Vários sensores de temperatura de cada controlador tem seu estado exibido, que indica se a temperatura Olá encontrada está dentro da tolerância. |
| Expansor SAS |E/S |Físico |Controller |Não |Indica o estado de saudação do expansor SAS hello, o que é usado tooconnect Olá armazenamento integrado toohello controlador. |
| Conector SAS [0-2] |E/S |Físico |Controller |Não |Indica o estado de saudação de cada conector SAS, que é usado tooconnect integrado armazenamento toohello SAS expansor. |
| Interconexão de plano intermediário de SBB |E/S |Físico |Controller |Não |Indica o estado de saudação do conector intermediário hello, o que é usado tooconnect cada intermediário de toohello controlador. |
| Energia de eletrônicos do compartimento |E/S |Físico |Controller |Não |Indica o estado de saudação do sistema de energia de Olá usado pelo compartimento hello. |
| Diagnósticos de eletrônicos do compartimento |E/S |Físico |Controller |Não |Indica o estado de saudação de subsistemas de diagnóstico Olá fornecidos pelo controlador de saudação. |
| Controlador de toodevice de Conexão |E/S |Físico |Controller |Não |Indica o estado de saudação da conexão Olá entre o módulo de e/s do EBOD hello e controlador do dispositivo hello. |

## <a name="next-steps"></a>Próximas etapas
* toouse Olá seu dispositivo, vá de tooadminister de serviço do Gerenciador de dispositivos de StorSimple muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).
* Se você precisar tootroubleshoot um componente de dispositivo que tem um status degradado ou com falha, consulte muito[StorSimple indicadores de monitoramento](storsimple-monitoring-indicators.md).
* tooreplace um componente de hardware com falha, consulte [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).
* Se você continuar a problemas de dispositivo de tooexperience [entre em contato com o Microsoft Support](storsimple-8000-contact-microsoft-support.md).

