---
title: gerenciamento de aaaDevice com o Azure IoT Hub | Microsoft Docs
description: "Visão geral do gerenciamento de dispositivos no Hub IoT do Azure: ciclo de vida do dispositivo de empresa e padrões de gerenciamento do dispositivo como a reinicialização, redefinição de fábrica, atualização de firmware, configuração, gêmeos de dispositivo, consultas, trabalhos."
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 7e22fb6eb3c541a513b16a047c7c3ef557255532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a>Visão geral do gerenciamento de dispositivos com o Hub IoT
## <a name="introduction"></a>Introdução
IoT Hub do Azure fornece recursos de saudação e um modelo de extensibilidade que permitem soluções de gerenciamento de dispositivo robusto de toobuild de desenvolvedores de back-end e de dispositivo. Intervalo de dispositivos de sensores restritas e microcontroladores de finalidade única, gateways toopowerful rotear comunicações para grupos de dispositivos.  Além disso, casos de uso de saudação e requisitos para operadores IoT variarem significativamente em setores.  Apesar dessa variação, gerenciamento de dispositivos com o IoT Hub fornece recursos hello, padrões e código bibliotecas toocater tooa conjunto diversificado de dispositivos e usuários finais.

Uma parte fundamental da criação de uma solução de IoT enterprise bem-sucedida é tooprovide uma estratégia para como operadores de lidar com o gerenciamento contínuo de saudação de sua coleção de dispositivos. Operadores de IoT exigem ferramentas simples e confiáveis e aplicativos que permitem toofocus em Olá estratégicos mais os aspectos de seus trabalhos. Esse artigo fornece:

* Uma breve visão geral do gerenciamento do Azure IoT Hub abordagem toodevice.
* Uma descrição dos princípios de gerenciamento de dispositivo comuns.
* Uma descrição do ciclo de vida do dispositivo hello.
* Uma visão geral dos padrões comuns de gerenciamento de dispositivo.

## <a name="device-management-principles"></a>Princípios de gerenciamento de dispositivos
IoT traz um conjunto exclusivo de desafios de gerenciamento de dispositivo e todas as soluções de classe empresarial devem abordar Olá princípios a seguir:

![Gráfico dos princípios de gerenciamento de dispositivos][img-dm_principles]

* **Escala e automação**: IoT soluções exigem ferramentas simples que podem automatizar tarefas de rotina e permitem que as operações de relativamente pequeno de sua equipe toomanage milhões de dispositivos. Diárias, operadores espera que as operações de dispositivo toohandle remotamente, em massa, e tooonly ser alertado quando ocorrerem problemas que exigem sua atenção direta.
* **Abertura e compatibilidade**: ecossistema de dispositivo de saudação é muito diferentes. Ferramentas de gerenciamento devem ser adaptada tooaccommodate uma variedade de classes de dispositivos, plataformas e protocolos. Operadores devem ser capazes de toosupport muitos tipos de dispositivos, hello mais restrita inseridos chips de processo único, toopowerful e computadores totalmente funcionais.
* **Reconhecimento de contexto**: os ambientes de IoT são dinâmicos e estão em constante mudança. A confiabilidade do serviço é fundamental. Operações de gerenciamento do dispositivo devem levar em Olá conta tooensure fatores a seguir que manutenção tempo de inatividade não afetam as operações de negócios críticos ou criar condições perigosas:
    * Janelas de manutenção do SLA
    * Estados de energia e de rede
    * Condições de uso
    * Localização geográfica do dispositivo
* **Muitas funções de serviço**: suporte para fluxos de trabalho exclusivo hello e processos de funções de operações do IoT é crucial. equipe de operações de saudação deve trabalhar harmoniously com hello devido às restrições de departamentos de TI internas.  Eles também devem localizar maneiras sustentável toosurface em tempo real dispositivo operações informações toosupervisors e outras funções de negócios gerenciais.

## <a name="device-lifecycle"></a>Ciclo de vida do dispositivo
Há um conjunto de estágios de gerenciamento de dispositivo em geral que são comuns tooall enterprise IoT projetos. IoT do Azure, há cinco estágios em Olá ciclo de vida do dispositivo:

![Olá cinco fases do ciclo de vida de dispositivo IoT do Azure: planejar, provisionar, configurar, monitorar, desativar][img-device_lifecycle]

Em cada um desses cinco estágios, existem vários requisitos de operador de dispositivo que devem ser atendida tooprovide uma solução completa:

* **Planejar**: habilitar operadores toocreate um esquema de metadados do dispositivo que permite que eles tooeasily e com precisão a consulta para e um grupo de dispositivos em massa para operações de gerenciamento de destino. Você pode usar o hello dispositivo duas toostore esses metadados do dispositivo no formulário de saudação de marcas e propriedades.
  
    *Leitura adicional*: [Introdução ao twins dispositivo][lnk-twins-getstarted], [entender twins dispositivo][lnk-twins-devguide], [como Propriedades de duas dispositivo toouse][lnk-twin-properties].
