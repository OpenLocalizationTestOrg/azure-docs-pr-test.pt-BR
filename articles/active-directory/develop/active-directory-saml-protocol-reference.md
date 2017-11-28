---
title: "aaaAzure Referência de protocolo do SAML AD | Microsoft Docs"
description: "Este artigo fornece uma visão geral de perfis de logon único do SAML e saída únicos Olá no Active Directory do Azure."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: priyamo
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: d712289b16dc40a6b43a96fadef729c55cdaac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Como o Active Directory do Azure usa o protocolo do SAML Olá
Usuários do Azure Active Directory (AD do Azure) usa Olá SAML 2.0 protocolo tooenable aplicativos tooprovide um logon único experiência tootheir. Olá [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) e [logout único](active-directory-single-sign-out-protocol-reference.md) perfis SAML do AD do Azure que explicam como declarações SAML, protocolos e vinculações são usadas no serviço de provedor de identidade hello.

Protocolo SAML requer o provedor de identidade da saudação (AD do Azure) e Olá serviço provedor (aplicativo hello) tooexchange obter informações sobre si mesmos.

Quando um aplicativo é registrado com o AD do Azure, o desenvolvedor do aplicativo hello registra informações relacionadas à Federação com o Azure AD. Isso inclui Olá **URI de redirecionamento** e **Metadata URI** do aplicativo hello.

O AD do Azure usa Olá **Metadata URI** de assinatura de chave e hello logout URI do serviço de nuvem Olá Olá de tooretrieve Olá nuvem serviço. Se o aplicativo hello não oferece suporte a um URI de metadados, o desenvolvedor de saudação deve contatar Microsoft suporte tooprovide Olá logout URI e chave de assinatura.

O Azure Active Directory expõe pontos de extremidade de logon único e logout único comuns e específicos de locatário (independente do locatário). Essas URLs representam locações endereçáveis--não são apenas identificadores-- para que você possa toohello ponto de extremidade tooread Olá metadados.

* ponto de extremidade Olá específico de locatário está localizado em `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.  Olá <TenantDomainName> espaço reservado representa um nome de domínio registrado ou o GUID TenantID de um locatário do AD do Azure. Por exemplo, metadados de federação de saudação do locatário de contoso.com Olá são em: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* ponto de extremidade Olá independente de locatário está localizado em `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. Esse endereço de ponto de extremidade, **comuns** for exibida, em vez de um nome de domínio de locatário ou ID.

Para obter informações sobre documentos de metadados de federação de saudação do AD do Azure publica, consulte [metadados de Federação](active-directory-federation-metadata.md).
