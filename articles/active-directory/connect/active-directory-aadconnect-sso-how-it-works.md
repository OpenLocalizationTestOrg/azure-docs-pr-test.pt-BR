---
title: "Azure AD Connect: Logon Único Contínuo – como ele funciona | Microsoft Docs"
description: "Este artigo descreve como funciona hello Azure Active Directory perfeita logon único no recurso."
services: active-directory
keywords: "o que é o Azure AD Connect, instalar o Active Directory, componentes necessários do Azure AD, SSO, Logon Único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Logon Único Contínuo do Azure Active Directory: aprofundamento técnico

Este artigo fornece detalhes técnicos em como funciona o recurso de saudação do Azure Active Directory perfeita-logon único (SSO contínuo).

>[!IMPORTANT]
>recurso de SSO contínuo Hello está atualmente em visualização.

## <a name="how-does-seamless-sso-work"></a>Como o SSO contínuo funciona?

Esta seção tem tooit de duas partes:
1. instalação de saudação do recurso de SSO contínuo hello.
2. Como uma transação única de entrada de usuário funciona com o SSO Contínuo.

### <a name="how-does-set-up-work"></a>Como funciona a configuração?

O SSO Contínuo é habilitado por meio do Azure AD Connect, conforme mostrado [aqui](active-directory-aadconnect-sso-quick-start.md). Ao habilitar o recurso de hello, Olá etapas a seguir ocorre:
- Uma conta de computador denominada `AZUREADSSOACCT` (que representa o Azure AD) é criada em seu AD (Active Directory) local.
- chave de descriptografia do Kerberos da conta do computador Olá é compartilhado com segurança com o Azure AD.
- Além disso, dois Kerberos nomes principais de serviço (SPNs) são criados toorepresent duas URLs são usadas durante a entrada do AD do Azure.

>[!NOTE]
> conta de computador Hello e SPNs do Kerberos Olá são criados em cada floresta do AD sincronizar tooAzure AD (usando o Azure AD Connect) e cujos usuários você deseja SSO contínuo. Mover Olá `AZUREADSSOACCT` tooan de conta de computador UO (unidade organizacional) em que outras contas de computador são armazenado tooensure que ele é gerenciado no hello mesmo maneira e não será excluído.

>[!IMPORTANT]
>É altamente recomendável que você [sobrepor a chave de descriptografia de Kerberos Olá](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) de saudação `AZUREADSSOACCT` conta de computador pelo menos a cada 30 dias.

### <a name="how-does-sign-in-with-seamless-sso-work"></a>Como a entrada com o SSO Contínuo funciona?

Após a conclusão da instalação hello, SSO contínuo funciona Olá mesma maneira como qualquer outra entrada que usa autenticação do Windows integrada (IWA). fluxo de saudação é o seguinte:

1. usuário de saudação tenta tooaccess um aplicativo (por exemplo, Olá Outlook Web App - https://outlook.office365.com/owa/) de um dispositivo corporativo domínio dentro da rede corporativa.
2. Se o usuário Olá não tiver entrado, usuário Olá é redirecionado toohello AD do Azure-página de entrada.

  >[!NOTE]
  >Se a solicitação de entrada hello AD do Azure inclui um `domain_hint` (identifica o locatário - por exemplo, contoso.onmicrosoft.com) ou `login_hint` (identificação de usuário Olá - por exemplo, user@contoso.onmicrosoft.com ou user@contoso.com) parâmetro e, em seguida, etapa 2 é ignorada.

3. tipos de usuário Olá em seu nome de usuário na página de entrada hello AD do Azure.
4. Usando JavaScript no plano de fundo hello, o AD do Azure desafios navegador hello, por meio de uma resposta 401 não autorizado, tooprovide um tíquete Kerberos.
5. navegador Hello, por sua vez, solicita um tíquete do Active Directory para Olá `AZUREADSSOACCT` conta de computador (que representa o AD do Azure).
6. Active Directory localiza a conta de computador hello e retorna um navegador de toohello de tíquete Kerberos criptografado com o segredo da conta de computador hello.
7. navegador de saudação encaminha o tíquete do Kerberos Olá adquiriu a tooAzure do Active Directory AD (em uma saudação [URLs do AD do Azure adicionados anteriormente as configurações de zona de Intranet do navegador toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).
8. Azure AD descriptografa Olá tíquete Kerberos, que inclui a identidade de saudação do usuário Olá conectado ao dispositivo corporativo hello, usar Olá anteriormente chave compartilhada.
9. Após a avaliação, AD do Azure retorna um aplicativo de token toohello back ou solicita Olá usuário tooperform provas adicionais, como autenticação multifator.
10. Se Olá usuário entrar for bem-sucedida, o usuário de saudação é tooaccess capaz de aplicativo de hello.

Olá diagrama a seguir ilustra todos os componentes de saudação e etapas de saudação envolvidos.

![Logon Único Contínuo](./media/active-directory-aadconnect-sso/sso2.png)

SSO contínuo é oportunista, o que significa que se ele falhar, a experiência de entrada hello reverterá ser tooits comportamento normal - ou seja, Olá usuário precisa tooenter toosign sua senha no.

## <a name="next-steps"></a>Próximas etapas

- [**Início Rápido** ](active-directory-aadconnect-sso-quick-start.md) – colocar o SSO Contínuo do Azure AD em funcionamento.
- [**Perguntas frequentes sobre** ](active-directory-aadconnect-sso-faq.md) -respostas toofrequently perguntas frequentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Saiba como tooresolve comum problemas com o recurso de saudação.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
