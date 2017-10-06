---
title: Connect Raspberry PI (C) tooAzure IoT - solucionar | Microsoft Docs
description: "Página de solução de problemas para experiência Raspberry Pi Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: problemas de iot, problemas internet das coisas
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="e7a42-104">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e7a42-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="e7a42-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="e7a42-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="e7a42-106">aplicativo Hello também será executado, mas Olá LED estiver piscando não</span><span class="sxs-lookup"><span data-stu-id="e7a42-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="e7a42-107">Esse problema é sempre conectividade de circuito de hardware toohello relacionados.</span><span class="sxs-lookup"><span data-stu-id="e7a42-107">This issue is always related toohello hardware circuit connectivity.</span></span> <span data-ttu-id="e7a42-108">Use Olá etapas tooidentify problemas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e7a42-108">Use hello following steps tooidentify problems.</span></span>

1. <span data-ttu-id="e7a42-109">Verifique que você escolheu Olá correto **GPIO** em seu quadro.</span><span class="sxs-lookup"><span data-stu-id="e7a42-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="e7a42-110">Olá duas portas devem ser **GPIO GND (Pin 6)** e **GPIO 04 (7 Pin)**.</span><span class="sxs-lookup"><span data-stu-id="e7a42-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="e7a42-111">Verifique se polaridade de saudação do seu LED está correta.</span><span class="sxs-lookup"><span data-stu-id="e7a42-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="e7a42-112">trecho mais Olá deve indicar Olá **positivo**, pin do nó.</span><span class="sxs-lookup"><span data-stu-id="e7a42-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="e7a42-113">Saudação de uso **3.3 v fixar** e **GND Pin** em framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="e7a42-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="e7a42-114">Trate Pi como Olá corrente.</span><span class="sxs-lookup"><span data-stu-id="e7a42-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="e7a42-115">Verifique que Olá LED funciona bem.</span><span class="sxs-lookup"><span data-stu-id="e7a42-115">Check that hello LED works fine.</span></span>

