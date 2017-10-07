---
title: "aaaCancel e excluir um trabalho de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toocancel e excluir trabalhos para Olá serviço de importação/exportação do Microsoft Azure."
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
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="09d48-103">Cancelando e excluindo trabalhos de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="09d48-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="09d48-104">Você pode solicitar que um trabalho seja cancelado antes de ser em Olá `Packaging` estado pela chamada hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) Olá operação e configuração `CancelRequested` elemento muito`true`.</span><span class="sxs-lookup"><span data-stu-id="09d48-104">You can request that a job be cancelled before it is in hello `Packaging` state by calling hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="09d48-105">Olá trabalho será cancelado em uma base de melhor esforço.</span><span class="sxs-lookup"><span data-stu-id="09d48-105">hello job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="09d48-106">Se as unidades estiverem no processo de saudação de transferência de dados, dados podem continuar toobe transferido mesmo depois que o cancelamento foi solicitado.</span><span class="sxs-lookup"><span data-stu-id="09d48-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="09d48-107">Um trabalho cancelado moverá toohello `Completed` de estado e mantidos por 90 dias, no ponto em que ela será excluída.</span><span class="sxs-lookup"><span data-stu-id="09d48-107">A cancelled job will move toohello `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="09d48-108">toodelete um trabalho, chamada hello [excluir trabalho](/rest/api/storageimportexport/jobs#Jobs_Delete) operação antes que o trabalho Olá tiver sido enviado (*ou seja,*, enquanto o trabalho de saudação em hello `Creating` estado).</span><span class="sxs-lookup"><span data-stu-id="09d48-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (*i.e.*, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="09d48-109">Você também pode excluir um trabalho quando ele estiver em Olá `Completed` estado.</span><span class="sxs-lookup"><span data-stu-id="09d48-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="09d48-110">Após a exclusão de um trabalho, suas informações e status não são mais acessíveis por meio da API REST de saudação ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="09d48-110">After a job has been deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09d48-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09d48-111">Next steps</span></span>

* [<span data-ttu-id="09d48-112">Usando a API REST do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="09d48-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
