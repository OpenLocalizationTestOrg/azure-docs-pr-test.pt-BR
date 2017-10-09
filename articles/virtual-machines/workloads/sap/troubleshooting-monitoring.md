---
title: "aaaTroubleshooting e monitoramento do SAP HANA no Azure (instâncias grandes) | Microsoft Docs"
description: "Solução de problemas e monitoramento do SAP HANA no Azure (Instâncias Grandes)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Como tootroubleshoot e monitor SAP HANA (instâncias grandes) no Azure


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>Monitoramento no SAP HANA no Azure (Instâncias Grandes)

SAP HANA no Azure (instâncias grandes) não é diferente de qualquer outra implantação de IaaS — necessário toomonitor que Olá o sistema operacional e o aplicativo hello é isso e como elas consomem Olá recursos a seguir:

- CPU
- Memória
- Largura de banda de rede
- Espaço em disco

Como com as máquinas virtuais do Azure, você precisa toofigure se classes de recursos Olá citados acima são suficientes ou se eles obtenham esgotados. Aqui estão mais detalhes sobre cada uma das classes diferentes de saudação:

**Consumo de recursos de CPU:** taxa de saudação SAP definido para determinadas cargas de trabalho em relação a HANA é imposto toomake-se de que deve ser suficiente recursos de CPU disponível toowork pelos dados de saudação que são armazenados na memória. No entanto, pode haver casos onde HANA consome muito da CPU ao executar consultas de conclusão toomissing índices ou problemas semelhantes. Isso significa que você deve monitorar o consumo de recursos de CPU de unidade de instância grande HANA hello, bem como recursos de CPU consumidos por serviços específicos de HANA hello.

**Consumo de memória:** é importante toomonitor de dentro do HANA, bem como fora do HANA na unidade de saudação. Dentro do HANA, monitore como dados saudação está consumindo HANA alocada memória em ordem toostay em Olá necessário dimensionar as diretrizes do SAP. Você também deseja toomonitor o consumo de memória em toomake nível de instância grande de saudação se software adicional instalado não-HANA não consomem muita memória e, portanto, concorre com HANA para a memória.

**Largura de banda de rede:** gateway de rede virtual do Azure Olá é limitado em largura de banda de dados em movimento em Olá VNet do Azure, portanto, é útil dados de saudação toomonitor recebidos por todos os Olá VMs do Azure dentro de um toofigure VNet o quão distante você toohello limites de saudação do Azure Gateway SKU selecionada. Na unidade de instância grande HANA Olá, ele fazer sentido toomonitor entrada e saída de tráfego de rede bem e acompanhar tookeep de volumes de saudação que são tratadas ao longo do tempo.

**Espaço em disco:** normalmente, o consumo de espaço em disco aumenta ao longo do tempo. Há muitos motivos para isso, mas a maioria deles é: aumento no volume de dados, execução de backups do log de transações, armazenamento de arquivos de rastreamento e execução de instantâneos de armazenamento. Portanto, é importante toomonitor uso de espaço em disco e gerenciar o espaço de disco Olá associado Olá instância grande HANA unidade.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>Monitoramento e solução de problemas no lado do HANA

Em ordem tooeffectively analisar problemas relacionados tooSAP HANA no Azure (instâncias grandes), é útil toonarrow para baixo da causa raiz de saudação de um problema. SAP publicou uma grande quantidade de documentação toohelp você.

Aplicável perguntas frequentes relacionadas tooSAP HANA desempenho pode ser encontrado no hello SAP observações a seguir:

