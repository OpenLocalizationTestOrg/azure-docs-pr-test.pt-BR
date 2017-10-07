---
title: "aaaCreate, link, excluir ou mover uma conta de integração de aplicativos lógicos do Azure | Microsoft Docs"
description: "Como toocreate uma integração de conta e vinculá-lo tooyour os aplicativos lógicos"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>O que é uma conta de integração?

Uma conta de integração permite que aplicativos de integração do enterprise toomanage artefatos, incluindo esquemas, mapas, certificados, parceiros e contratos. Qualquer aplicativo de integração que você criar usa um tooaccess de conta de integração esses esquemas, mapas, certificados e assim por diante.

## <a name="create-an-integration-account"></a>Criar uma conta de integração

1.  Entrar toohello [portal do Azure](http://portal.azure.com "portal do Azure"). No menu à esquerda do hello, selecione **mais serviços**.

    ![Escolha “Mais serviços”](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Na caixa de pesquisa hello, digite "integração" para o filtro. Na lista de resultados de saudação, selecione **contas de integração**.

    ![Filtre por "integração", selecione "Contas de Integração"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Na parte superior de saudação da página hello, escolha **adicionar**.

    ![Escolha Adicionar](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. Nome de sua conta de integração e selecione Olá assinatura do Azure que você deseja toouse. Você pode criar um novo **grupo de recursos** ou escolher um grupo de recursos existente. Selecione um **Local** para hospedar sua conta de integração e um **Tipo de preço**. 

    Quando você estiver pronto, escolha **Criar**.

    ![Forneça detalhes para sua conta de integração](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure provisiona sua conta de integração no local de saudação selecionada, que deve ser concluída em 1 minuto.

5. Atualize a página de saudação. Você verá a nova conta de integração listada.

    ![A nova conta de integração é exibida](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

Em seguida, vincule conta de integração de saudação que você tooyour criado aplicativo lógico. 

## <a name="link-an-integration-account-tooa-logic-app"></a>Vincular a um aplicativo de conta tooa lógica da integração

toogive seus aplicativos lógicos acessar toomaps, esquemas, contratos e outros artefatos em sua conta de integração, aplicativo de conta da integração link Olá tooyour lógica.

### <a name="prerequisites"></a>Pré-requisitos

* Uma conta de integração
* Um aplicativo lógico

> [!NOTE] 
> Verifique se seu aplicativo de conta e a lógica de integração no hello *mesmo local do Azure* antes de começar.


1. No hello portal do Azure, selecione seu aplicativo lógico e verifique o local da lógica do aplicativo.

    ![Selecionar seu aplicativo lógico, verificar o local](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. Em **Configurações**, selecione **Conta de Integração**.

    ![Selecionar “Conta de Integração”](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. De saudação **selecionar uma conta de integração** listar, conta de integração Olá selecione deseja toolink tooyour lógica aplicativo. toofinish vinculação, escolha **salvar**.

    ![Selecione sua conta de integração](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    Você obtém uma notificação que mostra a integração de conta é vinculado tooyour lógica aplicativo e todos os artefatos em sua conta de integração estão agora disponíveis tooyour lógica aplicativo.

    ![Seu aplicativo lógico está vinculado tooyour conta de integração](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

Agora que sua conta de integração está vinculado tooyour lógica aplicativo, é possível usar conectores de saudação B2B em seus aplicativos de lógica. Alguns conectores B2B comuns incluem a validação de XML e codificação/decodificação de arquivo simples.  

## <a name="delete-your-integration-account"></a>Excluir sua conta de integração

1. Escolha **Mais serviços**.

    ![Escolha “Mais serviços”](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Na caixa de pesquisa hello, digite "integração" para o filtro. Na lista de resultados de saudação, selecione **contas de integração**.

    ![Filtre por "integração", selecione "Contas de Integração"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Selecione a conta de integração de saudação que você deseja toodelete.

    ![Selecione toodelete de conta de integração](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. No menu de saudação, escolha **excluir**.

    ![Clique em “Excluir”](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Confirme sua conta de integração de saudação toodelete choice.

## <a name="move-your-integration-account"></a>Selecionar sua conta de integração

toomove um tooanother de conta de integração do Azure assinatura ou grupo de recursos, siga estas etapas.

> [!IMPORTANT]
> Depois de mover uma conta de integração, você deve atualizar todos os scripts toouse Olá novas IDs de recurso.

1. Escolha **Mais serviços**.

    ![Escolha “Mais serviços”](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Na caixa de pesquisa hello, digite "integração" para o filtro. Na lista de resultados de saudação, selecione **contas de integração**.

    ![Filtre por "integração", selecione "Contas de Integração"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. Selecione a conta de integração de saudação que você deseja toomove. Em **Configurações**, escolha **Propriedades**.

    ![Selecione toomove de conta de integração. Em Configurações, escolha Propriedades](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Alterar o grupo de recursos de saudação ou assinatura do Azure associado à sua conta de integração.

    ![Escolher Alterar grupo de recursos ou Alterar assinatura](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre os contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  

