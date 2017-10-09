# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Utilizar discos gerenciados nos modelos do Azure Resource Manager

Este documento explica como as diferenças de saudação entre discos gerenciados e ao usar máquinas virtuais do Azure Resource Manager modelos tooprovision. Isso ajudará tooupdate modelos existentes que estão usando discos de toomanaged de discos não gerenciados. Para referência, estamos usando Olá [101-vm simples do windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) modelo como um guia. Você pode ver o modelo hello usando [discos gerenciado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) e uma versão anterior usando [não gerenciado discos](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) se você gostaria que toodirectly compará-los.

## <a name="unmanaged-disks-template-formatting"></a>Formatação de modelo de Discos não gerenciados

toobegin, vamos dar uma olhada em discos como não gerenciados são implantados. Durante a criação de discos não gerenciados, é necessário um arquivos VHD do armazenamento conta toohold hello. É possível criar uma nova conta de armazenamento ou utilizar uma conta já existente. Este artigo mostra como toocreate uma nova conta de armazenamento. tooaccomplish isso, é necessário um recurso de conta de armazenamento em bloco de recursos hello, conforme mostrado abaixo.

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

No objeto de máquina virtual hello, precisamos de uma dependência no hello tooensure de conta de armazenamento que ele foi criado antes da máquina virtual de saudação. Dentro de saudação `storageProfile` seção, em seguida, especificamos Olá URI completo do hello local do VHD, que faz referência a conta de armazenamento hello e é necessária para o disco Olá SO e discos de dados. 

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

## <a name="managed-disks-template-formatting"></a>Formatação de modelo de discos gerenciados

Com discos gerenciado do Azure, disco Olá se torna um recurso de nível superior e não requer mais um toobe de conta de armazenamento criada pelo usuário hello. Discos gerenciados primeiro foram expostos no hello `2016-04-30-preview` versão da API, eles estão disponíveis em todas as versões de API subsequentes e agora são o tipo de disco saudação padrão. Olá seções a seguir percorrer as configurações padrão de saudação e detalham de como toofurther personalizar seus discos.

> [!NOTE]
> É recomendável toouse uma API versão posterior `2016-04-30-preview` como houve alterações significativas entre `2016-04-30-preview` e `2017-03-30`.
>
>

### <a name="default-managed-disk-settings"></a>Configurações de disco gerenciados padrão

toocreate uma VM com discos gerenciados, você não precisar de recursos de conta de armazenamento toocreate hello e pode atualizar o recurso de máquina virtual da seguinte maneira. Especificamente, observe que Olá `apiVersion` reflete `2017-03-30` e hello `osDisk` e `dataDisks` não mais se referir tooa URI específico para Olá VHD. Ao implantar sem especificar propriedades adicionais, disco Olá usará [armazenamento padrão LRS](../articles/storage/common/storage-redundancy.md). Se nenhum nome for especificado, ele assume o formato de saudação do `<VMName>_OsDisk_1_<randomstring>` para disco Olá SO e `<VMName>_disk<#>_<randomstring>` para cada disco de dados. Por padrão, a criptografia de disco do Azure está desabilitada; o cache é leitura/gravação para disco Olá SO e nenhum para discos de dados. Você pode perceber no exemplo hello abaixo que se ainda há uma dependência de conta de armazenamento, embora isso seja somente para armazenamento de diagnóstico e não é necessário para armazenamento em disco.

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

### <a name="using-a-top-level-managed-disk-resource"></a>Utilizar um recurso de disco gerenciado de nível superior

Como uma configuração de disco de Olá toospecifying alternativa no objeto de máquina virtual hello, você pode criar um recurso de disco de nível superior e anexá-lo como parte da criação da máquina virtual hello. Por exemplo, podemos criar um recurso de disco da seguinte maneira toouse como um disco de dados.

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

No objeto da VM Olá, podemos podem fazer referência a esta toobe de objeto de disco anexado. Especificando a ID de recurso de saudação do hello gerenciados disco criamos em Olá `managedDisk` propriedade permite que o anexo de saudação do disco hello como Olá VM é criada. Observe que Olá `apiVersion` para Olá recursos da VM é definido muito`2017-03-30`. Observe também que criamos uma dependência em Olá tooensure de recursos de disco que é criado com êxito antes da criação de VM. 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>Criar conjuntos de disponibilidade gerenciados com VMs utilizando discos gerenciados

toocreate gerenciados disponibilidade conjuntos com VMs usando discos gerenciados, adicione Olá `sku` disponibilidade do objeto toohello definir recursos e definir Olá `name` propriedade muito`Aligned`. Isso garante que discos Olá para cada VM sejam suficientemente isolados de outro tooavoid pontos únicos de falha. Observe também que Olá `apiVersion` para disponibilidade de saudação do conjunto de recursos está definido muito`2017-03-30`.

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

### <a name="additional-scenarios-and-customizations"></a>Cenários e personalizações adicionais

informações completas toofind especificações de API REST hello, analise Olá [criar um disco gerenciado documentação da API REST](/rest/api/manageddisks/disks/disks-create-or-update). Você encontrará cenários adicionais, bem como padrão e os valores aceitáveis que podem ser enviados toohello API por meio de implantações de modelo. 

## <a name="next-steps"></a>Próximas etapas

* Para modelos completos que usam discos gerenciados visite Olá seguindo os links de repositório de início rápido do Azure.
    * [VM do Windows VM com disco gerenciado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [VM do Linux VM com disco gerenciado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [Lista completa de modelos de disco gerenciado](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Visite Olá [visão geral do Azure gerenciados discos](../articles/virtual-machines/windows/managed-disks-overview.md) documento toolearn mais sobre discos de gerenciado.
* Examine a documentação de referência de modelo Olá para recursos da máquina virtual visitando Olá [referência de modelo Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) documento.
* Examine a documentação de referência de modelo Olá para recursos de disco visitando Olá [referência de modelo Microsoft.Compute/disks](/templates/microsoft.compute/disks) documento.
 
