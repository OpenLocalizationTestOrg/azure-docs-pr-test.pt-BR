---
title: "O que aconteceu com meu projeto do ASP.NET 5 (serviços conectados do Visual Studio) | Microsoft Docs"
description: "Descreve o que acontece após a conexão a uma conta de armazenamento do Azure em um projeto do ASP.NET 5 do Visual Studio usando os serviços conectados do Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2a25c24fd7625374d269622a805f386fcd52bb5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="cbb95-103">O que aconteceu com meu projeto do ASP.NET 5 (serviços conectados do Armazenamento do Azure do Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="cbb95-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="cbb95-104">Referências adicionadas</span><span class="sxs-lookup"><span data-stu-id="cbb95-104">References added</span></span>
<span data-ttu-id="cbb95-105">O pacote do NuGet do armazenamento do Azure foi adicionado ao seu projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cbb95-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="cbb95-106">Esse pacote adiciona as referências de .NET a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbb95-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="cbb95-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="cbb95-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="cbb95-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="cbb95-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="cbb95-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="cbb95-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="cbb95-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="cbb95-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="cbb95-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="cbb95-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="cbb95-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="cbb95-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="cbb95-113">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="cbb95-113">**System.Data**</span></span>
* <span data-ttu-id="cbb95-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="cbb95-114">**System.Spatial**</span></span>

<span data-ttu-id="cbb95-115">Além disso, o pacote NuGet **Microsoft.Framework.Configuration.Json** foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="cbb95-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="cbb95-116">Cadeia de conexão do Armazenamento do Azure adicionada</span><span class="sxs-lookup"><span data-stu-id="cbb95-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="cbb95-117">No arquivo config.json do seu projeto, foi criado um elemento com a cadeia de conexão e chave da conta de armazenamento selecionada.</span><span class="sxs-lookup"><span data-stu-id="cbb95-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="cbb95-118">Para obter mais informações, consulte [ASP.NET 5](http://www.asp.net/vnext).</span><span class="sxs-lookup"><span data-stu-id="cbb95-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>

