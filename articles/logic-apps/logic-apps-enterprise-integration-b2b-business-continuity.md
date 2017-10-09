---
title: "recuperação de aaaDisaster para conta de integração B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Recuperação de desastre dos Aplicativos Lógicos B2B"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Recuperação de desastre de região cruzada dos Aplicativos Lógicos B2B

As cargas de trabalho B2B envolvem transações de dinheiro como pedidos e faturas. Durante um evento de desastre, é essencial para uma saudação de toomeet business tooquickly recuperar que SLAs de nível de negócios acordados com seus parceiros. Este artigo demonstra como planejar toobuild uma continuidade de negócios B2B cargas de trabalho. 

* Prontidão para recuperação de desastre 
* Failover de região toosecondary durante um evento de desastre 
* Voltar região tooprimary após um evento de desastre

## <a name="disaster-recovery-readiness"></a>Prontidão para recuperação de desastre  

1. Identificar uma região secundária e criar um [conta integration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) na região secundária hello.

2. Adicione parceiros, esquemas e os contratos para fluxos de mensagens de saudação necessário onde Olá status de execução precisa toobe replicada toosecondary região integração conta.

   > [!TIP]
   > Verifique se há consistência na convenção de nomenclatura do artefato de conta para a integração Olá entre regiões. 

3. Olá toopull status da execução da região primária do hello, crie um aplicativo de lógica na região secundária hello. 

   Esse aplicativo lógico deve ter um *gatilho* e uma *ação*. 
   gatilho Olá deve se conectar a conta de integração de região tooprimary e ação Olá deve se conectar a conta de integração de região toosecondary. 
   Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de status de região primária executar hello e recebe novos registros de hello, se houver. ação de saudação atualiza toosecondary conta de integração de região. 
   Isso ajuda a tooget em tempo de execução incremental da região de toosecondary região primária.

4. Continuidade de negócios em aplicativos de lógica de conta de integração é projetado toosupport com base em protocolos B2B - X12, AS2 e EDIFACT. toofind obter etapas detalhadas, selecione Olá respectivos links.

5. Olá recomendação é muito toodeploy todos os recursos de região primária em uma região secundária. 

   Recursos de região primária incluem o banco de dados SQL ou banco de dados do Azure Cosmos, barramento de serviço do Azure e Hubs de eventos do Azure usado para mensagens, gerenciamento de API do Azure e o recurso de aplicativos do Azure lógica de saudação do serviço de aplicativo do Azure.   

6. Estabelece uma conexão de uma região secundária tooa a região primária. Olá toopull status da execução de uma região primária, crie um aplicativo de lógica em uma região secundária. 

   Olá lógica aplicativo deve ter um gatilho e uma ação. 
   gatilho Olá deve se conectar a conta de integração do tooa região primária. 
   ação de saudação deve se conectar a conta de integração do tooa região secundária. 
   Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de status de região primária executar hello e recebe novos registros de hello, se houver. 
   ação de saudação atualiza tooa conta de integração de região secundária. 
   Esse processo ajuda em tempo de execução incremental tooget da região secundária do toohello Olá região primária.

Continuidade de negócios em uma conta de integração de aplicativos lógicos fornece suporte baseado em protocolos de B2B Olá X12, AS2 e EDIFACT. Para obter etapas detalhadas sobre como usar X12 e AS2, consulte [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) e [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) neste artigo.

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>Failover de região secundária tooa durante um evento de desastre

Durante um evento de desastre, quando a região primária Olá não está disponível para continuidade de negócios, região secundária do tráfego direto toohello. Região secundária ajuda a um toorecover negócios rapidamente funções toomeet Olá RPO/RTO acordado por seus parceiros. Ele também minimiza esforços toofail através da região de tooanother de uma região. 

