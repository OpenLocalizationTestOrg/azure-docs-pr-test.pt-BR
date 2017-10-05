---
title: "Implantar a LAMP em uma máquina virtual Linux com a CLI do Azure 1.0 | Microsoft Docs"
description: Saiba como instalar a pilha LAMP em uma VM Linux no Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: feba2fb20d1831e92358ff5d1b4c9589d63d28dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-with-the-azure-cli-10"></a><span data-ttu-id="e1cef-103">Implantar a pilha LAMP com a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e1cef-103">Deploy LAMP stack with the Azure CLI 1.0</span></span>
<span data-ttu-id="e1cef-104">Este artigo explica como implantar um servidor Web Apache, MySQL e PHP (a pilha LAMP) no Azure.</span><span class="sxs-lookup"><span data-stu-id="e1cef-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="e1cef-105">Você precisa de uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)) e da [CLI do Azure](../../cli-install-nodejs.md) que esteja [conectada à sua conta do Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e1cef-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI](../../cli-install-nodejs.md) that is [connected to your Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e1cef-106">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="e1cef-106">CLI versions to complete the task</span></span>
<span data-ttu-id="e1cef-107">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="e1cef-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="e1cef-108">[CLI do Azure 1.0] – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="e1cef-108">[Azure CLI 1.0] – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e1cef-109">[CLI 2.0 do Azure](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="e1cef-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

```
# One command to create a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="e1cef-110">Implantar LAMP em VM existente</span><span class="sxs-lookup"><span data-stu-id="e1cef-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, the other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="e1cef-111">Passo a passo da implantação da LAMP em uma nova VM</span><span class="sxs-lookup"><span data-stu-id="e1cef-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="e1cef-112">Você pode começar criando um [grupo de recursos](../../azure-resource-manager/resource-group-overview.md) que conterá a nova VM:</span><span class="sxs-lookup"><span data-stu-id="e1cef-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain the new VM:</span></span>

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

<span data-ttu-id="e1cef-113">Para criar a própria VM, você pode usar um modelo do Azure Resource Manager já escrito encontrado [aqui no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="e1cef-113">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="e1cef-114">Você deverá ver uma resposta solicitando mais algumas entradas:</span><span class="sxs-lookup"><span data-stu-id="e1cef-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment to complete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

<span data-ttu-id="e1cef-115">Agora você criou uma VM Linux com LAMP já instalada.</span><span class="sxs-lookup"><span data-stu-id="e1cef-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="e1cef-116">Se quiser, você poderá verificar a instalação indo até [Verificar se a LAMP foi instalada com êxito](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="e1cef-116">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="e1cef-117">Passo a passo da implantação da LAMP em uma VM existente</span><span class="sxs-lookup"><span data-stu-id="e1cef-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="e1cef-118">Se você precisar de ajuda para criar uma VM Linux, clique [aqui para saber como criá-la](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1cef-118">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e1cef-119">Em seguida, você precisará usar o SSH na VM Linux.</span><span class="sxs-lookup"><span data-stu-id="e1cef-119">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="e1cef-120">Se você precisar de ajuda para criar uma chave SSH, clique [aqui para saber como criá-la no Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1cef-120">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="e1cef-121">Se você já tiver uma chave SSH, prossiga e use o SSH na linha de comando da sua VM Linux com `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="e1cef-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="e1cef-122">Agora que você está trabalhando na VM Linux, podemos detalhar a instalação da pilha LAMP em distribuições baseadas em Debian.</span><span class="sxs-lookup"><span data-stu-id="e1cef-122">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="e1cef-123">Os comandos exatos podem ser diferentes para outras distribuições de Linux.</span><span class="sxs-lookup"><span data-stu-id="e1cef-123">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="e1cef-124">Instalação no Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e1cef-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="e1cef-125">Você precisa dos seguintes pacotes instalados: `apache2`, `mysql-server`, `php5` e `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="e1cef-125">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="e1cef-126">Você pode instalá-los pegando esses pacotes diretamente ou usando Tasksel.</span><span class="sxs-lookup"><span data-stu-id="e1cef-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="e1cef-127">As instruções para as duas opções estão listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="e1cef-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="e1cef-128">Antes de instalar, você precisa baixar e atualizar as listas de pacotes.</span><span class="sxs-lookup"><span data-stu-id="e1cef-128">Before installing you need to download and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="e1cef-129">Pacotes individuais</span><span class="sxs-lookup"><span data-stu-id="e1cef-129">Individual packages</span></span>
<span data-ttu-id="e1cef-130">Como usar apt-get:</span><span class="sxs-lookup"><span data-stu-id="e1cef-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="e1cef-131">Usando o Tasksel</span><span class="sxs-lookup"><span data-stu-id="e1cef-131">Using tasksel</span></span>
<span data-ttu-id="e1cef-132">Como alternativa, você pode baixar o Tasksel, uma ferramenta do Debian/Ubuntu que instala vários pacotes relacionados como uma “tarefa” coordenada em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="e1cef-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="e1cef-133">Após executar uma das opções anteriores, você receberá uma solicitação para instalar esses pacotes e várias outras dependências.</span><span class="sxs-lookup"><span data-stu-id="e1cef-133">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="e1cef-134">Pressione 'y' e depois 'ENTER' para continuar e siga todas as solicitações para definir uma senha administrativa para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e1cef-134">Press 'y' and then 'Enter' to continue, and follow any other prompts to set an administrative password for MySQL.</span></span> <span data-ttu-id="e1cef-135">Essa ação instala as extensões PHP mínimas obrigatórias necessárias para usar o PHP com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="e1cef-135">This installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="e1cef-136">Execute o comando a seguir para ver outras extensões PHP que estão disponíveis em pacotes:</span><span class="sxs-lookup"><span data-stu-id="e1cef-136">Run the following command to see other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="e1cef-137">Criar documento info.php</span><span class="sxs-lookup"><span data-stu-id="e1cef-137">Create info.php document</span></span>
<span data-ttu-id="e1cef-138">Agora você deve ser capaz de verificar qual versão do Apache, MySQL e PHP você tem por meio da linha de comando digitando `apache2 -v`, `mysql -v` ou `php -v`.</span><span class="sxs-lookup"><span data-stu-id="e1cef-138">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="e1cef-139">Se você quiser realizar mais testes, crie uma página de informações rápida de PHP para exibição em um navegador.</span><span class="sxs-lookup"><span data-stu-id="e1cef-139">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="e1cef-140">Crie um arquivo com o editor de texto Nano usando este comando:</span><span class="sxs-lookup"><span data-stu-id="e1cef-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="e1cef-141">No editor de texto Nano GNU, adicione as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="e1cef-141">Within the GNU Nano text editor, add the following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="e1cef-142">Salve e saia do editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e1cef-142">Then save and exit the text editor.</span></span>

<span data-ttu-id="e1cef-143">Reinicie o Apache com este comando para que todas as novas instalações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="e1cef-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="e1cef-144">Verifique se a LAMP foi instalada com êxito</span><span class="sxs-lookup"><span data-stu-id="e1cef-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="e1cef-145">Agora é possível verificar a página de informações do PHP que você criou abrindo um navegador e acessando http://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="e1cef-145">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="e1cef-146">A página deve ser semelhante a esta imagem.</span><span class="sxs-lookup"><span data-stu-id="e1cef-146">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="e1cef-147">Você pode verificar a instalação do Apache exibindo a Página Padrão do Apache2 Ubuntu acessando http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="e1cef-147">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="e1cef-148">Você deverá ver algo parecido com esta imagem.</span><span class="sxs-lookup"><span data-stu-id="e1cef-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="e1cef-149">Parabéns, você instalou uma pilha LAMP em sua VM do Azure!</span><span class="sxs-lookup"><span data-stu-id="e1cef-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1cef-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1cef-150">Next steps</span></span>
<span data-ttu-id="e1cef-151">Consulte a documentação do Ubuntu sobre a pilha LAMP:</span><span class="sxs-lookup"><span data-stu-id="e1cef-151">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="e1cef-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="e1cef-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png