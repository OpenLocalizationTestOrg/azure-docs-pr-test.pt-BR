---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 1: Configurar NUC| Microsoft Docs"
description: "Configurar a Intel NUC toowork como um gateway de IoT entre um sensor e informações sobre o Azure IoT Hub toocollect sensor e enviá-lo tooIoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: gateway iot, intel nuc, computador nuc, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="ebbd9-104">Configurar um NUC da Intel como um gateway IoT</span><span class="sxs-lookup"><span data-stu-id="ebbd9-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ebbd9-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="ebbd9-105">What you will do</span></span>

- <span data-ttu-id="ebbd9-106">Configure um NUC da Intel como um gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="ebbd9-107">Instale pacote do Azure IoT borda Olá em NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="ebbd9-108">Execute um aplicativo de exemplo "hello_world" na funcionalidade de gateway do Intel NUC tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="ebbd9-109">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ebbd9-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ebbd9-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="ebbd9-110">What you will learn</span></span>

<span data-ttu-id="ebbd9-111">Nesta lição, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="ebbd9-112">Como tooconnect NUC Intel com periféricos.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="ebbd9-113">Como tooinstall e atualização de pacotes de saudação necessário em NUC Intel usando Olá inteligente Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="ebbd9-114">Como toorun hello "hello_world" exemplo de funcionalidade de gateway do aplicativo tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ebbd9-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="ebbd9-115">What you need</span></span>

- <span data-ttu-id="ebbd9-116">Um Intel NUC Kit DE3815TYKE com hello Intel IoT Gateway Software Suite (vento rio Linux * 7.0.0.13) pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="ebbd9-117">Um cabo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-117">An Ethernet cable.</span></span>
- <span data-ttu-id="ebbd9-118">Um teclado.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-118">A keyboard.</span></span>
- <span data-ttu-id="ebbd9-119">Um cabo HDMI ou VGA.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="ebbd9-120">Um monitor com uma porta HDMI ou VGA.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-120">A monitor with an HDMI or VGA port.</span></span>

![Kit de Gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="ebbd9-122">Conecte-se a Intel NUC com periféricos Olá</span><span class="sxs-lookup"><span data-stu-id="ebbd9-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="ebbd9-123">imagem de saudação abaixo está um exemplo de NUC Intel que está conectado com vários periféricos:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="ebbd9-124">Teclado tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="ebbd9-125">Conectado toohello monitor por um cabo VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="ebbd9-126">Conectado tooa rede com fio por um cabo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="ebbd9-127">Fonte de alimentação toohello conectado com um cabo de alimentação.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-127">Connected toohello power supply with a power cable.</span></span>

![Tooperipherals NUC Intel conectado](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="ebbd9-129">Conecte-se o sistema do Intel NUC toohello do computador host por meio do Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="ebbd9-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="ebbd9-130">Aqui, você precisa de teclado e monitor tooget Olá endereço IP do dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="ebbd9-131">Se você já souber Olá IP endereço, você pode ignorar toostep 3 nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="ebbd9-132">Ative Intel NUC pressionando o botão liga / desliga hello e log no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="ebbd9-133">Olá nome de usuário e senha são ambos `root`.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="ebbd9-134">Obtenha o endereço IP de saudação do NUC executando Olá `ifconfig` comando.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="ebbd9-135">Esta etapa é feita no dispositivo NUC hello.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="ebbd9-136">Aqui está um exemplo de saída do comando hello.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-136">Here is an example of hello command output.</span></span>

   ![Resultado de ifconfig mostrando o IP do NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="ebbd9-138">Neste exemplo, Olá valor segue `inet addr:` é o endereço IP de saudação que é necessário quando você planejar tooconnect remotamente a partir de um computador de host tooIntel NUC.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="ebbd9-139">Use um dos Olá seguir SSH clientes de sua tooIntel de tooconnect de máquina de host NUC.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="ebbd9-140">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="ebbd9-141">Olá compilação no cliente SSH no Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="ebbd9-142">É mais eficiente e produtiva toooperate no Intel NUC de um computador host.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="ebbd9-143">É necessário o endereço IP Olá Olá, nome de usuário e senha tooconnect Olá NUC pelo cliente do SSH.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="ebbd9-144">Este é o cliente SSH de uso de exemplo hello em macOS.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="ebbd9-145">![Cliente SSH em execução no macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="ebbd9-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="ebbd9-146">Instalar o pacote do Azure IoT borda Olá</span><span class="sxs-lookup"><span data-stu-id="ebbd9-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="ebbd9-147">pacote do Azure IoT borda Olá contém binários pré-compilados Olá Olá SDK e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="ebbd9-148">Esses binários são Azure IoT borda, hello Azure IoT SDK e as ferramentas de saudação correspondente.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="ebbd9-149">pacote de saudação também contém um aplicativo de exemplo "hello_world" que é a funcionalidade de gateway de saudação toovalidate usado.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="ebbd9-150">Borda de IoT é Olá fundamentais ao gateway hello.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="ebbd9-151">Olá tooinstall do pacote, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="ebbd9-152">Adicione repositório de nuvem IoT Olá executando Olá comandos em uma janela de terminal a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="ebbd9-153">Olá `rpm` comando importa Olá chave rpm.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="ebbd9-154">Olá `smart channel` comando adiciona rpm Olá toohello inteligente Package Manager do canal.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="ebbd9-155">Antes de executar Olá `smart update` comando, verá uma saída como abaixo.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![saída de comandos de canal inteligente e rpm](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="ebbd9-157">Instale o pacote de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="ebbd9-158">`packagegroup-cloud-azure`é o nome de saudação do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="ebbd9-159">Olá `smart install` comando é o pacote de saudação tooinstall usado.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="ebbd9-160">Depois de instalar o pacote de saudação, Intel NUC é esperado toowork como um gateway.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="ebbd9-161">Execute o aplicativo de exemplo hello Azure IoT borda "hello_world"</span><span class="sxs-lookup"><span data-stu-id="ebbd9-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="ebbd9-162">Vá muito`azureiotgatewaysdk/samples` e execute o aplicativo de exemplo hello exemplo "hello_world".</span><span class="sxs-lookup"><span data-stu-id="ebbd9-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="ebbd9-163">Este aplicativo de exemplo cria um gateway de saudação `hello_world.json` de arquivo e usa componentes fundamentais de saudação do hello Azure IoT borda arquitetura toolog um arquivo de tooa mensagem hello world a cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="ebbd9-164">Você pode executar o aplicativo de exemplo hello exemplo "hello_world" executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="ebbd9-165">aplicativo de exemplo Hello produz o seguinte Olá saída se a funcionalidade de gateway hello está funcionando corretamente:</span><span class="sxs-lookup"><span data-stu-id="ebbd9-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![saída do aplicativo](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="ebbd9-167">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ebbd9-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="ebbd9-168">Resumo</span><span class="sxs-lookup"><span data-stu-id="ebbd9-168">Summary</span></span>

<span data-ttu-id="ebbd9-169">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="ebbd9-169">Congratulations!</span></span> <span data-ttu-id="ebbd9-170">Você terminou de configurar o NUC da Intel como um gateway.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="ebbd9-171">Agora você está pronto toomove em toohello próxima lição tooset computador host e criar um hub IoT do Azure e registrar seu dispositivo lógico de hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbd9-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebbd9-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ebbd9-172">Next steps</span></span>
[<span data-ttu-id="ebbd9-173">Prepare o computador host e o Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="ebbd9-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
