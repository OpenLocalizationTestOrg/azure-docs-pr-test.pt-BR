---
title: "aaaReviewing status do trabalho de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como arquivos de log de Olá de toouse criados quando Olá importar ou exportar trabalho foi executado toosee status de saudação do trabalho de importação/exportação de saudação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>Examinando o Status do trabalho de Importação/Exportação do Azure com cópias de arquivos de log
Quando Olá serviço de importação/exportação do Microsoft Azure processa unidades associadas a um trabalho de importação ou exportação, ele grava cópia log arquivos toohello armazenamento conta tooor do qual você estiver importando ou exportando blobs. o arquivo de log Olá contém o status detalhado sobre cada arquivo que foi importado ou exportado. o arquivo de log de cópia do Hello URL tooeach é retornado quando você consulta o status de saudação de um trabalho concluído; consulte [obter trabalho](/rest/api/storageservices/Get-Job3) para obter mais informações.  

## <a name="example-urls"></a>URLs de exemplo

Olá seguem URLs de exemplo para copiar arquivos de log para um trabalho de importação com duas unidades:  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 Consulte [formato de arquivo de Log do serviço de importação/exportação](../storage-import-export-file-format-log.md) para formato de saudação dos logs de cópia e a lista completa de saudação dos códigos de status.  
  
## <a name="next-steps"></a>Próximas etapas
 
 * [Configurando Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup-v1.md)   
 * [Preparação de discos rígidos para um trabalho de importação](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [Reparação de um trabalho de importação](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [Reparação de um trabalho de exportação](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [Olá, ferramenta de importação/exportação do Azure de solução de problemas](storage-import-export-tool-troubleshooting-v1.md)
