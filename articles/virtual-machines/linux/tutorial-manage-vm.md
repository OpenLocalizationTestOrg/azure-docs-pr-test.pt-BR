---
title: aaaCreate e gerenciar VMs do Linux com hello CLI do Azure | Microsoft Docs
description: "Tutorial - criar e gerenciar máquinas virtuais Linux com hello CLI do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>Criar e gerenciar máquinas virtuais Linux com hello CLI do Azure

Máquinas virtuais do Azure fornecem um ambiente de computação totalmente configurável e flexível. Este tutorial aborda itens básicos de implantação de máquina virtual do Azure, como a seleção de um tamanho de VM, seleção de uma imagem de VM e implantação de uma VM. Você aprenderá como:

> [!div class="checklist"]
> * Criar e conectar tooa VM
> * Selecionar e usar imagens de VM
> * Exibir e usar tamanhos específicos de VM
> * Redimensionar uma VM
> * Exibir e compreender o estado da VM


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-resource-group"></a>Criar grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando. 

Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. Você deve criar um grupo de recursos antes de criar uma máquina virtual. Neste exemplo, um grupo de recursos denominado *myResourceGroupVM* é criado no hello *eastus* região. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

grupo de recursos de saudação é especificado ao criar ou modificar uma VM, que pode ser vista em todo este tutorial.

## <a name="create-virtual-machine"></a>Criar máquina virtual

