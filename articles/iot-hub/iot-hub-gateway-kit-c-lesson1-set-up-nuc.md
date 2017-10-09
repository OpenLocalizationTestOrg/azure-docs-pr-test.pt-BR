---
title: "Dispositivo SensorTag e Gateway do IoT do Azure – Lição 1: configurar NUC da Intel | Microsoft Docs"
description: "Configurar a Intel NUC toowork como um gateway de IoT entre um sensor e informações sobre o Azure IoT Hub toocollect sensor e enviá-lo tooIoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gateway iot, intel nuc, computador nuc, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="0483b-104">Configurar um NUC da Intel como um gateway IoT</span><span class="sxs-lookup"><span data-stu-id="0483b-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="0483b-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="0483b-105">What you will do</span></span>

- <span data-ttu-id="0483b-106">Configure um NUC da Intel como um gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="0483b-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="0483b-107">Instale pacote do Azure IoT borda Olá em Olá NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="0483b-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="0483b-108">Execute um aplicativo de exemplo "hello_world" em Olá funcionalidade de gateway do Intel NUC tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="0483b-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="0483b-109">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0483b-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0483b-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="0483b-110">What you will learn</span></span>

<span data-ttu-id="0483b-111">Nesta lição, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="0483b-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="0483b-112">Como tooconnect NUC Intel com periféricos.</span><span class="sxs-lookup"><span data-stu-id="0483b-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="0483b-113">Como tooinstall e atualização de pacotes de saudação necessário em NUC Intel usando Olá inteligente Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="0483b-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="0483b-114">Como toorun hello "hello_world" exemplo de funcionalidade de gateway do aplicativo tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="0483b-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0483b-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="0483b-115">What you need</span></span>

