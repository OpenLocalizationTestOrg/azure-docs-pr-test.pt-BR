---
title: aaaMount armazenamento de arquivo do Azure em VMs do Linux usando SMB com 1.0 da CLI do Azure | Microsoft Docs
description: Como toomount armazenamento de arquivo do Azure em VMs do Linux usando o SMB
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
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a>Montar o Armazenamento de arquivos do Azure em VMs Linux ao usar SMB com CLI 1.0 do Azure

Este artigo mostra como toomount armazenamento de arquivo do Azure em uma VM do Linux usando Olá protocolo de bloco de mensagens de servidor (SMB). Armazenamento de arquivos oferece os compartilhamentos de arquivos na nuvem Olá por meio do protocolo SMB padrão de saudação. requisitos de saudação são:

* Uma [conta do Azure](https://azure.microsoft.com/pricing/free-trial/)
* [Arquivos de chave Secure Shell (SSH) pública e privada](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a>CLI versões toouse
Você pode concluir a tarefa de saudação usando uma saudação versões de interface de linha de comando (CLI) a seguir:

- [1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="quick-commands"></a>Comandos rápidos
tarefa de saudação tooaccomplish rapidamente, execute as etapas de saudação nesta seção. Para obter mais informações e o contexto, começam com hello ["Passo a passo detalhado"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) seção.

### <a name="prerequisites"></a>Pré-requisitos
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
Adicionar Olá seguinte linha muito`/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado

Armazenamento de arquivos oferece os compartilhamentos de arquivos na nuvem Olá que usam protocolo SMB padrão de saudação. Com a versão mais recente de saudação do armazenamento de arquivos, você também pode montar um compartilhamento de arquivos de qualquer sistema operacional que dá suporte a SMB 3.0. Quando você usa uma montagem SMB no Linux, você obter backups fácil tooa robusto e permanente arquivamento local de armazenamento que é suportado por um SLA.

Movendo os arquivos de uma montagem SMB tooan VM que é hospedada no armazenamento de arquivo é que uma ótima maneira toodebug logs. Isso ocorre porque Olá compartilhamento SMB mesmo pode ser montado localmente tooyour estação de trabalho de Mac, Linux ou Windows. SMB não é a melhor solução Olá para streaming Linux ou logs do aplicativo em tempo real, porque Olá protocolo SMB não está compilado toohandle tais direitos pesada de registro em log. Uma ferramenta de camada de log unificada dedicada, como o Fluentd, poderá ser uma escolha melhor em relação ao SMB para coletar a saída de log do Linux e de aplicativo.

Para este passo a passo detalhada, criamos pré-requisitos Olá necessário toofirst criar compartilhamento de armazenamento de arquivo hello e, em seguida, recriá-lo por meio do SMB em uma VM Linux.

1. Crie uma conta de armazenamento do Azure usando Olá código a seguir:

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. Mostra chaves de conta de armazenamento hello.

    Quando você cria uma conta de armazenamento, chaves de conta Olá são criadas em pares para que eles podem ser girados sem qualquer interrupção do serviço. Quando você alternar toohello segunda chave no par hello, você pode criar um novo par de chaves. Novas chaves de conta de armazenamento sempre são criadas em pares, garantindo que você sempre tenha pelo menos um armazenamento sem uso chave pronto tooswitch para. chaves de conta de armazenamento do tooshow hello, use Olá código a seguir:

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. Crie compartilhamento de armazenamento de arquivo hello.

    compartilhamento de armazenamento de arquivo Hello contém um compartilhamento SMB hello. cota de saudação sempre é expresso em gigabytes (GB). toocreate Olá compartilhamento de arquivo de armazenamento, use Olá código a seguir:

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. Crie diretório de ponto de montagem de saudação.

    Você deve criar um diretório local no Olá Olá Linux arquivo sistema toomount compartilhamento de SMB. Qualquer coisa gravados ou lidos do diretório de montagem local de saudação é encaminhada toohello compartilhamento SMB que é hospedado no armazenamento de arquivo. diretório de saudação toocreate, use Olá código a seguir:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. Monte Olá compartilhamento SMB usando Olá código a seguir:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. Manter Olá montar SMB por meio de reinicializações.

    Quando você reinicializa Olá VM do Linux, hello montado compartilhamento SMB é desmontado durante o desligamento. compartilhamento SMB tooremount Olá na inicialização, você deve adicionar uma linha de toohello /etc/fstab Linux. Linux usa Olá fstab arquivo toolist Olá sistemas de arquivos que ele precisa toomount durante o processo de inicialização hello. Adicionando compartilhamento SMB Olá garante que esse compartilhamento de armazenamento de arquivo hello é um sistema de arquivos montados permanentemente para Olá VM do Linux. Adicionando Olá arquivo armazenamento SMB compartilhamento tooa nova VM é possível quando você usa a inicialização de nuvem.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Próximas etapas

- [Usando a nuvem init toocustomize uma VM do Linux durante a criação](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Adicionar um disco tooa VM do Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Criptografar discos em uma VM Linux usando Olá CLI do Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
