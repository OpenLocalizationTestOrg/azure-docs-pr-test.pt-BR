---
title: "O que aconteceu ao meu projeto do WebJob (serviço conectado do Armazenamento do Azure do Visual Studio)? | Microsoft Docs"
description: "Descreve o que acontece em um projeto do Azure WebJob após a conexão a uma conta de armazenamento usando os serviços conectados do Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8891685a99c5ba366b74af0a21396d4a5e499835
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="0cc72-104">O que aconteceu ao meu projeto do WebJob (serviço conectado do Armazenamento do Azure do Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="0cc72-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="0cc72-105">Referências adicionadas</span><span class="sxs-lookup"><span data-stu-id="0cc72-105">References Added</span></span>
<span data-ttu-id="0cc72-106">O pacote do NuGet do Armazenamento do Azure foi adicionado ao seu projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0cc72-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="0cc72-107">Esse pacote adiciona as referências de .NET a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cc72-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="0cc72-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="0cc72-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="0cc72-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="0cc72-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="0cc72-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="0cc72-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="0cc72-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="0cc72-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="0cc72-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="0cc72-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="0cc72-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="0cc72-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="0cc72-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="0cc72-114">**System.Data**</span></span>
* <span data-ttu-id="0cc72-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="0cc72-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="0cc72-116">Cadeia de conexão do Armazenamento do Azure adicionada</span><span class="sxs-lookup"><span data-stu-id="0cc72-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="0cc72-117">No arquivo App.config do seu projeto, as entradas **AzureWebJobsStorage** e **AzureWebJobsDashboard** foram atualizadas com a cadeia de conexão e a chave da conta de armazenamento selecionada.</span><span class="sxs-lookup"><span data-stu-id="0cc72-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="0cc72-118">Para sabe r mais, consulte [Recursos de documentação de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="0cc72-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

