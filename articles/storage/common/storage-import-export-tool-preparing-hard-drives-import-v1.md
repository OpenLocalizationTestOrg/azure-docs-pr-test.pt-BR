---
title: "unidades de disco rígido para uma importação/exportação do Azure aaaPreparing importar trabalho - v1 | Microsoft Docs"
description: "Saiba como tooprepare discos rígidos usando Olá WAImportExport v1 ferramenta toocreate um trabalho de importação para o serviço de importação/exportação do Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 1eb0c3c51e984e2869b5268254f468d4b43e9d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Preparando discos rígidos para um trabalho de importação
tooprepare um ou mais discos rígidos para um trabalho de importação, siga estas etapas:

-   Identificar Olá dados tooimport em Olá serviço Blob

-   Identificar os diretórios virtuais de destino e blobs no serviço Blob da saudação

-   Determinar quantas unidades você precisará

-   Copiar Olá dados tooeach os discos rígidos

 Para um fluxo de trabalho de exemplo, consulte [tooPrepare de fluxo de trabalho de exemplo, discos rígidos para um trabalho de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md).

## <a name="identify-hello-data-toobe-imported"></a>Identificar Olá toobe de dados importado
 Olá primeira etapa toocreating um trabalho de importação é toodetermine quais diretórios e arquivos que você vai tooimport. Isso pode ser uma lista de diretórios, uma lista de arquivos exclusivos ou uma combinação dos dois. Quando um diretório é incluído, todos os arquivos no diretório hello e seus subdiretórios farão parte do trabalho de importação de saudação.

> [!NOTE]
>  Como os subdiretórios são incluídos recursivamente quando um diretório pai é incluído, especifique o diretório de pai de Olá somente. Não especifique nenhum de seus subdiretórios.
>
>  Atualmente, Olá, ferramenta de importação/exportação do Microsoft Azure tem Olá limitação a seguir: se um diretório contiver mais dados do que um disco rígido pode conter, o diretório de saudação precisa toobe dividido em diretórios menores. Por exemplo, se um diretório contiver 2,5 TB de dados e Olá a capacidade do disco rígido é apenas de 2TB, é necessário o diretório de 2,5 TB Olá toobreak em diretórios menores. Essa limitação será corrigida em uma versão mais recente da ferramenta de saudação.

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>Identificar Olá locais de destino no serviço de blob Olá
 Para cada diretório ou arquivo que será importado, você precisa tooidentify um diretório virtual de destino ou blob em Olá serviço Blob do Azure. Você usará esses destinos como entradas toohello ferramenta de importação/exportação do Azure. Observe que os diretórios devem ser delimitados pelo caractere de barra invertida hello "/".

 Olá, a tabela a seguir mostra alguns exemplos de destinos de blob:

|Arquivo ou diretório de origem|Blob de destino ou diretório virtual|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.blob.core.windows.net/music|

## <a name="determine-how-many-drives-are-needed"></a>Determinar quantas unidades serão necessárias
 Em seguida, você precisa toodetermine:

-   número de saudação de discos rígidos necessários dados de saudação toostore.

-   diretórios de saudação e/ou arquivos independentes que serão copiado tooeach do disco rígido.

 Certifique-se de que você tem o número de saudação de discos rígidos, que você precisará toostore Olá dados que está transferindo.

## <a name="copy-data-tooyour-hard-drive"></a>Copie o disco rígido tooyour dados
 Esta seção descreve como toocall Olá toocopy ferramenta de importação/exportação do Azure tooone seus dados ou mais discos rígidos. Cada vez que você chamar Olá, ferramenta de importação/exportação do Azure, você cria um novo *copiar sessão*. Crie pelo menos uma sessão de cópia para cada unidade toowhich você copiar dados. em alguns casos, talvez seja necessário mais de um toocopy de sessão de cópia tudo de sua unidade de toosingle de dados. Veja alguns motivos pelos quais talvez você precise de várias sessões de cópia:

