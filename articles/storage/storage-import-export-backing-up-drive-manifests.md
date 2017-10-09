---
title: "aaaBacking backup de manifestos da unidade de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toohave sua unidade manifestos para serviço de importação/exportação do Microsoft Azure Olá passam por backup automaticamente."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Fazendo backup de manifestos de unidade de trabalhos de Importação/Exportação do Azure

Manifestos de unidade podem ser feitos backup tooblobs por configuração Olá `BackupDriveManifest` propriedade muito`true` em Olá [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operações da API REST. Por padrão, Olá manifestos de unidade sem backup. backups de manifesto da unidade Olá são armazenados como blobs de bloco em um contêiner na conta de armazenamento Olá associado ao trabalho hello. Por padrão, o nome do contêiner de saudação é `waimportexport`, mas você pode especificar um nome diferente na Olá `DiagnosticsPath` propriedade ao chamar hello `Put Job` ou `Update Job Properties` operações. Olá blob do manifesto de backup são nomeados em Olá formato a seguir: `waies/jobname_driveid_timestamp_manifest.xml`.

 Você pode recuperar Olá URI da unidade de backup Olá manifestos de um trabalho por chamada hello [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_Get) operação. blob Olá URI é retornado no hello `ManifestUri` propriedade para cada unidade.

## <a name="next-steps"></a>Próximas etapas

* [Usando a API REST do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