- <span data-ttu-id="0483b-116">Um Intel NUC Kit DE3815TYKE com hello Intel IoT Gateway Software Suite (vento rio Linux * 7.0.0.13) pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="0483b-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="0483b-117">[Clique aqui toopurchase Grove IoT comercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="0483b-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="0483b-118">Um cabo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="0483b-118">An Ethernet cable.</span></span>
- <span data-ttu-id="0483b-119">Um teclado.</span><span class="sxs-lookup"><span data-stu-id="0483b-119">A keyboard.</span></span>
- <span data-ttu-id="0483b-120">Um cabo HDMI ou VGA.</span><span class="sxs-lookup"><span data-stu-id="0483b-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="0483b-121">Um monitor com uma porta HDMI ou VGA.</span><span class="sxs-lookup"><span data-stu-id="0483b-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="0483b-122">Opcional: [Marcação de Sensor Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="0483b-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Kit de Gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="0483b-124">Conecte-se a Intel NUC com periféricos Olá</span><span class="sxs-lookup"><span data-stu-id="0483b-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="0483b-125">imagem de saudação abaixo está um exemplo de NUC Intel que está conectado com vários periféricos:</span><span class="sxs-lookup"><span data-stu-id="0483b-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="0483b-126">Teclado tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="0483b-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="0483b-127">Conectado tooa monitor com um cabo VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="0483b-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="0483b-128">Tooa conectado a rede com um cabo Ethernet com fio.</span><span class="sxs-lookup"><span data-stu-id="0483b-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="0483b-129">Fonte de alimentação tooa conectado com um cabo de alimentação.</span><span class="sxs-lookup"><span data-stu-id="0483b-129">Connected tooa power supply with a power cable.</span></span>

![Tooperipherals NUC Intel conectado](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="0483b-131">Conecte-se o sistema do Intel NUC toohello do computador host por meio do Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="0483b-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="0483b-132">Você precisará de um teclado e um endereço IP do monitor tooget saudação do seu dispositivo NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="0483b-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="0483b-133">Se você já souber Olá IP endereço, você pode ignorar toostep ahead 3 nesta seção.</span><span class="sxs-lookup"><span data-stu-id="0483b-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="0483b-134">Ativar Olá Intel NUC pressionando o botão liga / desliga hello e, em seguida, faça logon.</span><span class="sxs-lookup"><span data-stu-id="0483b-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="0483b-135">Olá nome de usuário e senha são ambos `root`.</span><span class="sxs-lookup"><span data-stu-id="0483b-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="0483b-136">Obter o endereço IP Olá Olá Intel NUC executando Olá `ifconfig` comando no dispositivo de NUC Intel hello.</span><span class="sxs-lookup"><span data-stu-id="0483b-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="0483b-137">Aqui está um exemplo de saída do comando hello.</span><span class="sxs-lookup"><span data-stu-id="0483b-137">Here is an example of hello command output.</span></span>

   ![Saída ifconfig mostrando o IP do NUC da Intel](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="0483b-139">Neste exemplo, Olá valor segue `inet addr:` é Olá endereço IP que você precisa conectar quando toohello Intel NUC de um computador host.</span><span class="sxs-lookup"><span data-stu-id="0483b-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="0483b-140">Use um dos Olá seguir SSH clientes de sua tooIntel de tooconnect do computador host NUC.</span><span class="sxs-lookup"><span data-stu-id="0483b-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="0483b-141">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="0483b-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="0483b-142">Olá SSH do cliente interno Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="0483b-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="0483b-143">É mais eficiente e produtiva toooperate um NUC Intel de um computador host.</span><span class="sxs-lookup"><span data-stu-id="0483b-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="0483b-144">Você vai precisar Olá endereço IP do Intel NUC, tooit do tooconnect de nome e a senha do usuário por meio de um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="0483b-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="0483b-145">Aqui está um exemplo que usa um cliente SSH no macOS.</span><span class="sxs-lookup"><span data-stu-id="0483b-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="0483b-146">![Cliente SSH em execução no macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="0483b-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="0483b-147">Instalar o pacote do Azure IoT borda Olá</span><span class="sxs-lookup"><span data-stu-id="0483b-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="0483b-148">pacote do Azure IoT borda Olá contém binários pré-compilados Olá IoT borda e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="0483b-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="0483b-149">Esses binários são Azure IoT borda, hello Azure IoT SDK e as ferramentas de saudação correspondente.</span><span class="sxs-lookup"><span data-stu-id="0483b-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="0483b-150">Olá pacote também contém um "hello_world" aplicativo de exemplo é a funcionalidade de gateway de saudação toovalidate usado.</span><span class="sxs-lookup"><span data-stu-id="0483b-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="0483b-151">Borda de IoT é Olá fundamentais ao gateway hello.</span><span class="sxs-lookup"><span data-stu-id="0483b-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="0483b-152">Execute o pacote de saudação de tooinstall essas etapas.</span><span class="sxs-lookup"><span data-stu-id="0483b-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="0483b-153">Adicione Olá repositório IoT nuvem executando Olá comandos em uma janela de terminal a seguir:</span><span class="sxs-lookup"><span data-stu-id="0483b-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="0483b-154">Digite 'y', quando você solicita too'Include esse canal?'</span><span class="sxs-lookup"><span data-stu-id="0483b-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="0483b-155">Se você receber um `import read failed(-1)` erro, use Olá problema de saudação tooresolve comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0483b-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="0483b-156">Olá `rpm` comando importa Olá chave rpm.</span><span class="sxs-lookup"><span data-stu-id="0483b-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="0483b-157">Olá `smart channel` comando adiciona rpm Olá toohello inteligente Package Manager do canal.</span><span class="sxs-lookup"><span data-stu-id="0483b-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="0483b-158">Antes de executar Olá `smart update` de comando, você verá uma saída como abaixo.</span><span class="sxs-lookup"><span data-stu-id="0483b-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![saída de comandos de canal inteligente e rpm](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="0483b-160">Execute o comando de atualização inteligente hello:</span><span class="sxs-lookup"><span data-stu-id="0483b-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="0483b-161">Instale pacote de Gateway do Azure IoT Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0483b-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="0483b-162">`packagegroup-cloud-azure`é o nome de saudação do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="0483b-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="0483b-163">Olá `smart install` comando é o pacote de saudação tooinstall usado.</span><span class="sxs-lookup"><span data-stu-id="0483b-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="0483b-164">Comando a seguir de execução Olá se você vir esse erro: 'não está disponível de chave pública'</span><span class="sxs-lookup"><span data-stu-id="0483b-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="0483b-165">Reinicializar Olá Intel NUC se você vir esse erro: 'Nenhum pacote fornece util-linux-dev'</span><span class="sxs-lookup"><span data-stu-id="0483b-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="0483b-166">Depois de instalar o pacote de saudação, Intel NUC é toofunction pronto como um gateway.</span><span class="sxs-lookup"><span data-stu-id="0483b-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="0483b-167">Execute o aplicativo de exemplo hello Azure IoT borda "hello_world"</span><span class="sxs-lookup"><span data-stu-id="0483b-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="0483b-168">saudação de aplicativo de exemplo a seguir cria um gateway de um `hello_world.json` de arquivo e usa componentes fundamentais de saudação do Azure IoT borda arquitetura toolog um arquivo de tooa de mensagem hello world (txt) a cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="0483b-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="0483b-169">Você pode executar o exemplo hello World Olá executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0483b-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="0483b-170">Permitir que o aplicativo hello World Olá executar alguns minutos e, em seguida, pressione Olá Enter chave toostop-lo.</span><span class="sxs-lookup"><span data-stu-id="0483b-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="0483b-171">![saída do aplicativo](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="0483b-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="0483b-172">Você pode ignorar quaisquer erros de 'identificador de argumento inválido(NULL)' que apareçam depois que você pressionar Enter.</span><span class="sxs-lookup"><span data-stu-id="0483b-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="0483b-173">Você pode verificar o gateway Olá foi executado com êxito abrindo o arquivo de log. txt Olá que agora está na pasta hello_world ![exibição de diretório de log. txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="0483b-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="0483b-174">Abra o log usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="0483b-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="0483b-175">Você verá conteúdo de saudação do log. txt, que será uma saída JSON formatado log das mensagens de saudação que foram gravados 5 segundos pelo módulo de Hello World gateway hello.</span><span class="sxs-lookup"><span data-stu-id="0483b-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="0483b-176">![exibição de diretório de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="0483b-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="0483b-177">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0483b-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="0483b-178">Resumo</span><span class="sxs-lookup"><span data-stu-id="0483b-178">Summary</span></span>

<span data-ttu-id="0483b-179">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="0483b-179">Congratulations!</span></span> <span data-ttu-id="0483b-180">Você terminou de configurar o NUC da Intel como um gateway.</span><span class="sxs-lookup"><span data-stu-id="0483b-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="0483b-181">Agora você está pronto toomove em toohello próxima lição tooset computador host e criar um Hub de IoT do Azure e registrar seu dispositivo lógico de Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0483b-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0483b-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0483b-182">Next steps</span></span>
[<span data-ttu-id="0483b-183">Use um gateway de IoT tooconnect tooAzure um dispositivo IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0483b-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

