---
title: "referência de aaaQuick para comandos de trabalho de importação da ferramenta de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Referência de comandos da Ferramenta de Importação/Exportação do Azure para comandos de trabalho de importação usados com frequência. Isso se refere a toov1 de Olá, ferramenta de importação/exportação."
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Referência rápida de comandos usados com frequência para trabalhos de importação
Esta seção fornece uma referência rápida de alguns comandos usados com frequência. Para obter o uso detalhado, consulte [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparando os discos rígidos para um trabalho de importação).  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a>Preparar discos hello quando os dados copiados já toohello discos
 Aqui está um tooprepare do comando de exemplo um discos quando os dados copiados já toohello disco rígido que não tenha sido criptografado com o BitLocker:  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>Copiar um único diretório tooa disco rígido  
 Aqui está um toocopy do comando de exemplo da fonte de um único diretório tooa disco rígido que não tenha sido criptografado com o BitLocker:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a>Copie a unidade de disco rígido wwo diretórios tooa  
 toocopy dois diretórios tooa unidade de origem, você precisará de dois comandos.  
  
 Olá primeiro comando Especifica o diretório de log hello, chave de conta de armazenamento, letra de unidade de destino e `format/encrypt` requisitos de parâmetros comuns de toohello de adição:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 Olá segundo comando Especifica o arquivo de diário hello, uma nova ID de sessão e locais de origem e destino hello:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>Copiar um arquivo grande tooa disco rígido em uma segunda sessão de cópia  
 Aqui está um exemplo de comando que copia uma unidade de tooa único arquivo grande que tenha sido preparada em uma sessão de cópia anterior:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Próximas etapas

* [Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
