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
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="88379-103">Diagnóstico e recuperação de erro para trabalhos de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="88379-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="88379-104">Para cada unidade processada, Olá serviço de importação/exportação do Azure cria um log de erros na conta de armazenamento Olá associado.</span><span class="sxs-lookup"><span data-stu-id="88379-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="88379-105">Você também pode habilitar o log detalhado por configuração Olá `LogLevel` propriedade muito`Verbose` ao chamar hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operações.</span><span class="sxs-lookup"><span data-stu-id="88379-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="88379-106">Por padrão, os logs são gravados tooa contêiner nomeado `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="88379-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="88379-107">Você pode especificar um nome diferente, definindo Olá `DiagnosticsPath` propriedade ao chamar hello `Put Job` ou `Update Job Properties` operações.</span><span class="sxs-lookup"><span data-stu-id="88379-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="88379-108">Olá logs são armazenados como blobs de bloco com hello convenção de nomenclatura a seguir: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="88379-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="88379-109">Você pode recuperar Olá URI dos logs de saudação para um trabalho por chamada hello [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_Get) operação.</span><span class="sxs-lookup"><span data-stu-id="88379-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="88379-110">Olá URI para o log detalhado Olá é retornado no hello `VerboseLogUri` propriedade para cada unidade, enquanto hello URI para o log de erros de saudação é retornado no hello `ErrorLogUri` propriedade.</span><span class="sxs-lookup"><span data-stu-id="88379-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="88379-111">Você pode usar Olá Olá tooidentify de dados seguintes problemas de registro em log.</span><span class="sxs-lookup"><span data-stu-id="88379-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="88379-112">Erros de unidade</span><span class="sxs-lookup"><span data-stu-id="88379-112">Drive errors</span></span>

<span data-ttu-id="88379-113">Olá itens a seguir é classificado como erros de disco:</span><span class="sxs-lookup"><span data-stu-id="88379-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="88379-114">Arquivo de manifesto de erros ao acessar ou ler Olá</span><span class="sxs-lookup"><span data-stu-id="88379-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="88379-115">Chaves incorretas do BitLocker</span><span class="sxs-lookup"><span data-stu-id="88379-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="88379-116">Erros de leitura/gravação da unidade</span><span class="sxs-lookup"><span data-stu-id="88379-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="88379-117">Erros de blob</span><span class="sxs-lookup"><span data-stu-id="88379-117">Blob errors</span></span>

<span data-ttu-id="88379-118">Olá itens a seguir é classificado como erros de blob:</span><span class="sxs-lookup"><span data-stu-id="88379-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="88379-119">Nomes de blob incorretos ou conflitantes</span><span class="sxs-lookup"><span data-stu-id="88379-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="88379-120">Arquivos ausentes</span><span class="sxs-lookup"><span data-stu-id="88379-120">Missing files</span></span>

-   <span data-ttu-id="88379-121">Blob não encontrado</span><span class="sxs-lookup"><span data-stu-id="88379-121">Blob not found</span></span>

-   <span data-ttu-id="88379-122">Arquivos truncados (arquivos Olá no disco Olá são menores do que o especificado no manifesto de saudação)</span><span class="sxs-lookup"><span data-stu-id="88379-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="88379-123">Conteúdo do arquivo corrompido (para trabalhos de importação, detectado com uma soma de verificação MD5 incompatível)</span><span class="sxs-lookup"><span data-stu-id="88379-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="88379-124">Arquivos de metadados e propriedades de blob corrompidos (detectados com uma soma de verificação MD5 incompatível)</span><span class="sxs-lookup"><span data-stu-id="88379-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="88379-125">Esquema incorreto para propriedades de blob hello e/ou arquivos de metadados</span><span class="sxs-lookup"><span data-stu-id="88379-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="88379-126">Pode haver casos onde algumas partes de um trabalho de importação ou exportação não concluída com êxito, enquanto hello geral trabalho ainda é concluída.</span><span class="sxs-lookup"><span data-stu-id="88379-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="88379-127">Nesse caso, você pode carregar ou baixar Olá ausente Olá dados pela rede, ou você pode criar um novo trabalho tootransfer Olá de dados.</span><span class="sxs-lookup"><span data-stu-id="88379-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="88379-128">Consulte Olá [referência da ferramenta de importação/exportação do Azure](storage-import-export-tool-how-to-v1.md) toolearn como toorepair Olá dados pela rede.</span><span class="sxs-lookup"><span data-stu-id="88379-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88379-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88379-129">Next steps</span></span>

* [<span data-ttu-id="88379-130">Usando a API REST do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="88379-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
