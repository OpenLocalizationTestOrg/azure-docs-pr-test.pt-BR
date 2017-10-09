---
title: aaaIoT DevKit toocloud - tooAzure conectar AZ3166 de DevKit de IoT IoT Hub | Microsoft Docs
description: Saiba como toosetup e conecte-se tooAzure AZ3166 de DevKit de IoT IoT Hub para ele plataforma de nuvem do Azure toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="4fbcf-103">Conecte-se tooAzure AZ3166 de DevKit de IoT IoT Hub na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="4fbcf-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="4fbcf-104">Olá [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) podem ser usado toodevelop e protótipo soluções de Internet das coisas (IoT) aproveita os serviços do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="4fbcf-105">Ele inclui um quadro de Arduino compatível com periféricos avançados e sensores, um pacote de quadro do código-fonte aberto e um [catálogo de projetos](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) crescente.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="4fbcf-106">O que fazer</span><span class="sxs-lookup"><span data-stu-id="4fbcf-106">What you do</span></span>
<span data-ttu-id="4fbcf-107">Conecte-se [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub que você cria, Olá coletar os dados de temperatura e umidade de sensores e envia o hub de tooIoT Olá dados.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="4fbcf-108">Você ainda não tem um DevKit?</span><span class="sxs-lookup"><span data-stu-id="4fbcf-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="4fbcf-109">Obtenha um novo [aqui](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="4fbcf-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="4fbcf-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="4fbcf-110">What you learn</span></span>

* <span data-ttu-id="4fbcf-111">Como tooconnect IoT DevKit tooWireless acesso aponte e preparar o ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="4fbcf-112">Como toocreate um hub IoT e registrar um dispositivo para MXChip DevKit de IoT.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="4fbcf-113">Como os dados do sensor toocollect executando um aplicativo de exemplo no MXChip DevKit de IoT.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="4fbcf-114">Como toosend Olá hub IoT do sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4fbcf-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="4fbcf-115">What you need</span></span>

* <span data-ttu-id="4fbcf-116">Uma placa MXChip IoT DevKit com um cabo micro USB.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="4fbcf-117">Experimente agora</span><span class="sxs-lookup"><span data-stu-id="4fbcf-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="4fbcf-118">Um computador que executa o Windows 10 ou macOS 10.10 +</span><span class="sxs-lookup"><span data-stu-id="4fbcf-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="4fbcf-119">Uma assinatura ativa do Azure</span><span class="sxs-lookup"><span data-stu-id="4fbcf-119">An active Azure subscription</span></span>
  * <span data-ttu-id="4fbcf-120">Ative uma [conta do Microsoft Azure de avaliação por 30 dias](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="4fbcf-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="4fbcf-121">Prepare seu hardware</span><span class="sxs-lookup"><span data-stu-id="4fbcf-121">Prepare your hardware</span></span>

<span data-ttu-id="4fbcf-122">Conecte Olá hardware tooyour computador.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="4fbcf-123">O hardware que você precisa</span><span class="sxs-lookup"><span data-stu-id="4fbcf-123">Hardware you need</span></span>

* <span data-ttu-id="4fbcf-124">Placa DevKit</span><span class="sxs-lookup"><span data-stu-id="4fbcf-124">DevKit board</span></span>
* <span data-ttu-id="4fbcf-125">Cabo micro USB</span><span class="sxs-lookup"><span data-stu-id="4fbcf-125">Micro USB cable</span></span>

![guia de introdução: hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="4fbcf-127">Conectar o computador de tooyour DevKit</span><span class="sxs-lookup"><span data-stu-id="4fbcf-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="4fbcf-128">Conexão USB final tooyour PC</span><span class="sxs-lookup"><span data-stu-id="4fbcf-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="4fbcf-129">Conecte-se Micro USB final toohello DevKit</span><span class="sxs-lookup"><span data-stu-id="4fbcf-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="4fbcf-130">Olá verde LED próxima toopower confirma a conexão</span><span class="sxs-lookup"><span data-stu-id="4fbcf-130">hello green LED next toopower confirms connection</span></span>

![guia de introdução: conexão](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="4fbcf-132">Configuração do Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="4fbcf-132">Configure WiFi</span></span>

<span data-ttu-id="4fbcf-133">Os projetos de IoT requerem conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="4fbcf-134">Use Olá instruções tooconfigure Olá DevKit tooconnect tooWiFi a seguir.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="4fbcf-135">Entrar no modo PA</span><span class="sxs-lookup"><span data-stu-id="4fbcf-135">Enter AP Mode</span></span>

<span data-ttu-id="4fbcf-136">Mantenha pressionado B, em seguida, enviar por push e liberar o botão de redefinição hello e versão botão B. Seu DevKit entrará no modo de ponto de acesso para a configuração de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="4fbcf-137">tela Hello exibirá Olá serviço definido Identifier(SSID) de saudação DevKit, bem como Olá configuração endereço IP do portal:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![guia de introdução: PA Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="4fbcf-139">Conecte-se tooDevKit Pacífico</span><span class="sxs-lookup"><span data-stu-id="4fbcf-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="4fbcf-140">Agora, use outra WiFi habilitado dispositivos (PC ou telefone celular) tooconnect toohello DevKit SSID (realçado na captura de tela de saudação acima), deixe Olá senha em branco.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![guia de introdução: SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="4fbcf-142">Configuração do Wi-Fi ao DevKit</span><span class="sxs-lookup"><span data-stu-id="4fbcf-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="4fbcf-143">Endereço IP hello abrir mostrado na tela de DevKit de saudação em seu computador ou navegador de telefone celular, selecione rede Wi-Fi de Olá deseja Olá DevKit tooconnect para e digite a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="4fbcf-144">Clique em **conectar** toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-144">Click **Connect** toocomplete:</span></span>

![Guia de Introdução: portal do Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="4fbcf-146">Depois que a conexão de saudação for bem-sucedida, Olá DevKit reiniciará em alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="4fbcf-147">Se for bem-sucedida, você verá o hello WiFi nome e endereço IP na tela hello:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![Guia de Introdução: IP do Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="4fbcf-149">endereço IP de saudação exibido foto Olá pode não corresponder Olá o IP real atribuído e exibida na tela de DevKit hello.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="4fbcf-150">Isso é normal como Wi-Fi usa DHCP toodynamically atribuir IPs.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="4fbcf-151">Após a configuração de Wi-Fi, suas credenciais serão mantidas no dispositivo Olá para essa conexão, mesmo se desconectado.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="4fbcf-152">Por exemplo, se você configurado Olá DevKit para Wi-Fi em casa e, em seguida, levou office de toohello DevKit Olá, você precisará tooreconfigure Pacífico modo (começando na etapa **insira Pacífico modo**) tooconnect Olá DevKit tooyour office Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="4fbcf-153">Começar a usar o DevKit</span><span class="sxs-lookup"><span data-stu-id="4fbcf-153">Start using DevKit</span></span>

<span data-ttu-id="4fbcf-154">saudação padrão aplicativo em execução no DevKit será verificar a versão mais recente de saudação do firmware hello e exibir alguns dados de diagnóstico de sensor para você.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="4fbcf-155">Atualizar o firmware mais recente do toohello</span><span class="sxs-lookup"><span data-stu-id="4fbcf-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="4fbcf-156">Você será solicitado na tela hello que ambos Olá versão de firmware mais recente e atual, se houver uma atualização necessária.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="4fbcf-157">Execute [atualizar firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guia tooupgrade-lo.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![Guia de Introdução: firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="4fbcf-159">Este é um esforço de uso único, quando você começar a desenvolver em Olá DevKit e carregar seu aplicativo, você terá mais recente do firmware Olá vêm com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="4fbcf-160">Teste de vários sensores</span><span class="sxs-lookup"><span data-stu-id="4fbcf-160">Test various sensors</span></span>

<span data-ttu-id="4fbcf-161">Pressione sensores de tootest botão B, continue a pressionar e liberar Olá B botão toocycle cada sensor.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![Guia de Introdução: sensores](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="4fbcf-163">Prepare o ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="4fbcf-163">Prepare development environment</span></span>

<span data-ttu-id="4fbcf-164">Agora é hora tooset ambiente de desenvolvimento Olá: ferramentas e os pacotes para toobuild impressionantes IoT aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="4fbcf-165">Você pode escolher a versão do Windows ou macOS de acordo com o sistema operacional de tooyour.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="4fbcf-166">Windows</span><span class="sxs-lookup"><span data-stu-id="4fbcf-166">Windows</span></span>

<span data-ttu-id="4fbcf-167">Recomendamos que você toouse Olá instalação pacote tooprepare Olá ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="4fbcf-168">Se você encontrar algum problema, você pode seguir Olá [etapas manuais](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="4fbcf-169">Baixe o pacote mais recente</span><span class="sxs-lookup"><span data-stu-id="4fbcf-169">Download latest package</span></span>

<span data-ttu-id="4fbcf-170">Olá `.zip` arquivo baixado contém todas as ferramentas necessárias e os pacotes necessários para o desenvolvimento de DevKit.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="4fbcf-171">Baixar</span><span class="sxs-lookup"><span data-stu-id="4fbcf-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="4fbcf-172">Olá `.zip` arquivo contém o seguinte Olá ferramentas e os pacotes.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="4fbcf-173">Se você já tiver alguns componentes instalados, o script hello detectará e ignorá-los.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="4fbcf-174">Node. js e Yarn: tempo de execução para o script de instalação hello e tarefas automatizadas</span><span class="sxs-lookup"><span data-stu-id="4fbcf-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="4fbcf-175">[MSI de 2.0 CLI do Azure](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -experiência de linha de comando de plataforma cruzada para gerenciar recursos do Azure, Olá MSI contém dependente Python e pip.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="4fbcf-176">[Visual Studio Code](https://code.visualstudio.com/): editor de códigos simples para o desenvolvimento do DevKit</span><span class="sxs-lookup"><span data-stu-id="4fbcf-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="4fbcf-177">[Extensão do Visual Studio Code para Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): permite o desenvolvimento do Arduino no VS Code</span><span class="sxs-lookup"><span data-stu-id="4fbcf-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="4fbcf-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): extensão Olá para Arduino depende essa ferramenta</span><span class="sxs-lookup"><span data-stu-id="4fbcf-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="4fbcf-179">Pacote de quadro DevKit: Ferramenta cadeias, bibliotecas e projetos para Olá DevKit</span><span class="sxs-lookup"><span data-stu-id="4fbcf-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="4fbcf-180">Utilitário de Link-ST: utilitários e drivers essenciais</span><span class="sxs-lookup"><span data-stu-id="4fbcf-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="4fbcf-181">Execute o script de instalação</span><span class="sxs-lookup"><span data-stu-id="4fbcf-181">Run installation script</span></span>

<span data-ttu-id="4fbcf-182">No Explorador de arquivos do Windows, localize Olá `.zip` e extraí-lo, localizar `install.cmd`, com o botão direito e selecione **"Executar como administrador"** toostart.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![Guia de Introdução: execução-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="4fbcf-184">Durante a instalação, você verá o progresso de saudação de cada ferramenta ou o pacote.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-184">During installation, you will see hello progress of each tool or package.</span></span>

![Introdução: instalação](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="4fbcf-186">Confirmar tooinstall drivers</span><span class="sxs-lookup"><span data-stu-id="4fbcf-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="4fbcf-187">Olá código VS para extensão Arduino depende Olá Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="4fbcf-188">Se esse for o hello estão instalando Olá Arduino IDE pela primeira vez, será solicitado tooinstall os drivers:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![Guia de Introdução: driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="4fbcf-190">Instalação de toofinish cerca de 10 minutos dependendo da velocidade de Internet deve demorar.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="4fbcf-191">Após a conclusão da instalação Olá, você deve ver código do Visual Studio e Arduino IDE atalhos na área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="4fbcf-192">Eventualmente, ao iniciar o VS Code, aparecerá um erro notificando que não foi possível encontrar o Arduino IDE nem o pacote de placa relacionado.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="4fbcf-193">toosolve-lo, código VS fechar, inicie Arduino IDE de uma vez e o código do VS devem localizar o caminho Arduino IDE corretamente.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="4fbcf-194">macOS (visualização)</span><span class="sxs-lookup"><span data-stu-id="4fbcf-194">macOS (Preview)</span></span>

<span data-ttu-id="4fbcf-195">Execute o ambiente de desenvolvimento de tooprepare essas etapas na macOS.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="4fbcf-196">Instalar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="4fbcf-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="4fbcf-197">Siga Olá [guia oficial](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall 2.0 do CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="4fbcf-198">Instale a CLI 2.0 do Azure com um comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="4fbcf-199">E reiniciar o shell de comando para efeito de tootake alterações:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="4fbcf-200">Instalação do Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="4fbcf-200">Install Arduino IDE</span></span>

<span data-ttu-id="4fbcf-201">Olá extensão Arduino de código do Visual Studio se baseia em Olá Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="4fbcf-202">Baixe e instale Olá [Arduino IDE para macOS](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="4fbcf-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="4fbcf-203">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4fbcf-203">Install Visual Studio Code</span></span>

<span data-ttu-id="4fbcf-204">Baixe e instale o [Visual Studio Code para macOS](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="4fbcf-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="4fbcf-205">Essa será a ferramenta de desenvolvimento principal Olá para criar aplicativos de DevKit de IoT.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="4fbcf-206">Baixe o pacote mais recente</span><span class="sxs-lookup"><span data-stu-id="4fbcf-206">Download latest package</span></span>

1. <span data-ttu-id="4fbcf-207">Instale o Node.js.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-207">Install Node.js.</span></span> <span data-ttu-id="4fbcf-208">Você pode usar o Gerenciador de pacotes macOS populares [Homebrew](https://brew.sh/) ou [pré-criadas instalador](https://nodejs.org/en/download/) tooinstall-lo.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="4fbcf-209">Baixe o arquivo `.zip` que contém scripts de tarefas necessárias para o desenvolvimento de DevKit no VS Code.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="4fbcf-210">Baixar</span><span class="sxs-lookup"><span data-stu-id="4fbcf-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="4fbcf-211">Localizar Olá `.zip` e extraia-o.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="4fbcf-212">Em seguida, inicie **Terminal** aplicativo e execução hello tooconfigure comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="4fbcf-213">Mova pasta extraída tooyour macOS usuário pasta:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="4fbcf-214">Instale os pacotes `npm`:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="4fbcf-215">Instalação da extensão de VS Code para Arduino</span><span class="sxs-lookup"><span data-stu-id="4fbcf-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="4fbcf-216">Código do Visual Studio permite extensões de mercado tooinstall diretamente na ferramenta hello, simplesmente clique ícone de extensões de saudação no painel de menus à esquerda do hello e procure `Arduino` tooinstall:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![extensões de instalação](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="4fbcf-218">Instalação do pacote de placa do DevKit</span><span class="sxs-lookup"><span data-stu-id="4fbcf-218">Install DevKit board package</span></span>

<span data-ttu-id="4fbcf-219">Você precisará tooadd placa de DevKit de hello usando Olá Gerenciador de quadro no código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="4fbcf-220">Use `Cmd+Shift+P` tooinvoke paleta e o tipo de comando **Arduino** , em seguida, localizar e selecionar **Arduino: Gerenciador de quadro**.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="4fbcf-221">Clique em **'URLs adicionais'** na parte inferior de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="4fbcf-222">![instalação adicional de URLs](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="4fbcf-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="4fbcf-223">Em Olá `settings.json` arquivo, adicione uma linha na parte inferior de saudação do `USER SETTINGS` painel e salvar.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![instalação de configurações de json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="4fbcf-225">Agora no hello placa Manager Pesquisar 'az3166' e instalar a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="4fbcf-226">![instalação az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="4fbcf-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="4fbcf-227">Agora você tem todas as ferramentas necessárias hello e pacotes instalados para macOS.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="4fbcf-228">Abra a pasta do projeto</span><span class="sxs-lookup"><span data-stu-id="4fbcf-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="4fbcf-229">Iniciar o Código VS</span><span class="sxs-lookup"><span data-stu-id="4fbcf-229">Launch VS Code</span></span>

<span data-ttu-id="4fbcf-230">Verifique se que o DevKit não está conectado.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="4fbcf-231">Inicie o VS código primeiro e conectar Olá DevKit tooyour computador.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="4fbcf-232">O VS Code o encontra automaticamente e abre uma página pop up de introdução:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="4fbcf-234">Eventualmente, ao iniciar o VS Code, aparecerá um erro notificando que não foi possível encontrar o Arduino IDE nem o pacote de placa relacionado.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="4fbcf-235">toosolve-lo, código VS fechar, inicie o IDE Arduino novamente e o código do VS devem localizar o caminho Arduino IDE corretamente.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="4fbcf-236">Abra a pasta de exemplos de Arduino</span><span class="sxs-lookup"><span data-stu-id="4fbcf-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="4fbcf-237">Alternar muito**'Arduino exemplos'** guia, navegue até muito`Examples for MXCHIP AZ3166 > AzureIoT` e clique em `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![Exemplos de minisolução](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="4fbcf-239">Se ocorrer o painel de saudação tooclose, tooreload-lo, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) paleta e o tipo de comando tooinvoke **Arduino** toofind e selecione **Arduino: exemplos**.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="4fbcf-240">Provisionamento dos serviços do Azure</span><span class="sxs-lookup"><span data-stu-id="4fbcf-240">Provision Azure services</span></span>

<span data-ttu-id="4fbcf-241">Na janela de solução hello, executar a tarefa `Ctrl+P` (macOS: `Cmd+P`), digitando a provisão de nuvem de tarefas:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="4fbcf-242">Em Olá o código de VS terminal, que uma linha de comando interativa orientará Olá provisionamento necessário serviços do Azure:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![provisionamento de nuvem de minisolução](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="4fbcf-244">Compilação e carregamento do esboço do Arduino</span><span class="sxs-lookup"><span data-stu-id="4fbcf-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="4fbcf-245">Instalação da biblioteca necessária</span><span class="sxs-lookup"><span data-stu-id="4fbcf-245">Install required library</span></span>

1. <span data-ttu-id="4fbcf-246">Pressione `F1` ou `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) paleta e o tipo de comando tooinvoke **Arduino** , em seguida, localizar e selecionar **Arduino: Gerenciador de biblioteca**.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="4fbcf-247">Procure `ArduinoJson` biblioteca e clique em **instalar**</span><span class="sxs-lookup"><span data-stu-id="4fbcf-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="4fbcf-248">Criar e carregar o código de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="4fbcf-248">Build and upload hello device code</span></span>

<span data-ttu-id="4fbcf-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'carregamento de dispositivo de tarefa'.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="4fbcf-250">Olá terminal solicitará que você tooenter modo de configuração.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="4fbcf-251">toodo, portanto, mantenha pressionado um e botão de redefinição de saudação push e versão.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="4fbcf-252">tela Hello exibirá 'Configuration'.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="4fbcf-253">Esta é cadeia de conexão do hello tooset recupera da etapa 'tarefa nuvem-provisão'.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="4fbcf-254">Em seguida, iniciará Verificando e carregando um esboço de Arduino hello:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![carregamento de dispositivo de minisolução](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="4fbcf-256">Olá DevKit reinicializará e iniciar a execução de código hello.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="4fbcf-257">Projeto de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="4fbcf-257">Test hello project</span></span>

<span data-ttu-id="4fbcf-258">No código VS, clique Olá power plug ícone tooopen Olá Monitor série da barra de status de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="4fbcf-259">aplicativo de exemplo Hello está executando com êxito quando você vir Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="4fbcf-260">Olá exibe Serial Monitor Olá mesmas informações que o conteúdo de Olá Olá a captura de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="4fbcf-261">Olá LED no MXChip IoT DevKit estiver piscando.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![Saída final no VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="4fbcf-263">Comentários e problemas</span><span class="sxs-lookup"><span data-stu-id="4fbcf-263">Problems and feedback</span></span>

<span data-ttu-id="4fbcf-264">Você pode encontrar [perguntas frequentes](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) se você encontrar problemas ou chegar toous de canais de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fbcf-265">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4fbcf-265">Next steps</span></span>

<span data-ttu-id="4fbcf-266">Você se conectou com êxito um tooyour MXChip DevKit de IoT IoT Hub e enviado Olá capturados hub IoT do sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="4fbcf-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="4fbcf-267">toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="4fbcf-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="4fbcf-268">Gerenciar mensagens do dispositivos de nuvem com o iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="4fbcf-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="4fbcf-269">Salvar mensagens de IoT Hub tooAzure armazenamento de dados</span><span class="sxs-lookup"><span data-stu-id="4fbcf-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="4fbcf-270">Usar dados de sensor em tempo real do Power BI toovisualize do Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4fbcf-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="4fbcf-271">Usar dados de sensor em tempo real de toovisualize de aplicativos Web do Azure de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4fbcf-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="4fbcf-272">Previsão do tempo usando dados de sensor de saudação do seu hub IoT no aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="4fbcf-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="4fbcf-273">Gerenciamento de dispositivos com o iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="4fbcf-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="4fbcf-274">Monitoramento remoto e notificações com Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="4fbcf-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)