---
title: "Especificações técnicas do aaaStorSimple | Microsoft Docs"
description: "Descreve as especificações técnicas do hello e informações de conformidade de padrões regulatórios para componentes de hardware do StorSimple hello."
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 98fa3307e2a929551c74e8b3179bb0fb61c0ab53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-specifications-and-compliance-for-hello-storsimple-device"></a>Especificações técnicas e conformidade para o dispositivo StorSimple Olá

## <a name="overview"></a>Visão geral

componentes de hardware de saudação do seu dispositivo do Microsoft Azure StorSimple aderem especificações técnicas toohello e padrões regulatórios descritos neste artigo. Especificações técnicas do Hello descrevem compartimentos e capacidade de armazenamento de módulos de energia e resfriamento (PCMs), unidades de disco, Olá. as informações de conformidade Olá abrange coisas como padrões internacionais, segurança e emissões e cabeamento.

## <a name="power-and-cooling-module-specifications"></a>Especificações do Módulo de Alimentação e de Refrigeração

o dispositivo StorSimple Olá tem dois 100 a 240 V ventilador duplo com conformidade SBB Power Cooling Modules (PCMs). Isso oferece uma configuração de alimentação redundante. Se um PCM falhar, o dispositivo Olá continua toooperate normalmente em Olá outro PCM até Olá falha de módulo é substituído.

Olá compartimento EBOD usa um PCM de 580 W e o compartimento principal usa um PCM de 764 W. Olá tabelas a seguir lista Olá as especificações técnicas associadas Olá PCMs.

| Especificação | PCM de 580 W (EBOD) | PCM de 764 W (Primário) |
| --- | --- | --- |
| Alimentação de saída máxima |580 W |764 |
| Frequência |50/60 Hz |50/60 Hz |
| Seleção de faixa de tensão |Faixa automática: 90-264 V AC, 47/63 Hz |Faixa automática: 90- 264 V AC, 47/63 Hz |
| Corrente de entrada máxima |20 A |20 A |
| Correção de fator de potência |Voltagem de entrada nominal >95% |Voltagem de entrada nominal >95% |
| Harmônicas |Atende EN61000-3-2 |Atende EN61000-3-2 |
| Saída |Tensão de espera de 5V @ 2.0 A |Tensão de espera de 5V @ 2.7 A |
| +5V @ 42 A |+5V @ 40 A | |
| +12V @ 38 A |+12V @ 38 A | |
| Conectado com a máquina ligada |Sim |Sim |
| Interruptores e LEDs |Interruptor LIGA/DESLIGA CA e quatro LEDs indicadores de status |Interruptor LIGA/DESLIGA CA e seis LEDs indicadores de status |
| Refrigeração do compartimento |Ventiladores de refrigeração axial com controle de velocidade variável de ventilador |Ventiladores de refrigeração axial com controle de velocidade variável de ventilador |

## <a name="power-consumption-statistics"></a>Estatísticas de consumo de energia

Olá, a tabela a seguir lista dados de consumo de energia típico hello (os valores reais podem variar de saudação publicada) do hello vários modelos do dispositivo StorSimple.

| Condições | 240 V AC | 240 V AC | 240 V AC | 110 V AC | 110 V AC | 110 V AC |
| --- | --- | --- | --- | --- | --- | --- |
|  Ventiladores lentos, unidades ociosas |1,45 A |0,31 kW |1057,76 BTU/h |3,19 A |0,34 kW |1160,13 BTU/h |
|  Ventiladores lentos, unidades acessando |1,54 A |0,33 kW |1126,01 BTU/h |3,27 A |0,36 kW |1228,37 BTU/h |
|  Ventiladores rápidos, unidades ociosas, dois PSUs ligados |2,14 A |0,49 kW |1671,95 BTU/h |4,99 A |0,54 kW |1842,56 BTU/h |
|  Ventiladores rápidos, unidades ociosas, um PSU ligado um ocioso |2,05 A |0,48 kW |1637,83 BTU/h |4,58 A |0,50 kW |1706,07 BTU/h |
|  Ventiladores rápidos, unidades acessando, dois PSUs ligados |2,26 A |0,51 kW |1740,19 BTU/h |4,95 A |0,54 kW |1842,56 BTU/h |
|  Ventiladores rápidos, unidades acessando, um PSU ligado um ocioso |2,14 A |0,49 kW |1671,95 BTU/h |4,81 A |0,53 kW |1808,44 BTU/h |

