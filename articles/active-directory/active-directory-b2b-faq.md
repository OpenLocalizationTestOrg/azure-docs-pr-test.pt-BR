---
title: "aaaAzure colaboração B2B do Active Directory perguntas frequentes | Microsoft Docs"
description: "Obtenha respostas toofrequently perguntas frequentes sobre a colaboração B2B do Azure Active Directory."
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Perguntas frequentes sobre a colaboração B2B do Azure Active Directory

As perguntas frequentes (FAQs) sobre a colaboração do Azure Active Directory (AD do Azure) para empresas (B2B) são atualizados periodicamente tooinclude novos tópicos.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>Colaboração B2B do Azure AD está disponível no portal clássico do Azure de Olá?
Não. Recursos de colaboração B2B do AD do Azure estão disponíveis apenas em Olá [portal do Azure](https://portal.azure.com) e em Olá [painel de acesso](https://myapps.microsoft.com/). 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>Podemos personalizar nossa página de conexão para que ela seja mais intuitiva para nossos usuários convidados de colaboração B2B?
Claro que não! Consulte nossa [postagem de blog sobre esse recurso](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/). Para obter mais informações sobre como toocustomize da sua organização entrar página, consulte [adicionar identidade visual de páginas de painel de acesso e toosign em](active-directory-add-company-branding.md).

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>Os usuários de colaboração B2B podem acessar o SharePoint Online e o OneDrive?
Sim. No entanto, é Olá toosearch de capacidade para os usuários existentes convidado no SharePoint Online usando o seletor de pessoas Olá **Off** por padrão. tooturn em Olá opção toosearch para os usuários de convidado, defina **ShowPeoplePickerSuggestionsForGuestUsers** muito**em**. Você pode ativar essa configuração no nível de locatário de saudação ou no nível de coleção de sites hello. Você pode alterar essa configuração usando os cmdlets de conjunto SPOTenant e Set-SPOSite hello. Com esses cmdlets, membros podem pesquisar todos os usuários convidados existentes no diretório de saudação. Alterações no escopo de locatário de saudação não afetam os sites do SharePoint Online já foi provisionados.

### <a name="is-hello-csv-upload-feature-still-supported"></a>É hello CSV carregar o recurso ainda tem suporte?
Sim. Para obter mais informações sobre como usar o recurso de carregamento de arquivo hello. csv, consulte [esse exemplo do PowerShell](active-directory-b2b-code-samples.md).

### <a name="how-can-i-customize-my-invitation-emails"></a>Como posso personalizar meus emails de convite?
Você pode personalizar quase tudo sobre o processo de emissor do convite hello usando Olá [B2B convite APIs](active-directory-b2b-api.md).

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>Um usuário externo convidado pode deixar a organização Olá depois que estão sendo convidados?
administrador da organização convidar Olá pode excluir um usuário de convidado de colaboração B2B do seu diretório, mas o usuário convidado de saudação não pode deixar Olá convidar o diretório da organização por si mesmos. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>Os usuários convidados podem redefinir seu método de autenticação multifator?
Sim. Usuários convidados podem redefinir sua saudação do método de autenticação multifator mesmo modo que os usuários regulares.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>Qual organização é responsável pelas licenças de autenticação multifator?
organização convidar Olá executa a autenticação multifator. Olá convidar organização deve se certificar de que organização Olá tem licenças suficientes para os seus usuários B2B que estão usando a autenticação multifator.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>E se uma organização de parceiros já tiver a autenticação multifator configurada? Podemos confiar em sua autenticação multifator e não usar nossa própria autenticação multifator?
Este recurso está planejado para uma versão futura, e que, em seguida, você pode selecionar tooexclude de parceiros específicos de autenticação de multifatores (Olá convidar da sua organização).

### <a name="how-can-i-use-delayed-invitations"></a>Como fazer para usar convites atrasados?
Uma organização pode desejar que os usuários de colaboração tooadd B2B, provisioná-los tooapplications conforme necessário e, em seguida, enviar convites. Você pode usar o hello B2B colaboração convite API toocustomize Olá integração fluxo de trabalho.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>Posso tornar um usuário convidado um administrador limitado?
Com certeza. Para obter mais informações, consulte [a função adicionando convidado usuários tooa](active-directory-users-assign-role-azure-portal.md).

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Colaboração B2B do Azure AD permite B2B usuários tooaccess Olá portal do Azure?
A menos que um usuário está atribuído saudação do administrador global ou limitado, os usuários de colaboração B2B não exigem acesso toohello portal do Azure. No entanto, os usuários de colaboração do B2B atribuídos Olá função de administrador global ou limitado podem acessar o portal de saudação. Além disso, se um usuário convidado não é atribuído a uma dessas funções de administrador acessa o portal de Olá, Olá usuário pode ser capaz de tooaccess determinadas partes do hello experiência. função de usuário convidado Olá tem algumas permissões no diretório de saudação.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>Pode bloquear o acesso toohello portal do Azure para usuários convidados?
Sim! Quando você configurar essa política, ser tooavoid cuidado acidentalmente o bloqueio de acesso toomembers e administradores.
tooblock um usuário convidado acessar toohello [portal do Azure](https://portal.azure.com), usar uma política de acesso condicional no hello API do modelo de implantação clássico do Windows Azure:
1. Modificar Olá **todos os usuários** para que ele contenha somente os membros de grupo.
  ![modificar a captura de tela de grupo Olá](media/active-directory-b2b-faq/modify-all-users-group.png)
2. Crie um grupo dinâmico que contém usuários convidados.
  ![captura de tela de Criar grupo](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Configure um acesso condicional política tooblock convidado acesso de usuários portal hello, conforme mostrado na seguinte Olá vídeo:
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>A colaboração do Azure AD B2B dá suporte à autenticação multifator e a contas de email do consumidor?
Sim. Há suporte para a autenticação multifator e a contas de email do consumidor na colaboração do Azure AD B2B.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>Você planeja toosupport redefinição de senha para usuários de colaboração B2B do Azure AD?
Sim. Aqui estão os detalhes importantes de saudação para redefinição de senha de autoatendimento (SSPR) para um usuário de B2B que é convidado de uma organização de parceiro:
 
* SSPR ocorre apenas no locatário de identidade de saudação do usuário de B2B hello.
* Se o locatário de identidade Olá é uma conta da Microsoft, Olá mecanismo SSPR conta da Microsoft é usado.
* Se o locatário de identidade Olá é um just-in-time (JIT) ou de locatário "viral", um email de redefinição de senha será enviado.
* Para outros locatários, o processo de SSPR padrão Olá é seguido para usuários de B2B. Como o membro SSPR para usuários de B2B, no contexto de saudação do recurso hello, aluguel está bloqueada. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>A redefinição de senha está disponível para usuários convidados em um locatário just-in-time (JIT) ou "viral" que aceitaram convites com um endereço de email corporativo ou de estudante, mas que não tinham uma conta existente do Azure AD?
Sim. Um email de redefinição de senha pode ser enviado que permite que um usuário tooreset sua senha no aluguel JIT hello.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>O Microsoft Dynamics CRM fornece suporte online para a colaboração do Azure AD B2B?
Atualmente, o Microsoft Dynamics CRM não fornece suporte online para a colaboração do Azure AD B2B. No entanto, estamos planejando toosupport isso em Olá futuras.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>O que é o tempo de vida de saudação de uma senha inicial para um usuário de colaboração B2B recém-criado?
O AD do Azure tem um conjunto fixo de caracteres, força da senha e requisitos de bloqueio de conta que se aplicam igualmente tooall contas de usuário de nuvem de AD do Azure. As contas de usuário de nuvem são contas que não estão federadas com outro provedor de identidade, como 
* Conta da Microsoft
* Facebook
* Serviços de Federação do Active Directory (AD FS)
* Outro locatário de nuvem (para colaboração B2B)

Para contas federadas, política de senha depende da política Olá aplicado nas configurações da conta Microsoft hello local aluguel e saudação do usuário.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Uma organização pode achar toohave diferente experiências em seus aplicativos para usuários de locatário e usuários convidados. Existem diretrizes padrão para isso? É a presença de saudação do hello identidade provedor declaração Olá modelo correto toouse?
 Um usuário convidado pode usar qualquer tooauthenticate do provedor de identidade. Para obter mais informações, consulte [Propriedades de um usuário de colaboração B2B](active-directory-b2b-user-properties.md). Saudação de uso **UserType** experiência do usuário de toodetermine de propriedade. Olá **UserType** declaração atualmente não está incluída no token de saudação. Aplicativos devem usar o diretório de Olá Olá Graph API tooquery para usuário hello e tooget Olá UserType.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>Onde posso encontrar um tooshare de comunidade de colaboração B2B soluções e toosubmit ideias?
Estamos constantemente ouvindo tooyour comentários, tooimprove colaboração B2B. Convida você tooshare seu usuário cenários, as práticas recomendadas e o que você gosta de colaboração B2B do Azure AD. Participar de discussões Olá Olá [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).
 
Também convida você toosubmit suas ideias e vote recursos futuros [ideias de colaboração B2B](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>Podemos enviar um convite é resgatado automaticamente, para que Olá usuário é apenas "pronto toogo"? Ou usuário Olá sempre tooclick por meio de URL de resgate toohello?
Convites são enviados por um usuário em Olá convidar organização que também seja um membro da organização do parceiro de saudação não exigem resgate por usuário do hello B2B.

É recomendável que você convidar um usuário de Olá parceiro organização toojoin Olá convidar organização. [Adicione essa função de emissor do convite de convidado de toohello de usuário na organização do recurso Olá](active-directory-b2b-add-guest-to-role.md). Este usuário pode convidar outros usuários na organização do parceiro de saudação usando Olá entrar UI, scripts do PowerShell, ou APIs. Em seguida, usuários de colaboração B2B da organização não é necessária tooredeem seus convites.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>Como funciona colaboração B2B ao parceiro Olá convidado está usando a federação tooadd sua própria autenticação local?
Se o parceiro de saudação tem um locatário do AD do Azure é federado toohello infraestrutura de autenticação local, no local-logon único (SSO) é feito automaticamente. Se o parceiro de saudação não tiver um locatário do AD do Azure, uma conta do AD do Azure é criada para novos usuários. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>Achei que o Azure AD B2B não aceitava endereços de email gmail.com e outlook.com nem que o B2C fosse usado para esses tipos de contas.
Estamos removendo Olá diferenças B2B e colaboração do negócio para a empresa (B2C) em termos de quais identidades têm suporte. identidade de saudação usada não é toochoose uma boa razão entre usando B2B ou B2C. Para obter informações sobre como escolher sua opção de colaboração, consulte [Comparação da colaboração B2B e B2C no Azure Active Directory](active-directory-b2b-compare-b2c.md).

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>Quais aplicativos e serviços fornecem suporte aos usuários convidados B2B do Azure?
Todos os aplicativos integrados ao Azure AD dão suporte a usuários convidados do B2B do Azure. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>Podemos forçar a autenticação multifator para usuários convidados B2B se os parceiros não têm a autenticação multifator?
Sim. Para obter mais informações, consulte [Acesso condicional para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md).

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>No SharePoint, é possível definir uma lista de “permissões” ou “negações” para usuários externos. Podemos fazer isso no Azure?
Sim. A colaboração do Azure AD B2B dá suporte a listas de permissões e negações. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>O que fazem licenças precisamos toouse B2B do Azure AD?
Para obter informações sobre as licenças que sua organização precisa toouse B2B do Azure AD, consulte [colaboração B2B do Azure Active Directory licenciamento orientação](active-directory-b2b-licensing.md).

### <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como os administradores do Azure AD adicionam usuários de colaboração B2B?](active-directory-b2b-admin-add-users.md)
* [Como os operadores de informação adicionam usuários de colaboração B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saudação do hello email de convite de colaboração B2B](active-directory-b2b-invitation-email.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento da colaboração B2B do Azure AD](active-directory-b2b-licensing.md)
* [Solução de problemas da colaboração do Azure AD B2B](active-directory-b2b-troubleshooting.md)
* [API e personalização da colaboração do Azure AD B2B](active-directory-b2b-api.md)
* [Autenticação multifator para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar usuários de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de artigos sobre gerenciamento de aplicativos no Azure AD](active-directory-apps-index.md)
