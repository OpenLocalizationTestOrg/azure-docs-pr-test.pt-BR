---
title: "aaaVirtual máquinas em um modelo do Gerenciador de recursos do Azure | Microsoft Azure"
description: "Saiba mais sobre como o recurso de máquina virtual de saudação é definido em um modelo do Gerenciador de recursos do Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a>Máquinas virtuais em um modelo do Azure Resource Manager

Este artigo descreve os aspectos de um modelo do Gerenciador de recursos do Azure que se aplicam a toovirtual máquinas. Este artigo não descreve um modelo completo para a criação de uma máquina virtual. Para isso, são necessárias definições de recursos para contas de armazenamento, interfaces de rede, endereços IP públicos e redes virtuais. Para obter mais informações sobre como esses recursos podem ser definidos juntos, consulte Olá [passo a passo do Gerenciador de recursos modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Existem várias [modelos na Galeria de saudação](https://azure.microsoft.com/documentation/templates/?term=VM) que incluem o recurso VM hello. Nem todos os elementos que podem ser incluídos em um modelo são descritos aqui.

Este exemplo mostra uma seção de recursos típicos de um modelo para a criação de um número especificado de VMs:

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
>Este exemplo se baseia em uma conta de armazenamento criada anteriormente. Você pode criar conta de armazenamento hello, implantando-a do modelo de saudação. exemplo Hello também se baseia em uma interface de rede e seus recursos dependentes que deve ser definidos no modelo de saudação. Esses recursos não são mostrados no exemplo hello.
>
>

## <a name="api-version"></a>Versão da API

Quando você implantar recursos usando um modelo, você tem toospecify uma versão de hello API toouse. exemplo Hello mostra o recurso de máquina virtual hello usando esse elemento apiVersion:

```
"apiVersion": "2016-04-30-preview",
```

versão de saudação do hello API que você especificar no modelo afeta as propriedades que você pode definir no modelo de saudação. Em geral, você deve selecionar a versão de API mais recente Olá durante a criação de modelos. Para modelos existentes, você pode decidir se deseja toocontinue usando uma versão anterior de API ou atualizar seu modelo para hello mais recente versão tootake aproveitar novos recursos.

Use essas oportunidades para obter as versões de API mais recentes hello:

- API REST – [listar todos os provedores de recursos](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)
- PowerShell – [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)
- CLI 2.0 do Azure – [az provider show](https://docs.microsoft.com/cli/azure/provider#show)

## <a name="parameters-and-variables"></a>Parâmetros e variáveis

[Parâmetros](../../resource-group-authoring-templates.md) facilitam para você toospecify valores para o modelo de hello quando você executá-lo. Esta seção de parâmetros é usada no exemplo hello:

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

Quando você implanta o modelo de exemplo hello, insira valores para nome hello e senha da conta de administrador de saudação em cada VM e Olá o número de VMs toocreate. Você tem a opção de saudação de especificar valores de parâmetros em um arquivo separado que é gerenciado com o modelo de hello, ou fornecendo valores quando solicitado.

[Variáveis](../../resource-group-authoring-templates.md) mais fácil para você tooset valores no modelo de saudação que são usadas repetidamente em toda ele ou que podem alterar ao longo do tempo. Esta seção de variáveis é usada no exemplo hello:

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

Quando você implanta o modelo de exemplo hello, valores de variáveis são usados para nome de saudação e o identificador da conta de armazenamento Olá criado anteriormente. Variáveis também são configurações de Olá tooprovide usado para a extensão de diagnóstico de saudação. Saudação de uso [práticas recomendadas para a criação de modelos do Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp você decidir como deseja toostructure Olá parâmetros e variáveis no modelo.

## <a name="resource-loops"></a>loops de recursos

Quando você precisar de mais de uma máquina virtual para seu aplicativo, será possível usar um elemento de cópia em um modelo. Esse elemento opcional percorre criando Olá número de VMs que você especificou como um parâmetro:

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

Além disso, observe que no exemplo hello Olá índice de loop é usado quando especificar alguns Olá valores para o recurso de saudação. Por exemplo, se você inseriu uma contagem de instâncias de três, nomes de saudação de discos do sistema operacional Olá são myOSDisk1, myOSDisk2 e myOSDisk3:

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
>Este exemplo usa discos gerenciados para máquinas virtuais de saudação.
>
>

Tenha em mente que a criação de um loop para um recurso no modelo de saudação pode exigir que você toouse Olá loop ao criar ou acessar outros recursos. Por exemplo, várias VMs não podem usar Olá a mesma interface de rede para que se seu modelo percorre criar três máquinas virtuais também deve fazer loop por meio da criação de três interfaces de rede. Ao atribuir um tooa de interface de rede VM, índice de loop Olá é usado tooidentify-lo:

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a>Dependências

A maioria dos recursos dependem de outros recursos toowork corretamente. Máquinas virtuais deve ser associadas uma rede virtual e toodo que precisa de uma interface de rede. Olá [dependsOn](../../resource-group-define-dependencies.md) elemento é usado toomake se essa interface de rede hello está pronto toobe usada antes de saudação VMs são criadas:

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

O Resource Manager implanta em paralelo quaisquer recursos que não dependem de outro recurso que está sendo implantado. Tenha cuidado ao configurar dependências, porque você pode inadvertidamente tornar sua implantação lenta ao especificar dependências desnecessárias. As dependências podem ser encadeadas por meio de vários recursos. Por exemplo, interface de rede Olá depende de endereço IP público de saudação e recursos de rede virtual.

Como saber se uma dependência é necessária? Examinar os valores de saudação definido no modelo de saudação. Se um elemento na definição de recurso de máquina virtual Olá pontos tooanother recurso que é implantado em Olá mesmo modelo, você precisa de uma dependência. Por exemplo, sua máquina virtual de exemplo define um perfil de rede:

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

tooset essa propriedade, a interface de rede Olá deve existir. Portanto, é necessário ter uma dependência. Você também precisa tooset uma dependência quando um recurso (filho) é definido dentro de outro recurso (pai). Por exemplo, configurações de diagnóstico hello e extensões de script personalizado são ambos definidas como recursos filho de máquina virtual de saudação. Não é possível criar até que a máquina virtual de saudação existe. Portanto, os dois recursos são marcados como dependentes na máquina virtual de saudação.

## <a name="profiles"></a>Perfis

Vários elementos de perfil são usados ao definir um recurso de máquina virtual. Alguns são obrigatórios e alguns são opcionais. Por exemplo, elementos de saudação hardwareProfile, osProfile, storageProfile e networkProfile são necessários, mas diagnosticsProfile Olá é opcional. Esses perfis definem configurações como:
   
- [tamanho](sizes.md)
- [nome](/architecture/best-practices/naming-conventions) e credenciais
- disco e [configurações do sistema operacional](cli-ps-findimage.md)
- [adaptador de rede](../../virtual-network/virtual-networks-multiple-nics.md) 
- diagnóstico de inicialização

## <a name="disks-and-images"></a>Discos e imagens
   
No Azure, arquivos VHD podem representar [discos ou imagens](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Sistema operacional de saudação em um arquivo vhd é especializada toobe uma VM específica, é chamado tooas um disco. Quando o sistema operacional de saudação em um arquivo vhd é generalizado toobe usado toocreate muitas máquinas virtuais, ele é chamado tooas uma imagem.   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a>Criar novas máquinas virtuais e novos discos de uma imagem de plataforma

Quando você cria uma máquina virtual, você deve decidir quais toouse do sistema operacional. elemento de imageReference Olá é usado toodefine Olá sistema de operacional de uma nova VM. exemplo Hello mostra uma definição para um sistema operacional Windows Server:

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

Se você quiser toocreate um sistema operacional Linux, você pode usar essa definição:

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

Configurações de disco do sistema operacional Olá são atribuídas com elemento de osDisk hello. Olá exemplo define um novo disco gerenciado com hello cache de conjunto de modo muito**ReadWrite** e disco hello está sendo criado de uma [imagem da plataforma](cli-ps-findimage.md):

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a>Criar novas máquinas virtuais de discos gerenciados existentes

Se você quiser que máquinas virtuais de toocreate de discos existentes, remova Olá imageReference e elementos de osProfile hello e definir essas configurações de disco:

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a>Criar novas máquinas virtuais de uma imagem gerenciada

Se você quiser toocreate uma máquina virtual de uma imagem gerenciada, altere Olá imageReference elemento e definir essas configurações de disco:

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a>Anexar discos de dados

Opcionalmente, você pode adicionar discos de dados toohello VMs. Olá [número de discos](sizes.md) depende do tamanho de saudação do disco do sistema operacional que você usa. Com hello tamanho das VMs Olá definido tooStandard_DS1_v2, o número máximo de saudação de discos de dados que pode ser adicionado toohello-los é dois. Exemplo hello, um disco de dados gerenciado está sendo adicionado tooeach VM:

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a>Extensões

Embora [extensões](extensions-features.md) são um recurso separado, são tooVMs estreitamente associado. As extensões podem ser adicionadas como um recurso filho da saudação VM ou como um recurso separado. exemplo Hello mostra Olá [extensão de diagnóstico](extensions-diagnostics-template.md) que está sendo adicionado toohello VMs:

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

Esse recurso de extensão usa variável de storageName hello e valores de tooprovide de variáveis de diagnóstico de saudação. Se você quiser toochange Olá dados coletados por essa extensão, você pode adicionar mais variável de wadperfcounters do toohello contadores de desempenho. Você também pode escolher dados de diagnóstico de saudação tooput em uma conta de armazenamento diferente de onde os discos de VM Olá estão armazenados.

Há muitas extensões que podem ser instalados em uma máquina virtual, mas hello mais úteis provavelmente é hello [extensão de Script personalizado](extensions-customscript.md). No exemplo hello, um script do PowerShell chamado start.ps1 é executado em cada máquina virtual quando ele é iniciado:

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

script de start.ps1 Olá pode realizar muitas tarefas de configuração. Por exemplo, discos de dados de saudação que são adicionados toohello VMs no exemplo hello não foram inicializados; Você pode usar um script personalizado tooinitialize-los. Se você tiver várias toodo de tarefas de inicialização, você pode usar o hello start.ps1 arquivo toocall outros scripts do PowerShell no armazenamento do Azure. exemplo Hello usa o PowerShell, mas você pode usar qualquer método de script que está disponível no sistema operacional Olá que você está usando.

Você pode ver o status de saudação de extensões de saudação instalada das configurações da saudação extensões no portal de saudação:

![Obter status de extensão](./media/template-description/virtual-machines-show-extensions.png)

Você também pode obter informações de extensão usando Olá **Get-AzureRmVMExtension** PowerShell comando hello **get de extensão de vm** comando 2.0 do CLI do Azure ou hello **obter informações de extensão**  API REST.

## <a name="deployments"></a>Implantações

Quando você implanta um modelo, recursos de saudação do Azure rastreia implantado como um grupo e automaticamente atribui um nome de grupo toothis implantado. nome de saudação da implantação de saudação é Olá igual ao nome de saudação do modelo de saudação.

Se você estiver curioso sobre o status de saudação de recursos na implantação hello, você pode usar folha de grupo de recursos de saudação em Olá portal do Azure:

![Obter informações sobre a implantação](./media/template-description/virtual-machines-deployment-info.png)
    
Não é um problema toouse Olá mesmo modelo toocreate tooupdate existente recursos ou. Quando você usa comandos toodeploy modelos, você tem Olá oportunidade toosay que [modo](../../resource-group-template-deploy.md) toouse desejado. modo de saudação pode ser definido como tooeither **concluir** ou **Incremental**. padrão de saudação é toodo as atualizações incrementais. Tenha cuidado ao usar o hello **concluir** modo porque você pode excluir acidentalmente recursos. Quando você define o modo de saudação muito**concluir**, Gerenciador de recursos exclui todos os recursos no grupo de recursos de saudação que não estão no modelo de saudação.

## <a name="next-steps"></a>Próximas etapas

- Crie seu próprio modelo usando [Criação de modelos do Azure Resource Manager](../../resource-group-authoring-templates.md).
- Implante o modelo de saudação que você criou usando [criar uma máquina virtual do Windows com um modelo do Gerenciador de recursos](ps-template.md).
- Saiba como toomanage Olá VMs que você criou, revisando [criar e gerenciar máquinas virtuais do Windows com o módulo do PowerShell do Azure Olá](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
