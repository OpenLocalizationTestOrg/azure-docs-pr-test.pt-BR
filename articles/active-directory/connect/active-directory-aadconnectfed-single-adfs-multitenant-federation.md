---
title: "aaaFederating vários AD do Azure com o AD FS único | Microsoft Docs"
description: "Este documento, você aprenderá como toofederate vários AD do Azure com um único do AD FS."
keywords: "federar, ADFS, AD FS, vários locatários, único AD FS, um ADFS, federação multilocatária, adfs de várias florestas, aad connect, federação, federação entre locatários"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="721e6-104">Federar várias instâncias do Azure AD com uma instância única do AD FS</span><span class="sxs-lookup"><span data-stu-id="721e6-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="721e6-105">Um único farm do AD FS de alta disponibilidade pode federar várias florestas se tiverem uma relação de confiança bidirecional.</span><span class="sxs-lookup"><span data-stu-id="721e6-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="721e6-106">Essas várias florestas podem ou não pode corresponder toohello mesmo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="721e6-106">These multiple forests may or may not correspond toohello same Azure Active Directory.</span></span> <span data-ttu-id="721e6-107">Este artigo fornece instruções sobre como tooconfigure federação entre uma única implantação do AD FS e mais de um florestas que toodifferent de sincronização do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="721e6-107">This article provides instructions on how tooconfigure federation between a single AD FS deployment and more than one forests that sync toodifferent Azure AD.</span></span>

![Federação de multilocatária com AD FS único](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="721e6-109">O write-back de dispositivo e o ingresso automático de dispositivo não têm suporte neste cenário.</span><span class="sxs-lookup"><span data-stu-id="721e6-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="721e6-110">Azure AD Connect não pode ser federação tooconfigure usada neste cenário do Azure AD Connect pode configurar a federação para domínios em um único AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="721e6-110">Azure AD Connect cannot be used tooconfigure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="721e6-111">Etapas para federar o AD FS com vários Azure AD</span><span class="sxs-lookup"><span data-stu-id="721e6-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="721e6-112">Considere a possibilidade de que um domínio contoso.com de Active Directory do Azure contoso.onmicrosoft.com já for federado com saudação do AD FS instalado no ambiente de Active Directory do contoso.com local ao local.</span><span class="sxs-lookup"><span data-stu-id="721e6-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with hello AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="721e6-113">Fabrikam.com é um domínio no Azure Active Directory fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="721e6-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="721e6-114">Etapa 1: estabelecer uma confiança mútua</span><span class="sxs-lookup"><span data-stu-id="721e6-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="721e6-115">Para o AD FS em contoso.com toobe tooauthenticate capaz de usuários no fabrikam.com, uma relação de confiança bidirecional é necessária entre contoso.com e fabrikam.com. Siga a orientação Olá neste [artigo](https://technet.microsoft.com/library/cc816590.aspx) toocreate Olá relação de confiança bidirecional.</span><span class="sxs-lookup"><span data-stu-id="721e6-115">For AD FS in contoso.com toobe able tooauthenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com. Follow hello guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="721e6-116">Etapa 2: modificar configurações de federação de contoso.com</span><span class="sxs-lookup"><span data-stu-id="721e6-116">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="721e6-117">emissor de padrão de saudação definido tooAD um único domínio federado FS é "http://ADFSServiceFQDN/adfs/services/trust", por exemplo, "http://fs.contoso.com/adfs/services/trust".</span><span class="sxs-lookup"><span data-stu-id="721e6-117">hello default issuer set for a single domain federated tooAD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="721e6-118">O Azure Active Directory requer um emissor exclusivo para cada domínio.</span><span class="sxs-lookup"><span data-stu-id="721e6-118">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="721e6-119">Como Olá mesmo AD FS vai toofederate dois domínios, o valor de emissor Olá deve toobe modificado de forma que ele seja exclusivo para cada domínio que do AD FS federa com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="721e6-119">Since hello same AD FS is going toofederate two domains, hello issuer value needs toobe modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="721e6-120">No servidor de saudação do AD FS, abra o PowerShell do Azure AD e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="721e6-120">On hello AD FS server, open Azure AD PowerShell and perform hello following steps:</span></span>
 
<span data-ttu-id="721e6-121">Conecte-se toohello Active Directory do Azure que contém a saudação domínio contoso.com Connect-MsolService atualização Olá configurações de federação para contoso.com Update-MsolFederatedDomain - DomainName contoso.com – SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="721e6-121">Connect toohello Azure Active Directory that contains hello domain contoso.com Connect-MsolService Update hello federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="721e6-122">Emissor na configuração de Federação do domínio Olá será alterada muito "http://contoso.com/adfs/services/trust" e a emissão de uma declaração de regra será adicionada para Olá AD do Azure terceira parte confiável tooissue Olá correto issuerId valor com base em sufixo UPN hello.</span><span class="sxs-lookup"><span data-stu-id="721e6-122">Issuer in hello domain federation setting will be changed too"http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for hello Azure AD Relying Party Trust tooissue hello correct issuerId value based on hello UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="721e6-123">Etapa 3: federar fabrikam.com com o AD FS</span><span class="sxs-lookup"><span data-stu-id="721e6-123">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="721e6-124">No AD do Azure powershell sessão executar Olá etapas a seguir: conectar-se tooAzure do Active Directory que contém a saudação domínio fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="721e6-124">In Azure AD powershell session perform hello following steps: Connect tooAzure Active Directory that contains hello domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="721e6-125">Converta toofederated de domínio fabrikam.com gerenciados hello:</span><span class="sxs-lookup"><span data-stu-id="721e6-125">Convert hello fabrikam.com managed domain toofederated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="721e6-126">Olá acima operação será federar Olá domínio fabrikam.com com hello mesmo AD FS.</span><span class="sxs-lookup"><span data-stu-id="721e6-126">hello above operation will federate hello domain fabrikam.com with hello same AD FS.</span></span> <span data-ttu-id="721e6-127">Você pode verificar as configurações de domínio hello usando Get-MsolDomainFederationSettings para os dois domínios.</span><span class="sxs-lookup"><span data-stu-id="721e6-127">You can verify hello domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="721e6-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="721e6-128">Next steps</span></span>
[<span data-ttu-id="721e6-129">Conectar o Active Directory com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="721e6-129">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
