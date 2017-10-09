---
title: carregamento do arquivo Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor - recurso de carregamento de arquivo use saudação do IoT Hub toomanage upload de arquivos de um contêiner de blob de armazenamento do Azure do dispositivo tooan."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a>Carregar arquivos com o Hub IoT

Conforme detalhado no hello [pontos de extremidade de IoT Hub] [ lnk-endpoints] artigo, um dispositivo pode iniciar um upload de arquivo enviando uma notificação por meio de um ponto de extremidade voltados para o dispositivo (**/devices/ {deviceId} / arquivos**). Quando um dispositivo notifica o IoT Hub que um carregamento for concluído, o IoT Hub envia uma mensagem de notificação de carregamento de arquivo por meio de saudação **/messages/servicebound/filenotifications** voltadas para o serviço de ponto de extremidade.

Em vez de controle de mensagens por meio de IoT Hub em si, o IoT Hub em vez disso, atua como um dispatcher tooan associados a conta de armazenamento do Azure. Um dispositivo solicita um token de armazenamento do IoT Hub que é específico toohello arquivo hello dispositivo deseja tooupload. dispositivo Olá usa Olá URI SAS tooupload Olá arquivo toostorage e quando Olá carregamento for concluído dispositivo Olá envia uma notificação de conclusão tooIoT Hub. IoT Hub verifica o carregamento do arquivo hello foi concluído e, em seguida, adiciona um arquivo carregamento notificação mensagem toohello voltadas para o serviço arquivo notificação ponto de extremidade.

Antes de carregar um arquivo tooIoT Hub de um dispositivo, você deve configurar seu hub por [associando um armazenamento do Azure] [ lnk-associate-storage] tooit de conta.

Seu dispositivo pode então [inicializar um carregamento] [ lnk-initialize] e, em seguida, [notificar o hub IoT] [ lnk-notify] quando o carregamento de saudação for concluído. Opcionalmente, quando um dispositivo notifica o IoT Hub que Olá carregamento for concluído, o serviço de saudação pode gerar um [mensagem de notificação][lnk-service-notification].

### <a name="when-toouse"></a>Quando toouse

Usar arquivos de mídia de toosend de carregamento de arquivo e lotes grandes telemetria carregados por dispositivos conectados de maneira intermitente ou a largura de banda de toosave compactado.

Consulte também[orientação de comunicação do dispositivo para nuvem] [ lnk-d2c-guidance] se em dúvida entre usando as propriedades relatadas, mensagens de dispositivo para nuvem ou carregamento de arquivo.

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>Associar uma conta do Armazenamento do Azure com o Hub IoT

funcionalidade de carregamento de arquivo de saudação toouse, primeiro você deve vincular uma conta de armazenamento do Azure toohello IoT Hub. Você pode concluir esta tarefa por meio de saudação [portal do Azure][lnk-management-portal], ou programaticamente por meio de saudação [APIs REST de provedor de recursos do IoT Hub] [ lnk-resource-provider-apis]. Depois que você tiver associado uma conta de armazenamento do Azure com o IoT Hub, Olá serviço retorna um URI de SAS tooa dispositivo quando o dispositivo de saudação inicia uma solicitação de carregamento de arquivo.

> [!NOTE]
> Olá [SDKs do Azure IoT] [ lnk-sdks] automaticamente identificador recuperando Olá URI SAS, carregando o arquivo hello e notificar o IoT Hub de um carregamento concluído.


## <a name="initialize-a-file-upload"></a>Inicializar um upload de arquivo
IoT Hub tem um ponto de extremidade especificamente para dispositivos toorequest um URI de SAS para um arquivo de tooupload de armazenamento. processo de carregamento de arquivo de saudação tooinitiate, Olá dispositivo envia uma solicitação POST muito`{iot hub}.azure-devices.net/devices/{deviceId}/files` com hello corpo JSON a seguir:

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

IoT Hub retorna Olá dados, qual dispositivo Olá usa o arquivo de saudação do tooupload a seguir:

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>Preterido: inicializar um carregamento de arquivo com um GET

> [!NOTE]
> Esta seção descreve a funcionalidade preterida como tooreceive um URI de SAS do IoT Hub. Use o método de POSTAGEM de saudação descrito anteriormente.

IoT Hub tem dois arquivos de toosupport de pontos de extremidade REST carregar um hello tooget URI SAS para armazenamento e Olá outros hub de IoT Olá toonotify de um carregamento concluído. Olá dispositivo inicia o processo de upload de arquivo hello enviando um hub de IoT GET toohello em `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`. hub IoT de saudação retorna:

* Um URI de SAS específico toohello toobe de arquivo carregado.
* Uma ID de correlação toobe usado após a conclusão do carregamento de saudação.

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>Notificar o Hub IoT de um upload de arquivo concluído

