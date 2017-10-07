---
title: "aaaManaging sua máquina virtual da imagem no hello Azure Marketplace | Microsoft Docs"
description: "Guia detalhado sobre como toomanage sua máquina virtual da imagem no hello Azure Marketplace após a publicação inicial"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>Guia de após a produção para a máquina virtual oferece em hello Azure Marketplace
Este artigo explica como você pode atualizar uma oferta de máquina virtual ao vivo em hello Azure Marketplace. Ele orienta você pelo processo de saudação da adição de um ou mais novo SKUs tooan oferta existente. Ele também orienta você pelo processo de saudação de remoção de uma oferta de máquina virtual ao vivo ou SKU da saudação Marketplace.

Depois de um oferta/SKU é testado no hello [portal do Azure](http://portal.azure.com), você não pode alterar Olá caixas de texto a seguir:

* **Identificador de oferta**: no hello publicação portal, vá muito**máquinas virtuais** e selecione sua oferta. Em seguida, clique em **IMAGENS DA VM** > **Identificador da oferta**.
* **Identificador de SKU**: no hello publicação portal, vá muito**máquinas virtuais** e selecione sua oferta. Em seguida, clique em **SKUS** > **Adicionar uma SKU**.
* **Namespace do publicador**: no hello publicação portal, vá muito**máquinas virtuais** > **passo a passo** > **Conte-nos sobre sua empresa** (localizado em "Etapa 2 registrar sua empresa") > **publicador Namespace** > **Namespace**.

Após Olá oferta/SKU está listado no hello [Marketplace](http://azure.microsoft.com/marketplace), você não pode alterar Olá caixas de texto a seguir:

* **Identificador de oferta**: no hello publicação portal, vá muito**máquinas virtuais** e selecione sua oferta. Em seguida, clique em **IMAGENS DA VM** > **Identificador da oferta**.
* **Identificador de SKU**: no hello publicação portal, vá muito**máquinas virtuais** e selecione sua oferta. Em seguida, clique em **SKUS** > **Adicionar uma SKU**.
* **Namespace do publicador**: no hello publicação portal, vá muito**máquinas virtuais** > **passo a passo** > **Conte-nos sobre sua empresa** (localizado em "Etapa 2 registrar") **Publicador Namespace** > **Namespace**.
* **Portas**: no hello publicação portal, vá muito**máquinas virtuais** e selecione sua oferta. Em seguida, clique em **IMAGENS DA VM** > **Abrir Portas**.
* **Alteração de preços das SKUs listadas**
* **Alteração do modelo de cobrança das SKUs listadas**
* **Remoção de regiões de cobrança de SKUs listados**
* **Contagem de SKU (s) listados de disco de dados de alteração de saudação**

## <a name="update-hello-technical-details-of-a-sku"></a>Atualizar detalhes técnicos de saudação de uma SKU
tooadd um novo toohello de versão listadas SKU e republicar a sua oferta, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **imagens da VM** guia.
4. Em Olá **SKUs** seção, localize Olá SKU que você deseja tooupdate.
5. Adicionar um novo número de versão para Olá SKU e clique em Olá  **+**  botão. versão nova do Hello deve estar em um formato X.Y.Z, onde X, Y e Z são números inteiros. As alterações de versão só devem ser incrementais.
6. Em Olá **URL do VHD de sistema operacional** caixa, insira a assinatura de acesso compartilhado Olá URI criado para o VHD do sistema operacional hello e salvar alterações de saudação.

   > [!IMPORTANT]
   > Você não pode incrementar/diminuir a contagem de disco de dados de saudação de uma SKU listada. É necessário toocreate um SKU novo nesse caso. Para obter orientações detalhadas, consulte a seção toohello [adicionar um SKU de novo em uma oferta listado](#add-a-new-sku-under-a-listed-offer).
   >
   >
7. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

    ![Imagens da VM](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>Atualizar os detalhes de não-Olá de uma oferta ou uma SKU
Você pode atualizar Olá sem conhecimento técnico (marketing, legal, suporte, categorias) detalhes de sua oferta ao vivo ou SKU no hello Marketplace.

### <a name="update-hello-offer-description-and-logos"></a>Descrição da atualização de oferta hello e logotipos
Olá tooupdate detalhes da oferta e republicar a sua oferta, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **MARKETING** guia.
4. Clique em **Inglês (EUA)**.
5. Clique em Olá **detalhes** guia. Em Olá **descrição** seção, atualização Olá oferta **título**, **resumo**, e **resumo longo** e salvar as alterações de saudação.

   > [!NOTE]
   > Quando você atualiza os detalhes de SKU Olá, esteja ciente dessas restrições: 
   * Não insira o texto duplicado para descrição da oferta hello e uma descrição de SKU de saudação.
   * Não insira o texto duplicado para o título SKU de saudação e resumo longo de oferta de saudação. 
   * Não insira o texto duplicado para o título SKU de saudação e o resumo de oferta de saudação.
   >
   >

    ![Detalhes](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. Em Olá **LOGOTIPOS** seção Olá **detalhes** guia, atualize os logotipos da saudação. Certifique-se de logotipos Olá sigam Olá [diretrizes do Azure Marketplace](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).

   > [!NOTE]
   > O ícone Hero é opcional. Você pode escolher não tooupload um ícone herói. No entanto, depois que um ícone herói é carregado, não há nenhum toodelete provisão de saudação portal de publicação. Siga Olá [diretrizes de ícone herói](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
   >
   >
7. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

    ![Logotipos](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>Atualizar a descrição do SKU Olá
Olá tooupdate SKU detalhes e republicar a sua oferta, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **MARKETING** guia.
4. Clique em **Inglês (EUA)**.
5. Clique em Olá **PLANOS** guia. Em Olá **SKUs** seção, atualize Olá SKU **título**, **resumo**, e **descrição** e salvar as alterações de saudação.

   > [!NOTE]
   > Quando você atualiza os detalhes de SKU Olá, esteja ciente dessas restrições: 
   * Não insira o texto duplicado para descrição da oferta hello e uma descrição de SKU de saudação. 
   * Não insira o texto duplicado para o título SKU de saudação e resumo longo de oferta de saudação. 
   * Não insira o texto duplicado para o título SKU de saudação e o resumo de oferta de saudação.
   >
   >
6. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

    ![Planos](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>Alterar os links existentes ou adicionar novos links
toochange os links existentes ou adicionar novos links e, em seguida, republicar a sua oferta, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **MARKETING** guia.
4. Clique em **Inglês (EUA)**.
5. Clique em Olá **LINKS** guia.
6. tooadd um novo link, em Olá **Links** seção, clique em **+ adicionar LINK**. Em Olá **Adicionar Link** caixa de diálogo caixa, insira o link Olá **título** e **URL** e salvar as alterações de saudação. Você pode inserir qualquer link que contenha informações que possam ajudar os clientes.
7. tooupdate ou excluir um link existente, selecione o link de saudação e clique Olá **editar** botão ou hello **excluir** botão.

   > [!NOTE]
   > Certifique-se de que os links de saudação que você inseriu nesta seção estão funcionando corretamente, porque esses links são validados durante o processo de solicitação de produção.
   >
   >
8. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

    ![Links](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![Adicionar Link](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>Alterar uma imagem de exemplo existente ou adicionar uma nova imagem de exemplo
toochange uma amostra existente da imagem ou adicionar novas imagens de exemplo e, em seguida, republicar a sua oferta, siga estas etapas:

> [!NOTE]
> Imagem de apenas uma amostra é exibida na Olá [portal do Azure](https://portal.azure.com).
>
>

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **MARKETING** guia.
4. Clique em **Inglês (EUA)**.
5. Clique em Olá **imagens de amostra** guia.
6. tooadd uma nova imagem de exemplo no hello **imagens de amostra** seção, clique em **carregar A nova imagem** e salvar as alterações de saudação.

   > [!NOTE]
   > Incluir uma imagem de exemplo é opcional.
   >
7. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

    ![Exemplo de Imagens](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>Atualizar conteúdo legal Olá
tooupdate Olá conteúdo legal e republicar a sua oferta, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **MARKETING** guia.
4. Clique em **Inglês (EUA)**.
5. Clique em Olá **legais** guia. Em Olá **legais** seção, atualize suas políticas/termos de uso. Digite ou cole Olá políticas/condições em Olá **os termos de uso** caixa e salvar as alterações de saudação.
6. limite de caracteres de saudação de termos legais de saudação de uso é 1 milhão de caracteres.
7. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

    ![Legal](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>Atualizar informações de suporte de saudação
Olá tooupdate informações de suporte e republicar a sua oferta, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **suporte** guia.
4. Em Olá **entre em contato com engenharia** seção detalhes de contato engenharia atualização hello. Esses detalhes são usados para comunicação interna entre o parceiro de saudação e Microsoft somente.
5. Em hello **atendimento ao cliente** seção, atualizar detalhes de contato de suporte hello e hello **suporte URL**. Esses detalhes são usados para comunicação interna entre o parceiro de saudação e Microsoft somente.

   > [!NOTE]
   > Se você quiser tooprovide apenas o suporte de email, digite um número de telefone fictício no hello **atendimento ao cliente** seção. Nesse caso, Olá email fornecido é usado em vez disso.
   >
   >
6. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

    ![Suporte](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>Categorias de saudação de atualização
Olá tooupdate categorias seção para sua oferta e republicam a sua oferta, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **categorias** guia.
4. Em Olá **categorias** seção, atualizar Olá categorias para sua oferta e salvar as alterações de saudação. Você pode escolher as categorias de toofive para Galeria do Azure Marketplace hello.
5. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
6. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

    ![Categorias](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>Adicionar uma nova SKU em uma oferta listada
tooadd um SKU de novo na oferta ao vivo, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **SKUS** guia. Em seguida, clique em **Adicionar uma SKU**. 
4. Na caixa de diálogo hello, insira um **identificador SKU** em minúsculas. Selecione Olá **traga seu próprio modelo de cobrança de licença (BYOL)** caixa de seleção se você quiser toopublish Olá SKU novo com um modelo de cobrança BYOL. Caso contrário, desmarque a caixa de seleção de saudação. Clique em toocreate marca de escala Olá um SKU de novo. Se você não escolheu o modelo de cobrança Olá BYOL, o modelo de cobrança de saudação é definido automaticamente toohourly. Se quiser que a avaliação gratuita de 30 dias de saudação para o modelo de cobrança por hora hello, selecione **um mês** para **é uma avaliação gratuita disponível?** Caso contrário, selecione **Sem Avaliação**. (**é uma avaliação gratuita disponível?**  será exibida apenas se você não selecionou BYOL enquanto criando Olá SKU novo.)

   > [!IMPORTANT]
   > **Ocultar este SKU de saudação Marketplace porque sempre deve ser comprado por meio de um modelo de solução** devem ser **Sim** *somente* se for aprovado para publicação de um modelo de solução. Caso contrário, essa opção sempre deverá ser marcada como **Não**.
   >
   >
4. No menu de Olá Olá esquerda, clique em Olá **imagens da VM** guia e descobrir Olá SKU novo que você criou.
5. tooset até Olá SKU novo, consulte [obter a certificação de sua imagem VM](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) para obter orientação.
6. tooadd material de marketing Olá SKU novo, consulte [Marketplace fornecer conteúdo de marketing](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
7. tooadd informações de preços para Olá SKU novo, consulte [definir preços](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).
8. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

    ![SKUs](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![Adicionar uma SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>Alterar a contagem do disco de dados Olá para um SKU listado
Você não pode incrementar/diminuir a contagem de disco de dados de saudação de uma SKU listada. É necessário toocreate um SKU novo nesse caso. Para obter orientações detalhadas, consulte a seção toohello [adicionar um SKU de novo em uma oferta listado](#add-a-new-sku-under-a-listed-offer).

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>Excluir uma oferta listada do hello Marketplace
Vários aspectos necessário toobe resolvido no caso de saudação de uma solicitação de tooremove uma oferta ao vivo. diretrizes de tooget da saudação suporte team tooremove uma oferta listada da saudação Marketplace, siga estas etapas:

1. Gerar um tíquete de suporte Olá [criar um incidente](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) página.

2. Selecione o **Tipo de problema** como **Gerenciando ofertas** e selecione a **Categoria** como **Modificando uma oferta e/ou uma SKU já em produção**.
3. Envie solicitação de saudação.

a equipe de suporte Olá orienta você pelo processo de exclusão de oferta/SKU de saudação.

> [!NOTE]
> Você sempre pode excluir oferta Olá enquanto ele está em status rascunho (mas não preparo ou produção). Em Olá **histórico** , clique em **Descartar rascunho**.
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>Excluir um SKU listado do hello Marketplace
toodelete uma SKU listada do hello Marketplace, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).

2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No painel Olá Olá esquerda, clique em Olá **SKUS** guia.
4. Selecione Olá SKU que você deseja toodelete e clique em Olá **excluir** botão.
5. Vá toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish Olá oferta no hello Marketplace.
6. Após a oferta de saudação é republicada em Olá Marketplace, Olá SKU é excluído do hello Marketplace e Olá portal do Azure.

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>Excluir a versão atual de saudação de uma SKU listada do hello Marketplace
versão atual do hello toodelete de uma SKU listada do hello Marketplace, siga estas etapas: 

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).

2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **imagens da VM** guia.
4. Selecione Olá SKU cujo atual versão você deseja toodelete e clique em Olá **excluir** botão.
5. Vá toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish Olá oferta no hello Marketplace.
6. Depois de oferta Olá obtém republicada no hello Marketplace, Olá versão atual do hello SKU listado é excluído da saudação Marketplace e Olá portal do Azure. Olá SKU é revertida versão anterior do tooits.

## <a name="revert-hello-listing-price-tooproduction-values"></a>Reverter Olá listando os valores de tooproduction de preço
valores de tooproduction do preço de lista de saudação toorevert, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).
2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **preços** guia.
4. Selecione uma região cujos preços que você deseja tooreset.

    ![Regiões de preço](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. Para SKUs com um modelo de cobrança por hora, redefina preços Olá para todos os núcleos hello como estão na produção para a região selecionada da saudação. Para SKUs com um modelo de cobrança BYOL, verifique Olá SKU disponível na região hello, selecionando a caixa de seleção Olá Olá SKU no hello **EXTERNALLY-LICENSED (BYOL) SKU disponibilidade** seção.

    ![Modelos de preços](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. Clique em **DEFINIR AUTOMATICAMENTE O PREÇO PARA OUTROS MERCADOS COM BASE NOS PREÇOS PARA OS ESTADOS UNIDOS**.

   > [!NOTE]
   > rótulo do botão Olá pode ser diferente dependendo da região de saudação que você selecionar. Porque estamos selecionado dos Estados Unidos, botão Olá é rotulado **AUTOPRICE outros MERCADOS com base em ON preços em Estados Unidos**.
   >
   >

    ![Preço automático](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. Na página 1 do Assistente de Autoprice hello, escolha o mercado base hello e clique em Olá **seta** botão.

    ![Mercado de base](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. Na página 2, escolha planos de serviço e metros (núcleos) e clique em Olá **seta** botão.

    ![Planos e medidores de serviço](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. Na página 3, clique em **ativar/desativar todas as** tooselect todas as regiões. Outra opção é marcar manualmente as caixas de seleção para regiões específicas. Clique em Olá **seta** botão.

    ![Escolher mercados](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. Na página 4, examine as taxas de câmbio hello e clique em **concluir**. Assistente de saudação redefine Olá preços seleções de tooyour de acordo.

11. Em Olá **preços** , clique em **Exibir resumo e alterações**.
    Para **Exibir Versão**, selecione **Rascunho**; para **Comparar com**, selecione **Produção**. Se você não percebem nenhuma diferença de preços, preços Olá revertido toohello valores de produção com êxito.

    ![Exibir resumo e alterações](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
13. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

## <a name="revert-hello-billing-model-tooproduction-values"></a>Reverter Olá valores tooproduction do modelo de cobrança
toorevert Olá cobrança tooproduction valores do modelo, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).

2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **SKUS** guia.
4. Clique em Olá **editar** modelo de cobrança de saudação do botão toorevert. Na janela de saudação que é aberta, selecione ou desmarque Olá **licenciamento e cobrança é feito externamente do Azure (também conhecido como trazer sua própria licença)** caixa de seleção.

    ![Editar cobrança](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. Siga as etapas de hello "Olá Revert listando os valores de tooproduction preço" neste artigo.
6. Vá toohello **publicar** guia e, em seguida, clique em **tooSTAGING PUSH**. Para obter orientações detalhadas sobre como testar sua oferta no ambiente de preparo de hello, consulte [testar sua oferta VM para Olá Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Depois que você testou sua oferta no preparo, acesse toohello **publicar** guia Olá portal de publicação. Clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>Reverter a configuração de visibilidade de saudação de um valor de produção de toohello SKU listado
configuração de visibilidade de saudação toorevert de um valor de produção de toohello SKU listado, siga estas etapas:

1. Entrar toohello [publicação portal](https://publish.windowsazure.com).

2. Vá toohello **máquinas virtuais** guia e selecione sua oferta.
3. No menu de Olá Olá esquerda, clique em Olá **SKUS** guia.
4. Selecione o SKU e reverter a configuração de visibilidade de saudação do valor do SKU toohello produção de hello.

    ![Visibilidade](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. Depois de terminar com alterações hello, clique em **SOLICITAR aprovação tooPUSH tooPRODUCTION** toorepublish sua oferta no hello Marketplace.

## <a name="see-also"></a>Consulte também
* [Introdução: Publicar uma oferta toohello Azure Marketplace](marketplace-publishing-getting-started.md)
* [Compreender o relatório de pagamento](marketplace-publishing-report-payout.md)
* [Alterar seu incentivo ao revendedor do Provedor de Soluções na Nuvem](marketplace-publishing-csp-incentive.md)
* [Solucionar problemas comuns de publicação no hello Marketplace](marketplace-publishing-support-common-issues.md)
* [Obtenha suporte como um editor](marketplace-publishing-get-publisher-support.md)
* [Criar uma imagem da VM local](marketplace-publishing-vm-image-creation-on-premise.md)
* [Criar uma máquina virtual executando o Windows no portal de visualização do Azure Olá](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
