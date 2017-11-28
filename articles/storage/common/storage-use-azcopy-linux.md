---
title: aaaCopy ou mover dados tooAzure armazenamento com AzCopy no Linux | Microsoft Docs
description: "Use Olá AzCopy Linux utilitário toomove ou copiar dados tooor do blob e o arquivo de conteúdo. Copiar dados tooAzure armazenamento de arquivos locais, ou copie dados dentro ou entre contas de armazenamento. Migre facilmente o armazenamento de tooAzure de dados."
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
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="3d3df-105">Transferir dados com o AzCopy no Linux</span><span class="sxs-lookup"><span data-stu-id="3d3df-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="3d3df-106">AzCopy no Linux é um utilitário de linha de comando projetado para copiar dados tooand do armazenamento de BLOBs do Microsoft Azure e o arquivo usando comandos simples com um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="3d3df-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="3d3df-107">Você pode copiar dados de um tooanother de objeto dentro de sua conta de armazenamento, ou entre contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d3df-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="3d3df-108">Há duas versões do AzCopy que podem ser baixadas.</span><span class="sxs-lookup"><span data-stu-id="3d3df-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="3d3df-109">O AzCopy no Linux se baseia no .NET Core Framework, que se destina a plataformas Linux que oferecem opções de linha de comando no estilo POSIX.</span><span class="sxs-lookup"><span data-stu-id="3d3df-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="3d3df-110">O [AzCopy no Windows](../storage-use-azcopy.md) se baseia no .NET Framework e oferece opções de linha de comando no estilo Windows.</span><span class="sxs-lookup"><span data-stu-id="3d3df-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="3d3df-111">Este artigo aborda o AzCopy no Linux.</span><span class="sxs-lookup"><span data-stu-id="3d3df-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="3d3df-112">Baixar e instalar o AzCopy</span><span class="sxs-lookup"><span data-stu-id="3d3df-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="3d3df-113">Instalação no Linux</span><span class="sxs-lookup"><span data-stu-id="3d3df-113">Installation on Linux</span></span>

