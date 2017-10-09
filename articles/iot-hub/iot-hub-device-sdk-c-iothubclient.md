---
title: dispositivo de IoT aaaAzure SDK para C - IoTHubClient | Microsoft Docs
description: "Como biblioteca de IoTHubClient toouse Olá no dispositivo de Azure IoT Olá SDK para aplicativos de dispositivo de toocreate C que se comunicam com um hub IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>SDK do dispositivo IoT do Azure para C – mais sobre o IoTHubClient
Olá [primeiro artigo](iot-hub-device-sdk-c-intro.md) em Olá essa série introduzido **dispositivo IoT do Azure SDK para C**. Esse artigo explicou que há duas camadas de arquitetura no SDK. Olá base é Olá **IoTHubClient** biblioteca que gerencia a comunicação com o IoT Hub diretamente. Também há Olá **serializador** biblioteca que se baseia em cima dessa tooprovide serviços de serialização. Neste artigo forneceremos detalhes adicionais sobre Olá **IoTHubClient** biblioteca.

artigo anterior de saudação descrito como Olá toouse **IoTHubClient** biblioteca toosend eventos tooIoT Hub e receber mensagens. Este artigo estende essa discussão, explicando como precisamente gerenciar toomore *quando* enviar e receber dados, apresentando toohello **APIs de nível inferior**. Explicaremos também como tooattach propriedades tooevents (e recuperá-los de mensagens) usando propriedade Olá tratamento recursos Olá **IoTHubClient** biblioteca. Por fim, forneceremos explicação adicional de diferentes maneiras toohandle mensagens recebidas do IoT Hub.

Olá artigo conclui abordando alguns dos diversos tópicos, incluindo mais sobre as credenciais do dispositivo e como toochange Olá comportamento de saudação **IoTHubClient** por meio de opções de configuração.

Vamos usar Olá **IoTHubClient** SDK exemplos tooexplain esses tópicos. Se você quiser toofollow ao longo, consulte Olá **hub IOT\_cliente\_exemplo\_http** e **hub IOT\_cliente\_exemplo\_amqp** aplicativos que estão incluídos no dispositivo do hello IoT do Azure SDK para C. tudo descrito nas seções a seguir de saudação é demonstrado nesses exemplos.

