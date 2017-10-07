---
title: formato de arquivo aaaAzure importar/exportar metadados e propriedades | Microsoft Docs
description: "Saiba como toospecify metadados e propriedades para um ou mais blobs que fazem parte de uma importação ou exportação de trabalho."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a>Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação do Azure
É possível especificar metadados e propriedades para um ou mais blobs como parte de um trabalho de importação ou exportação. tooset metadados ou propriedades para blobs que está sendo criados como parte de um trabalho de importação, você fornecer um arquivo de metadados ou propriedades na unidade de disco rígido Olá contendo Olá toobe de dados importado. Para um trabalho de exportação, propriedades e os metadados são gravadas tooa metadados ou propriedades de arquivo que está incluído no disco rígido de saudação retornado tooyou.  
  
## <a name="metadata-file-format"></a>Formato de arquivo de metadados  
formato de saudação de um arquivo de metadados é o seguinte:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|Elemento XML|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|`Metadata`|Elemento raiz|elemento de raiz Olá Olá do arquivo de metadados.|  
|`metadata-name`|Cadeia de caracteres|Opcional. elemento XML de saudação especifica o nome de saudação de metadados de saudação blob hello e seu valor Especifica o valor de saudação da configuração de metadados de saudação.|  
  
## <a name="properties-file-format"></a>Formato de arquivo de propriedades  
formato de saudação de um arquivo de propriedades é o seguinte:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|Elemento XML|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|`Properties`|Elemento raiz|elemento raiz de saudação do arquivo de propriedades de saudação.|  
|`Last-Modified`|Cadeia de caracteres|Opcional. Olá hora da última modificação para blob hello. Somente para trabalhos de exportação.|  
|`Etag`|Cadeia de caracteres|Opcional. Olá valor ETag do blob. Somente para trabalhos de exportação.|  
|`Content-Length`|Cadeia de caracteres|Opcional. tamanho de saudação do blob Olá em bytes. Somente para trabalhos de exportação.|  
|`Content-Type`|Cadeia de caracteres|Opcional. tipo de conteúdo de saudação do blob hello.|  
|`Content-MD5`|Cadeia de caracteres|Opcional. Olá hash MD5 do blob.|  
|`Content-Encoding`|Cadeia de caracteres|Opcional. Olá conteúdo do blob de codificação.|  
|`Content-Language`|Cadeia de caracteres|Opcional. Olá idioma do conteúdo do blob.|  
|`Cache-Control`|Cadeia de caracteres|Opcional. sequência de controle de cache Olá blob hello.|  

## <a name="next-steps"></a>Próximas etapas

Confira [Set Blob Properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) e [Setting and Retrieving Properties and Metadata for Blob Resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Definição e recuperação de propriedades e de metadados para recursos de blob) para obter as regras detalhadas sobre como definir as propriedades e os metadados do blob.
