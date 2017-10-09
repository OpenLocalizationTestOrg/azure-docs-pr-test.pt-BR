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
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="84c1a-103">Usar o Armazenamento de Arquivos do Azure com o Linux</span><span class="sxs-lookup"><span data-stu-id="84c1a-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="84c1a-104">[Armazenamento de arquivo do Azure](../storage-dotnet-how-to-use-files.md) é o sistema de arquivos de nuvem da Microsoft toouse fácil.</span><span class="sxs-lookup"><span data-stu-id="84c1a-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="84c1a-105">Compartilhamentos de arquivos do Azure podem ser montados em distribuições do Linux usando Olá [pacote Utilitários cifs](https://wiki.samba.org/index.php/LinuxCIFS_utils) de saudação [projeto Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="84c1a-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="84c1a-106">Este artigo mostra toomount de duas maneiras de um compartilhamento de arquivos do Azure: sob demanda com hello `mount` de comando e de inicialização, criando uma entrada em `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="84c1a-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="84c1a-107">Ordem toomount um compartilhamento de arquivos do Azure fora Olá região do Azure que está hospedado, como no local ou em uma região diferente do Azure, Olá SO deve oferecer suporte a funcionalidade de criptografia de saudação do SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="84c1a-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="84c1a-108">O recurso de criptografia do SMB 3.0 para Linux foi introduzido no kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="84c1a-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="84c1a-109">Este recurso permite a montagem do Compartilhamento de Arquivos do Azure do local ou de uma região diferente do Azure.</span><span class="sxs-lookup"><span data-stu-id="84c1a-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="84c1a-110">Em tempo de saudação da publicação, essa funcionalidade foi backported tooUbuntu de 16.04 e acima.</span><span class="sxs-lookup"><span data-stu-id="84c1a-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="84c1a-111">Pré-requisitos para montar um compartilhamento de arquivos do Azure com Linux e hello pacote de utilitários de cifs</span><span class="sxs-lookup"><span data-stu-id="84c1a-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="84c1a-112">**Escolher uma distribuição de Linux que pode ter o pacote de utilitários cifs Olá instalado**: a Microsoft recomenda Olá distribuições do Linux na Galeria de imagens do Azure Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="84c1a-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="84c1a-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="84c1a-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="84c1a-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="84c1a-114">RHEL 7+</span></span>
    * <span data-ttu-id="84c1a-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="84c1a-115">CentOS 7+</span></span>
    * <span data-ttu-id="84c1a-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="84c1a-116">Debian 8</span></span>
    * <span data-ttu-id="84c1a-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="84c1a-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="84c1a-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="84c1a-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="84c1a-119"><a id="install-cifs-utils"></a>**Olá cifs utilitários pacote é instalado**: Olá cifs-utilitários podem ser instalados usando o Gerenciador de pacotes de saudação na distribuição de Linux Olá de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="84c1a-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="84c1a-120">Em **Ubuntu** e **com base em Debian** distribuições, use Olá `apt-get` Gerenciador de pacotes:</span><span class="sxs-lookup"><span data-stu-id="84c1a-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="84c1a-121">Em **RHEL** e **CentOS**, use Olá `yum` Gerenciador de pacotes:</span><span class="sxs-lookup"><span data-stu-id="84c1a-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="84c1a-122">Em **openSUSE**, use Olá `zypper` Gerenciador de pacotes:</span><span class="sxs-lookup"><span data-stu-id="84c1a-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="84c1a-123">Em outras distribuições, usar o Gerenciador de pacote apropriado hello ou [de compilação do código-fonte](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="84c1a-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="84c1a-124">**Decidir sobre as permissões de diretório/arquivo hello do compartilhamento montado Olá**: exemplos de saudação abaixo, usamos 0777, toogive ler, gravar e executar permissões tooall os usuários.</span><span class="sxs-lookup"><span data-stu-id="84c1a-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="84c1a-125">Você pode substituí-las por outras [permissões chmod](https://en.wikipedia.org/wiki/Chmod) se desejar.</span><span class="sxs-lookup"><span data-stu-id="84c1a-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="84c1a-126">**Nome da conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o nome da conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="84c1a-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="84c1a-127">**Chave de conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o chave de armazenamento primária (ou secundário).</span><span class="sxs-lookup"><span data-stu-id="84c1a-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="84c1a-128">Atualmente, as chaves SAS não têm suporte para montagem.</span><span class="sxs-lookup"><span data-stu-id="84c1a-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="84c1a-129">**Certifique-se de que a porta 445 está aberta**: SMB se comunica pela porta TCP 445 - verificar toosee se o firewall não está bloqueando o TCP portas 445 do computador cliente.</span><span class="sxs-lookup"><span data-stu-id="84c1a-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="84c1a-130">Montar Olá sob demanda com compartilhamento de arquivos do Azure`mount`</span><span class="sxs-lookup"><span data-stu-id="84c1a-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="84c1a-131">**[Instalar o pacote de utilitários cifs Olá para a sua distribuição Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="84c1a-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="84c1a-132">**Crie uma pasta para o ponto de montagem Olá**: isso pode ser feito em qualquer lugar no sistema de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="84c1a-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="84c1a-133">**Compartilhamento de arquivo do Azure Use Olá montagem comando toomount Olá**: Lembre-se de tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` com informações apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="84c1a-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="84c1a-134">Quando você terminar de usar Olá compartilhamento de arquivos do Azure, você pode usar `sudo umount ./mymountpoint` toounmount compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="84c1a-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="84c1a-135">Criar um ponto de montagem persistente para o compartilhamento de arquivos do Azure Olá`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="84c1a-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="84c1a-136">**[Instalar o pacote de utilitários cifs Olá para a sua distribuição Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="84c1a-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="84c1a-137">**Crie uma pasta para o ponto de montagem Olá**: isso pode ser feito em qualquer lugar no sistema de arquivos hello, mas você precisa toonote Olá absoluto caminho da pasta de saudação.</span><span class="sxs-lookup"><span data-stu-id="84c1a-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="84c1a-138">saudação de exemplo a seguir cria uma pasta raiz.</span><span class="sxs-lookup"><span data-stu-id="84c1a-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="84c1a-139">**A seguir use Olá comando Olá tooappend seguinte linha muito`/etc/fstab`**: Lembre-se de tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` com informações apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="84c1a-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="84c1a-140">Você pode usar `sudo mount -a` toomount hello Azure compartilhamento após a edição `/etc/fstab` em vez de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="84c1a-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="84c1a-141">Comentários</span><span class="sxs-lookup"><span data-stu-id="84c1a-141">Feedback</span></span>
<span data-ttu-id="84c1a-142">Os usuários do Linux, queremos toohear de você!</span><span class="sxs-lookup"><span data-stu-id="84c1a-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="84c1a-143">Olá armazenamento de arquivo do Azure para o grupo de usuários do Linux fornece um fórum para você tooshare comentários como avaliar e adotar o armazenamento de arquivo em Linux.</span><span class="sxs-lookup"><span data-stu-id="84c1a-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="84c1a-144">Email [armazenamento de arquivo do Azure os usuários do Linux](mailto:azurefileslinuxusers@microsoft.com) grupo toojoin Olá dos usuários.</span><span class="sxs-lookup"><span data-stu-id="84c1a-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84c1a-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="84c1a-145">Next steps</span></span>
<span data-ttu-id="84c1a-146">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="84c1a-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="84c1a-147">Referência à API REST do serviço de arquivos</span><span class="sxs-lookup"><span data-stu-id="84c1a-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="84c1a-148">Como toouse AzCopy com o armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="84c1a-148">How toouse AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="84c1a-149">Usando Olá CLI do Azure com o armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="84c1a-149">Using hello Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="84c1a-150">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="84c1a-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="84c1a-151">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="84c1a-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