Você pode encontrar hello [ **dispositivo IoT do Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositório e exibir os detalhes de saudação API no hello [referência da API C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-lower-level-apis"></a>Olá APIs de nível inferior
artigo anterior Olá descrito operação básica de saudação do hello **IotHubClient** no contexto de saudação do hello **hub IOT\_cliente\_exemplo\_amqp** aplicativo. Por exemplo, ele explicado como tooinitialize hello usando esse código de biblioteca.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Ele também descritos como eventos toosend usando esta chamada de função.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

Olá Além disso, descreveu como tooreceive mensagens registrando uma função de retorno de chamada.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

artigo Olá também mostrou como recursos toofree usando código como o seguinte hello.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

No entanto, há complementar funções tooeach dessas APIs:

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Essas funções todos incluem "Tudo" no nome da API hello. Além disso, parâmetros de Olá de cada uma dessas funções são contrapartes de não-LL tootheir idênticos. No entanto, o comportamento de saudação dessas funções é diferente de uma maneira importante.

Quando você chama **IoTHubClient\_CreateFromConnectionString**, bibliotecas subjacente Olá criar um novo thread é executado no plano de fundo de saudação. Esse thread envia eventos para o Hub IoT e recebe mensagens dele. Sem esse thread é criado ao trabalhar com hello "Tudo" APIs. criação de saudação do thread de plano de fundo de saudação é um desenvolvedor de toohello conveniência. Você não tem tooworry sobre envio de eventos explicitamente e receber mensagens de IoT Hub – isso acontece automaticamente no plano de fundo de saudação. Por outro lado, Olá "Tudo" APIs oferecem controle explícito sobre a comunicação com o IoT Hub, se necessário.

toounderstand essa melhor, vamos examinar um exemplo:

Quando você chama **IoTHubClient\_SendEventAsync**, o que você está fazendo é colocar evento Olá em um buffer. Olá thread em segundo plano criado quando você chamar **IoTHubClient\_CreateFromConnectionString** continuamente monitora esse buffer e envia os dados que ele contém tooIoT Hub. Isso ocorre no plano de fundo de saudação em Olá mesmo tempo em que Olá thread principal está sendo executado outro trabalho.

Da mesma forma, quando você registrar uma função de retorno de chamada para mensagens usando **IoTHubClient\_SetMessageCallback**, está solicitando que o plano de fundo do hello SDK toohave Olá thread invocar a função de retorno de chamada hello quando uma mensagem recebida, independentemente do thread principal de saudação.

Olá "Tudo" APIs não cria um thread em segundo plano. Em vez disso, uma nova API deve ser chamado tooexplicitly enviar e receber dados de IoT Hub. Isso é demonstrado no exemplo a seguir de saudação.

Olá **hub IOT\_cliente\_exemplo\_http** aplicativo que está incluído no hello SDK demonstra Olá APIs de nível inferior. No exemplo, podemos enviar eventos tooIoT Hub com código como Olá seguinte:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

três primeiras linhas Hello criam mensagem de saudação e última linha de saudação envia eventos hello. No entanto, conforme mencionado anteriormente, "envio" evento de saudação significa que os dados de saudação simplesmente são colocados em um buffer. Nada é transmitido em rede hello quando chamamos **IoTHubClient\_LL\_SendEventAsync**. Em ordem tooactually entrada hello dados tooIoT Hub, você deve chamar **IoTHubClient\_LL\_DoWork**, como no exemplo:

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Esse código (da saudação **hub IOT\_cliente\_exemplo\_http** aplicativo) chama repetidamente **IoTHubClient\_LL\_DoWork** . Cada vez que **IoTHubClient\_LL\_DoWork** é chamado, ele envia alguns eventos de saudação buffer tooIoT Hub e recupera uma mensagem na fila de envio toohello dispositivo. Caso Olá significa que, se é registrado uma função de retorno de chamada para mensagens, em seguida, o retorno de chamada de saudação é invocado (supondo que todas as mensagens são colocadas em fila). Seria registramos uma função de retorno de chamada com o código como Olá seguinte:

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

saudação de motivo que **IoTHubClient\_LL\_DoWork** geralmente é chamado em um loop for que cada vez que ele é chamado, ele envia *alguns* buffer eventos tooIoT Hub e recupera *Olá lado* mensagem na fila para o dispositivo de saudação. Cada chamada não é garantida em buffer toosend todos os eventos ou enfileiradas tooretrieve todas as mensagens. Se você quiser toosend todos os eventos de saudação do buffer e continuam com outro processamento, você pode substituir esse loop por código como Olá seguinte:

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Esse código chama **IoTHubClient\_LL\_DoWork** até que todos os eventos no buffer de saudação receberam tooIoT Hub. Observe que isso também não significa que todas as mensagens em fila tenham sido recebidas. Parte do motivo Olá para isso é que Verificando mensagens "all" não é uma ação como determinista. O que acontece se você recuperar "all" das mensagens de saudação, mas, em seguida, o outro é enviado toohello dispositivo imediatamente após? É uma melhor toodeal de maneira com que com um tempo limite programado. Por exemplo, função de retorno de chamada de mensagem de saudação foi possível redefinir um temporizador toda vez que ele é invocado. Você pode então escrever processamento da lógica de toocontinue se, por exemplo, nenhuma mensagem foram recebidas na Olá última *X* segundos.

Quando você estiver concluído ingressing eventos e receber mensagens, ser toocall se Olá correspondente função tooclean recursos.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Basicamente, há apenas um conjunto de APIs toosend e receber dados de um thread em segundo plano e outro conjunto de APIs que Olá sem thread de segundo plano Olá a mesma coisa. Muitos desenvolvedores podem preferir Olá não - LL APIs, mas hello APIs de nível inferior são úteis quando Olá desenvolvedor deseja ter controle explícito sobre as transmissões de rede. Por exemplo, alguns dispositivos coletam dados ao longo do tempo e apenas inserem eventos em intervalos especificados (por exemplo, de hora em hora ou uma vez por dia). Olá dê APIs de nível inferior Olá controle de tooexplicitly capacidade ao enviar e receber dados de IoT Hub. Outros simplesmente preferirão simplicidade Olá que Olá que fornecem APIs de nível inferior. Tudo o que acontece no thread principal de saudação em vez de ocorra algum trabalho no plano de fundo de saudação.

O modelo que você escolher, ser toobe-se consistente no qual APIs que você usar. Se você iniciar chamando **IoTHubClient\_LL\_CreateFromConnectionString**, certifique-se de que você só usar Olá correspondente APIs de nível inferior para qualquer trabalho de acompanhamento:

* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy
* IoTHubClient\_LL\_DoWork

Olá oposto também é verdadeiro. Se você iniciar com **IoTHubClient\_CreateFromConnectionString**, em seguida, use Olá não - LL APIs para qualquer processamento adicional.

No dispositivo de IoT do Azure de saudação SDK para C, consulte Olá **hub IOT\_cliente\_exemplo\_http** APIs de nível inferior de aplicativo para um exemplo completo de saudação. Olá **hub IOT\_cliente\_exemplo\_amqp** aplicativo pode ser referenciado para obter um exemplo completo de saudação não - LL APIs.

## <a name="property-handling"></a>Manipulação de propriedades
Até o momento quando descrevemos o envio de dados, nós já foi referência toohello corpo de mensagem de saudação. Por exemplo, considere este código:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Este exemplo envia uma mensagem tooIoT Hub com texto de saudação "Olá, mundo". No entanto, IoT Hub também permite que a mensagem do propriedades toobe tooeach anexado. Propriedades são pares nome/valor que podem ser anexado toohello mensagem. Por exemplo, podemos modificar tooattach de código anterior Olá uma mensagem de toohello de propriedade:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Vamos começar chamando **IoTHubMessage\_propriedades** e passando-o identificador de saudação da nossa mensagem. O que obtemos é um **mapa\_tratar** referência que nos permite toostart Adicionando propriedades. Olá este último é feito chamando **mapa\_AddOrUpdate**, que usa uma referência tooa mapa\_identificador, o nome da propriedade hello e o valor da propriedade hello. Com essa API, podemos adicionar quantas propriedades quisermos.

Quando o evento Olá é lido da **Hubs de eventos**, receptor Olá pode enumerar Olá propriedades e recuperar seus valores correspondentes. Por exemplo, no .NET isso deve ser feito acessando Olá [coleção de propriedades no objeto de EventData Olá](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).

No exemplo anterior de saudação, estamos anexando evento tooan de propriedades que enviamos tooIoT Hub. Propriedades também podem ser anexados toomessages recebido do IoT Hub. Se quisermos tooretrieve propriedades de uma mensagem, podemos usar código como o seguinte de saudação em nossa função de retorno de chamada de mensagem:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

Olá chamada muito**IoTHubMessage\_propriedades** retorna Olá **mapa\_tratar** referência. Em seguida, passamos que referenciam muito**mapa\_GetInternals** tooobtain uma matriz de tooan de referência de nome/valor Olá pares (bem como uma contagem de propriedades de saudação). Neste ponto é uma simples questão de enumeração Olá propriedades tooget toohello valores que desejamos.

Você não tem propriedades toouse em seu aplicativo. No entanto, se você precisar tooset-los em eventos ou recuperá-los de mensagens, hello **IoTHubClient** biblioteca torna mais fácil.

## <a name="message-handling"></a>Manipulação de mensagens
Como mencionado anteriormente, quando chegam mensagens da saudação do IoT Hub **IoTHubClient** biblioteca responde invocando uma função de retorno de chamada registrado. Há um parâmetro de retorno dessa função que merece uma explicação adicional. Aqui está um trecho da função de retorno de chamada de saudação em Olá **hub IOT\_cliente\_exemplo\_http** aplicativo de exemplo:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Observe que o tipo de retorno de saudação é **IOTHUBMESSAGE\_disposição\_resultados** e neste caso específico retornamos **IOTHUBMESSAGE\_aceito**. Há outros valores que podemos voltar por essa função, alterar como Olá **IoTHubClient** biblioteca reage toohello de retorno de chamada de mensagem. Aqui estão as opções de saudação.

* **IOTHUBMESSAGE\_aceito** – a mensagem de saudação foi processada com êxito. Olá **IoTHubClient** biblioteca não chamará a função de retorno de chamada hello novamente com hello mesma mensagem.
* **IOTHUBMESSAGE\_rejeitado** – a mensagem não foi processada e não há nenhum toodo desejo Olá isso no futuro. Olá **IoTHubClient** biblioteca não deve chamar a função de retorno de chamada hello novamente com hello mesma mensagem.
* **IOTHUBMESSAGE\_ABANDONADO** – a mensagem não foi processada com êxito, mas Olá **IoTHubClient** biblioteca deve chamar a função de retorno de chamada hello novamente com hello mesma mensagem.

Para Olá primeiro dois códigos de retorno, hello **IoTHubClient** biblioteca envia tooIoT uma mensagem indicando que essa mensagem de saudação do Hub deve ser excluído da fila de dispositivo de saudação e não entregue novamente. efeito da saudação é Olá mesmo (mensagem de saudação é excluída da fila de dispositivo de saudação), mas se a mensagem de saudação foi aceitas ou rejeitada ainda é registrada.  Registrar essa distinção é útil toosenders de mensagem de saudação que pode escutar comentários e descobrir se um dispositivo aceitou ou rejeitou uma mensagem específica.

No caso de última Olá uma mensagem também é enviada tooIoT Hub, mas ele indica que essa mensagem de saudação deve ser entregue novamente. Normalmente você vai abandonar uma mensagem se você encontrar algum erro tootry tooprocess Olá mensagem novamente. Por outro lado, a rejeição de uma mensagem é apropriado quando você encontrar um erro irrecuperável (ou se você simplesmente decidir que não quer tooprocess mensagem de saudação).

Em qualquer caso, lembre-Olá diferentes de códigos de retorno para que você pode extrair o comportamento de saudação desejado Olá **IoTHubClient** biblioteca.

## <a name="alternate-device-credentials"></a>Credenciais de dispositivo alternativas
Conforme explicado anteriormente, Olá primeiro toodo ao trabalhar com hello **IoTHubClient** biblioteca é tooobtain uma **hub IOT\_cliente\_tratar** com uma chamada como Olá a seguir:

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Olá argumentos muito**IoTHubClient\_CreateFromConnectionString** são cadeia de caracteres de conexão de dispositivo hello e um parâmetro que indica o protocolo de saudação usamos toocommunicate com o IoT Hub. cadeia de caracteres de conexão de dispositivo Olá tem um formato que aparece da seguinte maneira:

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

Há quatro tipos de informação nesta cadeia de caracteres: nome do Hub IoT, sufixo do Hub IoT, ID do dispositivo e chave de acesso compartilhado. Obter o nome de domínio totalmente qualificado (FQDN) Olá de um hub IoT quando você cria sua instância do hub IoT no hello portal do Azure — isso fornece o nome do hub IoT hello (Olá primeira parte do hello FQDN) e o sufixo de hub IoT de saudação (restante de saudação do hello FQDN). Obter Olá ID do dispositivo e a chave de acesso compartilhado hello quando você registra seu dispositivo com o IoT Hub (conforme descrito em Olá [artigo anterior](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** lhe biblioteca de saudação tooinitialize unidirecional. Se preferir, você pode criar um novo **hub IOT\_cliente\_tratar** usando esses parâmetros individuais em vez de cadeia de caracteres de conexão de dispositivo hello. Isso é feito com hello código a seguir:

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

Isso é feito Olá mesma coisa que **IoTHubClient\_CreateFromConnectionString**.

Pode parecer óbvio que você desejaria toouse **IoTHubClient\_CreateFromConnectionString** em vez desse método mais detalhado de inicialização. Entretanto, tenha em mente que, ao registrar um dispositivo no Hub IoT, o que obtemos é uma ID de dispositivo e uma chave do dispositivo (e não uma cadeia de conexão). Olá *Gerenciador de dispositivo* ferramenta SDK introduzida no hello [artigo anterior](iot-hub-device-sdk-c-intro.md) usa bibliotecas no hello **SDK do serviço de Azure IoT** cadeia de conexão de dispositivo toocreate saudação do ID do dispositivo Hello, chave do dispositivo e o nome de host do IoT Hub. Para chamar **IoTHubClient\_LL\_criar** pode ser preferível porque poupa etapa Olá de gerar uma cadeia de caracteres de conexão. Use o método que for conveniente.

## <a name="configuration-options"></a>Opções de configuração
Até agora tudo descrito sobre Olá Olá de maneira **IoTHubClient** biblioteca funciona reflete o comportamento padrão. No entanto, há algumas opções que você pode definir toochange como funciona a biblioteca de saudação. Isso é feito aproveitando Olá **IoTHubClient\_LL\_SetOption** API. Considere este exemplo:

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

Há duas opções que normalmente são usadas:

* **SetBatching** (bool) – se **true**, os dados enviados tooIoT Hub é enviado em lotes. Se for **false**, as mensagens serão enviadas individualmente. saudação padrão é **false**. Observe que Olá **SetBatching** opção só se aplica a toohello HTTP protocolo e não toohello MQTT ou AMQP protocolos.
* **Tempo limite** (inteiro não atribuído) – Esse valor é representado em milissegundos. Se enviar uma solicitação HTTP ou o recebimento de uma resposta demora mais do que esse tempo, em seguida, conexão Olá expire.

Olá, opção de envio em lote é importante. Por padrão, Olá eventos em bibliotecas de ingresses individualmente (um único evento é tudo o que você passa muito**IoTHubClient\_LL\_SendEventAsync**). Se Olá opção de envio em lote é **true**, biblioteca Olá coleta quantos eventos possível de buffer de saudação (backup toohello tamanho máximo da mensagem que aceitará o IoT Hub).  Olá evento lote for enviado tooIoT Hub em uma única chamada HTTP (eventos individuais Olá são agrupados em uma matriz JSON). A habilitação do envio em lote geralmente resulta em grandes ganhos de desempenho, uma vez que você está reduzindo as viagens de ida e volta da rede. Ela também reduz significativamente a largura de banda, uma vez que você está enviando um conjunto de cabeçalhos HTTP com um lote de evento, em vez de um conjunto de cabeçalhos para cada evento individual. A menos que tenha um motivo específico toodo caso contrário, normalmente você desejará tooenable envio em lote.

## <a name="next-steps"></a>Próximas etapas
Este artigo descreve no comportamento de saudação de detalhe de saudação **IoTHubClient** biblioteca encontrado no hello **dispositivo IoT do Azure SDK para C**. Com essas informações, você deve ter uma boa compreensão dos recursos de saudação do hello **IoTHubClient** biblioteca. Olá [próximo artigo](iot-hub-device-sdk-c-serializer.md) fornece detalhes semelhantes em Olá **serializador** biblioteca.

toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá [SDKs do Azure IoT][lnk-sdks].

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
