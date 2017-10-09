---
title: registro de identidade aaaUnderstand hello Azure IoT Hub | Microsoft Docs
description: "Guia do desenvolvedor - descrição de saudação do registro de identidade de IoT Hub e como toouse-toomanage seus dispositivos. Inclui informações sobre Olá importar e exportar identidades de dispositivo em massa."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a>Entender o registro de identidade Olá em seu hub IoT

Cada hub IoT tem um registro de identidade que armazena informações sobre dispositivos de saudação permitido tooconnect toohello IoT hub. Antes que um dispositivo pode se conectar a tooan IoT hub, deve haver uma entrada para o dispositivo no registro de identidade do hub do hello IoT. Um dispositivo também deve autenticar com o hub IoT de saudação com base em credenciais armazenadas no registro de identidade hello.

ID do dispositivo Olá armazenada no registro de identidade Olá diferencia maiusculas de minúsculas.

Em um nível alto, registro de identidade Olá é uma coleção compatível com o restante dos recursos de identidade do dispositivo. Quando você adiciona uma entrada no registro de identidade hello, o IoT Hub cria um conjunto de recursos de cada dispositivo, como a fila de saudação que contém mensagens de nuvem para dispositivo em andamento.

### <a name="when-toouse"></a>Quando toouse

Use o registro de identidade hello quando você precisa:

* Provisione os dispositivos que se conectam tooyour IoT hub.
* Controle os pontos de extremidade do hub de tooyour acesso por dispositivo voltados para o dispositivo.

> [!NOTE]
> registro de identidade Olá não contém metadados específicos do aplicativo.

## <a name="identity-registry-operations"></a>Operações de registro de identidade

saudação do registro do IoT Hub identidade expõe Olá seguintes operações:

* Criar identidade do dispositivo
* Atualizar identidade do dispositivo
* Recuperar a identidade do dispositivo por ID
* Excluir identidade do dispositivo
* Lista de identidades de too1000
* Exportar todo o armazenamento de identidades tooAzure blob
* Importar identidades do Armazenamento de Blobs do Azure

Todas essas operações podem usar a simultaneidade otimista, conforme especificado na [RFC7232][lnk-rfc7232].

> [!IMPORTANT]
> Olá apenas de maneira tooretrieve todas as identidades no registro de identidade de um hub IoT é Olá toouse [exportar] [ lnk-export] funcionalidade.

Um registro de identidade do Hub IoT:

* Não contém metadados de aplicativo.
* Pode ser acessada como um dicionário, usando Olá **deviceId** como chave de saudação.
* Não permite consultas expressivas.

Normalmente, uma solução de IoT tem um armazenamento específico da solução separado que contém metadados específicos do aplicativo. Por exemplo, hello armazenamento de solução específica em uma solução de construção inteligente seria gravar sala Olá um sensor de temperatura é implantado.

> [!IMPORTANT]
> Use somente registro de identidade Olá para operações de provisionamento e gerenciamento de dispositivo. Operações de alta taxa de transferência em tempo de execução não devem depender executar operações no registro de identidade hello. Por exemplo, verificando o estado de conexão de saudação de um dispositivo antes de enviar um comando não é um padrão com suporte. Verifique se Olá de toocheck [taxas de limitação] [ lnk-quotas] para registro de identidade hello e hello [pulsação do dispositivo] [ lnk-guidance-heartbeat] padrão.

## <a name="disable-devices"></a>Desabilitar dispositivos

Você pode desativar dispositivos atualizando Olá **status** propriedade de uma identidade no registro de identidade hello. Normalmente, você deve usar essa propriedade em dois cenários:

* Durante um processo de orquestração de provisionamento. Para saber mais, veja [Provisionamento de dispositivo][lnk-guidance-provisioning].
* Se, por algum motivo, você considerar que um dispositivo está comprometido ou que se tornou não autorizado.

## <a name="import-and-export-device-identities"></a>Importar e exportar identidades de dispositivo

Você pode exportar identidades de dispositivo em massa de registro de identidade de um hub IoT, por meio de operações assíncronas no hello [o ponto de extremidade de provedor de recursos IoT Hub][lnk-endpoints]. Exportações são longas trabalhos que usam dados de identidade do dispositivo do blob fornecido pelo cliente contêiner toosave leem a partir do registro de identidade hello.

Você pode importar as identidades do dispositivo no registro de identidade do hub de IoT tooan em massa, usando as operações assíncronas em Olá [o ponto de extremidade de provedor de recursos IoT Hub][lnk-endpoints]. Importações são trabalhos de longa duração que usam dados em dados de identidade do dispositivo do blob fornecido pelo cliente contêiner toowrite no registro de identidade hello.

