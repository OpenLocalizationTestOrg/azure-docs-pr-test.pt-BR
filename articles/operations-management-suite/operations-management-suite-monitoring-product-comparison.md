---
title: "aaaMicrosoft monitoramento de comparação de produto | Microsoft Docs"
description: "O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem.  Este artigo identifica Olá serviços diferentes incluídos no OMS e fornece links tootheir detalhadas conteúdo."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Comparação de produtos de monitoramento da Microsoft
Este artigo fornece uma comparação entre o System Center Operations Manager (SCOM) e análise de Log no OMS Operations Management Suite () em termos de sua arquitetura, a lógica de saudação de como eles monitoram recursos e como eles executam a análise dos dados de saudação eles Colete.  Isso é toogive você um entendimento fundamental de suas diferenças e pontos fortes.  

## <a name="basic-architecture"></a>Arquitetura básica
### <a name="system-center-operations-manager"></a>System Center Operations Manager
Todos os componentes do SCOM estão instalados em seu data center.  [agentes são instalados](http://technet.microsoft.com/library/hh551142.aspx) em computadores com Windows e Linux que são gerenciados pelo SCOM.  Agentes de conectar-se muito[servidores de gerenciamento](https://technet.microsoft.com/library/hh301922.aspx) que se comunicam com hello e banco de dados do warehouse do SCOM.  Agentes dependem de servidores de toomanagement de tooconnect de autenticação de domínio.  Aqueles fora de um domínio confiável podem realizar a autenticação de certificado ou se conectar tooa [servidor Gateway](https://technet.microsoft.com/library/hh212823.aspx).

SCOM requer dois bancos de dados SQL, um para dados operacionais e outro data warehouse toosupport emissão de relatórios e análise de dados.  Um [Reporting Server](https://technet.microsoft.com/library/hh298611.aspx) tooreport SQL Reporting Services é executado nos dados de data warehouse de saudação. 

O SCOM pode monitorar recursos de nuvem usando pacotes de gerenciamento para produtos como [Azure](https://www.microsoft.com/download/details.aspx?id=38414), [Office 365](https://www.microsoft.com/download/details.aspx?id=43708) e [AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html).  Esses pacotes de gerenciamento usam um ou mais agentes locais como proxies para descobrir executando fluxos de trabalho toomeasure seu desempenho e disponibilidade e recursos de nuvem.  Agentes proxy também são usados muito[monitorar dispositivos de rede](https://technet.microsoft.com/library/hh212935.aspx) e outros recursos externos.

Olá, Console de operações é um aplicativo do Windows que se conecta tooone Olá de servidores de gerenciamento e permite Olá administrador tooview e analisa os dados coletados e configura o ambiente do SCOM hello.  Um console baseado na Web pode ser hospedado em qualquer servidor do IIS e fornece a análise de dados por meio de um navegador.

![Arquitetura do SCOM](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
A maioria dos componentes do OMS estão em Olá nuvem do Azure para que você pode implantar e gerenciá-lo com um custo mínimo e o esforço administrativo.  Todos os dados coletados pela análise de Log é armazenado no repositório do OMS hello.

O Log Analytics pode coletar dados de uma dessas três fontes:

* Máquinas físicas e virtuais que executam o Windows e Olá [agente de monitoramento da Microsoft (MMA)](https://technet.microsoft.com/library/mt484108.aspx) ou Linux e hello [Operations Management Suite Agent para Linux](https://technet.microsoft.com/library/mt622052.aspx).  Esses computadores podem ser locais ou máquinas virtuais do Azure ou de outra nuvem.
* Uma conta do Armazenamento do Azure com os dados do [Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) coletados por uma função de trabalho, função web ou máquina virtual do Azure.
* [Grupo de gerenciamento do SCOM Conexão tooa](https://technet.microsoft.com/library/mt484104.aspx).  Nessa configuração, os agentes de saudação se comunicam com servidores de gerenciamento do SCOM que oferecem o banco de dados do hello dados toohello SCOM onde ele é distribuído, em seguida, repositório de dados do OMS toohello.
  Os administradores analisar os dados coletados e configurar a análise de Log com o portal do OMS Olá que é hospedado no Azure e pode ser acessado em qualquer navegador.  Aplicativos móveis tooaccess esses dados estão disponíveis para plataformas de saudação padrão.

![Arquitetura do Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>Integração do SCOM e do Log Analytics
Quando o SCOM é usado como uma fonte de dados para análise de Log, você pode aproveitar recursos de saudação de ambos os produtos em um ambiente de monitoramento de híbrido.  Você pode configurar agentes SCOM existentes por meio de toobe do Console de operações Olá gerenciados pelo OMS, além de pacotes de gerenciamento de toorun toocontinuing do SCOM.  
Dados de um grupo de gerenciamento do SCOM conectado é entregue tooLog usando um dos quatro métodos de análise:

* Eventos e dados de desempenho são coletados pelo agente hello e entregues tooSCOM.  Servidores de gerenciamento no SCOM, em seguida, entregam Olá dados tooLog análise.
* Alguns eventos como logs do IIS e eventos de segurança continuam toobe diretamente entregues tooLog análise do agente de saudação.
* Algumas soluções serão entregar o agente de toohello software adicional ou exigem que o software seja instalado toocollect os dados adicionais.  Esses dados serão normalmente ser enviados diretamente tooLog análise.
* Algumas soluções coletará dados diretamente dos servidores de gerenciamento do SCOM que se originam do agente de saudação.  Por exemplo, Olá [solução de gerenciamento de alertas](https://technet.microsoft.com/library/mt484092.aspx) coleta alertas do SCOM depois que elas foram criadas.

## <a name="monitoring-logic"></a>Lógica de monitoramento
SCOM e análise de Log de trabalham com dados semelhantes coletados dos agentes, mas têm diferenças fundamentais em como definir e implementar sua lógica de coleta de dados e como eles analisam dados Olá que coletam.

### <a name="operations-manager"></a>Operations Manager
Lógica de monitoramento do SCOM é implementado em [pacotes de gerenciamento](https://technet.microsoft.com/library/hh457558.aspx) que contém a lógica para a descoberta de componentes toomonitor, medir a integridade de saudação desses componentes e para coletar dados tooanalyze.  Os dados de monitoramento podem ser tão simples quanto coletar um evento ou contador de desempenho, ou podem usar uma lógica complexa implementada em um script.  Pacotes de gerenciamento que incluem o monitoramento completo estão disponíveis para uma variedade de [aplicativos Microsoft e de terceiros](http://go.microsoft.com/fwlink/?LinkId=82105) em adição toohardware e dispositivos de rede.  Você pode [criar seus próprios pacotes de gerenciamento](http://aka.ms/mpauthor) para aplicativos personalizados.

Pacotes de gerenciamento contêm vários fluxos de trabalho que cada executa alguma função de monitoramento distinta, como um contador de desempenho de amostragem, verificando o estado de saudação de um serviço ou executar um script.  Cada fluxo de trabalho é executado de forma independente e define seus próprios resultados como banco de dados que ele gravará tooand se ele irá gerar um alerta. 

Você pode substituir os detalhes do fluxo de trabalho como a frequência de saudação que serem executados, onde eles consideram um erro de limite de saudação e Olá severidade do alerta Olá que elas geram.  Também é possível fornecer mais funcionalidade, adicionando seus próprios fluxos de trabalho.

![Substituições](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

Pacotes de gerenciamento são instalados no banco de dados do Operations Manager hello e distribuído tooagents automaticamente pelos servidores de gerenciamento.  Cada agente será automaticamente baixar pacotes de gerenciamento e carregar aplicativos toohello relevantes de fluxos de trabalho que esteja instalado.  Dados coletados pelo agente de saudação é entregue back toohello o servidor de gerenciamento para inserção em Olá banco de dados e data warehouse do SCOM.  Olá Console de operações permite que você tooview e analisar esses dados por meio de exibições personalizadas, painéis e relatórios incluídos no pacote de gerenciamento de saudação.

distribuição de saudação de pacotes de gerenciamento é ilustrada no hello diagrama a seguir.

![Fluxo de pacote de gerenciamento](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>Coleta de eventos e de desempenho
O Log Analytics coleta eventos e contadores de desempenho de sistemas de agente usando fontes, como o log de eventos do Windows, os logs do IIS e o Syslog.  Você pode definir critérios para o qual os dados são coletados por meio do portal da análise de Log hello e, em seguida, criar consultas de Log tooanalyze Olá coletado dados.  Um conjunto de critérios padrão é definido quando você cria seu espaço de trabalho do OMS, e é possível definir dados adicionais para determinados aplicativos. 

![Definindo os logs de eventos no Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

Enquanto o SCOM tem muitos fluxos de trabalho detalhados que normalmente definem critérios específicos para os dados e a ação de saudação que deve ser executada em resposta, a análise de Log tem critérios mais gerais para coleta de dados.  Consultas de log e soluções fornecem mais critérios de destino para analisar e atuar em dados específicos na nuvem Olá depois que ele é coletado.

#### <a name="solutions"></a>Soluções
As soluções fornecem lógica adicional para a análise e coleta de dados.  Você pode selecionar a assinatura do OMS soluções tooadd tooyour de saudação Galeria de soluções.

![Galeria de Soluções](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

Soluções principalmente executados na nuvem de saudação fornecendo análise de eventos e contadores de desempenho coletados no repositório do OMS hello.  Eles também podem definir toobe dados adicionais coletado que pode ser analisado com consultas de Log ou pela interface de usuário adicionais fornecidos pela solução de saudação no painel do OMS hello. 

Por exemplo, Olá [solução controle de alterações](https://technet.microsoft.com/library/mt484099.aspx) detecta alterações em sistemas de agente de configuração e grava eventos toohello OMS repositório que pode ser analisado com vários modos de exibição gráficos que resumem detectou alterações.  Você pode fazer drill down da exibição resumida de saudação em consultas de log que Olá exibição dados coletados pela solução Olá detalhados.

Enquanto você pode selecionar quais soluções Adicionar assinatura tooyour, você não tem Olá capacidade toocreate suas próprias soluções.  Você pode selecionar toocollect de contadores de desempenho e eventos de saudação e criar exibições personalizadas com base em suas próprias consultas de log.

Olá lógica de monitoramento para análise de Log é resumido Olá diagrama a seguir.

![Fluxo da Solução do Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>Monitoramento de integridade
### <a name="operations-manager"></a>Operations Manager
SCOM pode modelar Olá de componentes diferentes de um aplicativo e fornecer uma integridade em tempo real para cada.  Isso permite que você toonot somente exibição detectados erros e o desempenho ao longo do tempo, mas também toovalidate Olá integridade real de um aplicativo ou sistema e cada um de seus componentes em um determinado momento.  Porque ele entende Olá períodos de tempo que um aplicativo está disponível, mecanismo de integridade de saudação no SCOM também dá suporte a contratos de nível de serviço (SLA) que analisar e relatar a disponibilidade de saudação de um aplicativo ao longo do tempo.

Por exemplo, a exibição de Olá abaixo mostra a integridade em tempo real Olá de mecanismos de banco de dados SQL monitorados pelo SCOM.  integridade de saudação de cada um dos bancos de dados de saudação para um dos mecanismos de banco de dados de saudação é mostrada na parte inferior da saudação metade do modo de exibição de saudação.

![Exibição do estado](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

Olá Gerenciador de integridade de um dos mecanismos de banco de dados de saudação é mostrada abaixo com monitores de hello são usada toodetermine sua integridade geral.  Esses monitores são definidos no hello pacote de gerenciamento do SQL e executados em todos os mecanismos de banco de dados SQL descobertos pelo SCOM.

![Gerenciador de integridade](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

Componentes em vários sistemas podem ser combinados toomeasure Olá integridade de um aplicativo distribuído.  Isso pode ser especialmente útil para aplicativos de linha de negócios que incluem vários componentes distribuídos.  Você pode criar um modelo que mede a integridade de saudação de cada componente que pacote cumulativo de atualizações para disponibilidade para o aplicativo hello.

Active Directory é um exemplo de um pacote de gerenciamento que fornece um modelo tooanalyze os componentes distribuídos.  diagrama de exemplo Hello abaixo mostra integridade de saudação do hello ambiente geral e a relação de saudação entre florestas, domínios e controladores de domínio.  Cada um desses componentes inclui subcomponentes e vários monitores exemplo similar de toohello SQL acima.

![Exibição de diagrama do SCOM](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS não incluem um aplicativos comuns do toomodel mecanismo ou medir a integridade em tempo real.  As soluções individuais podem avaliar Olá integridade geral dos serviços específicos com base nos dados coletados e eles podem instalar lógica personalizada em análise em tempo real do hello agente tooperform.  Como soluções são executados na nuvem Olá com o repositório do OMS toohello acesso, eles geralmente fornecem uma análise mais profunda que normalmente é executada por pacotes de gerenciamento. 

Por exemplo, Olá [soluções de avaliação do AD e avaliação de SQL](https://technet.microsoft.com/library/mt484102.aspx) analisa os dados coletados e uma classificação de diferentes aspectos do ambiente de saudação.  Ele inclui recomendações de melhorias que podem ser feitas a disponibilidade de saudação tooimprove e desempenho do ambiente de saudação.

![Solução de Avaliação do AD](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>Análise de Dados
SCOM e análise de Log fornecem recursos diferentes tooanalyze coletado dados.  SCOM tem painéis e modos de exibição no Console de operações de saudação para analisar dados recentes em uma variedade de formatos e relatórios para apresentar dados de data warehouse de saudação em formato tabular.  Análise de log fornece uma linguagem de consulta de log completo e a interface para analisar dados no repositório do OMS hello.  Quando SCOM é usado como uma fonte de dados para análise de Log, o repositório Olá inclui dados coletados pelo SCOM para que ferramentas de análise de Log Olá possam ser usados tooanalyze dados de ambos os sistemas.

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>Modos de exibição
Modos de exibição no Console de operações de saudação permitem que você tooview diferentes tipos de dados coletados pelo SCOM em formatos diferentes, geralmente tabulares para eventos, alertas e os dados de estado e gráficos de linha para dados de desempenho.  Modos de exibição executam análise mínima ou consolidação de dados de saudação mas permitem que você toofilter de acordo com os critérios de tooparticular. 

![Modos de exibição](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

Pacotes de gerenciamento normalmente fornecem várias exibições com suporte a aplicativo hello ou sistema que ele monitora.  Isso pode incluir modos de exibição de estado para objetos diferentes Olá Olá pacote de gerenciamento descobre, modos de exibição para problemas detectados e modos de exibição de desempenho para contadores de alerta.

Modos de exibição são especialmente adequados para analisar o estado atual de saudação do ambiente de hello, incluindo alertas abertos e estado de integridade de saudação de sistemas monitorados e objetos.  Você pode analisar dados de evento ou desempenho de toodetailed com suporte a um determinado alerta em ordem toodiagnose sua causa. Da mesma forma, você pode exibir a integridade dos diferentes componentes de um aplicativo tooassess e o desempenho de saudação sua integridade atual.

#### <a name="dashboards"></a>Painéis
Painéis no hello Console de operações trabalhar principalmente com hello mesmos dados como exibições mas são mais personalizáveis e podem incluir visualizações mais ricas.  Um conjunto de painéis padrão que pode ser personalizado com facilidade está disponível para propósitos pessoais.  Você também pode usar um widget do PowerShell que pode exibir os dados retornados de uma consulta do PowerShell.

![Painel](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

Os desenvolvedores têm Olá capacidade tooadd componentes personalizados toodashboards incluem em seus pacotes de gerenciamento.  Eles podem ser determinado aplicativo tooa altamente especializados, como o painel Olá Olá pacote de gerenciamento do SQL mostrado abaixo.  Este painel também pode ser usado como modelo para versões personalizadas.

![Painel do SQL](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>Relatórios
Relatórios no SCOM analisam dados de data warehouse de saudação em formato tabular.  Eles podem ser impressos e agendados para a entrega automatizada em formatos de arquivo diferentes, incluindo PDF, CSV e Word.  Os relatórios funcionam com dados de data warehouse do hello então são adequados especialmente para análise de tendências de longo prazo.

Geralmente, os pacotes de gerenciamento fornecerão relatórios personalizados para determinado aplicativo.  Também é possível selecionar em uma biblioteca de relatórios genéricos que podem ser personalizados para seus próprios aplicativos ou para a execução de análise ad hoc.

A seguir está um exemplo de relatório de desempenho mostrando os dados coletados pelo Olá pacote de gerenciamento do Active Directory.

![Relatório](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
Análise de log tem um [de linguagem de consulta](https://technet.microsoft.com/library/mt484120.aspx) que você pode usar tooperform análise em dados de vários aplicativos sem Olá necessidade toocreate um modo de exibição personalizado ou um relatório.  Como o OMS é implementado na nuvem hello, desempenho de consultas e análise de dados não são as limitações de hardware do assunto tooany e pode analisar rapidamente consultas incluindo milhões de registros. 

Consultas de análise de Log também são base Olá de outros recursos.  Você pode salvar uma consulta, exportar seu resultados tooExcel ou que ele seja automaticamente executada em intervalos regulares e gerar um alerta se seus resultados correspondem a critérios específicos.  

![Fluxo de consulta de log](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

Veja abaixo um exemplo de uma consulta do Log Analytics.  Neste exemplo, todos os eventos com "iniciado" no nome de saudação são retornados e agrupados por evento ID.  usuário Olá simplesmente fornece consulta hello e análise de Log gera dinamicamente a análise de Olá Olá usuário interface tooperform.  Selecionar qualquer item na lista de saudação retornará Olá obter dados de evento.

![Consulta de log](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

Além disso tooproviding de análise ad hoc, consultas de análise de Log podem ser salvos para uso futuro e também adicionado tooyour [painel OMS](http://technet.microsoft.com/library/mt484090.aspx) conforme mostrado no exemplo a seguir de saudação.

![painel do OMS](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>Próximas etapas
* Implante o [SCOM (System Center Operations Manager)](https://technet.microsoft.com/library/hh205987.aspx).
* Inscreva-se no [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics).  

