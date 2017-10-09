---
title: aaaUpgrade tooAzure AD Proxy de aplicativo | Microsoft Docs
description: "Escolha qual solução de proxy será a melhor se você estiver atualizando do Microsoft Forefront ou do Unified Access Gateway."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>Comparar as soluções de acesso remoto

O Azure Active Directory Application Proxy é uma das duas soluções de acesso remoto que a Microsoft oferece. Olá outros é o Proxy de aplicativo Web, versão de local de saudação. Essas duas soluções substituem os produtos anteriores oferecidos pela Microsoft: Microsoft Forefront Threat Management Gateway (TMG) e Unified Access Gateway (UAG). Use este artigo toounderstand como essas quatro soluções comparam tooeach outros. Para aqueles que ainda utilizam Olá preterido soluções TMG ou UAG, use este plano do artigo toohelp tooone sua migração de saudação Proxy de aplicativo. 


## <a name="feature-comparison"></a>Comparação de recursos

Use essa tabela toounderstand como Threat Management Gateway (TMG), o Unified Access Gateway (UAG), o Proxy de aplicativo da Web (WAP) e o Proxy de aplicativo do Azure AD (AP) comparam tooeach outros.

| Recurso | TMG | UAG | WAP | AP |
| ------- | --- | --- | --- | --- |
| Autenticação de certificado | Sim | Sim | - | - |
| Publicar seletivamente os aplicativos de navegador | Sim | Sim | Sim | Sim |
| Pré-autenticação e logon único | Sim | Sim | Sim | Sim | 
| Firewall de Camada 2/3 | Sim | Sim | - | - |
| Recursos de proxy de encaminhamento | Sim | - | - | - |
| Funcionalidades de VPN | Sim | Sim | - | - |
| Suporte avançado a protocolo | - | Sim | Sim, se estiver em execução sobre HTTP | Sim, se a execução for feita via HTTP ou por meio do Gateway de Área de Trabalho Remota |
| Atua como um servidor proxy do ADFS | - | Sim | Sim | - |
| Um portal para acesso de aplicativo | - | Sim | - | Sim |
| Conversão de link de corpo de resposta | Sim | Sim | - | Sim | 
| Autenticação com cabeçalhos | - | Sim | - | Sim, com PingAccess | 
| Segurança em escala de nuvem | - | - | - | Sim | 
| Acesso condicional | - | Sim | - | Sim |
| Nenhum componente no perímetro da saudação (DMZ) | - | - | - | Sim |
| Nenhuma conexão de entrada | - | - | - | Sim |

Na maioria dos cenários, é recomendável aplicativo do Azure AD como solução modernos hello. P Proxy de Aplicativo Web é preferencial apenas em cenários que exigem um servidor proxy para o AD FS e não pode usar domínios personalizados no Azure Active Directory. 

Proxy de aplicativo do Azure AD oferece beneficiam exclusivos quando comparados toosimilar produtos, inclusive:

- Estendendo os recursos de tooon locais do AD do Azure
   - Proteção e segurança em escala de nuvem
   - Recursos como acesso condicional e autenticação multifator são tooenable fácil
- Não há componenet no perímetro Olá
- Nenhuma conexão de entrada necessária
- Painel de um acesso que os usuários podem ir toofor todos os seus aplicativos, como o O365, integrado ao AD do Azure aplicativos SaaS e aplicativos web do seu local. 


## <a name="next-steps"></a>Próximas etapas

- [Usar aplicativos de tooon local do aplicativo do Azure AD tooprovide acesso remoto seguro](active-directory-application-proxy-get-started.md)
- [Transição do Forefront TMG e UAG tooApplication Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).
