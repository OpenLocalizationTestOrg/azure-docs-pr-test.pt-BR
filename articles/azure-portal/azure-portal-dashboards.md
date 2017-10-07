---
title: "aaaCreate e compartilhar painéis de portal do Azure | Microsoft Docs"
description: "Este artigo explica como toocreate e editar painéis no hello portal do Azure."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a>Criar e compartilhar dashboards no hello portal do Azure
Você pode criar vários painéis e compartilhá-los com outras pessoas que tenham acesso tooyour Azure assinaturas.  Este artigo mostra Olá Noções básicas sobre criação, edição, publicação e gerenciamento de acesso toodashboards.

## <a name="create-a-dashboard"></a>Criar um painel
toocreate um dashboard, selecione Olá **novo painel** botão Avançar toohello atual do nome do painel.  

![criar painel](./media/azure-portal-dashboards/new-dashboard.png)

Essa ação cria um painel novo, vazio, privado e coloca você no modo de personalização onde é possível nomear seu painel e adicionar ou reorganizar blocos.  Nesse modo, Olá recolhível bloco Galeria leva para o menu de navegação à esquerda hello.  Olá Galeria lado a lado permite que você localize lado a lado para recursos do Azure de várias maneiras: você pode procurar por [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), por tipo de recurso, por [marca](../azure-resource-manager/resource-group-using-tags.md), ou por meio de pesquisa para o recurso por nome.  

![personalizar painel](./media/azure-portal-dashboards/customize-dashboard.png)

Adicione blocos arrastando e soltando na superfície do painel Olá onde desejar.

Há uma nova categoria chamada **Geral** para blocos que não estejam associados a um recurso específico.  Neste exemplo, podemos fixar o bloco de redução de saudação.  Use este painel de tooyour conteúdo personalizado tooadd lado a lado.  Olá bloco dá suporte a texto sem formatação, [sintaxe de Markdown](https://daringfireball.net/projects/markdown/syntax)e um conjunto limitado de HTML.  (Para segurança, você não pode fazer coisas como injetar `<script>` marcas ou usar um determinado elemento de estilo de CSS que possam interferir com o portal de saudação.) 

![adicionar markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a>Editar um painel
Depois de criar seu painel, você pode fixar blocos da Galeria de bloco de saudação ou representação de bloco de saudação de folhas. Vamos fixar a representação de saudação do nosso grupo de recursos. Você pode fixar ou durante a navegação Olá item ou na folha de grupo de recursos de saudação. Ambas as abordagens resultam em fixação de representação de bloco Olá Olá do grupo de recursos.

![PIN toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

Depois de fixar item hello, ele aparece no painel.

![exibir painel](./media/azure-portal-dashboards/view-dashboard.png)

Agora que temos um bloco de Markdown e um painel de toohello fixado do grupo de recursos, podemos redimensionar e reorganizar blocos Olá em um layout adequado.

Ao passar o mouse e selecionando "..." ou clicando duas vezes em um bloco, você pode ver todos os comandos de saudação contextuais para esse bloco. Por padrão, há dois itens:

1. **Desafixar do painel** – remove Olá bloco do painel Olá
2. **Personalizar** – entra no modo de personalização

![personalizar bloco](./media/azure-portal-dashboards/customize-tile.png)

Selecionando Personalizar, você pode redimensionar e reorganizar blocos. tooresize um bloco, selecione Olá novo tamanho no menu contextual do hello, conforme mostrado no Olá a imagem a seguir.

![redimensionar bloco](./media/azure-portal-dashboards/resize-tile.png)

Ou, se o bloco de saudação dá suporte a qualquer tamanho, você pode arrastar o tamanho do hello inferior direito toohello desejado.

![redimensionar bloco](./media/azure-portal-dashboards/resize-corner.png)

Depois de redimensionar blocos, exiba o painel de saudação.

![bloco de exibição](./media/azure-portal-dashboards/view-tile.png)

Quando terminar de personalizar um painel, basta selecionar Olá **feito personalizando** tooexit Personalizar modo ou com o botão direito e selecione **feito personalizando** Olá no menu de contexto.

## <a name="publish-a-dashboard-and-manage-access-control"></a>Publicar um painel e gerenciar o controle de acesso
Quando você cria um painel, é privado por padrão, o que significa que são Olá única pessoa pode vê-lo.  toomake-tooothers visíveis, use Olá **compartilhamento** Olá de botão aparece ao lado de outros comandos do painel.

![compartilhar painel](./media/azure-portal-dashboards/share-dashboard.png)

Você será solicitado toochoose que um assinatura e grupo de recursos para seu painel toobe publicado. tooseamlessly integrar painéis em ecossistema hello, implementamos painéis compartilhados como recursos do Azure (de modo que você não pode compartilhar digitando um endereço de email).  Acessar toohello informações exibidas pela maioria dos blocos de saudação no portal de saudação são administradas por [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md). Do ponto de vista do controle de acesso, os painéis compartilhados não são diferentes de uma máquina virtual ou de uma conta de armazenamento.  

Digamos que você tem uma assinatura do Azure e membros da equipe tiverem sido atribuídos a funções de saudação do **proprietário**, **Colaborador**, ou **leitor** de assinatura de saudação.  Os usuários que são proprietários ou colaboradores são capaz de toolist, exibir, criar, modificar ou excluir painéis em assinatura.  Os usuários que são leitores são capaz de toolist e exibir os painéis, mas não podem modificar ou excluí-los.  Usuários com acesso de leitor são painel compartilhado do tooa toomake capaz de edições locais, mas são não é possível toopublish server de back toohello essas alterações.  No entanto, eles podem fazer uma cópia privada de dashboard, Olá para seu próprio uso.  Como sempre, blocos individuais no painel de saudação impõem suas próprias regras de controle de acesso com base nos recursos de saudação corresponder a.  

Para sua conveniência, portal de saudação da publicação guias experiência em direção a um padrão de onde você coloca painéis em um grupo de recursos chamado **painéis**.  

![painel de publicação](./media/azure-portal-dashboards/publish-dashboard.png)

Você também pode escolher um grupo de recursos específico do painel tooa toopublish.  controle de acesso de saudação para esse painel faz a correspondência de controle de acesso de Olá Olá para grupo de recursos.  Os usuários que podem gerenciar recursos Olá desse grupo de recursos também têm acesso toohello painéis.

![publicar um grupo do painel tooresource](./media/azure-portal-dashboards/publish-to-resource-group.png)

Depois que o painel é publicado, Olá **compartilhamento + acesso** painel de controle será atualizar e mostram informações sobre o painel publicado hello, incluindo um link toomanage usuário acesso toohello painel de controle.  Isso inicia saudação padrão de controle de acesso baseado em função folha usada toomanage acesso para qualquer recurso do Azure.  Você pode sempre voltar toothis exibição selecionando **compartilhamento**.

![gerenciar o controle de acesso](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a>Próximas etapas
* toomanage recursos, consulte [recursos de gerenciamento Azure por meio do portal](../azure-resource-manager/resource-group-portal.md).
* toodeploy recursos, consulte [implantar recursos com modelos do Gerenciador de recursos e o portal do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).

