---
title: "aaaAgent solução de integridade no OMS | Microsoft Docs"
description: "Este artigo é pretendido toohelp você entender como toouse toomonitor essa solução Olá integridade de seus agentes que se reportam diretamente tooOMS ou System Center Operations Manager."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>Solução Integridade do Agente do OMS
solução de integridade do agente de saudação do OMS ajuda você a entender, para todos os agentes de saudação reporting diretamente toohello espaço de trabalho do OMS ou um tooOMS de grupo conectado de gerenciamento do System Center Operations Manager, que estão respondendo e enviando dados operacionais.  Você pode também manter controle das quantos agentes são implantados, onde são distribuídos geograficamente e realizar o reconhecimento de toomaintain outras consultas da distribuição Olá dos agentes implantados no Azure, outros ambientes de nuvem ou local.    

## <a name="prerequisites"></a>Pré-requisitos
Antes de implantar essa solução, confirme que atualmente têm suporte [agentes do Windows](../log-analytics/log-analytics-windows-agents.md) reporting toohello espaço de trabalho do OMS ou reporting tooan [grupo de gerenciamento do Operations Manager](../log-analytics/log-analytics-om-agents.md) integrado com o Espaço de trabalho do OMS.    

## <a name="solution-components"></a>Componentes da solução
Essa solução consiste em Olá recursos que são adicionados tooyour espaço de trabalho e agentes conectados diretamente ou grupo de gerenciamento conectados do Operations Manager a seguir.

### <a name="management-packs"></a>Pacotes de gerenciamento
Se o grupo de gerenciamento do System Center Operations Manager for conectado tooan espaço de trabalho do OMS, Olá pacotes de gerenciamento a seguir é instalado no Operations Manager.  Esses pacotes de gerenciamento também são instalados em computadores com Windows conectados diretamente após a adição dessa solução. Não há nada tooconfigure ou gerenciar esses pacotes de gerenciamento.