-   Você deve criar uma sessão de cópia separada para cada unidade na qual você copia.

-   Uma sessão de cópia pode copiar um único diretório ou unidade de toohello um único blob. Se você estiver copiando vários diretórios, vários blobs ou uma combinação de ambos, você precisará toocreate várias sessões de cópia.

-   Você pode especificar propriedades e metadados que serão definidos em blobs Olá importados como parte de um trabalho de importação. Propriedades de saudação ou metadados que você especificar para uma sessão de cópia aplicará blobs tooall especificados por essa sessão de cópia. Se você quiser toospecify propriedades ou metadados diferentes para alguns blobs, você precisará toocreate sessão de cópia de um separado. Consulte [definindo as propriedades e metadados durante o processo de importação de saudação](storage-import-export-tool-setting-properties-metadata-import-v1.md)para obter mais informações.

> [!NOTE]
>  Se você tiver vários computadores que atendem aos requisitos de saudação descritos em [Configurando Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup-v1.md), você pode copiar os discos rígidos toomultiple dados em paralelo executando uma instância da ferramenta em cada computador.

 Para cada disco rígido que você prepara com Olá, ferramenta de importação/exportação do Azure, a ferramenta de saudação criará um único arquivo de diário. Você precisará arquivos de diário de saudação de seu trabalho de importação unidades toocreate Olá todas. arquivo de diário Olá também pode ser usados tooresume preparação da unidade se Olá ferramenta for interrompida.

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>Sintaxe da Ferramenta de Importação/Exportação do Azure para um trabalho de importação
 unidades de tooprepare para um trabalho de importação, chame Olá ferramenta de importação/exportação do Azure com hello **PrepImport** comando. Quais parâmetros você incluir depende se isso for Olá primeira sessão de cópia ou uma sessão de cópia subsequentes.

 Olá, primeira sessão de cópia para uma unidade exige alguns parâmetros adicionais toospecify Olá chave conta de armazenamento; Letra de unidade de destino Olá; Se a unidade de saudação deve ser formatada; Se a unidade de saudação deve ser criptografada e nesse caso, Olá chave de BitLocker; e o diretório de log hello. Aqui está a sintaxe Olá para um toocopy de sessão de cópia inicial um diretório ou um único arquivo:

 **Primeiro copiar sessão toocopy um único diretório**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Primeiro copiar sessão toocopy um único arquivo**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 Em sessões de cópia subsequentes, não é necessário parâmetros iniciais do toospecify hello. Aqui é sintaxe Olá um toocopy de sessão de cópia subsequentes um diretório ou um único arquivo:

 **Sessões de cópia subsequentes toocopy um único diretório**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Sessões de cópia subsequentes toocopy um único arquivo**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Parâmetros para Olá primeiro copiar a sessão para um disco rígido
 Cada vez que executar arquivos de toocopy ferramenta de importação/exportação do Azure Olá toohello disco rígido, a ferramenta Olá cria uma sessão de cópia. Cada sessão de cópia copia um único diretório ou um único arquivo tooa disco rígido. estado de saudação de sessão de cópia de saudação é gravado toohello arquivo de diário. Se uma sessão de cópia for interrompida (por exemplo, devido a perda de energia do sistema tooa), ele poderá ser retomado executando a ferramenta Olá novamente e especificando o arquivo de diário Olá na linha de comando de saudação.

> [!WARNING]
>  Se você especificar Olá **/formato** parâmetro hello primeira sessão de cópia, Olá unidade será formatada e todos os dados na unidade hello serão apagados. Recomendamos o uso de unidades em branco apenas para a sessão de cópia.

 comando Olá usado para Olá a primeira sessão de cópia para cada unidade exige parâmetros diferentes comandos de saudação para sessões de cópia subsequentes. Olá tabela a seguir lista parâmetros adicionais de saudação que estão disponíveis para Olá primeira sessão de cópia:

