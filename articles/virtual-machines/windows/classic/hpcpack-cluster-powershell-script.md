---
title: cluster do Windows HPC aaaPowerShell script toodeploy | Microsoft Docs
description: "Executar um toodeploy de script do PowerShell um cluster do Windows HPC Pack 2012 R2 em máquinas virtuais do Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Criar um cluster de computação de alto desempenho (HPC) do Windows com o script de implantação de IaaS do HPC Pack Olá
Execute Olá HPC Pack IaaS implantação PowerShell script toodeploy um cluster de HPC Pack 2012 R2 completo para cargas de trabalho do Windows em máquinas virtuais do Azure. Olá cluster consiste em um nó principal do Active Directory associado que executam o Windows Server e Microsoft HPC Pack e janelas adicionais de computação recursos que você especificar. Se você quiser toodeploy um cluster de HPC Pack no Azure para cargas de trabalho do Linux, consulte [criar um cluster de HPC Linux com hello script de implantação IaaS do HPC Pack](../../linux/classic/hpcpack-cluster-powershell-script.md). Você também pode usar um modelo de Gerenciador de recursos do Azure toodeploy um cluster de HPC Pack. Para obter exemplos, confira [Criar um cluster HPC](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) e [Criar um cluster HPC com uma imagem do nó de computação personalizada](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).

> [!IMPORTANT] 
> Olá script do PowerShell descrito neste artigo cria um cluster do Microsoft HPC Pack 2012 R2 no Azure usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.
> Além disso, o script hello descrito neste artigo não dá suporte a HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a>Exemplo de arquivos de configuração
Olá exemplos a seguir, substitua seus próprios valores para a Id da assinatura ou nome e nomes de conta e o serviço de saudação.

### <a name="example-1"></a>Exemplo 1
Olá seguinte arquivo de configuração implanta um cluster de HPC Pack que tem cinco nós de computação executando o sistema de operacional do Windows Server 2012 R2 hello e um nó principal com bancos de dados locais. Todos os serviços de nuvem Olá são criados diretamente no hello local Oeste dos EUA. nó principal Olá atua como controlador de domínio da floresta de domínio hello.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a>Exemplo 2
Olá, arquivo de configuração a seguir implanta um cluster de HPC Pack em uma floresta de domínio existente. cluster Olá tem 1 nó principal com bancos de dados locais e 12 nós com hello extensão BGInfo VM aplicada de computação.
A instalação automática de atualizações do Windows está desabilitada para Olá todas as VMs na floresta de domínio hello. Todos os serviços de nuvem Olá são criados diretamente no local Ásia Oriental. nós de computação Olá são criados em três serviços de nuvem e três contas de armazenamento: *MyHPCCN-0001* muito*MyHPCCN-0005* na *MyHPCCNService01* e  *mycnstorage01*; *MyHPCCN-0006* muito*MyHPCCN0010* na *MyHPCCNService02* e *mycnstorage02*; e  *MyHPCCN-0011* muito*MyHPCCN-0012* na *MyHPCCNService03* e *mycnstorage03*). nós de computação Olá são criados de uma imagem privada existente capturada de um nó de computação. Olá automaticamente aumentar ou reduzir serviço está habilitado com padrão ampliar ou reduzir os intervalos.

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a>Exemplo 3
Olá, arquivo de configuração a seguir implanta um cluster de HPC Pack em uma floresta de domínio existente. cluster Olá contém um nó de cabeçalho, um servidor de banco de dados com um disco de dados de 500 GB, dois nós do agente executando o sistema de operacional do Windows Server 2012 R2 hello e cinco nós de computação executando o sistema de operacional do Windows Server 2012 R2 hello. Olá MyHPCCNService é criado no grupo de afinidade de saudação do serviço de nuvem *MyIBAffinityGroup*, e hello outros serviços em nuvem são criados no grupo de afinidade Olá *MyAffinityGroup*. Olá API de REST do Agendador de trabalho do HPC e o portal da web do HPC estão habilitados no nó de cabeçalho hello.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a>Exemplo 4
Olá, arquivo de configuração a seguir implanta um cluster de HPC Pack em uma floresta de domínio existente. cluster Olá tem dois nó principal com bancos de dados locais, dois modelos de nó do Azure são criados e três nós do tamanho médio Azure são criados para o modelo de nó do Azure *AzureTemplate1*. Um arquivo de script é executado no nó principal Olá após a configuração do nó principal hello.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a>Solucionar problemas
* **Erro "VNet não existe"** -se você executar Olá script toodeploy vários clusters no Azure simultaneamente em uma assinatura, uma ou mais implantações podem falhar com o erro hello "VNet *VNet\_nome* não existe".
  Se esse erro ocorrer, execute o script de saudação novamente para Olá Falha na implantação.
* **Problema ao acessar Olá Internet da rede virtual do Azure de saudação** - se criar um cluster com um novo controlador de domínio usando o script de implantação hello, ou manualmente promover um controlador de toodomain VM do nó principal, você pode enfrentar problemas Conectando Olá VMs toohello da Internet. Esse problema pode ocorrer se um servidor DNS encaminhador for configurado automaticamente no controlador de domínio Olá, e esse servidor DNS encaminhador não resolve corretamente.
  
    toowork alternativa para esse problema, faça logon no controlador de domínio toohello e qualquer definição de configuração do encaminhador de Olá remover ou configurar um servidor DNS encaminhador válido. tooconfigure essa configuração, no Gerenciador de servidores clique **ferramentas** >
    **DNS** tooopen Gerenciador DNS e, em seguida, clique duas vezes em **encaminhadores**.
* **Problema ao acessar a rede RDMA de VMs de computação intensa** - se adicionar computadores Windows Server ou nó do agente usando um compatíveis com RDMA de VMs de tamanho, como A8 ou A9, você pode enfrentar problemas de conexão de rede do aplicativo essas VMs toohello RDMA. Um motivo que ocorrer esse problema é se Olá extensão HpcVmDrivers não está instalado corretamente quando Olá VMs são adicionadas toohello cluster. Por exemplo, a extensão pode estar paralisada na Olá estado de instalação.
  
    toowork alternativa para esse problema, primeiro verificar Olá estado da extensão Olá Olá VMs. Se a extensão de saudação não está instalado corretamente, tente remover nós de saudação do cluster HPC hello e adicione nós Olá novamente. Por exemplo, você pode adicionar o nó de computação VMs executando o script Add-hpciaasnode.ps1 de saudação no nó de cabeçalho hello.

## <a name="next-steps"></a>Próximas etapas
* Tente executar uma carga de trabalho de teste no cluster hello. Para obter um exemplo, consulte Olá HPC Pack [guia de Introdução](https://technet.microsoft.com/library/jj884144).
* Para um tutorial tooscript Olá a implantação de cluster e execute uma carga de trabalho do HPC, consulte [começar com um cluster de HPC Pack em cargas de trabalho do Excel e SOA Azure toorun](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Tente toostart de ferramentas do HPC Pack, parar, adicionar e remover nós de computação de um cluster que você criar. Consulte [Gerenciar nós de computação em um cluster de Pacote HPC no Azure](hpcpack-cluster-node-manage.md).
* tooget configurar o cluster de toohello trabalhos toosubmit de um computador local, consulte [cluster trabalhos de HPC de envio de um computador de local tooan HPC Pack no Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

