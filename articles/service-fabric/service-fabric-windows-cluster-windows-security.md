---
title: "aaaSecure um cluster em execução no Windows usando a segurança do Windows | Microsoft Docs"
description: "Saiba como tooconfigure segurança de nó para nó e o nó do cliente em um autônomo cluster em execução no Windows usando a segurança do Windows."
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
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="784c4-103">Proteger um cluster autônomo no Windows usando a Segurança do Windows</span><span class="sxs-lookup"><span data-stu-id="784c4-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="784c4-104">tooprevent de cluster de malha do serviço de tooa de acesso não autorizado, você deve proteger o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="784c4-104">tooprevent unauthorized access tooa Service Fabric cluster, you must secure hello cluster.</span></span> <span data-ttu-id="784c4-105">Segurança é especialmente importante quando o cluster Olá executa cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="784c4-105">Security is especially important when hello cluster runs production workloads.</span></span> <span data-ttu-id="784c4-106">Este artigo descreve como segurança tooconfigure de nó do cliente e de nó para nó usando a segurança do Windows no hello *Clusterconfig* arquivo.</span><span class="sxs-lookup"><span data-stu-id="784c4-106">This article describes how tooconfigure node-to-node and client-to-node security by using Windows security in hello *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="784c4-107">processo de saudação corresponde toohello configurar segurança de [criar um cluster autônomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="784c4-107">hello process corresponds toohello configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="784c4-108">Para saber mais sobre como o Service Fabric usa a Segurança do Windows, veja [Cenários de segurança de cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="784c4-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="784c4-109">Você deve considerar seleção Olá de nó para nó segurança com cuidado porque não há nenhuma atualização de cluster de um tooanother de opção de segurança.</span><span class="sxs-lookup"><span data-stu-id="784c4-109">You should consider hello selection of node-to-node security carefully because there is no cluster upgrade from one security choice tooanother.</span></span> <span data-ttu-id="784c4-110">seleção de segurança do toochange hello, você tem toorebuild Olá completo do cluster.</span><span class="sxs-lookup"><span data-stu-id="784c4-110">toochange hello security selection, you have toorebuild hello full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="784c4-111">Configurar a segurança do Windows usando gMSA</span><span class="sxs-lookup"><span data-stu-id="784c4-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="784c4-112">exemplo Hello *ClusterConfig.gMSA.Windows.MultiMachine.JSON* baixar um arquivo de configuração com hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) autônomo pacote de cluster contém um modelo de configuração de segurança do Windows usando [conta de serviço gerenciado de grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="784c4-112">hello sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

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
  
