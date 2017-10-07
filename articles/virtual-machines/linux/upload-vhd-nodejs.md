---
title: aaaUpload uma imagem personalizada do Linux com o Azure CLI 1.0 | Microsoft Docs
description: "Criar e carregar tooAzure um disco rígido virtual (VHD) com uma imagem personalizada do Linux usando o modelo de implantação do Gerenciador de recursos de saudação e hello 1.0 da CLI do Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a>Carregar e criar uma VM do Linux de imagem de disco personalizada usando Olá 1.0 da CLI do Azure
Este artigo mostra como tooupload um disco rígido virtual (VHD) usando o tooAzure Olá modelo de implantação do Gerenciador de recursos e criar VMs do Linux usando essa imagem personalizada. Essa funcionalidade permite que você tooinstall e configurar um requisitos de tooyour de distribuição do Linux e, em seguida, usar esse VHD tooquickly criar máquinas virtuais (VMs) do Azure.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="quick-commands"></a>Comandos rápidos
Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção a seguir base tooupload comandos tooAzure uma VM. Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#requirements).

Certifique-se de que você tenha [hello Azure CLI 1.0](../../cli-install-nodejs.md) conectado e usando o modo do Gerenciador de recursos:

```azurecli
azure config mode arm
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `myimages`.

Em primeiro lugar, crie um grupo de recursos. Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `WestUs` local:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

Crie um toohold de conta de armazenamento seus discos virtuais. Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount`:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

Lista Olá chaves de acesso para sua conta de armazenamento. Anote `key1`:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

Crie um recipiente dentro de sua conta de armazenamento usando a chave de armazenamento de saudação obtidos. Olá, exemplo a seguir cria um contêiner denominado `myimages` usando o valor de chave de armazenamento de saudação do `key1`:

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

Por fim, carregue seu contêiner de toohello VHD que você criou. Especificar Olá caminho local tooyour VHD em `/path/to/disk/mydisk.vhd`:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

Agora você pode criar uma VM do disco virtual carregado [usando um modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd). Você também pode usar o hello CLI especificando o disco do hello URI tooyour (`--image-urn`). Olá, exemplo a seguir cria uma VM denominada `myVM` usando o disco virtual de saudação carregado anteriormente:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

