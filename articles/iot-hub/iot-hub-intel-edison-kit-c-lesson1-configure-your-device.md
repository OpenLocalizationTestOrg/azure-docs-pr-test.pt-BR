---
title: "Conectar o Intel Edison (C) ao IoT do Azure - Lição 1: configurar dispositivo | Microsoft Docs"
description: Configurar o Intel Edison para o primeiro uso.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "configuração do arduino, conectar arduino ao computador, configurar arduino, placa arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c92d9f7ba63b0a0929ff95599fd757ea425ef1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="e48c3-104">Configurar seu Intel Edison</span><span class="sxs-lookup"><span data-stu-id="e48c3-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e48c3-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="e48c3-105">What you will do</span></span>
<span data-ttu-id="e48c3-106">Configure o Intel Edison para o primeiro uso montando a placa, ligando-a e instalando a ferramenta de configuração no sistema operacional da área de trabalho para atualizar o firmware do Edison, definir sua senha e conectá-lo ao Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="e48c3-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="e48c3-107">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e48c3-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e48c3-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="e48c3-108">What you will learn</span></span>
<span data-ttu-id="e48c3-109">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="e48c3-109">In this article, you will learn:</span></span>

* <span data-ttu-id="e48c3-110">Como montar a placa do Edison e ligá-la.</span><span class="sxs-lookup"><span data-stu-id="e48c3-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="e48c3-111">Como atualizar o firmware do Edison, definir a senha e conectar ao Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="e48c3-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e48c3-112">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="e48c3-112">What you need</span></span>
<span data-ttu-id="e48c3-113">Para concluir esta operação, você precisará das seguintes partes do seu Kit de início do Intel Edison:</span><span class="sxs-lookup"><span data-stu-id="e48c3-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="e48c3-114">Módulo do Intel® Edison</span><span class="sxs-lookup"><span data-stu-id="e48c3-114">Intel® Edison module</span></span>
* <span data-ttu-id="e48c3-115">Placa de expansão Arduino</span><span class="sxs-lookup"><span data-stu-id="e48c3-115">Arduino expansion board</span></span>
* <span data-ttu-id="e48c3-116">As barras separadoras ou parafusos incluídos no pacote, incluindo dois parafusos para fixar o módulo à placa de expansão e quatro conjuntos de parafusos e espaçadores plásticos.</span><span class="sxs-lookup"><span data-stu-id="e48c3-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="e48c3-117">Um cabo USB do tipo Micro B para Tipo A</span><span class="sxs-lookup"><span data-stu-id="e48c3-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="e48c3-118">Uma fonte de alimentação CC (corrente contínua).</span><span class="sxs-lookup"><span data-stu-id="e48c3-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="e48c3-119">A fonte de alimentação deve ser classificada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e48c3-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="e48c3-120">7-15V CC</span><span class="sxs-lookup"><span data-stu-id="e48c3-120">7-15V DC</span></span>
  - <span data-ttu-id="e48c3-121">Pelo menos 1500 mA</span><span class="sxs-lookup"><span data-stu-id="e48c3-121">At least 1500mA</span></span>
  - <span data-ttu-id="e48c3-122">O pino central/interno deve ser o polo positivo da fonte de alimentação</span><span class="sxs-lookup"><span data-stu-id="e48c3-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![Coisas em seu Kit de Início](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="e48c3-124">Você também precisará de:</span><span class="sxs-lookup"><span data-stu-id="e48c3-124">You also need:</span></span>

* <span data-ttu-id="e48c3-125">Um computador executando o Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="e48c3-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="e48c3-126">Uma conexão sem fio com que o Edison se conectará.</span><span class="sxs-lookup"><span data-stu-id="e48c3-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="e48c3-127">Uma conexão com a Internet para baixar a ferramenta de configuração.</span><span class="sxs-lookup"><span data-stu-id="e48c3-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="e48c3-128">Montar sua placa</span><span class="sxs-lookup"><span data-stu-id="e48c3-128">Assemble your board</span></span>