|Parâmetro de linha de comando|Descrição|
|-----------------------------|-----------------|
|**/sk:**<StorageAccountKey\>|`Optional.`chave de conta de armazenamento Olá para dados de saudação do hello armazenamento conta toowhich será importado. Você deve incluir **/sk:**< StorageAccountKey\> ou **/csas:**< ContainerSas\> no comando hello.|
|**/csas:**<ContainerSas\>|`Optional`. contêiner de saudação conta de armazenamento SAS toouse tooimport dados toohello. Você deve incluir **/sk:**< StorageAccountKey\> ou **/csas:**< ContainerSas\> no comando hello.<br /><br /> valor Olá para este parâmetro deve começar com o nome do contêiner hello, seguido por um ponto de interrogação (?) e o token SAS hello. Por exemplo:<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> Olá permissões, se especificado na URL de saudação ou em uma política de acesso armazenada, devem incluir ler, gravam e excluir para trabalhos de importação e leitura, gravação e lista de trabalhos de exportação.<br /><br /> Quando esse parâmetro for especificado, todos os toobe blobs importados ou exportados deve estar dentro contêiner Olá especificado na assinatura de acesso compartilhado hello.|
|**/t:**<TargetDriveLetter\>|`Required.`Letra de unidade de saudação do disco rígido de destino Olá para sessão de cópia atual hello, sem saudação à direita de dois-pontos.|
|**/format**|`Optional.`Especifique esse parâmetro quando precisa de unidade Olá toobe formatado; Caso contrário, omiti-lo. Antes de ferramenta Olá formatos unidade hello, ele solicitará uma confirmação do console. toosuppress Olá confirmação, especifique o parâmetro /silentmode. de saudação.|
|**/silentmode**|`Optional.`Especifique essa confirmação de saudação do parâmetro toosuppress para formatar a unidade de destino hello.|
|**/encrypt**|`Optional.`Especifique esse parâmetro quando a unidade de saudação ainda não tiver sido criptografada com BitLocker e necessidades toobe criptografada pela ferramenta hello. Se a unidade de saudação já foi criptografada com BitLocker, omitir esse parâmetro e especifique Olá `/bk` parâmetro, fornecendo a chave de BitLocker existente hello.<br /><br /> Se você especificar Olá `/format` parâmetro, você também deve especificar Olá `/encrypt` parâmetro.|
|**/bk:**<BitLockerKey\>|`Optional.` Se `/encrypt` for especificado, omita este parâmetro. Se `/encrypt` for omitido, você precisa toohave já ter criptografado a unidade Olá com o BitLocker. Use esta chave de BitLocker do parâmetro toospecify hello. A criptografia do BitLocker é exigida em todos os discos rígidos para trabalhos de importação.|
|**/logdir:**<LogDirectory\>|`Optional.`diretório de log Olá Especifica que um diretório toobe usado logs detalhados toostore, bem como arquivos de manifesto temporários. Se não for especificado, diretório atual Olá será usado como diretório de log hello.|

### <a name="parameters-required-for-all-copy-sessions"></a>Parâmetros obrigatórios para todas as sessões de cópia
 arquivo de diário Olá contém o status de saudação para todas as sessões de cópia para um disco rígido. Ele também contém informações de saudação necessário Olá toocreate trabalho de importação. Você sempre deve especificar um arquivo de diário ao executar Olá, ferramenta de importação/exportação do Azure, bem como uma ID de sessão de cópia:

|||
|-|-|
|Parâmetro de linha de comando|Descrição|
|**/j:**<JournalFile\>|`Required.`arquivo de diário do Hello caminho toohello. Cada unidade deve ter exatamente um arquivo de diário. Observe que esse arquivo de diário Olá não deve residir na unidade de destino hello. extensão de arquivo de diário Olá é `.jrn`.|
|**/id:**<SessionId\>|`Required.`ID da sessão Olá identifica uma sessão de cópia. É usado tooensure de recuperação precisa de uma sessão de cópia interrompida. Arquivos que são copiados em uma sessão de cópia são armazenados em um diretório chamado após Olá ID da sessão na unidade de destino hello.|

