---
title: Conectar o Raspberry Pi (C) ao IoT do Azure - Solucionar problemas | Microsoft Docs
description: "Página de solução de problemas para experiência Raspberry Pi Node.js"
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
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="c4904-104">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="c4904-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="c4904-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="c4904-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="c4904-106">O aplicativo funciona bem, mas o LED não está piscando</span><span class="sxs-lookup"><span data-stu-id="c4904-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="c4904-107">Esse problema está sempre relacionado à conectividade de circuito do hardware.</span><span class="sxs-lookup"><span data-stu-id="c4904-107">This issue is always related to hardware circuit connectivity.</span></span> <span data-ttu-id="c4904-108">Use as etapas a seguir para identificar problemas:</span><span class="sxs-lookup"><span data-stu-id="c4904-108">Use the following steps to identify problems:</span></span>

1. <span data-ttu-id="c4904-109">Verifique se você escolheu o **GPIO** correto na placa.</span><span class="sxs-lookup"><span data-stu-id="c4904-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="c4904-110">As duas portas devem ser **GPIO GND (Pino 6)** e **GPIO 04 (Pino 7)**.</span><span class="sxs-lookup"><span data-stu-id="c4904-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="c4904-111">Verifique se a polaridade do seu LED está correta.</span><span class="sxs-lookup"><span data-stu-id="c4904-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="c4904-112">A base maior deve indicar o pino de nó **positivo**.</span><span class="sxs-lookup"><span data-stu-id="c4904-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="c4904-113">Use o **Pino 3.3 V** e o **Pino GND** em seu Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="c4904-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="c4904-114">Trate o Pi como corrente contínua.</span><span class="sxs-lookup"><span data-stu-id="c4904-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="c4904-115">Verifique se o LED funciona bem.</span><span class="sxs-lookup"><span data-stu-id="c4904-115">Check that the LED works fine.</span></span>

