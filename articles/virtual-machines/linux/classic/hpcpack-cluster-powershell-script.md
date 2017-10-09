---
title: aaaPowerShell script toodeploy cluster HPC do Linux | Microsoft Docs
description: "Executar um toodeploy de script do PowerShell um cluster Linux HPC Pack 2012 R2 em máquinas virtuais do Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Criar um cluster de computação de alto desempenho (HPC) do Linux com script de implantação de IaaS do HPC Pack Olá
Execute Olá HPC Pack IaaS implantação PowerShell script toodeploy um cluster de HPC Pack 2012 R2 completo para cargas de trabalho do Linux em máquinas virtuais do Azure. Olá cluster consiste em um nó principal do Active Directory associado que executam o Windows Server e Microsoft HPC Pack e nós de computação que executam uma saudação distribuições do Linux com suporte pelo pacote de HPC. Se você quiser toodeploy um cluster de HPC Pack em cargas de trabalho do Azure para Windows, consulte [criar um cluster do Windows HPC com hello script de implantação IaaS do HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Você também pode usar um modelo de Gerenciador de recursos do Azure toodeploy um cluster de HPC Pack. Para obter um exemplo, consulte [Criar um cluster HPC com nós de computação Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).

> [!IMPORTANT] 
> Olá script do PowerShell descrito neste artigo cria um cluster do Microsoft HPC Pack 2012 R2 no Azure usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.
> Além disso, o script hello descrito neste artigo não dá suporte a HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>Exemplo de arquivo de configuração
Olá seguinte arquivo de configuração cria um controlador de domínio e floresta de domínio e implanta um cluster de HPC Pack que tem um nó principal com bancos de dados locais e 10 nós de computação do Linux. Todos os serviços de nuvem Olá criados diretamente no local do hello Ásia Oriental. Olá Linux nós de computação são criados em dois serviços de nuvem e duas contas de armazenamento (ou seja, *MyLnxCN-0001* para *MyLnxCN-0005* na *MyLnxCNService01* e *mylnxstorage01*, e *MyLnxCN-0006* para *MyLnxCN 0010* na *MyLnxCNService02* e *mylnxstorage02* ). nós de computação Olá são criados de uma imagem do Linux OpenLogic CentOS versão 7.0. 

Substitua seus próprios valores para o nome da assinatura e nomes de conta e o serviço de saudação.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a>Solucionar problemas
* **Erro "VNet não existe"**. Se você executar toodeploy de script de implantação de IaaS do HPC Pack Olá vários clusters no Azure simultaneamente em uma assinatura, uma ou mais implantações podem falhar com o erro hello "VNet *VNet\_nome* não existe".
  Se esse erro ocorrer, execute script Olá Olá Falha na implantação.
* **Problema ao acessar Olá Internet da rede virtual do Azure de saudação**. Se você criar um cluster de HPC Pack com um novo controlador de domínio usando o script de implantação de hello, ou você promova manualmente um controlador de toodomain VM do nó principal, você pode enfrentar problemas ao conectar Olá VMs em Olá toohello de rede virtual do Azure à Internet. Isso pode ocorrer se um servidor DNS encaminhador for configurado automaticamente no controlador de domínio Olá, e esse servidor DNS encaminhador não resolve corretamente.
  
    toowork alternativa para esse problema, faça logon no controlador de domínio toohello e qualquer definição de configuração do encaminhador de Olá remover ou configurar um servidor DNS encaminhador válido. toodo isso, clique no Gerenciador do servidor **ferramentas** > **DNS** tooopen Gerenciador DNS e, em seguida, clique duas vezes em **encaminhadores**.

## <a name="next-steps"></a>Próximas etapas
* Consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para obter informações sobre distribuições do Linux com suporte, movimentação de dados e envio de cluster de HPC Pack tooan trabalhos com Linux nós de computação.
* Para tutoriais que usam Olá script toocreate um cluster em executar uma carga de trabalho do HPC Linux, consulte:
  * [Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure](hpcpack-cluster-namd.md)
  * [Executar o OpenFOAM com o Pacote HPC da Microsoft em nós de computação do Linux no Azure](hpcpack-cluster-openfoam.md)
  * [Executar o STAR-CCM+ com o Pacote HPC da Microsoft em nós de computação do Linux no Azure](hpcpack-cluster-starccm.md)

