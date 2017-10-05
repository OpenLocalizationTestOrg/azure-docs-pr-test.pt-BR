---
title: "Implantando aplicativos no Serviço de Aplicativo do Azure"
description: "Saiba como implantar aplicativos para o trabalho do Serviço de Aplicativo"
keywords: "serviço de aplicativo do azure, serviço de aplicativo, implantando, implantação"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="c7bb0-104">Visão geral da implantação do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="c7bb0-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="c7bb0-105">O Serviço de Aplicativo do Azure fornece um recurso avançado e integrado definido para dar suporte à criação de fluxos de trabalho de implantação flexível e poderosa.</span><span class="sxs-lookup"><span data-stu-id="c7bb0-105">Azure App Service provides a rich and integrated feature set to support creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="c7bb0-106">A implantação de aplicativos pode aproveitar opções que incluem publicação de controle do código-fonte local ou integração contínua, WebDeploy e FTP.</span><span class="sxs-lookup"><span data-stu-id="c7bb0-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="c7bb0-107">O método recomendado para implantação do aplicativo de produção é a alternância do slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="c7bb0-107">The recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="c7bb0-108">Os slots de implantação representam ambientes de preparo e integração associados a aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="c7bb0-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="c7bb0-109">Os slots de implantação podem ser configurados e depender de tráfego da Web para validação, e o tráfego pode ser alternado sob demanda para implantação na produção sem a necessidade de tempo de inatividade e aquecimento automatizado.</span><span class="sxs-lookup"><span data-stu-id="c7bb0-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment to production with no down time and automated warm-up.</span></span> <span data-ttu-id="c7bb0-110">As etapas de um fluxo de trabalho de implantação podem ser automatizadas facilmente por meio de produtos de gerenciamento de versão, como o Visual Studio Release Management.</span><span class="sxs-lookup"><span data-stu-id="c7bb0-110">The steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="c7bb0-111">Isso é útil para coordenar com outros recursos da solução (por exemplo, armazenamento de dados), recorrência e replicação em várias unidades de implantação.</span><span class="sxs-lookup"><span data-stu-id="c7bb0-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

