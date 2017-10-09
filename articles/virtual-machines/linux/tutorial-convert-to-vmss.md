---
title: conjunto de escala de tooa uma VM do Azure aaaConvert | Microsoft Docs
description: "Crie e implante uma escala de máquina virtual do Linux Azure com hello CLI do Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>Converter um conjunto de escala de tooa de máquina virtual do Azure existente

Este tutorial mostra como tooconvert toouse 2.0 do CLI do Azure uma escala de máquina virtual de tooa de máquina virtual configurada. Você também aprenderá como definir a configuração de saudação tooautomate de máquinas virtuais de saudação na escala de saudação. Para obter mais informações sobre como tooinstall CLI do Azure 2.0, consulte [guia de Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Para obter mais informações sobre conjuntos de dimensionamento, confira [Conjuntos de Dimensionamento de Máquina Virtual](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-hello-vm"></a>Etapa 1 - Olá desprovisionamento VM

Use SSH tooconnect toohello VM.

Saudação de desprovisionamento VM usando hello Azure VM agent toodelete arquivos e dados. Para obter uma visão geral detalhada do cancelamento do provisionamento, consulte [Capturar uma máquina virtual Linux](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>Etapa 2 - capturar uma imagem de VM de saudação

Para obter uma visão geral detalhada da captura, consulte [Capturar uma máquina virtual Linux](capture-image.md).

Desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Generalize Olá VM com [az vm generalizar](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Criar uma imagem do recurso VM Olá com [criar imagem az](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>Etapa 3 - criar conjunto de escala Olá

Obter Olá **id** da imagem de saudação.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

Crie uma VM com base no recurso de imagem com [az vmss create](/cli/azure/vmss#create):

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

Esse comando também anexou um disco de dados de 10 GB. Tenha em mente que, dependendo da saudação VM tamanho escolhido (usamos **Standard_DS1_v2**), Olá número de discos de dados permitido é diferente. Para obter mais informações, examine Olá [tamanhos de máquina virtual](sizes.md).

Depois que o conjunto de escala de saudação for concluída, conecte-se tooit. Obter uma lista de endereços IP para instâncias de saudação para SSH com [az vmss lista-instância-conexão-info](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Agora você pode conectar um disco de dados saudação do tooinitialize de instância de máquina virtual toohello

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>Etapa 4 - disco de dados Olá inicializar

Enquanto a máquina virtual de toohello conectado, particionar o disco de saudação com `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Gravar uma partição de toohello do sistema de arquivos com hello `mkfs` comando:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Monte o disco novo Olá para que seja acessível no sistema operacional de saudação:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

disco Olá agora pode ser acessa por meio de montagem de datadrive hello, que pode ser verificado com `ls /datadrive/`.

Olá encerrar a sessão SSH.


## <a name="step-5---configure-firewall"></a>Etapa 5 – Configurar o firewall

Fazem uma tachinha Olá firewall toohello servidor da Web hospedado pelo conjunto de escala de saudação. Quando o conjunto de escala Olá foi criado, um balanceador de carga também foi criado e você o usou **SSH** toohello máquinas virtuais. tooopen uma porta, você precisa de duas informações, que pode ser obtido usando a CLI do Azure.

* **Pool de endereços IP de front-end**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Pool de endereços IP de back-end**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Com esses dois nomes, você pode abrir a porta **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Etapa 6 – Automatizar a configuração

disco de dados Olá precisa toobe configurado em cada instância de máquina virtual. É possível automatizar a configuração de Olá da máquina virtual Olá Olá **CustomScript** extensão.

Primeiro, crie um *. sh* script que inclui comandos de formatação de disco hello.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Em seguida, carregar esse Olá de toowhere do arquivo de script **CustomScript** extensão pode acessá-lo. Uma cópia está disponível [aqui](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Crie um arquivo local chamado **settings.json** e coloque hello seguinte bloco JSON nele. Olá `flieUris` propriedade deve ser definida como toowhere carregado o arquivo de script.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Implantar essa escala de tooyour de comando com hello **CustomScript** extensão, referenciando Olá **settings.json** arquivo que acabamos de criar.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

Essa extensão é executada automaticamente em todas as instâncias e em todas as instâncias criadas posteriormente pelo dimensionamento.

## <a name="step-7---configure-autoscale-rules"></a>Etapa 7 – Configurar regras de dimensionamento automático

Atualmente, as regras de dimensionamento automático não podem ser definidas na CLI do Azure. Saudação de uso [portal do Azure](https://portal.azure.com) tooconfigure AutoEscala.

## <a name="step-8---management-tasks"></a>Etapa 8 – Tarefas de gerenciamento

Ciclo de vida de saudação do conjunto de escala hello, talvez seja necessário toorun uma ou mais tarefas de gerenciamento. Além disso, convém toocreate scripts que automatizam várias tarefas de ciclo de vida e Olá CLI do Azure fornece uma maneira rápida toodo essas tarefas. Estas são algumas tarefas comuns.

### <a name="get-connection-info"></a>Obter informações de conexão

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>Definir a contagem de instâncias (escala manual)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>Excluir grupo de recursos

Excluir um grupo de recursos exclui todos os recursos contidos nele.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre escala de máquinas virtuais Olá definir recursos apresentados neste tutorial, consulte Olá informações a seguir:

- [Visão geral dos conjuntos de dimensionamento de máquinas virtuais do Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Visão geral do Azure Load Balancer](../../load-balancer/load-balancer-overview.md)
- [Controlar o fluxo de tráfego de rede com grupos de segurança de rede](../../virtual-network/virtual-networks-nsg.md)