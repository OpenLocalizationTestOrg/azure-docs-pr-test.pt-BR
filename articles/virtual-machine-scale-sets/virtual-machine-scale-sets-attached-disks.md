---
title: aaaAzure discos de dados anexado do Virtual Machine escala conjuntos | Microsoft Docs
description: "Saiba como toouse anexou discos de dados com conjuntos de escala de máquinas virtuais"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Conjuntos de Dimensionamento de VMs do Azure e discos de dados anexados
Azure [conjuntos de escala de máquina virtual](/azure/virtual-machine-scale-sets/) agora oferecem suporte a máquinas virtuais com discos de dados anexado. Discos de dados podem ser definidos no perfil de armazenamento Olá para conjuntos de escala que foram criadas com discos gerenciado do Azure. Anteriormente hello somente opções de armazenamento diretamente conectado disponíveis com VMs em conjuntos de escala foram unidade Olá sistema operacional e unidades temporárias.

> [!NOTE]
>  Quando você cria uma escala com discos de dados anexados definidos, você ainda precisará toomount e Olá formato discos de dentro de uma VM toouse-los (assim como para autônomo VMs do Azure). Uma maneira conveniente toodo trata toouse uma extensão de script personalizado que chama um script padrão toopartition e formatar todos os discos de dados de saudação em uma máquina virtual.

## <a name="create-a-scale-set-with-attached-data-disks"></a>Criar uma escala com discos de dados anexados
Um toocreate de maneira simples definir uma escala com discos conectados é Olá toouse [CLI do Azure](https://github.com/Azure/azure-cli) _vmss criar_ comando. saudação de exemplo a seguir cria um grupo de recursos do Azure e um conjunto de escala VM de 10 Ubuntu máquinas virtuais, cada um com discos de dados anexados 2, de 50 GB e 100 GB, respectivamente.
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
Observe que Olá _vmss criar_ comando padrões determinados valores de configuração se você não especificá-los. toosee Olá as opções disponíveis que você pode substituir tente:
```bash
az vmss create --help
```
Outro toocreate de maneira um com discos de dados anexados a escala é toodefine uma escala definida em um modelo do Azure Resource Manager, inclua um _dataDisks_ seção Olá _storageProfile_e implantar Olá modelo. 50 GB e 100 GB disco exemplo Hello acima seria definido como esse modelo hello:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
Você pode ver um exemplo completo e pronto toodeploy de um modelo de conjunto de escala com um disco anexado definido aqui: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>Adicionar uma escala existente do tooan de disco de dados definido
> [!NOTE]
>  Você pode anexar apenas conjunto escala de tooa de discos de dados que foi criado com [discos gerenciado do Azure](./virtual-machine-scale-sets-managed-disks.md).

Você pode adicionar uma escala VM dados disco tooa definida usando a CLI do Azure _anexar disco de vmss az_ comando. Especifique um lun que ainda não esteja em uso. Olá CLI de exemplo a seguir adiciona uma unidade de 50 GB toolun 3:
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

Olá PowerShell de exemplo a seguir adiciona uma unidade de 50 GB toolun 3:
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> Diferentes tamanhos de VM tem limites diferentes em números de saudação de unidades conectadas que dão suporte. Verificar Olá [características de tamanho de máquina virtual](../virtual-machines/windows/sizes.md) antes de adicionar um novo disco.

Você também pode adicionar um disco com a adição de um novo toohello de entrada _dataDisks_ propriedade Olá _storageProfile_ de uma escala de conjunto de definição e aplicar alterações de saudação. tootest, encontrar uma definição de conjunto de escala existente no hello [Gerenciador de recursos do Azure](https://resources.azure.com/). Selecione _editar_ e adicionar uma nova lista de toohello de disco de discos de dados. Por exemplo usando o exemplo hello acima:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

Em seguida, selecione _colocar_ tooapply Olá altera o conjunto de escala de tooyour. Este exemplo funcionaria enquanto você estiver usando um tamanho VM que oferece suporte a mais de dois discos de dados anexado.

> [!NOTE]
> Quando você faz uma escala de tooa alteração definição como adicionar ou remover um disco de dados, aplica VMs tooall recentemente criado, mas só se aplica tooexisting VMs se hello _upgradePolicy_ propriedade está definida muito "automática". Se ele for definido muito "Manual", você precisa toomanually aplicar tooexisting de modelo novo Olá VMs. Você pode fazer isso no portal de saudação usando Olá _atualização AzureRmVmssInstance_ PowerShell ou usando Olá _az vmss update-instâncias_ comando CLI.

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>Adicionar discos de dados preenchida previamente tooan escala existente definido 
> Quando você adiciona discos tooan existente conjunto de escala de modelo, por design, Olá disco sempre será criado vazio. Este cenário também inclui novas instâncias criadas pelo conjunto de escala de saudação. Esse comportamento ocorre porque a definição de scaleset Olá tem um disco de dados vazio. Em ordem toocreate dados preenchida previamente unidades para um modelo de conjunto de escala existente, você pode escolher qualquer uma das duas opções:

* Copie dados de saudação instância 0 VM toohello os discos de dados em Olá outras VMs executando um script personalizado.
* Criar uma imagem gerenciada com disco Olá sistema operacional e disco de dados (com dados Olá necessário) e criar um novo scaleset com imagem hello. Dessa forma, cada nova VM criada terá um dados em disco que é fornecida na definição de saudação do hello scaleset. Desde que essa definição fará referência tooan imagem com um disco de dados que tiver personalizado a dados, todas as máquinas virtuais em Olá scaleset automaticamente aparecerá com essas alterações.

> Olá toocreate de forma que uma imagem personalizada pode ser encontrada aqui: [criar uma imagem gerenciada de uma VM generalizada no Azure](/azure/virtual-machines/windows/capture-image-resource/) 

> Olá, o usuário deve toocapture Olá instância VM 0 que tem Olá dados necessários e, em seguida, usar esse vhd para definição de imagem hello.

## <a name="removing-a-data-disk-from-a-scale-set"></a>Remoção de um disco de dados de um conjunto de escala
Você pode remover um disco de dados de um conjunto de dimensionamento de VM usando o comando _az vmss disk detach_ da CLI. Por exemplo hello comando a seguir remove Olá disco definido no lun 2:
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
Da mesma forma você também pode remover um disco de uma escala de conjunto, removendo uma entrada de saudação _dataDisks_ propriedade Olá _storageProfile_ e aplicar a alteração de saudação. 

## <a name="additional-notes"></a>Observações adicionais
Suporte para discos de dados anexados do conjunto de discos gerenciado do Azure e a escala está disponível na versão da API [ _2016-04-30-visualização_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) ou posterior do hello API Microsoft. Compute.

Saudação inicial de implementação de suporte de disco anexado para conjuntos de escala, você não pode anexar ou desanexar discos de dados para/de VMs individuais em um conjunto de escala.

Suporte do portal do Azure para discos de dados anexados em conjuntos de escala é limitada inicialmente. Dependendo dos requisitos, que você pode usar modelos do Azure, PowerShell, CLI, SDKs e API REST toomanage discos conectados.


