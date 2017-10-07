---
title: indicadores de monitoramento de aaaStorSimple | Microsoft Docs
description: "Descreve Olá diodos emissores (LEDs) e alarmes audíveis usados toomonitor Olá status do dispositivo do StorSimple hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>Usar o seu dispositivo StorSimple toomanage indicadores de monitoramento
## <a name="overview"></a>Visão geral
Seu dispositivo StorSimple inclui diodos emissores de (LEDs) e alarmes que você pode usar toomonitor Olá módulos e status geral do dispositivo do StorSimple hello. Olá indicadores de monitoramento pode ser encontrada em componentes de hardware de saudação do compartimento primário do dispositivo hello e compartimento do EBOD hello. Olá indicadores de monitoramento pode ser LEDs ou alarmes audíveis.

Há três estados usados tooindicate Olá status do LED de um módulo: verde piscando toored verde-âmbar, ou vermelho-âmbar.  

* LEDs verdes representam o status de funcionamento adequado.  
* LEDs toored-âmbar verde piscando representam a presença de saudação de condições não críticas que podem exigir a intervenção do usuário.  
* LEDs vermelho-âmbar indicam que há uma falha crítica presente dentro do módulo de saudação.  

Olá restante deste artigo descreve Olá vários LEDs indicadores de monitoramento, seus locais no dispositivo StorSimple de saudação, status do dispositivo Olá com base em Olá estados de LED e qualquer alarmes audível associado.

## <a name="front-panel-indicator-leds"></a>LEDs indicadores no painel frontal
o painel frontal Hello, também conhecido como Olá *painel de operações* ou *painel ops*, exibe o status agregado de saudação de todos os módulos de saudação no sistema de saudação. painel frontal da saudação é idêntico Olá StorSimple primário e hello compartimento EBOD e é ilustrado abaixo.  

   ![Painel frontal do dispositivo][1]

painel frontal Olá contém Olá indicadores a seguir:  

1. Botão silenciar
2. LED Indicador de energia (verde/vermelho-âmbar)
3. LED indicador de falha de módulo (aceso vermelho-âmbar/apagado)
4. LED indicador de falha lógica (aceso vermelho-âmbar/apagado)
5. Exibição da ID da unidade  

Olá, principal diferença entre o painel frontal Olá LEDs para dispositivo hello e de saudação compartimento EBOD é hello **número de identificação da unidade de sistema** mostrada na tela hello LED. unidade de padrão de saudação ID exibida no dispositivo de saudação é **00**, enquanto Olá ID da unidade padrão exibida no compartimento EBOD de saudação é **01**. Isso permite que você tooquickly diferenciar entre o dispositivo hello e compartimento do EBOD hello quando Olá dispositivo for ativado. Se o dispositivo estiver desativado, use informações de saudação fornecidas no [ativar um novo dispositivo](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) toodifferentiate dispositivo Olá Olá compartimento EBOD.  

## <a name="front-panel-led-status"></a>Status do LED do painel frontal
Use Olá status da tabela tooidentify Olá indicado pelo Olá LEDs no painel frontal do Olá para dispositivo de saudação ou compartimento do EBOD Olá a seguir.  

| Energia do sistema | Falha do módulo | Falha lógica | Alarme | Status |
| --- | --- | --- | --- | --- |
| Vermelho-âmbar |DESATIVADO |DESATIVADO |N/D |Perda de energia CA, funcionando com energia reserva ou energia CA no e módulos do controlador Olá foram removidos. |
| Verde |ATIVADO |ATIVADO |N/D |Estado de teste do painel de operações ligado (5s) |
| Verde |DESATIVADO |DESATIVADO |N/D |Energia ligada, todas as funções em boas condições |
| Verde |ATIVADO |N/D |LEDs de falha do ventilador, LEDs de falha de PCM |Qualquer falha de PCM, falha do ventilador, temperatura acima ou abaixo do recomendado |
| Verde |ATIVADO |N/D |LEDs de módulo de E/S |Qualquer falha do módulo do controlador |
| Verde |ATIVADO |N/D |N/D |Falha lógica no compartimento |
| Verde |Piscando |N/D |LED de status de módulo no módulo do controlador. LEDs de falha do ventilador, LEDs de falha de PCM |Tipo de módulo controlador desconhecido instalado, falha de barramento I2C, erro de configuração dos dados vitais do produto (VPD) do módulo do controlador |

## <a name="power-cooling-module-pcm-indicator-leds"></a>LEDs indicadores de refrigeração do módulo de energia (PCM)
Power resfriamento (PCM) LEDs indicadores do módulo podem ser encontrada em Olá parte traseira do compartimento principal hello ou compartimento EBOD em cada módulo PCM. Este tópico discute como Olá toouse LEDs de status de saudação toomonitor do seu dispositivo StorSimple a seguir.  

