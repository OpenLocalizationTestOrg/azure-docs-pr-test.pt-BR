---
title: "Implantação de aplicativo com extensões de máquina Virtual de aaaAutomating | Microsoft Docs"
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
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="d005d-103">Implantação de aplicativos com modelos do Azure Resource Manager para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="d005d-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="d005d-104">Depois que todos os requisitos de infra-estrutura do Azure foram identificados e convertidos em um modelo de implantação, implantação de aplicativo real Olá precisa toobe resolvido.</span><span class="sxs-lookup"><span data-stu-id="d005d-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="d005d-105">Implantação de aplicativo aqui se refere a tooinstalling Olá real binários em recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d005d-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="d005d-106">Para exemplo de repositório de música hello, .net Core, NGINX e Supervisor precisam toobe instalado e configurado em cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d005d-106">For hello Music Store sample, .Net Core, NGINX, and Supervisor need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="d005d-107">Olá binários necessário toobe instalado na máquina virtual de saudação do repositório de música e Olá banco de dados do repositório de música criado previamente.</span><span class="sxs-lookup"><span data-stu-id="d005d-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="d005d-108">Este documento detalha como extensões de máquina Virtual podem automatizar máquinas de virtuais de tooAzure de implantação e configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d005d-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="d005d-109">Todas as dependências e configurações exclusivas são realçadas.</span><span class="sxs-lookup"><span data-stu-id="d005d-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="d005d-110">Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="d005d-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="d005d-111">modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="d005d-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="d005d-112">Script de configuração</span><span class="sxs-lookup"><span data-stu-id="d005d-112">Configuration script</span></span>
<span data-ttu-id="d005d-113">Extensões de máquina virtual são programas especializados que são executadas em automação de configuração de tooprovide de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d005d-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="d005d-114">As extensões estão disponíveis para várias finalidades específicas, como antivírus, configuração de registro e configuração do Docker.</span><span class="sxs-lookup"><span data-stu-id="d005d-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="d005d-115">Uma extensão de script personalizado pode ser usado toorun os scripts em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d005d-115">A custom script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="d005d-116">Com exemplo de repositório de música hello, é backup de máquinas de virtuais toohello script personalizado extensão tooconfigure Olá Ubuntu e instalar o aplicativo de repositório de música hello.</span><span class="sxs-lookup"><span data-stu-id="d005d-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Ubuntu virtual machines and install hello Music Store application.</span></span> 

<span data-ttu-id="d005d-117">Antes de Detalhar como extensões de máquina virtual são declaradas em um modelo do Azure Resource Manager, examine o script hello que é executado.</span><span class="sxs-lookup"><span data-stu-id="d005d-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="d005d-118">Esse script configura Olá Ubuntu máquina virtual toohost Olá aplicativo de repositório de música.</span><span class="sxs-lookup"><span data-stu-id="d005d-118">This script configures hello Ubuntu virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="d005d-119">Quando executado, o script de Olá instala o software necessário todos os, instalar o aplicativo de repositório de música de saudação do controle de origem e preparar o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d005d-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

<span data-ttu-id="d005d-120">toolearn mais sobre hospedagem .net Core aplicativo no Linux, consulte [ambiente de produção publicar tooa Linux](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="d005d-120">toolearn more about hosting a .Net Core application on Linux, see [Publish tooa Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="d005d-121">Este exemplo é para fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="d005d-121">This sample is for demonstration purposes.</span></span>
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

## <a name="vm-script-extension"></a><span data-ttu-id="d005d-122">Extensão de script da VM</span><span class="sxs-lookup"><span data-stu-id="d005d-122">VM Script Extension</span></span>
<span data-ttu-id="d005d-123">Extensões de VM pode ser executadas em uma máquina virtual no momento da compilação, incluindo o recurso de extensão Olá no modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="d005d-123">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="d005d-124">extensão de saudação pode ser adicionado com o Assistente do Visual Studio adicionar recurso hello, ou inserindo um JSON válido no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d005d-124">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="d005d-125">Olá recursos de extensão do Script está aninhado em Olá recurso de máquina Virtual. Isso pode ser visto no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="d005d-125">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="d005d-126">Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [extensão do Script VM](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="d005d-126">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="d005d-127">Observe Olá abaixo JSON que Olá script é armazenado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="d005d-127">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="d005d-128">Esse script também pode ser armazenado no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d005d-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="d005d-129">Além disso, os modelos de Gerenciador de recursos do Azure permitem tooconstructed de cadeia de caracteres de execução de script hello, de modo que os valores de parâmetros de modelo podem ser usados como parâmetros para a execução do script.</span><span class="sxs-lookup"><span data-stu-id="d005d-129">Also, Azure Resource Manager templates allow hello script execution string tooconstructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="d005d-130">Nesse caso os dados são fornecidos ao implantar modelos Olá, e esses valores, em seguida, podem ser usados ao executar o script hello.</span><span class="sxs-lookup"><span data-stu-id="d005d-130">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="d005d-131">Para obter mais informações sobre como usar a extensão do script personalizado hello, consulte [extensões de script personalizado com modelos do Gerenciador de recursos](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d005d-131">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="d005d-132">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="d005d-132">Next Step</span></span>
<hr>

[<span data-ttu-id="d005d-133">Explorar mais modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d005d-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