* Para obter informações detalhadas sobre a importação de saudação e APIs de exportação, consulte [APIs REST de provedor de recursos do IoT Hub][lnk-resource-provider-apis].
* toolearn mais sobre como executar importam e exportar trabalhos, consulte [em massa de gerenciamento de identidades de dispositivo do IoT Hub][lnk-bulk-identity].

## <a name="device-provisioning"></a>Provisionamento de dispositivos

dados de dispositivo de saudação que armazena uma determinada solução de IoT dependem de requisitos específicos de saudação da solução. Porém, no mínimo, uma solução deve armazenar identidades e chaves de autenticação. O Hub IoT do Azure inclui um registro de identidades que pode armazenar valores para cada dispositivo, como IDs, chaves de autenticação e códigos de status. Uma solução pode usar outros serviços do Azure como armazenamento de tabela, o armazenamento de blob ou banco de dados do Cosmos toostore quaisquer dados de dispositivos adicionais.

*Provisionamento do dispositivo* é Olá o processo de adição de saudação inicial do dispositivo dados toohello armazena em sua solução. tooenable um novo hub de tooyour de tooconnect do dispositivo, você deve adicionar um dispositivo ID e as chaves toohello registro de identidade de IoT Hub. Como parte do processo de provisionamento de saudação, talvez seja necessário tooinitialize dados específicos do dispositivo outros repositórios de solução.

## <a name="device-heartbeat"></a>Pulsação do dispositivo

registro de identidade de IoT Hub Hello contém um campo chamado **connectionState**. Somente use Olá **connectionState** campo durante o desenvolvimento e depuração. Soluções de IoT não devem consultar o campo de saudação em tempo de execução. Por exemplo, não consultar Olá **connectionState** campo toocheck se um dispositivo está conectado antes de enviar uma mensagem de nuvem para dispositivo ou um SMS.

Se sua solução de IoT precisa tooknow se um dispositivo estiver conectado, você deve implementar Olá *padrão de pulsação*.

No padrão de pulsação hello, o dispositivo Olá envia mensagens de dispositivo para nuvem pelo menos uma vez a cada determinado período de tempo (por exemplo, pelo menos uma vez a cada hora). Portanto, mesmo se um dispositivo não tem qualquer toosend de dados, ele ainda envia uma mensagem de dispositivo para nuvem vazia (normalmente com uma propriedade que identifica como uma pulsação). No lado do serviço hello, solução de saudação mantém um mapa com a última pulsação de saudação recebida para cada dispositivo. Se a solução de saudação não receber uma mensagem de pulsação no tempo de saudação esperado do dispositivo Olá, ele pressupõe que há um problema com o dispositivo de saudação.

Uma implementação mais complexa pode incluir informações de saudação do [monitoramento das operações] [ lnk-devguide-opmon] dispositivos tooidentify que estão tentando tooconnect ou se comunicar, mas falha. Quando você implementa o padrão de pulsação Olá, verifique se toocheck [IoT Hub cotas e limitações][lnk-quotas].

> [!NOTE]
> Se uma conexão de saudação do IoT solução usa estado toodetermine somente se mensagens de nuvem para dispositivo toosend, e mensagens são não difusão toolarge conjuntos de dispositivos, considere o uso mais simples de saudação *curto tempo de expiração* padrão. Esse padrão atinge Olá mesmo resultado manter um registro de estado de conexão do dispositivo usando o padrão de pulsação de saudação, ao mesmo tempo, sendo mais eficiente. Se você solicitar confirmações de mensagens, o IoT Hub pode notificá-lo sobre quais dispositivos estão tooreceive capaz de mensagens e quais não são.

## <a name="device-lifecycle-notifications"></a>Notificações do ciclo de vida do dispositivo

O Hub IoT pode notificar sua solução de IoT quando uma identidade de dispositivo é criada ou excluída, enviando notificações do ciclo de vida do dispositivo. toodo assim, sua solução de IoT precisa de uma rota de toocreate e tooset Olá fonte de dados igual muito*DeviceLifecycleEvents*. Por padrão, nenhuma notificação de ciclo de vida é enviada, ou seja, nenhuma dessas rotas existe previamente. mensagem de notificação de saudação inclui propriedades e corpo.

Propriedades: Propriedades do sistema de mensagens são prefixadas com hello `'$'` símbolo.

| Nome | Valor |
| --- | --- |
$content-type | aplicativo/json |
$iothub-enqueuedtime |  Hora de envio da notificação de saudação |
$iothub-message-source | deviceLifecycleEvents |
$content-encoding | utf-8 |
opType | **createDeviceIdentity** ou **deleteDeviceIdentity** |
hubName | Nome do Hub IoT |
deviceId | ID do dispositivo Olá |
operationTimestamp | Carimbo de data/hora ISO8601 da operação |
iothub-message-schema | deviceLifecycleNotification |

