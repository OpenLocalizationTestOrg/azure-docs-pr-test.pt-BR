---
title: "aaaMicrosoft estados do usuário do Azure multi-Factor Authentication"
description: "Saiba mais sobre estados de usuário no Azure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a>Como a verificação de duas etapas toorequire para um usuário ou grupo

Há duas abordagens para exigir a verificação em duas etapas. Olá a primeira opção é tooenable cada usuário individual para o Azure multi-Factor Authentication (MFA). Quando os usuários estão habilitados individualmente, eles sempre executar a verificação em duas etapas (com algumas exceções, como quando eles entrarem dos endereços IP confiáveis ou se Olá lembradas dispositivos recurso está ativado). Olá segunda opção é tooset uma política de acesso condicional requer duas etapas verificação sob determinadas condições.

>[!TIP] 
>Escolha um desses métodos toorequire verificacao, não ambos. A habilitação de um usuário para a MFA do Azure substitui quaisquer políticas de acesso condicional.

## <a name="which-option-is-right-for-you"></a>Qual opção é ideal para você

**Ativando o Azure MFA alterando estados do usuário** é a abordagem tradicional Olá para exigir a verificação em duas etapas. Ele funciona para ambos os Azure MFA na nuvem hello e servidor Azure MFA. Todos os usuários de saudação que permitem a você ter Olá mesma experiência, que é a verificação de duas etapas tooperform toda vez que entrar. A habilitação de um usuário substitui qualquer política de acesso condicional que possa afetar esse usuário. 

