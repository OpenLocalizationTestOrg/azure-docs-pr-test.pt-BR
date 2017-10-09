---
title: "aaaAzure segurança operacional | Microsoft Docs"
description: "Saiba mais sobre o OMS (Microsoft Operations Management Suite), seus serviços e como ele funciona."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Segurança Operacional do Azure
## <a name="introduction"></a>Introdução

### <a name="overview"></a>Visão geral
Sabemos que a segurança é trabalho na nuvem hello e como é importante que você encontrar precisas e em tempo hábil de informações sobre a segurança do Azure. Um dos toouse de motivos melhor Azure Olá para seus aplicativos e serviços é tootake aproveitar a ampla variedade de saudação de ferramentas de segurança e recursos disponíveis. Essas ferramentas e recursos ajudam a tornar soluções seguras de possíveis toocreate na plataforma Azure segura de saudação. O Microsoft Azure deve fornecer confidencialidade, integridade e disponibilidade dos dados do cliente, ao mesmo tempo que também permite uma responsabilidade transparente.

clientes toohelp entendam melhor a matriz de saudação de controles de segurança implementado no Microsoft Azure de ambos os clientes de saudação e perspectivas operacionais da Microsoft, neste white paper, "Segurança operacionais do Azure", será gravado que fornece um obter uma visão completa de segurança operacional de saudação disponível com o Windows Azure.

### <a name="azure-platform"></a>Plataforma Azure
O Azure é uma plataforma de serviço de nuvem pública que dá suporte a uma ampla seleção de sistemas operacionais, linguagens de programação, estruturas, ferramentas, bancos de dados e dispositivos. Ele pode executar contêineres do Linux com a integração com o Docker, criar aplicativos com JavaScript, Python, .NET, PHP, Java e Node.js e criar back-ends para dispositivos iOS, Android e Windows. Serviço de nuvem do Azure suporta Olá tecnologias mesmo milhões de desenvolvedores e profissionais de TI já contam e confiam.

Quando você criar ou migra ativos de TI para, um provedor de serviços de nuvem pública que você depender de tooprotect de recursos da organização seus aplicativos e dados com controles de saudação e serviços Olá eles oferecem toomanage Olá segurança de seu baseado em nuvem ativos.

Infraestrutura do Azure foi projetada de saudação recurso tooapplications para hospedagem milhões de clientes simultaneamente, e fornece uma base confiável em que as empresas podem atender aos requisitos de segurança. Além disso, Azure fornece uma ampla gama de segurança configuráveis toocontrol de capacidade de opções e hello-los para que você possa personalizar requisitos exclusivos de segurança toomeet Olá das implantações de sua organização. Este documento ajudará você a entender como as funcionalidades de segurança do Azure podem ajudá-lo a atender a esses requisitos.

### <a name="abstract"></a>Resumo
Segurança operacional Azure refere-se a serviços toohello, controles e toousers de recursos disponíveis para proteger seus dados, aplicativos e outros recursos do Microsoft Azure. Segurança operacionais do Azure é construída em uma estrutura que incorpora conhecimento Olá obtido por meio de diversos recursos que são exclusivo tooMicrosoft, incluindo Olá Microsoft Security Development Lifecycle (SDL), Olá Microsoft Security Response Center programa e conhecimento profundo do cenário de ameaças de segurança cibernética hello.

