---
title: "trabalho de importação de unidades de disco rígido para uma importação/exportação do Azure aaaPreparing | Microsoft Docs"
description: "Saiba como tooprepare discos rígidos usando Olá WAImportExport ferramenta toocreate um trabalho de importação para Olá serviço de importação/exportação do Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: 3f247a9efee29da2d18140353edc9dd7103a0761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Preparação de discos rígidos para um trabalho de importação

Olá ferramenta WAImportExport é preparação da unidade hello e ferramenta de reparo que você pode usar com hello [serviço de importação/exportação do Microsoft Azure](storage-import-export-service.md). Você pode usar essa ferramenta toocopy dados toohello discos rígidos que você vai tooship tooan datacenter do Azure. Depois que um trabalho de importação for concluída, você pode usar essa ferramenta toorepair todos os blobs que foram corrompidos, estavam ausentes ou está em conflito com outros blobs. Depois de receber Olá unidades de um trabalho de exportação concluído, você pode usar essa ferramenta toorepair todos os arquivos que foram corrompidos ou ausentes em unidades de saudação. Neste artigo, vamos sobre o uso de saudação dessa ferramenta.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="requirements-for-waimportexportexe"></a>Requisitos de WAImportExport.exe

- **Configuração da máquina**
  - Windows 7, Windows Server 2008 R2 ou um sistema operacional Windows mais recente
  - O .NET Framework 4 deve estar instalado. Consulte [perguntas frequentes sobre](#faq) sobre como toocheck se o .net Framework está instalado na máquina de saudação.
- **Chave de conta de armazenamento** -é necessário pelo menos uma das chaves de conta Olá Olá conta de armazenamento.

### <a name="preparing-disk-for-import-job"></a>Preparação do disco para o trabalho de importação

- **BitLocker -** BitLocker deve ser habilitado na ferramenta Olá máquina executa Olá WAImportExport. Consulte Olá [perguntas frequentes sobre](#faq) como tooenable BitLocker.
- **Discos** acessíveis do computador no qual a ferramenta WAImportExport é executada. Confira nas [Perguntas frequentes](#faq) a especificação do disco.
- **Arquivos de origem** -arquivos de saudação planejar tooimport devem estar acessíveis do computador de cópia hello, independentemente de estarem em um compartilhamento de rede ou um disco rígido local.

### <a name="repairing-a-partially-failed-import-job"></a>Reparação de um trabalho de importação com falha parcial

- **Copie o arquivo de log** gerado quando o serviço de Importação/Exportação do Azure copia dados entre a Conta de Armazenamento e o Disco. Eles estão localizados em sua conta de armazenamento de destino.

### <a name="repairing-a-partially-failed-export-job"></a>Reparação de um trabalho de exportação com falha parcial

- **Copie o arquivo de log** gerado quando o serviço de Importação/Exportação do Azure copia dados entre a Conta de Armazenamento e o Disco. Ele está localizado em sua conta de armazenamento de origem.
- **Arquivo de manifesto** -[opcional] localizado na unidade exportada retornada pela Microsoft.

## <a name="download-and-install-waimportexport"></a>Baixar e instalar a WAImportExport

Baixar Olá [versão mais recente do WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280). Extraia o diretório de tooa conteúdo compactado Olá no seu computador.

A próxima tarefa é toocreate os arquivos CSV.

## <a name="prepare-hello-dataset-csv-file"></a>Preparar o arquivo CSV Olá conjunto de dados

### <a name="what-is-dataset-csv"></a>O que é o CSV de conjunto de dados

Arquivo CSV de DataSet é o valor de saudação do sinalizador de /conjunto de dados é um arquivo CSV que contém uma lista de diretórios e/ou uma lista de arquivos copiado de toobe tootarget unidades. Olá primeira etapa toocreating um trabalho de importação é toodetermine quais diretórios e arquivos que você vai tooimport. Isso pode ser uma lista de diretórios, uma lista de arquivos exclusivos ou uma combinação dos dois. Quando um diretório é incluído, todos os arquivos no diretório hello e seus subdiretórios farão parte do trabalho de importação de saudação.

Para cada toobe de diretório ou arquivo importado, você deve identificar um diretório virtual de destino ou blob no hello serviço Blob do Azure. Você usará esses destinos como ferramenta de WAImportExport toohello entradas. Diretórios devem ser delimitados pelo caractere de barra invertida hello "/".

Olá, a tabela a seguir mostra alguns exemplos de destinos de blob:

| Arquivo ou diretório de origem | Blob de destino ou diretório virtual |
| --- | --- |
| H:\Video | https://mystorageaccount.blob.core.windows.net/video |
| H:\Photo | https://mystorageaccount.blob.core.windows.net/photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.blob.core.windows.net/music |

### <a name="sample-datasetcsv"></a>Exemplo de dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>Campos do arquivo CSV de conjunto de dados

| Campo | Descrição |
| --- | --- |
| BasePath | **[Obrigatório]**<br/>valor desse parâmetro Hello representa a fonte de saudação onde se encontra Olá toobe de dados importado. ferramenta de saudação irá copiar recursivamente todos os dados localizados nesse caminho.<br><br/>**Valores permitidos**: isso tem toobe um caminho válido no computador local ou um caminho de compartilhamento válido e deve ser acessível por usuário hello. caminho do diretório Olá deve ser um caminho absoluto (não um caminho relativo). Se o caminho de saudação termina com "\\", representa um caminho terminando sem um diretório else"\\" representa um arquivo.<br/>Nenhuma regex é permitido neste campo. Se Olá caminho contiver espaços, coloque-a "".<br><br/>**Exemplo**: "c:\Directory\c\Directory\File.txt"<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[Obrigatório]**<br/> Olá caminho toohello diretório virtual de destino em sua conta de armazenamento do Windows Azure. diretório virtual Olá pode ou não existir. Se não existir, o serviço de Importação/Exportação criará um.<br/><br/>Ser toouse-se de que os nomes de contêiner válido ao especificar diretórios virtuais de destino ou blobs. Tenha em mente que os nomes de contêiner devem estar em minúsculas. Para conhecer as regras de nomenclatura de contêineres, consulte [Nomenclatura e referência de contêineres, blobs e metadados](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata). Se apenas a raiz é especificada, a estrutura de diretórios de Olá da fonte de saudação é replicada no contêiner de blob de destino hello. Se desejar que uma estrutura de diretórios diferentes Olá um na origem, várias linhas de mapeamento em CSV<br/><br/>Você pode especificar um contêiner ou um prefixo de blob como music/70s/. Olá diretório de destino deve começar com o nome do contêiner de hello, seguido por uma barra "/" e pode incluir opcionalmente um diretório virtual de blob que termina com "/".<br/><br/>Quando o contêiner de destino Olá é contêiner raiz de saudação, você deve especificar explicitamente contêiner raiz de hello, incluindo Olá barra invertida, como $root /. Como blobs no contêiner raiz de saudação não podem incluir "/" em seus nomes, os subdiretórios no diretório de origem de saudação não serão copiados quando o diretório de destino de saudação é o contêiner raiz de saudação.<br/><br/>**Exemplo**<br/>Se o caminho de blob de destino de saudação é https://mystorageaccount.blob.core.windows.net/video, o valor de saudação do campo pode ser vídeo /  |
| BlobType | **[Opcional]** block &#124; page<br/>Atualmente, o serviço de Importação/Exportação oferece suporte dois tipos de Blobs. Blobs de página e Blobs de bloco. Por padrão, todos os arquivos serão importados como Blobs de blocos. E \*. vhd e \*. vhdx será importado como Page BlobsThere é um limite de blob de blocos hello e o tamanho permitido do blob de página. Confira [Metas de escalabilidade do armazenamento](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files) para saber mais.  |
| Disposition | **[Opcional]** rename &#124; no-overwrite &#124; overwrite <br/> Este campo especifica o comportamento de cópia Olá durante ou importação seja Quando os dados estão sendo carregados toohello conta de armazenamento do disco de saudação. Opções disponíveis são: Renomear &#124; Substituir &#124; não-substituir. Padrões muito "Renomear" se nada for especificado. <br/><br/>**Rename**: se um objeto com o mesmo nome estiver presente, isso cria uma cópia no destino.<br/>Substituir: substitui o arquivo hello com arquivo mais recente. arquivo Hello com wins última modificação.<br/>**Substituir não**: ignora a gravação da saudação do arquivo se estiver presente.|
| MetadataFile | **[Opcional]** <br/>campo de toothis Olá valor é o arquivo de metadados de saudação que pode ser fornecido se precisar de saudação um toopreserve Olá metadados de objetos de saudação ou fornecer metadados personalizados. Arquivo de metadados de toohello de caminho para blobs de destino hello. Confira [Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação](storage-import-export-file-format-metadata-and-properties.md) para saber mais |
| PropertiesFile | **[Opcional]** <br/>Arquivo de propriedade caminho toohello para blobs de destino hello. Confira [Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação](storage-import-export-file-format-metadata-and-properties.md) para saber mais. |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>Preparar o arquivo CSV AdditionalDriveSet ou InitialDriveSet

### <a name="what-is-driveset-csv"></a>O que é o CSV driveset

Olá, valor do sinalizador de saudação /InitialDriveSet ou /AdditionalDriveSet é um arquivo CSV que contém a lista Olá de discos toowhich letras de unidade de saudação são mapeadas para que hello ferramenta pode corretamente lista de seleção Olá de discos toobe preparado. Se o tamanho dos dados Olá é maior do que um tamanho de disco único, ferramenta WAImportExport de saudação distribuirá dados saudação em vários discos inscritos nesse arquivo CSV de forma otimizada.

Não há nenhum limite no número de saudação de dados de saudação de discos pode ser gravado tooin uma única sessão. ferramenta de saudação distribui dados com base no tamanho do disco e tamanho da pasta. Ele selecionará disco hello mais otimizado para saudação do tamanho do objeto. Olá dados quando carregado toohello conta de armazenamento será convergida toohello back estrutura de diretório que foi especificada no arquivo de conjunto de dados. Em ordem toocreate um driveset CSV, siga as etapas de saudação abaixo.

### <a name="create-basic-volume-and-assign-drive-letter"></a>Criar um volume básico e atribuir uma letra de unidade

Em ordem toocreate um volume básico e atribuir uma letra de unidade, seguindo as instruções de hello "Mais simples partição para a criação de" fornecido no [visão geral do gerenciamento de disco](https://technet.microsoft.com/library/cc754936.aspx).

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>Exemplo de arquivo CSV InitialDriveSet e AdditionalDriveSet

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>Campos do arquivo CSV driveset

| Campos | Valor |
| --- | --- |
| DriveLetter | **[Obrigatório]**<br/> Cada unidade que está sendo fornecida toohello ferramenta como destino Olá precisa ter um volume NTFS simples nela e uma letra de unidade atribuída tooit.<br/> <br/>**Exemplo**: R ou r |
| FormatOption | **[Obrigatório]** Format &#124; AlreadyFormatted<br/><br/> **Formato**: especificar isso formatará a todos os dados de saudação em disco hello. <br/>**AlreadyFormatted**: ferramenta de saudação ignorará a formatação quando esse valor é especificado. |
| SilentOrPromptOnFormat | **[Obrigatório]** SilentMode &#124; PromptOnFormat<br/><br/>**SilentMode**: fornecer esse valor permitirá a ferramenta de saudação do usuário toorun no modo silencioso. <br/>**PromptOnFormat**: ferramenta Olá solicitará Olá usuário tooconfirm se Olá ação destina-se realmente em cada formato.<br/><br/>Se não for definido, o comando será anulado e exibirá a mensagem de erro: "Valor incorreto para SilentOrPromptOnFormat: nenhum" |
| Criptografia | **[Obrigatório]** Encrypt &#124; AlreadyEncrypted<br/> valor de saudação do campo decide qual tooencrypt de disco e que não a. <br/><br/>**Criptografar**: ferramenta formatará a unidade de saudação. Se o valor do campo "FormatOption" for "Formato", em seguida, esse valor é necessário toobe "Criptografar". Se "AlreadyEncrypted" for especificado, o resultado será um erro "Quando Format for especificado, Encrypt também deverá ser especificado".<br/>**AlreadyEncrypted**: ferramenta descriptografar unidade hello usando Olá BitLockerKey fornecido no campo "ExistingBitLockerKey". Se o valor do campo "FormatOption" for "AlreadyFormatted", esse valor poderá ser "Encrypt" ou "AlreadyEncrypted" |
| ExistingBitLockerKey | **[Obrigatório]**  Se o valor do campo "Encryption" for "AlreadyEncrypted"<br/> valor de saudação do campo é chave do BitLocker Olá que está associado ao disco determinado hello. <br/><br/>Este campo deve ser deixado em branco se o valor de saudação do campo "Criptografia" é "Criptografar".  Se o BitLocker Key for especificada nesse caso, o resultado será um erro "A Chave do Bitlocker não deve ser especificada".<br/>  **Exemplo**: 060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>Preparação do disco para o trabalho de importação

tooprepare unidades para um trabalho de importação, chame a ferramenta WAImportExport Olá Olá **PrepImport** comando. Quais parâmetros você incluir depende se isso for Olá primeira sessão de cópia ou uma sessão de cópia subsequentes.

### <a name="first-session"></a>Primeira sessão

Primeira sessão de cópia tooCopy uma ferramenta de WAImportExport de disco (dependendo do que é especificado no arquivo CSV) de várias Single/Multiple Directory tooa comando PrepImport para Olá primeiro copiar diretórios toocopy de sessão e/ou arquivos com uma nova sessão de cópia:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>Adicionar dados em uma sessão subsequente

Em sessões de cópia subsequentes, não é necessário parâmetros iniciais do toospecify hello. Você precisa toouse Olá mesmo arquivo de diário para que Olá ferramenta tooremember onde ele deixado no hello sessão anterior. estado de saudação de sessão de cópia de saudação é gravado toohello arquivo de diário. Esta é a sintaxe Olá para uma cópia subsequente diretórios adicionais de toocopy de sessão e/ou arquivos:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>Adicionar unidades toolatest sessão

Se dados saudação não se ajustou em unidades especificadas em InitialDriveset, você pode usar o hello ferramenta tooadd unidades adicionais toosame a sessão de cópia. 

>[!NOTE] 
>id da sessão Olá deve corresponder a id de sessão anterior de saudação. Arquivo de diário deve corresponder Olá especificada na sessão anterior.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Anule Olá sessão mais recente:

Se uma sessão de cópia for interrompida e não é possível tooresume (por exemplo, se um diretório de origem ficar inacessível), você deverá abortar Olá sessão atual para que ela pode ser revertida volta e novas sessões de cópia podem ser iniciadas:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Olá somente última sessão de cópia, se for finalizada de maneira anormal, poderá ser abortada. Observe que você não é possível anular Olá a primeira sessão de cópia para uma unidade. Em vez disso, você deve reiniciar a sessão de cópia de saudação com um novo arquivo de diário.

### <a name="resume-a-latest-interrupted-session"></a>Retomar a sessão interrompida mais recente

Se uma sessão de cópia for interrompida por qualquer motivo, você poderá retomá-la executando a ferramenta de saudação com apenas Olá arquivo de diário especificado:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**Exemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> Quando você retomar uma sessão de cópia, não modifique diretórios e arquivos de dados de origem Olá adicionando ou removendo arquivos.

## <a name="waimportexport-parameters"></a>Parâmetros de WAImportExport

| parâmetros | Descrição |
| --- | --- |
|     /j:&lt;JournalFile&gt;  | **Obrigatório**<br/> Arquivo de diário de toohello de caminho. Um arquivo de diário rastreia um conjunto de unidades e registros Olá andamento preparar essas unidades. arquivo de diário Olá sempre deve ser especificado.  |
|     /logdir:&lt;LogDirectory&gt;  | **Opcional**. diretório de log Hello.<br/> Arquivos de log detalhados, bem como alguns arquivos temporários serão gravados toothis directory. Se não for especificado, o atual diretório será usado como diretório de log hello. Olá diretório de log pode ser especificado somente uma vez para Olá mesmo arquivo de diário.  |
|     /id:&lt;SessionId&gt;  | **Obrigatório**<br/> Olá identificação de sessão usado tooidentify uma sessão de cópia. É usado tooensure de recuperação precisa de uma sessão de cópia interrompida.  |
|     /ResumeSession  | Opcional. Se Olá última sessão de cópia foi finalizada de maneira anormal, esse parâmetro pode ser especificado tooresume Olá sessão.   |
|     /AbortSession  | Opcional. Se Olá última sessão de cópia foi finalizada de maneira anormal, esse parâmetro pode ser especificado tooabort Olá sessão.  |
|     /sn:&lt;StorageAccountName&gt;  | **Obrigatório**<br/> Aplicável somente para RepairImport e RepairExport. nome de Olá Olá da conta de armazenamento.  |
|     /sk:&lt;StorageAccountKey&gt;  | **Obrigatório**<br/> chave Olá Olá da conta de armazenamento. |
|     /InitialDriveSet:&lt;driveset.csv&gt;  | **Necessário** ao executar Olá primeira sessão de cópia<br/> Um arquivo CSV que contém uma lista de unidades tooprepare.  |
|     /AdditionalDriveSet:&lt;driveset.csv&gt; | **Obrigatório**. Ao adicionar a sessão de cópia de toocurrent unidades. <br/> Um arquivo CSV que contém uma lista de unidades adicionais toobe adicionado.  |
|      /r:&lt;RepairFile&gt; | **Obrigatório** Aplicável somente para RepairImport e RepairExport.<br/> Caminho toohello arquivo para controlar o progresso do reparo. Cada unidade deve ter um, e somente um, arquivo de reparo.  |
|     /d:&lt;TargetDirectories&gt; | **Obrigatório**. Aplicável somente para RepairImport e RepairExport. Para RepairImport, toorepair de um ou mais diretórios separados por ponto e vírgula; Para RepairExport, um diretório toorepair, por exemplo, raiz de diretório da unidade de saudação.  |
|     /CopyLogFile:&lt;DriveCopyLogFile&gt; | **Obrigatório** Aplicável somente para RepairImport e RepairExport. Arquivo de log de cópia de unidade do caminho toohello (detalhado ou erro).  |
|     /ManifestFile:&lt;DriveManifestFile&gt; | **Obrigatório** Aplicável somente para RepairExport.<br/> Caminho toohello unidade arquivo de manifesto.  |
|     /PathMapFile:&lt;DrivePathMapFile&gt; | **Opcional**. Aplicável somente para RepairImport.<br/> Toohello de caminho do arquivo que contém mapeamentos de arquivo caminhos relativos toohello unidade raiz toolocations dos arquivos reais (delimitado por tabulação). Quando for especificado pela primeira vez, ele será preenchido com caminhos de arquivo com destinos vazios, o que significa que não será encontrado em TargetDirectories, terá o acesso negado, nome inválido ou existirá em vários diretórios. arquivo de mapa de caminho Olá pode ser editada manualmente tooinclude caminhos de destino correto hello e especificado novamente para caminhos de arquivo hello ferramenta tooresolve Olá corretamente.  |
|     /ExportBlobListFile:&lt;ExportBlobListFile&gt; | **Obrigatório**. Aplicável somente para PreviewExport.<br/> Toohello caminho XML arquivo contendo a lista de caminhos de blob ou prefixos de caminho para Olá blobs toobe exportados de blob. formato de arquivo Olá Olá mesmo como formato de blob de lista Olá blob em Olá operação Put Job da API REST do serviço de importação/exportação hello.  |
|     /DriveSize:&lt;DriveSize&gt; | **Obrigatório**. Aplicável somente para PreviewExport.<br/>  Tamanho de unidades toobe usado para exportação. Por exemplo, 500 GB, 1,5 TB. Observação: 1 GB = 1.000.000.000 bytes1 TB = 1.000.000.000.000 bytes  |
|     /DataSet:&lt;dataset.csv&gt; | **Obrigatório**<br/> Um arquivo CSV que contém uma lista de diretórios e/ou uma lista de arquivos toobe copiados tootarget unidades.  |
|     /silentmode  | **Opcional**.<br/> Se não for especificado, ele lembrará Olá requisito de unidades e precisa toocontinue sua confirmação.  |

## <a name="tool-output"></a>Saída da ferramenta

### <a name="sample-drive-manifest-file"></a>Exemplo de arquivo de manifesto da unidade

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>Exemplo de arquivo de diário (XML) para cada unidade

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>Arquivo de diário de exemplo (JRN) para a sessão que registra a trilha de saudação de sessões

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>Perguntas frequentes

### <a name="general"></a>Geral

#### <a name="what-is-waimportexport-tool"></a>O que é a ferramenta WAImportExport?

ferramenta de WAImportExport Olá é preparação da unidade hello e a ferramenta de reparo que você pode usar com hello serviço de importação/exportação do Microsoft Azure. Você pode usar essa ferramenta toocopy dados toohello discos rígidos que você vai tooship tooan data center do Azure. Depois que um trabalho de importação for concluída, você pode usar essa ferramenta toorepair todos os blobs que foram corrompidos, estavam ausentes ou está em conflito com outros blobs. Depois de receber Olá unidades de um trabalho de exportação concluído, você pode usar essa ferramenta toorepair todos os arquivos que foram corrompidos ou ausentes em unidades de saudação.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>Como faz Olá ferramenta WAImportExport funciona em vários discos e diretório fonte?

Se o tamanho dos dados Olá for maior que o tamanho do disco Olá, ferramenta WAImportExport de saudação distribuirá dados saudação em discos de saudação de forma otimizada. Olá discos de toomultiple de cópia de dados podem ser feitos em paralelo ou sequencialmente. Não há nenhum limite no número de saudação de dados de saudação de discos pode ser gravado toosimultaneously. ferramenta de saudação distribui dados com base no tamanho do disco e tamanho da pasta. Ele selecionará disco hello mais otimizado para saudação do tamanho do objeto. Olá dados quando carregado toohello conta de armazenamento será convergida volta toohello especificado a estrutura de diretórios.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>Onde posso encontrar a versão anterior da ferramenta WAImportExport?

A ferramenta WAImportExport tem todas as funcionalidades que a ferramenta WAImportExport V1 tinha. Ferramenta WAImportExport permite que os usuários toospecify várias origens e unidades de toomultiple de gravação. Além disso, um pode gerenciar facilmente vários locais de origem do qual dados saudação precisam toobe copiado em um único arquivo CSV. No entanto, no caso de precisar SAS suporte ou desejar toocopy única fonte toosingle disco, você pode [baixar WAImportExport V1 ferramenta] (http://go.microsoft.com/fwlink/? LinkID = 301900&amp;clcid = 0x409) e consulte muito[WAImportExport V1 referência](storage-import-export-tool-how-to-v1.md) para obter ajuda com o uso de WAImportExport V1.

#### <a name="what-is-a-session-id"></a>O que é uma ID de sessão?

ferramenta de saudação espera que a sessão de cópia de saudação (/ id) toobe parâmetro hello mesmo se a intenção de saudação toospread Olá dados em vários discos. Manter Olá mesmo nome de sessão de cópia Olá habilitará dados toocopy do usuário de um ou vários locais de origem para um ou vários discos/diretórios de destino. Mantendo a mesma id de sessão permite Olá ferramenta toopick backup de cópia de saudação de arquivos em que estava Olá última vez.

No entanto, a mesma sessão de cópia não pode ser tooimport usadas contas de armazenamento de toodifferent de dados.

Quando o nome de sessão de cópia é igual em várias execuções da ferramenta hello, Olá logfile (/ logdir) e a chave de conta de armazenamento (/ sk) é também toobe esperado Olá mesmo.

A SessionId pode conter letras, 0 a 9, sublinhado (\_), hífen (-) ou hash (#), e seu comprimento deve ser de 3 a 30.

Por exemplo, sessão-1 ou sessão#1 ou sessão\_1

#### <a name="what-is-a-journal-file"></a>O que é um arquivo de diário?

Cada vez que executar Olá WAImportExport ferramenta toocopy arquivos toohello disco rígido, a ferramenta Olá cria uma sessão de cópia. estado de saudação de sessão de cópia de saudação é gravado toohello arquivo de diário. Se uma sessão de cópia for interrompida (por exemplo, devido a perda de energia do sistema tooa), ele poderá ser retomado executando a ferramenta Olá novamente e especificando o arquivo de diário Olá na linha de comando de saudação.

Para cada disco rígido que você prepara com Olá, ferramenta de importação/exportação do Azure, a ferramenta de saudação criará um único arquivo de diário com o nome "&lt;DriveID&gt;. xml" onde Id da unidade é o número de série Olá associado unidade toohello Olá ferramenta lerá disco de saudação. Você precisará arquivos de diário de saudação de seu trabalho de importação unidades toocreate Olá todas. arquivo de diário Olá também pode ser usados tooresume preparação da unidade se Olá ferramenta for interrompida.

#### <a name="what-is-a-log-directory"></a>O que é um diretório de log?

diretório de log Olá Especifica que um diretório toobe usado logs detalhados toostore, bem como arquivos de manifesto temporários. Se não for especificado, diretório atual Olá será usado como diretório de log hello. Olá logs são logs detalhados.

### <a name="prerequisites"></a>Pré-requisitos

#### <a name="what-are-hello-specifications-of-my-disk"></a>Quais são as especificações de saudação do disco?

Um ou mais SATAII 2,5 polegadas ou 3,5 vazio ou III ou SSD rígido unidades de computador de cópia toohello conectado.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>Como habilitar o BitLocker em meu computador?

Toocheck de maneira simples é clicando na unidade do sistema. Ele mostrará opções do Bitlocker se o recurso de saudação é ativado. Se estiver desativado, você não o verá.

![Verificar o BitLocker](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

Este é um artigo em [como tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

É possível que seu computador não tenha o chip do TPM. Se não houver uma saída usando msc, examine Olá próxima FAQ.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>Como toodisable confiáveis Platform Module (TPM) no BitLocker?
> [!NOTE]
> Somente se não houver nenhum TPM em seus servidores, é necessário toodisable política TPM. Não é necessário toodisable TPM se houver um TPM confiável no servidor do usuário. 
> 

Em ordem toodisable TPM do BitLocker, percorrer Olá etapas a seguir:<br/>
1. Inicie o **Editor de Política de Grupo** digitando gpedit.msc em um prompt de comando. Se **Editor de política de grupo** toobe não estará disponível, para habilitar o BitLocker. Consulte as perguntas frequentes anteriores.
2. Abra **Política do Computador Local &gt; Configuração do Computador &gt; Modelos Administrativos &gt; Componentes do Windows&gt; Criptografia de Unidade de Disco BitLocker &gt; Unidades do Sistema Operacional**.
3. Edite a política **Exigir autenticação adicional na inicialização**.
4. Definir a política de saudação muito**habilitado** e certifique-se de **Permitir BitLocker sem um TPM compatível** é verificada.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>Como toocheck se o .NET 4 ou versão posterior está instalada no meu computador?

Todas as versões do Microsoft .NET Framework são instaladas no seguinte diretório: %Windir%\Microsoft.NET\Framework\

Navegue toohello acima mencionada parte no computador de destino onde a ferramenta Olá precisa toorun. Procure o nome da pasta que começa com "v4". A ausência de um diretório como esse significa que o .NET 4 não está instalado em seu computador. Você pode baixar o .Net 4 em seu computador usando o [Microsoft .NET Framework 4 (Instalador da Web)](https://www.microsoft.com/download/details.aspx?id=17851).

### <a name="limits"></a>limites

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>Quantas unidades pode, preparar/envio em Olá simultaneamente?

Não há nenhum limite no número de saudação de discos que Olá ferramenta pode preparar. No entanto, a ferramenta Olá espera letras de unidade como entradas. Que limita a preparação de disco simultâneas too25. Um único trabalho pode lidar no máximo com 10 discos por vez. Se você preparar os discos de mais de 10 direcionamento Olá a mesma conta de armazenamento, discos Olá podem ser distribuídos entre vários trabalhos.

#### <a name="can-i-target-more-than-one-storage-account"></a>Posso visar mais de uma conta de armazenamento?

Apenas uma conta de armazenamento pode ser enviada por trabalho e em uma única sessão de cópia.

### <a name="capabilities"></a>Funcionalidades

#### <a name="does-waimportexportexe-encrypt-my-data"></a>O WAImportExport.exe criptografa meus dados?

Sim. A criptografia do BitLocker é habilitada e exigida para esse processo.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>Qual será hierarquia Olá dos dados quando ele aparece na conta de armazenamento Olá?

Embora os dados são distribuídos entre discos, Olá dados quando carregado toohello conta de armazenamento será convergida toohello estrutura de diretório especificada no arquivo CSV Olá conjunto de dados de volta.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>A quantidade de saudação entrada discos terá ativa e/s em paralelo, quando a cópia está em andamento?

ferramenta Olá distribui dados em discos de entrada hello com base no tamanho Olá Olá de arquivos de entrada. Dito isso, número de saudação de discos ativos em paralelo delends completamente a natureza Olá Olá de dados de entrada. Dependendo do tamanho de saudação de arquivos individuais no conjunto de dados de entrada hello, um ou mais discos podem mostrar ativa e/s em paralelo. Confira a próxima pergunta para obter mais detalhes.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>Como ferramenta Olá distribuir arquivos Olá entre discos Olá?

A ferramenta de WAImportExport lê e grava arquivos, lote por lote, um lote contém no máximo 100000 arquivos. Isso significa que no máximo 100000 arquivos podem ser gravados em paralelo. Vários discos são gravados toosimultaneously se esses 100000 arquivos são distribuídas toomulti unidades. No entanto se ferramenta Olá grava toomultiple discos simultaneamente ou um único disco depende do tamanho cumulativo de saudação do lote de saudação. Por exemplo, no caso de arquivos menores, se todos os arquivos 10,0000 toofit capaz em uma única unidade, ferramenta gravará tooonly um disco durante o processamento de saudação desse lote.

### <a name="waimportexport-output"></a>Saída de WAImportExport

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>Há dois arquivos de diário, qual deles deverá posso carregar tooAzure portal?

**. XML** -para cada disco rígido que você prepara com a ferramenta WAImportExport de Olá, ferramenta de saudação criará um único arquivo de diário com nome `<DriveID>.xml` onde DriveID é o número de série Olá associado unidade toohello Olá ferramenta lê do disco de saudação. Você precisará arquivos de diário de saudação de todo o trabalho de importação unidades toocreate Olá no hello portal do Azure. Este arquivo de diário também pode ser usados tooresume preparação da unidade se Olá ferramenta for interrompida.

**.jrn** -arquivo de diário Olá com sufixo `.jrn` contém o status de saudação para todas as sessões de cópia para um disco rígido. Ele também contém informações de saudação necessário Olá toocreate trabalho de importação. Você sempre deve especificar um arquivo de diário ao ID de ferramenta de WAImportExport Olá em execução, bem como uma sessão de cópia

## <a name="next-steps"></a>Próximas etapas

* [Configurando Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup.md)
* [Processo de importação de definição de propriedades e metadados durante a saudação](storage-import-export-tool-setting-properties-metadata-import.md)
* [Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [Referência rápida para comandos usados frequentemente](storage-import-export-tool-quick-reference.md) 
* [Revisão do status do trabalho com arquivos de log de cópia](storage-import-export-tool-reviewing-job-status-v1.md)
* [Reparação de um trabalho de importação](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Reparação de um trabalho de exportação](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Olá, ferramenta de importação/exportação do Azure de solução de problemas](storage-import-export-tool-troubleshooting-v1.md)
