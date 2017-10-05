---
title: Mover dados de e para o Armazenamento de Blobs do Azure | Microsoft Docs
description: Mover dados de e para o Armazenamento de Blobs do Azure
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
ms.openlocfilehash: d9a626cccd3cdfcdc85f000bd3192aef2881e9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage"></a><span data-ttu-id="6d593-103">Mover dados para e do Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="6d593-103">Move data to and from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this to separate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="6d593-104">O melhor método para você depende de seu cenário.</span><span class="sxs-lookup"><span data-stu-id="6d593-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="6d593-105">O artigo [Cenários para análises avançadas no Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) ajudará você a determinar os recursos necessários para uma variedade de fluxos de trabalho de ciência de dados usados no processo de análise avançada.</span><span class="sxs-lookup"><span data-stu-id="6d593-105">The [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="6d593-106">Para obter uma introdução completa ao Armazenamento de Blobs do Azure, confira [Noções básicas do Serviço Blob do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e [Serviço Blob do Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d593-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="6d593-107">Como alternativa, você pode usar o [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) para:</span><span class="sxs-lookup"><span data-stu-id="6d593-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="6d593-108">criar e agendar um pipeline que baixa os dados do Armazenamento de Blobs do Azure,</span><span class="sxs-lookup"><span data-stu-id="6d593-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="6d593-109">passá-lo para um serviço Web publicado do Azure Machine Learning,</span><span class="sxs-lookup"><span data-stu-id="6d593-109">pass it to a published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="6d593-110">receber os resultados da análise preditiva, e</span><span class="sxs-lookup"><span data-stu-id="6d593-110">receive the predictive analytics results, and</span></span> 
* <span data-ttu-id="6d593-111">carrega os resultados no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d593-111">upload the results to storage.</span></span> 

<span data-ttu-id="6d593-112">Para obter mais informações, consulte [Criar pipelines preditivos usando o Azure Data Factory e o Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="6d593-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d593-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6d593-113">Prerequisites</span></span>
<span data-ttu-id="6d593-114">Este documento pressupõe que você tenha uma assinatura, uma conta de armazenamento do Azure e a chave de armazenamento correspondente dessa conta.</span><span class="sxs-lookup"><span data-stu-id="6d593-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="6d593-115">Antes de carregar/baixar os dados, você deve conhecer o nome e a chave da sua conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d593-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="6d593-116">Para configurar uma assinatura do Azure, consulte [Avaliação gratuita de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d593-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6d593-117">Para obter instruções sobre como criar uma conta de armazenamento e para obter informações sobre conta e chave, consulte [Sobre contas do armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6d593-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

