---
title: Copiar ou mover dados para o Armazenamento do Azure com o AzCopy no Windows | Microsoft Docs
description: "Use o utilitário AzCopy no Windows para mover ou copiar dados para ou de conteúdo de blob, tabela e arquivo. Copie dados para o Armazenamento do Azure de arquivos locais ou copie dados dentro na mesma conta ou entre contas de armazenamento. Migre facilmente seus dados para o Armazenamento do Azure."
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
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: 9806697747b2409d4bd0ae19dc0b9fe01f500dc0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a><span data-ttu-id="b1103-105">Transferir dados com AzCopy no Windows</span><span class="sxs-lookup"><span data-stu-id="b1103-105">Transfer data with the AzCopy on Windows</span></span>
<span data-ttu-id="b1103-106">O AzCopy é um utilitário de linha de comando projetado para copiar dados entre o Armazenamento de Blobs, de Arquivos e de Tabelas do Microsoft Azure usando comandos simples com o desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="b1103-106">AzCopy is a command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="b1103-107">Você pode copiar dados de um objeto para outro dentro de sua conta de armazenamento, ou entre contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b1103-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="b1103-108">Há duas versões do AzCopy que podem ser baixadas.</span><span class="sxs-lookup"><span data-stu-id="b1103-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="b1103-109">O AzCopy no Windows se baseia no .NET Framework e oferece opções de linha de comando no estilo Windows.</span><span class="sxs-lookup"><span data-stu-id="b1103-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="b1103-110">O [AzCopy no Linux](storage-use-azcopy-linux.md) se baseia no .NET Core Framework, que se destina a plataformas Linux que oferecem opções de linha de comando no estilo POSIX.</span><span class="sxs-lookup"><span data-stu-id="b1103-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="b1103-111">Este artigo aborda o AzCopy no Windows.</span><span class="sxs-lookup"><span data-stu-id="b1103-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="b1103-112">Baixar e instalar o AzCopy</span><span class="sxs-lookup"><span data-stu-id="b1103-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="b1103-113">AzCopy no Windows</span><span class="sxs-lookup"><span data-stu-id="b1103-113">AzCopy on Windows</span></span>
<span data-ttu-id="b1103-114">Baixe a [versão mais recente do AzCopy no Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="b1103-114">Download the [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="b1103-115">Instalação no Windows</span><span class="sxs-lookup"><span data-stu-id="b1103-115">Installation on Windows</span></span>
<span data-ttu-id="b1103-116">Depois de instalar o AzCopy no Windows usando o instalador, abra uma janela de comando e navegue até o diretório de instalação do AzCopy em seu computador, onde o executável `AzCopy.exe` está localizado.</span><span class="sxs-lookup"><span data-stu-id="b1103-116">After installing AzCopy on Windows using the installer, open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="b1103-117">Se quiser, você pode alterar o local da instalação do AzCopy para o caminho do sistema.</span><span class="sxs-lookup"><span data-stu-id="b1103-117">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="b1103-118">Por padrão, o AzCopy é instalado em `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` ou em `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="b1103-118">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="b1103-119">Como escrever seu primeiro comando do AzCopy</span><span class="sxs-lookup"><span data-stu-id="b1103-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="b1103-120">A sintaxe básica dos comandos do AzCopy é:</span><span class="sxs-lookup"><span data-stu-id="b1103-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="b1103-121">Os exemplos a seguir demonstram vários cenários para cópia de dados entre os Blobs, os Arquivos e as Tabelas do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b1103-121">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="b1103-122">Confira a seção [Parâmetros do AzCopy](#azcopy-parameters) para obter uma explicação detalhada dos parâmetros usados em cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="b1103-122">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="b1103-123">Blob: baixar</span><span class="sxs-lookup"><span data-stu-id="b1103-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="b1103-124">Baixar um único blob</span><span class="sxs-lookup"><span data-stu-id="b1103-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="b1103-125">Observe que se a pasta `C:\myfolder` não existir, o AzCopy a criará e baixará `abc.txt ` na nova pasta.</span><span class="sxs-lookup"><span data-stu-id="b1103-125">Note that if the folder `C:\myfolder` does not exist, AzCopy creates it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="b1103-126">Baixe um único blob de região secundária</span><span class="sxs-lookup"><span data-stu-id="b1103-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="b1103-127">Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.</span><span class="sxs-lookup"><span data-stu-id="b1103-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="b1103-128">Baixar todos os blobs</span><span class="sxs-lookup"><span data-stu-id="b1103-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="b1103-129">Suponhamos que os seguintes blobs residam no contêiner especificado:</span><span class="sxs-lookup"><span data-stu-id="b1103-129">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="b1103-130">Após a operação de download, o diretório `C:\myfolder` inclui os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="b1103-130">After the download operation, the directory `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="b1103-131">Se você não especificar a opção `/S`, nenhum blob será baixado.</span><span class="sxs-lookup"><span data-stu-id="b1103-131">If you do not specify option `/S`, no blobs are downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="b1103-132">Baixar blobs com prefixo especificado</span><span class="sxs-lookup"><span data-stu-id="b1103-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="b1103-133">Suponhamos que os blobs a seguir residam no contêiner especificado.</span><span class="sxs-lookup"><span data-stu-id="b1103-133">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="b1103-134">Todos os blobs que começam com o prefixo `a` são baixados:</span><span class="sxs-lookup"><span data-stu-id="b1103-134">All blobs beginning with the prefix `a` are downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="b1103-135">Após a operação de download, a pasta `C:\myfolder` inclui os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="b1103-135">After the download operation, the folder `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="b1103-136">O prefixo se aplica ao diretório virtual, que forma a primeira parte do nome do blob.</span><span class="sxs-lookup"><span data-stu-id="b1103-136">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="b1103-137">No exemplo mostrado acima, como não corresponde ao prefixo especificado, o diretório virtual não é baixado.</span><span class="sxs-lookup"><span data-stu-id="b1103-137">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="b1103-138">Além disso, se a opção `\S` não for especificada, o AzCopy não baixará nenhum blob.</span><span class="sxs-lookup"><span data-stu-id="b1103-138">In addition, if the option `\S` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="b1103-139">Defina a hora da última modificação dos arquivos exportados como sendo a mesma dos blobs de origem</span><span class="sxs-lookup"><span data-stu-id="b1103-139">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="b1103-140">Você também pode excluir blobs da operação de download com base na hora da última modificação</span><span class="sxs-lookup"><span data-stu-id="b1103-140">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="b1103-141">Por exemplo, se você quiser excluir blobs cuja hora da última modificação for a mesma ou mais recente do que o arquivo de destino, adicione a opção `/XN`:</span><span class="sxs-lookup"><span data-stu-id="b1103-141">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="b1103-142">Ou, se você quiser excluir blobs cuja hora da última modificação for a mesma ou mais antiga do que o arquivo de destino, adicione a opção `/XO`:</span><span class="sxs-lookup"><span data-stu-id="b1103-142">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="b1103-143">Blob: carregar</span><span class="sxs-lookup"><span data-stu-id="b1103-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="b1103-144">Carregar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="b1103-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="b1103-145">Se o contêiner de destino especificado não existir, o AzCopy o criará e carregará o arquivo nele.</span><span class="sxs-lookup"><span data-stu-id="b1103-145">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="b1103-146">Carregar arquivo único no diretório virtual</span><span class="sxs-lookup"><span data-stu-id="b1103-146">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="b1103-147">Se o diretório virtual especificado não existir, o AzCopy carregará o arquivo para incluir o diretório virtual em seu nome (*por exemplo*, `vd/abc.txt` no exemplo acima).</span><span class="sxs-lookup"><span data-stu-id="b1103-147">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="b1103-148">Carregar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="b1103-149">A especificação da opção `/S` carrega o conteúdo do diretório especificado no Armazenamento de blobs de maneira recursiva, o que significa que todas as subpastas e seus arquivos são carregados também.</span><span class="sxs-lookup"><span data-stu-id="b1103-149">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="b1103-150">Por exemplo, suponhamos que os seguintes arquivos residam na pasta `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="b1103-150">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="b1103-151">Após a operação de upload, o contêiner incluirá os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="b1103-151">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="b1103-152">Se você não especificar a opção `/S`, o AzCopy não carregará de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="b1103-152">If you do not specify option `/S`, AzCopy does not upload recursively.</span></span> <span data-ttu-id="b1103-153">Após a operação de upload, o contêiner incluirá os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="b1103-153">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="b1103-154">Carregar arquivos que correspondam ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="b1103-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="b1103-155">Vamos supor que a pasta `C:\myfolder`contenha os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="b1103-155">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="b1103-156">Após a operação de upload, o contêiner incluirá os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="b1103-156">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="b1103-157">Se você não especificar a opção `/S`, o AzCopy carregará somente os blobs que não residem em um diretório virtual:</span><span class="sxs-lookup"><span data-stu-id="b1103-157">If you do not specify option `/S`, AzCopy only uploads blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="b1103-158">Especificar o tipo de conteúdo MIME de um blob de destino</span><span class="sxs-lookup"><span data-stu-id="b1103-158">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="b1103-159">Por padrão, o AzCopy define o tipo de conteúdo de um blob de destino para `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="b1103-159">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="b1103-160">A partir da versão 3.1.0, você pode especificar explicitamente o tipo de conteúdo por meio da opção `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="b1103-160">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="b1103-161">Essa sintaxe define o tipo de conteúdo para todos os blobs em uma operação de carregamento.</span><span class="sxs-lookup"><span data-stu-id="b1103-161">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="b1103-162">Se você especificar `/SetContentType` sem um valor, o AzCopy definirá o tipo de conteúdo de cada blob ou arquivo de acordo com sua extensão de arquivo.</span><span class="sxs-lookup"><span data-stu-id="b1103-162">If you specify `/SetContentType` without a value, AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="b1103-163">Blob: copiar</span><span class="sxs-lookup"><span data-stu-id="b1103-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="b1103-164">Copiar um único blob dentro da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b1103-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="b1103-165">Quando você copia um blob em uma conta de armazenamento, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é realizada.</span><span class="sxs-lookup"><span data-stu-id="b1103-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="b1103-166">Copiar um único blob entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b1103-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="b1103-167">Quando você copia um blob entre contas de armazenamento, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é realizada.</span><span class="sxs-lookup"><span data-stu-id="b1103-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="b1103-168">Copiar um único blob de região secundária para região primária</span><span class="sxs-lookup"><span data-stu-id="b1103-168">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="b1103-169">Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.</span><span class="sxs-lookup"><span data-stu-id="b1103-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="b1103-170">Copiar um único blob e seus instantâneos entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b1103-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="b1103-171">Após a operação de cópia, o contêiner de destino incluirá o blob e seus instantâneos.</span><span class="sxs-lookup"><span data-stu-id="b1103-171">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="b1103-172">Supondo que o blob no exemplo acima tenha dois instantâneos, o contêiner incluirá os seguintes blob e instantâneos:</span><span class="sxs-lookup"><span data-stu-id="b1103-172">Assuming the blob in the example above has two snapshots, the container includes the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="b1103-173">Copiar blobs em regiões entre contas de armazenamento de forma síncrona.</span><span class="sxs-lookup"><span data-stu-id="b1103-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="b1103-174">O AzCopy por padrão copia dados entre dois pontos de extremidade de armazenamento assincronamente.</span><span class="sxs-lookup"><span data-stu-id="b1103-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="b1103-175">Portanto, a operação de cópia é executada em segundo plano usando a capacidade de largura de banda extra, sem nenhum SLA em termos da velocidade de como o blob é copiado, e o AzCopy verifica periodicamente o status da cópia até que a cópia esteja concluída ou tenha ocorrido uma falha.</span><span class="sxs-lookup"><span data-stu-id="b1103-175">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied, and AzCopy periodically checks the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="b1103-176">A opção `/SyncCopy` garante que a operação de cópia obtém uma velocidade consistente.</span><span class="sxs-lookup"><span data-stu-id="b1103-176">The `/SyncCopy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="b1103-177">O AzCopy realiza a cópia síncrona baixando os blobs para copiar da fonte especificada para a memória local, e, em seguida, carregá-los para o destino de armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="b1103-177">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="b1103-178">Talvez o `/SyncCopy` gere um custo de saída adicional comparando à cópia assíncrona. A abordagem recomendada é usar essa opção na VM do Azure que está na mesma região que a sua conta de armazenamento de origem, a fim de evitar o custo de saída.</span><span class="sxs-lookup"><span data-stu-id="b1103-178">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="b1103-179">Arquivo: baixar</span><span class="sxs-lookup"><span data-stu-id="b1103-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="b1103-180">Baixar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="b1103-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="b1103-181">Se a origem especificada for um compartilhamento de arquivos do Azure, você deverá especificar o nome exato do arquivo, (*por exemplo*, `abc.txt`) para baixar um único arquivo ou especificar a opção `/S` para baixar todos os arquivos do compartilhamento de maneira recursiva.</span><span class="sxs-lookup"><span data-stu-id="b1103-181">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="b1103-182">A tentativa de especificar um padrão de arquivo e a opção `/S` simultaneamente resulta em um erro.</span><span class="sxs-lookup"><span data-stu-id="b1103-182">Attempting to specify both a file pattern and option `/S` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="b1103-183">Baixar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="b1103-184">Observe que as pastas vazias não são baixadas.</span><span class="sxs-lookup"><span data-stu-id="b1103-184">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="b1103-185">Arquivo: carregar</span><span class="sxs-lookup"><span data-stu-id="b1103-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="b1103-186">Carregar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="b1103-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="b1103-187">Carregar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="b1103-188">Observe que as pastas vazias não são carregadas.</span><span class="sxs-lookup"><span data-stu-id="b1103-188">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="b1103-189">Carregar arquivos que correspondam ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="b1103-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="b1103-190">Arquivo: copiar</span><span class="sxs-lookup"><span data-stu-id="b1103-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="b1103-191">Copiar entre compartilhamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="b1103-192">Quando você copia um arquivo entre compartilhamentos de arquivos, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1103-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="b1103-193">Copiar de compartilhamento de arquivos para blob</span><span class="sxs-lookup"><span data-stu-id="b1103-193">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="b1103-194">Quando você copia um arquivo do compartilhamento de arquivos no blob, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1103-194">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="b1103-195">Copiar do blob para compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-195">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="b1103-196">Quando você copia um arquivo do blob no compartilhamentos de arquivos, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1103-196">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="b1103-197">Copiar arquivos de forma síncrona</span><span class="sxs-lookup"><span data-stu-id="b1103-197">Synchronously copy files</span></span>
<span data-ttu-id="b1103-198">Você pode especificar a opção `/SyncCopy` para copiar dados do Armazenamento de Arquivos para o Armazenamento de Arquivos, do Armazenamento de Arquivos para o Armazenamento de Blobs e vice-versa de forma síncrona. O AzCopy faz isso baixando os dados de origem para a memória local e carregando-os novamente no destino.</span><span class="sxs-lookup"><span data-stu-id="b1103-198">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="b1103-199">O custo de saída padrão se aplica.</span><span class="sxs-lookup"><span data-stu-id="b1103-199">Standard egress cost applies.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="b1103-200">Durante a cópia do Armazenamento de Arquivos para o Armazenamento de Blobs, o tipo de blob padrão é o blob de blocos, e o usuário pode especificar a opção `/BlobType:page` para alterar o tipo de blob de destino.</span><span class="sxs-lookup"><span data-stu-id="b1103-200">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="b1103-201">Observe que `/SyncCopy` pode gerar custo de saída adicional comparando a cópia assíncrona. A abordagem recomendada é usar essa opção na VM do Azure que está na mesma região que a sua conta de armazenamento de origem para evitar o custo de saída.</span><span class="sxs-lookup"><span data-stu-id="b1103-201">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="b1103-202">Tabela: exportar</span><span class="sxs-lookup"><span data-stu-id="b1103-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="b1103-203">Exportar tabela</span><span class="sxs-lookup"><span data-stu-id="b1103-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="b1103-204">O AzCopy grava um arquivo de manifesto na pasta de destino especificada.</span><span class="sxs-lookup"><span data-stu-id="b1103-204">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="b1103-205">O arquivo do manifesto é usado pelo processo de importação para localizar os arquivos de dados necessários e executar a validação de dados.</span><span class="sxs-lookup"><span data-stu-id="b1103-205">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="b1103-206">O arquivo de manifesto usa a seguinte convenção de nomenclatura por padrão:</span><span class="sxs-lookup"><span data-stu-id="b1103-206">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="b1103-207">O usuário também pode especificar a opção `/Manifest:<manifest file name>` para definir o nome do arquivo de manifesto.</span><span class="sxs-lookup"><span data-stu-id="b1103-207">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="b1103-208">Dividir exportação em vários arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="b1103-209">O AzCopy usa um *índice de volume* nos nomes dos arquivos de dados da divisão para diferenciar diversos arquivos.</span><span class="sxs-lookup"><span data-stu-id="b1103-209">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="b1103-210">O índice do volume é composto em duas partes: um *índice de intervalo de chaves de partição* e um *índice de arquivos de divisão*.</span><span class="sxs-lookup"><span data-stu-id="b1103-210">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="b1103-211">Os dois índices são de base zero.</span><span class="sxs-lookup"><span data-stu-id="b1103-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="b1103-212">O índice do intervalo de chaves de partição será 0 se o usuário não especificar a opção `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="b1103-212">The partition key range index is 0 if the user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="b1103-213">Por exemplo, digamos que o AzCopy gere dois arquivos de dados depois que o usuário especifica a opção `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="b1103-213">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="b1103-214">Os nomes dos arquivos de dados resultantes podem ser:</span><span class="sxs-lookup"><span data-stu-id="b1103-214">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="b1103-215">Observe que o menor valor possível para a opção `/SplitSize` é 32 MB.</span><span class="sxs-lookup"><span data-stu-id="b1103-215">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="b1103-216">Se o destino especificado for um armazenamento de Blobs, o AzCopy dividirá o arquivo de dados quando alcançar o tamanho limite do blob (200 GB), sem levar em conta se o usuário especificou ou não a opção `/SplitSize` .</span><span class="sxs-lookup"><span data-stu-id="b1103-216">If the specified destination is Blob storage, AzCopy splits the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="b1103-217">Exportar tabela para o formato de arquivo de dados JSON ou CSV</span><span class="sxs-lookup"><span data-stu-id="b1103-217">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="b1103-218">Por padrão, o AzCopy exporta tabelas para arquivos de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="b1103-218">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="b1103-219">Você pode especificar a opção `/PayloadFormat:JSON|CSV` para exportar as tabelas como JSON ou CSV.</span><span class="sxs-lookup"><span data-stu-id="b1103-219">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="b1103-220">Ao especificar o formato de carga CSV, o AzCopy também gera um arquivo de esquema com extensão `.schema.csv` para cada arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="b1103-220">When specifying the CSV payload format, AzCopy also generates a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="b1103-221">Exportar entidades de tabela simultaneamente</span><span class="sxs-lookup"><span data-stu-id="b1103-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="b1103-222">O AzCopy inicia operações simultâneas para exportar entidades quando o usuário especifica a opção `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="b1103-222">AzCopy starts concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="b1103-223">Cada operação exporta um intervalor de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="b1103-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="b1103-224">Observe que a opção `/NC`também controla a quantidade de operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="b1103-224">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="b1103-225">O AzCopy usa a quantidade de processadores de núcleo como valor padrão de `/NC` ao copiar entidades de tabela, mesmo que `/NC` não tenha sido especificado.</span><span class="sxs-lookup"><span data-stu-id="b1103-225">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="b1103-226">Quando o usuário especifica a opção `/PKRS`, o AzCopy usa o menor valor dos dois valores (intervalos de chaves de partição versus operações simultâneas especificadas implícita ou explicitamente) para determinar quantas operações simultâneas devem ser iniciadas.</span><span class="sxs-lookup"><span data-stu-id="b1103-226">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="b1103-227">Para obter mais detalhes, digite `AzCopy /?:NC` na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="b1103-227">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="b1103-228">Exportar tabela para blob</span><span class="sxs-lookup"><span data-stu-id="b1103-228">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="b1103-229">O AzCopy gerará um arquivo de dados JSON no contêiner do blob, seguindo esta convenção de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="b1103-229">AzCopy generates a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="b1103-230">O arquivo de dados JSON gerado segue o formato de carga para metadados mínimos.</span><span class="sxs-lookup"><span data-stu-id="b1103-230">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="b1103-231">Para obter detalhes sobre esse formado de carga, confira [Formato de carga para operações do serviço Tabela](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1103-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="b1103-232">Observe que ao exportar tabelas para blobs, o AzCopy baixará as entidades de tabela para arquivos de dados temporários locais e, em seguida, carregará essas entidades no blob.</span><span class="sxs-lookup"><span data-stu-id="b1103-232">Note that when exporting tables to blobs, AzCopy downloads the Table entities to local temporary data files and then uploads those entities to the blob.</span></span> <span data-ttu-id="b1103-233">Esses arquivos de dados temporários são colocados na pasta de arquivos do diário com o caminho padrão "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>" e você pode especificar a opção /Z:[pasta-de-arquivo-do-diário] para alterar o local da pasta de arquivo do diário e, portanto, alterar o local dos arquivos de dados temporários.</span><span class="sxs-lookup"><span data-stu-id="b1103-233">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="b1103-234">O tamanho dos arquivos de dados temporários é decidido pelo tamanho das entidades da tabela e pelo tamanho especificado com a opção /SplitSize, embora o arquivo de dados temporários no disco local seja excluído imediatamente após ser carregado no blob, verifique que você tem espaço em disco local suficiente para armazenar esses arquivos de dados temporários antes de serem excluídos.</span><span class="sxs-lookup"><span data-stu-id="b1103-234">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk is deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="b1103-235">Tabela: importar</span><span class="sxs-lookup"><span data-stu-id="b1103-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="b1103-236">Importar tabela</span><span class="sxs-lookup"><span data-stu-id="b1103-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="b1103-237">A opção `/EntityOperation` indica como inserir entidades na tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-237">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="b1103-238">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="b1103-238">Possible values are:</span></span>

* <span data-ttu-id="b1103-239">`InsertOrSkip`: ignora uma entidade existente ou insere uma nova entidade, caso ela não exista na tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="b1103-240">`InsertOrMerge`: mescla uma entidade existente ou insere uma nova entidade, caso ela não exista na tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="b1103-241">`InsertOrReplace`: substitui uma entidade existente ou insere uma nova entidade, caso ela não exista na tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="b1103-242">Observe que não é possível especificar a opção `/PKRS` no cenário de importação.</span><span class="sxs-lookup"><span data-stu-id="b1103-242">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="b1103-243">Diferente do cenário de exportação, no qual é necessário especificar a opção `/PKRS` para iniciar operações simultâneas, o AzCopy inicia as operações simultâneas por padrão quando você importar a tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-243">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy starts concurrent operations by default when you import a table.</span></span> <span data-ttu-id="b1103-244">A quantidade padrão de operações simultâneas iniciadas é igual à quantidade de processadores de núcleo. No entanto, você pode especificar uma quantidade diferente com a opção `/NC`.</span><span class="sxs-lookup"><span data-stu-id="b1103-244">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="b1103-245">Para obter mais detalhes, digite `AzCopy /?:NC` na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="b1103-245">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="b1103-246">Observe que o AzCopy dá suporte apenas à importação para JSON, não para CSV.</span><span class="sxs-lookup"><span data-stu-id="b1103-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="b1103-247">O AzCopy não dá suporte a importações de tabela de arquivos JSON e de manifesto criados pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="b1103-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="b1103-248">Ambos os arquivos devem vir de uma exportação de tabela AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b1103-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="b1103-249">Para evitar erros, não modifique o arquivo JSON ou de manifesto exportado.</span><span class="sxs-lookup"><span data-stu-id="b1103-249">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="b1103-250">Importar entidades na tabela usando blobs</span><span class="sxs-lookup"><span data-stu-id="b1103-250">Import entities to table using blobs</span></span>
<span data-ttu-id="b1103-251">Vamos supor que um contêiner de Blob contenha o seguinte: um arquivo JSON que representa uma Tabela do Azure, e seu arquivo de manifesto.</span><span class="sxs-lookup"><span data-stu-id="b1103-251">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="b1103-252">Você pode executar o comando a seguir para importar entidades em uma tabela usando o arquivo de manifesto nesse mesmo contêiner de blob:</span><span class="sxs-lookup"><span data-stu-id="b1103-252">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="b1103-253">Outros recursos do AzCopy</span><span class="sxs-lookup"><span data-stu-id="b1103-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="b1103-254">Copiar apenas os dados que não existem no destino</span><span class="sxs-lookup"><span data-stu-id="b1103-254">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="b1103-255">Os parâmetros `/XO` e `/XN` permitem a exclusão de recursos de origem mais antigos ou mais recentes da cópia, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b1103-255">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="b1103-256">Se você quiser copiar apenas os recursos de origem que não existem no destino, especifique os dois parâmetros no comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="b1103-256">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="b1103-257">Observe que isso não terá suporte quando a origem ou o destino for uma tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-257">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="b1103-258">Usar um arquivo de resposta para especificar parâmetros de linha de comando</span><span class="sxs-lookup"><span data-stu-id="b1103-258">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="b1103-259">É possível incluir qualquer parâmetro de linha de comando do AZCopy em um arquivo de resposta.</span><span class="sxs-lookup"><span data-stu-id="b1103-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="b1103-260">O AzCopy processa os parâmetros no arquivo como se eles tivessem sido especificados na linha de comando, realizando uma substituição direta pelo conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="b1103-260">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="b1103-261">Vamos supor que um arquivo de resposta chamado `copyoperation.txt`contenha as linhas a seguir.</span><span class="sxs-lookup"><span data-stu-id="b1103-261">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="b1103-262">Cada parâmetro do AzCopy pode ser especificado em uma única linha</span><span class="sxs-lookup"><span data-stu-id="b1103-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="b1103-263">ou, em linhas separadas:</span><span class="sxs-lookup"><span data-stu-id="b1103-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="b1103-264">O AzCopy falhará se você dividir o parâmetro em duas linhas, conforme mostrado aqui para o parâmetro `/sourcekey`:</span><span class="sxs-lookup"><span data-stu-id="b1103-264">AzCopy fails if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="b1103-265">Usar vários arquivos de resposta para especificar parâmetros de linha de comando</span><span class="sxs-lookup"><span data-stu-id="b1103-265">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="b1103-266">Vamos supor um arquivo de resposta chamado `source.txt` que especifique um contêiner de origem:</span><span class="sxs-lookup"><span data-stu-id="b1103-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="b1103-267">E um arquivo de resposta chamado `dest.txt` que especifique uma pasta de destino no sistema de arquivos:</span><span class="sxs-lookup"><span data-stu-id="b1103-267">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="b1103-268">E um arquivo de resposta chamado `options.txt` que especifique opções para o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="b1103-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="b1103-269">Para chamar o AzCopy usando esses arquivos de resposta, todos eles residindo em um diretório `C:\responsefiles`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="b1103-269">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="b1103-270">O AzCopy processa esse comando assim como faria se você tivesse incluído todos os parâmetros individuais na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="b1103-270">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="b1103-271">Especificar uma SAS</span><span class="sxs-lookup"><span data-stu-id="b1103-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="b1103-272">Você também pode especificar um SAS no URI do contêiner:</span><span class="sxs-lookup"><span data-stu-id="b1103-272">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="b1103-273">Pasta de arquivo de diário</span><span class="sxs-lookup"><span data-stu-id="b1103-273">Journal file folder</span></span>
<span data-ttu-id="b1103-274">Sempre que você emite um comando para o AzCopy, ele verifica se um arquivo de diário existe na pasta padrão ou se está em uma pasta especificada por meio dessa opção.</span><span class="sxs-lookup"><span data-stu-id="b1103-274">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="b1103-275">Se o arquivo de diário não estiver em nenhum dos lugares, o AzCopy tratará a operação como nova e gerar um novo arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="b1103-275">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="b1103-276">Se o arquivo de diário existir, o AzCopy verificará se a linha de comando inserida corresponde à linha de comando no arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="b1103-276">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="b1103-277">Se as duas linhas de comando forem correspondentes, o AzCopy retomará a operação incompleta.</span><span class="sxs-lookup"><span data-stu-id="b1103-277">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="b1103-278">Se elas não forem correspondentes, será solicitado que você substitua o arquivo de diário para iniciar uma nova operação ou que cancele a operação atual.</span><span class="sxs-lookup"><span data-stu-id="b1103-278">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="b1103-279">Se você quiser usar o local padrão para o arquivo de diário:</span><span class="sxs-lookup"><span data-stu-id="b1103-279">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="b1103-280">Se você omitir a opção `/Z` ou especificar a opção `/Z` sem o caminho da pasta, conforme mostrado acima, o AzCopy criará o arquivo de diário no local padrão, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="b1103-280">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="b1103-281">Se o arquivo de diário já existir, o AzCopy retomará a operação com base no arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="b1103-281">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="b1103-282">Se você quiser especificar um local personalizado para o arquivo de diário:</span><span class="sxs-lookup"><span data-stu-id="b1103-282">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="b1103-283">Este exemplo criará o arquivo de diário se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="b1103-283">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="b1103-284">Se ele existir, o AzCopy retomará a operação com base no arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="b1103-284">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="b1103-285">Se você quiser retomar uma operação do AzCopy:</span><span class="sxs-lookup"><span data-stu-id="b1103-285">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="b1103-286">Este exemplo retoma a última operação, cuja conclusão pode ter falhado.</span><span class="sxs-lookup"><span data-stu-id="b1103-286">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="b1103-287">Gerar um arquivo de log</span><span class="sxs-lookup"><span data-stu-id="b1103-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="b1103-288">Se você especificar a opção `/V` sem fornecer um caminho de arquivo para o log detalhado, o AzCopy criará o arquivo de log no local padrão, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="b1103-288">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="b1103-289">Caso contrário, você pode criar um arquivo de log em um local personalizado:</span><span class="sxs-lookup"><span data-stu-id="b1103-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="b1103-290">Observe que, se você especificar um caminho relativo depois da opção `/V`, como `/V:test/azcopy1.log`, o log detalhado será criado no diretório de trabalho atual dentro de uma subpasta chamada `test`.</span><span class="sxs-lookup"><span data-stu-id="b1103-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="b1103-291">Especificar o número de operações simultâneas para começar</span><span class="sxs-lookup"><span data-stu-id="b1103-291">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="b1103-292">A opção `/NC` especifica o número de operações de cópia simultâneas.</span><span class="sxs-lookup"><span data-stu-id="b1103-292">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="b1103-293">Por padrão, o AzCopy inicia uma determinada quantidade de operações simultâneas para aumentar a taxa de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="b1103-293">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="b1103-294">Para operações de tabela, o número de operações simultâneas é igual ao número de processadores que você tem.</span><span class="sxs-lookup"><span data-stu-id="b1103-294">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="b1103-295">Para operações de blob e arquivo, o número de operações simultâneas é igual a oito vezes o número de processadores que você tem.</span><span class="sxs-lookup"><span data-stu-id="b1103-295">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="b1103-296">Se estiver executando o AzCopy em uma rede de baixa largura de banda, você poderá especificar um número menor para essa /NC a fim de evitar uma falha causada pela concorrência de recursos.</span><span class="sxs-lookup"><span data-stu-id="b1103-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="b1103-297">Executar o AzCopy em um emulador de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b1103-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="b1103-298">Você pode executar o AzCopy no [emulador de armazenamento do Azure](storage-use-emulator.md) para Blobs:</span><span class="sxs-lookup"><span data-stu-id="b1103-298">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="b1103-299">e Tabelas:</span><span class="sxs-lookup"><span data-stu-id="b1103-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="b1103-300">Parâmetros do AzCopy</span><span class="sxs-lookup"><span data-stu-id="b1103-300">AzCopy Parameters</span></span>
<span data-ttu-id="b1103-301">Veja abaixo uma descrição dos parâmetros do AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b1103-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="b1103-302">Também é possível digitar um dos comandos a seguir na linha de comando para obter ajuda no uso do AzCopy:</span><span class="sxs-lookup"><span data-stu-id="b1103-302">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="b1103-303">Para obter ajuda detalhada da linha de comando para o AzCopy: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="b1103-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="b1103-304">Para obter ajuda detalhada para qualquer parâmetro do AzCopy: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="b1103-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="b1103-305">Para obter exemplos da linha de comando: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="b1103-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="b1103-306">/Source:"origem"</span><span class="sxs-lookup"><span data-stu-id="b1103-306">/Source:"source"</span></span>
<span data-ttu-id="b1103-307">Especifica os dados de origem para cópia.</span><span class="sxs-lookup"><span data-stu-id="b1103-307">Specifies the source data from which to copy.</span></span> <span data-ttu-id="b1103-308">A origem pode ser um diretório do sistema de arquivos, um contêiner de blob, um diretório virtual de blob, um compartilhamento de arquivos de armazenamento, um diretório de arquivos de armazenamento ou uma tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1103-308">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="b1103-309">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="b1103-310">/Dest: "destino"</span><span class="sxs-lookup"><span data-stu-id="b1103-310">/Dest:"destination"</span></span>
<span data-ttu-id="b1103-311">Especifica o destino da cópia.</span><span class="sxs-lookup"><span data-stu-id="b1103-311">Specifies the destination to copy to.</span></span> <span data-ttu-id="b1103-312">O destino pode ser um diretório do sistema de arquivos, um contêiner de blob, um diretório virtual de blob, um compartilhamento de arquivos de armazenamento, um diretório de arquivos de armazenamento ou uma tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1103-312">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="b1103-313">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="b1103-314">/Pattern:"padrão de arquivo"</span><span class="sxs-lookup"><span data-stu-id="b1103-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="b1103-315">Especifica um padrão de arquivo que indica quais arquivos devem ser copiados.</span><span class="sxs-lookup"><span data-stu-id="b1103-315">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="b1103-316">O comportamento do parâmetro /Pattern é determinado pelo local dos dados de origem e pela presença da opção do modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="b1103-316">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="b1103-317">O modo recursivo é especificado pela opção /S.</span><span class="sxs-lookup"><span data-stu-id="b1103-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="b1103-318">Se a origem especificada for um diretório no sistema de arquivos, os curingas padrão estão em vigor, e o padrão de arquivo fornecido é comparado com os arquivos dentro do diretório.</span><span class="sxs-lookup"><span data-stu-id="b1103-318">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="b1103-319">Se a opção /S for especificada, o AzCopy também compara o padrão especificado com todos os arquivos em todas as subpastas do diretório.</span><span class="sxs-lookup"><span data-stu-id="b1103-319">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="b1103-320">Se a origem especificada for um contêiner de blob ou um diretório virtual, os curingas não são aplicados.</span><span class="sxs-lookup"><span data-stu-id="b1103-320">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="b1103-321">Se a opção /S for especificada, o AzCopy interpreta o padrão do arquivo especificado como um prefixo de blob.</span><span class="sxs-lookup"><span data-stu-id="b1103-321">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="b1103-322">Se a opção /S não for especificada, o AzCopy compara o padrão do arquivo com os nomes de blob exatos.</span><span class="sxs-lookup"><span data-stu-id="b1103-322">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="b1103-323">Se a origem especificada for um compartilhamento de arquivos do Azure, você deve especificar o nome exato do arquivo (por exemplo, abc.txt) para copiar um único arquivo ou especificar a opção /S para copiar todos os arquivos recursivamente no compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="b1103-323">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="b1103-324">A tentativa de especificar um padrão de arquivo e a opção /S simultaneamente resulta em um erro.</span><span class="sxs-lookup"><span data-stu-id="b1103-324">Attempting to specify both a file pattern and option /S together results in an error.</span></span>

<span data-ttu-id="b1103-325">O AzCopy diferencia maiúsculas de minúsculas quando /Source é um contêiner de blob ou diretório virtual de blob, e não diferencia maiúsculas de minúsculas em todos os outros casos.</span><span class="sxs-lookup"><span data-stu-id="b1103-325">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="b1103-326">O padrão de arquivo usado quando nenhum padrão de arquivo é especificado é *.*</span><span class="sxs-lookup"><span data-stu-id="b1103-326">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="b1103-327">para uma localização do sistema de arquivos, ou um prefixo vazio para uma localização de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1103-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="b1103-328">Não é possível especificar diversos padrões para os arquivos.</span><span class="sxs-lookup"><span data-stu-id="b1103-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="b1103-329">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="b1103-330">/DestKey:"chave de armazenamento"</span><span class="sxs-lookup"><span data-stu-id="b1103-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="b1103-331">Especifica a chave de conta de armazenamento do recurso de destino.</span><span class="sxs-lookup"><span data-stu-id="b1103-331">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="b1103-332">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="b1103-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="b1103-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="b1103-334">Especifica uma SAS (Assinatura de acesso compartilhado) com as permissões de LEITURA e GRAVAÇÃO para o destino (se for aplicável).</span><span class="sxs-lookup"><span data-stu-id="b1103-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="b1103-335">Coloque a SAS entre aspas duplas, porque ela pode conter caracteres de linha de comando especiais.</span><span class="sxs-lookup"><span data-stu-id="b1103-335">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="b1103-336">Se o recurso de destino for um contêiner de blob, compartilhamento de arquivo ou tabela, você poderá especificar essa opção seguida pelo token da SAS, ou a SAS como parte do URI do contêiner de blob, compartilhamento de arquivo ou tabela de destino, sem essa opção.</span><span class="sxs-lookup"><span data-stu-id="b1103-336">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="b1103-337">Se a origem e o destino forem blobs, ambos devem residir na mesma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b1103-337">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="b1103-338">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="b1103-339">/Sourcekey: "chave de armazenamento"</span><span class="sxs-lookup"><span data-stu-id="b1103-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="b1103-340">Especifica a chave de conta de armazenamento para o recurso de origem.</span><span class="sxs-lookup"><span data-stu-id="b1103-340">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="b1103-341">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="b1103-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="b1103-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="b1103-343">Especifica uma Assinatura de acesso compartilhado com as permissões de LEITURA e LISTAGEM para a origem (se for aplicável).</span><span class="sxs-lookup"><span data-stu-id="b1103-343">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="b1103-344">Coloque a SAS entre aspas duplas, porque ela pode conter caracteres de linha de comando especiais.</span><span class="sxs-lookup"><span data-stu-id="b1103-344">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="b1103-345">Se o recurso da fonte for um contêiner de blob, e nenhuma chave ou uma SAS for fornecida, o contêiner será lido por meio de acesso anônimo.</span><span class="sxs-lookup"><span data-stu-id="b1103-345">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container is read via anonymous access.</span></span>

<span data-ttu-id="b1103-346">Se a origem for um compartilhamento de arquivo ou uma tabela, será necessário fornecer uma chave ou SAS.</span><span class="sxs-lookup"><span data-stu-id="b1103-346">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="b1103-347">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="b1103-348">/S</span><span class="sxs-lookup"><span data-stu-id="b1103-348">/S</span></span>
<span data-ttu-id="b1103-349">Especifica o modo recursivo para operações de cópia.</span><span class="sxs-lookup"><span data-stu-id="b1103-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="b1103-350">No modo recursivo, o AzCopy copia todos os blobs ou arquivos correspondentes ao padrão do arquivo, inclusive os presentes nas subpastas.</span><span class="sxs-lookup"><span data-stu-id="b1103-350">In recursive mode, AzCopy copies all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="b1103-351">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="b1103-352">/BlobType:"bloco" | "página" | "anexo"</span><span class="sxs-lookup"><span data-stu-id="b1103-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="b1103-353">Especifica se o blob de destino é um blob de blocos, um blob de páginas ou um blob anexo.</span><span class="sxs-lookup"><span data-stu-id="b1103-353">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="b1103-354">Essa opção só será possível quando você estiver carregando um blob.</span><span class="sxs-lookup"><span data-stu-id="b1103-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="b1103-355">Caso contrário, um erro é gerado.</span><span class="sxs-lookup"><span data-stu-id="b1103-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="b1103-356">Se o destino é um blob e essa opção não está especificada, por padrão, o AzCopy cria um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="b1103-356">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="b1103-357">**Aplicável a:** Blobs</span><span class="sxs-lookup"><span data-stu-id="b1103-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="b1103-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="b1103-358">/CheckMD5</span></span>
<span data-ttu-id="b1103-359">Calcula um hash MD5 para dados baixados e certifica que o hash MD5 armazenado no blob, ou a propriedade Content-MD5 do arquivo, corresponde ao hash calculado.</span><span class="sxs-lookup"><span data-stu-id="b1103-359">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="b1103-360">Como, por padrão, a verificação MD5 permanece desativada, você deve especificar essa opção para realizar a verificação MD5 ao baixar os dados.</span><span class="sxs-lookup"><span data-stu-id="b1103-360">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="b1103-361">O Azure Storage não assegura que o hash MD5 armazenado para o blob ou o arquivo esteja atualizado.</span><span class="sxs-lookup"><span data-stu-id="b1103-361">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="b1103-362">É de responsabilidade do cliente atualizar o MD5 sempre que o blob ou o arquivo é modificado.</span><span class="sxs-lookup"><span data-stu-id="b1103-362">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="b1103-363">O AzCopy sempre define a propriedade Content-MD5 para um blob ou um arquivo do Azure depois de carregá-lo no serviço.</span><span class="sxs-lookup"><span data-stu-id="b1103-363">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="b1103-364">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="b1103-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="b1103-365">/Snapshot</span></span>
<span data-ttu-id="b1103-366">Indica se é necessário transferir ou não os instantâneos.</span><span class="sxs-lookup"><span data-stu-id="b1103-366">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="b1103-367">Essa opção só é válida quando a origem é um blob.</span><span class="sxs-lookup"><span data-stu-id="b1103-367">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="b1103-368">Os instantâneos de blob transferidos são renomeados neste formato: nome-do-blob (hora-do-instantâneo).extensão</span><span class="sxs-lookup"><span data-stu-id="b1103-368">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="b1103-369">Por padrão, os instantâneos não são copiados.</span><span class="sxs-lookup"><span data-stu-id="b1103-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="b1103-370">**Aplicável a:** Blobs</span><span class="sxs-lookup"><span data-stu-id="b1103-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="b1103-371">/V: [arquivo de log detalhado]</span><span class="sxs-lookup"><span data-stu-id="b1103-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="b1103-372">Produz mensagens de status detalhadas em um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="b1103-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="b1103-373">Por padrão, o arquivo de log detalhado é chamado de AzCopyVerbose.log no `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="b1103-373">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="b1103-374">Se você especificar um local de arquivo existente para essa opção, o log detalhado será acrescentado a esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="b1103-374">If you specify an existing file location for this option, the verbose log is appended to that file.</span></span>  

<span data-ttu-id="b1103-375">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="b1103-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="b1103-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="b1103-377">Especifica uma pasta de arquivo de diário para retomar uma operação.</span><span class="sxs-lookup"><span data-stu-id="b1103-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="b1103-378">O AzCopy sempre dará suporte à retomada caso uma operação tenha sido interrompida.</span><span class="sxs-lookup"><span data-stu-id="b1103-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="b1103-379">Se essa opção não for especificada ou for especificada sem um caminho de pasta, o AzCopy criará o arquivo de diário no local padrão, que é %LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b1103-379">If this option is not specified, or it is specified without a folder path, then AzCopy creates the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="b1103-380">Sempre que você emite um comando para o AzCopy, ele verifica se um arquivo de diário existe na pasta padrão ou se está em uma pasta especificada por meio dessa opção.</span><span class="sxs-lookup"><span data-stu-id="b1103-380">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="b1103-381">Se o arquivo de diário não estiver em nenhum dos lugares, o AzCopy tratará a operação como nova e gerar um novo arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="b1103-381">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="b1103-382">Se o arquivo de diário existir, o AzCopy verificará se a linha de comando inserida corresponde à linha de comando no arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="b1103-382">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="b1103-383">Se as duas linhas de comando forem correspondentes, o AzCopy retomará a operação incompleta.</span><span class="sxs-lookup"><span data-stu-id="b1103-383">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="b1103-384">Se elas não forem correspondentes, será solicitado que você substitua o arquivo de diário para iniciar uma nova operação ou que cancele a operação atual.</span><span class="sxs-lookup"><span data-stu-id="b1103-384">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="b1103-385">O arquivo de diário é excluído mediante a conclusão bem-sucedida da operação.</span><span class="sxs-lookup"><span data-stu-id="b1103-385">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="b1103-386">A retomada de uma operação de um arquivo de diário criado por uma versão anterior do AzCopy não é compatível.</span><span class="sxs-lookup"><span data-stu-id="b1103-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="b1103-387">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="b1103-388">/@: “arquivo de parâmetro”</span><span class="sxs-lookup"><span data-stu-id="b1103-388">/@:"parameter-file"</span></span>
<span data-ttu-id="b1103-389">Especifica um arquivo que contém parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b1103-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="b1103-390">O AzCopy processa os parâmetros no arquivo como se eles tivessem sido especificados na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="b1103-390">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="b1103-391">Em um arquivo de resposta, é possível especificar vários parâmetros em um único arquivo ou especificar cada parâmetro na própria linha.</span><span class="sxs-lookup"><span data-stu-id="b1103-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="b1103-392">Um parâmetro individual não pode abranger várias linhas.</span><span class="sxs-lookup"><span data-stu-id="b1103-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="b1103-393">Os arquivos de resposta podem incluir linhas de comentários iniciadas pelo símbolo #.</span><span class="sxs-lookup"><span data-stu-id="b1103-393">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="b1103-394">É possível especificar vários arquivos de resposta.</span><span class="sxs-lookup"><span data-stu-id="b1103-394">You can specify multiple response files.</span></span> <span data-ttu-id="b1103-395">No entanto, o AzCopy não permite arquivos de resposta aninhados.</span><span class="sxs-lookup"><span data-stu-id="b1103-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="b1103-396">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="b1103-397">/Y</span><span class="sxs-lookup"><span data-stu-id="b1103-397">/Y</span></span>
<span data-ttu-id="b1103-398">Suprime todas as solicitações de confirmação do AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b1103-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="b1103-399">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="b1103-400">/L</span><span class="sxs-lookup"><span data-stu-id="b1103-400">/L</span></span>
<span data-ttu-id="b1103-401">Especifica uma operação de listagem apenas. Nenhum dado é copiado.</span><span class="sxs-lookup"><span data-stu-id="b1103-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="b1103-402">O AzCopy interpreta o uso dessa opção como uma simulação para execução da linha de comando sem essa opção /L, e conta quantos objetos são copiados. Você pode especificar a opção /V ao mesmo tempo para verificar quais objetos são copiados no log detalhado.</span><span class="sxs-lookup"><span data-stu-id="b1103-402">AzCopy interprets the using of this option as a simulation for running the command line without this option /L and counts how many objects are copied, you can specify option /V at the same time to check which objects are copied in the verbose log.</span></span>

<span data-ttu-id="b1103-403">O comportamento dessa opção também é determinado pelo local dos dados de origem e pela presença da opção no modo recursivo /S e pela opção de padrão de arquivo /Pattern.</span><span class="sxs-lookup"><span data-stu-id="b1103-403">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="b1103-404">O AzCopy exige a permissão de LISTAGEM e de LEITURA deste local de origem ao usar essa opção.</span><span class="sxs-lookup"><span data-stu-id="b1103-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="b1103-405">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="b1103-406">/MT</span><span class="sxs-lookup"><span data-stu-id="b1103-406">/MT</span></span>
<span data-ttu-id="b1103-407">Define a hora da última modificação do arquivo baixado como a mesma do blob de origem ou do arquivo.</span><span class="sxs-lookup"><span data-stu-id="b1103-407">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="b1103-408">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="b1103-409">/XN</span><span class="sxs-lookup"><span data-stu-id="b1103-409">/XN</span></span>
<span data-ttu-id="b1103-410">Exclui um recurso de origem mais novo.</span><span class="sxs-lookup"><span data-stu-id="b1103-410">Excludes a newer source resource.</span></span> <span data-ttu-id="b1103-411">O recurso não é copiado se a hora da última modificação na origem for igual ou mais recente do que o destino.</span><span class="sxs-lookup"><span data-stu-id="b1103-411">The resource is not copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="b1103-412">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="b1103-413">/XO</span><span class="sxs-lookup"><span data-stu-id="b1103-413">/XO</span></span>
<span data-ttu-id="b1103-414">Exclui um recurso de origem mais antigo.</span><span class="sxs-lookup"><span data-stu-id="b1103-414">Excludes an older source resource.</span></span> <span data-ttu-id="b1103-415">O recurso não é copiado se a hora da última modificação na origem for igual ou mais recente do que o destino.</span><span class="sxs-lookup"><span data-stu-id="b1103-415">The resource is not copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="b1103-416">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="b1103-417">/A</span><span class="sxs-lookup"><span data-stu-id="b1103-417">/A</span></span>
<span data-ttu-id="b1103-418">Carrega apenas arquivos que tenham o atributo Archive definido.</span><span class="sxs-lookup"><span data-stu-id="b1103-418">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="b1103-419">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="b1103-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="b1103-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="b1103-421">Carrega apenas arquivos que tenham algum dos atributos especificados definido.</span><span class="sxs-lookup"><span data-stu-id="b1103-421">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="b1103-422">Entre os atributos disponíveis estão:</span><span class="sxs-lookup"><span data-stu-id="b1103-422">Available attributes include:</span></span>

* <span data-ttu-id="b1103-423">R = Arquivos somente leitura</span><span class="sxs-lookup"><span data-stu-id="b1103-423">R = Read-only files</span></span>
* <span data-ttu-id="b1103-424">A = Arquivos prontos para arquivamento</span><span class="sxs-lookup"><span data-stu-id="b1103-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="b1103-425">S = Arquivos de sistema</span><span class="sxs-lookup"><span data-stu-id="b1103-425">S = System files</span></span>
* <span data-ttu-id="b1103-426">H = Arquivos ocultos</span><span class="sxs-lookup"><span data-stu-id="b1103-426">H = Hidden files</span></span>
* <span data-ttu-id="b1103-427">C = Arquivo compactado</span><span class="sxs-lookup"><span data-stu-id="b1103-427">C = Compressed files</span></span>
* <span data-ttu-id="b1103-428">N = Arquivos normais</span><span class="sxs-lookup"><span data-stu-id="b1103-428">N = Normal files</span></span>
* <span data-ttu-id="b1103-429">E = Arquivos criptografados</span><span class="sxs-lookup"><span data-stu-id="b1103-429">E = Encrypted files</span></span>
* <span data-ttu-id="b1103-430">T = Arquivos temporários</span><span class="sxs-lookup"><span data-stu-id="b1103-430">T = Temporary files</span></span>
* <span data-ttu-id="b1103-431">O = Arquivos offline</span><span class="sxs-lookup"><span data-stu-id="b1103-431">O = Offline files</span></span>
* <span data-ttu-id="b1103-432">I = Arquivos não indexados</span><span class="sxs-lookup"><span data-stu-id="b1103-432">I = Non-indexed files</span></span>

<span data-ttu-id="b1103-433">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="b1103-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="b1103-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="b1103-435">Exclui arquivos que tenham qualquer dos atributos especificados definido.</span><span class="sxs-lookup"><span data-stu-id="b1103-435">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="b1103-436">Entre os atributos disponíveis estão:</span><span class="sxs-lookup"><span data-stu-id="b1103-436">Available attributes include:</span></span>

* <span data-ttu-id="b1103-437">R = Arquivos somente leitura</span><span class="sxs-lookup"><span data-stu-id="b1103-437">R = Read-only files</span></span>
* <span data-ttu-id="b1103-438">A = Arquivos prontos para arquivamento</span><span class="sxs-lookup"><span data-stu-id="b1103-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="b1103-439">S = Arquivos de sistema</span><span class="sxs-lookup"><span data-stu-id="b1103-439">S = System files</span></span>
* <span data-ttu-id="b1103-440">H = Arquivos ocultos</span><span class="sxs-lookup"><span data-stu-id="b1103-440">H = Hidden files</span></span>
* <span data-ttu-id="b1103-441">C = Arquivo compactado</span><span class="sxs-lookup"><span data-stu-id="b1103-441">C = Compressed files</span></span>
* <span data-ttu-id="b1103-442">N = Arquivos normais</span><span class="sxs-lookup"><span data-stu-id="b1103-442">N = Normal files</span></span>
* <span data-ttu-id="b1103-443">E = Arquivos criptografados</span><span class="sxs-lookup"><span data-stu-id="b1103-443">E = Encrypted files</span></span>
* <span data-ttu-id="b1103-444">T = Arquivos temporários</span><span class="sxs-lookup"><span data-stu-id="b1103-444">T = Temporary files</span></span>
* <span data-ttu-id="b1103-445">O = Arquivos offline</span><span class="sxs-lookup"><span data-stu-id="b1103-445">O = Offline files</span></span>
* <span data-ttu-id="b1103-446">I = Arquivos não indexados</span><span class="sxs-lookup"><span data-stu-id="b1103-446">I = Non-indexed files</span></span>

<span data-ttu-id="b1103-447">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="b1103-448">/Delimiter: "delimitador"</span><span class="sxs-lookup"><span data-stu-id="b1103-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="b1103-449">Indica o caractere delimitador usado para delimitar diretórios virtuais em um nome de blob.</span><span class="sxs-lookup"><span data-stu-id="b1103-449">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="b1103-450">Por padrão, o AzCopy usa / como o caractere delimitador.</span><span class="sxs-lookup"><span data-stu-id="b1103-450">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="b1103-451">No entanto, o AzCopy dá suporte ao uso de qualquer caractere comum (como @, # ou %) como delimitador.</span><span class="sxs-lookup"><span data-stu-id="b1103-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="b1103-452">Se precisar incluir um desses caracteres especiais na linha de comando, coloque o nome do arquivo entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="b1103-452">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="b1103-453">Essa opção só é aplicável para o download de blobs.</span><span class="sxs-lookup"><span data-stu-id="b1103-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="b1103-454">**Aplicável a:** Blobs</span><span class="sxs-lookup"><span data-stu-id="b1103-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="b1103-455">/NC: "número-de-operações-simultâneas"</span><span class="sxs-lookup"><span data-stu-id="b1103-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="b1103-456">Especifica o número de operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="b1103-456">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="b1103-457">Por padrão, o AzCopy inicia uma determinada quantidade de operações simultâneas para aumentar a taxa de transferência dos dados.</span><span class="sxs-lookup"><span data-stu-id="b1103-457">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="b1103-458">O grande número de operações simultâneas em um ambiente com baixa largura de banda pode sobrecarregar a conexão de rede, evitando que as operações sejam concluídas.</span><span class="sxs-lookup"><span data-stu-id="b1103-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="b1103-459">Limite operações simultâneas com base na largura de banda real de rede disponível.</span><span class="sxs-lookup"><span data-stu-id="b1103-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="b1103-460">O limite máximo de operações simultâneas é 512.</span><span class="sxs-lookup"><span data-stu-id="b1103-460">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="b1103-461">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="b1103-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="b1103-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="b1103-463">Especifica se o recurso `source` é um blob disponível no ambiente de desenvolvimento local, em execução no emulador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b1103-463">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="b1103-464">**Aplicável a:** Blobs, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="b1103-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="b1103-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="b1103-466">Especifica se o recurso `destination` é um blob disponível no ambiente de desenvolvimento local, em execução no emulador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b1103-466">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="b1103-467">**Aplicável a:** Blobs, Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="b1103-468">/PKRS: "chave1#chave2#chave3#..."</span><span class="sxs-lookup"><span data-stu-id="b1103-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="b1103-469">Divide o intervalo de chaves de partição para possibilitar a exportação paralela dos dados, o que aumenta a velocidade dessa operação.</span><span class="sxs-lookup"><span data-stu-id="b1103-469">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="b1103-470">Se essa opção não for especificada, o AzCopy usa um único thread para exportar entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-470">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="b1103-471">Por exemplo, se o usuário especifica /PKRS:"aa#bb", o AzCopy inicia três operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="b1103-471">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="b1103-472">Cada operação exporta um dos três intervalos de chaves de partição, como mostramos abaixo:</span><span class="sxs-lookup"><span data-stu-id="b1103-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="b1103-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="b1103-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="b1103-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="b1103-474">[aa, bb)</span></span>

  <span data-ttu-id="b1103-475">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="b1103-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="b1103-476">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="b1103-477">/Splitsize: "tamanho do arquivo"</span><span class="sxs-lookup"><span data-stu-id="b1103-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="b1103-478">Especifica o tamanho da divisão do arquivo exportado em MB, o valor mínimo permitido é de 32.</span><span class="sxs-lookup"><span data-stu-id="b1103-478">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="b1103-479">Se essa opção não for especificada, o AzCopy exportará os dados da tabela para um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="b1103-479">If this option is not specified, AzCopy exports table data to a single file.</span></span>

<span data-ttu-id="b1103-480">Se os dados da tabela forem exportados para um blob e o tamanho do arquivo exportado alcançar o limite de 200 GB, o AzCopy divide o arquivo exportado, mesmo que essa opção não seja especificada.</span><span class="sxs-lookup"><span data-stu-id="b1103-480">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy splits the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="b1103-481">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="b1103-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="b1103-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="b1103-483">Especifica o comportamento da importação dos dados da tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-483">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="b1103-484">InsertOrSkip — Ignora uma entidade existente ou insere uma nova entidade, caso ela não exista na tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="b1103-485">InsertOrMerge — Mescla uma entidade existente ou insere uma nova entidade, caso ela não exista na tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="b1103-486">InsertOrReplace — Substitui uma entidade existente ou insere uma nova entidade, caso ela não exista na tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="b1103-487">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="b1103-488">/Manifesto: "arquivo de manifesto"</span><span class="sxs-lookup"><span data-stu-id="b1103-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="b1103-489">Especifica o arquivo de manifesto para a operação de exportação e importação de tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-489">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="b1103-490">Essa opção é opcional durante a operação de exportação. O AzCopy gera um arquivo de manifesto com nome predefinido se essa opção não for especificada.</span><span class="sxs-lookup"><span data-stu-id="b1103-490">This option is optional during the export operation, AzCopy generates a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="b1103-491">Essa opção é exigida durante a operação de importação para localização dos arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="b1103-491">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="b1103-492">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="b1103-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="b1103-493">/SyncCopy</span></span>
<span data-ttu-id="b1103-494">Indica se devem ser copiados de forma síncrona blobs ou arquivos entre dois pontos de extremidade de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1103-494">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="b1103-495">O AzCopy por padrão usa cópia assíncrona no servidor.</span><span class="sxs-lookup"><span data-stu-id="b1103-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="b1103-496">Especifique essa opção para executar uma cópia síncrona, que baixa blobs ou arquivos para a memória local e, em seguida, carrega-as para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1103-496">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="b1103-497">Você pode usar essa opção ao copiar arquivos no armazenamento de Blob no armazenamento de arquivo ou do armazenamento de Blob para armazenamento de arquivos ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="b1103-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="b1103-498">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="b1103-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="b1103-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="b1103-500">Especifica o tipo de conteúdo MIME para blobs ou arquivos de destino.</span><span class="sxs-lookup"><span data-stu-id="b1103-500">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="b1103-501">O AzCopy define o tipo de conteúdo para um blob ou arquivo application/octet-stream por padrão.</span><span class="sxs-lookup"><span data-stu-id="b1103-501">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="b1103-502">Você pode definir o tipo de conteúdo para todos os blobs ou arquivos explicitamente especificando um valor para essa opção.</span><span class="sxs-lookup"><span data-stu-id="b1103-502">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="b1103-503">Se você especificar essa opção sem um valor, AzCopy definirá cada blob ou tipo de conteúdo do arquivo de acordo com a sua extensão de arquivo.</span><span class="sxs-lookup"><span data-stu-id="b1103-503">If you specify this option without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="b1103-504">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="b1103-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="b1103-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="b1103-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="b1103-506">Especifica o formato do arquivo de dados exportados da tabela.</span><span class="sxs-lookup"><span data-stu-id="b1103-506">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="b1103-507">Se essa opção não for especificada, por padrão, o AzCopy exportará o arquivo de dados da tabela no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="b1103-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="b1103-508">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="b1103-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="b1103-509">Problemas Conhecidos e Práticas Recomendadas</span><span class="sxs-lookup"><span data-stu-id="b1103-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="b1103-510">Limite gravações simultâneas durante a cópia de dados</span><span class="sxs-lookup"><span data-stu-id="b1103-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="b1103-511">Ao copiar blobs ou arquivos usando o AZCopy, lembre-se de que outro aplicativo pode estar modificando os dados enquanto você os copia.</span><span class="sxs-lookup"><span data-stu-id="b1103-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="b1103-512">Se possível, verifique se os dados que está copiando não estão sendo modificados durante a cópia.</span><span class="sxs-lookup"><span data-stu-id="b1103-512">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="b1103-513">Por exemplo, ao copiar um VHD associado a uma máquina virtual do Azure, verifique se nenhum outro aplicativo está gravando no VHD, no momento.</span><span class="sxs-lookup"><span data-stu-id="b1103-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="b1103-514">Uma boa maneira de fazer isso é ceder o recurso para ser copiado.</span><span class="sxs-lookup"><span data-stu-id="b1103-514">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="b1103-515">Também é possível criar um instantâneo do VHD primeiro e, em seguida, copiar o instantâneo.</span><span class="sxs-lookup"><span data-stu-id="b1103-515">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="b1103-516">Se não for possível evitar que outros aplicativos gravem em blobs ou arquivos enquanto são copiados, lembre-se que, quando o trabalho terminar, os recursos copiados não poderão mais ter paridade total com os recursos de origem.</span><span class="sxs-lookup"><span data-stu-id="b1103-516">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="b1103-517">Execute uma instância de AzCopy em um computador.</span><span class="sxs-lookup"><span data-stu-id="b1103-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="b1103-518">O AzCopy foi projetado para maximizar a utilização de seu recurso de máquina para acelerar a transferência de dados, é recomendável executar apenas uma instância de AzCopy em um único computador e especifique a opção `/NC` se precisar de mais operações em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="b1103-518">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="b1103-519">Para obter mais detalhes, digite `AzCopy /?:NC` na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="b1103-519">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="b1103-520">Habilite algoritmos MD5 compatíveis com FIPS para o AzCopy quando você "Usar algoritmos compatíveis com FIPS para criptografia, hash e assinatura".</span><span class="sxs-lookup"><span data-stu-id="b1103-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="b1103-521">Por padrão, o AzCopy usa a implementação MD5 do .NET para calcular o MD5 ao copiar objetos, mas há alguns requisitos de segurança que precisam do AzCopy para permitir a configuração de MD5 compatível com FIPS.</span><span class="sxs-lookup"><span data-stu-id="b1103-521">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="b1103-522">Você pode criar um arquivo app.config `AzCopy.exe.config` com a propriedade `AzureStorageUseV1MD5` e reservá-lo com o AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="b1103-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="b1103-523">Para a propriedade "AzureStorageUseV1MD5" • True – valor padrão, o AzCopy usa a implementação MD5 do .NET.</span><span class="sxs-lookup"><span data-stu-id="b1103-523">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy uses .NET MD5 implementation.</span></span>
<span data-ttu-id="b1103-524">• False – o AzCopy usa o algoritmo MD5 compatível com FIPS.</span><span class="sxs-lookup"><span data-stu-id="b1103-524">• False – AzCopy uses FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="b1103-525">Observe que os algoritmos compatíveis com FIPS estão desabilitados por padrão em seu computador com Windows. Digite secpol.msc na janela Executar e marque essa opção em Configuração de Segurança -> Segurança -> Políticas Locais > Opções de Segurança > Criptografia do Sistema: usar algoritmos compatíveis com FIPS para criptografia, hash e assinatura.</span><span class="sxs-lookup"><span data-stu-id="b1103-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1103-526">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b1103-526">Next steps</span></span>
<span data-ttu-id="b1103-527">Para obter mais informações sobre o Armazenamento do Azure e o AzCopy, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="b1103-527">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="b1103-528">Documentação do Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="b1103-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="b1103-529">Introdução ao Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b1103-529">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="b1103-530">Como usar o Armazenamento de blob do .NET</span><span class="sxs-lookup"><span data-stu-id="b1103-530">How to use Blob storage from .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="b1103-531">Como usar o Armazenamento de Arquivos no .NET</span><span class="sxs-lookup"><span data-stu-id="b1103-531">How to use File storage from .NET</span></span>](../storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="b1103-532">Como usar o Armazenamento de Tabela do .NET</span><span class="sxs-lookup"><span data-stu-id="b1103-532">How to use Table storage from .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="b1103-533">Como criar, gerenciar ou excluir uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b1103-533">How to create, manage, or delete a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="b1103-534">Transferir dados com o AzCopy no Linux</span><span class="sxs-lookup"><span data-stu-id="b1103-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="b1103-535">Postagens de blog de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="b1103-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="b1103-536">Apresentando a versão de visualização da biblioteca de movimentação de dados do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b1103-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="b1103-537">AzCopy: Introducing synchronous copy and customized content type (AzCopy: introdução a cópia síncrona e tipo de conteúdo personalizado)</span><span class="sxs-lookup"><span data-stu-id="b1103-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="b1103-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support (AzCopy: anúncio de disponibilidade geral do AzCopy 3.0 mais versão de teste do AzCopy 4.0 com suporte para Tabela e Arquivo)</span><span class="sxs-lookup"><span data-stu-id="b1103-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="b1103-539">AzCopy: Optimized for Large-Scale Copy Scenarios (AzCopy: otimizado para cenários de cópia em larga escala)</span><span class="sxs-lookup"><span data-stu-id="b1103-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="b1103-540">AzCopy: Support for read-access geo-redundant storage (AzCopy: suporte para o armazenamento com redundância geográfica com acesso de leitura)</span><span class="sxs-lookup"><span data-stu-id="b1103-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="b1103-541">AzCopy: Transfer data with re-startable mode and SAS token (AzCopy: transferir dados com o modo reiniciável e token de SAS)</span><span class="sxs-lookup"><span data-stu-id="b1103-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="b1103-542">AzCopy: Using cross-account Copy Blob (AzCopy: usando blob de cópia em várias contas)</span><span class="sxs-lookup"><span data-stu-id="b1103-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="b1103-543">AzCopy: Uploading/downloading files for Azure Blobs (AzCopy: Upload/download de arquivos para Blobs do Azure)</span><span class="sxs-lookup"><span data-stu-id="b1103-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

