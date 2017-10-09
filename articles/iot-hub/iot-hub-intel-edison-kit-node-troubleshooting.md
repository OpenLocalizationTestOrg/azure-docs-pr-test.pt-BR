---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 4: solução de problemas | Microsoft Docs"
description: "Página de solução de problemas da experiência Node.js do Intel Edison"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "solução de problemas do arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="bd74f-104">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="bd74f-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="bd74f-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="bd74f-105">Hardware issues</span></span>
<span data-ttu-id="bd74f-106">Para obter informações sobre como resolver problemas comuns no Intel Edison, consulte Olá [página oficial de solução de problemas](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="bd74f-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="bd74f-107">Problemas do pacote de Node.js</span><span class="sxs-lookup"><span data-stu-id="bd74f-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="bd74f-108">Sem resposta durante as tarefas de gulp</span><span class="sxs-lookup"><span data-stu-id="bd74f-108">No response during gulp tasks</span></span>
<span data-ttu-id="bd74f-109">Se você encontrar problemas ao executar tarefas de gulp, você pode adicionar Olá `--verbose` opção de depuração.</span><span class="sxs-lookup"><span data-stu-id="bd74f-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="bd74f-110">Tente tooterminate atual gulp tarefas usando `Ctrl + C`, e, em seguida, Olá execução após o comando em suas mensagens de depuração de toosee de janela de console.</span><span class="sxs-lookup"><span data-stu-id="bd74f-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="bd74f-111">Você pode ver mensagens de erro detalhadas em sua saída do console.</span><span class="sxs-lookup"><span data-stu-id="bd74f-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="bd74f-112">Problemas de NPM</span><span class="sxs-lookup"><span data-stu-id="bd74f-112">NPM issues</span></span>
<span data-ttu-id="bd74f-113">Tente tooupdate seu pacote NPM com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd74f-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="bd74f-114">Se o problema de saudação ainda existe, deixar seus comentários no final deste artigo hello ou criar um problema do GitHub em nosso [repositório de exemplo][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="bd74f-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="bd74f-115">Depuração remota</span><span class="sxs-lookup"><span data-stu-id="bd74f-115">Remote debugging</span></span>

### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="bd74f-116">Execute o aplicativo de exemplo hello no modo de depuração</span><span class="sxs-lookup"><span data-stu-id="bd74f-116">Run hello sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="bd74f-117">Quando o mecanismo de depuração Olá estiver pronto, você deve ser capaz de toosee ```Debugger listening on port 5858``` da saída do console hello.</span><span class="sxs-lookup"><span data-stu-id="bd74f-117">Once hello debug engine is ready, you should be able toosee ```Debugger listening on port 5858``` from hello console output.</span></span>

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="bd74f-118">Configure o dispositivo remoto do código VS tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="bd74f-118">Configure VS Code tooconnect toohello remote device</span></span>

<span data-ttu-id="bd74f-119">Olá abrir **depurar** painel do lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd74f-119">Open hello **Debug** panel from hello left side.</span></span>

<span data-ttu-id="bd74f-120">Clique em Olá verde **iniciar depuração** botão (F5).</span><span class="sxs-lookup"><span data-stu-id="bd74f-120">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="bd74f-121">Código VS abriria um **Launch** arquivo, que é necessário tooupdate.</span><span class="sxs-lookup"><span data-stu-id="bd74f-121">VS Code would open a **launch.json** file, which you need tooupdate.</span></span>

<span data-ttu-id="bd74f-122">Saudação de atualização **Launch** com hello seguindo o conteúdo do arquivo, substitua `[device hostname or IP address]` com o endereço IP do dispositivo real hello ou nome de host.</span><span class="sxs-lookup"><span data-stu-id="bd74f-122">Update hello **launch.json** file with hello following content, replace `[device hostname or IP address]` with hello actual device IP address or hostname.</span></span>  

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

![Configuração de depuração remota](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="bd74f-124">Anexar o aplicativo remoto toohello</span><span class="sxs-lookup"><span data-stu-id="bd74f-124">Attach toohello remote application</span></span>

<span data-ttu-id="bd74f-125">Clique em Olá verde **iniciar depuração** (F5) botão e aproveitar a depuração.</span><span class="sxs-lookup"><span data-stu-id="bd74f-125">Click hello green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="bd74f-126">Você pode ler [JavaScript no código VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn mais sobre o depurador de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd74f-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Depuração remota interativa](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="bd74f-128">Problemas da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bd74f-128">Azure-CLI issues</span></span>
<span data-ttu-id="bd74f-129">Hello Azure interface de linha de comando (CLI do Azure) é uma compilação de visualização.</span><span class="sxs-lookup"><span data-stu-id="bd74f-129">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="bd74f-130">Procure a solução em Olá [guia de instalação de visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluções.</span><span class="sxs-lookup"><span data-stu-id="bd74f-130">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="bd74f-131">Tente tooupgrade cli do Azure toolatest versão quando comandos não funcionam conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="bd74f-131">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="bd74f-132">Se você encontrar quaisquer erros com a ferramenta hello, arquivo um [problema](https://github.com/Azure/azure-cli/issues) em Olá **problemas** seção do repositório do GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="bd74f-132">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="bd74f-133">Para ajudar a solucionar problemas comuns, consulte Olá [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="bd74f-133">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="bd74f-134">Se você atender a "Não foi possível localizar uma versão que satisfaz o requisito de hello", por favor, comando a seguir de execução Olá versão de toolastest pip tooupgrade.</span><span class="sxs-lookup"><span data-stu-id="bd74f-134">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="bd74f-135">Problemas de instalação do Python</span><span class="sxs-lookup"><span data-stu-id="bd74f-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="bd74f-136">Problemas de instalação herdada (macOS)</span><span class="sxs-lookup"><span data-stu-id="bd74f-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="bd74f-137">Ao instalar o **pip**, um erro de permissão será lançado quando houver pacotes mais antigos instalados com permissões **su**.</span><span class="sxs-lookup"><span data-stu-id="bd74f-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="bd74f-138">Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada.</span><span class="sxs-lookup"><span data-stu-id="bd74f-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="bd74f-139">Alguns **pip** pacotes de uma instalação anterior foram criados pela raiz, que faz com que o erro de permissão de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd74f-139">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="bd74f-140">Olá solução é tooremove esses pacotes instalados pela raiz.</span><span class="sxs-lookup"><span data-stu-id="bd74f-140">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="bd74f-141">Use essa tarefa de saudação toocomplete as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd74f-141">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="bd74f-142">Acesse: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="bd74f-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="bd74f-143">Listar pacotes criados por raiz: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="bd74f-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="bd74f-144">Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="bd74f-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="bd74f-145">Reinstale o Python.</span><span class="sxs-lookup"><span data-stu-id="bd74f-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="bd74f-146">Problemas do Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="bd74f-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="bd74f-147">Se você tiver configurado com êxito o hub IoT do Azure com `azure-cli`, e você precisa de uma ferramenta toomanage Olá os dispositivos que estão se conectando tooyour IoT hub, tente Olá ferramentas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd74f-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="bd74f-148">Gerenciador de Dispositivos</span><span class="sxs-lookup"><span data-stu-id="bd74f-148">Device Explorer</span></span>
<span data-ttu-id="bd74f-149">[Gerenciador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) é executado em sua máquina local do Windows e se conecta tooyour IoT hub no Azure.</span><span class="sxs-lookup"><span data-stu-id="bd74f-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="bd74f-150">Ele se comunica com os seguintes Olá [pontos de extremidade de IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="bd74f-150">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="bd74f-151">_Gerenciamento de identidade do dispositivo_ tooprovision e gerenciar dispositivos registrados com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bd74f-151">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="bd74f-152">_Receber o dispositivo para nuvem_ para que você pode monitorar as mensagens enviadas do hub IoT de tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bd74f-152">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="bd74f-153">_Enviar a nuvem para dispositivo_ para que você pode enviar mensagens tooyour dispositivos do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bd74f-153">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="bd74f-154">Configurar seu `IoT hub connection string` em toouse essa ferramenta todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="bd74f-154">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="bd74f-155">Gerenciador do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="bd74f-155">IoT hub Explorer</span></span>
<span data-ttu-id="bd74f-156">[Hub IoT Explorer](https://github.com/Azure/iothub-explorer) é uma ferramenta CLI em várias plataformas de exemplo toomanage clientes de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="bd74f-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="bd74f-157">Você pode usar dispositivos de Olá Olá ferramenta toomanage no registro de identidade hello, monitorar mensagens de dispositivo para nuvem e enviar comandos de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bd74f-157">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="bd74f-158">tooinstall Olá versão (pré-lançamento) mais recente da ferramenta de Gerenciador de Hub IOT hello, executar Olá comandos em seu ambiente de linha de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd74f-158">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="bd74f-159">Você pode usar Olá Olá de tooget obter ajuda adicional sobre todos os comandos do Gerenciador de Hub IOT e seus parâmetros de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd74f-159">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="bd74f-160">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bd74f-160">Azure portal</span></span>
<span data-ttu-id="bd74f-161">Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd74f-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="bd74f-162">Você também poderá Olá toouse [portal do Azure](../azure-portal-overview.md) toohelp provisionar, gerenciar e depurar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd74f-162">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="bd74f-163">Problemas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="bd74f-163">Azure storage issues</span></span>
<span data-ttu-id="bd74f-164">[Gerenciador de armazenamento do Microsoft Azure (visualização)](http://storageexplorer.com) é um aplicativo autônomo da Microsoft que você pode usar toowork com [armazenamento do Azure](https://azure.microsoft.com/en-us/services/storage/) dados no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="bd74f-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="bd74f-165">Usando essa ferramenta, você pode conectar-se a tabela de tooyour e ver dados hello.</span><span class="sxs-lookup"><span data-stu-id="bd74f-165">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="bd74f-166">Você pode usar essa ferramenta tootroubleshoot seus problemas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd74f-166">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd74f-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd74f-167">Next steps</span></span>
<span data-ttu-id="bd74f-168">Esta página inclui apenas os problemas mais comuns de saudação do kit de Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="bd74f-168">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="bd74f-169">Você também pode deixar comentários inferior tooreport problemas para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="bd74f-169">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="bd74f-170">Voltar muito[começar com Intel Edison (Node. js)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="bd74f-170">Go back too[Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started