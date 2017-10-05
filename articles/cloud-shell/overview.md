---
title: "Visão geral do Azure Cloud Shell (versão prévia) | Microsoft Docs"
description: "Visão geral do Azure Cloud Shell."
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 7165633cd354eeea2e3619f839338e6af1524e56
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="8f09c-103">Visão geral do Azure Cloud Shell (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="8f09c-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="8f09c-104">O Azure Cloud Shell é um shell interativo e acessível pelo navegador para o gerenciamento de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f09c-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="8f09c-105">Recursos</span><span class="sxs-lookup"><span data-stu-id="8f09c-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="8f09c-106">Experiência de shell baseada no navegador</span><span class="sxs-lookup"><span data-stu-id="8f09c-106">Browser-based shell experience</span></span>
<span data-ttu-id="8f09c-107">O Cloud Shell permite o acesso a uma experiência de linha de comando baseada em navegador, que foi criada tendo em mente as tarefas de gerenciamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f09c-107">Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="8f09c-108">Utilize o Cloud Shell para trabalhar de forma independente de um computador local, de uma maneira que somente a nuvem pode proporcionar.</span><span class="sxs-lookup"><span data-stu-id="8f09c-108">Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="8f09c-109">Estação de trabalho pré-configurada do Azure</span><span class="sxs-lookup"><span data-stu-id="8f09c-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="8f09c-110">O Cloud Shell vem pré-instalado com ferramentas de linha de comando populares e suporte para idiomas, para que você possa trabalhar mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="8f09c-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="8f09c-111">Exiba a lista completa de ferramentas para o Azure Cloud Shell aqui.</span><span class="sxs-lookup"><span data-stu-id="8f09c-111">View the full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="8f09c-112">Autenticação automática</span><span class="sxs-lookup"><span data-stu-id="8f09c-112">Automatic authentication</span></span>
<span data-ttu-id="8f09c-113">O Cloud Shell é autenticado de forma segura e automática a cada sessão para ter acesso instantâneo a seus recursos por meio da CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="8f09c-113">Cloud Shell securely authenticates automatically on each session for instant access to your resources through the Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="8f09c-114">Conectar o armazenamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="8f09c-114">Connect your Azure File storage</span></span>
<span data-ttu-id="8f09c-115">As máquinas do Cloud Shell são temporárias e, consequentemente, exigem que um compartilhamento de arquivos do Azure seja montado como `clouddrive` para manter seu diretório $Home.</span><span class="sxs-lookup"><span data-stu-id="8f09c-115">Cloud Shell machines are temporary and as a result require an Azure file share to be mounted as `clouddrive` to persist your $Home directory.</span></span>
<span data-ttu-id="8f09c-116">Na primeira inicialização, o Cloud Shell solicita a criação de um grupo de recursos, uma conta de armazenamento e um compartilhamento de arquivos em seu nome.</span><span class="sxs-lookup"><span data-stu-id="8f09c-116">On first launch Cloud Shell prompts to create a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="8f09c-117">Essa é uma etapa única e será anexada automaticamente para todas as sessões.</span><span class="sxs-lookup"><span data-stu-id="8f09c-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="8f09c-118">Criar novo armazenamento</span><span class="sxs-lookup"><span data-stu-id="8f09c-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="8f09c-119">Uma conta de LRS (armazenamento com redundância local) pode ser criada em seu nome com um Compartilhamento de Arquivos do Azure que contém uma imagem de disco de 5 GB padrão.</span><span class="sxs-lookup"><span data-stu-id="8f09c-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="8f09c-120">O compartilhamento de arquivos é montado como `clouddrive` para interação de compartilhamento de arquivos com a imagem do disco sendo usada para sincronizar e manter seu diretório $Home.</span><span class="sxs-lookup"><span data-stu-id="8f09c-120">The file share mounts as `clouddrive` for file share interaction with the disk image being used to sync and persist your $Home directory.</span></span> <span data-ttu-id="8f09c-121">Custos de armazenamento regulares se aplicam.</span><span class="sxs-lookup"><span data-stu-id="8f09c-121">Regular storage costs apply.</span></span>

<span data-ttu-id="8f09c-122">Três recursos serão criados em seu nome:</span><span class="sxs-lookup"><span data-stu-id="8f09c-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="8f09c-123">Um Grupo de Recursos chamado: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="8f09c-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="8f09c-124">Uma Conta de Armazenamento chamada: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="8f09c-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="8f09c-125">Um Compartilhamento de Arquivos chamado: `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="8f09c-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="8f09c-126">Todos os arquivos em seu diretório $Home como chaves SSH são mantidos em sua imagem de disco do usuário armazenada no compartilhamento de arquivo montados.</span><span class="sxs-lookup"><span data-stu-id="8f09c-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="8f09c-127">Aplica as práticas recomendadas ao salvar arquivos no diretório $Home e compartilhamento de arquivos montado.</span><span class="sxs-lookup"><span data-stu-id="8f09c-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="8f09c-128">Usar recursos existentes</span><span class="sxs-lookup"><span data-stu-id="8f09c-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="8f09c-129">É fornecida também uma opção avançada para permitir que você associe os recursos existentes ao Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8f09c-129">An advanced option is also provided allowing you to associate existing resources to Cloud Shell.</span></span> <span data-ttu-id="8f09c-130">Quando o prompt de configuração de armazenamento for apresentado, clique em “Mostrar configurações avançadas” para selecionar as opções adicionais.</span><span class="sxs-lookup"><span data-stu-id="8f09c-130">When presented with the storage setup prompt, click "Show advanced settings" to select additional options.</span></span> <span data-ttu-id="8f09c-131">As listas suspensas são filtradas para sua região do Cloud Shell atribuída e para contas de armazenamento com redundância local/global.</span><span class="sxs-lookup"><span data-stu-id="8f09c-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="8f09c-132">[Saiba mais sobre o armazenamento do Cloud Shell, atualização de compartilhamentos de arquivos e upload/download de arquivos.] (persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="8f09c-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="8f09c-133">Conceitos</span><span class="sxs-lookup"><span data-stu-id="8f09c-133">Concepts</span></span>
* <span data-ttu-id="8f09c-134">O Cloud Shell é executado em um computador temporário fornecido por sessão e por usuário</span><span class="sxs-lookup"><span data-stu-id="8f09c-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="8f09c-135">O Cloud Shell atinge o tempo limite após 20 minutos sem atividade interativa</span><span class="sxs-lookup"><span data-stu-id="8f09c-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="8f09c-136">O Cloud Shell só pode ser acessado com um compartilhamento de arquivos anexado</span><span class="sxs-lookup"><span data-stu-id="8f09c-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="8f09c-137">É atribuído ao Cloud Shell um computador por conta de usuário</span><span class="sxs-lookup"><span data-stu-id="8f09c-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="8f09c-138">As permissões são definidas da mesma forma que para um usuário normal do Linux</span><span class="sxs-lookup"><span data-stu-id="8f09c-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="8f09c-139">Saiba mais sobre todos os recursos do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8f09c-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="8f09c-140">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8f09c-140">Examples</span></span>
* <span data-ttu-id="8f09c-141">Criar ou editar scripts para automatizar o gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8f09c-141">Create or edit scripts to automate Azure management</span></span>
* <span data-ttu-id="8f09c-142">Gerenciar recursos simultaneamente por meio do portal do Azure e da CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8f09c-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="8f09c-143">Testar a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8f09c-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="8f09c-144">Teste todos esses exemplos no início rápido do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8f09c-144">Try out all these examples at the Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="8f09c-145">Preços</span><span class="sxs-lookup"><span data-stu-id="8f09c-145">Pricing</span></span>
<span data-ttu-id="8f09c-146">O computador que hospeda o Cloud Shell é gratuito,, com o pré-requisito de um compartilhamento de arquivos do Azure montado para persistir seu diretório $Home.</span><span class="sxs-lookup"><span data-stu-id="8f09c-146">The machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share to persist your $Home directory.</span></span> <span data-ttu-id="8f09c-147">Custos de armazenamento regulares se aplicam.</span><span class="sxs-lookup"><span data-stu-id="8f09c-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="8f09c-148">Navegadores com suporte</span><span class="sxs-lookup"><span data-stu-id="8f09c-148">Supported browsers</span></span>
<span data-ttu-id="8f09c-149">O Cloud Shell é recomendado para Chrome, Edge e Safari.</span><span class="sxs-lookup"><span data-stu-id="8f09c-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="8f09c-150">Embora tenha suporte para Chrome, Firefox, Safari, IE e Edge, o Cloud Shell está sujeito a configurações específicas do navegador.</span><span class="sxs-lookup"><span data-stu-id="8f09c-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject to specific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8f09c-151">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8f09c-151">Troubleshooting</span></span>
1. <span data-ttu-id="8f09c-152">Ao usar uma assinatura do Azure Active Directory, não consigo criar armazenamento devido ao erro “Error: 400 DisallowedOperation”.</span><span class="sxs-lookup"><span data-stu-id="8f09c-152">When using an Azure Active Directory subscription, I cannot create storage due to Error: 400 DisallowedOperation.</span></span> <span data-ttu-id="8f09c-153">Para resolver isso, use uma assinatura do Azure capaz de criar recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8f09c-153">To resolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="8f09c-154">Assinaturas do AD não são capazes de criar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f09c-154">AD subscriptions are not able to create Azure resources.</span></span>

<span data-ttu-id="8f09c-155">Para ver as limitações conhecidas específicas, visite [Limitações do Cloud Shell](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="8f09c-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