- [Nota SAP nº 2222200 – Perguntas frequentes: Rede SAP HANA](https://launchpad.support.sap.com/#/notes/2222200)
- [Nota SAP nº 2100040 – Perguntas frequentes: CPU SAP HANA](https://launchpad.support.sap.com/#/notes/0002100040)
- [Nota SAP nº 199997 – Perguntas frequentes: Memória SAP HANA](https://launchpad.support.sap.com/#/notes/2177064)
- [Nota SAP nº 200000 – Perguntas frequentes: Otimização de desempenho SAP HANA](https://launchpad.support.sap.com/#/notes/2000000)
- [Nota SAP nº 199930 – Perguntas frequentes: Análise de E/S SAP HANA](https://launchpad.support.sap.com/#/notes/1999930)
- [Nota da SAP #2177064 – Perguntas frequentes: Reinicialização e falhas do serviço SAP HANA](https://launchpad.support.sap.com/#/notes/2177064)

**Alertas do SAP HANA**

Como uma primeira etapa, verifique os logs atuais de alerta de SAP HANA hello. SAP HANA Studio, vá muito**Console de administração: alertas: mostrar: todos os alertas**. Este guia mostrará todos os alertas do SAP HANA valores específicos (memória física livre, utilização da CPU, etc.) que estão fora da saudação definir mínimo e máximo limites. Por padrão, as verificações são atualizados automaticamente a cada 15 minutos.

![No SAP HANA Studio, vá tooAdministration Console: alertas: mostrar: todos os alertas](./media/troubleshooting-monitoring/image1-show-alerts.png)

**CPU**

Para um alerta foi disparado devido a configuração de limite de tooimproper, uma resolução é valor de padrão de toohello tooreset ou um valor de limite mais razoável.

![Redefinir o valor padrão de toohello ou um valor de limite mais razoável](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

Olá alertas a seguir pode indicar problemas de recursos de CPU:

- Uso de CPU Host (Alerta 5)
- Operação de ponto de salvamento mais recente (Alerta 28)
- Duração do ponto de salvamento (Alerta 54)

Você pode observar o alto consumo de CPU em seu banco de dados do SAP HANA da saudação seguinte:

- O Alerta 5 (Uso de CPU Host) é emitido para o uso de CPU atual ou anterior
- Olá exibido o uso da CPU na tela de visão geral de saudação

![Exibido o uso da CPU na tela de visão geral de saudação](./media/troubleshooting-monitoring/image3-cpu-usage.png)

gráfico de carga Olá pode mostrar o alto consumo de CPU ou alto consumo nas Olá anterior:

![gráfico de carga Olá pode mostrar o alto consumo de CPU ou alto consumo nas Olá anterior](./media/troubleshooting-monitoring/image4-load-graph.png)

Um alerta disparado devido a utilização de CPU de toohigh pode ser causado por vários motivos, incluindo, mas não se limitando a: execução de determinadas transações, o carregamento de dados, o deslocamento de trabalhos de longa execução instruções SQL e o desempenho de consulta inválida (por exemplo, com BW em HANA cubos).

Consulte toohello [solução de problemas do SAP HANA: soluções e CPU relacionados faz com que o](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site para etapas de solução de problemas detalhada.

**Sistema operacional**

Um dos mais importantes de saudação verifica para SAP HANA no Linux é toomake se páginas enorme transparente estiver desabilitadas, consulte [2131662 de # nota SAP – transparente enorme páginas (THP) em servidores do SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).

- Você pode verificar se páginas enorme transparente são habilitadas por meio de saudação Linux comando a seguir: **cat /sys/kernel/mm/transparent\_hugepage/habilitado**
- Se _sempre_ é colocado entre colchetes, como a seguir, isso significa que páginas enorme transparente de saudação estão habilitadas: [sempre] madvise nunca; se _nunca_ é colocado entre colchetes, como a seguir, isso significa que Olá transparente Páginas enormes estão desabilitadas: sempre madvise [nunca]

Olá Linux comando a seguir deve retornar nada: **rpm - qa | grep ulimit.** Se parecer que _ulimit_ está instalado, desinstale-o imediatamente.

**Memória**

Você pode observar essa quantidade de saudação de memória alocada pelo Olá SAP HANA banco de dados é maior do que o esperado. Olá alertas a seguir indica problemas com alto uso da memória:

- Uso de memória do host físico (Alerta 1)
- Uso de memória do servidor de nomes (Alerta 12)
- Uso total da memória das tabelas do Repositório de Colunas (Alerta 40)
- Uso de memória dos serviços (Alerta 43)
- Uso de memória do armazenamento principal das tabelas do Repositório de Colunas (Alerta 45)
- Arquivos de despejo em tempo de execução (Alerta 46)

Consulte toohello [solução de problemas do SAP HANA: problemas de memória](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site para etapas de solução de problemas detalhada.

**Rede**

Consulte também[2081065 de # nota SAP – Solucionando problemas de rede do SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) e executar as etapas nesta nota da SAP de solução de problemas de rede de saudação.

1. Análise do tempo de ida e volta entre o cliente e servidor.
  R. Executar script SQL Olá [ _HANA\_rede\_clientes_](https://launchpad.support.sap.com/#/notes/1969700)_._
  
2. Análise da comunicação entre nós.
  R. Execute o script SQL [_HANA\_Rede\_Serviços_](https://launchpad.support.sap.com/#/notes/1969700)_._

3. Execute o comando do Linux **ifconfig** (saída Olá mostra se quaisquer perdas de pacote estão ocorrendo).
4. Execute o comando Linux **tcpdump**.

Além disso, use o código-fonte aberto Olá [IPERF](https://iperf.fr/) ferramenta (ou semelhante) toomeasure desempenho de rede do aplicativo real.

Consulte toohello [solução de problemas do SAP HANA: desempenho do sistema de rede e problemas de conectividade](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site para etapas de solução de problemas detalhada.

**Armazenamento**

Da perspectiva do usuário final, um aplicativo (ou sistema hello como um todo) é executado lentamente, não está respondendo ou até mesmo pode parecer toohang se houver problemas com o desempenho de e/s. Em Olá **Volumes** guia SAP HANA Studio, você pode ver Olá anexado volumes e quais volumes são usadas por cada serviço.

![Na guia de Volumes de saudação do SAP HANA Studio, você pode ver Olá anexado volumes e quais volumes são usadas por cada serviço](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

Na parte inferior de saudação da tela hello de que você pode ver os detalhes seus volumes anexados Olá volumes, como arquivos e estatísticas de e/s.

![Na parte inferior de saudação da tela hello de que você pode ver os detalhes seus volumes anexados Olá volumes, como arquivos e estatísticas de e/s](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

Consulte toohello [solução de problemas do SAP HANA: e/s relacionadas causas e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) e [solução de problemas do SAP HANA: disco relacionadas causas e soluções](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site para etapas de solução de problemas detalhada.

**Ferramentas de Diagnóstico**

Execute uma Verificação de Integridade do SAP HANA por meio do HANA\_Configuration\_Minichecks. Essa ferramenta retorna possíveis problemas técnicos críticos que devem já ter sido gerados como alertas no SAP HANA Studio.

Consulte também[1969700 de # nota SAP – conjunto de instrução SQL para o SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) e baixar Observação do hello SQL Statements.zip arquivo toothat anexado. Armazene esse arquivo. zip na unidade de disco rígido local hello.

No Studio do HANA SAP, em Olá **informações do sistema** guia, clique com botão direito no hello **nome** coluna e selecione **instruções SQL de importação**.

![No SAP HANA Studio, na guia de informações do sistema Olá, clique na coluna de nome hello e selecione instruções SQL de importação](./media/troubleshooting-monitoring/image7-import-statements-a.png)

Selecione Olá SQL Statements.zip arquivo armazenado localmente e uma pasta com instruções SQL correspondentes de saudação será importada. Neste ponto, Olá que várias verificações de diagnósticas diferentes podem ser executadas com essas instruções SQL.

Por exemplo, os requisitos de largura de banda de replicação de sistema do SAP HANA tootest, clique Olá **largura de banda** instrução em **replicação: largura de banda** e selecione **abrir** no Console do SQL.

instrução de SQL completa Olá abre toobe de parâmetros de entrada (seção de modificação) permitindo alterado e, em seguida, é executado.

![instrução de SQL completa Olá abre toobe de parâmetros de entrada (seção de modificação) permitindo alterado e, em seguida, executado](./media/troubleshooting-monitoring/image8-import-statements-b.png)

Outro exemplo é com o botão direito em instruções de saudação em **replicação: Visão geral do**. Selecione **Execute** Olá no menu de contexto:

![Outro exemplo é com o botão direito em instruções de saudação em replicação: Visão geral. Selecione executar no menu de contexto de saudação](./media/troubleshooting-monitoring/image9-import-statements-c.png)

Isso resulta em informações que ajudam com a solução de problemas:

![Isso resultará em informações que ajudam com a solução de problemas](./media/troubleshooting-monitoring/image10-import-statements-d.png)

Olá mesmo para HANA\_configuração\_Minichecks e verificar se há qualquer _X_ marcas no hello _C_ coluna (crítico).

Exemplos de saída:

**HANA\_Configuration\_MiniChecks\_Rev102.01+1** para verificações gerais do SAP HANA.

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 para verificações gerais SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_Services\_Overview** para uma visão geral de quais serviços SAP HANA estão em execução no momento.

![HANA\_Services\_Overview para uma visão geral de quais serviços SAP HANA estão em execução no momento](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_Services\_Statistics** para informações de serviço do SAP HANA (CPU, memória etc.).

![HANA\_Services\_Statistics para informações de serviço do SAP HANA ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_configuração\_visão geral\_Rev110 +** para obter informações gerais sobre a instância do SAP HANA hello.

![HANA\_configuração\_visão geral\_Rev110 + para obter informações gerais sobre a instância do SAP HANA Olá](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_configuração\_parâmetros\_Rev70 +** toocheck parâmetros de SAP HANA.

![HANA\_configuração\_parâmetros\_Rev70 + toocheck parâmetros de SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

