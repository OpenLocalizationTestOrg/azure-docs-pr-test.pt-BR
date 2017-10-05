---
title: "Automação da implantação de aplicativos com extensões de máquina virtual | Microsoft Docs"
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f972fef75aa8e13af7dab908c2b0e2ec28f1324
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="463ab-103">Implantação de aplicativos com modelos do Azure Resource Manager para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="463ab-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="463ab-104">Depois que todos os requisitos de infraestrutura do Azure foram identificados e convertidos em um modelo de implantação, a implantação real do aplicativo precisa ser resolvida.</span><span class="sxs-lookup"><span data-stu-id="463ab-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="463ab-105">Implantação de aplicativo aqui se refere a instalar os binários do aplicativo real nos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="463ab-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="463ab-106">Para o exemplo de Loja de Música, .Net Core, NGINX e Supervisor precisam ser instalados e configurados em cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="463ab-106">For the Music Store sample, .Net Core, NGINX, and Supervisor need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="463ab-107">Os binários da Loja de Música precisam ser instalados na máquina virtual e o banco de dados da Loja de Música criado previamente.</span><span class="sxs-lookup"><span data-stu-id="463ab-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="463ab-108">Este documento detalha como extensões de Máquina Virtual podem automatizar a implantação de aplicativos e configuração de máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="463ab-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="463ab-109">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="463ab-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="463ab-110">Para obter a melhor experiência, pré-implante uma instância da solução em sua assinatura do Azure e trabalhe com o modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="463ab-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="463ab-111">O modelo completo pode ser encontrado aqui – [Implantação de Loja de Música no Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="463ab-111">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="463ab-112">Script de configuração</span><span class="sxs-lookup"><span data-stu-id="463ab-112">Configuration script</span></span>
<span data-ttu-id="463ab-113">Extensões de máquina virtual são programas especializados executadas em máquinas virtuais para fornecer automação da configuração.</span><span class="sxs-lookup"><span data-stu-id="463ab-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="463ab-114">As extensões estão disponíveis para várias finalidades específicas, como antivírus, configuração de registro e configuração do Docker.</span><span class="sxs-lookup"><span data-stu-id="463ab-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="463ab-115">Uma extensão de script personalizado pode ser usada para executar qualquer script em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="463ab-115">A custom script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="463ab-116">Com o exemplo de Loja de Música, cabe à extensão de script personalizado configurar máquinas virtuais do Ubuntu e instalar o aplicativo de Loja de Música.</span><span class="sxs-lookup"><span data-stu-id="463ab-116">With the Music Store sample, it is up to the custom script extension to configure the Ubuntu virtual machines and install the Music Store application.</span></span> 

<span data-ttu-id="463ab-117">Antes de detalhar como extensões de máquina virtual são declaradas em um modelo do Azure Resource Manager, examine o script que é executado.</span><span class="sxs-lookup"><span data-stu-id="463ab-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="463ab-118">Esse script configura a máquina virtual do Ubuntu para hospedar o aplicativo de Loja de Música.</span><span class="sxs-lookup"><span data-stu-id="463ab-118">This script configures the Ubuntu virtual machine to host the Music Store application.</span></span> <span data-ttu-id="463ab-119">Quando executado, o script instala todo software necessário, instala o aplicativo de Loja de Música do controle do código-fonte e prepara o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="463ab-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

<span data-ttu-id="463ab-120">Para saber mais sobre como hospedar um aplicativo .Net Core no Linux, consulte [Publicar em um ambiente de produção do Linux](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="463ab-120">To learn more about hosting a .Net Core application on Linux, see [Publish to a Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="463ab-121">Este exemplo é para fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="463ab-121">This sample is for demonstration purposes.</span></span>
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a><span data-ttu-id="463ab-122">Extensão de script da VM</span><span class="sxs-lookup"><span data-stu-id="463ab-122">VM Script Extension</span></span>
<span data-ttu-id="463ab-123">Extensões de VM podem ser executadas em uma máquina virtual no momento do build incluindo o recurso de extensão no modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="463ab-123">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="463ab-124">A extensão pode ser adicionada usando o Assistente para Adicionar Recursos do Visual Studio ou inserindo JSON válido no modelo.</span><span class="sxs-lookup"><span data-stu-id="463ab-124">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="463ab-125">O recurso de extensão do script é aninhado dentro do recurso de máquina virtual; isso pode ser visto no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="463ab-125">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="463ab-126">Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Extensão de script da VM](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="463ab-126">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="463ab-127">Observe que no JSON a seguir o script é armazenado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="463ab-127">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="463ab-128">Esse script também pode ser armazenado no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="463ab-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="463ab-129">Além disso, os modelos do Azure Resource Manager permitem a criação da cadeia de caracteres de execução de script de forma que os valores de parâmetros de modelo podem ser usados como parâmetros para execução de script.</span><span class="sxs-lookup"><span data-stu-id="463ab-129">Also, Azure Resource Manager templates allow the script execution string to constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="463ab-130">Nesse caso, os dados são fornecidos ao implantar os modelos e, em seguida, esses valores podem ser usados ao executar o script.</span><span class="sxs-lookup"><span data-stu-id="463ab-130">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="463ab-131">Para obter mais informações sobre como usar a extensão de script personalizado, consulte [Extensões de script personalizado com modelos do Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="463ab-131">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="463ab-132">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="463ab-132">Next Step</span></span>
<hr>

[<span data-ttu-id="463ab-133">Explorar mais modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="463ab-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

