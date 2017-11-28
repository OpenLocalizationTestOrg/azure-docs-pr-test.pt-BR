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
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="1431a-103">Validar XML com esquemas para os aplicativos lógicos do Azure e hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="1431a-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="1431a-104">Esquemas confirme que documentos XML de saudação que receber são válidos e tem Olá esperado dados em um formato predefinido.</span><span class="sxs-lookup"><span data-stu-id="1431a-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="1431a-105">Esquemas também ajudam a validar mensagens trocadas em um cenário B2B.</span><span class="sxs-lookup"><span data-stu-id="1431a-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="1431a-106">Adicionar um esquema</span><span class="sxs-lookup"><span data-stu-id="1431a-106">Add a schema</span></span>

1. <span data-ttu-id="1431a-107">No portal do Azure de Olá, selecione **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="1431a-107">In hello Azure portal, select **More services**.</span></span>

    ![Portal do Azure, "Mais serviços"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="1431a-109">Na caixa de pesquisa do filtro hello, digite **integração**e selecione **contas de integração** Olá da lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="1431a-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![Filtre a caixa de pesquisa](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="1431a-111">Selecione Olá **conta integration** onde você deseja que o esquema de saudação tooadd.</span><span class="sxs-lookup"><span data-stu-id="1431a-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![Lista de contas de integração](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="1431a-113">Escolha Olá **esquemas** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="1431a-113">Choose hello **Schemas** tile.</span></span>

    ![Conta de integração de exemplo, "Esquemas"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="1431a-115">Adicione um arquivo de esquema com menos de 2 MB</span><span class="sxs-lookup"><span data-stu-id="1431a-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="1431a-116">Em Olá **esquemas** folha é aberta (de saudação etapas anteriores), escolha **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1431a-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![Folha Esquemas, "Adicionar"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="1431a-118">Digite um nome para o seu esquema.</span><span class="sxs-lookup"><span data-stu-id="1431a-118">Enter a name for your schema.</span></span> <span data-ttu-id="1431a-119">Carregar arquivo de esquema Olá selecionando Olá pasta ícone próximo toohello **esquema** caixa.</span><span class="sxs-lookup"><span data-stu-id="1431a-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="1431a-120">Após a conclusão do processo de carregamento de saudação, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="1431a-120">After hello upload process completes, select **OK**.</span></span>

    ![Captura de tela de "Adicionar esquema" com "Arquivo pequeno" realçado](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="1431a-122">Adicionar um arquivo de esquema maior que 2 MB (até no máximo too8 MB)</span><span class="sxs-lookup"><span data-stu-id="1431a-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="1431a-123">Essas etapas diferem com base no nível de acesso do contêiner de blob de saudação: **pública** ou **nenhum acesso anônimo**.</span><span class="sxs-lookup"><span data-stu-id="1431a-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="1431a-124">**toodetermine esse nível de acesso**</span><span class="sxs-lookup"><span data-stu-id="1431a-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="1431a-125">Abra o **Gerenciador de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="1431a-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="1431a-126">Em **contêineres de Blob**, selecione contêiner de blob de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="1431a-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="1431a-127">Selecione **Segurança**, **Nível de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="1431a-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="1431a-128">Se o nível de acesso de segurança Olá blob é **pública**, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="1431a-128">If hello blob security access level is **Public**, follow these steps.</span></span>

![Gerenciador de Armazenamento do Azure, com "Contêineres de Blob", "Segurança" e "Público" realçados](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="1431a-130">Carregar conta de armazenamento Olá esquema tooyour e copie Olá URI.</span><span class="sxs-lookup"><span data-stu-id="1431a-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![Conta de armazenamento com o URI realçado](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="1431a-132">Em **adicionar esquema**, selecione **arquivo grande**e fornecer Olá URI no hello **conteúdo URI** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1431a-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    ![Esquemas, com o botão "Adicionar" e "Arquivo grande" realçados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="1431a-134">Se o nível de acesso de segurança Olá blob é **nenhum acesso anônimo**, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="1431a-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

![Gerenciador de Armazenamento do Azure, com "Contêineres de Blob", "Segurança" e "Sem acesso anônimo" realçados](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="1431a-136">Carregar conta de armazenamento Olá esquema tooyour.</span><span class="sxs-lookup"><span data-stu-id="1431a-136">Upload hello schema tooyour storage account.</span></span>

    ![Conta de armazenamento](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="1431a-138">Gere uma assinatura de acesso compartilhado para o esquema de saudação.</span><span class="sxs-lookup"><span data-stu-id="1431a-138">Generate a shared access signature for hello schema.</span></span>

    ![Conta de armazenamento com a guia assinaturas de acesso compartilhado realçada](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="1431a-140">Em **adicionar esquema**, selecione **arquivo grande**e forneça a assinatura de acesso compartilhado Olá URI no hello **conteúdo URI** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1431a-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    ![Esquemas, com o botão "Adicionar" e "Arquivo grande" realçados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="1431a-142">Em Olá **esquemas** folha da sua conta de integração, seu esquema recém-adicionado deve aparecer.</span><span class="sxs-lookup"><span data-stu-id="1431a-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Sua conta de integração, com "Esquemas" e o novo esquema de saudação realçado](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="1431a-144">Editar esquemas</span><span class="sxs-lookup"><span data-stu-id="1431a-144">Edit schemas</span></span>

1. <span data-ttu-id="1431a-145">Escolha Olá **esquemas** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="1431a-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="1431a-146">Depois de saudação **esquemas** abre a folha, esquema Olá selecione que você deseja tooedit.</span><span class="sxs-lookup"><span data-stu-id="1431a-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="1431a-147">Em Olá **esquemas** folha, escolha **editar**.</span><span class="sxs-lookup"><span data-stu-id="1431a-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![Folha Esquemas](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="1431a-149">O arquivo de esquema Olá selecione que você deseja tooedit e selecione **abrir**.</span><span class="sxs-lookup"><span data-stu-id="1431a-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![Tooedit de arquivo de esquema aberto](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="1431a-151">Azure mostra uma mensagem que Olá esquema foi carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="1431a-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="1431a-152">Excluir esquemas</span><span class="sxs-lookup"><span data-stu-id="1431a-152">Delete schemas</span></span>

1. <span data-ttu-id="1431a-153">Escolha Olá **esquemas** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="1431a-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="1431a-154">Depois de saudação **esquemas** abre a folha, esquema Olá selecione deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="1431a-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="1431a-155">Em Olá **esquemas** folha, escolha **excluir**.</span><span class="sxs-lookup"><span data-stu-id="1431a-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![Folha Esquemas](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="1431a-157">tooconfirm que você deseja toodelete Olá selecionado esquema, escolha **Sim**.</span><span class="sxs-lookup"><span data-stu-id="1431a-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    ![Mensagem de confirmação "Excluir esquema"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="1431a-159">Em Olá **esquemas** folha, lista de esquema Olá atualiza e não inclui o esquema de saudação excluído.</span><span class="sxs-lookup"><span data-stu-id="1431a-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    ![Conta de integração com "Esquemas" realçado](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="1431a-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1431a-161">Next steps</span></span>
* <span data-ttu-id="1431a-162">[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do enterprise Olá").</span><span class="sxs-lookup"><span data-stu-id="1431a-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

