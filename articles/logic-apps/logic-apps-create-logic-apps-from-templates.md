---
title: "Criar fluxos de trabalho com modelos - Aplicativo Lógico do Azure | Microsoft Docs"
description: "Compilar fluxos de trabalho mais rápidos usando modelos de aplicativo lógico"
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/15/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 49b4bbfda4518b03ef6080bec1e2a493933af4f5
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="create-logic-app-workflows-from-prebuilt-templates"></a>Criar fluxos de trabalho de aplicativo lógico com modelos predefinidos

Para começar a criar fluxos de trabalho mais rapidamente, os Aplicativos Lógicos fornecem os modelos, que são aplicativos lógicos predefinidos que seguem os padrões geralmente usados. Use esses modelos como são fornecidos ou modifique-os para adequá-los ao seu cenário.

Estas são algumas categorias de modelo:

| Tipo do modelo | DESCRIÇÃO | 
| ------------- | ----------- | 
| Modelos de nuvem empresarial | Para integrar Blobs do Azure, Dynamics CRM, Salesforce, Box, além de incluir outros conectores para suas necessidades de nuvem empresarial. Por exemplo, você pode usar esses modelos para organizar clientes potenciais de negócios ou fazer backup dos dados de arquivos corporativos. | 
| Modelos de produtividade pessoal | Melhore a produtividade pessoal definindo lembretes diários, transformando os itens de trabalho importantes em listas de tarefas e automatizando tarefas demoradas para uma única etapa de aprovação de usuário. | 
| Modelos de nuvem do consumidor | Para integrar serviços de mídia social, como o Twitter, o Slack e o email. Útil para reforçar iniciativas de marketing de mídia social. Esses modelos também incluem tarefas como a cópia em nuvem, que aumenta a produtividade ao economizar o tempo gasto em tarefas tradicionalmente repetitivas. | 
| Modelos de pacote de integração empresarial | Para configurar de pipelines VETER (validar, extrair, transformar, enriquecer e rotear), recebendo um documento EDI X12 via AS2 e transformando-o em XML, bem como o tratamento de mensagens X12, EDIFACT e AS2. | 
| Modelos de padrão de protocolo | Para implementar padrões de protocolo como solicitação-resposta por HTTP e integrações entre FTP e SFTP. Use esses modelos como são fornecidos ou trabalhe neles para obter padrões de protocolo complexos. | 
||| 