### <a name="parameters-for-copying-a-single-directory"></a>Parâmetros para copiar um único diretório
 Ao copiar um único diretório, seguinte Olá necessárias e os parâmetros opcionais se aplicam:

|Parâmetro de linha de comando|Descrição|
|----------------------------|-----------------|
|**/srcdir:**<SourceDirectory\>|`Required.`diretório de origem de saudação que contém arquivos toobe copiados toohello unidade de destino. caminho do diretório Olá deve ser um caminho absoluto (não um caminho relativo).|
|**/dstdir:**<DestinationBlobVirtualDirectory\>|`Required.`Olá caminho toohello diretório virtual de destino em sua conta de armazenamento do Windows Azure. diretório virtual Olá pode ou não existir.<br /><br /> Você pode especificar um contêiner ou um prefixo de blob como `music/70s/`. Olá diretório de destino deve começar com o nome do contêiner de hello, seguido por uma barra "/" e pode incluir opcionalmente um diretório virtual de blob que termina com "/".<br /><br /> Quando o contêiner de destino Olá é contêiner raiz de saudação, você deve especificar explicitamente contêiner raiz de hello, incluindo a barra hello, como `$root/`. Como blobs no contêiner raiz de saudação não podem incluir "/" em seus nomes, os subdiretórios no diretório de origem de saudação não serão copiados quando o diretório de destino de saudação é o contêiner raiz de saudação.<br /><br /> Ser toouse-se de que os nomes de contêiner válido ao especificar diretórios virtuais de destino ou blobs. Tenha em mente que os nomes de contêiner devem estar em minúsculas. Para conhecer as regras de nomenclatura de contêineres, consulte [Nomenclatura e referência de contêineres, blobs e metadados](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).|
|**/Disposition:**<rename&#124;no-overwrite&#124;overwrite>|`Optional.`Especifica o comportamento de saudação quando um blob com hello especificado já existe um endereço. Os valores válidos para este parâmetro são: `rename`, `no-overwrite` e `overwrite`. Observe que esses valores diferenciam maiúsculas de minúsculas. Se nenhum valor for especificado, o padrão de saudação é `rename`.<br /><br /> Olá valor especificado para esse parâmetro afeta todos os arquivos de saudação no diretório de saudação especificado por Olá `/srcdir` parâmetro.|
|**/BlobType:**<BlockBlob&#124;PageBlob>|`Optional.`Especifica o tipo de blob de saudação para blobs de destino hello. Os valores válidos são: `BlockBlob` e `PageBlob`. Observe que esses valores diferenciam maiúsculas de minúsculas. Se nenhum valor for especificado, o padrão de saudação é `BlockBlob`.<br /><br /> Na maioria dos casos, `BlockBlob` é recomendado. Se você especificar `PageBlob`, comprimento de saudação de cada arquivo no diretório Olá deve ser um múltiplo de 512, tamanho de saudação de uma página para blobs de página.|
|**/PropertyFile:**<PropertyFile\>|`Optional.`Arquivo de propriedade caminho toohello para blobs de destino hello. Confira [Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação](../storage-import-export-file-format-metadata-and-properties.md) para saber mais.|
|**/MetadataFile:**<MetadataFile\>|`Optional.`Arquivo de metadados de toohello de caminho para blobs de destino hello. Confira [Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação](../storage-import-export-file-format-metadata-and-properties.md) para saber mais.|

### <a name="parameters-for-copying-a-single-file"></a>Parâmetros para copiar um único arquivo
 Ao copiar um único arquivo, hello parâmetros obrigatórios e opcionais a seguir se aplicam:

