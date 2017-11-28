---
title: "O que aconteceu ao meu projeto do WebJob (serviço conectado do Armazenamento do Azure do Visual Studio)? | Microsoft Docs"
description: "Descreve o que acontece em um projeto do Azure WebJob após a conexão a uma conta de armazenamento usando os serviços conectados do Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3b28ddeadc87937941d60b16fae817e59a220b22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="bf983-104">O que aconteceu ao meu projeto do WebJob (serviço conectado do Armazenamento do Azure do Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="bf983-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="bf983-105">Referências adicionadas</span><span class="sxs-lookup"><span data-stu-id="bf983-105">References Added</span></span>
<span data-ttu-id="bf983-106">O pacote do NuGet do Armazenamento do Azure foi adicionado ao seu projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf983-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="bf983-107">Esse pacote adiciona as referências de .NET a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf983-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="bf983-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="bf983-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="bf983-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="bf983-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="bf983-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="bf983-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="bf983-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="bf983-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="bf983-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="bf983-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="bf983-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="bf983-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="bf983-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="bf983-114">**System.Data**</span></span>
* <span data-ttu-id="bf983-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="bf983-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="bf983-116">Cadeia de conexão do Armazenamento do Azure adicionada</span><span class="sxs-lookup"><span data-stu-id="bf983-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="bf983-117">No arquivo App.config do seu projeto, as entradas **AzureWebJobsStorage** e **AzureWebJobsDashboard** foram atualizadas com a cadeia de conexão e a chave da conta de armazenamento selecionada.</span><span class="sxs-lookup"><span data-stu-id="bf983-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="bf983-118">Para sabe r mais, consulte [Recursos de documentação de WebJobs do Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="bf983-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

