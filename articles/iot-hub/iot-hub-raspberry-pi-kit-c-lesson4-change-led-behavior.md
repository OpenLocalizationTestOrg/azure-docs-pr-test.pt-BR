---
title: "Connect Raspberry PI (C) tooAzure IoT – lição 4: modificar o aplicativo | Microsoft Docs"
description: "Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento."
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
ms.openlocfilehash: f4739c4e9a58b4b0fe964b5c3c81e5918982099f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="3da30-104">Alterar Olá ativa e desativa o comportamento de saudação LED</span><span class="sxs-lookup"><span data-stu-id="3da30-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="3da30-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="3da30-105">What you will do</span></span>
<span data-ttu-id="3da30-106">Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento.</span><span class="sxs-lookup"><span data-stu-id="3da30-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="3da30-107">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3da30-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3da30-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="3da30-108">What you will learn</span></span>
<span data-ttu-id="3da30-109">Use adicional Olá de Node. js funções toochange LED do ativa e desativa o comportamento.</span><span class="sxs-lookup"><span data-stu-id="3da30-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3da30-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="3da30-110">What you need</span></span>
<span data-ttu-id="3da30-111">Você deve ter concluído com êxito [executar um aplicativo de exemplo na nuvem de tooreceive framboesa Pi toodevice mensagens](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="3da30-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud toodevice messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="3da30-112">Adicionar gulpfile.js e toomain.c de funções</span><span class="sxs-lookup"><span data-stu-id="3da30-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="3da30-113">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3da30-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="3da30-114">Olá abrir `main.c` arquivo e, em seguida, adicionar funções a seguir após a função blinkLED() de saudação:</span><span class="sxs-lookup"><span data-stu-id="3da30-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="3da30-116">Adicionar Olá seguintes condições antes de saudação padrão em Olá `if` bloco de saudação `receiveMessageCallback` função:</span><span class="sxs-lookup"><span data-stu-id="3da30-116">Add hello following conditions before hello default one in hello `if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="3da30-117">Agora você configurou instruções de toomore de toorespond Olá exemplo aplicativo por meio de mensagens.</span><span class="sxs-lookup"><span data-stu-id="3da30-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="3da30-118">Olá "em" instrução ativa Olá LED e hello "desativado" instrução desativa Olá LED.</span><span class="sxs-lookup"><span data-stu-id="3da30-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="3da30-119">Abrir o arquivo de gulpfile.js hello e, em seguida, adicionar uma nova função antes da função hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="3da30-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="3da30-121">Em Olá `sendMessage` funcionar, substitua a linha hello `var message = buildMessage(sentMessageCount);` com nova linha de Olá Olá trecho de código a seguir mostrada:</span><span class="sxs-lookup"><span data-stu-id="3da30-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="3da30-122">Salve todas as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="3da30-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="3da30-123">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="3da30-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="3da30-124">Implantar e executar o aplicativo de exemplo hello em Pi executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3da30-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="3da30-125">Você verá Olá LED ativar por dois segundos e, em seguida, desligue por outro dois segundos.</span><span class="sxs-lookup"><span data-stu-id="3da30-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="3da30-126">última mensagem de "stop" Hello interrompe o aplicativo de exemplo hello seja executado.</span><span class="sxs-lookup"><span data-stu-id="3da30-126">hello last "stop" message stops hello sample application from running.</span></span>

![Exemplo de aplicativo com mensagens de logon e logoff](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="3da30-128">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="3da30-128">Congratulations!</span></span> <span data-ttu-id="3da30-129">Você personalizou mensagens de saudação enviadas tooPi de seu hub IoT com êxito.</span><span class="sxs-lookup"><span data-stu-id="3da30-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="3da30-130">Resumo</span><span class="sxs-lookup"><span data-stu-id="3da30-130">Summary</span></span>
<span data-ttu-id="3da30-131">Essa seção demonstra como toocustomize mensagens para que o aplicativo de exemplo hello possa controlar Olá ativa e desativa o comportamento de saudação LED de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="3da30-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>
