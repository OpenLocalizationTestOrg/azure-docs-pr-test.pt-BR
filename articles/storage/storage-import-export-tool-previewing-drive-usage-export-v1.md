---
title: "uso da unidade aaaPreviewing para um trabalho de exportação de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como lista de saudação toopreview de blobs que você tiver selecionado para um trabalho de exportação no serviço de importação/exportação do Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 88495f921371458c0451da6878fd7cc9a45d20cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a>Visualizando o uso da unidade de um trabalho de exportação
Antes de criar um trabalho de exportação, você precisa toochoose um conjunto de blobs toobe exportado. Olá serviço de importação/exportação do Microsoft Azure permite que você toouse uma lista de caminhos de blob ou prefixos de blob blobs de saudação toorepresent que você selecionou.  
  
Em seguida, você precisa toodetermine quantas unidades você precisa toosend. Olá, ferramenta de importação/exportação fornece Olá `PreviewExport` uso de unidade do comando toopreview para blobs de saudação que você selecionou, com base no tamanho Olá Olá unidades que serão toouse.

## <a name="command-line-parameters"></a>Parâmetros de linha de comando

Você pode usar o hello parâmetros a seguir ao usar o hello `PreviewExport` comando da ferramenta de importação/exportação de saudação.

|Parâmetro de linha de comando|Descrição|  
|--------------------------|-----------------|  
|**/logdir:**<LogDirectory\>|Opcional. diretório de log Hello. Arquivos de log detalhados serão gravados toothis directory. Se nenhum diretório de log for especificado, diretório atual Olá será usado como diretório de log hello.|  
|**/sn:**<StorageAccountName\>|Obrigatório. trabalho de exportação de nome de Olá Olá da conta de armazenamento para hello.|  
|**/sk:**<StorageAccountKey\>|Necessário somente se uma SAS do contêiner não for especificada. trabalho de exportação da chave da conta Olá para conta de armazenamento Olá Olá.|  
|**/csas:**<ContainerSas\>|Necessário somente se uma chave de conta de armazenamento não for especificada. SAS do contêiner Olá para listagem Olá blobs toobe exportados no trabalho de exportação de saudação.|  
|**/ExportBlobListFile:**<ExportBlobListFile\>|Obrigatório. Toohello caminho XML arquivo contendo a lista de caminhos de blob ou prefixos de caminho para Olá blobs toobe exportados de blob. formato de arquivo Hello usado em Olá `BlobListBlobPath` elemento Olá [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação da API REST do serviço de importação/exportação de saudação.|  
|**/DriveSize:**<DriveSize\>|Obrigatório. Olá tamanho de unidades toouse para um trabalho de exportação, *, por exemplo,*, 500GB, 1,5 TB.|  

## <a name="command-line-example"></a>Exemplo de linha de comando

Olá, exemplo a seguir demonstra Olá `PreviewExport` comando:  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
Olá arquivo de lista de blob de exportação pode conter nomes de blob e prefixos de blob, conforme mostrado aqui:  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

Olá, ferramenta de importação/exportação do Azure lista todos os toobe blobs exportados e calcula como toopack-los em unidades de saudação especificado tamanho, levando em consideração qualquer sobrecarga necessária, em seguida, calcula o número de saudação de unidades necessárias blobs de saudação toohold e o uso da unidade informações.  
  
Aqui está um exemplo de saída de hello, com logs informativos omitidos:  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a>Próximas etapas

* [Referência da Ferramenta de Importação/Exportação do Azure](storage-import-export-tool-how-to-v1.md)