conta de armazenamento de destino Olá tem toobe Olá mesmo como em que você carregou o disco virtual para. Você também precisa toospecify ou responder a prompts para, todos os parâmetros adicionais exigidos pelo Olá de Olá `azure vm create` comando, como a rede virtual, o endereço IP público, o nome de usuário e as chaves de SSH. Você pode ler mais sobre Olá [parâmetros disponíveis do Gerenciador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Requisitos
Olá toocomplete seguintes etapas, você precisa:

* **Sistema operacional Linux instalado em um arquivo. vhd** -instalar um [distribuição aprovadas Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa o disco virtual no hello VHD formato. Várias ferramentas existem toocreate uma VM e o VHD:
  * Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando cuidado toouse VHD como seu formato de imagem. Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.
  * Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Não há suporte para o formato VHDX mais recente de saudação no Azure. Quando você cria uma máquina virtual, especifique o VHD como formato de saudação. Se necessário, você pode converter tooVHD de discos VHDX usando [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell. Além disso, Azure não oferece suporte Carregando VHDs dinâmicos, portanto, você precisa tooconvert toostatic esses discos VHDs antes de carregar. Você pode usar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) discos dinâmicos de tooconvert durante o processo de saudação de carregamento de tooAzure.
> 
> 

* Máquinas virtuais criadas de sua imagem personalizada devem residir no hello mesmo conta de armazenamento como a própria imagem Olá
  * Criar um toohold de conta e o contêiner de armazenamento sua imagem personalizada e VMs criadas
  * Depois de criar todas as VMs, você poderá excluir a imagem com segurança

Certifique-se de que você tenha [hello Azure CLI 1.0](../../cli-install-nodejs.md) conectado e usando o modo do Gerenciador de recursos:

```azurecli
azure config mode arm
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `myimages`.

<a id="prepimage"> </a>

## <a name="prepare-hello-image-toobe-uploaded"></a>Preparar Olá imagem toobe carregado
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


## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Grupos de recursos logicamente reunir toosupport de recursos do Azure Olá todas as suas máquinas virtuais, como redes virtuais hello e armazenamento. Leia mais sobre os [grupos de recursos do Azure aqui](../../azure-resource-manager/resource-group-overview.md). Antes de carregar a imagem de disco personalizada e criar máquinas virtuais, você primeiro precisa toocreate um grupo de recursos. 

Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `WestUS` local:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
As VMs são armazenadas como blobs de páginas em uma conta de armazenamento. Leia mais sobre o [armazenamento de blobs do Azure aqui](../../storage/common/storage-introduction.md#blob-storage). Você cria uma conta de armazenamento para suas VMs e imagem de disco personalizadas. Todas as máquinas virtuais que você criar a partir de seu toobe de necessidade de imagem de disco personalizada no Olá a mesma conta de armazenamento, como essa imagem.

Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount` no grupo de recursos de saudação criado anteriormente:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a>Listar chaves da conta de armazenamento
O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento. Essas chaves de acesso são usadas ao autenticar a conta de armazenamento de toohello, como toocarry operações de gravação. Leia mais sobre [gerenciando acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Você pode exibir as chaves de acesso com hello `azure storage account keys list` comando.

Exibir chaves de acesso Olá Olá conta de armazenamento criada:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
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
Em Olá mesma maneira que você crie diferentes diretórios toologically organizar seu sistema de arquivos local, crie contêineres dentro de um tooorganize de conta de armazenamento seus discos virtuais e imagens. Uma conta de armazenamento pode conter qualquer quantidade de contêineres. 

Olá, exemplo a seguir cria um contêiner denominado `myimages`, especificando a chave de acesso de saudação obtido na etapa anterior de saudação (`key1`):

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a>Carregar o VHD
Agora, você pode efetivamente carregar sua imagem de disco personalizada. Assim como ocorre com todos os discos virtuais usados pelas VMs, você carrega e armazenará sua imagem de disco personalizada como um blob de páginas.

Especifique sua chave de acesso, o contêiner de saudação criado na etapa anterior hello e hello, em seguida, a imagem de disco personalizada toohello caminho no computador local:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a>Criar uma VM com base em uma imagem personalizada
Quando você criar VMs de sua imagem de disco personalizada, especifique a imagem de disco de toohello URI de saudação. Certifique-se de que Olá correspondências de conta de armazenamento de destino onde a imagem de disco personalizada está armazenada. Você pode criar sua VM usando o modelo de CLI do Azure ou o Gerenciador de recursos de JSON de saudação.

### <a name="create-a-vm-using-hello-azure-cli"></a>Criar uma VM usando Olá CLI do Azure
Especificar Olá `--image-urn` o parâmetro hello `azure vm create` imagem do comando toopoint tooyour disco personalizada. Certifique-se de que `--storage-account-name` correspondências Olá conta de armazenamento onde a imagem de disco personalizada está armazenada. Você não tem toouse Olá mesmo contêiner como Olá toostore de imagem de disco personalizada suas VMs. Fazer toocreate se qualquer contêiner adicional em Olá mesma maneira que Olá etapas anteriores antes de carregar as imagens de disco personalizada.

Olá, exemplo a seguir cria uma VM denominada `myVM` da imagem do disco personalizada:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

Você ainda precisa toospecify ou responder a prompts para, todos os parâmetros adicionais exigidos pelo Olá de Olá `azure vm create` comando, como a rede virtual, o endereço IP público, o nome de usuário e as chaves de SSH. Leia mais sobre Olá [parâmetros disponíveis do Gerenciador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

### <a name="create-a-vm-using-a-json-template"></a>Criar uma VM usando um modelo JSON
Modelos do Gerenciador de recursos do Azure são arquivos de notação JSON (JavaScript Object) que definem o ambiente Olá desejar toobuild. modelos de saudação são divididos em toodifferent provedores de recursos, como computação ou rede. Você pode usar os modelos existentes ou escrever seus próprios. Saiba mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).

Dentro de saudação `Microsoft.Compute/virtualMachines` provedor do seu modelo, você tem um `storageProfile` nó que contém os detalhes de configuração Olá para sua VM. Olá dois parâmetros principais tooedit são Olá `image` e `vhd` URIs do ponto de imagem de disco personalizada tooyour e disco virtual da VM seu novo. a seguir Olá mostra um exemplo de hello JSON para usar uma imagem de disco personalizado:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

Você pode usar [este toocreate de modelo existente uma VM por meio de uma imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou leia sobre [criar seus próprios modelos do Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Uma vez que um modelo configurado, você cria suas VMs usando Olá `azure group deployment create` comando. Especifique Olá URI do seu modelo de JSON com hello `--template-uri` parâmetro:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

Se você tiver um arquivo JSON armazenado localmente no seu computador, você pode usar o hello `--template-file` parâmetro em vez disso:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Próximas etapas
Depois de preparar e carregar seu disco virtual personalizado, leia mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md). Você também pode desejar muito[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs. Se você tiver aplicativos em execução em suas VMs que você precisa tooaccess, certifique-se muito[abrir portas e os pontos de extremidade](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

