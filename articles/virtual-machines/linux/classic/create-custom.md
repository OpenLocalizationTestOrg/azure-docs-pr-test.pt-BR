---
title: "Criar uma VM Clássica do Linux usando a CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como criar uma máquina virtual do Linux com a CLI do Azure 1.0 usando o modelo de implantação Clássico"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 8ddbacbbb70c0cf1a2537fab4d981a316610a4d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-classic-linux-vm-with-the-azure-cli-10"></a><span data-ttu-id="8eba1-103">Como criar uma VM Clássica do Linux com a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="8eba1-103">How to Create a Classic Linux VM with the Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="8eba1-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8eba1-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8eba1-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="8eba1-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8eba1-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="8eba1-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8eba1-107">Para a versão do Resource Manager, consulte [aqui](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8eba1-107">For the Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8eba1-108">Este tópico descreve como criar uma VM (máquina virtual) do Linux com a CLI do Azure 1.0 usando o modelo de implantação Clássico.</span><span class="sxs-lookup"><span data-stu-id="8eba1-108">This topic describes how to create a Linux virtual machine (VM) with the Azure CLI 1.0 using the Classic deployment model.</span></span> <span data-ttu-id="8eba1-109">Vamos usar uma imagem do Linux das **IMAGENS** disponíveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="8eba1-109">We use a Linux image from the available **IMAGES** on Azure.</span></span> <span data-ttu-id="8eba1-110">Os comandos da CLI do Azure 1.0 oferecem as seguintes opções de configuração, entre outras:</span><span class="sxs-lookup"><span data-stu-id="8eba1-110">The Azure CLI 1.0 commands give the following configuration choices, among others:</span></span>

* <span data-ttu-id="8eba1-111">Conectar a VM a uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="8eba1-111">Connecting the VM to a virtual network</span></span>
* <span data-ttu-id="8eba1-112">Adicionar a VM a um serviço de nuvem existente</span><span class="sxs-lookup"><span data-stu-id="8eba1-112">Adding the VM to an existing cloud service</span></span>
* <span data-ttu-id="8eba1-113">Adicionar a VM a uma conta de armazenamento existente</span><span class="sxs-lookup"><span data-stu-id="8eba1-113">Adding the VM to an existing storage account</span></span>
* <span data-ttu-id="8eba1-114">Adicionar a VM a um conjunto de disponibilidade ou local.</span><span class="sxs-lookup"><span data-stu-id="8eba1-114">Adding the VM to an availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8eba1-115">Se você quiser que sua VM use uma rede virtual para que possa se conectar às suas máquinas virtuais diretamente pelo nome do host ou estabelecer conexões entre locais, especifique a rede virtual ao criar a VM.</span><span class="sxs-lookup"><span data-stu-id="8eba1-115">If you want your VM to use a virtual network so you can connect to it directly by hostname or set up cross-premises connections, make sure you specify the virtual network when you create the VM.</span></span> <span data-ttu-id="8eba1-116">Uma máquina virtual poderá ser configurada para ingressar em uma rede virtual somente quando você criar a VM.</span><span class="sxs-lookup"><span data-stu-id="8eba1-116">A VM can be configured to join a virtual network only when you create the VM.</span></span> <span data-ttu-id="8eba1-117">Para mais detalhes sobre redes virtuais, consulte [Visão geral da rede virtual do Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="8eba1-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-to-create-a-linux-vm-using-the-classic-deployment-model"></a><span data-ttu-id="8eba1-118">Como criar uma VM do Linux usando o modelo de implantação Clássico</span><span class="sxs-lookup"><span data-stu-id="8eba1-118">How to create a Linux VM using the Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

