---
title: Usar o Armazenamento de Arquivos do Azure com o Linux | Microsoft Docs
description: Saiba como montar um Compartilhamento de Arquivos do Azure com SMB no Linux.
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
ms.openlocfilehash: d8987082c559a374b8d19fd69e20cf5e81cb25ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="6648a-103">Usar o Armazenamento de Arquivos do Azure com o Linux</span><span class="sxs-lookup"><span data-stu-id="6648a-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="6648a-104">O [Armazenamento de arquivos do Azure](../storage-dotnet-how-to-use-files.md) é o sistema de arquivos de nuvem de fácil acesso da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6648a-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="6648a-105">Compartilhamentos de Arquivos do Azure podem ser montados em distribuições do Linux usando o [pacote cifs-utils](https://wiki.samba.org/index.php/LinuxCIFS_utils) do [projeto Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="6648a-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="6648a-106">Este artigo mostra duas maneiras de montar um Compartilhamento de Arquivos do Azure: sob demanda com o comando `mount` e na inicialização criando uma entrada em `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="6648a-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="6648a-107">Para montar um Compartilhamento de Arquivos do Azure fora da região do Azure no qual ele está hospedado, como local ou em uma região diferente do Azure, o sistema operacional deve dar suporte à funcionalidade de criptografia do SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="6648a-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="6648a-108">O recurso de criptografia do SMB 3.0 para Linux foi introduzido no kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="6648a-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="6648a-109">Este recurso permite a montagem do Compartilhamento de Arquivos do Azure do local ou de uma região diferente do Azure.</span><span class="sxs-lookup"><span data-stu-id="6648a-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="6648a-110">No momento da publicação deste artigo, essa funcionalidade foi retrocompatibilizada para o Ubuntu 16.04 e superior.</span><span class="sxs-lookup"><span data-stu-id="6648a-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="6648a-111">Pré-requisitos para montar um Compartilhamento de Arquivos do Azure com o Linux e o pacote cifs-utils</span><span class="sxs-lookup"><span data-stu-id="6648a-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="6648a-112">**Escolha uma distribuição do Linux que pode ter o pacote cifs-utils instalado**: a Microsoft recomenda as seguintes distribuições do Linux na Galeria de imagens do Azure:</span><span class="sxs-lookup"><span data-stu-id="6648a-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="6648a-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="6648a-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="6648a-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="6648a-114">RHEL 7+</span></span>
    * <span data-ttu-id="6648a-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="6648a-115">CentOS 7+</span></span>
    * <span data-ttu-id="6648a-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="6648a-116">Debian 8</span></span>
    * <span data-ttu-id="6648a-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="6648a-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="6648a-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="6648a-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="6648a-119"><a id="install-cifs-utils"></a>**O pacote cifs-utils é instalado**: o cifs-utils pode ser instalado usando o gerenciador de pacotes na distribuição do Linux escolhida.</span><span class="sxs-lookup"><span data-stu-id="6648a-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="6648a-120">Em distribuições **Ubuntu** e **Debian**, use o gerenciador de pacotes do `apt-get`:</span><span class="sxs-lookup"><span data-stu-id="6648a-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="6648a-121">No **RHEL** e **CentOS**, use o gerenciador de pacotes do `yum`:</span><span class="sxs-lookup"><span data-stu-id="6648a-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="6648a-122">No **openSUSE**, use o gerenciador de pacotes do `zypper`:</span><span class="sxs-lookup"><span data-stu-id="6648a-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="6648a-123">Em outras distribuições, use o gerenciador de pacotes apropriado ou [compile do código-fonte](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="6648a-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="6648a-124">**Decida as permissões de diretório/arquivo do compartilhamento montado**: nos exemplos abaixo, usamos 0777 para conceder as permissões de leitura, gravação e execução para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="6648a-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="6648a-125">Você pode substituí-las por outras [permissões chmod](https://en.wikipedia.org/wiki/Chmod) se desejar.</span><span class="sxs-lookup"><span data-stu-id="6648a-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="6648a-126">**Nome da conta de armazenamento**: para montar um compartilhamento de arquivos do Azure, você precisará do nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6648a-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="6648a-127">**Chave de conta de armazenamento**: para montar um compartilhamento de arquivos do Azure, você precisará da chave de armazenamento primária (ou secundária).</span><span class="sxs-lookup"><span data-stu-id="6648a-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="6648a-128">Atualmente, as chaves SAS não têm suporte para montagem.</span><span class="sxs-lookup"><span data-stu-id="6648a-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="6648a-129">**Verifique se a porta 445 está aberta**: o SMB se comunica pela porta TCP 445, por isso confira se o firewall não está bloqueando as portas TCP 445 do computador cliente.</span><span class="sxs-lookup"><span data-stu-id="6648a-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="6648a-130">Montar o Compartilhamento de Arquivos do Azure sob demanda com `mount`</span><span class="sxs-lookup"><span data-stu-id="6648a-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="6648a-131">**[Instale o pacote cifs-utils para sua distribuição Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="6648a-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="6648a-132">**Crie uma pasta para o ponto de montagem**: isso pode ser feito em qualquer lugar no sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="6648a-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="6648a-133">**Use o comando de montagem para montar o Compartilhamento de Arquivos do Azure**: lembre-se de substituir `<storage-account-name>`, `<share-name>` e `<storage-account-key>` pelas informações apropriadas.</span><span class="sxs-lookup"><span data-stu-id="6648a-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="6648a-134">Quando tiver terminado de usar o Compartilhamento de Arquivos do Azure, você pode usar `sudo umount ./mymountpoint` para desmontar o compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="6648a-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="6648a-135">Criar um ponto de montagem persistente para o Compartilhamento de Arquivos do Azure com `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="6648a-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="6648a-136">**[Instale o pacote cifs-utils para sua distribuição Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="6648a-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="6648a-137">**Crie uma pasta para o ponto de montagem**: isso pode ser feito em qualquer lugar no sistema de arquivos, mas você precisa observar o caminho absoluto da pasta.</span><span class="sxs-lookup"><span data-stu-id="6648a-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="6648a-138">O exemplo a seguir cria uma pasta na raiz.</span><span class="sxs-lookup"><span data-stu-id="6648a-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="6648a-139">**Use este comando para acrescentar a linha a seguir a `/etc/fstab`**: lembre-se de substituir `<storage-account-name>`, `<share-name>` e `<storage-account-key>` pelas informações apropriadas.</span><span class="sxs-lookup"><span data-stu-id="6648a-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="6648a-140">Você pode usar `sudo mount -a` para montar o Compartilhamento de Arquivos do Azure após a edição de `/etc/fstab` em vez de reinicializar.</span><span class="sxs-lookup"><span data-stu-id="6648a-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="6648a-141">Comentários</span><span class="sxs-lookup"><span data-stu-id="6648a-141">Feedback</span></span>
<span data-ttu-id="6648a-142">Usuários do Linux, queremos ouvir sua opinião!</span><span class="sxs-lookup"><span data-stu-id="6648a-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="6648a-143">O Armazenamento de arquivos do Azure para o grupo de usuários do Linux oferece um fórum para que você possa compartilhar comentários à medida que você avalia e adota o Armazenamento de arquivos no Linux.</span><span class="sxs-lookup"><span data-stu-id="6648a-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="6648a-144">Envie um email [aos usuários do Linux do Armazenamento de Arquivos do Azure](mailto:azurefileslinuxusers@microsoft.com) para participar do grupo de usuários.</span><span class="sxs-lookup"><span data-stu-id="6648a-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6648a-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6648a-145">Next steps</span></span>
<span data-ttu-id="6648a-146">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="6648a-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="6648a-147">Referência à API REST do serviço de arquivos</span><span class="sxs-lookup"><span data-stu-id="6648a-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="6648a-148">Como usar o AzCopy com o Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6648a-148">How to use AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="6648a-149">Usando a CLI do Azure com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="6648a-149">Using the Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="6648a-150">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="6648a-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="6648a-151">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="6648a-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
