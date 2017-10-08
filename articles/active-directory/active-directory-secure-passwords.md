---
title: "aaaAzure AD em camadas de segurança de senha | Microsoft Docs"
description: "Explica como o Azure AD impõe senhas fortes e protege as senhas dos usuários contra os cibercriminosos."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>Uma abordagem várias camadas de segurança de senha de tooAzure AD

Este artigo discute algumas práticas recomendadas que você pode seguir como um usuário ou como um administrador tooprotect seu Azure Active Directory (AD do Azure) ou Account da Microsoft.

 > [!NOTE]
 > Administradores do AD do Azure podem redefinir senhas de usuário usando diretrizes Olá Olá artigo [Olá redefinição da senha de um usuário no Active Directory do Azure](active-directory-users-reset-password-azure-portal.md).
 >
 > Os usuários podem redefinir suas próprias senhas usando diretrizes Olá Olá artigo [ajuda esqueci minha senha do AD do Azure](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Requisitos de senha

O AD do Azure incorpora Olá senhas comuns de toosecuring abordagens a seguir:

* Requisitos de comprimento de senha
* Requisitos de complexidade de senha
* Expiração de senha regular e periódica

Para obter informações sobre a redefinição de senha no Active Directory do Azure, consulte o tópico de saudação [senha de autoatendimento do AD do Azure Redefinir para Olá profissionais de TI](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Proteções de senha do Azure AD

O AD do Azure e Olá usar o sistema de conta Microsoft comprovados abordagens tooensure segura proteção de senhas de usuário e administrador incluindo:

* Senhas banidas dinamicamente
* Bloqueio de Senha Inteligente

Para obter informações sobre o gerenciamento de senha com base na pesquisa atual, consulte o white paper de saudação [diretrizes de senha](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Senhas banidas dinamicamente

As Contas da Microsoft e do Azure AD garantem a proteção por senha banindo dinamicamente as senhas comumente usadas. equipe de proteção de identidade do Azure ID Olá analisa rotineiramente senha banido listas, impedindo que os usuários selecionem as senhas usadas. Este serviço está disponível tooAzure AD e os clientes do serviço de conta Microsoft hello.

Durante a criação de senhas, é importante para os administradores tooencourage usuários toochoose senha frases que incluem uma combinação exclusiva de letras, números, caracteres ou palavras. Essa abordagem ajuda toomake toobe praticamente impossível comprometido mas mais fácil para os usuários tooremember as senhas de usuário.

#### <a name="password-breaches"></a>Violações de senha

Sempre, a Microsoft está trabalhando toostay um passo à frente de criminosos.

equipe do Azure AD Identity Protection Olá continuamente analisa as senhas que são normalmente usadas. Criminosos também usam semelhante tooinform de estratégias seus ataques, como criando um [tabela arco-íris](https://en.wikipedia.org/wiki/Rainbow_table) de violação de hashes de senha.

A Microsoft continuamente analisa [violações de dados](https://www.privacyrights.org/data-breaches) toomaintain uma lista de senha banido dinamicamente atualizada, o que garante que as senhas vulneráveis são proibidas antes de se tornarem um real de ameaças tooAzure AD clientes. Para obter mais informações sobre nossos esforços de segurança atual, consulte Olá [relatório de inteligência de segurança do Microsoft](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Bloqueio de Senha Inteligente

Quando o AD do Azure detecta um potencial toohack de tentar criminoso virtuais em uma senha de usuário, podemos bloquear a conta de usuário de Olá com bloqueio de senha inteligente. O AD do Azure é projetado risco de saudação toodetermine associado a sessões de logon específico. Em seguida, usando dados de segurança mais recentes de saudação, aplicamos bloqueio semântica toostop ameaças.

Se um usuário estiver bloqueado do AD do Azure, sua tela parece semelhante toohello que segue:

  ![Bloqueado no Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

Para outras contas da Microsoft, sua tela parece semelhante toohello que segue:

  ![Bloqueado em uma conta da Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Para obter informações sobre a redefinição de senha no Active Directory do Azure, consulte o tópico de saudação [senha de autoatendimento do AD do Azure Redefinir para Olá profissionais de TI](active-directory-passwords.md).

  >[!NOTE]
  >Se você for um administrador do AD do Azure, talvez você queira toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid com os usuários crie senhas tradicionais completamente.
  >

## <a name="next-steps"></a>Próximas etapas

* [Como tooupdate sua própria senha](active-directory-passwords-update-your-own-password.md)
* [conceitos básicos de saudação do gerenciamento de identidades do Azure](fundamentals-identity.md)
* [Relatório de atividade de registro de redefinição de senha](active-directory-passwords-reporting.md)


