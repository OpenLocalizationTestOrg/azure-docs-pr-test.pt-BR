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
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Transferência de dados com hello AzCopy no Windows
AzCopy é um utilitário de linha de comando projetado para copiar dados tooand do armazenamento de BLOBs do Microsoft Azure, o arquivo e a tabela usando comandos simples com um desempenho ideal. Você pode copiar dados de um tooanother de objeto dentro de sua conta de armazenamento, ou entre contas de armazenamento.

Há duas versões do AzCopy que podem ser baixadas. O AzCopy no Windows se baseia no .NET Framework e oferece opções de linha de comando no estilo Windows. O [AzCopy no Linux](storage-use-azcopy-linux.md) se baseia no .NET Core Framework, que se destina a plataformas Linux que oferecem opções de linha de comando no estilo POSIX. Este artigo aborda o AzCopy no Windows.

## <a name="download-and-install-azcopy"></a>Baixar e instalar o AzCopy
### <a name="azcopy-on-windows"></a>AzCopy no Windows
Baixar Olá [versão mais recente do AzCopy no Windows](http://aka.ms/downloadazcopy).

#### <a name="installation-on-windows"></a>Instalação no Windows
Depois de instalar o AzCopy no Windows usando o instalador hello, abra uma janela de comando e navegue toohello AzCopy diretório de instalação no seu computador - onde hello `AzCopy.exe` executável está localizado. Se desejar, você pode adicionar o caminho de sistema de tooyour Olá AzCopy instalação local. Por padrão, AzCopy é instalado muito`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` ou `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>Como escrever seu primeiro comando do AzCopy
Olá a sintaxe básica para comandos do AzCopy é:

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

Olá exemplos a seguir demonstram uma variedade de cenários para copiar dados tooand de Blobs do Microsoft Azure, arquivos e tabelas. Consulte toohello [AzCopy parâmetros](#azcopy-parameters) seção para obter uma explicação detalhada de parâmetros de saudação usados em cada exemplo.

## <a name="blob-download"></a>Blob: baixar
### <a name="download-single-blob"></a>Baixar um único blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Observe que, se pasta Olá `C:\myfolder` não existir, AzCopy irá criá-lo e baixar `abc.txt ` na nova pasta de saudação.

### <a name="download-single-blob-from-secondary-region"></a>Baixe um único blob de região secundária

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.

### <a name="download-all-blobs"></a>Baixar todos os blobs

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Suponha seguinte Olá blobs residem no contêiner especificado hello:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Após a operação de download de Olá Olá diretório `C:\myfolder` incluirá Olá seguintes arquivos:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Se você não especificar a opção `/S`, nenhum blob será baixado.

### <a name="download-blobs-with-specified-prefix"></a>Baixar blobs com prefixo especificado

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Suponha seguinte Olá blobs residem no contêiner especificado hello. Todos os blobs que começam com o prefixo Olá `a` serão baixados:

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Após a operação de download de Olá Olá pasta `C:\myfolder` incluirá Olá seguintes arquivos:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

prefixo de saudação aplica diretório virtual toohello, que constitui Olá primeira parte do nome do blob hello. Exemplo hello mostrado acima, diretório virtual Olá não coincide com prefixo especificado de hello, portanto ele não será baixado. Além disso, se hello opção `\S` não for especificado, AzCopy não baixará todos os blobs.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Definir a hora da última modificação Olá dos arquivos exportados toobe mesmo Olá blobs de origem

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

Você também pode excluir blobs de operação de download de saudação com base em sua hora da última modificação. Por exemplo, se você quiser blobs tooexclude cuja hora da última modificação é hello igual ou mais recente do que o arquivo de destino hello, adicionar Olá `/XN` opção:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

Ou se você quiser blobs tooexclude cuja hora da última modificação é hello mesmo ou mais antigo que o arquivo de destino hello, adicione Olá `/XO` opção:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>Blob: carregar
### <a name="upload-single-file"></a>Carregar um único arquivo

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Se Olá contêiner de destino especificado não existe, AzCopy será criá-lo e carregar o arquivo hello nele.

### <a name="upload-single-file-toovirtual-directory"></a>Carregar arquivo único diretório toovirtual

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Se Olá especificado não existe um diretório virtual, AzCopy carregará Olá arquivo tooinclude Olá diretório virtual em seu nome (*, por exemplo,*, `vd/abc.txt` no exemplo hello acima).

### <a name="upload-all-files"></a>Carregar todos os arquivos

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

Especificando a opção `/S` carregamentos conteúdo Olá Olá especificado diretório tooBlob armazenamento recursivamente, que significa que todas as subpastas e seus arquivos serão carregados também. Por exemplo, suponha que a seguir Olá arquivos residem na pasta `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Após a operação de carregamento de saudação contêiner Olá incluirá Olá seguintes arquivos:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Se você não especificar a opção `/S`, o AzCopy não carregará de forma recursiva. Após a operação de carregamento de saudação contêiner Olá incluirá Olá seguintes arquivos:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>Carregar arquivos que correspondam ao padrão especificado

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Suponha seguinte Olá arquivos residem na pasta `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Após a operação de carregamento de saudação contêiner Olá incluirá Olá seguintes arquivos:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Se você não especificar a opção `/S`, o AzCopy carregará somente os blobs que não residem em um diretório virtual:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Especifique o tipo de conteúdo MIME Olá de um blob de destino
Por padrão, AzCopy define Olá de tipo de conteúdo de um blob de destino muito`application/octet-stream`. A partir da versão 3.1.0, você pode especificar explicitamente o tipo de conteúdo Olá por meio da opção Olá `/SetContentType:[content-type]`. Essa sintaxe define o tipo de conteúdo Olá para todos os blobs em uma operação de carregamento.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

Se você especificar `/SetContentType` sem um valor, em seguida, AzCopy definirá cada blob ou tipo de conteúdo do arquivo de acordo com tooits extensão de arquivo.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>Blob: copiar
### <a name="copy-single-blob-within-storage-account"></a>Copiar um único blob dentro da conta de armazenamento

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

Quando você copia um blob em uma conta de armazenamento, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é realizada.

### <a name="copy-single-blob-across-storage-accounts"></a>Copiar um único blob entre contas de armazenamento

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Quando você copia um blob entre contas de armazenamento, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é realizada.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copiar um único blob da região de tooprimary região secundária

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copiar um único blob e seus instantâneos entre contas de armazenamento

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Após a operação de cópia hello, o contêiner de destino Olá incluirá Olá blob e seus instantâneos. Supondo que o blob de saudação no exemplo hello acima tem dois instantâneos, contêiner Olá incluirá a seguir Olá blob e instantâneos:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Copiar blobs em regiões entre contas de armazenamento de forma síncrona.
O AzCopy por padrão copia dados entre dois pontos de extremidade de armazenamento assincronamente. Então, a operação de cópia de saudação será executado no plano de fundo de saudação utilizando a capacidade de largura de banda sobressalente com nenhum SLA em termos de rapidez com que um blob será copiado e AzCopy verificará periodicamente o status da cópia Olá até Olá cópia é concluída ou falha.

Olá `/SyncCopy` opção garante que a operação de cópia Olá obterá velocidade consistente. AzCopy executa cópia síncrona Olá ao baixar blobs Olá toocopy de saudação especificado fonte toolocal da memória e, em seguida, carregá-las toohello destino de armazenamento de Blob.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`pode gerar saída adicional de custo cópia tooasynchronous comparados, hello a abordagem recomendada é toouse essa opção em uma VM do Azure que está em Olá mesma região que o custo de egresso fonte armazenamento conta tooavoid.

## <a name="file-download"></a>Arquivo: baixar
### <a name="download-single-file"></a>Baixar um único arquivo

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Se Olá especificado fonte for um compartilhamento de arquivos do Azure, você deve especificar nome de arquivo exatos Olá, (*, por exemplo,* `abc.txt`) toodownload um único arquivo, ou especifique a opção `/S` toodownload todos os arquivos no compartilhamento de saudação recursivamente. Tentativa de toospecify um padrão de arquivo e a opção `/S` juntos resultará em erro.

### <a name="download-all-files"></a>Baixar todos os arquivos

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Observe que nenhuma pasta vazia será baixada.

## <a name="file-upload"></a>Arquivo: carregar
### <a name="upload-single-file"></a>Carregar um único arquivo

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>Carregar todos os arquivos

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Observe que nenhuma pasta vazia será carregada.

### <a name="upload-files-matching-specified-pattern"></a>Carregar arquivos que correspondam ao padrão especificado

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>Arquivo: copiar
### <a name="copy-across-file-shares"></a>Copiar entre compartilhamentos de arquivos

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
Quando você copia um arquivo entre compartilhamentos de arquivos, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-file-share-tooblob"></a>Copiar de tooblob de compartilhamento de arquivo

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
Quando você copia um arquivo de tooblob de compartilhamento de arquivo, uma [cópia do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operação é executada.


### <a name="copy-from-blob-toofile-share"></a>Copiar de blob toofile compartilhamento

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
Quando você copia um arquivo de compartilhamento de toofile de blob, um [cópia do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operação é executada.

### <a name="synchronously-copy-files"></a>Copiar arquivos de forma síncrona
Você pode especificar Olá `/SyncCopy` opção toocopy dados de armazenamento de arquivo tooFile armazenamento, de armazenamento de arquivo tooBlob armazenamento e de armazenamento de Blob tooFile armazenamento de forma síncrona, AzCopy faz isso baixando memória de toolocal de dados de origem hello e carregá-lo novamente, toodestination. O custo de saída padrão será aplicado.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

Ao copiar do armazenamento de arquivo tooBlob armazenamento, tipo de blob saudação padrão é o blob de blocos, o usuário pode especificar a opção `/BlobType:page` toochange tipo de blob de destino de saudação.

Observe que `/SyncCopy` pode gerar saída adicional comparando cópia de tooasynchronous de custo, hello, abordagem recomendada é toouse essa opção Olá VM do Azure que está na saudação mesma região que o custo de egresso fonte armazenamento conta tooavoid.

## <a name="table-export"></a>Tabela: exportar
### <a name="export-table"></a>Exportar tabela

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy grava uma pasta de destino especificado do arquivo de manifesto toohello. arquivo de manifesto Olá é usado em arquivos de dados necessários de Olá Olá importação processo toolocate e executar a validação de dados. arquivo de manifesto Olá usa Olá seguindo a convenção de nomenclatura por padrão:

    <account name>_<table name>_<timestamp>.manifest

Usuário também pode especificar a opção de saudação `/Manifest:<manifest file name>` tooset nome de arquivo de manifesto de saudação.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>Dividir exportação em vários arquivos

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

AzCopy usa um *índice de volume* na Olá dividir os dados de arquivo nomes toodistinguish vários arquivos. índice de volume Olá consiste em duas partes, um *índice de intervalo de chave de partição* e um *índice de divisão de arquivo*. Os dois índices são de base zero.

índice de intervalo de chave de partição Olá será 0 se o usuário não especificar a opção `/PKRS`.

Por exemplo, suponha que AzCopy gera dois arquivos de dados depois que o usuário Olá Especifica a opção `/SplitSize`. Olá resultante nomes de arquivo de dados pode ser:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Observe que Olá mínimo valor possível para a opção `/SplitSize` é de 32 MB. Se Olá especificado destino é o armazenamento de Blob, AzCopy será dividir o arquivo de dados de saudação uma vez seu limite de tamanho de tamanhos atingir Olá blob (200GB), independentemente de se a opção `/SplitSize` tiver sido especificado pelo usuário hello.

### <a name="export-table-toojson-or-csv-data-file-format"></a>Exportar tabela tooJSON ou formato de arquivo de dados CSV
AzCopy por padrão exporta arquivos de dados de tooJSON de tabelas. Você pode especificar a opção de saudação `/PayloadFormat:JSON|CSV` tooexport tabelas de saudação como JSON ou CSV.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

Ao especificar o formato de carga CSV hello, AzCopy também irá gerar um arquivo de esquema com extensão de arquivo `.schema.csv` para cada arquivo de dados.

### <a name="export-table-entities-concurrently"></a>Exportar entidades de tabela simultaneamente

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy começará a entidades de tooexport operações simultâneas ao usuário Olá Especifica a opção `/PKRS`. Cada operação exporta um intervalor de chaves de partição.

Observe que o número de saudação de operações simultâneas também é controlado pela opção `/NC`. AzCopy usa o número de saudação de processadores de núcleo como valor padrão Olá `/NC` ao copiar entidades de tabela, mesmo se `/NC` não foi especificado. Quando o usuário Olá Especifica opção `/PKRS`, AzCopy usa Olá menor de saudação dois valores - partição intervalos de chaves versus operações simultâneas implicitamente ou explicitamente especificados - toodetermine Olá inúmeros toostart operações simultâneas. Para obter mais detalhes, digite `AzCopy /?:NC` na linha de comando hello.

### <a name="export-table-tooblob"></a>Exportar a tabela tooblob

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy irá gerar um arquivo de dados JSON no contêiner de blob Olá com a seguinte convenção de nomenclatura:

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

arquivo de dados JSON Olá gerado segue o formato de carga de saudação para metadados mínimos. Para obter detalhes sobre esse formado de carga, confira [Formato de carga para operações do serviço Tabela](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Observe que, ao exportar tabelas tooblobs, AzCopy será baixar arquivos de dados temporários Olá tabela entidades toolocal e, em seguida, carregar o blob de toohello essas entidades. Esses arquivos de dados temporários são colocados na pasta de arquivo de diário Olá com caminho de padrão de hello "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", você pode especificar a opção/z [pasta de arquivo diário] toochange Olá local de pasta do arquivo de diário e, portanto, alterar o local dos arquivos de dados temporários hello. tamanho dos arquivos é decidido por de suas entidades de tabela tamanho e Olá especificado com hello opção /SplitSize, embora o arquivo de dados temporário Olá no disco local será excluído imediatamente depois de ter sido os dados temporários Hello carregados toohello blob, certifique-se de ter toostore de espaço suficiente em disco local desses arquivos de dados temporários antes de serem excluídos.

## <a name="table-import"></a>Tabela: importar
### <a name="import-table"></a>Importar tabela

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

Olá opção `/EntityOperation` indica como entidades tooinsert em Olá tabela. Os valores possíveis são:

* `InsertOrSkip`: Ignora uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.
* `InsertOrMerge`: Mescla uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.
* `InsertOrReplace`: Substitui uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.

Observe que você não pode especificar a opção `/PKRS` no cenário de importação de saudação. Ao contrário do cenário de exportação hello, em que você deve especificar a opção `/PKRS` toostart as operações simultâneas, AzCopy por padrão iniciará operações simultâneas quando você importa uma tabela. número de operações simultâneas de Introdução do Hello padrão é toohello igual número de processadores de núcleo; No entanto, você pode especificar um número diferente de simultâneas com a opção `/NC`. Para obter mais detalhes, digite `AzCopy /?:NC` na linha de comando hello.

Observe que o AzCopy dá suporte apenas à importação para JSON, não para CSV. O AzCopy não dá suporte a importações de tabela de arquivos JSON e de manifesto criados pelo usuário. Ambos os arquivos devem vir de uma exportação de tabela AzCopy. erros de tooavoid, não modifique hello exportada JSON ou arquivo de manifesto.

### <a name="import-entities-tootable-using-blobs"></a>Importar entidades tootable usando blobs
Suponha que um contêiner de Blob contenha seguinte Olá: arquivo JSON de um que representa uma tabela do Azure e seu arquivo de manifesto que o acompanha.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

Você pode executar Olá entidades de tooimport de comando a seguir em uma tabela usando o arquivo de manifesto Olá desse contêiner de blob:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Outros recursos do AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Copiar somente os dados que não existem no destino de saudação
Olá `/XO` e `/XN` parâmetros permitem que os recursos de origem mais antiga ou mais recente de tooexclude que está sendo copiado, respectivamente. Se você desejar somente toocopy os recursos de origem que não existem no destino Olá, você pode especificar ambos os parâmetros em Olá AzCopy comando:

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Observe que isso não é suportado quando Olá origem ou destino é uma tabela.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>Usar parâmetros de linha de comando do arquivo toospecify uma resposta

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

É possível incluir qualquer parâmetro de linha de comando do AZCopy em um arquivo de resposta. AzCopy processos Olá parâmetros no arquivo hello como se eles tivessem sido especificados na linha de comando hello, executar uma substituição direta com o conteúdo de saudação do arquivo hello.

Suponha que um arquivo de resposta chamado `copyoperation.txt`, que contém Olá linhas a seguir. Cada parâmetro do AzCopy pode ser especificado em uma única linha

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

ou, em linhas separadas:

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy falhará se você dividir o parâmetro hello em duas linhas, conforme mostrado aqui para Olá `/sourcekey` parâmetro:

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>Usar vários parâmetros de linha de comando de toospecify resposta arquivos
Vamos supor um arquivo de resposta chamado `source.txt` que especifique um contêiner de origem:

    /Source:http://myaccount.blob.core.windows.net/mycontainer

E um arquivo de resposta chamado `dest.txt` que especifica uma pasta de destino no sistema de arquivos de saudação:

    /Dest:C:\myfolder

E um arquivo de resposta chamado `options.txt` que especifique opções para o AzCopy:

    /S /Y

toocall AzCopy com esses arquivos de resposta, que residem em um diretório `C:\responsefiles`, use este comando:

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy processa este comando exatamente como seria se você incluiu todos os parâmetros individuais na linha de comando Olá Olá:

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Especificar uma SAS

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

Você também pode especificar uma SAS no URI do contêiner hello:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Pasta de arquivo de diário
Cada vez que você emitir um comando tooAzCopy, ele verifica se um arquivo de diário existe na pasta padrão de hello, ou se ela existir em uma pasta que você especificou com esta opção. Se o arquivo de diário Olá não existir em qualquer lugar, AzCopy trata operação hello como novo e gera um novo arquivo de diário.

Se existir um arquivo de diário hello, o AzCopy verificará se Olá linha de comando que você inserir corresponde Olá a linha de comando no arquivo de diário hello. Se duas linhas de comando Olá corresponder, AzCopy reinicia a operação de incompleta de saudação. Se eles não coincidirem, você será solicitada tooeither substituir Olá diário arquivo toostart uma nova operação ou toocancel Olá atual operação.

Se desejar que o local do toouse saudação padrão para o arquivo de diário hello:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Se você omitir a opção `/Z`, ou especifique a opção `/Z` sem o caminho da pasta hello, como mostrado acima, AzCopy cria o arquivo de diário Olá no local padrão de saudação, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Se já existir um arquivo de diário Olá, AzCopy retoma operação Olá com base no arquivo de diário hello.

Se você desejar toospecify um local personalizado para o arquivo de diário hello:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

Este exemplo cria o arquivo de diário Olá se ele ainda não existir. Se ele existir, AzCopy retoma operação Olá com base no arquivo de diário hello.

Se você desejar tooresume uma operação AzCopy:

```azcopy
AzCopy /Z:C:\journalfolder\
```

Este exemplo retoma Olá última operação, que pode ter falhado toocomplete.

### <a name="generate-a-log-file"></a>Gerar um arquivo de log

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

Se você especificar a opção `/V` sem fornecer um log detalhado do toohello de caminho de arquivo, em seguida, AzCopy cria Olá arquivo de log no local padrão de saudação, que é `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

Caso contrário, você pode criar um arquivo de log em um local personalizado:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Observe que, se você especificar um caminho relativo a opção a seguir `/V`, como `/V:test/azcopy1.log`, log detalhado Olá será criado no diretório de trabalho atual hello dentro de uma subpasta chamada `test`.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Saudação de número de operações simultâneas toostart
Opção `/NC` Especifica o número de saudação de operações simultâneas de cópia. Por padrão, AzCopy inicia um determinado número de operações simultâneas tooincrease Olá transferência de transferência de dados. Para operações de tabela, o número de saudação de operações simultâneas é igual toohello número de processadores que você tem. Para operações de Blob e arquivo, número de saudação de operações simultâneas é ser igual 8 vezes Olá número de processadores que você tem. Se você estiver executando o AzCopy através de uma rede de baixa largura de banda, você pode especificar um número menor para /NC tooavoid falha causada por divisão dos recursos.

### <a name="run-azcopy-against-azure-storage-emulator"></a>Executar o AzCopy em um emulador de armazenamento do Azure
Você pode executar AzCopy em Olá [emulador de armazenamento do Azure](storage-use-emulator.md) para Blobs:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

e Tabelas:

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>Parâmetros do AzCopy
Veja abaixo uma descrição dos parâmetros do AzCopy. Você também pode digitar um dos comandos a seguir na linha de comando Olá para obter ajuda usando AzCopy de saudação:

* Para obter ajuda detalhada da linha de comando para o AzCopy: `AzCopy /?`
* Para obter ajuda detalhada para qualquer parâmetro do AzCopy: `AzCopy /?:SourceKey`
* Para obter exemplos da linha de comando: `AzCopy /?:Samples`

### <a name="sourcesource"></a>/Source:"origem"
Especifica os dados de origem de saudação da qual toocopy. origem de saudação pode ser um diretório de sistema de arquivos, um contêiner de blob, um diretório virtual de blob, um compartilhamento de arquivos de armazenamento, um diretório de arquivos de armazenamento ou uma tabela do Azure.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="destdestination"></a>/Dest: "destino"
Especifica a saudação toocopy de destino para. destino de saudação pode ser um diretório de sistema de arquivos, um contêiner de blob, um diretório virtual de blob, um compartilhamento de arquivos de armazenamento, um diretório de arquivos de armazenamento ou uma tabela do Azure.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="patternfile-pattern"></a>/Pattern:"padrão de arquivo"
Especifica um padrão de arquivo que indica qual toocopy de arquivos. comportamento de saudação do parâmetro de /Pattern Olá é determinado pelo local Olá Olá dos dados de origem e Olá presença da opção de modo recursivo hello. O modo recursivo é especificado pela opção /S.

Se a origem especificada Olá é um diretório no sistema de arquivos hello, caracteres curinga padrão está em vigor e padrão do arquivo de saudação fornecido é comparado com arquivos no diretório hello. Se opção que /s for especificado, em seguida, AzCopy também corresponder ao padrão de saudação especificado em relação a todos os arquivos em todas as subpastas abaixo do diretório de saudação.

Se a origem de saudação especificado é um contêiner de blob ou diretório virtual, curingas não são aplicados. Se a opção que /s for especificado, em seguida, AzCopy interpreta padrão de saudação de arquivo especificado como um prefixo de blob. Se a opção que /s não for especificado, em seguida, AzCopy faz a correspondência de padrão de arquivo hello com nomes de blob exato.

Se Olá especificado origem é um compartilhamento de arquivos do Azure e, em seguida, você deve especificar nome do arquivo exato Olá, (por exemplo, abc.txt) toocopy um único arquivo, ou especifique a opção /S toocopy todos os arquivos no hello compartilhamento recursivamente. Tentativa toospecify um padrão de arquivo e a opção /S juntos resultará em erro.

AzCopy usa a correspondência diferencia maiusculas de minúsculas quando Olá /Source é um contêiner de blob ou diretório virtual de blob e Olá de usa maiusculas de minúsculas correspondentes em todos os outros casos.

Olá padrão de arquivo padrão usado quando nenhum padrão de arquivo especificado é *.* para uma localização do sistema de arquivos, ou um prefixo vazio para uma localização de armazenamento do Azure. Não é possível especificar diversos padrões para os arquivos.

**Aplicável a:** Blobs, Arquivos

### <a name="destkeystorage-key"></a>/DestKey:"chave de armazenamento"
Especifica a chave de conta de armazenamento Olá para o recurso de destino hello.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="destsassas-token"></a>/DestSAS:"sas-token"
Especifica uma assinatura de acesso compartilhado (SAS) com permissões de leitura e gravação para o destino da saudação (se aplicável). Olá surround SAS com aspas duplas, como ele pode contém caracteres especiais de linha de comando.

Se o recurso de destino Olá é um contêiner de blob, compartilhamento de arquivo ou tabela, você pode especificar essa opção, seguida por um token SAS hello, ou você pode especificar Olá SAS como parte do contêiner de blob de destino hello, compartilhamento de arquivos ou URI da tabela, sem essa opção.

Se Olá origem e destino são ambos os blobs, o blob de destino Olá deve residir no hello mesmo conta de armazenamento como um blob de origem hello.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="sourcekeystorage-key"></a>/Sourcekey: "chave de armazenamento"
Especifica a chave de conta de armazenamento Olá para o recurso de fonte de saudação.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="sourcesassas-token"></a>/SourceSAS:"sas-token"
Especifica uma assinatura de acesso compartilhado com permissões de leitura e a lista de origem de saudação (se aplicável). Olá surround SAS com aspas duplas, como ele pode contém caracteres especiais de linha de comando.

Se o recurso de fonte de saudação é um contêiner de blob e uma chave, nem uma SAS é fornecida, o contêiner de blob hello serão lidos por meio do acesso anônimo.

Se a fonte de saudação é um compartilhamento de arquivo ou tabela, uma chave ou um SAS deve ser fornecido.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="s"></a>/S
Especifica o modo recursivo para operações de cópia. No modo recursivo, AzCopy copiar todos os blobs ou arquivos que correspondem a saudação padrão de arquivo especificado, incluindo aqueles em subpastas.

**Aplicável a:** Blobs, Arquivos

### <a name="blobtypeblock--page--append"></a>/BlobType:"bloco" | "página" | "anexo"
Especifica se o blob de destino Olá é um blob de bloco, um blob de página ou um blob de acréscimo. Essa opção só será possível quando você estiver carregando um blob. Caso contrário, um erro é gerado. Se o destino de saudação é um blob e essa opção não for especificada, por padrão, AzCopy cria um blob de bloco.

**Aplicável a:** Blobs

### <a name="checkmd5"></a>/CheckMD5
Calcula um hash MD5 para dados baixados e verifica se o hash MD5 Olá armazenados no blob hello ou hash Olá calculado corresponde a propriedade de Content-MD5 do arquivo. seleção de saudação MD5 é desativada por padrão, para que você deve especificar essa verificação de MD5 Olá opção tooperform durante o download de dados.

Observe que o armazenamento do Azure não garante que Olá hash MD5 armazenado para Olá blob ou arquivo é atualizado. Olá tooupdate de responsabilidade do cliente MD5 é sempre que Olá blob ou arquivo é modificado.

AzCopy sempre define Olá Content-MD5 propriedade um blob do Azure ou arquivo após carregá-lo toohello serviço.  

**Aplicável a:** Blobs, Arquivos

### <a name="snapshot"></a>/Snapshot
Indica se tootransfer instantâneos. Essa opção é válida somente quando a fonte de saudação for um blob.

Olá instantâneos de blob transferidos são renomeados neste formato: nome de blob (hora do instantâneo) .extension

Por padrão, os instantâneos não são copiados.

**Aplicável a:** Blobs

### <a name="vverbose-log-file"></a>/V: [arquivo de log detalhado]
Produz mensagens de status detalhadas em um arquivo de log.

Por padrão, o arquivo de log detalhado Olá é denominado AzCopyVerbose.log em `%LocalAppData%\Microsoft\Azure\AzCopy`. Se você especificar um local de arquivo existente para essa opção, log detalhado hello serão acrescentadas toothat arquivo.  

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="zjournal-file-folder"></a>/Z:[journal-file-folder]
Especifica uma pasta de arquivo de diário para retomar uma operação.

O AzCopy sempre dará suporte à retomada caso uma operação tenha sido interrompida.

Se essa opção não for especificada, ou ele é especificado sem um caminho de pasta, AzCopy irá criar o arquivo de diário Olá no local padrão de saudação, que é % LocalAppData%\Microsoft\Azure\AzCopy.

Cada vez que você emitir um comando tooAzCopy, ele verifica se um arquivo de diário existe na pasta padrão de hello, ou se ela existir em uma pasta que você especificou com esta opção. Se o arquivo de diário Olá não existir em qualquer lugar, AzCopy trata operação hello como novo e gera um novo arquivo de diário.

Se existir um arquivo de diário hello, o AzCopy verificará se Olá linha de comando que você inserir corresponde Olá a linha de comando no arquivo de diário hello. Se duas linhas de comando Olá corresponder, AzCopy reinicia a operação de incompleta de saudação. Se eles não coincidirem, você será solicitada tooeither substituir Olá diário arquivo toostart uma nova operação ou toocancel Olá atual operação.

arquivo de diário de saudação é excluído após a conclusão bem-sucedida da operação de saudação.

A retomada de uma operação de um arquivo de diário criado por uma versão anterior do AzCopy não é compatível.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="parameter-file"></a>/@: “arquivo de parâmetro”
Especifica um arquivo que contém parâmetros. AzCopy processos Olá parâmetros no arquivo hello como se eles tivessem sido especificados na linha de comando hello.

Em um arquivo de resposta, é possível especificar vários parâmetros em um único arquivo ou especificar cada parâmetro na própria linha. Um parâmetro individual não pode abranger várias linhas.

Arquivos de resposta podem incluir linhas de comentários que começam com hello # símbolo.

É possível especificar vários arquivos de resposta. No entanto, o AzCopy não permite arquivos de resposta aninhados.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="y"></a>/Y
Suprime todas as solicitações de confirmação do AzCopy.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="l"></a>/L
Especifica uma operação de listagem apenas. Nenhum dado é copiado.

AzCopy interpretará hello usando dessa opção como uma simulação de linha de comando Olá em execução sem essa opção /L e contagem de quantos objetos serão copiados, você pode especificar a opção /V no Olá a mesma hora toocheck quais objetos serão copiados em log detalhado hello.

comportamento de saudação dessa opção também é determinado pelo local Olá Olá dos dados de origem e a presença de Olá Olá recursiva modo opção /S e arquivo padrão da opção de /Pattern.

O AzCopy exige a permissão de LISTAGEM e de LEITURA deste local de origem ao usar essa opção.

**Aplicável a:** Blobs, Arquivos

### <a name="mt"></a>/MT
Define a hora da última modificação do arquivo baixado Olá toobe Olá mesmo como o blob de origem hello ou do arquivo.

**Aplicável a:** Blobs, Arquivos

### <a name="xn"></a>/XN
Exclui um recurso de origem mais novo. recurso de saudação não será copiado se hora da última modificação do código-fonte Olá Olá é hello igual ou mais recente do que o destino.

**Aplicável a:** Blobs, Arquivos

### <a name="xo"></a>/XO
Exclui um recurso de origem mais antigo. recurso Olá não será copiado se a hora da última modificação do código-fonte Olá Olá é hello mesmo ou mais antigo que o destino.

**Aplicável a:** Blobs, Arquivos

### <a name="a"></a>/A
Carrega somente os arquivos que têm o atributo de arquivo morto de saudação configurado.

**Aplicável a:** Blobs, Arquivos

### <a name="iarashcnetoi"></a>/IA:[RASHCNETOI]
Carrega somente os arquivos que têm algum Olá especificado de atributos.

Entre os atributos disponíveis estão:

* R = Arquivos somente leitura
* A = Arquivos prontos para arquivamento
* S = Arquivos de sistema
* H = Arquivos ocultos
* C = Arquivo compactado
* N = Arquivos normais
* E = Arquivos criptografados
* T = Arquivos temporários
* O = Arquivos offline
* I = Arquivos não indexados

**Aplicável a:** Blobs, Arquivos

### <a name="xarashcnetoi"></a>/XA:[RASHCNETOI]
Exclui os arquivos que têm algum Olá especificado conjunto de atributos.

Entre os atributos disponíveis estão:

* R = Arquivos somente leitura
* A = Arquivos prontos para arquivamento
* S = Arquivos de sistema
* H = Arquivos ocultos
* C = Arquivo compactado
* N = Arquivos normais
* E = Arquivos criptografados
* T = Arquivos temporários
* O = Arquivos offline
* I = Arquivos não indexados

**Aplicável a:** Blobs, Arquivos

### <a name="delimiterdelimiter"></a>/Delimiter: "delimitador"
Indica o caractere delimitador de saudação usado diretórios virtuais toodelimit em um nome de blob.

Por padrão, usa AzCopy / como o caractere delimitador de saudação. No entanto, o AzCopy dá suporte ao uso de qualquer caractere comum (como @, # ou %) como delimitador. Se você precisar tooinclude um desses caracteres especiais na linha de comando hello, inclua o nome do arquivo de saudação com aspas duplas.

Essa opção só é aplicável para o download de blobs.

**Aplicável a:** Blobs

### <a name="ncnumber-of-concurrent-operations"></a>/NC: "número-de-operações-simultâneas"
Especifica o número de saudação de operações simultâneas.

AzCopy por padrão inicia um determinado número de operações simultâneas tooincrease Olá transferência de transferência de dados. Observe que o grande número de operações simultâneas em um ambiente de baixa largura de banda pode sobrecarregar a conexão de rede de saudação e evitar operações de saudação de ser totalmente concluída. Limite operações simultâneas com base na largura de banda real de rede disponível.

limite superior de saudação para as operações simultâneas é 512.

**Aplicável a:** Blobs, Arquivos, Tabelas

### <a name="sourcetypeblob--table"></a>/SourceType:"Blob" | "Table"
Especifica que Olá `source` recurso é um blob disponível no ambiente de desenvolvimento local hello, em execução no emulador de armazenamento hello.

**Aplicável a:** Blobs, Tabelas

### <a name="desttypeblob--table"></a>/DestType:"Blob" | "Table"
Especifica que Olá `destination` recurso é um blob disponível no ambiente de desenvolvimento local hello, em execução no emulador de armazenamento hello.

**Aplicável a:** Blobs, Tabelas

### <a name="pkrskey1key2key3"></a>/PKRS: "chave1#chave2#chave3#..."
Divisões Olá tooenable de intervalo de chave de partição, exportação de dados de tabela em paralelo, o que aumenta a velocidade de Olá Olá da operação de exportação.

Se essa opção não for especificada, o AzCopy usa entidades de tabela tooexport de thread único. Por exemplo, se hello usuário Especifica /PKRS: "aa #bb" e, em seguida, AzCopy inicia três operações simultâneas.

Cada operação exporta um dos três intervalos de chaves de partição, como mostramos abaixo:

  [first-partition-key, aa)

  [aa, bb)

  [bb, last-partition-key]

**Aplicável a:** Tabelas

### <a name="splitsizefile-size"></a>/Splitsize: "tamanho do arquivo"
Especifica Olá arquivo exportado de dividir o tamanho em MB, Olá valor mínimo permitido é 32.

Se essa opção não for especificada, AzCopy será Exportar arquivo de toosingle de dados de tabela.

Se dados de tabela de saudação são exportado tooa blob e hello, tamanho do arquivo exportado atinge Olá limite de 200 GB para o tamanho do blob, AzCopy dividirá arquivo exportado do hello, mesmo se essa opção não for especificada.

**Aplicável a:** Tabelas

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"
Especifica o comportamento de importação de dados de tabela hello.

* InsertOrSkip - ignora uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.
* InsertOrMerge - mescla uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.
* InsertOrReplace - substitui uma entidade existente ou insere uma nova entidade se ele não existe na tabela de saudação.

**Aplicável a:** Tabelas

### <a name="manifestmanifest-file"></a>/Manifesto: "arquivo de manifesto"
Especifica o arquivo de manifesto Olá para tabela Olá exportar e importar a operação.

Essa opção é opcional durante a operação de exportação hello, AzCopy irá gerar um arquivo de manifesto com nome pré-definido se essa opção não for especificada.

Essa opção é necessária durante a operação de importação Olá para localizar os arquivos de dados de saudação.

**Aplicável a:** Tabelas

### <a name="synccopy"></a>/SyncCopy
Indica se toosynchronously copiar blobs ou arquivos entre dois pontos de extremidade de armazenamento do Azure.

O AzCopy por padrão usa cópia assíncrona no servidor. Especifique esse tooperform opção um síncrono copiar, que faz o download de blobs ou arquivos toolocal memória e, em seguida, carrega tooAzure armazenamento.

Você pode usar essa opção ao copiar arquivos no armazenamento de Blob no armazenamento de arquivo ou Blob storage tooFile armazenamento ou vice-versa.

**Aplicável a:** Blobs, Arquivos

### <a name="setcontenttypecontent-type"></a>/SetContentType:"content-type"
Especifica o tipo de conteúdo MIME Olá para blobs de destino ou arquivos.

Conjuntos de AzCopy Olá o tipo de conteúdo para um blob ou arquivo tooapplication/octet-stream por padrão. Você pode definir o tipo de conteúdo Olá para todos os blobs ou arquivos especificando explicitamente um valor para essa opção.

Se você especificar essa opção sem um valor, AzCopy definirá cada blob ou tipo de conteúdo do arquivo de acordo com tooits extensão de arquivo.

**Aplicável a:** Blobs, Arquivos

### <a name="payloadformatjson--csv"></a>/PayloadFormat:"JSON" | "CSV"
Especifica o formato de Olá Olá tabela exportada do arquivo de dados.

Se essa opção não for especificada, por padrão, o AzCopy exportará o arquivo de dados da tabela no formato JSON.

**Aplicável a:** Tabelas

## <a name="known-issues-and-best-practices"></a>Problemas Conhecidos e Práticas Recomendadas
### <a name="limit-concurrent-writes-while-copying-data"></a>Limite gravações simultâneas durante a cópia de dados
Quando você copia blobs ou arquivos com AzCopy, tenha em mente que outro aplicativo esteja modificando dados saudação enquanto você estiver copiando-lo. Se possível, certifique-se de que dados Olá que você está copiando não está sendo modificados durante a operação de cópia de saudação. Por exemplo, ao copiar um VHD associado a uma máquina virtual do Azure, certifique-se de que nenhum outro aplicativo no momento está escrevendo toohello VHD. Toodo uma boa maneira trata concedendo Olá recurso toobe copiado. Como alternativa, você pode criar um instantâneo de saudação VHD primeiro e copie instantâneo hello.

Se você não pode impedir que outros aplicativos gravando tooblobs ou arquivos enquanto eles estão sendo copiados, em seguida, tenha em mente que, pelo trabalho de Olá Olá tempo termina, hello recursos copiados não podem mais ter paridade completa com os recursos de origem hello.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Execute uma instância de AzCopy em um computador.
AzCopy é projetado toomaximize Olá utilização sua máquina recurso tooaccelerate Olá de transferência de dados, é recomendável executar apenas uma instância de AzCopy em um computador e especificar a opção Olá `/NC` se você precisar de operações simultâneas mais. Para obter mais detalhes, digite `AzCopy /?:NC` na linha de comando hello.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>Habilite algoritmos MD5 compatíveis com FIPS para o AzCopy quando você "Usar algoritmos compatíveis com FIPS para criptografia, hash e assinatura".
AzCopy por padrão usa Olá toocalculate da implementação .NET MD5 MD5 ao copiar objetos, mas há alguns requisitos de segurança que precisam de configuração FIPS MD5 compatível tooenable AzCopy.

Você pode criar um arquivo app.config `AzCopy.exe.config` com a propriedade `AzureStorageUseV1MD5` e reservá-lo com o AzCopy.exe.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Para a propriedade "AzureStorageUseV1MD5" • True - valor saudação padrão AzCopy usará implementação .NET MD5.
• False – o AzCopy usará o algoritmo MD5 compatível com FIPS.

Observe que os algoritmos compatíveis com FIPS estão desabilitados por padrão em seu computador com Windows. Digite secpol.msc na janela Executar e marque essa opção em Configuração de Segurança -> Segurança -> Políticas Locais > Opções de Segurança > Criptografia do Sistema: usar algoritmos compatíveis com FIPS para criptografia, hash e assinatura.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o armazenamento do Azure e AzCopy, consulte toohello recursos a seguir.

### <a name="azure-storage-documentation"></a>Documentação do Armazenamento do Azure:
* [Introdução tooAzure armazenamento](storage-introduction.md)
* [Como toouse armazenamento de BLOBs no .NET](storage-dotnet-how-to-use-blobs.md)
* [Como toouse armazenamento de arquivo do .NET](storage-dotnet-how-to-use-files.md)
* [Como toouse o armazenamento de tabela do .NET](storage-dotnet-how-to-use-tables.md)
* [Como toocreate, gerenciar ou excluir uma conta de armazenamento](storage-create-storage-account.md)
* [Transferir dados com o AzCopy no Linux](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Postagens de blog de armazenamento do Azure:
* [Apresentando a versão de visualização da biblioteca de movimentação de dados do armazenamento do Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Introducing synchronous copy and customized content type (AzCopy: introdução a cópia síncrona e tipo de conteúdo personalizado)](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support (AzCopy: anúncio de disponibilidade geral do AzCopy 3.0 mais versão de teste do AzCopy 4.0 com suporte para Tabela e Arquivo)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Optimized for Large-Scale Copy Scenarios (AzCopy: otimizado para cenários de cópia em larga escala)](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Support for read-access geo-redundant storage (AzCopy: suporte para o armazenamento com redundância geográfica com acesso de leitura)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: Transfer data with re-startable mode and SAS token (AzCopy: transferir dados com o modo reiniciável e token de SAS)](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: Using cross-account Copy Blob (AzCopy: usando blob de cópia em várias contas)](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Uploading/downloading files for Azure Blobs (AzCopy: Upload/download de arquivos para Blobs do Azure)](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

