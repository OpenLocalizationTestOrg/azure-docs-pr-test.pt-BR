---
title: Exemplos de CLI do Azure - Windows | Microsoft Docs
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
ms.openlocfilehash: f4b2e8a5583855df7472af3fbef01ac641caf6bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="b866b-103">Exemplos de CLI do Azure para máquinas virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="b866b-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="b866b-104">A tabela a seguir inclui links para scripts bash criados usando a CLI do Azure que implanta máquinas virtuais do Windows.</span><span class="sxs-lookup"><span data-stu-id="b866b-104">The following table includes links to bash scripts built using the Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="b866b-105">**Criar máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="b866b-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="b866b-106">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b866b-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="b866b-107">Cria uma máquina virtual do Windows com configuração mínima.</span><span class="sxs-lookup"><span data-stu-id="b866b-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="b866b-108">Criar uma máquina virtual totalmente configurada</span><span class="sxs-lookup"><span data-stu-id="b866b-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="b866b-109">Cria um grupo de recursos, a máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="b866b-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="b866b-110">Criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="b866b-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="b866b-111">Cria várias máquinas virtuais em uma configuração altamente disponíveis e de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="b866b-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="b866b-112">Criar uma máquina virtual e executar o script de configuração</span><span class="sxs-lookup"><span data-stu-id="b866b-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="b866b-113">Cria uma máquina virtual e usa a Extensão de Script Personalizado do Azure para instalar o IIS.</span><span class="sxs-lookup"><span data-stu-id="b866b-113">Creates a virtual machine and uses the Azure Custom Script extension to install IIS.</span></span> |
| [<span data-ttu-id="b866b-114">Criar uma máquina virtual e executar a configuração da DSC</span><span class="sxs-lookup"><span data-stu-id="b866b-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="b866b-115">Cria uma máquina virtual e usa a extensão DSC (Configuração de Estado de Desejado) do Azure para instalar o IIS.</span><span class="sxs-lookup"><span data-stu-id="b866b-115">Creates a virtual machine and uses the Azure Desired State Configuration (DSC) extension to install IIS.</span></span> |
|<span data-ttu-id="b866b-116">**Máquinas virtuais de rede**</span><span class="sxs-lookup"><span data-stu-id="b866b-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="b866b-117">Proteger o tráfego de rede entre as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="b866b-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="b866b-118">Cria duas máquinas virtuais, todos os recursos relacionados e grupos de segurança de rede (NSG) internos e externos.</span><span class="sxs-lookup"><span data-stu-id="b866b-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="b866b-119">**Proteger máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="b866b-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="b866b-120">Criptografar uma VM e discos de dados</span><span class="sxs-lookup"><span data-stu-id="b866b-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="b866b-121">Cria um Azure Key Vault, uma chave de criptografia e entidade de serviço e, em seguida, criptografa uma VM.</span><span class="sxs-lookup"><span data-stu-id="b866b-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="b866b-122">**Monitorar máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="b866b-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="b866b-123">Monitorar uma VM com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="b866b-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="b866b-124">Cria uma máquina virtual, instala o agente do Operations Management Suite e registra a VM em um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="b866b-124">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
| | |