|Parâmetro de linha de comando|Descrição|
|----------------------------|-----------------|
|**/srcfile:**<SourceFile\>|`Required.`Olá caminho completo toohello arquivo toobe copiado. caminho do diretório Olá deve ser um caminho absoluto (não um caminho relativo).|
|**/dstblob:**<DestinationBlobPath\>|`Required.`Olá caminho toohello blob de destino em sua conta de armazenamento do Windows Azure. blob Olá pode ou não existir.<br /><br /> Especifique nome que começa Olá blob com o nome do contêiner de saudação. nome do blob Olá não pode começar com "/" ou o nome de conta de armazenamento hello. Para conhecer as regras de nomenclatura de blobs, consulte [Nomenclatura e referência de contêineres, blobs e metadados](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).<br /><br /> Quando o contêiner de destino Olá é contêiner raiz de saudação, você deve especificar explicitamente `$root` como Olá contêiner, como `$root/sample.txt`. Observe que os blobs no contêiner raiz de saudação não pode incluir "/" em seus nomes.|
|**/Disposition:**<rename&#124;no-overwrite&#124;overwrite>|`Optional.`Especifica o comportamento de saudação quando um blob com hello especificado já existe um endereço. Os valores válidos para este parâmetro são: `rename`, `no-overwrite` e `overwrite`. Observe que esses valores diferenciam maiúsculas de minúsculas. Se nenhum valor for especificado, o padrão de saudação é `rename`.|
|**/BlobType:**<BlockBlob&#124;PageBlob>|`Optional.`Especifica o tipo de blob de saudação para blobs de destino hello. Os valores válidos são: `BlockBlob` e `PageBlob`. Observe que esses valores diferenciam maiúsculas de minúsculas. Se nenhum valor for especificado, o padrão de saudação é `BlockBlob`.<br /><br /> Na maioria dos casos, `BlockBlob` é recomendado. Se você especificar `PageBlob`, comprimento de saudação de cada arquivo no diretório Olá deve ser um múltiplo de 512, tamanho de saudação de uma página para blobs de página.|
|**/PropertyFile:**<PropertyFile\>|`Optional.`Arquivo de propriedade caminho toohello para blobs de destino hello. Confira [Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação](../storage-import-export-file-format-metadata-and-properties.md) para saber mais.|
|**/MetadataFile:**<MetadataFile\>|`Optional.`Arquivo de metadados de toohello de caminho para blobs de destino hello. Confira [Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação](../storage-import-export-file-format-metadata-and-properties.md) para saber mais.|

### <a name="resuming-an-interrupted-copy-session"></a>Retomando uma sessão de cópia interrompida
 Se uma sessão de cópia for interrompida por qualquer motivo, você poderá retomá-la executando a ferramenta de saudação com apenas Olá arquivo de diário especificado:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 Apenas hello mais recente sessão de cópia, se for finalizada de maneira anormal, poderá ser retomada.

> [!IMPORTANT]
>  Quando você retomar uma sessão de cópia, não modifique diretórios e arquivos de dados de origem Olá adicionando ou removendo arquivos.

### <a name="aborting-an-interrupted-copy-session"></a>Anulando uma sessão de cópia interrompida
 Se uma sessão de cópia for interrompida e não é possível tooresume (por exemplo, se um diretório de origem ficar inacessível), você deverá abortar Olá sessão atual para que ela pode ser revertida volta e novas sessões de cópia podem ser iniciadas:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 Olá somente última sessão de cópia, se for finalizada de maneira anormal, poderá ser abortada. Observe que você não é possível anular Olá a primeira sessão de cópia para uma unidade. Em vez disso, você deve reiniciar a sessão de cópia de saudação com um novo arquivo de diário.

## <a name="next-steps"></a>Próximas etapas

* [Configurando Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup-v1.md)
* [Processo de importação de definição de propriedades e metadados durante a saudação](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [Referência rápida para comandos usados frequentemente](storage-import-export-tool-quick-reference-v1.md) 
* [Revisão do status do trabalho com arquivos de log de cópia](storage-import-export-tool-reviewing-job-status-v1.md)
* [Reparação de um trabalho de importação](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Reparação de um trabalho de exportação](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Olá, ferramenta de importação/exportação do Azure de solução de problemas](storage-import-export-tool-troubleshooting-v1.md)