![Especificação do LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="e7a42-117">Outros problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="e7a42-117">Other hardware issues</span></span>
<span data-ttu-id="e7a42-118">Para obter informações sobre como resolver problemas comuns de framboesa Pi 3, consulte Olá [página oficial de solução de problemas](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="e7a42-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="e7a42-119">Problemas do pacote de Node.js</span><span class="sxs-lookup"><span data-stu-id="e7a42-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="e7a42-120">Sem resposta durante as tarefas de gulp</span><span class="sxs-lookup"><span data-stu-id="e7a42-120">No response during gulp tasks</span></span>
<span data-ttu-id="e7a42-121">Se você encontrar problemas ao executar tarefas de gulp, você pode adicionar Olá `--verbose` opção de depuração.</span><span class="sxs-lookup"><span data-stu-id="e7a42-121">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="e7a42-122">Tente tooterminate atual gulp tarefas usando `Ctrl + C`, e, em seguida, Olá execução após o comando em suas mensagens de depuração de toosee de janela de console.</span><span class="sxs-lookup"><span data-stu-id="e7a42-122">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="e7a42-123">Você pode ver mensagens de erro detalhadas em sua saída do console.</span><span class="sxs-lookup"><span data-stu-id="e7a42-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="e7a42-124">Problemas de descoberta de dispositivo</span><span class="sxs-lookup"><span data-stu-id="e7a42-124">Device discovery issues</span></span>
<span data-ttu-id="e7a42-125">Para obter ajuda na solução de problemas comuns com hello `devdisco` de comando, verifique Olá [Leiame](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="e7a42-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="e7a42-126">Problemas de NPM</span><span class="sxs-lookup"><span data-stu-id="e7a42-126">NPM issues</span></span>
<span data-ttu-id="e7a42-127">Tente tooupdate seu pacote NPM com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7a42-127">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="e7a42-128">Se o problema de saudação ainda existe, deixar seus comentários no final deste artigo hello ou criar um problema do GitHub em nosso [repositório de exemplo](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="e7a42-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="e7a42-129">Depuração remota</span><span class="sxs-lookup"><span data-stu-id="e7a42-129">Remote debugging</span></span>

<span data-ttu-id="e7a42-130">O suporte à depuração remota estará disponível em breve na Extensão C/C++ do Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e7a42-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="e7a42-131">Por enquanto, você pode usar GDB por meio do seu terminal SSH favorito:</span><span class="sxs-lookup"><span data-stu-id="e7a42-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="e7a42-132">Problemas da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e7a42-132">Azure-CLI issues</span></span>
<span data-ttu-id="e7a42-133">Hello Azure interface de linha de comando (CLI do Azure) é uma compilação de visualização.</span><span class="sxs-lookup"><span data-stu-id="e7a42-133">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="e7a42-134">Procure a solução em Olá [guia de instalação de visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluções.</span><span class="sxs-lookup"><span data-stu-id="e7a42-134">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="e7a42-135">Tente tooupgrade cli do Azure toolatest versão quando comandos não funcionam conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="e7a42-135">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="e7a42-136">Se você encontrar quaisquer erros com a ferramenta hello, arquivo um [problema](https://github.com/Azure/azure-cli/issues) em Olá **problemas** seção do repositório do GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="e7a42-136">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="e7a42-137">Para ajudar a solucionar problemas comuns, consulte Olá [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="e7a42-137">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="e7a42-138">Se você atender a "Não foi possível localizar uma versão que satisfaz o requisito de hello", por favor, comando a seguir de execução Olá versão de toolastest pip tooupgrade.</span><span class="sxs-lookup"><span data-stu-id="e7a42-138">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="e7a42-139">Problemas de instalação do Python</span><span class="sxs-lookup"><span data-stu-id="e7a42-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="e7a42-140">Problemas de instalação herdada (macOS)</span><span class="sxs-lookup"><span data-stu-id="e7a42-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="e7a42-141">Ao instalar o **pip**, um erro de permissão será lançado quando houver pacotes mais antigos instalados com permissões **su**.</span><span class="sxs-lookup"><span data-stu-id="e7a42-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="e7a42-142">Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada.</span><span class="sxs-lookup"><span data-stu-id="e7a42-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="e7a42-143">Alguns **pip** pacotes de uma instalação anterior foram criados pela raiz, que faz com que o erro de permissão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7a42-143">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="e7a42-144">Olá solução é tooremove esses pacotes instalados pela raiz.</span><span class="sxs-lookup"><span data-stu-id="e7a42-144">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="e7a42-145">Use essa tarefa de saudação toocomplete as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7a42-145">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="e7a42-146">Acesse: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="e7a42-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="e7a42-147">Listar pacotes criados por raiz: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="e7a42-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="e7a42-148">Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="e7a42-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="e7a42-149">Reinstale o Python.</span><span class="sxs-lookup"><span data-stu-id="e7a42-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="e7a42-150">Problemas do Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="e7a42-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="e7a42-151">Se você tiver configurado com êxito o hub IoT do Azure com `azure-cli`, e você precisa de uma ferramenta toomanage Olá os dispositivos que estão se conectando tooyour IoT hub, tente Olá ferramentas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7a42-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="e7a42-152">Gerenciador de Dispositivos</span><span class="sxs-lookup"><span data-stu-id="e7a42-152">Device Explorer</span></span>
<span data-ttu-id="e7a42-153">[Gerenciador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) é executado em sua máquina local do Windows e se conecta tooyour IoT hub no Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a42-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="e7a42-154">Ele se comunica com os seguintes Olá [pontos de extremidade de IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="e7a42-154">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="e7a42-155">*Gerenciamento de identidade do dispositivo* tooprovision e gerenciar dispositivos registrados com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e7a42-155">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="e7a42-156">*Receber o dispositivo para nuvem* para que você pode monitorar as mensagens enviadas do hub IoT de tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e7a42-156">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="e7a42-157">*Enviar a nuvem para dispositivo* para que você pode enviar mensagens tooyour dispositivos do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e7a42-157">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="e7a42-158">Configurar seu `IoT hub connection string` em toouse essa ferramenta todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="e7a42-158">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="e7a42-159">Gerenciador do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="e7a42-159">IoT hub Explorer</span></span>
<span data-ttu-id="e7a42-160">[Hub IoT Explorer](https://github.com/Azure/iothub-explorer) é uma ferramenta CLI em várias plataformas de exemplo toomanage clientes de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e7a42-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="e7a42-161">Você pode usar dispositivos de Olá Olá ferramenta toomanage no registro de identidade hello, monitorar mensagens de dispositivo para nuvem e enviar comandos de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e7a42-161">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="e7a42-162">tooinstall Olá versão (pré-lançamento) mais recente da ferramenta de Gerenciador de Hub IOT hello, executar Olá comandos em seu ambiente de linha de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7a42-162">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="e7a42-163">Você pode usar Olá Olá de tooget obter ajuda adicional sobre todos os comandos do Gerenciador de Hub IOT e seus parâmetros de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7a42-163">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="e7a42-164">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e7a42-164">Azure portal</span></span>
<span data-ttu-id="e7a42-165">Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a42-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="e7a42-166">Você também poderá Olá toouse [portal do Azure](../azure-portal-overview.md) toohelp provisionar, gerenciar e depurar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a42-166">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="e7a42-167">Problemas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e7a42-167">Azure storage issues</span></span>
<span data-ttu-id="e7a42-168">[Gerenciador de armazenamento do Microsoft Azure (visualização)](http://storageexplorer.com) é um aplicativo autônomo da Microsoft que você pode usar toowork com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="e7a42-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="e7a42-169">Usando essa ferramenta, você pode conectar-se a tabela de tooyour e ver dados hello.</span><span class="sxs-lookup"><span data-stu-id="e7a42-169">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="e7a42-170">Você pode usar essa ferramenta tootroubleshoot seus problemas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a42-170">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
