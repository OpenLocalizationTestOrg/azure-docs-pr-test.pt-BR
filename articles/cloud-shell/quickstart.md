---
title: "início rápido do Shell de nuvem (visualização) aaaAzure | Microsoft Docs"
description: "Início rápido para Olá Shell de nuvem do Azure"
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
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a><span data-ttu-id="2a061-103">Guia de início rápido para usar o hello Shell de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="2a061-103">Quickstart for using hello Azure Cloud Shell</span></span>

<span data-ttu-id="2a061-104">Este documento detalha como toouse Olá Shell de nuvem do Azure no hello [portal do Azure](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a061-104">This document details how toouse hello Azure Cloud Shell in hello [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="2a061-105">Iniciar o Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="2a061-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="2a061-106">Iniciar **nuvem Shell** de navegação superior Olá Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2a061-106">Launch **Cloud Shell** from hello top navigation of hello Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="2a061-107">Selecione uma assinatura toocreate uma conta de armazenamento e compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="2a061-107">Select a subscription toocreate a storage account and Azure file share</span></span>
3. <span data-ttu-id="2a061-108">Selecione "Criar armazenamento"</span><span class="sxs-lookup"><span data-stu-id="2a061-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="2a061-109">Você é autenticado automaticamente na CLI do Azure 2.0 em cada sessão.</span><span class="sxs-lookup"><span data-stu-id="2a061-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="2a061-110">Definir sua assinatura</span><span class="sxs-lookup"><span data-stu-id="2a061-110">Set your subscription</span></span>
1. <span data-ttu-id="2a061-111">Liste as assinaturas a que você tem acesso:</span><span class="sxs-lookup"><span data-stu-id="2a061-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="2a061-112">Defina sua assinatura preferencial:</span><span class="sxs-lookup"><span data-stu-id="2a061-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="2a061-113">Sua assinatura será lembrada em sessões futuras com o uso de `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="2a061-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="2a061-114">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2a061-114">Create a resource group</span></span>
<span data-ttu-id="2a061-115">Crie um novo grupo de recursos no Oeste dos EUA chamado "MyRG":</span><span class="sxs-lookup"><span data-stu-id="2a061-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="2a061-116">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="2a061-116">Create a Linux VM</span></span>
<span data-ttu-id="2a061-117">Crie uma VM do Ubuntu em seu novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2a061-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="2a061-118">Olá 2.0 do CLI do Azure criará as chaves de SSH e Olá instalação VM com eles.</span><span class="sxs-lookup"><span data-stu-id="2a061-118">hello Azure CLI 2.0 will create SSH keys and setup hello VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="2a061-119">Olá tooauthenticate de chaves públicas e privadas usadas sua VM são colocados em `/User/.ssh/id_rsa` e `/User/.ssh/id_rsa.pub` pelo Azure CLI 2.0 por padrão.</span><span class="sxs-lookup"><span data-stu-id="2a061-119">hello public and private keys used tooauthenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="2a061-120">Sua pasta .ssh é mantida na imagem de 5 GB do compartilhamento de arquivos anexado do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a061-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="2a061-121">Seu nome de usuário nessa VM será o nome de usuário usado no Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="2a061-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="2a061-122">SSH em sua VM Linux</span><span class="sxs-lookup"><span data-stu-id="2a061-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="2a061-123">Procurar o nome VM na barra de pesquisa do portal do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="2a061-123">Search for your VM name in hello Azure portal search bar</span></span>
2. <span data-ttu-id="2a061-124">Clique em "Conectar" e execute: `ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="2a061-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="2a061-125">Após estabelecer a conexão de SSH hello, você verá um prompt de boas-vinda de Ubuntu de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a061-125">Upon establishing hello SSH connection, you should see hello Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="2a061-126">Limpando</span><span class="sxs-lookup"><span data-stu-id="2a061-126">Cleaning up</span></span> 
<span data-ttu-id="2a061-127">Exclua o grupo de recursos e todos os recursos dentro dele:</span><span class="sxs-lookup"><span data-stu-id="2a061-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="2a061-128">Execute o `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="2a061-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a061-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a061-129">Next Steps</span></span>
[<span data-ttu-id="2a061-130">Saiba mais sobre o armazenamento persistente no Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="2a061-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="2a061-131">
[Saiba mais sobre a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="2a061-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="2a061-132">
[Saiba mais sobre o armazenamento de Arquivos do Azure](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2a061-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>