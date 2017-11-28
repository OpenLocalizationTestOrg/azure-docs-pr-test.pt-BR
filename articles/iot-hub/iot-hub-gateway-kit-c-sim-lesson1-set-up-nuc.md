---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 1: Configurar NUC| Microsoft Docs"
description: "Configure um NUC da Intel para funcionar como um gateway IoT entre um sensor e o Hub IoT do Azure a fim de coletar informações do sensor e enviá-las para o Hub IoT."
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
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="45ba3-104">Configurar um NUC da Intel como um gateway IoT</span><span class="sxs-lookup"><span data-stu-id="45ba3-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="45ba3-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="45ba3-105">What you will do</span></span>

- <span data-ttu-id="45ba3-106">Configure um NUC da Intel como um gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="45ba3-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="45ba3-107">Instale o pacote do Azure IoT Edge na NUC da Intel.</span><span class="sxs-lookup"><span data-stu-id="45ba3-107">Install the Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="45ba3-108">Execute um aplicativo de exemplo "hello_world" no NUC da Intel para verificar a funcionalidade do gateway.</span><span class="sxs-lookup"><span data-stu-id="45ba3-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="45ba3-109">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="45ba3-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="45ba3-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="45ba3-110">What you will learn</span></span>

<span data-ttu-id="45ba3-111">Nesta lição, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="45ba3-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="45ba3-112">Como conectar um NUC da Intel com periféricos.</span><span class="sxs-lookup"><span data-stu-id="45ba3-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="45ba3-113">Como instalar e atualizar os pacotes necessários no NUC da Intel usando o Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="45ba3-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="45ba3-114">Como executar o aplicativo de exemplo "hello_world" para verificar a funcionalidade do gateway.</span><span class="sxs-lookup"><span data-stu-id="45ba3-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="45ba3-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="45ba3-115">What you need</span></span>

- <span data-ttu-id="45ba3-116">Um Kit DE3815TYKE do NUC da Intel com o Pacote de Software do Gateway IoT da Intel (Wind River Linux *7.0.0.13) pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="45ba3-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="45ba3-117">Um cabo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="45ba3-117">An Ethernet cable.</span></span>
- <span data-ttu-id="45ba3-118">Um teclado.</span><span class="sxs-lookup"><span data-stu-id="45ba3-118">A keyboard.</span></span>
- <span data-ttu-id="45ba3-119">Um cabo HDMI ou VGA.</span><span class="sxs-lookup"><span data-stu-id="45ba3-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="45ba3-120">Um monitor com uma porta HDMI ou VGA.</span><span class="sxs-lookup"><span data-stu-id="45ba3-120">A monitor with an HDMI or VGA port.</span></span>

