---
title: "Recursos do Azure Cloud Shell (visualização) | Microsoft Docs"
description: "Visão geral dos recursos do Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="a64b2-103">Recursos e ferramentas para o Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a64b2-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="a64b2-104">Azure Cloud Shell é uma experiência de shell baseada em navegador para gerenciar e desenvolver recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a64b2-104">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span>

<span data-ttu-id="a64b2-105">O Cloud Shell oferece uma experiência de shell acessível ao navegador e pré-configurada para gerenciar recursos do Azure sem a sobrecarga da instalação, controle de versão e manutenção de uma máquina por conta própria.</span><span class="sxs-lookup"><span data-stu-id="a64b2-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="a64b2-106">O Cloud Shell provisiona máquinas com base em solicitação e, consequentemente, o estado da máquina não persistirá nas sessões.</span><span class="sxs-lookup"><span data-stu-id="a64b2-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="a64b2-107">Como o Cloud Shell é compilado para sessões interativas, os shells são encerrados automaticamente após 20 minutos de inatividade do shell.</span><span class="sxs-lookup"><span data-stu-id="a64b2-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="a64b2-108">Bash no Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a64b2-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="a64b2-109">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="a64b2-109">Tools</span></span>
|<span data-ttu-id="a64b2-110">Categoria</span><span class="sxs-lookup"><span data-stu-id="a64b2-110">Category</span></span>   |<span data-ttu-id="a64b2-111">Nome</span><span class="sxs-lookup"><span data-stu-id="a64b2-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="a64b2-112">Intérprete de shell do Linux</span><span class="sxs-lookup"><span data-stu-id="a64b2-112">Linux shell interpreter</span></span>|<span data-ttu-id="a64b2-113">Bash</span><span class="sxs-lookup"><span data-stu-id="a64b2-113">Bash</span></span><br> <span data-ttu-id="a64b2-114">sh</span><span class="sxs-lookup"><span data-stu-id="a64b2-114">sh</span></span>               |
|<span data-ttu-id="a64b2-115">Ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="a64b2-115">Azure tools</span></span>            |<span data-ttu-id="a64b2-116">CLI do Azure [1.0](https://github.com/Azure/azure-cli) e [2.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="a64b2-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="a64b2-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="a64b2-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="a64b2-118">Shipyard de lote</span><span class="sxs-lookup"><span data-stu-id="a64b2-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="a64b2-119">Editores de texto</span><span class="sxs-lookup"><span data-stu-id="a64b2-119">Text editors</span></span>           |<span data-ttu-id="a64b2-120">vim</span><span class="sxs-lookup"><span data-stu-id="a64b2-120">vim</span></span><br> <span data-ttu-id="a64b2-121">nano</span><span class="sxs-lookup"><span data-stu-id="a64b2-121">nano</span></span><br> <span data-ttu-id="a64b2-122">emacs</span><span class="sxs-lookup"><span data-stu-id="a64b2-122">emacs</span></span>       |
|<span data-ttu-id="a64b2-123">Controle do código-fonte</span><span class="sxs-lookup"><span data-stu-id="a64b2-123">Source control</span></span>         |<span data-ttu-id="a64b2-124">git</span><span class="sxs-lookup"><span data-stu-id="a64b2-124">git</span></span>                    |
|<span data-ttu-id="a64b2-125">Ferramentas de build</span><span class="sxs-lookup"><span data-stu-id="a64b2-125">Build tools</span></span>            |<span data-ttu-id="a64b2-126">make</span><span class="sxs-lookup"><span data-stu-id="a64b2-126">make</span></span><br> <span data-ttu-id="a64b2-127">maven</span><span class="sxs-lookup"><span data-stu-id="a64b2-127">maven</span></span><br> <span data-ttu-id="a64b2-128">npm</span><span class="sxs-lookup"><span data-stu-id="a64b2-128">npm</span></span><br> <span data-ttu-id="a64b2-129">pip</span><span class="sxs-lookup"><span data-stu-id="a64b2-129">pip</span></span>         |
|<span data-ttu-id="a64b2-130">Contêineres</span><span class="sxs-lookup"><span data-stu-id="a64b2-130">Containers</span></span>             |<span data-ttu-id="a64b2-131">[CLI do Docker](https://github.com/docker/cli)/[Computador do Docker](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="a64b2-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="a64b2-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="a64b2-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="a64b2-133">Escalação</span><span class="sxs-lookup"><span data-stu-id="a64b2-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="a64b2-134">CLI DO DC/OS</span><span class="sxs-lookup"><span data-stu-id="a64b2-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="a64b2-135">Bancos de dados</span><span class="sxs-lookup"><span data-stu-id="a64b2-135">Databases</span></span>              |<span data-ttu-id="a64b2-136">Cliente do MySQL</span><span class="sxs-lookup"><span data-stu-id="a64b2-136">MySQL client</span></span><br> <span data-ttu-id="a64b2-137">Cliente do PostgreSql</span><span class="sxs-lookup"><span data-stu-id="a64b2-137">PostgreSql client</span></span><br> [<span data-ttu-id="a64b2-138">Utilitário SQLCMD</span><span class="sxs-lookup"><span data-stu-id="a64b2-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="a64b2-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="a64b2-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="a64b2-140">outro</span><span class="sxs-lookup"><span data-stu-id="a64b2-140">Other</span></span>                  |<span data-ttu-id="a64b2-141">Cliente do iPython</span><span class="sxs-lookup"><span data-stu-id="a64b2-141">iPython Client</span></span><br> [<span data-ttu-id="a64b2-142">CLI do Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="a64b2-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="a64b2-143">Suporte ao idioma</span><span class="sxs-lookup"><span data-stu-id="a64b2-143">Language support</span></span>
|<span data-ttu-id="a64b2-144">idioma</span><span class="sxs-lookup"><span data-stu-id="a64b2-144">Language</span></span>   |<span data-ttu-id="a64b2-145">Versão</span><span class="sxs-lookup"><span data-stu-id="a64b2-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="a64b2-146">.NET</span><span class="sxs-lookup"><span data-stu-id="a64b2-146">.NET</span></span>       |<span data-ttu-id="a64b2-147">1.01</span><span class="sxs-lookup"><span data-stu-id="a64b2-147">1.01</span></span>       |
|<span data-ttu-id="a64b2-148">Go</span><span class="sxs-lookup"><span data-stu-id="a64b2-148">Go</span></span>         |<span data-ttu-id="a64b2-149">1.7</span><span class="sxs-lookup"><span data-stu-id="a64b2-149">1.7</span></span>        |
|<span data-ttu-id="a64b2-150">Java</span><span class="sxs-lookup"><span data-stu-id="a64b2-150">Java</span></span>       |<span data-ttu-id="a64b2-151">1.8</span><span class="sxs-lookup"><span data-stu-id="a64b2-151">1.8</span></span>        |
|<span data-ttu-id="a64b2-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="a64b2-152">Node.js</span></span>    |<span data-ttu-id="a64b2-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="a64b2-153">6.9.4</span></span>      |
|<span data-ttu-id="a64b2-154">Python</span><span class="sxs-lookup"><span data-stu-id="a64b2-154">Python</span></span>     |<span data-ttu-id="a64b2-155">2.7 e 3.5 (padrão)</span><span class="sxs-lookup"><span data-stu-id="a64b2-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="a64b2-156">Autenticação automática segura</span><span class="sxs-lookup"><span data-stu-id="a64b2-156">Secure automatic authentication</span></span>
<span data-ttu-id="a64b2-157">O Cloud Shell protege e autentica automaticamente o acesso de conta da CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="a64b2-157">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="a64b2-158">Persistência de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="a64b2-158">Azure Files persistence</span></span>
<span data-ttu-id="a64b2-159">Como o Cloud Shell é alocado com base em solicitação usando um computador temporário, os arquivos fora de $Home e o estado do computador não persistem entre as sessões.</span><span class="sxs-lookup"><span data-stu-id="a64b2-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="a64b2-160">Para persistir arquivos entre as sessões, o Cloud Shell orienta você pela anexação de um compartilhamento de arquivos do Azure na primeira inicialização.</span><span class="sxs-lookup"><span data-stu-id="a64b2-160">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="a64b2-161">Após a conclusão, o Cloud Shell anexará automaticamente o armazenamento para todas as sessões futuras.</span><span class="sxs-lookup"><span data-stu-id="a64b2-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="a64b2-162">Saiba mais sobre como anexar os compartilhamentos de arquivos do Azure ao Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a64b2-162">Learn more about attaching Azure file shares to Cloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="a64b2-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a64b2-163">Next steps</span></span>
[<span data-ttu-id="a64b2-164">Início rápido do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a64b2-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="a64b2-165">
[Saiba mais sobre a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="a64b2-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>