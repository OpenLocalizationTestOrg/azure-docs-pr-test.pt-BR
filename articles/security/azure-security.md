---
title: "aaaIntroduction tooAzure segurança | Microsoft Docs"
description: "Saiba mais sobre a Segurança do Azure, seus serviços e como ela funciona."
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
ms.date: 05/03/2017
ms.author: TomSh
ms.openlocfilehash: 2d42057e9586a0b6ce16a1582db3b3af842297af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security"></a>Introdução tooAzure segurança
## <a name="overview"></a>Visão geral
Sabemos que a segurança é trabalho na nuvem hello e como é importante que você encontrar precisas e em tempo hábil de informações sobre a segurança do Azure. Um dos toouse de motivos melhor Azure Olá para seus aplicativos e serviços é tootake aproveitar sua ampla variedade de recursos e ferramentas de segurança. Essas ferramentas e recursos ajudam a tornar soluções seguras de possíveis toocreate na plataforma Azure segura de saudação. O Microsoft Azure fornece confidencialidade, integridade e disponibilidade dos dados do cliente, ao mesmo tempo que também permite uma responsabilidade transparente.

toohelp você entender melhor a coleção de saudação de controles de segurança implementado no Microsoft Azure de perspectivas do cliente hello e as operações da Microsoft, neste white paper, "Introdução tooAzure segurança", será gravado tooprovide um obter uma visão completa de segurança de saudação disponível com o Microsoft Azure.

### <a name="azure-platform"></a>Plataforma Azure
O Azure é uma plataforma de serviço de nuvem pública que dá suporte a uma ampla seleção de sistemas operacionais, linguagens de programação, estruturas, ferramentas, bancos de dados e dispositivos. Ele pode executar contêineres do Linux com a integração com o Docker, criar aplicativos com JavaScript, Python, .NET, PHP, Java e Node.js e criar back-ends para dispositivos iOS, Android e Windows.

Serviços de nuvem pública do Azure oferecem suporte a saudação tecnologias mesmo milhões de desenvolvedores e profissionais de TI já contam e confiarem. Quando você criar ou migra ativos de TI para, um provedor de serviços de nuvem pública que você depender de tooprotect de recursos da organização seus aplicativos e dados com controles de saudação e serviços Olá eles oferecem toomanage Olá segurança de seu baseado em nuvem ativos.

Infraestrutura do Azure foi projetada de tooapplications de recurso para a hospedagem de milhões de clientes simultaneamente, e fornece uma base confiável em que as empresas podem atender aos requisitos de segurança.

Além disso, Azure fornece uma ampla gama de segurança configuráveis toocontrol de capacidade de opções e hello-los para que você possa personalizar requisitos exclusivos de segurança toomeet Olá das implantações de sua organização. Este documento ajuda você a entender como as funcionalidades de segurança do Azure podem ajudá-lo a atender a esses requisitos.

> [!Note]
> Olá o foco principal deste documento é voltado para o cliente controles que você pode usar toocustomize e aumentar a segurança dos seus aplicativos e serviços.
>
> Podemos fornecer algumas informações de visão geral, mas para obter informações detalhadas sobre como a Microsoft protege Olá plataforma Windows Azure, consulte as informações fornecidas no hello [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx).

### <a name="abstract"></a>Resumo
Inicialmente, as migrações de nuvem pública foram orientadas por tooinnovate de custo e economia e agilidade. Durante algum tempo, a segurança era considerada uma grande preocupação, e até mesmo uma estraga-prazeres para a migração na nuvem pública. No entanto, segurança de nuvem pública deixaram de ser uma grande preocupação tooone drivers de saudação de migração para a nuvem. Olá racional isso é Olá superior capacidade dos aplicativos de tooprotect de provedores de serviço de nuvem pública grande e dados de saudação de ativos com base em nuvem.

Infraestrutura do Azure foi projetada de saudação recurso tooapplications para hospedagem milhões de clientes simultaneamente, e fornece uma base confiável em que as empresas podem atender às suas necessidades de segurança. Além disso, Azure fornece uma ampla gama de segurança configuráveis toocontrol de capacidade de opções e hello-los para que você possa personalizar requisitos exclusivos de saudação do toomeet de segurança de sua toomeet de implantações de TI políticas de controle e aderir tooexternal normas.

Este documento descreve toosecurity de abordagem da Microsoft dentro da plataforma de nuvem do Microsoft Azure hello:
* Recursos de segurança implementados pelo Microsoft hello toosecure infraestrutura do Azure, os dados do cliente e aplicativos.
* Azure serviços e a segurança recursos disponíveis tooyou toomanage hello segurança dos serviços de saudação e seus dados dentro de suas assinaturas do Azure.

## <a name="summary-azure-security-capabilities"></a>Resumo dos recursos de segurança do Azure
a seguir tabela Olá fornece uma breve descrição dos recursos de segurança Olá implementadas pelo Microsoft hello toosecure infraestrutura do Azure, os dados do cliente e aplicativos seguros.
### <a name="security-features-implemented-toosecure-hello-azure-platform"></a>Segurança recursos implementados tooSecure Olá plataforma Azure:
Olá recursos listados a seguir são recursos que você pode examinar a garantia de saudação tooprovide que Olá que plataforma Azure é gerenciada de forma segura. Os links foram fornecidos para detalhar ainda mais a forma como a Microsoft aborda perguntas de confiança dos clientes em quatro áreas: Plataforma Segura, Privacidade e Controles, Conformidade e Transparência.


