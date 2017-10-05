---
title: "Guia de início rápido do Azure Cloud Shell (versão prévia) | Microsoft Docs"
description: "Guia de início rápido para o Azure Cloud Shell"
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
ms.openlocfilehash: 75676eb0ab784e2adbfd27b170c1dee5599b74ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-for-using-the-azure-cloud-shell"></a><span data-ttu-id="070f3-103">Guia de início rápido para usar o Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="070f3-103">Quickstart for using the Azure Cloud Shell</span></span>

<span data-ttu-id="070f3-104">Este documento fornece detalhes sobre como usar o Azure Cloud Shell no [Portal do Azure](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="070f3-104">This document details how to use the Azure Cloud Shell in the [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="070f3-105">Iniciar o Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="070f3-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="070f3-106">Inicie o **Cloud Shell** no painel de navegação superior do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="070f3-106">Launch **Cloud Shell** from the top navigation of the Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="070f3-107">Selecione uma assinatura para criar uma conta de armazenamento e um compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="070f3-107">Select a subscription to create a storage account and Azure file share</span></span>
3. <span data-ttu-id="070f3-108">Selecione "Criar armazenamento"</span><span class="sxs-lookup"><span data-stu-id="070f3-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="070f3-109">Você é autenticado automaticamente na CLI do Azure 2.0 em cada sessão.</span><span class="sxs-lookup"><span data-stu-id="070f3-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="070f3-110">Definir sua assinatura</span><span class="sxs-lookup"><span data-stu-id="070f3-110">Set your subscription</span></span>
1. <span data-ttu-id="070f3-111">Liste as assinaturas a que você tem acesso:</span><span class="sxs-lookup"><span data-stu-id="070f3-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="070f3-112">Defina sua assinatura preferencial:</span><span class="sxs-lookup"><span data-stu-id="070f3-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="070f3-113">Sua assinatura será lembrada em sessões futuras com o uso de `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="070f3-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="070f3-114">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="070f3-114">Create a resource group</span></span>
<span data-ttu-id="070f3-115">Crie um novo grupo de recursos no Oeste dos EUA chamado "MyRG":</span><span class="sxs-lookup"><span data-stu-id="070f3-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="070f3-116">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="070f3-116">Create a Linux VM</span></span>
<span data-ttu-id="070f3-117">Crie uma VM do Ubuntu em seu novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="070f3-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="070f3-118">A CLI do Azure 2.0 criará chaves SSH e configurará a VM com elas.</span><span class="sxs-lookup"><span data-stu-id="070f3-118">The Azure CLI 2.0 will create SSH keys and setup the VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="070f3-119">Por padrão, as chaves pública e privada usadas para autenticar sua VM são colocadas em `/User/.ssh/id_rsa` e `/User/.ssh/id_rsa.pub` pela CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="070f3-119">The public and private keys used to authenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="070f3-120">Sua pasta .ssh é mantida na imagem de 5 GB do compartilhamento de arquivos anexado do Azure.</span><span class="sxs-lookup"><span data-stu-id="070f3-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="070f3-121">Seu nome de usuário nessa VM será o nome de usuário usado no Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="070f3-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="070f3-122">SSH em sua VM Linux</span><span class="sxs-lookup"><span data-stu-id="070f3-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="070f3-123">Pesquise pelo nome de sua VM na barra de pesquisa do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="070f3-123">Search for your VM name in the Azure portal search bar</span></span>
2. <span data-ttu-id="070f3-124">Clique em "Conectar" e execute: `ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="070f3-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="070f3-125">Após estabelecer a conexão SSH, você deverá ver o prompt de boas-vindas do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="070f3-125">Upon establishing the SSH connection, you should see the Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="070f3-126">Limpando</span><span class="sxs-lookup"><span data-stu-id="070f3-126">Cleaning up</span></span> 
<span data-ttu-id="070f3-127">Exclua o grupo de recursos e todos os recursos dentro dele:</span><span class="sxs-lookup"><span data-stu-id="070f3-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="070f3-128">Execute o `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="070f3-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="070f3-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="070f3-129">Next Steps</span></span>
[<span data-ttu-id="070f3-130">Saiba mais sobre o armazenamento persistente no Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="070f3-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="070f3-131">
[Saiba mais sobre a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="070f3-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="070f3-132">
[Saiba mais sobre o armazenamento de Arquivos do Azure](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="070f3-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>