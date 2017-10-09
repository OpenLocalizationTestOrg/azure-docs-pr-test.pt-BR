---
title: aaaIntegrating com o Operations Management Suite (OMS) | Microsoft Docs
description: "Além disso toousing Olá recursos padrão do OMS, você pode integrá-lo com outros tooprovide de aplicativos e serviços de gerenciamento, um ambiente de gerenciamento híbrido, ambiente de tooyour exclusivo de cenários de gerenciamento personalizado tooprovide ou tooprovide um personalizado experiência de gerenciamento para seus clientes.  Este artigo fornece uma visão geral das diferentes opções para a integração com o OMS e links tooarticles fornecer informações técnicas detalhadas."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: dce752dcdc6c725bbafd49db4a5055750487ecf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a>Integração com o OMS (Operations Management Suite)
O Microsoft Operations Management Suite é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda você a gerenciar e proteger sua infraestrutura local e de nuvem.  Além disso toousing Olá recursos padrão do OMS, você pode integrá-lo com outros tooprovide de aplicativos e serviços de gerenciamento, um ambiente de gerenciamento híbrido, ambiente de tooyour exclusivo de cenários de gerenciamento personalizado tooprovide ou tooprovide um personalizado experiência de gerenciamento para seus clientes.  Este artigo fornece uma visão geral das diferentes opções para a integração com o OMS serviços e links tooarticles fornecer informações técnicas detalhadas. 

## <a name="log-analytics"></a>Log Analytics
Todos os dados de gerenciamento coletados pelo Log Analytics são armazenados em um repositório, que é hospedado no Azure.  Todos os dados armazenados no repositório de saudação está disponível em pesquisas de log que fornecem análise rápida em grandes volumes de dados.  Seus requisitos de integração podem ser toopopulate repositório de saudação com novos dados, tornando-o disponível para análise, ou dados tooextract no repositório de saudação tooprovide uma nova visualização ou toointegrate com outra ferramenta de gerenciamento.

Cada parte dos dados no repositório de saudação é armazenado como um registro.  Ao preencher repositório Olá, você deve fornecer aos usuários com o tipo de registro de saudação que usa sua solução e uma descrição de suas propriedades.  Quando você recuperar dados, você precisará dessas informações sobre dados Olá que você está trabalhando.

![Preenchendo o repositório do OMS Olá](media/operations-management-suite-integration/repository.png)

### <a name="populate-hello-log-analytics-repository"></a>Preencher o repositório de análise de Log Olá
Há vários métodos de preenchimento do repositório do OMS hello.  Olá método usado depende de fatores como onde os dados de origem hello estão localizados, o formato de saudação de saudação dados e que os clientes precisam toosupport.  Depois que os dados são armazenados no repositório de hello, ele não faz diferença como ele foi coletado.

Olá, seções a seguir descrevem Olá diferentes opções de preenchimento do repositório do OMS hello.

#### <a name="connected-sources-and-data-sources"></a>Fontes conectadas e Fontes de dados
Fontes conectadas são locais de saudação onde os dados podem ser recuperados para o repositório do OMS hello.  Fontes de dados e soluções executados em fontes conectadas e definem Olá dados específicos que são coletados.  Se seu aplicativo grava tooone dados dessas fontes de dados, você pode coletá-lo ao configurar fonte de dados de saudação.  Por exemplo, se seu aplicativo cria eventos de Syslog, em seguida, eles podem ser coletados pela fonte de dados de Syslog Olá em um agente do Linux.

