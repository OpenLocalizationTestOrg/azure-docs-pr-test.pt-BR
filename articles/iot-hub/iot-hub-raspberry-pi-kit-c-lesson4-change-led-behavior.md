---
title: "Conectar o Raspberry Pi (C) ao IoT do Azure - Lição 4: modificar aplicativo | Microsoft Docs"
description: Personalize as mensagens para alterar o comportamento liga e desliga do LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: led de controle com raspberry pi, controle de led de raspberry pi, led de controle de raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 0201b8ed-d5e6-4445-9a4d-1305003d1eff
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b1e441b20e161f4a03d4c2c300b21aca4fedb2a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="029e6-104">Alterar o comportamento de ativar e desativar do LED</span><span class="sxs-lookup"><span data-stu-id="029e6-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="029e6-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="029e6-105">What you will do</span></span>
<span data-ttu-id="029e6-106">Personalize as mensagens para alterar o comportamento liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="029e6-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="029e6-107">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="029e6-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="029e6-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="029e6-108">What you will learn</span></span>
<span data-ttu-id="029e6-109">Utilizar funções adicionais do Node.js para alterar o comportamento liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="029e6-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="029e6-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="029e6-110">What you need</span></span>
<span data-ttu-id="029e6-111">Você deve ter concluído com sucesso [Executar um aplicativo de exemplo no Raspberry Pi para receber mensagens da nuvem para o dispositivo](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="029e6-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud to device messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="029e6-112">Adicionar funções ao main.c e ao gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="029e6-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="029e6-113">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="029e6-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="029e6-114">Abra o arquivo `main.c` e, em seguida, adicione as seguintes funções após a função blinkLED():</span><span class="sxs-lookup"><span data-stu-id="029e6-114">Open the `main.c` file, and then add the following functions after blinkLED() function:</span></span>

   ```c
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![arquivo main.c com funções adicionais](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_c.png)
3. <span data-ttu-id="029e6-116">Adicione as seguintes condições antes do padrão, uma no bloco `if` da função `receiveMessageCallback`:</span><span class="sxs-lookup"><span data-stu-id="029e6-116">Add the following conditions before the default one in the `if` block of the `receiveMessageCallback` function:</span></span>

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="029e6-117">Agora você configurou o aplicativo de exemplo para responder a mais instruções por meio de mensagens.</span><span class="sxs-lookup"><span data-stu-id="029e6-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="029e6-118">A instrução "on" ativa o LED e a instrução "off" desativa o LED.</span><span class="sxs-lookup"><span data-stu-id="029e6-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="029e6-119">Abra o arquivo gulpfile.js e, em seguida, adicione uma nova função antes da função `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="029e6-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   }
   ```

   ![Arquivo Gulpfile.js com funções adicionais](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
5. <span data-ttu-id="029e6-121">Na função `sendMessage`, substitua a linha `var message = buildMessage(sentMessageCount);` com a nova linha mostrada no trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="029e6-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="029e6-122">Salve todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="029e6-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="029e6-123">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="029e6-123">Deploy and run the sample application</span></span>
<span data-ttu-id="029e6-124">Implante e execute o aplicativo de exemplo no Pi executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="029e6-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="029e6-125">Você deve ver o LED ativar por dois segundos e, em seguida, desativar por outros dois segundos.</span><span class="sxs-lookup"><span data-stu-id="029e6-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="029e6-126">A última mensagem "stop" interrompe a execução do aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="029e6-126">The last "stop" message stops the sample application from running.</span></span>

![Exemplo de aplicativo com mensagens de logon e logoff](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="029e6-128">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="029e6-128">Congratulations!</span></span> <span data-ttu-id="029e6-129">Você personalizou com sucesso as mensagens que são enviadas do Hub IoT para o Pi.</span><span class="sxs-lookup"><span data-stu-id="029e6-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="029e6-130">Resumo</span><span class="sxs-lookup"><span data-stu-id="029e6-130">Summary</span></span>
<span data-ttu-id="029e6-131">Essa seção opcional demonstra como personalizar as mensagens para que o aplicativo de exemplo controle o comportamento liga e desliga do LED de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="029e6-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>
