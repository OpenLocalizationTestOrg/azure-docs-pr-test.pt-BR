---
title: aaaUpload um disco Linux personalizada com o Azure CLI 2.0 | Microsoft Docs
description: "Criar e carregar um tooAzure de disco rígido virtual (VHD) usando o modelo de implantação do Gerenciador de recursos de saudação e hello 2.0 do CLI do Azure"
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Carregar e criar uma VM do Linux do disco personalizado com hello 2.0 do CLI do Azure
Este artigo mostra como tooupload tooan um disco rígido virtual (VHD) armazenamento do Azure a conta com hello 2.0 do CLI do Azure e criar VMs do Linux no disco personalizado. Você também pode executar essas etapas com hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Essa funcionalidade permite que você tooinstall e configurar um requisitos de tooyour de distribuição do Linux e, em seguida, usar esse VHD tooquickly criar máquinas virtuais (VMs) do Azure.

Este tópico usa contas de armazenamento para hello VHDs finais, mas você também pode fazer essas etapas usando [discos gerenciado](upload-vhd.md). 

## <a name="quick-commands"></a>Comandos rápidos
Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção a seguir base tooupload comandos tooAzure um VHD. Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#requirements).

Certifique-se de que você tenha mais recente Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `mydisks`.

Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `WestUs` local:

```azurecli
az group create --name myResourceGroup --location westus
```

Criar um toohold de conta de armazenamento discos virtuais com [criar conta de armazenamento az](/cli/azure/storage/account#create). Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount`:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

Listar Olá chaves de acesso para sua conta de armazenamento com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list). Anote `key1`:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

Criar um recipiente dentro de sua conta de armazenamento usando a chave de armazenamento de saudação obtidas com [criar contêiner de armazenamento az](/cli/azure/storage/container#create). Olá, exemplo a seguir cria um contêiner denominado `mydisks` usando o valor de chave de armazenamento de saudação do `key1`:

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

Por fim, carregar o contêiner de toohello VHD criado com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload). Especificar Olá caminho local tooyour VHD em `/path/to/disk/mydisk.vhd`:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

