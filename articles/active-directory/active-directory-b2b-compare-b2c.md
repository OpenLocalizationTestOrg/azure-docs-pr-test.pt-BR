---
title: "aaaCompare B2B B2C no Active Directory do Azure e colaboração | Microsoft Docs"
description: "Qual é a diferença Olá entre colaboração B2B do Azure Active Directory e Azure AD B2C?"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>Comparação da colaboração B2B e B2C no Azure Active Directory

Colaboração B2B do Azure Active Directory (AD do Azure) e o Azure AD B2C permitem toowork com usuários externos no AD do Azure. Mas como eles se comparam?


Recursos de colaboração B2B |     Oferta autônoma do B2C do AD do Azure
-------- | --------
Destinado: as organizações que desejam toobe tooauthenticate capaz de usuários de uma organização de parceiro, independentemente do provedor de identidade. | Destinado a: convidar clientes dos aplicativos Web e móveis, sejam indivíduos, clientes institucionais ou organizacionais, para o Azure AD.
Identidades suportadas: funcionários com contas corporativas ou escolares, parceiros com contas corporativas ou escolares ou qualquer email. Em breve toosupport federação direta.  | Identidades suportadas: os usuários do consumidor com contas de aplicativo local (qualquer nome de usuário ou email) ou identidades sociais suportadas com federação direta.
Quais usuários de parceiros de saudação do diretório estão em: parceiro usuários da organização externa Olá são gerenciados no hello mesmo diretório que os funcionários, mas anotado especialmente. Eles podem ser gerenciados hello mesmo maneira como os funcionários, pode ser adicionado toohello mesmo grupos e assim por diante  | Quais entidades de usuário do diretório Olá cliente estão em: no diretório de aplicativo hello. Gerenciadas separadamente da saudação funcionários e parceiros o diretório da organização (se houver.
Single sign-on (SSO) tooall Azure aplicativos conectados AD é suportado. Por exemplo, você pode fornecer acesso tooOffice 365 ou aplicativos locais e aplicativos de SaaS tooother como a equipe de vendas ou Workday.  |  SSO toocustomer propriedade aplicativos nos locatários de saudação do Azure AD B2C é suportado. SSO tooOffice 365 ou não há suporte para aplicativos da Microsoft e não - Microsoft SaaS tooother.
Ciclo de vida do parceiro: gerenciados pelo Olá host/convidar organização.  | Ciclo de vida do cliente: gerenciado pelo aplicativo hello ou autoatendimento.
Política de segurança e conformidade: gerenciados pelo Olá host/convidar organização.  | Política de segurança e conformidade: gerenciados pelo aplicativo hello.
Identidade visual: uso da marca da organização convidada/host.  |    Identidade visual: gerenciada pelo aplicativo. Normalmente tende toobe produto da marca, desaparece a organização Olá no plano de fundo de saudação.
Mais informações em: [Postagem de Blog](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [Documentação](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | Mais informações em: [Página](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [Documentação](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de usuário de colaboração B2B](active-directory-b2b-user-properties.md)
* [Adicionando uma função de tooa de usuário de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegação de convites de colaboração B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinâmicos e colaboração B2B](active-directory-b2b-dynamic-groups.md)
* [Configuração de aplicativos SaaS para colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuário de colaboração B2B](active-directory-b2b-user-token.md)
* [Mapeamento de declarações de usuário de colaboração B2B](active-directory-b2b-claims-mapping.md)
* [Compartilhamento externo do Office 365](active-directory-b2b-o365-external-user.md)
* [Limitações atuais da colaboração B2B](active-directory-b2b-current-limitations.md)
* [Como obter suporte para colaboração B2B](active-directory-b2b-support.md)
