---
title: "aaaWhat é colaboração B2B do Azure Active Directory? | Microsoft Docs"
description: "Colaboração B2B do Active Directory do Azure suporta as relações entre empresas habilitando tooselectively de parceiros de negócios acesso a aplicativos corporativos."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: 359989b66f3d012c306e8748a607662fffacb919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a>O que é a colaboração B2B do Azure AD?

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

Recursos de colaboração (B2B) do Azure AD business-to-business habilitam qualquer organização usando o AD do Azure toowork com segurança com usuários de qualquer outra organização, grande ou pequeno. Essas organizações podem usar o Azure AD ou não ou até mesmo ter uma organização de TI ou não. 

As organizações que usam o AD do Azure podem fornecer acesso parceiros tootheir toodocuments, recursos e aplicativos, mantendo o controle completo sobre seus próprios dados corporativos. Os desenvolvedores podem usar Olá AD do Azure business-to-business APIs toowrite aplicativos reunir duas organizações mais segura. Além disso, é muito fácil para os usuários finais toonavigate.

97% de nossos clientes nos disseram a colaboração B2B do Azure AD é muito importante toothem.

![gráfico de pizza](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

Desde o início de abril de 2017, já tínhamos cerca de 3 milhões de usuários usando recursos de colaboração B2B do Azure AD. E mais de 23% das organizações do Azure AD que têm mais de 10 usuários já estão se beneficiando desses recursos.

## <a name="hello-key-benefits-of-azure-ad-b2b-collaboration-tooyour-organization"></a>principais benefícios de saudação da organização de tooyour de colaboração B2B do Azure AD

### <a name="work-with-any-user-from-any-partner"></a>Trabalhar com qualquer usuário de qualquer parceiro

* Os parceiros usam suas próprias credenciais

* Nenhum requisito para parceiros toouse AD do Azure

* Diretórios externos nem configuração complexa são necessários

### <a name="simple-and-secure-collaboration"></a>Colaboração simples e segura

* Fornecer acesso tooany corporativos aplicativo ou dados, aplicando sofisticadas, o Azure diretivas de autorização baseados em AD

* Fácil para os usuários

* Segurança de altíssimo nível para aplicativos e dados

### <a name="no-management-overhead"></a>Sem sobrecarga de gerenciamento

* Sem conta externa ou gerenciamento de senhas

* Sem gerenciamento de ciclo de vida de conta manual ou sincronizada

* Sem sobrecarga administrativa externa

## <a name="you-can-easily-add-b2b-collaboration-users-tooyour-organization"></a>Você pode adicionar facilmente a organização de tooyour de usuários de colaboração B2B

Administradores podem adicionar usuários de colaboração (convidado) B2B Olá [portal do Azure](https://portal.azure.com).

![adicionar usuários convidados](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-toobring-their-own-identity"></a>Habilitar seu colaboradores toobring sua própria identidade

Os colaboradores B2B podem entrar com uma identidade de sua escolha. Se o usuário Olá não tiver uma conta da Microsoft ou uma conta do AD do Azure – um é criado para eles diretamente em tempo de saudação de resgate de oferta.

![Escolha de identidade de logon](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-tooapplication-and-group-owners"></a>Proprietários de tooapplication e de grupo delegado 
Aplicativo e proprietários de grupo podem adicionar usuários de B2B diretamente tooany aplicativo que você gosta, se ele é um aplicativo da Microsoft ou não. Administradores podem delegar permissão tooadd B2B usuários toonon administradores. Não-administradores podem usar o hello [painel de acesso do aplicativo do Azure AD](https://myapps.microsoft.com) tooadd B2B colaboração tooapplications de usuários ou grupos.

![painel de acesso](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![adicionar membro](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a>As políticas de autorização protegem o conteúdo corporativo

Políticas de acesso condicional, como autenticação multifator, podem ser aplicadas:
- No nível de locatário Olá
- No nível de aplicativo hello
- Para dados e aplicativos corporativos de tooprotect usuários específicos

![adicionar membro](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-tooeasily-build-applications-tooonboard"></a>Usar nossas APIs e aplicativos tooonboard de compilação tooeasily de código de exemplo
Traga seus parceiros externos na placa nas necessidades da organização do maneiras tooyour personalizado.

Usando Olá [convite de colaboração B2B APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), você pode personalizar suas experiências de integração, incluindo a criação de portais de inscrição de autoatendimento. Nós fornecemos o código de exemplo para o portal de autoatendimento [no Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

![portal de inscrição](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

Com a colaboração B2B do Azure AD, você pode obter toda a capacidade do AD do Azure tooprotect Olá seus relacionamentos com parceiros de forma que os usuários finais localizar fácil e intuitivo. Então vá em frente, Olá junção milhares de organizações que já estiver usando o Azure AD B2B para sua colaboração externa!

## <a name="next-steps"></a>Próximas etapas

* Experiências de administrador são encontradas em Olá [portal do Azure](https://portal.azure.com).

* Experiências de trabalhador de informações estão disponíveis no hello [painel de acesso](https://myapps.microsoft.com).

* E, como sempre, conecte-se com a equipe de produto Olá para quaisquer comentários, discussões e sugestões por meio de nosso [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?](active-directory-b2b-admin-add-users.md)
* [Como os operadores de informação adicionam usuários de colaboração B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saudação do hello email de convite de colaboração B2B](active-directory-b2b-invitation-email.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento da colaboração B2B do Azure AD](active-directory-b2b-licensing.md)
* [Solução de problemas de colaboração B2B do Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Perguntas frequentes sobre a colaboração B2B do Azure Active Directory](active-directory-b2b-faq.md)
* [API e personalização da colaboração B2B do Azure Active Directory](active-directory-b2b-api.md)
* [Autenticação multifator para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar usuários de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Auditoria e relatórios de um usuário de colaboração B2B](active-directory-b2b-auditing-and-reporting.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
