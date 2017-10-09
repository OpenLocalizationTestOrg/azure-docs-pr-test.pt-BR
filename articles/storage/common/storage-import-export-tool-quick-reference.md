---
title: "referência de aaaQuick para comandos de trabalho de importação de ferramenta de importação/exportação do Azure | Microsoft Docs"
description: "Referência de comandos da Ferramenta de Importação/Exportação do Azure para comandos de trabalho de importação usados com frequência."
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
ms.openlocfilehash: 35e46f24f764a5098ca465adb51badcab2d13e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Referência rápida de comandos usados com frequência para trabalhos de importação

Este artigo fornece uma referência rápida de alguns comandos usados com frequência. Para obter o uso detalhado, consulte [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md) (Preparando os discos rígidos para um trabalho de importação).

## <a name="first-session"></a>Primeira sessão

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a>Segunda sessão

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a>Anular a sessão mais recente

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a>Retomar a sessão interrompida mais recente

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a>Adicionar unidades toolatest sessão

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a>Próximas etapas

* [Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
