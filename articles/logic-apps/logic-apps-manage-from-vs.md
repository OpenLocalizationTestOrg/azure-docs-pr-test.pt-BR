---
title: "aplicativos de lógica de aaaManage no Visual Studio - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Gerenciar aplicativos lógicos e outros ativos do Azure com o Visual Studio Cloud Explorer"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>Gerenciar os aplicativos lógicos com o Visual Studio Cloud Explorer

Embora hello [portal do Azure](https://portal.azure.com/) oferece uma ótima maneira de você toodesign e gerenciar os aplicativos lógicos do Azure, você pode usar o Gerenciador de nuvem do Visual Studio para o gerenciamento de vários ativos do Azure, incluindo aplicativos lógicos. O Visual Studio Cloud Explorer lhe permite procurar, gerenciar, editar e baixar aplicativos lógicos publicados. As tarefas de gerenciamento incluem habilitar, desabilitar e visualizar o histórico de execução. 

Antes de acessar e gerenciar seus aplicativos lógicos no Visual Studio, instale e configure essas ferramentas do Visual Studio para Aplicativos Lógicos do Azure. 

## <a name="prerequisites"></a>Pré-requisitos

* [Visual Studio 2015 ou Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [SDK mais recente do Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou superior)
* [Gerenciador de Nuvem do Visual Studio](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* Web toohello de acesso ao usar o designer incorporado Olá

## <a name="install-visual-studio-tools-for-logic-apps"></a>Instalar ferramentas do Visual Studio para Aplicativos Lógicos

Depois de instalar os pré-requisitos do hello, baixar e instalar as ferramentas de aplicativos do hello Azure lógica para o Visual Studio.

1. Abra o Visual Studio. Em Olá **ferramentas** menu, selecione **extensões e atualizações**.
2. Expanda Olá **Online** categoria para que você pode pesquisar online na Olá Galeria do Visual Studio.
3. Procure por **Aplicativos Lógicos** até encontrar as **Ferramentas de Aplicativos Lógicos do Azure para Visual Studio**.
4. toodownload e extensão de saudação de instalação, clique em **baixar**.
5. Reinicie o Visual Studio após a instalação.

> [!NOTE]
> Olá toodownload ferramentas de aplicativos de lógica do Azure para Visual Studio ir diretamente, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>Procurar aplicativos lógicos no Cloud Explorer

1.  tooopen Cloud Explorer no hello **exibição** menu, escolha **Cloud Explorer**.
2.  Navegue para o aplicativo lógico, por grupo de recursos ou tipo de recurso. 

    * Se você procurar pelo tipo de recurso, selecione sua assinatura do Azure, expanda Olá **aplicativos lógicos** seção e, em seguida, selecione o aplicativo lógico. 
    * Se você procurar pelo grupo de recursos, expanda Olá grupo de recursos que tem sua lógica de aplicativo e selecione o aplicativo lógico.

    tooview comandos para seu aplicativo de lógica, com o botão direito seu aplicativo lógico tanto na parte inferior de saudação do Cloud Explorer, escolha Olá **ações** menu.

    ![Navegar para o aplicativo lógico](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>Editar o aplicativo lógico com o Designer de Aplicativos Lógicos

Do Pesquisador de objetos de nuvem, você pode abrir um aplicativo implantado no momento de lógica de Olá designer mesmo que você usa no hello portal do Azure. 

* tooedit seu aplicativo lógico, no Pesquisador de objetos de nuvem, seu aplicativo de lógica e selecione **abrir com o Editor de lógica de aplicativo**. 

* toopublish seu toohello atualizações de nuvem, escolha **publicar**. 

* toostart uma nova execução, escolha **disparador executar**.

![Designer de Aplicativos Lógicos](./media/logic-apps-manage-from-vs/designer.png)

No designer de hello, você também pode **baixar** um aplicativo lógico. Essa ação automaticamente parametriza definição de aplicativo hello lógica e salva a definição de saudação como um modelo de implantação do Gerenciador de recursos do Azure. Você pode adicionar este projeto de grupo de recursos do Azure de tooyour de modelo de implantação.

## <a name="browse-your-logic-app-run-history"></a>Procurar o histórico de execução do aplicativo lógico

Olá tooview executar histórico para seu aplicativo lógico, seu aplicativo de lógica e selecione **histórico de execução de abrir**. tooreorder seu histórico de execução com base em qualquer cabeçalho de coluna Olá propriedades Olá mostrado, selecione.

![Histórico da execução](media/logic-apps-manage-from-vs/runs.png)

Olá tooshow histórico para uma instância de execução para que você pode rever Olá executar resultados, inclusive entradas hello e saídas de cada etapa, clique duas vezes em uma saudação executar instâncias.

![Resultados do histórico de execução, entradas e saídas de etapas](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>Próximas etapas

* [Criar seu primeiro aplicativo lógico](logic-apps-create-a-logic-app.md)
* [Criar, compilar e implantar aplicativos lógicos no Visual Studio](logic-apps-deploy-from-vs.md)
* [Veja exemplos e cenários comuns](logic-apps-examples-and-scenarios.md)
* [Vídeo: Automatizar processos de negócios com os Aplicativos Lógicos do Azure](http://channel9.msdn.com/Events/Build/2016/T694)
* [Vídeo: integrar seus sistemas com os Aplicativos Lógicos do Azure](http://channel9.msdn.com/Events/Build/2016/P462)
