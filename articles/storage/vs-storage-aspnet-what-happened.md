---
title: O que aconteceu ao meu projeto do ASP.NET? | Microsoft Docs
description: "Descreve o que acontece após a adição do Armazenamento do Azure a um projeto do ASP.NET usando os serviços conectados do Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: e1fe1b6d-4e3d-476d-8b2f-f7ade050515e
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e2cdc2ff4df85f0224352bd32a3ec62480c3e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-aspnet-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="8fdc0-104">O que aconteceu ao meu projeto do ASP.NET (serviço conectado do Armazenamento do Azure do Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="8fdc0-104">What happened to my ASP.NET project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="8fdc0-105">Referências adicionadas</span><span class="sxs-lookup"><span data-stu-id="8fdc0-105">References added</span></span>
<span data-ttu-id="8fdc0-106">O pacote do NuGet do armazenamento do Azure foi adicionado ao seu projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8fdc0-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="8fdc0-107">Esse pacote adiciona as referências de .NET a seguir:</span><span class="sxs-lookup"><span data-stu-id="8fdc0-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="8fdc0-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="8fdc0-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="8fdc0-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="8fdc0-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="8fdc0-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="8fdc0-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="8fdc0-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="8fdc0-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="8fdc0-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="8fdc0-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="8fdc0-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="8fdc0-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="8fdc0-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="8fdc0-114">**System.Data**</span></span>
* <span data-ttu-id="8fdc0-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="8fdc0-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="8fdc0-116">Cadeia de conexão do Armazenamento do Azure adicionada</span><span class="sxs-lookup"><span data-stu-id="8fdc0-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="8fdc0-117">No arquivo web.config do seu projeto, foi criado um elemento com a cadeia de conexão e chave da conta de armazenamento selecionada.</span><span class="sxs-lookup"><span data-stu-id="8fdc0-117">In the web.config file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="8fdc0-118">Para obter mais informações, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="8fdc0-118">For more information, see [ASP.NET](http://www.asp.net).</span></span>

