---
title: "aaaClient bibliotecas necessárias para conectar o tooAzure Analysis Services | Microsoft Docs"
description: "Descreve as bibliotecas de cliente necessárias para aplicativos e ferramentas de cliente tooconnect Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="d8b7d-103">Bibliotecas de cliente para conectar o tooAzure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="d8b7d-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="d8b7d-104">Bibliotecas de cliente são necessárias para aplicativos cliente e servidores de serviços de tooAnalysis de tooconnect de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="d8b7d-105">O Analysis Services utiliza três bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="d8b7d-106">O ADOMD.NET e o AMO (Objetos de Gerenciamento do Analysis Services) são bibliotecas de cliente gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="d8b7d-107">provedor de OLE DB do Analysis Services da saudação (MSOLAP DLL) é uma biblioteca do native client.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="d8b7d-108">Normalmente, todos os três são instalados em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="d8b7d-109">Serviços de análise do Azure requer versões mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="d8b7d-110">Os aplicativos cliente da Microsoft, como o Power BI Desktop e o Excel, instalam as três bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="d8b7d-111">No entanto, dependendo da versão de saudação ou a frequência de atualizações, bibliotecas de cliente não podem ser versões mais recentes de saudação exigidas pelo Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="d8b7d-112">Olá mesmo se aplica toocustom aplicativos ou outras interfaces, como AsCmd, TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="d8b7d-113">Esses aplicativos exigem a instalação manual de bibliotecas de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="d8b7d-114">bibliotecas de saudação do cliente para instalação manual estão incluídas nos pacotes de recursos do SQL Server como pacotes de distribuição.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="d8b7d-115">No entanto, essas bibliotecas de cliente são toohello empatados versão do SQL Server e não podem ser hello mais recente.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="d8b7d-116">Bibliotecas de cliente para conexões de cliente são diferentes das tooconnect necessária de provedores de dados de uma fonte de dados do Azure Analysis Services server tooa.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="d8b7d-117">toolearn mais informações sobre conexões de fonte de dados, consulte [conexões de fonte de dados](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="d8b7d-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="d8b7d-118">Baixar Olá bibliotecas de cliente mais recentes</span><span class="sxs-lookup"><span data-stu-id="d8b7d-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="d8b7d-119">Use Olá bibliotecas de cliente a seguir se você estiver em um ambiente de produção e exige as versões de lançamento e suportadas completos.</span><span class="sxs-lookup"><span data-stu-id="d8b7d-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="d8b7d-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="d8b7d-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="d8b7d-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="d8b7d-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="d8b7d-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="d8b7d-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="d8b7d-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="d8b7d-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="d8b7d-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8b7d-124">Next steps</span></span>
<span data-ttu-id="d8b7d-125">[Conectar com Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="d8b7d-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="d8b7d-126">Conectar com o Power BI</span><span class="sxs-lookup"><span data-stu-id="d8b7d-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
