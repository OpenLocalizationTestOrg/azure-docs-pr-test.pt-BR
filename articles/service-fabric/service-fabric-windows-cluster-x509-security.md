---
title: Proteger um cluster do Azure Service Fabric no Windows usando certificados | Microsoft Docs
description: "Este artigo descreve como proteger a comunicação no cluster autônomo ou privado, bem como entre clientes e o cluster."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: 71ece1e43cc3c4ac3350cd59633065de06672420
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="0fa88-103">Proteger um cluster autônomo no Windows usando os certificados X.509</span><span class="sxs-lookup"><span data-stu-id="0fa88-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="0fa88-104">Este artigo descreve como proteger a comunicação entre os diversos nós do seu cluster do Windows autônomo, bem como autenticar os clientes que estejam se conectando a esse cluster, usando os certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="0fa88-104">This article describes how to secure the communication between the various nodes of your standalone Windows cluster, as well as how to authenticate clients connecting to this cluster, using X.509 certificates.</span></span> <span data-ttu-id="0fa88-105">Isso garante que somente usuários autorizados possam acessar o cluster e os aplicativos implantados e executar tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0fa88-105">This ensures that only authorized users can access the cluster, the deployed applications and perform management tasks.</span></span>  <span data-ttu-id="0fa88-106">A segurança do certificado deve ser habilitada no cluster quando o cluster é criado.</span><span class="sxs-lookup"><span data-stu-id="0fa88-106">Certificate security should be enabled on the cluster when the cluster is created.</span></span>  

