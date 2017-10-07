---
title: "aaaHow tooperform uma revisão de acesso | Microsoft Docs"
description: "Saiba como tooperform uma revisão com hello aplicativo Privileged Identity Management do Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a>Como tooperform um acesso examinar no Azure AD Privileged Identity Management
Active Directory (AD) Privileged Identity Management do Azure simplifica como as empresas gerenciam o acesso privilegiado tooresources no AD do Azure e outros Microsoft online services como Office 365 ou Microsoft Intune.  

Se você receber a função administrativa tooan, com privilégios de função administrador de sua organização pode solicitar que você tooregularly confirmar que você ainda precisa essa função para seu trabalho. Você poderá receber um email que inclui um link ou vá reta toohello [portal do Azure](https://portal.azure.com). Siga as etapas de saudação este tooperform artigo automaticamente examine atribuídas funções de.

Se você for um administrador com privilégios de função interessado em análises de acesso, obtenha mais detalhes em [como toostart um acesso examine](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="add-hello-privileged-identity-management-application"></a>Adicionar aplicativo do hello Privileged Identity Management
Você pode usar o aplicativo de gerenciamento de identidade com privilégios (PIM) de saudação do AD do Azure no hello [portal do Azure](https://portal.azure.com/) tooperform sua análise.  Se você não tiver o aplicativo do Azure AD Privileged Identity Management hello em seu portal, siga essas tooget etapas iniciado.

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Selecione seu nome de usuário no canto superior direito de saudação do hello portal do Azure e diretório hello selecione onde você irá operar.
3. Selecione **mais serviços** e usar Olá toosearch de caixa de texto de filtro para **do Azure AD Privileged Identity Management**.
4. Verificar **Pin toodashboard** e, em seguida, clique em **criar**. Olá aplicativo Privileged Identity Management será aberto.

## <a name="approve-or-deny-access"></a>Aprovar ou negar acesso
Quando você aprova ou nega o acesso, você está apenas dizendo revisor Olá se você usar essa função ou não. Escolha **aprovar** se você quiser toostay na função hello, ou **Deny** se você não precisa Olá a acesso mais. Seu status não será alterado imediatamente, até que o revisor Olá aplica resultados hello.
Siga essas etapas toofind e concluir a avaliação do acesso hello:

1. No aplicativo PIM do hello, selecione **acesso privilegiado de revisão**. Se você tiver quaisquer revisões acesso pendente, eles aparecem no hello que acesso do AD do Azure analisa folha.
2. Selecione a revisão Olá deseja toocomplete.
3. A menos que você criou revisão Olá, aparecem como Olá apenas usuário revisão hello. Selecione nome do próximo tooyour Olá marca de seleção.
4. Escolha **Aprovar** ou **Negar**. Talvez seja necessário um motivo para a sua decisão de saudação do tooinclude **fornecer um motivo** caixa de texto.  
5. Olá fechar **funções de análise do Azure AD** folha.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
