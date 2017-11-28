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
ms.openlocfilehash: eae4c112accaefa8bd1bf85f7b43badc2f491dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="9a8b5-104">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9a8b5-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="9a8b5-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="9a8b5-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="9a8b5-106">SensorTag de TI não pode ser conectado</span><span class="sxs-lookup"><span data-stu-id="9a8b5-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="9a8b5-107">Para solucionar problemas de conectividade do SensorTag, use o [aplicativo SensorTag](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="9a8b5-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="9a8b5-108">Problemas com o NUC da Intel</span><span class="sxs-lookup"><span data-stu-id="9a8b5-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="9a8b5-109">Para solucionar problemas de inicialização, consulte [solução de problemas de inicialização no NUC da Intel](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="9a8b5-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="9a8b5-110">Para solucionar problemas do sistema operacional, consulte [solução de problemas de sistema operacional no NUC da Intel](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="9a8b5-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="9a8b5-111">Para solucionar outros problemas, consulte [Códigos de Piscada e de Bipe para o NUC da Intel](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="9a8b5-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="9a8b5-112">Problemas do pacote de Node.js</span><span class="sxs-lookup"><span data-stu-id="9a8b5-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="9a8b5-113">Sem resposta durante as tarefas de gulp</span><span class="sxs-lookup"><span data-stu-id="9a8b5-113">No response during gulp tasks</span></span>

<span data-ttu-id="9a8b5-114">Se você encontrar problemas ao executar tarefas de gulp, adicione a opção `--verbose` para depuração.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="9a8b5-115">Tente finalizar as tarefas de gulp atuais usando `Ctrl + C` e, em seguida, execute o seguinte comando na janela do console para ver mensagens de depuração.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="9a8b5-116">Você pode ver mensagens de erro detalhadas em sua saída do console.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="9a8b5-117">Problemas de descoberta de dispositivo</span><span class="sxs-lookup"><span data-stu-id="9a8b5-117">Device discovery issues</span></span>

<span data-ttu-id="9a8b5-118">Para obter ajuda na solução de problemas comuns com o comando `discover-sensortag`, consulte a [página wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="9a8b5-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="9a8b5-119">problemas de npm</span><span class="sxs-lookup"><span data-stu-id="9a8b5-119">npm issues</span></span>

<span data-ttu-id="9a8b5-120">Tente atualizar o pacote npm executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a8b5-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="9a8b5-121">Se o problema persistir, deixe seus comentários no final deste artigo ou crie um problema de GitHub em nosso [repositório de exemplo](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9a8b5-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="9a8b5-122">Depuração Remota</span><span class="sxs-lookup"><span data-stu-id="9a8b5-122">Remote Debugging</span></span>
> <span data-ttu-id="9a8b5-123">As instruções abaixo se destinam à depuração dos scripts node.js usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="9a8b5-124">Execute o aplicativo de exemplo no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="9a8b5-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="9a8b5-125">Execute o aplicativo de exemplo no modo de depuração executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="9a8b5-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="9a8b5-126">Quando o mecanismo de depuração estiver pronto, você deverá ver `Debugger listening on port 5858` na saída do console.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="9a8b5-127">Configurar o Visual Studio Code para se conectar ao dispositivo remoto</span><span class="sxs-lookup"><span data-stu-id="9a8b5-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="9a8b5-128">Abra o painel **Depurar** painel no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="9a8b5-129">Clique no botão verde **Iniciar Depuração** (F5).</span><span class="sxs-lookup"><span data-stu-id="9a8b5-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="9a8b5-130">O Visual Studio Code abre um arquivo `launch.json`.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="9a8b5-131">Atualize o arquivo `launch.json` com o seguinte conteúdo.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="9a8b5-132">Substitua `[device hostname or IP address]` pelo nome do host ou endereço IP do dispositivo real.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="9a8b5-134">Anexar ao aplicativo remoto</span><span class="sxs-lookup"><span data-stu-id="9a8b5-134">Attach to the remote application</span></span>

<span data-ttu-id="9a8b5-135">Clique no botão verde **Iniciar Depuração** (F5) para iniciar a depuração.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="9a8b5-136">Leia [JavaScript no Código do VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) para saber mais sobre o depurador.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Depurar o Exemplo de BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="9a8b5-138">Problemas da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9a8b5-138">Azure CLI issues</span></span>

<span data-ttu-id="9a8b5-139">A interface de linha de comando do Azure (CLI do Azure) é uma compilação de visualização.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="9a8b5-140">Para procurar soluções, você pode consultar o [Guia de Instalação de Visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="9a8b5-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="9a8b5-141">Se você encontrar erros com a ferramenta, emita um [problema](https://github.com/Azure/azure-cli/issues) na seção **problemas** do repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="9a8b5-142">Para obter ajuda para solucionar problemas comuns, consulte o [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="9a8b5-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="9a8b5-143">Se você receber a mensagem “Não foi possível localizar uma versão que atenda ao requisito”, execute o seguinte comando para atualizar o pip para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="9a8b5-144">Problemas de instalação do Python</span><span class="sxs-lookup"><span data-stu-id="9a8b5-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="9a8b5-145">Problemas de instalação herdada (macOS)</span><span class="sxs-lookup"><span data-stu-id="9a8b5-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="9a8b5-146">Ao instalar o pip, um erro de permissão será lançado quando houver pacotes herdados instalados com permissões **su**.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="9a8b5-147">Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="9a8b5-148">Alguns pacotes do pip de uma instalação anterior foram criados pela raiz, o que causa o erro de permissão.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="9a8b5-149">A solução é remover os pacotes instalados pela raiz.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="9a8b5-150">Use as etapas a seguir para concluir esta tarefa:</span><span class="sxs-lookup"><span data-stu-id="9a8b5-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="9a8b5-151">Acesse `/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="9a8b5-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="9a8b5-152">Listar pacotes criados por raiz: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="9a8b5-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="9a8b5-153">Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="9a8b5-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="9a8b5-154">Reinstale o Python.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="9a8b5-155">Problemas do Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="9a8b5-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="9a8b5-156">Se você tiver provisionado com êxito o Hub IoT do Azure com a CLI do Azure e precisar de uma ferramenta para gerenciar os dispositivos conectados ao seu Hub IoT, tente as seguintes ferramentas.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="9a8b5-157">Gerenciador de Dispositivos</span><span class="sxs-lookup"><span data-stu-id="9a8b5-157">Device Explorer</span></span>

<span data-ttu-id="9a8b5-158">O [Gerenciador de Dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) é executado no computador local do Windows e se conecta ao seu hub IoT no Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="9a8b5-159">Ele se comunica com os seguintes [pontos de extremidade de Hub IoT](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="9a8b5-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="9a8b5-160">Gerenciamento de identidade do dispositivo para provisionar e gerenciar dispositivos registrados com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="9a8b5-161">Receber do dispositivo para nuvem para que você possa monitorar as mensagens enviadas de seu dispositivo ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="9a8b5-162">Enviar da nuvem para o dispositivo para que você possa enviar mensagens para seus dispositivos do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="9a8b5-163">Configure a cadeia de conexão do Hub IoT dentro desta ferramenta para usar todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="9a8b5-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="9a8b5-164">iothub-explorer</span></span>

<span data-ttu-id="9a8b5-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) é uma ferramenta de CLI de várias plataformas de exemplo para gerenciar clientes de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="9a8b5-166">Use a ferramenta para gerenciar os dispositivos no registro de identidade, monitorar mensagens de dispositivo para a nuvem e enviar comandos de nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="9a8b5-167">Para instalar a versão mais recente (pré-lançamento) da ferramenta iothub-explorer, execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a8b5-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="9a8b5-168">Para obter ajuda adicional sobre todos os comandos do iothub-explorer e seus parâmetros, execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a8b5-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="9a8b5-169">O Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9a8b5-169">The Azure portal</span></span>

<span data-ttu-id="9a8b5-170">Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="9a8b5-171">Você também poderá usar o [portal do Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) para ajudar a provisionar, gerenciar e depurar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="9a8b5-172">Problemas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="9a8b5-172">Azure Storage issues</span></span>

<span data-ttu-id="9a8b5-173">[O Gerenciador de Armazenamento do Microsoft Azure (Preview)](http://storageexplorer.com/) é um aplicativo autônomo da Microsoft que pode ser usado para trabalhar com dados do Armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="9a8b5-174">Com essa ferramenta você pode se conectar à sua tabela e ver os dados contidos nela.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="9a8b5-175">Você pode usar essa ferramenta para solucionar seus problemas de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8b5-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
