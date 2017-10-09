---
title: "Visão geral de segurança operacional aaaAzure | Microsoft Docs"
description: "Este artigo fornece uma visão geral da saudação segurança operacional do Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Visão geral de segurança operacional do Azure
Segurança operacional Azure refere-se a serviços toohello, controles e toousers de recursos disponíveis para proteger seus dados, aplicativos e outros recursos do Microsoft Azure. [Segurança operacional Azure](https://docs.microsoft.com/azure/security/azure-operational-security) é uma estrutura que incorpora conhecimento Olá obtida por meio de uma variedade de recursos que são exclusivo tooMicrosoft, incluindo Olá Microsoft Security Development Lifecycle (SDL), Olá Microsoft Security Programa de Response Center e profundo reconhecimento do cenário de ameaças de segurança Olá cibernéticos.

Este artigo de visão geral de segurança operacional Azure enfoca Olá áreas a seguir:

- Azure Operations Management Suite
-   Central de Segurança do Azure
-   Azure Monitor
-   Observador de Rede do Azure
-   Análise do Armazenamento do Azure
-   Azure Active Directory

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite
Operações de TI é responsável por gerenciar a infraestrutura de datacenter, aplicativos e dados, incluindo a estabilidade do hello e segurança desses sistemas. No entanto, obter informações de segurança em aumentar os ambientes de TI complexos geralmente requer organizações toocobble reúnem dados de vários sistemas de gerenciamento e segurança.

O [OMS (Microsoft Operations Management Suite)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda você a gerenciar e proteger sua infraestrutura local e de nuvem.

O OMS é uma solução de gerenciamento de TI baseada em nuvem com muitas ofertas, como a Automação de TI, Segurança e Conformidade, o Log Analytics e Backup e Recuperação. Como tal, ele é um toomanage auxílio perfeito e proteger sua infraestrutura de TI — locais e na nuvem hello.

funcionalidade de núcleo de saudação do OMS é fornecida por um conjunto de serviços que são executados no Azure. Cada serviço fornece uma função de gerenciamento específico, e você pode combinar os cenários de gerenciamento diferente de tooachieve de serviços. Que inclui:

-   Log Analytics
-   Automação
-   Backup
-   Site Recovery

### <a name="log-analytics"></a>Log Analytics
O [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) fornece serviços de monitoramento para o OMS coletando dados de recursos gerenciados em um repositório central. Esses dados podem incluir eventos, dados de desempenho ou dados personalizados fornecidos por meio da API de saudação. Depois de coletados, dados saudação estão disponíveis para alertas, análise e exportação. Esse método permite tooconsolidate dados de uma variedade de fontes de forma que você pode combinar dados de seus serviços do Azure com seu ambiente local existente. Ele também separa coleção Olá dos dados Olá pela ação de saudação executada com os dados para que todas as ações disponíveis tooall tipos de dados.

### <a name="automation"></a>Automação
Microsoft [automação do Azure](https://docs.microsoft.com/azure/automation/automation-intro) fornece uma maneira para os usuários tooautomate tarefas Olá manuais demoradas, propensas a erros e repetidas com frequência que geralmente são executadas em um ambiente de nuvem e enterprise. Economiza tempo e aumenta a confiabilidade de saudação de tarefas administrativas regulares e até mesmo agenda essas toobe automaticamente executada em intervalos regulares. Você pode automatizar processos usando runbooks ou automatizar o gerenciamento de configuração usando Configuração de Estado Desejado.

### <a name="backup"></a>Backup
[O Backup do Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) é Olá serviço baseado no Azure você pode usar tooback (ou proteger) e restaurar dados de saudação nuvem da Microsoft. Ele substitui a solução de backup local ou externa existente por uma solução confiável, segura e econômica baseada em nuvem. O Backup do Azure oferece vários componentes que você baixar e implanta no computador apropriado do hello, servidor, ou na nuvem hello. componente de saudação ou agente, que você implantar depende o que você deseja tooprotect. Todos os componentes de Backup do Azure (não importa se você estiver protegendo dados locais ou na nuvem Olá) podem ser usado tooback o Cofre de serviços de recuperação de tooa de dados no Azure. Consulte Olá [tabela de componentes de Backup do Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use).

### <a name="site-recovery"></a>Recuperação de site
[O Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) fornece continuidade dos negócios ao orquestrar a replicação do local virtual e máquinas físicas tooAzure ou site secundário tooa. Se seu site primário não estiver disponível, você failover local secundário toohello para que os usuários podem continuar trabalhando e failback quando sistemas retornam tooworking ordem. detecção de ameaças inteligente e eficiente.

## <a name="azure-active-directory"></a>Azure Active Directory
O [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario) é a solução IDaaS (Identidade como Serviço) abrangente da Microsoft que:

-   Habilita o IAM como um serviço de nuvem
-   Fornece gerenciamento de acesso central, logon único (SSO) e relatórios
-   Oferece suporte ao gerenciamento de acesso integrado para [milhares de aplicativos](https://azure.microsoft.com/marketplace/active-directory/) na Galeria de aplicativo hello, incluindo Salesforce, Google Apps, caixa, Concur e muito mais.

O Azure AD também inclui um pacote completo de [funcionalidades de gerenciamento de identidade](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports), incluindo [autenticação multifator](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), [registro de dispositivos]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview), [gerenciamento de senhas de autoatendimento](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/), [gerenciamento de grupos de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), [gerenciamento de contas com privilégios](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure), [controle de acesso baseado em função](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), [monitoramento de uso de aplicativos](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health), [auditoria avançada](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) e [alertas e monitoramento de segurança](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts).

Com o Azure Active Directory, todos os aplicativos que você publicar para seus parceiros e clientes (comercial ou consumidor) têm Olá mesmos recursos de gerenciamento de identidades e acesso. Isso permite que você toosignificantly reduzir os custos operacionais.

## <a name="azure-security-center"></a>Central de Segurança do Azure
[Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-get-started) Olá de ajuda a evitar, detectar e responder toothreats maior visibilidade e controle sobre a segurança de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

A [Central de Segurança](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine) ajuda a proteger os dados de máquinas virtuais no Azure, fornecendo visibilidade para configurações de segurança da máquina virtual e monitoramento de ameaças. A Central de Segurança pode monitorar as máquinas virtuais para:

-   Configurações de segurança do sistema operacional (SO) com hello recomendado regras de configuração
-   Segurança do sistema e atualizações críticas que estão ausentes
-   Recomendações de proteção de ponto de extremidade
-   Validação de criptografia de disco
-   Ataques de rede

Central de segurança do Azure usa [controle de acesso baseado em função (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure), que fornece [funções internas](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) que podem ser atribuídos toousers, grupos e serviços no Azure.

Central de segurança avalia a configuração de saudação de vulnerabilidades e problemas de segurança de tooidentify de recursos. Na Central de segurança, você ver apenas as informações relacionadas tooa recurso quando foi atribuída a função de saudação do leitor, colaborador ou proprietário para Olá assinatura ou grupo de recursos que o recurso pertence.

>[!Note]
>Consulte [permissões na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-permissions) toolearn mais sobre as funções e ações permitidas na Central de segurança.

Central de segurança usa Olá Microsoft Monitoring Agent – essa é Olá mesmo agente usado pelo serviço de Operations Management Suite e análise de Log de saudação. Dados coletados deste agente são armazenados em uma análise Log existente [espaço de trabalho](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access) associado à sua assinatura do Azure ou um novo espaço, levando em conta localização geográfica de saudação do hello VM.

## <a name="azure-monitor"></a>Azure Monitor
Problemas de desempenho em seu aplicativo de nuvem podem afetar seus negócios. Com diversos componentes interconectados e frequentes lançamentos, degradações podem ocorrer a qualquer momento. E se você estiver desenvolvendo um aplicativo, seus usuários normalmente descobrirão problemas que você não encontrou durante os testes. Você deve saber sobre esses problemas imediatamente e ferramentas para diagnosticar e corrigir problemas de saudação.

O [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) é uma ferramenta básica para monitorar serviços em execução no Azure. Ele fornece dados de nível de infraestrutura sobre taxa de transferência de saudação de um serviço e uma saudação em torno de ambiente. Se você estiver gerenciando seus aplicativos tudo no Azure, decidir se tooscale para cima ou para baixo de recursos, Monitor do Azure permite que você usa toostart.

Além disso, você pode usar o monitoramento dados toogain aprofundamento sobre seu aplicativo. Esse conhecimento pode ajudá-lo a facilidade de manutenção ou de desempenho do aplicativo tooimprove, ou automatizar ações que normalmente exigiriam a intervenção manual. Ele inclui:

-   Log de Atividades do Azure
-   Logs de Diagnóstico do Azure
-   Métricas
-   Diagnóstico do Azure

### <a name="azure-activity-log"></a>Log de Atividades do Azure
É um log que fornece informações sobre operações de saudação que foram executadas em recursos em sua assinatura. Olá [Log de atividades](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) era conhecido anteriormente como "Logs de auditoria" ou "Logs operacionais", pois ele relata eventos de plano de controle para suas assinaturas.

### <a name="azure-diagnostic-logs"></a>Logs de Diagnóstico do Azure
[Logs de diagnóstico do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) são emitidos por um recurso e fornecer dados ricos, frequentes sobre a operação de saudação do recurso. conteúdo de saudação desses logs varia por tipo de recurso.

Por exemplo, os logs de eventos do sistema Windows são uma categoria de Log de Diagnóstico para VMs, e logs de blobs, tabelas e filas são categorias de Logs de Diagnóstico para contas de armazenamento.

Os Logs de diagnóstico diferem de saudação [(anteriormente conhecido como Log operacional ou de Log de auditoria) do Log de atividades](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). log de atividades de saudação fornece uma visão em operações de saudação que foram executadas em recursos em sua assinatura. Os Logs de Diagnóstico fornecem informações em operações que o recurso realizou por conta própria.

### <a name="metrics"></a>Métricas
Monitor do Azure permite que você tooconsume telemetria toogain visibilidade do desempenho de saudação e a integridade de suas cargas de trabalho no Azure. tipo mais importante de saudação de dados de telemetria do Azure é métricas hello (também chamadas de contadores de desempenho) emitidas por recursos mais do Azure. Monitor do Azure fornece tooconfigure de diversas maneiras e consumir esses [métricas](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) para monitoramento e solução de problemas.

### <a name="azure-diagnostics"></a>Diagnóstico do Azure
Ele é o recurso de saudação dentro do Azure que habilita a coleta de saudação de dados de diagnóstico em um aplicativo implantado. Você pode usar a extensão de diagnóstico de saudação de várias fontes diferentes. As que têm suporte no momento são as [Funções de Trabalho ou Web do Serviço de Nuvem do Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), as [Máquinas Virtuais do Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) que executam o Microsoft Windows e o [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics).


## <a name="network-watcher"></a>Observador de Rede
Os clientes criam uma rede de ponta a ponta no Azure administrando e compondo vários recursos de rede individuais, como VNet, ExpressRoute, Gateway de Aplicativo, Balanceadores de carga e mais. Monitoramento está disponível em cada um dos recursos de rede hello.

rede de tooend Olá end pode ter configurações complexas e as interações entre os recursos, criar cenários complexos que precisam baseada em cenário de monitoramento por meio do observador de rede.

O [Observador de Rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) simplifica a monitoramento e o diagnóstico da rede do Azure. Ferramentas de diagnóstico e de visualização disponíveis com enable observador de rede que você tootake remoto capturas de pacotes em uma máquina de Virtual do Azure, obter ideias sobre o tráfego de rede usando logs de fluxo e diagnosticar conexões e Gateway de VPN.

Observador de rede atualmente tem Olá recursos a seguir:

- [Topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -fornece uma saudação de mostrando de exibição de nível de rede vários interconexões e associações entre recursos de rede em um grupo de recursos.
-   [Captura de Pacote Variável](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) – captura dados do pacote dentro e fora de uma máquina virtual. Avançado ajustados controles como sendo tooset capaz de tempo e opções de filtragem e limitações de tamanho fornecem versatilidade. dados de pacote de saudação podem ser armazenados em um repositório de blob ou no disco local do hello no formato. cap.
-   [Verificação do fluxos de IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) - verifica se um pacote é permitido ou negado com base nos parâmetros do pacote com cinco tuplas das informações do fluxo (IP de Destino, IP de Origem, Porta de Destino, Porta de Origem e Protocolo). Se o pacote de saudação é negado por um grupo de segurança, hello regra e o grupo negado de pacote de saudação é retornado.
-   [Próximo salto](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -determina o próximo salto Olá para pacotes que está sendo direcionado no hello malha de rede do Azure, permitindo que você rotas toodiagnose qualquer configuradas incorretamente definido pelo usuário.
-   [Exibição de grupo de segurança](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -obtém Olá segurança efetiva e aplicadas regras que são aplicadas em uma máquina virtual.
-   [Log de fluxo de NSG](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) -fluxo de logs para grupos de segurança de rede permitem que você toocapture logs tootraffic relacionados que são permitidas ou negadas pelas regras de segurança de saudação no grupo de saudação. Olá fluxo é definido pelas informações de uma tupla 5 – IP de origem, IP de destino, porta de origem, porta de destino e protocolo.
-   [Gateway de rede virtual e solução de problemas de Conexão](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -fornece Olá capacidade tootroubleshoot Gateways de rede Virtual e conexões.
-   [Limites de assinatura de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -permite o uso de recursos de rede tooview em limites de.
-   [Configurando o Log de diagnóstico](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) – fornece um único painel tooenable ou desabilitar logs de diagnóstico para recursos de rede em um grupo de recursos.

toolearn mais como ver o observador de rede tooconfigure, [configurar observador de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="developer-operations-devops"></a>DevOps (Operações de Desenvolvedor)
Desenvolvimento de aplicativos tooDevOps anterior, equipes foram responsável por reunir os requisitos de negócios para um programa de software e escrever código. Em seguida, uma equipe separada do controle de qualidade testa programa hello em um ambiente de desenvolvimento isolado, se os requisitos foram atendidos e versões Olá código para operações toodeploy. as equipes de implantação de saudação mais são fragmentadas em grupos em silos como banco de dados e de rede. Cada vez que um programa de software "gerado pela parede hello" tooan equipe independente adiciona afunilamentos.

[DevOps](https://www.visualstudio.com/learn/what-is-devops/) permite que as equipes toodeliver mais seguras, de alta qualidade com as soluções mais rápidas e mais baratas. Os clientes esperam uma experiência dinâmica e confiável ao consumir serviços e software.  Equipes rapidamente devem iterar nas atualizações de software, medir o impacto Olá atualizações Olá e responder rapidamente com novos problemas de tooaddress de iterações de desenvolvimento ou agregar mais valor.  AS plataformas de nuvem, como o Microsoft Azure, removem afunilamentos tradicionais e ajudam a massificar a infraestrutura. Software reigns em todas as empresas como Olá diferencial e fator em resultados de negócios. Nenhuma organização, developer ou trabalho IT pode ou deve evitar a movimentação de DevOps hello.

Profissionais de DevOps maduros adotarem várias Olá práticas recomendadas a seguir. Essas práticas [envolver pessoas](https://www.visualstudio.com/learn/what-is-devops-culture/) tooform estratégias com base em cenários de negócios de saudação.  Ferramentas podem ajudar a automatizar Olá várias práticas:

-   [Gerenciamento de planejamento e projeto Agile](https://www.visualstudio.com/learn/what-is-agile/) técnicas são usada tooplan e isolar o trabalho em sprints, gerenciar a capacidade de equipe e ajuda as equipes de se adaptar rapidamente às necessidades de negócios toochanging.
-   [Controle de versão, geralmente com Git](https://www.visualstudio.com/learn/what-is-git/), permite que as equipes localizadas em qualquer lugar no código-fonte Olá mundo tooshare e integrar com o pipeline de versão do software development tools tooautomate hello.
-   [Integração contínua](https://www.visualstudio.com/learn/what-is-continuous-integration/) unidades Olá mesclagem em andamento e o teste de código, que leva defeitos toofinding no início.  Outros benefícios incluem menos tempo gasto no combate a problemas de mesclagem e o recebimento de comentários rapidamente as para equipes de desenvolvimento.
-   [Fornecimento contínuo](https://www.visualstudio.com/learn/what-is-continuous-delivery/) das soluções de software tooproduction e ambientes de teste ajudam as organizações a corrigir erros rapidamente e responder alterando tooever negócios requisitos.
-   O [Monitoramento](https://www.visualstudio.com/learn/what-is-monitoring/) dos aplicativos em execução, incluindo ambientes de produção para a integridade do aplicativo, assim como o uso do cliente ajudam as organizações a formular uma hipótese e validar ou refutar rapidamente as estratégias.  Dados avançados são capturados e armazenados em vários formatos de log.
-   [Infraestrutura como código (IaC)](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/) é uma prática, o que permite a automação de saudação e validação da criação e a subdivisão do toohelp redes e máquinas virtuais no fornecimento de plataformas de hospedagem de aplicativo seguro e estável.
-   [Microservices](https://www.visualstudio.com/learn/what-are-microservices/) arquitetura é tooisolate utilizou casos de uso de negócios em serviços reutilizáveis pequenos.  Essa arquitetura oferece eficiência e escalabilidade.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o OMS solução de segurança e auditoria, consulte Olá artigos a seguir:

- [Operations Management Suite | Segurança e Conformidade](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Monitoramento e resposta tooSecurity alertas no Operations Management Suite solução de segurança e auditoria](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts).
- [Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources).
