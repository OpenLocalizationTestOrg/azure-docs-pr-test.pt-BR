---
title: "recursos de nuvem Shell (visualização) aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="06865-103">Recursos e ferramentas para o Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="06865-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="06865-104">Shell de nuvem do Azure é um toomanage de experiência do shell baseado no navegador e desenvolver recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="06865-104">Azure Cloud Shell is a browser-based shell experience toomanage and develop Azure resources.</span></span>

<span data-ttu-id="06865-105">Shell de nuvem oferece um navegador acessível, pré-configurado experiência do shell de gerenciamento de recursos do Azure sem sobrecarga de saudação de instalação, controle de versão e a manutenção de uma máquina por conta própria.</span><span class="sxs-lookup"><span data-stu-id="06865-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without hello overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="06865-106">O Cloud Shell provisiona máquinas com base em solicitação e, consequentemente, o estado da máquina não persistirá nas sessões.</span><span class="sxs-lookup"><span data-stu-id="06865-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="06865-107">Como o Cloud Shell é compilado para sessões interativas, os shells são encerrados automaticamente após 20 minutos de inatividade do shell.</span><span class="sxs-lookup"><span data-stu-id="06865-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="06865-108">Bash no Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="06865-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="06865-109">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="06865-109">Tools</span></span>
|<span data-ttu-id="06865-110">Categoria</span><span class="sxs-lookup"><span data-stu-id="06865-110">Category</span></span>   |<span data-ttu-id="06865-111">Nome</span><span class="sxs-lookup"><span data-stu-id="06865-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="06865-112">Intérprete de shell do Linux</span><span class="sxs-lookup"><span data-stu-id="06865-112">Linux shell interpreter</span></span>|<span data-ttu-id="06865-113">Bash</span><span class="sxs-lookup"><span data-stu-id="06865-113">Bash</span></span><br> <span data-ttu-id="06865-114">sh</span><span class="sxs-lookup"><span data-stu-id="06865-114">sh</span></span>               |
|<span data-ttu-id="06865-115">Ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="06865-115">Azure tools</span></span>            |<span data-ttu-id="06865-116">CLI do Azure [1.0](https://github.com/Azure/azure-cli) e [2.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="06865-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="06865-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="06865-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="06865-118">Shipyard de lote</span><span class="sxs-lookup"><span data-stu-id="06865-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="06865-119">Editores de texto</span><span class="sxs-lookup"><span data-stu-id="06865-119">Text editors</span></span>           |<span data-ttu-id="06865-120">vim</span><span class="sxs-lookup"><span data-stu-id="06865-120">vim</span></span><br> <span data-ttu-id="06865-121">nano</span><span class="sxs-lookup"><span data-stu-id="06865-121">nano</span></span><br> <span data-ttu-id="06865-122">emacs</span><span class="sxs-lookup"><span data-stu-id="06865-122">emacs</span></span>       |
|<span data-ttu-id="06865-123">Controle do código-fonte</span><span class="sxs-lookup"><span data-stu-id="06865-123">Source control</span></span>         |<span data-ttu-id="06865-124">git</span><span class="sxs-lookup"><span data-stu-id="06865-124">git</span></span>                    |
|<span data-ttu-id="06865-125">Ferramentas de build</span><span class="sxs-lookup"><span data-stu-id="06865-125">Build tools</span></span>            |<span data-ttu-id="06865-126">make</span><span class="sxs-lookup"><span data-stu-id="06865-126">make</span></span><br> <span data-ttu-id="06865-127">maven</span><span class="sxs-lookup"><span data-stu-id="06865-127">maven</span></span><br> <span data-ttu-id="06865-128">npm</span><span class="sxs-lookup"><span data-stu-id="06865-128">npm</span></span><br> <span data-ttu-id="06865-129">pip</span><span class="sxs-lookup"><span data-stu-id="06865-129">pip</span></span>         |
|<span data-ttu-id="06865-130">Contêineres</span><span class="sxs-lookup"><span data-stu-id="06865-130">Containers</span></span>             |<span data-ttu-id="06865-131">[CLI do Docker](https://github.com/docker/cli)/[Computador do Docker](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="06865-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="06865-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="06865-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="06865-133">Escalação</span><span class="sxs-lookup"><span data-stu-id="06865-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="06865-134">CLI DO DC/OS</span><span class="sxs-lookup"><span data-stu-id="06865-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="06865-135">Bancos de dados</span><span class="sxs-lookup"><span data-stu-id="06865-135">Databases</span></span>              |<span data-ttu-id="06865-136">Cliente do MySQL</span><span class="sxs-lookup"><span data-stu-id="06865-136">MySQL client</span></span><br> <span data-ttu-id="06865-137">Cliente do PostgreSql</span><span class="sxs-lookup"><span data-stu-id="06865-137">PostgreSql client</span></span><br> [<span data-ttu-id="06865-138">Utilitário SQLCMD</span><span class="sxs-lookup"><span data-stu-id="06865-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="06865-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="06865-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="06865-140">outro</span><span class="sxs-lookup"><span data-stu-id="06865-140">Other</span></span>                  |<span data-ttu-id="06865-141">Cliente do iPython</span><span class="sxs-lookup"><span data-stu-id="06865-141">iPython Client</span></span><br> [<span data-ttu-id="06865-142">CLI do Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="06865-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="06865-143">Suporte ao idioma</span><span class="sxs-lookup"><span data-stu-id="06865-143">Language support</span></span>
|<span data-ttu-id="06865-144">idioma</span><span class="sxs-lookup"><span data-stu-id="06865-144">Language</span></span>   |<span data-ttu-id="06865-145">Versão</span><span class="sxs-lookup"><span data-stu-id="06865-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="06865-146">.NET</span><span class="sxs-lookup"><span data-stu-id="06865-146">.NET</span></span>       |<span data-ttu-id="06865-147">1.01</span><span class="sxs-lookup"><span data-stu-id="06865-147">1.01</span></span>       |
|<span data-ttu-id="06865-148">Go</span><span class="sxs-lookup"><span data-stu-id="06865-148">Go</span></span>         |<span data-ttu-id="06865-149">1.7</span><span class="sxs-lookup"><span data-stu-id="06865-149">1.7</span></span>        |
|<span data-ttu-id="06865-150">Java</span><span class="sxs-lookup"><span data-stu-id="06865-150">Java</span></span>       |<span data-ttu-id="06865-151">1.8</span><span class="sxs-lookup"><span data-stu-id="06865-151">1.8</span></span>        |
|<span data-ttu-id="06865-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="06865-152">Node.js</span></span>    |<span data-ttu-id="06865-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="06865-153">6.9.4</span></span>      |
|<span data-ttu-id="06865-154">Python</span><span class="sxs-lookup"><span data-stu-id="06865-154">Python</span></span>     |<span data-ttu-id="06865-155">2.7 e 3.5 (padrão)</span><span class="sxs-lookup"><span data-stu-id="06865-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="06865-156">Autenticação automática segura</span><span class="sxs-lookup"><span data-stu-id="06865-156">Secure automatic authentication</span></span>
<span data-ttu-id="06865-157">Shell de nuvem com segurança e automaticamente autentica o acesso de conta para Olá 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="06865-157">Cloud Shell securely and automatically authenticates account access for hello Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="06865-158">Persistência de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="06865-158">Azure Files persistence</span></span>
<span data-ttu-id="06865-159">Como o Cloud Shell é alocado com base em solicitação usando um computador temporário, os arquivos fora de $Home e o estado do computador não persistem entre as sessões.</span><span class="sxs-lookup"><span data-stu-id="06865-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="06865-160">arquivos de toopersist entre as sessões, movimentações de Shell de nuvem por meio de anexação de um arquivo do Azure compartilhar na primeira inicialização.</span><span class="sxs-lookup"><span data-stu-id="06865-160">toopersist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="06865-161">Após a conclusão, o Cloud Shell anexará automaticamente o armazenamento para todas as sessões futuras.</span><span class="sxs-lookup"><span data-stu-id="06865-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="06865-162">Saiba mais sobre como anexar tooCloud de compartilhamentos de arquivos do Azure Shell.</span><span class="sxs-lookup"><span data-stu-id="06865-162">Learn more about attaching Azure file shares tooCloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="06865-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06865-163">Next steps</span></span>
[<span data-ttu-id="06865-164">Início rápido do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="06865-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="06865-165">
[Saiba mais sobre a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="06865-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>