dispositivo de saudação é responsável por carregar Olá arquivo toostorage usando Olá SDKs de armazenamento do Azure. Quando a saudação carregamento for concluído, o dispositivo de saudação também envia uma solicitação POST`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` com hello corpo JSON a seguir:

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

Olá valor `isSuccess` é um booleano que representa se o arquivo hello foi carregado com êxito. Olá código de status `statusCode` é Olá status de carregamento de saudação do hello arquivo toostorage e Olá `statusDescription` corresponde toohello `statusCode`.

## <a name="reference-topics"></a>Tópicos de referência:

Olá seguintes tópicos de referência fornecem mais informações sobre como carregar arquivos de um dispositivo.

## <a name="file-upload-notifications"></a>Notificações de upload de arquivo

Opcionalmente, quando um dispositivo de IoT Hub o notifica que um carregamento for concluído, o IoT Hub pode gerar uma mensagem de notificação que contém o nome e o armazenamento local do arquivo hello hello.

Como explicado em [Pontos de extremidade][lnk-endpoints], o Hub IoT fornece notificações de upload de arquivos por meio de um ponto de extremidade voltado para o serviço (**/messages/servicebound/fileuploadnotifications**) como mensagens. Olá semântica de recebimento para notificações de carregamento de arquivo são Olá mesmo para mensagens de nuvem para dispositivos e ter Olá mesmo [ciclo de vida da mensagem][lnk-lifecycle]. Cada mensagem recuperada do ponto de extremidade de notificação de carregamento de arquivo hello é um registro JSON com hello propriedades a seguir:

| Propriedade | Descrição |
| --- | --- |
| EnqueuedTimeUtc |O carimbo de hora que indica quando Olá notificação foi criada. |
| deviceId |**DeviceId** do dispositivo Olá que carregou o arquivo hello. |
| BlobUri |URI do arquivo hello carregado. |
| BlobName |Nome da saudação arquivo carregado. |
| LastUpdatedTime |O carimbo de hora que indica quando o arquivo hello foi atualizado pela última. |
| BlobSizeInBytes |Tamanho da saudação arquivo carregado. |

**Exemplo**. Este exemplo mostra o corpo de saudação de um arquivo de carregar a mensagem de notificação.

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a>Opções de configuração de notificação de upload de arquivo

Cada hub IoT expõe Olá as opções de configuração para notificações de carregamento de arquivo a seguir:

| Propriedade | Descrição | Intervalo e padrão |
| --- | --- | --- |
| **enableFileUploadNotifications** |Controla se as notificações de carregamento de arquivo são gravadas toohello ponto de extremidade de notificações de arquivo. |Bool. Padrão: True. |
| **fileNotifications.ttlAsIso8601** |TTL padrão para notificações de upload de arquivos. |Intervalo de ISO_8601 a too48H (mínimo 1 minuto). Padrão: 1 hora. |
| **fileNotifications.lockDuration** |Duração de bloqueio para a fila de notificações de carregamento de arquivo hello. |5 too300 segundos (mínimo 5 segundos). Padrão: 60 segundos. |
| **fileNotifications.maxDeliveryCount** |Contagem máxima de entrega para o arquivo hello carregar fila de notificação. |1 too100. Padrão: 100. |

## <a name="additional-reference-material"></a>Material de referência adicional

Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:

* [Pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.
* [Limitação e cotas] [ lnk-quotas] descreve cotas hello e comportamentos que se aplicam a toohello serviço de IoT Hub de limitação.
* [SDKs do Azure de dispositivo e serviço IoT] [ lnk-sdks] listas Olá SDKs, você pode usar ao desenvolver aplicativos do dispositivo e o serviço que interagem com o IoT Hub de vários idiomas.
* [Linguagem de consulta de IoT Hub] [ lnk-query] descreve a linguagem de consulta de saudação, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo.
* [Suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte de IoT Hub para o protocolo MQTT hello.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como tooupload arquivos de dispositivos usando o IoT Hub, você pode estar interessado em Olá tópicos do guia de desenvolvedor de IoT Hub a seguir:

* [Gerenciar identidades do dispositivo no Hub IoT][lnk-devguide-identities]
* [Controlar acesso tooIoT Hub][lnk-devguide-security]
* [Usar configurações e estado do dispositivo twins toosynchronize][lnk-devguide-device-twins]
* [Invocar um método direto em um dispositivo][lnk-devguide-directmethods]
* [Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]

Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá seguindo o tutorial de IoT Hub:

* [Como arquivos de tooupload de toohello de dispositivos de nuvem com o IoT Hub][lnk-fileupload-tutorial]

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
