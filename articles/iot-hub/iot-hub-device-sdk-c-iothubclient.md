---
title: SDK do dispositivo IoT do Azure para C - IoTHubClient | Microsoft Docs
description: Como usar a biblioteca do IoTHubClient no SDK do dispositivo IoT do Azure para C para criar aplicativos para dispositivos que se comunicam com um Hub IoT.
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
ms.openlocfilehash: 422d89014511f0d08ba57a893570ff7b253b7bc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="61b48-103">SDK do dispositivo IoT do Azure para C – mais sobre o IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="61b48-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="61b48-104">O [primeiro artigo](iot-hub-device-sdk-c-intro.md) desta série apresentou o **SDK do dispositivo IoT do Azure para C**. Esse artigo explicou que há duas camadas de arquitetura no SDK.</span><span class="sxs-lookup"><span data-stu-id="61b48-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="61b48-105">Na base está a biblioteca **IoTHubClient** , que gerencia a comunicação direta com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="61b48-106">Também há a biblioteca do **serializador** , que se baseia nisso para fornecer serviços de serialização.</span><span class="sxs-lookup"><span data-stu-id="61b48-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span></span> <span data-ttu-id="61b48-107">Neste artigo, forneceremos detalhes adicionais sobre a biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="61b48-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span></span>

<span data-ttu-id="61b48-108">O artigo anterior descreveu como usar a biblioteca **IoTHubClient** para enviar eventos ao Hub IoT e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="61b48-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span></span> <span data-ttu-id="61b48-109">Este artigo estende a discussão explicando como gerenciar com mais precisão *o momento em que* você envia e recebe dados, apresentando as **APIs de nível inferior**.</span><span class="sxs-lookup"><span data-stu-id="61b48-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span></span> <span data-ttu-id="61b48-110">Também vamos explicar como anexar propriedades aos eventos (e recuperá-las de mensagens) usando os recursos de tratamento de propriedade na biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="61b48-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span></span> <span data-ttu-id="61b48-111">Por fim, forneceremos uma explicação adicional sobre as diferentes formas de manipular as mensagens recebidas do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span></span>

<span data-ttu-id="61b48-112">O artigo é concluído com a abordagem de diversos tópicos, incluindo mais sobre as credenciais do dispositivo e como alterar o comportamento do **IoTHubClient** por meio das opções de configuração.</span><span class="sxs-lookup"><span data-stu-id="61b48-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="61b48-113">Usaremos os exemplos do SDK do **IoTHubClient** para explicar esses tópicos.</span><span class="sxs-lookup"><span data-stu-id="61b48-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span></span> <span data-ttu-id="61b48-114">Se você quiser acompanhar, confira os aplicativos **iothub\_client\_sample\_http** e **iothub\_client\_sample\_amqp** que estão incluídos no SDK do dispositivo IoT do Azure para o C. Tudo o que é descrito nas seções a seguir é demonstrado nestes exemplos.</span><span class="sxs-lookup"><span data-stu-id="61b48-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="61b48-115">Você pode encontrar o [**SDK do dispositivo IoT do Azure para C**](https://github.com/Azure/azure-iot-sdk-c) no repositório GitHub e exibir os detalhes da API [na referência da API do C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="61b48-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="61b48-116">As APIs de nível inferior</span><span class="sxs-lookup"><span data-stu-id="61b48-116">The lower-level APIs</span></span>
<span data-ttu-id="61b48-117">O artigo anterior descreveu a operação básica do **IotHubClient** dentro do contexto do aplicativo **iothub\_client\_sample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="61b48-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="61b48-118">Por exemplo, ele explicou como inicializar a biblioteca usando este código.</span><span class="sxs-lookup"><span data-stu-id="61b48-118">For example, it explained how to initialize the library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="61b48-119">Também descreveu como enviar eventos usando esta chamada de função.</span><span class="sxs-lookup"><span data-stu-id="61b48-119">It also described how to send events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="61b48-120">O artigo também descreveu como receber mensagens registrando uma função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="61b48-120">The article also described how to receive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="61b48-121">O artigo também mostrou como liberar recursos usando um código como o a seguir.</span><span class="sxs-lookup"><span data-stu-id="61b48-121">The article also showed how to free resources using code such as the following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="61b48-122">No entanto, há funções complementares para cada uma dessas APIs:</span><span class="sxs-lookup"><span data-stu-id="61b48-122">However there are companion functions to each of these APIs:</span></span>

