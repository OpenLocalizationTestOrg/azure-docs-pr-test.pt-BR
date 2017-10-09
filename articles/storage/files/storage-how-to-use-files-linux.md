---
title: aaaUse armazenamento de arquivo do Azure com Linux | Microsoft Docs
description: Saiba como toomount um arquivo Azure compartilhar no SMB no Linux.
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Usar o Armazenamento de Arquivos do Azure com o Linux
[Armazenamento de arquivo do Azure](../storage-dotnet-how-to-use-files.md) é o sistema de arquivos de nuvem da Microsoft toouse fácil. Compartilhamentos de arquivos do Azure podem ser montados em distribuições do Linux usando Olá [pacote Utilitários cifs](https://wiki.samba.org/index.php/LinuxCIFS_utils) de saudação [projeto Samba](https://www.samba.org/). Este artigo mostra toomount de duas maneiras de um compartilhamento de arquivos do Azure: sob demanda com hello `mount` de comando e de inicialização, criando uma entrada em `/etc/fstab`.

> [!NOTE]  
> Ordem toomount um compartilhamento de arquivos do Azure fora Olá região do Azure que está hospedado, como no local ou em uma região diferente do Azure, Olá SO deve oferecer suporte a funcionalidade de criptografia de saudação do SMB 3.0. O recurso de criptografia do SMB 3.0 para Linux foi introduzido no kernel 4.11. Este recurso permite a montagem do Compartilhamento de Arquivos do Azure do local ou de uma região diferente do Azure. Em tempo de saudação da publicação, essa funcionalidade foi backported tooUbuntu de 16.04 e acima.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Pré-requisitos para montar um compartilhamento de arquivos do Azure com Linux e hello pacote de utilitários de cifs
* **Escolher uma distribuição de Linux que pode ter o pacote de utilitários cifs Olá instalado**: a Microsoft recomenda Olá distribuições do Linux na Galeria de imagens do Azure Olá a seguir:

    * Ubuntu Server 14.04+
    * RHEL 7+
    * CentOS 7+
    * Debian 8
    * openSUSE 13.2+
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Olá cifs utilitários pacote é instalado**: Olá cifs-utilitários podem ser instalados usando o Gerenciador de pacotes de saudação na distribuição de Linux Olá de sua escolha. 

    Em **Ubuntu** e **com base em Debian** distribuições, use Olá `apt-get` Gerenciador de pacotes:

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    Em **RHEL** e **CentOS**, use Olá `yum` Gerenciador de pacotes:

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    Em **openSUSE**, use Olá `zypper` Gerenciador de pacotes:

    ```
    sudo zypper install samba*
    ```

    Em outras distribuições, usar o Gerenciador de pacote apropriado hello ou [de compilação do código-fonte](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Decidir sobre as permissões de diretório/arquivo hello do compartilhamento montado Olá**: exemplos de saudação abaixo, usamos 0777, toogive ler, gravar e executar permissões tooall os usuários. Você pode substituí-las por outras [permissões chmod](https://en.wikipedia.org/wiki/Chmod) se desejar. 

* **Nome da conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o nome da conta de armazenamento hello.

* **Chave de conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o chave de armazenamento primária (ou secundário). Atualmente, as chaves SAS não têm suporte para montagem.

* **Certifique-se de que a porta 445 está aberta**: SMB se comunica pela porta TCP 445 - verificar toosee se o firewall não está bloqueando o TCP portas 445 do computador cliente.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Montar Olá sob demanda com compartilhamento de arquivos do Azure`mount`
1. **[Instalar o pacote de utilitários cifs Olá para a sua distribuição Linux](#install-cifs-utils)**.

2. **Crie uma pasta para o ponto de montagem Olá**: isso pode ser feito em qualquer lugar no sistema de arquivo hello.

    ```
    mkdir mymountpoint
    ```

3. **Compartilhamento de arquivo do Azure Use Olá montagem comando toomount Olá**: Lembre-se de tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` com informações apropriadas hello.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Quando você terminar de usar Olá compartilhamento de arquivos do Azure, você pode usar `sudo umount ./mymountpoint` toounmount compartilhamento de saudação.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Criar um ponto de montagem persistente para o compartilhamento de arquivos do Azure Olá`/etc/fstab`
1. **[Instalar o pacote de utilitários cifs Olá para a sua distribuição Linux](#install-cifs-utils)**.

2. **Crie uma pasta para o ponto de montagem Olá**: isso pode ser feito em qualquer lugar no sistema de arquivos hello, mas você precisa toonote Olá absoluto caminho da pasta de saudação. saudação de exemplo a seguir cria uma pasta raiz.

    ```
    sudo mkdir /mymountpoint
    ```

3. **A seguir use Olá comando Olá tooappend seguinte linha muito`/etc/fstab`**: Lembre-se de tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` com informações apropriadas hello.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> Você pode usar `sudo mount -a` toomount hello Azure compartilhamento após a edição `/etc/fstab` em vez de reinicialização.

## <a name="feedback"></a>Comentários
Os usuários do Linux, queremos toohear de você!

Olá armazenamento de arquivo do Azure para o grupo de usuários do Linux fornece um fórum para você tooshare comentários como avaliar e adotar o armazenamento de arquivo em Linux. Email [armazenamento de arquivo do Azure os usuários do Linux](mailto:azurefileslinuxusers@microsoft.com) grupo toojoin Olá dos usuários.

## <a name="next-steps"></a>Próximas etapas
Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.
* [Referência à API REST do serviço de arquivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Como toouse AzCopy com o armazenamento do Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Usando Olá CLI do Azure com o armazenamento do Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Perguntas frequentes](../storage-files-faq.md)
* [Solução de problemas](storage-troubleshoot-linux-file-connection-problems.md)
