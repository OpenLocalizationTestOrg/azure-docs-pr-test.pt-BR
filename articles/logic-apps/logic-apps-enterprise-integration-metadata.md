---
title: "integração aaaManage conta artefato de metadados - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Adicionar ou recuperar metadados de artefato de contas de integração dos Aplicativo Lógico do Azure"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>Gerenciar metadados de artefato nas contas de integração de aplicativos lógicos

É possível definir metadados personalizados para artefatos em contas de integração e recuperar esses metadados durante o tempo de execução do aplicativo lógico. Por exemplo, é possível especificar metadados para artefatos como parceiros, contratos, esquemas e mapas – todos armazenam metadados usando pares chave-valor. Atualmente, os artefatos não é possível criar metadados por meio da interface do usuário, mas você pode usar APIs REST toocreate metadados. metadados de tooadd ao criar ou selecionar um parceiro, o contrato ou o esquema no hello portal do Azure, escolha **editar como JSON**. metadados de artefato tooretrieve em aplicativos lógicos, você pode usar o recurso de pesquisa de artefato de conta de integração de saudação.

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a>Adicionar metadados tooartifacts nas contas de integração

1. Crie uma [conta de integração](logic-apps-enterprise-integration-create-integration-account.md).

2. Adicionar uma conta de integração do artefato tooyour, por exemplo, um [parceiro](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [contrato](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), ou [esquema](logic-apps-enterprise-integration-schemas.md).

3.  Selecione o artefato hello, escolha **editar como JSON**e insira os detalhes de metadados.

    ![Inserir metadados](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Recuperar metadados de artefatos de aplicativos lógicos

1. Crie um [aplicativo lógico](logic-apps-create-a-logic-app.md).

2. Criar um [link da sua conta de integração lógica aplicativo tooyour](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app). 

3. No Designer de lógica de aplicativo, adicione um disparador como *solicitação* ou *HTTP* tooyour lógica aplicativo.

4.  Escolha **Próxima Etapa** > **Adicionar uma ação**. Pesquise *integração* para poder localizá-la e, em seguida, selecione **Conta de Integração – Pesquisa de Artefato da Conta de Integração**.

    ![Selecionar Pesquisa de Artefato da Conta de Integração](media/logic-apps-enterprise-integration-metadata/image2.png)

5. Selecione Olá **tipo de artefato**e fornecer Olá **nome do artefato**.

    ![Selecionar tipo de artefato e especificar um nome de artefato](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>Exemplo: Recuperar metadados do parceiro

Os metadados do parceiro têm estes detalhes de `routingUrl`:

![Encontrar metadados de “routingURL” do parceiro](media/logic-apps-enterprise-integration-metadata/image6.png)

1. No aplicativo lógico, adicione o gatilho, uma ação **Conta de Integração – Pesquisa de Artefato da Conta de Integração** do parceiro e um **HTTP**.

    ![Adicionar o gatilho, pesquisa de artefato e aplicativo de lógica de tooyour "HTTP"](media/logic-apps-enterprise-integration-metadata/image4.png)

2. Olá tooretrieve URI, vá tooCode exibição para seu aplicativo lógico. A definição do aplicativo lógico deve ser parecida com este exemplo:

    ![Procurar pesquisa](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre os contratos](logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  