| <span data-ttu-id="784c4-113">**Parâmetro de configuração**</span><span class="sxs-lookup"><span data-stu-id="784c4-113">**Configuration Setting**</span></span> | <span data-ttu-id="784c4-114">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="784c4-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="784c4-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="784c4-115">WindowsIdentities</span></span> |<span data-ttu-id="784c4-116">Contém as identidades de cliente e o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="784c4-116">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="784c4-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="784c4-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="784c4-118">Configura a segurança de nó para nó.</span><span class="sxs-lookup"><span data-stu-id="784c4-118">Configures node-to-node security.</span></span> <span data-ttu-id="784c4-119">Uma conta de serviço gerenciado de grupo.</span><span class="sxs-lookup"><span data-stu-id="784c4-119">A group managed service account.</span></span> |  
| <span data-ttu-id="784c4-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="784c4-120">ClusterSPN</span></span> |<span data-ttu-id="784c4-121">SPN de domínio totalmente qualificado para a conta gMSA</span><span class="sxs-lookup"><span data-stu-id="784c4-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="784c4-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="784c4-122">ClientIdentities</span></span> |<span data-ttu-id="784c4-123">Configura a segurança de cliente para nó.</span><span class="sxs-lookup"><span data-stu-id="784c4-123">Configures client-to-node security.</span></span> <span data-ttu-id="784c4-124">Uma matriz de contas de usuário do cliente.</span><span class="sxs-lookup"><span data-stu-id="784c4-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="784c4-125">Identidade</span><span class="sxs-lookup"><span data-stu-id="784c4-125">Identity</span></span> |<span data-ttu-id="784c4-126">identidade do cliente Hello, um usuário de domínio.</span><span class="sxs-lookup"><span data-stu-id="784c4-126">hello client identity, a domain user.</span></span> |  
| <span data-ttu-id="784c4-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="784c4-127">IsAdmin</span></span> |<span data-ttu-id="784c4-128">O valor True Especifica que esse usuário de domínio Olá tenha acesso de cliente de administrador, false para acesso de cliente do usuário.</span><span class="sxs-lookup"><span data-stu-id="784c4-128">True specifies that hello domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="784c4-129">[Segurança do nó toonode](service-fabric-cluster-security.md#node-to-node-security) é configurada definindo **ClustergMSAIdentity** quando do service fabric precisa toorun em gMSA.</span><span class="sxs-lookup"><span data-stu-id="784c4-129">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs toorun under gMSA.</span></span> <span data-ttu-id="784c4-130">Em relações de confiança de toobuild ordem entre os nós, eles devem ser informados uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="784c4-130">In order toobuild trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="784c4-131">Isso pode ser feito de duas maneiras diferentes: especifique Olá grupo de conta de serviço gerenciado que inclui todos os nós no cluster de saudação ou grupo de computadores do domínio Olá que inclui todos os nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="784c4-131">This can be accomplished in two different ways: Specify hello Group Managed Service Account that includes all nodes in hello cluster or Specify hello domain machine group that includes all nodes in hello cluster.</span></span> <span data-ttu-id="784c4-132">É altamente recomendável usar Olá [conta de serviço gerenciado de grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) abordagem, particularmente para clusters maiores (mais de 10 nós) ou para clusters que são provavelmente toogrow ou reduzidas.</span><span class="sxs-lookup"><span data-stu-id="784c4-132">We strongly recommend using hello [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely toogrow or shrink.</span></span>  
<span data-ttu-id="784c4-133">Essa abordagem não exige a saudação de criação de um grupo de domínio para o qual os administradores de cluster foram concedidos tooadd de direitos de acesso e remover membros.</span><span class="sxs-lookup"><span data-stu-id="784c4-133">This approach does not require hello creation of a domain group for which cluster administrators have been granted access rights tooadd and remove members.</span></span> <span data-ttu-id="784c4-134">Essas contas também são úteis para gerenciamento automático de senha.</span><span class="sxs-lookup"><span data-stu-id="784c4-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="784c4-135">Para obter mais informações, confira [Introdução a contas de serviços gerenciados de grupo](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="784c4-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="784c4-136">[Segurança do cliente toonode](service-fabric-cluster-security.md#client-to-node-security) é configurado usando **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="784c4-136">[Client toonode security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="784c4-137">Em ordem tooestablish relação de confiança entre um cluster de cliente e hello, configure Olá cluster tooknow quais identidades de cliente que pode confiar.</span><span class="sxs-lookup"><span data-stu-id="784c4-137">In order tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow which client identities that it can trust.</span></span> <span data-ttu-id="784c4-138">Isso pode ser feito de duas maneiras diferentes: especificar usuários Olá de grupo de domínio que podem se conectar ou especifique Olá usuários de nó do domínio que podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="784c4-138">This can be done in two different ways: Specify hello domain group users that can connect or specify hello domain node users that can connect.</span></span> <span data-ttu-id="784c4-139">Malha do serviço oferece suporte a dois tipos de controle de acesso diferentes para os clientes conectados tooa malha do serviço de cluster: administrador e usuário.</span><span class="sxs-lookup"><span data-stu-id="784c4-139">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="784c4-140">Controle de acesso permite Olá Olá tipos cluster administrador toolimit acesso toocertain das operações de cluster para diferentes grupos de usuários, tornando o cluster hello mais segura.</span><span class="sxs-lookup"><span data-stu-id="784c4-140">Access control provides hello ability for hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, making hello cluster more secure.</span></span>  <span data-ttu-id="784c4-141">Os administradores têm recursos de toomanagement de acesso completo (incluindo recursos de leitura/gravação).</span><span class="sxs-lookup"><span data-stu-id="784c4-141">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="784c4-142">Os usuários, por padrão, têm apenas acesso de leitura toomanagement recursos (por exemplo, recursos de consulta), Olá capacidade tooresolve e aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="784c4-142">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span> <span data-ttu-id="784c4-143">Para saber mais sobre controles de acesso, veja [Controle de acesso baseado em função para clientes do Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="784c4-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="784c4-144">Olá seguindo exemplo **segurança** seção configura a segurança do Windows usando gMSA e especifica que Olá máquinas *ServiceFabric.clusterA.contoso.com* gMSA fazem parte do cluster hello e que *CONTOSO\usera* tem acesso de cliente do administrador:</span><span class="sxs-lookup"><span data-stu-id="784c4-144">hello following example **security** section configures Windows security using gMSA and specifies that hello machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of hello cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
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
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="784c4-145">Configurar a segurança do Windows usando um grupo de máquinas</span><span class="sxs-lookup"><span data-stu-id="784c4-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="784c4-146">exemplo Hello *ClusterConfig.Windows.MultiMachine.JSON* baixar um arquivo de configuração com hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) autônomo pacote de cluster contém um modelo de configuração de segurança do Windows.</span><span class="sxs-lookup"><span data-stu-id="784c4-146">hello sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="784c4-147">Segurança do Windows é configurada em Olá **propriedades** seção:</span><span class="sxs-lookup"><span data-stu-id="784c4-147">Windows security is configured in hello **Properties** section:</span></span> 

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

| <span data-ttu-id="784c4-148">**Parâmetro de configuração**</span><span class="sxs-lookup"><span data-stu-id="784c4-148">**Configuration setting**</span></span> | <span data-ttu-id="784c4-149">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="784c4-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="784c4-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="784c4-150">ClusterCredentialType</span></span> |<span data-ttu-id="784c4-151">**ClusterCredentialType** está definido muito*Windows* se ClusterIdentity Especifica um nome de grupo de computador do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="784c4-151">**ClusterCredentialType** is set too*Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="784c4-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="784c4-152">ServerCredentialType</span></span> |<span data-ttu-id="784c4-153">Definir muito*Windows* tooenable a segurança do Windows para clientes.</span><span class="sxs-lookup"><span data-stu-id="784c4-153">Set too*Windows* tooenable Windows security for clients.</span></span><br /><br /><span data-ttu-id="784c4-154">Isso indica que clientes Olá Olá cluster e Olá em si são executados em um domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="784c4-154">This indicates that hello clients of hello cluster and hello cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="784c4-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="784c4-155">WindowsIdentities</span></span> |<span data-ttu-id="784c4-156">Contém as identidades de cliente e o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="784c4-156">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="784c4-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="784c4-157">ClusterIdentity</span></span> |<span data-ttu-id="784c4-158">Use um nome de grupo do computador, domain\machinegroup, segurança de nó para nó tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="784c4-158">Use a machine group name, domain\machinegroup, tooconfigure node-to-node security.</span></span> |  
| <span data-ttu-id="784c4-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="784c4-159">ClientIdentities</span></span> |<span data-ttu-id="784c4-160">Configura a segurança de cliente para nó.</span><span class="sxs-lookup"><span data-stu-id="784c4-160">Configures client-to-node security.</span></span> <span data-ttu-id="784c4-161">Uma matriz de contas de usuário do cliente.</span><span class="sxs-lookup"><span data-stu-id="784c4-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="784c4-162">Identidade</span><span class="sxs-lookup"><span data-stu-id="784c4-162">Identity</span></span> |<span data-ttu-id="784c4-163">Adicione o usuário de domínio do hello, domínio \ nomedeusuário para identidade de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="784c4-163">Add hello domain user, domain\username, for hello client identity.</span></span> |  
| <span data-ttu-id="784c4-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="784c4-164">IsAdmin</span></span> |<span data-ttu-id="784c4-165">Conjunto tootrue toospecify que Olá usuário de domínio tem acesso de administrador do cliente ou falso para acesso de cliente do usuário.</span><span class="sxs-lookup"><span data-stu-id="784c4-165">Set tootrue toospecify that hello domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="784c4-166">[Segurança do nó toonode](service-fabric-cluster-security.md#node-to-node-security) é configurada por meio de configuração **ClusterIdentity** se você quiser toouse um grupo de computadores em um domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="784c4-166">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want toouse a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="784c4-167">Para saber mais, confira [Criar um grupo de máquinas no Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span><span class="sxs-lookup"><span data-stu-id="784c4-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="784c4-168">A [segurança de cliente para nó](service-fabric-cluster-security.md#client-to-node-security) é configurada usando **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="784c4-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="784c4-169">tooestablish de confiança entre um cliente e hello cluster, você deve configurar Olá cluster tooknow Olá cliente identidades Olá cluster podem confiar.</span><span class="sxs-lookup"><span data-stu-id="784c4-169">tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow hello client identities that hello cluster can trust.</span></span> <span data-ttu-id="784c4-170">Você pode estabelecer confiança de duas maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="784c4-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="784c4-171">Especifique os usuários do grupo de domínio de saudação podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="784c4-171">Specify hello domain group users that can connect.</span></span>
- <span data-ttu-id="784c4-172">Especifica usuários de nó do domínio Olá podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="784c4-172">Specify hello domain node users that can connect.</span></span>

<span data-ttu-id="784c4-173">Malha do serviço oferece suporte a dois tipos de controle de acesso diferentes para os clientes conectados tooa malha do serviço de cluster: administrador e usuário.</span><span class="sxs-lookup"><span data-stu-id="784c4-173">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="784c4-174">Controle de acesso permite Olá cluster administrador toolimit acesso toocertain tipos de operações de cluster para diferentes grupos de usuários, que torna o cluster hello mais segura.</span><span class="sxs-lookup"><span data-stu-id="784c4-174">Access control enables hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, which makes hello cluster more secure.</span></span>  <span data-ttu-id="784c4-175">Os administradores têm recursos de toomanagement de acesso completo (incluindo recursos de leitura/gravação).</span><span class="sxs-lookup"><span data-stu-id="784c4-175">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="784c4-176">Os usuários, por padrão, têm apenas acesso de leitura toomanagement recursos (por exemplo, recursos de consulta), Olá capacidade tooresolve e aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="784c4-176">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>  

<span data-ttu-id="784c4-177">Olá seguindo exemplo **segurança** seção configura a segurança do Windows, especifica que Olá máquinas *ServiceFabric/clusterA.contoso.com* fazem parte do cluster hello e especifica que  *CONTOSO\usera* tem acesso de cliente do administrador:</span><span class="sxs-lookup"><span data-stu-id="784c4-177">hello following example **security** section configures Windows security, specifies that hello machines in *ServiceFabric/clusterA.contoso.com* are part of hello cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

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
> <span data-ttu-id="784c4-178">O Service Fabric não devem ser implantado em um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="784c4-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="784c4-179">Certifique-se de que Clusterconfig não incluem o endereço IP de Olá Olá do controlador de domínio ao usar um grupo de computador ou grupo a conta de serviço gerenciada (gMSA).</span><span class="sxs-lookup"><span data-stu-id="784c4-179">Make sure that ClusterConfig.json does not include hello IP address of hello domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="784c4-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="784c4-180">Next steps</span></span>
<span data-ttu-id="784c4-181">Depois de configurar a segurança do Windows em Olá *Clusterconfig* de arquivos, retomar o processo de criação de cluster Olá em [criar um cluster autônomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="784c4-181">After configuring Windows security in hello *ClusterConfig.JSON* file, resume hello cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="784c4-182">Para saber mais sobre a segurança de nó para nó, a segurança de cliente para nó e o controle de acesso baseado em função, consulte [Cenários de segurança de cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="784c4-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="784c4-183">Consulte [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para obter exemplos de conexão usando o PowerShell ou FabricClient.</span><span class="sxs-lookup"><span data-stu-id="784c4-183">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
