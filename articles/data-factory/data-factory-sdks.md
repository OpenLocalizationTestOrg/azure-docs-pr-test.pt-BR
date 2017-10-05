---
title: "Referência do desenvolvedor da Azure Data Factory"
description: Aprenda maneiras diferentes de criar, monitorar e gerenciar data factories do Azure
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: dc752fa1-a6c3-4753-904e-9f32d0a940b7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2017
ms.author: spelluru
redirect_url: https://azure.microsoft.com/services/data-factory/
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: e0f6c078b60df6bb7381d066bebb3e400b3b97ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory-developer-reference"></a><span data-ttu-id="61a3b-103">Referência do desenvolvedor da Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="61a3b-103">Azure Data Factory Developer Reference</span></span>
<span data-ttu-id="61a3b-104">Você pode criar, monitorar e gerenciar as fábricas usando o Portal do Azure, Azure PowerShell, Biblioteca de Classes .NET ou API REST.</span><span class="sxs-lookup"><span data-stu-id="61a3b-104">You can create, monitor, and manage the factories using either Azure portal, Azure PowerShell, .NET Class Library, or REST API.</span></span>

| <span data-ttu-id="61a3b-105">Método</span><span class="sxs-lookup"><span data-stu-id="61a3b-105">Method</span></span> | <span data-ttu-id="61a3b-106">Local do recurso</span><span class="sxs-lookup"><span data-stu-id="61a3b-106">Resource Location</span></span> | <span data-ttu-id="61a3b-107">Referências para o desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="61a3b-107">Developer References</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61a3b-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="61a3b-108">Azure portal</span></span> |[<span data-ttu-id="61a3b-109">https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="61a3b-109">https://portal.azure.com/</span></span>](https://portal.azure.com) |[<span data-ttu-id="61a3b-110">Introdução ao Azure Data Factory (Portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="61a3b-110">Get started with Azure Data Factory (Azure portal)</span></span>](data-factory-build-your-first-pipeline-using-editor.md) |
| <span data-ttu-id="61a3b-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61a3b-111">Azure PowerShell</span></span> |<span data-ttu-id="61a3b-112">Baixe o [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="61a3b-112">Download the latest [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span></span> |[<span data-ttu-id="61a3b-113">Referência de cmdlet</span><span class="sxs-lookup"><span data-stu-id="61a3b-113">Cmdlet reference</span></span>](https://msdn.microsoft.com/library/dn820234.aspx) |
| <span data-ttu-id="61a3b-114">Biblioteca de classes do .NET</span><span class="sxs-lookup"><span data-stu-id="61a3b-114">.NET Class Library</span></span> |<span data-ttu-id="61a3b-115">O SDK .NET do Azure Data Factory permite que você crie, monitore e gerencie as data factories do Azure e estenda o Data Factory usando uma atividade .NET.</span><span class="sxs-lookup"><span data-stu-id="61a3b-115">The Azure Data Factory .NET SDK enables you to create, monitor, and manage Azure data factories and extend Data Factory using a .NET activity.</span></span> <span data-ttu-id="61a3b-116">Confira os artigos [Usar atividades personalizadas em um pipeline do Azure Data Factory](data-factory-use-custom-activities.md) e [Criar, monitorar e gerenciar data factories do Azure usando o SDK do .NET da Data Factory](data-factory-create-data-factories-programmatically.md) para ajudá-lo a começar.</span><span class="sxs-lookup"><span data-stu-id="61a3b-116">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) and [Create, monitor, and manage Azure data factories using Data Factory .NET SDK](data-factory-create-data-factories-programmatically.md) articles to help you get started.</span></span><br/><br/><span data-ttu-id="61a3b-117"><b>Baixando o Nuget mais recente</b></span><span class="sxs-lookup"><span data-stu-id="61a3b-117"><b>Downloading the latest Nuget</b></span></span><br/><span data-ttu-id="61a3b-118">Você pode baixar o pacote mais recente do Nuget da Biblioteca de Gerenciamento do Azure Data Factory em [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span><span class="sxs-lookup"><span data-stu-id="61a3b-118">You can download the latest Azure Data Factory Management Library Nuget package from: [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span></span><br/><br/><span data-ttu-id="61a3b-119">**Usando o Console do Gerenciador de Pacotes no Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="61a3b-119">**Using Package Manager Console in Visual Studio**</span></span><br/><span data-ttu-id="61a3b-120">Você pode executar o seguinte comando no Console do Gerenciador de Pacotes do Visual Studio para obter a biblioteca de gerenciamento mais recente do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="61a3b-120">You can run the following command in Visual Studio’s Package Manager Console to get the latest Azure Data Factory Management Library</span></span><br/><br/><span data-ttu-id="61a3b-121">Install-Package Microsoft.Azure.Management.DataFactories</span><span class="sxs-lookup"><span data-stu-id="61a3b-121">Install-Package Microsoft.Azure.Management.DataFactories</span></span> |[<span data-ttu-id="61a3b-122">Referência do SDK .NET</span><span class="sxs-lookup"><span data-stu-id="61a3b-122">.NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt415893.aspx) |
| <span data-ttu-id="61a3b-123">API REST</span><span class="sxs-lookup"><span data-stu-id="61a3b-123">REST API</span></span> |<span data-ttu-id="61a3b-124">Você pode usar a API REST do Data Factory para criar, monitorar e gerenciar data factories do Azure.</span><span class="sxs-lookup"><span data-stu-id="61a3b-124">You can use the Data Factory REST API to create, monitor, and manage Azure data factories.</span></span> |[<span data-ttu-id="61a3b-125">referência da API REST (a página pode estar em inglês)</span><span class="sxs-lookup"><span data-stu-id="61a3b-125">REST API Reference</span></span>](https://msdn.microsoft.com/library/dn906738.aspx) |

