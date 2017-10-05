---
title: "Cancelar e excluir um trabalho de Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba como cancelar e excluir trabalhos do serviço de Importação/Exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1e989c72fc03697bf6d2e515ff53003703665d1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="5d326-103">Cancelando e excluindo trabalhos de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="5d326-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="5d326-104">Para solicitar que um trabalho seja cancelado antes que ele entre no estado `Packaging`, chame a operação [Atualizar Propriedades do Trabalho](/rest/api/storageimportexport/jobs#Jobs_Update) e defina o elemento `CancelRequested` como `true`.</span><span class="sxs-lookup"><span data-stu-id="5d326-104">To request that a job be canceled before it is in the `Packaging` state, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="5d326-105">O trabalho é cancelado com os melhores esforços.</span><span class="sxs-lookup"><span data-stu-id="5d326-105">The job is canceled on a best-effort basis.</span></span> <span data-ttu-id="5d326-106">Se as unidades estiverem transferindo dados, os dados poderão continuar sendo transferidos mesmo depois que o cancelamento tiver sido solicitado.</span><span class="sxs-lookup"><span data-stu-id="5d326-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="5d326-107">Um trabalho cancelado é movido para o estado `Completed` e é mantido por 90 dias, ponto em que é excluído.</span><span class="sxs-lookup"><span data-stu-id="5d326-107">A canceled job is moved to the `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="5d326-108">Para excluir um trabalho, chame a operação [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) antes que o trabalho seja enviado (ou seja, enquanto o trabalho está no estado `Creating`).</span><span class="sxs-lookup"><span data-stu-id="5d326-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (that is, while the job is in the `Creating` state).</span></span> <span data-ttu-id="5d326-109">Também é possível excluir um trabalho quando ele está no estado `Completed`.</span><span class="sxs-lookup"><span data-stu-id="5d326-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="5d326-110">Após a exclusão de um trabalho, suas informações e seu status não são mais acessíveis por meio da API REST ou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d326-110">After a job is deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d326-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5d326-111">Next steps</span></span>

* [<span data-ttu-id="5d326-112">Usando a API REST do serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="5d326-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
