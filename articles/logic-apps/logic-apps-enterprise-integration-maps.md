---
title: "aaaTransform XML com XSLT mapas - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Adicionar que XSLT mapeia tootransform dados XML com os aplicativos lógicos do Azure e hello Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a>Adicionar mapas para a transformação de dados XML

Enterprise integração usa mapas tootransform dados XML entre formatos. Um mapa é um documento XML que define os dados de saudação em um documento que deve ser transformado em outro formato. 

## <a name="why-use-maps"></a>Por que usar mapas?

Suponha que você recebe regularmente B2B ordens ou notas fiscais de um cliente que usa o formato YYYMMDD Olá para datas. No entanto, em sua organização, você armazenar datas no formato MMDDYYY hello. Você pode usar um mapa muito*transformação* formato de data YYYMMDD Olá em Olá MMDDYYY antes de armazenar os detalhes do pedido ou da fatura Olá em seu banco de dados de atividade do cliente.

## <a name="how-do-i-create-a-map"></a>Como faço para criar um mapa?

Você pode criar projetos de integração do BizTalk com hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do enterprise Olá") para Visual Studio 2015. Então, será possível criar um arquivo de mapa de integração que permitirá visualizar itens de mapa entre dois arquivos de esquema XML. Após criar esse projeto, você terá um documento XSLT.

## <a name="how-do-i-add-a-map"></a>Como adicionar um mapa?

1. No portal do Azure de Olá, selecione **procurar**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Na caixa de pesquisa do filtro hello, digite **integração**, em seguida, selecione **contas de integração** Olá da lista de resultados.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Selecione a conta de integração de Olá onde você deseja tooadd Olá mapa.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Selecione Olá **mapas** lado a lado.

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. Depois de abre a folha de mapas hello, escolha **adicionar**.

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. Insira um **Nome** para o mapa. mapa de saudação tooupload de arquivo, escolha o ícone de pasta Olá Olá direita da saudação **mapa** caixa de texto. Após a conclusão do processo de carregamento de saudação, escolha **Okey**.

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. Depois que o Azure adiciona a conta de integração do hello mapa tooyour, você obterá uma mensagem na tela que mostra se o arquivo de mapa foi adicionado ou não. Depois que você receber essa mensagem, escolha Olá **mapas** lado a lado para que você possa exibir hello recentemente adicionado o mapa.

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>Como editar um mapa?

Você deve carregar um novo arquivo de mapa com alterações Olá que desejar. Primeiro, você pode baixar mapa Olá para edição.

tooupload um novo mapa que substitui o mapa do hello existente, siga estas etapas.

1. Escolha Olá **mapas** lado a lado.

2. Depois de abre a folha de mapas hello, selecione mapa de saudação que você deseja tooedit.

3. Em Olá **mapas** folha, escolha **atualização**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. No selecionador de arquivo hello, selecione o arquivo de mapa de saudação que você deseja tooupload e selecione **abrir**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>Como um mapa de toodelete?

1. Escolha Olá **mapas** lado a lado.

2. Depois de abre a folha de mapas hello, selecione mapa de saudação deseja toodelete.

3. Clique em **Excluir**.

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. Confirme que você deseja que o mapa de saudação toodelete.

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")  
* [Saiba mais sobre os contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  
* [Saiba mais sobre transformações](logic-apps-enterprise-integration-transform.md "Saiba mais sobre as transformações de integração corporativa")  

