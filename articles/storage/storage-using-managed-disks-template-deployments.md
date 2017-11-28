---
title: Usando discos gerenciados nos modelos do Azure Resource Manager | Microsoft Docs
description: Detalha sobre como utilizar discos gerenciados nos modelos do Azure Resource Manager
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: 4c502784a57850d6f11200e95f7432d2206e920a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="35594-103">Utilizar discos gerenciados nos modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35594-103">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="35594-104">Este documento aborda as diferenças entre discos gerenciados e não gerenciados ao utilizar os modelos do Azure Resource Manager para provisionar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="35594-104">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="35594-105">Isso irá ajudá-lo a atualizar os modelos existentes que utilizam Discos não gerenciados para discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="35594-105">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="35594-106">Para referência, estamos usando o modelo [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) como um guia.</span><span class="sxs-lookup"><span data-stu-id="35594-106">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="35594-107">É possível visualizar o modelo utilizando ambos os [Discos gerenciados](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) e uma versão anterior utilizando [discos não gerenciados](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json), se você deseja compará-los diretamente.</span><span class="sxs-lookup"><span data-stu-id="35594-107">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="35594-108">Formatação de modelo de Discos não gerenciados</span><span class="sxs-lookup"><span data-stu-id="35594-108">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="35594-109">Para começar, veremos como os discos não gerenciados são implantados.</span><span class="sxs-lookup"><span data-stu-id="35594-109">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="35594-110">Ao criar discos não gerenciados, é necessária uma conta de armazenamento para armazenar os arquivos de VHD.</span><span class="sxs-lookup"><span data-stu-id="35594-110">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="35594-111">É possível criar uma nova conta de armazenamento ou utilizar uma conta já existente.</span><span class="sxs-lookup"><span data-stu-id="35594-111">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="35594-112">Este artigo mostra como criar uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="35594-112">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="35594-113">Para fazer isso, você precisa de um recurso de conta de armazenamento em bloco de recursos, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="35594-113">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="35594-114">Dentro do objeto de máquina virtual, é preciso uma dependência na conta de armazenamento para garantir que é criada antes da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="35594-114">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="35594-115">Na seção `storageProfile` especificamos o URI completo do local do VHD que faz referência à conta de armazenamento e necessário para o disco do SO e qualquer disco de dados.</span><span class="sxs-lookup"><span data-stu-id="35594-115">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="35594-116">Formatação de modelo de discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="35594-116">Managed disks template formatting</span></span>

<span data-ttu-id="35594-117">Com o Azure Managed Disks, o disco torna-se um recurso de nível superior e não exige mais uma conta de armazenamento a ser criada pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="35594-117">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="35594-118">Os discos gerenciados foram expostos pela primeira vez na versão da API `2016-04-30-preview`. Eles estão disponíveis em todas as versões de API subsequentes e agora são o tipo de disco padrão.</span><span class="sxs-lookup"><span data-stu-id="35594-118">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="35594-119">As seções a seguir percorrem as configurações padrão e detalham como personalizar ainda mais seus discos.</span><span class="sxs-lookup"><span data-stu-id="35594-119">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="35594-120">Recomendamos usar uma versão da API posterior a `2016-04-30-preview`, pois houve alterações consideráveis entre `2016-04-30-preview` e `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="35594-120">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="35594-121">Configurações de disco gerenciados padrão</span><span class="sxs-lookup"><span data-stu-id="35594-121">Default managed disk settings</span></span>

<span data-ttu-id="35594-122">Para criar uma VM com discos gerenciados, não é mais necessário criar o recurso da conta de armazenamento e atualizar o recurso da máquina virtual, conforme a seguir.</span><span class="sxs-lookup"><span data-stu-id="35594-122">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="35594-123">Observe especificamente que `apiVersion` reflete `2017-03-30` e `osDisk` e `dataDisks` não referem-se mais a um URI específico para VHD.</span><span class="sxs-lookup"><span data-stu-id="35594-123">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="35594-124">Ao implantar sem especificar propriedades adicionais, o disco usará o [Armazenamento LRS Standard](storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="35594-124">When deploying without specifying additional properties, the disk will use [Standard LRS storage](storage-redundancy.md).</span></span> <span data-ttu-id="35594-125">Se nenhum nome for especificado, será necessário o formato de `<VMName>_OsDisk_1_<randomstring>` para o disco do SO e `<VMName>_disk<#>_<randomstring>` para cada disco de dados.</span><span class="sxs-lookup"><span data-stu-id="35594-125">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="35594-126">Por padrão, a criptografia do disco do Azure está desabilitada; o caching é Leitura/Gravação para o disco do OS e Nenhum para os discos de dados.</span><span class="sxs-lookup"><span data-stu-id="35594-126">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="35594-127">É possível notar no exemplo abaixo que ainda há uma dependência de conta de armazenamento, porém, isso é apenas para armazenamento de diagnósticos e não é necessário para armazenamento em disco.</span><span class="sxs-lookup"><span data-stu-id="35594-127">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="35594-128">Utilizar um recurso de disco gerenciado de nível superior</span><span class="sxs-lookup"><span data-stu-id="35594-128">Using a top-level managed disk resource</span></span>

