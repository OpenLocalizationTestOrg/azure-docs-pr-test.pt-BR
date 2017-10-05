---
title: Copiar ou mover dados para o Armazenamento do Azure com o AzCopy no Linux | Microsoft Docs
description: "Use o utilitário AzCopy no Linux para mover ou copiar dados entre o conteúdo de blob e de arquivo. Copie dados para o Armazenamento do Azure de arquivos locais ou copie dados dentro na mesma conta ou entre contas de armazenamento. Migre facilmente seus dados para o Armazenamento do Azure."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: d17f63dcee590529756d48d699f78b3fb30f973c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="4533d-105">Transferir dados com o AzCopy no Linux</span><span class="sxs-lookup"><span data-stu-id="4533d-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="4533d-106">O AzCopy no Linux é um utilitário de linha de comando projetado para copiar dados entre o armazenamento de Blobs e de Arquivos do Microsoft Azure usando comandos simples com desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="4533d-106">AzCopy on Linux is a command-line utility designed for copying data to and from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="4533d-107">Você pode copiar dados de um objeto para outro dentro de sua conta de armazenamento, ou entre contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4533d-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="4533d-108">Há duas versões do AzCopy que podem ser baixadas.</span><span class="sxs-lookup"><span data-stu-id="4533d-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="4533d-109">O AzCopy no Linux se baseia no .NET Core Framework, que se destina a plataformas Linux que oferecem opções de linha de comando no estilo POSIX.</span><span class="sxs-lookup"><span data-stu-id="4533d-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="4533d-110">O [AzCopy no Windows](storage-use-azcopy.md) se baseia no .NET Framework e oferece opções de linha de comando no estilo Windows.</span><span class="sxs-lookup"><span data-stu-id="4533d-110">[AzCopy on Windows](storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="4533d-111">Este artigo aborda o AzCopy no Linux.</span><span class="sxs-lookup"><span data-stu-id="4533d-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="4533d-112">Baixar e instalar o AzCopy</span><span class="sxs-lookup"><span data-stu-id="4533d-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="4533d-113">Instalação no Linux</span><span class="sxs-lookup"><span data-stu-id="4533d-113">Installation on Linux</span></span>