* LEDs de PCM para o compartimento principal Olá
* LEDs de PCM para Olá compartimento EBOD

## <a name="pcm-leds-for-hello-primary-enclosure"></a>LEDs de PCM para o compartimento principal Olá
o dispositivo StorSimple Olá tem um módulo PCM 764W com uma bateria adicional. Olá ilustração a seguir mostra painel de LED Olá para dispositivo hello.  

   ![LEDs de PCM no compartimento principal Olá][2]

Legenda do LED:

1. Falha de energia CA
2. Falha do ventilador
3. Falha de bateria
4. PCM OK
5. Falha de CC
6. Bateria boa  

Painel de LED de status de saudação de saudação que PCM é indicado em hello. Painel de LED PCM Olá dispositivo possui seis LEDs. Quatro destes LEDs exibem o status de Olá de saudação de alimentação e ventilador hello. Olá restantes dois LEDs indica o status de saudação de módulo de bateria de backup Olá Olá PCM. Você pode usar o hello tabelas toodetermine Olá status Olá PCM a seguir.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>LEDs indicadores do PCM para a fonte de energia e para o ventilador
| Status | PCM OK (verde) | Falha de CA (âmbar) | Falha do ventilador (âmbar) | Falha de DC (âmbar) |
| --- | --- | --- | --- | --- |
| Sem energia CA (tooenclosure) |DESATIVADO |DESATIVADO |DESATIVADO |DESATIVADO |
| Sem energia de CA (somente este PCM) |DESATIVADO |ATIVADO |DESATIVADO |ATIVADO |
| CA presente PCM ligado - OK |ATIVADO |DESATIVADO |DESATIVADO |DESATIVADO |
| Falha no PCM (falha do ventilador) |DESATIVADO |DESATIVADO |ATIVADO |N/D |
| Falha no PCM (excesso de amperagem, sobretensão, sobrecorrente) |DESATIVADO |ATIVADO |ATIVADO |ATIVADO |
| PCM (ventilador fora da tolerância) |ATIVADO |DESATIVADO |DESATIVADO |ATIVADO |
| Modo standby |Piscando |DESATIVADO |DESATIVADO |DESATIVADO |
| Download de firmware do PCM |DESATIVADO |Piscando |Piscando |Piscando |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>LEDs do indicador PCM para bateria de backup Olá
| Status | Bateria boa (verde) | Falha na bateria (âmbar) |
| --- | --- | --- |
| Bateria ausente |DESATIVADO |DESATIVADO |
| Bateria presente e carregada |ATIVADO |DESATIVADO |
| Bateria carregando ou descarga de manutenção |Piscando |DESATIVADO |
| Falha “pequena” na bateria (recuperável) |DESATIVADO |Piscando |
| Falha “grave” na bateria (não recuperável) |DESATIVADO |ATIVADO |
| Bateria desarmada |Piscando |DESATIVADO |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>LEDs de PCM para Olá compartimento EBOD
Olá compartimento EBOD tem um PCM de 580W e nenhuma bateria adicional. painel PCM Olá Olá compartimento EBOD tem LEDs indicadores somente Olá fontes de alimentação e ventilador hello. Olá ilustração a seguir mostra esses LEDs.

   ![LEDs de PCM no compartimento EBOD de saudação][3] 

Você pode usar o hello após a tabela de status de saudação toodetermine de saudação PCM.  

