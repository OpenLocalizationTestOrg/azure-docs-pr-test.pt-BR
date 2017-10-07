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
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="5b7c3-103">Adicionar mapas para a transformação de dados XML</span><span class="sxs-lookup"><span data-stu-id="5b7c3-103">Add maps for XML data transform</span></span>

<span data-ttu-id="5b7c3-104">Enterprise integração usa mapas tootransform dados XML entre formatos.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-104">Enterprise integration uses maps tootransform XML data between formats.</span></span> <span data-ttu-id="5b7c3-105">Um mapa é um documento XML que define os dados de saudação em um documento que deve ser transformado em outro formato.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-105">A map is an XML document that defines hello data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="5b7c3-106">Por que usar mapas?</span><span class="sxs-lookup"><span data-stu-id="5b7c3-106">Why use maps?</span></span>

<span data-ttu-id="5b7c3-107">Suponha que você recebe regularmente B2B ordens ou notas fiscais de um cliente que usa o formato YYYMMDD Olá para datas.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses hello YYYMMDD format for dates.</span></span> <span data-ttu-id="5b7c3-108">No entanto, em sua organização, você armazenar datas no formato MMDDYYY hello.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-108">However, in your organization, you store dates in hello MMDDYYY format.</span></span> <span data-ttu-id="5b7c3-109">Você pode usar um mapa muito*transformação* formato de data YYYMMDD Olá em Olá MMDDYYY antes de armazenar os detalhes do pedido ou da fatura Olá em seu banco de dados de atividade do cliente.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-109">You can use a map too*transform* hello YYYMMDD date format into hello MMDDYYY before storing hello order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="5b7c3-110">Como faço para criar um mapa?</span><span class="sxs-lookup"><span data-stu-id="5b7c3-110">How do I create a map?</span></span>

<span data-ttu-id="5b7c3-111">Você pode criar projetos de integração do BizTalk com hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do enterprise Olá") para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-111">You can create BizTalk Integration projects with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="5b7c3-112">Então, será possível criar um arquivo de mapa de integração que permitirá visualizar itens de mapa entre dois arquivos de esquema XML.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="5b7c3-113">Após criar esse projeto, você terá um documento XSLT.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="5b7c3-114">Como adicionar um mapa?</span><span class="sxs-lookup"><span data-stu-id="5b7c3-114">How do I add a map?</span></span>

1. <span data-ttu-id="5b7c3-115">No portal do Azure de Olá, selecione **procurar**.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-115">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="5b7c3-116">Na caixa de pesquisa do filtro hello, digite **integração**, em seguida, selecione **contas de integração** Olá da lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-116">In hello filter search box, enter **integration**, then select **Integration Accounts** from hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="5b7c3-117">Selecione a conta de integração de Olá onde você deseja tooadd Olá mapa.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-117">Select hello integration account where you want tooadd hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="5b7c3-118">Selecione Olá **mapas** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-118">Select hello **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="5b7c3-119">Depois de abre a folha de mapas hello, escolha **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-119">After hello Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="5b7c3-120">Insira um **Nome** para o mapa.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="5b7c3-121">mapa de saudação tooupload de arquivo, escolha o ícone de pasta Olá Olá direita da saudação **mapa** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-121">tooupload hello map file, choose hello folder icon on hello right side of hello **Map** text box.</span></span> <span data-ttu-id="5b7c3-122">Após a conclusão do processo de carregamento de saudação, escolha **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-122">After hello upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="5b7c3-123">Depois que o Azure adiciona a conta de integração do hello mapa tooyour, você obterá uma mensagem na tela que mostra se o arquivo de mapa foi adicionado ou não.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-123">After Azure adds hello map tooyour integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="5b7c3-124">Depois que você receber essa mensagem, escolha Olá **mapas** lado a lado para que você possa exibir hello recentemente adicionado o mapa.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-124">After you get this message, choose hello **Maps** tile so you can view hello newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="5b7c3-125">Como editar um mapa?</span><span class="sxs-lookup"><span data-stu-id="5b7c3-125">How do I edit a map?</span></span>

<span data-ttu-id="5b7c3-126">Você deve carregar um novo arquivo de mapa com alterações Olá que desejar.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-126">You must upload a new map file with hello changes that you want.</span></span> <span data-ttu-id="5b7c3-127">Primeiro, você pode baixar mapa Olá para edição.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-127">You can first download hello map for editing.</span></span>

<span data-ttu-id="5b7c3-128">tooupload um novo mapa que substitui o mapa do hello existente, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-128">tooupload a new map that replaces hello existing map, follow these steps.</span></span>

1. <span data-ttu-id="5b7c3-129">Escolha Olá **mapas** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-129">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="5b7c3-130">Depois de abre a folha de mapas hello, selecione mapa de saudação que você deseja tooedit.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-130">After hello Maps blade opens, select hello map that you want tooedit.</span></span>

3. <span data-ttu-id="5b7c3-131">Em Olá **mapas** folha, escolha **atualização**.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-131">On hello **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="5b7c3-132">No selecionador de arquivo hello, selecione o arquivo de mapa de saudação que você deseja tooupload e selecione **abrir**.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-132">In hello file picker, select hello map file that you want tooupload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a><span data-ttu-id="5b7c3-133">Como um mapa de toodelete?</span><span class="sxs-lookup"><span data-stu-id="5b7c3-133">How toodelete a map?</span></span>

1. <span data-ttu-id="5b7c3-134">Escolha Olá **mapas** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-134">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="5b7c3-135">Depois de abre a folha de mapas hello, selecione mapa de saudação deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-135">After hello Maps blade opens, select hello map you want toodelete.</span></span>

3. <span data-ttu-id="5b7c3-136">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="5b7c3-137">Confirme que você deseja que o mapa de saudação toodelete.</span><span class="sxs-lookup"><span data-stu-id="5b7c3-137">Confirm that you want toodelete hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="5b7c3-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5b7c3-138">Next Steps</span></span>
* [<span data-ttu-id="5b7c3-139">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="5b7c3-139">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")  
* [<span data-ttu-id="5b7c3-140">Saiba mais sobre os contratos</span><span class="sxs-lookup"><span data-stu-id="5b7c3-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  
* [<span data-ttu-id="5b7c3-141">Saiba mais sobre transformações</span><span class="sxs-lookup"><span data-stu-id="5b7c3-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Saiba mais sobre as transformações de integração corporativa")  

