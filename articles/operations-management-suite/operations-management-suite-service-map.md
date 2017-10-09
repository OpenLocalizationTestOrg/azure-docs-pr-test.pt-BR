---
title: "Olá aaaUse solução de mapa de serviço no Operations Management Suite | Microsoft Docs"
description: "Mapa de serviço é uma solução Operations Management Suite que detecta automaticamente os componentes do aplicativo no Windows e mapas e sistemas Linux Olá comunicação entre serviços. Este artigo fornece detalhes sobre a implantação do Mapa do Serviço em seu ambiente e sobre como usá-lo em diversos cenários."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a>Usar solução de mapa de serviço de saudação do Operations Management Suite
Mapa de serviço detecta automaticamente os componentes do aplicativo em sistemas Windows e Linux e mapas Olá comunicação entre serviços. Com mapa de serviço, você pode exibir os servidores de forma Olá que você imagina: como sistemas interconectados que fornecem serviços essenciais. Mapa de serviço mostra conexões entre servidores, processos e portas em qualquer arquitetura conectado por TCP, sem nenhuma configuração necessária que Olá instalação de um agente.

Este artigo descreve os detalhes de saudação do uso de mapa de serviço. Para obter mais informações sobre como configurar o Mapa do Serviço e os agentes de integração, consulte [Configurar a solução Mapa do Serviço no Operations Management Suite](operations-management-suite-service-map-configure.md).


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>Casos de uso: Fazer com que seus processos de TI reconheçam a dependência

### <a name="discovery"></a>Descoberta
O Mapa do Serviço compila automaticamente um mapa de referência comum de dependências em seus servidores, processos e serviços de terceiros. Ele descobre e mapeia todas as dependências TCP, identificando surpresa conexões, sistemas remotos de terceiros que depende de você e dependências tootraditional as áreas escuras da sua rede, como o Active Directory. Mapa de serviço descobre as conexões de rede com falha que seus sistemas gerenciados estão tentando toomake, ajudando você a identificar possíveis erros de configuração do servidor, a interrupção do serviço e problemas de rede.

### <a name="incident-management"></a>Gerenciamento de incidentes
Mapa de serviço ajuda a eliminar as suposições de saudação do isolamento do problema, mostrando como os sistemas estão conectados e que afetam uns aos outros. Além disso, tooidentifying falha conexões, ajuda a identificar os balanceadores de carga configurado incorretamente, surpreendente ou excessiva de carga em serviços essenciais e autorizados clientes, como computadores de desenvolvedor falando tooproduction sistemas. Usando fluxos de trabalho integrados com o Operations Management Suite Change Tracking, você também pode ver se um evento de alteração em um computador de back-end ou serviço explica a causa raiz de saudação de um incidente.

### <a name="migration-assurance"></a>Garantia de migração
Ao utilizar o Mapa do Serviço você pode, efetivamente, planejar, acelerar e validar as migrações do Azure, permitindo assegurar que nada seja deixado para trás e que interrupções inesperadas não ocorram. Você pode descobrir interdependentes todos os sistemas que toomigrate necessidade juntos, avaliar a capacidade e a configuração do sistema e identificar se um sistema em execução ainda está atendendo usuários ou é um candidato para encerramento em vez de migração. Após a conclusão da movimentação hello, você pode verificar tooverify de carga e a identidade do cliente que sistemas de teste e os clientes que estão se conectando. Se suas definições de planejamento e de firewall de sub-rede tiverem problemas, as conexões com falha no mapa de serviço mapas ponto toohello sistemas que precisam de conectividade.

### <a name="business-continuity"></a>Continuidade dos negócios
Se você estiver usando o Azure Site Recovery e precisa de ajuda para definir a sequência de recuperação Olá para o seu ambiente de aplicativo, o mapa de serviço podem automaticamente mostram como sistemas dependem uns aos outros tooensure que seu plano de recuperação é confiável. Escolhendo um servidor crítico ou grupo e exibir seus clientes, você pode identificar quais sistemas de front-end toorecover depois que o servidor de saudação foi restaurado e está disponível. Por outro lado, observando as dependências de back-end de servidores críticos, você pode identificar quais sistemas toorecover antes de seus sistemas de foco são restaurados.

