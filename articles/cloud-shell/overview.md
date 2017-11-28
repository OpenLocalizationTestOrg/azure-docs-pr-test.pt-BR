---
title: "Visão geral do Shell de nuvem (visualização) aaaAzure | Microsoft Docs"
description: "Visão geral do hello Shell de nuvem do Azure."
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
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="42242-103">Visão geral do Azure Cloud Shell (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="42242-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="42242-104">O Azure Cloud Shell é um shell interativo e acessível pelo navegador para o gerenciamento de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="42242-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="42242-105">Recursos</span><span class="sxs-lookup"><span data-stu-id="42242-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="42242-106">Experiência de shell baseada no navegador</span><span class="sxs-lookup"><span data-stu-id="42242-106">Browser-based shell experience</span></span>
<span data-ttu-id="42242-107">Nuvem Shell permite tooa baseado em navegador de linha de comando experiência de acesso criada com tarefas de gerenciamento do Azure em mente.</span><span class="sxs-lookup"><span data-stu-id="42242-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="42242-108">Aproveite o Shell de nuvem toowork ilimitado de um computador local, de forma que somente a nuvem de saudação pode fornecer.</span><span class="sxs-lookup"><span data-stu-id="42242-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="42242-109">Estação de trabalho pré-configurada do Azure</span><span class="sxs-lookup"><span data-stu-id="42242-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="42242-110">O Cloud Shell vem pré-instalado com ferramentas de linha de comando populares e suporte para idiomas, para que você possa trabalhar mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="42242-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="42242-111">Olá completo de ferramentas lista Exibir para o Shell de nuvem do Azure aqui.</span><span class="sxs-lookup"><span data-stu-id="42242-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="42242-112">Autenticação automática</span><span class="sxs-lookup"><span data-stu-id="42242-112">Automatic authentication</span></span>
<span data-ttu-id="42242-113">Shell de nuvem com segurança autentica automaticamente em cada sessão para recursos do acesso instantâneo tooyour por meio de saudação 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="42242-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="42242-114">Conectar o armazenamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="42242-114">Connect your Azure File storage</span></span>
<span data-ttu-id="42242-115">Máquinas de Shell de nuvem são temporárias e assim exigem um toobe de compartilhamento de arquivos do Azure montado como `clouddrive` toopersist seu diretório $Home.</span><span class="sxs-lookup"><span data-stu-id="42242-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="42242-116">Na primeira inicialização Shell nuvem solicita toocreate que um grupo de recursos, conta de armazenamento e compartilhamento de arquivos em seu nome.</span><span class="sxs-lookup"><span data-stu-id="42242-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="42242-117">Essa é uma etapa única e será anexada automaticamente para todas as sessões.</span><span class="sxs-lookup"><span data-stu-id="42242-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="42242-118">Criar novo armazenamento</span><span class="sxs-lookup"><span data-stu-id="42242-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="42242-119">Uma conta de LRS (armazenamento com redundância local) pode ser criada em seu nome com um Compartilhamento de Arquivos do Azure que contém uma imagem de disco de 5 GB padrão.</span><span class="sxs-lookup"><span data-stu-id="42242-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="42242-120">compartilhamento de arquivo Hello monta como `clouddrive` para arquivo compartilhar interação com a imagem de disco de saudação que está sendo usado toosync e manter seu diretório $Home.</span><span class="sxs-lookup"><span data-stu-id="42242-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="42242-121">Custos de armazenamento regulares se aplicam.</span><span class="sxs-lookup"><span data-stu-id="42242-121">Regular storage costs apply.</span></span>

<span data-ttu-id="42242-122">Três recursos serão criados em seu nome:</span><span class="sxs-lookup"><span data-stu-id="42242-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="42242-123">Um Grupo de Recursos chamado: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="42242-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="42242-124">Uma Conta de Armazenamento chamada: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="42242-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="42242-125">Um Compartilhamento de Arquivos chamado: `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="42242-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="42242-126">Todos os arquivos em seu diretório $Home como chaves SSH são mantidos em sua imagem de disco do usuário armazenada no compartilhamento de arquivo montados.</span><span class="sxs-lookup"><span data-stu-id="42242-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="42242-127">Aplica as práticas recomendadas ao salvar arquivos no diretório $Home e compartilhamento de arquivos montado.</span><span class="sxs-lookup"><span data-stu-id="42242-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="42242-128">Usar recursos existentes</span><span class="sxs-lookup"><span data-stu-id="42242-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="42242-129">Uma opção avançada também é fornecida permitindo que você tooassociate existente recursos tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="42242-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="42242-130">Quando for apresentado com o prompt de configuração de armazenamento hello, clique em opções adicionais de tooselect "Show advanced settings".</span><span class="sxs-lookup"><span data-stu-id="42242-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="42242-131">As listas suspensas são filtradas para sua região do Cloud Shell atribuída e para contas de armazenamento com redundância local/global.</span><span class="sxs-lookup"><span data-stu-id="42242-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="42242-132">[Saiba mais sobre o armazenamento do Cloud Shell, atualização de compartilhamentos de arquivos e upload/download de arquivos.] (persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="42242-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="42242-133">Conceitos</span><span class="sxs-lookup"><span data-stu-id="42242-133">Concepts</span></span>
* <span data-ttu-id="42242-134">O Cloud Shell é executado em um computador temporário fornecido por sessão e por usuário</span><span class="sxs-lookup"><span data-stu-id="42242-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="42242-135">O Cloud Shell atinge o tempo limite após 20 minutos sem atividade interativa</span><span class="sxs-lookup"><span data-stu-id="42242-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="42242-136">O Cloud Shell só pode ser acessado com um compartilhamento de arquivos anexado</span><span class="sxs-lookup"><span data-stu-id="42242-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="42242-137">É atribuído ao Cloud Shell um computador por conta de usuário</span><span class="sxs-lookup"><span data-stu-id="42242-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="42242-138">As permissões são definidas da mesma forma que para um usuário normal do Linux</span><span class="sxs-lookup"><span data-stu-id="42242-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="42242-139">Saiba mais sobre todos os recursos do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="42242-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="42242-140">Exemplos</span><span class="sxs-lookup"><span data-stu-id="42242-140">Examples</span></span>
* <span data-ttu-id="42242-141">Criar ou editar scripts tooautomate gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="42242-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="42242-142">Gerenciar recursos simultaneamente por meio do portal do Azure e da CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="42242-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="42242-143">Testar a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="42242-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="42242-144">Experimente todos esses exemplos no início rápido da nuvem Shell hello.</span><span class="sxs-lookup"><span data-stu-id="42242-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="42242-145">Preços</span><span class="sxs-lookup"><span data-stu-id="42242-145">Pricing</span></span>
<span data-ttu-id="42242-146">máquina Olá Shell da nuvem de hospedagem é gratuita, com um pré-requisito de um arquivo do Azure montado compartilhar toopersist seu diretório $Home.</span><span class="sxs-lookup"><span data-stu-id="42242-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="42242-147">Custos de armazenamento regulares se aplicam.</span><span class="sxs-lookup"><span data-stu-id="42242-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="42242-148">Navegadores com suporte</span><span class="sxs-lookup"><span data-stu-id="42242-148">Supported browsers</span></span>
<span data-ttu-id="42242-149">O Cloud Shell é recomendado para Chrome, Edge e Safari.</span><span class="sxs-lookup"><span data-stu-id="42242-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="42242-150">Embora haja suporte para o Shell de nuvem para Chrome, Firefox, Safari, IE e borda, o Shell de nuvem é configurações do navegador toospecific assunto.</span><span class="sxs-lookup"><span data-stu-id="42242-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="42242-151">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="42242-151">Troubleshooting</span></span>
1. <span data-ttu-id="42242-152">Ao usar uma assinatura do Azure Active Directory, não é possível criar armazenamento vencimento tooError: DisallowedOperation 400.</span><span class="sxs-lookup"><span data-stu-id="42242-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="42242-153">tooresolve isso, use uma assinatura do Azure capaz de criar recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="42242-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="42242-154">Assinaturas AD é toocreate não é possível recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="42242-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="42242-155">Para ver as limitações conhecidas específicas, visite [Limitações do Cloud Shell](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="42242-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
