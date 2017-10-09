---
title: "aaaCreate seu primeiro fluxo de trabalho entre os serviços de nuvem - Azure lógica de aplicativos e aplicativos de nuvem | Microsoft Docs"
description: "Automatizar os processos de negócios para os cenários de integração de sistemas e integração de aplicativos empresariais (EAI) criando e executando fluxos de trabalho no Aplicativo Lógico do Azure"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "fluxo de trabalho, aplicativos de nuvem, serviços de nuvem, processos de negócios, integração de sistemas, integração de aplicativos empresariais, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>Criar seu primeiro aplicativo de lógica de processos do fluxo de trabalho tooautomate entre aplicativos de nuvem e os serviços de nuvem

Sem escrever nenhum código, você pode automatizar os processos de negócios mais fácil e rapidamente quando cria e executa os fluxos de trabalho com o [Aplicativo Lógico do Azure](logic-apps-what-are-logic-apps.md). Este primeiro exemplo mostra como toocreate um fluxo de trabalho de aplicativo lógica básica que verifica um RSS feed para o novo conteúdo em um site. Quando novos itens são exibidos no feed do site hello, Olá lógica aplicativo envia email de uma conta do Outlook ou Gmail.

toocreate e executar um aplicativo lógico, é necessário estes itens:

* Uma assinatura do Azure. Se você não tiver uma assinatura, poderá [iniciar com uma conta gratuita do Azure](https://azure.microsoft.com/free/). Caso contrário, você pode [inscrever-se para uma assinatura Pré-paga](https://azure.microsoft.com/pricing/purchase-options/).

  Sua assinatura do Azure é usada para a cobrança de uso do aplicativo lógico. Saiba como a [medição de uso](../logic-apps/logic-apps-pricing.md) e os [preços](https://azure.microsoft.com/pricing/details/logic-apps) funcionam para os Aplicativos Lógicos do Azure.

Além disso, este exemplo requer estes itens:

* Uma conta do Gmail, Office 365 Outlook ou Outlook.com

    > [!TIP]
    > Se você tiver uma [conta da Microsoft](https://account.microsoft.com/account) pessoal, terá uma conta do Outlook.com. Caso contrário, se tiver uma conta corporativa ou de estudante do Azure, terá uma conta do **Outlook do Office 365**.

* Tooa um link RSS do site feed. Este exemplo usa Olá [RSS feed histórias superiores do site do CNN.com Olá](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>Adicionar um gatilho que inicia o fluxo de trabalho

Um [ *gatilho* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é um evento que inicia o fluxo de trabalho do aplicativo de lógica e é Olá primeiro item que precisa de seu aplicativo lógico.

1. Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure").

2. No menu à esquerda do hello, escolha **novo** > **integração corporativa** > **aplicativo lógico** conforme mostrado aqui:

     ![Portal do Azure, Novo, Enterprise Integration, Aplicativo Lógico](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > Você também pode escolher **novo**, em seguida, na caixa de pesquisa hello, digite `logic app`, e pressione Enter. Então, escolha **Aplicativo Lógico** > **Criar**.

3. Nomeie seu aplicativo lógico e selecione sua assinatura do Azure. Agora, crie ou selecione um grupo de recursos do Azure, o que ajuda a organizar e gerenciar os recursos do Azure afins. Por fim, selecione a localização do datacenter Olá para hospedar seu aplicativo lógico. Quando você estiver pronto, escolha **Pin toodashboard** e **criar**.

     ![Detalhes do aplicativo lógico](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > Quando você seleciona **toodashboard Pin**, seu aplicativo lógico será exibido no saudação do painel do Azure após a implantação e é aberto automaticamente. Se seu aplicativo lógico não aparecerá no painel do hello, Olá **todos os recursos** lado a lado, escolha **consulte mais**e selecione o aplicativo lógico. Ou, no menu à esquerda do hello, escolha **mais serviços**. Em **Enterprise Integration**, escolha **Aplicativos Lógicos** e selecione seu aplicativo lógico.

4. Quando você abre o aplicativo lógico para Olá primeira vez, Olá lógica de aplicativo Designer mostra modelos que você pode usar tooget iniciado. Por ora, escolha **Aplicativo Lógico em Branco** para poder compilar seu aplicativo lógico do zero.

    Olá lógica de aplicativo Designer é aberto e mostra os serviços disponíveis e *gatilhos* que você pode usar em seu aplicativo lógico.

5. Na caixa de pesquisa hello, digite `RSS`e selecione esse gatilho: **RSS - quando um item do feed é publicado** 

    ![Gatilho do RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. Insira o link de saudação para RSS feed do site de saudação do que você deseja tootrack. 

     Você também pode alterar a **Frequência** e o **Intervalo**. 
     Essas configurações determinam a frequência com que o aplicativo lógico verifica se há novos itens e retorna todos os itens encontrados durante esse período de tempo.

     Neste exemplo, vamos verificar todos os dias para principais histórias postadas site CNN toohello.

     ![Configurar um gatilho com o RSS feed, frequência e intervalo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. Salve seu trabalho agora. (Na barra de comando designer hello, escolha **salvar**.)

   ![Salve seu aplicativo lógico](media/logic-apps-create-a-logic-app/save-logic-app.png)

   Quando você salvar, seu aplicativo lógico fica ativo, mas no momento, seu aplicativo lógico só verificará se há novos itens no hello especificado RSS feed. 
   toomake Este exemplo mais útil, que adicionamos uma ação que executa o aplicativo lógico após o disparador é acionado.

## <a name="add-an-action-that-responds-tooyour-trigger"></a>Adicione uma ação que responde tooyour gatilho

Uma [*ação*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é uma tarefa executada pelo fluxo de trabalho do aplicativo lógico. Depois de adicionar um aplicativo de lógica do gatilho tooyour, você pode adicionar operações de tooperform uma ação com dados gerados por que o disparador. Para nosso exemplo, agora é adicionar uma ação que envia email quando novos itens são exibidos no feed de RSS do site hello.

1. No designer de hello, sob o disparador, escolha **nova etapa** > **adicionar uma ação** conforme mostrado aqui:

   ![Adicionar uma ação](media/logic-apps-create-a-logic-app/add-new-action.png)

   Olá designer mostra [conectores disponíveis](../connectors/apis-list.md) para que você possa selecionar tooperform uma ação quando o disparador é acionado.

2. Com base na sua conta de email, siga as etapas de saudação para Outlook ou Gmail.

   * email toosend na conta do Outlook, na caixa de pesquisa hello, digite `outlook`. Em **Serviços**, escolha **Outlook.com** para as contas pessoais da Microsoft ou escolha **Outlook do Office 365** para as contas corporativas ou de estudante do Azure. 
   Em **Ações**, selecione **Enviar um email**.

       ![Selecionar a ação "Enviar um email" do Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * toosend email da sua conta do Gmail, na caixa de pesquisa hello, digite `gmail`. 
   Em **Ações**, selecione **Enviar email**.

       ![Escolher "Gmail - enviar email"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. Quando você for solicitado a fornecer credenciais, entre Olá username e password para sua conta de email. 

4. Forneça detalhes de saudação para esta ação, como endereço de email de destino Olá e escolher parâmetros Olá Olá dados tooinclude no email Olá, por exemplo:

   ![Selecione os dados tooinclude no email](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    Portanto, se você escolheu o Outlook, seu aplicativo lógico poderá parecer com este exemplo:

    ![Aplicativo lógico concluído](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  Salve suas alterações. (Na barra de comando designer hello, escolha **salvar**.)

6. Agora, você pode executar manualmente seu aplicativo lógico para testar. Na barra de comando designer hello, escolha **executar**. Caso contrário, você pode deixar seu aplicativo lógico verificar Olá especificado feed RSS com base em agendamento Olá que você configurou.

   Se seu aplicativo lógico localiza novos itens, Olá lógica aplicativo envia email que inclui os dados selecionados. 
   Se novos itens não forem encontrado, o aplicativo lógico ignora ação Olá que envia email.

7. toomonitor e verifique se seu aplicativo de lógica de execução e disparar histórico, no menu aplicativo lógica, escolha **visão geral**.

   ![Monitorar e verificar a execução de seu aplicativo lógico e o histórico de gatilhos](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > Se você não encontrar dados Olá que você espera que, na barra de comandos hello, tente escolher **atualizar**.

   toolearn mais sobre o status do seu aplicativo lógica ou execute e disparar histórico ou toodiagnose sua lógica de aplicativo, consulte [solucionar seu aplicativo lógico](logic-apps-diagnosing-failures.md).

      > [!NOTE]
      > Seu aplicativo lógico continuará sendo executado até que você desative o aplicativo. tooturn desativar seu aplicativo agora, no menu aplicativo lógica, escolha **visão geral**. Na barra de comandos hello, escolha **desabilitar**.

Parabéns, você acabou de configurar e executar seu primeiro aplicativo lógico básico. Você também aprendeu como é fácil criar fluxos de trabalho que automatizam os processos e integram os aplicativos e serviços de nuvem - tudo sem código.

## <a name="manage-your-logic-app"></a>Gerenciar seu aplicativo lógico

toomanage seu aplicativo, você pode executar tarefas como verificar o status de saudação, editar, exibir o histórico, desativar ou excluir o aplicativo lógico.

1. Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure").

2. No menu à esquerda do hello, escolha **mais serviços**. Em **Enterprise Integration**, escolha **Aplicativos Lógicos**. Selecione seu aplicativo lógico. 

   No menu de aplicativo do hello lógica, você pode encontrar essas tarefas de gerenciamento de aplicativo lógica:

   |Tarefa|Etapas| 
   |:---|:---| 
   | Exibir o status, histórico de execução e informações gerais de seu aplicativo| Escolha **Visão Geral**.| 
   | Editar seu aplicativo | Escolha **Designer de Aplicativos Lógicos**. | 
   | Exibir a definição JSON do fluxo de trabalho de seu aplicativo | Escolha **Exibir Código do Aplicativo Lógico**. | 
   | Exibir as operações executadas em seu aplicativo lógico | Escolha **Log de atividades**. | 
   | Exibir as antigas versões de seu aplicativo lógico | Escolha **Versões**. | 
   | Desativar temporariamente seu aplicativo | Escolha **visão geral**, em seguida, na barra de comandos hello, escolha **desabilitar**. | 
   | Excluir seu aplicativo | Escolha **visão geral**, em seguida, na barra de comandos hello, escolha **excluir**. Insira o nome do seu aplicativo lógico e escolha **Excluir**. | 

## <a name="get-help"></a>Obter ajuda

tooask perguntas, responder às perguntas e saber quais outros aplicativos do Azure lógica os usuários estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Próximas etapas

*  [Adicionar condições e executar fluxos de trabalho](../logic-apps/logic-apps-use-logic-app-features.md)
*    [Modelos de aplicativos lógicos](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [Criar aplicativos lógicos a partir dos modelos do Azure Resource Manager](../logic-apps/logic-apps-arm-provision.md)
