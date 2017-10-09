---
title: "alterações de máquina virtual aaaMonitor - grade de eventos do Azure & aplicativos lógicos | Microsoft Docs"
description: "Verifique as alterações de configuração em máquinas virtuais (VMs) usando a Grade de Eventos do Azure e os aplicativos lógicos"
keywords: "aplicativos lógicos, grades de eventos, máquina virtual, VM"
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a>Como monitorar alterações de máquina virtual com a Grade de Eventos do Azure e os aplicativos lógicos

Você pode iniciar um [fluxo de trabalho do aplicativo lógico](../logic-apps/logic-apps-what-are-logic-apps.md) automatizado quando eventos específicos ocorrem em recursos do Azure ou de terceiros. Esses recursos podem publicar esses eventos tooan [grade de eventos do Azure](../event-grid/overview.md). Por sua vez, a grade de eventos de saudação envia toosubscribers esses eventos com filas, e webhooks, ou [hubs de eventos](../event-hubs/event-hubs-what-is-event-hubs.md) como pontos de extremidade. Como um assinante, sua lógica de aplicativo pode aguardar os eventos da grade de eventos de saudação antes de executar fluxos de trabalho automatizados tarefas tooperform - sem que você escrever nenhum código.

Por exemplo, aqui estão alguns eventos que editores podem enviar toosubscribers por meio do serviço de grade de eventos do Azure hello:

* Criar, ler, atualizar ou excluir um recurso. Por exemplo, você pode monitorar as alterações que podem incorrer em encargos na sua assinatura do Azure e afetar sua fatura. 
* Adicionar ou remover uma pessoa de uma assinatura do Azure.
* Executar uma ação específica no seu aplicativo.
* Exibir uma nova mensagem em uma fila.

Este tutorial cria um aplicativo lógico que monitora alterações tooa virtual machine e envia emails sobre essas alterações. Quando você cria um aplicativo de lógica com uma assinatura de evento para um recurso do Azure, eventos de fluxo de recurso por meio de um aplicativo do evento grade toohello lógica. tutorial Olá orienta a criação deste aplicativo lógica:

