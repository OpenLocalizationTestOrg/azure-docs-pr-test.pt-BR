---
title: "Usando a Ferramenta de Importação/Exportação do Azure – v1 | Microsoft Docs"
description: "Saiba como usar a Ferramenta de Importação/Exportação a fim de preparar os discos rígidos para um trabalho de importação, bem como para reparar um trabalho de importação ou exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/15/2017
ms.author: muralikk
ms.openlocfilehash: 67bdfa8c2cd0f8314c82e2b334a3fa3a5c520c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-tool-v1"></a><span data-ttu-id="9ed91-103">Usando a Ferramenta de Importação/Exportação do Azure (v1)</span><span class="sxs-lookup"><span data-stu-id="9ed91-103">Using the Azure Import/Export Tool (v1)</span></span>

<span data-ttu-id="9ed91-104">A Ferramenta de Importação/Exportação do Azure (WAImportExport.exe) é usada para criar e gerenciar trabalhos do serviço de Importação/Exportação do Azure, permitindo a transferência de grandes quantidades de dados para dentro ou fora do Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed91-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="9ed91-105">Esta documentação refere-se à v1 da Ferramenta de Importação/Exportação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed91-105">This documentation is for v1 of the Azure Import/Export Tool.</span></span> <span data-ttu-id="9ed91-106">Para obter informações sobre como usar a versão mais recente da ferramenta, consulte [Using the Azure Import/Export Tool](storage-import-export-tool-how-to.md) (Usando a Ferramenta de Importação/Exportação do Azure).</span><span class="sxs-lookup"><span data-stu-id="9ed91-106">For information about using the most recent version of the tool, please see [Using the Azure Import/Export Tool](storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="9ed91-107">Nesses artigos, você verá como usar a ferramenta para fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9ed91-107">In these articles, you will see how to use the tool to do the following:</span></span>

- <span data-ttu-id="9ed91-108">Instalar e configurar a Ferramenta de Importação/Exportação.</span><span class="sxs-lookup"><span data-stu-id="9ed91-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="9ed91-109">Preparar os discos rígidos para um trabalho em que os dados são importados das unidades para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed91-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="9ed91-110">Examinar o status de um trabalho com Arquivos de Log de Cópia.</span><span class="sxs-lookup"><span data-stu-id="9ed91-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="9ed91-111">Reparar um trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="9ed91-111">Repair an import job.</span></span> 
- <span data-ttu-id="9ed91-112">Reparar um trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="9ed91-112">Repair an export job.</span></span> 
- <span data-ttu-id="9ed91-113">Solucionar problemas da Ferramenta de Importação/Exportação do Azure, caso você teve um problema durante o processo.</span><span class="sxs-lookup"><span data-stu-id="9ed91-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9ed91-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9ed91-114">Next steps</span></span>

* [<span data-ttu-id="9ed91-115">Configuração da ferramenta WAImportExport</span><span class="sxs-lookup"><span data-stu-id="9ed91-115">Setting up the WAImportExport tool</span></span>](storage-import-export-tool-how-to.md)