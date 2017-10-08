---
title: "repositórios de registro de contêiner aaaAzure | Microsoft Docs"
description: "Como repositórios de registro de contêiner do Azure toouse para imagens do Docker"
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
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="d8205-103">Repositórios de Registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="d8205-103">Azure container registry repositories</span></span>

<span data-ttu-id="d8205-104">Os Registros de Contêiner do Azure são compatíveis com uma variedade de serviços e orquestradores.</span><span class="sxs-lookup"><span data-stu-id="d8205-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="d8205-105">toomake-serviços de fonte de saudação tootrack mais fácil e agentes do qual ACR é usado, começamos usando o campo de cabeçalho de Docker Olá Olá Docker.config arquivo.</span><span class="sxs-lookup"><span data-stu-id="d8205-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="d8205-106">Exibir os repositórios em Olá Portal</span><span class="sxs-lookup"><span data-stu-id="d8205-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="d8205-107">cabeçalhos ACR Olá seguem o formato de saudação:</span><span class="sxs-lookup"><span data-stu-id="d8205-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="d8205-108">Nuvem: Azure, Azure Stack ou outras nuvens do Azure específicas do país ou do governo.</span><span class="sxs-lookup"><span data-stu-id="d8205-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="d8205-109">Embora no momento não haja suporte para o Azure Stack e nuvens do governo, este parâmetro habilita suporte futuro.</span><span class="sxs-lookup"><span data-stu-id="d8205-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="d8205-110">Serviço: o nome do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8205-110">Service: name of hello service.</span></span>
* <span data-ttu-id="d8205-111">Optionalservicename: o parâmetro opcional para serviços com subserviços ou toospecify um SKU (ex: aplicativos web correspondem com aplicativos do Azure/app-service/web).</span><span class="sxs-lookup"><span data-stu-id="d8205-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="d8205-112">Orchestrators e serviços de parceiro são incentivados toouse cabeçalho específico valores toohelp com nosso telemetria.</span><span class="sxs-lookup"><span data-stu-id="d8205-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="d8205-113">Os usuários também podem modificar o valor Olá passado toohello cabeçalho se desejarem.</span><span class="sxs-lookup"><span data-stu-id="d8205-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="d8205-114">valores Hello desejamos ACR parceiros toouse toopopulate hello "X-Meta-origem-cliente" campo são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d8205-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="d8205-115">Nome do Serviço</span><span class="sxs-lookup"><span data-stu-id="d8205-115">Service Name</span></span>              | <span data-ttu-id="d8205-116">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="d8205-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="d8205-117">Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="d8205-117">Azure Container Service</span></span>   | <span data-ttu-id="d8205-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="d8205-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="d8205-119">Serviço de Aplicativo – Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="d8205-119">App Service - Web Apps</span></span>    | <span data-ttu-id="d8205-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="d8205-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="d8205-121">Serviço de Aplicativo – Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="d8205-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="d8205-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="d8205-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="d8205-123">Batch</span><span class="sxs-lookup"><span data-stu-id="d8205-123">Batch</span></span>                     | <span data-ttu-id="d8205-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="d8205-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="d8205-125">Console de nuvem</span><span class="sxs-lookup"><span data-stu-id="d8205-125">Cloud Console</span></span>             | <span data-ttu-id="d8205-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="d8205-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="d8205-127">Funções</span><span class="sxs-lookup"><span data-stu-id="d8205-127">Functions</span></span>                 | <span data-ttu-id="d8205-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="d8205-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="d8205-129">Internet das Coisas – Hub</span><span class="sxs-lookup"><span data-stu-id="d8205-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="d8205-130">hub/de iot do Azure</span><span class="sxs-lookup"><span data-stu-id="d8205-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="d8205-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8205-131">HDInsight</span></span>                 | <span data-ttu-id="d8205-132">hdinsight/de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="d8205-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="d8205-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="d8205-133">Jenkins</span></span>                   | <span data-ttu-id="d8205-134">Azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="d8205-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="d8205-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d8205-135">Machine Learning</span></span>          | <span data-ttu-id="d8205-136">azure/data/machine-learning</span><span class="sxs-lookup"><span data-stu-id="d8205-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="d8205-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d8205-137">Service Fabric</span></span>            | <span data-ttu-id="d8205-138">Azure/computação/serviço-malha</span><span class="sxs-lookup"><span data-stu-id="d8205-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="d8205-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="d8205-139">VSTS</span></span>                      | <span data-ttu-id="d8205-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="d8205-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="d8205-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8205-141">Next steps</span></span>
[<span data-ttu-id="d8205-142">Saiba mais sobre registros e Olá suporte para serviços e orchestrators</span><span class="sxs-lookup"><span data-stu-id="d8205-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