## <a name="disk-drive-specifications"></a>Especificações da unidade de disco

Seu dispositivo StorSimple oferece suporte a unidades de disco SCSI Serial anexado (SAS) do fator de forma de 3,5 polegadas too12. unidades reais Olá podem ser uma mistura de unidades de estado sólido (SSDs) ou unidades de disco rígido (HDDs), dependendo da configuração de produto hello. 12 slots de unidade de disco Olá estão localizados em uma configuração de 3 a 4 na frente do compartimento de saudação. Olá compartimento EBOD possibilita o armazenamento adicional para outro 12 unidades de disco. Elas sempre serão HDDs.

## <a name="storage-specifications"></a>Especificações do armazenamento

dispositivos de StorSimple Olá tem uma mistura de unidades de disco rígido e unidades de estado sólidas para ambos os Olá 8100 e 8600. Olá total utilizável para Olá 8100 e 8600 são aproximadamente 15 TB e 38 TB respectivamente. Olá a tabela a seguir documenta os detalhes de saudação do SSD, unidade de disco rígido e a capacidade de nuvem no contexto Olá Olá capacidade de solução do StorSimple.

| Modelo/capacidade do dispositivo | 8100 | 8600 |
| --- | --- | --- |
| Número de HDDs (unidades de disco rígido) |8 |19 |
| Número de SSDs (unidades de estado sólido) |4 |5 |
| Capacidade de HDD único |4 TB |4 TB |
| Capacidade de SSD único |400 GB |800 GB |
| Capacidade reserva |4 TB |4 TB |
| Capacidade utilizável do HDD |14 TB |36 TB |
| Capacidade utilizável do SSD |800 GB |2 TB |
| Capacidade total utilizável* |~ 15 TB |~ 38 TB |
| Capacidade máxima da solução (incluindo a nuvem) |200 TB |500 TB |

<sup>* </sup>- *capacidade de uso total de saudação inclui capacidade Olá disponível para buffers de dados e metadados.*

## <a name="enclosure-dimensions-and-weight-specifications"></a>Dimensões do compartimento e especificações de peso

Olá, lista de tabelas a seguir Olá diversas especificações do compartimento para dimensões e peso.

### <a name="enclosure-dimensions"></a>Dimensões do compartimento

Olá tabela a seguir lista as dimensões de saudação do compartimento de saudação em milímetros e polegadas.

| Compartimento | Milímetros | Polegadas |
| --- | --- | --- |
| Altura |87,9 |3,46 |
| Largura do flange de montagem |483 |19,02 |
| Largura do corpo do compartimento |443 |17,44 |
| Profundidade de tooextremity do flange de fixação do corpo do compartimento |577 |22,72 |
| Profundidade de operações de extremidade distante de toofurthest do compartimento do painel |630,5 |24,82 |
| Profundidade do flange extremidade distante de toofurthest do compartimento de montagem |603 |23,74 |

### <a name="enclosure-weight"></a>Peso do compartimento

Dependendo da configuração de saudação, um compartimento principal totalmente carregado pode pesar de 21 kg de too33 e requer dois toohandle de pessoas-lo.

| Compartimento | Peso |
| --- | --- |
| Peso máximo (depende da configuração de saudação) |30 kg – 33 kg |
| Vazio (nenhuma unidade ajustada) |21 – 23 kg |

## <a name="enclosure-environment-specifications"></a>Especificações do ambiente de compartimento

Esta seção lista o ambiente de compartimento Olá especificações toohello relacionados. Olá temperatura, umidade, altitude, choque, vibração, orientação, segurança e compatibilidade eletromagnética (EMC) estão incluídos nessa categoria.

### <a name="temperature-and-humidity"></a>Temperatura e umidade

| Compartimento | Faixa de temperatura ambiente | Umidade relativa do ambiente | Umidade máxima da lâmpada |
| --- | --- | --- | --- |
| Operacional |5° C - 35° C (41° F - 95° F) |20-80% sem condensação- |28° C (82° F) |
| Não operacional |-40° C - 70° C (40° F - 158° F) |5% - 100% sem condensação |29° C (84° F) |

### <a name="airflow-altitude-shock-vibration-orientation-safety-and-emc"></a>Fluxo de ar, altitude, choque, vibração, orientação, segurança e EMC

