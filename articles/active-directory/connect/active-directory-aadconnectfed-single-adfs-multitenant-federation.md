---
title: "Associando vários Azure AD com um AD FS único | Microsoft Docs"
description: "Neste documento, você aprenderá a federar vários Azure AD com um único AD FS."
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
ms.openlocfilehash: 436bf5905d2b203dc4cceea97f4fb90593df7111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="aff14-104">Federar várias instâncias do Azure AD com uma instância única do AD FS</span><span class="sxs-lookup"><span data-stu-id="aff14-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="aff14-105">Um único farm do AD FS de alta disponibilidade pode federar várias florestas se tiverem uma relação de confiança bidirecional.</span><span class="sxs-lookup"><span data-stu-id="aff14-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="aff14-106">Essas várias florestas podem ou não corresponder ao mesmo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aff14-106">These multiple forests may or may not correspond to the same Azure Active Directory.</span></span> <span data-ttu-id="aff14-107">Este artigo fornece instruções sobre como configurar a federação entre uma única implantação do AD FS e mais de uma floresta que sincronizam com Azure AD diferentes.</span><span class="sxs-lookup"><span data-stu-id="aff14-107">This article provides instructions on how to configure federation between a single AD FS deployment and more than one forests that sync to different Azure AD.</span></span>

![Federação de multilocatária com AD FS único](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="aff14-109">O write-back de dispositivo e o ingresso automático de dispositivo não têm suporte neste cenário.</span><span class="sxs-lookup"><span data-stu-id="aff14-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="aff14-110">O Azure AD Connect não pode ser usado para configurar a federação neste cenário como o Azure AD Connect pode configurar a federação de domínios em um único Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aff14-110">Azure AD Connect cannot be used to configure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="aff14-111">Etapas para federar o AD FS com vários Azure AD</span><span class="sxs-lookup"><span data-stu-id="aff14-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="aff14-112">Imagine um domínio contoso.com no contoso.onmicrosoft.com do Azure Active Directory já é federado com o AD FS local instalado no ambiente de Active Directory local contoso.com.</span><span class="sxs-lookup"><span data-stu-id="aff14-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with the AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="aff14-113">Fabrikam.com é um domínio no Azure Active Directory fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="aff14-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="aff14-114">Etapa 1: estabelecer uma confiança mútua</span><span class="sxs-lookup"><span data-stu-id="aff14-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="aff14-115">Para que o AD FS em contoso.com seja capaz de autenticar usuários no fabrikam.com, uma relação de confiança bidirecional é necessária entre contoso.com e fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="aff14-115">For AD FS in contoso.com to be able to authenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com.</span></span> <span data-ttu-id="aff14-116">Siga as diretrizes neste [artigo](https://technet.microsoft.com/library/cc816590.aspx) para criar a relação de confiança bidirecional.</span><span class="sxs-lookup"><span data-stu-id="aff14-116">Follow the guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) to create the two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="aff14-117">Etapa 2: modificar configurações de federação de contoso.com</span><span class="sxs-lookup"><span data-stu-id="aff14-117">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="aff14-118">O emissor padrão definido para um único domínio federado ao AD FS é "http://ADFSServiceFQDN/adfs/services/trust", por exemplo, "http://fs.contoso.com/adfs/services/trust".</span><span class="sxs-lookup"><span data-stu-id="aff14-118">The default issuer set for a single domain federated to AD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="aff14-119">O Azure Active Directory requer um emissor exclusivo para cada domínio.</span><span class="sxs-lookup"><span data-stu-id="aff14-119">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="aff14-120">Já que o mesmo AD FS vai federar dois domínios, o valor do emissor deve ser modificado para ser exclusivo para cada domínio federado pelo AD FS com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aff14-120">Since the same AD FS is going to federate two domains, the issuer value needs to be modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="aff14-121">No servidor do AD FS, abra o Azure AD PowerShell e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="aff14-121">On the AD FS server, open Azure AD PowerShell and perform the following steps:</span></span>
 
<span data-ttu-id="aff14-122">Conecte-se ao Azure Active Directory que contém o domínio contoso.com Connect-MsolService Atualize as configurações de federação para contoso.com Update-MsolFederatedDomain - DomainName contoso.com – SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="aff14-122">Connect to the Azure Active Directory that contains the domain contoso.com Connect-MsolService Update the federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="aff14-123">O emissor na configuração da federação de domínio será alterado para "http://contoso.com/adfs/services/trust" e uma regra de declaração de emissão será adicionada para que a confiança da terceira parte confiável emita o valor de issuerId correto com base no sufixo UPN.</span><span class="sxs-lookup"><span data-stu-id="aff14-123">Issuer in the domain federation setting will be changed to "http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for the Azure AD Relying Party Trust to issue the correct issuerId value based on the UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="aff14-124">Etapa 3: federar fabrikam.com com o AD FS</span><span class="sxs-lookup"><span data-stu-id="aff14-124">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="aff14-125">Na sessão do Azure AD PowerShell, execute as seguintes etapas: conecte-se ao Azure Active Directory que contém o domínio fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="aff14-125">In Azure AD powershell session perform the following steps: Connect to Azure Active Directory that contains the domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="aff14-126">Converta o domínio gerenciado fabrikam.com em federado:</span><span class="sxs-lookup"><span data-stu-id="aff14-126">Convert the fabrikam.com managed domain to federated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="aff14-127">A operação acima vai federar o domínio fabrikam.com com o mesmo AD FS.</span><span class="sxs-lookup"><span data-stu-id="aff14-127">The above operation will federate the domain fabrikam.com with the same AD FS.</span></span> <span data-ttu-id="aff14-128">Você pode verificar as configurações de domínio usando Get-MsolDomainFederationSettings para os dois domínios.</span><span class="sxs-lookup"><span data-stu-id="aff14-128">You can verify the domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aff14-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aff14-129">Next steps</span></span>
[<span data-ttu-id="aff14-130">Conectar o Active Directory com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aff14-130">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
