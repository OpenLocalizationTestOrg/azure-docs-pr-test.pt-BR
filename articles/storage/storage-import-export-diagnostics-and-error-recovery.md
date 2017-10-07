---
title: "aaaDiagnostics e recuperação de erros para trabalhos de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como trabalhos do serviço tooenable o log detalhado de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a>Diagnóstico e recuperação de erro para trabalhos de Importação/Exportação do Azure
Para cada unidade processada, Olá serviço de importação/exportação do Azure cria um log de erros na conta de armazenamento Olá associado. Você também pode habilitar o log detalhado por configuração Olá `LogLevel` propriedade muito`Verbose` ao chamar hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operações.

 Por padrão, os logs são gravados tooa contêiner nomeado `waimportexport`. Você pode especificar um nome diferente, definindo Olá `DiagnosticsPath` propriedade ao chamar hello `Put Job` ou `Update Job Properties` operações. Olá logs são armazenados como blobs de bloco com hello convenção de nomenclatura a seguir: `waies/jobname_driveid_timestamp_logtype.xml`.

 Você pode recuperar Olá URI dos logs de saudação para um trabalho por chamada hello [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_Get) operação. Olá URI para o log detalhado Olá é retornado no hello `VerboseLogUri` propriedade para cada unidade, enquanto hello URI para o log de erros de saudação é retornado no hello `ErrorLogUri` propriedade.

Você pode usar Olá Olá tooidentify de dados seguintes problemas de registro em log.

## <a name="drive-errors"></a>Erros de unidade

Olá itens a seguir é classificado como erros de disco:

-   Arquivo de manifesto de erros ao acessar ou ler Olá

-   Chaves incorretas do BitLocker

-   Erros de leitura/gravação da unidade

## <a name="blob-errors"></a>Erros de blob

Olá itens a seguir é classificado como erros de blob:

-   Nomes de blob incorretos ou conflitantes

-   Arquivos ausentes

-   Blob não encontrado

-   Arquivos truncados (arquivos Olá no disco Olá são menores do que o especificado no manifesto de saudação)

-   Conteúdo do arquivo corrompido (para trabalhos de importação, detectado com uma soma de verificação MD5 incompatível)

-   Arquivos de metadados e propriedades de blob corrompidos (detectados com uma soma de verificação MD5 incompatível)

-   Esquema incorreto para propriedades de blob hello e/ou arquivos de metadados

Pode haver casos onde algumas partes de um trabalho de importação ou exportação não concluída com êxito, enquanto hello geral trabalho ainda é concluída. Nesse caso, você pode carregar ou baixar Olá ausente Olá dados pela rede, ou você pode criar um novo trabalho tootransfer Olá de dados. Consulte Olá [referência da ferramenta de importação/exportação do Azure](storage-import-export-tool-how-to-v1.md) toolearn como toorepair Olá dados pela rede.

## <a name="next-steps"></a>Próximas etapas

* [Usando a API REST do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