* <span data-ttu-id="61b48-123">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="61b48-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="61b48-124">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="61b48-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="61b48-125">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="61b48-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="61b48-126">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="61b48-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="61b48-127">Todas essas funções incluem "LL" no nome da API.</span><span class="sxs-lookup"><span data-stu-id="61b48-127">These functions all include “LL” in the API name.</span></span> <span data-ttu-id="61b48-128">Além disso, os parâmetros de cada uma dessas funções são idênticos aos de seus equivalentes não LL.</span><span class="sxs-lookup"><span data-stu-id="61b48-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span></span> <span data-ttu-id="61b48-129">No entanto, o comportamento dessas funções tem uma diferença importante.</span><span class="sxs-lookup"><span data-stu-id="61b48-129">However, the behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="61b48-130">Quando você chama **IoTHubClient\_CreateFromConnectionString**, as bibliotecas subjacentes criam um novo thread, que é executado em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="61b48-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span></span> <span data-ttu-id="61b48-131">Esse thread envia eventos para o Hub IoT e recebe mensagens dele.</span><span class="sxs-lookup"><span data-stu-id="61b48-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="61b48-132">Nenhum thread desse tipo é criado quando se trabalha com as APIs “LL”.</span><span class="sxs-lookup"><span data-stu-id="61b48-132">No such thread is created when working with the "LL" APIs.</span></span> <span data-ttu-id="61b48-133">A criação do thread de segundo plano é uma conveniência para o desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="61b48-133">The creation of the background thread is a convenience to the developer.</span></span> <span data-ttu-id="61b48-134">Você não precisa se preocupar em enviar eventos explicitamente e em receber mensagens do Hub IoT – isso acontece automaticamente em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="61b48-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span></span> <span data-ttu-id="61b48-135">Em contrapartida, as APIs “LL” dão a você um controle explícito sobre a comunicação com o Hub IoT, caso seja necessário.</span><span class="sxs-lookup"><span data-stu-id="61b48-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="61b48-136">Para entender isso melhor, vamos ver um exemplo:</span><span class="sxs-lookup"><span data-stu-id="61b48-136">To understand this better, let’s look at an example:</span></span>

<span data-ttu-id="61b48-137">Quando você chama **IoTHubClient\_SendEventAsync**, na verdade, você está colocando o evento em um buffer.</span><span class="sxs-lookup"><span data-stu-id="61b48-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span></span> <span data-ttu-id="61b48-138">O thread em segundo plano criado quando você chama **IoTHubClient\_CreateFromConnectionString** monitora continuamente esse buffer e envia todos os dados que ele contém ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span></span> <span data-ttu-id="61b48-139">Isso acontece em segundo plano ao mesmo tempo que o thread principal está executando outro trabalho.</span><span class="sxs-lookup"><span data-stu-id="61b48-139">This happens in the background at the same time that the main thread is performing other work.</span></span>

<span data-ttu-id="61b48-140">Da mesma forma, quando você registra uma função de retorno de chamada para mensagens usando **IoTHubClient\_SetMessageCallback**, você está instruindo ao SDK para que o thread em segundo plano invoque a função de retorno de chamada quando uma mensagem for recebida, independentemente do thread principal.</span><span class="sxs-lookup"><span data-stu-id="61b48-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span></span>

<span data-ttu-id="61b48-141">As APIs “LL” não criam um thread em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="61b48-141">The "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="61b48-142">Em vez disso, uma nova API deve ser chamada para enviar e receber dados explicitamente do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="61b48-143">Isso é demonstrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="61b48-143">This is demonstrated in the following example.</span></span>