| [Plataforma Segura](https://www.microsoft.com/en-us/trustcenter/Security/default.aspx)  | [Privacidade e Controles](https://www.microsoft.com/en-us/trustcenter/Privacy/default.aspx)  |[Conformidade](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)   | [Transparência](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| :-- | :-- | :-- | :-- |
| [Ciclo de Desenvolvimento de Segurança](https://www.microsoft.com/en-us/sdl/), auditorias internas | [Gerenciar os dados de todo o tempo de saudação](https://www.microsoft.com/en-us/trustcenter/Privacy/You-own-your-data) | [Central de Confiabilidade](https://www.microsoft.com/en-us/trustcenter/default.aspx) |[Como a Microsoft protege os dados do cliente nos serviços do Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| [Treinamento de segurança obrigatório, verificações de histórico](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc) |  [Controlar o local dos dados](https://www.microsoft.com/en-us/trustcenter/Privacy/Where-your-data-is-located) |  [Hub de Controles Comuns](https://www.microsoft.com/en-us/trustcenter/Common-Controls-Hub) |[Como a Microsoft gerencia o local de dados nos serviços do Azure](http://azuredatacentermap.azurewebsites.net/)|
| [Testes de penetração](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc), [Detecção de intrusão, DDoS](https://www.microsoft.com/en-us/trustcenter/Security/ThreatManagemen), [Auditorias e registro em log](https://www.microsoft.com/en-us/trustcenter/Security/AuditingAndLogging) | [Fornecer acesso a dados em seus próprios termos](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms) |  [Olá nuvem serviços devido cuidado lista de verificação](https://www.microsoft.com/en-us/trustcenter/Compliance/Due-Diligence-Checklist) |[Quem na Microsoft pode acessar seus dados e em quais termos](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)|
| [Data center de última geração](https://www.microsoft.com/en-us/cloud-platform/global-datacenters), segurança física, [Rede Segura](https://docs.microsoft.com/en-us/azure/security/security-network-overview) | [Respondendo a imposição de toolaw](https://www.microsoft.com/en-us/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data) |  [Conformidade por serviço, local e setor](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx) |[Como a Microsoft protege os dados do cliente nos serviços do Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)|
|  [Resposta ao incidente de segurança](http://aka.ms/SecurityResponsepaper), [Responsabilidade compartilhada](http://aka.ms/sharedresponsibility) |[Padrões de privacidade rigorosos](https://www.microsoft.com/en-us/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards) |  | [Revisar a certificação para serviços do Azure, Hub de transparência](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)|



### <a name="security-features-offered-by-azure-toosecure-data-and-application"></a>Recursos de segurança oferecidos pelo Azure tooSecure dados e aplicativos
Dependendo do modelo de serviço de nuvem Olá, é responsabilidade de variável para quem é responsável por gerenciar a segurança de saudação do serviço ou aplicativo hello. Há recursos disponíveis no hello plataforma Azure tooassist você atender essas responsabilidades por meio de recursos internos e parceiros de soluções que podem ser implantados em uma assinatura do Azure.

recursos internos de saudação são organizados em áreas funcionais seis (6): as operações, aplicativos, armazenamento, rede, computação e identidade. Detalhes adicionais sobre os recursos de saudação e recursos disponíveis no hello plataforma do Azure nas seguintes áreas seis (6) são fornecidos por meio de informações de resumo.

## <a name="operations"></a>Operações
Esta seção fornece outras informações sobre os principais recursos em operações de segurança, e informações de resumo sobre esses recursos.

### <a name="operations-management-suite-security-and-audit-dashboard"></a>Painel de Segurança e Auditoria do Operations Management Suite
Olá [solução do OMS segurança e auditoria](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) fornece uma visão abrangente da sua organização postura de segurança de TI com [consultas de pesquisa interna](https://blogs.technet.microsoft.com/msoms/2016/01/21/easy-microsoft-operations-management-suite-search-queries/) para problemas importantes que exigem sua atenção. Olá [segurança e auditoria](https://technet.microsoft.com/library/mt484091.aspx) dashboard é a tela inicial Olá para tudo relacionado toosecurity no OMS. Ele fornece uma visão alto nível Olá estado de segurança de seus computadores. Ele também inclui Olá capacidade tooview todos os eventos de saudação nas últimas 24 horas, 7 dias, ou qualquer outro período de tempo personalizado.

Além disso, você pode configurar o OMS segurança e conformidade muito[automaticamente realizar ações específicas](https://blogs.technet.microsoft.com/robdavies/2016/04/20/simple-look-at-oms-alert-remediation-with-runbooks-part-1/) quando um evento específico é detectado.

### <a name="azure-resource-manager"></a>Gerenciador de Recursos do Azure
[Gerenciador de recursos do Azure ](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) permite que você toowork com recursos de saudação em sua solução como um grupo. Você pode implantar, atualizar ou excluir todos os recursos de saudação para sua solução em uma única operação coordenada. Use um [modelo do Azure Resource Manager](https://blogs.technet.microsoft.com/canitpro/2015/06/29/devops-basics-infrastructure-as-code-arm-templates/) para a implantação, e esse modelo pode ser útil para diferentes ambientes, como teste, preparação e produção. Gerenciador de recursos fornece segurança, auditoria e marcação recursos toohelp gerenciar seus recursos após a implantação.

Implantações do Azure do Gerenciador de recursos com base em modelo ajudam a melhorar a segurança de saudação de soluções implantadas no Azure como controlar as configurações de segurança padrão e pode ser integrado em implantações padronizadas com base em modelo. Isso reduz o risco de saudação de erros de configuração de segurança que podem ocorrer durante as implantações do manuais.

### <a name="application-insights"></a>Application Insights
O [Application Insights](https://docs.microsoft.com/azure/application-insights/) é um serviço de Gerenciamento de Desempenho de Aplicativos (APM) extensível para desenvolvedores da Web. Com o Application Insights, você pode monitorar seus aplicativos Web ativos e detectar automaticamente as anomalias no desempenho. Ele inclui uma análise rigorosa ferramentas toohelp que diagnosticar problemas e toounderstand que os usuários, na verdade, fazem com seus aplicativos. Ele monitora o seu aplicativo todo o tempo de saudação executando, durante o teste e depois de publicado ou implantá-lo.

Application Insights cria gráficos e tabelas que mostram a você, por exemplo, que horas do dia para obter a maioria dos usuários, como aplicativo hello responsivo está, e também que ser fornecido por qualquer externos de serviços que ele depende.

Se houver falhas, falhas ou problemas de desempenho, você pode procurar dados de telemetria Olá causa de saudação toodiagnose detalhes. E serviço Olá envia emails se houver alterações na disponibilidade de saudação e o desempenho do seu aplicativo. Informações do aplicativo, portanto, se torna uma ferramenta de segurança importantes porque ela ajuda a disponibilidade Olá Olá confidencialidade, integridade e triplo de segurança de disponibilidade.

### <a name="azure-monitor"></a>Azure Monitor
[Monitor do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) oferece visualização, consulta, roteamento, alertas, AutoEscala e automação em ambos os dados de saudação infraestrutura do Azure ([Log de atividades](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)) e cada recurso do Azure individual ([ Logs de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)). Você pode usar o Monitor do Azure tooalert você nos eventos relacionados à segurança que são gerados nos logs do Azure.

### <a name="log-analytics"></a>Log Analytics
[Análise de log](https://azure.microsoft.com/documentation/services/log-analytics/) parte do [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) – fornece uma solução de gerenciamento de TI para locais e infraestrutura de terceiros baseados em nuvem (como o AWS) além tooAzure recursos. Dados do Monitor do Azure podem ser roteados diretamente tooLog análise para ver logs e métricas para todo o ambiente em um único local.

Análise de log pode ser uma ferramenta útil forense e outras análises de segurança, como a ferramenta de saudação permite que você tooquickly pesquisa por meio de grandes quantidades de entradas relacionadas à segurança com uma abordagem de consulta flexível. Além disso, os [logs de firewall e de proxy locais podem ser exportados para o Azure e disponibilizados para análise com o Log Analytics.](https://docs.microsoft.com/azure/log-analytics/log-analytics-proxy-firewall)

### <a name="azure-advisor"></a>Azure Advisor
[O Supervisor do Azure](https://docs.microsoft.com/azure/advisor/) é um consultor de nuvem personalizados que ajuda você a toooptimize as implantações do Azure. Ele analisa a configuração dos recursos e a telemetria do uso. Em seguida, recomenda soluções toohelp melhorar Olá [desempenho](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations), [segurança](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations), e [alta disponibilidade](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations) de seus recursos durante a procura de oportunidades muito[reduzir seu Azure geral gastar](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations). O Assistente do Azure fornece recomendações de segurança, o que pode melhorar consideravelmente sua postura de segurança geral para soluções implantadas no Azure. Essas recomendações são obtidas da análise de segurança executada pela [Central de Segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-intro)

### <a name="azure-security-center"></a>Central de Segurança do Azure
[Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) Olá de ajuda a evitar, detectar e responder toothreats maior visibilidade e controle sobre a segurança de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

Além disso, a Central de Segurança do Azure ajuda com operações de segurança, fornecendo um único painel que mostra alertas e recomendações para ação imediata. Geralmente, você pode corrigir problemas com um único clique dentro do console central de segurança do Azure hello.
## <a name="applications"></a>Aplicativos
seção de saudação fornece informações adicionais sobre os principais recursos de informações de segurança e o resumo do aplicativo sobre esses recursos.

### <a name="web-application-vulnerability-scanning"></a>Verificação de vulnerabilidades de aplicativos Web
Uma saudação tooget de maneiras mais fáceis de Introdução ao teste quanto a vulnerabilidades em sua [aplicativo de serviço de aplicativo](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) é hello toouse [integração com Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform vulnerabilidade de um clique a verificação seu aplicativo. Você pode exibir resultados de teste de saudação em um relatório de fácil de entender e aprender como toofix cada vulnerabilidade com instruções passo a passo.

### <a name="penetration-testing"></a>Teste de penetração
Se você preferir tooperform seu próprios penetração testes ou deseja toouse outro conjunto de scanner ou provedor, você deve seguir Olá [processo de aprovação de teste de penetração do Azure](https://security-forms.azure.com/penetration-testing/terms) e obter penetração de saudação desejada tooperform aprovação prévia testes.

### <a name="web-application-firewall"></a>Firewall do aplicativo Web
Olá firewall do aplicativo web (WAF) em [Azure Application Gateway](https://azure.microsoft.com/services/application-gateway/) ajuda a proteger aplicativos web contra ataques comuns baseado na web, como injeção de SQL, ataques de script entre sites e sequestro de sessão. Vem pré-configurada com proteção contra ameaças identificadas pelo Olá [abra Web aplicativo segurança projeto (OWASP) como Olá top 10 vulnerabilidades comuns](https://msdn.microsoft.com/library/).

### <a name="authentication-and-authorization-in-azure-app-service"></a>Autenticação e autorização no Serviço de Aplicativo do Azure
[Autenticação do serviço de aplicativo / autorização](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) é um recurso que fornece uma maneira para toosign seu aplicativo em usuários para que você não tem o código de toochange no back-end de aplicativo hello. Ele fornece uma maneira fácil tooprotect seu aplicativo e o trabalho com dados por usuário.

### <a name="layered-security-architecture"></a>Arquitetura de segurança em camadas
Como os [Ambientes do Serviço de Aplicativo](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-intro) fornecem um ambiente de tempo de execução isolado implantado em uma [Rede Virtual do Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview), os desenvolvedores podem criar uma arquitetura de segurança em camadas fornecendo níveis diferentes de acesso à rede para cada camada de aplicativo. Desejo comum é toohide API back-ends de acessar a Internet geral e só permitir que APIs toobe chamado por aplicativos web upstream. [Grupos de segurança (NSGs) de rede](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/) pode ser usado em sub-redes de rede Virtual do Azure que contém os ambientes de serviço de aplicativo toorestrict acesso público tooAPI aplicativos.

### <a name="web-server-diagnostics-and-application-diagnostics"></a>Diagnóstico de servidor Web e diagnóstico de aplicativos
Aplicativos do serviço de aplicativo web fornecem funcionalidade de diagnóstico para obter informações de registro em log do servidor de web hello e o aplicativo da web hello. Estes estão logicamente separados em [diagnóstico de servidor Web](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) e [diagnóstico de aplicativos](https://technet.microsoft.com/library/hh530058(v=sc.12).aspx). O servidor Web inclui dois grandes avanços em diagnóstico e solução de problemas de sites e aplicativos.

Olá primeiro novo recurso é informações de estado em tempo real sobre pools de aplicativos, processos de trabalho, sites, domínios de aplicativo e solicitações em execução. vantagens da nova segundo Olá são Olá eventos de rastreamento detalhados que controlam uma solicitação ao longo de todo o processo de solicitação e resposta hello.

tooenable Olá coleta esses eventos de rastreamento, o IIS 7 pode ser logs de rastreamento completo de captura tooautomatically configurado, em formato XML, para qualquer solicitação específica com base em códigos de resposta de erro ou tempo decorrido.

#### <a name="web-server-diagnostics"></a>Diagnóstico de servidor Web
Você pode habilitar ou desabilitar Olá tipos de logs a seguir:

-   Registro em Log Detalhado de Erros - informações detalhadas de erros para códigos de status HTTP que indiquem uma falha (código de status 400 ou superior). Pode conter informações que podem ajudar a determinar por que o servidor de saudação retornou o código de erro de saudação.

-   Falha no rastreamento de solicitação - informações detalhadas sobre solicitações com falha, incluindo um rastreamento de Olá IIS componentes usados tooprocess Olá solicitação e tempo Olá em cada componente. Isso pode ser útil se você está tentando executar o desempenho do site tooincrease ou isolar o que está causando um toobe específico de erro HTTP retornado.

-   Log do servidor - informações sobre transações HTTP usando o formato de arquivo de log estendido W3C de saudação do Web. Isso é útil ao determinar a métrica geral do site como o número de saudação de solicitações administradas ou quantas solicitações são de um endereço IP específico.

#### <a name="application-diagnostics"></a>diagnóstico de aplicativos
[Diagnóstico de aplicativo](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) permite a você informações toocapture produzidas por um aplicativo web. Aplicativos ASP.NET podem usar Olá [Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) classe toolog informações toohello aplicativo diagnóstico de log. No Application Diagnostics, há dois tipos principais de eventos, os relacionados ao desempenho tooapplication e aquelas relacionadas a erros e falhas de tooapplication. Olá falhas e erros podem ser divididos em problemas de conectividade, segurança e falha. Problemas de falha estão normalmente relacionados tooa problema com o código de aplicativo hello.

No Application Diagnostics, você pode ver os eventos agrupados destas maneiras:

-   Todos (exibe todos os eventos)
-   Erros do Aplicativo (exibe eventos de exceção)
-   Desempenho (exibe eventos de desempenho)

## <a name="storage"></a>Armazenamento
seção de saudação fornece informações adicionais sobre os principais recursos de segurança e resumo informações sobre esses recursos de armazenamento do Azure.

### <a name="role-based-access-control-rbac"></a>RBAC (Controle de Acesso Baseado em Função)
Você pode proteger a conta de armazenamento com o RBAC (Controle de Acesso Baseado em Função). Restringindo o acesso com base em Olá [necessário tooknow](https://en.wikipedia.org/wiki/Need_to_know) e [privilégio mínimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) princípios de segurança é fundamental para as organizações que desejam tooenforce políticas de segurança para acesso a dados. Esses direitos de acesso são concedidos atribuindo Olá apropriado RBAC função toogroups e aplicativos em um determinado escopo. Você pode usar [funções internas de RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles), como colaborador da conta de armazenamento, tooassign privilégios toousers. Acessar chaves de armazenamento de toohello para uma conta de armazenamento usando Olá [do Azure Resource Manager](https://docs.microsoft.com/azure/storage/storage-security-guide) modelo pode ser controlado por meio do controle de acesso baseado em função (RBAC).

### <a name="shared-access-signature"></a>Assinatura de acesso compartilhado
Um [assinatura de acesso compartilhado (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) fornece acesso delegado tooresources na sua conta de armazenamento. Olá SAS significa que você pode conceder a que um cliente limitado tooobjects permissões na conta de armazenamento para um período especificado e com um conjunto de permissões especificado. Você pode conceder essas permissões limitadas sem ter que tooshare suas chaves de acesso da conta.

### <a name="encryption-in-transit"></a>Criptografia em trânsito
A criptografia em trânsito é um mecanismo de proteção de dados quando eles são transmitidos entre redes. Com o Armazenamento do Azure, você pode proteger dados usando:
-   [Criptografia de nível de transporte](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), como HTTPS ao transferir dados dentro ou fora do Armazenamento do Azure.

-   [Criptografia na transmissão](https://docs.microsoft.com/azure/storage/storage-security-guide#using-encryption-during-transit-with-azure-file-shares), como a [criptografia SMB 3.0](https://docs.microsoft.com/azure/storage/storage-security-guide) para [compartilhamentos de Arquivo do Azure](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files).

-   Criptografia do lado do cliente, dados de saudação do tooencrypt antes que sejam transferidos para o armazenamento e dados de saudação toodecrypt depois que ela é transferida do armazenamento.

### <a name="encryption-at-rest"></a>Criptografia em repouso
Para muitas organizações, a criptografia de dados em repouso é uma etapa obrigatória no sentido de garantir a soberania, a privacidade e a conformidade dos dados. Há três recursos de segurança de armazenamento do Azure que fornecem criptografia de dados que estão “em repouso”:

-   [Criptografia do serviço de armazenamento](https://docs.microsoft.com/azure/storage/storage-service-encryption) permite que o serviço de armazenamento de saudação criptografa automaticamente os dados quando escrever tooAzure armazenamento de toorequest.

-   [Criptografia do lado do cliente](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) também fornece o recurso de saudação de criptografia em repouso.

-   [Criptografia de disco do Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) permite que você tooencrypt Olá OS discos e dados usados por uma máquina virtual IaaS.

### <a name="storage-analytics"></a>Análise de Armazenamento
O [Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) executa o registro em log e fornece dados de métrica para uma conta de armazenamento. Você pode usar este tootrace as solicitações de dados, analisar tendências de uso e diagnosticar problemas com sua conta de armazenamento. Análise de armazenamento registra informações detalhadas sobre o serviço de armazenamento de tooa de solicitações bem-sucedidas e com falha. Essas informações podem ser usadas toomonitor as solicitações individuais e toodiagnose problemas com um serviço de armazenamento. As solicitações são registradas em uma base de melhor esforço. Olá seguintes tipos de solicitações autenticadas é registrado:
-   Solicitações bem sucedidas.

-   Solicitações com falha, incluindo o tempo limite, limitação, rede, autorização e outros erros.

-   Solicitações que usam uma SAS (Assinatura de Acesso Compartilhado), incluindo solicitações bem-sucedidas e com falha.

-   Dados de tooanalytics solicitações.

### <a name="enabling-browser-based-clients-using-cors"></a>Habilitar clientes com base no navegador usando CORS
[Compartilhamento de recursos entre origens (CORS)](https://docs.microsoft.com/rest/api/storageservices/fileservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) é um mecanismo que permite domínios toogive outra permissão para acessar os recursos da outra. saudação de agente do usuário envia tooensure cabeçalhos adicionais que o código JavaScript Olá carregado de um determinado domínio pode tooaccess recursos localizados em outro domínio. domínio de segundo Olá responde com cabeçalhos adicionais permitir ou negar acesso ao domínio original Olá tooits recursos.

Armazenamento do Azure services agora oferecem suporte ao CORS para que depois de definir regras de CORS Olá para serviço hello, uma solicitação autenticada corretamente feita no serviço de saudação de um domínio diferente seja avaliada toodetermine se é permitido de acordo com as regras de toohello que tiver especificado.
## <a name="networking"></a>Rede
seção de saudação fornece informações adicionais sobre os principais recursos nas informações de resumo e segurança de rede do Azure sobre esses recursos.

### <a name="network-layer-controls"></a>Controles de camada de rede
Controle de acesso de rede é o ato de saudação de limitar tooand de conectividade de dispositivos específicos ou sub-redes e representa Olá principal de segurança de rede. meta de saudação do controle de acesso de rede é toomake-se de que suas máquinas virtuais e serviços são acessíveis tooonly usuários e dispositivos toowhich você deseja que eles acessível.

#### <a name="network-security-groups"></a>Grupos de segurança de rede
Um [grupo de segurança de rede (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) é um pacote com monitoração de estado básico filtragem de firewall e permite que você toocontrol acesso com base em um [5-tupla](https://www.techopedia.com/definition/28190/5-tuple). Os NSGs não fornecem inspeção da camada de aplicativo nem controles de acesso autenticado. Eles podem ser usados tráfego toocontrol mover entre as sub-redes em uma rede Virtual do Azure e o tráfego entre uma rede Virtual do Azure e hello da Internet.

#### <a name="route-control-and-forced-tunneling"></a>Controle de rota e túnel forçado
Olá capacidade toocontrol comportamento de roteamento em suas redes virtuais do Azure é um recurso de controle de acesso e segurança críticas de rede. Por exemplo, se você quiser toomake-se de que todos os tooand de tráfego de rede Virtual do Azure passa por esse dispositivo de segurança virtual, precisa toocontrol capaz de toobe e personalizar o comportamento de roteamento. É possível fazer isso configurando as Rotas Definidas pelo Usuário no Azure.

[Rotas definidas pelo usuário](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) permitem toocustomize caminhos de entrada e saídos para o tráfego de movimentação dentro e fora de máquinas virtuais individuais ou sub-redes tooinsure hello mais segura possível de rota. [Encapsulamento forçado](https://www.petri.com/azure-forced-tunneling) é um mecanismo que você pode usar tooensure seus serviços não são permitidos tooinitiate toodevices uma conexão em Olá da Internet.

Isso é diferente do que está sendo tooaccept capaz de conexões de entrada e, em seguida, responder toothem. Servidores web front-end precisam toorequests toorespond de hosts da Internet e para que o tráfego originado de Internet é permitido servidores da web de entrada toothese e Olá web pode responder.

O túnel forçado é comumente usados tooforce o tráfego de saída toohello Internet toogo por meio de firewalls e proxies de segurança local.

#### <a name="virtual-network-security-appliances"></a>Dispositivos de segurança de rede virtual
Enquanto o túnel forçado, rotas definidas pelo usuário e grupos de segurança de rede fornecem um nível de segurança em camadas de transporte e de rede de saudação do hello [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), pode haver ocasiões em que você deseja tooenable segurança em níveis mais altos de pilha de saudação. É possível acessar esses recursos avançados de segurança de rede por meio de uma solução de dispositivo de segurança de rede de parceiro do Azure. Você pode encontrar hello mais recentes soluções de segurança de rede de parceiro do Azure, visitando Olá [Azure Marketplace](https://azure.microsoft.com/marketplace/) e a pesquisa de "segurança" e "segurança de rede".

### <a name="azure-virtual-network"></a>Rede Virtual do Azure

Uma rede virtual do Azure (VNet) é uma representação de sua própria rede na nuvem hello. É uma isolamento lógico de saudação rede Azure fabric dedicado tooyour assinatura. Você pode controlar totalmente blocos de endereços IP hello, configurações de DNS, políticas de segurança e tabelas de rotas dentro dessa rede. Você pode segmentar a VNet em sub-redes e colocar as VMs (máquinas virtuais) de IaaS do Azure e/ou os [Serviços de nuvem (instâncias de função de PaaS)](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) em Redes Virtuais do Azure.

Além disso, você pode se conectar a rede Olá rede virtual tooyour local usando uma saudação [opções de conectividade](https://docs.microsoft.com/azure/vpn-gateway/) disponíveis no Azure. Em essência, você pode expandir tooAzure sua rede, com controle total em blocos de endereços IP com o benefício de saudação de escala corporativa que Azure fornece.

A rede do Azure dá suporte a vários cenários de acesso remoto seguro. Entre eles estão:

-   [Conecte-se de estações de trabalho individuais tooan rede Virtual do Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

-   [Conecte-se tooan de rede local na rede Virtual do Azure com uma VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

-   [Conecte-se tooan de rede local na rede Virtual do Azure com uma conexão WAN dedicada](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)

-   [Conectar redes virtuais do Azure tooeach outros](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)

### <a name="vpn-gateway"></a>Gateway de VPN
toosend o tráfego de rede entre sua rede Virtual do Azure e seu site local, você deve criar um gateway de VPN para sua rede Virtual do Azure. Um [gateway de VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) é um tipo de gateway de rede virtual que envia o tráfego criptografado em uma conexão pública. Você também pode usar o tráfego de toosend de gateways VPN entre redes virtuais do Azure sobre Olá malha de rede do Azure.

### <a name="express-route"></a>ExpressRoute
Microsoft Azure [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) é um link WAN dedicado que permite estender suas redes locais no hello nuvem da Microsoft em uma conexão privada dedicada facilitada por um provedor de conectividade.

![ExpressRoute](./media/azure-security/azure-security-fig1.png)

Com o ExpressRoute, você pode estabelecer serviços de nuvem de tooMicrosoft de conexões, como o Microsoft Azure, Office 365 e CRM Online. A conectividade pode ocorrer de uma rede “qualquer para qualquer” (VPN IP), uma rede Ethernet ponto a ponto ou uma conexão cruzada virtual por meio de um provedor de conectividade em uma colocalização.

Conexões de rota expressa não passam pela Olá Internet pública e, portanto, pode ser considerado mais seguro do que as soluções de VPN. Isso permite toooffer de conexões de rota expressa mais confiabilidade, velocidades mais rápidas, latências menores e maior segurança que as conexões típicas pela Internet da saudação.


### <a name="application-gateway"></a>Gateway de Aplicativo
O [Gateway de Aplicativo do Microsoft  Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) fornece um [ADC (Controlador de Entrega de Aplicativos)](https://en.wikipedia.org/wiki/Application_delivery_controller) como um serviço, oferecendo vários recursos de balanceamento de carga de camada 7 para o aplicativo.

![Gateway de Aplicativo](./media/azure-security/azure-security-fig2.png)

Ele permite que você produtividade de farm da web toooptimize descarregando CPU intensa SSL encerramento toohello Application Gateway (também conhecido como "Descarregamento de SSL" ou "Pontes SSL"). Ele também fornece outros recursos de roteamento de camada 7 incluindo round-robin distribuição de tráfego de entrada, a afinidade de sessão baseada em cookie, roteamento baseado no caminho de URL e Olá capacidade toohost vários sites por trás de um único Gateway de aplicativo. O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.

Ele fornece failover, o roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local.

O aplicativo fornece muitos recursos do Controlador de Entrega de Aplicativos (ADC), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de [Secure Sockets Layer (SSL)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-powershell), as sondas de integridade personalizadas, suporte para vários sites e muitos outros.

### <a name="web-application-firewall"></a>Firewall do Aplicativo Web
Firewall do aplicativo Web é um recurso do [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) que fornece proteção tooweb aplicativos que usam o gateway do aplicativo para as funções padrão do controle de entrega de aplicativos (ADC). Firewall do aplicativo Web faz isso, protegendo-os contra a maioria das Olá OWASP top 10 web vulnerabilidades comuns.

![Firewall do Aplicativo Web](./media/azure-security/azure-security-fig1.png)

-   Proteção contra injeção de SQL

-   Proteção Contra Ataques Comuns da Web, como a injeção de comandos, as solicitações HTTP indesejadas, a divisão de resposta HTTP e o ataque de inclusão de arquivo remoto

-   Proteção contra violações de protocolo HTTP

-   Proteção contra anomalias de protocolo HTTP, como ausência de host de agente do usuário e de cabeçalhos de aceitação

-   Prevenção contra bots, rastreadores e scanners

-   Detecção de problemas de configuração de aplicativo comuns (ou seja, Apache, IIS etc.)


Um tooprotect de firewall do aplicativo web centralizado contra ataques de web simplifica muito o gerenciamento de segurança e fornece a melhor aplicativo toohello de garantia contra ameaças de saudação de intrusões. Uma solução WAF também possa reagir de ameaça à segurança tooa mais rápida por uma vulnerabilidade conhecida em um local central em vez de proteção de cada um dos aplicativos web individuais de aplicação de patch. Aplicativo de gateways podem ser facilmente convertido tooan gateway de aplicativo com o firewall do aplicativo web.
### <a name="traffic-manager"></a>Gerenciador de Tráfego
Microsoft [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) permite que você toocontrol distribuição de saudação do tráfego do usuário para pontos de extremidade de serviço em data centers diferentes. Os pontos de extremidade de serviço com suporte no Gerenciador de Tráfego incluem VMs do Azure, Aplicativos Web e Serviços de Nuvem. Você também pode usar o Gerenciador de Tráfego com pontos de extremidade externos e não do Azure. O Traffic Manager usa Olá sistema DNS (Domain Name) toodirect cliente solicita toohello ponto de extremidade mais apropriado com base em um [o método de roteamento de tráfego](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) e a integridade de saudação de pontos de extremidade de saudação.

O Traffic Manager fornece uma variedade de roteamento de tráfego métodos toosuit diferentes necessidades de aplicativo, integridade do ponto de extremidade [monitoramento](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)e o failover automático. Gerenciador de tráfego é toofailure resiliente, incluindo Olá falha de toda a uma região do Azure.
### <a name="azure-load-balancer"></a>Azure Load Balancer
[O balanceador de carga do Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) fornece tooyour aplicativos de alto desempenho de disponibilidade e rede. É um balanceador de carga do tipo Camada 4 (TCP, UDP) que distribui o tráfego de entrada entre as instâncias de serviço íntegras definidas em um conjunto de balanceadores de carga. O Azure Load Balancer pode ser configurado para:

-   Balancear cargas de entrada da Internet tráfego toovirtual máquinas. Essa configuração é conhecida como [balanceamento de carga voltada para a Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Balanceie o tráfego de carga entre as máquinas virtuais em uma rede virtual, entre as máquinas virtuais nos serviços de nuvem ou entre os computadores locais e as máquinas virtuais em uma rede virtual entre as instalações. Essa configuração é conhecida como [balanceamento de carga interno](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview). 

- Encaminhar o tráfego externo tooa específico de máquina virtual

### <a name="internal-dns"></a>DNS interno
Você pode gerenciar a lista de saudação de servidores DNS usados em uma rede virtual no Portal de gerenciamento de saudação ou no arquivo de configuração de rede de saudação. Cliente poderá adicionar os servidores DNS too12 para cada rede virtual. Ao especificar servidores DNS, é importante tooverify se a lista de servidores DNS do cliente na ordem correta, Olá para o ambiente do cliente. As listas de servidores DNS não funcionam em round robin. Eles são usados na ordem de saudação que foram especificados. Se o primeiro servidor DNS hello, na lista de saudação é capaz de toobe atingido, o cliente de saudação usa esse servidor DNS, independentemente de servidor DNS hello está funcionando corretamente ou não. Olá toochange ordem do servidor DNS para a rede virtual do cliente, remover os servidores DNS Olá da lista de saudação e adicioná-las na ordem de saudação cliente quer. DNS dá suporte a proporção de disponibilidade de saudação do triplo de segurança "CIA" Olá.

### <a name="azure-dns"></a>DNS do Azure
Olá [Domain Name System](https://technet.microsoft.com/library/bb629410.aspx), ou DNS, é responsável pela conversão (ou seja, resolver) um site ou serviço name tooits endereço IP. O [DNS do Azure](https://docs.microsoft.com/azure/dns/dns-overview) é um serviço de hospedagem para domínios DNS, fornecendo resolução de nomes usando a infraestrutura do Microsoft Azure. Ao hospedar seus domínios no Azure, você pode gerenciar seu DNS registros usando Olá mesmo credenciais, APIs, ferramentas e cobrança como outros serviços do Azure. DNS dá suporte a proporção de disponibilidade de saudação do triplo de segurança "CIA" Olá.
### <a name="log-analytics-nsgs"></a>NSGs do Log Analytics
Você pode habilitar Olá categorias de log de diagnóstico a seguir para NSGs:
-   Evento: Contém entradas para o NSG as regras são aplicadas tooVMs e funções de instância com base no endereço MAC. status Olá para essas regras são coletados a cada 60 segundos.

-   Contador de regras: contém entradas de quantas vezes cada regra NSG é aplicado toodeny ou permitir o tráfego.

### <a name="azure-security-center"></a>Central de Segurança do Azure
Central de segurança ajuda a evitar, detectar e responder toothreats e fornece a você maior visibilidade e controle sobre, Olá segurança de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança. As recomendações da rede giram em torno de firewalls, Grupos de Segurança da Rede, configuração das regras do tráfego de entrada e muito mais.

As recomendações de rede disponíveis são as seguintes:

-   [Adicionar um Firewall de geração de Avançar](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall) recomenda que você adicione um Firewall de próxima geração (NGFW) de um tooincrease de parceiro Microsoft suas proteções de segurança

-   [Rotear o tráfego por meio de NGFW](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall#route-traffic-through-ngfw-only) recomenda que você configure regras de segurança de grupo (NSG) que forçar o tráfego de entrada tooyour VM por meio de seu NGFW de rede.

-   [Habilitar Grupos de Segurança de Rede em máquinas virtuais ou sub-redes](https://docs.microsoft.com/azure/security-center/security-center-enable-network-security-groups) Recomenda que você habilite NSGs em sub-redes ou VMs.

-   [Restringir o acesso por meio do ponto de extremidade voltado para a Internet](https://docs.microsoft.com/azure/security-center/security-center-restrict-access-through-internet-facing-endpoints) Recomenda que você configure regras de tráfego de entrada para NSGs.


## <a name="compute"></a>Computação

seção de saudação fornece informações adicionais sobre os principais recursos essa área e resumo as informações sobre esses recursos.

### <a name="antimalware--antivirus"></a>Antimalware e antivírus
Com o IaaS do Azure, você pode usar o software antimalware de fornecedores de segurança, como Microsoft, Symantec, Trend Micro, McAfee e Kaspersky tooprotect suas máquinas virtuais de arquivos mal-intencionados, adware e outras ameaças. O [Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) para Serviços de Nuvem e Máquinas Virtuais do Azure é uma funcionalidade de proteção que ajuda a identificar e remover vírus, spyware e outros softwares mal-intencionados. O Antimalware da Microsoft fornece alertas configuráveis conhecido tooinstall de tentativas de software mal-intencionado ou indesejado em si ou executar em seus sistemas do Azure. O Microsoft Antimalware também podem ser implantado usando a Central de Segurança do Azure

### <a name="hardware-security-module"></a>Módulos de segurança de hardware
Autenticação e criptografia não melhorar a segurança, a menos que Olá as próprias chaves são protegidas. Você pode simplificar o gerenciamento de saudação e segurança de chaves e segredos críticos, armazenando-os em [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis). Cofre de chaves fornece Olá opção toostore suas chaves nos padrões do hardware Security tooFIPS certificados de HSMs (módulos) 140-2 nível 2. Suas chaves de criptografia do SQL Server para backup ou [Transparent Data Encryption](https://msdn.microsoft.com/library/bb934049.aspx) podem ser armazenadas no Cofre de Chaves com quaisquer chaves ou segredos dos seus aplicativos. Permissões e acesso toothese protegido itens são gerenciados por meio de [Active Directory do Azure](https://azure.microsoft.com/documentation/services/active-directory/).

### <a name="virtual-machine-backup"></a>Backup de máquinas virtuais
O [Backup do Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) é uma solução que protege os dados do seu aplicativo com zero investimento de capital e custos operacionais mínimos. Erros de aplicativo podem corromper os dados e erros humanos podem introduzir erros em seus aplicativos que podem levar a problemas de toosecurity. Com o Backup do Azure, suas máquinas virtuais executando Windows e Linux estão protegidas.

### <a name="azure-site-recovery"></a>Azure Site Recovery
Uma parte importante da sua organização [recuperação de desastres/continuidade de negócios (BCDR)](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) estratégia é descobrir como tookeep cargas de trabalho corporativa e aplicativos de backup e em execução quando planejado e não planejado ocorre. O [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) ajuda a orquestrar a replicação, failover e recuperação dos aplicativos e cargas de trabalho para que eles estejam disponíveis a partir de um local secundário, caso o local principal fique inativo.

### <a name="sql-vm-tde"></a>TDE de VM do SQL
[TDE (Transparent Data Encryption)](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-keyvault) e CLE (criptografia de nível de coluna) são recursos de criptografia do SQL Server. Essa forma de criptografia requer armazenamento e os clientes toomanage Olá chaves de criptografia usado para criptografia.

Olá serviço Azure Key Vault (AKV) é projetado tooimprove Olá segurança e o gerenciamento dessas chaves em um local seguro e altamente disponível. Olá conector do SQL Server permite toouse do SQL Server que essas chaves do Cofre de chaves do Azure.

Se você estiver executando o SQL Server com máquinas locais, há etapas que você pode seguir tooaccess Azure Key Vault da máquina local do SQL Server. Mas, para SQL Server em máquinas virtuais do Azure, você pode economizar tempo usando o recurso de integração do Azure Key Vault hello. Com alguns tooenable de cmdlets do PowerShell do Azure esse recurso, você pode automatizar Olá seu Cofre de chaves de configuração necessárias para uma VM do SQL tooaccess.

### <a name="vm-disk-encryption"></a>Criptografia de disco da VM
O [Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) é um novo recurso que ajuda a criptografar os discos de suas máquinas virtuais IaaS Windows e Linux. Aplica-se Olá setor padrão BitLocker recursos do Windows e Olá DM Crypt Linux tooprovide da criptografia do volume para Olá SO e discos de dados de saudação. solução de saudação é integrada ao Azure Key Vault toohelp controlar e gerenciar chaves de criptografia de disco hello e segredos em sua assinatura do Cofre de chaves. solução de saudação também garante que todos os dados em discos de máquina virtual Olá sejam criptografados em repouso no armazenamento do Azure.

### <a name="virtual-networking"></a>Rede Virtual
As máquinas virtuais precisam de conectividade de rede. toosupport esse requisito, o Azure requer toobe de máquinas virtuais conectada tooan rede Virtual do Azure. Uma rede Virtual do Azure é um constructo lógico criado com base em malha de rede do Azure física hello. Cada [Rede Virtual do Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) lógica é isolada das todas as outras Redes Virtuais do Azure. Esse isolamento ajuda a garantir que o tráfego de rede em suas implantações não é os clientes do Microsoft Azure tooother acessível.

### <a name="patch-updates"></a>Atualizações de patch
Atualizações de patch fornecem a base de saudação para encontrar e corrigir problemas em potencial e simplificar o processo de gerenciamento de atualização de software hello, reduzindo o número de saudação de atualizações de software, que você deve implantar em sua empresa e aumentando a capacidade toomonitor conformidade.

### <a name="security-policy-management-and-reporting"></a>Gerenciamento de política de segurança e emissão de relatórios
[Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) ajuda a evitar, detectar e responder toothreats e fornece maior visibilidade e controle, segurança de saudação de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

### <a name="azure-security-center"></a>Central de Segurança do Azure
Central de segurança ajuda a evitar, detectar e reagir toothreats com maior visibilidade e controle sobre a segurança de saudação de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

## <a name="identify-and-access-management"></a>Gerenciamento de identidade e de acesso

A proteção de sistemas, aplicativos e dados começa com controles de acesso baseados em identidade. saudação de identidade e acesso recursos de gerenciamento que são criados em produtos e serviços Microsoft business ajudam a proteger suas informações pessoais e organizacionais contra acesso não autorizado, tornando disponíveis toolegitimate usuários onde e quando que precisam.

### <a name="secure-identity"></a>Proteção da identidade
A Microsoft usa várias tecnologias e práticas de segurança em seus produtos e a identidade dos serviços toomanage e acesso.
-   [Autenticação multifator](https://azure.microsoft.com/services/multi-factor-authentication/) requer usuários toouse vários métodos de acesso, local e na nuvem de saudação. Ela fornece uma autenticação forte com uma gama de opções de verificação simples, e proporciona ao usuários um processo de logon simples.

-   O [Microsoft Authenticator](https://aka.ms/authenticator) fornece uma experiência simples de Autenticação Multifator que funciona com o Microsoft Azure Active Directory e com contas da Microsoft, além de incluir suporte para itens vestíveis e aprovações com base em impressão digital.

-   [Imposição de política de senha](https://azure.microsoft.com/documentation/articles/active-directory-passwords-policy/) aumenta Olá segurança de senhas tradicionais, impondo requisitos de tamanho e complexidade, forçados a rotação periódica, e tentativas de bloqueio de conta após a autenticação com falha.

-   A [Autenticação baseada em token](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) permite a autenticação por meio do AD FS (Serviços de Federação do Active Directory) ou sistemas de token seguros de terceiros.

-   [Controle de acesso baseado em função (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/) habilita toogrant acesso com base em saudação do usuário atribuído a função, tornando fácil toogive usuários somente Olá quantidade de acesso que precisam tooperform seus trabalhos. Você pode personalizar o RBAC de acordo com o modelo de negócios e da tolerância a riscos de sua organização.

-   [Gerenciamento de identidade (identidade híbrida) integrado](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/) permite que você toomaintain o controle de acesso de usuários em plataformas de data centers e nuvem internas, criando uma identidade de usuário único para autenticação e autorização tooall recursos.

### <a name="secure-apps-and-data"></a>Aplicativos e dados seguros
[Active Directory do Azure](https://azure.microsoft.com/services/active-directory/), uma abrangente de identidade e acesso nuvem solução de gerenciamento, ajuda toodata acesso seguro no aplicativo no site e na nuvem hello e simplifica o gerenciamento de saudação de usuários e grupos. Ele combina serviços de diretório principal, avançados de controle de identidade, segurança e gerenciamento de acesso do aplicativo e torna mais fácil para os desenvolvedores toobuild baseado em políticas para gerenciamento de identidade em seus aplicativos. tooenhance Active Directory do Azure, você pode adicionar recursos pagos usando as edições do Active Directory Basic do Azure Premium P1 e P2 Premium Olá.

| Recursos gratuitos/comuns     | Recursos básicos    |Recursos do Premium P1 |Recursos do Premium P2 | Ingresso do Active Directory do Azure - apenas para recursos relacionados ao Windows 10|
| :------------- | :------------- |:------------- |:------------- |:------------- |
|   [Objetos de diretório](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#directory-objects), [(Adicionar/atualizar/excluir) de gerenciamento de usuário/grupo / usuário provisionamento, o registro de dispositivos](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#usergroup-management-addupdatedelete-user-based-provisioning-device-registration), [Single Sign-On (SSO)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#single-sign-on-sso), [autoatendimento Alteração de senha para usuários de nuvem](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-change-for-cloud-users), [Connect (mecanismo de sincronização que estende o tooAzure de diretórios locais do Active Directory)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-sync-engine-that-extends-on-premises-directories-to-azure-active-directory), [segurança / relatórios de uso](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#securityusage-reports)       |     [Gerenciamento/provisionamento de acesso baseado em grupo](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#group-based-access-managementprovisioning), [Redefinição de senha por autoatendimento para usuários de nuvem](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-reset-for-cloud-users), [Identidade visual da empresa (personalização do painel de acesso/páginas de logon)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#company-branding-logon-pagesaccess-panel-customization), [Proxy de Aplicativo](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#application-proxy), [SLA de 99,9%](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#sla-999) |  [Gerenciamento de grupo e aplicativo por autoatendimento/adições de aplicativo por autoatendimento/Grupos dinâmicos](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-group), [Redefinição/alteração/desbloqueio de senha por autoatendimento com write-back local](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-resetchangeunlock-with-on-premises-write-back), [Autenticação Multifator (local e na nuvem [Servidor de MFA])](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#multi-factor-authentication-cloud-and-on-premises-mfa-server), [MIM CAL + Servidor MIM](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mim-cal-mim-server), [Cloud App Discovery](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#cloud-app-discovery), [Connect Health](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-health), [Subreposição automática de senha para contas de grupo](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#automatic-password-rollover-for-group-accounts)|     [Proteção de identidade](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-identityprotection), [Privileged Identity Management](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure)|    [Ingressar em um dispositivo tooAzure AD, SSO de área de trabalho, o Microsoft Passport para AD do Azure, a recuperação do Bitlocker de administrador](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#join-a-device-to-azure-ad-desktop-sso-microsoft-passport-for-azure-ad-administrator-bitlocker-recovery), [MDM-registro automático, a recuperação do Bitlocker de autoatendimento, os administradores locais adicionais tooWindows 10 dispositivos por meio do Azure Associação de AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mdm-auto-enrollment)|


- [Cloud App Discovery](https://docs.microsoft.com/azure/active-directory/active-directory-cloudappdiscovery-whatis) é um recurso premium do Active Directory do Azure que permite que aplicativos de nuvem tooidentify que são usados por funcionários de saudação em sua organização.

- [Proteção contra identidade Active Directory do Azure](https://azure.microsoft.com/documentation/articles/active-directory-identityprotection/) é um serviço de segurança que usa o Active Directory do Azure anomalias detecção recursos tooprovide uma exibição consolidada em eventos de risco e possíveis vulnerabilidades que poderiam afetar seus identidades da organização.

- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds/) permite toojoin VMs do Azure tooa domínio sem necessidade de saudação toodeploy controladores de domínio. Os usuários entram toothese VMs usando suas credenciais corporativas do Active Directory e podem acessar diretamente os recursos.

- [B2C de diretório ativo do Azure](https://azure.microsoft.com/services/active-directory-b2c/) é um serviço de gerenciamento de identidade altamente disponível e globais para aplicativos voltados para o consumidor que podem dimensionar toohundreds de milhões de identidades e integrar entre móveis e web plataformas. Os clientes podem entrar tooall seus aplicativos por meio de experiências personalizáveis que usam as contas existentes de mídia social, ou você pode criar novas credenciais autônomo.

- [Colaboração do Azure de B2B do Active Directory](https://aka.ms/aad-b2b-collaboration) é uma solução de integração de parceiros seguros que suporta as relações entre empresas, permitindo a parceiros tooaccess seus aplicativos e dados corporativos seletivamente usando seus autogerenciada identidades.

- [Azure junção do Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/) permite que dispositivos de tooWindows 10 de recursos de nuvem de tooextend para o gerenciamento centralizado. Ele possibilita que os usuários tooconnect toohello corporativas ou organizacionais nuvem por meio do Active Directory do Azure e simplifica o acesso tooapps e recursos.

- [Proxy de Aplicativo do Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/) fornece SSO e acesso remoto seguro para aplicativos da Web hospedados no local.

## <a name="next-steps"></a>Próximas etapas
- [Introdução à Segurança do Microsoft Azure](https://docs.microsoft.com/azure/security/azure-security-getting-started)

Os serviços do Azure e recursos que você pode usar toohelp protegem seus serviços e dados no Azure

- [Central de Segurança do Azure](https://azure.microsoft.com/services/security-center/)

Evitar, detectar e responder toothreats com maior visibilidade e controle sobre a segurança de saudação de seus recursos do Azure

- [Monitoramento da integridade de segurança na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-monitoring)

Olá recursos de monitoramento em conformidade de toomonitor Central de segurança do Azure com as políticas.
