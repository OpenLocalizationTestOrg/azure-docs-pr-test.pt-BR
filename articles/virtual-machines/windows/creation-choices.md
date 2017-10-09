---
title: maneiras de aaaDifferent toocreate uma VM do Windows Azure | Microsoft Docs
description: "Lista maneiras diferentes de saudação toocreate uma máquina virtual com o Gerenciador de recursos do Windows."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="23be9-103">Diferentes maneiras toocreate uma máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="23be9-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="23be9-104">O Azure oferece toocreate de diferentes maneiras uma máquina virtual porque as máquinas virtuais são adequadas para fins e usuários diferentes.</span><span class="sxs-lookup"><span data-stu-id="23be9-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="23be9-105">Isso significa que você precise toomake algumas opções sobre a máquina virtual de saudação e como toocreate-lo.</span><span class="sxs-lookup"><span data-stu-id="23be9-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="23be9-106">Este artigo fornece um resumo dessas opções e links tooinstructions.</span><span class="sxs-lookup"><span data-stu-id="23be9-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="23be9-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="23be9-107">Azure portal</span></span>
<span data-ttu-id="23be9-108">Usar o portal do Azure de saudação é tootry uma maneira simples-out de uma máquina virtual, especialmente se você estiver começando com o Azure.</span><span class="sxs-lookup"><span data-stu-id="23be9-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="23be9-109">Criar uma máquina virtual que executa o Windows usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="23be9-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="23be9-110">Modelo</span><span class="sxs-lookup"><span data-stu-id="23be9-110">Template</span></span>
<span data-ttu-id="23be9-111">As máquinas virtuais exigem uma combinação de recursos (como conjuntos de disponibilidade e contas de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="23be9-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="23be9-112">Em vez de implantar e gerenciar cada recurso separadamente, você pode criar um modelo de Gerenciador de recursos do Azure que implanta e provisiona todos os recursos de saudação em uma única operação coordenado.</span><span class="sxs-lookup"><span data-stu-id="23be9-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="23be9-113">Criar uma máquina virtual do Windows com um modelo do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="23be9-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="23be9-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="23be9-114">Azure PowerShell</span></span>
<span data-ttu-id="23be9-115">Se preferir trabalhar em um shell de comando, será possível usar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23be9-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="23be9-116">Criar uma VM do Windows usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="23be9-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="23be9-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="23be9-117">Visual Studio</span></span>
<span data-ttu-id="23be9-118">Usar toobuild do Visual Studio, gerenciar, implantar VMs com hello Azure Tools para Visual Studio e Olá SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="23be9-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="23be9-119">Ferramentas do Azure para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="23be9-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