<span data-ttu-id="61b48-144">O aplicativo **iothub\_client\_sample\_http** que está incluído no SDK demonstra as APIs de nível inferior.</span><span class="sxs-lookup"><span data-stu-id="61b48-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span></span> <span data-ttu-id="61b48-145">Neste exemplo, enviamos eventos ao Hub IoT com um código como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="61b48-145">In that sample, we send events to IoT Hub with code such as the following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="61b48-146">As três primeiras linhas criam a mensagem e a última linha envia o evento.</span><span class="sxs-lookup"><span data-stu-id="61b48-146">The first three lines create the message, and the last line sends the event.</span></span> <span data-ttu-id="61b48-147">No entanto, como mencionado anteriormente, “enviar” o evento significa que os dados são simplesmente colocados em um buffer.</span><span class="sxs-lookup"><span data-stu-id="61b48-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span></span> <span data-ttu-id="61b48-148">Nada é transmitido pela rede quando chamamos **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="61b48-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="61b48-149">Para realmente inserir os dados no Hub IoT, você precisará chamar **IoTHubClient\_LL\_DoWork**, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="61b48-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="61b48-150">Este código (do aplicativo **iothub\_client\_sample\_http** application) chama repetidamente **IoTHubClient\_LL\_DoWork**.</span><span class="sxs-lookup"><span data-stu-id="61b48-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="61b48-151">Toda vez que **IoTHubClient\_LL\_DoWork** é chamado, ele envia alguns eventos do buffer para o Hub IoT e recupera uma mensagem na fila que está sendo enviada ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="61b48-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span></span> <span data-ttu-id="61b48-152">O último caso significa que, se registramos uma função de retorno de chamada para mensagens, o retorno de chamada é invocado (supondo que todas as mensagens estejam na fila).</span><span class="sxs-lookup"><span data-stu-id="61b48-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="61b48-153">Teríamos registrado uma função de retorno de chamada com um código como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="61b48-153">We would have registered such a callback function with code such as the following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="61b48-154">O motivo pelo qual **IoTHubClient\_LL\_DoWork** muitas vezes é chamado em um loop é que cada vez que ele é chamado, ele envia *alguns* eventos em buffer ao Hub IoT e recupera *a próxima* mensagem na fila para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="61b48-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span></span> <span data-ttu-id="61b48-155">Não há garantia de que cada chamada envie todos os eventos em buffer ou recupere todas as mensagens enfileiradas.</span><span class="sxs-lookup"><span data-stu-id="61b48-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span></span> <span data-ttu-id="61b48-156">Se você deseja enviar todos os eventos no buffer e continuar com outro processamento, é possível substituir esse loop por um código como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="61b48-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="61b48-157">Esse código chama **IoTHubClient\_LL\_DoWork** até que todos os eventos no buffer tenham sido enviados ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span></span> <span data-ttu-id="61b48-158">Observe que isso também não significa que todas as mensagens em fila tenham sido recebidas.</span><span class="sxs-lookup"><span data-stu-id="61b48-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="61b48-159">Parte do motivo para isso é que a verificação de “todas” as mensagens não é tão determinística como uma ação.</span><span class="sxs-lookup"><span data-stu-id="61b48-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="61b48-160">O que acontece se você recuperar "todas" as mensagens, mas então outra é enviada para o dispositivo imediatamente depois?</span><span class="sxs-lookup"><span data-stu-id="61b48-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span></span> <span data-ttu-id="61b48-161">Uma maneira melhor de lidar com isso é com um tempo limite programado.</span><span class="sxs-lookup"><span data-stu-id="61b48-161">A better way to deal with that is with a programmed timeout.</span></span> <span data-ttu-id="61b48-162">Por exemplo, a função de retorno de chamada de mensagem pode redefinir um timer sempre que for invocada.</span><span class="sxs-lookup"><span data-stu-id="61b48-162">For example, the message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="61b48-163">Você poderá, então, escrever a lógica para continuar processando se, por exemplo, nenhuma mensagem tiver sido recebida nos últimos *X* segundos.</span><span class="sxs-lookup"><span data-stu-id="61b48-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span></span>

