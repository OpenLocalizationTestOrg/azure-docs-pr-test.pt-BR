---
title: "as notificações de provisionamento de aaaAccount | Microsoft Docs"
description: "Saiba como tooensure que você será notificado sobre problemas relacionados a toouser de provisionamento que exigem atenção, permitindo que as notificações de provisionamento de conta."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: e33d1dd806fff43fc96f843a9dcddd7375d2e3c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="account-provisioning-notifications"></a>Notificações de provisionamento de conta
Com o provisionamento de usuário, você pode automatizar o processo de saudação do gerenciamento de usuários em aplicativos SaaS de terceiros. <br>
Embora esse seja um processo automatizado, sua interação com esse processo é de tootime de tempo necessária. <br>
Isso acontece, por exemplo hello, quando a senha de saudação da conta Olá configurou tooexchange dados com um terço de SaaS aplicativo expirou. 

Ao habilitar as notificações de provisionamento de conta, você pode garantir que você será notificado sobre problemas relacionado toouser provisionamento que exigem sua atenção.

Você ativa ou desativa notificações de provisionamento de conta como parte de sua configuração de provisionamento de usuário de um aplicativo SaaS de terceiro.

![Provisionamento do usuário][1] 

tooactivate as notificações de provisionamento de conta, selecione Olá a caixa de seleção em Olá **confirmação** página da caixa de diálogo e alias de email do tipo saudação do destinatário hello.

![Notificações de provisionamento de conta][2]

Você pode inserir uma lista de distribuição como destinatário; No entanto, é importante toonote email de notificação de saudação contém tooreports links que são acessíveis apenas pelos administradores de saudação do AD do Azure.

Se você tiver habilitadas de notificações de provisionamento de conta, você receberá emails sobre questões críticas que estão relacionada toouser provisionamento. No entanto, tooavoid uma sobrecarga de emails, você receberá apenas uma notificação de email por dia para cada SaaS email de notificação do aplicativo hello está habilitado.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Automatizar o provisionamento de usuário/desprovisionamento tooSaaS aplicativos](active-directory-saas-app-provisioning.md)
* [Personalizando os mapeamentos de atributos para provisionamento de usuários](active-directory-saas-customizing-attribute-mappings.md)
* [Escrevendo expressões para mapeamentos de atributo](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtros de escopo para provisionamento de usuários](active-directory-saas-scoping-filters.md)
* [Usando SCIM o provisionamento automático tooenable de usuários e grupos do Active Directory do Azure tooapplications](active-directory-scim-provisioning.md)
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
