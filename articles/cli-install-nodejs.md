---
title: "Olá aaaInstall 1.0 da CLI do Azure | Microsoft Docs"
description: "Instalar hello Azure CLI 1.0 para Windows, Linux e Mac toostart usando os serviços do Azure"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="bb4f7-103">Instalar Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bb4f7-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb4f7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb4f7-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="bb4f7-105">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="bb4f7-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="bb4f7-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="bb4f7-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="bb4f7-107">Este tópico descreve como tooinstall hello Azure CLI 1.0, que se baseia no nodeJs e oferece suporte a todas as APIs de implantação clássico chama, bem como um grande número de atividades de implantação do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="bb4f7-108">Você deve usar o hello [2.0 do CLI do Azure](/cli/azure/overview) para implantações de CLI novo ou intenções e gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="bb4f7-109">Instale rapidamente Olá toouse de Interface de linha de comando do Azure (Azure CLI 1.0) um conjunto de código-fonte aberto com base no shell de comandos para criar e gerenciar recursos do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="bb4f7-110">Você tem várias tooinstall de opções essas ferramentas de plataforma cruzada no seu computador:</span><span class="sxs-lookup"><span data-stu-id="bb4f7-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="bb4f7-111">**pacote de NPM** - execução npm (Gerenciador de pacotes de saudação para JavaScript) tooinstall Olá pacote mais recente do Azure CLI 1.0 em seu sistema operacional ou distribuição de Linux.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="bb4f7-112">Exige o node.js e o npm em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="bb4f7-113">**Installer** – Baixe um instalador para facilitar a instalação no Mac ou Windows.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="bb4f7-114">**Contêiner de docker** - começar a usar o hello CLI mais recente em um contêiner de Docker pronta para ser executada.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="bb4f7-115">Exige um host do Docker em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="bb4f7-116">Para obter mais opções e em segundo plano, consulte repositório do projeto de saudação em [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="bb4f7-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="bb4f7-117">Depois de instalar hello Azure CLI 1.0, [conectá-lo com sua assinatura do Azure](xplat-cli-connect.md) e execução hello **azure** comandos de sua interface de linha de comando (Bash, Terminal, prompt de comando e assim por diante) toowork com os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="bb4f7-118">Opção 1: Instalar um pacote npm</span><span class="sxs-lookup"><span data-stu-id="bb4f7-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="bb4f7-119">tooinstall Olá CLI de um pacote de npm, verifique se você baixou e instalou Olá [mais recente Node. js e npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="bb4f7-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="bb4f7-120">Em seguida, execute **de instalação de npm** pacote de cli do azure Olá tooinstall:</span><span class="sxs-lookup"><span data-stu-id="bb4f7-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="bb4f7-121">Em distribuições do Linux, talvez seja necessário toouse **sudo** toosuccessfully executar Olá **npm** comando, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bb4f7-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="bb4f7-122">Se você precisa tooinstall ou atualizar Node. js e npm em seu sistema operacional ou distribuição de Linux, é recomendável que você instale Olá versão mais recente da LTS Node. js (4. x).</span><span class="sxs-lookup"><span data-stu-id="bb4f7-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="bb4f7-123">Se você usar uma versão mais antiga, poderá obter erros de instalação.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="bb4f7-124">Se preferir, baixe hello mais recente Linux [arquivo tar] [ linux-installer] para npm Olá pacote localmente.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="bb4f7-125">Em seguida, instale o pacote de npm baixado Olá da seguinte maneira (em distribuições do Linux, talvez seja necessário toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="bb4f7-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="bb4f7-126">Opção 2: Usar um instalador</span><span class="sxs-lookup"><span data-stu-id="bb4f7-126">Option 2: Use an installer</span></span>
<span data-ttu-id="bb4f7-127">Se você usar um computador Mac ou Windows, Olá instaladores CLI a seguir está disponível para download:</span><span class="sxs-lookup"><span data-stu-id="bb4f7-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="bb4f7-128">[Instalador do Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="bb4f7-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="bb4f7-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="bb4f7-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="bb4f7-130">No Windows, você também pode baixar Olá [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall Olá CLI.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="bb4f7-131">Isso proporciona instalador Olá opção tooinstall adicionais do SDK do Azure e as ferramentas de linha de comando após a instalação Olá CLI.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="bb4f7-132">Opção 3: Usar um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="bb4f7-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="bb4f7-133">Se você tiver configurado seu computador como um [Docker](https://docs.docker.com/engine/understanding-docker/) host, você pode executar Olá 1.0 de CLI do Azure mais recentes em um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="bb4f7-134">Execução hello seguinte comando (em distribuições do Linux, talvez seja necessário toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="bb4f7-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="bb4f7-135">Executar comandos da CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bb4f7-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="bb4f7-136">Após hello Azure CLI 1.0 é instalado, execute Olá **azure** comando de sua interface de usuário de linha de comando (Bash, Terminal, prompt de comando e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="bb4f7-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="bb4f7-137">Por exemplo, o comando de Ajuda do toorun hello, digite o comando a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="bb4f7-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="bb4f7-138">Em algumas distribuições do Linux, você pode receber um erro semelhante muito`/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="bb4f7-139">Esse erro ocorre quando instalações recentes do Node.js são instaladas em /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="bb4f7-140">toofix, criar um link simbólico muito/usr/bin/nó executando este comando:</span><span class="sxs-lookup"><span data-stu-id="bb4f7-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="bb4f7-141">versão de hello toosee de hello Azure CLI 1.0 é instalado, Olá tipo a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb4f7-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="bb4f7-142">Agora você está pronto!</span><span class="sxs-lookup"><span data-stu-id="bb4f7-142">Now you are ready!</span></span> <span data-ttu-id="bb4f7-143">tooaccess todos os Olá CLI comandos toowork com seus próprios recursos, [conectar tooyour assinatura do Azure do hello CLI do Azure](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="bb4f7-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bb4f7-144">Quando você usa o CLI do Azure pela primeira vez, verá uma mensagem perguntando se você deseja tooallow informações de uso do Microsoft toocollect.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="bb4f7-145">A participação é voluntária.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-145">Participation is voluntary.</span></span> <span data-ttu-id="bb4f7-146">Se você escolher tooparticipate, você pode interromper a qualquer momento executando `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="bb4f7-147">tooenable participação a qualquer momento, execute `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="bb4f7-148">Atualizar Olá CLI</span><span class="sxs-lookup"><span data-stu-id="bb4f7-148">Update hello CLI</span></span>
<span data-ttu-id="bb4f7-149">Com frequência, a Microsoft lança versões atualizadas dos Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="bb4f7-150">Reinstalar Olá CLI usando o instalador de saudação para seu sistema operacional ou executar Olá contêiner de Docker mais recente.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="bb4f7-151">Ou, se você tiver hello Node. js e npm instalado mais recentes, atualizar, digitando o seguinte hello (em distribuições do Linux, talvez seja necessário toouse **sudo**).</span><span class="sxs-lookup"><span data-stu-id="bb4f7-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="bb4f7-152">Ativar o recurso auto-completar com TAB</span><span class="sxs-lookup"><span data-stu-id="bb4f7-152">Enable tab completion</span></span>
<span data-ttu-id="bb4f7-153">Há suporte para o recurso auto-completar de comandos da CLI para Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="bb4f7-154">tooenable no zsh, execute:</span><span class="sxs-lookup"><span data-stu-id="bb4f7-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="bb4f7-155">tooenable no bash, execute:</span><span class="sxs-lookup"><span data-stu-id="bb4f7-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="bb4f7-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb4f7-156">Next steps</span></span>
* <span data-ttu-id="bb4f7-157">[Conectar-se de saudação CLI tooyour assinatura do Azure](xplat-cli-connect.md) toocreate e gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb4f7-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="bb4f7-158">toolearn mais sobre Olá CLI do Azure, baixar o código-fonte, relatar problemas, ou contribuir toohello projeto, visite Olá [repositório GitHub para Olá CLI do Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="bb4f7-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="bb4f7-159">Se você tiver dúvidas sobre como usar o hello CLI do Azure ou do Azure, visite Olá [fóruns do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="bb4f7-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
