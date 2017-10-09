---
title: "Dispositivo simulado e Gateway do IoT do Azure - Solução de problemas | Microsoft Docs"
description: "Página de solução de problemas de gateway NUC Intel"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: problemas de iot, problemas internet das coisas
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="8e494-104">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8e494-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="8e494-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="8e494-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="8e494-106">SensorTag de TI não pode ser conectado</span><span class="sxs-lookup"><span data-stu-id="8e494-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="8e494-107">problemas de conectividade de SensorTag tootroubleshoot, use Olá [SensorTag aplicativo](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="8e494-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="8e494-108">Problemas com o NUC da Intel</span><span class="sxs-lookup"><span data-stu-id="8e494-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="8e494-109">tootroubleshoot problemas de inicialização, consulte muito[solução de problemas de inicialização não Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="8e494-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="8e494-110">tootroubleshoot problemas do sistema operacional, consulte muito[solução de problemas de sistema operacional Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="8e494-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="8e494-111">tootroubleshoot outros problemas, consulte muito[códigos de piscar e avisar para Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="8e494-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="8e494-112">Problemas do pacote de Node.js</span><span class="sxs-lookup"><span data-stu-id="8e494-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="8e494-113">Sem resposta durante as tarefas de gulp</span><span class="sxs-lookup"><span data-stu-id="8e494-113">No response during gulp tasks</span></span>

<span data-ttu-id="8e494-114">Se você encontrar problemas em vez de tarefas em execução, você pode adicionar Olá `--verbose` opção de depuração.</span><span class="sxs-lookup"><span data-stu-id="8e494-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="8e494-115">Tente tooterminate atual gulp tarefas usando `Ctrl + C`, e, em seguida, Olá execução após o comando em suas mensagens de depuração de toosee de janela de console.</span><span class="sxs-lookup"><span data-stu-id="8e494-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="8e494-116">Você pode ver mensagens de erro detalhadas em sua saída do console.</span><span class="sxs-lookup"><span data-stu-id="8e494-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="8e494-117">Problemas de descoberta de dispositivo</span><span class="sxs-lookup"><span data-stu-id="8e494-117">Device discovery issues</span></span>

<span data-ttu-id="8e494-118">Para obter ajuda na solução de problemas comuns com hello `discover-sensortag` de comando, verifique Olá [página wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="8e494-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="8e494-119">problemas de npm</span><span class="sxs-lookup"><span data-stu-id="8e494-119">npm issues</span></span>

<span data-ttu-id="8e494-120">Tente tooupdate seu pacote npm executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e494-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="8e494-121">Se o problema de saudação ainda existe, deixar seus comentários no final deste artigo hello ou criar um problema do GitHub em nosso [repositório de exemplo](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="8e494-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="8e494-122">Depuração Remota</span><span class="sxs-lookup"><span data-stu-id="8e494-122">Remote Debugging</span></span>
> <span data-ttu-id="8e494-123">As instruções abaixo se destinam à depuração dos scripts node.js usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="8e494-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="8e494-124">Execute o aplicativo de exemplo hello no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="8e494-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="8e494-125">Execute o aplicativo de exemplo hello no modo de depuração por meio de saudação comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e494-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="8e494-126">Quando o mecanismo de depuração Olá estiver pronto, você deverá ver `Debugger listening on port 5858` na saída do console hello.</span><span class="sxs-lookup"><span data-stu-id="8e494-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="8e494-127">Configure o dispositivo remoto do Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="8e494-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="8e494-128">Olá abrir **depurar** painel no lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e494-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="8e494-129">Clique em Olá verde **iniciar depuração** botão (F5).</span><span class="sxs-lookup"><span data-stu-id="8e494-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="8e494-130">O Visual Studio Code abre um arquivo `launch.json`.</span><span class="sxs-lookup"><span data-stu-id="8e494-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="8e494-131">Saudação de atualização `launch.json` arquivo com hello conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="8e494-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="8e494-132">Substituir `[device hostname or IP address]` com o nome de host ou endereço IP de dispositivo real do hello.</span><span class="sxs-lookup"><span data-stu-id="8e494-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Configuração de Depuração Remota](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="8e494-134">Anexar o aplicativo remoto toohello</span><span class="sxs-lookup"><span data-stu-id="8e494-134">Attach toohello remote application</span></span>

<span data-ttu-id="8e494-135">Clique em Olá verde **iniciar depuração** (F5) botão toostart depuração.</span><span class="sxs-lookup"><span data-stu-id="8e494-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="8e494-136">Leitura [JavaScript no código VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn mais sobre o depurador de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e494-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Depurar o Exemplo de BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="8e494-138">Problemas da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8e494-138">Azure CLI issues</span></span>

<span data-ttu-id="8e494-139">Hello Azure interface de linha de comando (CLI do Azure) é uma compilação de visualização.</span><span class="sxs-lookup"><span data-stu-id="8e494-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="8e494-140">soluções de tooseek, você pode usar o hello [guia de instalação de visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="8e494-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="8e494-141">Se você encontrar quaisquer erros com a ferramenta hello, arquivo um [problema](https://github.com/Azure/azure-cli/issues) em Olá **problemas** seção do repositório do GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="8e494-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="8e494-142">Para obter ajuda na solução de problemas comuns, consulte Olá [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="8e494-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="8e494-143">Se você atender a "Não foi possível localizar uma versão que satisfaz o requisito de hello", por favor, comando a seguir de execução Olá versão de toolastest pip tooupgrade.</span><span class="sxs-lookup"><span data-stu-id="8e494-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="8e494-144">Problemas de instalação do Python</span><span class="sxs-lookup"><span data-stu-id="8e494-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="8e494-145">Problemas de instalação herdada (macOS)</span><span class="sxs-lookup"><span data-stu-id="8e494-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="8e494-146">Ao instalar o pip, um erro de permissão será lançado quando houver pacotes herdados instalados com permissões **su**.</span><span class="sxs-lookup"><span data-stu-id="8e494-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="8e494-147">Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada.</span><span class="sxs-lookup"><span data-stu-id="8e494-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="8e494-148">Alguns pacotes de pip de uma instalação anterior foram criados pela raiz, que faz com que o erro de permissão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e494-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="8e494-149">Olá solução é tooremove esses pacotes instalados pela raiz.</span><span class="sxs-lookup"><span data-stu-id="8e494-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="8e494-150">Use essa tarefa de saudação toocomplete as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e494-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="8e494-151">Vá muito`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="8e494-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="8e494-152">Listar pacotes criados por raiz: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="8e494-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="8e494-153">Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="8e494-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="8e494-154">Reinstale o Python.</span><span class="sxs-lookup"><span data-stu-id="8e494-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="8e494-155">Problemas do Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="8e494-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="8e494-156">Se você tiver configurado com êxito o hub IoT do Azure com hello CLI do Azure, e você precisa de uma ferramenta toomanage Olá os dispositivos que estão se conectando tooyour IoT hub, tente Olá ferramentas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8e494-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="8e494-157">Gerenciador de Dispositivos</span><span class="sxs-lookup"><span data-stu-id="8e494-157">Device Explorer</span></span>

<span data-ttu-id="8e494-158">[Gerenciador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) é executado em sua máquina local do Windows e se conecta tooyour IoT hub no Azure.</span><span class="sxs-lookup"><span data-stu-id="8e494-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="8e494-159">Ele se comunica com os seguintes Olá [pontos de extremidade de IoT Hub](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="8e494-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="8e494-160">Tooprovision de gerenciamento de identidade do dispositivo e gerenciar dispositivos registrados com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8e494-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="8e494-161">Receba o dispositivo na nuvem para que você pode monitorar as mensagens enviadas do hub IoT de tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e494-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="8e494-162">Envie nuvem para dispositivo para que você pode enviar mensagens tooyour dispositivos do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8e494-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="8e494-163">Configure todos os seus recursos de sua cadeia de conexão de hub IoT dentro toouse essa ferramenta.</span><span class="sxs-lookup"><span data-stu-id="8e494-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="8e494-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="8e494-164">iothub-explorer</span></span>

<span data-ttu-id="8e494-165">[Gerenciador de Hub IOT](https://github.com/Azure/iothub-explorer) é uma ferramenta CLI em várias plataformas de exemplo toomanage clientes de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="8e494-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="8e494-166">Você pode usar dispositivos de Olá Olá ferramenta toomanage no registro de identidade hello, monitorar mensagens de dispositivo para nuvem e enviar comandos de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e494-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="8e494-167">tooinstall Olá versão mais recente (pré-lançamento) da ferramenta de Gerenciador de Hub IOT hello, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e494-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="8e494-168">tooget obter ajuda adicional sobre todos os Olá comandos do Gerenciador de Hub IOT e seus parâmetros, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e494-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="8e494-169">Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8e494-169">hello Azure portal</span></span>

<span data-ttu-id="8e494-170">Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e494-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="8e494-171">Você também poderá Olá toouse [portal do Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provisionar, gerenciar e depurar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e494-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="8e494-172">Problemas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8e494-172">Azure Storage issues</span></span>

<span data-ttu-id="8e494-173">[Gerenciador de armazenamento do Microsoft Azure (visualização)](http://storageexplorer.com/) é um aplicativo autônomo da Microsoft que você pode usar toowork com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="8e494-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="8e494-174">Usando essa ferramenta, você pode conectar-se a tabela de tooyour e ver dados hello.</span><span class="sxs-lookup"><span data-stu-id="8e494-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="8e494-175">Você pode usar essa ferramenta tootroubleshoot seus problemas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e494-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