<span data-ttu-id="0fa88-107">Para obter mais informações sobre segurança de cluster, como nós de segurança, segurança de nó de cliente e controle de acesso baseado em função, confira [Cenários de segurança de cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="0fa88-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="0fa88-108">De quais certificados você precisará?</span><span class="sxs-lookup"><span data-stu-id="0fa88-108">Which certificates will you need?</span></span>
<span data-ttu-id="0fa88-109">Para começar, [baixe o pacote de clusters autônomos](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) para um dos nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-109">To start with, [download the standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) to one of the nodes in your cluster.</span></span> <span data-ttu-id="0fa88-110">No pacote baixado, você encontrará um arquivo **ClusterConfig.X509.MultiMachine.json** .</span><span class="sxs-lookup"><span data-stu-id="0fa88-110">In the downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="0fa88-111">Abra o arquivo e revise a seção **Segurança** na seção **Propriedades**:</span><span class="sxs-lookup"><span data-stu-id="0fa88-111">Open the file and review the section for **security** under the **properties** section:</span></span>

```JSON
"security": {
    "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

<span data-ttu-id="0fa88-112">Esta seção descreve os certificados necessários para proteger o cluster do Windows autônomo.</span><span class="sxs-lookup"><span data-stu-id="0fa88-112">This section describes the certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="0fa88-113">Se estiver especificando um certificado de cluster, defina o valor de **ClusterCredentialType** como _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="0fa88-113">If you are specifying a cluster certificate, set the value of **ClusterCredentialType** to _**X509**_.</span></span> <span data-ttu-id="0fa88-114">Se estiver especificando um certificado do servidor para conexões externas, defina **ServerCredentialType** como _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="0fa88-114">If you are specifying server certificate for outside connections, set the **ServerCredentialType** to _**X509**_.</span></span> <span data-ttu-id="0fa88-115">Embora não seja obrigatório, recomendamos ter esses dois certificados para um cluster protegido adequadamente.</span><span class="sxs-lookup"><span data-stu-id="0fa88-115">Although not mandatory, we recommend to have both these certificates for a properly secured cluster.</span></span> <span data-ttu-id="0fa88-116">Se você definir esses valores como *X509*, também deverá especificar os certificados correspondentes; caso contrário, o Service Fabric gerará uma exceção.</span><span class="sxs-lookup"><span data-stu-id="0fa88-116">If you set these values to *X509* then you must also specify the corresponding certificates or Service Fabric will throw an exception.</span></span> <span data-ttu-id="0fa88-117">Em alguns cenários, talvez você apenas deseje especificar _ClientCertificateThumbprints_ ou _ReverseProxyCertificate_.</span><span class="sxs-lookup"><span data-stu-id="0fa88-117">In some scenarios, you may only want to specify the _ClientCertificateThumbprints_ or _ReverseProxyCertificate_.</span></span> <span data-ttu-id="0fa88-118">Nesses cenários, não é necessário definir _ClusterCredentialType_ nem _ServerCredentialType_ como _X509_.</span><span class="sxs-lookup"><span data-stu-id="0fa88-118">In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ to _X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="0fa88-119">Uma [impressão digital](https://en.wikipedia.org/wiki/Public_key_fingerprint) é a principal identidade de um certificado.</span><span class="sxs-lookup"><span data-stu-id="0fa88-119">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is the primary identity of a certificate.</span></span> <span data-ttu-id="0fa88-120">Leia [How to retrieve thumbprint of a certificate (Como recuperar a impressão digital de um certificado)](https://msdn.microsoft.com/library/ms734695.aspx) para descobrir a impressão digital do certificados que você cria.</span><span class="sxs-lookup"><span data-stu-id="0fa88-120">Read [How to retrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) to find out the thumbprint of the certificates that you create.</span></span>
> 
> 

<span data-ttu-id="0fa88-121">A tabela a seguir lista os certificados que serão necessárias na configuração do seu cluster:</span><span class="sxs-lookup"><span data-stu-id="0fa88-121">The following table lists the certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="0fa88-122">**Configuração de CertificateInformation**</span><span class="sxs-lookup"><span data-stu-id="0fa88-122">**CertificateInformation Setting**</span></span> | <span data-ttu-id="0fa88-123">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="0fa88-123">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="0fa88-124">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="0fa88-124">ClusterCertificate</span></span> |<span data-ttu-id="0fa88-125">Recomendado para o ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0fa88-125">Recommended for test environment.</span></span> <span data-ttu-id="0fa88-126">Esse certificado é necessário para proteger a comunicação entre os nós em um cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-126">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="0fa88-127">Você pode usar dois certificados diferentes, um principal e um secundário para atualização.</span><span class="sxs-lookup"><span data-stu-id="0fa88-127">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="0fa88-128">Defina a impressão digital do certificado principal na seção **Impressão Digital** e a do secundário nas variáveis **ThumbprintSecondary**.</span><span class="sxs-lookup"><span data-stu-id="0fa88-128">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="0fa88-129">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="0fa88-129">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="0fa88-130">Recomendado para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0fa88-130">Recommended for production environment.</span></span> <span data-ttu-id="0fa88-131">Esse certificado é necessário para proteger a comunicação entre os nós em um cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-131">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="0fa88-132">Você pode usar um ou dois nomes comuns de certificado de cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-132">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="0fa88-133">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="0fa88-133">ServerCertificate</span></span> |<span data-ttu-id="0fa88-134">Recomendado para o ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0fa88-134">Recommended for test environment.</span></span> <span data-ttu-id="0fa88-135">Esse certificado é apresentado ao cliente quando ele tenta se conectar a esse cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-135">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="0fa88-136">Para sua conveniência, você pode optar por usar o mesmo certificado para *ClusterCertificate* e *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="0fa88-136">For convenience, you can choose to use the same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="0fa88-137">Você pode usar dois certificados de servidor diferentes, um principal e um secundário, para atualização.</span><span class="sxs-lookup"><span data-stu-id="0fa88-137">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="0fa88-138">Defina a impressão digital do certificado principal na seção **Impressão Digital** e a do secundário nas variáveis **ThumbprintSecondary**.</span><span class="sxs-lookup"><span data-stu-id="0fa88-138">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="0fa88-139">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="0fa88-139">ServerCertificateCommonNames</span></span> |<span data-ttu-id="0fa88-140">Recomendado para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0fa88-140">Recommended for production environment.</span></span> <span data-ttu-id="0fa88-141">Esse certificado é apresentado ao cliente quando ele tenta se conectar a esse cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-141">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="0fa88-142">Para sua conveniência, você pode optar por usar o mesmo certificado para *ClusterCertificateCommonNames* e *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="0fa88-142">For convenience, you can choose to use the same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="0fa88-143">Você pode usar um ou dois nomes comuns de certificado.</span><span class="sxs-lookup"><span data-stu-id="0fa88-143">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="0fa88-144">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="0fa88-144">ClientCertificateThumbprints</span></span> |<span data-ttu-id="0fa88-145">Esse é um conjunto de certificados que você deseja instalar nos clientes autenticados.</span><span class="sxs-lookup"><span data-stu-id="0fa88-145">This is a set of certificates that you want to install on the authenticated clients.</span></span> <span data-ttu-id="0fa88-146">Você pode ter alguns certificados de cliente diferentes instalados nos computadores para os quais você deseja permitir o acesso ao cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-146">You can have a number of different client certificates installed on the machines that you want to allow access to the cluster.</span></span> <span data-ttu-id="0fa88-147">Defina a impressão digital de cada certificado na variável **CertificateThumbprint** .</span><span class="sxs-lookup"><span data-stu-id="0fa88-147">Set the thumbprint of each certificate in the **CertificateThumbprint** variable.</span></span> <span data-ttu-id="0fa88-148">Se você definir **IsAdmin** para *true*, o cliente com o certificado instalado poderá realizar atividades de gerenciamento de administrador no cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-148">If you set the **IsAdmin** to *true*, then the client with this certificate installed on it can do administrator management activities on the cluster.</span></span> <span data-ttu-id="0fa88-149">Se **IsAdmin** for *false*, o cliente com esse certificado só poderá executar as ações permitidas para direitos de acesso do usuário, normalmente, somente leitura.</span><span class="sxs-lookup"><span data-stu-id="0fa88-149">If the **IsAdmin** is *false*, the client with this certificate can only perform the actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="0fa88-150">Para obter mais informações sobre funções, leia [RBAC (controle de acesso baseado em função)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="0fa88-150">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="0fa88-151">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="0fa88-151">ClientCertificateCommonNames</span></span> |<span data-ttu-id="0fa88-152">Defina o nome comum do primeiro certificado do cliente para **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="0fa88-152">Set the common name of the first client certificate for the **CertificateCommonName**.</span></span> <span data-ttu-id="0fa88-153">A **CertificateIssuerThumbprint** é a impressão digital para o emissor deste certificado.</span><span class="sxs-lookup"><span data-stu-id="0fa88-153">The **CertificateIssuerThumbprint** is the thumbprint for the issuer of this certificate.</span></span> <span data-ttu-id="0fa88-154">Leia [Working with certificates (Trabalhando com certificados)](https://msdn.microsoft.com/library/ms731899.aspx) para saber mais sobre os nomes comuns e o emissor.</span><span class="sxs-lookup"><span data-stu-id="0fa88-154">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) to know more about common names and the issuer.</span></span> |
| <span data-ttu-id="0fa88-155">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="0fa88-155">ReverseProxyCertificate</span></span> |<span data-ttu-id="0fa88-156">Recomendado para o ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0fa88-156">Recommended for test environment.</span></span> <span data-ttu-id="0fa88-157">Esse é um certificado opcional que poderá ser especificado se você desejar proteger o [Proxy Reverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="0fa88-157">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="0fa88-158">Verifique se reverseProxyEndpointPort está definido em nodeTypes caso você esteja usando esse certificado.</span><span class="sxs-lookup"><span data-stu-id="0fa88-158">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="0fa88-159">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="0fa88-159">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="0fa88-160">Recomendado para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0fa88-160">Recommended for production environment.</span></span> <span data-ttu-id="0fa88-161">Esse é um certificado opcional que poderá ser especificado se você desejar proteger o [Proxy Reverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="0fa88-161">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="0fa88-162">Verifique se reverseProxyEndpointPort está definido em nodeTypes caso você esteja usando esse certificado.</span><span class="sxs-lookup"><span data-stu-id="0fa88-162">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="0fa88-163">Aqui está um exemplo de configuração de cluster em que os certificados de Cluster, Servidor e Cliente foram fornecidos.</span><span class="sxs-lookup"><span data-stu-id="0fa88-163">Here is example cluster configuration where the Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="0fa88-164">Observe que, para cluster / server / certificados reverseProxy, impressão digital e o nome comum não podem ser configurados juntos para o mesmo tipo de certificado.</span><span class="sxs-lookup"><span data-stu-id="0fa88-164">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed to be configured together for the same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace the localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a><span data-ttu-id="0fa88-165">Rolagem do certificado</span><span class="sxs-lookup"><span data-stu-id="0fa88-165">Certificate roll over</span></span>
<span data-ttu-id="0fa88-166">Ao usar o nome comum do certificado em vez de impressão digital, sobreposição de certificado não requer a atualização de configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-166">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="0fa88-167">Se envolver a sobreposição de certificado de rolagem do emissor,. Mantenha o antigo certificado de emissor no cert armazenar pelo menos 2 horas depois de instalar o novo certificado do emissor.</span><span class="sxs-lookup"><span data-stu-id="0fa88-167">If certificate roll over involves issuer roll over, please keep the old issuer cert in the cert store at least 2 hours after installing the new issuer cert.</span></span>

## <a name="acquire-the-x509-certificates"></a><span data-ttu-id="0fa88-168">Adquirir os certificados X.509</span><span class="sxs-lookup"><span data-stu-id="0fa88-168">Acquire the X.509 certificates</span></span>
<span data-ttu-id="0fa88-169">Para proteger a comunicação no cluster, primeiro você precisará obter certificados X.509 para os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-169">To secure communication within the cluster, you will first need to obtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="0fa88-170">Além disso, para limitar a conexão a este cluster a computadores e a usuários autorizados, você precisará obter e instalar certificados para os computadores cliente.</span><span class="sxs-lookup"><span data-stu-id="0fa88-170">Additionally, to limit connection to this cluster to authorized machines/users, you will need to obtain and install certificates for the client machines.</span></span>

<span data-ttu-id="0fa88-171">Para clusters que estão executando cargas de trabalho de produção, você deve usar um certificado X.509 assinado pela [AC (Autoridade de Certificação)](https://en.wikipedia.org/wiki/Certificate_authority) para proteger o cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-171">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate to secure the cluster.</span></span> <span data-ttu-id="0fa88-172">Para obter detalhes sobre como obter esses certificados, vá para [Como obter um certificado](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fa88-172">For details on obtaining these certificates, go to [How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="0fa88-173">Para clusters usados para fins de teste, você pode optar por usar um certificado assinado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0fa88-173">For clusters that you use for test purposes, you can choose to use a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="0fa88-174">Opcional: criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="0fa88-174">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="0fa88-175">Uma maneira de criar um certificado autoassinado que pode ser protegido corretamente é usar o script *CertSetup.ps1* na pasta do SDK do Service Fabric no diretório *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="0fa88-175">One way to create a self-signed cert that can be secured correctly is to use the *CertSetup.ps1* script in the Service Fabric SDK folder in the directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="0fa88-176">Edite esse arquivo para alterar o nome padrão do certificado (procure o valor *CN=ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="0fa88-176">Edit this file to change the default name of the certificate (look for the value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="0fa88-177">Execute esse script como `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="0fa88-177">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="0fa88-178">Agora, exporte o certificado para um arquivo PFX com uma senha protegida.</span><span class="sxs-lookup"><span data-stu-id="0fa88-178">Now export the certificate to a PFX file with a protected password.</span></span> <span data-ttu-id="0fa88-179">Primeiro, obtenha a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="0fa88-179">First get the thumbprint of the certificate.</span></span> <span data-ttu-id="0fa88-180">No menu *Iniciar*, execute *Gerenciar certificados de computador*.</span><span class="sxs-lookup"><span data-stu-id="0fa88-180">From the *Start* menu, run the *Manage computer certificates*.</span></span> <span data-ttu-id="0fa88-181">Navegue até a pasta **Computador Local\Pessoal** e localize o certificado que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="0fa88-181">Navigate to the **Local Computer\Personal** folder and find the certificate you just created.</span></span> <span data-ttu-id="0fa88-182">Clique duas vezes no certificado para abri-lo, selecione a guia *Detalhes* e role para baixo até o campo *Impressão digital*.</span><span class="sxs-lookup"><span data-stu-id="0fa88-182">Double-click the certificate to open it, select the *Details* tab and scroll down to the *Thumbprint* field.</span></span> <span data-ttu-id="0fa88-183">Copie o valor de impressão digital para o comando do PowerShell abaixo, depois de remover os espaços.</span><span class="sxs-lookup"><span data-stu-id="0fa88-183">Copy the thumbprint value into the PowerShell command below, after removing the spaces.</span></span>  <span data-ttu-id="0fa88-184">Altere o valor `String` para uma senha segura adequada para protegê-lo e execute o seguinte no PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0fa88-184">Change the `String` value to a suitable secure password to protect it and run the following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="0fa88-185">Para ver os detalhes de um certificado instalado no computador, você pode executar o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0fa88-185">To see the details of a certificate installed on the machine you can run the following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="0fa88-186">Se tiver uma assinatura do Azure, você também pode seguir as instruções na seção [Adicionar certificados ao Cofre de Chaves](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="0fa88-186">Alternatively, if you have an Azure subscription, follow the section [Add certificates to Key Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-the-certificates"></a><span data-ttu-id="0fa88-187">Instalar os certificados</span><span class="sxs-lookup"><span data-stu-id="0fa88-187">Install the certificates</span></span>
<span data-ttu-id="0fa88-188">Quando tiver o(s) certificado(s), você poderá instalá-lo(s) nos nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-188">Once you have certificate(s), you can install them on the cluster nodes.</span></span> <span data-ttu-id="0fa88-189">Os nós precisam ter o mais recente Windows PowerShell 3. x instalado neles.</span><span class="sxs-lookup"><span data-stu-id="0fa88-189">Your nodes need to have the latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="0fa88-190">Você precisará repetir essas etapas em cada nó, para os certificados do Cluster e do Servidor e todos os certificados secundários.</span><span class="sxs-lookup"><span data-stu-id="0fa88-190">You will need to repeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="0fa88-191">Copie o(s) arquivo(s) .pfx para o nó.</span><span class="sxs-lookup"><span data-stu-id="0fa88-191">Copy the .pfx file(s) to the node.</span></span>
2. <span data-ttu-id="0fa88-192">Abra uma janela do PowerShell como administrador e insira os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fa88-192">Open a PowerShell window as an administrator and enter the following commands.</span></span> <span data-ttu-id="0fa88-193">Substitua *$pswd* pela senha que você usou para criar esse certificado.</span><span class="sxs-lookup"><span data-stu-id="0fa88-193">Replace the *$pswd* with the password that you used to create this certificate.</span></span> <span data-ttu-id="0fa88-194">Substitua *$PfxFilePath* pelo caminho completo do .pfx copiado para esse nó.</span><span class="sxs-lookup"><span data-stu-id="0fa88-194">Replace the *$PfxFilePath* with the full path of the .pfx copied to this node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="0fa88-195">Agora defina o controle de acesso nesse certificado para que o processo do Service Fabric, executado na conta de Serviço de Rede, possa usá-lo executando o script a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fa88-195">Now set the access control on this certificate so that the Service Fabric process, which runs under the Network Service account, can use it by running the following script.</span></span> <span data-ttu-id="0fa88-196">Forneça a impressão digital do certificado e "NETWORK SERVICE" para a conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="0fa88-196">Provide the thumbprint of the certificate and "NETWORK SERVICE" for the service account.</span></span> <span data-ttu-id="0fa88-197">Verifique se as ACLs no certificado estão corretas abrindo o certificado em *Iniciar* > *Gerenciar certificados de computador* e observando *Todas as Tarefas* > *Gerenciar Chaves Privadas*.</span><span class="sxs-lookup"><span data-stu-id="0fa88-197">You can check that the ACLs on the certificate are correct by opening the certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify the user, the permissions and the permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of the machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get the current acl of the private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add the new ace to the acl of the private key
    $acl.SetAccessRule($accessRule)
   
    # Write back the new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe the access rights currently assigned to this certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="0fa88-198">Repita as etapas acima para cada certificado de servidor.</span><span class="sxs-lookup"><span data-stu-id="0fa88-198">Repeat the steps above for each server certificate.</span></span> <span data-ttu-id="0fa88-199">Você também pode usar estas etapas para instalar os certificados de cliente nos computadores que deseja permitir que acessem o cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-199">You can also use these steps to install the client certificates on the machines that you want to allow access to the cluster.</span></span>

## <a name="create-the-secure-cluster"></a><span data-ttu-id="0fa88-200">Criar o cluster seguro</span><span class="sxs-lookup"><span data-stu-id="0fa88-200">Create the secure cluster</span></span>
<span data-ttu-id="0fa88-201">Depois de configurar a seção **security** do arquivo **ClusterConfig.X509.MultiMachine.json**, vá para a seção [Criar seu cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) para configurar os nós e criar o cluster autônomo.</span><span class="sxs-lookup"><span data-stu-id="0fa88-201">After configuring the **security** section of the **ClusterConfig.X509.MultiMachine.json** file, you can proceed to [Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section to configure the nodes and create the standalone cluster.</span></span> <span data-ttu-id="0fa88-202">Lembre-se de usar o arquivo **ClusterConfig.X509.MultiMachine.json** ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-202">Remember to use the **ClusterConfig.X509.MultiMachine.json** file while creating the cluster.</span></span> <span data-ttu-id="0fa88-203">Por exemplo, o comando pode ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="0fa88-203">For example, your command might look like the following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="0fa88-204">Depois que o cluster do Windows autônomo seguro estiver em execução com sucesso e você tiver configurado os clientes autenticados para conectarem-se a ele, siga a seção [Conectar a um cluster seguro usando o PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) para conectar-se a ele.</span><span class="sxs-lookup"><span data-stu-id="0fa88-204">Once you have the secure standalone Windows cluster successfully running, and have setup the authenticated clients to connect to it, follow the section [Connect to a secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) to connect to it.</span></span> <span data-ttu-id="0fa88-205">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0fa88-205">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="0fa88-206">Em seguida, é possível executar outros comandos do PowerShell para trabalhar com esse cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa88-206">You can then run other PowerShell commands to work with this cluster.</span></span> <span data-ttu-id="0fa88-207">Por exemplo, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) para mostrar uma lista de nós nesse cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="0fa88-207">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) to show a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="0fa88-208">Para remover o cluster, conecte-se ao nó no cluster em que você baixou o pacote do Service Fabric, abra uma linha de comando e navegue até a pasta do pacote.</span><span class="sxs-lookup"><span data-stu-id="0fa88-208">To remove the cluster, connect to the node on the cluster where you downloaded the Service Fabric package, open a command line and navigate to the package folder.</span></span> <span data-ttu-id="0fa88-209">Agora execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0fa88-209">Now run the following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="0fa88-210">Configuração incorreta de certificado pode impedir que o cluster apareça durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="0fa88-210">Incorrect certificate configuration may prevent the cluster from coming up during deployment.</span></span> <span data-ttu-id="0fa88-211">Para autodiagnosticar problemas de segurança, procure no grupo de visualizador de eventos *Logs Aplicativos e Serviços* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="0fa88-211">To self-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

