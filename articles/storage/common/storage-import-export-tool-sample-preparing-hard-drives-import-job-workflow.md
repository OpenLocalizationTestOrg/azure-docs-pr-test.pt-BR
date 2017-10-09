---
title: "trabalho de importação de aaaSample fluxo de trabalho tooprep unidades de disco rígido para uma importação/exportação do Azure | Microsoft Docs"
description: "Veja um passo a passo para o processo completo de saudação preparar unidades para um trabalho de importação no hello serviço de importação/exportação do Azure."
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
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: fa7f36300b35b81757523de4960fd583bd4bf305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação

Este artigo o orienta pelo processo de conclusão de saudação preparar unidades para um trabalho de importação.

## <a name="sample-data"></a>Dados de amostra

Este exemplo importa Olá seguintes dados em uma conta de armazenamento do Azure denominada `mystorageaccount`:

|Local|Descrição|Tamanho dos dados|
|--------------|-----------------|-----|
|H:\Video\ |Uma coleção de vídeos|12 TB|
|H:\Photo\ |Uma coleção de fotos|30 GB|
|K:\Temp\FavoriteMovie.ISO|Uma imagem de disco Blu-ray™|25 GB|
|\\\bigshare\john\music\|Uma coleção de arquivos de música em um compartilhamento de rede|10 GB|

## <a name="storage-account-destinations"></a>Destinos de conta de armazenamento

trabalho de importação Olá importará dados saudação para Olá destinos na conta de armazenamento Olá a seguir:

|Fonte|Blob de destino ou diretório virtual|
|------------|-------------------------------------------|
|H:\Video\ |video/|
|H:\Photo\ |photo/|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |music|

Com esse mapeamento, Olá arquivo `H:\Video\Drama\GreatMovie.mov` serão importados toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.

## <a name="determine-hard-drive-requirements"></a>Determinar os requisitos de disco rígido

Em seguida, toodetermine quantos discos rígidos necessários, computação Olá tamanho dos dados de saudação:

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

Neste exemplo, duas unidades de disco rígido de 8TB devem ser suficientes. No entanto, como o diretório de origem Olá `H:\Video` tem 12TB de dados e a capacidade de seu único disco rígido é apenas 8TB, você será capaz de toospecify isso em Olá após a forma como o hello **driveset.csv** arquivo:

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
ferramenta de saudação distribui dados em dois discos rígidos de forma otimizada.

## <a name="attach-drives-and-configure-hello-job"></a>Anexar discos e configurar o trabalho de saudação
Você anexar a máquina de toohello ambos os discos e criar volumes. Em seguida, crie o arquivo **dataset.csv**:
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

Além disso, você pode definir Olá metadados para todos os arquivos a seguir:

* **UploadMethod:** serviço de Importação/Exportação do Windows Azure
* **DataSetName:** SampleData
* **CreationDate:** 10/1/2013

tooset metadados para arquivos de saudação importado, crie um arquivo de texto, `c:\WAImportExport\SampleMetadata.txt`, com hello conteúdo a seguir:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

Você também pode definir algumas propriedades para Olá `FavoriteMovie.ISO` blob:

* **Content-Type:** application/octet-stream
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==
* **Cache-Control:** no-cache

tooset essas propriedades, crie um arquivo de texto, `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>Olá execução ferramenta de importação/exportação do Azure (WAImportExport.exe)

Agora você está pronto toorun Olá ferramenta de importação/exportação do Azure tooprepare Olá duas unidades de disco rígido.

**Para a primeira sessão de saudação:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Se precisarem de mais dados toobe adicionado, crie outro arquivo de conjunto de dados (mesmo formato Initialdataset).

**Para Olá segunda sessão:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Depois de concluir as sessões de cópia de Olá, você pode desconectar duas unidades de saudação do computador de cópia hello e enviá-las toohello do Azure data center apropriado. Você vai carregar arquivos de diário de saudação dois `<FirstDriveSerialNumber>.xml` e `<SecondDriveSerialNumber>.xml`, ao criar trabalho de importação Olá Olá portal do Azure.

## <a name="next-steps"></a>Próximas etapas

* [Preparação de discos rígidos para um trabalho de importação](../storage-import-export-tool-preparing-hard-drives-import.md)
* [Referência rápida para comandos usados frequentemente](../storage-import-export-tool-quick-reference.md)
