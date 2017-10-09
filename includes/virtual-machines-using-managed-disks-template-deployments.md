# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="cc64d-101">Utilizar discos gerenciados nos modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cc64d-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="cc64d-102">Este documento explica como as diferenças de saudação entre discos gerenciados e ao usar máquinas virtuais do Azure Resource Manager modelos tooprovision.</span><span class="sxs-lookup"><span data-stu-id="cc64d-102">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="cc64d-103">Isso ajudará tooupdate modelos existentes que estão usando discos de toomanaged de discos não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cc64d-103">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="cc64d-104">Para referência, estamos usando Olá [101-vm simples do windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) modelo como um guia.</span><span class="sxs-lookup"><span data-stu-id="cc64d-104">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="cc64d-105">Você pode ver o modelo hello usando [discos gerenciado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) e uma versão anterior usando [não gerenciado discos](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) se você gostaria que toodirectly compará-los.</span><span class="sxs-lookup"><span data-stu-id="cc64d-105">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="cc64d-106">Formatação de modelo de Discos não gerenciados</span><span class="sxs-lookup"><span data-stu-id="cc64d-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="cc64d-107">toobegin, vamos dar uma olhada em discos como não gerenciados são implantados.</span><span class="sxs-lookup"><span data-stu-id="cc64d-107">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="cc64d-108">Durante a criação de discos não gerenciados, é necessário um arquivos VHD do armazenamento conta toohold hello.</span><span class="sxs-lookup"><span data-stu-id="cc64d-108">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="cc64d-109">É possível criar uma nova conta de armazenamento ou utilizar uma conta já existente.</span><span class="sxs-lookup"><span data-stu-id="cc64d-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="cc64d-110">Este artigo mostra como toocreate uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cc64d-110">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="cc64d-111">tooaccomplish isso, é necessário um recurso de conta de armazenamento em bloco de recursos hello, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cc64d-111">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

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

<span data-ttu-id="cc64d-112">No objeto de máquina virtual hello, precisamos de uma dependência no hello tooensure de conta de armazenamento que ele foi criado antes da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc64d-112">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="cc64d-113">Dentro de saudação `storageProfile` seção, em seguida, especificamos Olá URI completo do hello local do VHD, que faz referência a conta de armazenamento hello e é necessária para o disco Olá SO e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="cc64d-113">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="cc64d-114">Formatação de modelo de discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="cc64d-114">Managed disks template formatting</span></span>

<span data-ttu-id="cc64d-115">Com discos gerenciado do Azure, disco Olá se torna um recurso de nível superior e não requer mais um toobe de conta de armazenamento criada pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="cc64d-115">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="cc64d-116">Discos gerenciados primeiro foram expostos no hello `2016-04-30-preview` versão da API, eles estão disponíveis em todas as versões de API subsequentes e agora são o tipo de disco saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="cc64d-116">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="cc64d-117">Olá seções a seguir percorrer as configurações padrão de saudação e detalham de como toofurther personalizar seus discos.</span><span class="sxs-lookup"><span data-stu-id="cc64d-117">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="cc64d-118">É recomendável toouse uma API versão posterior `2016-04-30-preview` como houve alterações significativas entre `2016-04-30-preview` e `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="cc64d-118">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="cc64d-119">Configurações de disco gerenciados padrão</span><span class="sxs-lookup"><span data-stu-id="cc64d-119">Default managed disk settings</span></span>

<span data-ttu-id="cc64d-120">toocreate uma VM com discos gerenciados, você não precisar de recursos de conta de armazenamento toocreate hello e pode atualizar o recurso de máquina virtual da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="cc64d-120">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="cc64d-121">Especificamente, observe que Olá `apiVersion` reflete `2017-03-30` e hello `osDisk` e `dataDisks` não mais se referir tooa URI específico para Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="cc64d-121">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="cc64d-122">Ao implantar sem especificar propriedades adicionais, disco Olá usará [armazenamento padrão LRS](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="cc64d-122">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="cc64d-123">Se nenhum nome for especificado, ele assume o formato de saudação do `<VMName>_OsDisk_1_<randomstring>` para disco Olá SO e `<VMName>_disk<#>_<randomstring>` para cada disco de dados.</span><span class="sxs-lookup"><span data-stu-id="cc64d-123">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="cc64d-124">Por padrão, a criptografia de disco do Azure está desabilitada; o cache é leitura/gravação para disco Olá SO e nenhum para discos de dados.</span><span class="sxs-lookup"><span data-stu-id="cc64d-124">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="cc64d-125">Você pode perceber no exemplo hello abaixo que se ainda há uma dependência de conta de armazenamento, embora isso seja somente para armazenamento de diagnóstico e não é necessário para armazenamento em disco.</span><span class="sxs-lookup"><span data-stu-id="cc64d-125">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="cc64d-126">Utilizar um recurso de disco gerenciado de nível superior</span><span class="sxs-lookup"><span data-stu-id="cc64d-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="cc64d-127">Como uma configuração de disco de Olá toospecifying alternativa no objeto de máquina virtual hello, você pode criar um recurso de disco de nível superior e anexá-lo como parte da criação da máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="cc64d-127">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="cc64d-128">Por exemplo, podemos criar um recurso de disco da seguinte maneira toouse como um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="cc64d-128">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

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

