---
title: Instalar a CLI do Azure 1.0 | Microsoft Docs
description: "Instalar a CLI do Azure 1.0 para Mac, Linux e Windows para começar a usar os serviços do Azure"
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
ms.openlocfilehash: 63b35ed25b809a16b61b685fd35aa67474b0a369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-cli-10"></a><span data-ttu-id="1fc6f-103">Instalar a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1fc6f-103">Install the Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fc6f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fc6f-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="1fc6f-105">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="1fc6f-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="1fc6f-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="1fc6f-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="1fc6f-107">Este tópico descreve como instalar a CLI do Azure 1.0, que se baseia no nodeJs e dá suporte a todas as chamadas à API de implantação clássica, bem como uma variedade de atividades de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-107">This topic describes how to install the Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="1fc6f-108">É necessário usar a [CLI do Azure 2.0](/cli/azure/overview) para implantações e gerenciamento novos ou prospectivos da CLI.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-108">You should use the [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="1fc6f-109">Instale rapidamente a CLI (Interface de Linha de Comando) do Azure 1.0 para usar um conjunto de comandos de software livre baseados em shell para criar e gerenciar recursos no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="1fc6f-110">Você tem várias opções para instalar essas ferramentas de plataforma cruzada em seu computador:</span><span class="sxs-lookup"><span data-stu-id="1fc6f-110">You have several options to install these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="1fc6f-111">**pacote npm** – Execute o npm (o gerenciador de pacotes para JavaScript) para instalar o último pacote da CLI do Azure 1.0 na distribuição Linux ou no sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="1fc6f-112">Exige o node.js e o npm em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="1fc6f-113">**Installer** – Baixe um instalador para facilitar a instalação no Mac ou Windows.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="1fc6f-114">**Contêiner do Docker** – Comece a usar a CLI mais recente em um contêiner do Docker pronto para ser executado.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="1fc6f-115">Exige um host do Docker em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="1fc6f-116">Para obter mais opções e um histórico, consulte o repositório do projeto no [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="1fc6f-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="1fc6f-117">Depois que a CLI do Azure 1.0 for instalada, [conecte-a à sua assinatura do Azure](xplat-cli-connect.md) e execute os comandos **azure** na interface de linha de comando (Bash, Terminal, Prompt de comando e assim por diante) para trabalhar com os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="1fc6f-118">Opção 1: Instalar um pacote npm</span><span class="sxs-lookup"><span data-stu-id="1fc6f-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="1fc6f-119">Para instalar a CLI de um pacote npm, você precisa baixar e instalar os [Node.js e o npm mais recentes](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="1fc6f-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="1fc6f-120">Em seguida, execute **npm install** para instalar o pacote azure-cli:</span><span class="sxs-lookup"><span data-stu-id="1fc6f-120">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="1fc6f-121">Em distribuições Linux, talvez você precise usar **sudo** para executar o comando **npm** com êxito, como segue:</span><span class="sxs-lookup"><span data-stu-id="1fc6f-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="1fc6f-122">Se precisar instalar ou atualizar o Node.js e o npm em sua distribuição ou SO do Linux, é recomendável que você instale a versão mais recente do Node.js LTS (4. x).</span><span class="sxs-lookup"><span data-stu-id="1fc6f-122">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="1fc6f-123">Se você usar uma versão mais antiga, poderá obter erros de instalação.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="1fc6f-124">Se preferir, baixe o [arquivo tar][linux-installer] do Linux mais recente para o pacote npm localmente.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span></span> <span data-ttu-id="1fc6f-125">Em seguida, instale o pacote npm baixado da seguinte maneira (em distribuições Linux, talvez seja necessário usar **sudo**):</span><span class="sxs-lookup"><span data-stu-id="1fc6f-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span></span>

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="1fc6f-126">Opção 2: Usar um instalador</span><span class="sxs-lookup"><span data-stu-id="1fc6f-126">Option 2: Use an installer</span></span>
<span data-ttu-id="1fc6f-127">Se você usar um computador com Windows ou Mac, os instaladores de CLI a seguir estarão disponíveis para download:</span><span class="sxs-lookup"><span data-stu-id="1fc6f-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span></span>

