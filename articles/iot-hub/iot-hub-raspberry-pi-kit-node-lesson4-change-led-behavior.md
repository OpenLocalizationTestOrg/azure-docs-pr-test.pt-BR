---
title: "Conecte-se framboesa Pi (nó) tooAzure IoT – lição 4: modificar o aplicativo | Microsoft Docs"
description: "Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: led de controle com raspberry pi, controle de led de raspberry pi, led de controle de raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 99b542fcb8639add0f5a0f7a49dd8abd0e224a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="793d3-104">Alterar Olá ativa e desativa o comportamento de saudação LED</span><span class="sxs-lookup"><span data-stu-id="793d3-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="793d3-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="793d3-105">What you will do</span></span>
<span data-ttu-id="793d3-106">Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento.</span><span class="sxs-lookup"><span data-stu-id="793d3-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="793d3-107">Se você tiver problemas, buscar soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="793d3-107">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="793d3-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="793d3-108">What you will learn</span></span>
<span data-ttu-id="793d3-109">Use adicional Olá de Node. js funções toochange LED do ativa e desativa o comportamento.</span><span class="sxs-lookup"><span data-stu-id="793d3-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="793d3-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="793d3-110">What you need</span></span>
<span data-ttu-id="793d3-111">Você deve ter concluído com êxito [executar um aplicativo de exemplo em Pi framboesa tooreceive mensagens de nuvem para dispositivo](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="793d3-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="793d3-112">Adicionar funções do Node.js</span><span class="sxs-lookup"><span data-stu-id="793d3-112">Add Node.js functions</span></span>
1. <span data-ttu-id="793d3-113">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="793d3-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="793d3-114">Olá abrir `app.js` de arquivo e depois adicione Olá funções final Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="793d3-114">Open hello `app.js` file, and then add hello following functions at hello end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Arquivo App.js com funções adicionais](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="793d3-116">Adicionar Olá condições antes de saudação padrão a seguir no bloco de caso de opção de saudação do hello `receiveMessageCallback` função:</span><span class="sxs-lookup"><span data-stu-id="793d3-116">Add hello following conditions before hello default one in hello switch-case block of hello `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="793d3-117">Agora você configurou instruções de toomore de toorespond Olá exemplo aplicativo por meio de mensagens.</span><span class="sxs-lookup"><span data-stu-id="793d3-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="793d3-118">Olá "em" instrução ativa Olá LED e hello "desativado" instrução desativa Olá LED.</span><span class="sxs-lookup"><span data-stu-id="793d3-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="793d3-119">Abrir o arquivo de gulpfile.js hello e, em seguida, adicionar uma nova função antes da função hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="793d3-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>
   
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
   
   ![Arquivo Gulpfile.js com funções adicionais](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. <span data-ttu-id="793d3-121">Em Olá `sendMessage` funcionar, substitua a linha hello `var message = buildMessage(sentMessageCount);` com nova linha de Olá Olá trecho de código a seguir mostrada:</span><span class="sxs-lookup"><span data-stu-id="793d3-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="793d3-122">Salve todas as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="793d3-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="793d3-123">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="793d3-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="793d3-124">Implantar e executar o aplicativo de exemplo hello em Pi executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="793d3-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="793d3-125">Você verá Olá LED ativar por dois segundos e, em seguida, desligue por outro dois segundos.</span><span class="sxs-lookup"><span data-stu-id="793d3-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="793d3-126">última mensagem de "stop" Hello interrompe o aplicativo de exemplo hello seja executado.</span><span class="sxs-lookup"><span data-stu-id="793d3-126">hello last "stop" message stops hello sample application from running.</span></span>

![Exemplo de aplicativo com mensagens de logon e logoff](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="793d3-128">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="793d3-128">Congratulations!</span></span> <span data-ttu-id="793d3-129">Você personalizou mensagens de saudação enviadas tooPi de seu hub IoT com êxito.</span><span class="sxs-lookup"><span data-stu-id="793d3-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="793d3-130">Resumo</span><span class="sxs-lookup"><span data-stu-id="793d3-130">Summary</span></span>
<span data-ttu-id="793d3-131">Essa seção demonstra como toocustomize mensagens para que o aplicativo de exemplo hello possa controlar Olá ativa e desativa o comportamento de saudação LED de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="793d3-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