<span data-ttu-id="35594-129">Como alternativa para especificar a configuração do disco no objeto da máquina virtual, você pode criar um recurso de disco de nível superior e anexá-lo como parte da criação da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="35594-129">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="35594-130">Por exemplo, é possível criar um recurso de disco da seguinte forma para utiiza como um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="35594-130">For example, we can create a disk resource as follows to use as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="35594-131">Dentro do objeto da VM é possível fazer referência a este objeto de disco para ser anexado.</span><span class="sxs-lookup"><span data-stu-id="35594-131">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="35594-132">Especificar o ID do recurso do disco gerenciado criado na propriedade `managedDisk` permite a conexão do disco à medida que a VM é criada.</span><span class="sxs-lookup"><span data-stu-id="35594-132">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="35594-133">Observe que o `apiVersion` para o recurso da VM está definido como `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="35594-133">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="35594-134">Observe também que uma dependência foi criada no recurso de disco para garantir que tenha sido criado com êxito antes da criação da VM.</span><span class="sxs-lookup"><span data-stu-id="35594-134">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="35594-135">Criar conjuntos de disponibilidade gerenciados com VMs utilizando discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="35594-135">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="35594-136">Para criar conjuntos de disponibilidade gerenciados com VMs utilizando discos gerenciados, adicione o objeto `sku` ao recurso do conjunto de disponibilidade e defina a propriedade `name` para `Aligned`.</span><span class="sxs-lookup"><span data-stu-id="35594-136">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="35594-137">Isso garante que os discos para cada VM estejam suficientemente isolados uns dos outros para evitar pontos únicos de falha.</span><span class="sxs-lookup"><span data-stu-id="35594-137">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="35594-138">Observe também que o `apiVersion` para o recurso do conjunto de disponibilidade está definido como `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="35594-138">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="35594-139">Cenários e personalizações adicionais</span><span class="sxs-lookup"><span data-stu-id="35594-139">Additional scenarios and customizations</span></span>

<span data-ttu-id="35594-140">Para encontrar informações completas sobre as especificações de API REST, revise [criar uma documentação de API REST de disco gerenciado](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="35594-140">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="35594-141">Você encontrará cenários adicionais, assim como valores padrão e aceitáveis que podem ser enviados para a API por meio de implantações de modelos.</span><span class="sxs-lookup"><span data-stu-id="35594-141">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="35594-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35594-142">Next steps</span></span>

* <span data-ttu-id="35594-143">Para modelos completos que utilizam discos gerenciados, visite os seguintes links do Repositório de Início Rápido do Azure.</span><span class="sxs-lookup"><span data-stu-id="35594-143">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="35594-144">VM do Windows VM com disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="35594-144">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="35594-145">VM do Linux VM com disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="35594-145">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="35594-146">Lista completa de modelos de disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="35594-146">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="35594-147">Consulte o documento [Visão Geral do Azure Managed Disks](storage-managed-disks-overview.md) para saber mais sobre discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="35594-147">Visit the [Azure Managed Disks Overview](storage-managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="35594-148">Revise a documentação de referência do modelo para recursos da máquina virtual, visitando o documento em [Microsoft.Compute/referência de modelo de virtualMachines](/templates/microsoft.compute/virtualmachines).</span><span class="sxs-lookup"><span data-stu-id="35594-148">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="35594-149">Revise a documentação de referência do modelo para recursos de disco, visitando o documento em [Microsoft.Compute/referência de modelo de discos](/templates/microsoft.compute/disks).</span><span class="sxs-lookup"><span data-stu-id="35594-149">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