<span data-ttu-id="cc64d-129">No objeto da VM Olá, podemos podem fazer referência a esta toobe de objeto de disco anexado.</span><span class="sxs-lookup"><span data-stu-id="cc64d-129">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="cc64d-130">Especificando a ID de recurso de saudação do hello gerenciados disco criamos em Olá `managedDisk` propriedade permite que o anexo de saudação do disco hello como Olá VM é criada.</span><span class="sxs-lookup"><span data-stu-id="cc64d-130">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="cc64d-131">Observe que Olá `apiVersion` para Olá recursos da VM é definido muito`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="cc64d-131">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="cc64d-132">Observe também que criamos uma dependência em Olá tooensure de recursos de disco que é criado com êxito antes da criação de VM.</span><span class="sxs-lookup"><span data-stu-id="cc64d-132">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="cc64d-133">Criar conjuntos de disponibilidade gerenciados com VMs utilizando discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="cc64d-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="cc64d-134">toocreate gerenciados disponibilidade conjuntos com VMs usando discos gerenciados, adicione Olá `sku` disponibilidade do objeto toohello definir recursos e definir Olá `name` propriedade muito`Aligned`.</span><span class="sxs-lookup"><span data-stu-id="cc64d-134">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="cc64d-135">Isso garante que discos Olá para cada VM sejam suficientemente isolados de outro tooavoid pontos únicos de falha.</span><span class="sxs-lookup"><span data-stu-id="cc64d-135">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="cc64d-136">Observe também que Olá `apiVersion` para disponibilidade de saudação do conjunto de recursos está definido muito`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="cc64d-136">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="cc64d-137">Cenários e personalizações adicionais</span><span class="sxs-lookup"><span data-stu-id="cc64d-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="cc64d-138">informações completas toofind especificações de API REST hello, analise Olá [criar um disco gerenciado documentação da API REST](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="cc64d-138">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="cc64d-139">Você encontrará cenários adicionais, bem como padrão e os valores aceitáveis que podem ser enviados toohello API por meio de implantações de modelo.</span><span class="sxs-lookup"><span data-stu-id="cc64d-139">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cc64d-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc64d-140">Next steps</span></span>

* <span data-ttu-id="cc64d-141">Para modelos completos que usam discos gerenciados visite Olá seguindo os links de repositório de início rápido do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc64d-141">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="cc64d-142">VM do Windows VM com disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="cc64d-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="cc64d-143">VM do Linux VM com disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="cc64d-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="cc64d-144">Lista completa de modelos de disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="cc64d-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="cc64d-145">Visite Olá [visão geral do Azure gerenciados discos](../articles/virtual-machines/windows/managed-disks-overview.md) documento toolearn mais sobre discos de gerenciado.</span><span class="sxs-lookup"><span data-stu-id="cc64d-145">Visit hello [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="cc64d-146">Examine a documentação de referência de modelo Olá para recursos da máquina virtual visitando Olá [referência de modelo Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) documento.</span><span class="sxs-lookup"><span data-stu-id="cc64d-146">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="cc64d-147">Examine a documentação de referência de modelo Olá para recursos de disco visitando Olá [referência de modelo Microsoft.Compute/disks](/templates/microsoft.compute/disks) documento.</span><span class="sxs-lookup"><span data-stu-id="cc64d-147">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
