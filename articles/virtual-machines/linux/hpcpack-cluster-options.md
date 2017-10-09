---
title: "Opções de cluster de HPC Pack aaaLinux na nuvem Olá | Microsoft Docs"
description: "Saiba mais sobre opções com Microsoft HPC Pack toocreate e gerenciar um Linux computação de alto desempenho cluster (HPC) em Olá nuvem do Azure"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a>As opções com HPC Pack toocreate e gerenciar um cluster HPC no Azure para cargas de trabalho do Linux
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Este artigo se concentra em cargas de trabalho de opções toouse HPC Pack toorun Linux. Também há opções para executar [cargas de trabalho de HPC do Windows com o HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Executar um cluster HPC Pack em VMs do Azure
### <a name="azure-templates"></a>Modelos do Azure
* (GitHub) [Modelos de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [Cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)
* (Início rápido) [Criar um cluster HPC Pack com nós de computação do Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)

### <a name="powershell-deployment-script"></a>Script de implantação do PowerShell
* [Criar um cluster de HPC Linux com hello script de implantação IaaS do HPC Pack](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Tutoriais
* [Tutorial: introdução a nós de computação Linux em um cluster de HPC Pack no Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: executar o NAMD com o Microsoft HPC Pack em nós de computação Linux no Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: executar OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Tutorial: executar o STAR-CCM+ com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a>Gerenciamento de clusters
* [Enviar o cluster de HPC Pack tooan trabalhos no Azure](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Gerenciamento de trabalho no HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Criar clusters de RDMA para cargas de trabalho MPI
* [Tutorial: executar OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configurar um aplicativo de MPI toorun Linux RDMA cluster](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

