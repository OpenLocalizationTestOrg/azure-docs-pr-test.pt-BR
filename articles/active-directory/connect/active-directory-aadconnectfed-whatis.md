---
title: "aaaAzure AD Connect e federação | Microsoft Docs"
description: "Esta página é local central Olá toda a documentação sobre operações do AD FS que usam o Azure AD Connect."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Azure AD Connect e federação
O Azure Active Directory (Azure AD) Connect permite a você configurar a federação com os Serviços de Federação do Active Directory (AD FS) locais e o Azure AD. Com federação entrar, você pode habilitar toosign de usuários nos serviços de baseado no AD tooAzure com suas senhas locais – e, enquanto estiver na rede corporativa da saudação, sem ter que tooenter suas senhas novamente. Usando a opção de Federação Olá com o AD FS, você pode implantar uma nova instalação do AD FS, ou você pode especificar uma instalação existente em um farm do Windows Server 2012 R2.

Este tópico é saudação inicial para obter informações sobre as funcionalidades relacionadas à Federação para o Azure AD Connect. Ela lista links de tópicos de tooall relacionados. Para links tooAzure AD Connect, consulte [integrando suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).

## <a name="azure-ad-connect-federation-topics"></a>Azure AD Connect: tópicos sobre federação
| Tópico | O que ela abrange e quando tooread-lo |
|:--- |:--- |
| **Opções de entrada de usuário do Azure AD Connect** | |
| [Noções básicas sobre as opções de entrada do usuário](active-directory-aadconnect-user-signin.md) |Saiba mais sobre opções de entrada do usuário vários e como eles afetam a experiência do usuário Olá entrada do Azure. |
| **Instalação do AD FS usando o Azure AD Connect** | |
| [Pré-requisitos](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |Consulte Olá pré-requisitos para a instalação bem-sucedida do AD FS por meio do Azure AD Connect. |
| [Configurar um farm do AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Instale um novo farm do AD FS usando o Azure AD Connect. |
| [Federar ao Azure AD usando uma ID de logon alternativa ](active-directory-aadconnect-federation-management.md#alternateid) | Configurar a federação usando uma ID de logon alternativa  |
| **Modificar configuração do hello AD FS** | |
| [Reparar confiança Olá](active-directory-aadconnect-federation-management.md#repairthetrust) |Reparo Olá atual confiança entre locais do AD FS e o Office 365/Azure. |
| [Adicionar um novo servidor do AD FS](active-directory-aadconnect-federation-management.md#addadfsserver) |Expanda um farm do AD FS com um servidor do AD FS adicional após a instalação inicial. |
| [Adicionar um novo servidor WAP do AD FS](active-directory-aadconnect-federation-management.md#addwapserver) |Expanda um farm do AD FS com um servidor WAP (Proxy de Aplicativo Web) adicional após a instalação inicial. |
| [Adicionar um novo domínio federado](active-directory-aadconnect-federation-management.md#addfeddomain) |Adicione outro toobe domínio federado com AD do Azure. |
| [Atualizar o certificado SSL de saudação](active-directory-aadconnectfed-ssl-update.md)| Atualize o certificado SSL Olá para um farm do AD FS. |
| **Outra configuração de federação** | |
| [Federar várias instâncias do Azure AD com uma única instância do AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | Federar vários Azure ADs a um único farm do AD FS| 
| [Adicionar uma ilustração/logotipo personalizado da empresa](active-directory-aadconnect-federation-management.md#customlogo) |Modificar a experiência de entrada hello especificar Olá logotipo personalizado que é mostrado no hello AD FS-página de entrada. |
| [Adicionar uma descrição de entrada](active-directory-aadconnect-federation-management.md#addsignindescription) |Alterar Olá entrar descrição na página de entrada hello do AD FS. |
| [Modificar regras de declaração do AD FS](active-directory-aadconnect-federation-management.md#modclaims) |Modificar ou adicionar regras de declaração do AD FS que correspondem a configuração de sincronização tooAzure AD Connect. |


## <a name="additional-resources"></a>Recursos adicionais
* [Federando dois Azure ADs a um único AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Implantação do AD FS no Azure](active-directory-aadconnect-azure-adfs.md)
* [Implantação do AD FS de alta disponibilidade entre fronteiras geográficas no Azure com o Gerenciador de Tráfego do Azure](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
