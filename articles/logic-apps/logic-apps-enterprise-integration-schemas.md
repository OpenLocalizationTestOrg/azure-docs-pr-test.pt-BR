---
title: "aaaSchemas para validação de XML - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Validar documentos XML com esquemas para o Aplicativo Lógico do Azure e o Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>Validar XML com esquemas para os aplicativos lógicos do Azure e hello Enterprise Integration Pack

Esquemas confirme que documentos XML de saudação que receber são válidos e tem Olá esperado dados em um formato predefinido. Esquemas também ajudam a validar mensagens trocadas em um cenário B2B.

## <a name="add-a-schema"></a>Adicionar um esquema

1. No portal do Azure de Olá, selecione **mais serviços**.

    ![Portal do Azure, "Mais serviços"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. Na caixa de pesquisa do filtro hello, digite **integração**e selecione **contas de integração** Olá da lista de resultados.

    ![Filtre a caixa de pesquisa](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. Selecione Olá **conta integration** onde você deseja que o esquema de saudação tooadd.

    ![Lista de contas de integração](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. Escolha Olá **esquemas** lado a lado.

    ![Conta de integração de exemplo, "Esquemas"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>Adicione um arquivo de esquema com menos de 2 MB

1. Em Olá **esquemas** folha é aberta (de saudação etapas anteriores), escolha **adicionar**.

    ![Folha Esquemas, "Adicionar"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. Digite um nome para o seu esquema. Carregar arquivo de esquema Olá selecionando Olá pasta ícone próximo toohello **esquema** caixa. Após a conclusão do processo de carregamento de saudação, selecione **Okey**.

    ![Captura de tela de "Adicionar esquema" com "Arquivo pequeno" realçado](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>Adicionar um arquivo de esquema maior que 2 MB (até no máximo too8 MB)

Essas etapas diferem com base no nível de acesso do contêiner de blob de saudação: **pública** ou **nenhum acesso anônimo**.

**toodetermine esse nível de acesso**

1.  Abra o **Gerenciador de Armazenamento do Azure**. 

2.  Em **contêineres de Blob**, selecione contêiner de blob de saudação desejado. 

3.  Selecione **Segurança**, **Nível de Acesso**.

Se o nível de acesso de segurança Olá blob é **pública**, siga estas etapas.

![Gerenciador de Armazenamento do Azure, com "Contêineres de Blob", "Segurança" e "Público" realçados](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. Carregar conta de armazenamento Olá esquema tooyour e copie Olá URI.

    ![Conta de armazenamento com o URI realçado](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. Em **adicionar esquema**, selecione **arquivo grande**e fornecer Olá URI no hello **conteúdo URI** caixa de texto.

    ![Esquemas, com o botão "Adicionar" e "Arquivo grande" realçados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

Se o nível de acesso de segurança Olá blob é **nenhum acesso anônimo**, siga estas etapas.

![Gerenciador de Armazenamento do Azure, com "Contêineres de Blob", "Segurança" e "Sem acesso anônimo" realçados](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. Carregar conta de armazenamento Olá esquema tooyour.

    ![Conta de armazenamento](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. Gere uma assinatura de acesso compartilhado para o esquema de saudação.

    ![Conta de armazenamento com a guia assinaturas de acesso compartilhado realçada](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. Em **adicionar esquema**, selecione **arquivo grande**e forneça a assinatura de acesso compartilhado Olá URI no hello **conteúdo URI** caixa de texto.

    ![Esquemas, com o botão "Adicionar" e "Arquivo grande" realçados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. Em Olá **esquemas** folha da sua conta de integração, seu esquema recém-adicionado deve aparecer.

    ![Sua conta de integração, com "Esquemas" e o novo esquema de saudação realçado](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>Editar esquemas

1. Escolha Olá **esquemas** lado a lado.

2. Depois de saudação **esquemas** abre a folha, esquema Olá selecione que você deseja tooedit.

3. Em Olá **esquemas** folha, escolha **editar**.

    ![Folha Esquemas](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. O arquivo de esquema Olá selecione que você deseja tooedit e selecione **abrir**.

    ![Tooedit de arquivo de esquema aberto](media/logic-apps-enterprise-integration-schemas/edit-31.png)

Azure mostra uma mensagem que Olá esquema foi carregado com êxito.

## <a name="delete-schemas"></a>Excluir esquemas

1. Escolha Olá **esquemas** lado a lado.

2. Depois de saudação **esquemas** abre a folha, esquema Olá selecione deseja toodelete.

3. Em Olá **esquemas** folha, escolha **excluir**.

    ![Folha Esquemas](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. tooconfirm que você deseja toodelete Olá selecionado esquema, escolha **Sim**.

    ![Mensagem de confirmação "Excluir esquema"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    Em Olá **esquemas** folha, lista de esquema Olá atualiza e não inclui o esquema de saudação excluído.

    ![Conta de integração com "Esquemas" realçado](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do enterprise Olá").  

