---
title: "aaaAzure a detecção de ameaças avançadas | Microsoft Docs"
description: "Saiba mais sobre a Proteção de Identidade e seus recursos."
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
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a>Detecção Avançada de Ameaças do Azure
## <a name="introduction"></a>Introdução

### <a name="overview"></a>Visão geral

A Microsoft desenvolveu uma série de White Papers, visões gerais de segurança, as práticas recomendadas e listas de verificação tooassist Azure clientes sobre Olá vários recursos relacionados à segurança disponíveis no e ao redor hello plataforma Azure. Olá tópicos variam em termos de amplitude e profundidade e são atualizadas periodicamente. Este documento é parte da série, como resumido Olá abstrata seção a seguir.

### <a name="azure-platform"></a>Plataforma Azure

O Azure é uma plataforma de serviço de nuvem pública que dá suporte à saudação a seleção mais ampla de sistemas operacionais, linguagens de programação, estruturas, ferramentas, bancos de dados e dispositivos.
Ele dá suporte a saudação linguagens de programação a seguir:
-   Execute contêineres do Linux com a integração com o Docker.
-   Criar aplicativos com JavaScript, Python, .NET, PHP, Java e Node.js
-   Crie back-ends para dispositivos iOS, Android e Windows.

Serviços de nuvem pública do Azure oferecem suporte a saudação tecnologias mesmo milhões de desenvolvedores e profissionais de TI já contam e confiarem.

Quando você estiver migrando tooa de nuvem pública com uma organização, essa organização é responsável tooprotect seus dados e fornecer segurança e controle de sistema de saudação.

Infraestrutura do Azure foi projetada de saudação recurso tooapplications para hospedagem milhões de clientes simultaneamente, e fornece uma base confiável em que as empresas podem atender às suas necessidades de segurança. O Azure fornece uma ampla gama de opções tooconfigure e personalizar segurança toomeet Olá requisitos das implantações de aplicativo. Este documento ajuda você a atender a esses requisitos.

### <a name="abstract"></a>Resumo

O Microsoft Azure oferece a funcionalidade de detecção avançada de ameaças interna por meio de serviços como o Azure Active Directory, Azure Operations Management Suite (OMS) e a Central de Segurança do Azure. Esta coleção de recursos e serviços de segurança fornece uma maneira simples e rápida toounderstand o que está acontecendo em suas implantações do Azure.

Este white paper orientará você hello "abordagens do Microsoft Azure" para diagnóstico de vulnerabilidade de ameaça e avaliando os riscos de saudação associados com atividades mal-intencionadas hello, direcionadas em servidores e outros recursos do Azure. Isso ajuda a métodos de saudação tooidentify de identificação e gerenciamento de vulnerabilidade com otimização de soluções Olá plataforma Windows Azure e serviços de segurança do cliente e tecnologias.

Este white paper concentra-se na tecnologia de saudação da plataforma Windows Azure e controles de atendimento e não tenta tooaddress SLAs, modelos e considerações de práticas recomendadas de DevOps de preços.

## <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

![Azure Active Directory Identity Protection](./media/azure-threat-detection/azure-threat-detection-fig1.png)


[Proteção contra identidade Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) é um recurso do hello [do Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) edition que fornece uma visão geral dos eventos de risco hello e possíveis vulnerabilidades que afetam sua organização identidades. Microsoft tem protegendo identidades baseado em nuvem para mais de uma década, e com o Azure AD Identity Protection, a Microsoft está fazendo esses mesmos sistemas de proteção disponível tooenterprise clientes. O Identity Protection usa os recursos de detecção de anomalias existentes do Azure AD (disponíveis por meio dos [Relatórios de Atividade Anômala do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports)) e apresenta novos tipos de evento de risco que pode detectar anomalias em tempo real.

Proteção de identidade usa algoritmos de aprendizado de máquina adaptável e anomalias de toodetect heurística e eventos de risco que podem indicar que uma identidade tiver sido comprometida. Usando esses dados, proteção de identidade gera relatórios e alertas que permitem que você tooinvestigate esses eventos de risco e tomar as devidas providências de solução ou de minimização.

Contudo, o Azure Active Directory Identity Protection é mais do que apenas uma ferramenta de monitoramento e criação de relatórios. Com base em eventos de risco, proteção de identidade calcula um nível de risco do usuário para cada usuário, permitindo que você tooconfigure risco políticas tooautomatically proteger Olá identidades da sua organização.

Essas políticas com base em risco em adição tooother [controles de acesso condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) fornecidos pelo Active Directory do Azure e [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), automaticamente pode bloquear ou oferecer ações de correção adaptável que incluem redefinições de senha e a imposição de autenticação multifator.

### <a name="identity-protections-capabilities"></a>Recursos do Identity Protection

O Azure Active Directory Identity Protection é mais do que apenas uma ferramenta de monitoramento e criação de relatórios. tooprotect identidades da sua organização, você pode configurar políticas baseadas em risco que respondem automaticamente toodetected problemas quando um nível de risco especificado for atingido. Essas políticas, além de tooother condicional acessar controles fornecidos pelo Active Directory do Azure e o EMS, pode bloquear automaticamente ou iniciar ações de correção adaptável, inclusive redefinições de senha e a imposição de autenticação multifator.

Exemplos de algumas maneiras de saudação proteção de identidade do Azure pode ajudar a proteger suas contas e identidades incluem:

[Detecção de eventos de risco e contas arriscadas:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   Detecção de seis tipos de evento de risco usando regras de aprendizado de máquina e heurística
-   Calcular os níveis de risco do usuário
-   Fornecendo recomendações personalizadas tooimprove postura de segurança geral, realçando vulnerabilidades

[Investigação dos eventos de risco:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   Enviar notificações para eventos de risco
-   Investigar os eventos de risco usando informações relevantes e contextuais
-   Fornecendo tootrack investigações de fluxos de trabalho básicos
-   Fornecer acesso fácil tooremediation ações, como a redefinição de senha

[Políticas de acesso condicional baseadas em risco:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   Diretiva toomitigate arriscadas entradas bloqueando entradas ou a necessidade de desafios de autenticação multifator.
-   Diretiva tooblock ou contas de usuário de arriscados segura
-   Diretiva toorequire usuários tooregister para autenticação multifator

### <a name="azure-ad-privileged-identity-management-pim"></a>Azure AD Privileged Identity Management (PIM)

Com o [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure),

![Gerenciamento de identidades com privilégios do AD do Azure](./media/azure-threat-detection/azure-threat-detection-fig2.png)

Você pode gerenciar, controlar e monitorar o acesso em sua organização. Isso inclui tooresources de acesso no AD do Azure e outros Microsoft online services como Office 365 ou Microsoft Intune.

O Azure AD Privileged Identity Management ajuda você a:

-   Obter um alerta e relatar os administradores do AD do Azure e tooMicrosoft "just in time" acesso administrativo a serviços Online como o Office 365 e Intune

-   Obter relatórios sobre o histórico de acesso de administrador e as alterações nas atribuições de administrador

-   Receber alertas sobre a função de tooa de acesso privilegiado

## <a name="microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS)

O [Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem. Como o OMS é implementado como um serviço baseado em nuvem, é possível colocá-lo em funcionamento com investimentos mínimos em serviços de infraestrutura. Os novos recursos são entregues automaticamente, evitando os custos contínuos com manutenção e atualização.

Além disso tooproviding de serviços importantes no seu próprio, OMS pode integrar com componentes do System Center, como [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend os investimentos existentes de gerenciamento de segurança para Olá na nuvem. System Center e o OMS podem trabalhar juntos tooprovide experiência um gerenciamento híbrido completa.

### <a name="holistic-security-and-compliance-posture"></a>Postura de conformidade e segurança holística

Olá [painel OMS segurança e auditoria](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) fornece uma visão abrangente da sua organização postura de segurança de TI com consultas de pesquisa interna para problemas importantes que exigem sua atenção. o painel de segurança e auditoria Olá é a tela inicial Olá para tudo relacionado toosecurity no OMS. Ele fornece informações de alto nível em estado de segurança de saudação de seus computadores. Ele também inclui Olá capacidade tooview todos os eventos de saudação nas últimas 24 horas, 7 dias, ou qualquer outro período de tempo personalizado.

Ajuda de painéis do OMS você entender rapidamente e facilmente Olá postura geral de segurança de qualquer ambiente, tudo no contexto de saudação de operações de TI, incluindo: avaliação de atualização de software, avaliação de antimalware e linhas de base de configuração. Além disso, os dados do log de segurança são prontamente acessados toostreamline Olá segurança e conformidade de processos de auditoria.

painel do OMS segurança e auditoria Olá é organizada em quatro categorias principais:

![Painel Segurança e Auditoria do OMS](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   **Domínios de segurança:** nessa área, você será capaz de toofurther explorar registros de segurança ao longo do tempo, acessar avaliação de malware, atualize a avaliação, segurança de rede, informações de identidade e acesso, computadores com eventos de segurança e ter rapidamente Painel de Central de segurança do acesso tooAzure.

-   **Problemas importantes:** essa opção permite que você tooquickly identificar Olá número de problemas ativos e Olá severidade desses problemas.

-   **Detecções (visualização):** permite padrões de ataque tooidentify visualizando alertas de segurança conforme eles ocorrem em relação a seus recursos.

-   **Inteligência de ameaça:** permite padrões de ataque tooidentify pelo número total de saudação de servidores com saída tráfego IP mal-intencionado, Olá mal-intencionado tipo de ameaça e um mapa que mostra onde esses IPs são provenientes de visualização.

-   **Consultas comuns de segurança:** essa opção fornece uma lista de segurança mais comuns de saudação consultas que você pode usar toomonitor seu ambiente. Quando você clicar em uma das consultas, ele abre a folha de pesquisa de saudação com resultados de saudação para essa consulta.

### <a name="insight-and-analytics"></a>Insight and Analytics
No Centro de saudação do [análise de Log](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) é o repositório do OMS hello, que está hospedado no hello nuvem do Azure.

![Insight and Analytics](./media/azure-threat-detection/azure-threat-detection-fig4.png)

Dados são coletados no repositório de saudação de fontes conectadas por configurar fontes de dados e Adicionar assinatura tooyour de soluções.

![subscription](./media/azure-threat-detection/azure-threat-detection-fig5.png)

Soluções e fontes de dados irá criar diferentes tipos de registro que têm seu próprio conjunto de propriedades, mas ainda podem ser analisados no repositório de toohello de consultas. Isso permite que você toouse Olá mesmo toowork de ferramentas e os métodos com diferentes tipos de dados coletado por fontes diferentes.


A maioria da interação com a análise de Log é por meio do portal do OMS hello, que é executado em qualquer navegador e fornece acesso tooconfiguration configurações e várias ferramentas tooanalyze e agir sobre dados coletados. No portal de saudação, você pode usar [pesquisas de log](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) onde você pode criar consultas tooanalyze coletado dados, [painéis](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), que pode ser personalizada com exibições gráficas de pesquisas mais valiosas e [soluções](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), que fornece ferramentas adicionais de análise e funcionalidade.

![ferramentas de análise](./media/azure-threat-detection/azure-threat-detection-fig6.png)

As soluções adicionam funcionalidade tooLog análise. Eles principalmente executados na nuvem hello e fornecem a análise dos dados coletados no repositório do OMS hello. Eles também podem definir novos toobe de tipos de registro coletado que pode ser analisado com pesquisas de Log ou pela interface de usuário adicionais fornecidos pela solução de saudação no painel do OMS hello.
Olá, segurança e auditoria é um exemplo desses tipos de soluções.



### <a name="automation--control-alert-on-security-configuration-drifts"></a>Automação e Controle: alerta de dessincronização de configuração de segurança

Automação do Azure automatiza processos administrativos com runbooks que se baseiam no PowerShell e executar em Olá nuvem do Azure. Runbooks também podem ser executados em um servidor de recursos de local de toomanage seu local de data center. A Automação do Azure fornece o gerenciamento de configuração com o DSC (Desired State Configuration) do PowerShell.

![Automação do Azure](./media/azure-threat-detection/azure-threat-detection-fig7.png)

Você pode criar e gerenciar recursos de DSC hospedados no Azure e aplicá-las no local e toocloud toodefine de sistemas e automaticamente impor sua configuração ou obter relatórios em caso de descompasso toohelp garantir que as configurações de segurança permaneçam em política.

## <a name="azure-security-center"></a>Central de Segurança do Azure

A Central de Segurança do Azure ajuda a proteger os recursos do Azure. Ela fornece monitoramento de segurança integrado e gerenciamento de políticas em suas assinaturas do Azure. No serviço de saudação, você é capaz de toodefine políticas não apenas em relação a suas assinaturas do Azure, mas também em [grupos de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal), portanto, pode ser mais granular.

![Central de Segurança do Azure](./media/azure-threat-detection/azure-threat-detection-fig8.png)

Pesquisadores de segurança da Microsoft estão constantemente em bloqueio de saudação para ameaças. Eles têm acesso tooan extenso conjunto de telemetria obtida com a presença global da Microsoft na nuvem hello e local. Esta coleção profundos e diversas de conjuntos de dados permite que a Microsoft toodiscover novo ataque padrões e tendências em seus produtos de consumidor e empresariais no local, bem como os serviços online.

Dessa forma, a Central de Segurança pode atualizar rapidamente seus algoritmos de detecção conforme os invasores lançam explorações novas e cada vez mais sofisticadas. Isso ajuda a acompanhar o ritmo de um ambiente de ameaças que muda rapidamente.

![Central de Segurança](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

Detecção de ameaças de segurança central funciona automaticamente Coletando informações de segurança de seus recursos do Azure, rede hello e soluções de parceiros conectado.  Ele analisa essas informações, correlacionando informações de várias fontes, tooidentify ameaças.
Alertas de segurança são priorizados na Central de segurança, juntamente com recomendações sobre como tooremediate Olá ameaça.

A Central de Segurança emprega análise de segurança avançada, que vai além das abordagens baseadas em assinatura. Soluções de dados grandes e [aprendizado de máquina](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) tecnologias são eventos tooevaluate usado pela estrutura de nuvem inteira hello – detecção de ameaças que seriam impossível tooidentify usando abordagens manuais e prevendo Olá evolução de ataques. Essas análises de segurança inclui o seguinte hello.

### <a name="threat-intelligence"></a>Inteligência contra ameaças

A Microsoft tem uma grande quantidade de inteligência contra ameaças globais.
Fluxo de telemetria em de várias fontes, como Azure, Office 365, Microsoft CRM online, o Microsoft Dynamics AX, outlook.com, MSN.com, Olá Microsoft Digital Crimes unidade (DCU) e Microsoft Security Response Center (MSRC).

![Inteligência contra ameaças](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

Os pesquisadores também recebem informações de inteligência de ameaça que são compartilhadas entre os provedores de serviços de nuvem principal e assina toothreat intelligence feeds de terceiros. Central de segurança do Azure pode usar este tooalert informações você toothreats de atores de ruins conhecidos. Alguns exemplos incluem:

-   **Controlar Olá Power de aprendizado de máquina -** Central de segurança do Azure tem acesso tooa grande quantidade de dados sobre a atividade de rede de nuvem, que pode ser usado toodetect ameaças direcionando as implantações do Azure. Por exemplo:

-   **Detecções de força bruta -** é toocreate usado um padrão de histórico de tentativas de acesso remoto, que permite que ele toodetect ataques de força bruta contra as portas SQL, RDP e SSH de aprendizado de máquina.

-   **Saída DDoS e detecção de Botnet** -um objetivo comum de ataques direcionados a recursos de nuvem é a capacidade de computação Olá toouse de tooexecute esses recursos outros ataques.

-   **Novos servidores de análise comportamental e VMs -** depois que um servidor ou máquina virtual estiver comprometida, os invasores empregam uma ampla variedade de técnicas tooexecute mal-intencionados no sistema ao evitar detecção, garantindo a persistência e pelo que não controles de segurança.

-   **Detecção de ameaças de banco de dados SQL do Azure -** tooaccess ou exploração bancos de dados de tentativas de detecção de ameaças para o banco de dados SQL, que identifica as atividades anômalas de banco de dados indicando incomuns e potencialmente prejudiciais.

### <a name="behavioral-analytics"></a>Análise comportamental

Análise de comportamento é uma técnica que analisa e compara tooa coleção de padrões conhecidos. No entanto, esses padrões não são assinaturas simples. Eles são determinados por meio de algoritmos de aprendizagem de máquina complexos que são aplicadas toomassive conjuntos de dados.

![Análise comportamental](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


Eles também são determinados pela análise cuidadosa de comportamentos mal-intencionados por analistas especialistas. Central de segurança do Azure podem usar recursos de tooidentify comprometido de análise de comportamento com base na análise de logs de máquina virtual, logs de dispositivo de rede virtual, logs de infraestrutura, despejos de memória e outras fontes.

Além disso, há correlação com outros toocheck de sinais para dar suporte a evidência de uma campanha generalizada. Essa correlação ajuda tooidentify eventos que são consistentes com estabelecida indicadores de comprometimento.

Alguns exemplos incluem:
-   **Execução do processo suspeita:** invasores empregam várias técnicas tooexecute mal-intencionados sem detecção. Por exemplo, um invasor pode dar malware Olá mesmos nomes de arquivos do sistema legítimo, mas coloque esses arquivos em um local alternativo, use um nome que é muito parecido com um arquivo benigno ou máscara Olá true extensão de. Monitores e comportamentos de processos de modelos de Central de segurança processam exceções de toodetect execuções como estes.

-   **Oculta as tentativas de malware e exploração:** malware sofisticado pode escapar produtos antimalware tradicional nunca gravar toodisk ou criptografar os componentes de software armazenados no disco. No entanto, esse tipo de malware pode ser detectado usando a análise de memória, como malware Olá deve deixar rastreamentos em toofunction de memória. Quando o software falha, um despejo de captura uma parte da memória em tempo de saudação de travamento hello. Analisando a memória Olá no despejo hello, Central de segurança do Azure pode detectar técnicas usadas tooexploit vulnerabilidades no software, acessar dados confidenciais e clandestinamente persistir em um computador comprometido, sem afetar o desempenho de saudação do seu computador.

-   **Lateral movimentação e reconhecimento interno:** toopersist em um comprometido rede e localizar/coleta dados valioso, os invasores muitas vezes tentam toomove lateralmente da saudação comprometida tooothers máquina dentro Olá a mesma rede. Central de segurança monitora o processo e tentativas de logon atividades toodiscover tooexpand destaque de um invasor em rede hello, como a execução do comando remoto, rede de investigação e enumeração de conta.

-   **Scripts do PowerShell mal-intencionados:** PowerShell pode ser usado por invasores tooexecute mal-intencionados em máquinas virtuais de destino para fins de vários. A Central de Segurança inspeciona a atividade do PowerShell para obter evidência de atividades suspeitas.

-   **Ataques de saída:** os invasores geralmente recursos de nuvem com objetivo hello usando esses ataques adicionais de toomount de recursos de destino. Máquinas virtuais comprometidas, por exemplo, pode ser usado toolaunch ataques de força bruta em relação a outras máquinas virtuais, enviar SPAM ou verificação de portas abertas e outros dispositivos na Internet de saudação. Aplicando máquina toonetwork tráfego de aprendizado, Central de segurança pode detectar quando as comunicações de rede de saída excederem norma hello. Quando enviar SPAM, Central de segurança também correlaciona tráfego incomuns de email com inteligência do Office 365 toodetermine se mensagens de saudação provavelmente mal-intencionado ou Olá resultado de uma campanha de email legítimo.

### <a name="anomaly-detection"></a>Detecção de anomalias

Central de segurança do Azure também usa as ameaças tooidentify de detecção de anomalias. Análise de toobehavioral contraste (o que depende de padrões conhecidos derivados de grandes conjuntos de dados), detecção de anomalias mais "personalizada" e concentra-se nas linhas de base são implantações tooyour específico. Aprendizado de máquina toodetermine aplicada a atividade normal para implantações e, em seguida, regras de condições de exceções de toodefine gerado que podem representar um evento de segurança. Aqui está um exemplo:

-   **Ataques de força bruta vindos de RDP/SSH**: suas implantações podem ter máquinas virtuais ocupadas com uma grande quantidade diária de logons e outras máquinas virtuais que têm poucos ou nenhum logon. Central de segurança do Azure pode determinar a atividade de logon de linha de base para as máquinas virtuais e usar toodefine de aprendizado de máquina em torno de atividades de logon normal hello. Se houver qualquer discrepância com linha de base de saudação definida para relacionadas ao logon características, em seguida, pode ser gerado um alerta. Novamente, o aprendizado de máquina determina o que é relevante.

### <a name="continuous-threat-intelligence-monitoring"></a>Monitoramento Contínuo de Inteligência contra Ameaças

Central de segurança do Azure funciona com segurança dados ciência equipes de pesquisa e em toda Olá, mundo que monitoram continuamente as alterações no cenário de ameaças hello. Isso inclui Olá iniciativas a seguir:

-   **Monitoramento de inteligência contra ameaças**: a inteligência contra ameaças inclui mecanismos, indicadores, implicações e conselhos acionáveis sobre ameaças iminentes ou existentes. Essas informações são compartilhadas na comunidade de segurança hello e Microsoft monitora continuamente os feeds de inteligência de ameaça de fontes internas e externas.

-   **Compartilhamento de sinal**: ideias de equipes de segurança de todo o amplo portfólio da Microsoft de serviços locais e de nuvem, servidores e dispositivos de ponto de extremidade cliente são compartilhadas e analisadas.

-   **Especialistas de segurança da Microsoft**: comprometimento contínuo com as equipes da Microsoft que trabalham em campos de segurança especializada, como computação forense e detecção de ataque à Web.

-   **Detecção de ajuste:** algoritmos são executados em conjuntos de dados de clientes reais e pesquisadores de segurança de trabalhar com os resultados de saudação do toovalidate de clientes. Verdadeiros e falsos positivos são algoritmos de aprendizado de máquina toorefine usado.

Esses esforços combinados culminar detecções novos e aprimorados, que você pode se beneficiar de instantaneamente – não há nenhuma ação para você tootake.

## <a name="advanced-threat-detection-features---other-azure-services"></a>Recursos de Detecção Avançada de Ameaças – Outros Serviços do Azure

### <a name="virtual-machine-microsoft-antimalware"></a>Máquina Virtual: Antimalware da Microsoft

[O Antimalware da Microsoft](https://docs.microsoft.com/azure/security/azure-security-antimalware) Azure é uma solução de agente único para aplicativos e ambientes de locatário, projetado toorun no plano de fundo de saudação sem intervenção humana. Você pode implantar proteção com base nas necessidades de saudação de suas cargas de trabalho do aplicativo, com o básico seguro por padrão ou avançadas de configuração personalizada, incluindo o monitoramento de antimalware. Antimalware do Azure é uma opção de segurança para máquinas virtuais do Azure e é instalado automaticamente em todas as máquinas virtuais de PaaS do Azure.

**Recursos do Azure toodeploy e habilitar o Antimalware da Microsoft para seus aplicativos**

#### <a name="microsoft-antimalware-core-features"></a>Recursos básicos de Antimalware da Microsoft

-   **Proteção em tempo real -** monitora a atividade em serviços de nuvem e em máquinas virtuais toodetect e bloquear a execução de malware.

-   **Varredura - programada** executa periodicamente destino varredura toodetect tipos de malware, inclusive ativamente programas em execução.

-   **Remediação de Malware -** atua automaticamente sobre o malware detectado, por exemplo, excluindo ou colocando arquivos mal-intencionados em quarentena e limpando entradas de Registro mal-intencionadas.

-   **Atualizações de assinatura -** automaticamente instala hello mais recente assinaturas (definições de vírus) tooensure proteção está atualizada em uma frequência predeterminada.

-   **Atualizações de mecanismo antimalware -** automaticamente atualizações Olá mecanismo Antimalware da Microsoft.

-   **Atualizações de plataforma de antimalware –** automaticamente atualizações Olá plataforma Antimalware da Microsoft.

-   **Proteção ativa -** relata telemetria metadados sobre ameaças detectadas e recursos suspeitas tooMicrosoft tooensure Azure resposta rápida toohello e em evolução panorama de ameaças, permitindo a entrega de assinatura síncrona em tempo real por meio de Olá Microsoft Active Protection System (MAPS).

-   **Exemplos de relatórios -** fornece e exemplos de relatórios toohelp de serviço de Antimalware da Microsoft toohello refinar serviço hello e solução de problemas de ativação.

-   **Exclusões –** permite que aplicativos e tooconfigure de administradores de serviço certos arquivos, processos e unidades tooexclude da proteção e verificação de desempenho e/ou outros motivos.

-   **Coleta de eventos de antimalware -** registra a integridade do serviço antimalware hello, atividades suspeitas e ações de correção realizadas no log de eventos do sistema operacional hello e coleta-los na conta de armazenamento do Azure do cliente hello.

### <a name="azure-sql-database-threat-detection"></a>Detecção de Ameaças do Banco de Dados SQL do Azure

[Detecção de ameaças do banco de dados SQL do Azure](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) é um novo recurso de inteligência de segurança incorporado Olá serviço do Azure SQL Database. Contornar Olá toolearn, perfil de relógio e detectar atividades anormais de banco de dados, a detecção de ameaças de banco de dados SQL do Azure identifica o banco de dados de toohello ameaças potenciais.

Os agentes de segurança ou outros administradores designados podem obter uma notificação imediata sobre atividades suspeitas de banco de dados conforme eles ocorrem. Cada notificação fornece detalhes de atividade suspeita hello e recomenda como toofurther investigar e reduzir a ameaça de saudação.

Atualmente, a detecção de ameaças de banco de dados SQL do Azure detecta possíveis vulnerabilidades e ataques de injeção de SQL e padrões de acesso do banco de dados anormais.

Ao receber a notificação de email de detecção de ameaças, os usuários são capaz de toonavigate e exibição Olá relevantes registros de auditoria usando o link profundo do hello em mensagens de saudação que abre um visualizador de auditoria e/ou pré-configurado auditoria modelo do Excel que mostra a auditoria relevantes Olá registros de tempo de saudação do evento de suspeita Olá toohello a seguir de acordo com:
-   Armazenamento de auditoria de servidor/banco de dados de saudação com atividades do hello anormal do banco de dados

-   Tabela de armazenamento de auditoria relevantes que foi usada em tempo de Olá Olá toowrite auditoria do log de eventos

-   Registros de hello hora a seguir porque ocorre o evento de saudação de auditoria.

-   Registros de auditoria com a ID de evento semelhantes no tempo de saudação do evento de saudação (opcional para alguns detectores)

Detectores de ameaça do banco de dados SQL use um dos Olá metodologias de detecção a seguir:

-   **Detecção determinística –** detectar padrões suspeitos (com base em regras) em consultas de cliente do SQL Olá que correspondem a ataques conhecidos. Essa metodologia tem detecção alta e baixa de falsos positivos, porém limitadas cobertura porque ele está em categoria de saudação de "atômicas detecções".

-   **Detecção de behavioural –** defeitos de atividade anormal, que é um comportamento anormal do banco de dados de saudação que não foi detectado durante a saudação últimos 30 dias.  Um exemplo de atividade anormal do cliente SQL pode ser um pico de logons com falha/consultas, alto volume de dados que estão sendo extraídos, consultas canônicas incomuns e IP endereços usados tooaccess Olá banco de dados desconhecido

### <a name="application-gateway-web-application-firewall"></a>Firewall do Aplicativo Web do Gateway de Aplicativo

[Firewall do aplicativo de Web](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) é um recurso do [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) que fornece proteção tooweb aplicativos que usam o gateway de aplicativo padrão [decontroledeentregadeaplicativos](https://kemptechnologies.com/in/application-delivery-controllers) funções. Firewall do aplicativo Web faz isso, protegendo-os contra a maioria das Olá [OWASP top 10 vulnerabilidades comuns da web](https://www.owasp.org/index.php/Top_10_2010-Main)

![Firewall do Aplicativo Web do Gateway de Aplicativo](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   Proteção contra injeção de SQL

-   Proteção contra scripts entre sites

-   Proteção Contra Ataques Comuns da Web, como a injeção de comandos, as solicitações HTTP indesejadas, a divisão de resposta HTTP e o ataque de inclusão de arquivo remoto

-   Proteção contra violações de protocolo HTTP

-   Proteção contra anomalias de protocolo HTTP, como ausência de host de agente do usuário e de cabeçalhos de aceitação

-   Prevenção contra bots, rastreadores e scanners

-   Detecção de problemas de configuração de aplicativo comuns (ou seja, Apache, IIS etc.)

Configurar WAF no Application Gateway fornece Olá benefício tooyou a seguir:

-   Proteger seu aplicativo da web contra ataques sem código de toobackend de modificação e vulnerabilidades de web.

-   Proteger web vários aplicativos em Olá a mesma hora atrás de um application gateway. Gateway de aplicativo oferece suporte a hospedagem de sites too20 atrás de um único gateway que pode ser protegido contra ataques de web.

-   Monitore seu aplicativo Web contra ataques usando o relatório em tempo real gerado pelos logs do WAF do gateway de aplicativo.

-   Alguns controles de conformidade exigem toobe de pontos de extremidade protegido por uma solução WAF todos os da internet. Usando o gateway de aplicativo com WAF habilitado, você pode atender a esses requisitos de conformidade.

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a>Detecção de Anomalias – uma API criada com o Azure Machine Learning

Detecção de anomalias é uma API criada com o Azure Machine Learning que é útil para detectar os diferentes tipos de padrões anômalos em seus dados de série temporal. Olá API atribui uma anomalia pontuação tooeach dados ponto na série de tempo de saudação, que pode ser usado para a geração de alertas, monitoramento por meio de painéis ou conectar-se com seus sistemas de emissão de tíquetes.

Olá [API de detecção de anomalias](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) pode detectar Olá seguintes tipos de anomalias nos dados de série temporal:

-   **Altos e baixos:** por exemplo, ao monitorar o número de saudação do serviço de tooa de falhas de logon ou número de check-outs em um site de comércio eletrônico, picos incomuns ou queda poderia indicar ataques de segurança ou interrupções de serviço.

-   **Tendências positivas e negativas:** ao monitorar o uso de memória em computação, por exemplo, reduzindo o tamanho de memória livre é uma indicação de um vazamento de memória potencial; quando o comprimento da fila do serviço de monitoramento, uma tendência de aumento persistente pode indicar um problema de software subjacente.

-   **As alterações e no intervalo dinâmico de valores de nível:** por exemplo, nível altera as latências de um serviço depois que um serviço de atualização ou diminuir níveis de exceções após a atualização pode ser toomonitor interessante.

aprendizado de máquina Olá com base em API que permite:

-   **Detecção robusta e flexível:** modelos de detecção de anomalias Olá permitir que os usuários tooconfigure configurações de sensibilidade e detectar anomalias entre conjuntos de dados não sazonais e sazonais. Os usuários podem ajustar menos Olá detecção modelo toomake Olá detecção de anomalias de API ou precisa de mais confidencial tootheir de acordo. Isso significa detectando Olá menos ou mais anomalias visíveis nos dados com e sem padrões sazonais.

-   **Detecção em tempo hábil e escalonável:** modo tradicional de saudação de monitoramento com presentes limites definidos por conhecimento do domínio dos especialistas são toomillions cara e não escalonável de alterar dinamicamente os conjuntos de dados. modelos de detecção de anomalias Olá nesta API são aprendidos e modelos são ajustados automaticamente de dados históricos e em tempo real.

-   **Detecção proativa e acionável:** a detecção de alteração de nível e de tendência lenta podem ser aplicadas para detecção de anomalias. sinais anormal antecipado Olá detectados podem ser usado toodirect pessoas tooinvestigate e agir em áreas de problema de saudação.  Além disso, os modelos de análise de causas básicas e as ferramentas de alertas podem ser desenvolvioas sobre esse serviço de API de detecção de anomalias.

detecção de anomalias Olá API é uma solução eficaz e eficiente para uma ampla variedade de cenários, como a integridade do serviço & KPI monitoramento, IoT, monitoramento de desempenho e monitoramento de tráfego de rede. Aqui estão alguns cenários comuns onde essa API pode ser útil:
- Os departamentos de TI precisam de eventos de tootrack de ferramentas, código de erro, o log de uso e desempenho (CPU, memória e assim por diante) de maneira oportuna.

-   Sites de comércio online deseja tootrack atividades do cliente, modos de exibição de página, cliques e assim por diante.

-   Utilitário empresas deseja tootrack consumo de água, gás, eletricidade e outros recursos.

-   Serviços de gerenciamento de recurso/construção deseja toomonitor temperatura, umidade, tráfego e assim por diante.

-   IoT/fabricantes deseja que os dados de sensor toouse no tempo série toomonitor o fluxo de trabalho, qualidade e assim por diante.

-   Provedores de serviços, como centros de chamada precisam de tendência de demanda de serviço toomonitor, volume de incidentes, aguarde comprimento da fila e assim por diante.

-   Grupos de análise de negócios deseja toomonitor business dos KPIs (como volume de vendas, opiniões de clientes, preços) anormal movimentação em tempo real.

### <a name="cloud-app-security"></a>Segurança de Aplicativo de Nuvem

[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) é um componente crítico da pilha do Microsoft Cloud Security hello. É uma solução abrangente que pode ajudar sua organização, como mover tootake proveito de promessa de saudação de aplicativos em nuvem, mas mantê-lo no controle, a visibilidade das atividades aprimorada. Ele também ajuda a aumentar a proteção de saudação de dados críticos em aplicativos de nuvem.

Com as ferramentas que ajudam a descobrir shadow IT, avaliar os riscos, impor políticas, investigar atividades e parar ameaças, sua organização pode mover com mais segurança toohello nuvem enquanto mantêm o controle de dados críticos.

<table style="width:100%">
 <tr>
   <td>Descobrir</td>
   <td>Descobrir a TI de sombra com o sombra IT com a Segurança de Aplicativo de Nuvem. Ganhe visibilidade, detectando aplicativos, atividades, usuários, dados e arquivos em seu ambiente de nuvem. Descobrir aplicativos de terceiros que estão conectados tooyour nuvem.</td>
 </tr>
 <tr>
   <td>Investigar</td>
   <td>Investigue seus aplicativos de nuvem usando ferramentas para análise forense nuvem toodeep-se aprofundar em aplicativos arriscados, usuários específicos e arquivos em sua rede. Localize padrões nos dados Olá coletados da nuvem. Gere relatórios toomonitor sua nuvem.</td>

 </tr>
 <tr>
   <td>Controle</td>
   <td>Reduzir o risco definindo políticas e alertas tooachieve máximo controle sobre o tráfego de rede de nuvem. Use o Cloud App Security toomigrate toosafe seus usuários, alternativas de aplicativo de nuvem sancionados.</td>

 </tr>
 <tr>
   <td>Proteger</td>
   <td>Use Cloud App Security toosanction ou impedir que os aplicativos, aplicar prevenção de perda de dados, as permissões de controle e de compartilhamento e gerar alertas e relatórios personalizados.</td>

 </tr>
 <tr>
   <td>Controle</td>
   <td>Reduzir o risco definindo políticas e alertas tooachieve máximo controle sobre o tráfego de rede de nuvem. Use o Cloud App Security toomigrate toosafe seus usuários, alternativas de aplicativo de nuvem sancionados.</td>

 </tr>
</table>


![Segurança de Aplicativo de Nuvem](./media/azure-threat-detection/azure-threat-detection-fig14.png)

A Segurança de Aplicativo de Nuvem integra a visibilidade com sua nuvem por

-   Usando o Cloud Discovery toomap e identificar seu ambiente de nuvem e Olá aplicativos de nuvem que sua organização está usando.


-   Sancionar e proibir aplicativos em sua nuvem.



-   Usando conectores de fácil de implantar aplicativos que aproveitam APIs, de provedor para visibilidade e controle dos aplicativos que você se conectar a.

-   Ajudando você a ter controle contínuo de configuração e ajustar continuamente, políticas.

Sobre a coleta de dados dessas fontes, o Cloud App Security executa uma análise sofisticada nos dados de saudação. Ele imediatamente alerta tooanomalous atividades e fornece visibilidade profunda sobre seu ambiente de nuvem. Você pode configurar uma política de segurança de aplicativo de nuvem e usá-lo tooprotect tudo no seu ambiente de nuvem.

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a>Recursos ATD de terceiros por meio do Azure Marketplace

### <a name="web-application-firewall"></a>Firewall do Aplicativo Web

Firewall de aplicativo Web inspeciona carregamentos de malware blocos injeções de SQL, script entre sites e o tráfego de entrada da web e aplicativo DDoS e outros ataques direcionados em seus aplicativos web. Ele também inspeciona respostas de saudação de servidores de web de back-end de Olá para prevenção de perda de dados (DLP). mecanismo de controle de acesso integrado Olá permite políticas de controle de acesso granular administradores toocreate para autenticação, autorização e contabilização (AAA), que fornece autenticação forte organizações e controle de usuário.

**Destaques:**
-   Detecta e bloqueia SQL injeções, scripts intersites, carregamentos de malware, DDoS de aplicativo ou quaisquer outros ataques contra seu aplicativo.

-   Autenticação e controle de acesso.

-   Verifica os dados confidenciais do tráfego de saída toodetect e pode mascarar ou bloquear Olá informações sendo vazados.

-   Acelera a entrega de saudação do conteúdo do aplicativo web, usando recursos como cache, a compactação e outras otimizações de tráfego.

A seguir é exemplos de firewalls de aplicativo da Web disponíveis no mercado do Azure:

[Firewall do aplicativo Web Barracuda, Brocade Virtual Firewall do aplicativo Web (Brocade vWAF), Imperva SecureSphere & Olá ThreatSTOP IP Firewall.](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a>Próximas etapas

- [Recursos de detecção da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

Recursos de detecção Avançado da Central de segurança do Azure ajuda a ameaças ativas tooidentify, direcionando os recursos do Microsoft Azure e fornece a você com informações de saudação necessário toorespond rapidamente.

- [Detecção de Ameaças do Banco de Dados SQL](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

Detecção de ameaças do banco de dados SQL do Azure ajudou a suas preocupações sobre o banco de dados de tootheir ameaças potenciais.