* **Provisionar**: com segurança provisionar novos dispositivos tooIoT Hub e habilitar operadores tooimmediately descobrir recursos do dispositivo.  Usar identidades de dispositivo flexível de toocreate Olá Hub IoT identidade do registro e as credenciais e executar essa operação em massa usando um trabalho. Crie dispositivos tooreport seus recursos e as condições por meio das propriedades de dispositivo em duas de dispositivo de saudação.
  
    *Leitura adicional*: [gerenciar identidades de dispositivo][lnk-identity-registry], [em massa de gerenciamento de identidades de dispositivo][lnk-bulk-identity], [Como dispositivo toouse macros propriedades][lnk-twin-properties].
* **Configurar**: facilitar em massa toodevices de atualizações de firmware e alterações de configuração, mantendo a integridade e segurança. Execute essas operações de gerenciamento de dispositivo em massa usando propriedades desejadas ou com trabalhos de difusão e métodos diretos.
  
    *Leitura adicional*: [usar métodos diretos][lnk-c2d-methods], [invocar um método direto em um dispositivo][lnk-methods-devguide], [como Propriedades de duas dispositivo toouse][lnk-twin-properties], [agenda e trabalhos de difusão][lnk-jobs], [agendar trabalhos em vários dispositivos] [lnk-jobs-devguide].
* **Monitor**: monitorar a integridade geral do dispositivo da coleta, o status de saudação de operações em andamento e tooissues alertar os operadores que podem exigir atenção.  Aplica Olá dispositivo duas tooallow dispositivos tooreport em tempo real condições operacionais e o status de operações de atualização. Crie relatórios de painel avançado que emite mais imediato saudação superfície por meio de dispositivo duas consultas.
  
    *Leitura adicional*: [como dispositivo toouse macros propriedades][lnk-twin-properties], [linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens] [ lnk-query-language].
* **Desativar**: substituir ou desativar dispositivos após uma falha, atualize o ciclo, ou no final de saudação do tempo de vida de serviço hello.  Usar informações do dispositivo Olá dispositivo duas toomaintain se o dispositivo físico hello está sendo substituído ou arquivado se desativado. Saudação de uso do registro de identidade de IoT Hub para revogar com segurança identidades de dispositivo e as credenciais.
  
    *Leitura adicional*: [como dispositivo toouse macros propriedades][lnk-twin-properties], [gerenciar identidades de dispositivo][lnk-identity-registry].

## <a name="device-management-patterns"></a>Padrões de gerenciamento de dispositivos
IoT Hub permite Olá conjunto de padrões de gerenciamento de dispositivo a seguir.  Olá [tutoriais de gerenciamento de dispositivo] [ lnk-get-started] Mostrar mais detalhadamente como tooextend toofit esses padrões seu cenário exato e como toodesign novos padrões com base nesses modelos de núcleo.

* **Reinicialize** -aplicativo de back-end Olá informa dispositivo Olá por meio de um método que ele iniciou uma reinicialização.  Olá dispositivo usa Olá relatou o status de reinicialização de Olá de tooupdate de propriedades do dispositivo de saudação.
  
    ![Gráfico de padrão de reinicialização de gerenciamento de dispositivos][img-reboot_pattern]
* **Redefinição de fábrica** -aplicativo de back-end Olá informa dispositivo Olá por meio de um método que ele iniciou uma redefinição de fábrica.  Olá dispositivo usa Olá relatou o status de dispositivo de saudação de redefinição de fábrica de saudação do tooupdate de propriedades.
  
    ![Gráfico de padrão de redefinição de fábrica de gerenciamento de dispositivos][img-facreset_pattern]
* **Configuração** -aplicativo de back-end Olá usa Olá desejado propriedades tooconfigure software em execução no dispositivo de saudação.  Olá dispositivo usa Olá relatou o status de configuração de tooupdate propriedades de dispositivo de saudação.
  
    ![Gráfico de padrão de configuração de gerenciamento de dispositivos][img-config_pattern]
* **Atualização de firmware** -aplicativo de back-end Olá informa dispositivo Olá por meio de um método que ele iniciou uma atualização de firmware.  dispositivo Olá inicia uma imagem de firmware do processo de várias etapas toodownload Olá, aplicar a imagem do firmware hello e finalmente reconectar toohello serviço de IoT Hub.  Em todo o processo de várias etapas hello, Olá dispositivo usa Olá relatado progresso de saudação tooupdate propriedades e status de dispositivo de saudação.
  
    ![Gráfico de padrão de atualização de firmware de gerenciamento de dispositivos][img-fwupdate_pattern]
* **Relatório de progresso e o status** -back-end de solução Olá executa consultas de duas do dispositivo, em um conjunto de dispositivos, tooreport status hello e o progresso das ações em execução em dispositivos de saudação.
  
    ![Gráfico de padrão de status e progresso de relatório de gerenciamento de dispositivos][img-report_progress_pattern]

## <a name="next-steps"></a>Próximas etapas
Olá recursos, padrões e bibliotecas de código que o IoT Hub fornece gerenciamento de dispositivos, permitem que você toocreate IoT aplicativos que atendem os requisitos empresariais IoT operador em cada estágio do ciclo de vida de dispositivo.

toocontinue aprender sobre recursos de gerenciamento de dispositivo Olá no IoT Hub, consulte Olá [Introdução ao gerenciamento de dispositivo] [ lnk-get-started] tutorial.

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md
