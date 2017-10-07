---
title: "aaaTroubleshooting colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "Correções para problemas comuns com a colaboração B2B do Azure Active Directory"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Solução de problemas de colaboração B2B do Azure Active Directory

Confira aqui algumas correções para problemas comuns da colaboração B2B do Azure Active Directory (Azure AD).


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>Adicionar um usuário externo, mas não vê-los no meu Catálogo de endereços Global ou no seletor de pessoas Olá

Em casos em que os usuários externos não são preenchidos na lista hello, objeto Olá pode levar tooreplicate de alguns minutos.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>Um usuário convidado de B2B não está aparecendo no seletor de pessoas do SharePoint Online/OneDrive 
 
Olá toosearch de capacidade para os usuários existentes de convidado no seletor de pessoas saudação do SharePoint Online (SPO) é desativado por comportamento herdado de toomatch padrão.

Você pode habilitar esse recurso usando Olá a definição 'ShowPeoplePickerSuggestionsForGuestUsers' na coleção de locatário e site Olá nível. Você pode definir o recurso de saudação usando Olá conjunto SPOTenant e SPOSite do conjunto de cmdlets, que permitem aos membros toosearch todos os usuários convidados existentes no diretório de saudação. Alterações no escopo de locatário Olá não afetam a sites SPO já provisionados.

## <a name="invitations-have-been-disabled-for-directory"></a>Os convites foram desabilitados para o diretório

Se você será notificado de que você não tem permissões tooinvite os usuários, verifique se sua conta de usuário está autorizado tooinvite a usuários externos em configurações de usuário:

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

Se você modificou essas configurações ou Olá emissor do convite convidado função tooa usuário atribuído recentemente, pode haver um atraso de 15 a 60 minutos antes de saudação alterações entrem em vigor.

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>usuário Hello, convidado está recebendo um erro durante o resgate

Os erros comuns incluem:

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>O Admin do convidado não permite a criação de Usuários Verificados por Email em seu locatário

Quando convidar usuários cuja organização está usando o Active Directory do Azure, mas Olá onde a conta de usuário específica não existe (por exemplo, Olá usuário não existe no AD do Azure contoso.com). administrador de saudação de contoso.com pode ter uma política em vigor para impedir que usuários que está sendo criado. usuário Olá deve verificar com toodetermine seu administrador se os usuários externos são permitidos. Olá administrador do usuário externo pode ser necessário tooallow usuários de Email é verificado em seu domínio (consulte este [artigo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) em permitir que os usuários verificado de Email).

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>O usuário externo ainda não existe em um domínio federado

Se você estiver usando a autenticação de Federação e usuário Olá ainda não existir no Active Directory do Azure, o usuário Olá não pode ser convidado.

tooresolve esse problema, Olá administrador de usuário externo deve sincronizar tooAzure de conta do usuário de saudação do Active Directory.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>Como ‘\#’, que normalmente não é um caractere válido, é sincronizado com o Azure AD?

"\#" é um caractere reservado no UPNs para colaboração B2B do Azure AD ou usuários externos, porque a conta de convidado Olá user@contoso.com se torna user_contoso.com#EXT@fabrikam.onmicrosoft.com. Portanto, \# em UPNs provenientes de locais não são permitidas toosign em toohello portal do Azure. 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>Recebo um erro ao adicionar usuários externos tooa sincronizados grupo

Os usuários externos podem ser adicionados somente muito "atribuído" ou grupos de "Segurança" e não toogroups que são dominados local.

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>Meu usuário externo não recebeu um email tooredeem

Verifique com seu ISP convidado Hello ou tooensure de filtro de spam Olá endereço a seguir é permitido:Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>Observem que essa mensagem de saudação personalizada não obtém incluída com mensagens de convite às vezes

toocomply com as leis de privacidade, nossas APIs não incluem mensagens personalizadas no convite por email hello quando:

- emissor do convite Olá não tem um endereço de email no hello convidar locatário
- Quando uma entidade de serviço de aplicativo envia o convite Olá

Se esse cenário é importante tooyou, suprimir nosso email de convite de API e enviá-lo por meio do mecanismo de email de saudação de sua escolha. Consulte toomake de departamento jurídico da sua organização se nenhum email que enviar dessa forma também está em conformidade com as leis de privacidade.

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?](active-directory-b2b-admin-add-users.md)
* [Como os operadores de informação adicionam usuários de colaboração B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saudação do hello email de convite de colaboração B2B](active-directory-b2b-invitation-email.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento da colaboração B2B do Azure AD](active-directory-b2b-licensing.md)
* [Perguntas frequentes sobre a colaboração B2B do Azure Active Directory](active-directory-b2b-faq.md)
* [API e personalização da colaboração B2B do Azure Active Directory](active-directory-b2b-api.md)
* [Autenticação multifator para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar usuários de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