![Visão geral – como monitorar uma máquina virtual com a grade de eventos e o aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar um aplicativo lógico que monitora os eventos de uma grade de eventos.
> * Adicionar uma condição que verifica especificamente se há alterações na máquina virtual.
> * Enviar email quando sua máquina virtual é alterada.

## <a name="prerequisites"></a>Pré-requisitos

* Uma conta de email de [qualquer provedor de email compatível com Aplicativos Lógicos do Azure](../connectors/apis-list.md), como o Office 365 Outlook, Outlook.com ou Gmail para envio de notificações. Este tutorial usa o Office 365 Outlook.

* Uma [máquina virtual](https://azure.microsoft.com/services/virtual-machines). Se você ainda não fez isso, crie uma máquina virtual por meio de um [tutorial sobre como criar uma VM](https://docs.microsoft.com/azure/virtual-machines/). máquina de virtual toomake Olá publicar eventos, você [toodo qualquer outra transação não é necessário](../event-grid/overview.md).

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a>Criar um aplicativo lógico que monitora os eventos de uma grade de eventos

Primeiro, crie um aplicativo lógico e adicionar um gatilho de grade de eventos que monitora Olá o grupo de recursos para sua máquina virtual. 

1. Entrar toohello [portal do Azure](https://portal.azure.com). 

2. De saudação canto superior esquerdo do menu principal do Azure hello, escolha **novo** > **integração corporativa** > **aplicativo lógico**.

   ![Criar aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. Crie seu aplicativo lógico com configurações de saudação especificadas em Olá a tabela a seguir:

   ![Defina os detalhes do aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | Configuração | Valor sugerido | Descrição | 
   | ------- | --------------- | ----------- | 
   | **Nome** | *{nome de seu aplicativo lógico}* | Forneça um nome exclusivo de aplicativo lógico. | 
   | **Assinatura** | *{sua assinatura do Azure}* | Selecione Olá a mesma assinatura do Azure para todos os serviços neste tutorial. | 
   | **Grupo de recursos** | *{seu grupo de recursos do Azure}* | Selecione Olá mesmo grupo de recursos do Azure para todos os serviços neste tutorial. | 
   | **Localidade** | *{sua região do Azure}* | Selecione Olá mesma região para todos os serviços neste tutorial. | 
   | | | 

4. Quando você estiver pronto, selecione **Pin toodashboard**e escolha **criar**.

   Agora você criou um recurso do Azure para o seu aplicativo lógico. 
   Depois que o Azure implanta o aplicativo lógico, Olá lógica aplicativos Designer mostra modelos padrões comuns para que você possa começar mais rapidamente.

   > [!NOTE] 
   > Quando você seleciona **toodashboard Pin**, seu aplicativo lógico é aberto automaticamente no Designer de aplicativos de lógica. Se isso não acontecer, encontre e abra o aplicativo lógico manualmente.

5. Agora escolha um modelo de aplicativo lógico. Em **Modelos**, escolha **Aplicativo lógico em branco** para compilar seu aplicativo lógico do zero.

   ![Escolher o modelo de aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   Olá lógica aplicativos Designer agora mostra [ *conectores* ](../connectors/apis-list.md) e [ *gatilhos* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) que você pode usar toostart sua lógica de aplicativo, além de ações que você pode adicionar após um disparar tooperform tarefas. Um gatilho é um evento que cria uma instância do aplicativo lógico e inicia o fluxo de trabalho do aplicativo lógico. 
   Seu aplicativo lógica precisa de um disparador como o primeiro item de saudação.

6. Na caixa de pesquisa hello, digite "grade de eventos" como filtro. Selecione este gatilho: **Grade de Eventos do Azure - em um evento de recurso**

   ![Selecione este gatilho: "Grade de Eventos do Azure - em um evento de recurso"](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. Quando solicitado, entre em tooAzure grade de eventos com suas credenciais do Azure.

   ![Entrar com suas credenciais do Azure](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > Se você estiver conectado com uma conta pessoal da Microsoft, como @outlook.com ou @hotmail.com, gatilho de evento grade Olá pode não ser exibidos corretamente. Como alternativa, escolha [conectar-se com o serviço Principal](/azure-resource-manager/resource-group-create-service-principal-portal.md), ou autenticar como um membro de saudação do Azure Active Directory associado à sua assinatura do Azure, por exemplo, *nome de usuário* @emailoutlook.onmicrosoft.com.

8. Agora, assine seus eventos de toopublisher lógica do aplicativo. Forneça detalhes de saudação para sua assinatura do evento conforme especificado no Olá a tabela a seguir:

   ![Forneça detalhes para a assinatura de evento](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | Configuração | Valor sugerido | Descrição | 
   | ------- | --------------- | ----------- | 
   | **Assinatura** | *{assinatura de máquina virtual do Azure}* | Selecione a assinatura do Azure do publicador do evento hello. Para este tutorial, selecione Olá assinatura do Azure para sua máquina virtual. | 
   | **Tipo de recurso** | Microsoft.Resources.resourceGroups | Selecione o tipo de recurso do publicador do evento hello. Para este tutorial, selecione Olá valor especificado para que o seu aplicativo lógico monitora somente grupos de recursos. | 
   | **Nome do recurso** | *{nome do grupo de recursos da máquina virtual}* | Selecione o nome do recurso do publisher hello. Para este tutorial, selecione o nome de Olá Olá do grupo de recursos para sua máquina virtual. | 
   | Para acessar as configurações opcionais, escolha **Mostrar opções avançadas**. | *{consulte as descrições}* | * **Filtro do prefixo**: para este tutorial, deixe essa configuração em branco. comportamento padrão de saudação corresponde a todos os valores. No entanto, você pode especificar uma cadeia de caracteres de prefixo como filtro, por exemplo, um caminho e um parâmetro para um recurso específico. <p>* **Filtro de sufixo**: para este tutorial, deixe essa configuração em branco. comportamento padrão de saudação corresponde a todos os valores. No entanto, você pode especificar uma cadeia de caracteres de sufixo como filtro, por exemplo, uma extensão de nome de arquivo, quando quiser tipos específicos de arquivo.<p>* **Nome da Assinatura**: forneça um nome exclusivo para a assinatura de evento. |
   | | | 

   Quando terminar, seu gatilho da grade de eventos poderá parecer com este exemplo:
   
   ![Exemplo: detalhes de gatilho de grade de eventos](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. Salve seu aplicativo lógico. Na barra de ferramentas designer hello, escolha **salvar**. toocollapse e ocultar os detalhes de uma ação em seu aplicativo lógico, escolha barra de título da ação hello.

   ![Salve seu aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   Quando você salvar seu aplicativo lógica com um gatilho de evento de grade, o Azure cria automaticamente uma inscrição de evento para o recurso de tooyour selecionado do aplicativo de lógica. Para que quando o recurso de saudação publica uma grade de eventos do evento toohello, essa grade de eventos envia automaticamente Olá evento tooyour lógica aplicativo. Este evento dispara seu aplicativo lógico, em seguida, cria e executa uma instância de fluxo de trabalho de saudação que você define nas próximas etapas.

Seu aplicativo lógico agora está ativo e escuta tooevents da grade de eventos hello, mas não faz nada até que você adicione o fluxo de trabalho de toohello de ações. 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a>Como adicionar uma condição que verifica se há alterações na máquina virtual

toorun seu fluxo de trabalho de aplicativo de lógica somente quando ocorre um evento específico, adicione uma condição que verifica a máquina virtual "operações de gravação". Quando essa condição for verdadeira, seu aplicativo lógico envia que email com detalhes sobre a máquina virtual de saudação atualizada.

1. No Designer de lógica do aplicativo, em acionador de grade de eventos hello, escolha **nova etapa** > **adicionar uma condição**.

   ![Adicionar um aplicativo de lógica de tooyour condição](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   Olá lógica de aplicativo Designer adiciona um fluxo de trabalho de tooyour condição vazio, incluindo toofollow de caminhos de ação com base em se a condição de saudação é true ou false.

   ![Condição vazia](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. Em Olá **condição** caixa, escolha **Editar no modo avançado**.
Digite esta expressão:

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   Agora, sua condição é semelhante a este exemplo:

   ![Condição vazia](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   Essa expressão verifica evento Olá `body` para um `data` objeto onde hello `operationName` é de propriedade hello `Microsoft.Compute/virtualMachines/write` operação. 
   Saiba mais sobre [Esquema de grade de eventos do evento](../event-grid/event-schema.md).

3. tooprovide uma descrição para a condição de saudação, escolha Olá **elipses** (**...** ) na forma de condição hello e escolha **Renomear**.

   > [!NOTE] 
   > Olá exemplos mais adiante neste tutorial também fornecem descrições para as etapas no fluxo de trabalho do aplicativo hello lógica.

4. Escolha agora **Editar no modo básico** para que a expressão de saudação resolve automaticamente conforme mostrado:

   ![Condição de aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. Salve seu aplicativo lógico.

## <a name="send-email-when-your-virtual-machine-changes"></a>Enviar email quando sua máquina virtual é alterada

Agora, adicione um [ *ação* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) para que você recebe um email quando Olá especificado a condição for verdadeira.

1. Na condição de saudação **se verdadeiro** caixa, escolha **adicionar uma ação**.

   ![Como adicionar uma ação para condição definida como verdadeira](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. Na caixa de pesquisa hello, digite "email" como filtro. Com base no seu provedor de email, localize e selecione o conector de correspondência de saudação. Em seguida, selecione a ação "enviar email" Olá para o conector. Por exemplo: 

   * Para um Azure ou de estudante conta, o conector do Outlook do Office 365 Olá select. 
   * Para contas da Microsoft pessoais, selecione Olá Outlook.com. 
   * Para contas do Gmail, selecione o conector do Gmail hello. 

   Vamos toocontinue com o conector do Outlook do Office 365 hello. 
   Se você usar um provedor diferente, Olá etapas permanecem Olá mesmo, mas a interface do usuário pode aparecer diferente. 

   ![Selecione a ação "enviar email"](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. Se você ainda não tiver uma conexão para o seu provedor de email, entre na conta de email de tooyour quando for solicitado para autenticação.

4. Forneça detalhes para email Olá conforme especificado no Olá a tabela a seguir:

   ![Ação de esvaziar email](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > tooselect de campos disponíveis no fluxo de trabalho, clique em uma caixa de edição assim que Olá **conteúdo dinâmico** abre, ou escolha **adicionar conteúdo dinâmico**. Para mais campos, escolha **ver mais** para cada seção na lista de saudação. Olá tooclose **conteúdo dinâmico** , escolha **adicionar conteúdo dinâmico**.

   | Configuração | Valor sugerido | Descrição | 
   | ------- | --------------- | ----------- | 
   | **Para** | *{endereço de email do destinatário}* |Insira o endereço de email do destinatário hello. Para fins de teste, você pode usar seu próprio endereço de email. | 
   | **Assunto** | Recurso atualizado: **Assunto**| Inserir o conteúdo de saudação de assunto do email hello. Para este tutorial, insira Olá sugerido texto e do evento Olá selecione **assunto** campo. Aqui, o assunto do email inclui nome Olá para o recurso de saudação atualizado (máquina virtual). | 
   | **Corpo** | Grupo de recursos: **Tópico** <p>Tipo de evento: **Tipo de Evento**<p>ID do evento: **ID**<p>Hora: **Hora do Evento** | Inserir o conteúdo de saudação do corpo do email hello. Para este tutorial, insira Olá sugerido texto e do evento Olá selecione **tópico**, **tipo de evento**, **ID**, e **hora do evento** campos para que seu email inclui o nome do grupo de recursos hello, tipo de evento, carimbo de hora do evento e ID de evento de atualização de saudação. <p>tooadd de linhas em branco em seu conteúdo, pressione Shift + Enter. | 
   | | | 

   > [!NOTE] 
   > Se você selecionar um campo que representa uma matriz, o designer de saudação adiciona automaticamente um **para cada** loop em torno de ação de saudação que faz referência a matriz de saudação. Dessa forma, seu aplicativo lógico executará essa ação em cada item da matriz.

   Agora, a ação do email pode parecer com este exemplo:

   ![Selecione tooinclude saídas no email](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   Seu aplicativo lógico concluído pode parecer com este exemplo:

   ![Aplicativo lógico concluído](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. Salve seu aplicativo lógico. toocollapse e ocultar detalhes de cada ação em seu aplicativo lógico, escolha barra de título da ação hello.

   ![Salve seu aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   Seu aplicativo lógico agora está ativo, mas aguarda a máquina de virtual tooyour alterações antes de fazer qualquer coisa. 
   tootest sua lógica de aplicativo agora, continuar toohello próxima seção.

## <a name="test-your-logic-app-workflow"></a>Testar o fluxo de trabalho de seu aplicativo lógico

1. toocheck que seu aplicativo lógico está ficando Olá especificado eventos, atualizar a máquina virtual. 

   Por exemplo, você pode redimensionar sua máquina virtual no portal do Azure de saudação ou [redimensionar a VM com o Azure PowerShell](../virtual-machines/windows/resize-vm.md). 

   Você receberá um email em alguns instantes. Por exemplo:

   ![Email sobre a atualização da máquina virtual](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. Olá tooreview é executado e histórico de gatilho para seu aplicativo lógico, no menu aplicativo lógica, escolha **visão geral**. tooview mais detalhes sobre uma execução, escolha a linha hello para que execute.

   ![Histórico de execuções do aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. entradas de saudação do tooview e saídas para cada etapa, expanda etapa Olá que você deseja tooreview. Essas informações podem ajudar você a diagnosticar e depurar problemas em seu aplicativo lógico.
 
   ![Detalhes do histórico de execução do aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

Parabéns, você acabou de criar e executar um aplicativo lógico capaz de monitorar eventos de recursos por uma grade de eventos e envio de emails para notificar o acontecimento de tais eventos. Você também aprendeu como é fácil criar fluxos de trabalho que automatizam processos e integram sistemas e serviços de nuvem.

## <a name="clean-up-resources"></a>Limpar recursos

Este tutorial usa recursos e executa ações que geram encargos na sua assinatura do Azure. Então quando você concluiu o tutorial hello e teste, verifique se você desabilitar ou excluir recursos onde você não deseja tooincur encargos.

Você pode interromper o aplicativo de lógica de execução e enviar email sem excluir o aplicativo hello. No menu do aplicativo lógico, escolha **Visão geral**. Na barra de ferramentas hello, escolha **desabilitar**.

![Como desabilitar o aplicativo lógico](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a>Perguntas frequentes

**P**: que outras tarefas de monitoração de máquina virtual eu posso executar com grades de eventos e aplicativos lógicos? </br>
**R**: você pode monitorar outras alterações de configuração, por exemplo:

* Uma máquina virtual obtém direitos de controle de acesso baseado em função (RBAC).
* As alterações são feitas de grupo de segurança de rede tooa (NSG) em uma interface de rede (NIC).
* Discos para uma máquina virtual são adicionados ou removidos.
* Um endereço IP público é atribuído a NIC de máquina virtual tooa.

## <a name="next-steps"></a>Próximas etapas

* [Visão geral da grade de eventos](../event-grid/overview.md)
* [Conceitos da grade de eventos](../event-grid/concepts.md)
* [Início rápido: Como criar e encaminhar eventos personalizados com a grade de eventos](../event-grid/custom-event-quickstart.md)
* [Esquema de evento da grade de eventos](../event-grid/event-schema.md)
* [Aplicativos Lógicos do Azure](../logic-apps/logic-apps-what-are-logic-apps.md)
* [Criar fluxos de trabalho de aplicativo lógico com modelos predefinidos](../logic-apps/logic-apps-use-logic-app-templates.md)