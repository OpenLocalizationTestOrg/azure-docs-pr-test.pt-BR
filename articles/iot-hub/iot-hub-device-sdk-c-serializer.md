---
title: dispositivo de IoT aaaAzure SDK para C - serializador | Microsoft Docs
description: "Como biblioteca de serializador Olá toouse no dispositivo de Azure IoT Olá SDK para aplicativos de dispositivo de toocreate C que se comunicam com um hub IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>SDK do dispositivo IoT do Azure para C – mais sobre o serializador
Olá [primeiro artigo](iot-hub-device-sdk-c-intro.md) em Olá essa série introduzido **dispositivo IoT do Azure SDK para C**. artigo Avançar Olá fornecida uma descrição mais detalhada da saudação [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md). Este artigo é concluída cobertura de saudação SDK, fornecendo uma descrição mais detalhada da saudação restantes componente: Olá **serializador** biblioteca.

artigo introdutório Hello, como descrito Olá toouse **serializador** biblioteca toosend eventos tooand receber mensagens de IoT Hub. Neste artigo, estendemos essa discussão, fornecendo uma explicação mais completa de como toomodel seus dados com hello **serializador** linguagem de macro. Olá também inclui mais detalhes sobre como a biblioteca de saudação serializa mensagens (e, em alguns casos como você pode controlar o comportamento de serialização Olá). Também descreveremos alguns parâmetros que você pode modificar que determinam o tamanho Olá dos modelos de saudação que você criar.

Finalmente, o artigo Olá revisitar alguns tópicos abordados nos artigos anteriores, como mensagens e manipulação de propriedade. Como descobriremos o trabalho esses recursos em Olá mesmo maneira usando Olá **serializador** biblioteca que funcionam com hello **IoTHubClient** biblioteca.

Tudo descrito neste artigo se baseia Olá **serializador** amostras do SDK. Se você quiser toofollow ao longo, consulte Olá **simplesample\_amqp** e **simplesample\_http** aplicativos incluídos no dispositivo do hello IoT do Azure SDK para C.