<span data-ttu-id="4533d-114">O AzCopy no Linux exige o .NET Core Framework na plataforma.</span><span class="sxs-lookup"><span data-stu-id="4533d-114">AzCopy on Linux requires .NET Core framework on the platform.</span></span> <span data-ttu-id="4533d-115">Consulte as instruções de instalação na página do [.NET Core](https://www.microsoft.com/net/core#linuxubuntu).</span><span class="sxs-lookup"><span data-stu-id="4533d-115">See the installation instructions on the [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="4533d-116">Como exemplo, vamos instalar o .NET Core no Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="4533d-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="4533d-117">Para obter o último guia de instalação, visite a página de instalação do [.NET Core no Linux](https://www.microsoft.com/net/core#linuxubuntu).</span><span class="sxs-lookup"><span data-stu-id="4533d-117">For the latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="4533d-118">Depois de instalar o .NET Core, baixe e instale o AzCopy.</span><span class="sxs-lookup"><span data-stu-id="4533d-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="4533d-119">Você poderá remover os arquivos extraídos depois que o AzCopy no Linux for instalado.</span><span class="sxs-lookup"><span data-stu-id="4533d-119">You can remove the extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="4533d-120">Como alternativa, caso você não tenha privilégios de superusuário, também poderá executar o AzCopy usando o script de shell “azcopy” na pasta extraída.</span><span class="sxs-lookup"><span data-stu-id="4533d-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using the shell script 'azcopy' in the extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="4533d-121">Instalação alternativa no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4533d-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="4533d-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="4533d-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="4533d-123">Adicionar fonte de apt ao .Net Core:</span><span class="sxs-lookup"><span data-stu-id="4533d-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="4533d-124">Adicionar fonte de apt ao repositório de produtos do Linux da Microsoft e instale o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4533d-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="4533d-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="4533d-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="4533d-126">Adicionar fonte de apt ao .Net Core:</span><span class="sxs-lookup"><span data-stu-id="4533d-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="4533d-127">Adicionar fonte de apt ao repositório de produtos do Linux da Microsoft e instale o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4533d-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="4533d-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="4533d-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="4533d-129">Adicionar fonte de apt ao .Net Core:</span><span class="sxs-lookup"><span data-stu-id="4533d-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="4533d-130">Adicionar fonte de apt ao repositório de produtos do Linux da Microsoft e instale o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4533d-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="4533d-131">Como escrever seu primeiro comando do AzCopy</span><span class="sxs-lookup"><span data-stu-id="4533d-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="4533d-132">A sintaxe básica dos comandos do AzCopy é:</span><span class="sxs-lookup"><span data-stu-id="4533d-132">The basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="4533d-133">Os exemplos a seguir demonstram vários cenários para cópia de dados entre os Blobs e os Arquivos do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4533d-133">The following examples demonstrate various scenarios for copying data to and from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="4533d-134">Consulte o menu `azcopy --help` para obter uma explicação detalhada dos parâmetros usados em cada amostra.</span><span class="sxs-lookup"><span data-stu-id="4533d-134">Refer to the `azcopy --help` menu for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="4533d-135">Blob: baixar</span><span class="sxs-lookup"><span data-stu-id="4533d-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="4533d-136">Baixar um único blob</span><span class="sxs-lookup"><span data-stu-id="4533d-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4533d-137">Se a pasta `/mnt/myfiles` não existir, o AzCopy a criará e baixará `abc.txt ` na nova pasta.</span><span class="sxs-lookup"><span data-stu-id="4533d-137">If the folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="4533d-138">Baixe um único blob de região secundária</span><span class="sxs-lookup"><span data-stu-id="4533d-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4533d-139">Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.</span><span class="sxs-lookup"><span data-stu-id="4533d-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="4533d-140">Baixar todos os blobs</span><span class="sxs-lookup"><span data-stu-id="4533d-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="4533d-141">Suponhamos que os seguintes blobs residam no contêiner especificado:</span><span class="sxs-lookup"><span data-stu-id="4533d-141">Assume the following blobs reside in the specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="4533d-142">Após a operação de download, o diretório `/mnt/myfiles` inclui os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="4533d-142">After the download operation, the directory `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="4533d-143">Se você não especificar a opção `--recursive`, nenhum blob será baixado.</span><span class="sxs-lookup"><span data-stu-id="4533d-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="4533d-144">Baixar blobs com prefixo especificado</span><span class="sxs-lookup"><span data-stu-id="4533d-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="4533d-145">Suponhamos que os blobs a seguir residam no contêiner especificado.</span><span class="sxs-lookup"><span data-stu-id="4533d-145">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="4533d-146">Todos os blobs que começam com o prefixo `a` são baixados.</span><span class="sxs-lookup"><span data-stu-id="4533d-146">All blobs beginning with the prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="4533d-147">Após a operação de download, a pasta `/mnt/myfiles` inclui os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="4533d-147">After the download operation, the folder `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="4533d-148">O prefixo se aplica ao diretório virtual, que forma a primeira parte do nome do blob.</span><span class="sxs-lookup"><span data-stu-id="4533d-148">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="4533d-149">No exemplo mostrado acima, o diretório virtual não corresponde ao prefixo especificado e, portanto, nenhum blob é baixado.</span><span class="sxs-lookup"><span data-stu-id="4533d-149">In the example shown above, the virtual directory does not match the specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="4533d-150">Além disso, se a opção `--recursive` não for especificada, o AzCopy não baixará nenhum blob.</span><span class="sxs-lookup"><span data-stu-id="4533d-150">In addition, if the option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="4533d-151">Defina a hora da última modificação dos arquivos exportados como sendo a mesma dos blobs de origem</span><span class="sxs-lookup"><span data-stu-id="4533d-151">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="4533d-152">Você também pode excluir blobs da operação de download com base na hora da última modificação</span><span class="sxs-lookup"><span data-stu-id="4533d-152">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="4533d-153">Por exemplo, se você quiser excluir blobs cuja hora da última modificação for a mesma ou mais recente do que o arquivo de destino, adicione a opção `--exclude-newer`:</span><span class="sxs-lookup"><span data-stu-id="4533d-153">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="4533d-154">Ou, se você quiser excluir blobs cuja hora da última modificação for a mesma ou mais antiga do que o arquivo de destino, adicione a opção `--exclude-older`:</span><span class="sxs-lookup"><span data-stu-id="4533d-154">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="4533d-155">Blob: carregar</span><span class="sxs-lookup"><span data-stu-id="4533d-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="4533d-156">Carregar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="4533d-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4533d-157">Se o contêiner de destino especificado não existir, o AzCopy o criará e carregará o arquivo nele.</span><span class="sxs-lookup"><span data-stu-id="4533d-157">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="4533d-158">Carregar arquivo único no diretório virtual</span><span class="sxs-lookup"><span data-stu-id="4533d-158">Upload single file to virtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4533d-159">Se o diretório virtual especificado não existir, o AzCopy carregará o arquivo para incluir o diretório virtual no nome do blob (*por exemplo*, `vd/abc.txt` no exemplo acima).</span><span class="sxs-lookup"><span data-stu-id="4533d-159">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in the blob name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="4533d-160">Carregar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="4533d-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="4533d-161">A especificação da opção `--recursive` carrega o conteúdo do diretório especificado no Armazenamento de blobs de maneira recursiva, o que significa que todas as subpastas e seus arquivos são carregados também.</span><span class="sxs-lookup"><span data-stu-id="4533d-161">Specifying option `--recursive` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="4533d-162">Por exemplo, suponhamos que os seguintes arquivos residam na pasta `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="4533d-162">For instance, assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="4533d-163">Após a operação de upload, o contêiner incluirá os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="4533d-163">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="4533d-164">Quando a opção `--recursive` não é especificada, somente os seguintes três arquivos são carregados:</span><span class="sxs-lookup"><span data-stu-id="4533d-164">When the option `--recursive` is not specified, only the following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="4533d-165">Carregar arquivos que correspondam ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="4533d-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="4533d-166">Vamos supor que a pasta `/mnt/myfiles`contenha os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="4533d-166">Assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="4533d-167">Após a operação de upload, o contêiner incluirá os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="4533d-167">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="4533d-168">Quando a opção `--recursive` não é especificada, o AzCopy ignora os arquivos que estão em subdiretórios:</span><span class="sxs-lookup"><span data-stu-id="4533d-168">When the option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="4533d-169">Especificar o tipo de conteúdo MIME de um blob de destino</span><span class="sxs-lookup"><span data-stu-id="4533d-169">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="4533d-170">Por padrão, o AzCopy define o tipo de conteúdo de um blob de destino para `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="4533d-170">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="4533d-171">No entanto, você pode especificar explicitamente o tipo de conteúdo por meio da opção `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="4533d-171">However, you can explicitly specify the content type via the option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="4533d-172">Essa sintaxe define o tipo de conteúdo para todos os blobs em uma operação de carregamento.</span><span class="sxs-lookup"><span data-stu-id="4533d-172">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="4533d-173">Se a opção `--set-content-type` for especificada sem um valor, o AzCopy definirá o tipo de conteúdo de cada blob ou arquivo de acordo com sua extensão de arquivo.</span><span class="sxs-lookup"><span data-stu-id="4533d-173">If the option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="4533d-174">Blob: copiar</span><span class="sxs-lookup"><span data-stu-id="4533d-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="4533d-175">Copiar um único blob dentro da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="4533d-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4533d-176">Quando você copia um blob sem a opção --sync-copy, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é executada.</span><span class="sxs-lookup"><span data-stu-id="4533d-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="4533d-177">Copiar um único blob entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="4533d-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="4533d-178">Quando você copia um blob sem a opção --sync-copy, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é executada.</span><span class="sxs-lookup"><span data-stu-id="4533d-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="4533d-179">Copiar um único blob de região secundária para região primária</span><span class="sxs-lookup"><span data-stu-id="4533d-179">Copy single blob from secondary region to primary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="4533d-180">Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.</span><span class="sxs-lookup"><span data-stu-id="4533d-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="4533d-181">Copiar um único blob e seus instantâneos entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="4533d-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="4533d-182">Após a operação de cópia, o contêiner de destino incluirá o blob e seus instantâneos.</span><span class="sxs-lookup"><span data-stu-id="4533d-182">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="4533d-183">O contêiner inclui o seguinte blob e seus instantâneos:</span><span class="sxs-lookup"><span data-stu-id="4533d-183">The container includes the following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="4533d-184">Copiar blobs em regiões entre contas de armazenamento de forma síncrona.</span><span class="sxs-lookup"><span data-stu-id="4533d-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="4533d-185">O AzCopy por padrão copia dados entre dois pontos de extremidade de armazenamento assincronamente.</span><span class="sxs-lookup"><span data-stu-id="4533d-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="4533d-186">Portanto, a operação de cópia é executada em segundo plano usando a capacidade de largura de banda extra, que não tem nenhum SLA em termos da velocidade de cópia de um blob.</span><span class="sxs-lookup"><span data-stu-id="4533d-186">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="4533d-187">A opção `--sync-copy` garante que a operação de cópia obtém uma velocidade consistente.</span><span class="sxs-lookup"><span data-stu-id="4533d-187">The `--sync-copy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="4533d-188">O AzCopy realiza a cópia síncrona baixando os blobs para copiar da fonte especificada para a memória local, e, em seguida, carregá-los para o destino de armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="4533d-188">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="4533d-189">`--sync-copy` poderá gerar custos de saída adicionais, comparado à cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="4533d-189">`--sync-copy` might generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="4533d-190">A abordagem recomendada é usar essa opção em uma VM do Azure que está na mesma região de sua conta de armazenamento de origem, para evitar o custo de saída.</span><span class="sxs-lookup"><span data-stu-id="4533d-190">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="4533d-191">Arquivo: baixar</span><span class="sxs-lookup"><span data-stu-id="4533d-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="4533d-192">Baixar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="4533d-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="4533d-193">Se a origem especificada for um compartilhamento de arquivos do Azure, você deverá especificar o nome exato do arquivo, (*por exemplo*, `abc.txt`) para baixar um único arquivo ou especificar a opção `--recursive` para baixar todos os arquivos do compartilhamento de maneira recursiva.</span><span class="sxs-lookup"><span data-stu-id="4533d-193">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `--recursive` to download all files in the share recursively.</span></span> <span data-ttu-id="4533d-194">A tentativa de especificar um padrão de arquivo e a opção `--recursive` simultaneamente resulta em um erro.</span><span class="sxs-lookup"><span data-stu-id="4533d-194">Attempting to specify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="4533d-195">Baixar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="4533d-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="4533d-196">Observe que as pastas vazias não são baixadas.</span><span class="sxs-lookup"><span data-stu-id="4533d-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="4533d-197">Arquivo: carregar</span><span class="sxs-lookup"><span data-stu-id="4533d-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="4533d-198">Carregar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="4533d-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="4533d-199">Carregar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="4533d-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="4533d-200">Observe que as pastas vazias não são carregadas.</span><span class="sxs-lookup"><span data-stu-id="4533d-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="4533d-201">Carregar arquivos que correspondam ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="4533d-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="4533d-202">Arquivo: copiar</span><span class="sxs-lookup"><span data-stu-id="4533d-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="4533d-203">Copiar entre compartilhamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="4533d-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="4533d-204">Quando você copia um arquivo entre compartilhamentos de arquivos, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="4533d-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="4533d-205">Copiar de compartilhamento de arquivos para blob</span><span class="sxs-lookup"><span data-stu-id="4533d-205">Copy from file share to blob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="4533d-206">Quando você copia um arquivo do compartilhamento de arquivos no blob, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="4533d-206">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="4533d-207">Copiar do blob para compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="4533d-207">Copy from blob to file share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="4533d-208">Quando você copia um arquivo do blob no compartilhamentos de arquivos, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="4533d-208">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="4533d-209">Copiar arquivos de forma síncrona</span><span class="sxs-lookup"><span data-stu-id="4533d-209">Synchronously copy files</span></span>
<span data-ttu-id="4533d-210">Especifique a opção `--sync-copy` para copiar dados do Armazenamento de Arquivos para o Armazenamento de Arquivos, do Armazenamento de Arquivos para o Armazenamento de Blobs e do Armazenamento de Blobs para o Armazenamento de Arquivos de forma síncrona.</span><span class="sxs-lookup"><span data-stu-id="4533d-210">You can specify the `--sync-copy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously.</span></span> <span data-ttu-id="4533d-211">O AzCopy executa esta operação baixando os dados de origem na memória local e, em seguida, carregando-os para o destino.</span><span class="sxs-lookup"><span data-stu-id="4533d-211">AzCopy runs this operation by downloading the source data to local memory, and then uploading it to destination.</span></span> <span data-ttu-id="4533d-212">Nesse caso, se aplica o custo de saída padrão.</span><span class="sxs-lookup"><span data-stu-id="4533d-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="4533d-213">Durante a cópia do Armazenamento de Arquivos para o Armazenamento de Blobs, o tipo de blob padrão é o blob de blocos, e o usuário pode especificar a opção `/BlobType:page` para alterar o tipo de blob de destino.</span><span class="sxs-lookup"><span data-stu-id="4533d-213">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="4533d-214">Observe que `--sync-copy` pode gerar custos de saída adicionais, comparado à cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="4533d-214">Note that `--sync-copy` might generate additional egress cost comparing to asynchronous copy.</span></span> <span data-ttu-id="4533d-215">A abordagem recomendada é usar essa opção em uma VM do Azure que está na mesma região de sua conta de armazenamento de origem, para evitar o custo de saída.</span><span class="sxs-lookup"><span data-stu-id="4533d-215">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="4533d-216">Outros recursos do AzCopy</span><span class="sxs-lookup"><span data-stu-id="4533d-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="4533d-217">Copiar apenas os dados que não existem no destino</span><span class="sxs-lookup"><span data-stu-id="4533d-217">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="4533d-218">Os parâmetros `--exclude-older` e `--exclude-newer` permitem a exclusão de recursos de origem mais antigos ou mais recentes da cópia, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="4533d-218">The `--exclude-older` and `--exclude-newer` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="4533d-219">Se você quiser copiar apenas os recursos de origem que não existem no destino, especifique os dois parâmetros no comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4533d-219">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a><span data-ttu-id="4533d-220">Usar um arquivo de configuração para especificar parâmetros de linha de comando</span><span class="sxs-lookup"><span data-stu-id="4533d-220">Use a configuration file to specify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="4533d-221">É possível incluir qualquer parâmetro de linha de comando do AzCopy em um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="4533d-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="4533d-222">O AzCopy processa os parâmetros no arquivo como se eles tivessem sido especificados na linha de comando, realizando uma substituição direta pelo conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="4533d-222">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="4533d-223">Suponha um arquivo de configuração chamado `copyoperation`, que contém as linhas a seguir.</span><span class="sxs-lookup"><span data-stu-id="4533d-223">Assume a configuration file named `copyoperation`, that contains the following lines.</span></span> <span data-ttu-id="4533d-224">Cada parâmetro do AzCopy pode ser especificado em uma única linha.</span><span class="sxs-lookup"><span data-stu-id="4533d-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="4533d-225">ou, em linhas separadas:</span><span class="sxs-lookup"><span data-stu-id="4533d-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="4533d-226">O AzCopy falhará se você dividir o parâmetro em duas linhas, conforme mostrado aqui para o parâmetro `--source-key`:</span><span class="sxs-lookup"><span data-stu-id="4533d-226">AzCopy fails if you split the parameter across two lines, as shown here for the `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="4533d-227">Especificar uma SAS</span><span class="sxs-lookup"><span data-stu-id="4533d-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="4533d-228">Você também pode especificar um SAS no URI do contêiner:</span><span class="sxs-lookup"><span data-stu-id="4533d-228">You can also specify a SAS on the container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="4533d-229">Observe que o AzCopy atualmente dá suporte apenas a [SAS de Conta](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="4533d-229">Note that AzCopy currently only supports the [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="4533d-230">Pasta de arquivo de diário</span><span class="sxs-lookup"><span data-stu-id="4533d-230">Journal file folder</span></span>
<span data-ttu-id="4533d-231">Sempre que você emite um comando para o AzCopy, ele verifica se um arquivo de diário existe na pasta padrão ou se está em uma pasta especificada por meio dessa opção.</span><span class="sxs-lookup"><span data-stu-id="4533d-231">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="4533d-232">Se o arquivo de diário não estiver em nenhum dos lugares, o AzCopy tratará a operação como nova e gerar um novo arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="4533d-232">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="4533d-233">Se o arquivo de diário existir, o AzCopy verificará se a linha de comando inserida corresponde à linha de comando no arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="4533d-233">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="4533d-234">Se as duas linhas de comando forem correspondentes, o AzCopy retomará a operação incompleta.</span><span class="sxs-lookup"><span data-stu-id="4533d-234">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="4533d-235">Se elas não forem correspondentes, o AzCopy solicitará que o usuário substitua o arquivo de diário para iniciar uma nova operação ou cancele a operação atual.</span><span class="sxs-lookup"><span data-stu-id="4533d-235">If they do not match, AzCopy prompts user to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="4533d-236">Se você quiser usar o local padrão para o arquivo de diário:</span><span class="sxs-lookup"><span data-stu-id="4533d-236">If you want to use the default location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="4533d-237">Se você omitir a opção `--resume` ou especificar a opção `--resume` sem o caminho da pasta, conforme mostrado acima, o AzCopy criará o arquivo de diário no local padrão, que é `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4533d-237">If you omit option `--resume`, or specify option `--resume` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="4533d-238">Se o arquivo de diário já existir, o AzCopy retomará a operação com base no arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="4533d-238">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="4533d-239">Se você quiser especificar um local personalizado para o arquivo de diário:</span><span class="sxs-lookup"><span data-stu-id="4533d-239">If you want to specify a custom location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="4533d-240">Este exemplo criará o arquivo de diário se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="4533d-240">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="4533d-241">Se ele existir, o AzCopy retomará a operação com base no arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="4533d-241">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="4533d-242">Se desejar retomar uma operação do AzCopy, repita o mesmo comando.</span><span class="sxs-lookup"><span data-stu-id="4533d-242">If you want to resume an AzCopy operation, repeat the same command.</span></span> <span data-ttu-id="4533d-243">Em seguida, o AzCopy no Linux solicitará a confirmação:</span><span class="sxs-lookup"><span data-stu-id="4533d-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="4533d-244">Logs detalhados de saída</span><span class="sxs-lookup"><span data-stu-id="4533d-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="4533d-245">Especificar o número de operações simultâneas para começar</span><span class="sxs-lookup"><span data-stu-id="4533d-245">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="4533d-246">A opção `--parallel-level` especifica o número de operações de cópia simultâneas.</span><span class="sxs-lookup"><span data-stu-id="4533d-246">Option `--parallel-level` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="4533d-247">Por padrão, o AzCopy inicia uma determinada quantidade de operações simultâneas para aumentar a taxa de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="4533d-247">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="4533d-248">O número de operações simultâneas é igual a oito vezes o número de processadores que você tem.</span><span class="sxs-lookup"><span data-stu-id="4533d-248">The number of concurrent operations is equal eight times the number of processors you have.</span></span> <span data-ttu-id="4533d-249">Se você estiver executando o AzCopy em uma rede de baixa largura de banda, poderá especificar um número menor para o nível --parallel-, a fim de evitar uma falha causada pela competição de recursos.</span><span class="sxs-lookup"><span data-stu-id="4533d-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level to avoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="4533d-250">Para exibir a lista completa de parâmetros do AzCopy, confira o menu “azcopy --help”.</span><span class="sxs-lookup"><span data-stu-id="4533d-250">To view the complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="4533d-251">Problemas conhecidos e melhores práticas</span><span class="sxs-lookup"><span data-stu-id="4533d-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-the-system"></a><span data-ttu-id="4533d-252">Erro: o .NET Core não foi encontrado no sistema.</span><span class="sxs-lookup"><span data-stu-id="4533d-252">Error: .NET Core is not found in the system.</span></span>
<span data-ttu-id="4533d-253">Se você receber um erro informando que o .NET Core não está instalado no sistema, a variável PATH do binário `dotnet` do .NET Core poderá estar ausente.</span><span class="sxs-lookup"><span data-stu-id="4533d-253">If you encounter an error stating that .NET Core is not installed in the system, the PATH to the .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="4533d-254">Para resolver esse problema, encontre o binário do .NET Core no sistema:</span><span class="sxs-lookup"><span data-stu-id="4533d-254">In order to address this issue, find the .NET Core binary in the system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="4533d-255">Isso retorna o caminho para o binário do dotnet.</span><span class="sxs-lookup"><span data-stu-id="4533d-255">This returns the path to the dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="4533d-256">Agora adicione esse caminho à variável PATH.</span><span class="sxs-lookup"><span data-stu-id="4533d-256">Now add this path to the PATH variable.</span></span> <span data-ttu-id="4533d-257">Para o sudo, edite secure_path para conter o caminho para o binário do dotnet:</span><span class="sxs-lookup"><span data-stu-id="4533d-257">For sudo, edit secure_path to contain the path to the dotnet binary:</span></span>
```bash 
sudo visudo
### Append the path found in the preceding example to 'secure_path' variable
```

<span data-ttu-id="4533d-258">Neste exemplo, a variável secure_path é:</span><span class="sxs-lookup"><span data-stu-id="4533d-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="4533d-259">Para o usuário atual, edite .bash_profile/.profile para incluir o caminho para o binário do dotnet na variável PATH</span><span class="sxs-lookup"><span data-stu-id="4533d-259">For the current user, edit .bash_profile/.profile to include the path to the dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append the path found in the preceding example to 'PATH' variable
```

<span data-ttu-id="4533d-260">Verifique se o .NET Core agora está em PATH:</span><span class="sxs-lookup"><span data-stu-id="4533d-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="4533d-261">Erro ao instalar o AzCopy</span><span class="sxs-lookup"><span data-stu-id="4533d-261">Error Installing AzCopy</span></span>
<span data-ttu-id="4533d-262">Caso tenha problemas com a instalação do AzCopy, tente executar o AzCopy usando o script bash na pasta `azcopy` extraída.</span><span class="sxs-lookup"><span data-stu-id="4533d-262">If you encounter issues with AzCopy installation, you may try to run AzCopy using the bash script in the extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="4533d-263">Limite gravações simultâneas durante a cópia de dados</span><span class="sxs-lookup"><span data-stu-id="4533d-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="4533d-264">Ao copiar blobs ou arquivos usando o AZCopy, lembre-se de que outro aplicativo pode estar modificando os dados enquanto você os copia.</span><span class="sxs-lookup"><span data-stu-id="4533d-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="4533d-265">Se possível, verifique se os dados que está copiando não estão sendo modificados durante a cópia.</span><span class="sxs-lookup"><span data-stu-id="4533d-265">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="4533d-266">Por exemplo, ao copiar um VHD associado a uma máquina virtual do Azure, verifique se nenhum outro aplicativo está gravando no VHD, no momento.</span><span class="sxs-lookup"><span data-stu-id="4533d-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="4533d-267">Uma boa maneira de fazer isso é ceder o recurso para ser copiado.</span><span class="sxs-lookup"><span data-stu-id="4533d-267">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="4533d-268">Também é possível criar um instantâneo do VHD primeiro e, em seguida, copiar o instantâneo.</span><span class="sxs-lookup"><span data-stu-id="4533d-268">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="4533d-269">Se não for possível evitar que outros aplicativos gravem em blobs ou arquivos enquanto são copiados, lembre-se que, quando o trabalho terminar, os recursos copiados não poderão mais ter paridade total com os recursos de origem.</span><span class="sxs-lookup"><span data-stu-id="4533d-269">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="4533d-270">Execute uma instância de AzCopy em um computador.</span><span class="sxs-lookup"><span data-stu-id="4533d-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="4533d-271">O AzCopy foi projetado para maximizar a utilização de seu recurso de máquina para acelerar a transferência de dados, é recomendável executar apenas uma instância de AzCopy em um único computador e especifique a opção `--parallel-level` se precisar de mais operações em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="4533d-271">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="4533d-272">Para obter mais detalhes, digite `AzCopy --help parallel-level` na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="4533d-272">For more details, type `AzCopy --help parallel-level` at the command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4533d-273">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4533d-273">Next steps</span></span>
<span data-ttu-id="4533d-274">Para obter mais informações sobre o Armazenamento do Azure e o AzCopy, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="4533d-274">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="4533d-275">Documentação do Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="4533d-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="4533d-276">Introdução ao Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4533d-276">Introduction to Azure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="4533d-277">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="4533d-277">Create a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="4533d-278">Gerenciar blobs com o Gerenciador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="4533d-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="4533d-279">Usando a CLI 2.0 do Azure com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4533d-279">Using the Azure CLI 2.0 with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="4533d-280">Como usar o armazenamento de Blob por meio do C++</span><span class="sxs-lookup"><span data-stu-id="4533d-280">How to use Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="4533d-281">Como usar o Armazenamento de Blob do Java</span><span class="sxs-lookup"><span data-stu-id="4533d-281">How to use Blob storage from Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="4533d-282">Como usar o armazenamento de Blob do Node.js</span><span class="sxs-lookup"><span data-stu-id="4533d-282">How to use Blob storage from Node.js</span></span>](storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="4533d-283">Como usar o armazenamento de Blob no Python</span><span class="sxs-lookup"><span data-stu-id="4533d-283">How to use Blob storage from Python</span></span>](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="4533d-284">Postagens de blog de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="4533d-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="4533d-285">Anunciando a Versão Prévia do AzCopy no Linux</span><span class="sxs-lookup"><span data-stu-id="4533d-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="4533d-286">Apresentando a versão de visualização da biblioteca de movimentação de dados do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4533d-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="4533d-287">AzCopy: Introducing synchronous copy and customized content type (AzCopy: introdução a cópia síncrona e tipo de conteúdo personalizado)</span><span class="sxs-lookup"><span data-stu-id="4533d-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="4533d-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support (AzCopy: anúncio de disponibilidade geral do AzCopy 3.0 mais versão de teste do AzCopy 4.0 com suporte para Tabela e Arquivo)</span><span class="sxs-lookup"><span data-stu-id="4533d-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="4533d-289">AzCopy: Optimized for Large-Scale Copy Scenarios (AzCopy: otimizado para cenários de cópia em larga escala)</span><span class="sxs-lookup"><span data-stu-id="4533d-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="4533d-290">AzCopy: Support for read-access geo-redundant storage (AzCopy: suporte para o armazenamento com redundância geográfica com acesso de leitura)</span><span class="sxs-lookup"><span data-stu-id="4533d-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="4533d-291">AzCopy: Transferir dados com o modo reiniciável e um token SAS</span><span class="sxs-lookup"><span data-stu-id="4533d-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="4533d-292">AzCopy: Using cross-account Copy Blob (AzCopy: usando blob de cópia em várias contas)</span><span class="sxs-lookup"><span data-stu-id="4533d-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="4533d-293">AzCopy: Uploading/downloading files for Azure Blobs (AzCopy: Upload/download de arquivos para Blobs do Azure)</span><span class="sxs-lookup"><span data-stu-id="4533d-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

