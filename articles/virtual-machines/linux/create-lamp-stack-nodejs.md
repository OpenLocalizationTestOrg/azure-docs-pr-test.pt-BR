---
title: "aaaDeploy LÂMPADA em uma máquina virtual Linux Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como tooinstall Olá LÂMPADA de pilha em uma VM do Linux no Azure"
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
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="e5586-103">Implantar a pilha LAMP com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e5586-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="e5586-104">Este artigo o orienta como toodeploy um Apache web server, MySQL e PHP (pilha de LÂMPADA Olá) no Azure.</span><span class="sxs-lookup"><span data-stu-id="e5586-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="e5586-105">Você precisa de uma conta do Azure ([obter uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)) e hello [CLI do Azure](../../cli-install-nodejs.md) que é [conectado tooyour conta do Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e5586-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e5586-106">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="e5586-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e5586-107">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5586-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e5586-108">[Azure CLI 1.0] – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="e5586-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e5586-109">[2.0 do CLI do Azure](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="e5586-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="e5586-110">Implantar LAMP em VM existente</span><span class="sxs-lookup"><span data-stu-id="e5586-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="e5586-111">Passo a passo da implantação da LAMP em uma nova VM</span><span class="sxs-lookup"><span data-stu-id="e5586-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="e5586-112">Você pode começar criando um [grupo de recursos](../../azure-resource-manager/resource-group-overview.md) que irá conter Olá nova VM:</span><span class="sxs-lookup"><span data-stu-id="e5586-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

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

<span data-ttu-id="e5586-113">toocreate Olá própria máquina virtual, você pode usar um modelo do Azure Resource Manager já escrito encontrado [aqui no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="e5586-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="e5586-114">Você deverá ver uma resposta solicitando mais algumas entradas:</span><span class="sxs-lookup"><span data-stu-id="e5586-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
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

<span data-ttu-id="e5586-115">Agora você criou uma VM Linux com LAMP já instalada.</span><span class="sxs-lookup"><span data-stu-id="e5586-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="e5586-116">Se desejar, você pode verificar a instalação Olá saltando para baixo demais[verificar o LAMP instalado com êxito](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="e5586-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="e5586-117">Passo a passo da implantação da LAMP em uma VM existente</span><span class="sxs-lookup"><span data-stu-id="e5586-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="e5586-118">Se você precisar de ajuda para criar uma VM do Linux, você pode head [toolearn aqui como toocreate uma VM do Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5586-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e5586-119">Em seguida, você precisa tooSSH em Olá VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="e5586-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="e5586-120">Se você precisar de ajuda com a criação de uma chave SSH, você pode head [toolearn aqui como toocreate uma chave SSH no Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5586-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="e5586-121">Se você já tiver uma chave SSH, prossiga e use o SSH na linha de comando da sua VM Linux com `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="e5586-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="e5586-122">Agora que você estiver trabalhando em sua VM do Linux, podemos pode percorrer instalando pilha LAMP de saudação em distribuições de Debian.</span><span class="sxs-lookup"><span data-stu-id="e5586-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="e5586-123">comandos exato Olá podem ser diferentes para outras distribuições de Linux.</span><span class="sxs-lookup"><span data-stu-id="e5586-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="e5586-124">Instalação no Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e5586-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="e5586-125">Você precisa Olá pacotes instalados a seguir: `apache2`, `mysql-server`, `php5`, e `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="e5586-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="e5586-126">Você pode instalar esses pacotes ao obtê-los diretamente ou usando o Tasksel.</span><span class="sxs-lookup"><span data-stu-id="e5586-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="e5586-127">As instruções para as duas opções estão listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="e5586-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="e5586-128">Antes de instalar, você precisa toodownload e listas de pacote de atualização.</span><span class="sxs-lookup"><span data-stu-id="e5586-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="e5586-129">Pacotes individuais</span><span class="sxs-lookup"><span data-stu-id="e5586-129">Individual packages</span></span>
<span data-ttu-id="e5586-130">Como usar apt-get:</span><span class="sxs-lookup"><span data-stu-id="e5586-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="e5586-131">Usando o Tasksel</span><span class="sxs-lookup"><span data-stu-id="e5586-131">Using tasksel</span></span>
<span data-ttu-id="e5586-132">Como alternativa, você pode baixar o Tasksel, uma ferramenta do Debian/Ubuntu que instala vários pacotes relacionados como uma “tarefa” coordenada em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="e5586-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="e5586-133">Depois de executar qualquer uma das opções anteriores hello, você vai ser solicitado tooinstall esses pacotes e várias outras dependências.</span><span class="sxs-lookup"><span data-stu-id="e5586-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="e5586-134">Pressione 'y' e 'Enter' toocontinue e execute qualquer tooset outros solicita uma senha administrativa para MySQL.</span><span class="sxs-lookup"><span data-stu-id="e5586-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="e5586-135">Isso instala Olá mínimo necessário PHP extensões necessário toouse PHP com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="e5586-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="e5586-136">Execute outras extensões PHP que estão disponíveis como pacotes de Olá toosee de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5586-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="e5586-137">Criar documento info.php</span><span class="sxs-lookup"><span data-stu-id="e5586-137">Create info.php document</span></span>
<span data-ttu-id="e5586-138">Você agora deve ser capaz de toocheck qual versão do PHP, MySQL e Apache ter pela linha de comando Olá digitando `apache2 -v`, `mysql -v`, ou `php -v`.</span><span class="sxs-lookup"><span data-stu-id="e5586-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="e5586-139">Se você como tootest ainda mais, você pode criar um tooview de página de informações rápida do PHP em um navegador.</span><span class="sxs-lookup"><span data-stu-id="e5586-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="e5586-140">Crie um arquivo com o editor de texto Nano usando este comando:</span><span class="sxs-lookup"><span data-stu-id="e5586-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="e5586-141">No editor de texto do GNU Nano hello, adicione Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="e5586-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="e5586-142">Em seguida, salve e feche o editor de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5586-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="e5586-143">Reinicie o Apache com este comando para que todas as novas instalações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="e5586-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="e5586-144">Verifique se a LAMP foi instalada com êxito</span><span class="sxs-lookup"><span data-stu-id="e5586-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="e5586-145">Agora você pode verificar a página de informações do PHP Olá criado abrindo um navegador e indo toohttp://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="e5586-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="e5586-146">Ela deve ser a imagem toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="e5586-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="e5586-147">Você pode verificar a instalação do Apache exibindo saudação do Apache2 Ubuntu padrão página indo tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="e5586-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="e5586-148">Você deverá ver algo parecido com esta imagem.</span><span class="sxs-lookup"><span data-stu-id="e5586-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="e5586-149">Parabéns, você instalou uma pilha LAMP em sua VM do Azure!</span><span class="sxs-lookup"><span data-stu-id="e5586-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5586-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5586-150">Next steps</span></span>
<span data-ttu-id="e5586-151">Check-out Olá Ubuntu documentação na pilha de LÂMPADA hello:</span><span class="sxs-lookup"><span data-stu-id="e5586-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="e5586-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="e5586-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png