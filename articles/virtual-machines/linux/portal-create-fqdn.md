---
title: aaaCreate FQDN para uma VM do Linux no hello portal do Azure | Microsoft Docs
description: "Saiba como toocreate um nome de domínio totalmente qualificado, ou FQDN, para um Gerenciador de recursos com base em máquina virtual no portal do Azure de saudação."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a><span data-ttu-id="24274-103">Criar um nome de domínio totalmente qualificado no hello portal do Azure para uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="24274-103">Create a fully qualified domain name in hello Azure portal for a Linux VM</span></span>

<span data-ttu-id="24274-104">Quando você cria uma máquina virtual (VM) no hello [portal do Azure](https://portal.azure.com), um recurso IP público para a máquina virtual de saudação é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="24274-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="24274-105">Você usa essa saudação de acesso de tooremotely do endereço IP VM.</span><span class="sxs-lookup"><span data-stu-id="24274-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="24274-106">Embora o portal de saudação não cria um [nome de domínio totalmente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), ou o FQDN, você pode adicionar um depois hello VM é criada.</span><span class="sxs-lookup"><span data-stu-id="24274-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once hello VM is created.</span></span> <span data-ttu-id="24274-107">Este artigo demonstra Olá etapas toocreate um nome DNS ou o FQDN.</span><span class="sxs-lookup"><span data-stu-id="24274-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="24274-108">Criar um FQDN</span><span class="sxs-lookup"><span data-stu-id="24274-108">Create a FQDN</span></span>
<span data-ttu-id="24274-109">Este artigo pressupõe que você já tenha criado uma VM.</span><span class="sxs-lookup"><span data-stu-id="24274-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="24274-110">Se necessário, você pode [criar uma máquina virtual no portal de saudação](quick-create-portal.md) ou [com hello CLI do Azure](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="24274-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with hello Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="24274-111">Siga estas etapas depois que a VM estiver em execução:</span><span class="sxs-lookup"><span data-stu-id="24274-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="24274-112">Você pode se conectar remotamente toohello VM usando este DNS nome, como com `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="24274-112">You can now connect remotely toohello VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24274-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="24274-113">Next steps</span></span>
<span data-ttu-id="24274-114">Agora que sua VM tem um IP público e um nome DNS, é possível implantar estruturas comuns do aplicativo ou serviços, como o nginx, MongoDB, Docker, etc.</span><span class="sxs-lookup"><span data-stu-id="24274-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="24274-115">Leia mais sobre como [usar o Resource Manager](../../azure-resource-manager/resource-group-overview.md) para obter dicas sobre a criação de implantações do Azure.</span><span class="sxs-lookup"><span data-stu-id="24274-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