Corpo: Esta seção está em formato JSON e representa duas Olá de saudação criada a identidade do dispositivo. Por exemplo,

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a>Tópicos de referência:

Olá seguintes tópicos de referência fornecem mais informações sobre o registro de identidade hello.

## <a name="device-identity-properties"></a>Propriedades de identidade do dispositivo

Identidades de dispositivo são representadas como documentos JSON com hello propriedades a seguir:

| Propriedade | Opções | Descrição |
| --- | --- | --- |
| deviceId |obrigatória, somente leitura em atualizações |Uma cadeia de caracteres diferenciam maiusculas de minúsculas (a too128 caracteres) de caracteres alfanuméricos ASCII de 7 bits + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| generationId |obrigatória, somente leitura |Uma IoT diferencia maiusculas de minúsculas, gerado pelo hub, cadeia de caracteres a too128 caracteres. Esse valor é usado toodistinguish dispositivos com hello mesmo **deviceId**, quando tiver sido excluídos e criados novamente. |
| etag |obrigatória, somente leitura |Uma cadeia de caracteres que representa um ETag fraco para a identidade do dispositivo hello, como por [RFC7232][lnk-rfc7232]. |
| auth |opcional |Um objeto composto que contém as informações de autenticação e os materiais de segurança. |
| auth.symkey |opcional |Um objeto composto que contém as chaves primária e secundária, armazenadas no formato base64. |
| status |obrigatório |Um indicador de acesso. Pode estar **Habilitado** ou **Desabilitado**. Se **habilitado**, dispositivo Olá é permitido tooconnect. Se estiver **Desabilitado**, este dispositivo não poderá acessar qualquer ponto de extremidade voltado para o dispositivo. |
| statusReason |opcional |Um 128 caracteres longa cadeia de caracteres que motivo Olá repositórios de status de identidade do dispositivo hello. Todos os caracteres UTF-8 são permitidos. |
| statusUpdateTime |somente leitura |Um indicador temporal, mostrando a data de saudação e a hora da última atualização de status hello. |
| connectionState |somente leitura |Um campo indicando o status da conexão: **Conectado** ou **Desconectado**. Este campo representa Olá exibição IoT Hub de status de conexão do dispositivo hello. **Importante**: esse campo deve ser usado apenas para fins de desenvolvimento/depuração. estado de conexão de saudação é atualizado somente para dispositivos usando MQTT ou AMQP. Além disso, ele se baseia nos pings do nível de protocolo (pings MQTT ou AMQP) e pode ter um atraso máximo de apenas cinco minutos. Por esses motivos, pode haver falsos positivos, como dispositivos relatados como conectados, mas que estão desconectados. |
| connectionStateUpdatedTime |somente leitura |Um indicador temporal, mostrando date de hello e o último estado de conexão do tempo Olá foi atualizado. |
| lastActivityTime |somente leitura |Um indicador temporal, mostrando date de hello e última Olá dispositivo conectado, recebeu ou enviou uma mensagem. |

> [!NOTE]
> Estado de Conexão só pode representar Olá exibição IoT Hub do status de saudação da conexão hello. Atualizações toothis estado pode ser atrasado, com as configurações e condições da rede.

## <a name="additional-reference-material"></a>Material de referência adicional

Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:

* [Pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.
* [Limitação e cotas] [ lnk-quotas] descreve cotas hello e comportamentos que se aplicam a toohello serviço de IoT Hub de limitação.
* [SDKs do Azure de dispositivo e serviço IoT] [ lnk-sdks] listas Olá SDKs, você pode usar ao desenvolver aplicativos do dispositivo e o serviço que interagem com o IoT Hub de vários idiomas.
* [Linguagem de consulta de IoT Hub] [ lnk-query] descreve a linguagem de consulta de saudação, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo.
* [Suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte de IoT Hub para o protocolo MQTT hello.

## <a name="next-steps"></a>Próximas etapas

Agora, você aprendeu como registro de identidade do toouse Olá Hub IoT, você pode estar interessado em Olá tópicos do guia de desenvolvedor de IoT Hub a seguir:

* [Controlar acesso tooIoT Hub][lnk-devguide-security]
* [Usar configurações e estado do dispositivo twins toosynchronize][lnk-devguide-device-twins]
* [Invocar um método direto em um dispositivo][lnk-devguide-directmethods]
* [Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]

Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá seguindo o tutorial de IoT Hub:

* [Introdução ao Hub IoT do Azure][lnk-getstarted-tutorial]

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
