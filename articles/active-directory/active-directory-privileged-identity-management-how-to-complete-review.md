---
title: "aaaHow toocomplete uma revisão de acesso | Microsoft Docs"
description: "Depois que você iniciou uma revisão de acesso no Azure AD Privileged Identity Management, saiba como toocomplete-lo e exibir resultados de Olá"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>Como toocomplete um acesso examinar no Azure AD Privileged Identity Management
os administradores de função com privilégios podem examinar o acesso privilegiado após uma [revisão de segurança ter sido iniciada](active-directory-privileged-identity-management-how-to-start-security-review.md). O Azure AD Privileged Identity Management (PIM) automaticamente enviará um email solicitando que os usuários tooreview seu acesso. Se um usuário não obteve um email, você pode enviá-los instruções Olá [como tooperform segurança examine](active-directory-privileged-identity-management-how-to-perform-security-review.md).

Após o período de revisão de segurança hello, ou todos os usuários de saudação terminar seus Self revisar, siga as etapas de saudação nesta revisão de saudação do artigo toomanage e ver os resultados de saudação.

## <a name="manage-security-reviews"></a>Gerenciar revisões de segurança
1. Vá toohello [portal do Azure](https://portal.azure.com/) e selecione hello **do Azure AD Privileged Identity Management** aplicativo em seu painel.
2. Selecione Olá **acessar revisões** seção do painel de saudação.
3. Selecione a revisão de acesso de saudação que você deseja toomanage.

Na folha de detalhe da avaliação do acesso hello, há várias formas para gerenciar essa revisão.

![Botões de análise de acesso do PIM - captura de tela][1]

### <a name="remind"></a>Lembrar
Se uma revisão de acesso está configurada para que os usuários de saudação examinar se, Olá **lembrar** botão envia uma notificação. 

### <a name="stop"></a>Parar
Todas as revisões de acesso têm uma data de término, mas você pode usar o hello **parar** toofinish botão antecipadamente. Se todos os usuários ainda não foram revisados neste momento, eles não será capaz de tooafter Parar análise hello. Não é possível reiniciar uma análise após ela ter sido interrompida.

### <a name="apply"></a>Aplicar
Depois de uma revisão de acesso é concluída, seja porque você atingiu a data de término hello ou parado-lo manualmente, Olá **aplicar** botão implementa o resultado de saudação da revisão de saudação. Se o acesso do usuário foi negado na revisão Olá, esta é a etapa de saudação removerá sua atribuição de função.  

### <a name="export"></a>Exportação
Se você quiser resultados de saudação do tooapply de revisão de segurança Olá manualmente, você pode exportar revisão hello. Olá **exportar** botão começará a baixar um arquivo CSV. Você pode gerenciar resultados Olá no Excel ou em outros programas que abrem os arquivos CSV.

### <a name="delete"></a>Exclusão
Se você não estiver interessado em Olá analise qualquer adicional, excluí-lo. Olá **excluir** botão remove Olá revisão da saudação aplicativo PIM.

> [!IMPORTANT]
> Você não receberá um aviso antes da exclusão, portanto certifique-se de que você deseja toodelete examinar. 

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
