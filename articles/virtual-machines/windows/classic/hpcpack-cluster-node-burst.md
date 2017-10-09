---
title: "cluster de HPC Pack aaaAdd intermitência nós tooan | Microsoft Docs"
description: "Saiba como tooexpand um pacote de HPC cluster no Azure sob demanda, adicionando instâncias de função de trabalho em execução em um serviço de nuvem"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>Adicionar o cluster sob demanda "disparar" nós tooan HPC Pack no Azure
Se você configurar um [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster no Azure, talvez seja uma maneira tooquickly escala Olá capacidade do cluster para cima ou para baixo, sem manter um conjunto de VMs do nó de computação pré-configurados. Este artigo mostra como tooadd sob demanda "disparar" nós (instâncias de função trabalho em execução em um serviço de nuvem) como o nó principal de tooa do recursos de computação no Azure. 

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

![Nós de disparo contínuo][burst]

Olá etapas neste artigo ajudá-lo a adicionar nós do Azure rapidamente tooa baseado em nuvem HPC Pack VM do nó principal para uma implantação de teste ou prova de conceito. etapas de alto nível Olá são Olá mesmas etapas Olá muito "disparar tooAzure" cluster de HPC Pack de local de tooan de capacidade de computação em nuvem de tooadd. Para obter um tutorial, veja [Configurar um cluster de cálculo híbrido com o Microsoft HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Para obter orientação detalhada e considerações para implantações de produção, consulte [disparar tooAzure com Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).

## <a name="prerequisites"></a>Pré-requisitos
* **Nó de cabeçalho do HPC Pack implantado em uma VM do Azure** – Você pode usar uma VM de nó de cabeçalho autônomo ou uma que faça parte de um cluster maior. toocreate um nó de cabeçalho autônomo, consulte [implantar um nó de cabeçalho do HPC Pack em uma VM do Azure](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para opções de implantação de cluster de HPC Pack automatizado, consulte [opções toocreate e gerenciar um cluster de HPC do Windows Azure com Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
  > [!TIP]
  > Se você usar o hello [script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md) toocreate Olá cluster no Azure, você pode incluir nós de disparo do Azure em sua implantação automatizada. Consulte exemplos de saudação nesse artigo.
  > 
  > 
* **Assinatura do Azure** -tooadd Azure nós, você pode escolher Olá a mesma assinatura usada toodeploy Olá VM do nó principal, ou uma assinatura diferente (ou assinaturas).
* **Cota de núcleos** -você pode precisar de uma cota de saudação tooincrease de núcleos, especialmente se você escolher toodeploy vários nós do Azure com tamanhos de vários núcleos. uma cota de tooincrease [abrir uma solicitação de suporte do cliente online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sem custo adicional.

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>Etapa 1: Criar um serviço de nuvem e uma conta de armazenamento para Olá nós do Azure
Use Olá portal clássico do Azure ou saudação de tooconfigure ferramentas equivalentes a seguir de recursos que são necessário toodeploy seus nós do Azure:

* Um novo serviço de nuvem do Azure
* Uma nova conta de armazenamento do Azure

> [!NOTE]
> Não reutilize um serviço de nuvem existente em sua assinatura. 
> 
> 

**Considerações**

* Configure um serviço de nuvem separado para cada modelo de nó do Azure que você planeje toocreate. No entanto, você pode usar Olá a mesma conta de armazenamento para vários modelos de nó.
* É recomendável que você localize Olá serviço em nuvem e conta de armazenamento Olá para implantação de saudação em Olá mesma região do Azure.

## <a name="step-2-configure-an-azure-management-certificate"></a>Etapa 2: configurar um certificado de gerenciamento do Azure
tooadd Azure nós como recursos de computação, você precisa de um certificado de gerenciamento no nó principal hello e carregamento correspondente toohello assinatura do Azure usada para implantação de saudação do certificado.

Para este cenário, você pode escolher Olá **padrão certificado de gerenciamento do HPC Azure** que HPC Pack instala e configura automaticamente no nó principal. Este certificado é útil para implantações de prova de conceito e fins de teste. toouse certificado, carregue o arquivo C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer do nó principal do hello assinatura de toothe VM. certificado tooupload Olá Olá [portal clássico do Azure](https://manage.windowsazure.com), clique em **configurações** > **certificados de gerenciamento**.

Opções adicionais tooconfigure Olá certificado de gerenciamento, consulte [Olá tooConfigure de cenários certificado de gerenciamento do Azure para implantações de disparo do Azure](http://technet.microsoft.com/library/gg481759.aspx).

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>Etapa 3: Implantar um cluster de toohello de nós do Azure
Olá tooadd etapas e iniciar o Azure nós neste cenário geralmente são Olá mesmo como etapas Olá com um nó principal local. Para obter mais informações, consulte Olá seções a seguir [etapas tooDeploy nós do Azure com Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):

* Criar um modelo de nó do Azure
* Adicionar o cluster do Windows HPC toohello nós do Azure
* Iniciar (provisionar) Olá nós do Azure

Depois de adicionar e iniciar os nós hello, que estejam prontos para você toouse toorun trabalhos em cluster.

Se tiver problemas ao implantar nós do Azure, veja [Troubleshoot Deployments of Azure Nodes with Microsoft HPC Pack](http://technet.microsoft.com/library/jj159097.aspx)(Solucionar problemas de nós do Azure com o Microsoft HPC Pack).

## <a name="next-steps"></a>Próximas etapas
* nós de disparo toouse um tamanho de instância de computação intensa para hello, consulte Considerações Olá [tamanhos de VM de computação de alto desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Se você quiser aumentar ou reduzir automaticamente Olá recursos de acordo com a carga de trabalho do hello cluster de computação do Azure, consulte [automaticamente aumentar e reduzir os recursos de computação do Azure em um cluster de HPC Pack](hpcpack-cluster-node-autogrowshrink.md).

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
