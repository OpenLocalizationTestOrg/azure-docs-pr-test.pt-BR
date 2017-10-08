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
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>Federar várias instâncias do Azure AD com uma instância única do AD FS

Um único farm do AD FS de alta disponibilidade pode federar várias florestas se tiverem uma relação de confiança bidirecional. Essas várias florestas podem ou não pode corresponder toohello mesmo Azure Active Directory. Este artigo fornece instruções sobre como tooconfigure federação entre uma única implantação do AD FS e mais de um florestas que toodifferent de sincronização do AD do Azure.

![Federação de multilocatária com AD FS único](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> O write-back de dispositivo e o ingresso automático de dispositivo não têm suporte neste cenário.

> [!NOTE]
> Azure AD Connect não pode ser federação tooconfigure usada neste cenário do Azure AD Connect pode configurar a federação para domínios em um único AD do Azure.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>Etapas para federar o AD FS com vários Azure AD

Considere a possibilidade de que um domínio contoso.com de Active Directory do Azure contoso.onmicrosoft.com já for federado com saudação do AD FS instalado no ambiente de Active Directory do contoso.com local ao local. Fabrikam.com é um domínio no Azure Active Directory fabrikam.onmicrosoft.com.

##<a name="step-1-establish-a-two-way-trust"></a>Etapa 1: estabelecer uma confiança mútua
 
Para o AD FS em contoso.com toobe tooauthenticate capaz de usuários no fabrikam.com, uma relação de confiança bidirecional é necessária entre contoso.com e fabrikam.com. Siga a orientação Olá neste [artigo](https://technet.microsoft.com/library/cc816590.aspx) toocreate Olá relação de confiança bidirecional.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>Etapa 2: modificar configurações de federação de contoso.com 
 
emissor de padrão de saudação definido tooAD um único domínio federado FS é "http://ADFSServiceFQDN/adfs/services/trust", por exemplo, "http://fs.contoso.com/adfs/services/trust". O Azure Active Directory requer um emissor exclusivo para cada domínio. Como Olá mesmo AD FS vai toofederate dois domínios, o valor de emissor Olá deve toobe modificado de forma que ele seja exclusivo para cada domínio que do AD FS federa com o Active Directory do Azure. 
 
No servidor de saudação do AD FS, abra o PowerShell do Azure AD e execute Olá etapas a seguir:
 
Conecte-se toohello Active Directory do Azure que contém a saudação domínio contoso.com Connect-MsolService atualização Olá configurações de federação para contoso.com Update-MsolFederatedDomain - DomainName contoso.com – SupportMultipleDomain
 
Emissor na configuração de Federação do domínio Olá será alterada muito "http://contoso.com/adfs/services/trust" e a emissão de uma declaração de regra será adicionada para Olá AD do Azure terceira parte confiável tooissue Olá correto issuerId valor com base em sufixo UPN hello.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>Etapa 3: federar fabrikam.com com o AD FS
 
No AD do Azure powershell sessão executar Olá etapas a seguir: conectar-se tooAzure do Active Directory que contém a saudação domínio fabrikam.com

    Connect-MsolService
Converta toofederated de domínio fabrikam.com gerenciados hello:

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
Olá acima operação será federar Olá domínio fabrikam.com com hello mesmo AD FS. Você pode verificar as configurações de domínio hello usando Get-MsolDomainFederationSettings para os dois domínios.

## <a name="next-steps"></a>Próximas etapas
[Conectar o Active Directory com o Azure Active Directory](active-directory-aadconnect.md)
