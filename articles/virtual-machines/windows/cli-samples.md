---
title: aaaAzure CLI do Windows | Microsoft Docs
description: Exemplos de CLI do Azure - Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eef61a24d14897dd0a88a3f467854cc21b1938d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="5e57f-103">Exemplos de CLI do Azure para máquinas virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="5e57f-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="5e57f-104">Olá tabela a seguir inclui links toobash scripts criados usando Olá CLI do Azure implantar máquinas virtuais do Windows.</span><span class="sxs-lookup"><span data-stu-id="5e57f-104">hello following table includes links toobash scripts built using hello Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="5e57f-105">**Criar máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="5e57f-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="5e57f-106">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5e57f-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="5e57f-107">Cria uma máquina virtual do Windows com configuração mínima.</span><span class="sxs-lookup"><span data-stu-id="5e57f-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="5e57f-108">Criar uma máquina virtual totalmente configurada</span><span class="sxs-lookup"><span data-stu-id="5e57f-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="5e57f-109">Cria um grupo de recursos, a máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="5e57f-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="5e57f-110">Criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="5e57f-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="5e57f-111">Cria várias máquinas virtuais em uma configuração altamente disponíveis e de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="5e57f-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="5e57f-112">Criar uma máquina virtual e executar o script de configuração</span><span class="sxs-lookup"><span data-stu-id="5e57f-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="5e57f-113">Cria uma máquina virtual e usa hello Azure personalizado Script extensão tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="5e57f-113">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="5e57f-114">Criar uma máquina virtual e executar a configuração da DSC</span><span class="sxs-lookup"><span data-stu-id="5e57f-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="5e57f-115">Cria uma máquina virtual e usa tooinstall de extensão de configuração de estado desejado (DSC) da Azure Olá IIS.</span><span class="sxs-lookup"><span data-stu-id="5e57f-115">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
|<span data-ttu-id="5e57f-116">**Máquinas virtuais de rede**</span><span class="sxs-lookup"><span data-stu-id="5e57f-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="5e57f-117">Proteger o tráfego de rede entre as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5e57f-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="5e57f-118">Cria duas máquinas virtuais, todos os recursos relacionados e grupos de segurança de rede (NSG) internos e externos.</span><span class="sxs-lookup"><span data-stu-id="5e57f-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="5e57f-119">**Proteger máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="5e57f-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="5e57f-120">Criptografar uma VM e discos de dados</span><span class="sxs-lookup"><span data-stu-id="5e57f-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="5e57f-121">Cria um Azure Key Vault, uma chave de criptografia e entidade de serviço e, em seguida, criptografa uma VM.</span><span class="sxs-lookup"><span data-stu-id="5e57f-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="5e57f-122">**Monitorar máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="5e57f-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="5e57f-123">Monitorar uma VM com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="5e57f-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="5e57f-124">Cria uma máquina virtual, instala o agente do Operations Management Suite hello e registra Olá VM em um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="5e57f-124">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |
