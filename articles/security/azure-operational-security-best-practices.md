---
title: "práticas recomendadas de segurança operacional aaaAzure | Microsoft Docs"
description: "Este artigo fornece um conjunto de melhores práticas de Segurança Operacional do Azure."
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
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: b3b17ef20fb3545b1c268ac0d7ce692e07c8da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-best-practices"></a>Práticas recomendadas de Segurança Operacional do Azure
Segurança operacional Azure refere-se a serviços toohello, controles e toousers de recursos disponíveis para proteger seus dados, aplicativos e outros recursos do Microsoft Azure. Segurança operacionais do Azure é construída em uma estrutura que incorpora conhecimento Olá obtido por meio de diversos recursos que são exclusivo tooMicrosoft, incluindo Olá Microsoft Security Development Lifecycle (SDL), Olá Microsoft Security Response Center programa e conhecimento profundo do cenário de ameaças de segurança cibernética hello.

Neste artigo, veremos uma coleção de melhores práticas de segurança de banco de dados do Azure. Essas práticas recomendadas são derivadas da nossa experiência com segurança de banco de dados do Azure e experiências de saudação de clientes, como por conta própria.

Para cada prática recomendada, vamos explicar:
-   A prática recomendada que Olá é
-   Por que você deseja tooenable essa prática recomendada
-   O que pode ser resultado de saudação se você não a prática recomendada de saudação tooenable
- Como você pode aprender a prática recomendada de saudação tooenable

Este artigo de Azure operacional práticas recomendadas de segurança se baseia em uma opinião consenso e recursos da plataforma Azure e conjuntos de recursos, que existem em tempo de saudação que este artigo foi escrito. Tecnologias e opiniões alterar ao longo do tempo e este artigo será atualizado em um tooreflect regularmente essas alterações.

As melhores práticas de Segurança Operacional do Azure discutidas neste artigo incluem:

-   Monitorar, gerenciar e proteger a infraestrutura de nuvem
-   Gerenciar identidade e implementar o SSO (logon único)
-   Rastrear solicitações, analisar tendências de uso e diagnosticar problemas
-   Serviços de monitoramento com uma solução de monitoramento centralizada
-   Evitar, detectar e responder toothreats
-   Monitoramento de rede baseado em cenário de ponta a ponta
-   Implantação segura usando ferramentas do DevOps comprovadas

## <a name="monitor-manage-and-protect-cloud-infrastructure"></a>Monitorar, gerenciar e proteger a infraestrutura de nuvem
Operações de TI é responsável por gerenciar a infraestrutura de datacenter, aplicativos e dados, incluindo a estabilidade do hello e segurança desses sistemas. No entanto, obter informações de segurança em aumentar os ambientes de TI complexos geralmente requer organizações toocobble reúnem dados de vários sistemas de gerenciamento e segurança.

O [OMS (Microsoft Operations Management Suite)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda você a gerenciar e proteger sua infraestrutura local e de nuvem.

[Solução de segurança do OMS e auditoria](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) permite IT tooactively monitorar todos os recursos, que podem ajudar a minimiza o impacto de saudação de incidentes de segurança. A Segurança e Auditoria do OMS tem domínios de segurança que podem ser usados para monitorar os recursos.

Para obter mais informações sobre o OMS, leia o artigo de saudação [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

toohelp impedir, detectar e responder toothreats, [Operations Management Suite (OMS) solução de segurança e auditoria](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) coleta e processa os dados sobre seus recursos, que inclui:

-   Log de eventos de segurança
-   Eventos de ETW (Rastreamento de Eventos para Windows)
-   Eventos de auditoria do AppLocker
-   Log do Firewall do Windows
-   Eventos de Análise de Ameaças Avançadas
-   Resultados da avaliação de linha de base
-   Resultados da avaliação antimalware
-   Resultados da avaliação de atualização/patch
-   Fluxos de syslog que sejam explicitamente habilitados no agente Olá


## <a name="manage-identity-and-implement-single-sign-on"></a>Gerenciar identidade e implementar o logon único
O [Azure AD (Azure Active Directory)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) é o serviço de gerenciamento de identidade e diretório multilocatário baseado em nuvem da Microsoft.

O [Azure AD](https://azure.microsoft.com/services/active-directory/) também inclui um pacote completo de funcionalidades de [gerenciamento de identidade](https://docs.microsoft.com/azure/security/security-identity-management-overview), incluindo [autenticação multifator](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), registro de dispositivos, gerenciamento de senhas de autoatendimento, gerenciamento de grupos de autoatendimento, gerenciamento de contas com privilégios, controle de acesso baseado em função, monitoramento de uso de aplicativos, auditoria avançada e alertas e monitoramento de segurança.

Olá recursos a seguir pode ajudar a proteger aplicativos baseados em nuvem, simplificar os processos de TI, reduzir os custos e ajudar a garantir que as metas corporativas de conformidade sejam atendidas:

-   Gerenciamento de identidade e acesso para a nuvem Olá
-   Simplificar o acesso de usuário tooany aplicativo de nuvem
-   Proteja dados e aplicativos confidenciais
-   Habilite o autoatendimento aos seus funcionários
-   Integre-se com o Azure Active Directory

### <a name="identity-and-access-management-for-hello-cloud"></a>Gerenciamento de identidade e acesso para a nuvem Olá
Azure Active Directory (AD do Azure) é uma abrangente [solução de nuvem de gerenciamento de identidade e acesso](https://www.microsoft.com/cloud-platform/identity-management), que oferece um conjunto robusto de recursos toomanage usuários e grupos. Ele ajuda a proteger o acesso local tooon e aplicativos, inclusive serviços web do Microsoft como Office 365 e muito softwares da Microsoft como um aplicativo de serviço (SaaS) na nuvem.
toolearn mais como proteção de identidade tooenable no AD do Azure, consulte [ativando o Azure Active Directory identidade proteção](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable).

### <a name="simplify-user-access-tooany-cloud-app"></a>Simplificar o acesso de usuário tooany aplicativo de nuvem
[Habilitar logon único](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) toosimplify toothousands de acesso de usuário de aplicativos de nuvem de dispositivos do Windows, Mac, Android e iOS. Os usuários podem iniciar os aplicativos por meio de um painel de acesso personalizado baseado na Web ou por meio de um aplicativo móvel, usando suas credenciais da empresa. Use toogo de módulo de Proxy de aplicativo hello AD do Azure além de aplicativos SaaS e publicar no local da web aplicativos tooprovide altamente acesso remoto seguro e logon único.

### <a name="protect-sensitive-data-and-applications"></a>Proteja dados e aplicativos confidenciais
Habilitar [Azure multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) tooprevent não autorizado acessar tooon locais e aplicativos em nuvem, fornecendo um nível adicional de autenticação. Proteja seus negócios e reduza ameaças em potencial com monitoramento de segurança, alertas e relatórios baseados em machine learning que identificam padrões de acesso inconsistentes.

### <a name="enable-self-service-for-your-employees"></a>Habilite o autoatendimento aos seus funcionários
Delega funcionários de tooyour tarefas importantes, como a redefinição de senhas e criar e gerenciar grupos. [Habilite alteração de senha](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), redefinição e gerenciamento de grupos por autoatendimento com o Azure AD.

### <a name="integrate-with-azure-active-directory"></a>Integre-se com o Azure Active Directory
Estender [do Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-to-integrate) e qualquer outro local diretórios tooAzure AD tooenable logon único para todos os aplicativos baseados em nuvem. Atributos de usuário podem ser sincronizadas automaticamente tooyour diretório na nuvem de todos os tipos de diretórios locais.

toolearn mais sobre a integração do Active Directory do Azure e como tooenable, leia o artigo de saudação [integrar seus diretórios locais com o Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="trace-requests-analyze-usage-trends-and-diagnose-issues"></a>Rastrear solicitações, analisar tendências de uso e diagnosticar problemas
O [Azure Storage Analytics](https://docs.microsoft.com/azure/storage/storage-analytics) executa o registro em log e fornece dados de métrica para uma conta de armazenamento. Você pode usar este tootrace as solicitações de dados, analisar tendências de uso e diagnosticar problemas com sua conta de armazenamento.

A métrica da Análise de Armazenamento vem habilitada por padrão nas novas contas de armazenamento. Você pode habilitar o log e configurar as métricas e log em Olá portal do Azure; Para obter detalhes, consulte [monitorar uma conta de armazenamento no portal do Azure de saudação](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Você também pode habilitar a análise de armazenamento programaticamente por meio de saudação API REST ou biblioteca de saudação do cliente. Use Olá definir propriedades de serviço operação tooenable análise de armazenamento individualmente para cada serviço.

Para obter um guia detalhado sobre como usar a análise de armazenamento e outra ferramentas tooidentify, diagnosticar e solucionar problemas relacionados ao armazenamento do Azure, consulte [monitorar, diagnosticar e solucionar problemas de armazenamento do Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-monitoring-diagnosing-troubleshooting).

toolearn mais sobre a integração do Active Directory do Azure e como tooenable, leia o artigo de saudação [habilitando e configurando a análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/Enabling-and-Configuring-Storage-Analytics?redirectedfrom=MSDN).

## <a name="monitoring-services"></a>Serviços de monitoramento
Os aplicativos em nuvem são complexos com muitas partes móveis. O monitoramento fornece tooensure de dados que seu aplicativo permaneça ativo e em execução em um estado íntegro. Ele também ajuda você toostave off problemas potenciais ou solucionar problemas após os. Além disso, você pode usar o monitoramento dados toogain aprofundamento sobre seu aplicativo. Esse conhecimento pode ajudá-lo a facilidade de manutenção ou de desempenho do aplicativo tooimprove, ou automatizar ações que normalmente exigiriam a intervenção manual.

### <a name="monitor-azure-resources"></a>Monitorar os recursos do Azure
[Monitor do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started) é serviço de plataforma Olá que fornece uma única fonte para monitorar os recursos do Azure. Monitor do Azure, você pode visualizar, consultar, encaminhar, arquivar e executar ações sobre métricas hello e logs vindos de recursos no Azure. Você pode trabalhar com esses dados usando a folha de portal de Monitor hello, [Cmdlets do PowerShell Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples), [CLI de plataforma cruzada](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples), ou [APIs de REST do Azure Monitor](https://msdn.microsoft.com/library/dn931943.aspx).

### <a name="enable-autoscale-with-azure-monitor"></a>Habilitar o Dimensionamento Automático com o Azure Monitor
Habilitar [Azure Monitor AutoEscala](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-autoscale-get-started) aplica-se apenas conjuntos de escala de máquina toovirtual (VMSS), os serviços de nuvem, planos de serviço de aplicativo e ambientes de serviço de aplicativo.

### <a name="manage-roles-permissions-and-security"></a>Gerencie permissões e segurança de funções
Muitas equipes necessário toostrictly [regular o acesso toomonitoring](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-roles-permissions-security) dados e configurações. Por exemplo, se você tem os membros da equipe que trabalham exclusivamente no monitoramento (engenheiros de suporte, os engenheiros de devops) ou se você usar um provedor de serviço gerenciado, convém toogrant tooonly dados de monitoramento e restrinja sua capacidade toocreate a eles acesso, modificar, ou Exclua recursos.

Isso mostra como tooquickly aplicar um monitoramento RBAC função tooa usuário internas no Azure ou criar sua própria função personalizada para um usuário que precisa de permissões limitadas de monitoramentos. Também discute considerações de segurança para os recursos relacionados ao Monitor do Azure e como você pode limitar o acesso toohello dados que eles contêm.

## <a name="prevent-detect-and-respond-toothreats"></a>Evitar, detectar e responder toothreats
Detecção de ameaças de segurança central funciona automaticamente Coletando informações de segurança de recursos do Azure, rede hello e soluções de parceiros conectado. Ele analisa essas informações, geralmente correlacionando informações de várias fontes, tooidentify ameaças. Alertas de segurança são priorizados na Central de segurança, juntamente com recomendações sobre como tooremediate Olá ameaça.

-   [Configure uma política de segurança](https://docs.microsoft.com/azure/security-center/security-center-policies) para sua assinatura do Azure.
-   Saudação de uso [recomendações na Central de segurança](https://docs.microsoft.com/azure/security-center/security-center-recommendations) toohelp proteger seus recursos do Azure.
-   Confira e gerencie os [alertas de segurança](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) atuais.

[Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) Olá de ajuda a evitar, detectar e responder toothreats maior visibilidade e controle sobre a segurança de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

Central de segurança oferece recursos de prevenção, detecção e resposta que são criados no tooAzure de ameaça eficiente e fácil de usar. Os principais recursos são:

-   Entenda o estado da segurança na nuvem
-   Controle a segurança da nuvem
-   Implante facilmente soluções de segurança em nuvem integradas
-   Detecte ameaças e responda rapidamente

### <a name="understand-cloud-security-state"></a>Entenda o estado da segurança na nuvem
Central de segurança do Azure Use tooget uma visão central do estado de segurança de saudação de todos os recursos do Azure. Em um relance, verificar se os controles de segurança apropriados Olá estão em vigor e configurado corretamente e identificam rapidamente todos os recursos, que exigem atenção.

### <a name="take-control-of-cloud-security"></a>Controle a segurança da nuvem
Definir [políticas de segurança](https://docs.microsoft.com/azure/security-center/security-center-policies) para sua empresa tooyour de acordo com as assinaturas do Azure da segurança de nuvem precisa, adaptado toohello tipo de aplicativos ou confidencialidade dos dados de saudação em cada assinatura. Use proprietários de recursos recomendações orientado por política tooguide pelo processo de saudação de implementação de controles necessários — eliminam suposições Olá sem segurança na nuvem.

### <a name="easily-deploy-integrated-cloud-security-solutions"></a>Implante facilmente soluções de segurança em nuvem integradas
[Habilite soluções de segurança](https://docs.microsoft.com/azure/security-center/security-center-partner-integration) da Microsoft e de parceiros, incluindo firewalls e antimalwares líderes da indústria. Use simplificada soluções de segurança toodeploy provisionamento, alterações de redes ainda estão configuradas para você. Seus eventos de segurança de soluções de parceiros são coletados automaticamente para análise e alerta.

### <a name="detect-threats-and-respond-fast"></a>Detecte ameaças e responda rapidamente
Esteja sempre preparado para enfrentar as ameaças em nuvem atuais e emergentes com uma abordagem integrada e baseada em análise. Ao combinar a experiência e a [inteligência global](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities) de ameaças da Microsoft com informações sobre eventos relacionados à segurança da nuvem em suas implantações do Azure, a Central de Segurança ajuda a detectar ameaças reais de maneira precoce e a reduzir os falsos positivos. Alertas de segurança de nuvem fornecer ideias sobre a campanha de ataque hello, incluindo eventos relacionados e os recursos afetados e sugerem maneiras tooremediate problemas e recuperar rapidamente.

## <a name="end-to-end-scenario-based-network-monitoring"></a>Monitoramento de rede baseado em cenário de ponta a ponta
Os clientes criam uma rede de ponta a ponta no Azure administrando e compondo vários recursos de rede individuais, como VNet, ExpressRoute, Gateway de Aplicativo, Balanceadores de carga e mais. Monitoramento está disponível em cada um dos recursos de rede hello.

[Inspetor de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) é um serviço regional que permite que você toomonitor e diagnosticar as condições em um nível do cenário de rede no e do Azure. Diagnóstico de rede e as ferramentas de visualização disponíveis com o observador de rede ajudarão-lo a entender, diagnosticar e obter a rede de tooyour insights no Azure.

### <a name="automate-remote-network-monitoring-with-packet-capture"></a>Automatizar o monitoramento remoto de rede com a captura de pacote
Monitorar e diagnosticar problemas de rede sem efetuar login no tooyour (máquinas virtuais) usando o observador de rede. Gatilho [captura de pacote](https://docs.microsoft.com/azure/network-watcher/network-watcher-alert-triggered-packet-capture) por configuração de alertas e obter informações de desempenho tooreal de acesso no nível de pacote de saudação. Ao ver um problema, você poderá investigar os detalhes para um diagnóstico melhor.

### <a name="gain-insight-into-your-network-traffic-using-flow-logs"></a>Obtenha informações sobre seu tráfego de rede usando os logs de fluxo
Criar um entendimento aprofundado sobre o padrão de tráfego de sua rede, usando os [logs de fluxo do Grupo de Segurança de Rede](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview). As informações fornecidas pelos logs de fluxo ajudam a reunir dados para conformidade, auditoria e monitoramento do seu perfil de segurança de rede.

### <a name="diagnose-vpn-connectivity-issues"></a>Diagnosticar problemas de conectividade de VPN
Observador de rede fornece a você Olá capacidade muito[diagnosticar os problemas mais comuns do Gateway de VPN e conexões](https://docs.microsoft.com/azure/network-watcher/network-watcher-diagnose-on-premises-connectivity). Permitindo que você não só tooidentify Olá problema, mas também toouse Olá detalhadas logs investigar ainda mais toohelp criado.

toolearn mais informações sobre como tooconfigure observador de rede e como tooenable, leia o artigo de saudação [configurar observador de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="secure-deployment-using-proven-devops-tools"></a>Implantação segura usando ferramentas do DevOps comprovadas
Estes são alguns dos Olá lista do Azure DevOps práticas recomendadas neste espaço Microsoft Cloud, que faz com que as empresas e equipes produtiva e mais eficiente.

-   **Infraestrutura como código (IaC):** infraestrutura como código é um conjunto de técnicas e práticas recomendadas, o que ajudam os profissionais de TI remover carga Olá associada ao gerenciamento da infraestrutura modular e compilação do hello dia tooday. Ele permite que os profissionais de TI toobuild e manter seu ambiente de servidor modernos de maneira semelhante a como os desenvolvedores de software, criar e mantêm o código do aplicativo. Para o Azure, temos [do Azure Resource Manager]( https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) permite que você tooprovision seus aplicativos usando um modelo declarativo. Em um modelo único, você pode implantar vários serviços, juntamente com suas dependências. Use Olá toorepeatedly do mesmo modelo implantar seu aplicativo durante cada estágio do ciclo de vida do aplicativo hello.
-   **Implantação e integração contínua:** você pode configurar seus projetos de equipe Visual Studio Online muito[criar e implantar automaticamente](https://www.visualstudio.com/docs/build/overview) tooAzure aplicativos web ou serviços de nuvem. VSO implanta automaticamente binários Olá depois de fazer uma compilação tooAzure após cada check-in do código. Olá processo de compilação do pacote descrito aqui é equivalente toohello comando de pacote no Visual Studio, e Olá publicação toohello equivalente comando de publicar no Visual Studio.
-   **Gerenciamento de liberações:** Visual Studio [Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview) é uma ótima solução para automatizar a implantação de vários estágio e gerenciando Olá liberar o processo. Crie implantação contínua gerenciado pipelines toorelease rapidamente, facilmente e com frequência. Com o Release Management, podemos automatizar grande parte do nosso processo de lançamento e ter fluxos de trabalho de aprovação predefinidos. Implantar no local e toohello de nuvem, estender e personalizar conforme necessário.
-   **Monitoramento de desempenho do aplicativo:** detecte e resolva problemas e melhore continuamente seus aplicativos. Diagnostique problemas rapidamente em seu aplicativo em tempo real. Entenda o que os usuários fazem com ele. A configuração é fácil questão de adicionar código JS e uma entrada de webconfig, e você verá resultados em minutos no portal de saudação com todos os detalhes de saudação. [Ideias de aplicativo](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/) ajuda as empresas para detecção mais rápida de problemas e correção.
-   **Carregar teste & AutoEscala:** pode encontrar problemas de desempenho em nossa qualidade de implantação do aplicativo tooimprove e toomake que nosso aplicativo esteja sempre disponível ou se toocater toohello necessidades dos negócios. Verifique se seu aplicativo pode lidar com o tráfego da sua próxima campanha de marketing ou de seu próximo lançamento. Inicie a execução de [testes de carga](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing) baseados em nuvem sem demora com o Visual Studio Online.

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre [Segurança Operacional Azure](https://docs.microsoft.com/azure/security/azure-operational-security).
- tooLearn mais [Operations Management Suite | Segurança e conformidade](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Introdução à solução de Segurança e Auditoria do Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started).
