---
title: "aaaIT conector de gerenciamento de serviço do OMS | Microsoft Docs"
description: "Use o monitor de toocentrally Olá conector de gerenciamento de serviço de TI e gerenciar itens de trabalho ITSM Olá no OMS e resolver problemas rapidamente."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>Gerenciar itens de trabalho de ITSM de forma centralizada usando o Conector de Gerenciamento de Serviço de TI (Visualização)

![Símbolo do Conector de Gerenciamento do Serviço de TI](./media/log-analytics-itsmc/itsmc-symbol.png)

Você pode usar o hello conector de gerenciamento de serviço de TI (ITSMC) no monitor de toocentrally de análise de logs do OMS e gerenciar itens de trabalho entre seus produtos/serviços ITSM.

Olá conector de gerenciamento de serviço de TI se integra a seus serviços e produtos de gerenciamento de serviço de TI (ITSM) existentes com análise de logs do OMS.  solução de saudação tem integração bidirecional com ITSM produtos/serviços, onde ele fornece Olá incidentes opção toocreate os usuários do OMS, alertas ou eventos em solução ITSM. conector de saudação também importa dados, como incidentes e solicitações de alteração de solução ITSM em análise de logs do OMS.

Com o Conector de Gerenciamento de Serviço de TI, você pode:

  - Monitorar e gerenciar itens de trabalho para produtos/serviços de ITSM usados em sua organização de forma centralizada.
  - Criar itens de trabalho de ITSM (como alerta, evento e incidente) no ITSM com base em alertas do OMS e por meio da pesquisa de logs.
  - Ler incidentes e solicitações de alteração na solução de ITSM e correlacioná-los com os dados de logs relevantes no espaço de trabalho do Log Analytics.
  - Localizar qualquer evento inesperado e incomuns e resolvê-los, mesmo para que os usuários finais de saudação chamar e relatá-los toohello helpdesk.
  - Importar dados de itens de trabalho para o Log Analytics e criar relatórios de KPI (indicador chave de desempenho).  Com esses relatórios, você pode identificar, avaliar e tomar decisões em relação a vários itens importantes, como avaliação de malware.
  - Exibir painéis estruturados para obter informações mais profundas sobre incidentes, solicitações de alteração e sistemas afetados.
  - Solucionar problemas mais rapidamente, correlacionando com outras soluções de gerenciamento no espaço de trabalho de análise de Log de saudação.


## <a name="prerequisites"></a>Pré-requisitos

itens de trabalho tooimport Olá ITSM em análise de logs do OMS, Olá solução exige que uma conexão entre hello conector de gerenciamento de serviço de TI no hello OMS e Olá TI SM produto/serviço do qual você importa os itens de trabalho hello.


## <a name="configuration"></a>Configuração

Saudação de adicionar espaço de trabalho do OMS conector de gerenciamento de serviço de TI solução tooyour, usando Olá processo descrito na [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).

Conector de gerenciamento de serviço IT bloco que você vê na Galeria de soluções de saudação:

![bloco do conector](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Após a adição bem-sucedida, você verá Olá conector de gerenciamento de serviço de TI em **OMS** > **configurações** > **fontes conectadas.**

![ITSMC conectado](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Por padrão, o Olá conector de gerenciamento de serviço de TI atualiza os dados da conexão Olá uma vez em cada 24 horas. toorefresh instantaneamente para as edições ou modelo as da conexão atualizações de dados que você fizer, clique em conexão botão exibido tooyour próxima atualização hello.

 ![Atualização do ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Pacotes de gerenciamento
Essa solução não exige nenhum pacote de gerenciamento.

## <a name="connected-sources"></a>Fontes conectadas

Olá ITSM seguintes produtos/serviços são suportados pelo Olá conector de gerenciamento de serviço de TI:

- [SCSM (System Center Service Manager)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>Usando a solução de saudação

Quando você conecta Olá conector de gerenciamento de serviço de TI de OMS com seu serviço ITSM, serviços de análise de Log Olá inicia a coleta de dados Olá Olá conectado ITSM produtos/serviço.

> [!NOTE]
> - Os dados importados pelo Conector de Gerenciamento do Serviço de TI são exibidos no Log Analytics como eventos chamados **ServiceDesk_CL**.
- O evento contém um campo chamado **ServiceDeskWorkItemType_s**. que pode ter seu valor como um incidente, ou solicitação de alteração, dependendo de saudação do item de trabalho dados contidos em Olá **ServiceDesk_CL** eventos.

## <a name="input-data"></a>Dados de entrada
Itens de trabalho importados de saudação ITSM produtos/serviços.

Olá informações a seguir mostram exemplos de dados coletados pelo conector de gerenciamento de serviços de saudação:

> [!NOTE]
> Dependendo de saudação do item de trabalho tipo importado para a análise de Log, **ServiceDesk_CL** contém Olá campos a seguir:

**Item de trabalho:** **Incidentes**  
ServiceDeskWorkItemType_s="Incident"

**Campos**

- ServiceDeskConnectionName
- ID da Central de Serviços
- Estado
- Urgência
- Impacto
- Prioridade
- Escalonamento
- Criado por
- Resolvido por
- Fechado por
- Fonte
- Atribuído a
- Categoria
- Title
- Descrição
- Data de criação
- Data de fechamento
- Data de resolução
- Data da última modificação
- Computador


**Item de trabalho:** **Solicitações de alteração**

ServiceDeskWorkItemType_s="ChangeRequest"

**Campos**
- ServiceDeskConnectionName
- ID da Central de Serviços
- Criado por
- Fechado por
- Fonte
- Atribuído a
- Title
- Tipo
- Categoria
- Estado
- Escalonamento
- Status do conflito
- Urgência
- Prioridade
- Risco
- Impacto
- Atribuído a
- Data de criação
- Data de fechamento
- Data da última modificação
- Data de solicitação
- Data de início prevista
- Data de término prevista
- Data de início do trabalho
- Data de término do trabalho
- Descrição
- Computador

## <a name="output-data-for-a-servicenow-incident"></a>Dados de saída de um incidente do ServiceNow

| Campo do OMS | Campo do ITSM |
|:--- |:--- |
| ServiceDeskId_s| Número |
| IncidentState_s | Estado |
| Urgency_s |Urgência |
| Impact_s |Impacto|
| Priority_s | Prioridade |
| CreatedBy_s | Aberto por |
| ResolvedBy_s | Resolvido por|
| ClosedBy_s  | Fechado por |
| Source_s| Tipo de contato |
| AssignedTo_s | Atribuído muito |
| Category_s | Categoria |
| Title_s|  Descrição breve |
| Description_s|  Observações |
| CreatedDate_t|  Aberto |
| ClosedDate_t| closed|
| ResolvedDate_t|Resolvido|
| Computador  | Item de configuração |

## <a name="output-data-for-a-servicenow-change-request"></a>Dados de saída para uma solicitação de alteração do ServiceNow

| Campo do OMS | Campo do ITSM |
|:--- |:--- |
| ServiceDeskId_s| Número |
| CreatedBy_s | Solicitado por |
| ClosedBy_s | Fechado por |
| AssignedTo_s | Atribuído muito |
| Title_s|  Descrição breve |
| Type_s|  Tipo |
| Category_s|  Catgory |
| CRState_s|  Estado|
| Urgency_s|  Urgência |
| Priority_s| Prioridade|
| Risk_s| Risco|
| Impact_s| Impacto|
| RequestedDate_t  | Solicitado por data |
| ClosedDate_t | Data de fechamento |
| PlannedStartDate_t  |     Data de início planejada |
| PlannedEndDate_t  |   Data de término planejada |
| WorkStartDate_t  | Data de início real |
| WorkEndDate_t | Data de término real|
| Description_s | Descrição |
| Computador  | Item de Configuração |

**Tela de exemplo do Log Analytics para dados de ITSM:**

![Tela do Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>Conector de Gerenciamento de Serviço de TI – integração com outras soluções do OMS

Conector de gerenciamento de serviço IT, atualmente oferece suporte à integração com hello solução Mapa de serviço.

Mapa de serviço detecta automaticamente Olá componentes de aplicativos no Windows e mapas e sistemas Linux Olá comunicação entre serviços. Ele permite que você tooview os servidores que você imagina – como sistemas interconectados que fornecem serviços essenciais. O Mapa do Serviço mostra conexões entre servidores, processos e portas em qualquer arquitetura conectada a TCP sem nenhuma configuração necessária além da instalação de um agente. Mais informações: [Mapa do Serviço](../operations-management-suite/operations-management-suite-service-map.md).

Com essa integração, você pode exibir itens de suporte técnico de serviço Olá criados em soluções ITSM hello, conforme mostrado no exemplo a seguir de saudação:

![Solução integrada ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>Criar itens de trabalho de ITSM para alertas do OMS

Para alertas do OMS hello, você pode criar itens de trabalho associados em fontes de ITSM Olá conectado.  toodo, Olá use procedimento a seguir:

1. De **pesquisa de Log** janela, execute um dados tooview de consulta de pesquisa de log. Resultados da consulta são fonte Olá para itens de trabalho.
2. Em **pesquisa de Log**, clique em **alerta** tooopen Olá **Adicionar regra de alerta** página.

    ![Tela do Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. Em Olá **Adicionar regra de alerta** janela, forneça detalhes Olá necessária para **nome**, **severidade**, **consulta de pesquisa**, e  **Critérios de alerta** (medida da métrica/janela de tempo).
4. Selecione **Sim** para **Ações de ITSM**.
5. Selecione sua conexão ITSM da saudação **Selecionar Conexão** lista.
6. Forneça detalhes Olá conforme necessário.
7. toocreate um item de trabalho separada para cada entrada de log de saudação esse alerta, selecione **criar itens de trabalho individuais para cada entrada de log** caixa de seleção.

    Ou

    Deixe essa caixa de seleção toocreate não selecionado apenas um item de trabalho para qualquer número de entradas de log sob esse alerta.

7. Clique em **Salvar**.

alerta OMS Hello será criada sob **alertas**. Olá trabalho da conexão ITSM correspondente itens são criados quando a condição do alerta Olá especificada for atendida.

## <a name="create-itsm-work-items-from-oms-logs"></a>Criar itens de trabalho de ITSM com base em logs do OMS

Você pode criar itens de trabalho em fontes de ITSM Olá conectado usando a pesquisa de Log do OMS. toodo, Olá use procedimento a seguir:

1. De **pesquisa de Log**, pesquisar dados Olá necessário, selecione os detalhes de saudação e clique em **criar item de trabalho**.

    Olá **item de trabalho de ITSM criar** janela é exibida:

    ![Tela do Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Adicione Olá detalhes a seguir:

  - **Título do item de trabalho**: título Olá item de trabalho.
  - **Descrição do item de trabalho**: descrição Olá novo item de trabalho.
  - **Afetou o computador**: nome do computador Olá onde esses dados de log foi encontrados.
  - **Selecione a Conexão**: conexão ITSM no qual você deseja toocreate este item de trabalho.
  - **Item de trabalho**: tipo de item de trabalho.

3. toouse um modelo de item de trabalho existente de um incidente, clique em **Sim** em **gerar item de trabalho com base no modelo de saudação** opção e, em seguida, clique em **criar**.

    Ou,

    Clique em **não** se você quiser tooprovide seus valores personalizados.

4. Forneça os valores adequados no Olá Olá **tipo de contato**, **impacto**, **urgência**, **categoria**, e **subcategoria**  caixas de texto e clique **criar**.

item de trabalho Olá será criado no hello ITSM, que você também pode exibir no OMS.

## <a name="troubleshoot-itsm-connections-in-oms"></a>Solucionar problemas de conexões de ITSM no OMS
1.  Se a falha de conexão de interface de usuário da fonte conectada e obter Olá **erro ao salvar a conexão** mensagem, Olá a seguir:
 - No caso de conexões de ServiceNow, Cherwell e Provance, certifique-se você segredo de ID e cliente cliente e o nome de usuário/senha Olá inseridos corretamente para cada uma das conexões de saudação. Se Olá erro persistir, verifique se você tem privilégios suficientes em conexão Olá correspondente ITSM produto toomake hello.
 - No caso do Service Manager, certifique-se de que Olá Web aplicativo é implantado com êxito e conexão híbrida é criada. conexão de saudação tooverify é estabelecida com êxito com hello na Service Manager máquina local, visite a URL do aplicativo Web hello conforme detalhado na documentação de saudação para fazer Olá [conexão híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  Se não estiver obtendo sincronizados dados do ServiceNow do OMS, certifique-se de que essa instância do ServiceNow Olá não está em suspensão. Isso pouco e pode ocorrer em Olá ServiceNow Dev instâncias, quando estão ociosos. Else, problema de saudação de relatório.
3.  Se estiverem obtendo acionados alertas do OMS, mas itens de trabalho não estão obtendo criados no produto ITSM ou itens de configuração não estão recebendo itens toowork criado/vinculado ou para todas as informações genéricas, Olá a seguir:
 -  Solução de conector do serviço de gerenciamento de TI no portal do OMS pode ser usado tooget um resumo de itens de trabalho/conexões/computadores etc. Clique em mensagem de erro de saudação na folha de status hello, navegue muito**pesquisa de Log** e exibir conexão Olá com erro hello usando detalhes da saudação na mensagem de erro de saudação.
 - diretamente você pode exibir informações de erros/relacionados Olá no hello **pesquisa de Log** página usando *tipo = ServiceDeskLog_CL*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Solucionar problemas de implantação do aplicativo Web do Service Manager
1.  No caso de problemas com a implantação de aplicativo web, certifique-se de ter permissões suficientes na assinatura de saudação mencionado toocreate/implantar recursos.
2.  Se **referência de objeto não definida tooinstance de um objeto** mensagem de erro é exibida durante a execução Olá [script](log-analytics-itsmc-service-manager-script.md) Certifique-se de que você inseriu valores válidos em **configuração do usuário**seção.
3.  Se você não toocreate namespace de retransmissão de barramento de serviço, certifique-se de que Olá exigido de provedor de recursos está registrado na assinatura de saudação. Se não estiver registrado, manualmente criá-la de saudação portal do Azure. Você também pode criá-lo ao [criar conexão de híbrida Olá](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) de saudação portal do Azure.


## <a name="contact-us"></a>Fale conosco

Para todas as consultas ou comentários em Olá conector de gerenciamento de serviço de TI, entre em contato conosco em [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Próximas etapas
[Adicionar ITSM produtos/serviços tooIT conector de gerenciamento de serviço](log-analytics-itsmc-connections.md).