Especifique Olá URI tooyour disco (`--image`) com [criar vm az](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada `myVM` usando o disco virtual de saudação carregado anteriormente:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

conta de armazenamento de destino Olá tem toobe Olá mesmo como em que você carregou o disco virtual para. Você também precisa toospecify ou responder a prompts para, todos os parâmetros adicionais exigidos pelo Olá de Olá **criar vm az** comando, como a rede virtual, o endereço IP público, o nome de usuário e as chaves de SSH. Você pode ler mais sobre Olá [parâmetros disponíveis do Gerenciador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Requisitos
Olá toocomplete seguintes etapas, você precisa:

* **Sistema operacional Linux instalado em um arquivo. vhd** -instalar um [distribuição aprovadas Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa o disco virtual no hello VHD formato. Várias ferramentas existem toocreate uma VM e o VHD:
  * Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando cuidado toouse VHD como seu formato de imagem. Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.
  * Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Não há suporte para o formato VHDX mais recente de saudação no Azure. Quando você cria uma máquina virtual, especifique o VHD como formato de saudação. Se necessário, você pode converter tooVHD de discos VHDX usando [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell. Além disso, Azure não oferece suporte Carregando VHDs dinâmicos, portanto, você precisa tooconvert toostatic esses discos VHDs antes de carregar. Você pode usar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) discos dinâmicos de tooconvert durante o processo de saudação de carregamento de tooAzure.
> 
> 

* Máquinas virtuais criadas do disco de dados personalizado devem residir no hello mesmo conta de armazenamento como o próprio disco Olá
  * Criar um toohold de conta e o contêiner de armazenamento, seu disco personalizado e VMs criadas
  * Depois de criar todas as VMs, você poderá excluir o disco com segurança

Certifique-se de que você tenha mais recente Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `mydisks`.

<a id="prepimage"> </a>

## <a name="prepare-hello-disk-toobe-uploaded"></a>Preparar Olá disco toobe carregado
O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Olá artigos a seguir orientam você pelo como tooprepare Olá várias distribuições do Linux com suporte no Azure.

* **[Distribuições com base em CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Outros — Distribuições não endossadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Consulte também Olá  **[notas de instalação Linux](create-upload-generic.md#general-linux-installation-notes)**  mais geral dicas sobre como preparar imagens do Linux do Azure.

> [!NOTE]
> Olá [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica-se tooVMs executando o Linux somente quando uma saudação aprovados distribuições é usado com os detalhes de configuração Olá conforme especificado em 'Versões com suporte' [Linux no Azure aprovadas Distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Grupos de recursos logicamente reunir toosupport de recursos do Azure Olá todas as suas máquinas virtuais, como redes virtuais hello e armazenamento. Mais informações sobre grupos de recursos, veja [visão geral de grupos de recurso](../../azure-resource-manager/resource-group-overview.md). Antes de carregar o disco personalizado e criar máquinas virtuais, é necessário primeiro toocreate um grupo de recursos com [criar grupo az](/cli/azure/group#create).

Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westus` local:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Criar uma conta de armazenamento para seu disco personalizado e VMs com [az storage account create](/cli/azure/storage/account#create). Todas as máquinas virtuais com discos não gerenciados que você cria com seu toobe de necessidade de disco personalizada no Olá a mesma conta de armazenamento que esse disco. 

Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount` no grupo de recursos de saudação criado anteriormente:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a>Listar chaves da conta de armazenamento
O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento. Essas chaves de acesso são usadas ao autenticar a conta de armazenamento de toohello, como toocarry operações de gravação. Leia mais sobre [gerenciando acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Exibir chaves de acesso de saudação com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).

Exibir chaves de acesso Olá Olá conta de armazenamento criada:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
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
Anote `key1` como você o usará toointeract com as próximas etapas Olá sua conta de armazenamento.

## <a name="create-a-storage-container"></a>Criar um contêiner de armazenamento
Em Olá mesma maneira que você crie diferentes diretórios toologically organizar seu sistema de arquivos local, crie contêineres dentro de um tooorganize de conta de armazenamento seus discos. Uma conta de armazenamento pode conter qualquer quantidade de contêineres. Crie um contêiner com [az storage container create](/cli/azure/storage/container#create).

Olá, exemplo a seguir cria um contêiner denominado `mydisks`:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a>Carregar o VHD
Agora, carregue seu disco personalizado com [az storage blob upload](/cli/azure/storage/blob#upload). Carregue e armazene seu disco personalizado como um blob de páginas.

Especifique sua chave de acesso, o contêiner de saudação criado na etapa anterior hello e, em seguida, Olá disco personalizada do caminho toohello no computador local:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a>Criar hello VM
toocreate uma VM com discos não gerenciados, especifique o disco de tooyour do URI de saudação (`--image`) com [criar vm az](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada `myVM` usando o disco virtual de saudação carregado anteriormente:

Especificar Olá `--image` parâmetro com [criar vm az](/cli/azure/vm#create) toopoint tooyour personalizado disco. Certifique-se de que `--storage-account` correspondências Olá conta de armazenamento onde o disco personalizado é armazenado. Você não tem toouse Olá mesmo contêiner como Olá disco personalizada toostore suas VMs. Fazer toocreate se qualquer contêiner adicional em Olá mesma maneira que Olá etapas anteriores antes de carregar o disco personalizado.

Olá, exemplo a seguir cria uma VM denominada `myVM` do disco personalizado:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

Você ainda precisa toospecify ou responder a prompts para, todos os parâmetros adicionais exigidos pelo Olá de Olá **criar vm az** comando, como o nome de usuário e as chaves de SSH.


## <a name="resource-manager-template"></a>Modelo do Resource Manager
Modelos do Gerenciador de recursos do Azure são arquivos de notação JSON (JavaScript Object) que definem o ambiente Olá desejar toobuild. modelos de saudação são divididos em toodifferent provedores de recursos, como computação ou rede. Você pode usar os modelos existentes ou escrever seus próprios. Saiba mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).

Dentro de saudação `Microsoft.Compute/virtualMachines` provedor do seu modelo, você tem um `storageProfile` nó que contém os detalhes de configuração Olá para sua VM. Olá dois parâmetros principais tooedit são Olá `image` e `vhd` URIs que aponte disco personalizada tooyour e disco virtual da VM seu novo. a seguir Olá mostra um exemplo de hello JSON para usar um disco personalizado:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Você pode usar [este toocreate de modelo existente uma VM por meio de uma imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou leia sobre [criar seus próprios modelos do Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Quando você tiver um modelo configurado, usar [criar implantação de grupo az](/cli/azure/group/deployment#create) toocreate suas VMs. Especifique Olá URI do seu modelo de JSON com hello `--template-uri` parâmetro:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

Se você tiver um arquivo JSON armazenado localmente no seu computador, você pode usar o hello `--template-file` parâmetro em vez disso:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Próximas etapas
Depois de preparar e carregar seu disco virtual personalizado, leia mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md). Você também pode desejar muito[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs. Se você tiver aplicativos em execução em suas VMs que você precisa tooaccess, certifique-se muito[abrir portas e os pontos de extremidade](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

