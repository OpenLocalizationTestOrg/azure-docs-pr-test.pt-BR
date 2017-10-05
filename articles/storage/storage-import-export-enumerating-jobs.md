---
title: "Listar todos os trabalhos de Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba como listar todos os trabalhos do serviço de Importação/Exportação do Azure em uma assinatura."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f2e619be-1bbd-4a54-9472-9e2f70a83b64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1977bfc0e516088310f45ecdd960287eeed2c2d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enumerating-jobs-in-the-azure-importexport-service"></a><span data-ttu-id="50033-103">Enumerando trabalhos no serviço de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="50033-103">Enumerating jobs in the Azure Import/Export service</span></span>
<span data-ttu-id="50033-104">Para enumerar todos os trabalhos em uma assinatura, chame a operação [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List).</span><span class="sxs-lookup"><span data-stu-id="50033-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="50033-105">`List Jobs` retorna uma lista de trabalhos, bem como os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="50033-105">`List Jobs` returns a list of jobs as well as the following attributes:</span></span>

-   <span data-ttu-id="50033-106">O tipo de trabalho (Importação ou Exportação)</span><span class="sxs-lookup"><span data-stu-id="50033-106">The type of job (Import or Export)</span></span>

-   <span data-ttu-id="50033-107">O estado atual do trabalho</span><span class="sxs-lookup"><span data-stu-id="50033-107">The current job state</span></span>

-   <span data-ttu-id="50033-108">A conta de armazenamento associada ao trabalho</span><span class="sxs-lookup"><span data-stu-id="50033-108">The job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="50033-109">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="50033-109">Next steps</span></span>

* [<span data-ttu-id="50033-110">Usando a API REST do serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="50033-110">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
