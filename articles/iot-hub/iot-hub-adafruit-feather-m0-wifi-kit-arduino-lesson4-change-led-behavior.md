---
title: "Connect Arduino (C) tooAzure IoT – lição 4: modificar o aplicativo | Microsoft Docs"
description: "Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controlar led com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8cc438650f01ae4335d91c94df6a29e0ffbdc508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="63d96-104">Alterar Olá ativa e desativa o comportamento de saudação LED</span><span class="sxs-lookup"><span data-stu-id="63d96-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="63d96-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="63d96-105">What you will do</span></span>
<span data-ttu-id="63d96-106">Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento.</span><span class="sxs-lookup"><span data-stu-id="63d96-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="63d96-107">Se você tiver problemas, procure por soluções em Olá [página de solução](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) para seu quadro Adafruit difusão M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="63d96-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="63d96-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="63d96-108">What you will learn</span></span>
<span data-ttu-id="63d96-109">Use adicional Olá de Arduino funções toochange LED do ativa e desativa o comportamento.</span><span class="sxs-lookup"><span data-stu-id="63d96-109">Use additional Arduino functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="63d96-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="63d96-110">What you need</span></span>
<span data-ttu-id="63d96-111">Você deve ter concluído com êxito [executar um aplicativo de exemplo na nuvem Arduino placa tooreceive toodevice mensagens][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="63d96-111">You must have successfully completed [Run a sample application on your Arduino board tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="63d96-112">Adicionar gulpfile.js e toomain.c de funções</span><span class="sxs-lookup"><span data-stu-id="63d96-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="63d96-113">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="63d96-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="63d96-114">Olá abrir `app.ino` arquivo e, em seguida, adicionar funções a seguir após a função blinkLED() de saudação:</span><span class="sxs-lookup"><span data-stu-id="63d96-114">Open hello `app.ino` file, and then add hello following functions after blinkLED() function:</span></span>

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Arquivo app.ino com funções adicionais][app-ino-file]
3. <span data-ttu-id="63d96-116">Adicionar Olá seguintes condições antes de saudação `else if` bloco de saudação `receiveMessageCallback` função:</span><span class="sxs-lookup"><span data-stu-id="63d96-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="63d96-117">Agora você configurou instruções de toomore de toorespond Olá exemplo aplicativo por meio de mensagens.</span><span class="sxs-lookup"><span data-stu-id="63d96-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="63d96-118">Olá "em" instrução ativa Olá LED e hello "desativado" instrução desativa Olá LED.</span><span class="sxs-lookup"><span data-stu-id="63d96-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="63d96-119">Abrir o arquivo de gulpfile.js hello e, em seguida, adicionar uma nova função antes da função hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="63d96-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Arquivo Gulpfile.js com funções adicionais][gulp-file-js]
5. <span data-ttu-id="63d96-121">Em Olá `sendMessage` funcionar, substitua a linha hello `var message = buildMessage(sentMessageCount);` com nova linha de Olá Olá trecho de código a seguir mostrada:</span><span class="sxs-lookup"><span data-stu-id="63d96-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="63d96-122">Salve todas as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="63d96-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="63d96-123">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="63d96-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="63d96-124">Implantar e executar o aplicativo de exemplo hello em seu quadro Arduino executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="63d96-124">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="63d96-125">Você verá Olá LED ativar por dois segundos e, em seguida, desligue por outro dois segundos.</span><span class="sxs-lookup"><span data-stu-id="63d96-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="63d96-126">última mensagem de "stop" Hello interrompe o aplicativo de exemplo hello seja executado.</span><span class="sxs-lookup"><span data-stu-id="63d96-126">hello last "stop" message stops hello sample application from running.</span></span>

![liga e desliga][on-and-off]

<span data-ttu-id="63d96-128">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="63d96-128">Congratulations!</span></span> <span data-ttu-id="63d96-129">Você personalizou mensagens de saudação enviadas tooyour Arduino placa de seu hub IoT com êxito.</span><span class="sxs-lookup"><span data-stu-id="63d96-129">You’ve successfully customized hello messages that are sent tooyour Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="63d96-130">Resumo</span><span class="sxs-lookup"><span data-stu-id="63d96-130">Summary</span></span>
<span data-ttu-id="63d96-131">Essa seção demonstra como toocustomize mensagens para que o aplicativo de exemplo hello possa controlar Olá ativa e desativa o comportamento de saudação LED de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="63d96-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png