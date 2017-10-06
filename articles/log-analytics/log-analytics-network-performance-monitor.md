---
title: "aaaNetwork solução de Monitor de desempenho no Azure Log Analytics | Microsoft Docs"
description: "Monitor de desempenho de rede no Azure Log Analytics ajuda você a monitorar o desempenho de saudação de suas redes no próximo toodetect de tempo real e localizar os afunilamentos de desempenho de rede."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: e074948221fdd003c640861d759c4ce69ced1cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-performance-monitor-solution-in-log-analytics"></a>Solução Monitor de Desempenho de Rede no Azure Log Analytics

![Símbolo do Monitor de Desempenho de Rede](./media/log-analytics-network-performance-monitor/npm-symbol.png)

Este documento descreve como tooset-up e use Olá solução de Monitor de desempenho de rede em análise de Log, o que ajuda a monitorar o desempenho de saudação de suas redes no próximo toodetect de tempo real e localizar os afunilamentos de desempenho de rede. Com hello solução do Monitor de desempenho de rede, você pode monitorar perda hello e latência entre duas redes, servidores ou sub-redes. Monitor de desempenho de rede detecta problemas de rede como blackholing de tráfego, roteamento erros e problemas de métodos de monitoramento de rede convencional não são capaz toodetect. O Monitor de Desempenho de Rede gera alertas e notifica como e quando um limite é ultrapassado para um link de rede. Esses limites podem ser aprendidos automaticamente pelo sistema hello, ou você pode configurar regras de alerta personalizado toouse. Monitor de desempenho de rede garante a detecção oportuna de problemas de desempenho de rede e localiza a origem de saudação do hello problema tooa determinado segmento de rede ou dispositivo.

Você pode detectar problemas de rede com o painel de solução de saudação que exibe informações resumidas sobre a sua rede, incluindo eventos de integridade de rede recentes, links de rede não íntegro e links de sub-rede que enfrentam a latência e alta perda de pacotes. Você pode busca detalhada em uma rede link tooview Olá atual status de integridade de links de sub-rede, bem como links de nó para nó. Você também pode exibir as tendências históricas de saudação da perda e latência de rede hello, sub-rede e nível de nó para nó. Você pode detectar problemas de rede transitórios exibindo gráficos de tendências históricas de perda de pacotes e latência e localizar afunilamentos de rede em um mapa de topologia. gráfico de topologia interativo Olá permite que as rotas de rede de salto por salto de saudação toovisualize e determinar Olá origem do problema de saudação. Como outras soluções, você pode usar a pesquisa de Log de análise de vários relatórios personalizados do toocreate requisitos com base nos dados de saudação coletados pelo Monitor de desempenho de rede.

solução de saudação usa transações sintéticas como falhas na rede toodetect um mecanismo principal. Assim, você pode usá-la sem levar em consideração o fornecedor ou modelo de um dispositivo de rede específico. Ele funciona no local, na nuvem (IaaS) e em ambientes híbridos. solução Olá detecta automaticamente a topologia de rede hello e várias rotas em sua rede.

Rede típica monitoramento produtos enfocam monitoramento Olá integridade do dispositivo (roteadores, comutadores etc.) de rede, mas não fornecem informações sobre a qualidade real Olá de conectividade de rede entre dois pontos, o que faz do Monitor de desempenho de rede.

### <a name="using-hello-solution-standalone"></a>Usando Olá solução autônoma
Se desejar que a qualidade de saudação toomonitor de conexões de rede entre as cargas de trabalho críticas, redes, datacenters ou sites do office, você pode usar solução de Monitor de desempenho de rede de saudação por si só toomonitor integridade da conectividade entre:

* vários datacenters ou sites do Office conectados por meio de uma rede pública ou privada
* cargas de trabalho críticas que estão executando aplicativos de linha de negócios
* Serviços de nuvem pública como o Microsoft Azure ou redes serviços AWS (Amazon Web) e no local, se você tiver IaaS (VM) disponível e você tiver gateways configurado tooallow comunicação entre redes locais e redes de nuvem
* Redes do Azure e locais quando você usar o ExpressRoute

### <a name="using-hello-solution-with-other-networking-tools"></a>Usando a solução de saudação com outras ferramentas de rede
Se você quiser toomonitor um aplicativo de linha de negócios, você pode usar o hello solução do Monitor de desempenho de rede como ferramentas de rede um complementar solução tooother. Uma rede lenta pode levar aplicativos tooslow e Monitor de desempenho de rede pode ajudá-lo a investigar problemas de desempenho de aplicativo são causados por problemas de rede subjacentes. Porque Olá solução não requer quaisquer dispositivos toonetwork de acesso, o administrador de aplicativo hello não precisa toorely em uma rede team tooprovide saber como rede hello está afetando os aplicativos.