![Kit de Gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="45ba3-122">Conectar um NUC da Intel com os periféricos</span><span class="sxs-lookup"><span data-stu-id="45ba3-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="45ba3-123">A imagem abaixo é um exemplo de NUC da Intel conectado a vários periféricos:</span><span class="sxs-lookup"><span data-stu-id="45ba3-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="45ba3-124">Conectado a um teclado.</span><span class="sxs-lookup"><span data-stu-id="45ba3-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="45ba3-125">Conectado ao monitor por um cabo VGA ou HDMI.</span><span class="sxs-lookup"><span data-stu-id="45ba3-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="45ba3-126">Conectado a uma rede com fios por um cabo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="45ba3-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="45ba3-127">Conectado à fonte de alimentação por um cabo de alimentação.</span><span class="sxs-lookup"><span data-stu-id="45ba3-127">Connected to the power supply with a power cable.</span></span>

![NUC da Intel conectado a periféricos](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="45ba3-129">Conectar-se ao sistema do NUC da Intel do computador host via SSH (Secure Shell)</span><span class="sxs-lookup"><span data-stu-id="45ba3-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="45ba3-130">Aqui, você precisa de um teclado e um monitor para obter o endereço IP do dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="45ba3-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="45ba3-131">Se você já sabe o endereço IP, pode pular para a etapa 3 nesta seção.</span><span class="sxs-lookup"><span data-stu-id="45ba3-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="45ba3-132">Ative o NUC da Intel pressionando o botão de energia e faça logon no sistema.</span><span class="sxs-lookup"><span data-stu-id="45ba3-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="45ba3-133">O nome de usuário e a senha padrão são ambos `root`.</span><span class="sxs-lookup"><span data-stu-id="45ba3-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="45ba3-134">Obtenha o endereço IP do NUC executando o comando `ifconfig`.</span><span class="sxs-lookup"><span data-stu-id="45ba3-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="45ba3-135">Esta etapa é realizada no dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="45ba3-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="45ba3-136">Aqui está um exemplo do resultado do comando.</span><span class="sxs-lookup"><span data-stu-id="45ba3-136">Here is an example of the command output.</span></span>

   ![Resultado de ifconfig mostrando o IP do NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="45ba3-138">Neste exemplo, o valor após `inet addr:` é o endereço IP necessário para se conectar remotamente de um computador host ao NUC da Intel.</span><span class="sxs-lookup"><span data-stu-id="45ba3-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="45ba3-139">Use um dos seguintes clientes SSH do seu computador host para se conectar ao NUC da Intel.</span><span class="sxs-lookup"><span data-stu-id="45ba3-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="45ba3-140">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="45ba3-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="45ba3-141">O cliente SSH integrado no Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="45ba3-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="45ba3-142">É mais eficiente e produtivo operar no NUC da Intel desde um computador host.</span><span class="sxs-lookup"><span data-stu-id="45ba3-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="45ba3-143">Você precisa do endereço IP, do nome de usuário e da senha para conectar-se ao NUC via cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="45ba3-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="45ba3-144">Eis o exemplo de uso de cliente SSH no macOS.</span><span class="sxs-lookup"><span data-stu-id="45ba3-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="45ba3-145">![Cliente SSH em execução no macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="45ba3-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="45ba3-146">Instalar o pacote do Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="45ba3-146">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="45ba3-147">O pacote do Azure IoT Edge contém os binários pré-compilados do SDK e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="45ba3-147">The Azure IoT Edge package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="45ba3-148">Esses binários são o Azure IoT Edge, o SDK de IoT do Azure e as ferramentas correspondentes.</span><span class="sxs-lookup"><span data-stu-id="45ba3-148">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="45ba3-149">O pacote também contém um aplicativo de exemplo "hello_world" usado para validar a funcionalidade do gateway.</span><span class="sxs-lookup"><span data-stu-id="45ba3-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="45ba3-150">O IoT Edge é a parte principal do gateway.</span><span class="sxs-lookup"><span data-stu-id="45ba3-150">IoT Edge is the core part of the gateway.</span></span> <span data-ttu-id="45ba3-151">Para instalar o pacote, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="45ba3-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="45ba3-152">Adicione o repositório de nuvem IoT executando os seguintes comandos em uma janela de terminal:</span><span class="sxs-lookup"><span data-stu-id="45ba3-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="45ba3-153">O comando `rpm` importa a chave de rpm.</span><span class="sxs-lookup"><span data-stu-id="45ba3-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="45ba3-154">O comando `smart channel` adiciona o canal de rpm ao Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="45ba3-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="45ba3-155">Antes de executar o comando `smart update`, você verá uma saída semelhante à mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="45ba3-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![saída de comandos de canal inteligente e rpm](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="45ba3-157">Execute o comando a seguir para instalar o pacote:</span><span class="sxs-lookup"><span data-stu-id="45ba3-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="45ba3-158">`packagegroup-cloud-azure` é o nome do pacote.</span><span class="sxs-lookup"><span data-stu-id="45ba3-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="45ba3-159">O comando `smart install` é usado para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="45ba3-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="45ba3-160">Depois que o pacote é instalado, espera-se que o NUC da Intel funcione como um gateway.</span><span class="sxs-lookup"><span data-stu-id="45ba3-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="45ba3-161">Executar o aplicativo de exemplo “hello_world” do Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="45ba3-161">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="45ba3-162">Vá para `azureiotgatewaysdk/samples` e execute o aplicativo de exemplo "hello_world".</span><span class="sxs-lookup"><span data-stu-id="45ba3-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="45ba3-163">Este aplicativo de exemplo cria um gateway com base no arquivo `hello_world.json` e usa os componentes fundamentais da arquitetura do Azure IoT Edge para registrar uma mensagem “olá, mundo” em um arquivo a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="45ba3-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Edge architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="45ba3-164">Você pode executar o aplicativo de exemplo "hello_world" executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="45ba3-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="45ba3-165">O aplicativo de exemplo produz a seguinte saída se a funcionalidade de gateway estiver funcionando corretamente:</span><span class="sxs-lookup"><span data-stu-id="45ba3-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![saída do aplicativo](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="45ba3-167">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="45ba3-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="45ba3-168">Resumo</span><span class="sxs-lookup"><span data-stu-id="45ba3-168">Summary</span></span>

<span data-ttu-id="45ba3-169">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="45ba3-169">Congratulations!</span></span> <span data-ttu-id="45ba3-170">Você terminou de configurar o NUC da Intel como um gateway.</span><span class="sxs-lookup"><span data-stu-id="45ba3-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="45ba3-171">Agora você está pronto para passar para a próxima lição para configurar o computador host, criar um Hub IoT do Azure e registrar o dispositivo lógico do Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="45ba3-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45ba3-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45ba3-172">Next steps</span></span>
[<span data-ttu-id="45ba3-173">Prepare o computador host e o Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="45ba3-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