### <a name="patch-management"></a>Gerenciamento de patch
Mapa de serviço melhora a utilização do hello avaliação de atualização de sistema do Operations Management Suite mostrando quais outras equipes e servidores dependem de seu serviço, portanto você pode notificá-lo com antecedência antes de você colocar os sistemas para aplicação de patch. O Mapa do Serviço também aprimora o gerenciamento de patch no Operations Management Suite, mostrando se seus serviços estão disponíveis e conectados corretamente após terem sido corrigidos e reiniciados.


## <a name="mapping-overview"></a>Visão geral do mapeamento
Agentes de mapa de serviço coletam informações sobre todos os processos de conexão TCP Olá servidor em que são instalados e detalhes sobre Olá conexões de entrada e saída de cada processo. Na lista de saudação no painel esquerdo do hello, você pode selecionar computadores ou grupos que têm toovisualize de agentes do mapa de serviço suas dependências em um intervalo de tempo especificado. Dependência de máquina mapeia o foco em um computador específico e eles mostram todas as máquinas de saudação que são clientes TCP diretos ou servidores da máquina.  Os mapas do Grupo de Computadores mostram os conjuntos de servidores e suas dependências.

![Visão geral do Mapa do Serviço](media/oms-service-map/service-map-overview.png)

Máquinas podem ser expandidas em Olá Olá de tooshow mapa executando processos com conexões de rede durante o intervalo de tempo de saudação selecionado. Quando um computador remoto com um agente de mapa de serviço é expandido tooshow detalhes do processo, são mostrados apenas os processos que se comunicam com a máquina de foco hello. Contagem de saudação de máquinas de front-end sem agente que se conectam à máquina de foco de saudação é indicada no lado esquerdo de saudação de processos de saudação que se conectam ao. Se a máquina de foco Olá faz uma máquina de back-end de tooa de conexão que não tiver um agente, servidor de back-end de saudação é incluído em um grupo de porta do servidor, junto com outra conexões toohello mesmo número da porta.

Por padrão, o mapa de serviço mapeia Mostrar Olá últimos 30 minutos de informações de dependência. Usando controles de tempo de saudação à esquerda superior hello, você pode consultar mapas para intervalos de tempo de histórico de backup tooone hora tooshow como dependências pesquisadas no hello passado (por exemplo, durante um incidente ou antes de uma alteração ocorreu). Os dados do Mapa do Serviço são armazenados por 30 dias em espaços de trabalho pagos, e por sete dias em espaços de trabalho gratuitos.

## <a name="status-badges-and-border-coloring"></a>Notificações de status e a cor de borda
Olá inferior de cada servidor no mapa de saudação é uma lista de notificações de status transmitir informações de status sobre o servidor de saudação. notificações de saudação indicam que há algumas informações relevantes para o servidor de saudação de uma das integrações de solução do hello Operations Management Suite. Clicar em uma notificação leva você diretamente toohello detalhes do status de saudação no painel direito da saudação. Olá atualmente selos de status disponíveis incluem alertas, Central de serviços, as alterações, segurança e atualizações.

Dependendo da severidade Olá de notificações de status de hello, bordas de nó da máquina podem ser colorido vermelho (crítico), amarelo (aviso) ou azul (informativas). cor de saudação representa status mais graves de saudação de qualquer uma das notificações de status de saudação. Uma borda cinza indica um nó que não possui indicadores de status.

