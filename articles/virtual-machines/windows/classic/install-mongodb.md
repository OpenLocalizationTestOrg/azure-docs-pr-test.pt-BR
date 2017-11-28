---
title: aaaInstall MongoDB em uma VM do Windows Azure | Microsoft Docs
description: "Saiba como tooinstall MongoDB em uma VM do Azure criado com o modelo de implantação clássico Olá executando o Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="b615a-103">Instalar o MongoDB em uma VM do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="b615a-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b615a-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b615a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b615a-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="b615a-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b615a-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b615a-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b615a-107">tooinstall e configurar usando o modelo de implantação do Gerenciador de recursos de saudação do MongoDB, consulte [neste artigo](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="b615a-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="b615a-108">[O MongoDB][MongoDB] é um popular banco de dados NoSQL de software livre e alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="b615a-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="b615a-109">Este artigo o orienta pelo processo de criação de uma máquina virtual do Windows Server (VM) usando Olá [portal do Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="b615a-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="b615a-110">Em seguida, você cria e anexar um disco de dados toohello VM antes de instalar e configurar o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b615a-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="b615a-111">Se você tiver uma VM existente no Azure que deseja toouse, você pode ir direto muito[instalando e configurando o MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="b615a-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="b615a-112">Criar uma máquina virtual na qual o Windows Server está em execução</span><span class="sxs-lookup"><span data-stu-id="b615a-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="b615a-113">Siga essas instruções toocreate uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b615a-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="b615a-114">Você pode adicionar um ponto de extremidade para o MongoDB ao criar a máquina virtual de saudação e configurá-lo da seguinte maneira: nome-o como **Mongo**, use **TCP** como protocolo de saudação e defina os dois Olá portas públicas e privadas muito**27017**.</span><span class="sxs-lookup"><span data-stu-id="b615a-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="b615a-115">Anexar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="b615a-115">Attach a data disk</span></span>
<span data-ttu-id="b615a-116">tooprovide armazenamento da máquina virtual de hello, anexar um disco de dados e inicializá-lo para que o Windows pode usá-lo.</span><span class="sxs-lookup"><span data-stu-id="b615a-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="b615a-117">Se já tiver um disco de dados, você poderá anexar esse disco ou um disco vazio.</span><span class="sxs-lookup"><span data-stu-id="b615a-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="b615a-118">Para obter instruções sobre como inicializar disco hello, consulte "como: inicializar um novo disco de dados no Windows Server" em [como tooattach dados de um disco máquina de virtual do Windows tooa](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="b615a-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="b615a-119">Instalar e executar o MongoDB na máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="b615a-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="b615a-120">Resumo</span><span class="sxs-lookup"><span data-stu-id="b615a-120">Summary</span></span>
<span data-ttu-id="b615a-121">Neste tutorial, você aprendeu como toocreate uma máquina virtual executando o Windows Server, se conectam remotamente tooit e anexar um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="b615a-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="b615a-122">Você também aprendeu como tooinstall e configurar o MongoDB na máquina virtual baseados em Windows de saudação.</span><span class="sxs-lookup"><span data-stu-id="b615a-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="b615a-123">Agora você pode acessar o MongoDB na máquina de virtual baseado em Windows hello, por seguintes Olá avançado tópicos Olá [documentação do MongoDB][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="b615a-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

