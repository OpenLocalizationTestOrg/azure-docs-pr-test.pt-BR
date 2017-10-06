---
title: "experiências de aaaSign com o Azure AD Identity Protection | Microsoft Docs"
description: "Fornece uma visão geral da experiência do usuário hello quando Identity Protection tem atenuados ou corrigida, um usuário ou quando a autenticação multifator é necessária por uma política."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>Experiências de entrada com a proteção de identidade do Azure AD
Com o Azure Active Directory Identity Protection, é possível:

* Exigir usuários tooregister para autenticação multifator
* lidar com entradas arriscadas e usuários comprometidos

resposta de Olá Olá toothese dos problemas do sistema tem um impacto na experiência de logon do usuário, porque apenas diretamente entrando fornecendo um nome de usuário e uma senha não será possível mais. Etapas adicionais serão necessária tooget um usuário de volta com segurança aos negócios.

Este tópico fornece uma visão geral da experiência de entrada de um usuário em relação a todos os casos que podem ocorrer.

**Autenticação multifator**

* Registro de autenticação multifator

**Entrada em risco**

* Recuperação de entrada arriscada
* Entrada arriscada bloqueada
* Registro da autenticação multifator durante a entrada arriscada

**Usuário em risco**

* Recuperação de conta comprometida
* Conta comprometida bloqueada

## <a name="multi-factor-authentication-registration"></a>Registro de autenticação multifator
Olá melhor experiência de usuário para ambos, Olá fluxo de recuperação de conta comprometida e Olá arriscado fluxo de entrada, é quando o usuário Olá pode recuperar automaticamente. Se os usuários são registrados para autenticação multifator, eles já tem um número de telefone associado à conta que pode ser usado toopass desafios de segurança. Nenhum envolvimento de Ajuda do suporte técnico ou administrador é necessário toorecover contra o comprometimento de conta. Assim, é altamente recomendável tooget aos usuários registrados para autenticação multifator. 

Os administradores podem:

* Defina uma política que exige que usuários tooset suas contas de verificação de segurança adicional. 
* Permitir ignorar o registro de autenticação multifator para backup too30 dias, no caso de desejarem toogive usuários antes de registrar um período de cortesia.

**registro de autenticação multifator Olá tem três etapas:**

1. Na primeira etapa de hello, usuário Olá recebe uma notificação sobre a conta de saudação do hello requisito tooset para autenticação multifator. 
   
    ![Correção](./media/active-directory-identityprotection-flows/140.png "Correção")
2. autenticação de multifator tooset backup, é necessário que o sistema de saudação do toolet Saiba como você deseja toobe contatado.
   
    ![Correção](./media/active-directory-identityprotection-flows/141.png "Correção")
3. sistema Olá envia um desafio tooyou e precisar toorespond.
   
    ![Correção](./media/active-directory-identityprotection-flows/142.png "Correção")

## <a name="risky-sign-in-recovery"></a>Recuperação de entrada arriscada
Quando um administrador tiver configurado uma política para entrar riscos, Olá afetado serão notificados quando eles tentam toosign-in. 

**fluxo de entrada arriscados Olá tem duas etapas:** 

1. usuário de saudação é informado de que algo incomum foi detectado sobre sua entrada no sistema, como fazendo logon em um novo local, dispositivo ou aplicativo. 
   
    ![Correção](./media/active-directory-identityprotection-flows/120.png "Correção")
2. usuário Olá é necessário tooprove sua identidade, resolvendo um desafio de segurança. Se o usuário hello está registrado para autenticação multifator precisam tooround-viagem e um número de telefone de tootheir de código de segurança. Como esta é apenas uma entrada arriscada e não uma conta comprometida, usuário Olá não tenha senha de saudação toochange neste fluxo. 
   
    ![Correção](./media/active-directory-identityprotection-flows/121.png "Correção")

## <a name="risky-sign-in-blocked"></a>Entrada arriscada bloqueada
Os administradores também podem optar tooset entrar risco política tooblock aos usuários após entrar dependendo do nível de risco de saudação. tooget desbloqueado, os usuários finais devem entrar em contato com um administrador ou suporte técnico ou tente entrando de um dispositivo ou local familiar. Não é possível recuperar-se sozinho com uma solução de autenticação multifator neste caso.

![Correção](./media/active-directory-identityprotection-flows/200.png "Correção")

## <a name="compromised-account-recovery"></a>Recuperação de conta comprometida
Quando uma política de segurança de risco do usuário tiver sido configurada, os usuários que atendem usuário Olá corre o risco de nível especificado na política de saudação (e, portanto, serão considerados comprometidos) deve passar pelo fluxo de recuperação de comprometimento de usuário Olá antes que eles podem entrar. 

**fluxo de recuperação de comprometimento de usuário Olá tem três etapas:**

1. usuário de saudação é informado de que a segurança da conta está em risco devido a atividades suspeitas ou vazadas credenciais.
   
    ![Correção](./media/active-directory-identityprotection-flows/101.png "Correção")
2. usuário Olá é necessário tooprove sua identidade, resolvendo um desafio de segurança. Se o usuário hello está registrado para autenticação multifator, eles podem recuperar automaticamente sejam comprometidos. Será necessário tooround-viagem e um número de telefone de tootheir de código de segurança. 
   
   ![Correção](./media/active-directory-identityprotection-flows/110.png "Correção")
3. Olá, finalmente, o usuário é forçado toochange sua senha porque outra pessoa pode ter tido acesso tootheir conta. 
   Veja as capturas de tela desta experiência abaixo.
   
   ![Correção](./media/active-directory-identityprotection-flows/111.png "Correção")

## <a name="compromised-account-blocked"></a>Conta comprometida bloqueada
tooget um usuário que foi bloqueado por uma política de segurança do usuário risco desbloqueada, o usuário Olá deve contatar um administrador ou o suporte técnico. Não é possível recuperar-se sozinho com uma solução de autenticação multifator neste caso.

![Correção](./media/active-directory-identityprotection-flows/104.png "Correção")

## <a name="reset-password"></a>Redefinir senha
Caso os usuários comprometidos sejam impedidos de entrar, um administrador poderá gerar uma senha temporária para eles. Olá usuários terão toochange sua senha durante uma próxima vez que entrar.

![Correção](./media/active-directory-identityprotection-flows/160.png "Correção")

## <a name="see-also"></a>Consulte também
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md) 

