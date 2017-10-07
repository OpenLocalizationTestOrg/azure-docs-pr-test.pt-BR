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
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Implantação de aplicativos com modelos do Azure Resource Manager para VMs Linux

Depois que todos os requisitos de infra-estrutura do Azure foram identificados e convertidos em um modelo de implantação, implantação de aplicativo real Olá precisa toobe resolvido. Implantação de aplicativo aqui se refere a tooinstalling Olá real binários em recursos do Azure. Para exemplo de repositório de música hello, .net Core, NGINX e Supervisor precisam toobe instalado e configurado em cada máquina virtual. Olá binários necessário toobe instalado na máquina virtual de saudação do repositório de música e Olá banco de dados do repositório de música criado previamente.

Este documento detalha como extensões de máquina Virtual podem automatizar máquinas de virtuais de tooAzure de implantação e configuração de aplicativo. Todas as dependências e configurações exclusivas são realçadas. Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello. modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="configuration-script"></a>Script de configuração
Extensões de máquina virtual são programas especializados que são executadas em automação de configuração de tooprovide de máquinas virtuais. As extensões estão disponíveis para várias finalidades específicas, como antivírus, configuração de registro e configuração do Docker. Uma extensão de script personalizado pode ser usado toorun os scripts em uma máquina virtual. Com exemplo de repositório de música hello, é backup de máquinas de virtuais toohello script personalizado extensão tooconfigure Olá Ubuntu e instalar o aplicativo de repositório de música hello. 

Antes de Detalhar como extensões de máquina virtual são declaradas em um modelo do Azure Resource Manager, examine o script hello que é executado. Esse script configura Olá Ubuntu máquina virtual toohost Olá aplicativo de repositório de música. Quando executado, o script de Olá instala o software necessário todos os, instalar o aplicativo de repositório de música de saudação do controle de origem e preparar o banco de dados de saudação. 

toolearn mais sobre hospedagem .net Core aplicativo no Linux, consulte [ambiente de produção publicar tooa Linux](https://docs.asp.net/en/latest/publishing/linuxproduction.html).

> Este exemplo é para fins de demonstração.
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

## <a name="vm-script-extension"></a>Extensão de script da VM
Extensões de VM pode ser executadas em uma máquina virtual no momento da compilação, incluindo o recurso de extensão Olá no modelo do Azure Resource Manager hello. extensão de saudação pode ser adicionado com o Assistente do Visual Studio adicionar recurso hello, ou inserindo um JSON válido no modelo de saudação. Olá recursos de extensão do Script está aninhado em Olá recurso de máquina Virtual. Isso pode ser visto no exemplo a seguir de saudação.

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [extensão do Script VM](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359). 

Observe Olá abaixo JSON que Olá script é armazenado no GitHub. Esse script também pode ser armazenado no Armazenamento de Blobs do Azure. Além disso, os modelos de Gerenciador de recursos do Azure permitem tooconstructed de cadeia de caracteres de execução de script hello, de modo que os valores de parâmetros de modelo podem ser usados como parâmetros para a execução do script. Nesse caso os dados são fornecidos ao implantar modelos Olá, e esses valores, em seguida, podem ser usados ao executar o script hello.

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

Para obter mais informações sobre como usar a extensão do script personalizado hello, consulte [extensões de script personalizado com modelos do Gerenciador de recursos](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="next-step"></a>Próxima etapa
<hr>

[Explorar mais modelos do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

