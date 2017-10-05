---
title: "Exemplos do Azure PowerShell - Serviço de Aplicativo | Microsoft Docs"
description: "Exemplos do Azure PowerShell - Serviço de Aplicativo"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="3c6fe-103">Exemplos do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c6fe-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="3c6fe-104">A tabela a seguir inclui links para scripts bash compilados usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="3c6fe-105">**Como criar o aplicativo**</span><span class="sxs-lookup"><span data-stu-id="3c6fe-105">**Create app**</span></span>||
| [<span data-ttu-id="3c6fe-106">Como criar um aplicativo Web com a implantação do GitHub</span><span class="sxs-lookup"><span data-stu-id="3c6fe-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="3c6fe-107">Cria um aplicativo Web do Azure que recebe o código do GitHub.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="3c6fe-108">Como criar um aplicativo Web com a implantação contínua do GitHub</span><span class="sxs-lookup"><span data-stu-id="3c6fe-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="3c6fe-109">Cria um aplicativo Web do Azure que implanta continuamente o código do GitHub.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="3c6fe-110">Criar um aplicativo Web e implantar o código com FTP</span><span class="sxs-lookup"><span data-stu-id="3c6fe-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="3c6fe-111">Cria um aplicativo Web do Azure os carregue os arquivos de um diretório local usando FTP.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="3c6fe-112">Como criar um aplicativo Web e implantar o código de um repositório Git local</span><span class="sxs-lookup"><span data-stu-id="3c6fe-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="3c6fe-113">Cria um aplicativo Web do Azure e configura o push de código de um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="3c6fe-114">Como criar um aplicativo Web e implantar o código em um ambiente de preparo</span><span class="sxs-lookup"><span data-stu-id="3c6fe-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="3c6fe-115">Cria um aplicativo Web do Azure com um slot de implantação para alterações de código de preparo.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="3c6fe-116">**Como configurar o aplicativo**</span><span class="sxs-lookup"><span data-stu-id="3c6fe-116">**Configure app**</span></span>||
| [<span data-ttu-id="3c6fe-117">Como mapear um domínio personalizado para um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="3c6fe-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="3c6fe-118">Cria um aplicativo Web do Azure e mapeia um nome de domínio personalizado para ele.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="3c6fe-119">Associar um certificado SSL personalizado a um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="3c6fe-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="3c6fe-120">Cria um aplicativo Web do Azure e associa o certificado SSL de um nome de domínio personalizado a ele.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="3c6fe-121">**Como escalar um aplicativo**</span><span class="sxs-lookup"><span data-stu-id="3c6fe-121">**Scale app**</span></span>||
| [<span data-ttu-id="3c6fe-122">Como escalar manualmente um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="3c6fe-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="3c6fe-123">Cria um aplicativo Web do Azure e pode ser dimensionado em 2 instâncias.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="3c6fe-124">Como escalar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="3c6fe-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="3c6fe-125">Cria dois aplicativos Web do Azure em duas regiões geográficas diferentes e os disponibiliza por meio de um único ponto de extremidade usando o Gerenciador de tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="3c6fe-126">**Como conectar o aplicativo aos recursos**</span><span class="sxs-lookup"><span data-stu-id="3c6fe-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="3c6fe-127">Como conectar um aplicativo Web a um Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="3c6fe-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="3c6fe-128">Cria um aplicativo Web do Azure e um Banco de Dados SQL e, em seguida, adiciona a cadeia de conexão do banco de dados para as configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="3c6fe-129">Como conectar um aplicativo Web a uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3c6fe-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="3c6fe-130">Cria um aplicativo Web do Azure e uma conta de armazenamento e, em seguida, adiciona a cadeia de conexão de armazenamento às configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="3c6fe-131">**Como monitorar o aplicativo**</span><span class="sxs-lookup"><span data-stu-id="3c6fe-131">**Monitor app**</span></span>||
| [<span data-ttu-id="3c6fe-132">Como monitorar um aplicativo Web com logs do servidor Web</span><span class="sxs-lookup"><span data-stu-id="3c6fe-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="3c6fe-133">Cria um aplicativo Web do Azure, habilita o registro em log para ele e baixa os logs em sua máquina local.</span><span class="sxs-lookup"><span data-stu-id="3c6fe-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
