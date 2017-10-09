---
title: "aaaSecure uma malha do Azure serviço de cluster no Windows usando certificados | Microsoft Docs"
description: "Este artigo descreve como toosecure comunicação dentro Olá autônomo ou privada cluster bem como entre clientes e o cluster de saudação."
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
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="bca4f-103">Proteger um cluster autônomo no Windows usando os certificados X.509</span><span class="sxs-lookup"><span data-stu-id="bca4f-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="bca4f-104">Este artigo descreve como a comunicação entre Olá toosecure Olá vários nós de cluster do Windows autônoma, assim como tooauthenticate os clientes conectados toothis cluster, usando certificados x. 509.</span><span class="sxs-lookup"><span data-stu-id="bca4f-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="bca4f-105">Isso garante que somente usuários autorizados possam acessar o cluster de Olá Olá aplicativos implantados e executar tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="bca4f-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="bca4f-106">Segurança de certificado deve ser habilitada no cluster hello quando Olá cluster é criado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="bca4f-107">Para obter mais informações sobre segurança de cluster, como nós de segurança, segurança de nó de cliente e controle de acesso baseado em função, confira [Cenários de segurança de cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="bca4f-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="bca4f-108">De quais certificados você precisará?</span><span class="sxs-lookup"><span data-stu-id="bca4f-108">Which certificates will you need?</span></span>
<span data-ttu-id="bca4f-109">toostart, [baixar pacote de cluster autônomo Olá](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone de nós de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="bca4f-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="bca4f-110">Em Olá baixado o pacote, você encontrará um **ClusterConfig.X509.MultiMachine.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="bca4f-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="bca4f-111">Abra o arquivo hello e examine a seção Olá para **segurança** em Olá **propriedades** seção:</span><span class="sxs-lookup"><span data-stu-id="bca4f-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

<span data-ttu-id="bca4f-112">Esta seção descreve os certificados de saudação que é necessário para proteger o cluster do Windows autônoma.</span><span class="sxs-lookup"><span data-stu-id="bca4f-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="bca4f-113">Se você estiver especificando um certificado de cluster, defina o valor de saudação do **ClusterCredentialType** too_**X509**_. Se você estiver especificando o certificado do servidor para conexões externas, defina Olá **ServerCredentialType** muito_**X509**_. Embora não seja obrigatório, é recomendável toohave ambos esses certificados para um cluster protegido adequadamente. Se você definir esses valores muito*X509* , em seguida, você também deve especificar Olá certificados correspondentes ou do Service Fabric lançará uma exceção. Em alguns cenários, convém apenas Olá toospecify _ClientCertificateThumbprints_ ou _ReverseProxyCertificate_. Nesses cenários, você não precisa definir _ClusterCredentialType_ ou _ServerCredentialType_ too_X509_.</span><span class="sxs-lookup"><span data-stu-id="bca4f-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="bca4f-114">Um [impressão digital](https://en.wikipedia.org/wiki/Public_key_fingerprint) é Olá a identidade primária de um certificado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="bca4f-115">Leitura [como impressão digital de um certificado do tooretrieve](https://msdn.microsoft.com/library/ms734695.aspx) toofind out impressão digital de saudação de certificados de saudação que você criar.</span><span class="sxs-lookup"><span data-stu-id="bca4f-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="bca4f-116">Olá tabela a seguir lista os certificados de saudação necessários na sua configuração de cluster:</span><span class="sxs-lookup"><span data-stu-id="bca4f-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="bca4f-117">**Configuração de CertificateInformation**</span><span class="sxs-lookup"><span data-stu-id="bca4f-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="bca4f-118">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="bca4f-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="bca4f-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="bca4f-119">ClusterCertificate</span></span> |<span data-ttu-id="bca4f-120">Recomendado para o ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bca4f-120">Recommended for test environment.</span></span> <span data-ttu-id="bca4f-121">Esse certificado é toosecure necessário Olá comunicação entre os nós de saudação em um cluster.</span><span class="sxs-lookup"><span data-stu-id="bca4f-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="bca4f-122">Você pode usar dois certificados diferentes, um principal e um secundário para atualização.</span><span class="sxs-lookup"><span data-stu-id="bca4f-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="bca4f-123">Definir a impressão digital de saudação do certificado principal Olá no hello **impressão digital** seção e que Olá secundário no hello **ThumbprintSecondary** variáveis.</span><span class="sxs-lookup"><span data-stu-id="bca4f-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="bca4f-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="bca4f-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="bca4f-125">Recomendado para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bca4f-125">Recommended for production environment.</span></span> <span data-ttu-id="bca4f-126">Esse certificado é toosecure necessário Olá comunicação entre os nós de saudação em um cluster.</span><span class="sxs-lookup"><span data-stu-id="bca4f-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="bca4f-127">Você pode usar um ou dois nomes comuns de certificado de cluster.</span><span class="sxs-lookup"><span data-stu-id="bca4f-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="bca4f-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="bca4f-128">ServerCertificate</span></span> |<span data-ttu-id="bca4f-129">Recomendado para o ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bca4f-129">Recommended for test environment.</span></span> <span data-ttu-id="bca4f-130">Esse certificado é apresentado toohello cliente quando ele tenta tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="bca4f-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="bca4f-131">Para sua conveniência, você pode escolher toouse Olá mesmo certificado para *ClusterCertificate* e *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="bca4f-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="bca4f-132">Você pode usar dois certificados de servidor diferentes, um principal e um secundário, para atualização.</span><span class="sxs-lookup"><span data-stu-id="bca4f-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="bca4f-133">Definir a impressão digital de saudação do certificado principal Olá no hello **impressão digital** seção e que Olá secundário no hello **ThumbprintSecondary** variáveis.</span><span class="sxs-lookup"><span data-stu-id="bca4f-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="bca4f-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="bca4f-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="bca4f-135">Recomendado para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bca4f-135">Recommended for production environment.</span></span> <span data-ttu-id="bca4f-136">Esse certificado é apresentado toohello cliente quando ele tenta tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="bca4f-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="bca4f-137">Para sua conveniência, você pode escolher toouse Olá mesmo certificado para *ClusterCertificateCommonNames* e *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="bca4f-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="bca4f-138">Você pode usar um ou dois nomes comuns de certificado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="bca4f-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="bca4f-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="bca4f-140">Este é um conjunto de certificados que você deseja tooinstall em clientes Olá autenticado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="bca4f-141">Você pode ter um número diferente de certificados de cliente instalado nos computadores de saudação que você deseja que o cluster de toohello tooallow acesso.</span><span class="sxs-lookup"><span data-stu-id="bca4f-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="bca4f-142">Definir a impressão digital de saudação de cada certificado em Olá **CertificateThumbprint** variável.</span><span class="sxs-lookup"><span data-stu-id="bca4f-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="bca4f-143">Se você definir Olá **IsAdmin** muito*true*, e em seguida, cliente Olá com esse certificado instalado pode fazer administrador atividades de gerenciamento de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="bca4f-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="bca4f-144">Se hello **IsAdmin** é *false*, cliente Olá com esse certificado só pode executar ações de saudação permitidas para direitos de acesso do usuário, normalmente somente leitura.</span><span class="sxs-lookup"><span data-stu-id="bca4f-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="bca4f-145">Para obter mais informações sobre funções, leia [RBAC (controle de acesso baseado em função)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="bca4f-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="bca4f-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="bca4f-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="bca4f-147">Conjunto Olá nome comum do certificado de cliente primeiro Olá Olá **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="bca4f-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="bca4f-148">Olá **CertificateIssuerThumbprint** é a impressão digital de saudação para emissor Olá deste certificado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="bca4f-149">Leitura [trabalhar com certificados](https://msdn.microsoft.com/library/ms731899.aspx) tooknow mais sobre nomes comuns e emissor hello.</span><span class="sxs-lookup"><span data-stu-id="bca4f-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="bca4f-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="bca4f-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="bca4f-151">Recomendado para o ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bca4f-151">Recommended for test environment.</span></span> <span data-ttu-id="bca4f-152">Este é um certificado opcional que pode ser especificado se você quiser toosecure seu [Proxy Inverter](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="bca4f-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="bca4f-153">Verifique se reverseProxyEndpointPort está definido em nodeTypes caso você esteja usando esse certificado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="bca4f-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="bca4f-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="bca4f-155">Recomendado para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bca4f-155">Recommended for production environment.</span></span> <span data-ttu-id="bca4f-156">Este é um certificado opcional que pode ser especificado se você quiser toosecure seu [Proxy Inverter](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="bca4f-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="bca4f-157">Verifique se reverseProxyEndpointPort está definido em nodeTypes caso você esteja usando esse certificado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="bca4f-158">Aqui está o exemplo de configuração de cluster onde os certificados de Cluster de servidor e cliente Olá foram fornecidos.</span><span class="sxs-lookup"><span data-stu-id="bca4f-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="bca4f-159">Observe que, para cluster / server / certificados reverseProxy, impressão digital e o nome comum não são permitidas toobe configurados juntos para Olá mesmo tipo de certificado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

## <a name="certificate-roll-over"></a><span data-ttu-id="bca4f-160">Rolagem do certificado</span><span class="sxs-lookup"><span data-stu-id="bca4f-160">Certificate roll over</span></span>
<span data-ttu-id="bca4f-161">Ao usar o nome comum do certificado em vez de impressão digital, sobreposição de certificado não requer a atualização de configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="bca4f-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="bca4f-162">Se a sobreposição de certificado envolve emissor sobrepor, mantenha antigo certificado de emissor Olá no repositório de certificados de saudação pelo menos 2 horas depois de instalar o novo certificado de emissor hello.</span><span class="sxs-lookup"><span data-stu-id="bca4f-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="bca4f-163">Obter certificados x. 509 de saudação</span><span class="sxs-lookup"><span data-stu-id="bca4f-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="bca4f-164">comunicação toosecure em cluster Olá, você primeiro precisará certificados x. 509 de tooobtain para os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="bca4f-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="bca4f-165">Além disso, toolimit conexão toothis tooauthorized máquinas/usuários do cluster, será necessário tooobtain e instalar certificados para computadores cliente do hello.</span><span class="sxs-lookup"><span data-stu-id="bca4f-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="bca4f-166">Para clusters que executam cargas de trabalho de produção, você deve usar um [autoridade de certificação (CA)](https://en.wikipedia.org/wiki/Certificate_authority) assinados do cluster de saudação de toosecure de certificado x. 509.</span><span class="sxs-lookup"><span data-stu-id="bca4f-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="bca4f-167">Para obter detalhes sobre como obter esses certificados, acesse muito[como: obter um certificado](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="bca4f-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="bca4f-168">Para clusters que usam para fins de teste, você pode escolher toouse um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="bca4f-169">Opcional: criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="bca4f-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="bca4f-170">Uma maneira toocreate um certificado autoassinado que pode ser protegido corretamente é toouse Olá *CertSetup.ps1* script na pasta do SDK do Service Fabric Olá no diretório Olá *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="bca4f-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="bca4f-171">Editar esse nome do arquivo toochange Olá padrão do certificado de saudação (procure o valor de saudação *CN = ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="bca4f-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="bca4f-172">Execute esse script como `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="bca4f-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="bca4f-173">Exporte arquivo PFX do hello certificado tooa com uma senha protegida.</span><span class="sxs-lookup"><span data-stu-id="bca4f-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="bca4f-174">Primeiro obtenha a impressão digital de saudação do certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="bca4f-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="bca4f-175">De saudação *iniciar* menu, executar Olá *gerenciar certificados de computador*.</span><span class="sxs-lookup"><span data-stu-id="bca4f-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="bca4f-176">Navegue toohello **Local\Pessoal.** pasta e localize Olá certificado apenas criado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="bca4f-177">Clique duas vezes em Olá certificado tooopen-lo, selecione Olá *detalhes* guia e role para baixo toohello *impressão digital* campo.</span><span class="sxs-lookup"><span data-stu-id="bca4f-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="bca4f-178">Copie o valor de impressão digital Olá comando do PowerShell Olá abaixo, após remover espaços hello.</span><span class="sxs-lookup"><span data-stu-id="bca4f-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="bca4f-179">Saudação de alteração `String` valor tooa adequado senha segura tooprotect-lo e execução hello a seguir no PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bca4f-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="bca4f-180">detalhes de saudação toosee de um certificado instalado no hello máquina que você pode executar Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="bca4f-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="bca4f-181">Como alternativa, se você tiver uma assinatura do Azure, siga a seção Olá [adicionar certificados tooKey cofre](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="bca4f-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="bca4f-182">Instalar certificados de saudação</span><span class="sxs-lookup"><span data-stu-id="bca4f-182">Install hello certificates</span></span>
<span data-ttu-id="bca4f-183">Uma vez que o certificado, você pode instalá-los em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="bca4f-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="bca4f-184">Os nós precisam toohave hello mais recente do Windows PowerShell 3. x instalado neles.</span><span class="sxs-lookup"><span data-stu-id="bca4f-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="bca4f-185">Você precisará toorepeat essas etapas em cada nó de Cluster e o servidor de certificados e todos os certificados secundários.</span><span class="sxs-lookup"><span data-stu-id="bca4f-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="bca4f-186">Copie o nó de toohello hello. pfx (s).</span><span class="sxs-lookup"><span data-stu-id="bca4f-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="bca4f-187">Abra uma janela do PowerShell como administrador e digite Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="bca4f-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="bca4f-188">Substituir saudação *$pswd* com senha Olá usado toocreate esse certificado.</span><span class="sxs-lookup"><span data-stu-id="bca4f-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="bca4f-189">Substituir saudação *$PfxFilePath* com caminho completo de saudação do nó de toothis copiado do hello. pfx.</span><span class="sxs-lookup"><span data-stu-id="bca4f-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="bca4f-190">Defina agora o controle de acesso de saudação neste certificado para que o processo de Service Fabric hello, que é executado sob Olá conta de serviço de rede, pode usá-lo executando Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="bca4f-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="bca4f-191">Forneça Olá a impressão digital do certificado hello e "Serviço de rede" hello conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="bca4f-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="bca4f-192">Você pode verificar que Olá ACLs no certificado Olá estão corretas abrindo certificado Olá no *iniciar* > *gerenciar certificados de computador* e examinando *todas as tarefas*  >  *Gerenciar chaves particulares*.</span><span class="sxs-lookup"><span data-stu-id="bca4f-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="bca4f-193">Repita as etapas de saudação acima para cada certificado de servidor.</span><span class="sxs-lookup"><span data-stu-id="bca4f-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="bca4f-194">Você também pode usar essas etapas tooinstall Olá certificados de cliente em computadores de saudação que você deseja que o cluster de toohello tooallow acesso.</span><span class="sxs-lookup"><span data-stu-id="bca4f-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="bca4f-195">Criar cluster seguro Olá</span><span class="sxs-lookup"><span data-stu-id="bca4f-195">Create hello secure cluster</span></span>
<span data-ttu-id="bca4f-196">Depois de configurar Olá **segurança** seção Olá **ClusterConfig.X509.MultiMachine.json** arquivo, você pode continuar muito[criar seu cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure de seção Olá nós e criar um cluster Olá autônomo.</span><span class="sxs-lookup"><span data-stu-id="bca4f-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="bca4f-197">Lembre-se de saudação toouse **ClusterConfig.X509.MultiMachine.json** arquivo durante a criação de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bca4f-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="bca4f-198">Por exemplo, o comando pode parecer com hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="bca4f-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="bca4f-199">Depois que você tiver Olá seguro autônomo do Windows cluster com êxito em execução e que a instalação Olá clientes autenticados tooconnect tooit, execute a seção de saudação [conectar tooa cluster seguro usando o PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="bca4f-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="bca4f-200">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bca4f-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="bca4f-201">Você pode executar outra toowork de comandos do PowerShell com este cluster.</span><span class="sxs-lookup"><span data-stu-id="bca4f-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="bca4f-202">Por exemplo, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow uma lista de nós neste cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="bca4f-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="bca4f-203">cluster de saudação tooremove, conectar toohello nó no cluster Olá onde você baixou o pacote do Service Fabric hello, abra uma linha de comando e navegue toohello pasta do pacote.</span><span class="sxs-lookup"><span data-stu-id="bca4f-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="bca4f-204">Agora execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bca4f-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="bca4f-205">Configuração de certificado incorreto pode impedir que o cluster Olá chegando durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="bca4f-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="bca4f-206">tooself-diagnosticar problemas de segurança, consulte no grupo de Visualizador de eventos *Applications and Services Logs* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="bca4f-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

