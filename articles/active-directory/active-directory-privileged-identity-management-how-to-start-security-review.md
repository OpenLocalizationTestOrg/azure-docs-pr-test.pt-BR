---
title: "aaaHow toostart uma revisão de acesso | Microsoft Docs"
description: "Saiba como toocreate um acesso examinar de identidades com privilégios com hello aplicativo Privileged Identity Management do Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>Como toostart um acesso examinar no Azure AD Privileged Identity Management
As atribuições de função se tornam "obsoletas" quando os usuários têm acesso privilegiado de que não precisam mais. Em ordem tooreduce Olá os riscos associados com essas atribuições de funções obsoletas administradores com privilégios de função devem examinar regularmente funções hello que os usuários tem sido fornecidos. Este documento aborda etapas Olá para iniciar uma revisão de acesso no Azure AD Privileged Identity Management (PIM).

## <a name="start-an-access-review"></a>Iniciar uma revisão de acesso
> [!NOTE]
> Se você não adicionou o painel de tooyour do aplicativo de PIM Olá no hello portal do Azure, consulte as etapas de saudação em [guia de Introdução ao Privileged Identity Management do Azure](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Na página principal do aplicativo do PIM de Olá, há três toostart de maneiras uma revisão de acesso:

* **Acessar revisões** > **Adicionar**
* **Funções** > **botão** Revisar
* Selecione Olá função específica toobe revisado na lista de funções hello > **revisão** botão

Quando você clica na Olá **examine** botão hello **iniciar uma revisão de acesso** folha é exibida. Nesta folha, você está indo tooconfigure Olá revisão com um nome e tempo limite, escolha tooreview uma função e decide quem executará revisão hello.

![Iniciar uma análise de acesso – captura de tela][1]

### <a name="configure-hello-review"></a>Configurar análise Olá
toocreate um acesso revisar, é necessário tooname-lo e definir uma data de início e término.

![Configurar a análise – captura de tela][2]

Verifique o comprimento de saudação do hello revisar tempo suficiente para que os usuários toocomplete. Se terminar antes da data de término hello, você pode interromper sempre revisão Olá no início.

### <a name="choose-a-role-tooreview"></a>Escolha uma função tooreview
Cada análise se concentra em apenas uma função. A menos que você iniciou Olá acesso revisão da folha de uma função específica, você precisará toochoose uma função agora.

1. Navegue muito**examinar associação de função**
   
    ![Examinar a associação de função – captura de tela][3]
2. Escolha uma função na lista de saudação.

### <a name="decide-who-will-perform-hello-review"></a>Decidir quem executará revisão Olá
Há três opções para executar uma análise. Você pode atribuir Olá revisão toosomeone toocomplete else, você poderá fazê-lo, ou você pode fazer com que a cada usuário revisar seu próprios acesso.

1. Navegue muito**selecionar revisores**
   
    ![Selecionar revisores – captura de tela][4]
2. Escolha uma das opções de saudação:
   
   * **Selecionar revisor**: use essa opção quando você não souber quem precisa de acesso. Com essa opção, você pode atribuir o proprietário do recurso Olá revisão tooa ou toocomplete do Gerenciador de grupo.
   * **Me**: útil se você quiser toopreview como acesso revisões de trabalho, ou se desejar tooreview em nome de pessoas que não é possível.
   * **Membros reveja próprios**: Use esta opção toohave Olá usuários revisão suas atribuições de função.

### <a name="start-hello-review"></a>Revisão de saudação inicial
Por fim, você tem Olá opção toorequire que os usuários forneçam um motivo se eles aprovar o acesso. Adicione uma descrição de revisão de saudação se desejar e selecione **iniciar**.

Certifique-se de permitir que os usuários saibam que se trata de uma revisão de acesso aguardar que eles e mostrá-los [como tooperform um acesso examine](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-hello-access-review"></a>Gerenciar Olá acesso revisão
Você pode acompanhar o progresso de saudação como revisores Olá concluir suas revisões em Olá painel PIM do AD do Azure, em Olá acesso revisões de seção. Sem direitos de acesso serão alterados no diretório Olá até [revisão Olá conclui](active-directory-privileged-identity-management-how-to-complete-review.md).

Até que o período de revisão hello está acima, pode lembrar usuários toocomplete revisão ou parada Olá revisão no início do access Olá seção examina.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>Sumário do PIM
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
