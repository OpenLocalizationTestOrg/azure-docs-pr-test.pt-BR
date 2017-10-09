---
title: armazenamento de arquivo do Azure em VMs do Linux usando SMB de aaaMount | Microsoft Docs
description: Como toomount armazenamento de arquivo do Azure em VMs do Linux usando SMB com hello 2.0 do CLI do Azure
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>Montar o Armazenamento de Arquivos do Azure em VMs Linux usando SMB

Este artigo mostra como Olá tooutilize serviço de armazenamento de arquivo do Azure em uma VM do Linux usando SMB montar com hello 2.0 do CLI do Azure. Armazenamento de arquivo do Azure oferece compartilhamentos de arquivos na nuvem hello usando o protocolo SMB padrão de saudação. Você também pode executar essas etapas com hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). requisitos de saudação são:

- [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/)
- [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md)

## <a name="quick-commands"></a>Comandos rápidos

* Um grupo de recursos
* Uma Rede virtual do Azure
* Um grupo de segurança de rede com uma entrada SSH
* Uma sub-rede
* Uma conta de armazenamento do Azure
* Chaves de conta de armazenamento do Azure
* Um compartilhamento do Armazenamento de arquivos do Azure
* Uma VM do Linux

Substitua os exemplos por suas próprias configurações.

### <a name="create-a-directory-for-hello-local-mount"></a>Crie um diretório de montagem local Olá

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>Armazenamento de arquivo hello SMB compartilhamento toohello montagem ponto de montagem

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Manter Olá montagem após uma reinicialização
toodo, então, adicionar Olá toohello linha a seguir `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado

Armazenamento de arquivos oferece os compartilhamentos de arquivos na nuvem Olá que usam protocolo SMB padrão de saudação. Com a versão mais recente de saudação do armazenamento de arquivos, você também pode montar um compartilhamento de arquivos de qualquer sistema operacional que dá suporte a SMB 3.0. Quando você usa uma montagem SMB no Linux, você obter backups fácil tooa robusto e permanente arquivamento local de armazenamento que é suportado por um SLA.

Movendo os arquivos de uma montagem SMB tooan VM que é hospedada no armazenamento de arquivo é que uma ótima maneira toodebug logs. Isso ocorre porque Olá compartilhamento SMB mesmo pode ser montado localmente tooyour estação de trabalho de Mac, Linux ou Windows. SMB não é a melhor solução Olá para streaming Linux ou logs do aplicativo em tempo real, porque Olá protocolo SMB não está compilado toohandle tais direitos pesada de registro em log. Uma ferramenta de camada de log unificada dedicada, como o Fluentd, poderá ser uma escolha melhor em relação ao SMB para coletar a saída de log do Linux e de aplicativo.

Para este passo a passo detalhada, criamos pré-requisitos Olá necessário toofirst criar compartilhamento de armazenamento de arquivo hello e, em seguida, recriá-lo por meio do SMB em uma VM Linux.

1. Criar um grupo de recursos com [criar grupo az](/cli/azure/group#create) toohold compartilhamento de arquivos de saudação.

    toocreate um grupo de recursos denominado `myResourceGroup` em Olá local "US West", use Olá exemplo a seguir:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Criar uma conta de armazenamento do Azure com [criar conta de armazenamento az](/cli/azure/storage/account#create) toostore Olá arquivos reais.

    toocreate uma conta de armazenamento denominada mystorageaccount usando o armazenamento de Standard_LRS Olá SKU, use Olá exemplo a seguir:

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Mostra chaves de conta de armazenamento hello.

    Quando você cria uma conta de armazenamento, chaves de conta Olá são criadas em pares para que eles podem ser girados sem qualquer interrupção do serviço. Quando você alternar toohello segunda chave no par hello, você pode criar um novo par de chaves. Novas chaves de conta de armazenamento sempre são criadas em pares, garantindo que você sempre tenha pelo menos um armazenamento não usado conta chave pronto tooswitch para.

    Exibir chaves de conta de armazenamento Olá com hello [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list). Olá chaves de conta de armazenamento para Olá chamado `mystorageaccount` são listadas na saudação de exemplo a seguir:

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract uma única chave, use Olá `--query` sinalizador. Olá, exemplo a seguir extrai chave primeiro hello (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Crie compartilhamento de armazenamento de arquivo hello.

    compartilhamento de armazenamento de arquivo Hello contém Olá compartilhamento SMB com [criar compartilhamento de armazenamento az](/cli/azure/storage/share#create). cota de saudação sempre é expresso em gigabytes (GB). Passar em uma das chaves de saudação da saudação anterior `az storage account keys list` comando. Crie um compartilhamento chamado mystorageshare com uma cota de 10 GB usando Olá exemplo a seguir:

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. Crie um diretório de ponto de montagem.

    Crie um diretório local no Olá Olá Linux arquivo sistema toomount compartilhamento de SMB. Qualquer coisa gravados ou lidos do diretório de montagem local de saudação é encaminhada toohello compartilhamento SMB que é hospedado no armazenamento de arquivo. toocreate um diretório local no /mnt/Retention/ mymountdirectory, use Olá exemplo a seguir:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Monte o diretório local de toohello Olá de compartilhamento SMB.

    Fornece seu próprio nome de usuário de conta de armazenamento e a chave de conta de armazenamento de credenciais de montagem de saudação da seguinte maneira:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. Manter Olá montar SMB por meio de reinicializações.

    Quando você reinicializa Olá VM do Linux, hello montado compartilhamento SMB é desmontado durante o desligamento. Olá tooremount compartilhamento SMB na inicialização, adicionar uma linha de toohello /etc/fstab Linux. Linux usa Olá fstab arquivo toolist Olá sistemas de arquivos que ele precisa toomount durante o processo de inicialização hello. Adicionando compartilhamento SMB Olá garante que esse compartilhamento de armazenamento de arquivo hello é um sistema de arquivos montados permanentemente para Olá VM do Linux. Adicionando Olá arquivo armazenamento SMB compartilhamento tooa nova VM é possível quando você usa a inicialização de nuvem.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Próximas etapas

- [Usando a nuvem init toocustomize uma VM do Linux durante a criação](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Adicionar um disco tooa VM do Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Criptografar discos em uma VM Linux usando Olá CLI do Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