<span data-ttu-id="61b48-164">Quando terminar de inserir os eventos e receber mensagens, certifique-se de chamar a função correspondente para limpar os recursos.</span><span class="sxs-lookup"><span data-stu-id="61b48-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="61b48-165">Basicamente, há apenas um conjunto de APIs para enviar e receber dados com um thread em segundo plano e outro conjunto de APIs que faz a mesma coisa sem o thread em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="61b48-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span></span> <span data-ttu-id="61b48-166">Muitos desenvolvedores podem preferir as APIs não LL, mas as APIs de nível inferior são úteis quando o desenvolvedor desejar ter um controle explícito sobre as transmissões de rede.</span><span class="sxs-lookup"><span data-stu-id="61b48-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="61b48-167">Por exemplo, alguns dispositivos coletam dados ao longo do tempo e apenas inserem eventos em intervalos especificados (por exemplo, de hora em hora ou uma vez por dia).</span><span class="sxs-lookup"><span data-stu-id="61b48-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="61b48-168">As APIs de nível inferior permitem controlar explicitamente o momento em que você envia e recebe dados do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="61b48-169">Outras pessoas simplesmente preferirão a simplicidade oferecida pelas APIs de nível inferior.</span><span class="sxs-lookup"><span data-stu-id="61b48-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span></span> <span data-ttu-id="61b48-170">Tudo acontece no thread principal, em vez de algum trabalho acontecendo em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="61b48-170">Everything happens on the main thread rather than some work happening in the background.</span></span>

