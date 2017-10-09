---
title: aaaCreate e carregar um VHD Linux tooAzure | Microsoft Docs
description: "Criar e carregar um Azure disco rígido virtual (VHD) que contém o sistema de operacional Linux hello usando o modelo de implantação clássico Olá"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a>Criando e carregando um disco rígido Virtual que contém Olá o sistema operacional Linux
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Você também pode [carregar uma imagem de disco personalizada usando o Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este artigo mostra como toocreate e carregar um disco rígido virtual (VHD) para que você pode usá-lo como sua própria imagem toocreate as máquinas virtuais no Azure. Saiba como tooprepare hello, você pode usar toocreate várias máquinas virtuais com base em imagem. 


## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você tenha Olá itens a seguir:

* **Sistema operacional Linux instalado em um arquivo. vhd** -você instalou um [distribuição aprovadas Azure Linux](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) disco virtual tooa no formato VHD hello. Várias ferramentas existem toocreate uma VM e o VHD:
  * Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando cuidado toouse VHD como seu formato de imagem. Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.
  * Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Não há suporte para o formato VHDX mais recente de saudação no Azure. Quando você cria uma máquina virtual, especifique o VHD como formato de saudação. Se necessário, você pode converter tooVHD de discos VHDX usando [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell. Além disso, Azure não oferece suporte Carregando VHDs dinâmicos, portanto, você precisa tooconvert toostatic esses discos VHDs antes de carregar. Você pode usar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) discos dinâmicos de tooconvert durante o processo de saudação de carregamento de tooAzure.

* **Interface de linha de comando do Azure** -Olá de instalação mais recente [Interface de linha de comando do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) Olá tooupload VHD.

<a id="prepimage"> </a>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a>Etapa 1: Preparar Olá imagem toobe carregado
O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Olá artigos a seguir orientam você na como tooprepare Olá várias distribuições do Linux com suporte no Azure. Depois de concluir as etapas de Olá Olá guias a seguir, volte aqui uma vez que um arquivo VHD que está pronto tooupload tooAzure:

* **[Distribuições com base em CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Outros — Distribuições não endossadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

> [!NOTE]
> Olá SLA da plataforma Windows Azure se aplica a máquinas toovirtual executando Olá sistema operacional somente quando uma saudação aprovados distribuições do Linux é usado com os detalhes de configuração Olá conforme especificado em 'Versões com suporte' em [Linux em distribuições Azure-Endorsed ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Todas as distribuições do Linux na Galeria de imagens do Azure de saudação são endossadas distribuições com a configuração solicitada hello.
> 
> 

Consulte também Olá  **[notas de instalação Linux](../create-upload-generic.md#general-linux-installation-notes)**  mais geral dicas sobre como preparar imagens do Linux do Azure.

<a id="connect"> </a>

## <a name="step-2-prepare-hello-connection-tooazure"></a>Etapa 2: Preparar Olá conexão tooAzure
Verifique se está usando Olá CLI do Azure no modelo de implantação clássico hello (`azure config mode asm`), em seguida, faça logon no tooyour conta:

```azurecli
azure login
```


<a id="upload"> </a>

## <a name="step-3-upload-hello-image-tooazure"></a>Etapa 3: Carregar Olá imagem tooAzure
É necessário um tooupload de conta de armazenamento para seu arquivo VHD para. Você pode escolher uma conta de armazenamento existente ou [criar uma nova](../../../storage/common/storage-create-storage-account.md).

Use imagem de Olá Olá CLI do Azure tooupload usando Olá comando a seguir:

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

No exemplo anterior de saudação:

* **BlobStorageURL** é URL Olá Olá conta de armazenamento planejar toouse
* **YourImagesFolder** é o contêiner Olá no armazenamento de blob onde você deseja toostore suas imagens
* **VHDName** é Olá rótulo que aparece no portal tooidentify saudação do disco rígido virtual.
* **PathToVHDFile** é o caminho completo do hello e nome do arquivo. vhd de saudação em seu computador.

saudação de comando a seguir mostra um exemplo completo:

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a>Etapa 4: Criar uma VM da imagem Olá
Criar uma VM usando `azure vm create` em Olá mesma forma que uma VM regular. Especifique o nome de saudação você deu a imagem na etapa anterior hello. Saudação de exemplo a seguir, usamos Olá **myImage** nome de imagem fornecido na etapa anterior hello:

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

toocreate suas próprias VMs, fornecer seu próprio nome de usuário + senha local, nome DNS e nome da imagem.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte [referência da CLI do Azure para o modelo de implantação clássico do Azure Olá](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