* Pacote de inteligência do Microsoft System Center Advisor HealthAssessment Direct (Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Pacote de inteligência do Microsoft System Center Advisor HealthAssessment Server Channel (Microsoft.IntelligencePacks.HealthAssessmentViaServer).  

Para obter mais informações sobre como os pacotes de gerenciamento da solução são atualizados, consulte [tooLog conectar o Operations Manager análise](../log-analytics/log-analytics-om-agents.md).

## <a name="configuration"></a>Configuração
Adicionar tooyour de solução de integridade do agente Olá espaço de trabalho do OMS usando Olá processo descrito em [adicionar soluções](../log-analytics/log-analytics-add-solutions.md). Não é necessária nenhuma configuração.


## <a name="data-collection"></a>Coleta de dados
### <a name="supported-agents"></a>Agentes com suporte
Olá, a tabela a seguir descreve Olá conectado fontes que são suportadas por essa solução.

| Fonte Conectada | Suportado | Descrição |
| --- | --- | --- |
| Agentes do Windows | Sim | Os eventos de pulsação são coletados dos agentes diretos do Windows.|
| Grupo de gerenciamento do System Center Operations Manager | Sim | Eventos de pulsação são coletados dos agentes reporting toohello grupo de gerenciamento a cada 60 segundos e, em seguida, encaminhados tooLog análise. Análise de uma conexão direta de tooLog de agentes do Operations Manager não é necessária. Dados de evento de pulsação são encaminhados do repositório de análise de Log toohello do grupo de gerenciamento de saudação.|

## <a name="using-hello-solution"></a>Usando a solução de saudação
Quando você adiciona o espaço de trabalho do hello solução tooyour OMS, Olá **integridade do agente** bloco será adicionado tooyour painel do OMS. Esse bloco mostra número total de saudação de agentes e número de saudação dos agentes não responder em Olá últimas 24 horas.<br><br> ![Bloco da solução Integridade do Agente no painel](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

Clique em Olá **integridade do agente** bloco tooopen Olá **integridade do agente** painel.  Painel de saudação inclui colunas de saudação de Olá a tabela a seguir. Cada coluna lista os eventos de dez principais Olá pela contagem que correspondem a critérios da coluna para Olá especificado intervalo de tempo. Você pode executar uma pesquisa de log que fornece a lista inteira de saudação selecionando **ver todos os** na parte inferior direita do hello de cada coluna, ou clicando o cabeçalho da coluna hello.

| Coluna | Descrição |
|--------|-------------|
| Contagem de agentes ao longo do tempo | Uma tendência de sua contagem de agentes durante um período de sete dias para agentes do Linux e do Windows.|
| Contagem de agentes sem resposta | Uma lista de agentes que ainda não enviou uma pulsação em Olá últimas 24 horas.|
| Distribuição por tipo de sistema operacional | Uma partição de quantos agentes de Windows e Linux você tem em seu ambiente.|
| Distribuição por versão do agente | Uma partição Olá diferentes das versões do agente instalado em seu ambiente e uma contagem de cada um deles.|
| Distribuição por categoria de agente | Uma partição de categorias diferentes de saudação de agentes que estão enviando eventos de pulsação: agentes diretos, os agentes do MOM ou Olá servidor de gerenciamento do MOM.|
| Distribuição por grupo de gerenciamento | Uma partição de diferentes grupos de gerenciamento do SCOM Olá em seu ambiente.|
| Localização geográfica de agentes | Uma partição de países diferentes hello, em que os agentes e uma contagem total de número de saudação de agentes que foram instaladas em cada país.|
| Contagem de gateways instalados | número de saudação de servidores que têm hello OMS Gateway instalado e uma lista desses servidores.|

![Exemplo de painel da solução Integridade do Agente](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Registros do Log Analytics
solução de saudação cria um tipo de registro no repositório do OMS hello.  

### <a name="heartbeat-records"></a>Registros de pulsação
Um registro com o tipo **pulsação** é criado.  Esses registros têm propriedades de saudação no Olá a tabela a seguir.  

| Propriedade | Descrição |
| --- | --- |
| Tipo | *Pulsação*|
| Categoria | O valor é *Agente Direto*, *Agente SCOM* ou *o Servidor de Gerenciamento do SCOM*.|
| Computador | Nome do computador.|
| OSType | Sistema operacional Windows ou Linux.|
| OSMajorVersion | Versão principal do sistema operacional.|
| OSMinorVersion | Versão secundária do sistema operacional.|
| Versão | Versão do agente do OMS ou do agente do Operations Manager.|
| SCAgentChannel | O valor é *Direct* e/ou *SCManagementServer*.|
| IsGatewayInstalled | Se o Gateway do OMS está instalado, o valor é *true*; caso contrário, o valor é *false*.|
| ComputerIP | Endereço IP do computador de saudação.|
| RemoteIPCountry | Localização geográfica onde o computador está implantado.|
| ManagementGroupName | Nome do grupo de gerenciamento do Operations Manager.|
| SourceComputerId | ID exclusiva do computador.|
| RemoteIPLongitude | Longitude do local geográfico do computador.|
| RemoteIPLatitude | Latitude da localização geográfica do computador.|

Cada agente no servidor de gerenciamento do Operations Manager tooan enviará dois pulsações e valor da propriedade SCAgentChannel incluirá ambos reporting **direto** e **SCManagementServer** dependendo do que Fontes de dados de análise de log e soluções habilitadas em sua assinatura do OMS. Se você se lembra, dados de soluções são enviados diretamente de um Gerenciador de operações toohello do servidor de gerenciamento do OMS serviço web, ou devido a saudação volume de dados coletados no agente hello, são enviados diretamente do serviço web do hello agente tooOMS. Para eventos de pulsação que têm valor Olá **SCManagementServer**, Olá ComputerIP valor é o endereço IP de saudação saudação do servidor de gerenciamento porque, na verdade, os dados de saudação são carregados por ele.  Para pulsações onde SCAgentChannel está definido muito**direto**, é o endereço IP público de saudação do agente de saudação.  

## <a name="sample-log-searches"></a>Pesquisas de log de exemplo
Olá tabela a seguir fornece pesquisas de log de exemplo para registros coletados por essa solução.

| Consultar | Descrição |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |Número total de agentes |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |Contagem de agentes não responder em Olá últimas 24 horas |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |Contagem de agentes sem resposta nos últimos 15 minutos de saudação |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Computadores online (em Olá últimas 24 horas) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Total agentes off-line nos últimos 30 minutos (para Olá últimas 24 horas) |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |Obter uma tendência do número de agentes ao longo do tempo por OSType|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |Distribuição por tipo de sistema operacional |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |Distribuição por versão do agente |
| Type=Heartbeat&#124;measure count() by Category |Distribuição por categoria de agente |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | Distribuição por grupo de gerenciamento |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |Localização geográfica de agentes |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |Número de Gateways do OMS instalados |


>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](../log-analytics/log-analytics-log-search-upgrade.md), e em seguida, Olá acima consultas alteraria toohello a seguir.
>
>| Consultar | Descrição |
|:---|:---|
| Heartbeat &#124; distinct Computer |Número total de agentes |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |Contagem de agentes não responder em Olá últimas 24 horas |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |Contagem de agentes sem resposta nos últimos 15 minutos de saudação |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Computadores online (em Olá últimas 24 horas) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Total agentes off-line nos últimos 30 minutos (para Olá últimas 24 horas) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Obter uma tendência do número de agentes ao longo do tempo por OSType|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Distribuição por tipo de sistema operacional |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |Distribuição por versão do agente |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |Distribuição por categoria de agente |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | Distribuição por grupo de gerenciamento |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |Localização geográfica de agentes |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |Número de Gateways do OMS instalados |

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre os [Alertas no Log Analytics](../log-analytics/log-analytics-alerts.md) para obter detalhes sobre como gerar alertas por meio do Log Analytics.
