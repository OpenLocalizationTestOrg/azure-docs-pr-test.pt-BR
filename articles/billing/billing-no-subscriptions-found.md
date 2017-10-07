---
title: assinaturas aaaNo encontrou um erro ao tentar toosign no portal de tooAzure ou centro de contas do Azure | Microsoft Docs
description: "Fornece a solução de saudação para um problema no qual a assinaturas não encontram erro ocorre quando se inscreve no portal de tooAzure ou centro de contas do Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Erro Nenhuma assinatura encontrada no Portal do Azure ou no centro de contas do Azure
Você poderá receber uma mensagem de erro "Nenhuma assinatura encontrada" ao tentar toosign em toohello [portal do Azure](https://portal.azure.com/) ou hello [Centro de contas do Azure](https://account.windowsazure.com/Subscriptions). Este artigo fornece uma solução para esse problema.

## <a name="symptom"></a>Sintoma

Quando você tentar toosign em toohello [portal do Azure](https://portal.azure.com/) ou hello [Centro de contas do Azure](https://account.windowsazure.com/Subscriptions), você receberá Olá a seguinte mensagem de erro: "Nenhuma assinatura encontrada".

## <a name="cause"></a>Causa

Esse problema ocorrerá se sua conta não tiver permissões suficientes. 

## <a name="solution"></a>Solução

Certifique-se de que você faça login como administrador correto do hello. Um administrador de conta pode acessar somente o Centro de contas de saudação. Os administradores de serviços (SA) e os coadministradores (CA) têm acesso de permissão somente toohello portal do Azure ou Olá portal clássico do Azure.

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a>Cenário 1: Mensagem de erro é recebida em Olá [portal do Azure](https://portal.azure.com)

toofix esse problema:

* Certifique-se de que Olá correto de diretório do Azure está selecionado, clicando em sua conta na parte superior de saudação à direita.

  ![Diretório selecione Olá Olá parte superior direita da saudação portal do Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* Se hello directory à direita do Azure está selecionado, mas você ainda recebe a mensagem de erro Olá, [sua conta como um proprietário](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Cenário 2: Mensagem de erro é recebida em Olá [Centro de contas do Azure](https://account.windowsazure.com/Subscriptions)

Verifique se a conta Olá usada é Olá administrador da conta. é tooverify que Olá administrador da conta, siga estas etapas:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, selecione **assinatura**.
3. Selecione Olá assinatura que você deseja toocheck e, em seguida, selecione **configurações**.
4. Selecione **Propriedades**. Olá administrador da conta Olá assinatura é exibido no hello **administrador da conta** caixa.

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda precisar de Ajuda, [entre em contato com o suporte](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget seu problema resolvido rapidamente. 
