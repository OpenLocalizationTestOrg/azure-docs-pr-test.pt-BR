---
title: "Conecte o Raspberry Pi (Nó) ao IoT do Azure - Lição 4: modificar aplicativo | Microsoft Docs"
description: Personalize as mensagens para alterar o comportamento liga e desliga do LED.
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
ms.openlocfilehash: b2ae23ac9cc1723936c4b4e1900b95cdcde744df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="1d97e-104">Alterar o comportamento de ativar e desativar do LED</span><span class="sxs-lookup"><span data-stu-id="1d97e-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1d97e-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="1d97e-105">What you will do</span></span>
<span data-ttu-id="1d97e-106">Personalize as mensagens para alterar o comportamento liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="1d97e-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="1d97e-107">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1d97e-107">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1d97e-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="1d97e-108">What you will learn</span></span>
<span data-ttu-id="1d97e-109">Utilizar funções adicionais do Node.js para alterar o comportamento liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="1d97e-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1d97e-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="1d97e-110">What you need</span></span>
<span data-ttu-id="1d97e-111">Você deve ter concluído com sucesso [Executar um aplicativo de exemplo no Raspberry Pi para receber mensagens da nuvem para o dispositivo](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="1d97e-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="1d97e-112">Adicionar funções do Node.js</span><span class="sxs-lookup"><span data-stu-id="1d97e-112">Add Node.js functions</span></span>
1. <span data-ttu-id="1d97e-113">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="1d97e-113">Open the sample application in Visual Studio code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="1d97e-114">Abra o arquivo `app.js` e, em seguida, adicione as seguintes funções no final:</span><span class="sxs-lookup"><span data-stu-id="1d97e-114">Open the `app.js` file, and then add the following functions at the end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Arquivo App.js com funções adicionais](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="1d97e-116">Adicione as seguintes condições antes do padrão um do bloco de caso de opção da função `receiveMessageCallback`:</span><span class="sxs-lookup"><span data-stu-id="1d97e-116">Add the following conditions before the default one in the switch-case block of the `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="1d97e-117">Agora você configurou o aplicativo de exemplo para responder a mais instruções por meio de mensagens.</span><span class="sxs-lookup"><span data-stu-id="1d97e-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="1d97e-118">A instrução "on" ativa o LED e a instrução "off" desativa o LED.</span><span class="sxs-lookup"><span data-stu-id="1d97e-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="1d97e-119">Abra o arquivo gulpfile.js e, em seguida, adicione uma nova função antes da função `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="1d97e-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>
   
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
5. <span data-ttu-id="1d97e-121">Na função `sendMessage`, substitua a linha `var message = buildMessage(sentMessageCount);` com a nova linha mostrada no trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="1d97e-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="1d97e-122">Salve todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="1d97e-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="1d97e-123">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="1d97e-123">Deploy and run the sample application</span></span>
<span data-ttu-id="1d97e-124">Implante e execute o aplicativo de exemplo no Pi executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1d97e-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="1d97e-125">Você deve ver o LED ativar por dois segundos e, em seguida, desativar por outros dois segundos.</span><span class="sxs-lookup"><span data-stu-id="1d97e-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="1d97e-126">A última mensagem "stop" interrompe a execução do aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1d97e-126">The last "stop" message stops the sample application from running.</span></span>

![Exemplo de aplicativo com mensagens de logon e logoff](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="1d97e-128">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="1d97e-128">Congratulations!</span></span> <span data-ttu-id="1d97e-129">Você personalizou com sucesso as mensagens que são enviadas do Hub IoT para o Pi.</span><span class="sxs-lookup"><span data-stu-id="1d97e-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="1d97e-130">Resumo</span><span class="sxs-lookup"><span data-stu-id="1d97e-130">Summary</span></span>
<span data-ttu-id="1d97e-131">Essa seção opcional demonstra como personalizar as mensagens para que o aplicativo de exemplo controle o comportamento liga e desliga do LED de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="1d97e-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

