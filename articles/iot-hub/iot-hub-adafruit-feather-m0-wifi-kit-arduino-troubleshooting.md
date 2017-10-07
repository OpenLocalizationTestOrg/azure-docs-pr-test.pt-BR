---
title: Connect Arduino (C) tooAzure IoT - solucionar | Microsoft Docs
description: "Página de solução de problemas para a experiência do Adafruit Feather M0 WiFi Arduino"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "solução de problemas do arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed793041ffa1887dbe73067f7c48d2417e982866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="b5220-104">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b5220-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="b5220-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="b5220-105">Hardware issues</span></span>
<span data-ttu-id="b5220-106">Para obter informações sobre como resolver problemas comuns em seu quadro Adafruit difusão M0 Wi-Fi Arduino, consulte Olá [página oficial de solução de problemas](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="b5220-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see hello [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="b5220-107">Problemas do pacote de Node.js</span><span class="sxs-lookup"><span data-stu-id="b5220-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="b5220-108">Sem resposta durante as tarefas de gulp</span><span class="sxs-lookup"><span data-stu-id="b5220-108">No response during gulp tasks</span></span>
<span data-ttu-id="b5220-109">Se você encontrar problemas ao executar tarefas de gulp, você pode adicionar Olá `--verbose` opção de depuração.</span><span class="sxs-lookup"><span data-stu-id="b5220-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="b5220-110">Tente tooterminate atual gulp tarefas usando `Ctrl + C`, e, em seguida, Olá execução após o comando em suas mensagens de depuração de toosee de janela de console.</span><span class="sxs-lookup"><span data-stu-id="b5220-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="b5220-111">Você pode ver mensagens de erro detalhadas em sua saída do console.</span><span class="sxs-lookup"><span data-stu-id="b5220-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="b5220-112">Ou você pode adicionar `--listen` informações de log tooopen porta serial toooutput dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b5220-112">Or you can add `--listen` tooopen serial port toooutput device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="b5220-113">Problemas de NPM</span><span class="sxs-lookup"><span data-stu-id="b5220-113">NPM issues</span></span>
<span data-ttu-id="b5220-114">Tente tooupdate seu pacote NPM com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5220-114">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="b5220-115">Se o problema de saudação ainda existe, deixar seus comentários no final deste artigo hello ou criar um problema do GitHub em nosso [repositório de exemplo][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="b5220-115">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="b5220-116">Problemas da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b5220-116">Azure-CLI issues</span></span>
<span data-ttu-id="b5220-117">Hello Azure interface de linha de comando (CLI do Azure) é uma compilação de visualização.</span><span class="sxs-lookup"><span data-stu-id="b5220-117">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="b5220-118">Procure a solução em Olá [guia de instalação de visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluções.</span><span class="sxs-lookup"><span data-stu-id="b5220-118">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="b5220-119">Tente tooupgrade cli do Azure toolatest versão quando comandos não funcionam conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="b5220-119">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="b5220-120">Se você encontrar quaisquer erros com a ferramenta hello, arquivo um [problema](https://github.com/Azure/azure-cli/issues) em Olá **problemas** seção do repositório do GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="b5220-120">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="b5220-121">Para ajudar a solucionar problemas comuns, consulte Olá [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="b5220-121">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="b5220-122">Se você atender a "Não foi possível localizar uma versão que satisfaz o requisito de hello", por favor, comando a seguir de execução Olá versão de toolastest pip tooupgrade.</span><span class="sxs-lookup"><span data-stu-id="b5220-122">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="b5220-123">Problemas de instalação do Python</span><span class="sxs-lookup"><span data-stu-id="b5220-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="b5220-124">Problemas de instalação herdada (macOS)</span><span class="sxs-lookup"><span data-stu-id="b5220-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="b5220-125">Ao instalar o **pip**, um erro de permissão será lançado quando houver pacotes mais antigos instalados com permissões **su**.</span><span class="sxs-lookup"><span data-stu-id="b5220-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="b5220-126">Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada.</span><span class="sxs-lookup"><span data-stu-id="b5220-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="b5220-127">Alguns **pip** pacotes de uma instalação anterior foram criados pela raiz, que faz com que o erro de permissão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5220-127">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="b5220-128">Olá solução é tooremove esses pacotes instalados pela raiz.</span><span class="sxs-lookup"><span data-stu-id="b5220-128">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="b5220-129">Use essa tarefa de saudação toocomplete as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5220-129">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="b5220-130">Acesse: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="b5220-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="b5220-131">Listar pacotes criados por raiz: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="b5220-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="b5220-132">Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="b5220-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="b5220-133">Reinstale o Python.</span><span class="sxs-lookup"><span data-stu-id="b5220-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="b5220-134">Problemas do Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="b5220-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="b5220-135">Se você tiver configurado com êxito o hub IoT do Azure com `azure-cli`, e você precisa de uma ferramenta toomanage Olá os dispositivos que estão se conectando tooyour IoT hub, tente Olá ferramentas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5220-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="b5220-136">Gerenciador de Dispositivos</span><span class="sxs-lookup"><span data-stu-id="b5220-136">Device Explorer</span></span>
<span data-ttu-id="b5220-137">[Gerenciador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) é executado em sua máquina local do Windows e se conecta tooyour IoT hub no Azure.</span><span class="sxs-lookup"><span data-stu-id="b5220-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="b5220-138">Ele se comunica com os seguintes Olá [pontos de extremidade de IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="b5220-138">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="b5220-139">*Gerenciamento de identidade do dispositivo* tooprovision e gerenciar dispositivos registrados com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b5220-139">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="b5220-140">*Receber o dispositivo para nuvem* para que você pode monitorar as mensagens enviadas do hub IoT de tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b5220-140">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="b5220-141">*Enviar a nuvem para dispositivo* para que você pode enviar mensagens tooyour dispositivos do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b5220-141">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="b5220-142">Configurar seu `IoT hub connection string` em toouse essa ferramenta todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="b5220-142">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="b5220-143">Gerenciador do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="b5220-143">IoT hub Explorer</span></span>
<span data-ttu-id="b5220-144">[Hub IoT Explorer](https://github.com/Azure/iothub-explorer) é uma ferramenta CLI em várias plataformas de exemplo toomanage clientes de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b5220-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="b5220-145">Você pode usar dispositivos de Olá Olá ferramenta toomanage no registro de identidade hello, monitorar mensagens de dispositivo para nuvem e enviar comandos de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b5220-145">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="b5220-146">tooinstall Olá versão (pré-lançamento) mais recente da ferramenta de Gerenciador de Hub IOT hello, executar Olá comandos em seu ambiente de linha de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5220-146">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="b5220-147">Você pode usar Olá Olá de tooget obter ajuda adicional sobre todos os comandos do Gerenciador de Hub IOT e seus parâmetros de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b5220-147">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="b5220-148">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b5220-148">Azure portal</span></span>
<span data-ttu-id="b5220-149">Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b5220-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="b5220-150">Você também poderá Olá toouse [portal do Azure](../azure-portal-overview.md) toohelp provisionar, gerenciar e depurar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b5220-150">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="b5220-151">Problemas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b5220-151">Azure storage issues</span></span>
<span data-ttu-id="b5220-152">[Gerenciador de armazenamento do Microsoft Azure (visualização)](http://storageexplorer.com) é um aplicativo autônomo da Microsoft que você pode usar toowork com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="b5220-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="b5220-153">Usando essa ferramenta, você pode conectar-se a tabela de tooyour e ver dados hello.</span><span class="sxs-lookup"><span data-stu-id="b5220-153">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="b5220-154">Você pode usar essa ferramenta tootroubleshoot seus problemas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b5220-154">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md