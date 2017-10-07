---
title: "autenticação de multifator toorequire aaaHow | Microsoft Docs"
description: "Saiba como toorequire multi-factor authentication (MFA) com privilégios identidades com a extensão do Azure Active Directory Privileged Identity Management hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>Como toorequire MFA no Azure AD Privileged Identity Management
Recomendamos que você exija o MFA (Multi-Factor Authentication) para todos os administradores. Isso reduz o risco de saudação de um ataque de vencimento de senha tooa comprometida.

Você pode exigir que os usuários concluam um desafio de MFA quando entrarem. Olá postagem de blog [MFA para Office 365 e MFA para o Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) compara o que está incluído nas assinaturas do Office e do Azure, com recursos de saudação contidos na oferta do Microsoft Azure multi-Factor Authentication hello.

Você também pode exigir que os usuários concluam um desafio de MFA quando ativarem uma função no Azure AD PIM. Dessa forma, se usuário Olá não concluir um desafio MFA quando eles se conectou, eles poderão ser solicitada toodo caso por PIM.

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>Solicitação de MFA no Privileged Identity Management do Azure AD
Ao gerenciar identidades no PIM como um administrador de função com privilégios, você poderá ver os alertas que recomendam o MFA para contas com privilégios. Clique em segurança Olá alerta no painel PIM hello e uma nova folha será aberta com uma lista de contas de administrador de saudação que requer MFA.  É possível exigir MFA selecionando várias funções e, em seguida, clicando em Olá **corrigir** botão, ou você pode clique em Olá reticências próximo tooindividual funções e clique em Olá **corrigir** botão.

> [!IMPORTANT]
> Neste momento, o Azure MFA só funciona com o trabalho ou escolares, não contas da Microsoft (geralmente uma conta pessoal que usou toosign nos serviços de tooMicrosoft Skype, Xbox, Outlook.com, etc.). Por isso, qualquer pessoa que usar uma conta da Microsoft não pode ser um administrador qualificado porque eles não podem usar a MFA tooactivate suas funções. Se esses usuários precisam ter toocontinue gerenciar cargas de trabalho usando uma conta da Microsoft, elevá-las toopermanent administradores por enquanto.
> 
> 

Além disso, você pode alterar o requisito de MFA de saudação para uma função específica clicando no hello seção funções do painel do PIM hello. Em seguida, clique em **configurações** na folha de função hello e, em seguida, selecionando **habilitar** em autenticação multifator.

## <a name="how-azure-ad-pim-validates-mfa"></a>Como o PIM do Azure AD valida a MFA
Há duas opções de validação de MFA quando um usuário ativa uma função.

Olá a opção mais simples é toorely no Azure MFA para usuários que estiver ativando uma função com privilégios. toodo isso, primeiro verifique se os usuários licenciados, se necessário e tem registrado para o Azure MFA. Para obter mais informações sobre como toodo está em [guia de Introdução ao Azure multi-Factor Authentication na nuvem Olá](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md). Ele é recomendado, mas não obrigatório, que você configure tooenforce MFA do AD do Azure para esses usuários quando eles entrarem. Isso ocorre porque a verificações MFA de saudação serão feitas pelo Azure AD PIM em si.

Alternativamente, se os usuários se autenticarem localmente, você poderá fazer com que o provedor de identidade seja responsável pelo MFA. Por exemplo, se você configurou a autenticação de cartão inteligente com base em toorequire dos serviços de Federação do AD antes de acessar o AD do Azure, [protegendo recursos de nuvem com autenticação multifator do Azure e o AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) inclui instruções Para configurar o AD FS toosend declarações tooAzure AD. Quando um usuário tenta tooactivate uma função, o Azure AD PIM aceitará que MFA já foi validado para usuário Olá depois de receber declarações adequadas hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

