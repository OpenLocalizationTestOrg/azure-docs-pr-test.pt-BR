---
title: aaaHow Azure assinaturas associadas com o Active Directory do Azure | Microsoft Docs
description: "Entrar no tooMicrosoft do Azure e problemas, como a relação de saudação entre uma assinatura do Azure e Active Directory do Azure relacionados."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Como as assinaturas do Azure são associadas ao Azure Active Directory
Este artigo aborda informações sobre Olá relação entre uma assinatura do Azure e o Azure Active Directory (AD do Azure) e como tooadd diretório tooyour AD do Azure assinatura existente.

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>TooAzure de relação da sua assinatura do Azure AD
Sua assinatura do Azure tem uma relação de confiança com o AD do Azure, o que significa que ele confia dispositivos, serviços e usuários de tooauthenticate directory hello. Várias assinaturas podem confiar Olá mesmo diretório, mas cada assinatura confia em apenas um diretório. 

relação de confiança de saudação que tem uma assinatura com um diretório é diferente de relacionamento Olá que ele tem com outros recursos no Azure (sites, bancos de dados e assim por diante). Se uma assinatura expirar, acessar toohello também para outros recursos associados à assinatura de saudação. Mas um diretório do AD do Azure permanece no Azure, e você pode gerenciar o diretório hello usando assinatura nova hello e associar uma assinatura diferente esse diretório.

![diagrama de como as assinaturas são associadas](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

Todos os usuários têm um único diretório inicial que os autentica, mas eles também podem ser convidados em outros diretórios. No AD do Azure, você pode ver os diretórios de saudação do qual sua conta de usuário é um membro ou convidado.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD e assinaturas do serviço de nuvem
O AD do Azure fornece identidade e diretório de núcleo Olá atrás da maioria dos serviços de nuvem da Microsoft, incluindo os recursos de gerenciamento:

* As tabelas
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Você obtém Olá livre de serviço do AD do Azure quando você se inscrever para qualquer um desses serviços de nuvem da Microsoft. Se você quiser tooadd um diretório de tooan AD do Azure de outra assinatura do Azure, você deve estar conectado com uma conta da Microsoft. Se você entrar tooAzure com um trabalho ou conta escola, você não pode adicionar um diretório existente do tooan de assinatura do Azure porque sua conta corporativa ou escolar não pode ser autenticada diretamente pelo Azure. 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>tooadd diretório tooyour AD do Azure assinatura existente
Você deve entrar com uma conta que existe em ambos os diretório atual Olá quais Olá inscrição está associada e no diretório Olá deseja tooadd-o para. 

1. Entrar toohello [Centro de contas Azure](https://account.windowsazure.com/Home/Index) com uma conta que é Olá administrador da conta de assinatura Olá cuja propriedade você deseja tootransfer.
2. Certifique-se de usuário Olá que você deseja o proprietário da assinatura Olá toobe está no diretório de saudação direcionada.
3. Clique em **Transferir assinatura**.
4. Especifique o destinatário hello. destinatário de saudação automaticamente recebe um email com um link de aceitação.
5. destinatário de saudação clica Olá link e segue as instruções hello, inclusive, inserir suas informações de pagamento. Quando o destinatário Olá for bem-sucedida, assinatura de saudação é transferida. 
6. diretório padrão de saudação de assinatura de saudação é alterado toohello diretório que o usuário hello está em.


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>Sugestões toomanage uma assinatura e um diretório
funções administrativas do Olá para uma assinatura do Azure gerenciam recursos vinculados toohello assinatura do Azure. Esta seção explica as diferenças de saudação entre os administradores de assinatura do Azure e administradores de diretório do AD do Azure. Funções administrativas e outras sugestões para usá-las toomanage sua assinatura estão descritas em [atribuindo funções de administrador no Azure Active Directory](active-directory-assign-admin-roles.md).

Por padrão, recebem a função de administrador de serviço de saudação de quando você se inscrever. Se outras pessoas precisam toosign no e acessar serviços usando Olá mesma assinatura, você pode adicioná-los como coadministradores. 

O AD do Azure tem um conjunto diferente de diretório de saudação toomanage funções administrativas e recursos relacionados à identidade. Por exemplo, administrador global de saudação de um diretório pode adicionar usuários e o diretório de toohello grupos ou exija a autenticação multifator para usuários. Função de administrador global toohello é atribuído a um usuário que cria um diretório e pode atribuir funções administrativas tooother usuários. Funções administrativas do AD do Azure também são usadas por outros serviços, como o Office 365 e Microsoft Intune. 

Mas o ponto importante aqui é que os administradores de assinatura do Azure e os administradores de diretório do Azure AD são duas funções separadas. 
* Administradores de assinatura do Azure podem gerenciar recursos no Azure e podem usar o AD do Azure no portal do Azure de saudação (porque Olá portal do Azure é um recurso do Azure). 
* Administradores de diretório podem gerenciar propriedades apenas no diretório do AD do Azure hello.

Uma pessoa pode desempenhar ambas as funções, mas isso não é obrigatório. Um administrador global do diretório não pode receber a atribuição de administrador de serviços ou coadministrador de uma assinatura do Azure, ou vice-versa. Sem ser um administrador de assinatura hello, usuário Olá pode entrar toohello portal do Azure, mas não pode gerenciar diretórios Olá para essa assinatura no portal de saudação. No entanto, esse usuário poderá gerenciar diretórios usando outras ferramentas, como o PowerShell do Azure AD ou hello Centro de administração do Office 365.

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre como os administradores de toochange para uma assinatura do Azure, consulte [transferir a propriedade de uma conta de tooanother de assinatura do Azure](../billing/billing-subscription-transfer.md)
* toolearn mais sobre como o acesso aos recursos é controlado no Microsoft Azure, consulte [Noções básicas sobre o acesso a recursos no Azure](active-directory-understanding-resource-access.md)
* Para obter mais informações sobre como as funções de tooassign no AD do Azure, consulte [atribuindo funções de administrador no Active Directory do Azure](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
