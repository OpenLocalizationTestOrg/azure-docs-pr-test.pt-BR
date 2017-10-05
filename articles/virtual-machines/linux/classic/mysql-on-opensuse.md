---
title: Instalar o MySQL em uma VM OpenSUSE | Microsoft Docs
description: "Saiba como instalar o MySQL em uma máquina virtual Linux OpenSUSE no Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 01b798a25575b66f89057315ce80d6cc0cde53b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="2795e-103">Instalar MySQL em uma máquina virtual com o OpenSUSE Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="2795e-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="2795e-104">O [MySQL][MySQL] é um popular Banco de Dados SQL de software livre.</span><span class="sxs-lookup"><span data-stu-id="2795e-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="2795e-105">Este tutorial mostra como criar uma máquina virtual com o OpenSUSE Linux e instalar o MySQL.</span><span class="sxs-lookup"><span data-stu-id="2795e-105">This tutorial shows you how to create a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2795e-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2795e-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2795e-107">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="2795e-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="2795e-108">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="2795e-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="2795e-109">Criar uma máquina virtual que executa o OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="2795e-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-the-virtual-machine"></a><span data-ttu-id="2795e-110">Instalar e executar MySQL na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2795e-110">Install and run MySQL on the virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="2795e-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2795e-111">Next steps</span></span>
<span data-ttu-id="2795e-112">Para obter detalhes sobre o MySQL, consulte a [Documentação do MySQL][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="2795e-112">For details about MySQL, see the [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

