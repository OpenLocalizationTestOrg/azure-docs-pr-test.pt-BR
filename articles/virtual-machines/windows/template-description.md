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
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="b321c-103">Máquinas virtuais em um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b321c-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="b321c-104">Este artigo descreve os aspectos de um modelo do Gerenciador de recursos do Azure que se aplicam a toovirtual máquinas.</span><span class="sxs-lookup"><span data-stu-id="b321c-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="b321c-105">Este artigo não descreve um modelo completo para a criação de uma máquina virtual. Para isso, são necessárias definições de recursos para contas de armazenamento, interfaces de rede, endereços IP públicos e redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="b321c-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="b321c-106">Para obter mais informações sobre como esses recursos podem ser definidos juntos, consulte Olá [passo a passo do Gerenciador de recursos modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="b321c-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="b321c-107">Existem várias [modelos na Galeria de saudação](https://azure.microsoft.com/documentation/templates/?term=VM) que incluem o recurso VM hello.</span><span class="sxs-lookup"><span data-stu-id="b321c-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="b321c-108">Nem todos os elementos que podem ser incluídos em um modelo são descritos aqui.</span><span class="sxs-lookup"><span data-stu-id="b321c-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="b321c-109">Este exemplo mostra uma seção de recursos típicos de um modelo para a criação de um número especificado de VMs:</span><span class="sxs-lookup"><span data-stu-id="b321c-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="b321c-110">Este exemplo se baseia em uma conta de armazenamento criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b321c-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="b321c-111">Você pode criar conta de armazenamento hello, implantando-a do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="b321c-112">exemplo Hello também se baseia em uma interface de rede e seus recursos dependentes que deve ser definidos no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="b321c-113">Esses recursos não são mostrados no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="b321c-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="b321c-114">Versão da API</span><span class="sxs-lookup"><span data-stu-id="b321c-114">API Version</span></span>

<span data-ttu-id="b321c-115">Quando você implantar recursos usando um modelo, você tem toospecify uma versão de hello API toouse.</span><span class="sxs-lookup"><span data-stu-id="b321c-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="b321c-116">exemplo Hello mostra o recurso de máquina virtual hello usando esse elemento apiVersion:</span><span class="sxs-lookup"><span data-stu-id="b321c-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="b321c-117">versão de saudação do hello API que você especificar no modelo afeta as propriedades que você pode definir no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="b321c-118">Em geral, você deve selecionar a versão de API mais recente Olá durante a criação de modelos.</span><span class="sxs-lookup"><span data-stu-id="b321c-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="b321c-119">Para modelos existentes, você pode decidir se deseja toocontinue usando uma versão anterior de API ou atualizar seu modelo para hello mais recente versão tootake aproveitar novos recursos.</span><span class="sxs-lookup"><span data-stu-id="b321c-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="b321c-120">Use essas oportunidades para obter as versões de API mais recentes hello:</span><span class="sxs-lookup"><span data-stu-id="b321c-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="b321c-121">API REST – [listar todos os provedores de recursos](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="b321c-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="b321c-122">PowerShell – [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="b321c-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="b321c-123">CLI 2.0 do Azure – [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="b321c-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="b321c-124">Parâmetros e variáveis</span><span class="sxs-lookup"><span data-stu-id="b321c-124">Parameters and variables</span></span>

<span data-ttu-id="b321c-125">[Parâmetros](../../resource-group-authoring-templates.md) facilitam para você toospecify valores para o modelo de hello quando você executá-lo.</span><span class="sxs-lookup"><span data-stu-id="b321c-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="b321c-126">Esta seção de parâmetros é usada no exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="b321c-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="b321c-127">Quando você implanta o modelo de exemplo hello, insira valores para nome hello e senha da conta de administrador de saudação em cada VM e Olá o número de VMs toocreate.</span><span class="sxs-lookup"><span data-stu-id="b321c-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="b321c-128">Você tem a opção de saudação de especificar valores de parâmetros em um arquivo separado que é gerenciado com o modelo de hello, ou fornecendo valores quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="b321c-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="b321c-129">[Variáveis](../../resource-group-authoring-templates.md) mais fácil para você tooset valores no modelo de saudação que são usadas repetidamente em toda ele ou que podem alterar ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="b321c-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="b321c-130">Esta seção de variáveis é usada no exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="b321c-130">This variables section is used in hello example:</span></span>

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

<span data-ttu-id="b321c-131">Quando você implanta o modelo de exemplo hello, valores de variáveis são usados para nome de saudação e o identificador da conta de armazenamento Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b321c-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="b321c-132">Variáveis também são configurações de Olá tooprovide usado para a extensão de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="b321c-133">Saudação de uso [práticas recomendadas para a criação de modelos do Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp você decidir como deseja toostructure Olá parâmetros e variáveis no modelo.</span><span class="sxs-lookup"><span data-stu-id="b321c-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="b321c-134">loops de recursos</span><span class="sxs-lookup"><span data-stu-id="b321c-134">Resource loops</span></span>

<span data-ttu-id="b321c-135">Quando você precisar de mais de uma máquina virtual para seu aplicativo, será possível usar um elemento de cópia em um modelo.</span><span class="sxs-lookup"><span data-stu-id="b321c-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="b321c-136">Esse elemento opcional percorre criando Olá número de VMs que você especificou como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="b321c-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="b321c-137">Além disso, observe que no exemplo hello Olá índice de loop é usado quando especificar alguns Olá valores para o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="b321c-138">Por exemplo, se você inseriu uma contagem de instâncias de três, nomes de saudação de discos do sistema operacional Olá são myOSDisk1, myOSDisk2 e myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="b321c-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="b321c-139">Este exemplo usa discos gerenciados para máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="b321c-140">Tenha em mente que a criação de um loop para um recurso no modelo de saudação pode exigir que você toouse Olá loop ao criar ou acessar outros recursos.</span><span class="sxs-lookup"><span data-stu-id="b321c-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="b321c-141">Por exemplo, várias VMs não podem usar Olá a mesma interface de rede para que se seu modelo percorre criar três máquinas virtuais também deve fazer loop por meio da criação de três interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="b321c-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="b321c-142">Ao atribuir um tooa de interface de rede VM, índice de loop Olá é usado tooidentify-lo:</span><span class="sxs-lookup"><span data-stu-id="b321c-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="b321c-143">Dependências</span><span class="sxs-lookup"><span data-stu-id="b321c-143">Dependencies</span></span>

<span data-ttu-id="b321c-144">A maioria dos recursos dependem de outros recursos toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="b321c-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="b321c-145">Máquinas virtuais deve ser associadas uma rede virtual e toodo que precisa de uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="b321c-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="b321c-146">Olá [dependsOn](../../resource-group-define-dependencies.md) elemento é usado toomake se essa interface de rede hello está pronto toobe usada antes de saudação VMs são criadas:</span><span class="sxs-lookup"><span data-stu-id="b321c-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="b321c-147">O Resource Manager implanta em paralelo quaisquer recursos que não dependem de outro recurso que está sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="b321c-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="b321c-148">Tenha cuidado ao configurar dependências, porque você pode inadvertidamente tornar sua implantação lenta ao especificar dependências desnecessárias.</span><span class="sxs-lookup"><span data-stu-id="b321c-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="b321c-149">As dependências podem ser encadeadas por meio de vários recursos.</span><span class="sxs-lookup"><span data-stu-id="b321c-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="b321c-150">Por exemplo, interface de rede Olá depende de endereço IP público de saudação e recursos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b321c-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="b321c-151">Como saber se uma dependência é necessária?</span><span class="sxs-lookup"><span data-stu-id="b321c-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="b321c-152">Examinar os valores de saudação definido no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="b321c-153">Se um elemento na definição de recurso de máquina virtual Olá pontos tooanother recurso que é implantado em Olá mesmo modelo, você precisa de uma dependência.</span><span class="sxs-lookup"><span data-stu-id="b321c-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="b321c-154">Por exemplo, sua máquina virtual de exemplo define um perfil de rede:</span><span class="sxs-lookup"><span data-stu-id="b321c-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="b321c-155">tooset essa propriedade, a interface de rede Olá deve existir.</span><span class="sxs-lookup"><span data-stu-id="b321c-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="b321c-156">Portanto, é necessário ter uma dependência.</span><span class="sxs-lookup"><span data-stu-id="b321c-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="b321c-157">Você também precisa tooset uma dependência quando um recurso (filho) é definido dentro de outro recurso (pai).</span><span class="sxs-lookup"><span data-stu-id="b321c-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="b321c-158">Por exemplo, configurações de diagnóstico hello e extensões de script personalizado são ambos definidas como recursos filho de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="b321c-159">Não é possível criar até que a máquina virtual de saudação existe.</span><span class="sxs-lookup"><span data-stu-id="b321c-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="b321c-160">Portanto, os dois recursos são marcados como dependentes na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="b321c-161">Perfis</span><span class="sxs-lookup"><span data-stu-id="b321c-161">Profiles</span></span>

<span data-ttu-id="b321c-162">Vários elementos de perfil são usados ao definir um recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b321c-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="b321c-163">Alguns são obrigatórios e alguns são opcionais.</span><span class="sxs-lookup"><span data-stu-id="b321c-163">Some are required and some are optional.</span></span> <span data-ttu-id="b321c-164">Por exemplo, elementos de saudação hardwareProfile, osProfile, storageProfile e networkProfile são necessários, mas diagnosticsProfile Olá é opcional.</span><span class="sxs-lookup"><span data-stu-id="b321c-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="b321c-165">Esses perfis definem configurações como:</span><span class="sxs-lookup"><span data-stu-id="b321c-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="b321c-166">tamanho</span><span class="sxs-lookup"><span data-stu-id="b321c-166">size</span></span>](sizes.md)
- <span data-ttu-id="b321c-167">[nome](/architecture/best-practices/naming-conventions) e credenciais</span><span class="sxs-lookup"><span data-stu-id="b321c-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="b321c-168">disco e [configurações do sistema operacional](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="b321c-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="b321c-169">adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="b321c-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="b321c-170">diagnóstico de inicialização</span><span class="sxs-lookup"><span data-stu-id="b321c-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="b321c-171">Discos e imagens</span><span class="sxs-lookup"><span data-stu-id="b321c-171">Disks and images</span></span>
   
<span data-ttu-id="b321c-172">No Azure, arquivos VHD podem representar [discos ou imagens](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b321c-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b321c-173">Sistema operacional de saudação em um arquivo vhd é especializada toobe uma VM específica, é chamado tooas um disco.</span><span class="sxs-lookup"><span data-stu-id="b321c-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="b321c-174">Quando o sistema operacional de saudação em um arquivo vhd é generalizado toobe usado toocreate muitas máquinas virtuais, ele é chamado tooas uma imagem.</span><span class="sxs-lookup"><span data-stu-id="b321c-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="b321c-175">Criar novas máquinas virtuais e novos discos de uma imagem de plataforma</span><span class="sxs-lookup"><span data-stu-id="b321c-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="b321c-176">Quando você cria uma máquina virtual, você deve decidir quais toouse do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="b321c-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="b321c-177">elemento de imageReference Olá é usado toodefine Olá sistema de operacional de uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="b321c-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="b321c-178">exemplo Hello mostra uma definição para um sistema operacional Windows Server:</span><span class="sxs-lookup"><span data-stu-id="b321c-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="b321c-179">Se você quiser toocreate um sistema operacional Linux, você pode usar essa definição:</span><span class="sxs-lookup"><span data-stu-id="b321c-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="b321c-180">Configurações de disco do sistema operacional Olá são atribuídas com elemento de osDisk hello.</span><span class="sxs-lookup"><span data-stu-id="b321c-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="b321c-181">Olá exemplo define um novo disco gerenciado com hello cache de conjunto de modo muito**ReadWrite** e disco hello está sendo criado de uma [imagem da plataforma](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="b321c-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="b321c-182">Criar novas máquinas virtuais de discos gerenciados existentes</span><span class="sxs-lookup"><span data-stu-id="b321c-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="b321c-183">Se você quiser que máquinas virtuais de toocreate de discos existentes, remova Olá imageReference e elementos de osProfile hello e definir essas configurações de disco:</span><span class="sxs-lookup"><span data-stu-id="b321c-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="b321c-184">Criar novas máquinas virtuais de uma imagem gerenciada</span><span class="sxs-lookup"><span data-stu-id="b321c-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="b321c-185">Se você quiser toocreate uma máquina virtual de uma imagem gerenciada, altere Olá imageReference elemento e definir essas configurações de disco:</span><span class="sxs-lookup"><span data-stu-id="b321c-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="b321c-186">Anexar discos de dados</span><span class="sxs-lookup"><span data-stu-id="b321c-186">Attach data disks</span></span>

<span data-ttu-id="b321c-187">Opcionalmente, você pode adicionar discos de dados toohello VMs.</span><span class="sxs-lookup"><span data-stu-id="b321c-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="b321c-188">Olá [número de discos](sizes.md) depende do tamanho de saudação do disco do sistema operacional que você usa.</span><span class="sxs-lookup"><span data-stu-id="b321c-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="b321c-189">Com hello tamanho das VMs Olá definido tooStandard_DS1_v2, o número máximo de saudação de discos de dados que pode ser adicionado toohello-los é dois.</span><span class="sxs-lookup"><span data-stu-id="b321c-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="b321c-190">Exemplo hello, um disco de dados gerenciado está sendo adicionado tooeach VM:</span><span class="sxs-lookup"><span data-stu-id="b321c-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="b321c-191">Extensões</span><span class="sxs-lookup"><span data-stu-id="b321c-191">Extensions</span></span>

<span data-ttu-id="b321c-192">Embora [extensões](extensions-features.md) são um recurso separado, são tooVMs estreitamente associado.</span><span class="sxs-lookup"><span data-stu-id="b321c-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="b321c-193">As extensões podem ser adicionadas como um recurso filho da saudação VM ou como um recurso separado.</span><span class="sxs-lookup"><span data-stu-id="b321c-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="b321c-194">exemplo Hello mostra Olá [extensão de diagnóstico](extensions-diagnostics-template.md) que está sendo adicionado toohello VMs:</span><span class="sxs-lookup"><span data-stu-id="b321c-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

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

<span data-ttu-id="b321c-195">Esse recurso de extensão usa variável de storageName hello e valores de tooprovide de variáveis de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="b321c-196">Se você quiser toochange Olá dados coletados por essa extensão, você pode adicionar mais variável de wadperfcounters do toohello contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="b321c-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="b321c-197">Você também pode escolher dados de diagnóstico de saudação tooput em uma conta de armazenamento diferente de onde os discos de VM Olá estão armazenados.</span><span class="sxs-lookup"><span data-stu-id="b321c-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="b321c-198">Há muitas extensões que podem ser instalados em uma máquina virtual, mas hello mais úteis provavelmente é hello [extensão de Script personalizado](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="b321c-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="b321c-199">No exemplo hello, um script do PowerShell chamado start.ps1 é executado em cada máquina virtual quando ele é iniciado:</span><span class="sxs-lookup"><span data-stu-id="b321c-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="b321c-200">script de start.ps1 Olá pode realizar muitas tarefas de configuração.</span><span class="sxs-lookup"><span data-stu-id="b321c-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="b321c-201">Por exemplo, discos de dados de saudação que são adicionados toohello VMs no exemplo hello não foram inicializados; Você pode usar um script personalizado tooinitialize-los.</span><span class="sxs-lookup"><span data-stu-id="b321c-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="b321c-202">Se você tiver várias toodo de tarefas de inicialização, você pode usar o hello start.ps1 arquivo toocall outros scripts do PowerShell no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b321c-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="b321c-203">exemplo Hello usa o PowerShell, mas você pode usar qualquer método de script que está disponível no sistema operacional Olá que você está usando.</span><span class="sxs-lookup"><span data-stu-id="b321c-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="b321c-204">Você pode ver o status de saudação de extensões de saudação instalada das configurações da saudação extensões no portal de saudação:</span><span class="sxs-lookup"><span data-stu-id="b321c-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![Obter status de extensão](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="b321c-206">Você também pode obter informações de extensão usando Olá **Get-AzureRmVMExtension** PowerShell comando hello **get de extensão de vm** comando 2.0 do CLI do Azure ou hello **obter informações de extensão**  API REST.</span><span class="sxs-lookup"><span data-stu-id="b321c-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="b321c-207">Implantações</span><span class="sxs-lookup"><span data-stu-id="b321c-207">Deployments</span></span>

<span data-ttu-id="b321c-208">Quando você implanta um modelo, recursos de saudação do Azure rastreia implantado como um grupo e automaticamente atribui um nome de grupo toothis implantado.</span><span class="sxs-lookup"><span data-stu-id="b321c-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="b321c-209">nome de saudação da implantação de saudação é Olá igual ao nome de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="b321c-210">Se você estiver curioso sobre o status de saudação de recursos na implantação hello, você pode usar folha de grupo de recursos de saudação em Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="b321c-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![Obter informações sobre a implantação](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="b321c-212">Não é um problema toouse Olá mesmo modelo toocreate tooupdate existente recursos ou.</span><span class="sxs-lookup"><span data-stu-id="b321c-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="b321c-213">Quando você usa comandos toodeploy modelos, você tem Olá oportunidade toosay que [modo](../../resource-group-template-deploy.md) toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="b321c-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="b321c-214">modo de saudação pode ser definido como tooeither **concluir** ou **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="b321c-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="b321c-215">padrão de saudação é toodo as atualizações incrementais.</span><span class="sxs-lookup"><span data-stu-id="b321c-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="b321c-216">Tenha cuidado ao usar o hello **concluir** modo porque você pode excluir acidentalmente recursos.</span><span class="sxs-lookup"><span data-stu-id="b321c-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="b321c-217">Quando você define o modo de saudação muito**concluir**, Gerenciador de recursos exclui todos os recursos no grupo de recursos de saudação que não estão no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b321c-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b321c-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b321c-218">Next Steps</span></span>

- <span data-ttu-id="b321c-219">Crie seu próprio modelo usando [Criação de modelos do Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b321c-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="b321c-220">Implante o modelo de saudação que você criou usando [criar uma máquina virtual do Windows com um modelo do Gerenciador de recursos](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="b321c-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="b321c-221">Saiba como toomanage Olá VMs que você criou, revisando [criar e gerenciar máquinas virtuais do Windows com o módulo do PowerShell do Azure Olá](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b321c-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