<span data-ttu-id="e48c3-129">Esta seção contém etapas para anexar o módulo Intel® Edison à sua placa de expansão.</span><span class="sxs-lookup"><span data-stu-id="e48c3-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="e48c3-130">Coloque o módulo Intel® Edison dentro do contorno branco na placa de expansão, alinhando os orifícios no módulo aos parafusos na placa de expansão.</span><span class="sxs-lookup"><span data-stu-id="e48c3-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="e48c3-131">Pressione o módulo logo abaixo das palavras `What will you make?` até sentir um clique.</span><span class="sxs-lookup"><span data-stu-id="e48c3-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![montar a placa 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="e48c3-133">Use as duas porcas sextavadas (incluídas no pacote) para prender o módulo à placa de expansão.</span><span class="sxs-lookup"><span data-stu-id="e48c3-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![montar a placa 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="e48c3-135">Insira um parafuso em um dos quatro orifícios nos cantos na placa de expansão.</span><span class="sxs-lookup"><span data-stu-id="e48c3-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="e48c3-136">Gire e aperte um dos espaçadores plásticos brancos no parafuso.</span><span class="sxs-lookup"><span data-stu-id="e48c3-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![montar a placa 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="e48c3-138">Repita para os espaçadores dos outros três cantos.</span><span class="sxs-lookup"><span data-stu-id="e48c3-138">Repeat for the other three corner spacers.</span></span>

   ![montar a placa 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="e48c3-140">Agora, sua placa está montada.</span><span class="sxs-lookup"><span data-stu-id="e48c3-140">Now your board is assembled.</span></span>

   ![montar a placa](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="e48c3-142">Ligar o Edison</span><span class="sxs-lookup"><span data-stu-id="e48c3-142">Power up Edison</span></span>

1. <span data-ttu-id="e48c3-143">Conecte à fonte de alimentação.</span><span class="sxs-lookup"><span data-stu-id="e48c3-143">Plug in the power supply.</span></span>

   ![Conectar à fonte de alimentação](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="e48c3-145">Um LED verde (rotulado como DS1 na placa de expansão Arduino*) deve acender e permanecer aceso.</span><span class="sxs-lookup"><span data-stu-id="e48c3-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="e48c3-146">Aguarde um minuto para a placa concluir a inicialização.</span><span class="sxs-lookup"><span data-stu-id="e48c3-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e48c3-147">Se não tiver uma fonte de alimentação CC, você ainda poderá ligar a placa usando uma porta USB.</span><span class="sxs-lookup"><span data-stu-id="e48c3-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="e48c3-148">Confira a seção `Connect Edison to your computer` para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="e48c3-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="e48c3-149">Ligar sua placa dessa maneira pode resultar em um comportamento imprevisível da placa, especialmente ao usar Wi-Fi ou motores de acionamento.</span><span class="sxs-lookup"><span data-stu-id="e48c3-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="e48c3-150">Conectar o Edison ao computador</span><span class="sxs-lookup"><span data-stu-id="e48c3-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="e48c3-151">Mude a posição do microcomutador para baixo, na direção das duas portas micro USB, para que o Edison fique no modo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e48c3-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="e48c3-152">Veja [aqui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) as diferenças entre o modo de dispositivo e o modo de host.</span><span class="sxs-lookup"><span data-stu-id="e48c3-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Mudar a posição do microcomutador para baixo](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="e48c3-154">Conecte o cabo micro USB à porta micro USB superior.</span><span class="sxs-lookup"><span data-stu-id="e48c3-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Porta micro USB superior](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="e48c3-156">Conecte a outra extremidade do cabo USB ao computador.</span><span class="sxs-lookup"><span data-stu-id="e48c3-156">Plug the other end of USB cable into your computer.</span></span>

   ![USB do computador](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="e48c3-158">Você saberá que a placa foi inicializada completamente quando o computador montar uma nova unidade (muito semelhante a inserir um cartão SD no computador).</span><span class="sxs-lookup"><span data-stu-id="e48c3-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="e48c3-159">Baixe e execute a ferramenta de configuração</span><span class="sxs-lookup"><span data-stu-id="e48c3-159">Download and run the configuration tool</span></span>
<span data-ttu-id="e48c3-160">Obtenha a ferramenta de configuração mais recente [deste link](https://software.intel.com/en-us/iot/hardware/edison/downloads), listada sob o título `Installers`.</span><span class="sxs-lookup"><span data-stu-id="e48c3-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="e48c3-161">Execute a ferramenta e siga as instruções na tela, clicando em Avançar quando necessário</span><span class="sxs-lookup"><span data-stu-id="e48c3-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="e48c3-162">Atualizar o firmware</span><span class="sxs-lookup"><span data-stu-id="e48c3-162">Flash firmware</span></span>
1. <span data-ttu-id="e48c3-163">Na página `Set up options`, clique em `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="e48c3-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="e48c3-164">Selecione a imagem para atualizar sua placa seguindo um destes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="e48c3-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="e48c3-165">Para baixar e atualizar sua placa com a imagem de firmware mais recente disponível da Intel, selecione `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="e48c3-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="e48c3-166">Para atualizar sua placa com uma imagem que você já salvou no computador, selecione `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="e48c3-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="e48c3-167">Navegue e selecione a imagem com que você quer atualizar a placa.</span><span class="sxs-lookup"><span data-stu-id="e48c3-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="e48c3-168">A ferramenta de configuração tentará atualizar a placa.</span><span class="sxs-lookup"><span data-stu-id="e48c3-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="e48c3-169">Todo o processo de atualização pode levar até 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="e48c3-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="e48c3-170">Definir senha</span><span class="sxs-lookup"><span data-stu-id="e48c3-170">Set password</span></span>
1. <span data-ttu-id="e48c3-171">Na página `Set up options`, clique em `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="e48c3-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="e48c3-172">É possível definir um nome personalizado para sua placa Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="e48c3-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="e48c3-173">Isso é opcional.</span><span class="sxs-lookup"><span data-stu-id="e48c3-173">This is optional.</span></span>
3. <span data-ttu-id="e48c3-174">Digite uma senha para a placa e clique em `Set password`.</span><span class="sxs-lookup"><span data-stu-id="e48c3-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="e48c3-175">Marque a senha, que será usada mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e48c3-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="e48c3-176">Conectar ao Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="e48c3-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="e48c3-177">Na página `Set up options`, clique em `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="e48c3-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="e48c3-178">Aguarde até um minuto para que seu computador identifique as redes Wi-Fi disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e48c3-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="e48c3-179">Na lista suspensa `Detected Networks`, selecione a rede.</span><span class="sxs-lookup"><span data-stu-id="e48c3-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="e48c3-180">Na lista suspensa `Security`, selecione o tipo de segurança da rede.</span><span class="sxs-lookup"><span data-stu-id="e48c3-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="e48c3-181">Forneça suas informações de logon e senha e clique em `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="e48c3-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="e48c3-182">Marque o endereço IP, que será usado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e48c3-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="e48c3-183">Verifique se o Edison está conectado à mesma rede que o computador.</span><span class="sxs-lookup"><span data-stu-id="e48c3-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="e48c3-184">Seu computador se conecta ao Edison usando o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="e48c3-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="e48c3-185">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="e48c3-185">Congratulations!</span></span> <span data-ttu-id="e48c3-186">Você configurou o Edison com êxito.</span><span class="sxs-lookup"><span data-stu-id="e48c3-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="e48c3-187">Resumo</span><span class="sxs-lookup"><span data-stu-id="e48c3-187">Summary</span></span>
<span data-ttu-id="e48c3-188">Neste artigo, você aprendeu como montar a placa Edison, atualizar o firmware, definir a senha e conectá-la ao Wi-Fi usando a ferramenta de configuração.</span><span class="sxs-lookup"><span data-stu-id="e48c3-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="e48c3-189">Observe que o LED ainda não está aceso.</span><span class="sxs-lookup"><span data-stu-id="e48c3-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="e48c3-190">A tarefa seguinte é instalar as ferramentas e o software necessários para preparar a execução de um aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="e48c3-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e48c3-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e48c3-191">Next steps</span></span>
<span data-ttu-id="e48c3-192">[Obter as ferramentas][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="e48c3-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md