Este white paper descreve tooAzure segurança operacional do abordagem da Microsoft dentro da plataforma de nuvem do Microsoft Azure hello e abrange os serviços a seguir:
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Observador de Rede do Azure](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft Operations Management Suite

Microsoft Operations Management Suite (OMS) é hello solução de gerenciamento de TI para a nuvem híbrida de saudação. Usada sozinha ou tooextend sua implantação do System Center existente, o OMS oferece Olá máxima flexibilidade e controle de gerenciamento baseado em nuvem de sua infraestrutura.

![Microsoft Operations Management Suite](./media/azure-operational-security/azure-operational-security-fig1.png)

Com o OMS, você pode gerenciar qualquer instância em qualquer nuvem, incluindo local, Azure, AWS, Windows Server, Linux, VMware e OpenStack, com um custo menor do que as soluções dos concorrentes. Projetado para nuvem Olá, mundo, o OMS oferece um novo toomanaging de abordagem sua empresa que é hello mais rápida e mais econômica maneira toomeet novos negócios desafios e acomodar novas cargas de trabalho, aplicativos e ambientes de nuvem.

### <a name="oms-services"></a>Serviços do OMS

funcionalidade de núcleo de saudação do OMS é fornecida por um conjunto de serviços que são executados no Azure. Cada serviço fornece uma função de gerenciamento específico, e você pode combinar os cenários de gerenciamento diferente de tooachieve de serviços.

| O Barramento de  | serviço|
| :------------- | :-------------|
| Log Analytics | Monitorar e analisar a disponibilidade de saudação e o desempenho de recursos diferentes, incluindo físicos e máquinas virtuais. |
|Automação | Automatizar processos manuais e impor configurações de máquinas físicas e virtuais. |
| Backup | Fazer backup e restaurar dados críticos. |
| Site Recovery | Fornecer alta disponibilidade para aplicativos críticos. |

### <a name="log-analytics"></a>Log Analytics

O [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) fornece serviços de monitoramento para o OMS coletando dados de recursos gerenciados em um repositório central. Esses dados podem incluir eventos, dados de desempenho ou dados personalizados fornecidos por meio da API de saudação. Depois de coletados, dados saudação estão disponíveis para alertas, análise e exportação.


Esse método permite que você tooconsolidate dados de várias fontes, para que você pode combinar dados de seus serviços do Azure com seus ambientes locais. Ele também separa coleção Olá dos dados Olá pela ação de saudação executada com os dados para que todas as ações disponíveis tooall tipos de dados.


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

saudação de serviço de análise de Log gerencia seus dados baseados em nuvem com segurança usando Olá métodos a seguir:
-   segregação de dados
-   retenção de dados
-   segurança física
-   gerenciamento de incidentes
-   conformidade
-   certificações de padrões de segurança

### <a name="azure-backup"></a>Serviço de Backup do Azure

[O Backup do Azure](http://azure.microsoft.com/documentation/services/backup) fornece dados de backup e restauração dos serviços e faz parte do pacote OMS Olá de produtos e serviços.
Ele protege seus dados de aplicativos e os retém por vários anos, sem nenhum investimento de capital e custos operacionais mínimos. Ele pode fazer backup de dados de servidores físicos e virtuais do Windows além tooapplication cargas de trabalho como o SQL Server e SharePoint. Ele também pode ser usado por [System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate protegido tooAzure de dados para armazenamento de longo prazo e redundância.


Os dados protegidos no Backup do Azure são armazenados em um cofre de backup localizado em uma região geográfica específica. Olá dados são replicados dentro Olá mesma região e, dependendo do tipo de saudação do cofre, também pode ser o região tooanother replicados para garantir a resiliência adicional.

### <a name="management-solutions"></a>Soluções de gerenciamento
O [OMS (Microsoft Operations Management Suite)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda você a gerenciar e proteger sua infraestrutura local e de nuvem.


[Soluções de Gerenciamento](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) são conjuntos de lógica pré-empacotados que implementam um cenário de gerenciamento específico usando um ou mais serviços do OMS. Soluções diferentes estão disponíveis da Microsoft e de parceiros que você pode adicionar facilmente tooyour assinatura do Azure tooincrease Olá valor seu investimento do OMS. Como parceiro, você pode criar sua próprias soluções toosupport seus aplicativos e serviços e fornecê-los toousers por meio de saudação do Azure Marketplace ou modelos de início rápido.


![Soluções de gerenciamento](./media/azure-operational-security/azure-operational-security-fig4.png)

Um bom exemplo de uma solução que usa várias funcionalidades adicionais tooprovide de serviços é hello [solução de gerenciamento de atualização de](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management). Esta solução usa Olá [análise de Log](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) agente para Windows e Linux toocollect obter informações sobre as atualizações necessárias em cada agente. Ele grava esse repositório de análise de Log de toohello dados onde você pode analisar com um painel incluído.

Quando você cria uma implantação, os runbooks [automação do Azure](https://docs.microsoft.com/azure/automation/automation-intro) tooinstall usado necessárias atualizações. Gerenciar todo o processo no portal de saudação e não é necessário tooworry sobre detalhes subjacentes hello.

## <a name="azure-security-center"></a>Central de Segurança do Azure

A Central de Segurança do Azure ajuda a proteger os recursos do Azure. Ela fornece monitoramento de segurança integrado e gerenciamento de políticas em suas assinaturas do Azure. No serviço de saudação, você é capaz de toodefine políticas não apenas em relação a suas assinaturas do Azure, mas também em [grupos de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups), portanto, pode ser mais granular.

### <a name="security-policies-and-recommendations"></a>Políticas de segurança e recomendações 

Uma política de segurança define o conjunto de saudação de controles que são recomendados para recursos em Olá especificado assinatura ou grupo de recursos.

Central de segurança, você definirá da empresa tooyour requisitos de segurança e tipo hello de aplicativos ou confidencialidade dos dados saudação de acordo com as políticas.

![Políticas de segurança e recomendações ](./media/azure-operational-security/azure-operational-security-fig5.png)


Políticas que estão habilitadas no nível de assinatura Olá automaticamente propaguem tooall grupos de recursos de assinatura do hello conforme mostrado no diagrama Olá Olá direita:


### <a name="data-collection"></a>Coleta de dados

Central de segurança coleta dados de suas máquinas virtuais (VMs) tooassess seu estado de segurança, forneça recomendações de segurança e alertá-lo toothreats. Quando você acessa pela primeira vez a Central de Segurança, a coleta de dados é habilitada em todas as VMs em sua assinatura. Coleta de dados é recomendada, mas você pode recusá-lo ao desativar a coleta de dados Olá política Central de segurança.

### <a name="data-sources"></a>Fontes de dados

- Central de segurança do Azure analisa dados de saudação visibilidade de tooprovide fontes a seguir em seu estado de segurança, identificar vulnerabilidades recomendável atenuações e detectar ameaças ativas:

-   Os serviços do Azure: Usa informações sobre a configuração de saudação de serviços do Azure que você implantou comunicando-se com o provedor de recursos do serviço.

- Tráfego da Rede: usa os metadados do tráfego da rede de exemplo a partir da infraestrutura da Microsoft, como a origem/IP de destino/porta, tamanho do pacote e protocolo da rede.

-   Soluções de Parceiros: usa alertas de segurança das soluções de parceiros integradas, como firewalls e soluções antimalware.

-   Suas Máquinas Virtuais: usa as informações da configuração e informações sobre os eventos de segurança, como eventos do Windows e logs de auditoria, logs do IIS, mensagens do syslog e arquivos de despejo corrompidos de suas máquinas virtuais.

### <a name="data-protection"></a>Proteção de dados

impedir que clientes toohelp, detectam e respondem toothreats, Central de segurança do Azure coleta e processa os dados relacionados à segurança, incluindo informações de configuração, metadados, logs de eventos, os arquivos de despejo de falha e muito mais. A Microsoft obedece toostrict diretrizes de conformidade e segurança — da codificação toooperating um serviço.

-   **Diferenciação de dados**: dados são mantidos separados logicamente em cada componente serviço hello. Todos os dados são marcados por organização. Essa marcação persiste em todo o ciclo de vida de dados de saudação e é imposta em cada camada de serviço hello.

-   **Acesso a dados**: tooprovide recomendações de segurança e investigar potenciais ameaças de segurança, funcionários da Microsoft podem acessar as informações coletadas ou analisados pelos serviços do Azure, incluindo arquivos de despejo de falha, processar eventos de criação de disco de VM os instantâneos e artefatos, que podem incluir acidentalmente os dados do cliente ou dados pessoais de suas máquinas virtuais. Cumprimento toohello [política de privacidade e termos do Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), qual estado em que a Microsoft não é usa os dados do cliente ou derivar informações dele para fins comerciais propaganda ou semelhantes.

-   **Use dados**: a Microsoft usa os padrões e inteligência de ameaça Vista em vários locatários tooenhance nossos recursos de detecção e prevenção; fazemos acordo com os compromissos de privacidade de saudação descritos em nosso [privacidade Instrução](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).

### <a name="data-location"></a>Local dos dados

A Central de Segurança do Azure coleta as cópias transitórias dos seus arquivos de despejo corrompidos e analisa-as para obter evidências das tentativas de exploração e comprometimentos bem-sucedidos. Central de segurança do Azure executa essa análise no hello mesma área geográfica como Olá espaço de trabalho e exclusões Olá cópias efêmeras quando a análise for concluída. Artefatos de máquina são armazenados centralmente no hello mesma região como Olá VM.

-   **Suas Contas de Armazenamento**: uma conta de armazenamento é especificada para cada região em que as máquinas virtuais estão em execução. Isso permite que você toostore dados Olá mesma região que a máquina virtual de saudação do qual Olá os dados são coletados.

-   **Armazenamento central de segurança do Azure**: informações sobre alertas de segurança, incluindo alertas de parceiro, recomendações e status de integridade de segurança são armazenadas centralmente, atualmente Olá dos Estados Unidos. Essas informações podem incluir informações de configuração relacionados e eventos de segurança coletados de suas máquinas virtuais como tooprovide necessário você com o status de integridade Olá segurança alerta, recomendação ou segurança.


## <a name="azure-monitor"></a>Azure Monitor

Olá [OMS segurança](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) e habilita de solução de auditoria IT tooactively monitorar todos os recursos, que podem ajudar a minimiza o impacto de saudação de incidentes de segurança. A Segurança e Auditoria do OMS tem domínios de segurança que podem ser usados para monitorar os recursos. domínio de segurança Olá fornece acesso rápido toooptions, para o monitoramento Olá segurança domínios a seguir são abordados em mais detalhes:

-   Avaliação de malware
-   Avaliação de atualização
-   Identidade e Acesso.

Monitor do Azure fornece tooinformation ponteiros em tipos específicos de recursos. Ele oferece visualização, consulta, roteamento, alertas, AutoEscala e automação em dados de saudação infraestrutura do Azure (Log de atividade) e cada recurso do Azure individual (Logs de diagnóstico).

![Azure Monitor](./media/azure-operational-security/azure-operational-security-fig6.png)


Os aplicativos em nuvem são complexos com muitas partes móveis. O monitoramento fornece tooensure de dados que seu aplicativo permaneça ativo e em execução em um estado íntegro. Ele também ajuda você toostave off problemas potenciais ou solucionar problemas após os.

Além disso, você pode usar o monitoramento dados toogain aprofundamento sobre seu aplicativo. Esse conhecimento pode ajudá-lo a facilidade de manutenção ou de desempenho do aplicativo tooimprove, ou automatizar ações que normalmente exigiriam a intervenção manual.

### <a name="azure-activity-log"></a>Log de Atividades do Azure


É um log que fornece informações sobre operações de saudação que foram executadas em recursos em sua assinatura. Hello atividade Log era conhecido anteriormente como "Logs de auditoria" ou "Logs operacionais", pois ele relata eventos de plano de controle para suas assinaturas.

![Log de Atividades do Azure](./media/azure-operational-security/azure-operational-security-fig7.png)

Usando hello atividade de Log, você pode determinar Olá ', quem e quando ' para qualquer gravação as operações executadas em recursos de saudação em sua assinatura (PUT, POST, DELETE). Você também pode saber o status de saudação da operação de saudação e outras propriedades relevantes. Olá Log de atividades não incluir leitura (GET) operações ou operações para recursos que usam o modelo clássico de saudação.

### <a name="azure-diagnostic-logs"></a>Logs de Diagnóstico do Azure

Esses logs são emitidos por um recurso e fornecem dados ricos, frequentes sobre a operação de saudação do recurso. conteúdo de saudação desses logs varia por tipo de recurso.

Por exemplo, os logs de eventos do sistema Windows são uma categoria de Log de Diagnóstico para VMs, e logs de blobs, tabelas e filas são categorias de Logs de Diagnóstico para contas de armazenamento.

Os Logs de diagnóstico diferem de saudação [(anteriormente conhecido como Log operacional ou de Log de auditoria) do Log de atividades](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). log de atividades de saudação fornece uma visão em operações de saudação que foram executadas em recursos em sua assinatura. Os Logs de Diagnóstico fornecem informações em operações que o recurso realizou por conta própria.

### <a name="metrics"></a>Métricas

Monitor do Azure permite que você tooconsume telemetria toogain visibilidade do desempenho de saudação e a integridade de suas cargas de trabalho no Azure. tipo mais importante de saudação de dados de telemetria do Azure é métricas hello (também chamadas de contadores de desempenho) emitidas por recursos mais do Azure. Monitor do Azure fornece tooconfigure de diversas maneiras e consumir esses [métricas](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) para monitoramento e solução de problemas. Métricas são uma fonte valiosa de telemetria e permitem que você toodo Olá tarefas a seguir:

-   **Rastrear o desempenho de saudação** do recurso (como uma VM, site ou lógica de aplicativo) por plotagem suas métricas em um gráfico de portal e fixando tooa esse gráfico do painel.

-   **Ser notificado de um problema** que impactos Olá desempenho do recurso quando uma métrica ultrapassar um certo limite.

-   **Configurar ações automatizadas**, como dimensionar automaticamente um recurso ou disparar um runbook quando uma métrica cruza certo limite.

-   **Executar análises avançadas** ou gerar relatórios sobre as tendências de desempenho ou uso do recurso.

-   **Arquivamento** Olá histórico de desempenho ou a integridade do recurso para fins de auditoria ou de conformidade.

### <a name="azure-diagnostics"></a>Diagnóstico do Azure

Ele é o recurso de saudação dentro do Azure que habilita a coleta de saudação de dados de diagnóstico em um aplicativo implantado. Você pode usar a extensão de diagnóstico de saudação de várias fontes diferentes. As que têm suporte no momento são as [Funções de Trabalho ou Web do Serviço de Nuvem do Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), as [Máquinas Virtuais do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/overview) que executam o Microsoft Windows e o [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics). Outros serviços do Azure têm seu próprios diagnósticos separados.

## <a name="azure-network-watcher"></a>Observador de Rede do Azure

A auditoria da segurança de sua rede é fundamental para detectar vulnerabilidades de rede e garantir a conformidade com o modelo de governança regulatória e segurança de TI. Com a exibição de grupo de segurança, você pode recuperar regras de grupo de segurança de rede e segurança de saudação configurada e Olá regras de segurança efetiva. Lista de saudação de regras aplicadas, você pode determinar portas Olá que estejam abertos e avaliam a vulnerabilidade de rede.

[Inspetor de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) é um serviço regional que permite que você toomonitor e diagnosticar as condições em um nível de rede no e do Azure. Diagnóstico de rede e as ferramentas de visualização disponíveis com o observador de rede ajudarão-lo a entender, diagnosticar e obter a rede de tooyour insights no Azure. Esse serviço inclui a captura de pacotes, próximo salto, verificação do fluxo de IP, exibição do grupo de segurança e logs de fluxo de NSG. Monitoramento do nível do cenário fornece uma exibição de tooend final dos recursos de rede no monitoramento de recursos de rede do contraste tooindividual.

![Observador de Rede do Azure](./media/azure-operational-security/azure-operational-security-fig8.png)

Observador de rede atualmente tem Olá recursos a seguir:

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">Logs de auditoria</a>**-as operações executadas como parte da configuração de saudação de redes são registradas. Esses logs podem ser exibidos no portal do Azure de saudação ou recuperados por meio de ferramentas da Microsoft, como o Power BI ou ferramentas de terceiros. Logs de auditoria estão disponíveis por meio do portal hello, PowerShell, CLI e API de Rest. Para obter mais informações sobre os Logs de auditoria, consulte Operações de auditoria com o Resource Manager. Os logs de auditoria estão disponíveis para as operações realizadas em todos os recursos da rede.


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">Verificações do fluxo de IP </a>** – verifica se um pacote é permitido ou negado com base nos parâmetros do pacote com cinco tuplas das informações do fluxo (IP de Destino, IP de Origem, Porta de Destino, Porta de Origem e Protocolo). Se o pacote de saudação é negado por um grupo de segurança de rede, regra hello e grupos de segurança de rede que o pacote de saudação de negado é retornado.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">Próximo salto</a>**  -determina o próximo salto Olá para pacotes que está sendo direcionado no hello malha de rede do Azure, permitindo que você rotas toodiagnose qualquer configuradas incorretamente definido pelo usuário.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">Exibição de grupo de segurança</a>**  -obtém Olá segurança efetiva e aplicadas regras que são aplicadas em uma máquina virtual.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">Log de fluxo de NSG</a>**  -fluxo de logs para grupos de segurança de rede permitem que você toocapture logs tootraffic relacionados que são permitidas ou negadas pelas regras de segurança de saudação no grupo de saudação. Olá fluxo é definido pelas informações de uma tupla 5 – IP de origem, IP de destino, porta de origem, porta de destino e protocolo.

## <a name="azure-storage-analytics"></a>Análise do Armazenamento do Azure

[Análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) pode armazenar métricas que incluem dados de estatísticas e a capacidade de transações agregadas sobre o serviço de armazenamento de tooa solicitações. As transações são relatadas no nível de operação ambos Olá API e no nível de serviço de armazenamento hello e capacidade é relatada no nível de serviço de armazenamento de saudação. Dados de métrica pode ser usado tooanalyze uso do serviço de armazenamento, diagnosticar problemas com solicitações feitas no serviço de armazenamento hello e desempenho de saudação tooimprove dos aplicativos que usam um serviço.

O [Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) executa o registro em log e fornece dados de métrica para uma conta de armazenamento. Você pode usar este tootrace as solicitações de dados, analisar tendências de uso e diagnosticar problemas com sua conta de armazenamento. Log de análise de armazenamento está disponível para Olá [serviços Blob, fila e tabela](https://docs.microsoft.com/azure/storage/storage-introduction). Análise de armazenamento registra informações detalhadas sobre o serviço de armazenamento de tooa de solicitações bem-sucedidas e com falha.

Essas informações podem ser usadas toomonitor as solicitações individuais e toodiagnose problemas com um serviço de armazenamento. As solicitações são registradas em uma base de melhor esforço. Entradas de log são criadas somente se houver solicitações feitas no ponto de extremidade de serviço hello. Para exemplo se uma conta de armazenamento tiver atividade em seu ponto de extremidade de Blob, mas não em seus pontos de extremidade de fila ou tabela, somente logs pertencente toohello serviço Blob é criado.

toouse análise de armazenamento, você deve habilitá-lo individualmente para cada serviço, você deseja toomonitor. Você pode habilitá-lo no hello [portal do Azure](https://portal.azure.com/); para obter detalhes, consulte [monitorar uma conta de armazenamento no portal do Azure de saudação](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Você também pode habilitar a análise de armazenamento programaticamente por meio de saudação API REST ou biblioteca de saudação do cliente. Use Olá definir propriedades de serviço operação tooenable análise de armazenamento individualmente para cada serviço.

dados agregados Hello são armazenados em um blob conhecido (para registro em log) e em tabelas conhecidas (para Métrica), que podem ser acessadas usando o serviço de Blob hello e APIs do serviço de tabela.

Análise de armazenamento tem um limite de 20 TB em quantidade Olá dos dados armazenados que são independentes do limite total de saudação para sua conta de armazenamento. Todos os logs são armazenados em [blobs de blocos](https://docs.microsoft.com/azure/storage/storage-analytics) em um contêiner chamado $logs, que é criado automaticamente quando o Storage Analytics é habilitado em uma conta de armazenamento.

Olá seguintes ações executadas pelo Storage Analytics é faturável:

-   Blobs de toocreate solicitações de registro em log
-   Solicitações toocreate de entidades de tabela de métricas.

> [!Note]
> Para obter mais informações sobre cobrança e políticas de retenção de dados, consulte [Storage Analytics e cobrança](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing).
> Para otimizar o desempenho, você deseja toolimit número de saudação de discos altamente utilizados anexado toohello máquina virtual tooavoid possíveis de limitação. Se todos os discos não estão sendo intensamente utilizados no hello mesmo tempo, conta de armazenamento Olá pode dar suporte a um disco número maior.

> [!Note]
> Para obter mais informações sobre os limites da conta de armazenamento, consulte [Escalabilidade e metas de desempenho do Armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-scalability-targets).


Olá seguintes tipos de solicitações autenticadas e anônimas está conectado.

| Autenticada  | Anônima|
| :------------- | :-------------|
| Solicitações bem-sucedidas | Solicitações bem-sucedidas |
|Solicitações com falha, incluindo tempo limite, limitação, rede, autorização e outros erros | Solicitações que usam uma SAS (Assinatura de Acesso Compartilhado), incluindo solicitações bem-sucedidas e com falha |
| Solicitações que usam uma SAS (Assinatura de Acesso Compartilhado), incluindo solicitações bem-sucedidas e com falha |Erros de tempo limite para o cliente e o servidor |
|   Dados de tooanalytics de solicitações |    Solicitações GET com falha com o código de erro 304 (Não Modificado) |
| As solicitações feitas pela própria análise de armazenamento, como criação de log ou exclusão, não estão conectadas. Uma lista completa dos dados saudação conectado está documentada em Olá [operações registradas em log de análise de armazenamento e mensagens de Status](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) e [formato de Log de análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) tópicos. | Todas as outras solicitações anônimas com falha não estão conectadas. Uma lista completa dos dados saudação conectado está documentada em Olá [operações registradas em log de análise de armazenamento e mensagens de Status](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) e [formato de Log de análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |
## <a name="azure-active-directory"></a>Azure Active Directory

O Azure AD também inclui um pacote completo de funcionalidades de gerenciamento de identidade, incluindo autenticação multifator, registro de dispositivos, gerenciamento de senhas de autoatendimento, gerenciamento de grupos de autoatendimento, gerenciamento de contas com privilégios, controle de acesso baseado em função, monitoramento de uso de aplicativos, auditoria avançada, alertas e monitoramento de segurança.

-   Aprimore a segurança dos aplicativos com o acesso condicional e a autenticação multifator do AD do Azure.

-   Monitore o uso dos aplicativos e proteja sua empresa contra ameaças avançadas com monitoramento e relatórios de segurança.

O Active Directory do Azure (Azure AD) inclui relatórios de auditoria, atividade e segurança para seu diretório. [Olá relatório de auditoria do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) ajuda os clientes tooidentify privilegiado ações que ocorreram no seu Active Directory do Azure. Ações privilegiadas incluem alterações de elevação (por exemplo, criação de função ou redefinições de senha), alterar configurações de política (por exemplo políticas de senha), ou a configuração de toodirectory de alterações (por exemplo, alterações toodomain configurações de federação).

relatórios de Olá fornecem o registro de auditoria Olá para o nome do evento hello, ator Olá que executou a ação hello, o recurso de destino Olá afetada pela alteração Olá e data de saudação (em UTC). Os clientes são tooretrieve capaz de lista de saudação de eventos de auditoria para seu Azure Active Directory por meio de saudação [portal do Azure](https://portal.azure.com/), conforme descrito em [Exibir Logs de auditoria](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Aqui está uma lista de relatórios de saudação incluídos:

| Relatórios de segurança  | Relatórios de atividades| Relatórios de auditoria |
| :------------- | :-------------| :-------------|
|Entradas de fontes desconhecidas | Uso do aplicativo: resumo | Relatório de auditoria de diretório |
|Entradas após várias falhas | Uso do aplicativo: detalhado |   |
|Entradas de várias geografias | Painel do aplicativo |  |
|Entradas de endereços IP com atividade suspeita |Erros de provisionamento de conta |  |
|Atividades de entrada irregulares |Dispositivos de usuário individual |  |
|Entradas de dispositivos possivelmente infectados |Atividade de usuário individual |   |
|Usuários com atividade de entrada anômala |Relatório de atividade de grupos |   |
| |Relatório de atividade de registro de redefinição de senha |   |
| |Atividade de redefinição de senha |   | |



dados Olá desses relatórios podem ser útil tooyour aplicativos, como sistemas SIEM, auditoria e ferramentas de business intelligence. relatórios de saudação do AD do Azure [APIs](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) fornecem acesso programático toohello dados por meio de um conjunto de APIs com base em REST. Você pode chamar essas APIs em várias ferramentas e linguagens de programação.

Eventos em Olá relatório de auditoria do AD do Azure são mantidos por 180 dias.

> [!Note]
> Para saber mais sobre retenção de relatórios, confira [Políticas de retenção de relatório do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Para clientes interessados em armazenar seus [eventos de auditoria](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) para períodos de retenção mais longo, hello API de relatório pode ser usado tooregularly eventos de auditoria de pull em um repositório de dados separado.

## <a name="summary"></a>Resumo

Resumos este artigo proteger sua privacidade e segurança de dados, oferecendo softwares e serviços que ajudam você gerenciam Olá infraestrutura de TI da sua organização. A Microsoft reconhece que, quando eles entrega tooothers seus dados, essa confiança requer segurança rigorosa. A Microsoft obedece toostrict diretrizes de conformidade e segurança — da codificação toooperating um serviço. Segurança e proteção de dados é uma prioridade principal da Microsoft.

Este artigo explica

-   Como dados são coletados, processados e protegidos Olá Operations Management Suite (OMS).

-   Analisar eventos rapidamente em várias fontes de dados. Identificar riscos à segurança e compreender o escopo de saudação e o impacto de ataques e ameaças toomitigate danos de saudação de uma violação de segurança.

-   Identificar padrões de ataque visualizando o tráfego IP mal-intencionado de saída e tipos de ameaça mal-intencionados. Entenda a postura de segurança de saudação de todo o seu ambiente, independentemente da plataforma.

-   Capture todos Olá eventos e log dados necessários para uma auditoria de segurança ou de conformidade. Tempo de saudação de barra e recursos necessários toosupply com um conjunto de dados de eventos e log completo, exportável e pesquisável de auditoria de segurança.

<ul>
<li>Colete eventos relacionados à segurança, a auditoria e a análise de violação tookeep um fechamento olho seus ativos:</li>
<ul>
<li>Postura de segurança</li>
<li>Problemas importantes</li>
<li>Ameaças resumidas</li>
</ul>
</ul>

## <a name="next-steps"></a>Próximas etapas

- [Design e segurança operacional](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft projeta seus serviços e software com a segurança em mente toohelp Certifique-se de que sua infraestrutura de nuvem é flexível e protegido contra ataques.

- [Operations Management Suite | Segurança e Conformidade](https://www.microsoft.com/cloud-platform/security-and-compliance)

Microsoft security dados e análise tooperform mais inteligente e eficiente de usar a detecção de ameaças.

- [Planejamento da Central de segurança do Azure e operações](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) um conjunto de etapas e tarefas que você pode seguir toooptimize o uso da Central de segurança com base em requisitos de segurança da sua organização e o modelo de gerenciamento de nuvem.

