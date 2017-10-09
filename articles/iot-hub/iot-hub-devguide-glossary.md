---
title: "Glossário de termos do IoT Hub de aaaAzure | Microsoft Docs"
description: "Guia do desenvolvedor - um glossário de termos comuns relacionadas tooAzure IoT Hub."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 16ef29ea-a185-48c3-ba13-329325dc6716
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 217eb082c13e06df5c07543c65d498ad3e395939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="glossary-of-iot-hub-terms"></a>Glossário de termos do Hub IoT
Este artigo lista alguns dos termos comuns de saudação usados no hello artigos de IoT Hub.

## <a name="advanced-message-queueing-protocol"></a>Procolo AMQP
[Advanced Message Queueing Protocol (AMQP)](https://www.amqp.org/) é uma das mensagens de saudação protocolos que [IoT Hub](#iot-hub) oferece suporte para a comunicação com dispositivos. Para obter mais informações sobre protocolos que dá suporte ao IoT Hub de mensagens de saudação, consulte [enviar e receber mensagens com o IoT Hub](iot-hub-devguide-messaging.md).

## <a name="azure-cli"></a>CLI do Azure
Olá [CLI do Azure](../cli-install-nodejs.md) é uma ferramenta de plataforma cruzada, código-fonte aberto, com base em shell de comando para criar e gerenciar recursos do Microsoft Azure. Esta versão do hello CLI é implementado usando o Node. js.

## <a name="azure-cli-20"></a>CLI do Azure 2.0
Olá [2.0 do CLI do Azure](https://docs.microsoft.com/cli/azure/install-az-cli2) é uma ferramenta de plataforma cruzada, código-fonte aberto, com base em shell de comando para criar e gerenciar recursos do Microsoft Azure. Esta versão de visualização do hello CLI é implementada usando Python.


## <a name="azure-iot-device-sdks"></a>SDKs do dispositivo IoT do Azure
Há _dispositivo SDKs_ disponível para vários idiomas que permitem que você toocreate [aplicativos de dispositivo](#device-app) que interagem com um hub IoT. Olá IoT Hub tutoriais mostram como toouse esses SDKs do dispositivo. Você pode encontrar o código-fonte hello e obter mais informações sobre o dispositivo Olá SDKs neste GitHub [repositório](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-iot-edge"></a>Azure IoT Edge
Borda de IoT permite que aplicativos toowrite que permitem que dispositivos conectados por gateway toocommunicate com [IoT Hub](#iot-hub). Olá IoT borda tutoriais mostram como toouse esse serviço. Você pode encontrar o código-fonte hello e obter mais informações sobre a borda de IoT do Azure neste GitHub [repositório](https://github.com/Azure/iot-edge).

## <a name="azure-iot-service-sdks"></a>SDKs do serviço IoT do Azure
Há _serviço SDKs_ disponível para vários idiomas que permitem que você toocreate [aplicativos de back-end](#back-end-app) que interagem com um hub IoT. Olá IoT Hub tutoriais mostram como toouse estes service SDKs. Você pode encontrar o código-fonte hello e obter mais informações sobre o serviço de saudação SDKs neste GitHub [repositório](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-portal"></a>Portal do Azure
Olá [portal do Microsoft Azure](https://portal.azure.com) é um local central onde você pode provisionar e gerenciar seus recursos do Azure. Ele organiza seu conteúdo usando _folhas_. Em alguns dos tutoriais do hello Hub IoT, você poderá ser solicitado Olá toouse [portal clássico do Azure](https://manage.windowsazure.com).

## <a name="azure-powershell"></a>Azure PowerShell
[O Azure PowerShell](/powershell/azure/overview) é uma coleção de cmdlets, você pode usar toomanage do Azure com o Windows PowerShell. Use Olá cmdlets toocreate, testar, implantar e gerenciar soluções e os serviços fornecidos por meio de saudação plataforma Windows Azure.

## <a name="azure-resource-manager"></a>Gerenciador de Recursos do Azure
[Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md) permite que você toowork com recursos de saudação em sua solução como um grupo. Você pode implantar, atualizar ou excluir recursos de saudação para sua solução em uma única operação coordenada.

## <a name="azure-service-bus"></a>Barramento de Serviço do Azure
[Barramento de serviço](../service-bus/index.md) fornece comunicação habilitado para a nuvem com mensagens corporativas e comunicação retransmitida que ajuda você a se conectar a soluções locais com a nuvem de saudação. Alguns tutoriais do Hub IoT utilizam [filas](../service-bus-messaging/service-bus-messaging-overview.md) do Barramento de Serviço.

## <a name="azure-storage"></a>Armazenamento do Azure
O [Armazenamento do Azure](../storage/common/storage-introduction.md) é uma solução de armazenamento de nuvem. Ele inclui o serviço de armazenamento de Blob de saudação que você pode usar toostore não estruturado dados do objeto. Alguns tutoriais do Hub IoT usam o armazenamento de blobs.

## <a name="back-end-app"></a>Aplicativo de back-end
No contexto de saudação do [IoT Hub](#iot-hub), um aplicativo de back-end é um aplicativo que se conecta tooone de pontos de extremidade de serviço voltados Olá em um hub IoT. Por exemplo, um aplicativo de back-end pode recuperar [dispositivo para nuvem](#device-to-cloud)mensagens ou gerenciar Olá [registro identidade](#identity-registry). Normalmente, um aplicativo de back-end é executado na nuvem de hello, mas em muitos dos tutoriais Olá Olá aplicativos de back-end são aplicativos de console em execução no computador de desenvolvimento local.

## <a name="built-in-endpoints"></a>Pontos de extremidade internos
Cada hub IoT inclui um [ponto de extremidade](iot-hub-devguide-endpoints.md) interno que é compatível com o Hub de Eventos. Você pode usar qualquer mecanismo que funciona com mensagens de dispositivo para nuvem tooread Hubs de eventos desse ponto de extremidade.

## <a name="cloud-gateway"></a>Gateway de nuvem
Um gateway de nuvem permite a conectividade para dispositivos que não pode se conectar diretamente muito[IoT Hub](#iot-hub). Um gateway de nuvem é hospedado na nuvem de saudação em contraste tooa [gateway campo](#field-gateway) que é executado em dispositivos tooyour local. Um caso de uso típico para um gateway de nuvem é tooimplement conversão de protocolo para seus dispositivos.

## <a name="cloud-to-device"></a>Nuvem para o dispositivo
Refere-se toomessages enviada de um dispositivo conectado de tooa de hub IoT. Geralmente, essas mensagens são comandos que instruem Olá dispositivo tootake uma ação. Para saber mais, confira [Enviar e receber mensagens com o Hub IoT](iot-hub-devguide-messaging.md).

## <a name="connection-string"></a>Cadeia de conexão
Você pode usar cadeias de caracteres de conexão em seu aplicativo código tooencapsulate Olá informações necessárias tooconnect tooan ponto de extremidade. Uma cadeia de caracteres de conexão normalmente inclui o endereço de saudação do ponto de extremidade de saudação e informações de segurança, mas os formatos variam em serviços de cadeia de conexão. Há dois tipos de cadeia de caracteres de conexão associada Olá serviço IoT Hub:
- *Cadeias de conexão do dispositivo* Habilitar pontos de extremidade de dispositivos tooconnect toohello voltadas para o dispositivo em um hub IoT.
- *Cadeias de caracteres de conexão de IoT Hub* Habilitar pontos de extremidade de aplicativos back-end tooconnect toohello voltadas para o serviço em um hub IoT.

## <a name="custom-endpoints"></a>Pontos de extremidade personalizados
Você pode criar [pontos de extremidade](iot-hub-devguide-endpoints.md) em um toodeliver de hub IoT mensagens enviadas por um [regra de roteamento](#routing-rules). Pontos de extremidade personalizados se conectar diretamente tooan hub de eventos, uma fila do barramento de serviço ou um tópico do barramento de serviço.

## <a name="custom-gateway"></a>Gateway personalizado
Um gateway permite a conectividade para dispositivos que não pode se conectar diretamente muito[IoT Hub](#iot-hub). Você pode usar [Azure IoT borda](#azure-iot-edge) toobuild gateways personalizados que implementam as mensagens de toohandle lógica personalizada, conversões de protocolo personalizado e outros tipos de processamento em Olá borda.

## <a name="data-point-message"></a>Mensagem de ponto de dados
Uma mensagem de ponto de dados é uma mensagem do [dispositivo para nuvem](#device-to-cloud) que contém dados de [telemetria](#telemetry), como velocidade do vento ou temperatura.

## <a name="desired-configuration"></a>Configuração desejada
No contexto de saudação de um [duas dispositivo](iot-hub-devguide-device-twins.md), desejado a configuração se refere a toohello o conjunto completo de propriedades e metadados em duas de dispositivo de saudação que devem ser sincronizados com o dispositivo de saudação.

## <a name="desired-properties"></a>Propriedades desejadas
No contexto de saudação de um [duas dispositivo](iot-hub-devguide-device-twins.md), desejado de propriedades é uma subseção de duas de dispositivo de saudação que é usada com [relatado propriedades](#reported-properties) toosynchronize configuração do dispositivo ou condição. Propriedades desejadas só podem ser definidas um [aplicativo de back-end](#back-end-app) e são observadas por Olá [aplicativo de dispositivo](#device-app).

## <a name="device-to-cloud"></a>Dispositivo para nuvem
Refere-se toomessages enviado de um dispositivo conectado[IoT Hub](#iot-hub). Essas mensagens podem ser do tipo [ponto de dados](#data-point-message) ou [interativas](#interactive-message). Para saber mais, confira [Enviar e receber mensagens com o Hub IoT](iot-hub-devguide-messaging.md).

## <a name="device"></a>Dispositivo
No contexto de saudação do IoT, um dispositivo é normalmente um dispositivo de computação de autônomo em pequena escala, que pode coletar dados ou outros dispositivos de controle. Por exemplo, um dispositivo pode ser um dispositivo de monitoramento ambiental ou um controlador para sistemas de regar e ventilação Olá em um greenhouse. Olá [catálogo dispositivo](https://catalog.azureiotsuite.com/) fornece uma lista de dispositivos de hardware toowork certificada com [IoT Hub](#iot-hub).

## <a name="device-app"></a>Aplicativo de dispositivo
Um aplicativo de dispositivo é executado em seu [dispositivo](#device) e identificadores Olá comunicação com seu [hub IoT](#iot-hub). Normalmente, você usa uma saudação [dispositivo IoT do Azure SDKs](#azure-iot-device-sdks) quando você implementar um aplicativo de dispositivo. Em muitos dos tutoriais do hello IoT, você deve usar um [dispositivo simulado](#simulated-device) para sua conveniência.

## <a name="device-condition"></a>Condição do dispositivo
Refere-se informações de estado toodevice, como o método de conectividade hello atualmente em uso, conforme relatado por um [aplicativo de dispositivo](#device-app). Os [aplicativos de dispositivo](#device-app) também podem relatar suas funcionalidades. Você pode consultar informações de condição e de funcionalidade usando dispositivos gêmeos.

## <a name="device-data"></a>Dados do dispositivo
Os dados do dispositivo refere-se a dados de cada dispositivo de toohello armazenados em Olá IoT Hub [registro identidade](#identity-registry). É possível tooimport e exporte os dados.

## <a name="device-explorer"></a>Gerenciador de dispositivos
Olá [explorer dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) é uma ferramenta que é executado no Windows e permite que você toomanage seus dispositivos em Olá [registro identidade](#identity-registry).hello ferramenta também pode enviar e receber dispositivos de tooyour de mensagens.

## <a name="device-identities-rest-api"></a>API REST de Identidades de Dispositivo
Olá [API de REST de identidades do dispositivo](https://docs.microsoft.com/rest/api/iothub/iothubresource) permite que você toomanage seus dispositivos registrados no hello [registro identidade](#identity-registry) usando uma API REST. Normalmente, você deve usar um nível mais alto de saudação [serviço SDKs](#azure-iot-service-sdks) conforme mostrado no hello tutoriais de IoT Hub.

## <a name="device-identity"></a>Identidade do dispositivo
Olá identidade do dispositivo está Olá identificador exclusivo atribuído tooevery registrado no hello [registro identidade](#identity-registry).

## <a name="device-management"></a>Gerenciamento de dispositivos
Gerenciamento de dispositivo engloba o ciclo de vida completo Olá associado ao gerenciamento de dispositivos de saudação em sua solução de IoT incluindo planejamento, provisionamento, configuração, monitoramento e desativação.

## <a name="device-management-patterns"></a>Padrões de gerenciamento de dispositivos
O [hub IoT](#iot-hub) permite que os padrões comuns de gerenciamento de dispositivos, incluindo reinicialização, execução de redefinições de fábrica e execução de atualizações de firmware nos seus dispositivos.

## <a name="device-messaging-rest-api"></a>API REST de Mensagens do Dispositivo
Você pode usar o hello [API REST do sistema de mensagens do dispositivo](https://docs.microsoft.com/rest/api/iothub/httpruntime) de um dispositivo de dispositivo para nuvem toosend mensagens tooan IoT hub e receber [nuvem para dispositivo](#cloud-to-device) mensagens de um hub IoT. Normalmente, você deve usar um nível mais alto de saudação [dispositivo SDKs](#azure-iot-device-sdks) conforme mostrado no hello tutoriais de IoT Hub.

## <a name="device-provisioning"></a>Provisionamento de dispositivos
Provisionamento do dispositivo é o processo de saudação de adição de saudação inicial [os dados do dispositivo](#device-data) toohello armazena em sua solução. tooenable um novo hub de tooyour de tooconnect do dispositivo, você deve adicionar um dispositivo ID e as chaves toohello IoT Hub [registro identidade](#identity-registry). Como parte do processo de provisionamento de saudação, talvez seja necessário tooinitialize dados específicos do dispositivo outros repositórios de solução.

## <a name="device-twin"></a>Dispositivo gêmeo
Um [dispositivo gêmeo](iot-hub-devguide-device-twins.md) é um documento JSON que armazena informações de estado do dispositivo, como metadados, configurações e condições. O [Hub IoT](#iot-hub) persiste um dispositivo gêmeo para cada dispositivo que você provisiona no hub IoT. Twins dispositivo habilitar toosynchronize [condições de dispositivo](#device-condition) e configurações entre dispositivos hello e solução de saudação back-end. Você pode consultar dispositivos específicos do dispositivo twins toolocate e consultar o status de operações de longa execução hello.

## <a name="device-twin-queries"></a>Consultas de dispositivo gêmeo
[Consultas de duas dispositivo](iot-hub-devguide-query-language.md) use Olá tipo SQL IoT Hub consulta idioma tooretrieve informações de twins seu dispositivo. Você pode usar o hello mesmo IoT Hub consultar informações de tooretrieve de idioma sobre [trabalhos](#job) em execução em seu hub IoT.

## <a name="device-twin-rest-api"></a>API REST de Dispositivo Gêmeo
Você pode usar o hello [API REST do dispositivo duas](https://docs.microsoft.com/rest/api/iothub/devicetwinapi) da solução Olá back-end toomanage twins seu dispositivo. Olá API permite que você tooretrieve e atualização [duas dispositivo](#device-twin) propriedades e invocar [direto métodos](#direct-method). Normalmente, você deve usar um nível mais alto de saudação [serviço SDKs](#azure-iot-service-sdks) conforme mostrado no hello tutoriais de IoT Hub.

## <a name="device-twin-synchronization"></a>Sincronização de dispositivos gêmeos
Sincronização de duas dispositivo usa Olá [propriedades desejadas](#desired-properties) em tooconfigure de twins seu dispositivo seus dispositivos e recuperar [relatado propriedades](#reported-properties) de toostore seus dispositivos em duas de dispositivo de saudação.

## <a name="direct-method"></a>Método direto
Um [método direto](iot-hub-devguide-direct-methods.md) é uma maneira para que você tootrigger tooexecute um método em um dispositivo ao chamar uma API em seu hub IoT.

## <a name="endpoint"></a>Ponto de extremidade
Um hub IoT expõe várias [pontos de extremidade](iot-hub-devguide-endpoints.md) que permitem que o hub IoT de toohello de tooconnect de aplicativos. Há pontos de extremidade voltados para o dispositivo que permitem operações de tooperform de dispositivos, como enviar [dispositivo para nuvem](#device-to-cloud) mensagens e o recebimento [nuvem para dispositivo](#cloud-to-device) mensagens. Não há pontos de extremidade de gerenciamento de serviço voltados que permitem [aplicativos de back-end](#back-end-app) tooperform operações, como [identidade do dispositivo](#device-identity) gerenciamento e o gerenciamento de dispositivos de duas. Há voltado para o serviço [pontos de extremidade internos](#built-in-endpoints) para ler mensagens de dispositivo para a nuvem. Você pode criar [pontos de extremidade personalizados](#custom-endpoints) tooreceive mensagens de dispositivo para nuvem enviadas por um [regra de roteamento](#routing-rules).

## <a name="event-hubs-service"></a>Serviço Hubs de Eventos
[Hubs de Eventos](../event-hubs/event-hubs-what-is-event-hubs.md) é um serviço de entrada de dados altamente dimensionável que pode incluir milhões de eventos por segundo. serviço de saudação permite tooprocess e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados. Para obter uma comparação com hello serviço IoT Hub, consulte [comparação de IoT Hub do Azure e Hubs de eventos do Azure](iot-hub-compare-event-hubs.md).

## <a name="event-hub-compatible-endpoint"></a>Ponto de extremidade compatível com o Hub de Eventos
tooread [dispositivo para nuvem](#device-to-cloud) mensagens enviadas tooyour IoT hub, é possível conectar o ponto de extremidade tooan em seu hub e usar qualquer tooread de método do Hub de eventos-compatível com essas mensagens. Métodos compatíveis com o Hub de eventos incluem o uso de saudação [SDKs de Hubs de evento](../event-hubs/event-hubs-programming-guide.md) e [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md).

## <a name="field-gateway"></a>Gateway de campo
Um gateway de campo permite a conectividade para dispositivos que não pode se conectar diretamente muito[IoT Hub](#iot-hub) e normalmente é implantado localmente com seus dispositivos. Para saber mais, confira [O que é o Hub IoT do Azure?](iot-hub-what-is-iot-hub.md)

## <a name="free-account"></a>Conta gratuita
Você pode criar um [conta do Azure gratuita](https://azure.microsoft.com/pricing/free-trial/) toocomplete Olá tutoriais de IoT Hub e experimentar hello serviço IoT Hub (e outros serviços do Azure).

## <a name="gateway"></a>Gateway
Um gateway permite a conectividade para dispositivos que não pode se conectar diretamente muito[IoT Hub](#iot-hub). Veja também [Gateway de campo](#field-gateway), [Gateway de nuvem](#cloud-gateway) e [Gateway personalizado](#custom-gateway).

## <a name="identity-registry"></a>Registro de identidade
Olá [registro identidade](iot-hub-devguide-identity-registry.md) é permitido de componente interno de saudação de um hub IoT que armazena informações sobre dispositivos individuais Olá tooconnect tooan IoT hub.

## <a name="interactive-message"></a>Mensagem interativa
Uma mensagem interativa é uma [nuvem para dispositivo](#cloud-to-device) mensagem que dispara uma ação imediata no back-end de solução hello. Por exemplo, um dispositivo pode enviar um alarme sobre uma falha que deve ser registrado automaticamente no sistema CRM tooa.

## <a name="iot-hub"></a>Hub IoT
O Hub IoT é um serviço totalmente gerenciado que permite comunicações bidirecionais confiáveis e seguras entre milhões de dispositivos e um back-end da solução. Para saber mais, confira [O que é o Hub IoT do Azure?](iot-hub-what-is-iot-hub.md) Usando o [assinatura do Azure](#subscription), você pode criar toohandle de hubs IoT seu IoT cargas de trabalho do sistema de mensagens.

## <a name="iot-hub-metrics"></a>Métricas do Hub IoT
[Métricas de IoT Hub](iot-hub-metrics.md) lhe fornecer dados sobre o estado de saudação de hubs de IoT Olá na sua [assinatura do Azure](#subscription). Habilitar as métricas de IoT Hub você tooassess Olá a integridade geral do serviço de saudação e dispositivos Olá conectado tooit. Métricas de IoT Hub podem ajudá-lo a ver o que está acontecendo com o hub IoT e investigar a causa raiz de problemas sem a necessidade de toocontact suporte do Azure.

## <a name="iot-hub-query-language"></a>Linguagem de consulta do Hub IoT
Olá [linguagem de consulta de IoT Hub](iot-hub-devguide-query-language.md) é uma linguagem semelhante a SQL permite que você tooquery sua [trabalhos](#job) e twins do dispositivo.

## <a name="iot-hub-resource-provider-rest-api"></a>API REST do Provedor de Recursos do Hub IoT
Você pode usar o hello [API de REST do provedor de recursos de Hub IoT](https://docs.microsoft.com/rest/api/iothub/resourceprovider/iot-hub-resource-provider-rest) toomanage hubs de IoT Olá no seu [assinatura do Azure](#subscription) executar operações como criar, atualizar e excluir hubs.

## <a name="iot-suite"></a>IoT Suite
O Azure IoT Suite reúne em um pacote vários serviços do Azure com soluções pré-configuradas. Essas soluções pré-configuradas permitem tooget familiarizar rapidamente com implementações de ponta a ponta dos cenários comuns de IoT. Para saber mais, confira [O que é o Azure IoT Suite?](../iot-suite/iot-suite-overview.md)

## <a name="iothub-explorer"></a>iothub-explorer
Olá [Gerenciador de Hub IOT](https://github.com/azure/iothub-explorer) é uma ferramenta de linha de comando de plataforma cruzada. Olá ferramenta permite que você toomanage seus dispositivos em Olá [registro identidade](#identity-registry), enviar e receber mensagens e arquivos de seus dispositivos e monitorar as operações de hub IoT.

## <a name="job"></a>Trabalho
O back-end da solução pode usar [trabalhos](iot-hub-devguide-jobs.md) tooschedule e rastrear atividades em um conjunto de dispositivos registrados com o hub IoT. As atividades incluem atualização de [propriedades desejadas](#desired-properties) do dispositivo gêmeo, atualização de [marcas](#tags) do dispositivo gêmeo e invocação de [métodos diretos](#direct-method). [IoT Hub](#iot-hub) também usa trabalhos muito[importação e exportação de tooand](iot-hub-devguide-identity-registry.md#import-and-export-device-identities) de saudação [registro identidade](#identity-registry).

## <a name="jobs-rest-api"></a>API REST de Trabalhos
Olá [trabalhos REST API](https://docs.microsoft.com/rest/api/iothub/jobapi) permite que você toomanage [trabalhos](#job) em execução em seu hub IoT.

## <a name="module"></a>Módulo
No [Azure IoT Edge](iot-hub-linux-iot-edge-get-started.md), um [módulo](iot-hub-linux-iot-edge-get-started.md) é um componente que executa uma tarefa específica. As tarefas podem incluir a inclusão de uma mensagem de um dispositivo, transformando a mensagem ou enviar um hub de IoT tooan mensagem. Um agente é responsável pelo encaminhamento de mensagens entre os módulos. O Azure IoT Edge inclui um conjunto de módulos de exemplo. Você também pode criar seus próprios módulos personalizados.

## <a name="mqtt"></a>MQTT
[MQTT](http://mqtt.org/) é uma das mensagens de saudação protocolos que [IoT Hub](#iot-hub) oferece suporte para a comunicação com dispositivos. Para obter mais informações sobre protocolos que dá suporte ao IoT Hub de mensagens de saudação, consulte [enviar e receber mensagens com o IoT Hub](iot-hub-devguide-messaging.md).

## <a name="operations-monitoring"></a>Monitoramento de operações
IoT Hub [monitoramento das operações](iot-hub-operations-monitoring.md) permite que você toomonitor status de saudação de operações em seu hub IoT em tempo real. O [Hub IoT](#iot-hub) controla eventos em várias categorias de operações. Você pode optar por enviar eventos de um ou mais categorias tooan o ponto de extremidade de IoT Hub para processamento. Você pode monitorar dados Olá erros ou configurar o processamento mais complexo com base nos padrões de dados.

## <a name="physical-device"></a>Dispositivo físico
Um dispositivo físico é um dispositivo real como um Pi framboesa que se conecta tooan IoT hub. Para sua conveniência, muitos dos tutoriais do Hub IoT Olá usam [simulados dispositivos](#simulated-device) tooenable toorun você amostras no seu computador local.

## <a name="primary-and-secondary-keys"></a>Chaves primárias e secundárias
Quando você conecta o dispositivo tooa voltados ou voltados para o serviço de ponto de extremidade em um hub IoT, seu [cadeia de caracteres de conexão](#connection-string) inclui toogrant chave você acessar. Quando você adiciona um dispositivo toohello [registro identidade](#identity-registry) ou adicionar um [política de acesso compartilhado](#shared-access-policy) tooyour hub, serviço hello gera uma chave primária e secundária. Ter duas chaves permite que você tooroll através de um tooanother chave quando você atualiza uma chave sem perder o hub de IoT toohello acesso.

## <a name="protocol-gateway"></a>Gateway de protocolo
Um gateway de protocolo normalmente é implantado na nuvem hello e fornece o protocolo de serviços de tradução para dispositivos que conectam muito[IoT Hub](#iot-hub). Para saber mais, confira [O que é o Hub IoT do Azure?](iot-hub-what-is-iot-hub.md)

## <a name="quotas-and-throttling"></a>Cotas e limitação
Há vários [cotas](iot-hub-devguide-quotas-throttling.md) que se aplicam a uso tooyour de [IoT Hub](#iot-hub), muitas das Olá cotas variam com base na camada de saudação do hub IoT de saudação. [IoT Hub](#iot-hub) também se aplica [limita](iot-hub-devguide-quotas-throttling.md) use tooyour do serviço de saudação em tempo de execução.

## <a name="reported-configuration"></a>Configuração relatada
No contexto de saudação de um [duas dispositivo](iot-hub-devguide-device-twins.md), configuração relatada se refere a toohello o conjunto completo de propriedades e metadados em duas de dispositivo de saudação que devem ser relatados de back-end de solução toohello.

## <a name="reported-properties"></a>Propriedades reportadas
No contexto de saudação de um [duas dispositivo](iot-hub-devguide-device-twins.md), relatados propriedades é uma subseção de saudação dispositivo duas usada com [propriedades desejadas](#desired-properties) toosynchronize configuração do dispositivo ou condição. Relatado propriedades só podem ser definidas por Olá [aplicativo de dispositivo](#device-app) e pode ser lido e consultados por uma [aplicativo de back-end](#back-end-app).

## <a name="resource-group"></a>Grupo de recursos
[Gerenciador de recursos do Azure](#azure-resource-manager) toogroup de grupos de recursos usa recursos relacionados juntos. Você pode usar as operações tooperform de grupo de recursos em todos os recursos de saudação no grupo Olá simultaneamente.

## <a name="retry-policy"></a>Política de repetição
Usar um toohandle de política de repetição [erros transitórios](https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx) quando você conectar o serviço de nuvem tooa.

## <a name="routing-rules"></a>Regras de roteamento
Configurar [regras de roteamento](iot-hub-devguide-messages-read-custom.md) em sua tooa de mensagens de dispositivo para nuvem IoT hub tooroute [ponto de extremidade interno](#built-in-endpoints) ou muito[pontos de extremidade personalizados](#custom-endpoints) para processamento por seu backup de solução final.

## <a name="sasl-plain"></a>SASL SIMPLES
SASL simples é um protocolo que Olá [AMQP](#advanced-message-queue-protocol) usa o protocolo tootransfer tokens de segurança.

## <a name="shared-access-signature"></a>Assinatura de acesso compartilhado
As SAS (Assinaturas de Acesso Compartilhado) são um mecanismo de autenticação com base em hashes seguros SHA-256 ou URIs. A autenticação de SAS tem dois componentes: uma _Política de acesso Compartilhado_ e uma _Assinatura de Acesso Compartilhado_ (normalmente chamada de token). Um dispositivo usa tooauthenticate SAS com um hub IoT. [Aplicativos de back-end](#back-end-app) também usar tooauthenticate SAS com pontos de extremidade do hello voltados para o serviço em um hub IoT. Normalmente, você incluir o token SAS Olá em Olá [cadeia de caracteres de conexão](#connection-string) que um aplicativo usa tooestablish um hub de IoT tooan conexão.

## <a name="shared-access-policy"></a>Política de acesso compartilhado
Uma política de acesso compartilhado define permissões de saudação concedidas tooanyone que tem uma opção válida [chave primária ou secundária](#primary-and-secondary-keys) associados a essa política. Você pode gerenciar as políticas de acesso compartilhada de saudação e chaves para o hub Olá [portal](#azure-portal).

## <a name="simulated-device"></a>Dispositivo simulado
Para sua conveniência, muitas das Olá IoT Hub tutoriais usam simulados tooenable dispositivos você toorun as amostras no seu computador local. Em contraste, uma [dispositivo físico](#physical-device) é um dispositivo real como um Pi framboesa que se conecta tooan IoT hub.

## <a name="solution"></a>Solução
Um _solução_ podem se referir a solução do Visual Studio tooa que inclui um ou mais projetos. Um _solução_ também podem se referir a solução de IoT tooan que inclui elementos, como dispositivos, [aplicativos de dispositivos](#device-app), um hub IoT, outros serviços do Azure, e [aplicativos de back-end](#back-end-app).

## <a name="subscription"></a>Assinatura
Uma assinatura do Azure é onde ocorre a cobrança. Cada recurso do Azure que você cria ou serviço do Azure que usa está associado a uma única assinatura. Muitos cotas também se aplicam no nível de saudação de uma assinatura.

## <a name="system-properties"></a>Propriedades do sistema
No contexto de saudação de um [duas dispositivo](iot-hub-devguide-device-twins.md), propriedades do sistema são somente leitura e incluem informações sobre o uso do dispositivo hello como o último estado de conexão e de tempo de atividade.

## <a name="tags"></a>Marcas
No contexto de saudação de um [duas dispositivo](iot-hub-devguide-device-twins.md), marcas são metadados do dispositivo armazenada e recuperada por Olá solução back-end na forma de saudação de um documento JSON. Marcas não são visíveis tooapps em um dispositivo.

## <a name="telemetry"></a>Telemetria
Coletar dados de telemetria, como velocidade do vento ou de temperatura de dispositivos e usar [mensagens de ponto de dados](#data-point-messages) hub IoT do toosend Olá telemetria tooan.

## <a name="token-service"></a>Serviço de token
Você pode usar um serviço de token de tooimplement um mecanismo de autenticação para seus dispositivos. Ele usa um IoT Hub [política de acesso compartilhado](#shared-access-policy) com **DeviceConnect** permissões toocreate *no escopo do dispositivo* tokens. Esses tokens habilitar um hub IoT de tooyour de tooconnect de dispositivo. Um dispositivo usa um tooauthenticate do mecanismo de autenticação personalizada com o serviço de token de saudação. Se o dispositivo Olá autentica com êxito, o serviço de token de saudação emite um token SAS para Olá dispositivo toouse tooaccess seu hub IoT.

## <a name="x509-client-certificate"></a>Certificado de cliente X.509
Um dispositivo pode usar um tooauthenticate de certificado x. 509 com [IoT Hub](#iot-hub). Usando um certificado x. 509 é uma alternativa toousing um [token SAS](#shared-access-signature).
