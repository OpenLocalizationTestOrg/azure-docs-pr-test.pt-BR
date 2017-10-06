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
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="9a1c5-103">SDK do dispositivo IoT do Azure para C – mais sobre o serializador</span><span class="sxs-lookup"><span data-stu-id="9a1c5-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="9a1c5-104">Olá [primeiro artigo](iot-hub-device-sdk-c-intro.md) em Olá essa série introduzido **dispositivo IoT do Azure SDK para C**. artigo Avançar Olá fornecida uma descrição mais detalhada da saudação [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="9a1c5-105">Este artigo é concluída cobertura de saudação SDK, fornecendo uma descrição mais detalhada da saudação restantes componente: Olá **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="9a1c5-106">artigo introdutório Hello, como descrito Olá toouse **serializador** biblioteca toosend eventos tooand receber mensagens de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="9a1c5-107">Neste artigo, estendemos essa discussão, fornecendo uma explicação mais completa de como toomodel seus dados com hello **serializador** linguagem de macro.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="9a1c5-108">Olá também inclui mais detalhes sobre como a biblioteca de saudação serializa mensagens (e, em alguns casos como você pode controlar o comportamento de serialização Olá).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="9a1c5-109">Também descreveremos alguns parâmetros que você pode modificar que determinam o tamanho Olá dos modelos de saudação que você criar.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="9a1c5-110">Finalmente, o artigo Olá revisitar alguns tópicos abordados nos artigos anteriores, como mensagens e manipulação de propriedade.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="9a1c5-111">Como descobriremos o trabalho esses recursos em Olá mesmo maneira usando Olá **serializador** biblioteca que funcionam com hello **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="9a1c5-112">Tudo descrito neste artigo se baseia Olá **serializador** amostras do SDK.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="9a1c5-113">Se você quiser toofollow ao longo, consulte Olá **simplesample\_amqp** e **simplesample\_http** aplicativos incluídos no dispositivo do hello IoT do Azure SDK para C.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="9a1c5-114">Você pode encontrar hello [ **dispositivo IoT do Azure SDK para C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repositório e exibir os detalhes de saudação API no hello [referência da API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="9a1c5-115">linguagem de modelagem Olá</span><span class="sxs-lookup"><span data-stu-id="9a1c5-115">hello modeling language</span></span>
<span data-ttu-id="9a1c5-116">Olá [artigo introdutório](iot-hub-device-sdk-c-intro.md) em Olá essa série introduzido **dispositivo IoT do Azure SDK para C** modelagem por meio do exemplo hello fornecido no hello **simplesample\_amqp**  aplicativo:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="9a1c5-117">Como você pode ver, Olá linguagem de modelagem é baseado em macros do C.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="9a1c5-118">Sempre comece sua definição com **BEGIN\_NAMESPACE** e sempre termine com **END\_NAMESPACE**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="9a1c5-119">É comum tooname Olá espaço para nome de sua empresa ou, como neste exemplo, o projeto Olá que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="9a1c5-120">O que acontece dentro do namespace de saudação são definições de modelo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="9a1c5-121">Neste caso, há um único modelo para um anemômetro.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="9a1c5-122">Novamente, o modelo Olá pode ter qualquer nome, mas normalmente isso é chamado de dispositivo de saudação ou tipo de dados você deseja tooexchange com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="9a1c5-123">Modelos contêm uma definição de eventos hello, você pode tooIoT entrada Hub (Olá *dados*), bem como mensagens de saudação receber IoT Hub (Olá *ações*).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="9a1c5-124">Como você pode ver do exemplo hello, eventos têm um tipo e um nome. as ações têm um nome e parâmetros opcionais (cada um com um tipo).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="9a1c5-125">O que não será demonstrado neste exemplo são tipos de dados adicionais que são suportados pelo Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="9a1c5-126">Abordaremos isso na sequência.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="9a1c5-127">IoT Hub refere-se a dados toohello um dispositivo envia tooit como *eventos*, enquanto a linguagem de modelagem de saudação refere-se tooit como *dados* (definido usando **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="9a1c5-128">Da mesma forma, o IoT Hub refere-se dados toohello enviar toodevices como *mensagens*, enquanto a linguagem de modelagem de saudação refere-se tooit como *ações* (definido usando **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="9a1c5-129">Saiba que esses termos podem ser usados de forma intercambiável neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="9a1c5-130">Tipos de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="9a1c5-130">Supported data types</span></span>
<span data-ttu-id="9a1c5-131">Olá, tipos de dados a seguir têm suporte em modelos criados com hello **serializador** biblioteca:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="9a1c5-132">Tipo</span><span class="sxs-lookup"><span data-stu-id="9a1c5-132">Type</span></span> | <span data-ttu-id="9a1c5-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="9a1c5-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9a1c5-134">double</span><span class="sxs-lookup"><span data-stu-id="9a1c5-134">double</span></span> |<span data-ttu-id="9a1c5-135">número de ponto flutuante de precisão dupla</span><span class="sxs-lookup"><span data-stu-id="9a1c5-135">double precision floating point number</span></span> |
| <span data-ttu-id="9a1c5-136">int</span><span class="sxs-lookup"><span data-stu-id="9a1c5-136">int</span></span> |<span data-ttu-id="9a1c5-137">inteiro de 32 bits</span><span class="sxs-lookup"><span data-stu-id="9a1c5-137">32 bit integer</span></span> |
| <span data-ttu-id="9a1c5-138">flutuante</span><span class="sxs-lookup"><span data-stu-id="9a1c5-138">float</span></span> |<span data-ttu-id="9a1c5-139">número de ponto flutuante de precisão única</span><span class="sxs-lookup"><span data-stu-id="9a1c5-139">single precision floating point number</span></span> |
| <span data-ttu-id="9a1c5-140">longo</span><span class="sxs-lookup"><span data-stu-id="9a1c5-140">long</span></span> |<span data-ttu-id="9a1c5-141">inteiro longo</span><span class="sxs-lookup"><span data-stu-id="9a1c5-141">long integer</span></span> |
| <span data-ttu-id="9a1c5-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="9a1c5-142">int8\_t</span></span> |<span data-ttu-id="9a1c5-143">inteiro de 8 bits</span><span class="sxs-lookup"><span data-stu-id="9a1c5-143">8 bit integer</span></span> |
| <span data-ttu-id="9a1c5-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="9a1c5-144">int16\_t</span></span> |<span data-ttu-id="9a1c5-145">inteiro de 16 bits</span><span class="sxs-lookup"><span data-stu-id="9a1c5-145">16 bit integer</span></span> |
| <span data-ttu-id="9a1c5-146">int32\_t</span><span class="sxs-lookup"><span data-stu-id="9a1c5-146">int32\_t</span></span> |<span data-ttu-id="9a1c5-147">inteiro de 32 bits</span><span class="sxs-lookup"><span data-stu-id="9a1c5-147">32 bit integer</span></span> |
| <span data-ttu-id="9a1c5-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="9a1c5-148">int64\_t</span></span> |<span data-ttu-id="9a1c5-149">inteiro de 64 bits</span><span class="sxs-lookup"><span data-stu-id="9a1c5-149">64 bit integer</span></span> |
| <span data-ttu-id="9a1c5-150">bool</span><span class="sxs-lookup"><span data-stu-id="9a1c5-150">bool</span></span> |<span data-ttu-id="9a1c5-151">Booliano</span><span class="sxs-lookup"><span data-stu-id="9a1c5-151">boolean</span></span> |
| <span data-ttu-id="9a1c5-152">ascii\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="9a1c5-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="9a1c5-153">Cadeia de caracteres ASCII</span><span class="sxs-lookup"><span data-stu-id="9a1c5-153">ASCII string</span></span> |
| <span data-ttu-id="9a1c5-154">EDM\_DATE\_TIME\_OFFSET</span><span class="sxs-lookup"><span data-stu-id="9a1c5-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="9a1c5-155">diferença de data e horário</span><span class="sxs-lookup"><span data-stu-id="9a1c5-155">date time offset</span></span> |
| <span data-ttu-id="9a1c5-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="9a1c5-156">EDM\_GUID</span></span> |<span data-ttu-id="9a1c5-157">GUID</span><span class="sxs-lookup"><span data-stu-id="9a1c5-157">GUID</span></span> |
| <span data-ttu-id="9a1c5-158">EDM\_BINARY</span><span class="sxs-lookup"><span data-stu-id="9a1c5-158">EDM\_BINARY</span></span> |<span data-ttu-id="9a1c5-159">binário</span><span class="sxs-lookup"><span data-stu-id="9a1c5-159">binary</span></span> |
| <span data-ttu-id="9a1c5-160">DECLARE\_STRUCT</span><span class="sxs-lookup"><span data-stu-id="9a1c5-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="9a1c5-161">tipo de dados complexo</span><span class="sxs-lookup"><span data-stu-id="9a1c5-161">complex data type</span></span> |

<span data-ttu-id="9a1c5-162">Vamos começar com hello último tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="9a1c5-163">Olá **DECLARE\_STRUCT** permite a você os tipos de dados complexos de toodefine, que são agrupamentos de saudação outros tipos primitivos.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="9a1c5-164">Esses agrupamentos nos permitem toodefine um modelo que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-164">These groupings allow us toodefine a model that looks like this:</span></span>

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

<span data-ttu-id="9a1c5-165">Nosso modelo contém um único evento de dados do tipo **TestType**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="9a1c5-166">**TestType** é um tipo complexo que inclui vários membros, que coletivamente demonstram os tipos primitivos Olá Olá com suporte **serializador** linguagem de modelagem.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="9a1c5-167">Com um modelo como este, podemos escrever código toosend dados tooIoT Hub que aparece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="9a1c5-168">Basicamente, está sendo atribuído um membro de tooevery valor de saudação **teste** estrutura e, em seguida, chamar **SendAsync** toosend Olá **teste** de dados evento toohello na nuvem.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="9a1c5-169">**SendAsync** é uma função auxiliar que envia um evento de dados único tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

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

<span data-ttu-id="9a1c5-170">Essa função serializa Olá recebe eventos de dados e envia tooIoT Hub usando **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="9a1c5-171">Isso é hello mesmo código discutido nos artigos anteriores (**SendAsync** encapsula a lógica de saudação em uma função conveniente).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="9a1c5-172">É uma outra função auxiliar usada no código anterior Olá **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="9a1c5-173">Essa função transforma Olá momento determinado em um valor do tipo **EDM\_data\_tempo\_deslocamento**:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="9a1c5-174">Se você executar esse código, a seguinte mensagem de saudação é enviada tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="9a1c5-175">Observe que a serialização de saudação é JSON, que é o formato de saudação gerado pelo Olá **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="9a1c5-176">Também Observe que cada membro da saudação serializado objeto JSON corresponde membros Olá Olá **TestType** que definimos em nosso modelo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="9a1c5-177">Olá valores também exatamente correspondam aos valores usados no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="9a1c5-178">No entanto, observe que os dados binários Olá são codificada em base64: "AQID" é Olá codificação base64 de {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="9a1c5-179">Este exemplo demonstra a vantagem de saudação do uso de saudação **serializador** biblioteca---permite que nós toosend JSON toohello nuvem, sem ter que lidar com a serialização em nosso aplicativo tooexplicitly.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="9a1c5-180">Temos tooworry sobre está definindo valores Olá Olá eventos de dados em nosso modelo e, em seguida, chamando toosend simple de APIs nuvem de toohello esses eventos.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="9a1c5-181">Com essas informações, podemos definir modelos que incluem o intervalo de saudação de tipos de dados com suporte, incluindo tipos complexos (mesmo que pode incluir tipos complexos em outros tipos complexos).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="9a1c5-182">No entanto, ele serializado JSON gerado pelo Olá exemplo acima abre um ponto importante.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="9a1c5-183">*Como* podemos enviar dados por hello **serializador** biblioteca determina exatamente como Olá JSON é formado.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="9a1c5-184">Abordaremos esse ponto específico na sequência.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="9a1c5-185">Mais informações sobre a serialização</span><span class="sxs-lookup"><span data-stu-id="9a1c5-185">More about serialization</span></span>
<span data-ttu-id="9a1c5-186">seção anterior Olá realça um exemplo de saída de hello gerado pelo Olá **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="9a1c5-187">Nesta seção, vamos explicar como biblioteca Olá serializa os dados e como você pode controlar esse comportamento usando APIs de serialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="9a1c5-188">Ordem tooadvance Olá sobre serialização, trabalharemos com um novo modelo com base em um termostato.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="9a1c5-189">Primeiro, vamos fornecer algumas informações no cenário de saudação tooaddress estamos tentando.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="9a1c5-190">Queremos toomodel um termostato que mede a temperatura e umidade.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="9a1c5-191">Cada parte dos dados será toobe enviado tooIoT Hub de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="9a1c5-192">Por padrão, Olá ingresses termostato um evento de temperatura uma vez a cada 2 minutos; um evento de umidade é ingressed uma vez a cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="9a1c5-193">Quando o evento é ingressed, ele deve incluir um carimbo de hora que mostra o tempo de saudação que correspondente a temperatura hello ou umidade foi medida.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="9a1c5-194">Devido a esse cenário, demonstraremos dois modos diferentes toomodel Olá de dados e explicaremos efeito Olá que modelagem tem em Olá serializado saída.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="9a1c5-195">Modelo 1</span><span class="sxs-lookup"><span data-stu-id="9a1c5-195">Model 1</span></span>
<span data-ttu-id="9a1c5-196">Aqui está o hello primeira versão de um modelo que oferece suporte a Olá cenário anterior:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

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

<span data-ttu-id="9a1c5-197">Observe que esse modelo Olá inclui dois eventos de dados: **temperatura** e **umidade**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="9a1c5-198">Ao contrário de exemplos anteriores, o tipo de saudação de cada evento é uma estrutura definida usando **DECLARE\_STRUCT**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="9a1c5-199">**TemperatureEvent** inclui uma medição de temperatura e um carimbo de data e hora; **HumidityEvent** contém uma medição de umidade e um carimbo de data e hora.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="9a1c5-200">Esse modelo fornece um modo natural toomodel Olá de dados para o cenário Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="9a1c5-201">Quando podemos enviar uma nuvem de toohello de evento, ou enviaremos um temperatura/carimbo de hora ou um par de umidade/timestamp.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="9a1c5-202">Podemos enviar uma nuvem de toohello temperatura eventos usando código como Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

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

<span data-ttu-id="9a1c5-203">Podemos vai usar valores codificados para temperatura e umidade no código de exemplo hello, mas imagine que, na verdade, recuperando esses valores por amostragem sensores de saudação correspondente em termostato hello.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="9a1c5-204">código de saudação acima usa Olá **GetDateTimeOffset** auxiliar que foi apresentado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="9a1c5-205">Por motivos que se tornarão desmarque posteriores, esse código explicitamente separa tarefa Olá de serialização e enviar evento hello.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="9a1c5-206">código anterior Olá serializa eventos de temperatura Olá em um buffer.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="9a1c5-207">Em seguida, **sendMessage** é uma função auxiliar (incluído no **simplesample\_amqp**) que envia Olá evento tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

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

<span data-ttu-id="9a1c5-208">Esse código é um subconjunto de saudação **SendAsync** auxiliar descrita na seção anterior do hello, portanto não entraremos sobre ele novamente aqui.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="9a1c5-209">Quando executamos evento Olá anterior código toosend Olá temperatura, esse formato serializado do evento Olá é enviado tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="9a1c5-210">Estamos enviando uma temperatura que pertence ao tipo **TemperatureEvent** e esse struct contém um membro **Temperature** e outro **Time**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="9a1c5-211">Isso é refletido diretamente nos dados Olá serializado.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="9a1c5-212">Da mesma forma, podemos enviar um evento de umidade com este código:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="9a1c5-213">formulário de saudação serializado que enviou tooIoT Hub aparece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="9a1c5-214">Novamente, tudo conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-214">Again, this is as expected.</span></span>

<span data-ttu-id="9a1c5-215">Com esse modelo, você pode imaginar como outros eventos podem ser facilmente adicionados.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="9a1c5-216">Definir mais de estruturas usando **DECLARE\_STRUCT**e incluem o evento correspondente Olá Olá modelo usando **WITH\_dados**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="9a1c5-217">Agora, vamos modificar o modelo Olá para que ela inclua Olá mesmos dados, mas com uma estrutura diferente.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="9a1c5-218">Modelo 2</span><span class="sxs-lookup"><span data-stu-id="9a1c5-218">Model 2</span></span>
<span data-ttu-id="9a1c5-219">Considere este toohello modelo alternativo um acima:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="9a1c5-220">Nesse caso, eliminamos Olá **DECLARE\_STRUCT** macros e são simplesmente definindo itens de dados de saudação do nosso cenário usando tipos simples de saudação linguagem de modelagem.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="9a1c5-221">Para o momento de saudação vamos ignorar Olá **tempo** eventos.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="9a1c5-222">Com essa aside, eis Olá código tooingress **temperatura**:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

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

<span data-ttu-id="9a1c5-223">Esse código envia seguinte Olá serializado evento tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="9a1c5-224">E código hello para enviar eventos de umidade Olá aparece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="9a1c5-225">Esse código envia esse Hub tooIoT:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="9a1c5-226">Até o momento, ainda não há surpresas.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-226">So far there are still no surprises.</span></span> <span data-ttu-id="9a1c5-227">Agora vamos alterar como usamos macro de SERIALIZAR hello.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="9a1c5-228">Olá **SERIALIZE** macro pode levar vários eventos de dados como argumentos.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="9a1c5-229">Isso nos permite Olá tooserialize **temperatura** e **umidade** evento junto e enviá-los tooIoT Hub em uma chamada:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="9a1c5-230">Você pode imaginar que resultados de saudação do código é que os eventos de dois dados são enviados tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="9a1c5-231">[</span><span class="sxs-lookup"><span data-stu-id="9a1c5-231">[</span></span>

<span data-ttu-id="9a1c5-232">{"Temperatura":75},</span><span class="sxs-lookup"><span data-stu-id="9a1c5-232">{"Temperature":75},</span></span>

<span data-ttu-id="9a1c5-233">{"Umidade":45}</span><span class="sxs-lookup"><span data-stu-id="9a1c5-233">{"Humidity":45}</span></span>

<span data-ttu-id="9a1c5-234">]</span><span class="sxs-lookup"><span data-stu-id="9a1c5-234">]</span></span>

<span data-ttu-id="9a1c5-235">Em outras palavras, você pode esperar que esse código é mesmo Olá como enviar **temperatura** e **umidade** separadamente.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="9a1c5-236">É apenas uma toopass conveniência ambos os eventos muito**SERIALIZE** Olá mesmo chamar.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="9a1c5-237">No entanto, esse não for o caso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-237">However, that’s not hello case.</span></span> <span data-ttu-id="9a1c5-238">Em vez disso, código de saudação acima envia esse evento de dados único tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="9a1c5-239">{"Temperatura":75, "Umidade":45}</span><span class="sxs-lookup"><span data-stu-id="9a1c5-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="9a1c5-240">Isso pode parecer estranho, pois nosso modelo define **Temperature** e **Humidity** como dois eventos *separados*:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="9a1c5-241">Mais toohello um ponto, podemos não modelar estes eventos onde **temperatura** e **umidade** estão em Olá mesma estrutura:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="9a1c5-242">Se usarmos esse modelo, poderá ser mais fácil toounderstand como **temperatura** e **umidade** será enviado em Olá mesmo serializado mensagem.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="9a1c5-243">No entanto talvez não seja criptografado por ele funciona dessa forma, quando você passa os dois eventos de dados muito**SERIALIZE** usando o modelo de 2.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="9a1c5-244">Esse comportamento é toounderstand mais fácil se você souber suposições Olá que Olá **serializador** biblioteca está fazendo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="9a1c5-245">sentido de toomake isso vamos voltar tooour modelo:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="9a1c5-246">Pense nesse modelo em termos orientados ao objeto.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="9a1c5-247">Neste caso, estamos modelando um dispositivo físico (um termostato), e esse dispositivo inclui atributos como **Temperature** e **Humidity**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="9a1c5-248">Podemos enviar todo o estado de nosso modelo de código, como a seguir Olá Olá:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="9a1c5-249">Supondo que Olá valores de temperatura, umidade e tempo são definidos, veremos um evento como esse tooIoT enviado Hub:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="9a1c5-250">Às vezes você pode desejar somente toosend *alguns* propriedades de nuvem de toohello modelo hello (Isso é especialmente verdadeiro se o seu modelo contiver um grande número de eventos de dados).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="9a1c5-251">É útil toosend apenas um subconjunto de eventos de dados, como em nosso exemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="9a1c5-252">Isso gera exatamente Olá mesmo serializado eventos como se tivesse definimos um **TemperatureEvent** com um **temperatura** e **tempo** membro, como usamos com modelos de 1.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="9a1c5-253">Nesse caso foi capaz de toogenerate exatamente hello mesmo serializado eventos usando um modelo diferente (modelo 2) porque é chamado **SERIALIZE** de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="9a1c5-254">Olá ponto importante é que, se você passar vários eventos de dados muito**SERIALIZE,** , em seguida, ele assume que cada evento é uma propriedade em um único objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="9a1c5-255">abordagem recomendada Olá depende de você e como você pensar em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="9a1c5-256">Se você estiver enviando "eventos de" nuvem toohello e cada evento contém um conjunto definido de propriedades, primeira abordagem de saudação faz muito sentido.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="9a1c5-257">Nesse caso você usaria **DECLARE\_STRUCT** toodefine Olá a estrutura de cada evento e, em seguida, incluí-los em seu modelo com hello **WITH\_dados** macro.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="9a1c5-258">Em seguida, você enviar cada evento como foi Olá primeiro exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="9a1c5-259">Nessa abordagem, você só passaria um evento único de dados muito**SERIALIZADOR**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="9a1c5-260">Se você pensar em seu modelo de forma orientada a objeto, em seguida, segunda abordagem de saudação pode suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="9a1c5-261">Nesse caso, Olá elementos definidos usando **WITH\_dados** hello "propriedades" de seu objeto.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="9a1c5-262">Você passar qualquer subconjunto de eventos muito**SERIALIZE** que desejar, dependendo de quanto o estado do objeto"" deseja toosend toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="9a1c5-263">Nenhuma abordagem é certa ou errada.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="9a1c5-264">Apenas esteja ciente de como Olá **serializador** biblioteca funciona e a abordagem de modelagem de saudação pick que melhor atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="9a1c5-265">Manipulação de mensagens</span><span class="sxs-lookup"><span data-stu-id="9a1c5-265">Message handling</span></span>
<span data-ttu-id="9a1c5-266">Até o momento neste artigo somente discutiu enviar eventos tooIoT Hub e não resolvidos de recebimento de mensagens.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="9a1c5-267">Olá motivo para isso é que precisamos tooknow sobre o recebimento de mensagens em grande parte foi abordado em um [anteriormente artigo](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="9a1c5-268">O artigo mostrava o processamento de mensagens por meio do registro de uma função de retorno de chamada da mensagem:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="9a1c5-269">Você, em seguida, escrever a função de retorno de chamada de saudação que é invocada quando uma mensagem é recebida:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-269">You then write hello callback function that’s invoked when a message is received:</span></span>

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

<span data-ttu-id="9a1c5-270">Essa implementação de **IoTHubMessage** Olá de chamadas de função específica para cada ação em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="9a1c5-271">Por exemplo, se o seu modelo definir esta ação:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="9a1c5-272">Você deverá definir uma função com esta assinatura:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="9a1c5-273">**SetAirResistance** é chamado quando ela é enviada tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="9a1c5-274">Ainda que ainda não explicar é qual versão Olá serializado da mensagem é semelhante.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="9a1c5-275">Em outras palavras, se você quiser toosend um **SetAirResistance** dispositivo de tooyour de mensagem, o que parecidos com?</span><span class="sxs-lookup"><span data-stu-id="9a1c5-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="9a1c5-276">Se você estiver enviando um dispositivo de tooa de mensagem, você faria isso por meio do SDK do serviço de Azure IoT hello.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="9a1c5-277">Você ainda precisa tooknow conteúdo string toosend tooinvoke uma ação específica.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="9a1c5-278">formato geral de Hello para enviar uma mensagem aparece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="9a1c5-279">Você está enviando um objeto JSON serializado com duas propriedades: **nome** é Olá nome da ação de saudação (mensagem) e **parâmetros** contém parâmetros de saudação da ação.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="9a1c5-280">Por exemplo, tooinvoke **SetAirResistance** você pode enviar este dispositivo tooa de mensagem:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="9a1c5-281">nome da ação Olá deve corresponder exatamente uma ação definida no modelo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="9a1c5-282">nomes de parâmetro Hello devem corresponder também.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-282">hello parameter names must match as well.</span></span> <span data-ttu-id="9a1c5-283">Observe também a diferenciação de maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-283">Also note case sensitivity.</span></span> <span data-ttu-id="9a1c5-284">**Name** e **Parameters** devem estar sempre com a primeira letra maiúscula.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="9a1c5-285">Certifique-se de que caso de Olá toomatch de seus parâmetros e o nome da ação em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="9a1c5-286">Neste exemplo, o nome da ação Olá é "SetAirResistance" e não "setairresistance".</span><span class="sxs-lookup"><span data-stu-id="9a1c5-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="9a1c5-287">Olá duas outras ações **TurnFanOn** e **TurnFanOff** podem ser invocados pelo dispositivo de tooa essas mensagens de envio:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="9a1c5-288">Esta seção descreveu tudo o que você precisa tooknow quando eventos de envio e recebimento de mensagens com hello **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="9a1c5-289">Antes de continuarmos, vamos abordar alguns parâmetros que você pode configurar e que controlam o tamanho de seu modelo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="9a1c5-290">Configuração de macro</span><span class="sxs-lookup"><span data-stu-id="9a1c5-290">Macro configuration</span></span>
<span data-ttu-id="9a1c5-291">Se você estiver usando Olá **serializador** biblioteca uma parte importante da saudação SDK toobe atento foi encontrada na biblioteca do azure-c-compartilhado-utilitário hello.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="9a1c5-292">Se você clonou repositório hello Azure-iot-sdk-c do GitHub usando hello – recursiva opção, você encontrará esta biblioteca de utilitário compartilhados aqui:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="9a1c5-293">Se você não tiver clonado biblioteca hello, você pode encontrar [aqui](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="9a1c5-294">Biblioteca de utilitário compartilhados hello, você encontrará Olá pasta a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="9a1c5-295">Essa pasta contém uma solução do Visual Studio chamada **macro\_utils\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="9a1c5-296">programa de saudação nesta solução gera Olá **macro\_utils.h** arquivo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="9a1c5-297">Há uma macro padrão\_utils.h arquivo incluído Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="9a1c5-298">Esta solução permite que você toomodify alguns parâmetros e, em seguida, recrie Olá arquivo de cabeçalho com base nesses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="9a1c5-299">Olá dois parâmetros de chave toobe preocupada com são **nArithmetic** e **nMacroParameters** que é definido nestas duas linhas encontradas em macro\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="9a1c5-300">Esses valores são parâmetros de padrão de saudação incluídos Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="9a1c5-301">Cada parâmetro tem Olá significado a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="9a1c5-302">nMacroParameters – controla a quantidade de parâmetros que você pode ter em uma definição de macro DECLARE\_MODEL.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="9a1c5-303">nArithmetic – controles Olá total de membros permitidos em um modelo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="9a1c5-304">motivo Olá que esses parâmetros são importantes é porque eles controlam quanto seu modelo pode ser.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="9a1c5-305">Por exemplo, veja esta definição de modelo:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="9a1c5-306">Como mencionado anteriormente, **DECLARE\_MODEL** é apenas uma macro de C.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="9a1c5-307">Olá nomes de modelo hello e hello **WITH\_dados** instrução (ainda outra macro) é parâmetros de **DECLARE\_modelo**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="9a1c5-308">**nMacroParameters** define o número de parâmetros que pode ser incluído em **DECLARE\_MODEL**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="9a1c5-309">Efetivamente, isso define quantos eventos de dados e declarações de ação você pode ter.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="9a1c5-310">Dessa forma, com limite de padrão de saudação de 124 isso significa que você pode definir um modelo com uma combinação de aproximadamente 60 ações e eventos de dados.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="9a1c5-311">Se você tentar tooexceed esse limite, você receberá erros de compilador que procuram toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="9a1c5-312">Olá **nArithmetic** parâmetro é mais sobre o funcionamento interno de saudação do idioma de macro Olá de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="9a1c5-313">Ele controla o número total de saudação de membros, você pode ter em seu modelo, incluindo **DECLARE_STRUCT** macros.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="9a1c5-314">Portanto, se começar a ver erros do compilador como esse, tente aumentar **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="9a1c5-315">Se você quiser toochange esses parâmetros, modifique os valores de saudação em macro Olá\_utils.tt arquivo, recompile Olá macro\_utilitários\_h\_generator.sln solução e o programa compilado Olá execução.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="9a1c5-316">Ao fazer isso, uma nova macro\_utils.h arquivo é gerado e inserido no hello.\\ comuns\\directory inc.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="9a1c5-317">Em ordem toouse Olá nova versão da macro\_utils.h, remover Olá **serializador** pacote NuGet de sua solução e em seu lugar incluem hello **serializador** projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="9a1c5-318">Isso permite que o toocompile de código no código-fonte da biblioteca do serializador Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="9a1c5-319">Isso inclui a macro Olá atualizado\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="9a1c5-320">Se você deseja toodo para **simplesample\_amqp**, iniciar, removendo o pacote do NuGet Olá para a biblioteca de serializador Olá de solução hello:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="9a1c5-321">Em seguida, adicione tooyour esse projeto solução do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="9a1c5-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="9a1c5-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="9a1c5-323">Quando terminar, sua solução deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="9a1c5-324">Agora, quando você compila sua solução, hello atualizado macro\_utils.h está incluído em seu binário.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="9a1c5-325">Observe que aumentar demais esses valores pode exceder os limites do compilador.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="9a1c5-326">toothis ponto, hello **nMacroParameters** é Olá parâmetro principal que toobe em questão.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="9a1c5-327">especificação de C99 Olá Especifica que um mínimo de 127 parâmetros são permitidas em uma definição de macro.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="9a1c5-328">Olá compilador Microsoft segue a especificação de saudação exatamente (e tem um limite de 127), portanto, não será capaz de tooincrease **nMacroParameters** além do padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="9a1c5-329">Outros compiladores podem permitir toodo assim (por exemplo, compilador de GNU Olá dá suporte a um limite superior).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="9a1c5-330">Até agora falamos sobre tudo o que você precisa tooknow sobre como toowrite com o código Olá **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="9a1c5-331">Antes da conclusão, vamos rever alguns tópicos dos artigos anteriores sobre os quais você pode estar se perguntando.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="9a1c5-332">Olá APIs de nível inferior</span><span class="sxs-lookup"><span data-stu-id="9a1c5-332">hello lower-level APIs</span></span>
<span data-ttu-id="9a1c5-333">aplicativo de exemplo Hello na qual focalizado neste artigo é **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="9a1c5-334">Este exemplo usa Olá nível mais alto (Olá não-"tudo") APIs toosend eventos e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="9a1c5-335">Se você usar essas APIs, haverá um thread em execução em segundo plano que cuida dos eventos de envio e do recebimento de mensagens.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="9a1c5-336">No entanto, você pode usar Olá nível inferior (IL) APIs tooeliminate esse thread em segundo plano e assumir o controle explícito sobre o envio de eventos ou receber mensagens de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="9a1c5-337">Conforme descrito em uma [artigo anterior](iot-hub-device-sdk-c-iothubclient.md), há um conjunto de funções que consiste em Olá APIs de nível superior:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="9a1c5-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="9a1c5-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="9a1c5-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="9a1c5-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="9a1c5-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="9a1c5-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="9a1c5-341">IoTHubClient\_Destroy</span><span class="sxs-lookup"><span data-stu-id="9a1c5-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="9a1c5-342">Essas APIs são demonstradas em **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="9a1c5-343">Há também um conjunto análogo de APIs de nível inferior.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="9a1c5-344">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="9a1c5-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="9a1c5-345">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="9a1c5-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="9a1c5-346">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="9a1c5-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="9a1c5-347">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="9a1c5-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="9a1c5-348">Observe que trabalho de APIs de nível inferior Olá exatamente Olá mesma maneira que descrito nos artigos da saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="9a1c5-349">Você pode usar o primeiro conjunto de APIs de saudação se você quiser um toohandle de thread em segundo plano eventos de envio e recebimento de mensagens.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="9a1c5-350">Use o segundo conjunto de APIs de saudação se desejar que o controle explícito sobre quando você envia e recebe dados de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="9a1c5-351">O conjunto de APIs trabalho igualmente bem com hello **serializador** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="9a1c5-352">Para obter um exemplo de como hello APIs de nível inferior são usados com hello **serializador** biblioteca, consulte Olá **simplesample\_http** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="9a1c5-353">Tópicos adicionais</span><span class="sxs-lookup"><span data-stu-id="9a1c5-353">Additional topics</span></span>
<span data-ttu-id="9a1c5-354">Outros tópicos que vale a pena mencionar novamente são relacionados ao tratamento de propriedades, ao uso de credenciais alternativas de dispositivo e às opções de configuração.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="9a1c5-355">Todos estes tópicos foram abordados em um [artigo anterior](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="9a1c5-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="9a1c5-356">Olá ponto principal é que todos esses recursos funcionam em Olá mesma maneira com hello **serializador** biblioteca que funcionam com hello **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="9a1c5-357">Por exemplo, se você quiser tooattach eventos de tooan de propriedades do modelo, use **IoTHubMessage\_propriedades** e **mapa**\_**AddorUpdate**, Olá mesma maneira que descrita anteriormente:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="9a1c5-358">Se o evento de saudação foi gerado de saudação **serializador** biblioteca ou criados manualmente usando Olá **IoTHubClient** biblioteca não importa.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="9a1c5-359">Para Olá credenciais de dispositivo, usando alternativas **IoTHubClient\_LL\_criar** funciona tão bem como **IoTHubClient\_CreateFromConnectionString** para alocar um **hub IOT\_cliente\_tratar**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="9a1c5-360">Por fim, se você estiver usando Olá **serializador** biblioteca, você pode definir opções de configuração com **IoTHubClient\_LL\_SetOption** assim como você fez ao usar Olá **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="9a1c5-361">Um recurso que é exclusivo toohello **serializador** biblioteca são inicialização Olá APIs.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="9a1c5-362">Antes de começar a trabalhar com a biblioteca de saudação, você deve chamar **serializador\_init**:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="9a1c5-363">Isso é feito antes de chamar **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="9a1c5-364">Da mesma forma, quando você terminar trabalhando com biblioteca de hello, última chamada de saudação fará é muito**serializador\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="9a1c5-365">Caso contrário, todos os Olá outros recursos listados acima trabalho Olá mesmo em Olá **serializador** biblioteca como funcionaria em Olá **IoTHubClient** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="9a1c5-366">Para obter mais informações sobre qualquer um desses tópicos, consulte Olá [artigo anterior](iot-hub-device-sdk-c-iothubclient.md) na série.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a1c5-367">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9a1c5-367">Next steps</span></span>
<span data-ttu-id="9a1c5-368">Este artigo descreve em aspectos exclusivos de saudação de detalhes de saudação **serializador** biblioteca contida em Olá **dispositivo IoT do Azure SDK para C**. Com informações de saudação fornecidas, você deve ter uma boa compreensão de como os modelos de toouse toosend eventos e receber mensagens de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="9a1c5-369">Isso também conclui a série de três partes Olá em como os aplicativos toodevelop com hello **dispositivo IoT do Azure SDK para C**. Isso deve ser suficiente informações toonot somente introdução você mas lhe oferece uma compreensão completa de como funcionam Olá APIs.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="9a1c5-370">Para obter informações adicionais, há alguns exemplos em Olá que SDK não abordado aqui.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="9a1c5-371">Caso contrário, Olá [documentação do SDK](https://github.com/Azure/azure-iot-sdk-c) é um bom recurso para obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="9a1c5-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="9a1c5-372">toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá [SDKs do Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="9a1c5-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="9a1c5-373">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="9a1c5-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9a1c5-374">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="9a1c5-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
