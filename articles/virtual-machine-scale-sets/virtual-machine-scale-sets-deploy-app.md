---
title: "Define aaaDeploy um aplicativo em escala de máquinas virtuais"
description: "Use extensões toodepoy um aplicativo em conjuntos de escala de máquina Virtual do Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Implantar o aplicativo em conjuntos de dimensionamento de máquinas virtuais

Este artigo descreve as diferentes maneiras de como definir o software tooinstall escala de saudação do tempo de saudação é provisionado.

Talvez você queira Olá tooreview [visão geral do Design definir escala](virtual-machine-scale-sets-design-overview.md) artigo, que descreve alguns dos limites de saudação impostos por conjuntos de escala de máquina virtual.

## <a name="capture-and-reuse-an-image"></a>Capturar e reutilizar uma imagem

Você pode usar uma máquina virtual que no Azure tooprepare uma imagem de base para a escala configurou. Esse processo cria um disco gerenciado na sua conta de armazenamento, você pode fazer referência como imagem de base Olá para o conjunto de escala. 

Olá seguintes etapas:

1. Crie uma Máquina Virtual do Azure
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. Remoto em Olá a máquina virtual e personalizar a preferência de tooyour sistema hello.

   Se você quiser, é possível instalar o aplicativo agora. No entanto, saiba que ao instalar seu aplicativo agora, você pode fazer upgrade do seu aplicativo mais complicado porque talvez seja necessário tooremove-lo primeiro. Em vez disso, você pode usar essa etapa tooinstall todos os pré-requisitos que seu aplicativo pode ser necessário, como um recurso de tempo de execução ou sistema operacional específico.

3. Siga hello "capturar uma máquina" tutorial para o [Linux] [ linux-vm-capture] ou [Windows][windows-vm-capture].

4. Criar um [conjunto de escala de máquinas virtuais] [ vmss-create] com hello capturados na etapa anterior de saudação do URI da imagem.

