---
title: "parceiros de aaaCreate para mensagens entre empresas (B2B) - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Saiba como a integração de tooyour parceiros tooadd conta com hello pacote de integração de empresa e aplicativos lógicos"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a>Adicionar ou atualizar parceiros em contratos B2B no seu fluxo de trabalho

Os parceiros são as entidades que participam de mensagens e transações B2B (entre empresas). Antes de criar os parceiros que representam você e a outra organização nessas transações, é necessário que ambas as partes compartilhem informações que identificam e validam as mensagens enviadas. Depois de abordar esses detalhes e são toostart pronto sua relação de negócios, você pode criar parceiros em sua toorepresent de conta de integração que ambos.

## <a name="what-roles-do-partners-have-in-your-integration-account"></a>Quais são as funções dos parceiros na conta de integração?

toodefine detalhes sobre mensagens de saudação trocadas entre os parceiros, você cria acordos entre parceiros. No entanto, antes de criar um contrato, você deve ter adicionado contas de integração de tooyour pelo menos dois parceiros. Sua organização deve fazer parte do contrato de Olá Olá **parceiro host**. Olá outro parceiro ou **parceiro convidado** representa Olá organização que troca mensagens com sua organização. parceiro de convidado Olá pode ser outra empresa, ou até mesmo um departamento em sua própria organização.

Depois de adicionar esses parceiros, você pode criar um contrato.

Receber e enviar as configurações são orientadas do hello ponto de vista do hello parceiro hospedado. Por exemplo, Olá receber as configurações de um contrato de determinar como o parceiro Olá hospedado recebe as mensagens enviadas de um parceiro convidado. Da mesma forma, as configurações de envio de saudação no contrato de saudação indicam como parceiro Olá hospedado envia o parceiro de convidado de toohello de mensagens.

## <a name="how-toocreate-a-partner"></a>Como um parceiro de toocreate?

1. No portal do Azure de Olá, selecione **procurar**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Na caixa de pesquisa do filtro hello, digite **integração**, em seguida, selecione **contas de integração** na lista de resultados de saudação.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Selecione onde você deseja tooadd seus parceiros de conta do hello integration.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Selecione Olá **parceiros** lado a lado.

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. Na folha de parceiros hello, escolha **adicionar**.

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. Insira um nome para seu parceiro e, em seguida, escolha um **Qualificador**. Finalmente, insira um **valor** toohelp identificar documentos que entram em seus aplicativos.

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. progresso de saudação toosee para o processo de criação de parceiro, selecione Olá *bell* ícone de notificação.

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. tooconfirm seus parceiros novos foram com êxito adicionado, selecione Olá **parceiros** lado a lado.

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    Depois de selecionar o bloco de parceiros hello, você também verá parceiros recém-adicionado na folha de parceiros de saudação.

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a>Como parceiros de tooedit existente em sua conta de integração

1. Selecione Olá **parceiros** lado a lado.
2. Depois de abre a folha de parceiros hello, selecione o parceiro de saudação deseja tooedit.
3. Em Olá **atualização parceiro** lado a lado, faça as alterações.
4. Depois de terminar, escolha **salvar**, ou toocancel as alterações, selecione **descartar**.

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a>Como toodelete um parceiro

1. Selecione Olá **parceiros** lado a lado.
2. Depois de abre a folha de parceiro hello, selecione o parceiro de saudação que você deseja toodelete.
3. Clique em **Excluir**.

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre os contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  

