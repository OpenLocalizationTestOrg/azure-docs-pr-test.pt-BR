---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 4: piscar Olá LED | Microsoft Docs"
description: "Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controlar led com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="abeaa-104">Alterar Olá ativa e desativa o comportamento de saudação LED</span><span class="sxs-lookup"><span data-stu-id="abeaa-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="abeaa-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="abeaa-105">What you will do</span></span>
<span data-ttu-id="abeaa-106">Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento.</span><span class="sxs-lookup"><span data-stu-id="abeaa-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="abeaa-107">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="abeaa-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="abeaa-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="abeaa-108">What you will learn</span></span>
<span data-ttu-id="abeaa-109">Use Olá toochange de funções adicionais LED do ativa e desativa o comportamento.</span><span class="sxs-lookup"><span data-stu-id="abeaa-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="abeaa-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="abeaa-110">What you need</span></span>
<span data-ttu-id="abeaa-111">Você deve ter concluído com êxito [executar um aplicativo de exemplo na nuvem do Intel Edison tooreceive mensagens toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="abeaa-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-tooappjs-and-gulpfilejs"></a><span data-ttu-id="abeaa-112">Adicionar gulpfile.js e tooapp.js de funções</span><span class="sxs-lookup"><span data-stu-id="abeaa-112">Add functions tooapp.js and gulpfile.js</span></span>
1. <span data-ttu-id="abeaa-113">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="abeaa-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="abeaa-114">Olá abrir `app.js` arquivo e, em seguida, adicionar funções a seguir após a função blinkLED() de saudação:</span><span class="sxs-lookup"><span data-stu-id="abeaa-114">Open hello `app.js` file, and then add hello following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![arquivo app.js com funções adicionais](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="abeaa-116">Adicionar hello condições a seguir antes de saudação 'blink' caso no bloco de caso de opção de saudação do hello `receiveMessageCallback` função:</span><span class="sxs-lookup"><span data-stu-id="abeaa-116">Add hello following conditions before hello 'blink' case in hello switch-case block of hello `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="abeaa-117">Agora você configurou instruções de toomore de toorespond Olá exemplo aplicativo por meio de mensagens.</span><span class="sxs-lookup"><span data-stu-id="abeaa-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="abeaa-118">Olá "em" instrução ativa Olá LED e hello "desativado" instrução desativa Olá LED.</span><span class="sxs-lookup"><span data-stu-id="abeaa-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="abeaa-119">Abrir o arquivo de gulpfile.js hello e, em seguida, adicionar uma nova função antes da função hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="abeaa-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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

   ![Arquivo Gulpfile.js com funções adicionais][gulpfile]
5. <span data-ttu-id="abeaa-121">Em Olá `sendMessage` funcionar, substitua a linha hello `var message = buildMessage(sentMessageCount);` com nova linha de Olá Olá trecho de código a seguir mostrada:</span><span class="sxs-lookup"><span data-stu-id="abeaa-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="abeaa-122">Salve todas as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="abeaa-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="abeaa-123">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="abeaa-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="abeaa-124">Implantar e executar o aplicativo de exemplo hello Edison executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="abeaa-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="abeaa-125">Você verá Olá LED ativar por dois segundos e, em seguida, desligue por outro dois segundos.</span><span class="sxs-lookup"><span data-stu-id="abeaa-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="abeaa-126">última mensagem de "stop" Hello interrompe o aplicativo de exemplo hello seja executado.</span><span class="sxs-lookup"><span data-stu-id="abeaa-126">hello last "stop" message stops hello sample application from running.</span></span>

![liga e desliga][on-and-off]

<span data-ttu-id="abeaa-128">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="abeaa-128">Congratulations!</span></span> <span data-ttu-id="abeaa-129">Você personalizou mensagens de saudação enviadas tooEdison de seu hub IoT com êxito.</span><span class="sxs-lookup"><span data-stu-id="abeaa-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="abeaa-130">Resumo</span><span class="sxs-lookup"><span data-stu-id="abeaa-130">Summary</span></span>
<span data-ttu-id="abeaa-131">Essa seção demonstra como toocustomize mensagens para que o aplicativo de exemplo hello possa controlar Olá ativa e desativa o comportamento de saudação LED de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="abeaa-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
