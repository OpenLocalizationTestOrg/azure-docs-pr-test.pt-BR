---
title: "O que aconteceu ao meu projeto do serviço de nuvem? | Microsoft Docs"
description: "Descreve o que acontece em um projeto de serviços de nuvem após a conexão a uma conta de armazenamento do Azure usando os serviços conectados do Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 4c9de56f6daf07097c0f593db37d14dce3bce05f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="26c9b-104">O que aconteceu ao meu projeto dos serviços de nuvem (serviço conectado do Armazenamento do Azure do Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="26c9b-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="26c9b-105">Referências adicionadas</span><span class="sxs-lookup"><span data-stu-id="26c9b-105">References added</span></span>
<span data-ttu-id="26c9b-106">O pacote do NuGet do armazenamento do Azure foi adicionado ao seu projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26c9b-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="26c9b-107">Esse pacote adiciona as referências de .NET a seguir:</span><span class="sxs-lookup"><span data-stu-id="26c9b-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="26c9b-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="26c9b-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="26c9b-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="26c9b-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="26c9b-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="26c9b-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="26c9b-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="26c9b-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="26c9b-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="26c9b-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="26c9b-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="26c9b-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="26c9b-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="26c9b-114">**System.Data**</span></span>
* <span data-ttu-id="26c9b-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="26c9b-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="26c9b-116">Cadeia de conexão do Armazenamento do Azure adicionada</span><span class="sxs-lookup"><span data-stu-id="26c9b-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="26c9b-117">Elementos foram criados com a cadeia de conexão e chave da conta de armazenamento selecionada.</span><span class="sxs-lookup"><span data-stu-id="26c9b-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="26c9b-118">Foram realizadas modificações nos seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="26c9b-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="26c9b-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="26c9b-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="26c9b-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="26c9b-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="26c9b-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="26c9b-121">**ServiceConfiguration.Local.cscfg**</span></span>

