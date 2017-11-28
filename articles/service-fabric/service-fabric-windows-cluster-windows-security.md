---
title: "Proteger um cluster em execução no Windows usando a Segurança do Windows | Microsoft Docs"
description: "Saiba como configurar a segurança de nó para nó e de cliente para nó em um cluster autônomo em execução no Windows usando a Segurança do Windows."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: e093a631b0cf81195981a8e3d345504ebce02723
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="c1b1f-103">Proteger um cluster autônomo no Windows usando a Segurança do Windows</span><span class="sxs-lookup"><span data-stu-id="c1b1f-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="c1b1f-104">Para evitar acesso não autorizado a um cluster do Service Fabric, você deve proteger o cluster.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-104">To prevent unauthorized access to a Service Fabric cluster, you must secure the cluster.</span></span> <span data-ttu-id="c1b1f-105">A segurança é especialmente importante quando o cluster executa cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-105">Security is especially important when the cluster runs production workloads.</span></span> <span data-ttu-id="c1b1f-106">Este artigo descreve como configurar a segurança de nó para nó e de cliente para nó usando a Segurança do Windows no arquivo *ClusterConfig.JSON*.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-106">This article describes how to configure node-to-node and client-to-node security by using Windows security in the *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="c1b1f-107">O processo corresponde à etapa configurar segurança de [Criar um cluster autônomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-107">The process corresponds to the configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="c1b1f-108">Para saber mais sobre como o Service Fabric usa a Segurança do Windows, veja [Cenários de segurança de cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c1b1f-109">Você deve considerar a seleção de segurança de nó para nó com cuidado, já que não há nenhuma atualização de cluster de uma opção de segurança para outra.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-109">You should consider the selection of node-to-node security carefully because there is no cluster upgrade from one security choice to another.</span></span> <span data-ttu-id="c1b1f-110">Para alterar a seleção de segurança, você precisa recompilar o cluster completo.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-110">To change the security selection, you have to rebuild the full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="c1b1f-111">Configurar a segurança do Windows usando gMSA</span><span class="sxs-lookup"><span data-stu-id="c1b1f-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="c1b1f-112">O arquivo de configuração *ClusterConfig.gMSA.Windows.MultiMachine.JSON* de exemplo baixado com o pacote de clusters independentes [Microsoft.Azure.ServiceFabric.WindowsServer<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) contém um modelo para a configuração da segurança do Windows usando [Conta de Serviço Gerenciado por Grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="c1b1f-112">The sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| <span data-ttu-id="c1b1f-113">**Parâmetro de configuração**</span><span class="sxs-lookup"><span data-stu-id="c1b1f-113">**Configuration Setting**</span></span> | <span data-ttu-id="c1b1f-114">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="c1b1f-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="c1b1f-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="c1b1f-115">WindowsIdentities</span></span> |<span data-ttu-id="c1b1f-116">Contém as identidades do cluster e do cliente.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-116">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="c1b1f-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="c1b1f-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="c1b1f-118">Configura a segurança de nó para nó.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-118">Configures node-to-node security.</span></span> <span data-ttu-id="c1b1f-119">Uma conta de serviço gerenciado de grupo.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-119">A group managed service account.</span></span> |  
| <span data-ttu-id="c1b1f-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="c1b1f-120">ClusterSPN</span></span> |<span data-ttu-id="c1b1f-121">SPN de domínio totalmente qualificado para a conta gMSA</span><span class="sxs-lookup"><span data-stu-id="c1b1f-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="c1b1f-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="c1b1f-122">ClientIdentities</span></span> |<span data-ttu-id="c1b1f-123">Configura a segurança de cliente para nó.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-123">Configures client-to-node security.</span></span> <span data-ttu-id="c1b1f-124">Uma matriz de contas de usuário do cliente.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="c1b1f-125">Identidade</span><span class="sxs-lookup"><span data-stu-id="c1b1f-125">Identity</span></span> |<span data-ttu-id="c1b1f-126">A identidade do cliente, um usuário de domínio.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-126">The client identity, a domain user.</span></span> |  
| <span data-ttu-id="c1b1f-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="c1b1f-127">IsAdmin</span></span> |<span data-ttu-id="c1b1f-128">True especifica que o usuário de domínio tem acesso de cliente de administrador, false para acesso de cliente de usuário.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-128">True specifies that the domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="c1b1f-129">[A segurança entre nós](service-fabric-cluster-security.md#node-to-node-security) é configurada definindo **ClustergMSAIdentity** quando a malha do serviço precisar ser executada em gMSA.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-129">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs to run under gMSA.</span></span> <span data-ttu-id="c1b1f-130">Para criar as relações de confiança entre os nós, eles deverão estar cientes uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-130">In order to build trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="c1b1f-131">Isso pode ser feito de duas maneiras diferentes: especifique a conta de serviço gerenciada por grupo que inclui todos os nós no cluster, ou especifique o grupo de máquina de domínio que inclui todos os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-131">This can be accomplished in two different ways: Specify the Group Managed Service Account that includes all nodes in the cluster or Specify the domain machine group that includes all nodes in the cluster.</span></span> <span data-ttu-id="c1b1f-132">É altamente recomendável usar a abordagem de [gMSA (Conta de Serviço Gerenciado de Grupo)](https://technet.microsoft.com/library/hh831782.aspx) , especialmente para clusters maiores (com mais de 10 nós) ou para clusters com probabilidade de aumentar ou reduzir.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-132">We strongly recommend using the [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely to grow or shrink.</span></span>  
<span data-ttu-id="c1b1f-133">Essa abordagem não exige a criação de um grupo de domínios para o qual os administradores de cluster receberam direitos de acesso para adicionar e remover membros.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-133">This approach does not require the creation of a domain group for which cluster administrators have been granted access rights to add and remove members.</span></span> <span data-ttu-id="c1b1f-134">Essas contas também são úteis para gerenciamento automático de senha.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="c1b1f-135">Para obter mais informações, confira [Introdução a contas de serviços gerenciados de grupo](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="c1b1f-136">[Segurança de cliente para nó](service-fabric-cluster-security.md#client-to-node-security) é configurada usando **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-136">[Client to node security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="c1b1f-137">Para estabelecer a confiança entre um cliente e o cluster, você deverá configurar o cluster para saber em quais identidades de cliente ele poderá confiar.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-137">In order to establish trust between a client and the cluster, you must configure the cluster to know which client identities that it can trust.</span></span> <span data-ttu-id="c1b1f-138">Isso pode ser feito de duas maneiras diferentes: especifique os usuários do grupo de domínio que podem se conectar ou especifique os usuários de nó do domínio que podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-138">This can be done in two different ways: Specify the domain group users that can connect or specify the domain node users that can connect.</span></span> <span data-ttu-id="c1b1f-139">O Service Fabric oferece suporte a dois tipos de controle de acesso diferentes para clientes conectados a um cluster do Service Fabric: administrador e usuário.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-139">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="c1b1f-140">O controle de acesso oferece a capacidade para que o administrador de cluster limite o acesso a determinados tipos de operação de cluster para diferentes grupos de usuários, tornando o cluster mais seguro.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-140">Access control provides the ability for the cluster administrator to limit access to certain types of cluster operations for different groups of users, making the cluster more secure.</span></span>  <span data-ttu-id="c1b1f-141">Os administradores têm acesso completo aos recursos de gerenciamento (incluindo recursos de leitura/gravação).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-141">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="c1b1f-142">Os usuários, por padrão, têm apenas acesso de leitura aos recursos de gerenciamento (por exemplo, recursos de consulta) e a capacidade de resolver serviços e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-142">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span> <span data-ttu-id="c1b1f-143">Para saber mais sobre controles de acesso, veja [Controle de acesso baseado em função para clientes do Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="c1b1f-144">A seção de **segurança** do exemplo a seguir configura a segurança do Windows usando gMSA e especifica que os computadores no gMSA *ServiceFabric/clusterA.contoso.com* fazem parte do cluster e que *CONTOSO\usera* tem acesso de cliente do administrador:</span><span class="sxs-lookup"><span data-stu-id="c1b1f-144">The following example **security** section configures Windows security using gMSA and specifies that the machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of the cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="c1b1f-145">Configurar a segurança do Windows usando um grupo de máquinas</span><span class="sxs-lookup"><span data-stu-id="c1b1f-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="c1b1f-146">O arquivo de configuração *ClusterConfig.Windows.MultiMachine.JSON* de exemplo baixado com o pacote de clusters independentes [Microsoft.Azure.ServiceFabric.WindowsServer<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) contém um modelo para a configuração da segurança do Windows.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-146">The sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="c1b1f-147">A segurança do Windows é configurada na seção **Propriedades** :</span><span class="sxs-lookup"><span data-stu-id="c1b1f-147">Windows security is configured in the **Properties** section:</span></span> 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| <span data-ttu-id="c1b1f-148">**Parâmetro de configuração**</span><span class="sxs-lookup"><span data-stu-id="c1b1f-148">**Configuration setting**</span></span> | <span data-ttu-id="c1b1f-149">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="c1b1f-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c1b1f-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="c1b1f-150">ClusterCredentialType</span></span> |<span data-ttu-id="c1b1f-151">**ClusterCredentialType** será definido como *Windows* se ClusterIdentity especificar um Nome de Grupo de Máquinas do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-151">**ClusterCredentialType** is set to *Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="c1b1f-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="c1b1f-152">ServerCredentialType</span></span> |<span data-ttu-id="c1b1f-153">Definido como *Windows* para habilitar a Segurança do Windows para clientes.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-153">Set to *Windows* to enable Windows security for clients.</span></span><br /><br /><span data-ttu-id="c1b1f-154">Isso indica que os clientes do cluster e o próprio cluster estão sendo executados em um domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-154">This indicates that the clients of the cluster and the cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="c1b1f-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="c1b1f-155">WindowsIdentities</span></span> |<span data-ttu-id="c1b1f-156">Contém as identidades do cluster e do cliente.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-156">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="c1b1f-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="c1b1f-157">ClusterIdentity</span></span> |<span data-ttu-id="c1b1f-158">Use um nome de grupo de computadores, domínio\grupodecomputadores, para configurar a segurança de nó para nó.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-158">Use a machine group name, domain\machinegroup, to configure node-to-node security.</span></span> |  
| <span data-ttu-id="c1b1f-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="c1b1f-159">ClientIdentities</span></span> |<span data-ttu-id="c1b1f-160">Configura a segurança de cliente para nó.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-160">Configures client-to-node security.</span></span> <span data-ttu-id="c1b1f-161">Uma matriz de contas de usuário do cliente.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="c1b1f-162">Identidade</span><span class="sxs-lookup"><span data-stu-id="c1b1f-162">Identity</span></span> |<span data-ttu-id="c1b1f-163">Adicione o usuário de domínio, domínio\nomedeusuário, à identidade do cliente.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-163">Add the domain user, domain\username, for the client identity.</span></span> |  
| <span data-ttu-id="c1b1f-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="c1b1f-164">IsAdmin</span></span> |<span data-ttu-id="c1b1f-165">Defina como true para especificar que o usuário de domínio tem acesso de cliente de administrador ou false para acesso de cliente de usuário.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-165">Set to true to specify that the domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="c1b1f-166">[A segurança entre nós](service-fabric-cluster-security.md#node-to-node-security) é definida usando a configuração **ClusterIdentity**, se você quiser usar um grupo de máquinas em um Domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-166">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want to use a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="c1b1f-167">Para saber mais, confira [Criar um grupo de máquinas no Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="c1b1f-168">A [segurança de cliente para nó](service-fabric-cluster-security.md#client-to-node-security) é configurada usando **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="c1b1f-169">Para estabelecer a confiança entre um cliente e o cluster, você deverá configurar o cluster para saber em quais identidades de cliente ele poderá confiar.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-169">To establish trust between a client and the cluster, you must configure the cluster to know the client identities that the cluster can trust.</span></span> <span data-ttu-id="c1b1f-170">Você pode estabelecer confiança de duas maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="c1b1f-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="c1b1f-171">Especificar os usuários do grupo de domínio que podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-171">Specify the domain group users that can connect.</span></span>
- <span data-ttu-id="c1b1f-172">Especificar os usuários do nó de domínio que podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-172">Specify the domain node users that can connect.</span></span>

<span data-ttu-id="c1b1f-173">O Service Fabric oferece suporte a dois tipos de controle de acesso diferentes para clientes conectados a um cluster do Service Fabric: administrador e usuário.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-173">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="c1b1f-174">O controle de acesso permite que o administrador de cluster limite o acesso a determinados tipos de operação de cluster para diferentes grupos de usuários, tornando o cluster mais seguro.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-174">Access control enables the cluster administrator to limit access to certain types of cluster operations for different groups of users, which makes the cluster more secure.</span></span>  <span data-ttu-id="c1b1f-175">Os administradores têm acesso completo aos recursos de gerenciamento (incluindo recursos de leitura/gravação).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-175">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="c1b1f-176">Os usuários, por padrão, têm apenas acesso de leitura aos recursos de gerenciamento (por exemplo, recursos de consulta) e a capacidade de resolver serviços e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-176">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>  

<span data-ttu-id="c1b1f-177">A seção de **segurança** do exemplo a seguir configura a segurança do Windows e especifica que os computadores em *ServiceFabric/clusterA.contoso.com* fazem parte do cluster e especifica que *CONTOSO\usera* tem acesso de cliente do administrador:</span><span class="sxs-lookup"><span data-stu-id="c1b1f-177">The following example **security** section configures Windows security, specifies that the machines in *ServiceFabric/clusterA.contoso.com* are part of the cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> <span data-ttu-id="c1b1f-178">O Service Fabric não devem ser implantado em um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="c1b1f-179">Certifique-se de que ClusterConfig.json não inclui o endereço IP do controlador de domínio ao usar um grupo de computadores ou gMSA (grupo da conta de serviço gerenciado).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-179">Make sure that ClusterConfig.json does not include the IP address of the domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c1b1f-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1b1f-180">Next steps</span></span>
<span data-ttu-id="c1b1f-181">Depois de configurar a segurança do Windows no arquivo *ClusterConfig.JSON* , retome o processo de criação de cluster em [Criar um cluster autônomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-181">After configuring Windows security in the *ClusterConfig.JSON* file, resume the cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="c1b1f-182">Para saber mais sobre a segurança de nó para nó, a segurança de cliente para nó e o controle de acesso baseado em função, consulte [Cenários de segurança de cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="c1b1f-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="c1b1f-183">Consulte [Conectar a um cluster seguro](service-fabric-connect-to-secure-cluster.md) para obter exemplos de conexão usando o PowerShell ou o FabricClient.</span><span class="sxs-lookup"><span data-stu-id="c1b1f-183">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