![Notificações de status](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>Grupos de Computadores
Grupos de computadores permitem que você toosee mapas gira em torno de um conjunto de servidores, não apenas um para ver todos os membros de saudação de um cluster de várias camado de aplicativo ou servidor em um mapa.

Os usuários selecionar quais servidores pertencem juntos em um grupo e escolha um nome para o grupo de saudação.  Você pode escolher tooview Olá grupo com todos os seus processos e conexões, ou exibi-lo com apenas processos hello e conexões que estão diretamente relacionam toohello outros membros do grupo de saudação.

![Grupo de Computadores](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>Criar um Grupo de Computadores
toocreate um grupo, selecione hello ou mais máquinas desejado em máquinas de saudação lista e clique em **adicionar toogroup**.

![Criar Grupo](media/oms-service-map/machine-groups-create.png)

Lá, você pode escolher **criar novo** e dê um nome de grupo de saudação.

![Nome do Grupo](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>Grupos de computadores são servidores too10 atualmente limitado, mas estamos planejando tooincrease esse limite em breve.

### <a name="viewing-a-group"></a>Exibir um Grupo
Depois de criar alguns grupos, você pode exibi-los, escolhendo a guia de grupos de saudação.

![Guia Grupos](media/oms-service-map/machine-groups-tab.png)

Selecione o mapa de saudação do hello grupo nome tooview para esse grupo de computadores.
![Grupo de computadores](media/oms-service-map/machine-group.png) máquinas Olá que pertencem a toohello grupo são descritas em branco no mapa de saudação.

Olá expansão grupo listará máquinas Olá que compõem a saudação grupo de computadores.

![Computadores do Grupo de Computadores](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>Filtrar por processos
Você pode alternar exibição de mapa de saudação entre mostrando todas as conexões e processos no grupo de saudação e Olá apenas aqueles que estão diretamente relacionados toohello grupo de computadores.  Olá exibição padrão é tooshow todos os processos.  Você pode alterar a exibição de Olá Olá ícone de filtro acima mapa hello.

![Grupo do Filtro](media/oms-service-map/machine-groups-filter.png)

Quando **todos os processos** é selecionada, mapa Olá incluirá todas as conexões em cada uma das máquinas hello e processos em Olá grupo.

![Todos os processos do Grupo de Computadores](media/oms-service-map/machine-groups-all.png)

Se você alterar Olá tooshow de exibição somente **grupo conectado processos**, mapa hello serão restritas para baixo tooonly esses processos e as conexões que estão diretamente conectados tooother máquinas no grupo hello, criando uma exibição simplificada.

![Processos filtrados do Grupo de Computadores](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a>Adicionar grupo de tooa de máquinas
tooadd máquinas grupo existente tooan, verifique a saudação caixas próximas máquinas toohello desejado e, em seguida, clique em **adicionar toogroup**.  Em seguida, escolha o grupo de saudação para que deseja tooadd Olá máquinas.
 
### <a name="removing-machines-from-a-group"></a>Remover computadores de um grupo
Na lista de grupos de Olá, expanda Olá grupo nome toolist Olá máquinas Olá grupo de computadores.  Em seguida, clique em Olá reticências menu próximo toohello computador você deseja tooremove e escolha **remover**.

![Remova o computador do grupo](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>Remover ou renomear um grupo
Clique em Olá reticências menu próxima toohello grupo nome no hello lista de grupos.

![Menu do Grupo de Computadores](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>Ícones de função
Alguns processos possuem funções específicas em computadores: servidores Web, servidores de aplicativos, banco de dados, etc. Mapa de serviço anota processo e identificam caixas de máquina com toohelp de ícones de função em um servidor ou função de saudação rapidamente um processo desempenha.

| Ícone de função | Descrição |
|:--|:--|
| ![Servidor Web](media/oms-service-map/role-web-server.png) | Servidor Web |
| ![Servidor de aplicativos](media/oms-service-map/role-application-server.png) | Servidor de aplicativos |
| ![Servidor de banco de dados](media/oms-service-map/role-database.png) | Servidor de banco de dados |
| ![Servidor LDAP](media/oms-service-map/role-ldap.png) | Servidor LDAP |
| ![Servidor SMB](media/oms-service-map/role-smb.png) | Servidor SMB |

![Ícones de função](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>Conexões com falha
Conexões com falha são mostrados no mapa de serviço é mapeado para processos e computadores, com uma linha vermelha tracejada que indica que um sistema cliente está falhando tooreach um processo ou uma porta. Conexões com falha são relatados de qualquer sistema com um agente de mapa de serviço implantado, se o sistema é uma tentativa de conexão de saudação falhada Olá. Mapa de serviço mede esse processo observando soquetes TCP que não tooestablish uma conexão. Essa falha pode resultar de um firewall, uma configuração incorreta no hello cliente ou servidor, ou um serviço remoto não está disponível.

![Conexões com falha](media/oms-service-map/failed-connections.png)

Entender as conexões com falha pode ajudar com a solução de problemas, validação da migração, análise de segurança e noções básicas sobre arquitetura em geral. Conexões com falha, às vezes, serão inofensivos, mas eles geralmente apontem diretamente tooa problema, como um ambiente de failover de repente se torne inacessível, ou de duas camadas de aplicativo que está sendo tootalk não é possível após a migração de nuvem.

## <a name="client-groups"></a>Grupos de Clientes
Grupos de cliente são caixas no mapa de saudação que representam computadores cliente que não têm agentes de dependência. Um único grupo de cliente representa clientes Olá para um processo individual ou uma máquina.

![Grupos de Clientes](media/oms-service-map/client-groups.png)

endereços IP de saudação de toosee dos servidores de saudação em um grupo de cliente, o grupo Olá select. conteúdo de saudação do grupo Olá listados Olá **propriedades do grupo de cliente** painel.

![Propriedades do Grupo de Clientes](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>Grupos de Portas do Servidor
Os Grupos de Portas do Servidor são caixas que representam portas de servidor em servidores que não possuem Agentes de Dependência. caixa de Olá contém a porta do servidor de saudação e uma contagem do número de saudação de servidores com a porta de toothat de conexões. Expanda as conexões e servidores individuais do Olá Olá caixa toosee. Se houver apenas um servidor na caixa hello, Olá nome ou endereço IP é listado.

![Grupos de Portas do Servidor](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>Menu de contexto
Clicando em reticências hello (...) na parte superior de saudação à direita de qualquer servidor exibe o menu de contexto de saudação para esse servidor.

![Conexões com falha](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>Carregar mapa do servidor
Clicando em **carregar o mapa de servidor** leva você tooa novo mapa com servidor de saudação selecionado como a nova máquina de foco hello.

### <a name="show-self-links"></a>Mostrar self-links
Clicando em **Self-Links Mostrar** redesenha Olá server nó, incluindo quaisquer links automáticos, que são conexões TCP que começam e terminam com processos no servidor de saudação. Se links automáticos são mostrados, Olá alterações de comando de menu muito**Self-Links ocultar**, de modo que você pode desativá-los.

## <a name="computer-summary"></a>Resumo do computador
Olá **Resumo da máquina** painel inclui uma visão geral do sistema operacional do servidor, as contagens de dependência e dados de outras soluções do Operations Management Suite. Esses dados incluem métricas de desempenho, tíquetes de central serviços, controle de alterações, segurança e atualizações.

![Painel Resumo do Computador](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>Propriedades do computador e do processo
Quando você navega em um mapa de mapa de serviço, você pode selecionar máquinas e processos toogain um contexto adicional sobre suas propriedades. Máquinas fornecem informações sobre DNS nome, IPv4 endereços, CPU e memória, capacidade, tipo VM, sistema operacional e versão, reinicialize última hora e IDs de saudação de seus agentes do Operations Management Suite e mapa de serviço.

![Painel Propriedades do Computador](media/oms-service-map/machine-properties.png)

É possível coletar detalhes do processo dos metadados do sistema operacional sobre processos em execução, incluindo o nome do processo, a descrição do processo, nome de usuário e domínio (no Windows), nome da empresa, nome do produto, a versão do produto, o diretório de trabalho, a linha de comando e a hora de início do processo.

![Painel Propriedades do Processo](media/oms-service-map/process-properties.png)

Olá **resumo do processo** painel fornece informações adicionais sobre a conectividade do processo hello, incluindo suas portas associadas, conexões de entrada e saída e conexões com falha.

![Painel Resumo do Processo](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Integração de Alertas do Operations Management Suite
Mapa de serviço se integra ao Operations Management Suite alertas tooshow acionado alertas para servidor de saudação selecionado no intervalo de tempo de saudação selecionado. servidor de saudação exibe um ícone se há alertas atuais e hello **máquina alertas** painel lista os alertas de saudação.

![Painel Alertas do Computador](media/oms-service-map/machine-alerts.png)

alertas relevantes do tooenable mapa de serviço toodisplay, crie uma regra de alerta é acionado para um computador específico. alertas de toocreate adequada:
- Incluir uma cláusula toogroup por computador (por exemplo, **pelo intervalo de computador 1 minuto**).
- Escolha tooalert com base na medida de métrica.

![Configuração do alerta](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Integração de eventos de log do Operations Management Suite
Mapa de serviço se integra com tooshow de pesquisa de Log uma contagem de todos os eventos de log disponíveis para o servidor de saudação selecionado durante o intervalo de tempo de saudação selecionado. Você pode clicar qualquer linha na lista de saudação do evento contagens toojump tooLog pesquisa e ver os eventos de log individuais hello.

![Painel Eventos de Log do Computador](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Integração da Central de Serviços do Operations Management Suite
Integração com o mapa de serviço com hello conector de gerenciamento de serviço de TI é automática quando ambas as soluções são habilitadas e configuradas no seu espaço de trabalho do Operations Management Suite. integração de saudação no mapa de serviço denominada "Central de serviços". Para obter mais informações, consulte [Gerenciar itens de trabalho de ITSM de forma centralizada usando o Conector de Gerenciamento de Serviço de TI](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).

Olá **Central de serviços de máquina** painel lista todos os eventos de gerenciamento de serviços para o servidor de saudação selecionado no intervalo de tempo de saudação selecionado. servidor de saudação exibe um ícone se o item atual e painel de Central de serviços de máquina Olá listá-los.

![Painel Central de Serviços do Computador](media/oms-service-map/service-desk.png)

item de saudação tooopen em sua solução ITSM conectada, clique em **Item de trabalho do modo de exibição**.

tooview Olá detalhes do item de saudação na pesquisa de Log, clique em **Mostrar na pesquisa de Log**.


## <a name="operations-management-suite-change-tracking-integration"></a>Integração do Controle de Alterações do Operations Management Suite
A integração do Mapa do Serviço com o Controle de Alterações é automática quando ambas as soluções estão habilitadas e configuradas no espaço de trabalho do Operations Management Suite.

Olá **o controle de alterações da máquina** painel lista todas as alterações, com hello mais recente primeiro, junto com um toodrill link para baixo tooLog pesquisa para obter detalhes adicionais.

![Painel Controle de Alterações do Computador](media/oms-service-map/change-tracking.png)

Olá, imagem a seguir é uma exibição detalhada de um evento ConfigurationChange que você pode ver depois de selecionar **Mostrar na análise de Log**.

![Evento ConfigurationChange](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Integração de desempenho do Operations Management Suite
Olá **o desempenho da máquina** painel exibe as métricas de desempenho padrão do servidor de saudação selecionado. métricas de saudação incluem utilização de CPU, utilização de memória, bytes de rede enviados e recebidos e uma lista dos principais processos de saudação por bytes de rede enviados e recebidos. dados de desempenho da rede tooget hello, você também deve ter habilitado Olá solução 2.0 de dados de transmissão no Operations Management Suite.

![Painel Desempenho do Computador](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Integração de segurança do Operations Management Suite
A integração do Mapa do Serviço com a Segurança e Auditoria é automática quando ambas as soluções estão habilitadas e configuradas no espaço de trabalho do Operations Management Suite.

Olá **de segurança do computador** painel mostra dados de saudação solução Operations Management Suite segurança e auditoria para o servidor de saudação selecionado. Painel de saudação lista um resumo dos problemas de segurança pendentes para o servidor de saudação durante o intervalo de tempo de saudação selecionado. Clicar em qualquer um de saudação detalhada de problemas de segurança para baixo em uma pesquisa de Log para obter detalhes sobre eles.

![Painel Segurança do Computador](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Integração de Atualizações do Operations Management Suite
A integração do Mapa do Serviço com o Gerenciamento de Atualizações é automática quando ambas as soluções estão habilitadas e configuradas no espaço de trabalho do Operations Management Suite.

Olá **máquina atualizações** painel exibe dados de Olá solução de gerenciamento de atualizações do Operations Management Suite para servidor de saudação selecionado. Painel de saudação lista um resumo de todas as atualizações ausentes para o servidor de saudação durante o intervalo de tempo de saudação selecionado.

![Painel Controle de Alterações do Computador](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Registros do Log Analytics
Dados de inventário do processo e do computador do Mapa do Serviço estão disponíveis para [pesquisa](../log-analytics/log-analytics-log-searches.md) no Log Analytics. Você pode aplicar essa tooscenarios de dados que inclui o planejamento da migração, análise de capacidade de descoberta e solução de problemas de desempenho sob demanda.

Um registro é gerado por hora para cada computador exclusivo e o processo, além de toohello registros que são gerados quando um processo ou o computador for iniciado ou estiver onboard tooService do mapa. Esses registros têm propriedades de saudação no hello tabelas a seguir. campos de saudação e os valores em eventos de ServiceMapComputer_CL Olá mapeiam toofields de saudação recursos de máquina em Olá ServiceMap API do Azure Resource Manager. Hello campos e valores em eventos de ServiceMapProcess_CL Olá mapeiam campos toohello de saudação recurso processo Olá ServiceMap API do Azure Resource Manager. campo de ResourceName_s de saudação coincide com o campo de nome de saudação no recurso de Gerenciador de recursos correspondente hello. 

>[!NOTE]
>Como aumentarem os recursos de mapa de serviço, esses campos são toochange de assunto.

Há propriedades geradas internamente, você pode usar computadores e processos exclusivo tooidentify:

- Computador: Use ResourceId ou ResourceName_s toouniquely identificar um computador em um espaço de trabalho do Operations Management Suite.
- Processo: Use ResourceId toouniquely identificar um processo dentro de um espaço de trabalho do Operations Management Suite. ResourceName_s é exclusivo no contexto de saudação da máquina de saudação no qual Olá processo está sendo executado (MachineResourceName_s) 

Porque podem haver vários registros para um processo especificado e o computador em um intervalo de tempo especificado, as consultas podem retornar mais de um registro para Olá mesmo computador ou processo. tooinclude Olá somente o registro mais recente, adicione "| eliminação de duplicação ResourceId"toohello consulta.

### <a name="servicemapcomputercl-records"></a>Registros ServiceMapComputer_CL
Registros com um tipo de *ServiceMapComputer_CL* têm dados de inventário para servidores com agentes do Mapa do Serviço. Esses registros têm propriedades Olá em Olá a tabela a seguir:

| Propriedade | Descrição |
|:--|:--|
| Tipo | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Olá identificador exclusivo para uma máquina no espaço de trabalho de saudação |
| ResourceName_s | Olá identificador exclusivo para uma máquina no espaço de trabalho de saudação |
| ComputerName_s | computador Olá FQDN |
| Ipv4Addresses_s | Uma lista de endereços do IPv4 do servidor de saudação |
| Ipv6Addresses_s | Uma lista de endereços do IPv6 do servidor de saudação |
| DnsNames_s | Uma matriz de nomes DNS |
| OperatingSystemFamily_s | Windows ou Linux |
| OperatingSystemFullName_s | Olá nome completo do sistema operacional de saudação  |
| Bitness_s | número de bits de saudação da máquina de saudação (32 bits ou 64 bits)  |
| PhysicalMemory_d | memória física Olá em MB |
| Cpus_d | número de saudação de CPUs |
| CpuSpeed_d | Olá velocidade da CPU em MHz|
| VirtualizationState_s | *desconhecido*, *físico*, *virtual*, *hipervisor* |
| VirtualMachineType_s | *hyperv*, *vmware*, e assim por diante |
| VirtualMachineNativeMachineId_g | Olá ID da VM conforme atribuído pelo seu hipervisor |
| VirtualMachineName_s | nome de saudação do hello VM |
| BootTime_t | tempo de inicialização de saudação |



### <a name="servicemapprocesscl-type-records"></a>Registros do tipo ServiceMapProcess_CL Type
Registros com um tipo de *ServiceMapProcess_CL* têm dados de inventário para processos conectados com TCP em servidores com agentes do Mapa do Serviço. Esses registros têm propriedades Olá em Olá a tabela a seguir:

| Propriedade | Descrição |
|:--|:--|
| Tipo | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Olá identificador exclusivo de um processo no espaço de trabalho de saudação |
| ResourceName_s | Olá identificador exclusivo para um processo em máquina Olá no qual ele está em execução|
| MachineResourceName_s | nome do recurso de saudação da máquina Olá |
| ExecutableName_s | nome de saudação do executável do processo Olá |
| StartTime_t | hora de início de pool de processo Olá |
| FirstPid_d | saudação PID primeiro no pool de processos de saudação |
| Description_s | Descrição do processo Olá |
| CompanyName_s | nome de saudação da empresa de saudação |
| InternalName_s | nome interno da saudação |
| ProductName_s | nome de saudação do produto de saudação |
| ProductVersion_s | versão do produto Olá |
| FileVersion_s | versão do arquivo Hello |
| CommandLine_s | linha de comando Olá |
| ExecutablePath _s | arquivo executável do Hello caminho toohello |
| WorkingDirectory_s | diretório de trabalho Olá |
| UserName | conta de saudação no qual Olá processo está em execução. |
| UserDomain | domínio Olá no qual Olá processo está em execução. |


## <a name="sample-log-searches"></a>Pesquisas de log de exemplo

### <a name="list-all-known-machines"></a>Lista todas as máquinas conhecidas
Type=ServiceMapComputer_CL | dedup ResourceId

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a>Capacidade de memória física de saudação da lista de todos os computadores gerenciados.
Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>Listar o nome, DNS, IP e sistema operacional do computador.
Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId

### <a name="find-all-processes-with-sql-in-hello-command-line"></a>Localiza todos os processos com "sql" na linha de comando Olá
Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>Localizar uma máquina (registro mais recente) por nome de recurso
Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>Localizar um computador (registro mais recente) pelo endereço IP
Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId

### <a name="list-all-known-processes-on-a-specified-machine"></a>Listar todos os processos conhecidos em um computador especificado
Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="list-all-computers-running-sql"></a>Listar todos os computadores que executam SQL
Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a>Listar todas as versões de produtos exclusivas de curl no meu datacenter
Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>Criar um grupo de computadores de todos os computadores executando CentOS
Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s


## <a name="rest-api"></a>API REST
Todos os dados de servidor, o processo e a dependência da saudação no mapa de serviço está disponível por meio de saudação [API REST do serviço mapa](https://docs.microsoft.com/rest/api/servicemap/).


## <a name="diagnostic-and-usage-data"></a>Dados de uso e de diagnóstico
A Microsoft coleta automaticamente dados de uso e desempenho por meio do hello serviço mapa de serviço. A Microsoft usa esse tooprovide de dados e melhorar a qualidade do hello, segurança e integridade de saudação serviço mapa de serviço. tooprovide recursos para solução de problemas precisos e eficientes, dados de saudação incluem informações sobre a configuração de saudação do seu software, como o sistema operacional e versão, endereço IP, nome DNS e o nome de estação de trabalho. A Microsoft não coleta nomes, endereços ou outras informações de contato.

Para obter mais informações sobre o uso e coleta de dados, consulte Olá [declaração de privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).


## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [pesquisas de log](../log-analytics/log-analytics-log-searches.md) nos dados de tooretrieve de análise de Log que são coletados pelo mapa de serviço.


## <a name="troubleshooting"></a>Solucionar problemas
Consulte Olá [Olá documento de mapa de serviço de configuração de solução de problemas](operations-management-suite-service-map-configure.md#troubleshooting).


## <a name="feedback"></a>Comentários
Você tem algum comentário sobre o Mapa de Serviço ou sobre esta documentação?  Visita nossa [página Voz do Usuário](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), onde você pode sugerir recursos ou votar em sugestões existentes.