Há uma latência esperada ao copiar os números de controle de uma região secundária tooa a região primária. tooavoid enviar controle gerado duplicados números toopartners durante um evento de desastre, recomendação Olá é tooincrement números de controle de saudação em contratos de região secundária hello usando [cmdlets do PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>Retorno de evento de pós-desastres região primária tooa

toofall tooa back região primária quando ele estiver disponível, siga estas etapas:

1. Pare de aceitar mensagens de parceiros na região secundária hello.  

2. Incrementar números de controle de saudação gerado para todos os contratos de região primária hello usando [cmdlets do PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).  

3. Tráfego direto da região primária do toohello Olá região secundária.

4. Verificar aplicativo hello lógica criado na região secundária do Olá de obter status da execução da região primária Olá está habilitado.

## <a name="x12"></a>X12 

A continuidade dos negócios para documentos EDI X12 tem como base os números de controle:

> [!TIP]
> Você também pode usar o hello [X12 rápido iniciar modelo](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate lógica aplicativos. Criar contas de integração primários e secundários são modelo de saudação toouse pré-requisitos. Olá modelo ajuda toocreate dois aplicativos de lógica, um para números de controle recebido e outro para os números de controle gerado. Ações e respectivos gatilhos são criadas em aplicativos de lógica de hello, conectando Olá gatilho toohello integração principal contas e Olá ação toohello integração secundário.

**Pré-requisitos**

tooenable a recuperação de desastres para mensagens de entrada, selecione Olá duplicados Verifique as configurações em configurações de recebimento do contrato Olá X12.

![Selecionar configurações de verificação de duplicadas](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. Crie um [aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) em uma região secundária.    

2. Pesquise **X12** e selecione **X12 – quando um número de controle é modificado**.   

   ![Pesquise por X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   gatilho Olá solicita tooestablish uma conta de integração de tooan de conexão. 
   Olá gatilho deve estar conectado a conta de integração do tooa região primária.

3. Insira um nome de conexão, selecione seu *conta de integração da região primária* de saudação lista e escolha **criar**.   

   ![Nome da conta de integração da região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. Olá **sincronização do número de controle DateTime toostart** configuração é opcional. Olá **frequência** pode ser definido muito**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.   

   ![DateTime e Frequency](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. Selecione **Nova etapa** > **Adicionar uma ação**.

   ![Nova Etapa, Adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. Pesquise em **X12** e selecione **X12 – adicionar ou atualizar números de controle**.   

   ![Adicionar ou atualizar números de controle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. tooconnect tooa região secundária integração conta de ação, selecione **alterar conexão** > **adicionar nova conexão** para obter uma lista de contas de integração disponíveis hello. Insira um nome de conexão, selecione seu *conta de integração de região secundária* de saudação lista e escolha **criar**. 

   ![Nome da conta de integração da região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. Alternar tooraw entradas clicando no ícone de saudação no canto superior direito.

   ![Opção tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. Selecione corpo do seletor de conteúdo dinâmico Olá e salve o aplicativo lógico de saudação.

   ![Campos de conteúdo dinâmico](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de números de controle do hello região primária recebida e recebe novos registros de saudação. 
   ação Olá atualiza os registros de saudação na conta de integração do hello região secundária. 
   Se não houver nenhuma atualização, status de gatilho Olá aparece como **ignorados**.   

   ![Tabela de números de controle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Com base no intervalo de tempo de saudação, em tempo de execução incremental Olá replica de uma região secundária tooa a região primária. Durante um evento de desastre, quando Olá primário região não é disponível de tráfego direto toohello secundário para continuidade de negócios. 

## <a name="edifact"></a>EDIFACT 

A continuidade dos negócios para documentos EDI EDIFACT tem como base os números de controle.

**Pré-requisitos**

tooenable a recuperação de desastres para mensagens de entrada, selecione Olá duplicados Verifique as configurações em configurações de recebimento do seu contrato EDIFACT.

![Selecionar configurações de verificação de duplicadas](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. Crie um [aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) em uma região secundária.    

2. Pesquise **EDIFACT** e selecione **EDIFACT – quando um número de controle é modificado**.

   ![Pesquisar por EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   gatilho Olá solicita tooestablish uma conta de integração de tooan de conexão. 
   Olá gatilho deve estar conectado a conta de integração do tooa região primária. 

3. Insira um nome de conexão, selecione seu *conta de integração da região primária* de saudação lista e escolha **criar**.    

   ![Nome da conta de integração da região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. Olá **sincronização do número de controle DateTime toostart** configuração é opcional. Olá **frequência** pode ser definido muito**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.    

   ![DateTime e Frequency](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. Selecione **Nova etapa** > **Adicionar uma ação**.    

   ![Nova Etapa, Adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. Pesquise em **EDIFACT** e selecione **EDIFACT – adicionar ou atualizar números de controle**.   

   ![Adicionar ou atualizar números de controle](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. tooconnect tooa região secundária integração conta de ação, selecione **alterar conexão** > **adicionar nova conexão** para obter uma lista de contas de integração disponíveis hello. Insira um nome de conexão, selecione seu *conta de integração de região secundária* de saudação lista e escolha **criar**.

   ![Nome da conta de integração da região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. Alternar tooraw entradas clicando no ícone de saudação no canto superior direito.

   ![Opção tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. Selecione corpo do seletor de conteúdo dinâmico Olá e salve o aplicativo lógico de saudação.   

   ![Campos de conteúdo dinâmico](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de números de controle do hello região primária recebida e recebe novos registros de saudação.
   ação de Olá atualiza a conta de integração do hello registros toohello região secundária. 
   Se não houver nenhuma atualização, status de gatilho Olá aparece como **ignorados**.

   ![Tabela de números de controle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Com base no intervalo de tempo de saudação, em tempo de execução incremental Olá replica de uma região secundária tooa a região primária. Durante um evento de desastre, quando Olá primário região não é disponível de tráfego direto toohello secundário para continuidade de negócios. 

## <a name="as2"></a>AS2 

Continuidade dos negócios para documentos que usam o protocolo do AS2 Olá baseia-se a ID de mensagem de saudação e valor MIC hello.

> [!TIP]
> Você também pode usar o hello [modelo de início rápido do AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate lógica aplicativos. Criar contas de integração primários e secundários são modelo de saudação toouse pré-requisitos. modelo de saudação ajuda a criar um aplicativo de lógica que tem um gatilho e uma ação. Olá lógica aplicativo cria uma conexão de uma conta do gatilho tooa integração principal e conta de ação tooa integração secundário.

1. Criar um [aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) na região secundária hello.  

2. Pesquise **AS2** e selecione **AS2 – quando um valor de MIC é criado**.   

   ![Pesquise por AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   Um gatilho solicitará que você tooestablish uma conta de integração de tooan de conexão. 
   Olá gatilho deve estar conectado a conta de integração do tooa região primária. 
   
3. Insira um nome de conexão, selecione seu *conta de integração da região primária* de saudação lista e escolha **criar**.

   ![Nome da conta de integração da região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. Olá **sincronização de valor DateTime toostart MIC** configuração é opcional. Olá **frequência** pode ser definido muito**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.   

   ![DateTime e Frequency](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. Selecione **Nova etapa** > **Adicionar uma ação**.  

   ![Nova Etapa, Adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. Pesquise em **AS2** e selecione **AS2 – adicionar ou atualizar conteúdos de MIC**.  

   ![Adição ou atualização do MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. Selecione tooconnect uma conta de integração secundário ação tooa, **alterar conexão** > **adicionar nova conexão** para obter uma lista de contas de integração disponíveis hello. Insira um nome de conexão, selecione seu *conta de integração de região secundária* de saudação lista e escolha **criar**.

   ![Nome da conta de integração da região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. Alternar tooraw entradas clicando no ícone de saudação no canto superior direito.

   ![Opção tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. Selecione corpo do seletor de conteúdo dinâmico Olá e salve o aplicativo lógico de saudação.   

   ![Conteúdo dinâmico](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   Com base no intervalo de tempo de saudação, gatilho Olá pesquisa a tabela de região primária hello e recebe novos registros de saudação. ação de saudação atualiza toohello conta de integração de região secundária. 
   Se não houver nenhuma atualização, status de gatilho Olá aparece como **ignorados**.  

   ![Tabela da região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

Com base no intervalo de tempo de saudação, em tempo de execução incremental Olá replica de região secundária do toohello Olá região primária. Durante um evento de desastre, quando Olá primário região não é disponível de tráfego direto toohello secundário para continuidade de negócios. 

## <a name="next-steps"></a>Próximas etapas

[Monitorar mensagens do B2B](logic-apps-monitor-b2b-message.md)

