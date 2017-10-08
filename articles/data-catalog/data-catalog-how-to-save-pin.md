---
title: "aaaSave pesquisas e ativos de dados de pin no catálogo de dados do Azure | Microsoft Docs"
description: "Como tooarticle realce recursos no catálogo de dados do Azure para salvar as fontes de dados e ativos de dados para uso posterior."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a>Salva pesquisas e fixa ativos de dados no Catálogo de Dados do Azure
## <a name="introduction"></a>Introdução
O Catálogo de Dados do Azure fornece recursos para descoberta de fontes de dados. Rapidamente pesquisar e filtrar as fontes de dados do hello catálogo toolocate e entender a finalidade pretendida, tornando-a como dados à direita do mais fácil de saudação de toofind para o trabalho de saudação à mão.

Mas se você precisar tooregularly trabalhar com hello mesmo dados? E se você e outros usuários regularmente contribuem toohello seu conhecimento mesmas fontes de dados no catálogo Olá? Nessas situações, tendo problema toorepeatedly Olá mesmo pesquisas podem ser ineficientes. É aqui que pesquisas salvas e ativos de dados fixos podem ajudar.

## <a name="saved-searches"></a>Pesquisas salvas
Uma pesquisa salva no Catálogo de Dados é uma definição de pesquisa reutilizável por usuário. Você pode definir uma pesquisa, inclusive os termos de pesquisa, as marcas e outros filtros e, em seguida, salvá-la. Você pode executar novamente a definição de pesquisa Olá salvada tooreturn posterior qualquer ativos de dados que correspondem a seus critérios de pesquisa.

### <a name="create-a-saved-search"></a>Criar uma pesquisa salva
toocreate uma pesquisa salva, Olá a seguir:
1. No portal do catálogo de dados do Azure de hello, na Olá **pesquisa atual** janela, clique em **salvar**. 

    ![Configurações da Pesquisa Atual, link Salvar](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. Insira critérios de pesquisa de saudação que você deseja tooreuse e, em seguida, clique em **salvar**.

    ![Configurações da Pesquisa Atual, nome da pesquisa salva](./media/data-catalog-how-to-save-pin/02-name.png)

3. Quando você for solicitado, insira um nome para a pesquisa salva de saudação. Escolha um nome que seja significativo e que descreve a saudação de ativos de dados que serão retornadas pela pesquisa de saudação.

### <a name="manage-saved-searches"></a>Gerenciar pesquisas salvas
Depois de salvar uma ou mais pesquisas, um **pesquisas salvas** opção é exibida embaixo Olá **pesquisa atual** caixa. Quando a saudação lista for expandida, todas as pesquisas salvas são exibidas.

 ![Lista de pesquisas salvas](./media/data-catalog-how-to-save-pin/03-list.png)

Proceda do seguinte hello:

* tooexecute uma pesquisa, selecione uma pesquisa salva na lista de saudação.

* tooview uma lista de opções de gerenciamento para uma pesquisa salva, clique em Olá nome de pesquisa toohello próxima seta.

    ![Opções para gerenciar as pesquisas salvas](./media/data-catalog-how-to-save-pin/04-managing.png)

* tooenter um novo nome para pesquisa de saudação salva, selecione **Renomear**. definição de pesquisa de saudação não é alterada.

* a pesquisa na lista, selecione Olá salvada tooremove **excluir**e, em seguida, confirme a exclusão de saudação.

* pesquisa de saudação salvada toomark como a pesquisa padrão, selecione **Salvar como padrão**. Se você executar uma pesquisa de "empty" na página de início do hello Data Catalog do Azure, o padrão de pesquisa é executada. Além disso, Olá pesquisa que está marcada como pesquisa de padrão de saudação é exibida na parte superior de saudação do hello **pesquisas salvas** lista.

### <a name="organizational-saved-searches"></a>Pesquisas organizacionais salvas
Todos os usuários na sua organização podem salvar pesquisas para uso próprio. Os administradores do catálogo de dados também podem salvar pesquisas para todos os usuários dentro da organização hello. Quando os administradores salvar uma pesquisa, eles serão apresentados com um **compartilhamento dentro da empresa Olá** opção. Saudação de compartilhamentos essa opção Salvar pesquisa para todos os usuários na organização Olá a seleção.

 ![Pesquisas organizacionais salvas](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>Ativos de dados fixos
Com pesquisas salvas, você pode salvar e reutilizar as definições de pesquisa. ativos de dados de saudação que são retornados pelas pesquisas Olá podem ser alterado ao longo do tempo como conteúdo de saudação de alteração de catálogo hello. Quando você fixa ativos de dados, você pode identificar explicitamente toomake de ativos de dados específicos-los mais fácil tooaccess sem a necessidade de toouse uma pesquisa.

A fixação de um ativo de dados é simples. lista de tooadd Olá dados ativos tooyour fixado, basta clicar em Olá **pin** ícone. Olá ícone é exibido no canto Olá Olá ativo lado a lado na exibição lado a lado de saudação e na coluna mais à esquerda Olá Olá o modo de exibição de lista no portal do catálogo de dados do Azure Olá.

![ícone de pino Olá ativo de dados](./media/data-catalog-how-to-save-pin/05-pinning.png)

Desafixar um ativo de dados é igualmente simples. Basta clicar Olá **Desafixar** ícone tootoggle Olá configuração ativo selecionado hello.

![ativo de dados Olá Desafixar ícone](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a>Olá seção Meus ativos
Olá inclui home page do portal do catálogo de dados um **ativos Meus** seção que exibe os ativos do usuário atual do toohello de interesse. Essa seção inclui os ativos fixos e as pesquisas salvas.

![Olá seção Meus ativos na home page do hello](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>Resumo
Catálogo de dados do Azure fornece recursos que tornam mais fácil fontes de dados de saudação toodiscover que for necessário, para que você e outros membros da organização podem gastar menos tempo procurando dados e a hora mais trabalhar com ele. As pesquisas salvas e os ativos de dados fixos aprimoram esses recursos principais para que os usuários possam facilmente identificar fontes de dados com as quais eles trabalham repetidamente.
