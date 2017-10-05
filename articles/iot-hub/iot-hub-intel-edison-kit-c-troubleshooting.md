---
title: "Conectar o Intel Edison (C) ao IoT do Azure - Solução de problemas | Microsoft Docs"
description: "Página de solução de problemas da experiência do Intel Edison C"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "solução de problemas do arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dd6338ad29e0bb858c33e5bb24b8f41d3c22575a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="e42f1-104">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e42f1-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="e42f1-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="e42f1-105">Hardware issues</span></span>
<span data-ttu-id="e42f1-106">Para obter informações sobre como resolver problemas comuns no Intel Edison, consulte a [página oficial de solução de problemas](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="e42f1-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="e42f1-107">Problemas do pacote de Node.js</span><span class="sxs-lookup"><span data-stu-id="e42f1-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="e42f1-108">Sem resposta durante as tarefas de gulp</span><span class="sxs-lookup"><span data-stu-id="e42f1-108">No response during gulp tasks</span></span>
<span data-ttu-id="e42f1-109">Se você encontrar problemas ao executar tarefas de gulp, será possível adicionar a opção `--verbose` para depuração.</span><span class="sxs-lookup"><span data-stu-id="e42f1-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="e42f1-110">Tente finalizar as tarefas de gulp atuais usando `Ctrl + C` e, em seguida, execute o seguinte comando na janela do console para ver mensagens de depuração.</span><span class="sxs-lookup"><span data-stu-id="e42f1-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="e42f1-111">Você pode ver mensagens de erro detalhadas em sua saída do console.</span><span class="sxs-lookup"><span data-stu-id="e42f1-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="e42f1-112">Problemas de NPM</span><span class="sxs-lookup"><span data-stu-id="e42f1-112">NPM issues</span></span>
<span data-ttu-id="e42f1-113">Tente atualizar o pacote NPM com o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e42f1-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="e42f1-114">Se o problema persistir, deixe seus comentários no final deste artigo ou crie um problema do GitHub em nosso [repositório de exemplo][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="e42f1-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="e42f1-115">Problemas da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e42f1-115">Azure-CLI issues</span></span>
<span data-ttu-id="e42f1-116">A interface de linha de comando do Azure (CLI do Azure) é uma compilação de visualização.</span><span class="sxs-lookup"><span data-stu-id="e42f1-116">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="e42f1-117">Procure pela solução no [Guia de Instalação de Visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) para buscar soluções.</span><span class="sxs-lookup"><span data-stu-id="e42f1-117">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="e42f1-118">Tente atualizar a CLI do Azure para a versão mais recente quando comandos não funcionarem conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="e42f1-118">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="e42f1-119">Se você encontrar erros com a ferramenta, emita um [problema](https://github.com/Azure/azure-cli/issues) na seção **problemas** do repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="e42f1-119">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="e42f1-120">Para obter ajuda para solucionar problemas comuns, consulte o [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="e42f1-120">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="e42f1-121">Se você receber a mensagem “Não foi possível localizar uma versão que atenda ao requisito”, execute o seguinte comando para atualizar o pip para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="e42f1-121">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="e42f1-122">Problemas de instalação do Python</span><span class="sxs-lookup"><span data-stu-id="e42f1-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="e42f1-123">Problemas de instalação herdada (macOS)</span><span class="sxs-lookup"><span data-stu-id="e42f1-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="e42f1-124">Ao instalar o **pip**, um erro de permissão será lançado quando houver pacotes mais antigos instalados com permissões **su**.</span><span class="sxs-lookup"><span data-stu-id="e42f1-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="e42f1-125">Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada.</span><span class="sxs-lookup"><span data-stu-id="e42f1-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="e42f1-126">Alguns pacotes do **pip** de uma instalação anterior foram criados pela raiz, o que causa o erro de permissão.</span><span class="sxs-lookup"><span data-stu-id="e42f1-126">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="e42f1-127">A solução é remover os pacotes instalados pela raiz.</span><span class="sxs-lookup"><span data-stu-id="e42f1-127">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="e42f1-128">Use as etapas a seguir para concluir esta tarefa:</span><span class="sxs-lookup"><span data-stu-id="e42f1-128">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="e42f1-129">Acesse: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="e42f1-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="e42f1-130">Listar pacotes criados por raiz: `ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="e42f1-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="e42f1-131">Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="e42f1-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="e42f1-132">Reinstale o Python.</span><span class="sxs-lookup"><span data-stu-id="e42f1-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="e42f1-133">Problemas do Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="e42f1-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="e42f1-134">Se você tiver provisionado com êxito o Hub IoT do Azure com `azure-cli` e precisar de uma ferramenta para gerenciar os dispositivos conectados ao seu Hub IoT, experimente usar as seguintes ferramentas:</span><span class="sxs-lookup"><span data-stu-id="e42f1-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="e42f1-135">Gerenciador de Dispositivos</span><span class="sxs-lookup"><span data-stu-id="e42f1-135">Device Explorer</span></span>
<span data-ttu-id="e42f1-136">O [Gerenciador de Dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) é executado no computador local do Windows e se conecta ao seu hub IoT no Azure.</span><span class="sxs-lookup"><span data-stu-id="e42f1-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="e42f1-137">Ele se comunica com os seguintes [pontos de extremidade de Hub IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="e42f1-137">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="e42f1-138">_Gerenciamento de identidade do dispositivo_ para provisionar e gerenciar dispositivos registrados com seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e42f1-138">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="e42f1-139">_Receber do dispositivo para nuvem_ para que você possa monitorar as mensagens enviadas de seu dispositivo ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e42f1-139">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="e42f1-140">_Enviar do dispositivo para nuvem_ para que você possa enviar mensagens para seus dispositivos de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e42f1-140">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="e42f1-141">Configure o `IoT hub connection string` dentro desta ferramenta para usar todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="e42f1-141">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="e42f1-142">Gerenciador do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="e42f1-142">IoT hub Explorer</span></span>
<span data-ttu-id="e42f1-143">O [Gerenciador do Hub IoT](https://github.com/Azure/iothub-explorer) é uma ferramenta de CLI de várias plataformas de exemplo para gerenciar clientes de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e42f1-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="e42f1-144">Use a ferramenta para gerenciar os dispositivos no registro de identidade, monitorar mensagens de dispositivo para a nuvem e enviar comandos de nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e42f1-144">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="e42f1-145">Para instalar a versão mais recente (pré-lançamento) da ferramenta Gerenciador do iothub, execute o comando a seguir em seu ambiente de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="e42f1-145">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="e42f1-146">Você pode usar o comando a seguir para obter ajuda adicional sobre todos os comandos do Gerenciador do iothub e seus parâmetros:</span><span class="sxs-lookup"><span data-stu-id="e42f1-146">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="e42f1-147">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e42f1-147">Azure portal</span></span>
<span data-ttu-id="e42f1-148">Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e42f1-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="e42f1-149">Você também poderá usar o [portal do Azure](../azure-portal-overview.md) para ajudar a provisionar, gerenciar e depurar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e42f1-149">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="e42f1-150">Problemas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e42f1-150">Azure storage issues</span></span>
<span data-ttu-id="e42f1-151">[O Gerenciador de Armazenamento do Microsoft Azure (visualização)](http://storageexplorer.com) é um aplicativo autônomo da Microsoft que pode ser usado para trabalhar com os dados do [Armazenamento do Azure](https://azure.microsoft.com/en-us/services/storage/) no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="e42f1-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="e42f1-152">Com essa ferramenta você pode se conectar à sua tabela e ver os dados contidos nela.</span><span class="sxs-lookup"><span data-stu-id="e42f1-152">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="e42f1-153">Você pode usar essa ferramenta para solucionar seus problemas de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e42f1-153">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e42f1-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e42f1-154">Next steps</span></span>
<span data-ttu-id="e42f1-155">Esta página inclui apenas os problemas mais comuns do kit Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="e42f1-155">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="e42f1-156">Você também pode deixar comentários na parte inferior para relatar problemas para solução de problemas no futuro.</span><span class="sxs-lookup"><span data-stu-id="e42f1-156">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="e42f1-157">Voltar para [Introdução ao Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e42f1-157">Go back to [Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started