---
title: dispositivo SDK do Azure IoT aaaThe para C | Microsoft Docs
description: "Introdução ao dispositivo do hello IoT do Azure SDK para C e saiba como toocreate aplicativos de dispositivos que se comunicam com um hub IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>SDK do dispositivo IoT do Azure para C

Olá **dispositivo IoT do Azure SDK** é um conjunto de bibliotecas projetou o processo de saudação do toosimplify de envio de mensagens tooand recebendo mensagens de saudação **Azure IoT Hub** serviço. Há diferentes variações de saudação SDK, cada um direcionado para uma plataforma específica, mas este artigo descreve Olá **dispositivo IoT do Azure SDK para C**.

dispositivo SDK do Azure IoT Olá para C é gravado em ANSI C (C99) toomaximize portabilidade. Este recurso torna Olá bibliotecas adequado toooperate em várias plataformas e dispositivos, especialmente onde minimizando o disco e volume de memória é uma prioridade.

Há uma ampla variedade de plataformas na qual Olá SDK foi testado (consulte Olá [Azure Certified para catálogo de dispositivo IoT](https://catalog.azureiotsuite.com/) para obter detalhes). Embora este artigo inclui instruções passo a passo do código de exemplo em execução na plataforma do Windows hello, código de saudação descrito neste artigo é idêntico em intervalo de saudação de plataformas com suporte.

Este artigo apresenta toohello arquitetura do dispositivo do hello IoT do Azure SDK para C. Ele demonstra como enviar dados tooIoT Hub tooinitialize biblioteca de dispositivo Olá e receber mensagens dela. informações de saudação neste artigo devem ser suficiente tooget iniciado usando Olá SDK, mas também fornece ponteiros tooadditional informações sobre as bibliotecas de saudação.

## <a name="sdk-architecture"></a>Arquitetura do SDK

Você pode encontrar hello [ **dispositivo IoT do Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositório e exibir os detalhes de saudação API no hello [referência da API C](https://azure.github.io/azure-iot-sdk-c/index.html).

Olá a versão mais recente das bibliotecas de saudação pode ser encontrada Olá **mestre** ramificação do repositório de saudação:

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* Olá implementação básica do hello SDK está em Olá **hub IOT\_cliente** pasta que contém a implementação de saudação da camada de API mais baixa Olá no hello SDK: Olá **IoTHubClient** biblioteca. Olá **IoTHubClient** biblioteca contém APIs implementando bruto de mensagens para enviar mensagens tooIoT Hub e receber mensagens de IoT Hub. Ao usar essa biblioteca, você será o responsável por implementar a serialização de mensagens, mas outros detalhes de comunicação com o Hub IoT serão tratados para você.
* Olá **serializador** pasta contém exemplos que mostram como dados tooserialize antes de enviar tooAzure Hub IoT usando Olá biblioteca de cliente e funções auxiliares. uso de saudação do serializador Olá não é obrigatório e é fornecido como uma conveniência. Olá toouse **serializador** biblioteca, você define um modelo que especifica dados toosend tooIoT Hub e hello mensagens de saudação esperado tooreceive dele. Após a definição de modelo hello, Olá SDK fornece uma superfície de API que permite que você tooeasily trabalham com o dispositivo para nuvem e mensagens de nuvem para dispositivo sem se preocupar Olá detalhes de serialização. biblioteca de saudação depende de outras bibliotecas de código-fonte aberto que implementam o transporte usando protocolos como MQTT e AMQP.
* Olá **IoTHubClient** biblioteca depende de outras bibliotecas de código-fonte aberto:
  * Olá [C Azure compartilhado utilitário](https://github.com/Azure/azure-c-shared-utility) library, que fornece a funcionalidade comum para as tarefas básicas (como cadeias de caracteres, manipulação de lista e e/s) necessária em vários SDKs de C relacionadas ao Azure.
  * Olá [uAMQP Azure](https://github.com/Azure/azure-uamqp-c) biblioteca, que é uma implementação de cliente do AMQP otimizado para dispositivos de recurso restringido.
  * Olá [uMQTT Azure](https://github.com/Azure/azure-umqtt-c) biblioteca, que é uma biblioteca de finalidade geral implementando Olá MQTT protocolo e otimizado para dispositivos de recurso restringido.

Uso dessas bibliotecas é mais fácil toounderstand examinando o código de exemplo. Olá seções a seguir orientam você durante vários aplicativos de exemplo hello que estão incluídos no SDK do hello. Este passo a passo deve fornecer uma boa sinta-se para Olá diversos recursos das camadas de arquitetura de saudação de hello SDK e uma saudação de toohow Introdução APIs funcionam.

## <a name="before-you-run-hello-samples"></a>Antes de executar os exemplos de saudação

Antes de executar os exemplos de saudação no dispositivo do hello IoT do Azure SDK para C, você deve [criar uma instância de serviço de IoT Hub de hello](iot-hub-create-through-portal.md) na sua assinatura do Azure. Em seguida, conclua Olá tarefas a seguir:

* Preparar seu ambiente de desenvolvimento
* Obtenha as credenciais do dispositivo.

### <a name="prepare-your-development-environment"></a>Preparar seu ambiente de desenvolvimento

Os pacotes são fornecidos para plataformas comuns (como NuGet para Windows ou apt_get para Debian e Ubuntu) e exemplos de saudação usam esses pacotes, quando disponível. Em alguns casos, você precisa toocompile Olá SDK para ou em seu dispositivo. Se você precisar toocompile Olá SDK, consulte [preparar seu ambiente de desenvolvimento](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) no repositório do GitHub hello.

código de aplicativo de exemplo de hello tooobtain, baixar uma cópia da saudação SDK do GitHub. Obter sua cópia da fonte de saudação do hello **mestre** ramificação da saudação [repositório GitHub](https://github.com/Azure/azure-iot-sdk-c).


### <a name="obtain-hello-device-credentials"></a>Obter credenciais de dispositivo Olá

Agora que você tem o código-fonte exemplo hello, Olá próxima coisa toodo é tooget um conjunto de credenciais do dispositivo. Para um dispositivo toobe capaz de tooaccess um hub IoT, primeiro você deve adicionar Olá dispositivo toohello registro de identidade de IoT Hub. Quando você adiciona seu dispositivo, você pode obter um conjunto de credenciais de dispositivo necessários para o hub de IoT Olá dispositivo toobe capaz de tooconnect toohello. aplicativos de exemplo Hello discutidos na próxima seção, Olá esperam essas credenciais na forma de saudação de um **cadeia de caracteres de conexão de dispositivo**.

Há várias toohelp de ferramentas de software livre gerenciar seu hub IoT.

* Um aplicativo do Windows chamado [Gerenciador de Dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).
* Uma ferramenta CLI de plataforma cruzada Node.js chamada [iothub-explorer](https://github.com/azure/iothub-explorer).

Este tutorial usa Olá gráfica *explorer dispositivo* ferramenta. Você também pode usar o hello *Gerenciador de Hub IOT* ferramenta se você preferir toouse uma ferramenta CLI.

ferramenta de Gerenciador de dispositivo Olá usa hello Azure IoT serviço bibliotecas tooperform várias funções no IoT Hub, incluindo a adição de dispositivos. Se você usar Olá dispositivo explorer ferramenta tooadd um dispositivo, você obtém uma cadeia de caracteres de conexão para seu dispositivo. Você precisa de aplicativos de exemplo essa conexão cadeia de caracteres toorun hello.

Se você não estiver familiarizado com a ferramenta de Gerenciador de dispositivo hello, Olá procedimento a seguir descreve como toouse-tooadd um dispositivo e obter uma cadeia de caracteres de conexão do dispositivo.

ferramenta de Gerenciador de dispositivo do tooinstall hello, consulte [como toouse Olá Gerenciador de dispositivo para dispositivos de IoT Hub](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).

Quando você executar o programa de saudação, você verá essa interface:

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

Insira seu **cadeia de caracteres de Conexão de Hub IoT** no hello primeiro campo e clique em **atualização**. Esta etapa configura a ferramenta de saudação para que ele possa se comunicar com o IoT Hub.

Quando Olá cadeia de caracteres de conexão de IoT Hub é configurado, clique em Olá **gerenciamento** guia:

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

Essa guia é onde você gerencia dispositivos Olá registrados em seu hub IoT.

Crie um dispositivo clicando Olá **criar** botão. Um diálogo é exibido com um conjunto de chaves pré-populadas (primárias e secundárias). Insira uma **ID de dispositivo** e clique em **Criar**.

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

Quando o dispositivo de saudação é criado, Olá dispositivos listam atualizações com todos os dispositivos de saudação registrado, incluindo Olá que aquele que você acabou de criar. Se você clicar com o botão direito do mouse no novo dispositivo, este menu será exibido:

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

Se você escolher **copiar a cadeia de caracteres de conexão para o dispositivo selecionado**, cadeia de caracteres de conexão de dispositivo Olá é toohello copiado na área de transferência. Manter uma cópia de cadeia de caracteres de conexão de dispositivo hello. É necessário ao executar aplicativos de exemplo hello descritos Olá seções a seguir.

Quando tiver concluído as etapas de saudação acima, você está pronto toostart executando algum código. Os dois exemplos de tem uma constante na parte superior de Olá Olá principal do arquivo de origem que permite que você tooenter uma cadeia de caracteres de conexão. Olá, por exemplo, a linha correspondente da saudação **hub IOT\_cliente\_exemplo\_mqtt** aplicativo aparece da seguinte maneira.

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>Use a biblioteca de IoTHubClient Olá

Dentro de saudação **hub IOT\_cliente** pasta Olá [iot do azure-c sdk](https://github.com/azure/azure-iot-sdk-c) repositório, há um **exemplos** pasta que contém um aplicativo chamado **hub IOT\_cliente\_exemplo\_mqtt**.

versão do Windows Hello de saudação **hub IOT\_cliente\_exemplo\_mqtt** aplicativo inclui Olá após a solução do Visual Studio:

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> Se você abrir este projeto no Visual Studio de 2017, aceite Olá prompts tooretarget Olá toohello mais recente versão do projeto.

Essa solução contém um único projeto. Há quatro pacotes NuGet instalados na solução:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt

Você sempre precisa Olá **Microsoft.Azure.C.SharedUtility** pacote quando você estiver trabalhando com hello SDK. Este exemplo usa o protocolo MQTT de hello, portanto você deve incluir Olá **Microsoft.Azure.umqtt** e **Microsoft.Azure.IoTHub.MqttTransport** pacotes (há pacotes equivalentes para AMQP e HTTP ). Como exemplo hello usa Olá **IoTHubClient** biblioteca, você também deve incluir Olá **Microsoft.Azure.IoTHub.IoTHubClient** pacote em sua solução.

Você pode encontrar a implementação Olá para o aplicativo de exemplo hello no hello **hub IOT\_cliente\_exemplo\_mqtt.c** arquivo de origem.

Olá, etapas a seguir usam esta toowalk do aplicativo de exemplo você durante o que é necessário Olá toouse **IoTHubClient** biblioteca.

### <a name="initialize-hello-library"></a>Inicializar a biblioteca de saudação

> [!NOTE]
> Antes de começar a trabalhar com bibliotecas de saudação, talvez seja necessário tooperform alguns plataforma específica. Por exemplo, se você planeja toouse AMQP Linux, você deverá inicializar biblioteca OpenSSL de saudação. Olá amostras Olá [repositório GitHub](https://github.com/Azure/azure-iot-sdk-c) chamar a função de utilitário hello **plataforma\_init** quando Olá cliente inicia e chamar hello **plataforma\_deinit**  função antes de sair. Essas funções são declaradas no arquivo de cabeçalho platform.h hello. Examine as definições de saudação dessas funções para sua plataforma de destino no hello [repositório](https://github.com/Azure/azure-iot-sdk-c) toodetermine se precisar tooinclude qualquer código de inicialização específico da plataforma no seu cliente.

toostart trabalhando com bibliotecas hello, primeiro alocar um identificador de cliente de IoT Hub:

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

Você passar uma cópia da cadeia de conexão do dispositivo Olá que você obteve da função de toothis hello dispositivo explorer ferramenta. Você também pode designar Olá toouse de protocolo de comunicação. Este exemplo usa MQTT, mas AMQP e HTTP também são opções.

Quando você tem uma opção válida **hub IOT\_cliente\_tratar**, você pode iniciar uma chamada hello APIs toosend e receber mensagens tooand de IoT Hub.

### <a name="send-messages"></a>Enviar mensagens

aplicativo de exemplo Hello configura um hub IoT do loop toosend mensagens tooyour. saudação de trecho de código a seguir:

- Cria uma mensagem.
- Adiciona uma mensagem de toohello de propriedade.
- Envia uma mensagem.

Em primeiro lugar, crie uma mensagem:

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

Toda vez que você enviar uma mensagem, você pode especificar uma função de retorno de chamada de tooa de referência que é invocada quando dados saudação são enviados. Neste exemplo, é chamada de função de retorno de chamada hello **SendConfirmationCallback**. saudação de trecho de código a seguir mostra essa função de retorno de chamada:

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

Observe Olá chamada toohello **IoTHubMessage\_destruir** funcionar quando você terminar com a mensagem de saudação. Essa função libera os recursos de saudação alocados ao criar mensagem de saudação.

### <a name="receive-messages"></a>Receber mensagens

O recebimento de uma mensagem é uma operação assíncrona. Primeiro, é registrar Olá tooinvoke de retorno de chamada quando o dispositivo Olá recebe uma mensagem:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

Olá último parâmetro é um toowhatever de ponteiro nulo desejado. No exemplo hello, é um número inteiro tooan de ponteiro, mas pode ser um ponteiro tooa a estrutura de dados mais complexa. Este parâmetro permite Olá toooperate de função de retorno de chamada no estado compartilhado com chamador Olá dessa função.

Quando o dispositivo Olá recebe uma mensagem, hello função de retorno de chamada registrado é invocada. Essa função de retorno de chamada recupera:

* id de mensagem de saudação e id de correlação da mensagem de saudação.
* conteúdo da mensagem de saudação.
* Todas as propriedades personalizadas da mensagem de saudação.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Saudação de uso **IoTHubMessage\_GetByteArray** mensagem de saudação do função tooretrieve, que neste exemplo é uma cadeia de caracteres.

### <a name="uninitialize-hello-library"></a>Não inicializar a biblioteca de saudação

Quando você terminar de enviar eventos e receber mensagens, você pode não inicializar Olá IoT biblioteca. toodo assim, emita Olá chamada de função a seguir:

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Essa chamada libera recursos Olá anteriormente alocados pelo Olá **IoTHubClient\_CreateFromConnectionString** função.

Como você pode ver, é fácil toosend e receber mensagens de saudação **IoTHubClient** biblioteca. biblioteca Hello trata os detalhes de saudação de se comunicar com o IoT Hub, incluindo qual protocolo toouse (da perspectiva de saudação do desenvolvedor hello, essa é uma opção de configuração simples).

Olá **IoTHubClient** biblioteca também fornece um controle preciso sobre como dados de saudação tooserialize o dispositivo envia tooIoT Hub. Em alguns casos, esse nível de controle é uma vantagem, mas em outros é um detalhe de implementação que você não deseja toobe preocupada com. Se esse for o caso de Olá, você pode considerar o uso Olá **serializador** biblioteca, o que é descrita na próxima seção, Olá.

## <a name="use-hello-serializer-library"></a>Usar a biblioteca de serializador Olá

Olá conceitualmente **serializador** biblioteca fica na parte superior Olá **IoTHubClient** biblioteca no hello SDK. Ele usa Olá **IoTHubClient** biblioteca para Olá subjacente a comunicação com o IoT Hub, mas ele adiciona recursos de modelagem que remove a carga de saudação de lidar com a serialização da mensagem de desenvolvedor hello. O funcionamento dessa biblioteca é mais bem demonstrado por um exemplo.

Olá interna **serializador** pasta Olá [repositório do azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c), é um **exemplos** pasta que contém um aplicativo chamado **simplesample \_mqtt**. versão do Windows Hello deste exemplo inclui Olá após a solução do Visual Studio:

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> Se você abrir este projeto no Visual Studio de 2017, aceite Olá prompts tooretarget Olá toohello mais recente versão do projeto.

Como com o exemplo anterior de hello, este inclui vários pacotes do NuGet:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt

Você viu a maioria desses pacotes no exemplo anterior de saudação, mas **Microsoft.Azure.IoTHub.Serializer** é novo. Este pacote é necessário quando você usar o hello **serializador** biblioteca.

Você pode encontrar a implementação de saudação do aplicativo de exemplo hello no hello **simplesample\_mqtt.c** arquivo.

Olá seções a seguir orientam você durante partes-chave Olá deste exemplo.

### <a name="initialize-hello-library"></a>Inicializar a biblioteca de saudação

toostart trabalhando com hello **serializador** biblioteca, chamada hello inicialização APIs:

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

Olá chamada toohello **serializador\_init** função é uma única chamada e inicializa Olá biblioteca subjacente. Em seguida, você pode chamar hello **IoTHubClient\_LL\_CreateFromConnectionString** função, que é Olá a mesma API como Olá **IoTHubClient** exemplo. Essa chamada define a cadeia de caracteres de conexão do dispositivo (essa chamada também é onde você escolher o protocolo de saudação desejado toouse). Este exemplo usa MQTT como transporte hello, mas pode usar AMQP ou HTTP.

Finalmente, chame Olá **criar\_modelo\_instância** função. **WeatherStation** é o namespace de saudação do modelo de saudação e **ContosoAnemometer** é nome de saudação do modelo de saudação. Depois de criar a instância de modelo hello, você pode usá-lo toostart enviando e recebendo mensagens. No entanto, é importante toounderstand é que um modelo.

### <a name="define-hello-model"></a>Definir modelo Olá

Um modelo no hello **serializador** biblioteca define as mensagens de saudação seu dispositivo pode enviar tooIoT mensagens de Hub e hello, chamadas *ações* em Olá linguagem, que pode receber de modelagem. Definir um modelo usando um conjunto de macros C como Olá **simplesample\_mqtt** aplicativo de exemplo:

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Olá **começar\_NAMESPACE** e **final\_NAMESPACE** ambas as macros levar Olá namespace de modelo hello como um argumento. Espera-se que qualquer coisa entre essas macros é a definição de saudação do seu modelo ou modelos e estruturas de dados de Olá Olá modelos usam.

Neste exemplo, há um único modelo chamado **ContosoAnemometer**. Esse modelo define duas partes de dados que o dispositivo pode enviar tooIoT Hub: **DeviceId** e **WindSpeed**. Ele também define três ações (mensagens) que o dispositivo pode receber: **TurnFanOn**, **TurnFanOff** e **SetAirResistance**. Cada elemento de dados tem um tipo, e cada ação tem um nome (e, opcionalmente, um conjunto de parâmetros).

dados saudação e as ações definidas no modelo de saudação definem uma superfície de API que você pode usar toosend mensagens tooIoT Hub e responder toomessages enviados toohello dispositivo. O uso desse modelo é compreendido melhor por meio de um exemplo.

### <a name="send-messages"></a>Enviar mensagens

modelo de Olá define dados Olá pode enviar tooIoT Hub. Neste exemplo, isso significa que uma saudação dois itens de dados definidos usando Olá **WITH_DATA** macro. Há várias etapas e necessário toosend **DeviceId** e **WindSpeed** hub de IoT tooan valores. Olá é primeiro tooset Olá dados toosend:

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

Olá modelo definido anteriormente permite que você os valores hello tooset definindo membros de um **struct**. Em seguida, serialize a mensagem de saudação desejado toosend:

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

Esse código serializa o buffer de dispositivo para nuvem tooa hello (referenciado por **destino**). código de Hello, em seguida, invoca Olá **sendMessage** função tooIoT de mensagem de saudação toosend Hub:

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


Olá segundo parâmetro toolast de **IoTHubClient\_LL\_SendEventAsync** é uma função de retorno de chamada de tooa de referência que é chamada quando dados saudação são enviados com êxito. Aqui está a função de retorno de chamada hello no exemplo hello:

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

Olá segundo parâmetro é um contexto de toouser ponteiro; Olá ponteiro mesmo passado muito**IoTHubClient\_LL\_SendEventAsync**. Nesse caso, o contexto de saudação é um contador simple, mas pode ser qualquer coisa que você deseja.

Isso é tudo que há mensagens de dispositivo para nuvem toosending. Olá somente coisa toocover é como tooreceive mensagens.

### <a name="receive-messages"></a>Receber mensagens

Receber uma mensagem de funcionamento da mesma forma toohello mensagens funcionam no hello **IoTHubClient** biblioteca. Primeiramente, você registra uma função de retorno de chamada de mensagem:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

Em seguida, você escrever a função de retorno de chamada de saudação que é invocada quando uma mensagem é recebida:

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

Esse código é clichê - ele tem hello mesmo para qualquer solução. Esta função recebe a mensagem de saudação e cuida de roteamento a função apropriada toohello por meio da chamada de saudação muito**EXECUTE\_comando**. função Hello chamada neste ponto depende da definição Olá das ações de saudação em seu modelo.

Quando você define uma ação em seu modelo, será necessário tooimplement uma função que é chamada quando o dispositivo recebe a mensagem de saudação do correspondente. Por exemplo, se o seu modelo definir esta ação:

```c
WITH_ACTION(SetAirResistance, int, Position)
```

Defina uma função com esta assinatura:

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

Observe como o nome de saudação do função hello corresponde o nome de Olá da ação Olá no modelo de saudação e que Olá da função hello correspondem Olá parâmetros especificados para a ação de saudação. Olá primeiro parâmetro é sempre necessário e contém uma instância de toohello ponteiro do seu modelo.

Quando o dispositivo Olá recebe uma mensagem que corresponde a essa assinatura, função correspondente Olá é chamada. Portanto, além de ter tooinclude Olá boilerplate código de **IoTHubMessage**, recebendo mensagens é apenas uma questão de definir uma função simples para cada ação definida no modelo.

### <a name="uninitialize-hello-library"></a>Não inicializar a biblioteca de saudação

Quando você terminar de envio de dados e receber mensagens, você pode não inicializar Olá IoT biblioteca:

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

Cada uma dessas três funções de acordo com hello três funções de inicialização descritas anteriormente. Chamar essas APIs garante a liberação dos recursos alocados anteriormente.

## <a name="next-steps"></a>Próximas etapas

Este artigo coberto Noções básicas de saudação do uso de bibliotecas de saudação em Olá **dispositivo IoT do Azure SDK para C**. Ele acompanha suficiente toounderstand informações que está incluído na Olá SDK, sua arquitetura e como tooget começaram a funcionar com hello exemplos do Windows. artigo Avançar Olá continua descrição Olá Olá SDK explicando [mais informações sobre a biblioteca de IoTHubClient Olá](iot-hub-device-sdk-c-iothubclient.md).

toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá [SDKs do Azure IoT][lnk-sdks].

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
