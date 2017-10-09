---
title: "aaaCreate uma VM do Linux clássica usando Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual de Linux com hello Azure CLI 1.0 usando Olá modelo de implantação clássico"
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
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="255c8-103">Como tooCreate uma VM do Linux clássica com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="255c8-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="255c8-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="255c8-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="255c8-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="255c8-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="255c8-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="255c8-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="255c8-107">Para a versão do Gerenciador de recursos de hello, consulte [aqui](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="255c8-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="255c8-108">Este tópico descreve como toocreate uma máquina virtual do Linux (VM) com o uso de hello Azure CLI 1.0 Olá modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="255c8-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="255c8-109">Podemos usar uma imagem do Linux do hello disponível **imagens** no Azure.</span><span class="sxs-lookup"><span data-stu-id="255c8-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="255c8-110">comandos de saudação 1.0 da CLI do Azure oferecem Olá opções de configuração, entre outros:</span><span class="sxs-lookup"><span data-stu-id="255c8-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="255c8-111">Conexão de rede virtual do hello VM tooa</span><span class="sxs-lookup"><span data-stu-id="255c8-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="255c8-112">Adicionar serviço de nuvem existente do hello VM tooan</span><span class="sxs-lookup"><span data-stu-id="255c8-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="255c8-113">Adicionar conta de armazenamento existente do hello VM tooan</span><span class="sxs-lookup"><span data-stu-id="255c8-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="255c8-114">Adicionar conjunto de disponibilidade Olá VM tooan ou local</span><span class="sxs-lookup"><span data-stu-id="255c8-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="255c8-115">Se você quiser toouse sua VM uma rede virtual para que possa conectar tooit diretamente pelo nome de host ou configurar conexões entre locais, certifique-se de que especificar rede virtual hello quando você cria Olá VM.</span><span class="sxs-lookup"><span data-stu-id="255c8-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="255c8-116">Uma VM pode ser configurado toojoin uma rede virtual somente quando você cria Olá VM.</span><span class="sxs-lookup"><span data-stu-id="255c8-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="255c8-117">Para mais detalhes sobre redes virtuais, consulte [Visão geral da rede virtual do Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="255c8-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="255c8-118">Como toocreate uma VM do Linux usando Olá modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="255c8-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

