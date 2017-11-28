---
title: Connect Raspberry PI (C) tooAzure IoT - solucionar | Microsoft Docs
description: "Página de experiência de framboesa Pi Node Olá de solução de problemas"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: problemas de iot, problemas internet das coisas
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="ff89b-104">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ff89b-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="ff89b-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="ff89b-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="ff89b-106">aplicativo Hello também será executado, mas Olá LED estiver piscando não</span><span class="sxs-lookup"><span data-stu-id="ff89b-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="ff89b-107">Esse problema é sempre conectividade de circuito toohardware relacionados.</span><span class="sxs-lookup"><span data-stu-id="ff89b-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="ff89b-108">Use Olá etapas tooidentify problemas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff89b-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="ff89b-109">Verifique que você escolheu Olá correto **GPIO** em seu quadro.</span><span class="sxs-lookup"><span data-stu-id="ff89b-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="ff89b-110">Olá duas portas devem ser **GPIO GND (Pin 6)** e **GPIO 04 (7 Pin)**.</span><span class="sxs-lookup"><span data-stu-id="ff89b-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="ff89b-111">Verifique se polaridade de saudação do seu LED está correta.</span><span class="sxs-lookup"><span data-stu-id="ff89b-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="ff89b-112">trecho mais Olá deve indicar Olá **positivo**, pin do nó.</span><span class="sxs-lookup"><span data-stu-id="ff89b-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="ff89b-113">Saudação de uso **3.3 v fixar** e **GND Pin** em framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="ff89b-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="ff89b-114">Trate Pi como Olá corrente.</span><span class="sxs-lookup"><span data-stu-id="ff89b-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="ff89b-115">Verifique que Olá LED funciona bem.</span><span class="sxs-lookup"><span data-stu-id="ff89b-115">Check that hello LED works fine.</span></span>