* [Fontes de dados no Log Analytics](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a>Soluções
Soluções de estendem os recursos de saudação do OMS.  Uma solução pode coletar dados de origem conectada hello, ou ele pode executar a análise em registros já coletados no repositório de saudação.  Cada solução fornecida pela Microsoft tem um artigo individual que fornece detalhes de saudação em dados Olá que coleta.

* [Soluções no Log Analytics](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a>API do coletor de dados HTTP
Olá API de coletor de dados de HTTP de análise de Log é uma API REST que permite que o repositório de análise de Log do tooadd JSON dados toohello.  Quando você tiver um aplicativo que não fornece dados por meio de um Olá outras fontes de dados ou soluções, você pode aproveitar essa API.  Ele pode ser repositório de saudação toopopulate usado de qualquer cliente que pode chamar a API de saudação e não depende da agenda de coleta de saudação de qualquer fonte de dados ou a solução.

* [API do coletor de dados HTTP do Log Analytics](../log-analytics/log-analytics-data-collector-api.md)

### <a name="retrieve-data-from-hello-log-analytics-repository"></a>Recuperar dados do repositório de análise de Log Olá
Há vários métodos para recuperar dados do repositório do OMS hello.  Você pode desejar usuários tooretrieve dados usando o console do OMS hello e fornecê-los com diferentes tipos de visualizações e análise.  Você também pode recuperar dados de saudação de um processo externo, como outra solução de gerenciamento.

#### <a name="log-searches"></a>Pesquisas de log
Todos os dados armazenados no repositório do OMS hello está disponível por meio de pesquisas de log.  Os usuários poderão executar seu próprios análise ad hoc no console do OMS hello ou criar um painel com uma visualização de uma pesquisa de log específico.  As soluções podem conter exibições personalizadas com visualizações baseadas em pesquisas predefinidas.  Você pode usar dados de tooaccess de API de pesquisa de Log de saudação no repositório do OMS saudação de uma ferramenta externa do aplicativo ou gerenciamento.  

* [Pesquisas de log no Log Analytics](../log-analytics/log-analytics-log-searches.md)
* [API REST de pesquisa de log do Log Analytics](../log-analytics/log-analytics-log-search-api.md)
* [Cmdlets do Log Analytics](https://msdn.microsoft.com/library/mt188224.aspx)

#### <a name="custom-views"></a>Modos de exibição personalizados
Olá View Designer permite que você toocreate modos de exibição personalizados no console do OMS Olá que fornecem aos usuários com a visualização e análise de dados de saudação em sua solução.  Cada modo de exibição inclui um bloco que é exibido na página principal de saudação do console hello e qualquer número de partes de visualização se baseiam em pesquisas de log que você definir.

* [Designer de exibição do Log Analytics](../log-analytics/log-analytics-view-designer.md)

#### <a name="power-bi"></a>Power BI
Análise de log automaticamente pode exportar dados do repositório do OMS Olá no Power BI para que você possa aproveitar suas visualizações e ferramentas de análise.  Ele executa esta exportação em um agendamento para que dados saudação toodate são atualizados. 

* [Exportar dados de análise de Log tooPower BI](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a>Automação
OMS pode automatizar processos tooreact toocollected dados ou tooperform outras funções de gerenciamento.  Pode coletar dados de seu aplicativo e inseri-lo no repositório do OMS hello, ou você pode automatizar correção de saudação de um problema conhecido no toodata resposta encontrado no repositório de saudação. 

![Automação](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a>Runbooks
Runbooks na automação do Azure executar scripts do PowerShell e fluxos de trabalho no hello nuvem do Azure.  Você pode usá-los toomanage recursos no Azure ou outros recursos que podem ser acessados da nuvem de saudação.  Os Runbooks também podem ser executados em um data center local usando o Hybrid Runbook Worker.  Você pode iniciar um runbook de saudação portal do Azure ou de processos externos usando um número de métodos, como o PowerShell ou Olá API de automação.

* [Como iniciar um Runbook na Automação do Azure](../automation/automation-starting-a-runbook.md)
* [Cmdlets da Automação do Azure](https://msdn.microsoft.com/library/dn690262.aspx)
* [API REST de Automação](https://msdn.microsoft.com/library/mt662285.aspx)
* [Automação .NET](https://msdn.microsoft.com//library/mt465763.aspx)

### <a name="alerts"></a>Alertas
Regras de alerta executar pesquisas de log de acordo com o agendamento de tooa automaticamente.  Se os resultados da saudação corresponder específico alerta resultante de saudação critérios pode iniciar um runbook na automação do Azure ou chamar um webhook que pode iniciar um processo externo.  Ambas essas respostas podem incluir detalhes do alerta Olá incluindo Olá dados retornados na pesquisa de log de saudação.

* [Alertas no Log Analytics](../log-analytics/log-analytics-alerts.md)
* [API de alerta do Log Analytics](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a>Backup e Site Recovery
De Backup e recuperação de Site do Azure fornecem serviços para proteger os dados da empresa e garantir a disponibilidade de saudação de servidores e aplicativos.  Você pode aproveitar esses serviços tooperform esses cenários como fornecendo serviços de backup para seu aplicativo ou iniciar um failover de uma máquina virtual.

* [Cmdlets do Backup do Azure](https://msdn.microsoft.com/library/mt619253.aspx)
* [API REST do Azure Site Recovery](https://msdn.microsoft.com/library/azure/mt750497.aspx)
* [Cmdlets do Azure Site Recovery](https://msdn.microsoft.com/library/mt637930.aspx)

## <a name="custom-solutions"></a>Soluções personalizadas
Você pode encapsular a lógica de integração em uma solução personalizada toorun no espaço de trabalho ou no espaço de trabalho do cliente.  Sua solução pode incluir qualquer um dos métodos de integração Olá neste artigo em adição tooother recursos tooprovide um cenário de gerenciamento completo.  recursos de saudação na solução de saudação são compactados, de modo que quando a solução Olá for removida, todos os recursos de saudação que ele criou são removidos do espaço de trabalho OMS hello e assinatura do Azure.

Por exemplo, sua solução pode incluir um dados toogather e o processo do runbook de automação e preencher, em seguida, o repositório de análise de Log hello usando Olá API do coletor de dados de HTTP.  Você também pode incluir uma exibição personalizada que apresenta e analisa os dados coletado de saudação.  

* Criação de soluções personalizadas (em breve)    

## <a name="next-steps"></a>Próximas etapas
* Saudação de referência [OMS SDK](operations-management-suite-sdk.md) para obter informações técnicas sobre a automatização de serviços do OMS.  

