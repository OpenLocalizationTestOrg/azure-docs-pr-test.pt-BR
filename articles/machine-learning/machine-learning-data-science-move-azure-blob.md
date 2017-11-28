---
title: aaaMove tooand de dados do armazenamento de BLOBs do Azure | Microsoft Docs
description: Mover dados tooand do armazenamento de BLOBs do Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a><span data-ttu-id="5dcc9-103">Mover dados tooand do armazenamento de BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="5dcc9-103">Move data tooand from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="5dcc9-104">O melhor método para você depende de seu cenário.</span><span class="sxs-lookup"><span data-stu-id="5dcc9-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="5dcc9-105">Olá [cenários para análises avançadas no aprendizado de máquina do Azure](machine-learning-data-science-plan-sample-scenarios.md) artigo o ajudará a determinar os recursos de saudação é necessário para uma variedade de fluxos de trabalho de ciência de dados usados em Olá avançado do processo de análise.</span><span class="sxs-lookup"><span data-stu-id="5dcc9-105">hello [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine hello resources you need for a variety of data science workflows used in hello advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="5dcc9-106">Para um armazenamento de blob tooAzure introdução completa, consulte muito[Noções básicas de Blob do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e muito[serviço Blob do Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="5dcc9-106">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="5dcc9-107">Como alternativa, você pode usar o [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) para:</span><span class="sxs-lookup"><span data-stu-id="5dcc9-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="5dcc9-108">criar e agendar um pipeline que baixa os dados do Armazenamento de Blobs do Azure,</span><span class="sxs-lookup"><span data-stu-id="5dcc9-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="5dcc9-109">passe-tooa publicado serviço da web de aprendizado de máquina do Azure,</span><span class="sxs-lookup"><span data-stu-id="5dcc9-109">pass it tooa published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="5dcc9-110">receber os resultados de análise preditiva Olá, e</span><span class="sxs-lookup"><span data-stu-id="5dcc9-110">receive hello predictive analytics results, and</span></span> 
* <span data-ttu-id="5dcc9-111">carregar Olá toostorage de resultados.</span><span class="sxs-lookup"><span data-stu-id="5dcc9-111">upload hello results toostorage.</span></span> 

<span data-ttu-id="5dcc9-112">Para obter mais informações, consulte [Criar pipelines preditivos usando o Azure Data Factory e o Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="5dcc9-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dcc9-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5dcc9-113">Prerequisites</span></span>
<span data-ttu-id="5dcc9-114">Este documento assume que você tenha uma assinatura do Azure, uma conta de armazenamento e chave de armazenamento correspondente Olá para essa conta.</span><span class="sxs-lookup"><span data-stu-id="5dcc9-114">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="5dcc9-115">Antes de carregar/baixar os dados, você deve conhecer o nome e a chave da sua conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dcc9-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="5dcc9-116">tooset uma assinatura do Azure, consulte [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5dcc9-116">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5dcc9-117">Para obter instruções sobre como criar uma conta de armazenamento e obter informações sobre conta e chave, consulte [Sobre contas do armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5dcc9-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

