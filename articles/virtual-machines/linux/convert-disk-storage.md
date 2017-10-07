---
title: "aaaConvert Azure gerenciados armazenamento de discos de padrão toopremium e vice-versa | Microsoft Docs"
description: "Como tooconvert Azure gerenciada armazenamento de discos de toopremium padrão e vice-versa, usando a CLI do Azure."
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Converter Azure discos de armazenamento gerenciada do toopremium padrão e vice-versa

Os Managed Disks oferecem duas opções de armazenamento: [Premium](../../storage/storage-premium-storage.md) (baseado em SSD) e [Padrão](../../storage/storage-standard-storage.md) (baseado em HDD). Ele permite que você tooeasily alternar entre as opções de saudação dois com tempo de inatividade mínimo com base em suas necessidades de desempenho. Ele não está disponível para discos não gerenciados. Mas você pode facilmente [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily alternar entre as opções de saudação dois.

Este artigo mostra como tooconvert gerenciada discos de toopremium padrão e vice-versa, usando a CLI do Azure. Se você precisa tooinstall ou atualizá-lo, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli.md). 

## <a name="before-you-begin"></a>Antes de começar

* conversão Olá exige uma reinicialização do hello VM, agende para migração de saudação do seu armazenamento de discos durante uma janela de manutenção já existente. 
* Se você estiver usando discos não gerenciados, primeiro [converter discos toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch este artigo entre as opções de armazenamento Olá dois. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Converter todos os Olá gerenciados discos de uma VM do toopremium padrão e vice-versa

Saudação de exemplo a seguir, mostramos como tooswitch todos Olá discos de máquina virtual do armazenamento toopremium padrão. discos de premium toouse gerenciado, a VM deve usar um [tamanho da VM](sizes.md) que oferece suporte ao armazenamento premium. Este exemplo também alterna tamanho tooa que dá suporte ao armazenamento premium.

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Converter um disco gerenciado de toopremium padrão e vice-versa

Para sua carga de trabalho de desenvolvimento/teste, talvez você queira toohave mistura de discos standard e premium tooreduce seu custo. Para fazer isso por meio da atualização toopremium armazenamento, somente os discos de saudação que exigem um melhor desempenho. Saudação de exemplo a seguir, mostramos como tooswitch um único disco de máquina virtual do armazenamento toopremium padrão e vice-versa. discos de premium toouse gerenciado, a VM deve usar um [tamanho da VM](sizes.md) que oferece suporte ao armazenamento premium. Este exemplo também alterna tamanho tooa que dá suporte ao armazenamento premium.

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a>Próximas etapas

Faça uma cópia somente leitura de uma VM usando [instantâneos](snapshot-copy-managed-disk.md).

