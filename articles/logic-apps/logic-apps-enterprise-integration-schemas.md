---
title: "Esquemas para validação de XML – Aplicativo Lógico do Azure | Microsoft Docs"
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
ms.openlocfilehash: 4f58a587c1f10aea1cee89e46fa9ec340e0d21c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-the-enterprise-integration-pack"></a><span data-ttu-id="3a042-103">Validar XML com esquemas para o Aplicativo Lógico do Azure e o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="3a042-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span></span>

<span data-ttu-id="3a042-104">Esquemas confirmam que os documentos XML recebidos são válidos e têm os dados esperados em um formato predefinido.</span><span class="sxs-lookup"><span data-stu-id="3a042-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span></span> <span data-ttu-id="3a042-105">Esquemas também ajudam a validar mensagens trocadas em um cenário B2B.</span><span class="sxs-lookup"><span data-stu-id="3a042-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="3a042-106">Adicionar um esquema</span><span class="sxs-lookup"><span data-stu-id="3a042-106">Add a schema</span></span>

1. <span data-ttu-id="3a042-107">No portal do Azure, clique em **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="3a042-107">In the Azure portal, select **More services**.</span></span>

    ![Portal do Azure, "Mais serviços"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="3a042-109">Insira **integração** na caixa de pesquisa do filtro e selecione **Contas de Integração** na lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="3a042-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span></span>

    ![Filtre a caixa de pesquisa](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="3a042-111">Escolha a **conta de integração** à qual você deseja adicionar o esquema.</span><span class="sxs-lookup"><span data-stu-id="3a042-111">Select the **integration account** where you want to add the schema.</span></span>

    ![Lista de contas de integração](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="3a042-113">Escolha o bloco **Esquemas**.</span><span class="sxs-lookup"><span data-stu-id="3a042-113">Choose the **Schemas** tile.</span></span>

    ![Conta de integração de exemplo, "Esquemas"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="3a042-115">Adicione um arquivo de esquema com menos de 2 MB</span><span class="sxs-lookup"><span data-stu-id="3a042-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="3a042-116">Na folha **Esquemas** (das etapas anteriores), selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3a042-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span></span>

    ![Folha Esquemas, "Adicionar"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="3a042-118">Digite um nome para o seu esquema.</span><span class="sxs-lookup"><span data-stu-id="3a042-118">Enter a name for your schema.</span></span> <span data-ttu-id="3a042-119">Para carregar o arquivo de esquema, selecione o ícone de pasta ao lado da caixa **Esquema**.</span><span class="sxs-lookup"><span data-stu-id="3a042-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span></span> <span data-ttu-id="3a042-120">Após a conclusão do processo de upload, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a042-120">After the upload process completes, select **OK**.</span></span>

    ![Captura de tela de "Adicionar esquema" com "Arquivo pequeno" realçado](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-to-8-mb-maximum"></a><span data-ttu-id="3a042-122">Adicione um arquivo de esquema com mais de 2 MB (até um máximo de 8 MB)</span><span class="sxs-lookup"><span data-stu-id="3a042-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span></span>

<span data-ttu-id="3a042-123">Essas etapas dependem do nível de acesso do contêiner de blob: **Público** ou **Sem acesso anônimo**.</span><span class="sxs-lookup"><span data-stu-id="3a042-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="3a042-124">**Para determinar esse nível de acesso**</span><span class="sxs-lookup"><span data-stu-id="3a042-124">**To determine this access level**</span></span>

1.  <span data-ttu-id="3a042-125">Abra o **Gerenciador de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="3a042-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="3a042-126">Em **Contêineres de Blob**, selecione o contêiner de blob que você deseja.</span><span class="sxs-lookup"><span data-stu-id="3a042-126">Under **Blob Containers**, select the blob container you want.</span></span> 

3.  <span data-ttu-id="3a042-127">Selecione **Segurança**, **Nível de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="3a042-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="3a042-128">Se o nível de acesso de segurança do blob é **Público**, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="3a042-128">If the blob security access level is **Public**, follow these steps.</span></span>

![Gerenciador de Armazenamento do Azure, com "Contêineres de Blob", "Segurança" e "Público" realçados](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="3a042-130">Carregue o esquema na conta de armazenamento e copie o URI.</span><span class="sxs-lookup"><span data-stu-id="3a042-130">Upload the schema to your storage account, and copy the URI.</span></span>

    ![Conta de armazenamento com o URI realçado](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="3a042-132">Selecione o **arquivo grande** em **Adicionar Esquema** e forneça o URI na caixa de texto **URI de Conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="3a042-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span></span>

    ![Esquemas, com o botão "Adicionar" e "Arquivo grande" realçados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="3a042-134">Se o nível de acesso da segurança do blob é **Sem acesso anônimo**, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="3a042-134">If the blob security access level is **No anonymous access**, follow these steps.</span></span>

![Gerenciador de Armazenamento do Azure, com "Contêineres de Blob", "Segurança" e "Sem acesso anônimo" realçados](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="3a042-136">Carregue o esquema na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3a042-136">Upload the schema to your storage account.</span></span>

    ![Conta de armazenamento](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="3a042-138">Gere uma Assinatura de Acesso Compartilhado para o esquema.</span><span class="sxs-lookup"><span data-stu-id="3a042-138">Generate a shared access signature for the schema.</span></span>

    ![Conta de armazenamento com a guia assinaturas de acesso compartilhado realçada](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="3a042-140">Escolha **Arquivo grande** em **Adicionar Esquema** e forneça o URI da Assinatura de Acesso Compartilhado na caixa de texto **URI de Conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="3a042-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span></span>

    ![Esquemas, com o botão "Adicionar" e "Arquivo grande" realçados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="3a042-142">Na folha **Esquemas** da conta de integração, você deve ver o esquema recém-adicionado.</span><span class="sxs-lookup"><span data-stu-id="3a042-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Sua conta de integração com "Esquemas" e o novo esquema realçados](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="3a042-144">Editar esquemas</span><span class="sxs-lookup"><span data-stu-id="3a042-144">Edit schemas</span></span>

1. <span data-ttu-id="3a042-145">Escolha o bloco **Esquemas**.</span><span class="sxs-lookup"><span data-stu-id="3a042-145">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="3a042-146">Após a folha **Esquemas** se abrir, selecione o esquema que deseja editar.</span><span class="sxs-lookup"><span data-stu-id="3a042-146">After the **Schemas** blade opens, select the schema that you want to edit.</span></span>

3. <span data-ttu-id="3a042-147">Na folha **Esquemas**, selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="3a042-147">On the **Schemas** blade, choose **Edit**.</span></span>

    ![Folha Esquemas](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="3a042-149">Selecione o arquivo de esquema que você deseja editar e, em seguida, selecione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="3a042-149">Select the schema file that you want to edit, then select **Open**.</span></span>

    ![Arquivo de esquema aberto para edição](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="3a042-151">O Azure mostrará uma mensagem informando que o esquema foi carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="3a042-151">Azure shows a message that the schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="3a042-152">Excluir esquemas</span><span class="sxs-lookup"><span data-stu-id="3a042-152">Delete schemas</span></span>

1. <span data-ttu-id="3a042-153">Escolha o bloco **Esquemas**.</span><span class="sxs-lookup"><span data-stu-id="3a042-153">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="3a042-154">Após a folha **Esquemas** se abrir, selecione o esquema que deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="3a042-154">After the **Schemas** blade opens, select the schema you want to delete.</span></span>

3. <span data-ttu-id="3a042-155">Na folha **Esquemas**, selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="3a042-155">On the **Schemas** blade, choose **Delete**.</span></span>

    ![Folha Esquemas](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="3a042-157">Clique em **Sim** para confirmar que deseja excluir o esquema selecionado.</span><span class="sxs-lookup"><span data-stu-id="3a042-157">To confirm that you want to delete the selected schema, choose **Yes**.</span></span>

    ![Mensagem de confirmação "Excluir esquema"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="3a042-159">Na folha **Esquemas**, a lista de esquemas será atualizada e não incluirá mais o esquema excluído.</span><span class="sxs-lookup"><span data-stu-id="3a042-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span></span>

    ![Conta de integração com "Esquemas" realçado](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="3a042-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3a042-161">Next steps</span></span>
* <span data-ttu-id="3a042-162">[Saiba mais sobre o Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o Enterprise Integration Pack").</span><span class="sxs-lookup"><span data-stu-id="3a042-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span></span>  

