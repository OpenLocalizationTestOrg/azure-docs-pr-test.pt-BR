---
title: Criando um aplicativo de Proxy de aplicativo de aaaProblem | Microsoft Docs
description: "Como tootroubleshoot problemas de criação de aplicativos de Proxy de aplicativo no portal de administração do AD do Azure Olá"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a>Problemas ao criar um aplicativo de Application Proxy 

Abaixo estão alguns dos problemas comuns de saudação face de pessoas ao criar um novo aplicativo de proxy de aplicativo.

## <a name="recommended-documents"></a>Documentos recomendados 

toolearn mais sobre como criar um aplicativo de Proxy de aplicativo por meio de saudação Portal de administração, consulte [publicar aplicativos usando o Proxy de aplicativo do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Se você a seguir etapas Olá nesse documento e estiver recebendo um erro ao criar o aplicativo hello, consulte detalhes do erro Olá para obter informações e sugestões para como toofix Olá aplicativo. A maioria das mensagens de erro incluem uma correção sugerida. 

## <a name="specific-things-toocheck"></a>Toocheck coisas específicas

erros comuns de tooavoid, verifique se:

-   Você é um administrador com permissão toocreate um aplicativo de Proxy de aplicativo

-   URL interna Olá é exclusivo

-   URL externa de saudação é exclusivo

-   Olá início URLs com http ou https e terminar com um "/"

-   Olá URL deve ser um nome de domínio e não um endereço IP

mensagem de erro de saudação deve exibir no canto superior direito da saudação quando você cria o aplicativo hello. Você também pode selecionar as mensagens de erro de Olá Olá notificação ícone toosee.

   ![Prompt de notificação](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>Próximas etapas
[Habilitar Proxy de aplicativo no portal do Azure de saudação](active-directory-application-proxy-enable.md)
