---
title: "Bibliotecas de cliente necessárias para conectar-se ao Azure Analysis Services | Microsoft Docs"
description: "Descreve as bibliotecas de cliente necessárias às ferramentas e ao aplicativos cliente para conectar o Azure Analysis Services"
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
ms.openlocfilehash: a96e7fe671dc051da35168fa7b49ecba53b4c4a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a><span data-ttu-id="10658-103">Bibliotecas de cliente para conectar-se ao Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="10658-103">Client libraries for connecting to Azure Analysis Services</span></span>

<span data-ttu-id="10658-104">Bibliotecas de cliente são necessárias para que ferramentas e aplicativos cliente se conectem aos servidores do Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="10658-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span></span> 

<span data-ttu-id="10658-105">O Analysis Services utiliza três bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="10658-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="10658-106">O ADOMD.NET e o AMO (Objetos de Gerenciamento do Analysis Services) são bibliotecas de cliente gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="10658-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="10658-107">O provedor OLE DB do Analysis Services (MSOLAP DLL) é uma biblioteca de cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="10658-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="10658-108">Normalmente, as três bibliotecas são instaladas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="10658-108">Typically, all three are installed at the same time.</span></span> <span data-ttu-id="10658-109">O Azure Analysis Services exige as versões mais recentes.</span><span class="sxs-lookup"><span data-stu-id="10658-109">Azure Analysis Services requires the latest versions.</span></span> 

<span data-ttu-id="10658-110">Os aplicativos cliente da Microsoft, como o Power BI Desktop e o Excel, instalam as três bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="10658-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="10658-111">Contudo, dependendo da versão ou da frequência de atualizações, as bibliotecas de cliente podem não ser as versões mais recentes exigidas pelo Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="10658-111">However, depending on the version or frequency of updates, client libraries may not be the latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="10658-112">O mesmo se aplica a aplicativos personalizados ou outras interfaces, como AsCmd, TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="10658-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="10658-113">Esses aplicativos exigem a instalação manual das bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="10658-113">These applications require manually installing the libraries.</span></span> <span data-ttu-id="10658-114">As bibliotecas de cliente para instalação manual estão incluídas nos pacotes de recursos do SQL Server como pacotes distribuíveis.</span><span class="sxs-lookup"><span data-stu-id="10658-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="10658-115">No entanto, essas bibliotecas de cliente estão vinculadas à versão do SQL Server e talvez não sejam as mais recentes.</span><span class="sxs-lookup"><span data-stu-id="10658-115">However, these client libraries are tied to the SQL Server version and may not be the latest.</span></span>  

<span data-ttu-id="10658-116">As bibliotecas de cliente para conexões de cliente são diferentes dos provedores de dados necessários para se conectar de um servidor Azure Analysis Services a uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="10658-116">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span></span> <span data-ttu-id="10658-117">Para saber mais sobre conexões de fonte de dados, confira [Conexões de fonte de dados](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="10658-117">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-the-latest-client-libraries"></a><span data-ttu-id="10658-118">Baixar as bibliotecas de cliente mais recentes</span><span class="sxs-lookup"><span data-stu-id="10658-118">Download the latest client libraries</span></span>  
<span data-ttu-id="10658-119">Use as bibliotecas de cliente a seguir se estiver em um ambiente de produção e precisar de versões totalmente liberadas e com suporte completo.</span><span class="sxs-lookup"><span data-stu-id="10658-119">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="10658-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="10658-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="10658-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="10658-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="10658-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="10658-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="10658-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="10658-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="10658-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10658-124">Next steps</span></span>
<span data-ttu-id="10658-125">[Conectar com Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="10658-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="10658-126">Conectar com o Power BI</span><span class="sxs-lookup"><span data-stu-id="10658-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