Você pode encontrar hello [ **dispositivo IoT do Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositório e exibir os detalhes de saudação API no hello [referência da API C](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-modeling-language"></a>linguagem de modelagem Olá
Olá [artigo introdutório](iot-hub-device-sdk-c-intro.md) em Olá essa série introduzido **dispositivo IoT do Azure SDK para C** modelagem por meio do exemplo hello fornecido no hello **simplesample\_amqp**  aplicativo:

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Como você pode ver, Olá linguagem de modelagem é baseado em macros do C. Sempre comece sua definição com **BEGIN\_NAMESPACE** e sempre termine com **END\_NAMESPACE**. É comum tooname Olá espaço para nome de sua empresa ou, como neste exemplo, o projeto Olá que você está trabalhando.

O que acontece dentro do namespace de saudação são definições de modelo. Neste caso, há um único modelo para um anemômetro. Novamente, o modelo Olá pode ter qualquer nome, mas normalmente isso é chamado de dispositivo de saudação ou tipo de dados você deseja tooexchange com o IoT Hub.  

Modelos contêm uma definição de eventos hello, você pode tooIoT entrada Hub (Olá *dados*), bem como mensagens de saudação receber IoT Hub (Olá *ações*). Como você pode ver do exemplo hello, eventos têm um tipo e um nome. as ações têm um nome e parâmetros opcionais (cada um com um tipo).

O que não será demonstrado neste exemplo são tipos de dados adicionais que são suportados pelo Olá SDK. Abordaremos isso na sequência.

> [!NOTE]
> IoT Hub refere-se a dados toohello um dispositivo envia tooit como *eventos*, enquanto a linguagem de modelagem de saudação refere-se tooit como *dados* (definido usando **WITH_DATA**). Da mesma forma, o IoT Hub refere-se dados toohello enviar toodevices como *mensagens*, enquanto a linguagem de modelagem de saudação refere-se tooit como *ações* (definido usando **WITH_ACTION**). Saiba que esses termos podem ser usados de forma intercambiável neste artigo.
> 
> 

### <a name="supported-data-types"></a>Tipos de dados com suporte
Olá, tipos de dados a seguir têm suporte em modelos criados com hello **serializador** biblioteca:

| Tipo | Descrição |
| --- | --- |
| double |número de ponto flutuante de precisão dupla |
| int |inteiro de 32 bits |
| flutuante |número de ponto flutuante de precisão única |
| longo |inteiro longo |
| int8\_t |inteiro de 8 bits |
| int16\_t |inteiro de 16 bits |
| int32\_t |inteiro de 32 bits |
| int64\_t |inteiro de 64 bits |
| bool |Booliano |
| ascii\_char\_ptr |Cadeia de caracteres ASCII |
| EDM\_DATE\_TIME\_OFFSET |diferença de data e horário |
| EDM\_GUID |GUID |
| EDM\_BINARY |binário |
| DECLARE\_STRUCT |tipo de dados complexo |

Vamos começar com hello último tipo de dados. Olá **DECLARE\_STRUCT** permite a você os tipos de dados complexos de toodefine, que são agrupamentos de saudação outros tipos primitivos. Esses agrupamentos nos permitem toodefine um modelo que tem esta aparência:

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

Nosso modelo contém um único evento de dados do tipo **TestType**. **TestType** é um tipo complexo que inclui vários membros, que coletivamente demonstram os tipos primitivos Olá Olá com suporte **serializador** linguagem de modelagem.

Com um modelo como este, podemos escrever código toosend dados tooIoT Hub que aparece da seguinte maneira:

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

Basicamente, está sendo atribuído um membro de tooevery valor de saudação **teste** estrutura e, em seguida, chamar **SendAsync** toosend Olá **teste** de dados evento toohello na nuvem. **SendAsync** é uma função auxiliar que envia um evento de dados único tooIoT Hub:

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

Essa função serializa Olá recebe eventos de dados e envia tooIoT Hub usando **IoTHubClient\_SendEventAsync**. Isso é hello mesmo código discutido nos artigos anteriores (**SendAsync** encapsula a lógica de saudação em uma função conveniente).

É uma outra função auxiliar usada no código anterior Olá **GetDateTimeOffset**. Essa função transforma Olá momento determinado em um valor do tipo **EDM\_data\_tempo\_deslocamento**:

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

Se você executar esse código, a seguinte mensagem de saudação é enviada tooIoT Hub:

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Observe que a serialização de saudação é JSON, que é o formato de saudação gerado pelo Olá **serializador** biblioteca. Também Observe que cada membro da saudação serializado objeto JSON corresponde membros Olá Olá **TestType** que definimos em nosso modelo. Olá valores também exatamente correspondam aos valores usados no código de saudação. No entanto, observe que os dados binários Olá são codificada em base64: "AQID" é Olá codificação base64 de {0x01, 0x02, 0x03}.

Este exemplo demonstra a vantagem de saudação do uso de saudação **serializador** biblioteca---permite que nós toosend JSON toohello nuvem, sem ter que lidar com a serialização em nosso aplicativo tooexplicitly. Temos tooworry sobre está definindo valores Olá Olá eventos de dados em nosso modelo e, em seguida, chamando toosend simple de APIs nuvem de toohello esses eventos.

Com essas informações, podemos definir modelos que incluem o intervalo de saudação de tipos de dados com suporte, incluindo tipos complexos (mesmo que pode incluir tipos complexos em outros tipos complexos). No entanto, ele serializado JSON gerado pelo Olá exemplo acima abre um ponto importante. *Como* podemos enviar dados por hello **serializador** biblioteca determina exatamente como Olá JSON é formado. Abordaremos esse ponto específico na sequência.

## <a name="more-about-serialization"></a>Mais informações sobre a serialização
seção anterior Olá realça um exemplo de saída de hello gerado pelo Olá **serializador** biblioteca. Nesta seção, vamos explicar como biblioteca Olá serializa os dados e como você pode controlar esse comportamento usando APIs de serialização de saudação.

Ordem tooadvance Olá sobre serialização, trabalharemos com um novo modelo com base em um termostato. Primeiro, vamos fornecer algumas informações no cenário de saudação tooaddress estamos tentando.

Queremos toomodel um termostato que mede a temperatura e umidade. Cada parte dos dados será toobe enviado tooIoT Hub de maneira diferente. Por padrão, Olá ingresses termostato um evento de temperatura uma vez a cada 2 minutos; um evento de umidade é ingressed uma vez a cada 15 minutos. Quando o evento é ingressed, ele deve incluir um carimbo de hora que mostra o tempo de saudação que correspondente a temperatura hello ou umidade foi medida.

Devido a esse cenário, demonstraremos dois modos diferentes toomodel Olá de dados e explicaremos efeito Olá que modelagem tem em Olá serializado saída.

### <a name="model-1"></a>Modelo 1
Aqui está o hello primeira versão de um modelo que oferece suporte a Olá cenário anterior:

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

Observe que esse modelo Olá inclui dois eventos de dados: **temperatura** e **umidade**. Ao contrário de exemplos anteriores, o tipo de saudação de cada evento é uma estrutura definida usando **DECLARE\_STRUCT**. **TemperatureEvent** inclui uma medição de temperatura e um carimbo de data e hora; **HumidityEvent** contém uma medição de umidade e um carimbo de data e hora. Esse modelo fornece um modo natural toomodel Olá de dados para o cenário Olá descrito acima. Quando podemos enviar uma nuvem de toohello de evento, ou enviaremos um temperatura/carimbo de hora ou um par de umidade/timestamp.

Podemos enviar uma nuvem de toohello temperatura eventos usando código como Olá seguinte:

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Podemos vai usar valores codificados para temperatura e umidade no código de exemplo hello, mas imagine que, na verdade, recuperando esses valores por amostragem sensores de saudação correspondente em termostato hello.

código de saudação acima usa Olá **GetDateTimeOffset** auxiliar que foi apresentado anteriormente. Por motivos que se tornarão desmarque posteriores, esse código explicitamente separa tarefa Olá de serialização e enviar evento hello. código anterior Olá serializa eventos de temperatura Olá em um buffer. Em seguida, **sendMessage** é uma função auxiliar (incluído no **simplesample\_amqp**) que envia Olá evento tooIoT Hub:

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

Esse código é um subconjunto de saudação **SendAsync** auxiliar descrita na seção anterior do hello, portanto não entraremos sobre ele novamente aqui.

Quando executamos evento Olá anterior código toosend Olá temperatura, esse formato serializado do evento Olá é enviado tooIoT Hub:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Estamos enviando uma temperatura que pertence ao tipo **TemperatureEvent** e esse struct contém um membro **Temperature** e outro **Time**. Isso é refletido diretamente nos dados Olá serializado.

Da mesma forma, podemos enviar um evento de umidade com este código:

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

formulário de saudação serializado que enviou tooIoT Hub aparece da seguinte maneira:

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Novamente, tudo conforme o esperado.

Com esse modelo, você pode imaginar como outros eventos podem ser facilmente adicionados. Definir mais de estruturas usando **DECLARE\_STRUCT**e incluem o evento correspondente Olá Olá modelo usando **WITH\_dados**.

Agora, vamos modificar o modelo Olá para que ela inclua Olá mesmos dados, mas com uma estrutura diferente.

### <a name="model-2"></a>Modelo 2
Considere este toohello modelo alternativo um acima:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Nesse caso, eliminamos Olá **DECLARE\_STRUCT** macros e são simplesmente definindo itens de dados de saudação do nosso cenário usando tipos simples de saudação linguagem de modelagem.

Para o momento de saudação vamos ignorar Olá **tempo** eventos. Com essa aside, eis Olá código tooingress **temperatura**:

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Esse código envia seguinte Olá serializado evento tooIoT Hub:

```
{"Temperature":75}
```

E código hello para enviar eventos de umidade Olá aparece da seguinte maneira:

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Esse código envia esse Hub tooIoT:

```
{"Humidity":45}
```

Até o momento, ainda não há surpresas. Agora vamos alterar como usamos macro de SERIALIZAR hello.

Olá **SERIALIZE** macro pode levar vários eventos de dados como argumentos. Isso nos permite Olá tooserialize **temperatura** e **umidade** evento junto e enviá-los tooIoT Hub em uma chamada:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Você pode imaginar que resultados de saudação do código é que os eventos de dois dados são enviados tooIoT Hub:

[

{"Temperatura":75},

{"Umidade":45}

]

Em outras palavras, você pode esperar que esse código é mesmo Olá como enviar **temperatura** e **umidade** separadamente. É apenas uma toopass conveniência ambos os eventos muito**SERIALIZE** Olá mesmo chamar. No entanto, esse não for o caso de saudação. Em vez disso, código de saudação acima envia esse evento de dados único tooIoT Hub:

{"Temperatura":75, "Umidade":45}

Isso pode parecer estranho, pois nosso modelo define **Temperature** e **Humidity** como dois eventos *separados*:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Mais toohello um ponto, podemos não modelar estes eventos onde **temperatura** e **umidade** estão em Olá mesma estrutura:

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

Se usarmos esse modelo, poderá ser mais fácil toounderstand como **temperatura** e **umidade** será enviado em Olá mesmo serializado mensagem. No entanto talvez não seja criptografado por ele funciona dessa forma, quando você passa os dois eventos de dados muito**SERIALIZE** usando o modelo de 2.

Esse comportamento é toounderstand mais fácil se você souber suposições Olá que Olá **serializador** biblioteca está fazendo. sentido de toomake isso vamos voltar tooour modelo:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Pense nesse modelo em termos orientados ao objeto. Neste caso, estamos modelando um dispositivo físico (um termostato), e esse dispositivo inclui atributos como **Temperature** e **Humidity**.

Podemos enviar todo o estado de nosso modelo de código, como a seguir Olá Olá:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Supondo que Olá valores de temperatura, umidade e tempo são definidos, veremos um evento como esse tooIoT enviado Hub:

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Às vezes você pode desejar somente toosend *alguns* propriedades de nuvem de toohello modelo hello (Isso é especialmente verdadeiro se o seu modelo contiver um grande número de eventos de dados). É útil toosend apenas um subconjunto de eventos de dados, como em nosso exemplo anterior:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Isso gera exatamente Olá mesmo serializado eventos como se tivesse definimos um **TemperatureEvent** com um **temperatura** e **tempo** membro, como usamos com modelos de 1. Nesse caso foi capaz de toogenerate exatamente hello mesmo serializado eventos usando um modelo diferente (modelo 2) porque é chamado **SERIALIZE** de maneira diferente.

Olá ponto importante é que, se você passar vários eventos de dados muito**SERIALIZE,** , em seguida, ele assume que cada evento é uma propriedade em um único objeto JSON.

abordagem recomendada Olá depende de você e como você pensar em seu modelo. Se você estiver enviando "eventos de" nuvem toohello e cada evento contém um conjunto definido de propriedades, primeira abordagem de saudação faz muito sentido. Nesse caso você usaria **DECLARE\_STRUCT** toodefine Olá a estrutura de cada evento e, em seguida, incluí-los em seu modelo com hello **WITH\_dados** macro. Em seguida, você enviar cada evento como foi Olá primeiro exemplo acima. Nessa abordagem, você só passaria um evento único de dados muito**SERIALIZADOR**.

Se você pensar em seu modelo de forma orientada a objeto, em seguida, segunda abordagem de saudação pode suas necessidades. Nesse caso, Olá elementos definidos usando **WITH\_dados** hello "propriedades" de seu objeto. Você passar qualquer subconjunto de eventos muito**SERIALIZE** que desejar, dependendo de quanto o estado do objeto"" deseja toosend toohello nuvem.

Nenhuma abordagem é certa ou errada. Apenas esteja ciente de como Olá **serializador** biblioteca funciona e a abordagem de modelagem de saudação pick que melhor atenda às suas necessidades.

## <a name="message-handling"></a>Manipulação de mensagens
Até o momento neste artigo somente discutiu enviar eventos tooIoT Hub e não resolvidos de recebimento de mensagens. Olá motivo para isso é que precisamos tooknow sobre o recebimento de mensagens em grande parte foi abordado em um [anteriormente artigo](iot-hub-device-sdk-c-intro.md). O artigo mostrava o processamento de mensagens por meio do registro de uma função de retorno de chamada da mensagem:

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

Você, em seguida, escrever a função de retorno de chamada de saudação que é invocada quando uma mensagem é recebida:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
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

Essa implementação de **IoTHubMessage** Olá de chamadas de função específica para cada ação em seu modelo. Por exemplo, se o seu modelo definir esta ação:

```
WITH_ACTION(SetAirResistance, int, Position)
```

Você deverá definir uma função com esta assinatura:

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** é chamado quando ela é enviada tooyour dispositivo.

Ainda que ainda não explicar é qual versão Olá serializado da mensagem é semelhante. Em outras palavras, se você quiser toosend um **SetAirResistance** dispositivo de tooyour de mensagem, o que parecidos com?

Se você estiver enviando um dispositivo de tooa de mensagem, você faria isso por meio do SDK do serviço de Azure IoT hello. Você ainda precisa tooknow conteúdo string toosend tooinvoke uma ação específica. formato geral de Hello para enviar uma mensagem aparece da seguinte maneira:

```
{"Name" : "", "Parameters" : "" }
```

Você está enviando um objeto JSON serializado com duas propriedades: **nome** é Olá nome da ação de saudação (mensagem) e **parâmetros** contém parâmetros de saudação da ação.

Por exemplo, tooinvoke **SetAirResistance** você pode enviar este dispositivo tooa de mensagem:

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

nome da ação Olá deve corresponder exatamente uma ação definida no modelo. nomes de parâmetro Hello devem corresponder também. Observe também a diferenciação de maiúsculas e minúsculas. **Name** e **Parameters** devem estar sempre com a primeira letra maiúscula. Certifique-se de que caso de Olá toomatch de seus parâmetros e o nome da ação em seu modelo. Neste exemplo, o nome da ação Olá é "SetAirResistance" e não "setairresistance".

Olá duas outras ações **TurnFanOn** e **TurnFanOff** podem ser invocados pelo dispositivo de tooa essas mensagens de envio:

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

Esta seção descreveu tudo o que você precisa tooknow quando eventos de envio e recebimento de mensagens com hello **serializador** biblioteca. Antes de continuarmos, vamos abordar alguns parâmetros que você pode configurar e que controlam o tamanho de seu modelo.

## <a name="macro-configuration"></a>Configuração de macro
Se você estiver usando Olá **serializador** biblioteca uma parte importante da saudação SDK toobe atento foi encontrada na biblioteca do azure-c-compartilhado-utilitário hello.
Se você clonou repositório hello Azure-iot-sdk-c do GitHub usando hello – recursiva opção, você encontrará esta biblioteca de utilitário compartilhados aqui:

```
.\\c-utility
```

Se você não tiver clonado biblioteca hello, você pode encontrar [aqui](https://github.com/Azure/azure-c-shared-utility).

Biblioteca de utilitário compartilhados hello, você encontrará Olá pasta a seguir:

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

Essa pasta contém uma solução do Visual Studio chamada **macro\_utils\_h\_generator.sln**:

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

programa de saudação nesta solução gera Olá **macro\_utils.h** arquivo. Há uma macro padrão\_utils.h arquivo incluído Olá SDK. Esta solução permite que você toomodify alguns parâmetros e, em seguida, recrie Olá arquivo de cabeçalho com base nesses parâmetros.

Olá dois parâmetros de chave toobe preocupada com são **nArithmetic** e **nMacroParameters** que é definido nestas duas linhas encontradas em macro\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

Esses valores são parâmetros de padrão de saudação incluídos Olá SDK. Cada parâmetro tem Olá significado a seguir:

* nMacroParameters – controla a quantidade de parâmetros que você pode ter em uma definição de macro DECLARE\_MODEL.
* nArithmetic – controles Olá total de membros permitidos em um modelo.

motivo Olá que esses parâmetros são importantes é porque eles controlam quanto seu modelo pode ser. Por exemplo, veja esta definição de modelo:

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

Como mencionado anteriormente, **DECLARE\_MODEL** é apenas uma macro de C. Olá nomes de modelo hello e hello **WITH\_dados** instrução (ainda outra macro) é parâmetros de **DECLARE\_modelo**. **nMacroParameters** define o número de parâmetros que pode ser incluído em **DECLARE\_MODEL**. Efetivamente, isso define quantos eventos de dados e declarações de ação você pode ter. Dessa forma, com limite de padrão de saudação de 124 isso significa que você pode definir um modelo com uma combinação de aproximadamente 60 ações e eventos de dados. Se você tentar tooexceed esse limite, você receberá erros de compilador que procuram toothis semelhante:

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

Olá **nArithmetic** parâmetro é mais sobre o funcionamento interno de saudação do idioma de macro Olá de seu aplicativo.  Ele controla o número total de saudação de membros, você pode ter em seu modelo, incluindo **DECLARE_STRUCT** macros. Portanto, se começar a ver erros do compilador como esse, tente aumentar **nArithmetic**:

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Se você quiser toochange esses parâmetros, modifique os valores de saudação em macro Olá\_utils.tt arquivo, recompile Olá macro\_utilitários\_h\_generator.sln solução e o programa compilado Olá execução. Ao fazer isso, uma nova macro\_utils.h arquivo é gerado e inserido no hello.\\ comuns\\directory inc.

Em ordem toouse Olá nova versão da macro\_utils.h, remover Olá **serializador** pacote NuGet de sua solução e em seu lugar incluem hello **serializador** projeto do Visual Studio. Isso permite que o toocompile de código no código-fonte da biblioteca do serializador Olá Olá. Isso inclui a macro Olá atualizado\_utils.h. Se você deseja toodo para **simplesample\_amqp**, iniciar, removendo o pacote do NuGet Olá para a biblioteca de serializador Olá de solução hello:

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

Em seguida, adicione tooyour esse projeto solução do Visual Studio:

> .\\c\\serializer\\build\\windows\\serializer.vcxproj
> 
> 

Quando terminar, sua solução deve ter esta aparência:

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

Agora, quando você compila sua solução, hello atualizado macro\_utils.h está incluído em seu binário.

Observe que aumentar demais esses valores pode exceder os limites do compilador. toothis ponto, hello **nMacroParameters** é Olá parâmetro principal que toobe em questão. especificação de C99 Olá Especifica que um mínimo de 127 parâmetros são permitidas em uma definição de macro. Olá compilador Microsoft segue a especificação de saudação exatamente (e tem um limite de 127), portanto, não será capaz de tooincrease **nMacroParameters** além do padrão de saudação. Outros compiladores podem permitir toodo assim (por exemplo, compilador de GNU Olá dá suporte a um limite superior).

Até agora falamos sobre tudo o que você precisa tooknow sobre como toowrite com o código Olá **serializador** biblioteca. Antes da conclusão, vamos rever alguns tópicos dos artigos anteriores sobre os quais você pode estar se perguntando.

## <a name="hello-lower-level-apis"></a>Olá APIs de nível inferior
aplicativo de exemplo Hello na qual focalizado neste artigo é **simplesample\_amqp**. Este exemplo usa Olá nível mais alto (Olá não-"tudo") APIs toosend eventos e receber mensagens. Se você usar essas APIs, haverá um thread em execução em segundo plano que cuida dos eventos de envio e do recebimento de mensagens. No entanto, você pode usar Olá nível inferior (IL) APIs tooeliminate esse thread em segundo plano e assumir o controle explícito sobre o envio de eventos ou receber mensagens de nuvem hello.

Conforme descrito em uma [artigo anterior](iot-hub-device-sdk-c-iothubclient.md), há um conjunto de funções que consiste em Olá APIs de nível superior:

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_Destroy

Essas APIs são demonstradas em **simplesample\_amqp**.

Há também um conjunto análogo de APIs de nível inferior.

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

Observe que trabalho de APIs de nível inferior Olá exatamente Olá mesma maneira que descrito nos artigos da saudação anterior. Você pode usar o primeiro conjunto de APIs de saudação se você quiser um toohandle de thread em segundo plano eventos de envio e recebimento de mensagens. Use o segundo conjunto de APIs de saudação se desejar que o controle explícito sobre quando você envia e recebe dados de IoT Hub. O conjunto de APIs trabalho igualmente bem com hello **serializador** biblioteca.

Para obter um exemplo de como hello APIs de nível inferior são usados com hello **serializador** biblioteca, consulte Olá **simplesample\_http** aplicativo.

## <a name="additional-topics"></a>Tópicos adicionais
Outros tópicos que vale a pena mencionar novamente são relacionados ao tratamento de propriedades, ao uso de credenciais alternativas de dispositivo e às opções de configuração. Todos estes tópicos foram abordados em um [artigo anterior](iot-hub-device-sdk-c-iothubclient.md). Olá ponto principal é que todos esses recursos funcionam em Olá mesma maneira com hello **serializador** biblioteca que funcionam com hello **IoTHubClient** biblioteca. Por exemplo, se você quiser tooattach eventos de tooan de propriedades do modelo, use **IoTHubMessage\_propriedades** e **mapa**\_**AddorUpdate**, Olá mesma maneira que descrita anteriormente:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Se o evento de saudação foi gerado de saudação **serializador** biblioteca ou criados manualmente usando Olá **IoTHubClient** biblioteca não importa.

Para Olá credenciais de dispositivo, usando alternativas **IoTHubClient\_LL\_criar** funciona tão bem como **IoTHubClient\_CreateFromConnectionString** para alocar um **hub IOT\_cliente\_tratar**.

Por fim, se você estiver usando Olá **serializador** biblioteca, você pode definir opções de configuração com **IoTHubClient\_LL\_SetOption** assim como você fez ao usar Olá **IoTHubClient** biblioteca.

Um recurso que é exclusivo toohello **serializador** biblioteca são inicialização Olá APIs. Antes de começar a trabalhar com a biblioteca de saudação, você deve chamar **serializador\_init**:

```
serializer_init(NULL);
```

Isso é feito antes de chamar **IoTHubClient\_CreateFromConnectionString**.

Da mesma forma, quando você terminar trabalhando com biblioteca de hello, última chamada de saudação fará é muito**serializador\_deinit**:

```
serializer_deinit();
```

Caso contrário, todos os Olá outros recursos listados acima trabalho Olá mesmo em Olá **serializador** biblioteca como funcionaria em Olá **IoTHubClient** biblioteca. Para obter mais informações sobre qualquer um desses tópicos, consulte Olá [artigo anterior](iot-hub-device-sdk-c-iothubclient.md) na série.

## <a name="next-steps"></a>Próximas etapas
Este artigo descreve em aspectos exclusivos de saudação de detalhes de saudação **serializador** biblioteca contida em Olá **dispositivo IoT do Azure SDK para C**. Com informações de saudação fornecidas, você deve ter uma boa compreensão de como os modelos de toouse toosend eventos e receber mensagens de IoT Hub.

Isso também conclui a série de três partes Olá em como os aplicativos toodevelop com hello **dispositivo IoT do Azure SDK para C**. Isso deve ser suficiente informações toonot somente introdução você mas lhe oferece uma compreensão completa de como funcionam Olá APIs. Para obter informações adicionais, há alguns exemplos em Olá que SDK não abordado aqui. Caso contrário, Olá [documentação do SDK](https://github.com/Azure/azure-iot-sdk-c) é um bom recurso para obter informações adicionais.

toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá [SDKs do Azure IoT][lnk-sdks].

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