Criar uma máquina virtual com hello [criar vm az](https://docs.microsoft.com/cli/azure/vm#create) comando. 

Há várias opções disponíveis ao criar uma máquina virtual, como a imagem do sistema operacional, as credenciais administrativas e o dimensionamento do disco. Neste exemplo, criaremos uma máquina virtual chamada *myVM* no Ubuntu. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

Uma vez Olá que VM foi criada, Olá CLI do Azure gera informações sobre Olá VM. Anote Olá `publicIpAddress`, esse endereço pode ser usado tooaccess Olá VM. 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>Conecte-se tooVM

Agora você pode conectar toohello VM usando o SSH. Substitua o endereço IP de exemplo hello com hello `publicIpAddress` anotados na etapa anterior hello.

```bash
ssh 52.174.34.95
```

Depois de concluir Olá VM, feche a sessão SSH de hello. 

```bash
exit
```

## <a name="understand-vm-images"></a>Entender as imagens de VM

Olá marketplace do Azure inclui muitas imagens que podem ser usados toocreate VMs. Nas etapas anteriores do hello, uma máquina virtual foi criada usando uma imagem do Ubuntu. Nesta etapa, Olá que CLI do Azure é marketplace de saudação toosearch usado para uma imagem CentOS, que é então usado toodeploy uma segunda máquina virtual.  

toosee uma lista de saudação imagens usadas mais comumente, use Olá [lista de imagens de vm az](/cli/azure/vm/image#list) comando.

```azurecli-interactive 
az vm image list --output table
```

saída do comando Olá retorna imagens da VM mais populares Olá no Azure.

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

Uma lista completa pode ser vista adicionando Olá `--all` argumento. lista de imagens Olá também pode ser filtrada por `--publisher` ou `–-offer`. Neste exemplo, lista de saudação é filtrada para todas as imagens com uma oferta que corresponde a *CentOS*. 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

Resultado parcial:

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

toodeploy uma VM usando uma imagem específica, anote o valor de Olá Olá *Urn* coluna. Ao especificar a imagem de hello, número de versão de imagem Olá pode ser substituído por "mais recente", que seleciona a versão mais recente de saudação da distribuição de saudação. Neste exemplo, Olá `--image` argumento é usado toospecify versão mais recente do hello de uma imagem CentOS 6.5.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>Entender os tamanhos de VM

Um tamanho de máquina virtual determina a quantidade de saudação de recursos de computação, como memória, CPU e GPU que são feitas a máquina virtual de toohello disponíveis. Máquinas virtuais precisam toobe dimensionada apropriadamente para carga de trabalho Olá esperado. Se a carga de trabalho aumentar, uma máquina virtual existente pode ser redimensionada.

### <a name="vm-sizes"></a>Tamanhos de VM

Olá, a tabela a seguir categoriza tamanhos em casos de uso.  

| Tipo                     | Tamanhos           |    Descrição       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Propósito geral](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7| CPU/memória equilibrados. Ideal para desenvolvimento / teste e pequenas toomedium soluções de aplicativos e dados.  |
| [Computação otimizada](sizes-compute.md)   | Fs, F             | Relação de CPU/memória alta. Boa para aplicativos de tráfego médio, dispositivos de rede e processos em lote.        |
| [Memória otimizada](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Relação de memória/núcleo alta. Excelente para bancos de dados relacionais, caches toolarge médios e análise de memória.                 |
| [Armazenamento otimizado](../virtual-machines-windows-sizes-storage.md)      | Ls                | Alta taxa de transferência de disco e de E/S. Ideal para Big Data, SQL e bancos de dados NoSQL.                                                         |
| [GPU](sizes-gpu.md)          | NV, NC            | VMs especializadas, destinadas para renderização gráfica e edição de vídeo pesadas.       |
| [Alto desempenho](sizes-hpc.md) | H, A8-11          | Nossas VMs de CPU mais potentes com adaptadores de rede de alto rendimento (RDMA) opcionais. 


### <a name="find-available-vm-sizes"></a>Encontrar tamanhos de VM disponíveis

toosee uma lista de VM tamanhos disponíveis em uma determinada região, use Olá [lista-tamanhos de vm az](/cli/azure/vm#list-sizes) comando. 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

Resultado parcial:

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>Criar VM com um tamanho específico

No exemplo de criação VM anterior hello, um tamanho não foi fornecida, que resulta em um tamanho padrão. Um tamanho de VM pode ser selecionado no momento da criação usando [criar vm az](/cli/azure/vm#create) e hello `--size` argumento. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>Redimensionar uma VM

Depois que uma máquina virtual foi implantada, pode ser redimensionada tooincrease ou diminuir a alocação de recursos.

Antes de redimensionar uma VM, verifique se hello tamanho desejado está disponível no cluster do Azure atual de saudação. Olá [az vm lista-vm--opções de redimensionamento](/cli/azure/vm#list-vm-resize-options) Olá retorna a lista de tamanhos de comando. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
Se Olá desejado tamanho estiver disponível, hello VM pode ser redimensionada de um estado ligado, mas ele é reinicializado durante a operação de saudação. Saudação de uso [az vm redimensionar]( /cli/azure/vm#resize) comando tooperform Olá redimensionamento.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Se o tamanho desejado de saudação não está em cluster atual hello, Olá VM necessidades toobe desalocada antes da operação de redimensionamento Olá pode ocorrer. Saudação de uso [az vm desalocar]( /cli/azure/vm#deallocate) toostop de comando e desalocar Olá VM. Observe que quando hello VM está ligada novamente, os dados no disco temporário Olá podem ser removidos. endereço IP público de saudação também altera a menos que um endereço IP estático está sendo usado. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

Depois de desalocada, Olá redimensionamento pode ocorrer. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Depois de redimensionar hello, Olá VM pode ser iniciado.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>Estados de energia da VM

Uma VM do Azure pode ter um dentre vários estados de energia. Nesse estado representa o estado atual de saudação do hello VM do ponto de vista de saudação do hipervisor Olá. 

### <a name="power-states"></a>Estados de energia

| Estado de energia | Descrição
|----|----|
| Iniciando | Indica a máquina virtual de hello está sendo iniciada. |
| Executando | Indica que a máquina virtual hello está em execução. |
| Parando | Indica que a máquina virtual hello está sendo interrompida. | 
| Parada | Indica que a máquina virtual hello está parada. Máquinas virtuais no estado interrompido de saudação ainda incorrerá em encargos de computação.  |
| Desalocando | Indica que a máquina virtual hello está sendo desalocada. |
| Desalocada | Indica que a máquina virtual Olá é removido da saudação hipervisor, mas ainda está disponível no plano de controle de saudação. Máquinas virtuais no estado desalocada da saudação não incorrerá em encargos de computação. |
| - | Indica que o estado de energia de saudação da máquina virtual de saudação é desconhecido. |

### <a name="find-power-state"></a>Localizar o estado de energia

estado de saudação tooretrieve de uma VM específica, use Olá [az vm obter exibição de instância](/cli/azure/vm#get-instance-view) comando. Ser toospecify se um nome válido para uma máquina virtual e o grupo de recursos. 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

Saída:

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>Tarefas de gerenciamento

Durante a saudação ciclo de vida de uma máquina virtual, talvez você queira toorun tarefas de gerenciamento como iniciar, parar ou excluir uma máquina virtual. Além disso, talvez você queira toocreate scripts tooautomate repetitivas ou complexas tarefas. Usando Olá CLI do Azure, muitas tarefas comuns de gerenciamento podem ser executadas da linha de comando hello, ou em scripts. 

### <a name="get-ip-address"></a>Como obter o endereço IP

Esse comando retorna os endereços IP públicos e privados de saudação de uma máquina virtual.  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>Como interromper uma máquina virtual

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>Como iniciar uma máquina virtual

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>Excluir grupo de recursos

Excluir um grupo de recursos exclui todos os recursos contidos nele.

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu sobre a criação e o gerenciamento básico de VM e como:

> [!div class="checklist"]
> * Criar e conectar tooa VM
> * Selecionar e usar imagens de VM
> * Exibir e usar tamanhos específicos de VM
> * Redimensionar uma VM
> * Exibir e compreender o estado da VM

Avançar toohello toolearn próximo de tutorial sobre discos de VM.  

> [!div class="nextstepaction"]
> [Criar e gerenciar discos de VM](./tutorial-manage-disks.md)
