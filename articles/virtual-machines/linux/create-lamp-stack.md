---
title: "aaaDeploy LÂMPADA em uma máquina virtual do Linux no Azure | Microsoft Docs"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="63578-103">Implantar pilha LAMP no Azure</span><span class="sxs-lookup"><span data-stu-id="63578-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="63578-104">Este artigo o orienta como toodeploy um Apache web server, MySQL e PHP (pilha de LÂMPADA Olá) no Azure.</span><span class="sxs-lookup"><span data-stu-id="63578-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="63578-105">Você precisa de uma conta do Azure ([obter uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)) e hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="63578-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="63578-106">Você também pode executar essas etapas com hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="63578-106">You can also perform these steps with hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="63578-107">Resumo rápido do comando</span><span class="sxs-lookup"><span data-stu-id="63578-107">Quick command summary</span></span>

1. <span data-ttu-id="63578-108">Salvar e editar Olá [azuredeploy.parameters.json arquivo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preferência em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="63578-108">Save and edit hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preference on your local machine.</span></span>
2. <span data-ttu-id="63578-109">Executar Olá toocreate de dois comandos a seguir em um grupo de recursos e, em seguida, implante o modelo:</span><span class="sxs-lookup"><span data-stu-id="63578-109">Run hello following two commands toocreate a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="63578-110">Implantar LAMP em VM existente</span><span class="sxs-lookup"><span data-stu-id="63578-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="63578-111">a seguir Olá comandos pacotes de atualizações, instala o Apache, MySQL e PHP:</span><span class="sxs-lookup"><span data-stu-id="63578-111">hello following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="63578-112">Passo a passo da implantação da LAMP em uma nova VM</span><span class="sxs-lookup"><span data-stu-id="63578-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="63578-113">Criar um grupo de recursos com [criar grupo az](/cli/azure/group#create) toocontain Olá nova VM:</span><span class="sxs-lookup"><span data-stu-id="63578-113">Create a resource group with [az group create](/cli/azure/group#create) toocontain hello new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="63578-114">toocreate Olá própria máquina virtual, você pode usar um modelo do Azure Resource Manager já escrito encontrado [aqui no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="63578-114">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="63578-115">Salvar Olá [azuredeploy.parameters.json arquivo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) máquina local tooyour.</span><span class="sxs-lookup"><span data-stu-id="63578-115">Save hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour local machine.</span></span>
3. <span data-ttu-id="63578-116">Editar saudação **azuredeploy.parameters.json** tooyour arquivo preferencial entradas.</span><span class="sxs-lookup"><span data-stu-id="63578-116">Edit hello **azuredeploy.parameters.json** file tooyour preferred inputs.</span></span>
4. <span data-ttu-id="63578-117">Implantar o modelo de saudação com [implantação do grupo az criar] referência Olá baixado o arquivo json:</span><span class="sxs-lookup"><span data-stu-id="63578-117">Deploy hello template with [az group deployment create] referencing hello downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="63578-118">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="63578-118">hello output is similar toohello following example:</span></span>

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

<span data-ttu-id="63578-119">Agora você criou uma VM Linux com LAMP já instalada.</span><span class="sxs-lookup"><span data-stu-id="63578-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="63578-120">Se desejar, você pode verificar a instalação Olá saltando para baixo demais[verificar o LAMP instalado com êxito](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="63578-120">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="63578-121">Passo a passo da implantação da LAMP em uma VM existente</span><span class="sxs-lookup"><span data-stu-id="63578-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="63578-122">Se você precisar de ajuda para criar uma VM do Linux, você pode head [toolearn aqui como toocreate uma VM do Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="63578-122">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="63578-123">Em seguida, você precisa tooSSH em Olá VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="63578-123">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="63578-124">Se você precisar de ajuda com a criação de uma chave SSH, você pode head [toolearn aqui como toocreate uma chave SSH no Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="63578-124">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="63578-125">Se você já tiver uma chave SSH, prossiga e use o SSH na linha de comando da sua VM Linux com `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="63578-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="63578-126">Agora que você estiver trabalhando em sua VM do Linux, podemos pode percorrer instalando pilha LAMP de saudação em distribuições de Debian.</span><span class="sxs-lookup"><span data-stu-id="63578-126">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="63578-127">comandos exato Olá podem ser diferentes para outras distribuições de Linux.</span><span class="sxs-lookup"><span data-stu-id="63578-127">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="63578-128">Instalação no Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="63578-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="63578-129">Você precisa Olá pacotes instalados a seguir: `apache2`, `mysql-server`, `php5`, e `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="63578-129">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="63578-130">Você pode instalar esses pacotes ao obtê-los diretamente ou usando o Tasksel.</span><span class="sxs-lookup"><span data-stu-id="63578-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="63578-131">Antes de instalar, você precisa toodownload e listas de pacote de atualização.</span><span class="sxs-lookup"><span data-stu-id="63578-131">Before installing you need toodownload and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="63578-132">Pacotes individuais</span><span class="sxs-lookup"><span data-stu-id="63578-132">Individual packages</span></span>
<span data-ttu-id="63578-133">Como usar apt-get:</span><span class="sxs-lookup"><span data-stu-id="63578-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="63578-134">Usando o Tasksel</span><span class="sxs-lookup"><span data-stu-id="63578-134">Using tasksel</span></span>
<span data-ttu-id="63578-135">Como alternativa, você pode baixar o Tasksel, uma ferramenta do Debian/Ubuntu que instala vários pacotes relacionados como uma “tarefa” coordenada em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="63578-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="63578-136">Depois de executar qualquer uma das opções anteriores hello, você vai ser solicitado tooinstall esses pacotes e várias outras dependências.</span><span class="sxs-lookup"><span data-stu-id="63578-136">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="63578-137">tooset uma senha administrativa para MySQL, pressione 'y' e 'Enter' toocontinue e siga os outros avisos.</span><span class="sxs-lookup"><span data-stu-id="63578-137">tooset an administrative password for MySQL, press 'y' and then 'Enter' toocontinue, and follow any other prompts.</span></span> <span data-ttu-id="63578-138">Esse processo instala Olá mínimo necessário PHP extensões necessário toouse PHP com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="63578-138">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="63578-139">Execute outras extensões PHP que estão disponíveis como pacotes de Olá toosee de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="63578-139">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="63578-140">Criar documento info.php</span><span class="sxs-lookup"><span data-stu-id="63578-140">Create info.php document</span></span>
<span data-ttu-id="63578-141">Você agora deve ser capaz de toocheck qual versão do PHP, MySQL e Apache ter pela linha de comando Olá digitando `apache2 -v`, `mysql -v`, ou `php -v`.</span><span class="sxs-lookup"><span data-stu-id="63578-141">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="63578-142">Se você como tootest ainda mais, você pode criar um tooview de página de informações rápida do PHP em um navegador.</span><span class="sxs-lookup"><span data-stu-id="63578-142">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="63578-143">Crie um arquivo com o editor de texto Nano usando este comando:</span><span class="sxs-lookup"><span data-stu-id="63578-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="63578-144">No editor de texto do GNU Nano hello, adicione Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="63578-144">Within hello GNU Nano text editor, add hello following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="63578-145">Em seguida, salve e feche o editor de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="63578-145">Then save and exit hello text editor.</span></span>

<span data-ttu-id="63578-146">Reinicie o Apache com este comando para que todas as novas instalações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="63578-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="63578-147">Verifique se a LAMP foi instalada com êxito</span><span class="sxs-lookup"><span data-stu-id="63578-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="63578-148">Agora você pode verificar a página de informações do PHP Olá criado abrindo um navegador e indo toohttp://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="63578-148">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="63578-149">Ela deve ser a imagem toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="63578-149">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="63578-150">Você pode verificar a instalação do Apache exibindo saudação do Apache2 Ubuntu padrão página indo tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="63578-150">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="63578-151">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="63578-151">hello output is similar toohello following example:</span></span>

![][3]

<span data-ttu-id="63578-152">Parabéns, você instalou uma pilha LAMP em sua VM do Azure!</span><span class="sxs-lookup"><span data-stu-id="63578-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="63578-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63578-153">Next steps</span></span>
<span data-ttu-id="63578-154">Check-out Olá Ubuntu documentação na pilha de LÂMPADA hello:</span><span class="sxs-lookup"><span data-stu-id="63578-154">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="63578-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="63578-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