| Status | PCM OK (verde) | Falha de CA (âmbar) | Falha do ventilador (âmbar) | Falha de DC (âmbar) |
| --- | --- | --- | --- | --- |
| Sem energia CA (tooenclosure) |DESATIVADO |DESATIVADO |DESATIVADO |DESATIVADO |
| Sem energia de CA (somente este PCM) |DESATIVADO |ATIVADO |DESATIVADO |ATIVADO |
| CA presente PCM ligado - OK |ATIVADO |DESATIVADO |DESATIVADO |DESATIVADO |
| Falha no PCM (falha do ventilador) |DESATIVADO |DESATIVADO |ATIVADO |X |
| Falha no PCM (excesso de amperagem, sobretensão, sobrecorrente |DESATIVADO |ATIVADO |ATIVADO |ATIVADO |
| PCM (ventilador fora da tolerância) |ATIVADO |DESATIVADO |DESATIVADO |ATIVADO |
| Modelo standby |Piscando |DESATIVADO |DESATIVADO |DESATIVADO |
| Download de firmware do PCM |DESATIVADO |Piscando |Piscando |Piscando |

## <a name="controller-module-indicator-leds"></a>LEDs indicadores do módulo do controlador
o dispositivo StorSimple Olá contém LEDs do controlador primário hello e módulos do controlador EBOD hello.   

### <a name="monitoring-leds-for-hello-primary-controller"></a>LEDs de monitoramento para o controlador primário Olá
Olá ilustração a seguir ajuda a identificar Olá LEDs no controlador primário hello. (Todos os componentes de saudação são listado tooaid na orientação.)  

   ![LEDs de monitoramento - controlador primário][4]

Use Olá toodetermine tabela a seguir se o módulo do controlador hello está operando corretamente.  

### <a name="controller-indicator-leds"></a>LEDs indicadores do controlador
| LED | Descrição |
| --- | --- |
| LED de ID (azul) |Indica que o módulo hello está sendo identificado. Se hello LED azul estiver piscando em um controlador em execução, então hello controlador é Olá controlador ativo e hello outro é controlador em espera hello. Para obter mais informações, consulte [identificar controlador ativo do hello em seu dispositivo](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| LED de falha (âmbar) |Indica uma falha no controlador de saudação. |
| LED de OK (verde) |O verde constante indica que controlador Olá Okey. Verde piscando indica um erro de configuração de VPD do controlador. |
| LEDs de atividade de SAS (verde) |Verde estável indica uma conexão sem atividade. Verde piscando indica a conexão Olá tem uma atividade em andamento. |
| LEDs de status de Ethernet |O lado direito indica atividade do link/rede: (verde estável) link ativo, (verde piscando) atividade de rede. O lado esquerdo indica a velocidade da rede: (amarelo) 1000 Mb/s, (verde) 100 Mb/s e (OFF) 10 Mb/s Dependendo do modelo de componente hello, essa luz talvez pisque mesmo se a interface de rede de saudação não está habilitado. |
| LEDs de POST |Indica o progresso de inicialização hello quando Olá controlador é ligado. Se o dispositivo StorSimple Olá falhar tooboot, este LED ajudará a Microsoft Support identificar Olá ponto no processo de inicialização Olá no qual Olá falha ocorreu. |

> [!IMPORTANT]
> Se o LED com falha Olá estiver aceso, há um problema com o módulo do controlador Olá que pode ser resolvido ao reiniciar o controlador de saudação. Entre em contato com Microsoft Support se reiniciar controlador de saudação não resolver este problema.  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>LEDs de monitoramento para Olá EBOD (compartimento EBOD)
Cada um dos Olá 6 Gb/controladores EBOD SAS de s possui LEDs que indicam seu status, conforme mostrado na ilustração a seguir de saudação.  

  ![LEDs de monitoramento - compartimento EBOD][5]

Use Olá toodetermine tabela a seguir se o módulo do controlador EBOD hello está funcionando normalmente.  

### <a name="ebod-controller-module-indicator-leds"></a>LEDs indicadores do módulo do controlador EBOD
| Status | Módulo de E/S OK (verde) | Falha no módulo de E/S (âmbar) | Atividade da porta do host (verde) |
| --- | --- | --- | --- |
| Módulo do controlador OK |ATIVADO |DESATIVADO |- |
| Falha do módulo do controlador |DESATIVADO |ATIVADO |- |
| Nenhuma conexão externa de porta de host |- |- |DESATIVADO |
| Conexão externa de porta de host – sem atividade |- |- |ATIVADO |
| Conexão externa de porta de host – com atividade |- |- |Piscando |
| Erro de metadados do módulo do controlador |Piscando |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>LEDs do indicador de unidade de disco para o compartimento primário hello e ebod
o dispositivo StorSimple Olá tem unidades de disco localizadas no compartimento principal hello e compartimento do EBOD hello. Cada drive de disco contém LEDs de indicador de monitoramento, conforme descrito nesta seção. 

Para unidades de disco hello, status da unidade Olá é indicado por um verde LED e um LED amarelo-avermelhado montados na frente de saudação de cada módulo portador de unidade. Olá ilustração a seguir mostra esses LEDs.

  ![LEDs de unidade de disco][6]

Use Olá estado de saudação toodetermine da tabela de cada unidade de disco, que por sua vez, afeta Olá status do LED do painel frontal geral a seguir.  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>LEDs do indicador de unidade de disco para Olá compartimento EBOD
| Status | LED de Atividade OK (verde) | LED de falha (vermelho) | LED do painel de operações associado |
| --- | --- | --- | --- |
| Nenhum driver instalado |DESATIVADO |DESATIVADO |Nenhum |
| Driver instalado e operacional |Piscando com atividade |X |Nenhum |
| Conjunto de identidades do dispositivo Enclosure Services do SCSI (SES) |ATIVADO |Piscando 1 segundo ligado/1 segundo desligado |Nenhum |
| Conjunto de bits de falha do dispositivo SES |ATIVADO |ATIVADO |Falha lógica (vermelha) |
| Falha no circuito de controle de energia |DESATIVADO |ATIVADO |Falha no módulo (vermelho) |

## <a name="audible-alarms"></a>Alarmes audíveis
Um dispositivo StorSimple contém alarmes audíveis associados ao compartimento principal hello e compartimento do EBOD hello. Um alarme audível está localizado no painel frontal hello (também conhecido como saudação do painel ops) de ambos os compartimentos. alarme audível Olá indica quando uma condição de falha está presente. Olá seguintes condições ativarão o alarme hello:  

* Falha do ventilador
* Tensão fora dos limites
* Temperatura acima ou abaixo dos limites
* Saturação térmica
* Falha no sistema
* Falha lógica
* Falha no fornecimento de energia
* Remoção de um módulo de refrigeração de energia (PCM)  

Olá, tabela a seguir descreve Olá vários estados do alarme.  

### <a name="alarm-states"></a>Estados de alarme.
| Estado de alarme | Ação | Ação com o botão de mudo pressionado |
| --- | --- | --- |
| S0 |Modo normal: silencioso |Dois bipes |
| S1 |Modo de falha: 1 segundo ligado/1 segundo desligado |Transição tooS2 ou S3 (consulte as observações) |
| S2 |Modo lembrete: bipe intermitente |Nenhum |
| S3 |Modo mudo: silencioso |Nenhum |
| S4 |Modo de falha crítica: alarme contínuo |Não disponível: mudo não ativo |

> [!NOTE]
> * No estado de alarme S1, se você não pressionar mudo em 2 minutos, o estado de saudação mudará automaticamente tooS2 ou S3.  
> * Estados de alarme S1 tooS4 retornar tooS0 depois que a condição de falha de saudação é limpa.  
> * O estado de falha crítica S4 pode ser inserido a partir de qualquer outro estado.  


Você pode colocar o alarme audível Olá pressionando o botão Mudo saudação do painel ops hello. O mudo será acionado após dois minutos se o botão Mudo Olá não for operado manualmente. Quando a saudação alarme ficar no mudo, ele continuará toosound com tooindicate breves avisos sonoros intermitentes que ainda há um problema. alarme Olá será silenciado quando todos os problemas de saudação são desmarcados.

Olá, tabela a seguir descreve Olá várias condições do alarme.

### <a name="alarm-conditions"></a>Condições de alarme.
| Status | Severidade | Alarme | LED do painel de operações |
| --- | --- | --- | --- |
| Alerta de PCM – perda de energia de CC de um único PCM |Falha – nenhuma perda de redundância |S1 |Falha do módulo |
| Alerta de PCM – perda de energia de CC de um único PCM |Falha – perda de redundância |S1 |Falha do módulo |
| Falha do ventilador do PCM |Falha – perda de redundância |S1 |Falha do módulo |
| Falha do PCM detectada no módulo do SBB |Falha |S1 |Falha do módulo |
| PCM removido |Erro de configuração |Nenhum |Falha do módulo |
| Erro de configuração do compartimento |Falha – crítica |S1 |Falha do módulo |
| Alerta aviso de temperatura baixa |Aviso |S1 |Falha do módulo |
| Alerta aviso de temperatura alta |Aviso |S1 |Falha do módulo |
| Alarme de sobretemperatura |Falha – crítica |S1 |Falha do módulo |
| Falha do barramento I2C |Falha – perda de redundância |S1 |Falha do módulo |
| Erro de comunicação do painel de operações (I2C) |Falha – crítica |S1 |Falha do módulo |
| Erro no controlador |Falha – crítica |S1 |Falha do módulo |
| Falha do módulo da interface SBB |Falha – crítica |S1 |Falha do módulo |
| Falha no módulo da interface SBB – Nenhum módulo em funcionamento restante |Falha – crítica |S4 |Falha do módulo |
| Módulo da interface SBB removido |Aviso |Nenhum |Falha do módulo |
| Falha de controle de energia do drive |Aviso – nenhuma perda de energia no drive |S1 |Falha do módulo |
| Falha de controle de energia do drive |Falha – crítica; perda de energia do drive |S1 |Falha do módulo |
| Drive removido |Aviso |Nenhum |Falha do módulo |
| Energia insuficiente disponível |Aviso |Nenhum |Falha do módulo |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre os [componentes e o status de hardware do StorSimple](storsimple-8000-monitor-hardware-status.md).

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


