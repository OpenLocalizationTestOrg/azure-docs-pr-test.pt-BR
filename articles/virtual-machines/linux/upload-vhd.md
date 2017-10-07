---
title: aaaUpload ou copiar uma VM do Linux personalizado com o Azure CLI 2.0 | Microsoft Docs
description: "Carregar ou copiar uma máquina virtual personalizada usando o modelo de implantação do Gerenciador de recursos de saudação e hello 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Criar uma VM do Linux do disco personalizado com hello 2.0 do CLI do Azure

<!-- rename toocreate-vm-specialized -->

Este artigo mostra como tooupload um disco rígido virtual (VHD) personalizado ou copie um um VHD existente no Azure e criar novas máquinas de virtuais de Linux (VMs) do disco de saudação personalizada. Você pode instalar e configurar um requisitos de tooyour de distribuição do Linux e, em seguida, usar esse VHD tooquickly criar uma nova máquina virtual do Azure.

Se você quiser toocreate várias VMs do disco personalizado, você deve criar uma imagem da VM ou VHD. Para obter mais informações, consulte [criar uma imagem personalizada de uma VM do Azure usando Olá CLI](tutorial-custom-images.md).

Você tem duas opções:
* [Carregar um VHD](#option-1-upload-a-specialized-vhd)
* [Copiar uma VM existente do Azure](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>Comandos rápidos

Ao criar uma nova VM usando [criar vm az](/cli/azure/vm#create) de um disco especializado ou personalizado você **anexar** disco hello (– anexar-disco do SO) em vez de especificar uma imagem personalizada ou marketplace (-imagem). Olá, exemplo a seguir cria uma VM denominada *myVM* usando Olá gerenciado disco chamado *myManagedDisk* criado a partir de seu VHD personalizado:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>Requisitos
Olá toocomplete seguintes etapas, você precisa:

* Uma máquina virtual Linux que foi preparada para uso no Azure. Olá [preparar Olá VM](#prepare-the-vm) este artigo aborda como distribuição de toofind informações específicas sobre como instalar hello Azure Linux Agent (waagent) que é necessária para Olá VM toowork corretamente no Azure e você toobe capaz de tooconnect tooit usando o SSH.
* arquivo VHD de saudação de uma já existente [distribuição aprovadas Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa o disco virtual no formato VHD hello. Várias ferramentas existem toocreate uma VM e o VHD:
  * Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando cuidado toouse VHD como seu formato de imagem. Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando **qemu-img convert**.
  * Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Não há suporte para o formato VHDX mais recente de saudação no Azure. Quando você cria uma máquina virtual, especifique o VHD como formato de saudação. Se necessário, você pode converter tooVHD de discos VHDX usando [qemu img converter](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell. Além disso, Azure não oferece suporte Carregando VHDs dinâmicos, portanto, você precisa tooconvert toostatic esses discos VHDs antes de carregar. Você pode usar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) discos dinâmicos de tooconvert durante o processo de saudação de carregamento de tooAzure.
> 
> 


* Certifique-se de que você tenha mais recente Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Exemplos de nomes de parâmetro incluem *myResourceGroup*, *mystorageaccount* e *mydisks*.

<a id="prepimage"> </a>

## <a name="prepare-hello-vm"></a>Preparar Olá VM

O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Olá artigos a seguir orientam você pelo como tooprepare Olá várias distribuições do Linux com suporte no Azure.

* [Distribuições com base em CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES e openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Outro – distribuições não endossadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Consulte também Olá [notas de instalação Linux](create-upload-generic.md#general-linux-installation-notes) mais geral dicas sobre como preparar imagens do Linux do Azure.

> [!NOTE]
> Olá [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica-se tooVMs executando o Linux somente quando uma saudação aprovados distribuições é usado com os detalhes de configuração Olá conforme especificado em 'Versões com suporte' [Linux no Azure aprovadas Distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="option-1-upload-a-vhd"></a>Opção 1: Carregar um VHD

Você pode carregar um VHD personalizado que esteja em execução em um computador local ou que você tenha exportado de outra nuvem. toouse Olá VHD toocreate uma nova VM do Azure, você precisa de armazenamento de tooa do tooupload Olá VHD da conta e criar um disco gerenciado de saudação VHD. 

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Antes de carregar o disco personalizado e criar máquinas virtuais, é necessário primeiro toocreate um grupo de recursos com [criar grupo az](/cli/azure/group#create).

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local: [visão geral de discos gerenciado do Azure](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Criar uma conta de armazenamento para seu disco personalizado e VMs com [az storage account create](/cli/azure/storage/account#create). 

Olá, exemplo a seguir cria uma conta de armazenamento denominada *mystorageaccount* no grupo de recursos de saudação criado anteriormente:

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>Listar chaves da conta de armazenamento
O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento. Essas chaves de acesso são usadas ao autenticar a conta de armazenamento de toohello, como realizar operações de gravação. Leia mais sobre [gerenciando acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Exibir chaves de acesso de saudação com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).

Exibir chaves de acesso Olá Olá conta de armazenamento criada:

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

saída de Hello é semelhante a:

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
Anote **key1** como você o usará toointeract com as próximas etapas Olá sua conta de armazenamento.

### <a name="create-a-storage-container"></a>Criar um contêiner de armazenamento
Em Olá mesma maneira que você crie diferentes diretórios toologically organizar seu sistema de arquivos local, crie contêineres dentro de um tooorganize de conta de armazenamento seus discos. Uma conta de armazenamento pode conter qualquer quantidade de contêineres. Crie um contêiner com [az storage container create](/cli/azure/storage/container#create).

Olá, exemplo a seguir cria um contêiner denominado *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Carregar Olá VHD
Agora, carregue seu disco personalizado com [az storage blob upload](/cli/azure/storage/blob#upload). Carregue e armazene seu disco personalizado como um blob de páginas.

Especifique sua chave de acesso, o contêiner de saudação criado na etapa anterior hello e, em seguida, Olá disco personalizada do caminho toohello no computador local:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
Carregando Olá VHD pode demorar um pouco.

### <a name="create-a-managed-disk"></a>Criar um disco gerenciado


Criar um disco gerenciado de saudação VHD usando [criar disco az](/cli/azure/disk#create). Olá, exemplo a seguir cria um disco gerenciado chamado *myManagedDisk* de saudação VHD carregado tooyour conta de armazenamento e contêiner:

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>Opção 2: Copiar uma VM existente

Você também pode criar hello VM personalizado no Azure e, em seguida, copiar o disco de saudação SO e anexá-lo tooa nova VM toocreate outra cópia. Isso é bom para teste, mas se você quiser toouse uma VM do Azure existente como modelo Olá para várias novas VMs, você realmente deve criar um **imagem** em vez disso. Para obter mais informações sobre como criar uma imagem de uma VM existente do Azure, consulte [criar uma imagem personalizada de uma VM do Azure usando Olá CLI](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>Criar um instantâneo

Este exemplo cria um instantâneo de uma VM denominada *myVM* no grupo de recursos *myResourceGroup* e cria um instantâneo denominado *osDiskSnapshot*.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Criar disco gerenciado Olá

Crie um novo disco gerenciado de instantâneo de saudação.

Obter ID de saudação do instantâneo hello. Neste exemplo, chamado instantâneo Olá *osDiskSnapshot* e em Olá *myResourceGroup* grupo de recursos.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Crie disco de saudação gerenciado. Neste exemplo, vamos criar um disco gerenciado chamado *myManagedDisk* com base em nosso instantâneo, que tem um tamanho de 128 GB no armazenamento padrão.

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Criar hello VM

Agora, crie a VM com [criar vm az](/cli/azure/vm#create) e anexar (– anexar-disco do SO) Olá gerenciados disco como disco Olá sistema operacional. Olá, exemplo a seguir cria uma VM denominada *myNewVM* usando Olá gerenciado disco criado a partir de seu VHD carregado:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

Você deve ser capaz de tooSSH em Olá VM usando credenciais de saudação do VM de origem hello. 

## <a name="next-steps"></a>Próximas etapas
Depois de preparar e carregar seu disco virtual personalizado, leia mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md). Você também pode desejar muito[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs. Se você tiver aplicativos em execução em suas VMs que você precisa tooaccess, certifique-se muito[abrir portas e os pontos de extremidade](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

