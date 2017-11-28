---
title: "aaaDeploying tooAzure de aplicativos do serviço de aplicativo"
description: "Saiba como tooDeploy aplicativos tooApp serviço funcionam"
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
ms.openlocfilehash: 925341e12daf3cb05b25199f5c5218e82f062f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="5b846-104">Visão geral da implantação do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="5b846-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="5b846-105">Serviço de aplicativo do Azure fornece uma ampla e toosupport criando fluxos de trabalho de implantação poderoso e flexível de conjunto de recursos integrados.</span><span class="sxs-lookup"><span data-stu-id="5b846-105">Azure App Service provides a rich and integrated feature set toosupport creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="5b846-106">A implantação de aplicativos pode aproveitar opções que incluem publicação de controle do código-fonte local ou integração contínua, WebDeploy e FTP.</span><span class="sxs-lookup"><span data-stu-id="5b846-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="5b846-107">Olá recomendado o método de implantação de aplicativos de produção é troca de slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="5b846-107">hello recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="5b846-108">Os slots de implantação representam ambientes de preparo e integração associados a aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="5b846-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="5b846-109">Slots de implantação podem ser configurados e direcionados com tráfego da web para validação e tráfego pode ser trocado sob demanda para implantação tooproduction sem nenhum tempo de inatividade e automatizado de aquecimento.</span><span class="sxs-lookup"><span data-stu-id="5b846-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment tooproduction with no down time and automated warm-up.</span></span> <span data-ttu-id="5b846-110">etapas de saudação de um fluxo de trabalho de implantação podem ser automatizadas facilmente por meio de produtos de gerenciamento de versão, como gerenciamento de versão do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5b846-110">hello steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="5b846-111">Isso é útil para coordenar com outros recursos da solução (por exemplo, armazenamento de dados), recorrência e replicação em várias unidades de implantação.</span><span class="sxs-lookup"><span data-stu-id="5b846-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

