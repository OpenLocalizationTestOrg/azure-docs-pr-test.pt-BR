---
title: "O que aconteceu ao meu projeto do serviço de nuvem? | Microsoft Docs"
description: "Descreve o que acontece em um projeto de serviços de nuvem após a conexão a uma conta de armazenamento do Azure usando os serviços conectados do Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4e0d4864c2fad624fbde39080146dc62ebebff09
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="299bc-104">O que aconteceu ao meu projeto dos serviços de nuvem (serviço conectado do Armazenamento do Azure do Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="299bc-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="299bc-105">Referências adicionadas</span><span class="sxs-lookup"><span data-stu-id="299bc-105">References added</span></span>
<span data-ttu-id="299bc-106">O pacote do NuGet do armazenamento do Azure foi adicionado ao seu projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="299bc-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="299bc-107">Esse pacote adiciona as referências de .NET a seguir:</span><span class="sxs-lookup"><span data-stu-id="299bc-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="299bc-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="299bc-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="299bc-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="299bc-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="299bc-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="299bc-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="299bc-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="299bc-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="299bc-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="299bc-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="299bc-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="299bc-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="299bc-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="299bc-114">**System.Data**</span></span>
* <span data-ttu-id="299bc-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="299bc-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="299bc-116">Cadeia de conexão do Armazenamento do Azure adicionada</span><span class="sxs-lookup"><span data-stu-id="299bc-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="299bc-117">Elementos foram criados com a cadeia de conexão e chave da conta de armazenamento selecionada.</span><span class="sxs-lookup"><span data-stu-id="299bc-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="299bc-118">Foram realizadas modificações nos seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="299bc-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="299bc-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="299bc-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="299bc-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="299bc-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="299bc-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="299bc-121">**ServiceConfiguration.Local.cscfg**</span></span>

