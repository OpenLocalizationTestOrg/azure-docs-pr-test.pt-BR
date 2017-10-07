---
title: "aaaSetting propriedades e metadados de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como toospecify toobe de propriedades e metadados definidos em blobs de destino de saudação ao executar Olá ferramenta de importação/exportação do Azure tooprepare suas unidades. Isso se refere a toov1 de Olá, ferramenta de importação/exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5b7b1c346ecde8a26d985bd5de7efcf7d86eb9e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>Processo de importação de definição de propriedades e metadados durante a saudação
Quando você executa Olá ferramenta de importação/exportação do Microsoft Azure tooprepare suas unidades, você pode especificar propriedades e metadados toobe definidos em blobs de destino hello. Siga estas etapas:  
  
1.  Propriedades do blob tooset, crie um arquivo de texto no computador local que especifica os nomes de propriedade e valores.  
  
2.  tooset metadados de blob, crie um arquivo de texto no computador local que especifica os valores e nomes de metadados.  
  
3.  Passar Olá tooone de caminho completo ou ambos esses arquivos toohello ferramenta de importação/exportação do Azure como parte da saudação `PrepImport` operação.  
  
> [!NOTE]
>  Ao especificar um arquivo de propriedades ou de metadados como parte de uma sessão de cópia, essas propriedades ou esses metadados são definidos para cada blob importado como parte da sessão de cópia. Se você quiser toospecify um conjunto diferente de propriedades ou metadados para alguns dos blobs hello está sendo importados, você precisará toocreate sessão com propriedades diferentes ou arquivos de metadados de copiar um separado.  
  
## <a name="specify-blob-properties-in-a-text-file"></a>Especificar as propriedades de blob em um arquivo de texto  
Propriedades de blob toospecify, criar um arquivo de texto local e inclua XML que especifica os nomes de propriedade como elementos e valores de propriedade como valores. Este é um exemplo que especifica alguns valores de propriedade:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Salvar Olá arquivo tooa local como `C:\WAImportExport\ImportProperties.txt`.  
  
## <a name="specify-blob-metadata-in-a-text-file"></a>Especificar os metadados de blob em um arquivo de texto  
Da mesma forma, toospecify metadados de blob, crie um arquivo de texto local que especifica os nomes de metadados como elementos e valores de metadados como valores. Este é um exemplo que especifica alguns valores de metadados:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Salvar Olá arquivo tooa local como `C:\WAImportExport\ImportMetadata.txt`.  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a>Criar uma saudação incluindo da sessão de cópia propriedades ou arquivos de metadados  
Quando você executa o trabalho de importação do hello ferramenta de importação/exportação do Azure tooprepare hello, especifique o arquivo de propriedades de Olá na linha de comando hello usando Olá `PropertyFile` parâmetro. Especificar arquivo de metadados de saudação na linha de comando hello usando Olá `/MetadataFile` parâmetro. Este é um exemplo que especifica os dois arquivos:  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a>Próximas etapas

* [Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação](../storage-import-export-file-format-metadata-and-properties.md)
