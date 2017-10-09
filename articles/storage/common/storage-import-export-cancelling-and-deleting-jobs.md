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
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="ce5b5-103">Cancelando e excluindo trabalhos de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="ce5b5-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="ce5b5-104">toorequest que um trabalho cancelado antes que ele está em Olá `Packaging` estado, chamada hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operação e conjunto Olá `CancelRequested` elemento muito`true`.</span><span class="sxs-lookup"><span data-stu-id="ce5b5-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="ce5b5-105">Olá trabalho for cancelado em uma base de melhor esforço.</span><span class="sxs-lookup"><span data-stu-id="ce5b5-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="ce5b5-106">Se as unidades estiverem no processo de saudação de transferência de dados, dados podem continuar toobe transferido mesmo depois que o cancelamento foi solicitado.</span><span class="sxs-lookup"><span data-stu-id="ce5b5-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="ce5b5-107">Um trabalho cancelado é movido toohello `Completed` de estado e são mantidas por 90 dias, no ponto em que ele é excluído.</span><span class="sxs-lookup"><span data-stu-id="ce5b5-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="ce5b5-108">toodelete um trabalho, chamada hello [excluir trabalho](/rest/api/storageimportexport/jobs#Jobs_Delete) operação antes que o trabalho Olá tiver sido enviado (ou seja, enquanto o trabalho de saudação estiver no hello `Creating` estado).</span><span class="sxs-lookup"><span data-stu-id="ce5b5-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="ce5b5-109">Você também pode excluir um trabalho quando ele estiver em Olá `Completed` estado.</span><span class="sxs-lookup"><span data-stu-id="ce5b5-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="ce5b5-110">Depois que um trabalho é excluído, suas informações e status não são mais acessíveis por meio da API REST de saudação ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce5b5-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce5b5-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce5b5-111">Next steps</span></span>

* [<span data-ttu-id="ce5b5-112">Usando a API REST do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="ce5b5-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
