---
title: "Diagnóstico e recuperação de erro para os trabalhos de Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba como habilitar o log detalhado para os trabalhos do serviço de Importação/Exportação do Microsoft Azure."
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
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="00dc0-103">Diagnóstico e recuperação de erro para trabalhos de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="00dc0-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="00dc0-104">Para cada unidade processada, o serviço de Importação/Exportação do Azure cria um log de erros na conta de armazenamento associada.</span><span class="sxs-lookup"><span data-stu-id="00dc0-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="00dc0-105">Também é possível habilitar o log detalhado definindo a propriedade `LogLevel` como `Verbose` ao chamar as operações [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update).</span><span class="sxs-lookup"><span data-stu-id="00dc0-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="00dc0-106">Por padrão, os logs são gravados em um contêiner denominado `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="00dc0-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="00dc0-107">Você pode especificar outro nome definindo a propriedade `DiagnosticsPath` ao chamar as operações `Put Job` ou `Update Job Properties`.</span><span class="sxs-lookup"><span data-stu-id="00dc0-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="00dc0-108">Os logs são armazenados como blobs de blocos com a seguinte convenção de nomenclatura: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="00dc0-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="00dc0-109">É possível recuperar o URI dos logs de um trabalho chamando a operação [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="00dc0-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="00dc0-110">O URI do log detalhado é retornado na propriedade `VerboseLogUri` de cada unidade, enquanto o URI do log de erros é retornado na propriedade `ErrorLogUri`.</span><span class="sxs-lookup"><span data-stu-id="00dc0-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="00dc0-111">É possível usar os dados de log para identificar os problemas a seguir.</span><span class="sxs-lookup"><span data-stu-id="00dc0-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="00dc0-112">Erros de unidade</span><span class="sxs-lookup"><span data-stu-id="00dc0-112">Drive errors</span></span>

<span data-ttu-id="00dc0-113">Os seguintes itens são classificados como erros de unidade:</span><span class="sxs-lookup"><span data-stu-id="00dc0-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="00dc0-114">Erros ao acessar ou ler o arquivo de manifesto</span><span class="sxs-lookup"><span data-stu-id="00dc0-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="00dc0-115">Chaves incorretas do BitLocker</span><span class="sxs-lookup"><span data-stu-id="00dc0-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="00dc0-116">Erros de leitura/gravação da unidade</span><span class="sxs-lookup"><span data-stu-id="00dc0-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="00dc0-117">Erros de blob</span><span class="sxs-lookup"><span data-stu-id="00dc0-117">Blob errors</span></span>

<span data-ttu-id="00dc0-118">Os seguintes itens são classificados como erros de blob:</span><span class="sxs-lookup"><span data-stu-id="00dc0-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="00dc0-119">Nomes de blob incorretos ou conflitantes</span><span class="sxs-lookup"><span data-stu-id="00dc0-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="00dc0-120">Arquivos ausentes</span><span class="sxs-lookup"><span data-stu-id="00dc0-120">Missing files</span></span>

-   <span data-ttu-id="00dc0-121">Blob não encontrado</span><span class="sxs-lookup"><span data-stu-id="00dc0-121">Blob not found</span></span>

-   <span data-ttu-id="00dc0-122">Arquivos truncados (os arquivos no disco são menores que os especificados no manifesto)</span><span class="sxs-lookup"><span data-stu-id="00dc0-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="00dc0-123">Conteúdo do arquivo corrompido (para trabalhos de importação, detectado com uma soma de verificação MD5 incompatível)</span><span class="sxs-lookup"><span data-stu-id="00dc0-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="00dc0-124">Arquivos de metadados e propriedades de blob corrompidos (detectados com uma soma de verificação MD5 incompatível)</span><span class="sxs-lookup"><span data-stu-id="00dc0-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="00dc0-125">Esquema incorreto para os arquivos de propriedades e/ou metadados de blob</span><span class="sxs-lookup"><span data-stu-id="00dc0-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="00dc0-126">Pode haver casos em que algumas partes de um trabalho de importação ou exportação não são concluídas com êxito, enquanto o trabalho geral ainda é concluído.</span><span class="sxs-lookup"><span data-stu-id="00dc0-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="00dc0-127">Nesse caso, é possível carregar ou baixar as partes ausentes dos dados pela rede ou criar um novo trabalho para transferir os dados.</span><span class="sxs-lookup"><span data-stu-id="00dc0-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="00dc0-128">Consulte a [Referência da Ferramenta de Importação/Exportação do Azure](storage-import-export-tool-how-to-v1.md) para saber como reparar os dados pela rede.</span><span class="sxs-lookup"><span data-stu-id="00dc0-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00dc0-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00dc0-129">Next steps</span></span>

* [<span data-ttu-id="00dc0-130">Usando a API REST do serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="00dc0-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