<span data-ttu-id="61b48-171">Seja qual for o modelo escolhido, seja consistente em relação às APIs usadas.</span><span class="sxs-lookup"><span data-stu-id="61b48-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span></span> <span data-ttu-id="61b48-172">Se você começar chamando **IoTHubClient\_LL\_CreateFromConnectionString**, lembre-se de usar apenas as APIs de nível inferior correspondentes para qualquer trabalho de acompanhamento:</span><span class="sxs-lookup"><span data-stu-id="61b48-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="61b48-173">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="61b48-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="61b48-174">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="61b48-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="61b48-175">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="61b48-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="61b48-176">IoTHubClient\_LL\_DoWork</span><span class="sxs-lookup"><span data-stu-id="61b48-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="61b48-177">O contrário também é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="61b48-177">The opposite is true as well.</span></span> <span data-ttu-id="61b48-178">Se você começar com **IoTHubClient\_CreateFromConnectionString**, use as APIs não LL para qualquer processamento adicional.</span><span class="sxs-lookup"><span data-stu-id="61b48-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="61b48-179">No SDK do dispositivo IoT do Azure para C, veja o aplicativo **iothub\_client\_sample\_http** para obter um exemplo completo das APIs de nível inferior.</span><span class="sxs-lookup"><span data-stu-id="61b48-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span></span> <span data-ttu-id="61b48-180">O aplicativo **iothub\_client\_sample\_amqp** pode ser referenciado para um exemplo completo das APIs não LL.</span><span class="sxs-lookup"><span data-stu-id="61b48-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="61b48-181">Manipulação de propriedades</span><span class="sxs-lookup"><span data-stu-id="61b48-181">Property handling</span></span>
<span data-ttu-id="61b48-182">Até agora, quando descrevemos o envio de dados, nos referimos ao corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="61b48-182">So far when we've described sending data, we've been referring to the body of the message.</span></span> <span data-ttu-id="61b48-183">Por exemplo, considere este código:</span><span class="sxs-lookup"><span data-stu-id="61b48-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="61b48-184">Este exemplo envia uma mensagem ao Hub IoT com o texto “Hello World”.</span><span class="sxs-lookup"><span data-stu-id="61b48-184">This example sends a message to IoT Hub with the text "Hello World."</span></span> <span data-ttu-id="61b48-185">Entretanto, o Hub IoT também permite que as propriedades sejam anexadas a cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="61b48-185">However, IoT Hub also allows properties to be attached to each message.</span></span> <span data-ttu-id="61b48-186">As propriedades são pares de nome/valor que podem ser anexados à mensagem.</span><span class="sxs-lookup"><span data-stu-id="61b48-186">Properties are name/value pairs that can be attached to the message.</span></span> <span data-ttu-id="61b48-187">Por exemplo, podemos modificar o código anterior para anexar uma propriedade à mensagem:</span><span class="sxs-lookup"><span data-stu-id="61b48-187">For example, we can modify the previous code to attach a property to the message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="61b48-188">Começamos chamando **IoTHubMessage\_Properties** e transmitindo-o ao identificador da nossa mensagem.</span><span class="sxs-lookup"><span data-stu-id="61b48-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span></span> <span data-ttu-id="61b48-189">O que obtemos é uma referência de **MAP\_HANDLE** que nos permite começar a adicionar propriedades.</span><span class="sxs-lookup"><span data-stu-id="61b48-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span></span> <span data-ttu-id="61b48-190">O último é realizado chamando **Map\_AddOrUpdate**, que usa uma referência para um MAP\_HANDLE, o nome da propriedade, e o valor da propriedade.</span><span class="sxs-lookup"><span data-stu-id="61b48-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span></span> <span data-ttu-id="61b48-191">Com essa API, podemos adicionar quantas propriedades quisermos.</span><span class="sxs-lookup"><span data-stu-id="61b48-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="61b48-192">Quando o evento é lido no **Hubs de Eventos**, o receptor pode enumerar as propriedades e recuperar seus valores correspondentes.</span><span class="sxs-lookup"><span data-stu-id="61b48-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span></span> <span data-ttu-id="61b48-193">Por exemplo, no .NET, isso seria realizado acessando a [Coleção de propriedades no objeto EventData](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="61b48-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="61b48-194">No exemplo anterior, estávamos anexando propriedades a um evento que enviamos ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span></span> <span data-ttu-id="61b48-195">As propriedades também podem ser anexadas às mensagens recebidas do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-195">Properties can also be attached to messages received from IoT Hub.</span></span> <span data-ttu-id="61b48-196">Se quisermos recuperar as propriedades de uma mensagem, podemos usar um código como o seguinte em nossa função de retorno de chamada de mensagem:</span><span class="sxs-lookup"><span data-stu-id="61b48-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from the message
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

<span data-ttu-id="61b48-197">A chamada para **IoTHubMessage\_Properties** retorna a referência **MAP\_HANDLE**.</span><span class="sxs-lookup"><span data-stu-id="61b48-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="61b48-198">Então transmitimos essa referência para **Map\_GetInternals** para obter uma referência para uma matriz de pares de nome/valor (bem como uma contagem das propriedades).</span><span class="sxs-lookup"><span data-stu-id="61b48-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span></span> <span data-ttu-id="61b48-199">Nesse momento, é simplesmente uma questão de enumerar as propriedades para obter os valores que queremos.</span><span class="sxs-lookup"><span data-stu-id="61b48-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span></span>

<span data-ttu-id="61b48-200">Não é preciso usar propriedades em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="61b48-200">You don't have to use properties in your application.</span></span> <span data-ttu-id="61b48-201">Entretanto, caso você precise defini-las em eventos ou recuperá-las de mensagens, a biblioteca **IoTHubClient** facilitará essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="61b48-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="61b48-202">Manipulação de mensagens</span><span class="sxs-lookup"><span data-stu-id="61b48-202">Message handling</span></span>
<span data-ttu-id="61b48-203">Como declarado anteriormente, quando as mensagens chegam do Hub IoT, a biblioteca **IoTHubClient** responde invocando uma função de retorno de chamada registrada.</span><span class="sxs-lookup"><span data-stu-id="61b48-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="61b48-204">Há um parâmetro de retorno dessa função que merece uma explicação adicional.</span><span class="sxs-lookup"><span data-stu-id="61b48-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="61b48-205">Veja um trecho da função de retorno de chamada no aplicativo de exemplo **iothub\_client\_sample\_http**:</span><span class="sxs-lookup"><span data-stu-id="61b48-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="61b48-206">Observe que o tipo de retorno é **IOTHUBMESSAGE\_DISPOSITION\_RESULT** e, nesse caso específico, retornamos **IOTHUBMESSAGE\_ACCEPTED**.</span><span class="sxs-lookup"><span data-stu-id="61b48-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="61b48-207">Há outros valores que podemos retornar dessa função que mudam a forma como a biblioteca **IoTHubClient** reage ao retorno de chamada da mensagem.</span><span class="sxs-lookup"><span data-stu-id="61b48-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span></span> <span data-ttu-id="61b48-208">Veja as opções.</span><span class="sxs-lookup"><span data-stu-id="61b48-208">Here are the options.</span></span>

* <span data-ttu-id="61b48-209">**IOTHUBMESSAGE\_ACCEPTED**: a mensagem foi processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="61b48-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span></span> <span data-ttu-id="61b48-210">A biblioteca **IoTHubClient** não invocará a função de retorno de chamada novamente com a mesma mensagem.</span><span class="sxs-lookup"><span data-stu-id="61b48-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="61b48-211"><seg>
  **IOTHUBMESSAGE\_REJECTED**: a mensagem não foi processada e não há intenção de fazer isso no futuro..</seg></span><span class="sxs-lookup"><span data-stu-id="61b48-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span></span> <span data-ttu-id="61b48-212">A biblioteca **IoTHubClient** não deve invocar a função de retorno de chamada novamente com a mesma mensagem.</span><span class="sxs-lookup"><span data-stu-id="61b48-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="61b48-213">**IOTHUBMESSAGE\_ABANDONED**: a mensagem não foi processada com êxito, mas a biblioteca **IoTHubClient** deve invocar a função de retorno de chamada novamente com a mesma mensagem.</span><span class="sxs-lookup"><span data-stu-id="61b48-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span></span>

<span data-ttu-id="61b48-214">Para os dois primeiros códigos de retorno, a biblioteca **IoTHubClient** envia uma mensagem ao Hub IoT indicando que a mensagem deve ser excluída da fila do dispositivo e não entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="61b48-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span></span> <span data-ttu-id="61b48-215">O efeito líquido é o mesmo (a mensagem será excluída da fila do dispositivo), mas sem levar em conta se a mensagem foi aceita ou rejeitada, ela ainda será registrada.</span><span class="sxs-lookup"><span data-stu-id="61b48-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="61b48-216">O registro dessa distinção é útil para os remetentes da mensagem, que podem ouvir comentários e descobrir se um dispositivo aceitou ou rejeitou uma mensagem específica.</span><span class="sxs-lookup"><span data-stu-id="61b48-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="61b48-217">No último caso, uma mensagem também é enviada ao Hub IoT, mas ela indica que a mensagem deve ser entregue novamente.</span><span class="sxs-lookup"><span data-stu-id="61b48-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span></span> <span data-ttu-id="61b48-218">Geralmente, você abandonará uma mensagem se encontrar algum erro, mas é conveniente tentar processar a mensagem novamente.</span><span class="sxs-lookup"><span data-stu-id="61b48-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span></span> <span data-ttu-id="61b48-219">Em contrapartida, rejeitar uma mensagem é apropriado quando você encontrar um erro irrecuperável (ou se simplesmente decidir que não quer processar a mensagem).</span><span class="sxs-lookup"><span data-stu-id="61b48-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span></span>

<span data-ttu-id="61b48-220">De qualquer forma, esteja ciente dos diferentes códigos de retorno para que você possa extrair o comportamento que deseja da biblioteca **IoTHubClient** .</span><span class="sxs-lookup"><span data-stu-id="61b48-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="61b48-221">Credenciais de dispositivo alternativas</span><span class="sxs-lookup"><span data-stu-id="61b48-221">Alternate device credentials</span></span>
<span data-ttu-id="61b48-222">Como explicado anteriormente, a primeira coisa a fazer ao trabalhar com a biblioteca **IoTHubClient** é obter um **IOTHUB\_CLIENT\_HANDLE** com uma chamada como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="61b48-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="61b48-223">Os argumentos para **IoTHubClient\_CreateFromConnectionString** são a cadeia de conexão do dispositivo e um parâmetro que indica o protocolo que usamos para nos comunicar com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span></span> <span data-ttu-id="61b48-224">A cadeia de conexão do dispositivo tem um formato parecido com este:</span><span class="sxs-lookup"><span data-stu-id="61b48-224">The device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="61b48-225">Há quatro tipos de informação nesta cadeia de caracteres: nome do Hub IoT, sufixo do Hub IoT, ID do dispositivo e chave de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="61b48-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="61b48-226">Você obtém o FQDN (nome de domínio totalmente qualificado) de um Hub IoT quando cria a instância do Hub IoT no portal do Azure — isso fornece o nome do Hub IoT (a primeira parte do FQDN) e o sufixo do Hub IoT (o restante do FQDN).</span><span class="sxs-lookup"><span data-stu-id="61b48-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span></span> <span data-ttu-id="61b48-227">Você obtém a ID do dispositivo e a chave de acesso compartilhado ao registrar seu dispositivo no Hub IoT (como descrito no [artigo anterior](iot-hub-device-sdk-c-intro.md)).</span><span class="sxs-lookup"><span data-stu-id="61b48-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="61b48-228">**IoTHubClient\_CreateFromConnectionString** oferece uma maneira de inicializar a biblioteca.</span><span class="sxs-lookup"><span data-stu-id="61b48-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span></span> <span data-ttu-id="61b48-229">Se preferir, você poderá criar um novo **IOTHUB\_CLIENT\_HANDLE** usando esses parâmetros individuais em vez da cadeia de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="61b48-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span></span> <span data-ttu-id="61b48-230">Isso é obtido com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="61b48-230">This is achieved with the following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="61b48-231">Ele faz a mesma coisa que **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="61b48-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="61b48-232">Pode parecer óbvio que você queira usar **IoTHubClient\_CreateFromConnectionString** no lugar desse método mais detalhado de inicialização.</span><span class="sxs-lookup"><span data-stu-id="61b48-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="61b48-233">Entretanto, tenha em mente que, ao registrar um dispositivo no Hub IoT, o que obtemos é uma ID de dispositivo e uma chave do dispositivo (e não uma cadeia de conexão).</span><span class="sxs-lookup"><span data-stu-id="61b48-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="61b48-234">A ferramenta SDK do *gerenciador de dispositivos* apresentada no [artigo anterior](iot-hub-device-sdk-c-intro.md) usa bibliotecas no **SDK do serviço IoT do Azure** para criar a cadeia de conexão do dispositivo com base na ID e chave do dispositivo e do nome de host do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="61b48-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="61b48-235">Dessa forma, é preferível chamar **IoTHubClient\_LL\_Create**, pois economiza a etapa de geração de uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="61b48-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span></span> <span data-ttu-id="61b48-236">Use o método que for conveniente.</span><span class="sxs-lookup"><span data-stu-id="61b48-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="61b48-237">Opções de configuração</span><span class="sxs-lookup"><span data-stu-id="61b48-237">Configuration options</span></span>
<span data-ttu-id="61b48-238">Até agora, tudo que foi descrito sobre como a biblioteca **IoTHubClient** funciona reflete seu comportamento padrão.</span><span class="sxs-lookup"><span data-stu-id="61b48-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="61b48-239">Entretanto, há algumas opções que você pode definir para alterar o funcionamento da biblioteca.</span><span class="sxs-lookup"><span data-stu-id="61b48-239">However, there are a few options that you can set to change how the library works.</span></span> <span data-ttu-id="61b48-240">Isso pode ser feito aproveitando a API **IoTHubClient\_LL\_SetOption**.</span><span class="sxs-lookup"><span data-stu-id="61b48-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="61b48-241">Considere este exemplo:</span><span class="sxs-lookup"><span data-stu-id="61b48-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="61b48-242">Há duas opções que normalmente são usadas:</span><span class="sxs-lookup"><span data-stu-id="61b48-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="61b48-243">**SetBatching** (bool) – Se for **true**, os dados enviados ao Hub IoT serão enviados em lotes.</span><span class="sxs-lookup"><span data-stu-id="61b48-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span></span> <span data-ttu-id="61b48-244">Se for **false**, as mensagens serão enviadas individualmente.</span><span class="sxs-lookup"><span data-stu-id="61b48-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="61b48-245">O padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="61b48-245">The default is **false**.</span></span> <span data-ttu-id="61b48-246">Observe que a opção **SetBatching** se aplica somente ao protocolo HTTP e não aos protocolos MQTT ou AMQP.</span><span class="sxs-lookup"><span data-stu-id="61b48-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="61b48-247">**Tempo limite** (inteiro não atribuído) – Esse valor é representado em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="61b48-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="61b48-248">Se o envio de uma solicitação HTTP ou o recebimento de uma resposta demorar mais que esse tempo, o tempo limite da conexão se esgotará.</span><span class="sxs-lookup"><span data-stu-id="61b48-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span></span>

<span data-ttu-id="61b48-249">A opção de envio em lote é importante.</span><span class="sxs-lookup"><span data-stu-id="61b48-249">The batching option is important.</span></span> <span data-ttu-id="61b48-250">Por padrão, a biblioteca insere eventos individualmente (um evento único é tudo o que você transmite para **IoTHubClient\_LL\_SendEventAsync**).</span><span class="sxs-lookup"><span data-stu-id="61b48-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="61b48-251">Mas se a opção de envio em lote for **true**, a biblioteca coletará o máximo de eventos que puder do buffer (até o tamanho máximo de mensagem que o Hub IoT aceitar).</span><span class="sxs-lookup"><span data-stu-id="61b48-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="61b48-252">O lote do evento é enviado ao Hub IoT em uma única chamada de HTTP (os eventos individuais são agrupados em uma matriz JSON).</span><span class="sxs-lookup"><span data-stu-id="61b48-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span></span> <span data-ttu-id="61b48-253">A habilitação do envio em lote geralmente resulta em grandes ganhos de desempenho, uma vez que você está reduzindo as viagens de ida e volta da rede.</span><span class="sxs-lookup"><span data-stu-id="61b48-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="61b48-254">Ela também reduz significativamente a largura de banda, uma vez que você está enviando um conjunto de cabeçalhos HTTP com um lote de evento, em vez de um conjunto de cabeçalhos para cada evento individual.</span><span class="sxs-lookup"><span data-stu-id="61b48-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="61b48-255">A menos que você tenha um motivo específico para fazer o contrário, o comum é habilitar o envio em lote.</span><span class="sxs-lookup"><span data-stu-id="61b48-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61b48-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61b48-256">Next steps</span></span>
<span data-ttu-id="61b48-257">Este artigo descreve em detalhes o comportamento da biblioteca **IoTHubClient** encontrada no **SDK do dispositivo IoT do Azure para C**. Com essas informações, você deverá ter um bom entendimento dos recursos da biblioteca **IoTHubClient**.</span><span class="sxs-lookup"><span data-stu-id="61b48-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span></span> <span data-ttu-id="61b48-258">O [próximo artigo](iot-hub-device-sdk-c-serializer.md) fornece detalhes semelhantes sobre a biblioteca do **serializador** .</span><span class="sxs-lookup"><span data-stu-id="61b48-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span></span>

<span data-ttu-id="61b48-259">Para saber mais sobre como desenvolver para o Hub IoT, consulte os [SDKs do Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="61b48-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="61b48-260">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="61b48-260">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="61b48-261">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="61b48-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
