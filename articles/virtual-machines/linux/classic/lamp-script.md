---
title: "aaaUse Olá a extensão CustomScript em uma VM do Linux | Microsoft Docs"
description: "Saiba como aplicativos de toodeploy toouse Olá CustomScript extensão em máquinas virtuais Linux no Azure criados usando o modelo de implantação clássico hello."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="66363-103">Implantar um aplicativo de LÂMPADA usando Olá extensão de CustomScript do Azure para Linux</span><span class="sxs-lookup"><span data-stu-id="66363-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="66363-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="66363-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="66363-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="66363-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="66363-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="66363-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="66363-107">Para obter informações sobre como implantar uma pilha LAMP usando o modelo do Gerenciador de recursos de hello, consulte [aqui](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66363-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="66363-108">Olá extensão de CustomScript do Microsoft Azure para Linux fornece uma maneira toocustomize suas máquinas virtuais (VMs) executando código arbitrário escrito em qualquer linguagem de script hello VM (por exemplo, Python e Bash) com suporte.</span><span class="sxs-lookup"><span data-stu-id="66363-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="66363-109">Isso fornece uma maneira muito flexível tooautomate máquinas de toomultiple de implantação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66363-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="66363-110">Você pode implantar Olá extensão CustomScript usando Olá portal do Azure, do Windows PowerShell ou hello Azure Interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="66363-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="66363-111">Neste artigo, que vamos usar Olá CLI do Azure toodeploy um tooan de aplicativo de LÂMPADA Ubuntu VM simple criado usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="66363-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66363-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="66363-112">Prerequisites</span></span>
<span data-ttu-id="66363-113">Para este exemplo, primeiro crie duas VMs do Azure executando o Ubuntu 14.04 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="66363-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="66363-114">Olá VMs são chamadas *script vm* e *vm de lâmpada*.</span><span class="sxs-lookup"><span data-stu-id="66363-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="66363-115">Quando você criar VMs hello, use nomes exclusivos.</span><span class="sxs-lookup"><span data-stu-id="66363-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="66363-116">Uma é usado toorun Olá CLI comandos e um é usado toodeploy Olá LÂMPADA aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66363-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="66363-117">Você também precisa de uma conta de armazenamento do Azure e uma chave tooaccess it (você pode obter isso de saudação portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="66363-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="66363-118">Se precisar de ajuda para criar VMs do Linux no Azure, consulte muito[criar uma máquina Virtual executando o Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="66363-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="66363-119">comandos de instalação de saudação pressupõem Ubuntu, mas você pode adaptar a instalação Olá para qualquer suporte a distribuição de Linux.</span><span class="sxs-lookup"><span data-stu-id="66363-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="66363-120">Olá script vm VM precisa toohave que CLI do Azure instalado, com um tooAzure de conexão do trabalho.</span><span class="sxs-lookup"><span data-stu-id="66363-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="66363-121">Para obter ajuda sobre isso, consulte muito[instalar e configurar Olá Interface de linha de comando do Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="66363-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="66363-122">Carregar um script</span><span class="sxs-lookup"><span data-stu-id="66363-122">Upload a script</span></span>
<span data-ttu-id="66363-123">Vamos usar Olá extensão CustomScript toorun um script em uma pilha de LÂMPADA Olá remota VM tooinstall e criar uma página do PHP.</span><span class="sxs-lookup"><span data-stu-id="66363-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="66363-124">No script de saudação tooaccess ordem de qualquer lugar, poderá carregá-lo como um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="66363-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="66363-125">Visão geral do script</span><span class="sxs-lookup"><span data-stu-id="66363-125">Script overview</span></span>
<span data-ttu-id="66363-126">exemplo de script Hello instala um tooUbuntu de pilha LAMP (incluindo a configuração de uma instalação silenciosa do MySQL), grava um arquivo simple do PHP e Apache é iniciado.</span><span class="sxs-lookup"><span data-stu-id="66363-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="66363-127">Carregar o script</span><span class="sxs-lookup"><span data-stu-id="66363-127">Upload script</span></span>
<span data-ttu-id="66363-128">Salve o script hello como um arquivo de texto, por exemplo *install_lamp.sh*e, em seguida, carregá-lo tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="66363-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="66363-129">Você pode fazer isso facilmente com o Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="66363-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="66363-130">Olá, exemplo a seguir carrega contêiner de armazenamento Olá arquivo tooa chamado "scripts".</span><span class="sxs-lookup"><span data-stu-id="66363-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="66363-131">Se contêiner Olá não existir, será necessário toocreate-lo primeiro.</span><span class="sxs-lookup"><span data-stu-id="66363-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="66363-132">Crie também um arquivo JSON que descreve como toodownload Olá script do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="66363-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="66363-133">Salvar como *public_config.json* (substituindo "mystorage" com o nome de saudação da sua conta de armazenamento):</span><span class="sxs-lookup"><span data-stu-id="66363-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="66363-134">Implantar a extensão de saudação</span><span class="sxs-lookup"><span data-stu-id="66363-134">Deploy hello extension</span></span>
<span data-ttu-id="66363-135">Agora você pode usar o hello próximo comando toodeploy Olá extensão de CustomScript Linux toohello remoto VM usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="66363-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="66363-136">comando anterior Olá baixa e executa Olá *install_lamp.sh* script hello VM chamada *vm de lâmpada*.</span><span class="sxs-lookup"><span data-stu-id="66363-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="66363-137">Desde que o aplicativo hello inclui um servidor web, lembre-se tooopen um HTTP de porta de escuta em Olá VM remoto com o próximo comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="66363-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="66363-138">Monitoramento e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="66363-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="66363-139">Você pode verificar como execuções de script personalizado Olá examinando o arquivo de log de saudação Olá VM remoto.</span><span class="sxs-lookup"><span data-stu-id="66363-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="66363-140">SSH muito*vm de lâmpada* e arquivo de log final Olá com o próximo comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="66363-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="66363-141">Depois de executar Olá extensão CustomScript, você pode procurar a página do PHP toohello criado para obter informações.</span><span class="sxs-lookup"><span data-stu-id="66363-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="66363-142">Olá PHP página exemplo hello neste artigo é *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="66363-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66363-143">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="66363-143">Additional resources</span></span>
<span data-ttu-id="66363-144">Você pode usar o mesmo toodeploy de etapas básicas de hello aplicativos mais complexos.</span><span class="sxs-lookup"><span data-stu-id="66363-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="66363-145">Neste exemplo, o script de instalação Olá foi salvo como um blob público no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="66363-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="66363-146">Uma opção mais segura seria o script de instalação Olá toostore como um blob seguro com um [assinatura de acesso seguro](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="66363-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="66363-147">Recursos adicionais para a CLI do Azure, Linux e hello extensão CustomScript são listados a seguir.</span><span class="sxs-lookup"><span data-stu-id="66363-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="66363-148">Automatizar tarefas de personalização de VM do Linux usando a extensão CustomScript</span><span class="sxs-lookup"><span data-stu-id="66363-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="66363-149">Extensões Linux do Azure (GitHub)</span><span class="sxs-lookup"><span data-stu-id="66363-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)