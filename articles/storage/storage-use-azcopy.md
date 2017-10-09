---
title: aaaCopy ou mover dados tooAzure armazenamento com AzCopy no Windows | Microsoft Docs
description: "Use Olá AzCopy Windows utilitário toomove ou copiar dados tooor do blob, tabela e o conteúdo do arquivo. Copiar dados tooAzure armazenamento de arquivos locais, ou copie dados dentro ou entre contas de armazenamento. Migre facilmente o armazenamento de tooAzure de dados."
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
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="bb692-105">Transferência de dados com hello AzCopy no Windows</span><span class="sxs-lookup"><span data-stu-id="bb692-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="bb692-106">AzCopy é um utilitário de linha de comando projetado para copiar dados tooand do armazenamento de BLOBs do Microsoft Azure, o arquivo e a tabela usando comandos simples com um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="bb692-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="bb692-107">Você pode copiar dados de um tooanother de objeto dentro de sua conta de armazenamento, ou entre contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bb692-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="bb692-108">Há duas versões do AzCopy que podem ser baixadas.</span><span class="sxs-lookup"><span data-stu-id="bb692-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="bb692-109">O AzCopy no Windows se baseia no .NET Framework e oferece opções de linha de comando no estilo Windows.</span><span class="sxs-lookup"><span data-stu-id="bb692-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="bb692-110">O [AzCopy no Linux](storage-use-azcopy-linux.md) se baseia no .NET Core Framework, que se destina a plataformas Linux que oferecem opções de linha de comando no estilo POSIX.</span><span class="sxs-lookup"><span data-stu-id="bb692-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="bb692-111">Este artigo aborda o AzCopy no Windows.</span><span class="sxs-lookup"><span data-stu-id="bb692-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="bb692-112">Baixar e instalar o AzCopy</span><span class="sxs-lookup"><span data-stu-id="bb692-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="bb692-113">AzCopy no Windows</span><span class="sxs-lookup"><span data-stu-id="bb692-113">AzCopy on Windows</span></span>
<span data-ttu-id="bb692-114">Baixar Olá [versão mais recente do AzCopy no Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="bb692-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="bb692-115">Instalação no Windows</span><span class="sxs-lookup"><span data-stu-id="bb692-115">Installation on Windows</span></span>
<span data-ttu-id="bb692-116">Depois de instalar o AzCopy no Windows usando o instalador hello, abra uma janela de comando e navegue toohello AzCopy diretório de instalação no seu computador - onde hello `AzCopy.exe` executável está localizado.</span><span class="sxs-lookup"><span data-stu-id="bb692-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="bb692-117">Se desejar, você pode adicionar o caminho de sistema de tooyour Olá AzCopy instalação local.</span><span class="sxs-lookup"><span data-stu-id="bb692-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="bb692-118">Por padrão, AzCopy é instalado muito`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` ou `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="bb692-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="bb692-119">Como escrever seu primeiro comando do AzCopy</span><span class="sxs-lookup"><span data-stu-id="bb692-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="bb692-120">Olá a sintaxe básica para comandos do AzCopy é:</span><span class="sxs-lookup"><span data-stu-id="bb692-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="bb692-121">Olá exemplos a seguir demonstram uma variedade de cenários para copiar dados tooand de Blobs do Microsoft Azure, arquivos e tabelas.</span><span class="sxs-lookup"><span data-stu-id="bb692-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="bb692-122">Consulte toohello [AzCopy parâmetros](#azcopy-parameters) seção para obter uma explicação detalhada de parâmetros de saudação usados em cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="bb692-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="bb692-123">Blob: baixar</span><span class="sxs-lookup"><span data-stu-id="bb692-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="bb692-124">Baixar um único blob</span><span class="sxs-lookup"><span data-stu-id="bb692-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="bb692-125">Observe que, se pasta Olá `C:\myfolder` não existir, AzCopy irá criá-lo e baixar `abc.txt ` na nova pasta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="bb692-126">Baixe um único blob de região secundária</span><span class="sxs-lookup"><span data-stu-id="bb692-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="bb692-127">Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.</span><span class="sxs-lookup"><span data-stu-id="bb692-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="bb692-128">Baixar todos os blobs</span><span class="sxs-lookup"><span data-stu-id="bb692-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="bb692-129">Suponha seguinte Olá blobs residem no contêiner especificado hello:</span><span class="sxs-lookup"><span data-stu-id="bb692-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="bb692-130">Após a operação de download de Olá Olá diretório `C:\myfolder` incluirá Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="bb692-130">After hello download operation, hello directory `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="bb692-131">Se você não especificar a opção `/S`, nenhum blob será baixado.</span><span class="sxs-lookup"><span data-stu-id="bb692-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="bb692-132">Baixar blobs com prefixo especificado</span><span class="sxs-lookup"><span data-stu-id="bb692-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="bb692-133">Suponha seguinte Olá blobs residem no contêiner especificado hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="bb692-134">Todos os blobs que começam com o prefixo Olá `a` serão baixados:</span><span class="sxs-lookup"><span data-stu-id="bb692-134">All blobs beginning with hello prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="bb692-135">Após a operação de download de Olá Olá pasta `C:\myfolder` incluirá Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="bb692-135">After hello download operation, hello folder `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="bb692-136">prefixo de saudação aplica diretório virtual toohello, que constitui Olá primeira parte do nome do blob hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="bb692-137">Exemplo hello mostrado acima, diretório virtual Olá não coincide com prefixo especificado de hello, portanto ele não será baixado.</span><span class="sxs-lookup"><span data-stu-id="bb692-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="bb692-138">Além disso, se hello opção `\S` não for especificado, AzCopy não baixará todos os blobs.</span><span class="sxs-lookup"><span data-stu-id="bb692-138">In addition, if hello option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="bb692-139">Definir a hora da última modificação Olá dos arquivos exportados toobe mesmo Olá blobs de origem</span><span class="sxs-lookup"><span data-stu-id="bb692-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="bb692-140">Você também pode excluir blobs de operação de download de saudação com base em sua hora da última modificação.</span><span class="sxs-lookup"><span data-stu-id="bb692-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="bb692-141">Por exemplo, se você quiser blobs tooexclude cuja hora da última modificação é hello igual ou mais recente do que o arquivo de destino hello, adicionar Olá `/XN` opção:</span><span class="sxs-lookup"><span data-stu-id="bb692-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="bb692-142">Ou se você quiser blobs tooexclude cuja hora da última modificação é hello mesmo ou mais antigo que o arquivo de destino hello, adicione Olá `/XO` opção:</span><span class="sxs-lookup"><span data-stu-id="bb692-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="bb692-143">Blob: carregar</span><span class="sxs-lookup"><span data-stu-id="bb692-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="bb692-144">Carregar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="bb692-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="bb692-145">Se Olá contêiner de destino especificado não existe, AzCopy será criá-lo e carregar o arquivo hello nele.</span><span class="sxs-lookup"><span data-stu-id="bb692-145">If hello specified destination container does not exist, AzCopy will create it and upload hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="bb692-146">Carregar arquivo único diretório toovirtual</span><span class="sxs-lookup"><span data-stu-id="bb692-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="bb692-147">Se Olá especificado não existe um diretório virtual, AzCopy carregará Olá arquivo tooinclude Olá diretório virtual em seu nome (*, por exemplo,*, `vd/abc.txt` no exemplo hello acima).</span><span class="sxs-lookup"><span data-stu-id="bb692-147">If hello specified virtual directory does not exist, AzCopy will upload hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="bb692-148">Carregar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="bb692-149">Especificando a opção `/S` carregamentos conteúdo Olá Olá especificado diretório tooBlob armazenamento recursivamente, que significa que todas as subpastas e seus arquivos serão carregados também.</span><span class="sxs-lookup"><span data-stu-id="bb692-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="bb692-150">Por exemplo, suponha que a seguir Olá arquivos residem na pasta `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="bb692-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="bb692-151">Após a operação de carregamento de saudação contêiner Olá incluirá Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="bb692-151">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="bb692-152">Se você não especificar a opção `/S`, o AzCopy não carregará de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="bb692-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="bb692-153">Após a operação de carregamento de saudação contêiner Olá incluirá Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="bb692-153">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="bb692-154">Carregar arquivos que correspondam ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="bb692-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="bb692-155">Suponha seguinte Olá arquivos residem na pasta `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="bb692-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="bb692-156">Após a operação de carregamento de saudação contêiner Olá incluirá Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="bb692-156">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="bb692-157">Se você não especificar a opção `/S`, o AzCopy carregará somente os blobs que não residem em um diretório virtual:</span><span class="sxs-lookup"><span data-stu-id="bb692-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="bb692-158">Especifique o tipo de conteúdo MIME Olá de um blob de destino</span><span class="sxs-lookup"><span data-stu-id="bb692-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="bb692-159">Por padrão, AzCopy define Olá de tipo de conteúdo de um blob de destino muito`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="bb692-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="bb692-160">A partir da versão 3.1.0, você pode especificar explicitamente o tipo de conteúdo Olá por meio da opção Olá `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="bb692-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="bb692-161">Essa sintaxe define o tipo de conteúdo Olá para todos os blobs em uma operação de carregamento.</span><span class="sxs-lookup"><span data-stu-id="bb692-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="bb692-162">Se você especificar `/SetContentType` sem um valor, em seguida, AzCopy definirá cada blob ou tipo de conteúdo do arquivo de acordo com tooits extensão de arquivo.</span><span class="sxs-lookup"><span data-stu-id="bb692-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="bb692-163">Blob: copiar</span><span class="sxs-lookup"><span data-stu-id="bb692-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="bb692-164">Copiar um único blob dentro da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="bb692-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="bb692-165">Quando você copia um blob em uma conta de armazenamento, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é realizada.</span><span class="sxs-lookup"><span data-stu-id="bb692-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="bb692-166">Copiar um único blob entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="bb692-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="bb692-167">Quando você copia um blob entre contas de armazenamento, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é realizada.</span><span class="sxs-lookup"><span data-stu-id="bb692-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="bb692-168">Copiar um único blob da região de tooprimary região secundária</span><span class="sxs-lookup"><span data-stu-id="bb692-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="bb692-169">Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.</span><span class="sxs-lookup"><span data-stu-id="bb692-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="bb692-170">Copiar um único blob e seus instantâneos entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="bb692-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="bb692-171">Após a operação de cópia hello, o contêiner de destino Olá incluirá Olá blob e seus instantâneos.</span><span class="sxs-lookup"><span data-stu-id="bb692-171">After hello copy operation, hello target container will include hello blob and its snapshots.</span></span> <span data-ttu-id="bb692-172">Supondo que o blob de saudação no exemplo hello acima tem dois instantâneos, contêiner Olá incluirá a seguir Olá blob e instantâneos:</span><span class="sxs-lookup"><span data-stu-id="bb692-172">Assuming hello blob in hello example above has two snapshots, hello container will include hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="bb692-173">Copiar blobs em regiões entre contas de armazenamento de forma síncrona.</span><span class="sxs-lookup"><span data-stu-id="bb692-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="bb692-174">O AzCopy por padrão copia dados entre dois pontos de extremidade de armazenamento assincronamente.</span><span class="sxs-lookup"><span data-stu-id="bb692-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="bb692-175">Então, a operação de cópia de saudação será executado no plano de fundo de saudação utilizando a capacidade de largura de banda sobressalente com nenhum SLA em termos de rapidez com que um blob será copiado e AzCopy verificará periodicamente o status da cópia Olá até Olá cópia é concluída ou falha.</span><span class="sxs-lookup"><span data-stu-id="bb692-175">Therefore, hello copy operation will run in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="bb692-176">Olá `/SyncCopy` opção garante que a operação de cópia Olá obterá velocidade consistente.</span><span class="sxs-lookup"><span data-stu-id="bb692-176">hello `/SyncCopy` option ensures that hello copy operation will get consistent speed.</span></span> <span data-ttu-id="bb692-177">AzCopy executa cópia síncrona Olá ao baixar blobs Olá toocopy de saudação especificado fonte toolocal da memória e, em seguida, carregá-las toohello destino de armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="bb692-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="bb692-178">`/SyncCopy`pode gerar saída adicional de custo cópia tooasynchronous comparados, hello a abordagem recomendada é toouse essa opção em uma VM do Azure que está em Olá mesma região que o custo de egresso fonte armazenamento conta tooavoid.</span><span class="sxs-lookup"><span data-stu-id="bb692-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="bb692-179">Arquivo: baixar</span><span class="sxs-lookup"><span data-stu-id="bb692-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="bb692-180">Baixar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="bb692-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="bb692-181">Se Olá especificado fonte for um compartilhamento de arquivos do Azure, você deve especificar nome de arquivo exatos Olá, (*, por exemplo,* `abc.txt`) toodownload um único arquivo, ou especifique a opção `/S` toodownload todos os arquivos no compartilhamento de saudação recursivamente.</span><span class="sxs-lookup"><span data-stu-id="bb692-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="bb692-182">Tentativa de toospecify um padrão de arquivo e a opção `/S` juntos resultará em erro.</span><span class="sxs-lookup"><span data-stu-id="bb692-182">Attempting toospecify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="bb692-183">Baixar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="bb692-184">Observe que nenhuma pasta vazia será baixada.</span><span class="sxs-lookup"><span data-stu-id="bb692-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="bb692-185">Arquivo: carregar</span><span class="sxs-lookup"><span data-stu-id="bb692-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="bb692-186">Carregar um único arquivo</span><span class="sxs-lookup"><span data-stu-id="bb692-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="bb692-187">Carregar todos os arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="bb692-188">Observe que nenhuma pasta vazia será carregada.</span><span class="sxs-lookup"><span data-stu-id="bb692-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="bb692-189">Carregar arquivos que correspondam ao padrão especificado</span><span class="sxs-lookup"><span data-stu-id="bb692-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="bb692-190">Arquivo: copiar</span><span class="sxs-lookup"><span data-stu-id="bb692-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="bb692-191">Copiar entre compartilhamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="bb692-192">Quando você copia um arquivo entre compartilhamentos de arquivos, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb692-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="bb692-193">Copiar de tooblob de compartilhamento de arquivo</span><span class="sxs-lookup"><span data-stu-id="bb692-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="bb692-194">Quando você copia um arquivo de tooblob de compartilhamento de arquivo, uma [cópia do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operação é executada.</span><span class="sxs-lookup"><span data-stu-id="bb692-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="bb692-195">Copiar de blob toofile compartilhamento</span><span class="sxs-lookup"><span data-stu-id="bb692-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="bb692-196">Quando você copia um arquivo de compartilhamento de toofile de blob, um [cópia do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operação é executada.</span><span class="sxs-lookup"><span data-stu-id="bb692-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="bb692-197">Copiar arquivos de forma síncrona</span><span class="sxs-lookup"><span data-stu-id="bb692-197">Synchronously copy files</span></span>
<span data-ttu-id="bb692-198">Você pode especificar Olá `/SyncCopy` opção toocopy dados de armazenamento de arquivo tooFile armazenamento, de armazenamento de arquivo tooBlob armazenamento e de armazenamento de Blob tooFile armazenamento de forma síncrona, AzCopy faz isso baixando memória de toolocal de dados de origem hello e carregá-lo novamente, toodestination.</span><span class="sxs-lookup"><span data-stu-id="bb692-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="bb692-199">O custo de saída padrão será aplicado.</span><span class="sxs-lookup"><span data-stu-id="bb692-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="bb692-200">Ao copiar do armazenamento de arquivo tooBlob armazenamento, tipo de blob saudação padrão é o blob de blocos, o usuário pode especificar a opção `/BlobType:page` toochange tipo de blob de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="bb692-201">Observe que `/SyncCopy` pode gerar saída adicional comparando cópia de tooasynchronous de custo, hello, abordagem recomendada é toouse essa opção Olá VM do Azure que está na saudação mesma região que o custo de egresso fonte armazenamento conta tooavoid.</span><span class="sxs-lookup"><span data-stu-id="bb692-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="bb692-202">Tabela: exportar</span><span class="sxs-lookup"><span data-stu-id="bb692-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="bb692-203">Exportar tabela</span><span class="sxs-lookup"><span data-stu-id="bb692-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="bb692-204">AzCopy grava uma pasta de destino especificado do arquivo de manifesto toohello.</span><span class="sxs-lookup"><span data-stu-id="bb692-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="bb692-205">arquivo de manifesto Olá é usado em arquivos de dados necessários de Olá Olá importação processo toolocate e executar a validação de dados.</span><span class="sxs-lookup"><span data-stu-id="bb692-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="bb692-206">arquivo de manifesto Olá usa Olá seguindo a convenção de nomenclatura por padrão:</span><span class="sxs-lookup"><span data-stu-id="bb692-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="bb692-207">Usuário também pode especificar a opção de saudação `/Manifest:<manifest file name>` tooset nome de arquivo de manifesto de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="bb692-208">Dividir exportação em vários arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="bb692-209">AzCopy usa um *índice de volume* na Olá dividir os dados de arquivo nomes toodistinguish vários arquivos.</span><span class="sxs-lookup"><span data-stu-id="bb692-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="bb692-210">índice de volume Olá consiste em duas partes, um *índice de intervalo de chave de partição* e um *índice de divisão de arquivo*.</span><span class="sxs-lookup"><span data-stu-id="bb692-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="bb692-211">Os dois índices são de base zero.</span><span class="sxs-lookup"><span data-stu-id="bb692-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="bb692-212">índice de intervalo de chave de partição Olá será 0 se o usuário não especificar a opção `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="bb692-212">hello partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="bb692-213">Por exemplo, suponha que AzCopy gera dois arquivos de dados depois que o usuário Olá Especifica a opção `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="bb692-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="bb692-214">Olá resultante nomes de arquivo de dados pode ser:</span><span class="sxs-lookup"><span data-stu-id="bb692-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="bb692-215">Observe que Olá mínimo valor possível para a opção `/SplitSize` é de 32 MB.</span><span class="sxs-lookup"><span data-stu-id="bb692-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="bb692-216">Se Olá especificado destino é o armazenamento de Blob, AzCopy será dividir o arquivo de dados de saudação uma vez seu limite de tamanho de tamanhos atingir Olá blob (200GB), independentemente de se a opção `/SplitSize` tiver sido especificado pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-216">If hello specified destination is Blob storage, AzCopy will split hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="bb692-217">Exportar tabela tooJSON ou formato de arquivo de dados CSV</span><span class="sxs-lookup"><span data-stu-id="bb692-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="bb692-218">AzCopy por padrão exporta arquivos de dados de tooJSON de tabelas.</span><span class="sxs-lookup"><span data-stu-id="bb692-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="bb692-219">Você pode especificar a opção de saudação `/PayloadFormat:JSON|CSV` tooexport tabelas de saudação como JSON ou CSV.</span><span class="sxs-lookup"><span data-stu-id="bb692-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="bb692-220">Ao especificar o formato de carga CSV hello, AzCopy também irá gerar um arquivo de esquema com extensão de arquivo `.schema.csv` para cada arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="bb692-220">When specifying hello CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="bb692-221">Exportar entidades de tabela simultaneamente</span><span class="sxs-lookup"><span data-stu-id="bb692-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="bb692-222">AzCopy começará a entidades de tooexport operações simultâneas ao usuário Olá Especifica a opção `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="bb692-222">AzCopy will start concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="bb692-223">Cada operação exporta um intervalor de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="bb692-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="bb692-224">Observe que o número de saudação de operações simultâneas também é controlado pela opção `/NC`.</span><span class="sxs-lookup"><span data-stu-id="bb692-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="bb692-225">AzCopy usa o número de saudação de processadores de núcleo como valor padrão Olá `/NC` ao copiar entidades de tabela, mesmo se `/NC` não foi especificado.</span><span class="sxs-lookup"><span data-stu-id="bb692-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="bb692-226">Quando o usuário Olá Especifica opção `/PKRS`, AzCopy usa Olá menor de saudação dois valores - partição intervalos de chaves versus operações simultâneas implicitamente ou explicitamente especificados - toodetermine Olá inúmeros toostart operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="bb692-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="bb692-227">Para obter mais detalhes, digite `AzCopy /?:NC` na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="bb692-228">Exportar a tabela tooblob</span><span class="sxs-lookup"><span data-stu-id="bb692-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="bb692-229">AzCopy irá gerar um arquivo de dados JSON no contêiner de blob Olá com a seguinte convenção de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="bb692-229">AzCopy will generate a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="bb692-230">arquivo de dados JSON Olá gerado segue o formato de carga de saudação para metadados mínimos.</span><span class="sxs-lookup"><span data-stu-id="bb692-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="bb692-231">Para obter detalhes sobre esse formado de carga, confira [Formato de carga para operações do serviço Tabela](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb692-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="bb692-232">Observe que, ao exportar tabelas tooblobs, AzCopy será baixar arquivos de dados temporários Olá tabela entidades toolocal e, em seguida, carregar o blob de toohello essas entidades.</span><span class="sxs-lookup"><span data-stu-id="bb692-232">Note that when exporting tables tooblobs, AzCopy will download hello Table entities toolocal temporary data files and then upload those entities toohello blob.</span></span> <span data-ttu-id="bb692-233">Esses arquivos de dados temporários são colocados na pasta de arquivo de diário Olá com caminho de padrão de hello "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", você pode especificar a opção/z [pasta de arquivo diário] toochange Olá local de pasta do arquivo de diário e, portanto, alterar o local dos arquivos de dados temporários hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="bb692-234">tamanho dos arquivos é decidido por de suas entidades de tabela tamanho e Olá especificado com hello opção /SplitSize, embora o arquivo de dados temporário Olá no disco local será excluído imediatamente depois de ter sido os dados temporários Hello carregados toohello blob, certifique-se de ter toostore de espaço suficiente em disco local desses arquivos de dados temporários antes de serem excluídos.</span><span class="sxs-lookup"><span data-stu-id="bb692-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk will be deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="bb692-235">Tabela: importar</span><span class="sxs-lookup"><span data-stu-id="bb692-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="bb692-236">Importar tabela</span><span class="sxs-lookup"><span data-stu-id="bb692-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="bb692-237">Olá opção `/EntityOperation` indica como entidades tooinsert em Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="bb692-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="bb692-238">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="bb692-238">Possible values are:</span></span>

* <span data-ttu-id="bb692-239">`InsertOrSkip`: Ignora uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="bb692-240">`InsertOrMerge`: Mescla uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="bb692-241">`InsertOrReplace`: Substitui uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="bb692-242">Observe que você não pode especificar a opção `/PKRS` no cenário de importação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="bb692-243">Ao contrário do cenário de exportação hello, em que você deve especificar a opção `/PKRS` toostart as operações simultâneas, AzCopy por padrão iniciará operações simultâneas quando você importa uma tabela.</span><span class="sxs-lookup"><span data-stu-id="bb692-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="bb692-244">número de operações simultâneas de Introdução do Hello padrão é toohello igual número de processadores de núcleo; No entanto, você pode especificar um número diferente de simultâneas com a opção `/NC`.</span><span class="sxs-lookup"><span data-stu-id="bb692-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="bb692-245">Para obter mais detalhes, digite `AzCopy /?:NC` na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="bb692-246">Observe que o AzCopy dá suporte apenas à importação para JSON, não para CSV.</span><span class="sxs-lookup"><span data-stu-id="bb692-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="bb692-247">O AzCopy não dá suporte a importações de tabela de arquivos JSON e de manifesto criados pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="bb692-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="bb692-248">Ambos os arquivos devem vir de uma exportação de tabela AzCopy.</span><span class="sxs-lookup"><span data-stu-id="bb692-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="bb692-249">erros de tooavoid, não modifique hello exportada JSON ou arquivo de manifesto.</span><span class="sxs-lookup"><span data-stu-id="bb692-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="bb692-250">Importar entidades tootable usando blobs</span><span class="sxs-lookup"><span data-stu-id="bb692-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="bb692-251">Suponha que um contêiner de Blob contenha seguinte Olá: arquivo JSON de um que representa uma tabela do Azure e seu arquivo de manifesto que o acompanha.</span><span class="sxs-lookup"><span data-stu-id="bb692-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="bb692-252">Você pode executar Olá entidades de tooimport de comando a seguir em uma tabela usando o arquivo de manifesto Olá desse contêiner de blob:</span><span class="sxs-lookup"><span data-stu-id="bb692-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="bb692-253">Outros recursos do AzCopy</span><span class="sxs-lookup"><span data-stu-id="bb692-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="bb692-254">Copiar somente os dados que não existem no destino de saudação</span><span class="sxs-lookup"><span data-stu-id="bb692-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="bb692-255">Olá `/XO` e `/XN` parâmetros permitem que os recursos de origem mais antiga ou mais recente de tooexclude que está sendo copiado, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="bb692-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="bb692-256">Se você desejar somente toocopy os recursos de origem que não existem no destino Olá, você pode especificar ambos os parâmetros em Olá AzCopy comando:</span><span class="sxs-lookup"><span data-stu-id="bb692-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="bb692-257">Observe que isso não é suportado quando Olá origem ou destino é uma tabela.</span><span class="sxs-lookup"><span data-stu-id="bb692-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="bb692-258">Usar parâmetros de linha de comando do arquivo toospecify uma resposta</span><span class="sxs-lookup"><span data-stu-id="bb692-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="bb692-259">É possível incluir qualquer parâmetro de linha de comando do AZCopy em um arquivo de resposta.</span><span class="sxs-lookup"><span data-stu-id="bb692-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="bb692-260">AzCopy processos Olá parâmetros no arquivo hello como se eles tivessem sido especificados na linha de comando hello, executar uma substituição direta com o conteúdo de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="bb692-261">Suponha que um arquivo de resposta chamado `copyoperation.txt`, que contém Olá linhas a seguir.</span><span class="sxs-lookup"><span data-stu-id="bb692-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="bb692-262">Cada parâmetro do AzCopy pode ser especificado em uma única linha</span><span class="sxs-lookup"><span data-stu-id="bb692-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="bb692-263">ou, em linhas separadas:</span><span class="sxs-lookup"><span data-stu-id="bb692-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="bb692-264">AzCopy falhará se você dividir o parâmetro hello em duas linhas, conforme mostrado aqui para Olá `/sourcekey` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="bb692-264">AzCopy will fail if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="bb692-265">Usar vários parâmetros de linha de comando de toospecify resposta arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="bb692-266">Vamos supor um arquivo de resposta chamado `source.txt` que especifique um contêiner de origem:</span><span class="sxs-lookup"><span data-stu-id="bb692-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="bb692-267">E um arquivo de resposta chamado `dest.txt` que especifica uma pasta de destino no sistema de arquivos de saudação:</span><span class="sxs-lookup"><span data-stu-id="bb692-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="bb692-268">E um arquivo de resposta chamado `options.txt` que especifique opções para o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="bb692-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="bb692-269">toocall AzCopy com esses arquivos de resposta, que residem em um diretório `C:\responsefiles`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="bb692-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="bb692-270">AzCopy processa este comando exatamente como seria se você incluiu todos os parâmetros individuais na linha de comando Olá Olá:</span><span class="sxs-lookup"><span data-stu-id="bb692-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="bb692-271">Especificar uma SAS</span><span class="sxs-lookup"><span data-stu-id="bb692-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="bb692-272">Você também pode especificar uma SAS no URI do contêiner hello:</span><span class="sxs-lookup"><span data-stu-id="bb692-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="bb692-273">Pasta de arquivo de diário</span><span class="sxs-lookup"><span data-stu-id="bb692-273">Journal file folder</span></span>
<span data-ttu-id="bb692-274">Cada vez que você emitir um comando tooAzCopy, ele verifica se um arquivo de diário existe na pasta padrão de hello, ou se ela existir em uma pasta que você especificou com esta opção.</span><span class="sxs-lookup"><span data-stu-id="bb692-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="bb692-275">Se o arquivo de diário Olá não existir em qualquer lugar, AzCopy trata operação hello como novo e gera um novo arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="bb692-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="bb692-276">Se existir um arquivo de diário hello, o AzCopy verificará se Olá linha de comando que você inserir corresponde Olá a linha de comando no arquivo de diário hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-276">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="bb692-277">Se duas linhas de comando Olá corresponder, AzCopy reinicia a operação de incompleta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="bb692-278">Se eles não coincidirem, você será solicitada tooeither substituir Olá diário arquivo toostart uma nova operação ou toocancel Olá atual operação.</span><span class="sxs-lookup"><span data-stu-id="bb692-278">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="bb692-279">Se desejar que o local do toouse saudação padrão para o arquivo de diário hello:</span><span class="sxs-lookup"><span data-stu-id="bb692-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="bb692-280">Se você omitir a opção `/Z`, ou especifique a opção `/Z` sem o caminho da pasta hello, como mostrado acima, AzCopy cria o arquivo de diário Olá no local padrão de saudação, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="bb692-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="bb692-281">Se já existir um arquivo de diário Olá, AzCopy retoma operação Olá com base no arquivo de diário hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="bb692-282">Se você desejar toospecify um local personalizado para o arquivo de diário hello:</span><span class="sxs-lookup"><span data-stu-id="bb692-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="bb692-283">Este exemplo cria o arquivo de diário Olá se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="bb692-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="bb692-284">Se ele existir, AzCopy retoma operação Olá com base no arquivo de diário hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="bb692-285">Se você desejar tooresume uma operação AzCopy:</span><span class="sxs-lookup"><span data-stu-id="bb692-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="bb692-286">Este exemplo retoma Olá última operação, que pode ter falhado toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bb692-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="bb692-287">Gerar um arquivo de log</span><span class="sxs-lookup"><span data-stu-id="bb692-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="bb692-288">Se você especificar a opção `/V` sem fornecer um log detalhado do toohello de caminho de arquivo, em seguida, AzCopy cria Olá arquivo de log no local padrão de saudação, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="bb692-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="bb692-289">Caso contrário, você pode criar um arquivo de log em um local personalizado:</span><span class="sxs-lookup"><span data-stu-id="bb692-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="bb692-290">Observe que, se você especificar um caminho relativo a opção a seguir `/V`, como `/V:test/azcopy1.log`, log detalhado Olá será criado no diretório de trabalho atual hello dentro de uma subpasta chamada `test`.</span><span class="sxs-lookup"><span data-stu-id="bb692-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="bb692-291">Saudação de número de operações simultâneas toostart</span><span class="sxs-lookup"><span data-stu-id="bb692-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="bb692-292">Opção `/NC` Especifica o número de saudação de operações simultâneas de cópia.</span><span class="sxs-lookup"><span data-stu-id="bb692-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="bb692-293">Por padrão, AzCopy inicia um determinado número de operações simultâneas tooincrease Olá transferência de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="bb692-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="bb692-294">Para operações de tabela, o número de saudação de operações simultâneas é igual toohello número de processadores que você tem.</span><span class="sxs-lookup"><span data-stu-id="bb692-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="bb692-295">Para operações de Blob e arquivo, número de saudação de operações simultâneas é ser igual 8 vezes Olá número de processadores que você tem.</span><span class="sxs-lookup"><span data-stu-id="bb692-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="bb692-296">Se você estiver executando o AzCopy através de uma rede de baixa largura de banda, você pode especificar um número menor para /NC tooavoid falha causada por divisão dos recursos.</span><span class="sxs-lookup"><span data-stu-id="bb692-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="bb692-297">Executar o AzCopy em um emulador de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="bb692-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="bb692-298">Você pode executar AzCopy em Olá [emulador de armazenamento do Azure](storage-use-emulator.md) para Blobs:</span><span class="sxs-lookup"><span data-stu-id="bb692-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="bb692-299">e Tabelas:</span><span class="sxs-lookup"><span data-stu-id="bb692-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="bb692-300">Parâmetros do AzCopy</span><span class="sxs-lookup"><span data-stu-id="bb692-300">AzCopy Parameters</span></span>
<span data-ttu-id="bb692-301">Veja abaixo uma descrição dos parâmetros do AzCopy.</span><span class="sxs-lookup"><span data-stu-id="bb692-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="bb692-302">Você também pode digitar um dos comandos a seguir na linha de comando Olá para obter ajuda usando AzCopy de saudação:</span><span class="sxs-lookup"><span data-stu-id="bb692-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="bb692-303">Para obter ajuda detalhada da linha de comando para o AzCopy: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="bb692-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="bb692-304">Para obter ajuda detalhada para qualquer parâmetro do AzCopy: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="bb692-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="bb692-305">Para obter exemplos da linha de comando: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="bb692-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="bb692-306">/Source:"origem"</span><span class="sxs-lookup"><span data-stu-id="bb692-306">/Source:"source"</span></span>
<span data-ttu-id="bb692-307">Especifica os dados de origem de saudação da qual toocopy.</span><span class="sxs-lookup"><span data-stu-id="bb692-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="bb692-308">origem de saudação pode ser um diretório de sistema de arquivos, um contêiner de blob, um diretório virtual de blob, um compartilhamento de arquivos de armazenamento, um diretório de arquivos de armazenamento ou uma tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb692-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="bb692-309">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="bb692-310">/Dest: "destino"</span><span class="sxs-lookup"><span data-stu-id="bb692-310">/Dest:"destination"</span></span>
<span data-ttu-id="bb692-311">Especifica a saudação toocopy de destino para.</span><span class="sxs-lookup"><span data-stu-id="bb692-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="bb692-312">destino de saudação pode ser um diretório de sistema de arquivos, um contêiner de blob, um diretório virtual de blob, um compartilhamento de arquivos de armazenamento, um diretório de arquivos de armazenamento ou uma tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb692-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="bb692-313">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="bb692-314">/Pattern:"padrão de arquivo"</span><span class="sxs-lookup"><span data-stu-id="bb692-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="bb692-315">Especifica um padrão de arquivo que indica qual toocopy de arquivos.</span><span class="sxs-lookup"><span data-stu-id="bb692-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="bb692-316">comportamento de saudação do parâmetro de /Pattern Olá é determinado pelo local Olá Olá dos dados de origem e Olá presença da opção de modo recursivo hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="bb692-317">O modo recursivo é especificado pela opção /S.</span><span class="sxs-lookup"><span data-stu-id="bb692-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="bb692-318">Se a origem especificada Olá é um diretório no sistema de arquivos hello, caracteres curinga padrão está em vigor e padrão do arquivo de saudação fornecido é comparado com arquivos no diretório hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="bb692-319">Se opção que /s for especificado, em seguida, AzCopy também corresponder ao padrão de saudação especificado em relação a todos os arquivos em todas as subpastas abaixo do diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="bb692-320">Se a origem de saudação especificado é um contêiner de blob ou diretório virtual, curingas não são aplicados.</span><span class="sxs-lookup"><span data-stu-id="bb692-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="bb692-321">Se a opção que /s for especificado, em seguida, AzCopy interpreta padrão de saudação de arquivo especificado como um prefixo de blob.</span><span class="sxs-lookup"><span data-stu-id="bb692-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="bb692-322">Se a opção que /s não for especificado, em seguida, AzCopy faz a correspondência de padrão de arquivo hello com nomes de blob exato.</span><span class="sxs-lookup"><span data-stu-id="bb692-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="bb692-323">Se Olá especificado origem é um compartilhamento de arquivos do Azure e, em seguida, você deve especificar nome do arquivo exato Olá, (por exemplo, abc.txt) toocopy um único arquivo, ou especifique a opção /S toocopy todos os arquivos no hello compartilhamento recursivamente.</span><span class="sxs-lookup"><span data-stu-id="bb692-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="bb692-324">Tentativa toospecify um padrão de arquivo e a opção /S juntos resultará em erro.</span><span class="sxs-lookup"><span data-stu-id="bb692-324">Attempting toospecify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="bb692-325">AzCopy usa a correspondência diferencia maiusculas de minúsculas quando Olá /Source é um contêiner de blob ou diretório virtual de blob e Olá de usa maiusculas de minúsculas correspondentes em todos os outros casos.</span><span class="sxs-lookup"><span data-stu-id="bb692-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="bb692-326">Olá padrão de arquivo padrão usado quando nenhum padrão de arquivo especificado é *.*</span><span class="sxs-lookup"><span data-stu-id="bb692-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="bb692-327">para uma localização do sistema de arquivos, ou um prefixo vazio para uma localização de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb692-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="bb692-328">Não é possível especificar diversos padrões para os arquivos.</span><span class="sxs-lookup"><span data-stu-id="bb692-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="bb692-329">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="bb692-330">/DestKey:"chave de armazenamento"</span><span class="sxs-lookup"><span data-stu-id="bb692-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="bb692-331">Especifica a chave de conta de armazenamento Olá para o recurso de destino hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="bb692-332">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="bb692-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="bb692-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="bb692-334">Especifica uma assinatura de acesso compartilhado (SAS) com permissões de leitura e gravação para o destino da saudação (se aplicável).</span><span class="sxs-lookup"><span data-stu-id="bb692-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="bb692-335">Olá surround SAS com aspas duplas, como ele pode contém caracteres especiais de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="bb692-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="bb692-336">Se o recurso de destino Olá é um contêiner de blob, compartilhamento de arquivo ou tabela, você pode especificar essa opção, seguida por um token SAS hello, ou você pode especificar Olá SAS como parte do contêiner de blob de destino hello, compartilhamento de arquivos ou URI da tabela, sem essa opção.</span><span class="sxs-lookup"><span data-stu-id="bb692-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="bb692-337">Se Olá origem e destino são ambos os blobs, o blob de destino Olá deve residir no hello mesmo conta de armazenamento como um blob de origem hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="bb692-338">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="bb692-339">/Sourcekey: "chave de armazenamento"</span><span class="sxs-lookup"><span data-stu-id="bb692-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="bb692-340">Especifica a chave de conta de armazenamento Olá para o recurso de fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="bb692-341">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="bb692-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="bb692-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="bb692-343">Especifica uma assinatura de acesso compartilhado com permissões de leitura e a lista de origem de saudação (se aplicável).</span><span class="sxs-lookup"><span data-stu-id="bb692-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="bb692-344">Olá surround SAS com aspas duplas, como ele pode contém caracteres especiais de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="bb692-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="bb692-345">Se o recurso de fonte de saudação é um contêiner de blob e uma chave, nem uma SAS é fornecida, o contêiner de blob hello serão lidos por meio do acesso anônimo.</span><span class="sxs-lookup"><span data-stu-id="bb692-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container will be read via anonymous access.</span></span>

<span data-ttu-id="bb692-346">Se a fonte de saudação é um compartilhamento de arquivo ou tabela, uma chave ou um SAS deve ser fornecido.</span><span class="sxs-lookup"><span data-stu-id="bb692-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="bb692-347">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="bb692-348">/S</span><span class="sxs-lookup"><span data-stu-id="bb692-348">/S</span></span>
<span data-ttu-id="bb692-349">Especifica o modo recursivo para operações de cópia.</span><span class="sxs-lookup"><span data-stu-id="bb692-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="bb692-350">No modo recursivo, AzCopy copiar todos os blobs ou arquivos que correspondem a saudação padrão de arquivo especificado, incluindo aqueles em subpastas.</span><span class="sxs-lookup"><span data-stu-id="bb692-350">In recursive mode, AzCopy will copy all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="bb692-351">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="bb692-352">/BlobType:"bloco" | "página" | "anexo"</span><span class="sxs-lookup"><span data-stu-id="bb692-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="bb692-353">Especifica se o blob de destino Olá é um blob de bloco, um blob de página ou um blob de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="bb692-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="bb692-354">Essa opção só será possível quando você estiver carregando um blob.</span><span class="sxs-lookup"><span data-stu-id="bb692-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="bb692-355">Caso contrário, um erro é gerado.</span><span class="sxs-lookup"><span data-stu-id="bb692-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="bb692-356">Se o destino de saudação é um blob e essa opção não for especificada, por padrão, AzCopy cria um blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="bb692-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="bb692-357">**Aplicável a:** Blobs</span><span class="sxs-lookup"><span data-stu-id="bb692-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="bb692-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="bb692-358">/CheckMD5</span></span>
<span data-ttu-id="bb692-359">Calcula um hash MD5 para dados baixados e verifica se o hash MD5 Olá armazenados no blob hello ou hash Olá calculado corresponde a propriedade de Content-MD5 do arquivo.</span><span class="sxs-lookup"><span data-stu-id="bb692-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="bb692-360">seleção de saudação MD5 é desativada por padrão, para que você deve especificar essa verificação de MD5 Olá opção tooperform durante o download de dados.</span><span class="sxs-lookup"><span data-stu-id="bb692-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="bb692-361">Observe que o armazenamento do Azure não garante que Olá hash MD5 armazenado para Olá blob ou arquivo é atualizado.</span><span class="sxs-lookup"><span data-stu-id="bb692-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="bb692-362">Olá tooupdate de responsabilidade do cliente MD5 é sempre que Olá blob ou arquivo é modificado.</span><span class="sxs-lookup"><span data-stu-id="bb692-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="bb692-363">AzCopy sempre define Olá Content-MD5 propriedade um blob do Azure ou arquivo após carregá-lo toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="bb692-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="bb692-364">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="bb692-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="bb692-365">/Snapshot</span></span>
<span data-ttu-id="bb692-366">Indica se tootransfer instantâneos.</span><span class="sxs-lookup"><span data-stu-id="bb692-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="bb692-367">Essa opção é válida somente quando a fonte de saudação for um blob.</span><span class="sxs-lookup"><span data-stu-id="bb692-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="bb692-368">Olá instantâneos de blob transferidos são renomeados neste formato: nome de blob (hora do instantâneo) .extension</span><span class="sxs-lookup"><span data-stu-id="bb692-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="bb692-369">Por padrão, os instantâneos não são copiados.</span><span class="sxs-lookup"><span data-stu-id="bb692-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="bb692-370">**Aplicável a:** Blobs</span><span class="sxs-lookup"><span data-stu-id="bb692-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="bb692-371">/V: [arquivo de log detalhado]</span><span class="sxs-lookup"><span data-stu-id="bb692-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="bb692-372">Produz mensagens de status detalhadas em um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="bb692-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="bb692-373">Por padrão, o arquivo de log detalhado Olá é denominado AzCopyVerbose.log em `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="bb692-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="bb692-374">Se você especificar um local de arquivo existente para essa opção, log detalhado hello serão acrescentadas toothat arquivo.</span><span class="sxs-lookup"><span data-stu-id="bb692-374">If you specify an existing file location for this option, hello verbose log will be appended toothat file.</span></span>  

<span data-ttu-id="bb692-375">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="bb692-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="bb692-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="bb692-377">Especifica uma pasta de arquivo de diário para retomar uma operação.</span><span class="sxs-lookup"><span data-stu-id="bb692-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="bb692-378">O AzCopy sempre dará suporte à retomada caso uma operação tenha sido interrompida.</span><span class="sxs-lookup"><span data-stu-id="bb692-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="bb692-379">Se essa opção não for especificada, ou ele é especificado sem um caminho de pasta, AzCopy irá criar o arquivo de diário Olá no local padrão de saudação, que é % LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="bb692-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="bb692-380">Cada vez que você emitir um comando tooAzCopy, ele verifica se um arquivo de diário existe na pasta padrão de hello, ou se ela existir em uma pasta que você especificou com esta opção.</span><span class="sxs-lookup"><span data-stu-id="bb692-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="bb692-381">Se o arquivo de diário Olá não existir em qualquer lugar, AzCopy trata operação hello como novo e gera um novo arquivo de diário.</span><span class="sxs-lookup"><span data-stu-id="bb692-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="bb692-382">Se existir um arquivo de diário hello, o AzCopy verificará se Olá linha de comando que você inserir corresponde Olá a linha de comando no arquivo de diário hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-382">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="bb692-383">Se duas linhas de comando Olá corresponder, AzCopy reinicia a operação de incompleta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="bb692-384">Se eles não coincidirem, você será solicitada tooeither substituir Olá diário arquivo toostart uma nova operação ou toocancel Olá atual operação.</span><span class="sxs-lookup"><span data-stu-id="bb692-384">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="bb692-385">arquivo de diário de saudação é excluído após a conclusão bem-sucedida da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="bb692-386">A retomada de uma operação de um arquivo de diário criado por uma versão anterior do AzCopy não é compatível.</span><span class="sxs-lookup"><span data-stu-id="bb692-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="bb692-387">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="bb692-388">/@: “arquivo de parâmetro”</span><span class="sxs-lookup"><span data-stu-id="bb692-388">/@:"parameter-file"</span></span>
<span data-ttu-id="bb692-389">Especifica um arquivo que contém parâmetros.</span><span class="sxs-lookup"><span data-stu-id="bb692-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="bb692-390">AzCopy processos Olá parâmetros no arquivo hello como se eles tivessem sido especificados na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="bb692-391">Em um arquivo de resposta, é possível especificar vários parâmetros em um único arquivo ou especificar cada parâmetro na própria linha.</span><span class="sxs-lookup"><span data-stu-id="bb692-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="bb692-392">Um parâmetro individual não pode abranger várias linhas.</span><span class="sxs-lookup"><span data-stu-id="bb692-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="bb692-393">Arquivos de resposta podem incluir linhas de comentários que começam com hello # símbolo.</span><span class="sxs-lookup"><span data-stu-id="bb692-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="bb692-394">É possível especificar vários arquivos de resposta.</span><span class="sxs-lookup"><span data-stu-id="bb692-394">You can specify multiple response files.</span></span> <span data-ttu-id="bb692-395">No entanto, o AzCopy não permite arquivos de resposta aninhados.</span><span class="sxs-lookup"><span data-stu-id="bb692-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="bb692-396">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="bb692-397">/Y</span><span class="sxs-lookup"><span data-stu-id="bb692-397">/Y</span></span>
<span data-ttu-id="bb692-398">Suprime todas as solicitações de confirmação do AzCopy.</span><span class="sxs-lookup"><span data-stu-id="bb692-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="bb692-399">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="bb692-400">/L</span><span class="sxs-lookup"><span data-stu-id="bb692-400">/L</span></span>
<span data-ttu-id="bb692-401">Especifica uma operação de listagem apenas. Nenhum dado é copiado.</span><span class="sxs-lookup"><span data-stu-id="bb692-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="bb692-402">AzCopy interpretará hello usando dessa opção como uma simulação de linha de comando Olá em execução sem essa opção /L e contagem de quantos objetos serão copiados, você pode especificar a opção /V no Olá a mesma hora toocheck quais objetos serão copiados em log detalhado hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-402">AzCopy will interpret hello using of this option as a simulation for running hello command line without this option /L and count how many objects will be copied, you can specify option /V at hello same time toocheck which objects will be copied in hello verbose log.</span></span>

<span data-ttu-id="bb692-403">comportamento de saudação dessa opção também é determinado pelo local Olá Olá dos dados de origem e a presença de Olá Olá recursiva modo opção /S e arquivo padrão da opção de /Pattern.</span><span class="sxs-lookup"><span data-stu-id="bb692-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="bb692-404">O AzCopy exige a permissão de LISTAGEM e de LEITURA deste local de origem ao usar essa opção.</span><span class="sxs-lookup"><span data-stu-id="bb692-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="bb692-405">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="bb692-406">/MT</span><span class="sxs-lookup"><span data-stu-id="bb692-406">/MT</span></span>
<span data-ttu-id="bb692-407">Define a hora da última modificação do arquivo baixado Olá toobe Olá mesmo como o blob de origem hello ou do arquivo.</span><span class="sxs-lookup"><span data-stu-id="bb692-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="bb692-408">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="bb692-409">/XN</span><span class="sxs-lookup"><span data-stu-id="bb692-409">/XN</span></span>
<span data-ttu-id="bb692-410">Exclui um recurso de origem mais novo.</span><span class="sxs-lookup"><span data-stu-id="bb692-410">Excludes a newer source resource.</span></span> <span data-ttu-id="bb692-411">recurso de saudação não será copiado se hora da última modificação do código-fonte Olá Olá é hello igual ou mais recente do que o destino.</span><span class="sxs-lookup"><span data-stu-id="bb692-411">hello resource will not be copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="bb692-412">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="bb692-413">/XO</span><span class="sxs-lookup"><span data-stu-id="bb692-413">/XO</span></span>
<span data-ttu-id="bb692-414">Exclui um recurso de origem mais antigo.</span><span class="sxs-lookup"><span data-stu-id="bb692-414">Excludes an older source resource.</span></span> <span data-ttu-id="bb692-415">recurso Olá não será copiado se a hora da última modificação do código-fonte Olá Olá é hello mesmo ou mais antigo que o destino.</span><span class="sxs-lookup"><span data-stu-id="bb692-415">hello resource will not be copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="bb692-416">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="bb692-417">/A</span><span class="sxs-lookup"><span data-stu-id="bb692-417">/A</span></span>
<span data-ttu-id="bb692-418">Carrega somente os arquivos que têm o atributo de arquivo morto de saudação configurado.</span><span class="sxs-lookup"><span data-stu-id="bb692-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="bb692-419">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="bb692-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="bb692-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="bb692-421">Carrega somente os arquivos que têm algum Olá especificado de atributos.</span><span class="sxs-lookup"><span data-stu-id="bb692-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="bb692-422">Entre os atributos disponíveis estão:</span><span class="sxs-lookup"><span data-stu-id="bb692-422">Available attributes include:</span></span>

* <span data-ttu-id="bb692-423">R = Arquivos somente leitura</span><span class="sxs-lookup"><span data-stu-id="bb692-423">R = Read-only files</span></span>
* <span data-ttu-id="bb692-424">A = Arquivos prontos para arquivamento</span><span class="sxs-lookup"><span data-stu-id="bb692-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="bb692-425">S = Arquivos de sistema</span><span class="sxs-lookup"><span data-stu-id="bb692-425">S = System files</span></span>
* <span data-ttu-id="bb692-426">H = Arquivos ocultos</span><span class="sxs-lookup"><span data-stu-id="bb692-426">H = Hidden files</span></span>
* <span data-ttu-id="bb692-427">C = Arquivo compactado</span><span class="sxs-lookup"><span data-stu-id="bb692-427">C = Compressed files</span></span>
* <span data-ttu-id="bb692-428">N = Arquivos normais</span><span class="sxs-lookup"><span data-stu-id="bb692-428">N = Normal files</span></span>
* <span data-ttu-id="bb692-429">E = Arquivos criptografados</span><span class="sxs-lookup"><span data-stu-id="bb692-429">E = Encrypted files</span></span>
* <span data-ttu-id="bb692-430">T = Arquivos temporários</span><span class="sxs-lookup"><span data-stu-id="bb692-430">T = Temporary files</span></span>
* <span data-ttu-id="bb692-431">O = Arquivos offline</span><span class="sxs-lookup"><span data-stu-id="bb692-431">O = Offline files</span></span>
* <span data-ttu-id="bb692-432">I = Arquivos não indexados</span><span class="sxs-lookup"><span data-stu-id="bb692-432">I = Non-indexed files</span></span>

<span data-ttu-id="bb692-433">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="bb692-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="bb692-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="bb692-435">Exclui os arquivos que têm algum Olá especificado conjunto de atributos.</span><span class="sxs-lookup"><span data-stu-id="bb692-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="bb692-436">Entre os atributos disponíveis estão:</span><span class="sxs-lookup"><span data-stu-id="bb692-436">Available attributes include:</span></span>

* <span data-ttu-id="bb692-437">R = Arquivos somente leitura</span><span class="sxs-lookup"><span data-stu-id="bb692-437">R = Read-only files</span></span>
* <span data-ttu-id="bb692-438">A = Arquivos prontos para arquivamento</span><span class="sxs-lookup"><span data-stu-id="bb692-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="bb692-439">S = Arquivos de sistema</span><span class="sxs-lookup"><span data-stu-id="bb692-439">S = System files</span></span>
* <span data-ttu-id="bb692-440">H = Arquivos ocultos</span><span class="sxs-lookup"><span data-stu-id="bb692-440">H = Hidden files</span></span>
* <span data-ttu-id="bb692-441">C = Arquivo compactado</span><span class="sxs-lookup"><span data-stu-id="bb692-441">C = Compressed files</span></span>
* <span data-ttu-id="bb692-442">N = Arquivos normais</span><span class="sxs-lookup"><span data-stu-id="bb692-442">N = Normal files</span></span>
* <span data-ttu-id="bb692-443">E = Arquivos criptografados</span><span class="sxs-lookup"><span data-stu-id="bb692-443">E = Encrypted files</span></span>
* <span data-ttu-id="bb692-444">T = Arquivos temporários</span><span class="sxs-lookup"><span data-stu-id="bb692-444">T = Temporary files</span></span>
* <span data-ttu-id="bb692-445">O = Arquivos offline</span><span class="sxs-lookup"><span data-stu-id="bb692-445">O = Offline files</span></span>
* <span data-ttu-id="bb692-446">I = Arquivos não indexados</span><span class="sxs-lookup"><span data-stu-id="bb692-446">I = Non-indexed files</span></span>

<span data-ttu-id="bb692-447">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="bb692-448">/Delimiter: "delimitador"</span><span class="sxs-lookup"><span data-stu-id="bb692-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="bb692-449">Indica o caractere delimitador de saudação usado diretórios virtuais toodelimit em um nome de blob.</span><span class="sxs-lookup"><span data-stu-id="bb692-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="bb692-450">Por padrão, usa AzCopy / como o caractere delimitador de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="bb692-451">No entanto, o AzCopy dá suporte ao uso de qualquer caractere comum (como @, # ou %) como delimitador.</span><span class="sxs-lookup"><span data-stu-id="bb692-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="bb692-452">Se você precisar tooinclude um desses caracteres especiais na linha de comando hello, inclua o nome do arquivo de saudação com aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="bb692-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="bb692-453">Essa opção só é aplicável para o download de blobs.</span><span class="sxs-lookup"><span data-stu-id="bb692-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="bb692-454">**Aplicável a:** Blobs</span><span class="sxs-lookup"><span data-stu-id="bb692-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="bb692-455">/NC: "número-de-operações-simultâneas"</span><span class="sxs-lookup"><span data-stu-id="bb692-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="bb692-456">Especifica o número de saudação de operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="bb692-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="bb692-457">AzCopy por padrão inicia um determinado número de operações simultâneas tooincrease Olá transferência de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="bb692-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="bb692-458">Observe que o grande número de operações simultâneas em um ambiente de baixa largura de banda pode sobrecarregar a conexão de rede de saudação e evitar operações de saudação de ser totalmente concluída.</span><span class="sxs-lookup"><span data-stu-id="bb692-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="bb692-459">Limite operações simultâneas com base na largura de banda real de rede disponível.</span><span class="sxs-lookup"><span data-stu-id="bb692-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="bb692-460">limite superior de saudação para as operações simultâneas é 512.</span><span class="sxs-lookup"><span data-stu-id="bb692-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="bb692-461">**Aplicável a:** Blobs, Arquivos, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="bb692-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="bb692-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="bb692-463">Especifica que Olá `source` recurso é um blob disponível no ambiente de desenvolvimento local hello, em execução no emulador de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="bb692-464">**Aplicável a:** Blobs, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="bb692-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="bb692-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="bb692-466">Especifica que Olá `destination` recurso é um blob disponível no ambiente de desenvolvimento local hello, em execução no emulador de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="bb692-467">**Aplicável a:** Blobs, Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="bb692-468">/PKRS: "chave1#chave2#chave3#..."</span><span class="sxs-lookup"><span data-stu-id="bb692-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="bb692-469">Divisões Olá tooenable de intervalo de chave de partição, exportação de dados de tabela em paralelo, o que aumenta a velocidade de Olá Olá da operação de exportação.</span><span class="sxs-lookup"><span data-stu-id="bb692-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="bb692-470">Se essa opção não for especificada, o AzCopy usa entidades de tabela tooexport de thread único.</span><span class="sxs-lookup"><span data-stu-id="bb692-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="bb692-471">Por exemplo, se hello usuário Especifica /PKRS: "aa #bb" e, em seguida, AzCopy inicia três operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="bb692-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="bb692-472">Cada operação exporta um dos três intervalos de chaves de partição, como mostramos abaixo:</span><span class="sxs-lookup"><span data-stu-id="bb692-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="bb692-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="bb692-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="bb692-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="bb692-474">[aa, bb)</span></span>

  <span data-ttu-id="bb692-475">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="bb692-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="bb692-476">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="bb692-477">/Splitsize: "tamanho do arquivo"</span><span class="sxs-lookup"><span data-stu-id="bb692-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="bb692-478">Especifica Olá arquivo exportado de dividir o tamanho em MB, Olá valor mínimo permitido é 32.</span><span class="sxs-lookup"><span data-stu-id="bb692-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="bb692-479">Se essa opção não for especificada, AzCopy será Exportar arquivo de toosingle de dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="bb692-479">If this option is not specified, AzCopy will export table data toosingle file.</span></span>

<span data-ttu-id="bb692-480">Se dados de tabela de saudação são exportado tooa blob e hello, tamanho do arquivo exportado atinge Olá limite de 200 GB para o tamanho do blob, AzCopy dividirá arquivo exportado do hello, mesmo se essa opção não for especificada.</span><span class="sxs-lookup"><span data-stu-id="bb692-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy will split hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="bb692-481">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="bb692-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="bb692-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="bb692-483">Especifica o comportamento de importação de dados de tabela hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="bb692-484">InsertOrSkip - ignora uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="bb692-485">InsertOrMerge - mescla uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="bb692-486">InsertOrReplace - substitui uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="bb692-487">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="bb692-488">/Manifesto: "arquivo de manifesto"</span><span class="sxs-lookup"><span data-stu-id="bb692-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="bb692-489">Especifica o arquivo de manifesto Olá para tabela Olá exportar e importar a operação.</span><span class="sxs-lookup"><span data-stu-id="bb692-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="bb692-490">Essa opção é opcional durante a operação de exportação hello, AzCopy irá gerar um arquivo de manifesto com nome pré-definido se essa opção não for especificada.</span><span class="sxs-lookup"><span data-stu-id="bb692-490">This option is optional during hello export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="bb692-491">Essa opção é necessária durante a operação de importação Olá para localizar os arquivos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="bb692-492">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="bb692-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="bb692-493">/SyncCopy</span></span>
<span data-ttu-id="bb692-494">Indica se toosynchronously copiar blobs ou arquivos entre dois pontos de extremidade de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb692-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="bb692-495">O AzCopy por padrão usa cópia assíncrona no servidor.</span><span class="sxs-lookup"><span data-stu-id="bb692-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="bb692-496">Especifique esse tooperform opção um síncrono copiar, que faz o download de blobs ou arquivos toolocal memória e, em seguida, carrega tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bb692-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="bb692-497">Você pode usar essa opção ao copiar arquivos no armazenamento de Blob no armazenamento de arquivo ou Blob storage tooFile armazenamento ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="bb692-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="bb692-498">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="bb692-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="bb692-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="bb692-500">Especifica o tipo de conteúdo MIME Olá para blobs de destino ou arquivos.</span><span class="sxs-lookup"><span data-stu-id="bb692-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="bb692-501">Conjuntos de AzCopy Olá o tipo de conteúdo para um blob ou arquivo tooapplication/octet-stream por padrão.</span><span class="sxs-lookup"><span data-stu-id="bb692-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="bb692-502">Você pode definir o tipo de conteúdo Olá para todos os blobs ou arquivos especificando explicitamente um valor para essa opção.</span><span class="sxs-lookup"><span data-stu-id="bb692-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="bb692-503">Se você especificar essa opção sem um valor, AzCopy definirá cada blob ou tipo de conteúdo do arquivo de acordo com tooits extensão de arquivo.</span><span class="sxs-lookup"><span data-stu-id="bb692-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="bb692-504">**Aplicável a:** Blobs, Arquivos</span><span class="sxs-lookup"><span data-stu-id="bb692-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="bb692-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="bb692-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="bb692-506">Especifica o formato de Olá Olá tabela exportada do arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="bb692-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="bb692-507">Se essa opção não for especificada, por padrão, o AzCopy exportará o arquivo de dados da tabela no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="bb692-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="bb692-508">**Aplicável a:** Tabelas</span><span class="sxs-lookup"><span data-stu-id="bb692-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="bb692-509">Problemas Conhecidos e Práticas Recomendadas</span><span class="sxs-lookup"><span data-stu-id="bb692-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="bb692-510">Limite gravações simultâneas durante a cópia de dados</span><span class="sxs-lookup"><span data-stu-id="bb692-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="bb692-511">Quando você copia blobs ou arquivos com AzCopy, tenha em mente que outro aplicativo esteja modificando dados saudação enquanto você estiver copiando-lo.</span><span class="sxs-lookup"><span data-stu-id="bb692-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="bb692-512">Se possível, certifique-se de que dados Olá que você está copiando não está sendo modificados durante a operação de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb692-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="bb692-513">Por exemplo, ao copiar um VHD associado a uma máquina virtual do Azure, certifique-se de que nenhum outro aplicativo no momento está escrevendo toohello VHD.</span><span class="sxs-lookup"><span data-stu-id="bb692-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="bb692-514">Toodo uma boa maneira trata concedendo Olá recurso toobe copiado.</span><span class="sxs-lookup"><span data-stu-id="bb692-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="bb692-515">Como alternativa, você pode criar um instantâneo de saudação VHD primeiro e copie instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="bb692-516">Se você não pode impedir que outros aplicativos gravando tooblobs ou arquivos enquanto eles estão sendo copiados, em seguida, tenha em mente que, pelo trabalho de Olá Olá tempo termina, hello recursos copiados não podem mais ter paridade completa com os recursos de origem hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="bb692-517">Execute uma instância de AzCopy em um computador.</span><span class="sxs-lookup"><span data-stu-id="bb692-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="bb692-518">AzCopy é projetado toomaximize Olá utilização sua máquina recurso tooaccelerate Olá de transferência de dados, é recomendável executar apenas uma instância de AzCopy em um computador e especificar a opção Olá `/NC` se você precisar de operações simultâneas mais.</span><span class="sxs-lookup"><span data-stu-id="bb692-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="bb692-519">Para obter mais detalhes, digite `AzCopy /?:NC` na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="bb692-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="bb692-520">Habilite algoritmos MD5 compatíveis com FIPS para o AzCopy quando você "Usar algoritmos compatíveis com FIPS para criptografia, hash e assinatura".</span><span class="sxs-lookup"><span data-stu-id="bb692-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="bb692-521">AzCopy por padrão usa Olá toocalculate da implementação .NET MD5 MD5 ao copiar objetos, mas há alguns requisitos de segurança que precisam de configuração FIPS MD5 compatível tooenable AzCopy.</span><span class="sxs-lookup"><span data-stu-id="bb692-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="bb692-522">Você pode criar um arquivo app.config `AzCopy.exe.config` com a propriedade `AzureStorageUseV1MD5` e reservá-lo com o AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="bb692-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="bb692-523">Para a propriedade "AzureStorageUseV1MD5" • True - valor saudação padrão AzCopy usará implementação .NET MD5.</span><span class="sxs-lookup"><span data-stu-id="bb692-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="bb692-524">• False – o AzCopy usará o algoritmo MD5 compatível com FIPS.</span><span class="sxs-lookup"><span data-stu-id="bb692-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="bb692-525">Observe que os algoritmos compatíveis com FIPS estão desabilitados por padrão em seu computador com Windows. Digite secpol.msc na janela Executar e marque essa opção em Configuração de Segurança -> Segurança -> Políticas Locais > Opções de Segurança > Criptografia do Sistema: usar algoritmos compatíveis com FIPS para criptografia, hash e assinatura.</span><span class="sxs-lookup"><span data-stu-id="bb692-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb692-526">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb692-526">Next steps</span></span>
<span data-ttu-id="bb692-527">Para obter mais informações sobre o armazenamento do Azure e AzCopy, consulte toohello recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="bb692-527">For more information about Azure Storage and AzCopy, refer toohello following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="bb692-528">Documentação do Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="bb692-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="bb692-529">Introdução tooAzure armazenamento</span><span class="sxs-lookup"><span data-stu-id="bb692-529">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="bb692-530">Como toouse armazenamento de BLOBs no .NET</span><span class="sxs-lookup"><span data-stu-id="bb692-530">How toouse Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="bb692-531">Como toouse armazenamento de arquivo do .NET</span><span class="sxs-lookup"><span data-stu-id="bb692-531">How toouse File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="bb692-532">Como toouse o armazenamento de tabela do .NET</span><span class="sxs-lookup"><span data-stu-id="bb692-532">How toouse Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="bb692-533">Como toocreate, gerenciar ou excluir uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="bb692-533">How toocreate, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="bb692-534">Transferir dados com o AzCopy no Linux</span><span class="sxs-lookup"><span data-stu-id="bb692-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="bb692-535">Postagens de blog de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="bb692-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="bb692-536">Apresentando a versão de visualização da biblioteca de movimentação de dados do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="bb692-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="bb692-537">AzCopy: Introducing synchronous copy and customized content type (AzCopy: introdução a cópia síncrona e tipo de conteúdo personalizado)</span><span class="sxs-lookup"><span data-stu-id="bb692-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="bb692-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support (AzCopy: anúncio de disponibilidade geral do AzCopy 3.0 mais versão de teste do AzCopy 4.0 com suporte para Tabela e Arquivo)</span><span class="sxs-lookup"><span data-stu-id="bb692-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="bb692-539">AzCopy: Optimized for Large-Scale Copy Scenarios (AzCopy: otimizado para cenários de cópia em larga escala)</span><span class="sxs-lookup"><span data-stu-id="bb692-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="bb692-540">AzCopy: Support for read-access geo-redundant storage (AzCopy: suporte para o armazenamento com redundância geográfica com acesso de leitura)</span><span class="sxs-lookup"><span data-stu-id="bb692-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="bb692-541">AzCopy: Transfer data with re-startable mode and SAS token (AzCopy: transferir dados com o modo reiniciável e token de SAS)</span><span class="sxs-lookup"><span data-stu-id="bb692-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="bb692-542">AzCopy: Using cross-account Copy Blob (AzCopy: usando blob de cópia em várias contas)</span><span class="sxs-lookup"><span data-stu-id="bb692-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="bb692-543">AzCopy: Uploading/downloading files for Azure Blobs (AzCopy: Upload/download de arquivos para Blobs do Azure)</span><span class="sxs-lookup"><span data-stu-id="bb692-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