![Especificação do LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="c4904-117">Outros problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="c4904-117">Other hardware issues</span></span>
<span data-ttu-id="c4904-118">Para obter informações sobre como resolver problemas comuns no Raspberry Pi 3, consulte a [página oficial de solução de problemas](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="c4904-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="c4904-119">Problemas do pacote de Node.js</span><span class="sxs-lookup"><span data-stu-id="c4904-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="c4904-120">Sem resposta durante as tarefas de gulp</span><span class="sxs-lookup"><span data-stu-id="c4904-120">No response during gulp tasks</span></span>
<span data-ttu-id="c4904-121">Se você encontrar problemas ao executar tarefas de gulp, adicione a opção `--verbose` para depuração.</span><span class="sxs-lookup"><span data-stu-id="c4904-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="c4904-122">Tente finalizar as tarefas de gulp atuais usando Ctrl + C e, em seguida, execute o seguinte comando na janela do console para ver mensagens de depuração.</span><span class="sxs-lookup"><span data-stu-id="c4904-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="c4904-123">Você pode ver mensagens de erro detalhadas em sua saída do console.</span><span class="sxs-lookup"><span data-stu-id="c4904-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="c4904-124">Problemas de descoberta de dispositivo</span><span class="sxs-lookup"><span data-stu-id="c4904-124">Device discovery issues</span></span>
<span data-ttu-id="c4904-125">Para obter ajuda na solução de problemas comuns com o comando `devdisco`, consulte o [Leiame](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="c4904-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="c4904-126">problemas de npm</span><span class="sxs-lookup"><span data-stu-id="c4904-126">npm issues</span></span>
<span data-ttu-id="c4904-127">Tente atualizar o pacote npm usando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4904-127">Try to update your npm package by using the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="c4904-128">Se o problema persistir, deixe seus comentários no final deste artigo ou crie um problema de GitHub em nosso [repositório de exemplo](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c4904-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="c4904-129">Depuração remota</span><span class="sxs-lookup"><span data-stu-id="c4904-129">Remote debugging</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="c4904-130">Execute o aplicativo de exemplo no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="c4904-130">Run the sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="c4904-131">Quando o mecanismo de depuração estiver pronto, você deverá ver ```Debugger listening on port 5858``` na saída do console.</span><span class="sxs-lookup"><span data-stu-id="c4904-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="c4904-132">Configurar o Visual Studio Code para se conectar ao dispositivo remoto</span><span class="sxs-lookup"><span data-stu-id="c4904-132">Configure Visual Studio Code to connect to the remote device</span></span>
1. <span data-ttu-id="c4904-133">Abra o painel **Depurar** painel no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="c4904-133">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="c4904-134">Clique no botão verde **Iniciar Depuração** (F5).</span><span class="sxs-lookup"><span data-stu-id="c4904-134">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="c4904-135">O Visual Studio Code abre um arquivo launch.json.</span><span class="sxs-lookup"><span data-stu-id="c4904-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="c4904-136">Atualize o arquivo launch.json com o seguinte conteúdo.</span><span class="sxs-lookup"><span data-stu-id="c4904-136">Update the launch.json file with the following content.</span></span> <span data-ttu-id="c4904-137">Substitua `[device hostname or IP address]` pelo nome do host ou endereço IP do dispositivo real.</span><span class="sxs-lookup"><span data-stu-id="c4904-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="c4904-138">Para saber mais sobre a depuração do Visual Studio, consulte [Depuração no Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="c4904-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="c4904-140">Anexar ao aplicativo remoto</span><span class="sxs-lookup"><span data-stu-id="c4904-140">Attach to the remote application</span></span>
<span data-ttu-id="c4904-141">Clique no botão verde **Iniciar Depuração** (F5) para iniciar a depuração.</span><span class="sxs-lookup"><span data-stu-id="c4904-141">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="c4904-142">Leia [JavaScript no Código do VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) para saber mais sobre o depurador.</span><span class="sxs-lookup"><span data-stu-id="c4904-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Depuração remota interativa](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="c4904-144">Problemas da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c4904-144">Azure CLI issues</span></span>
<span data-ttu-id="c4904-145">A interface de linha de comando do Azure (CLI do Azure) é uma compilação de visualização.</span><span class="sxs-lookup"><span data-stu-id="c4904-145">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="c4904-146">Para procurar soluções, você pode consultar o [Guia de Instalação de Visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="c4904-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="c4904-147">Se você encontrar erros com a ferramenta, emita um [problema](https://github.com/Azure/azure-cli/issues) na seção **problemas** do repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="c4904-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="c4904-148">Para obter ajuda para solucionar problemas comuns, consulte o [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="c4904-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="c4904-149">Problemas de instalação do Python</span><span class="sxs-lookup"><span data-stu-id="c4904-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="c4904-150">Problemas de instalação herdada (macOS)</span><span class="sxs-lookup"><span data-stu-id="c4904-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="c4904-151">Ao instalar o pip, um erro de permissão será lançado quando houver pacotes herdados instalados com permissões **su**.</span><span class="sxs-lookup"><span data-stu-id="c4904-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="c4904-152">Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada.</span><span class="sxs-lookup"><span data-stu-id="c4904-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="c4904-153">Alguns pacotes do pip de uma instalação anterior foram criados pela raiz, o que causa o erro de permissão.</span><span class="sxs-lookup"><span data-stu-id="c4904-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="c4904-154">A solução é remover os pacotes instalados pela raiz.</span><span class="sxs-lookup"><span data-stu-id="c4904-154">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="c4904-155">Use as etapas a seguir para concluir esta tarefa:</span><span class="sxs-lookup"><span data-stu-id="c4904-155">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="c4904-156">Acesse: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="c4904-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="c4904-157">Listar pacotes criados por raiz: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="c4904-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="c4904-158">Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="c4904-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="c4904-159">Reinstale o Python.</span><span class="sxs-lookup"><span data-stu-id="c4904-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="c4904-160">Problemas do Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="c4904-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="c4904-161">Se você tiver provisionado com êxito o Hub IoT do Azure com a CLI do Azure e precisar de uma ferramenta para gerenciar os dispositivos conectados ao seu Hub IoT, tente as seguintes ferramentas.</span><span class="sxs-lookup"><span data-stu-id="c4904-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="c4904-162">Gerenciador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="c4904-162">Device explorer</span></span>
<span data-ttu-id="c4904-163">O [Gerenciador de dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) é executado no computador local do Windows e se conecta ao seu hub IoT no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4904-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="c4904-164">Ele se comunica com os seguintes [pontos de extremidade de Hub IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="c4904-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="c4904-165">*Gerenciamento de identidade do dispositivo* para provisionar e gerenciar dispositivos registrados com seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4904-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="c4904-166">*Receber do dispositivo para nuvem* para que você possa monitorar as mensagens enviadas de seu dispositivo ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4904-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="c4904-167">*Enviar do dispositivo para nuvem* para que você possa enviar mensagens para seus dispositivos de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4904-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="c4904-168">Configure a cadeia de conexão do Hub IoT dentro desta ferramenta para usar todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="c4904-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="c4904-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="c4904-169">iothub-explorer</span></span>
<span data-ttu-id="c4904-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) é uma ferramenta de CLI de várias plataformas de exemplo para gerenciar dispositivos.</span><span class="sxs-lookup"><span data-stu-id="c4904-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span></span> <span data-ttu-id="c4904-171">Use a ferramenta para gerenciar os dispositivos no Registro de identidade, monitorar mensagens de dispositivo para a nuvem e enviar mensagens de nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c4904-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="c4904-172">Para instalar a versão mais recente (pré-lançamento) da ferramenta Gerenciador do iothub, execute o comando a seguir em seu ambiente de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="c4904-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="c4904-173">Você pode usar o comando a seguir para obter ajuda adicional sobre todos os comandos do Gerenciador do iothub e seus parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c4904-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="c4904-174">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c4904-174">Azure portal</span></span>
<span data-ttu-id="c4904-175">Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4904-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="c4904-176">Você também poderá usar o [portal do Azure](../azure-portal-overview.md) para ajudar a provisionar, gerenciar e depurar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4904-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="c4904-177">Problemas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c4904-177">Azure Storage issues</span></span>
<span data-ttu-id="c4904-178">[O Gerenciador de Armazenamento do Microsoft Azure (Preview)](http://storageexplorer.com) é um aplicativo autônomo da Microsoft que pode ser usado para trabalhar com dados do Armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="c4904-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="c4904-179">Com essa ferramenta você pode se conectar à sua tabela e ver os dados contidos nela.</span><span class="sxs-lookup"><span data-stu-id="c4904-179">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="c4904-180">Você pode usar essa ferramenta para solucionar seus problemas de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4904-180">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

