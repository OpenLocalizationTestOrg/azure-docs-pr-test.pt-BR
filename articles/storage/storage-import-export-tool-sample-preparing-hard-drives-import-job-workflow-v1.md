---
title: "trabalho - v1 de importação de aaaSample fluxo de trabalho tooprep unidades de disco rígido para uma importação/exportação do Azure | Microsoft Docs"
description: "Veja um passo a passo para o processo completo de saudação preparar unidades para um trabalho de importação no hello serviço de importação/exportação do Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação
Este tópico o orienta pelo processo de conclusão de saudação preparar unidades para um trabalho de importação.  
  
Este exemplo importa Olá seguintes dados em uma conta de armazenamento do Windows Azure denominada `mystorageaccount`:  
  
|Local|Descrição|  
|--------------|-----------------|  
|H:\Video|Uma coleção de vídeos, 5 TB no total.|  
|H:\Photo|Uma coleção de fotos, 30 GB no total.|  
|K:\Temp\FavoriteMovie.ISO|Uma imagem de disco Blu-ray™, 25 GB.|  
|\\\bigshare\john\music|Uma coleção de arquivos de música em um compartilhamento de rede, 10 GB no total.|  
  
trabalho de importação Olá importará esses dados para Olá destinos na conta de armazenamento Olá a seguir:  
  
|Fonte|Blob de destino ou diretório virtual|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.blob.core.windows.net/music|  
  
Com esse mapeamento, Olá arquivo `H:\Video\Drama\GreatMovie.mov` serão importados toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.  
  
Em seguida, toodetermine quantos discos rígidos necessários, computação Olá tamanho dos dados de saudação:  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
Neste exemplo, duas unidades de disco rígido de 3TB devem ser suficientes. No entanto, como o diretório de origem Olá `H:\Video` tem 5TB de dados e a capacidade do disco rígido único é apenas 3TB, é necessário toobreak `H:\Video` em dois diretórios secundários antes de executar Olá ferramenta de importação/exportação do Microsoft Azure: `H:\Video1` e `H:\Video2`. Esta etapa gera Olá diretórios de origem a seguir:  
  
|Local|Tamanho|Blob de destino ou diretório virtual|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2,5 TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Video2|2,5 TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|30GB|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovies.ISO|25 GB|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10GB|https://mystorageaccount.blob.core.windows.net/music|  
  
 Observe que, embora Olá `H:\Video`diretório seja dividido tootwo diretórios, eles apontam toohello mesmo diretório virtual de destino na conta de armazenamento hello. Dessa forma, todos os arquivos de vídeos são mantidos em um único `video` contêiner na conta de armazenamento hello.  
  
 Em seguida, Olá acima fonte diretórios são uniformemente distribuído toohello dois discos rígidos:  
  
||||  
|-|-|-|  
|Disco rígido|Diretórios de origem|Tamanho total|  
|Primeira unidade|H:\Video1|2.5TB + 30GB|  
||H:\Photo||  
|Segunda unidade|H:\Video2|2.5TB + 35GB|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
Além disso, você pode definir Olá metadados para todos os arquivos a seguir:  
  
-   **UploadMethod:** serviço de Importação/Exportação do Windows Azure  
  
-   **DataSetName:** SampleData  
  
-   **CreationDate:** 10/1/2013  
  
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
  
-   **Content-Type:** application/octet-stream  
  
-   **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==  
  
-   **Cache-Control:** no-cache  
  
tooset essas propriedades, crie um arquivo de texto, `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Agora você está pronto toorun Olá ferramenta de importação/exportação do Azure tooprepare Olá duas unidades de disco rígido. Observe que:  
  
-   Olá primeira unidade é gerada como a unidade X.  
  
-   Olá segunda unidade é gerada como a unidade Y.  
  
-   Olá chave Olá conta de armazenamento `mystorageaccount` é `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>Preparando o disco para importação quando dados são carregados previamente
 
 Se Olá dados toobe importado já está presente no disco hello, use Olá sinalizador /skipwrite. Valor de /t e /srcdir deve apontar toohello disco que está sendo preparado para importação. Se nem todos os Olá dados em disco Olá precisa toogo toohello mesmo diretório virtual de destino ou raiz da conta de armazenamento de Olá Olá execução mesmo comando para cada diretório separadamente mantendo o valor de saudação do /id mesmo em todas as execuções.

>[!NOTE] 
>Não especifique /format como ele será apagar dados de Olá no disco hello. Você pode especificar / criptografar ou /bk dependendo se o disco de saudação já está criptografado ou não. 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>Sessões de cópia — primeira unidade

Para a primeira unidade de hello, execute Olá, ferramenta de importação/exportação do Azure da fonte de duas vezes Olá toocopy dois diretórios:  

**Primeira sessão de cópia**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**Segunda sessão de cópia**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>Sessões de cópia — segunda unidade
 
Para Olá segunda unidade, execute Olá ferramenta de importação/exportação do Azure três vezes, uma vez para Olá diretórios de origem e uma vez para Olá autônomo Blu-Ray™ arquivo de imagem):  
  
**Primeira sessão de cópia** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**Segunda sessão de cópia**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**Terceira sessão de cópia**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>Conclusão da sessão de cópia

Depois de concluir as sessões de cópia de Olá, você pode desconectar duas unidades de saudação do computador de cópia hello e enviá-las toohello apropriado do Windows Azure Datacenter. Você vai carregar arquivos de diário de saudação dois `FirstDrive.jrn` e `SecondDrive.jrn`, ao criar trabalho de importação Olá Olá [Portal de gerenciamento do Windows Azure](https://manage.windowsazure.com/).  
  
## <a name="next-steps"></a>Próximas etapas

* [Preparação de discos rígidos para um trabalho de importação](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Referência rápida para comandos usados frequentemente](storage-import-export-tool-quick-reference-v1.md) 