Além disso, se você já investir em outra ferramentas de monitoramento de rede, solução de saudação pode complementar essas ferramentas porque mais tradicionais soluções de monitoramento de rede não fornecem informações sobre métricas de desempenho de rede de ponta a ponta como perda e latência.  Olá solução do Monitor de desempenho de rede pode ajudar a preencher essa lacuna.

## <a name="installing-and-configuring-agents-for-hello-solution"></a>Instalando e Configurando agentes para solução de saudação
Usar Olá processos básicos tooinstall agentes em [Windows conectar computadores tooLog análise](log-analytics-windows-agents.md) e [tooLog conectar o Operations Manager análise](log-analytics-om-agents.md).

> [!NOTE]
> Você precisa agentes tooinstall pelo menos 2 na ordem toohave suficiente toodiscover de dados e monitorar os recursos de rede. Caso contrário, solução de saudação permanecerá em um estado de configuração até você instalar e configurar agentes adicionais.
>
>

### <a name="where-tooinstall-hello-agents"></a>Onde tooinstall Olá agentes
Antes de instalar agentes, considere a topologia de saudação da sua rede e quais partes da saudação rede que você deseja toomonitor. É recomendável que você instalar mais de um agente para cada sub-rede que você deseja toomonitor. Em outras palavras, para cada sub-rede que você deseja toomonitor, escolha dois ou mais servidores ou máquinas virtuais e instalar o agente de saudação neles.

Se você não tiver certeza sobre a topologia de saudação da sua rede, instale agentes de saudação em servidores com cargas de trabalho críticas, onde você deseja que o desempenho da rede toomonitor hello. Por exemplo, convém rastrear tookeep de uma conexão de rede entre um servidor Web e um servidor executando o SQL Server. Neste exemplo, você deve instalar um agente em ambos os servidores.

Os agentes monitoram a conectividade de rede (links) entre o host não Olá próprios hosts. Toomonitor caso, um link de rede, você deve instalar agentes em ambos os pontos de extremidade do link.

### <a name="configure-agents"></a>Configurar agentes

