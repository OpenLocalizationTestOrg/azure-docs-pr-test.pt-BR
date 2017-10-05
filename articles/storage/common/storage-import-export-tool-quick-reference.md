---
title: "Referência rápida para comandos de trabalhos de importação da Ferramenta de Importação/Exportação do Azure | Microsoft Docs"
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
ms.openlocfilehash: d51ae35ead0e7d8289de663e5b7b48d28271e810
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="2301b-103">Referência rápida de comandos usados com frequência para trabalhos de importação</span><span class="sxs-lookup"><span data-stu-id="2301b-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="2301b-104">Este artigo fornece uma referência rápida de alguns comandos usados com frequência.</span><span class="sxs-lookup"><span data-stu-id="2301b-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="2301b-105">Para obter o uso detalhado, consulte [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md) (Preparando os discos rígidos para um trabalho de importação).</span><span class="sxs-lookup"><span data-stu-id="2301b-105">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="2301b-106">Primeira sessão</span><span class="sxs-lookup"><span data-stu-id="2301b-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="2301b-107">Segunda sessão</span><span class="sxs-lookup"><span data-stu-id="2301b-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="2301b-108">Anular a sessão mais recente</span><span class="sxs-lookup"><span data-stu-id="2301b-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="2301b-109">Retomar a sessão interrompida mais recente</span><span class="sxs-lookup"><span data-stu-id="2301b-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-to-latest-session"></a><span data-ttu-id="2301b-110">Adicionar unidades à sessão mais recente</span><span class="sxs-lookup"><span data-stu-id="2301b-110">Add drives to latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="2301b-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2301b-111">Next steps</span></span>

* [<span data-ttu-id="2301b-112">Fluxo de trabalho de exemplo para preparar discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="2301b-112">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