**Habilitar a MFA do Azure com uma política de acesso condicional** é uma abordagem mais flexível para exigir a verificação em duas etapas. Ele só funciona para Azure MFA na nuvem Olá, no entanto, e o acesso condicional é um [paga o recurso do Active Directory do Azure](https://www.microsoft.com/cloud-platform/azure-active-directory-features). Você pode criar políticas de acesso condicional que se aplicam a toogroups, bem como para usuários individuais. Grupos de alto risco podem receber mais restrições do que grupos de baixo risco, ou a verificação em duas etapas pode ser exigida apenas para aplicativos de nuvem de alto risco e ignorada para os de baixo risco. 

Ambas as opções prompt tooregister de usuários para hello Azure multi-Factor Authentication pela primeira vez que entrar depois de ativar o requisitos de saudação. Ambas as opções também funcionam com hello configurável [configurações de autenticação multifator do Azure](multi-factor-authentication-whats-next.md)

## <a name="enable-azure-mfa-by-changing-user-status"></a>Habilitar a MFA do Azure alterando o status do usuário

Contas de usuário no Azure multi-Factor Authentication têm Olá seguintes três estados distintos:

| Status | Descrição | Aplicativos que não usam navegador afetados |
|:---:|:---:|:---:|
| Desabilitado |estado do saudação padrão para um novo usuário não registrado do Azure multi-Factor Authentication (MFA). |Não |
| habilitado |usuário Olá tenha sido registrado no Azure MFA, mas não foi registrado. Eles serão solicitados tooregister Olá próxima vez que entrar. |Não.  Eles continuam toowork até que o processo de registro Olá seja concluído. |
| Imposto |usuário Olá foi registrado e concluiu o processo de registro Olá para o Azure MFA. |Sim.  Os aplicativos exigem senhas de aplicativo. |

Estado do usuário reflete se um administrador tenha registrado-los no Azure MFA, e se eles concluído o processo de registro de saudação.

Todos os usuários começam com o status *desabilitado*. Quando você registra os usuários na MFA do Azure, seu estado é alterado para *habilitado*. Quando usuários habilitados entrarem e concluir o processo de registro hello, seu estado é alterado muito*imposta*.  

### <a name="view-hello-status-for-a-user"></a>Exibir o status de saudação para um usuário

Saudação de uso após etapas tooaccess Olá página onde você pode exibir e gerenciar os estados do usuário:

1. Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador.
2. Vá muito**Active Directory do Azure** > **usuários e grupos** > **todos os usuários**.
3. Selecione **Autenticação Multifator**.
   ![Selecionar a Autenticação Multifator](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. Uma nova página, que exibe os estados de saudação do usuário, é aberto.
   ![estados do usuário da Autenticação Multifator do Azure – captura de tela](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-hello-status-for-a-user"></a>Alterar status de saudação para um usuário

1. Use Olá anterior etapas tooget toohello autenticação multifator usuários página.
2. Localizar Olá usuário que você deseja tooenable para o Azure MFA. Talvez seja necessário toochange Olá exibição na parte superior da saudação. 
   ![Localizar usuário – captura de tela](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. Verifique o nome hello caixa próximo tootheir.
4. Olá à direita, em etapas rápidas, escolha **habilitar** ou **desabilitar**.
   ![Habilitar o usuário selecionado – captura de tela](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*Habilitado* usuários automaticamente alternar muito*imposta* quando eles se registrar para o Azure MFA. Você não deve alterar manualmente Olá tooenforced de estado de usuário. 

5. Confirme sua seleção na janela pop-up de saudação que é aberta. 

Depois de habilitar os usuários, você deverá notificá-los por email. Informe que serão solicitadas Olá tooregister próxima vez que entrar. Além disso, se sua organização usa aplicativos sem navegador que não dão suporte a autenticação moderna, eles precisarão toocreate senhas de aplicativo. Você também pode incluir um link tooour [guia do usuário final de Azure MFA](./end-user/multi-factor-authentication-end-user.md) toohelp-los começar.

### <a name="use-powershell"></a>Usar o PowerShell
estado toochange Olá usuário status usando [PowerShell do Azure AD](/powershell/azure/overview), alterar `$st.State`. Há três opções de estado possíveis:

* habilitado
* Imposto
* Desabilitado  

Não mova os usuários diretamente toohello *imposto* estado. Aplicativos não baseados em navegador irá parar de funcionar porque Olá o usuário não funcionam por meio de registro MFA e obtido um [senha de aplicativo](multi-factor-authentication-whats-next.md#app-passwords). 

Usando o PowerShell é uma boa opção quando você precisar toobulk permitindo que os usuários. Crie um script do PowerShell que percorre uma lista de usuários e os habilita:

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

Aqui está um exemplo:

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a>Habilitar a MFA do Azure com uma política de acesso condicional

O acesso condicional é um recurso pago do Azure Active Directory, com várias opções de configuração possíveis. Essas etapas explicam toocreate unidirecional uma política. Para saber mais, leia sobre o [Acesso condicional no Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).

1. Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador.
2. Vá muito**Active Directory do Azure** > **acesso condicional**.
3. Selecione **Nova política**.
4. Em **Atribuições**, selecione **Usuários e grupos**. Saudação de uso **incluir** e **excluir** guias toospecify quais usuários e grupos que será gerenciado pela política de saudação.
5. Em **Atribuições**, selecione **Aplicativos de nuvem**. Escolha tooinclude **todos os aplicativos de nuvem**.
6. Em **Controles de acesso**, selecione **Grant**. Escolha **Exigir autenticação multifator**.
7. Ativar **habilitar política** muito**na** e, em seguida, selecione **salvar**.

Olá outras opções de política de acesso condicional Olá permitem toospecify exatamente quando a verificação em duas etapas é necessária. Por exemplo, você pode criar uma diretiva que informa: quando prestadores de serviço tooaccess nosso aplicativo de compras de redes não confiáveis em dispositivos que não estão associados ao domínio, exigir verificação em duas etapas. 

## <a name="next-steps"></a>Próximas etapas

- Obtenha dicas sobre Olá [as práticas recomendadas para acesso condicional](../active-directory/active-directory-conditional-access-best-practices.md)

- Gerenciar configurações de Autenticação Multifator para [seus usuários e os dispositivos deles](multi-factor-authentication-manage-users-and-devices.md)