Protocolo ICMP toouse Olá para transações sintéticas, você deverá tooenable Olá seguindo as regras de firewall de forma confiável utilizando o ICMP:

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow
```


Se você pretende toouse Olá protocolo TCP, você precisa tooopen portas de firewall para tooensure os computadores que os agentes podem se comunicar. Você precisar toodownload e, em seguida, executar Olá [script do PowerShell EnableRules.ps1](https://gallery.technet.microsoft.com/OMS-Network-Performance-04a66634) sem parâmetros em uma janela do PowerShell com privilégios administrativos.

script Hello cria chaves do registro necessárias pelo Olá Monitor de desempenho de rede e ele cria conexões de TCP regras tooallow agentes toocreate firewall do Windows com o outro. chaves de registro de saudação criadas pelo script hello também especificam se toolog Olá depurar logs e o caminho de saudação para o arquivo de logs de saudação. Ele também define a porta TCP de agente Olá usada para comunicação. valores Hello para essas chaves são definidos automaticamente pelo script hello, portanto você não deve alterar manualmente essas chaves.

porta Olá aberta por padrão é 8084. Você pode usar uma porta personalizada, fornecendo o parâmetro hello `portNumber` toohello script. No entanto, hello mesma porta deve ser usada em todos os computadores de saudação onde o script hello é executado.

> [!NOTE]
> Olá EnableRules.ps1 script configura regras de firewall do Windows somente no computador Olá onde o script hello é executado. Se você tiver um firewall de rede, você deve garantir que ele permite que o tráfego destinado para a porta TCP hello está sendo usada pelo Monitor de desempenho de rede.
>
>

## <a name="configuring-hello-solution"></a>Configurando a solução Olá
Use Olá tooinstall informações a seguir e configurar a solução de saudação.

1. Olá solução do Monitor de desempenho de rede obtém dados de computadores que executam o Windows Server 2008 SP 1 ou posterior ou Windows 7 SP1 ou posterior, que são Olá mesmo requisitos de Olá agente de monitoramento da Microsoft (MMA). Agentes NPM também podem executar na área de trabalho/sistemas operacionais Windows (Windows 10, Windows 8.1, Windows 8 e Windows 7).
    >[!NOTE]
    >agentes de saudação para sistemas operacionais Windows server oferecem suporte a TCP e ICMP como protocolos de saudação para transação sintética. No entanto, agentes Olá para sistemas operacionais Windows client suportam somente ICMP como protocolo de saudação para transação sintética.

2. Adicionar espaço de trabalho do hello Monitor de desempenho de rede solução tooyour de [marketplace do Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.NetworkMonitoringOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).  
   ![Símbolo do Monitor de Desempenho de Rede](./media/log-analytics-network-performance-monitor/npm-symbol.png)
3. No portal do OMS hello, você verá um novo bloco intitulado **Monitor de desempenho de rede** com mensagem de saudação *solução requer configuração adicional*. Você precisará redes de tooadd tooconfigure Olá solução com base em sub-redes e nós que são detectados pelos agentes. Clique em **Monitor de desempenho de rede** toostart Configurando a rede de padrão de saudação.  
   ![A solução requer configuração adicional](./media/log-analytics-network-performance-monitor/npm-config.png)

### <a name="configure-hello-solution-with-a-default-network"></a>Configurar a solução de saudação com uma rede padrão
Na página de configuração hello, você verá uma única rede denominada **padrão**. Quando você não tiver definido as redes, todas as sub-redes descobertas automaticamente Olá são colocadas na rede de padrão de saudação.

Sempre que você criar uma rede, você adiciona um tooit de sub-rede e a sub-rede é removido da rede de padrão de saudação. Se você excluir uma rede, todas as suas sub-redes são retornadas automaticamente toohello padrão rede.

Em outras palavras, a rede de padrão de saudação é contêiner Olá para todas as sub-redes de saudação que não estão contidos em qualquer rede definida pelo usuário. Você não pode editar ou excluir a rede de padrão de saudação. Ela sempre permanece no sistema de saudação. No entanto, você poderá criar tantas redes quantas forem necessárias.

Na maioria dos casos, sub-redes Olá em sua organização serão organizados em mais de uma rede e você deverá criar um ou mais toologically de redes suas sub-redes de grupo.

### <a name="create-new-networks"></a>Criar novas redes
Uma rede no Monitor de Desempenho de Rede é um contêiner de sub-redes. Você pode criar uma rede com qualquer nome que você deseja e adicionar sub-redes toohello rede. Por exemplo, você pode criar uma rede chamada *Building1* e, em seguida, adicionar sub-redes, ou você pode criar uma rede chamada *DMZ* e, em seguida, adicione todas as sub-redes que pertencem a rede de toothis toodemilitarized região.

#### <a name="toocreate-a-new-network"></a>toocreate uma nova rede
1. Clique em **Adicionar rede** e, em seguida, digite o nome de rede de hello e descrição.
2. Selecione uma ou mais sub-redes e clique em **Adicionar**.
3. Clique em **salvar** toosave configuração de saudação.  
   ![adicionar rede](./media/log-analytics-network-performance-monitor/npm-add-network.png)

### <a name="wait-for-data-aggregation"></a>Aguardar a agregação de dados
Depois de salvar a configuração Olá pela primeira vez, a solução de saudação começa coletando informações de perda e latência de pacote de rede entre os nós de saudação onde os agentes estão instalados. Esse processo pode levar algum tempo, às vezes, 30 minutos. Durante esse estado, o bloco de Monitor de desempenho de rede de saudação na página de visão geral de saudação exibe uma mensagem informando *agregação de dados no processo*.

![agregação de dados em andamento](./media/log-analytics-network-performance-monitor/npm-aggregation.png)

Quando dados saudação foi carregados, você verá dados mostrando de bloco atualizado do Monitor de desempenho de rede de saudação.

![Bloco do Monitor de Desempenho de Rede](./media/log-analytics-network-performance-monitor/npm-tile.png)

Clique em Painel de controle do hello bloco tooview Olá Monitor de desempenho de rede.

![Painel do Monitor de Desempenho de Rede](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="edit-monitoring-settings-for-subnets"></a>Editar configurações de monitoramento para sub-redes
Todas as sub-redes em que pelo menos um agente foi instalado são listadas na Olá **sub-redes** guia, na página de configuração de saudação.

#### <a name="tooenable-or-disable-monitoring-for-particular-subnetworks"></a>tooenable ou desabilite o monitoramento para sub-redes específicos
1. Marque ou desmarque Olá caixa próxima toohello **ID de subrede** e, em seguida, verifique se **uso para monitoramento** está marcada ou desmarcada, conforme apropriado. Você pode marcar ou desmarcar várias sub-redes. Quando desabilitado, sub-redes não são monitoradas como agentes de saudação será atualizado toostop ping outros agentes.
2. Escolha nós Olá que você deseja toomonitor para uma determinada sub-rede selecionando sub-rede Olá de lista hello e mover Olá nós necessárias entre as listas de saudação que contém nós de não monitorados e monitorados.
   Você pode adicionar um personalizado **descrição** toohello de subrede, se desejar.
3. Clique em **salvar** toosave configuração de saudação.  
   ![editar sub-rede](./media/log-analytics-network-performance-monitor/npm-edit-subnet.png)

### <a name="choose-nodes-toomonitor"></a>Escolha toomonitor nós
Todos os nós de saudação que tem um agente instalado neles estão listados na Olá **nós** guia.

#### <a name="tooenable-or-disable-monitoring-for-nodes"></a>tooenable ou desabilite o monitoramento para nós
1. Marque ou desmarque nós Olá que você deseja toomonitor ou interromper o monitoramento.
2. Clique em **Usar para Monitoramento** ou desmarque essa opção, conforme apropriado.
3. Clique em **Salvar**.  
   ![habilitar o monitoramento de nós](./media/log-analytics-network-performance-monitor/npm-enable-node-monitor.png)

### <a name="set-monitoring-rules"></a>Definir regras de monitoramento
Monitor de desempenho de rede gera eventos de integridade sobre conectividade de saudação entre um par de nós ou links de rede ou sub-rede quando um limite for ultrapassado. Esses limites podem ser aprendidos automaticamente pelo sistema hello, ou você pode configurar regras de alerta personalizadas.

Olá *regra padrão* é criado pelo sistema hello e cria um evento sempre que a perda ou a latência entre qualquer par de redes ou sub-rede vincula aprendeu sistema limite de saudação violações de integridade. Você pode escolher toodisable saudação padrão regra e criar regras personalizadas para monitoramentos

#### <a name="toocreate-custom-monitoring-rules"></a>toocreate personalizado de regras de monitoramento
1. Clique em **Adicionar regra** em Olá **Monitor** guia e insira o nome da regra hello e descrição.
2. Selecione o par de saudação de toomonitor de links de rede ou sub-rede das listas de saudação.
3. Primeiro selecione a rede Olá no qual Olá primeira sub-rede/s de interesse está contido na lista suspensa de rede hello e selecione Olá sub-rede/s na lista suspensa de sub-rede correspondente hello.
   Selecione **todas as sub-redes** se você quiser toomonitor todos Olá sub-redes em um link de rede. Da mesma forma, selecione Olá outra sub-rede/s de interesse. E, você pode clicar em **Adicionar exceção** tooexclude monitoramento para links de sub-rede específica da seleção Olá você fez.
4. Escolha entre os protocolos TCP e ICMP para executar transações sintéticas.
5. Se você não quiser toocreate eventos de integridade para itens de saudação que você selecionou, desmarque **habilitar o monitoramento de integridade em links de saudação coberto por essa regra**.
6. Escolha as condições de monitoramento.
   Você pode definir limites personalizados para geração de eventos de integridade digitando os valores de limite. Sempre que o valor de saudação da condição de saudação ultrapasse seu limite selecionado para o par de rede/sub-rede selecionada hello, será gerado um evento de integridade.
7. Clique em **salvar** toosave configuração de saudação.  
   ![criar regra de monitoramento personalizada](./media/log-analytics-network-performance-monitor/npm-monitor-rule.png)

Depois de salvar uma regra de monitoramento, você pode integrar essa regra ao Gerenciamento de Alertas clicando em **Criar Alerta**. Uma regra de alerta é criada automaticamente com a consulta de pesquisa hello e outras parâmetros preenchidos automaticamente. Usando uma regra de alerta, você pode receber alertas por email, além de toohello de alertas existentes dentro de NPM. Os alertas também podem disparar ações corretivas com runbooks ou podem integrar soluções de gerenciamento de serviço existentes usando webhooks. Você pode clicar em **alerta gerenciar** tooedit configurações de alerta de saudação.

### <a name="choose-hello-right-protocol-icmp-or-tcp"></a>Escolha o ICMP de protocolo da direita hello ou TCP

Monitor de desempenho de rede (NPM) usa as métricas de desempenho de rede transações sintéticas toocalculate como latência de perda e o link do pacote. toounderstand isso melhor, considere uma NPM agente tooone conectado de término de um link de rede. Este NPM agente envia investigação pacotes tooa segundo NPM agente tooanother conectado final da rede hello. Olá segundo agente as respostas com pacotes de resposta. Esse processo é repetido algumas vezes. Medindo o número de saudação de respostas e o tempo gasto tooreceive cada resposta, agente NPM primeiro Olá avalia a latência de link e descartes de pacotes.

Olá formato, o tamanho e a sequência desses pacotes é determinado pelo protocolo de saudação que você escolher ao criar regras de monitoramento. Com base no protocolo de pacotes de saudação, Olá dispositivos de rede intermediários (roteadores, comutadores etc.) pode processar esses pacotes de maneira diferente. Consequentemente, sua escolha de protocol afeta precisão Olá dos resultados de saudação. Além disso, sua escolha de protocol também determina se você deve executar etapas manuais depois de implantar a solução NPM hello.

NPM oferece que Olá escolha entre os protocolos TCP e ICMP para executar transações sintéticas.
Se você escolher ICMP quando você criar uma regra de transação sintética, usado pelos agentes NPM de saudação latência de rede do protocolo ICMP mensagens toocalculate hello e perda de pacotes. Saudação de usa de eco ICMP mesma mensagem que é enviada pelo utilitário de Ping convencional Olá. Quando você usa o TCP como protocolo de saudação, os agentes NPM enviar pacote TCP SYN pela rede hello. Isso é seguido por um handshake TCP conclusão e, em seguida, remover conexão hello usando pacotes de primeira.

#### <a name="points-tooconsider-before-choosing-hello-protocol"></a>Tooconsider pontos antes de escolher o protocolo de saudação
Considere Olá informações a seguir antes de escolher um toouse de protocolo:

##### <a name="discovering-multiple-network-routes"></a>Descobrindo várias rotas de rede
O TCP é mais preciso ao descobrir várias rotas e exige menos agentes em cada sub-rede. Por exemplo, um ou dois agentes que usem TCP podem descobrir todos os caminhos redundantes entre sub-redes. No entanto, você precisa usando ICMP tooachieve semelhantes resultados de vários agentes. Usando o ICMP e, se você tiver *N* número de rotas entre duas sub-redes, precisará de mais de 5*N* agentes na sub-rede de origem ou de destino.

##### <a name="accuracy-of-results"></a>Precisão dos resultados
Roteadores e switches tendem tooassign menor prioridade tooICMP ECHO pacotes comparados tooTCP pacotes. Em determinadas situações, quando os dispositivos de rede sobrecarregados, Olá obtido por TCP mais de perto refletem perda hello e latência apresentados por aplicativos. Isso ocorre porque a maioria do tráfego do aplicativo hello flui sobre TCP. Nesses casos, o ICMP fornece tooTCP de resultados em comparação comparados menos precisa.

##### <a name="firewall-configuration"></a>Configuração do firewall
Protocolo TCP requer que os pacotes TCP são enviados tooa porta de destino. porta padrão de saudação usada pelos agentes NPM é 8084, no entanto, você pode alterar isso quando você configurar agentes. Portanto, você precisa tooensure que seus firewalls de rede ou as regras NSG (no Azure) permitindo o tráfego na porta hello. Você também precisa toomake se o firewall Olá local nos computadores de saudação onde os agentes são instalados é configurado tooallow tráfego nessa porta.

Você pode usar regras de firewall de tooconfigure de scripts do PowerShell nos computadores que executam o Windows, no entanto, você precisa tooconfigure firewall da sua rede manualmente.

Por outro lado, o ICMP não funciona usando a porta. Na maioria dos cenários de empresa, o tráfego ICMP é permitido por meio de saudação firewalls tooallow toouse ferramentas de diagnóstico de rede, como Olá utilitário Ping. Portanto, se você puder executar Ping em um computador de outro, você pode usar protocolo ICMP de saudação sem a necessidade de firewalls tooconfigure manualmente.

> [!NOTE]
> Caso você não tiver certeza de qual protocolo toouse, escolha toostart ICMP com. Se você não estiver satisfeito com os resultados de saudação, você pode alternar sempre tooTCP mais tarde.


#### <a name="how-tooswitch-hello-protocol"></a>Como tooswitch Olá protocolo

Se você escolheu toouse ICMP durante a implantação, você pode alternar tooTCP a qualquer momento, editando padrão Olá regra de monitoramento.

##### <a name="tooedit-hello-default-monitoring-rule"></a>regra de monitoramento tooedit saudação padrão
1.  Navegue muito**o desempenho da rede** > **Monitor** > **configurar** > **Monitor** e, em seguida, clique em **regra padrão**.
2.  Role toohello **protocolo** seção e selecione o protocolo de saudação que você deseja toouse.
3.  Clique em **salvar** tooapply configuração de saudação.

Mesmo se a regra padrão de saudação está usando um protocolo específico, você pode criar novas regras com um protocolo diferente. Você pode criar uma mistura de regras onde algumas regras de saudação usam o ICMP e outro usa o TCP.




## <a name="data-collection-details"></a>Detalhes da coleta de dados
Monitor de desempenho de rede usa pacotes de handshake TCP SYN-SYNACK-ACK ao TCP é escolhido e resposta de eco de ICMP de eco ICMP quando ICMP é escolhido como Olá toocollect perda e latência de informações do protocolo. Rastreamento de rotas é também usado tooget informações de topologia.

Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para o Monitor de desempenho de rede.

| plataforma | Agente direto | Agente SCOM | Armazenamento do Azure | SCOM necessário? | Os dados do agente SCOM enviados por meio do grupo de gerenciamento | frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  |  |Mensagens de handshakes TCP/ECO ICMP a cada 5 segundos, dados enviados a cada 3 minutos |

solução de saudação usa integridade de saudação tooassess transações sintéticas de rede hello. Agentes do OMS instalados em vários ponto em pacotes TCP Olá rede exchange ou de eco ICMP (dependendo do protocolo de saudação selecionado para monitoramento) entre si. No processo de saudação agentes Saiba Olá ida e volta tempo e perda de pacotes, se houver. Periodicamente, cada agente também executa um rastreamento rota tooother agentes toofind, que todos os Olá várias rotas de rede Olá que deve ser testado. Usando esses dados, os agentes de saudação podem deduzir latência de rede hello e valores de perdas de pacote. Olá testes são repetidos cada cinco segundos e os dados são agregados por um período de três minutos por agentes de saudação antes de carregá-lo toohello serviço de análise de Log.

> [!NOTE]
> Embora os agentes se comunicam uns com os outros frequentemente, elas não geram um muito tráfego de rede ao realizar testes de saudação. Agentes confiam apenas em perda de saudação do TCP SYN-SYNACK-ACK handshake pacotes toodetermine e latência – nenhum dado que os pacotes são trocados. Durante esse processo, os agentes se comunicam entre si somente quando necessário e otimização de topologia de comunicação do agente Olá tooreduce o tráfego de rede.
>
>

## <a name="using-hello-solution"></a>Usando a solução de saudação
Esta seção explica todas as funções de painel hello e como toouse-los.

### <a name="solution-overview-tile"></a>Bloco de Visão Geral da Solução
Depois de habilitar a solução de Monitor de desempenho de rede hello, Olá solução lado a lado na página de visão geral do OMS Olá fornece uma visão geral da integridade da rede hello. Ele exibe um gráfico de rosca, mostrando o número de saudação de links de sub-rede com e sem integridade. Quando você clica em bloco hello, ele abre o painel de solução de saudação.

![Bloco do Monitor de Desempenho de Rede](./media/log-analytics-network-performance-monitor/npm-tile.png)

### <a name="network-performance-monitor-solution-dashboard"></a>Painel de solução do Monitor de Desempenho de Rede
Olá **rede resumo** folha mostra um resumo das redes Olá junto com seu tamanho. Isso é seguido por blocos mostrando o número total de conexões de rede, links de sub-rede e caminhos no sistema de saudação (um caminho consiste em endereços IP hello dois hosts com agentes e todos os saltos de saudação entre eles).

Olá **primeiros eventos de integridade de rede** folha fornece uma lista de alertas e eventos de integridade mais recentes no sistema hello e tempo de saudação desde que o evento Olá esteve ativo. Um alerta ou evento de integridade é gerada sempre que a perda de pacotes de saudação ou latência de um link de rede ou sub-rede excede um limite.

Olá **Links de rede não íntegro superior** folha mostra uma lista de links de rede não íntegro. Estes são links de rede de saudação que têm um ou mais eventos de integridade adversas para eles no momento da saudação.

Olá **superior sub-rede Links com mais perda** e **Links de sub-rede com latência mais** folhas Mostrar links de sub-rede superior Olá por perda de pacotes e principais links de sub-rede por latência, respectivamente. Alta latência ou alguma perda de pacotes podem ser esperadas em determinados links de rede. Esses links aparecem na lista de dez principais hello, mas não são marcados como não íntegro.

Olá **consultas comuns** folha contém um conjunto de consultas de pesquisa que buscar diretamente os dados de monitoramento de rede bruta. Você pode usar essas consultas como um ponto de partida para criar suas próprias consultas para relatórios personalizados.

![Painel do Monitor de Desempenho de Rede](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="drill-down-for-depth"></a>Busca detalhada para profundidade
Você pode clicar em vários links Olá solução painel toodrill suspensa mais profundo em qualquer área de interesse. Por exemplo, quando você vir um link de rede não íntegro aparecem no painel de saudação ou de um alerta, você pode clicar em ele tooinvestigate ainda mais. Você será levado tooa página que lista todos os links de sub-rede Olá para o link de rede específico hello. Você será o status de integridade, latência e perda de Olá de toosee capaz de cada link de sub-rede e rapidamente descobrir quais links de sub-rede estão causando o problema de saudação. Você pode clicar em **exibir vínculos de nós** toosee todos os links de nó Olá para a sub-rede não íntegros Olá link. Em seguida, você pode Consulte links de nó para nó individual e encontrar links de nó não íntegros hello.

Você pode clicar em **topologia exibição** tooview topologia de salto por salto Olá de rotas de saudação entre os nós de origem e destino hello. Olá rotas Íntegro ou saltos são mostrados em vermelho para que você possa identificar rapidamente parte específica do hello problema tooa da rede hello.

![dados de busca detalhada](./media/log-analytics-network-performance-monitor/npm-drill.png)

### <a name="network-state-recorder"></a>Gravador de Estado da Rede

Cada modo de exibição exibe um instantâneo da integridade da rede em um ponto específico no tempo. Por padrão, o estado mais recente Olá é mostrado. barra de saudação na parte superior de saudação da página Olá mostra Olá ponto no tempo para o qual o estado de hello está sendo exibido. Você pode escolher toogo Voltar no tempo e exibir instantâneo de Olá de sua integridade da rede clicando na barra de saudação em **ações**. Você também pode escolher tooenable ou desabilitar a atualização automática para qualquer página enquanto você exibe o estado mais recente hello.

![estado da rede](./media/log-analytics-network-performance-monitor/network-state.png)

#### <a name="trend-charts"></a>Gráficos de tendência
Em cada nível que você fazer drill-down, você pode ver a tendência de saudação da perda e latência de um link de rede. Gráficos de tendência também estão disponíveis para links de sub-rede e nó. Você pode alterar o intervalo de tempo de saudação para Olá gráfico tooplot usando o controle de tempo de saudação na parte superior de saudação do gráfico de saudação.

Gráficos de tendência mostram uma perspectiva de histórica do desempenho de saudação de um link de rede. Alguns problemas de rede são transitórios na natureza e seriam difícil toocatch apenas observando estado atual de saudação da rede de saudação. Isso ocorre porque problemas podem rapidamente de superfície e desaparecer antes que alguém perceba, apenas tooreappear em um momento posterior. Esses problemas transitórios também podem ser difícil para os administradores de aplicativos, porque os problemas geralmente superfície como inexplicáveis aumento no tempo de resposta, mesmo quando todos os componentes do aplicativo aparecem toorun sem problemas.

Você pode facilmente detectar esses tipos de problemas, observando um gráfico de tendência onde o problema de saudação aparecerá como um aumento repentino na perda de pacote ou latência de rede.

![gráfico de tendência](./media/log-analytics-network-performance-monitor/npm-trend.png)

#### <a name="hop-by-hop-topology-map"></a>Mapa de topologia de salto a salto
Mostra o Monitor de desempenho Olá topologia de nó por nó de rotas entre dois nós em um mapa de topologia interativa da rede. Você pode exibir o mapa de topologia Olá selecionando um link de nó e, em seguida, clicando em **topologia exibição**. Além disso, você pode exibir o mapa de topologia Olá clicando **caminhos** bloco no painel de saudação. Quando você clica em **caminhos** no painel de saudação, você terá tooselect Olá nós de origem e destino, no painel à esquerda de saudação do e, em seguida, clique em **plotar** tooplot rotas de saudação entre nós Olá dois.

mapa de topologia Olá exibe a quantidade de rotas entre Olá dois nós e quais caminhos Olá levar de pacotes de dados. Afunilamentos de desempenho de rede são marcados em vermelho no mapa de topologia de saudação. Você pode localizar uma conexão de rede com defeito ou um dispositivo de rede com defeito examinando elementos coloridos de vermelhos no mapa de topologia de saudação.

Quando você clica em um nó ou passe o mouse sobre ele no mapa de topologia hello, você verá as propriedades de saudação do nó de hello como o FQDN e o endereço IP. Clique em um toosee de salto é o endereço IP. Você pode escolher toofilter rotas específicas por meio de filtros de saudação no painel de ação recolhível hello. E, também é possível simplificar as topologias de rede Olá ocultando nós intermediários hello, usando o controle deslizante de saudação no painel de ações de saudação. Você pode ampliar ou estão fora do mapa de topologia hello usando a roda do mouse.

Observe que topologia Olá mostrada no mapa de saudação topologia de camada 3 e não contém conexões e dispositivos da camada 2.

![mapa de topologia de salto a salto](./media/log-analytics-network-performance-monitor/npm-topology.png)

#### <a name="fault-localization"></a>Localização de falhas
Monitor de desempenho de rede é capaz de toofind gargalos de rede Olá sem se conectar a dispositivos de rede toohello. Monitor de desempenho de rede com base nos dados de saudação que ele coleta da rede hello e aplicando os algoritmos avançados no gráfico de rede hello, faz uma estimativa probabilística do hello partes da rede que são provavelmente origem Olá Olá problema.

Essa abordagem é útil toodetermine gargalos de rede de saudação quando toohops de acesso não está disponível porque ele não requer qualquer toobe dados coletado Olá dispositivos de rede como roteadores ou comutadores. Isso também é útil quando saltos Olá entre dois nós não estão no seu controle administrativo. Por exemplo, saltos Olá podem ser roteadores do ISP.

### <a name="log-analytics-search"></a>Pesquisa de Análise de Log
Todos os dados graficamente expostos por meio do painel de Monitor de desempenho de rede hello e páginas de detalhamento também está disponível nativamente na pesquisa de análise de Log. Você pode consultar dados hello usando linguagem de consulta de pesquisa hello e criar relatórios personalizados por meio da exportação Olá dados tooExcel ou Power BI. Olá **consultas comuns** folha no painel de saudação tem algumas consultas úteis que você pode usar como ponto de partida para criar seus próprios relatórios e consultas de saudação.

![consultas de pesquisa](./media/log-analytics-network-performance-monitor/npm-queries.png)

## <a name="investigate-hello-root-cause-of-a-health-alert"></a>Investigue a causa raiz de saudação de um alerta de integridade
Agora que você leu sobre o Monitor de desempenho de rede, vamos examinar uma investigação simple causa raiz Olá para um evento de integridade.

1. Na página de visão geral do hello, você obterá um instantâneo rápido da integridade de saudação de sua rede observando Olá **Monitor de desempenho de rede** lado a lado. Observe que, sem sub-redes Olá 6, links que estão sendo monitorados, 2 estão íntegras. Isso requer investigação. Clique em Painel de controle do hello bloco tooview Olá solução.  
   ![Bloco do Monitor de Desempenho de Rede](./media/log-analytics-network-performance-monitor/npm-investigation01.png)
2. Imagem de exemplo hello abaixo, você observará que há um evento de integridade de um link de rede que não está íntegro. Você decidir problema de saudação tooinvestigate e clique em Olá **DMZ2 DMZ1** toofind de link de rede fora da raiz de saudação do problema de saudação.  
   ![exemplo de link de rede não íntegro](./media/log-analytics-network-performance-monitor/npm-investigation02.png)
3. página de drill-down Olá mostra todos os links de sub-rede Olá no **DMZ2 DMZ1** link de rede. Observe que para os dois links de sub-rede hello, latência de saudação ultrapassou o limite de saudação fazer o link de rede de saudação não íntegro. Você também pode ver as tendências de latência de saudação de ambos os links de sub-rede Olá. Você pode usar o tempo de saudação controle de seleção em Olá gráfico toofocus na Olá necessário intervalo de tempo. Você pode ver o tempo de saudação do dia hello quando a latência atingiu seu horário de pico. Posteriormente, você pode pesquisar logs de saudação para esse problema de saudação de tooinvestigate período de tempo. Clique em **exibir vínculos de nós** toodrill suspensa adicional.  
   ![exemplo de links de sub-rede não íntegros](./media/log-analytics-network-performance-monitor/npm-investigation03.png)
4. Página anterior toohello semelhante, página de drill-down Olá de link de determinada sub-rede Olá lista seus links de nó constituintes. Você pode executar ações semelhantes aqui como você fez na etapa anterior hello. Clique em **topologia exibição** tooview topologia de saudação entre nós Olá 2.  
   ![exemplo de links de nó não íntegro](./media/log-analytics-network-performance-monitor/npm-investigation04.png)
5. Todos os caminhos de saudação entre nós Olá 2 selecionado são plotados no mapa de topologia de saudação. Você pode visualizar a topologia de salto por salto Olá de rotas entre dois nós no mapa de topologia de saudação. Isso lhe dá uma visão clara de rotas quantos existem entre dois nós de saudação e quais caminhos Olá pacotes de dados estão demorando. Os afunilamentos de desempenho de rede são marcados em vermelho. Você pode localizar uma conexão de rede com defeito ou um dispositivo de rede com defeito examinando elementos coloridos de vermelhos no mapa de topologia de saudação.  
   ![exemplo de modo de exibição de topologia não íntegra](./media/log-analytics-network-performance-monitor/npm-investigation05.png)
6. perda de Hello, latência e número de saudação de saltos em cada caminho podem ser analisadas Olá **ação** painel. Use Olá scrollbar tooview Olá detalhes dos caminhos não íntegro.  Use Olá filtros tooselect Olá caminhos com nó Íntegro Olá para que topologia Olá para apenas Olá selecionado caminhos são plotados. Você pode usar o toozoom de roda de mouse ou não o mapa de topologia de saudação.

   Em Olá abaixo de imagem podem ver claramente Olá causa raiz de saudação problema áreas toohello seção específica de rede de saudação examinando caminhos hello e saltos na cor vermelha. Clicar em um nó no mapa de topologia de saudação revela propriedades Olá Olá do nó de, incluindo Olá FQDN e o endereço IP. Clicar em um nó mostra o endereço IP de saudação do salto hello.  
   ![topologia não íntegra - exemplo de detalhes do caminho](./media/log-analytics-network-performance-monitor/npm-investigation06.png)

## <a name="provide-feedback"></a>Fornecer comentários

- **UserVoice** -é possível postar suas ideias para os recursos do Monitor de desempenho de rede que você deseja nos toowork em de. Visite nossa [página UserVoice](https://feedback.azure.com/forums/267889-log-analytics/category/188146-network-monitoring).
- **Junte-se ao nosso coorte** - Estamos sempre interessados em novos clientes para o nosso coorte. Como parte do mesmo, você obtenha acesso antecipado toonew recursos e ajude-na melhorar o desempenho de rede. Se estiver interessado em participar, preencha essa [pesquisa rápida](https://aka.ms/npmcohort).

## <a name="next-steps"></a>Próximas etapas
* [Pesquisar logs](log-analytics-log-searches.md) tooview detalhadas registros de dados de desempenho de rede.
