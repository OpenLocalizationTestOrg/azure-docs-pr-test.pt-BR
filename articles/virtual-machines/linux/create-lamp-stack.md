---
title: "Implantar LAMP em uma máquina virtual do Linux no Azure | Microsoft Docs"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: ad69876bfbeba5f948a81e5c48c659fdf2265ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="f6b6b-103">Implantar pilha LAMP no Azure</span><span class="sxs-lookup"><span data-stu-id="f6b6b-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="f6b6b-104">Este artigo explica como implantar um servidor Web Apache, MySQL e PHP (a pilha LAMP) no Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="f6b6b-105">Você precisa de uma conta do Azure ([Obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)) e da [CLI do Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="f6b6b-106">Você também pode executar essas etapas com a [CLI do Azure 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="f6b6b-107">Resumo rápido do comando</span><span class="sxs-lookup"><span data-stu-id="f6b6b-107">Quick command summary</span></span>

1. <span data-ttu-id="f6b6b-108">Salve e edite o [arquivo azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) de acordo com sua preferência em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span></span>
2. <span data-ttu-id="f6b6b-109">Execute os dois comandos a seguir para criar um grupo de recursos e, em seguida, implantar seu modelo:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-109">Run the following two commands to create a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="f6b6b-110">Implantar LAMP em VM existente</span><span class="sxs-lookup"><span data-stu-id="f6b6b-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="f6b6b-111">Os comandos a seguir atualizam os pacotes e instalam o Apache, o MySQL e o PHP:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="f6b6b-112">Passo a passo da implantação da LAMP em uma nova VM</span><span class="sxs-lookup"><span data-stu-id="f6b6b-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="f6b6b-113">Crie um grupo de recursos com [az group create](/cli/azure/group#create) para conter a nova VM:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="f6b6b-114">Para criar a própria VM, você pode usar um modelo do Azure Resource Manager já escrito encontrado [aqui no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="f6b6b-115">Salve o [arquivo azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span></span>
3. <span data-ttu-id="f6b6b-116">Edite o **arquivo azuredeploy.parameters.json** em suas entradas preferenciais.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span></span>
4. <span data-ttu-id="f6b6b-117">Implante o modelo com [az group deployment create] fazendo referência ao arquivo JSON baixado:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="f6b6b-118">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-118">The output is similar to the following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="f6b6b-119">Agora você criou uma VM Linux com LAMP já instalada.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="f6b6b-120">Se quiser, você poderá verificar a instalação indo até [Verificar se a LAMP foi instalada com êxito](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="f6b6b-121">Passo a passo da implantação da LAMP em uma VM existente</span><span class="sxs-lookup"><span data-stu-id="f6b6b-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="f6b6b-122">Se você precisar de ajuda para criar uma VM Linux, clique [aqui para saber como criá-la](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="f6b6b-123">Em seguida, você precisará usar o SSH na VM Linux.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-123">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="f6b6b-124">Se você precisar de ajuda para criar uma chave SSH, clique [aqui para saber como criá-la no Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="f6b6b-125">Se você já tiver uma chave SSH, prossiga e use o SSH na linha de comando da sua VM Linux com `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="f6b6b-126">Agora que você está trabalhando na VM Linux, podemos detalhar a instalação da pilha LAMP em distribuições baseadas em Debian.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="f6b6b-127">Os comandos exatos podem ser diferentes para outras distribuições de Linux.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-127">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="f6b6b-128">Instalação no Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f6b6b-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="f6b6b-129">Você precisa dos seguintes pacotes instalados: `apache2`, `mysql-server`, `php5` e `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="f6b6b-130">Você pode instalar esses pacotes ao obtê-los diretamente ou usando o Tasksel.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="f6b6b-131">Antes de instalar, você precisará baixar e atualizar as listas de pacotes.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-131">Before installing you need to download and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="f6b6b-132">Pacotes individuais</span><span class="sxs-lookup"><span data-stu-id="f6b6b-132">Individual packages</span></span>
<span data-ttu-id="f6b6b-133">Como usar apt-get:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="f6b6b-134">Usando o Tasksel</span><span class="sxs-lookup"><span data-stu-id="f6b6b-134">Using tasksel</span></span>
<span data-ttu-id="f6b6b-135">Como alternativa, você pode baixar o Tasksel, uma ferramenta do Debian/Ubuntu que instala vários pacotes relacionados como uma “tarefa” coordenada em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="f6b6b-136">Após executar uma das opções anteriores, você receberá uma solicitação para instalar esses pacotes e várias outras dependências.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="f6b6b-137">Para definir uma senha administrativa para o MySQL, pressione 'y' e depois 'Enter' para continuar e siga todas as solicitações.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span></span> <span data-ttu-id="f6b6b-138">Esse processo instala as extensões PHP mínimas obrigatórias e necessárias para usar o PHP com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="f6b6b-139">Execute o comando a seguir para ver outras extensões PHP que estão disponíveis em pacotes:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-139">Run the following command to see other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="f6b6b-140">Criar documento info.php</span><span class="sxs-lookup"><span data-stu-id="f6b6b-140">Create info.php document</span></span>
<span data-ttu-id="f6b6b-141">Agora você deve ser capaz de verificar qual versão do Apache, MySQL e PHP você tem por meio da linha de comando digitando `apache2 -v`, `mysql -v` ou `php -v`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="f6b6b-142">Se você quiser realizar mais testes, crie uma página de informações rápida de PHP para exibição em um navegador.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="f6b6b-143">Crie um arquivo com o editor de texto Nano usando este comando:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="f6b6b-144">No editor de texto Nano GNU, adicione as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-144">Within the GNU Nano text editor, add the following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="f6b6b-145">Salve e saia do editor de texto.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-145">Then save and exit the text editor.</span></span>

<span data-ttu-id="f6b6b-146">Reinicie o Apache com este comando para que todas as novas instalações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="f6b6b-147">Verifique se a LAMP foi instalada com êxito</span><span class="sxs-lookup"><span data-stu-id="f6b6b-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="f6b6b-148">Agora é possível verificar a página de informações do PHP que você criou abrindo um navegador e acessando http://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="f6b6b-149">A página deve ser semelhante a esta imagem.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-149">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="f6b6b-150">Você pode verificar a instalação do Apache exibindo a Página Padrão do Apache2 Ubuntu acessando http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="f6b6b-151">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-151">The output is similar to the following example:</span></span>

![][3]

<span data-ttu-id="f6b6b-152">Parabéns, você instalou uma pilha LAMP em sua VM do Azure!</span><span class="sxs-lookup"><span data-stu-id="f6b6b-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6b6b-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6b6b-153">Next steps</span></span>
<span data-ttu-id="f6b6b-154">Consulte a documentação do Ubuntu sobre a pilha LAMP:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-154">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="f6b6b-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="f6b6b-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
