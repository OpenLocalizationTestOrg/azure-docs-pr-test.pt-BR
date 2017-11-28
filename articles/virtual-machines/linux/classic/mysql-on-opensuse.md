---
title: aaaInstall MySQL em uma VM OpenSUSE | Microsoft Docs
description: "Saiba tooinstall MySQL em uma máquina OpenSUSE Linux VMirtual no Azure."
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
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="107c7-103">Instalar MySQL em uma máquina virtual com o OpenSUSE Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="107c7-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="107c7-104">O [MySQL][MySQL] é um popular Banco de Dados SQL de software livre.</span><span class="sxs-lookup"><span data-stu-id="107c7-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="107c7-105">Este tutorial mostra como toocreate uma máquina virtual executando o OpenSUSE Linux, em seguida, instalar o MySQL.</span><span class="sxs-lookup"><span data-stu-id="107c7-105">This tutorial shows you how toocreate a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="107c7-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="107c7-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="107c7-107">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="107c7-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="107c7-108">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="107c7-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="107c7-109">Criar uma máquina virtual que executa o OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="107c7-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a><span data-ttu-id="107c7-110">Instalar e executar o MySQL na máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="107c7-110">Install and run MySQL on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="107c7-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="107c7-111">Next steps</span></span>
<span data-ttu-id="107c7-112">Para obter detalhes sobre o MySQL, consulte Olá [documentação do MySQL][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="107c7-112">For details about MySQL, see hello [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

