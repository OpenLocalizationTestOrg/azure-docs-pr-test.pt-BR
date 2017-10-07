---
title: "mensagens de aaaTrack B2B no Operations Management Suite - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Acompanhar a comunicação B2B da conta de integração e os aplicativos lógicos no OMS (Operations Management Suite) com o Azure Log Analytics"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>Controlar a comunicação do B2B Olá Microsoft Operations Management Suite (OMS)

Depois de configurar a comunicação B2B entre dois processos ou aplicativos de negócios em execução por meio de sua conta de integração, essas entidades poderão trocar mensagens entre si. toocheck se essas mensagens são processadas corretamente, você pode acompanhar AS2, X12, e mensagens EDIFACT com [Azure Log Analytics](../log-analytics/log-analytics-overview.md) em Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Por exemplo, você pode usar essas funcionalidades de acompanhamento baseado na Web para o acompanhamento de mensagens:

* Status e contagem de mensagens
* Status de confirmações
* Correlacionar mensagens com confirmações
* Descrição de erro detalhada para falhas
* Recursos de pesquisa

## <a name="requirements"></a>Requisitos

* Um aplicativo lógico configurado com o log de diagnósticos. Saiba [como toocreate um aplicativo lógico](logic-apps-create-a-logic-app.md) e [como tooset o registro em log para esse aplicativo lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Uma conta de integração configurada com o monitoramento e log. Saiba [como uma conta de integração de toocreate](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [como tooset o monitoramento e registro em log para essa conta](../logic-apps/logic-apps-monitor-b2b-message.md).

* Se você ainda não o fez, [publicar dados de diagnóstico tooLog análise](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) no OMS.

> [!NOTE]
> Depois que você cumpriu requisitos anteriores hello, você deve ter um espaço de trabalho Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Você deve usar Olá mesmo espaço de trabalho do OMS para controlar a comunicação de B2B no OMS. 
>  
> Se você não tiver um espaço de trabalho do OMS, saiba [como toocreate um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>Adicionar Olá lógica aplicativos B2B solução toohello Operations Management Suite (OMS)

toohave OMS rastrear mensagens de B2B para seu aplicativo lógico, você deve adicionar Olá **lógica aplicativos B2B** portal do OMS toohello solução. Saiba mais sobre [adicionando soluções tooOMS](../log-analytics/log-analytics-get-started.md).

1. Em Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**. Pesquise “log analytics” e, em seguida, escolha **Log Analytics**, conforme mostrado aqui:

   ![Encontrar o Log Analytics](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. Em **Log Analytics**, encontre e selecione o espaço de trabalho do OMS. 

   ![Selecionar o espaço de trabalho do OMS](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. Em **Gerenciamento**, escolha **Portal do OMS**.

   ![Escolher o portal do OMS](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Depois de abrir a home page do OMS hello, escolha **Galeria de soluções**.    

   ![Escolher a Galeria de Soluções](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. Em **Todas as soluções**, encontre e escolha **Aplicativos Lógicos B2B**.     

   ![Escolher Aplicativos Lógicos B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. Em **Aplicativos Lógicos B2B**, escolha **Adicionar**.

   ![Escolha Adicionar](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   Na home page do hello OMS, Olá lado a lado para **lógica aplicativos B2B mensagens** agora aparece. 
   Este bloco atualiza a contagem de mensagem de saudação quando as mensagens B2B são processadas.

   ![Home page do OMS, bloco Mensagens dos Aplicativos Lógicos B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>Acompanhar o status da mensagem e os detalhes em Olá Operations Management Suite

1. Depois que as mensagens B2B são processadas, você pode exibir detalhes e status de saudação dessas mensagens. Na home page de saudação do OMS, escolha Olá **lógica aplicativos B2B mensagens** lado a lado.

   ![Contagem de mensagens atualizada](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > Por padrão, Olá **lógica aplicativos B2B mensagens** bloco mostra dados com base em um único dia. toochange Olá escopo intervalo diferente de tooa, escolha controle de escopo de saudação na parte superior de saudação da página OMS hello:
   > 
   > ![Alterar o escopo de dados](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. Após o status da mensagem de saudação painel é exibido, você pode exibir mais detalhes para um tipo de mensagem específica, que mostra dados com base em um único dia. Escolha o bloco de saudação do **AS2**, **X12**, ou **EDIFACT**.

   ![Exibir status da mensagem](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   Uma lista de mensagens é exibida para o bloco escolhido. 
   toolearn mais sobre as propriedades de saudação para cada tipo de mensagem, consulte essas descrições de propriedade de mensagem:

   * [Propriedades de mensagens AS2](#as2-message-properties)
   * [Propriedades de mensagens X12](#x12-message-properties)
   * [Propriedades de mensagens EDIFACT](#EDIFACT-message-properties)

   Por exemplo, veja abaixo a aparência de uma lista de mensagens AS2:

   ![Exibir mensagens AS2](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. entradas de saudação tooview ou exportação e saídas de mensagens específicas, selecione essas mensagens e escolha **baixar**. Quando você for solicitado, salve o computador local do tooyour do arquivo hello. zip e, em seguida, extrair o arquivo. 

   pasta extraída Olá inclui uma pasta para cada mensagem selecionada. 
   Se você configurar confirmações, a pasta de mensagem de saudação também inclui arquivos com detalhes de confirmação. 
   Cada pasta de mensagens tem, pelo menos, estes arquivos: 
   
   * Detalhes de carga de carga e a saída de entrada de arquivos legível por hello
   * Arquivos codificados com hello entradas e saídas

   Para cada tipo de mensagem, você pode encontrar a pasta hello e formatos de nome de arquivo aqui:

   * [Formatos de nome de pasta e arquivo AS2](#as2-folder-file-names)
   * [Formatos de nome de pasta e arquivo X12](#x12-folder-file-names)
   * [Formatos de nome de pasta e arquivo EDIFACT](#edifact-folder-file-names)

   ![Baixar arquivos de mensagem](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. tooview todas as ações que têm Olá a mesma ID da execução, em Olá **pesquisa de Log** página, escolha uma mensagem na lista de mensagens de saudação.

   Classifique essas ações por coluna ou pesquise resultados específicos.

   ![Ações com hello mesmo ID da execução](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * resultados de toosearch com consultas predefinidas, escolha **Favoritos**.

   * Saiba [como toobuild consulta adicionando filtros](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md). 
   Saiba mais sobre [como toofind dados com log de pesquisa na análise de Log](../log-analytics/log-analytics-log-searches.md).

   * toochange consulta na caixa de pesquisa hello, atualização Olá consulta com hello colunas e valores que você deseja toouse como filtros.

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>Descrições de propriedade e formatos de nome de mensagens AS2, X12 e EDIFACT

Para cada tipo de mensagem, aqui estão descrições de propriedade hello e formatos de nome para os arquivos de mensagem baixada.

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>Descrições de propriedade da mensagem AS2

Aqui estão as descrições de propriedade Olá para cada mensagem AS2.

| Propriedade | Descrição |
| --- | --- |
| Remetente | parceiro convidado de saudação especificado em **configurações de recebimento**, ou parceiro do host de saudação especificado em **configurações de envio** para um acordo AS2 |
| Receptor | parceiro de host Olá especificado em **configurações de recebimento**, ou parceiro convidado de saudação especificado em **configurações de envio** para um acordo AS2 |
| Aplicativo Lógico | Olá lógica aplicativo onde ações Olá AS2 são configuradas |
| Status | Olá status da mensagem AS2 <br>Êxito = recebimento ou envio de uma mensagem AS2 válida. Nenhum MDN está configurado. <br>Êxito = recebimento ou envio de uma mensagem AS2 válida. O MDN está configurado e é recebido ou o MDN é enviado. <br>Com Falha = recebimento de uma mensagem AS2 inválida. Nenhum MDN está configurado. <br>Pendente = recebimento ou envio de uma mensagem AS2 válida. O MDN está configurado e o MDN é esperado. |
| Ack | Olá status da mensagem MDN <br>Aceito = recebimento ou envio de um MDN positivo. <br>Pending = aguardando tooreceive ou enviar um MDN. <br>Rejeitado = recebimento ou envio de um MDN negativo. <br>Não é necessário = MDN não está definido no contrato de saudação. |
| Direção | Olá direção da mensagem AS2 |
| ID de Correlação | ID de saudação que se correlaciona todos os disparadores de saudação e ações em um aplicativo de lógica |
| ID da Mensagem | ID de mensagem de saudação AS2 de cabeçalhos de mensagem de saudação AS2 |
| Timestamp | tempo de saudação quando Olá AS2 ação processado a mensagem de saudação |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>Formatos de nome AS2 para arquivos de mensagem baixados

Aqui estão Olá formatos de nome para cada pasta de mensagens AS2 baixada e arquivos.

| Pasta ou arquivo | Formato de nome |
| :------------- | :---------- |
| Pasta de mensagens | [sender]\_[receiver]\_AS2\_[correlation-ID]\_[message-ID]\_[timestamp] |
| Entrada, saída e, se configurado, os arquivos de confirmação | **Conteúdo de entrada**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_input_payload.txt </p>**Conteúdo de saída**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_output\_payload.txt </p></p>**Entradas**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_inputs.txt </p></p>**Saídas**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_outputs.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>Descrições das propriedades da mensagem X12

Aqui estão descrições de propriedade Olá para cada X12 mensagem.

| Propriedade | Descrição |
| --- | --- |
| Remetente | parceiro convidado de saudação especificado em **configurações de recebimento**, ou parceiro do host de saudação especificado em **configurações de envio** para um X12 contrato |
| Receptor | parceiro de host Olá especificado em **configurações de recebimento**, ou parceiro convidado de saudação especificado em **configurações de envio** para um X12 contrato |
| Aplicativo Lógico | Olá lógica aplicativo onde ações Olá X12 são configuradas |
| Status | status da mensagem de saudação X12 <br>Êxito = recebimento ou envio de uma mensagem X12 válida. Nenhuma confirmação funcional está configurada. <br>Êxito = recebimento ou envio de uma mensagem X12 válida. Uma confirmação funcional está configurada e é recebida ou uma confirmação funcional é enviada. <br>Com Falha = recebimento ou envio de uma mensagem X12 inválida. <br>Pendente = recebimento ou envio de uma mensagem X12 válida. Uma confirmação funcional está configurada e uma confirmação funcional é esperada. |
| Ack | Status da Confirmação Funcional (997) <br>Aceito = recebimento ou envio de uma confirmação funcional positiva. <br>Rejeitado = recebimento ou envio de uma confirmação funcional negativa. <br>Pendente = aguardando uma confirmação funcional, mas não recebida. <br>Pendente = gerado uma confirmação funcional, mas não é possível enviar toopartner. <br>Não Obrigatório = uma confirmação funcional não está configurada. |
| Direção | direção da mensagem de saudação X12 |
| ID de Correlação | ID de saudação que se correlaciona todos os disparadores de saudação e ações em um aplicativo de lógica |
| Tipo de mensagem | saudação de tipo de mensagem 12 X de EDI |
| ICN | Número de controle de intercâmbio de saudação para mensagem de saudação X12 |
| TSCN | Olá número de controle de conjunto de transação para a mensagem de saudação X12 |
| Timestamp | tempo de saudação quando ação Olá X12 processado a mensagem de saudação |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>Formatos de nome X12 para arquivos de mensagem baixados

Aqui estão os formatos de nome de saudação cada baixadas X12 pastas e arquivos de mensagem.

| Pasta ou arquivo | Formato de nome |
| :------------- | :---------- |
| Pasta de mensagens | [sender]\_[receiver]\_X12\_[interchange-control-number]\_[global-control-number]\_[transaction-set-control-number]\_[timestamp] |
| Entrada, saída e, se configurado, os arquivos de confirmação | **Conteúdo de entrada**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_input_payload.txt </p>**Conteúdo de saída**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_output\_payload.txt </p></p>**Entradas**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_inputs.txt </p></p>**Saídas**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_outputs.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>Descrições das propriedades da mensagem EDIFACT

Aqui estão as descrições de propriedade Olá para cada mensagem EDIFACT.

| Propriedade | Descrição |
| --- | --- |
| Remetente | parceiro convidado de saudação especificado em **configurações de recebimento**, ou parceiro do host de saudação especificado em **configurações de envio** para um acordo EDIFACT |
| Receptor | parceiro de host Olá especificado em **configurações de recebimento**, ou parceiro convidado de saudação especificado em **configurações de envio** para um acordo EDIFACT |
| Aplicativo Lógico | Olá lógica aplicativo em que ações de EDIFACT Olá são configuradas |
| Status | Olá status da mensagem EDIFACT <br>Êxito = recebimento ou envio de uma mensagem EDIFACT válida. Nenhuma confirmação funcional está configurada. <br>Êxito = recebimento ou envio de uma mensagem EDIFACT válida. Uma confirmação funcional está configurada e é recebida ou uma confirmação funcional é enviada. <br>Com Falha = recebimento ou envio de uma mensagem EDIFACT inválida <br>Pendente = recebimento ou envio de uma mensagem EDIFACT válida. Uma confirmação funcional está configurada e uma confirmação funcional é esperada. |
| Ack | Status da Confirmação Funcional (997) <br>Aceito = recebimento ou envio de uma confirmação funcional positiva. <br>Rejeitado = recebimento ou envio de uma confirmação funcional negativa. <br>Pendente = aguardando uma confirmação funcional, mas não recebida. <br>Pendente = gerado uma confirmação funcional, mas não é possível enviar toopartner. <br>Não Obrigatório = uma confirmação funcional não está configurada. |
| Direção | Olá direção da mensagem EDIFACT |
| ID de Correlação | ID de saudação que se correlaciona todos os disparadores de saudação e ações em um aplicativo de lógica |
| Tipo de mensagem | tipo de mensagem EDIFACT de saudação |
| ICN | Número de controle de intercâmbio de saudação para mensagem de saudação do EDIFACT |
| TSCN | Olá número de controle de conjunto de transação para a mensagem de saudação do EDIFACT |
| Timestamp | tempo de saudação quando Olá ação EDIFACT processado a mensagem de saudação |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>Formatos de nome EDIFACT para arquivos de mensagem baixados

Aqui estão Olá formatos de nome para cada pasta de mensagens EDIFACT baixada e arquivos.

| Pasta ou arquivo | Formato de nome |
| :------------- | :---------- |
| Pasta de mensagens | [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_[global-control-number]\_[transaction-set-control-number]\_[timestamp] |
| Entrada, saída e, se configurado, os arquivos de confirmação | **Conteúdo de entrada**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_input_payload.txt </p>**Conteúdo de saída**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_output\_payload.txt </p></p>**Entradas**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_inputs.txt </p></p>**Saídas**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_outputs.txt |
|          |             |

## <a name="next-steps"></a>Próximas etapas

* [Consulta de mensagens B2B no Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [Esquemas de acompanhamento de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Esquemas de acompanhamento de X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Esquemas de acompanhamento personalizado](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)