| Compartimento | Especificações operacionais |
| --- | --- |
| Fluxo de ar |Fluxo de ar do sistema é toorear frontal. O sistema deve ser operado com uma instalação de exaustão traseira de baixa pressão. Pressão traseira criada por portas e obstáculos no rack não devem exceder 5 pascals (medidor de água de 0,5 mm). |
| Altitude, operacional |-30 metros too3045 metros (-100 pés too10, 000 pés) com temperatura máxima eliminação classificados por 5 ° C acima de 7.000 pés. |
| Altitude, não operacional |-305 metros too12, 192 metros (-1.000 pés too40, 000 pés) |
| Choque, operacional |Seno de 5g 10 ms ½ |
| Choque, não operacional |Seno de 30g 10 ms ½ |
| Vibração, operacional |0,21g RMS 5-500 Hz aleatório |
| Vibração, não operacional |1,04g RMS 2-200 Hz aleatório |
| Vibração, realocação |Seno de 3g 2-200 Hz |
| Orientação e montagem |Montagem de rack de 19"(2 unidades EIA) |
| Trilhos do rack |racks de profundidade de mínimo de 700 mm (31,50 polegadas) de toofit compatível com a IEC 297 |
| Segurança e aprovações |CE e UL EN 61000-3, IEC 61000-3, UL 61000-3 |
| EMC |EN55022 (CISPR - A), FCC A |

## <a name="international-standards-compliance"></a>Conformidade com padrões internacionais

Seu dispositivo StorSimple do Microsoft Azure está em conformidade com hello padrões internacionais a seguir:  

* CE - EN 60950 - 1
* CB relatório tooIEC 60950-1
* UL e cUL tooUL 60950-1

## <a name="safety-compliance"></a>Conformidade de segurança

Seu dispositivo do Microsoft Azure StorSimple atende Olá classificações de segurança a seguir:

* Aprovação do tipo de produto do sistema: UL, cUL, CE
* Conformidade de segurança: UL 60950, IEC 60950, EN 60950

## <a name="emc-compliance"></a>Conformidade com EMC

Seu dispositivo do Microsoft Azure StorSimple atende Olá classificações EMC a seguir.

### <a name="emissions"></a>Emissões

dispositivo Olá é compatível com a EMC para níveis de emissões conduzidas e irradiadas.

* Níveis de limite de emissões conduzidas: CFR 47 Parte 15B classe A EN55022 Classe A CISPR Classe A
* Níveis de limite de emissões irradiadas: CFR 47 Parte 15B classe A EN55022 Classe A CISPR Classe A

### <a name="harmonics-and-flicker"></a>Harmônicas e cintilação

dispositivo de saudação está de acordo com o EN61000-3-2/3.

### <a name="immunity-limit-levels"></a>Níveis de limite de imunidade

dispositivo de saudação está de acordo com o EN55024.

## <a name="ac-power-cord-compliance"></a>Conformidade do cabo de alimentação de CA

Olá plug e hello completa montagem dos cabos de alimentação deve atender aos padrões de saudação apropriados para país Olá nos quais Olá dispositivo está sendo usado e eles devem ter as aprovações de segurança que são aceitáveis em que país. tabelas a seguir de saudação padrões de lista de saudação EUA e Europa.

### <a name="ac-power-cords---usa-must-be-nrtl-listed"></a>Cabos de alimentação de CA - EUA (devem estar listados no NRTL)

| Componente | Especificação |
| --- | --- |
| Tipo de cabo |SV ou SVT, 18 AWG (mínimo), 3 condutores, 2,0 metros de comprimento máximo |
| Plugue |Plugue de conexão do tipo aterramento NEMA 5-15P com taxa de 120 V, 10 A ou IEC 320 C14, 250 V, 10 A |
| Soquete |IEC 320 C-13, 250 V, 10 A |

### <a name="ac-power-cords---europe"></a>Cabos de alimentação de CA - Europa

| Componente | Especificação |
| --- | --- |
| Tipo de cabo |Harmonizadas, H05-VVF-3G1.0 |
| Soquete |IEC 320 C-13, 250 V, 10 A |

## <a name="supported-network-cables"></a>Cabos de rede com suporte

Para interfaces de rede do hello 10 GbE, DATA 2 e 3 de dados, consulte toohello [lista de cabos de rede com suporte e módulos](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).

## <a name="next-steps"></a>Próximas etapas

Agora você está pronto toodeploy um dispositivo StorSimple em seu data center. Para saber mais, confira [Implantando o dispositivo local](storsimple-8000-deployment-walkthrough-u2.md).

