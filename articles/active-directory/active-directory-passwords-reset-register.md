---
title: 'Azure AD: registro SSPR | Microsoft Docs'
description: "Registrar dados de autenticação para redefinição de senha de autoatendimento do Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: dfcd0106616218c84d23920b124bed5b202cdd6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="register-for-self-service-password-reset"></a>Registro de redefinição de senha de autoatendimento

> [!IMPORTANT]
> **Você está aqui por que está enfrentando problemas para iniciar sessão?** Se sim, [veja aqui como alterar e redefinir sua senha](active-directory-passwords-update-your-own-password.md).

Como um usuário final, você pode redefinir sua senha ou desbloquear sua conta sem ter que toospeak tooa pessoa usando a redefinição de senha de autoatendimento (SSPR). Antes de usar essa funcionalidade, você tem métodos de autenticação tooregister ou confirme os métodos de autenticação Olá predefinido o administrador tenha populada.

## <a name="register-or-confirm-authentication-data-with-sspr"></a>Registrar ou confirmar dados de autenticação com SSPR

1. Navegador da web de Olá aberta no seu dispositivo e acesse toohello [página de registro de redefinição de senha](http://aka.ms/ssprsetup)
2. Insira seu nome de usuário e senha fornecidos pelo administrador
3. Dependendo de como sua equipe de TI tiver configurado as coisas, um ou mais dos seguintes Olá opções estão disponíveis para você tooconfigure e verificam. O administrador pode preencher algumas para você se eles tiverem suas informações de saudação toouse permissão.
    * Telefone comercial é apenas capaz de toobe definida pelo administrador
    * Telefone de autenticação deve ser definido como número de telefone tooanother teria acesso toolike um telefone celular que possa receber uma chamada ou texto.
    * Email de autenticação deve ser definido como endereço de email alternativo tooan que você pode acessar sem senha Olá precisar tooreset.
    * Perguntas de segurança fornece uma lista de perguntas que o administrador aprovou para você tooanswer. Você não pode usar o hello mesma pergunta ou responder mais de uma vez.
4. Forneça e verifique as informações de saudação exigidas por seu administrador. Se houver mais de uma opção, sugerimos que você registre a flexibilidade de tooprovide vários métodos quando outro método não está disponível (exemplo: tooaccess viajando e não é possível seu telefone comercial)

    ![Registre os métodos de autenticação e clique em Concluir][Register]

5. Quando concluir a etapa 4 escolha **concluir** e agora você será capaz de toouse autoatendimento redefinição de senha quando você precisar tooin Olá futuro.

Se você inserir dados em Email de autenticação ou Olá telefone de autenticação, não é visível no diretório global hello. Olá somente quem pode ver esses dados é você e seus administradores. Somente você pode ver Olá responde perguntas de segurança de tooyour.

Os administradores podem exigir você tooconfirm seus métodos de autenticação após um período de tempo toomake se que você ainda tem métodos apropriados de saudação registrados.

## <a name="common-problems-and-their-solutions"></a>problemas comuns e suas soluções

 Aqui estão alguns casos de erro comuns e suas soluções:

| Caso de erro| Que erro você vê?| Solução |
| --- | --- | --- |
| Uma página “Contate seu administrador” é exibida após a inserção da minha ID de usuário | Entre em contato com o seu administrador <br> <br> Detectamos que a senha da sua conta de usuário não é gerenciada pela Microsoft. Como resultado, estamos não é possível tooautomatically redefinir sua senha. <br> <br> Você precisa toocontact sua equipe de TI para obter mais assistência. | Você está vendo esta mensagem porque sua equipe de TI gerencia a sua senha em seu ambiente local e não permite que você tooreset a senha das não pode acessar o link de conta. <br> <br> tooreset sua senha, entre em contato com sua equipe de TI de sua equipe diretamente para Ajuda e permita-lhes saber deseja tooreset sua senha para que eles podem habilitar esse recurso para você.|
| Recebo uma mensagem de erro "sua conta não está habilitada para redefinição de senha" depois de inserir a ID de usuário | Sua conta não está habilitada para redefinição de senha <br> <br> A equipe de TI não configurou sua conta para usar esse serviço. <br> <br> Se desejar, podemos contatá-um administrador na sua organização tooreset sua senha para você. | Você está vendo esta mensagem porque sua equipe de TI não tiver habilitado a redefinição de senha para sua organização das não pode acessar o link de conta ou ainda não licenciado toouse recurso de saudação. <br> <br> tooreset sua senha, clique em contato um link de administrador toosend uma empresa tooyour de email da equipe de TI e avise você deseja tooreset sua senha para que eles podem habilitar esse recurso para você. |
| Recebo uma mensagem de erro "não foi possível verificar sua conta" depois de inserir a ID de usuário | Não foi possível verificar sua conta <br> <br> Se desejar, podemos contatá-um administrador na sua organização tooreset sua senha para você. | Você está vendo esta mensagem porque você está habilitados para redefinição de senha, mas você não registrou o serviço de saudação toouse. tooregister senha redefinida, vá toohttp://aka.ms/ssprsetup após você ter recuperado acesso tooyour conta. <br> <br> tooreset sua senha, clique em contato um administrador link toosend uma empresa tooyour de email equipe de TI. |

## <a name="next-steps"></a>Próximas etapas

* [Como toochange a uso de senha de autoatendimento de redefinição de senha](active-directory-passwords-update-your-own-password.md)
* [Página de registro de redefinição de senha](http://aka.ms/ssprsetup)
* [Portal de redefinição de senha:](https://passwordreset.microsoftonline.com/)
* [Não é possível entrar tooyour conta da Microsoft](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "Página de registro de redefinição de senha mostrando métodos registrados e botão Concluir"

