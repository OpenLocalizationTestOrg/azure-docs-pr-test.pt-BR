---
title: "Repositórios de Registro de contêiner do Azure | Microsoft Docs"
description: "Como usar os repositórios de Registro de contêiner do Azure para imagens do Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="5d61e-103">Repositórios de Registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="5d61e-103">Azure container registry repositories</span></span>

<span data-ttu-id="5d61e-104">Os Registros de Contêiner do Azure são compatíveis com uma variedade de serviços e orquestradores.</span><span class="sxs-lookup"><span data-stu-id="5d61e-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="5d61e-105">Para tornar mais fácil de controlar os serviços de origem e os agentes dos quais o ACR é usado, começamos usando o campo de cabeçalho do Docker no arquivo Docker.config.</span><span class="sxs-lookup"><span data-stu-id="5d61e-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="5d61e-106">Exibindo repositórios no Portal</span><span class="sxs-lookup"><span data-stu-id="5d61e-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="5d61e-107">Os cabeçalhos do ACR seguem o formato:</span><span class="sxs-lookup"><span data-stu-id="5d61e-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="5d61e-108">Nuvem: Azure, Azure Stack ou outras nuvens do Azure específicas do país ou do governo.</span><span class="sxs-lookup"><span data-stu-id="5d61e-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="5d61e-109">Embora no momento não haja suporte para o Azure Stack e nuvens do governo, este parâmetro habilita suporte futuro.</span><span class="sxs-lookup"><span data-stu-id="5d61e-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="5d61e-110">Serviço: nome do serviço.</span><span class="sxs-lookup"><span data-stu-id="5d61e-110">Service: name of the service.</span></span>
* <span data-ttu-id="5d61e-111">Optionalservicename: parâmetro opcional para serviços com subserviços ou para especificar uma SKU (ex: aplicativos Web correspondem a Azure/app-service/web-apps).</span><span class="sxs-lookup"><span data-stu-id="5d61e-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="5d61e-112">Orquestradores e serviços de parceiro são incentivados a usar valores de cabeçalho específicos para ajudar em nossa telemetria.</span><span class="sxs-lookup"><span data-stu-id="5d61e-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="5d61e-113">Os usuários também podem modificar o valor passado para o cabeçalho, se desejarem.</span><span class="sxs-lookup"><span data-stu-id="5d61e-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="5d61e-114">Os valores que desejamos que os parceiros do ACR usem para preencher o campo "X-Meta-Origem-Cliente" estão abaixo:</span><span class="sxs-lookup"><span data-stu-id="5d61e-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="5d61e-115">Nome do Serviço</span><span class="sxs-lookup"><span data-stu-id="5d61e-115">Service Name</span></span>              | <span data-ttu-id="5d61e-116">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="5d61e-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="5d61e-117">Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="5d61e-117">Azure Container Service</span></span>   | <span data-ttu-id="5d61e-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="5d61e-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="5d61e-119">Serviço de Aplicativo – Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="5d61e-119">App Service - Web Apps</span></span>    | <span data-ttu-id="5d61e-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="5d61e-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="5d61e-121">Serviço de Aplicativo – Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="5d61e-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="5d61e-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="5d61e-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="5d61e-123">Batch</span><span class="sxs-lookup"><span data-stu-id="5d61e-123">Batch</span></span>                     | <span data-ttu-id="5d61e-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="5d61e-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="5d61e-125">Console de nuvem</span><span class="sxs-lookup"><span data-stu-id="5d61e-125">Cloud Console</span></span>             | <span data-ttu-id="5d61e-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="5d61e-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="5d61e-127">Funções</span><span class="sxs-lookup"><span data-stu-id="5d61e-127">Functions</span></span>                 | <span data-ttu-id="5d61e-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="5d61e-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="5d61e-129">Internet das Coisas – Hub</span><span class="sxs-lookup"><span data-stu-id="5d61e-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="5d61e-130">hub/de iot do Azure</span><span class="sxs-lookup"><span data-stu-id="5d61e-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="5d61e-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="5d61e-131">HDInsight</span></span>                 | <span data-ttu-id="5d61e-132">hdinsight/de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="5d61e-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="5d61e-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="5d61e-133">Jenkins</span></span>                   | <span data-ttu-id="5d61e-134">Azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="5d61e-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="5d61e-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5d61e-135">Machine Learning</span></span>          | <span data-ttu-id="5d61e-136">azure/data/machine-learning</span><span class="sxs-lookup"><span data-stu-id="5d61e-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="5d61e-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5d61e-137">Service Fabric</span></span>            | <span data-ttu-id="5d61e-138">Azure/computação/serviço-malha</span><span class="sxs-lookup"><span data-stu-id="5d61e-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="5d61e-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="5d61e-139">VSTS</span></span>                      | <span data-ttu-id="5d61e-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="5d61e-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="5d61e-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5d61e-141">Next steps</span></span>
[<span data-ttu-id="5d61e-142">Saiba mais sobre os registros e os serviços e orquestradores com suporte</span><span class="sxs-lookup"><span data-stu-id="5d61e-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