Caso você não tenha uma assinatura do Azure, [crie uma conta gratuita do Azure](https://azure.microsoft.com/free/) antes de começar. Para obter mais informações sobre como compilar um aplicativo lógico, consulte [Criar um aplicativo lógico](../logic-apps/quickstart-create-first-logic-app-workflow.md).

## <a name="create-logic-apps-from-templates"></a>Criar aplicativos lógicos de modelos

1. Se ainda não tiver feito isso, entre no [Portal do Azure](https://portal.azure.com "Portal do Azure").

2. No menu principal do Azure, escolha **Novo** > **Enterprise Integration** > **Aplicativo Lógico**.

   ![Portal do Azure, Novo, Enterprise Integration, Aplicativo Lógico](./media/logic-apps-create-logic-apps-from-templates/azure-portal-create-logic-app.png)

3. Crie seu aplicativo lógico com as configurações na tabela da imagem:

   ![Defina os detalhes do aplicativo lógico](./media/logic-apps-create-logic-apps-from-templates/logic-app-settings.png)

   | Configuração | Valor | DESCRIÇÃO | 
   | ------- | ----- | ----------- | 
   | **Nome** | *nome-seu-aplicativo-lógico* | Forneça um nome exclusivo de aplicativo lógico. | 
   | **Assinatura** | *seu-nome-da-assinatura-do-Azure* | Selecione a assinatura do Azure que você deseja usar. | 
   | **Grupo de recursos** | *seu-nome-do-grupo-de-recursos-do-Azure* | Crie ou selecione um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) para este aplicativo lógico e organize todos os recursos associados ao aplicativo. | 
   | **Localidade** | *sua-região-do-datacenter-do-Azure* | Selecione a região do datacenter para implantar seu aplicativo lógico, por exemplo, Oeste dos EUA. | 
   | **Log Analytics** | **Off** (padrão) ou **On** | Ative o [log de diagnósticos](../logic-apps/logic-apps-monitor-your-logic-apps.md#turn-on-diagnostics-logging-for-your-logic-app) para seu aplicativo lógico por meio do [Azure Log Analytics](../log-analytics/log-analytics-overview.md). Requer que você já tenha um espaço de trabalho do [Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md). | 
   |||| 

4. Quando estiver pronto, selecione **Fixar no painel**. Dessa forma, seu aplicativo lógico aparece automaticamente no painel do Azure e é aberto após a implantação. Escolha **Criar**.

   > [!NOTE]
   > Se você não deseja fixar seu aplicativo lógico, é necessário localizar e abrir manualmente o aplicativo lógico após a implantação para poder continuar.

   Depois que o Azure implanta o aplicativo lógico, o Designer de Aplicativos Lógicos é exibido e mostra uma página com um vídeo de introdução. 
   Neste vídeo, você encontrará modelos para padrões de aplicativos lógicos comuns. 

5. Role a tela até passar pelo vídeo de introdução e pelos gatilhos comuns até **Modelos**. Escolha um modelo predefinido. Por exemplo: 

   ![Escolha um modelo de aplicativo lógico](./media/logic-apps-create-logic-apps-from-templates/choose-logic-app-template.png)

   > [!TIP]
   > Para criar seu aplicativo lógico do zero, escolha **Aplicativo Lógico em Branco**.

   Quando você seleciona um modelo predefinido, é possível exibir mais informações sobre esse modelo. 
   Por exemplo: 

   ![Escolha um modelo predefinido](./media/logic-apps-create-logic-apps-from-templates/logic-app-choose-prebuilt-template.png)

6. Para continuar com o modelo selecionado, escolha **Usar este modelo**. 

7. Com base nos conectores no modelo, será solicitado que você execute qualquer uma das etapas a seguir:

   * Entre com suas credenciais para os sistemas ou serviços que são referenciados pelo modelo.

   * Crie conexões para todos os serviços ou sistemas referenciados pelo modelo. Para criar uma conexão, forneça um nome para ela e, se necessário, selecione o recurso que você deseja usar. 

   * Se você já configurou essas conexões, escolha **Continuar**.

   Por exemplo: 

   ![Criar conexões](./media/logic-apps-create-logic-apps-from-templates/logic-app-create-connection.png)

   Quando terminar, seu aplicativo lógico se abre e aparece no Designer de Aplicativos Lógicos.

   > [!TIP]
   > Para retornar para o visualizador do modelo, escolha **Modelos** na barra de ferramentas do designer. Essa ação descartará as alterações não salvas, por isso uma mensagem de aviso será exibida para confirmar a solicitação.

8. Continue a compilar seu aplicativo lógico.

   > [!NOTE] 
   > Muitos modelos incluem conectores que já podem ter as propriedades obrigatórias pré-populadas. No entanto, alguns modelos ainda podem exigir que você forneça valores para poder implantar o aplicativo lógico corretamente. Se você tentar implantá-lo sem preencher os campos de propriedades ausentes, receberá uma mensagem de erro. 

## <a name="update-logic-apps-with-templates"></a>Atualizar aplicativos lógicos com modelos

1. No [Portal do Azure](https://portal.azure.com "Portal do Azure"), encontre e abra seu aplicativo lógico no Designer de Aplicativos Lógicos.

2. Na barra de ferramentas do designer, escolha **Modelos**. Essa ação descartará as alterações não salvas, por isso uma mensagem de aviso será exibida para você poder confirmar que deseja continuar. Para confirmar, escolha **OK**. Por exemplo: 

   ![Escolha “Modelos”](./media/logic-apps-create-logic-apps-from-templates/logic-app-update-existing-with-template.png)

3. Role a tela até passar pelo vídeo de introdução e pelos gatilhos comuns até **Modelos**. Escolha um modelo predefinido. Por exemplo: 

   ![Escolha um modelo de aplicativo lógico](./media/logic-apps-create-logic-apps-from-templates/choose-logic-app-template.png)

   Quando você seleciona um modelo predefinido, é possível exibir mais informações sobre esse modelo. 
   Por exemplo: 

   ![Escolha um modelo predefinido](./media/logic-apps-create-logic-apps-from-templates/logic-app-choose-prebuilt-template.png)

4. Para continuar com o modelo selecionado, escolha **Usar este modelo**. 

5. Com base nos conectores no modelo, será solicitado que você execute qualquer uma das etapas a seguir:

   * Entre com suas credenciais para os sistemas ou serviços que são referenciados pelo modelo.

   * Crie conexões para todos os serviços ou sistemas referenciados pelo modelo. Para criar uma conexão, forneça um nome para ela e, se necessário, selecione o recurso que você deseja usar. 

   * Se você já configurou essas conexões, escolha **Continuar**.

   ![Criar conexões](./media/logic-apps-create-logic-apps-from-templates/logic-app-create-connection.png)

   Seu aplicativo lógico agora será aberto e aparecerá no Designer de Aplicativos Lógicos.

8. Continue a compilar seu aplicativo lógico. 

   > [!TIP]
   > Se suas alterações não tiverem sido salvas, você poderá descartar seu trabalho e retornar ao seu aplicativo lógico anterior. Na barra de ferramentas do designer, escolha **Descartar**.

> [!NOTE] 
> Muitos modelos incluem conectores que podem já ter as propriedades obrigatórias pré-populadas. No entanto, alguns modelos ainda podem exigir que você forneça valores para poder implantar o aplicativo lógico corretamente. Se você tentar implantá-lo sem preencher os campos de propriedades ausentes, receberá uma mensagem de erro.

## <a name="deploy-logic-apps-built-from-templates"></a>Implantar aplicativos lógicos compilados de modelos

Depois de fazer as alterações no modelo, salve suas alterações. Essa ação também publica automaticamente seu aplicativo lógico.

Clique em **Salvar** na barra de ferramentas do designer.

![Salvar e publicar seu aplicativo lógico](./media/logic-apps-create-logic-apps-from-templates/logic-app-save.png)  

## <a name="get-support"></a>Obtenha suporte

* Em caso de dúvidas, visite o [Fórum dos Aplicativos Lógicos do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).
* Para enviar ou votar em ideias de recurso, visite o [site de comentários do usuário de Aplicativos Lógicos](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como compilar aplicativos lógicos por meio de exemplos, cenários, histórias de clientes e tutoriais passo a passo.

> [!div class="nextstepaction"]
> [Leia exemplos de aplicativos lógicos, cenários e tutoriais passo a passo](../logic-apps/logic-apps-examples-and-scenarios.md)