Para obter mais informações, consulte [Visão geral do Managed Disks](../virtual-machines/windows/managed-disks-overview.md) e [Utilizar discos de dados anexados](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-hello-scale-set-is-provisioned"></a>Instalar ao conjunto de escala de saudação é provisionado

Extensões de máquinas virtuais podem ser aplicadas tooa conjunto de escalas da máquina virtual. Com uma extensão de máquina virtual, você pode personalizar máquinas virtuais de saudação em uma escala definida como um grupo inteiro. Para obter mais informações, consulte [Extensões da máquina virtual](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Há três extensões principais que podem ser utilizadas, dependendo se o sistema operacional é baseado no Linux ou baseado no Windows.

### <a name="windows"></a>Windows

Para um sistema operacional baseado no Windows, use o hello **v 1.8 de Script personalizado** extensão ou hello **PowerShell DSC** extensão.

#### <a name="custom-script"></a>Custom Script

saudação de extensão do Script personalizado executa um script em cada instância de máquina virtual no conjunto de escala de saudação. Um arquivo de configuração ou variável indica quais arquivos são baixados toohello VM e, em seguida, o comando é executado. Você pode usar este toorun um instalador, um script, um arquivo em lotes, qualquer executável por exemplo.

PowerShell usa uma tabela de hash para configurações de saudação. Este exemplo configura Olá script personalizado extensão toorun um script do PowerShell que instala o IIS.

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Saudação de uso `-ProtectedSetting` alternar para as configurações que podem conter informações confidenciais.

---------


CLI do Azure usa um arquivo json para configurações de saudação. Este exemplo configura Olá script personalizado extensão toorun um script do PowerShell que instala o IIS. Salvar Olá arquivo json como a seguir _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

Em seguida, execute esse comando da CLI do Azure.

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Saudação de uso `--protected-settings` alternar para as configurações que podem conter informações confidenciais.

### <a name="powershell-dsc"></a>DSC do PowerShell

Você pode usar instâncias de vm do conjunto de escala do DSC do PowerShell toocustomize hello. Olá **DSC** extensão publicada por **PowerShell** implanta e executa a configuração de DSC Olá fornecido em cada instância de máquina virtual. Um arquivo de configuração ou variável informa extensão Olá onde *. zip* pacote for e que _função script_ toorun de combinação.

PowerShell usa uma tabela de hash para configurações de saudação. Esse exemplo implanta um pacote de DSC que instala o IIS.

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Saudação de uso `-ProtectedSetting` alternar para as configurações que podem conter informações confidenciais.

-----------

CLI do Azure usa json para configurações de saudação. Esse exemplo implanta um pacote de DSC que instala o IIS. Salvar Olá arquivo json como a seguir _settings.json_.

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

Em seguida, execute esse comando da CLI do Azure.

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Saudação de uso `--protected-settings` alternar para as configurações que podem conter informações confidenciais.

### <a name="linux"></a>Linux

Linux pode usar qualquer Olá **v 2.0 do Script personalizado** extensão ou use **init nuvem** durante a criação.

Script personalizado é uma extensão simple que instâncias de máquina virtual de toohello arquivos de baixa e executa um comando.

#### <a name="custom-script"></a>Custom Script

Salvar Olá arquivo json como a seguir _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

Use Olá CLI do Azure tooadd este tooan de extensão existente do conjunto de escalas da máquina virtual. Cada máquina virtual em escala Olá definidas automaticamente execuções Olá extensão.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Saudação de uso `--protected-settings` alternar para as configurações que podem conter informações confidenciais.

#### <a name="cloud-init"></a>Inicialização de nuvem

Nuvem Init é usado quando o conjunto de escala Olá é criado. Primeiro, crie um arquivo local chamado _init.txt nuvem_ e adicione tooit sua configuração. Por exemplo, consulte [essas linhas gerais](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)

Olá Use CLI do Azure toocreate uma escala definida. Olá `--custom-data` campo aceita o nome de arquivo hello de um script de inicialização de nuvem.

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a>Como gerenciar atualizações de aplicativos?

Se você implantou seu aplicativo por meio de uma extensão, altere a definição de extensão de saudação de alguma forma. Essa alteração faz com que as instâncias de máquina virtual Olá extensão toobe reimplantado tooall. Algo **deve** alterado sobre extensão hello, como renomear um arquivo referenciado, caso contrário, faz do Azure não veja que Olá extensão foi alterada.

Se você implantadas aplicativo hello na sua própria imagem do sistema operacional, use um pipeline de implantação automática para atualizações de aplicativos. Crie seu toofacilitate arquitetura rápida de troca de uma escala de preparada definido em produção. Um bom exemplo dessa abordagem é hello [trabalho do Azure Spinnaker driver](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Packer](https://www.packer.io/) e [Terraform](https://www.terraform.io/) suporte do Azure Resource Manager, para que você também pode definir suas imagens "de código" e criá-las no Azure, em seguida, usar Olá VHD em seu conjunto de escala. No entanto, isso seria problemático para imagens do marketplace, nas quais extensões/scripts personalizados se tornam mais importantes, já que você não manipula diretamente os bits do marketplace.

## <a name="what-happens-when-a-scale-set-scales-out"></a>O que acontece quando um conjunto de dimensionamento é escalado horizontalmente?
Quando você adiciona um ou mais conjuntos de escala tooa de máquinas virtuais, o aplicativo hello é instalado automaticamente. Para exemplo se o conjunto de escala Olá tem extensões definidas, eles executados em uma nova máquina virtual sempre que ela é criada. Se o conjunto de escala Olá baseia-se em uma imagem personalizada, qualquer nova máquina virtual é uma cópia da imagem personalizada do hello fonte. Se Olá máquinas de virtuais de conjunto de escala são hosts de contêiner, você pode ter contêineres de saudação do tooload de código de inicialização em uma extensão de Script personalizado. Ou, uma extensão poderá instalar um agente que se registre com um orquestrador de cluster, como o Serviço de Contêiner do Azure.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>Como você implementa uma atualização de SO em domínios de atualização?
Suponha que você queira tooupdate sua imagem de sistema operacional, mantendo a escala de máquinas virtuais de saudação definido em execução. PowerShell e hello CLI do Azure podem atualizar imagens de máquinas virtuais hello, uma máquina virtual por vez. Olá [atualizar um conjunto de escala de máquinas virtuais](./virtual-machine-scale-sets-upgrade-scale-set.md) artigo também fornece informações adicionais sobre quais opções estão disponível tooperform atualizar um sistema operacional em um conjunto de escala de máquina virtual.

## <a name="next-steps"></a>Próximas etapas

* [Use o PowerShell toomanage seu conjunto de escala.](virtual-machine-scale-sets-windows-manage.md)
* [Criar um modelo de conjunto de dimensionamento.](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