* <span data-ttu-id="1fc6f-128">[Instalador do Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="1fc6f-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="1fc6f-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="1fc6f-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="1fc6f-130">No Windows, você também pode baixar o [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) para instalar a CLI.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-130">On Windows, you can also download the [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) to install the CLI.</span></span> <span data-ttu-id="1fc6f-131">Esse instalador lhe dá a opção de instalar o SDK do Azure e ferramentas de linha de comando adicionais após a instalação da CLI.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-131">This installer gives you the option to install additional Azure SDK and command-line tools after installing the CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="1fc6f-132">Opção 3: Usar um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="1fc6f-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="1fc6f-133">Se você tiver configurado o computador como um host do [Docker](https://docs.docker.com/engine/understanding-docker/), poderá executar a última CLI do Azure 1.0 em um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="1fc6f-134">Execute o seguinte comando (em distribuições Linux, talvez você precise usar **sudo**):</span><span class="sxs-lookup"><span data-stu-id="1fc6f-134">Run the following command (on Linux distributions you might need to use **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="1fc6f-135">Executar comandos da CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1fc6f-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="1fc6f-136">Depois que a CLI do Azure 1.0 for instalada, execute o comando **azure** na interface do usuário de linha de comando (Bash, Terminal, Prompt de comando e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="1fc6f-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="1fc6f-137">Por exemplo, para executar o comando de ajuda, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1fc6f-137">For example, to run the help command, type the following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="1fc6f-138">Em algumas distribuições Linux, você poderá receber um erro semelhante a `/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-138">On some Linux distributions, you may receive an error similar to `/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="1fc6f-139">Esse erro ocorre quando instalações recentes do Node.js são instaladas em /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="1fc6f-140">Para corrigi-lo, crie um link simbólico para /usr/bin/node executando este comando:</span><span class="sxs-lookup"><span data-stu-id="1fc6f-140">To fix it, create a symbolic link to /usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="1fc6f-141">Para ver a versão da CLI do Azure 1.0 instalada, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1fc6f-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="1fc6f-142">Agora você está pronto!</span><span class="sxs-lookup"><span data-stu-id="1fc6f-142">Now you are ready!</span></span> <span data-ttu-id="1fc6f-143">Para acessar todos os comandos da CLI para trabalhar com seus próprios recursos, [conecte-se à sua assinatura do Azure por meio da CLI do Azure](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="1fc6f-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1fc6f-144">Ao usar a CLI do Azure pela primeira vez, você verá uma mensagem perguntando se deseja permitir que a Microsoft colete informações de uso.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-144">When you first use Azure CLI, you see a message asking if you want to allow Microsoft to collect usage information.</span></span> <span data-ttu-id="1fc6f-145">A participação é voluntária.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-145">Participation is voluntary.</span></span> <span data-ttu-id="1fc6f-146">Se optar por participar, você poderá parar a qualquer momento executando `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-146">If you choose to participate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="1fc6f-147">Para habilitar a participação a qualquer momento, execute `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-147">To enable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-the-cli"></a><span data-ttu-id="1fc6f-148">Atualizar a CLI</span><span class="sxs-lookup"><span data-stu-id="1fc6f-148">Update the CLI</span></span>
<span data-ttu-id="1fc6f-149">Com frequência, a Microsoft lança versões atualizadas da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-149">Microsoft frequently releases updated versions of the Azure CLI.</span></span> <span data-ttu-id="1fc6f-150">Reinstale a CLI usando o instalador do seu sistema operacional ou execute o contêiner do Docker mais recente.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span></span> <span data-ttu-id="1fc6f-151">Ou, se tiver o Node.js e o npm mais recentes instalados, atualize-os digitando o seguinte (em distribuições Linux, talvez você precise usar **sudo**).</span><span class="sxs-lookup"><span data-stu-id="1fc6f-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="1fc6f-152">Ativar o recurso auto-completar com TAB</span><span class="sxs-lookup"><span data-stu-id="1fc6f-152">Enable tab completion</span></span>
<span data-ttu-id="1fc6f-153">Há suporte para o recurso auto-completar de comandos da CLI para Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="1fc6f-154">Para habilitá-lo no zsh, execute:</span><span class="sxs-lookup"><span data-stu-id="1fc6f-154">To enable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="1fc6f-155">Para habilitá-lo no bash, execute:</span><span class="sxs-lookup"><span data-stu-id="1fc6f-155">To enable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="1fc6f-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1fc6f-156">Next steps</span></span>
* <span data-ttu-id="1fc6f-157">[Conecte-se da CLI à sua assinatura do Azure](xplat-cli-connect.md) para criar e gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc6f-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span></span>
* <span data-ttu-id="1fc6f-158">Para saber mais sobre a CLI do Azure, baixar o código-fonte, relatar problemas ou colaborar com o projeto, visite o [Repositório GitHub para a CLI do Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="1fc6f-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="1fc6f-159">Se tiver dúvidas quanto ao uso da CLI do Azure ou do Azure, visite os [Fóruns do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="1fc6f-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