<span data-ttu-id="3d3df-114">AzCopy no Linux requer o framework .NET Core na plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d3df-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="3d3df-115">Consulte as instruções de instalação de saudação em Olá [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) página.</span><span class="sxs-lookup"><span data-stu-id="3d3df-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="3d3df-116">Como exemplo, vamos instalar o .NET Core no Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="3d3df-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="3d3df-117">Guia de instalação mais recente hello, visite [.NET Core no Linux](https://www.microsoft.com/net/core#linuxubuntu) página de instalação.</span><span class="sxs-lookup"><span data-stu-id="3d3df-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="3d3df-118">Depois de instalar o .NET Core, baixe e instale o AzCopy.</span><span class="sxs-lookup"><span data-stu-id="3d3df-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="3d3df-119">Você pode remover arquivos de saudação extraído quando AzCopy no Linux está instalado.</span><span class="sxs-lookup"><span data-stu-id="3d3df-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="3d3df-120">Como alternativa se você não tem privilégios de superusuário, você também pode executar AzCopy usando script de shell Olá 'azcopy' na pasta extraída hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="3d3df-121">Instalação alternativa no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3d3df-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="3d3df-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="3d3df-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="3d3df-123">Adicionar fonte de apt ao .Net Core:</span><span class="sxs-lookup"><span data-stu-id="3d3df-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="3d3df-124">Adicionar fonte de apt ao repositório de produtos do Linux da Microsoft e instale o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="3d3df-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="3d3df-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="3d3df-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="3d3df-126">Adicionar fonte de apt ao .Net Core:</span><span class="sxs-lookup"><span data-stu-id="3d3df-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="3d3df-127">Adicionar fonte de apt ao repositório de produtos do Linux da Microsoft e instale o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="3d3df-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="3d3df-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="3d3df-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="3d3df-129">Adicionar fonte de apt ao .Net Core:</span><span class="sxs-lookup"><span data-stu-id="3d3df-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="3d3df-130">Adicionar fonte de apt ao repositório de produtos do Linux da Microsoft e instale o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="3d3df-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="3d3df-131">Como escrever seu primeiro comando do AzCopy</span><span class="sxs-lookup"><span data-stu-id="3d3df-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="3d3df-132">Olá a sintaxe básica para comandos do AzCopy é:</span><span class="sxs-lookup"><span data-stu-id="3d3df-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="3d3df-133">Olá exemplos a seguir demonstram vários cenários para copiar dados tooand de Blobs do Microsoft Azure e arquivos.</span><span class="sxs-lookup"><span data-stu-id="3d3df-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="3d3df-134">Consulte toohello `azcopy --help` menu para obter uma explicação detalhada de parâmetros de saudação usados em cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="3d3df-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="3d3df-135">Blob: baixar</span><span class="sxs-lookup"><span data-stu-id="3d3df-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="3d3df-136">Baixar um único blob</span><span class="sxs-lookup"><span data-stu-id="3d3df-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3d3df-137">Se pasta Olá `/mnt/myfiles` não existir, downloads e cria AzCopy `abc.txt ` na nova pasta de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d3df-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="3d3df-138">Baixe um único blob de região secundária</span><span class="sxs-lookup"><span data-stu-id="3d3df-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3d3df-139">Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.</span><span class="sxs-lookup"><span data-stu-id="3d3df-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="3d3df-140">Baixar todos os blobs</span><span class="sxs-lookup"><span data-stu-id="3d3df-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="3d3df-141">Suponha seguinte Olá blobs residem no contêiner especificado hello:</span><span class="sxs-lookup"><span data-stu-id="3d3df-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="3d3df-142">Após a operação de download de Olá Olá diretório `/mnt/myfiles` inclui Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="3d3df-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="3d3df-143">Se você não especificar a opção `--recursive`, nenhum blob será baixado.</span><span class="sxs-lookup"><span data-stu-id="3d3df-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="3d3df-144">Baixar blobs com prefixo especificado</span><span class="sxs-lookup"><span data-stu-id="3d3df-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="3d3df-145">Suponha seguinte Olá blobs residem no contêiner especificado hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="3d3df-146">Todos os blobs que começam com o prefixo Olá `a` são baixados.</span><span class="sxs-lookup"><span data-stu-id="3d3df-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="3d3df-147">Após a operação de download de Olá Olá pasta `/mnt/myfiles` inclui Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="3d3df-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="3d3df-148">prefixo de saudação aplica diretório virtual toohello, que constitui Olá primeira parte do nome do blob hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="3d3df-149">Exemplo hello mostrado acima, diretório virtual Olá não coincide com prefixo especificado de hello, para que nenhum blob é baixado.</span><span class="sxs-lookup"><span data-stu-id="3d3df-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="3d3df-150">Além disso, se hello opção `--recursive` não for especificado, AzCopy não baixar todos os blobs.</span><span class="sxs-lookup"><span data-stu-id="3d3df-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="3d3df-151">Definir a hora da última modificação Olá dos arquivos exportados toobe mesmo Olá blobs de origem</span><span class="sxs-lookup"><span data-stu-id="3d3df-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="3d3df-152">Você também pode excluir blobs de operação de download de saudação com base em sua hora da última modificação.</span><span class="sxs-lookup"><span data-stu-id="3d3df-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="3d3df-153">Por exemplo, se você quiser blobs tooexclude cuja hora da última modificação é hello igual ou mais recente do que o arquivo de destino hello, adicionar Olá `--exclude-newer` opção:</span><span class="sxs-lookup"><span data-stu-id="3d3df-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="3d3df-154">Ou se você quiser blobs tooexclude cuja hora da última modificação é hello mesmo ou mais antigo que o arquivo de destino hello, adicione Olá `--exclude-older` opção:</span><span class="sxs-lookup"><span data-stu-id="3d3df-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="3d3df-155">Blob: carregar</span><span class="sxs-lookup"><span data-stu-id="3d3df-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3d3df-156">Carregar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="3d3df-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3d3df-157">Se Olá contêiner de destino especificado não existe, AzCopy cria e carregamentos Olá arquivo nele.</span><span class="sxs-lookup"><span data-stu-id="3d3df-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="3d3df-158">Carregar arquivo único diretório toovirtual</span><span class="sxs-lookup"><span data-stu-id="3d3df-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3d3df-159">Se Olá especificado não existe um diretório virtual, AzCopy carrega Olá arquivo tooinclude Olá diretório virtual no nome do blob hello (*, por exemplo,*, `vd/abc.txt` no exemplo hello acima).</span><span class="sxs-lookup"><span data-stu-id="3d3df-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="3d3df-160">Carregar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="3d3df-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="3d3df-161">Especificando a opção `--recursive` carregamentos conteúdo Olá Olá especificado diretório tooBlob armazenamento recursivamente, que significa que todas as subpastas e seus arquivos são carregados também.</span><span class="sxs-lookup"><span data-stu-id="3d3df-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="3d3df-162">Por exemplo, suponha que a seguir Olá arquivos residem na pasta `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="3d3df-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="3d3df-163">Após a operação de carregamento de saudação contêiner Olá inclui Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="3d3df-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="3d3df-164">Olá quando a opção `--recursive` não for especificado, somente hello seguintes três arquivos são carregados:</span><span class="sxs-lookup"><span data-stu-id="3d3df-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3d3df-165">Carregar arquivos que correspondam ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="3d3df-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="3d3df-166">Suponha seguinte Olá arquivos residem na pasta `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="3d3df-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="3d3df-167">Após a operação de carregamento de saudação contêiner Olá inclui Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="3d3df-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="3d3df-168">Olá quando a opção `--recursive` não for especificado, AzCopy ignora os arquivos que estão em subpastas:</span><span class="sxs-lookup"><span data-stu-id="3d3df-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="3d3df-169">Especifique o tipo de conteúdo MIME Olá de um blob de destino</span><span class="sxs-lookup"><span data-stu-id="3d3df-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="3d3df-170">Por padrão, AzCopy define Olá de tipo de conteúdo de um blob de destino muito`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="3d3df-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="3d3df-171">No entanto, você pode especificar explicitamente o tipo de conteúdo Olá por meio da opção Olá `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="3d3df-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="3d3df-172">Essa sintaxe define o tipo de conteúdo Olá para todos os blobs em uma operação de carregamento.</span><span class="sxs-lookup"><span data-stu-id="3d3df-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="3d3df-173">Se hello opção `--set-content-type` for especificado sem um valor, AzCopy define cada blob ou arquivo do tipo de conteúdo de acordo com tooits extensão de arquivo.</span><span class="sxs-lookup"><span data-stu-id="3d3df-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="3d3df-174">Blob: copiar</span><span class="sxs-lookup"><span data-stu-id="3d3df-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="3d3df-175">Copiar um único blob dentro da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3d3df-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3d3df-176">Quando você copia um blob sem a opção --sync-copy, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é executada.</span><span class="sxs-lookup"><span data-stu-id="3d3df-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="3d3df-177">Copiar um único blob entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3d3df-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="3d3df-178">Quando você copia um blob sem a opção --sync-copy, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é executada.</span><span class="sxs-lookup"><span data-stu-id="3d3df-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="3d3df-179">Copiar um único blob da região de tooprimary região secundária</span><span class="sxs-lookup"><span data-stu-id="3d3df-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="3d3df-180">Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.</span><span class="sxs-lookup"><span data-stu-id="3d3df-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="3d3df-181">Copiar um único blob e seus instantâneos entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3d3df-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="3d3df-182">Após a operação de cópia hello, o contêiner de destino Olá inclui Olá blob e seus instantâneos.</span><span class="sxs-lookup"><span data-stu-id="3d3df-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="3d3df-183">Olá, contêiner inclui Olá seguinte blob e seus instantâneos:</span><span class="sxs-lookup"><span data-stu-id="3d3df-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="3d3df-184">Copiar blobs em regiões entre contas de armazenamento de forma síncrona.</span><span class="sxs-lookup"><span data-stu-id="3d3df-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="3d3df-185">O AzCopy por padrão copia dados entre dois pontos de extremidade de armazenamento assincronamente.</span><span class="sxs-lookup"><span data-stu-id="3d3df-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="3d3df-186">Portanto, as execuções de operação de cópia Olá no plano de fundo de saudação utilizando a capacidade de largura de banda sobressalente com nenhum SLA em termos de rapidez com que um blob é copiado.</span><span class="sxs-lookup"><span data-stu-id="3d3df-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="3d3df-187">Olá `--sync-copy` opção garante que a operação de cópia de saudação obtém velocidade consistente.</span><span class="sxs-lookup"><span data-stu-id="3d3df-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="3d3df-188">AzCopy executa cópia síncrona Olá ao baixar blobs Olá toocopy de saudação especificado fonte toolocal da memória e, em seguida, carregá-las toohello destino de armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="3d3df-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="3d3df-189">`--sync-copy`pode gerar saída adicional em comparação de custo tooasynchronous cópia.</span><span class="sxs-lookup"><span data-stu-id="3d3df-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="3d3df-190">Olá a abordagem recomendada é toouse essa opção em uma VM do Azure, que está em Olá mesma região que o custo de egresso fonte armazenamento conta tooavoid.</span><span class="sxs-lookup"><span data-stu-id="3d3df-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="3d3df-191">Arquivo: baixar</span><span class="sxs-lookup"><span data-stu-id="3d3df-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="3d3df-192">Baixar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="3d3df-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="3d3df-193">Se Olá especificado fonte for um compartilhamento de arquivos do Azure, você deve especificar nome de arquivo exatos Olá, (*, por exemplo,* `abc.txt`) toodownload um único arquivo, ou especifique a opção `--recursive` toodownload todos os arquivos no compartilhamento de saudação recursivamente.</span><span class="sxs-lookup"><span data-stu-id="3d3df-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="3d3df-194">Tentativa de toospecify um padrão de arquivo e a opção `--recursive` juntos resulta em erro.</span><span class="sxs-lookup"><span data-stu-id="3d3df-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="3d3df-195">Baixar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="3d3df-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="3d3df-196">Observe que as pastas vazias não são baixadas.</span><span class="sxs-lookup"><span data-stu-id="3d3df-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="3d3df-197">Arquivo: carregar</span><span class="sxs-lookup"><span data-stu-id="3d3df-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="3d3df-198">Carregar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="3d3df-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="3d3df-199">Carregar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="3d3df-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="3d3df-200">Observe que as pastas vazias não são carregadas.</span><span class="sxs-lookup"><span data-stu-id="3d3df-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="3d3df-201">Carregar arquivos que correspondam ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="3d3df-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="3d3df-202">Arquivo: copiar</span><span class="sxs-lookup"><span data-stu-id="3d3df-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="3d3df-203">Copiar entre compartilhamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="3d3df-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="3d3df-204">Quando você copia um arquivo entre compartilhamentos de arquivos, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d3df-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="3d3df-205">Copiar de tooblob de compartilhamento de arquivo</span><span class="sxs-lookup"><span data-stu-id="3d3df-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="3d3df-206">Quando você copia um arquivo de tooblob de compartilhamento de arquivo, uma [cópia do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operação é executada.</span><span class="sxs-lookup"><span data-stu-id="3d3df-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="3d3df-207">Copiar de blob toofile compartilhamento</span><span class="sxs-lookup"><span data-stu-id="3d3df-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="3d3df-208">Quando você copia um arquivo de compartilhamento de toofile de blob, um [cópia do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operação é executada.</span><span class="sxs-lookup"><span data-stu-id="3d3df-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="3d3df-209">Copiar arquivos de forma síncrona</span><span class="sxs-lookup"><span data-stu-id="3d3df-209">Synchronously copy files</span></span>
<span data-ttu-id="3d3df-210">Você pode especificar Olá `--sync-copy` opção toocopy dados do armazenamento de arquivo tooFile armazenamento, de armazenamento de arquivo tooBlob armazenamento e de armazenamento de Blob tooFile armazenamento de forma síncrona.</span><span class="sxs-lookup"><span data-stu-id="3d3df-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="3d3df-211">AzCopy executa esta operação por memória de toolocal de dados de origem Olá o download e, em seguida, carregá-lo toodestination.</span><span class="sxs-lookup"><span data-stu-id="3d3df-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="3d3df-212">Nesse caso, se aplica o custo de saída padrão.</span><span class="sxs-lookup"><span data-stu-id="3d3df-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="3d3df-213">Ao copiar do armazenamento de arquivo tooBlob armazenamento, tipo de blob saudação padrão é o blob de blocos, o usuário pode especificar a opção `/BlobType:page` toochange tipo de blob de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d3df-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="3d3df-214">Observe que `--sync-copy` pode gerar saída adicional comparando cópia de tooasynchronous de custo.</span><span class="sxs-lookup"><span data-stu-id="3d3df-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="3d3df-215">Olá a abordagem recomendada é toouse essa opção em uma VM do Azure, que está em Olá mesma região que o custo de egresso fonte armazenamento conta tooavoid.</span><span class="sxs-lookup"><span data-stu-id="3d3df-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="3d3df-216">Outros recursos do AzCopy</span><span class="sxs-lookup"><span data-stu-id="3d3df-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="3d3df-217">Copiar somente os dados que não existem no destino de saudação</span><span class="sxs-lookup"><span data-stu-id="3d3df-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="3d3df-218">Olá `--exclude-older` e `--exclude-newer` parâmetros permitem que os recursos de origem mais antiga ou mais recente de tooexclude que está sendo copiado, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="3d3df-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="3d3df-219">Se você desejar somente toocopy os recursos de origem que não existem no destino Olá, você pode especificar ambos os parâmetros em Olá AzCopy comando:</span><span class="sxs-lookup"><span data-stu-id="3d3df-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="3d3df-220">Usar parâmetros de linha de comando do arquivo toospecify uma configuração</span><span class="sxs-lookup"><span data-stu-id="3d3df-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="3d3df-221">É possível incluir qualquer parâmetro de linha de comando do AzCopy em um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="3d3df-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="3d3df-222">AzCopy processos Olá parâmetros no arquivo hello como se eles tivessem sido especificados na linha de comando hello, executar uma substituição direta com o conteúdo de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="3d3df-223">Suponha que um arquivo de configuração chamado `copyoperation`, que contém Olá linhas a seguir.</span><span class="sxs-lookup"><span data-stu-id="3d3df-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="3d3df-224">Cada parâmetro do AzCopy pode ser especificado em uma única linha.</span><span class="sxs-lookup"><span data-stu-id="3d3df-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="3d3df-225">ou, em linhas separadas:</span><span class="sxs-lookup"><span data-stu-id="3d3df-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="3d3df-226">AzCopy falhará se você dividir o parâmetro hello em duas linhas, conforme mostrado aqui para Olá `--source-key` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="3d3df-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="3d3df-227">Especificar uma SAS</span><span class="sxs-lookup"><span data-stu-id="3d3df-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="3d3df-228">Você também pode especificar uma SAS no URI do contêiner hello:</span><span class="sxs-lookup"><span data-stu-id="3d3df-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="3d3df-229">Observe que AzCopy atualmente suporta apenas Olá [SAS conta](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="3d3df-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="3d3df-230">Pasta de arquivo de diário</span><span class="sxs-lookup"><span data-stu-id="3d3df-230">Journal file folder</span></span>
<span data-ttu-id="3d3df-231">Cada vez que você emitir um comando tooAzCopy, ele verifica se um arquivo de diário existe na pasta padrão de hello, ou se ela existir em uma pasta que você especificou com esta opção.</span><span class="sxs-lookup"><span data-stu-id="3d3df-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="3d3df-232">Se o arquivo de diário Olá não existir em qualquer lugar, AzCopy trata operação hello como novo e gera um novo arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="3d3df-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="3d3df-233">Se existir um arquivo de diário hello, o AzCopy verifica se o hello linha de comando que você inserir coincide com a saudação de linha de comando no arquivo de diário hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="3d3df-234">Se duas linhas de comando Olá corresponder, AzCopy reinicia a operação de incompleta de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d3df-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="3d3df-235">Se eles não corresponderem, AzCopy solicita usuário tooeither substituir Olá diário arquivo toostart uma nova operação ou a operação atual do toocancel hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="3d3df-236">Se desejar que o local do toouse saudação padrão para o arquivo de diário hello:</span><span class="sxs-lookup"><span data-stu-id="3d3df-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="3d3df-237">Se você omitir a opção `--resume`, ou especifique a opção `--resume` sem o caminho da pasta hello, como mostrado acima, AzCopy cria o arquivo de diário Olá no local padrão de saudação, que é `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="3d3df-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="3d3df-238">Se já existir um arquivo de diário Olá, AzCopy retoma operação Olá com base no arquivo de diário hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="3d3df-239">Se você desejar toospecify um local personalizado para o arquivo de diário hello:</span><span class="sxs-lookup"><span data-stu-id="3d3df-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="3d3df-240">Este exemplo cria o arquivo de diário Olá se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="3d3df-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="3d3df-241">Se ele existir, AzCopy retoma operação Olá com base no arquivo de diário hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="3d3df-242">Se você desejar tooresume uma operação AzCopy, repita Olá mesmo comando.</span><span class="sxs-lookup"><span data-stu-id="3d3df-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="3d3df-243">Em seguida, o AzCopy no Linux solicitará a confirmação:</span><span class="sxs-lookup"><span data-stu-id="3d3df-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="3d3df-244">Logs detalhados de saída</span><span class="sxs-lookup"><span data-stu-id="3d3df-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="3d3df-245">Saudação de número de operações simultâneas toostart</span><span class="sxs-lookup"><span data-stu-id="3d3df-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="3d3df-246">Opção `--parallel-level` Especifica o número de saudação de operações simultâneas de cópia.</span><span class="sxs-lookup"><span data-stu-id="3d3df-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="3d3df-247">Por padrão, AzCopy inicia um determinado número de operações simultâneas tooincrease Olá transferência de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="3d3df-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="3d3df-248">saudação de número de operações simultâneas é igual Olá de oito vezes o número de processadores que você tem.</span><span class="sxs-lookup"><span data-stu-id="3d3df-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="3d3df-249">Se você estiver executando o AzCopy através de uma rede de baixa largura de banda, você pode especificar um número mais baixo para - falhas no nível de paralelo tooavoid causado por divisão dos recursos.</span><span class="sxs-lookup"><span data-stu-id="3d3df-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="3d3df-250">lista completa de saudação tooview AzCopy parâmetros, check-out 'azcopy – Ajuda' menu.</span><span class="sxs-lookup"><span data-stu-id="3d3df-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="3d3df-251">Problemas conhecidos e melhores práticas</span><span class="sxs-lookup"><span data-stu-id="3d3df-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="3d3df-252">Erro: O .NET Core não é encontrado no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d3df-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="3d3df-253">Se você encontrar um erro informando que o núcleo do .NET não está instalado no sistema hello, Olá binário de .NET Core toohello caminho `dotnet` podem estar ausentes.</span><span class="sxs-lookup"><span data-stu-id="3d3df-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="3d3df-254">Em ordem tooaddress esse problema, localize o binário do .NET Core Olá no sistema de saudação:</span><span class="sxs-lookup"><span data-stu-id="3d3df-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="3d3df-255">Isso retorna Olá caminho toohello dotnet binário.</span><span class="sxs-lookup"><span data-stu-id="3d3df-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="3d3df-256">Agora, adicione essa variável de caminho de toohello de caminho.</span><span class="sxs-lookup"><span data-stu-id="3d3df-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="3d3df-257">Sudo, edite secure_path toocontain Olá caminho toohello dotnet binário:</span><span class="sxs-lookup"><span data-stu-id="3d3df-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="3d3df-258">Neste exemplo, a variável secure_path é:</span><span class="sxs-lookup"><span data-stu-id="3d3df-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="3d3df-259">Para o usuário atual do hello, editar.bash_profile/.profile tooinclude Olá caminho toohello dotnet binário na variável PATH</span><span class="sxs-lookup"><span data-stu-id="3d3df-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="3d3df-260">Verifique se o .NET Core agora está em PATH:</span><span class="sxs-lookup"><span data-stu-id="3d3df-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="3d3df-261">Erro ao instalar o AzCopy</span><span class="sxs-lookup"><span data-stu-id="3d3df-261">Error Installing AzCopy</span></span>
<span data-ttu-id="3d3df-262">Se você tiver problemas com a instalação de AzCopy, você pode tentar toorun AzCopy usando scripts de bash Olá em Olá extraído `azcopy` pasta.</span><span class="sxs-lookup"><span data-stu-id="3d3df-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="3d3df-263">Limite gravações simultâneas durante a cópia de dados</span><span class="sxs-lookup"><span data-stu-id="3d3df-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="3d3df-264">Quando você copia blobs ou arquivos com AzCopy, tenha em mente que outro aplicativo esteja modificando dados saudação enquanto você estiver copiando-lo.</span><span class="sxs-lookup"><span data-stu-id="3d3df-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="3d3df-265">Se possível, certifique-se de que dados Olá que você está copiando não está sendo modificados durante a operação de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d3df-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="3d3df-266">Por exemplo, ao copiar um VHD associado a uma máquina virtual do Azure, certifique-se de que nenhum outro aplicativo no momento está escrevendo toohello VHD.</span><span class="sxs-lookup"><span data-stu-id="3d3df-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="3d3df-267">Toodo uma boa maneira trata concedendo Olá recurso toobe copiado.</span><span class="sxs-lookup"><span data-stu-id="3d3df-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="3d3df-268">Como alternativa, você pode criar um instantâneo de saudação VHD primeiro e copie instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="3d3df-269">Se você não pode impedir que outros aplicativos gravando tooblobs ou arquivos enquanto eles estão sendo copiados, em seguida, tenha em mente que, pelo trabalho de Olá Olá tempo termina, hello recursos copiados não podem mais ter paridade completa com os recursos de origem hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="3d3df-270">Execute uma instância de AzCopy em um computador.</span><span class="sxs-lookup"><span data-stu-id="3d3df-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="3d3df-271">AzCopy é projetado toomaximize Olá utilização sua máquina recurso tooaccelerate Olá de transferência de dados, é recomendável executar apenas uma instância de AzCopy em um computador e especificar a opção Olá `--parallel-level` se você precisar de operações simultâneas mais.</span><span class="sxs-lookup"><span data-stu-id="3d3df-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="3d3df-272">Para obter mais detalhes, digite `AzCopy --help parallel-level` na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="3d3df-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d3df-273">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d3df-273">Next steps</span></span>
<span data-ttu-id="3d3df-274">Para obter mais informações sobre o armazenamento do Azure e AzCopy, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d3df-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="3d3df-275">Documentação do Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="3d3df-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="3d3df-276">Introdução tooAzure armazenamento</span><span class="sxs-lookup"><span data-stu-id="3d3df-276">Introduction tooAzure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="3d3df-277">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3d3df-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="3d3df-278">Gerenciar blobs com o Gerenciador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="3d3df-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="3d3df-279">Usando Olá 2.0 do CLI do Azure com o armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3d3df-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="3d3df-280">Como toouse armazenamento de Blob de C++</span><span class="sxs-lookup"><span data-stu-id="3d3df-280">How toouse Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="3d3df-281">Como toouse armazenamento de Blob do Java</span><span class="sxs-lookup"><span data-stu-id="3d3df-281">How toouse Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="3d3df-282">Como toouse armazenamento de Blob do Node. js</span><span class="sxs-lookup"><span data-stu-id="3d3df-282">How toouse Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="3d3df-283">Como toouse armazenamento de Blob do Python</span><span class="sxs-lookup"><span data-stu-id="3d3df-283">How toouse Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="3d3df-284">Postagens de blog de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="3d3df-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="3d3df-285">Anunciando a Versão Prévia do AzCopy no Linux</span><span class="sxs-lookup"><span data-stu-id="3d3df-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="3d3df-286">Apresentando a versão de visualização da biblioteca de movimentação de dados do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3d3df-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="3d3df-287">AzCopy: Introducing synchronous copy and customized content type (AzCopy: introdução a cópia síncrona e tipo de conteúdo personalizado)</span><span class="sxs-lookup"><span data-stu-id="3d3df-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="3d3df-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support (AzCopy: anúncio de disponibilidade geral do AzCopy 3.0 mais versão de teste do AzCopy 4.0 com suporte para Tabela e Arquivo)</span><span class="sxs-lookup"><span data-stu-id="3d3df-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="3d3df-289">AzCopy: Optimized for Large-Scale Copy Scenarios (AzCopy: otimizado para cenários de cópia em larga escala)</span><span class="sxs-lookup"><span data-stu-id="3d3df-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="3d3df-290">AzCopy: Support for read-access geo-redundant storage (AzCopy: suporte para o armazenamento com redundância geográfica com acesso de leitura)</span><span class="sxs-lookup"><span data-stu-id="3d3df-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="3d3df-291">AzCopy: Transferir dados com o modo reiniciável e um token SAS</span><span class="sxs-lookup"><span data-stu-id="3d3df-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="3d3df-292">AzCopy: Using cross-account Copy Blob (AzCopy: usando blob de cópia em várias contas)</span><span class="sxs-lookup"><span data-stu-id="3d3df-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="3d3df-293">AzCopy: Uploading/downloading files for Azure Blobs (AzCopy: Upload/download de arquivos para Blobs do Azure)</span><span class="sxs-lookup"><span data-stu-id="3d3df-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