![Especificação do LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="ff89b-117">Outros problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="ff89b-117">Other hardware issues</span></span>
<span data-ttu-id="ff89b-118">Para obter informações sobre como resolver problemas comuns de framboesa Pi 3, consulte Olá [página oficial de solução de problemas](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ff89b-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="ff89b-119">Problemas do pacote de Node.js</span><span class="sxs-lookup"><span data-stu-id="ff89b-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="ff89b-120">Sem resposta durante as tarefas de gulp</span><span class="sxs-lookup"><span data-stu-id="ff89b-120">No response during gulp tasks</span></span>
<span data-ttu-id="ff89b-121">Se você encontrar problemas em vez de tarefas em execução, você pode adicionar Olá `--verbose` opção de depuração.</span><span class="sxs-lookup"><span data-stu-id="ff89b-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="ff89b-122">Tente tooterminate atual gulp tarefas usando Ctrl + C e execute a saudação comando em suas mensagens de depuração de toosee de janela de console a seguir.</span><span class="sxs-lookup"><span data-stu-id="ff89b-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="ff89b-123">Você pode ver mensagens de erro detalhadas em sua saída do console.</span><span class="sxs-lookup"><span data-stu-id="ff89b-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="ff89b-124">Problemas de descoberta de dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff89b-124">Device discovery issues</span></span>
<span data-ttu-id="ff89b-125">Para obter ajuda na solução de problemas comuns com hello `devdisco` de comando, verifique Olá [Leiame](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="ff89b-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="ff89b-126">problemas de npm</span><span class="sxs-lookup"><span data-stu-id="ff89b-126">npm issues</span></span>
<span data-ttu-id="ff89b-127">Tente tooupdate seu pacote npm usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff89b-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="ff89b-128">Se o problema de saudação ainda existe, deixar seus comentários no final deste artigo hello ou criar um problema do GitHub em nosso [repositório de exemplo](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ff89b-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="ff89b-129">Depuração remota</span><span class="sxs-lookup"><span data-stu-id="ff89b-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="ff89b-130">Execute o aplicativo de exemplo hello no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="ff89b-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="ff89b-131">Quando o mecanismo de depuração Olá estiver pronto, você deverá ver ```Debugger listening on port 5858``` na saída do console hello.</span><span class="sxs-lookup"><span data-stu-id="ff89b-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="ff89b-132">Configure o dispositivo remoto do Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="ff89b-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="ff89b-133">Olá abrir **depurar** painel no lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff89b-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="ff89b-134">Clique em Olá verde **iniciar depuração** botão (F5).</span><span class="sxs-lookup"><span data-stu-id="ff89b-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="ff89b-135">O Visual Studio Code abre um arquivo launch.json.</span><span class="sxs-lookup"><span data-stu-id="ff89b-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="ff89b-136">Atualize o arquivo de Launch de saudação com hello conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ff89b-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="ff89b-137">Substituir `[device hostname or IP address]` com o nome de host ou endereço IP de dispositivo real do hello.</span><span class="sxs-lookup"><span data-stu-id="ff89b-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="ff89b-138">toolearn mais sobre Olá Visual Studio depuração, consulte muito[depuração no Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="ff89b-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Configuração de depuração remota](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="ff89b-140">Anexar o aplicativo remoto toohello</span><span class="sxs-lookup"><span data-stu-id="ff89b-140">Attach toohello remote application</span></span>
<span data-ttu-id="ff89b-141">Clique em Olá verde **iniciar depuração** (F5) botão toostart depuração.</span><span class="sxs-lookup"><span data-stu-id="ff89b-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="ff89b-142">Leitura [JavaScript no código VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn mais sobre o depurador de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff89b-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Depuração remota interativa](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="ff89b-144">Problemas da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ff89b-144">Azure CLI issues</span></span>
<span data-ttu-id="ff89b-145">Hello Azure interface de linha de comando (CLI do Azure) é uma compilação de visualização.</span><span class="sxs-lookup"><span data-stu-id="ff89b-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="ff89b-146">soluções de tooseek, você pode usar o hello [guia de instalação de visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="ff89b-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="ff89b-147">Se você encontrar quaisquer erros com a ferramenta hello, arquivo um [problema](https://github.com/Azure/azure-cli/issues) em Olá **problemas** seção do repositório do GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="ff89b-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="ff89b-148">Para obter ajuda na solução de problemas comuns, consulte Olá [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="ff89b-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="ff89b-149">Problemas de instalação do Python</span><span class="sxs-lookup"><span data-stu-id="ff89b-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="ff89b-150">Problemas de instalação herdada (macOS)</span><span class="sxs-lookup"><span data-stu-id="ff89b-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="ff89b-151">Ao instalar o pip, um erro de permissão será lançado quando houver pacotes herdados instalados com permissões **su**.</span><span class="sxs-lookup"><span data-stu-id="ff89b-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="ff89b-152">Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada.</span><span class="sxs-lookup"><span data-stu-id="ff89b-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="ff89b-153">Alguns pacotes de pip de uma instalação anterior foram criados pela raiz, que faz com que o erro de permissão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff89b-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="ff89b-154">Olá solução é tooremove esses pacotes instalados pela raiz.</span><span class="sxs-lookup"><span data-stu-id="ff89b-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="ff89b-155">Use essa tarefa de saudação toocomplete as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff89b-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="ff89b-156">Acesse: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="ff89b-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="ff89b-157">Listar pacotes criados por raiz: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="ff89b-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="ff89b-158">Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="ff89b-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="ff89b-159">Reinstale o Python.</span><span class="sxs-lookup"><span data-stu-id="ff89b-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="ff89b-160">Problemas do Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="ff89b-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="ff89b-161">Se você tiver configurado com êxito o hub IoT do Azure com a CLI do Azure, e você precisa de uma ferramenta toomanage Olá os dispositivos que estão se conectando tooyour IoT hub, tente Olá ferramentas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ff89b-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="ff89b-162">Gerenciador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="ff89b-162">Device explorer</span></span>
<span data-ttu-id="ff89b-163">Olá [explorer dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ferramenta é executada em sua máquina local do Windows e se conecta tooyour IoT hub no Azure.</span><span class="sxs-lookup"><span data-stu-id="ff89b-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="ff89b-164">Ele se comunica com os seguintes Olá [pontos de extremidade de IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="ff89b-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="ff89b-165">*Gerenciamento de identidade do dispositivo* tooprovision e gerenciar dispositivos registrados com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff89b-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="ff89b-166">*Receber o dispositivo para nuvem* para que você pode monitorar as mensagens enviadas do hub IoT de tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff89b-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="ff89b-167">*Enviar a nuvem para dispositivo* para que você pode enviar mensagens tooyour dispositivos do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff89b-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="ff89b-168">Configure todos os seus recursos de sua cadeia de conexão de hub IoT dentro toouse essa ferramenta.</span><span class="sxs-lookup"><span data-stu-id="ff89b-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="ff89b-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="ff89b-169">iothub-explorer</span></span>
<span data-ttu-id="ff89b-170">[Gerenciador de Hub IOT](https://github.com/Azure/iothub-explorer) é uma ferramenta CLI em várias plataformas de exemplo toomanage dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ff89b-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="ff89b-171">Você pode usar dispositivos de Olá Olá ferramenta toomanage no registro de identidade Olá, monitorar mensagens de dispositivo para nuvem e enviar mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff89b-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="ff89b-172">tooinstall Olá versão (pré-lançamento) mais recente da ferramenta de Gerenciador de Hub IOT hello, executar Olá comandos em seu ambiente de linha de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff89b-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="ff89b-173">Você pode usar Olá Olá de tooget obter ajuda adicional sobre todos os comandos do Gerenciador de Hub IOT e seus parâmetros de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff89b-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="ff89b-174">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ff89b-174">Azure portal</span></span>
<span data-ttu-id="ff89b-175">Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff89b-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="ff89b-176">Você também poderá Olá toouse [portal do Azure](../azure-portal-overview.md) toohelp provisionar, gerenciar e depurar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff89b-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="ff89b-177">Problemas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ff89b-177">Azure Storage issues</span></span>
<span data-ttu-id="ff89b-178">[Gerenciador de armazenamento do Microsoft Azure (visualização)](http://storageexplorer.com) é um aplicativo autônomo da Microsoft que você pode usar toowork com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="ff89b-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="ff89b-179">Usando essa ferramenta, você pode conectar-se a tabela de tooyour e ver dados hello.</span><span class="sxs-lookup"><span data-stu-id="ff89b-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="ff89b-180">Você pode usar essa ferramenta tootroubleshoot seus problemas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff89b-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

