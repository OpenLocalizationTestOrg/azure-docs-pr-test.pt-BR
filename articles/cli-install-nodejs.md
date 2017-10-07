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
# <a name="install-hello-azure-cli-10"></a>Instalar Olá 1.0 da CLI do Azure
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [CLI 1.0 do Azure](cli-install-nodejs.md)
> * [CLI 2.0 do Azure](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> Este tópico descreve como tooinstall hello Azure CLI 1.0, que se baseia no nodeJs e oferece suporte a todas as APIs de implantação clássico chama, bem como um grande número de atividades de implantação do Gerenciador de recursos. Você deve usar o hello [2.0 do CLI do Azure](/cli/azure/overview) para implantações de CLI novo ou intenções e gerenciamento.

Instale rapidamente Olá toouse de Interface de linha de comando do Azure (Azure CLI 1.0) um conjunto de código-fonte aberto com base no shell de comandos para criar e gerenciar recursos do Microsoft Azure. Você tem várias tooinstall de opções essas ferramentas de plataforma cruzada no seu computador:

* **pacote de NPM** - execução npm (Gerenciador de pacotes de saudação para JavaScript) tooinstall Olá pacote mais recente do Azure CLI 1.0 em seu sistema operacional ou distribuição de Linux. Exige o node.js e o npm em seu computador.
* **Installer** – Baixe um instalador para facilitar a instalação no Mac ou Windows.
* **Contêiner de docker** - começar a usar o hello CLI mais recente em um contêiner de Docker pronta para ser executada. Exige um host do Docker em seu computador.

Para obter mais opções e em segundo plano, consulte repositório do projeto de saudação em [GitHub](https://github.com/azure/azure-xplat-cli).

Depois de instalar hello Azure CLI 1.0, [conectá-lo com sua assinatura do Azure](xplat-cli-connect.md) e execução hello **azure** comandos de sua interface de linha de comando (Bash, Terminal, prompt de comando e assim por diante) toowork com os recursos do Azure.

## <a name="option-1-install-an-npm-package"></a>Opção 1: Instalar um pacote npm
tooinstall Olá CLI de um pacote de npm, verifique se você baixou e instalou Olá [mais recente Node. js e npm](https://nodejs.org/en/download/package-manager/). Em seguida, execute **de instalação de npm** pacote de cli do azure Olá tooinstall:

```bash
npm install -g azure-cli
```

Em distribuições do Linux, talvez seja necessário toouse **sudo** toosuccessfully executar Olá **npm** comando, da seguinte maneira:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> Se você precisa tooinstall ou atualizar Node. js e npm em seu sistema operacional ou distribuição de Linux, é recomendável que você instale Olá versão mais recente da LTS Node. js (4. x). Se você usar uma versão mais antiga, poderá obter erros de instalação.

Se preferir, baixe hello mais recente Linux [arquivo tar] [ linux-installer] para npm Olá pacote localmente. Em seguida, instale o pacote de npm baixado Olá da seguinte maneira (em distribuições do Linux, talvez seja necessário toouse **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Opção 2: Usar um instalador
Se você usar um computador Mac ou Windows, Olá instaladores CLI a seguir está disponível para download:

* [Instalador do Mac OS X][mac-installer]
* [Windows MSI][windows-installer]

> [!TIP]
> No Windows, você também pode baixar Olá [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall Olá CLI. Isso proporciona instalador Olá opção tooinstall adicionais do SDK do Azure e as ferramentas de linha de comando após a instalação Olá CLI.

## <a name="option-3-use-a-docker-container"></a>Opção 3: Usar um contêiner do Docker
Se você tiver configurado seu computador como um [Docker](https://docs.docker.com/engine/understanding-docker/) host, você pode executar Olá 1.0 de CLI do Azure mais recentes em um contêiner do Docker. Execução hello seguinte comando (em distribuições do Linux, talvez seja necessário toouse **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Executar comandos da CLI do Azure 1.0
Após hello Azure CLI 1.0 é instalado, execute Olá **azure** comando de sua interface de usuário de linha de comando (Bash, Terminal, prompt de comando e assim por diante). Por exemplo, o comando de Ajuda do toorun hello, digite o comando a seguir hello:

```azurecli
azure help
```

> [!NOTE]
> Em algumas distribuições do Linux, você pode receber um erro semelhante muito`/usr/bin/env: ‘node’: No such file or directory`. Esse erro ocorre quando instalações recentes do Node.js são instaladas em /usr/bin/nodejs. toofix, criar um link simbólico muito/usr/bin/nó executando este comando:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

versão de hello toosee de hello Azure CLI 1.0 é instalado, Olá tipo a seguir:

```azurecli
azure --version
```

Agora você está pronto! tooaccess todos os Olá CLI comandos toowork com seus próprios recursos, [conectar tooyour assinatura do Azure do hello CLI do Azure](xplat-cli-connect.md).

> [!NOTE]
> Quando você usa o CLI do Azure pela primeira vez, verá uma mensagem perguntando se você deseja tooallow informações de uso do Microsoft toocollect. A participação é voluntária. Se você escolher tooparticipate, você pode interromper a qualquer momento executando `azure telemetry --disable`. tooenable participação a qualquer momento, execute `azure telemetry --enable`.

## <a name="update-hello-cli"></a>Atualizar Olá CLI
Com frequência, a Microsoft lança versões atualizadas dos Olá CLI do Azure. Reinstalar Olá CLI usando o instalador de saudação para seu sistema operacional ou executar Olá contêiner de Docker mais recente. Ou, se você tiver hello Node. js e npm instalado mais recentes, atualizar, digitando o seguinte hello (em distribuições do Linux, talvez seja necessário toouse **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Ativar o recurso auto-completar com TAB
Há suporte para o recurso auto-completar de comandos da CLI para Mac e Linux.

tooenable no zsh, execute:

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable no bash, execute:

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Próximas etapas
* [Conectar-se de saudação CLI tooyour assinatura do Azure](xplat-cli-connect.md) toocreate e gerenciar recursos do Azure.
* toolearn mais sobre Olá CLI do Azure, baixar o código-fonte, relatar problemas, ou contribuir toohello projeto, visite Olá [repositório GitHub para Olá CLI do Azure](https://github.com/azure/azure-xplat-cli).
* Se você tiver dúvidas sobre como usar o hello CLI do Azure ou do Azure, visite Olá [fóruns do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
