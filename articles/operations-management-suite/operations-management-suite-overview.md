---
title: "aaaOperations visão geral do Management Suite (OMS) | Microsoft Docs"
description: "O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem.  Este artigo descreve o valor de saudação do OMS, identifica Olá diferentes serviços e ofertas incluídas no OMS e fornece links tootheir detalhadas conteúdo."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>O que é Operations Management Suite (OMS)?
Este artigo fornece uma introdução tooOperations Management Suite (OMS) incluindo uma visão geral de valor comercial de saudação fornece, soluções de gerenciamento e os serviços de saudação inclui e ofertas de saudação que reúnem diferentes serviços e soluções.  Links são incluídos toohello detalhadas documentação sobre implantação e uso de cada serviço e a solução.

## <a name="from-on-premises-toohello-cloud"></a>Da nuvem de toohello local
A Microsoft vem há tempos oferecendo produtos para gerenciar ambientes corporativos.  Vários produtos foram consolidados em um conjunto de produtos de gerenciamento do System Center de saudação em 2007.  Isso incluído Configuration Manager que fornece recursos como distribuição de software e inventário, Operations Manager, que fornece monitoramento proativo de sistemas e aplicativos, Orchestrator que inclui processos manuais de tooautomate runbooks e o Data Protection Manager para backup e recuperação de dados críticos.

Com mais de recursos de computação movendo nuvem toohello, produtos do System Center decorrente mais recursos de nuvem, como o Operations Manager e do Orchestrator gerenciamento de recursos no Azure.  No entanto, eles foram projetados como soluções locais e exigem um investimento significativo na implantação e manutenção do ambiente de gerenciamento local.  toocompletely aproveitar a nuvem hello e suporte futuro aplicativos, um novo toomanagement de abordagem era necessária.

## <a name="introducing-operations-management-suite"></a>Apresentamos o Operations Management Suite
Operations Management Suite (também conhecido como o OMS) é uma coleção de serviços de gerenciamento que foram criados na nuvem de saudação do início da saudação.  Em vez de implantar e gerenciar recursos locais, os componentes do OMS estão totalmente hospedados no Azure.  A configuração é mínima e você pode ter tudo funcionando literalmente em questão de minutos.  

- **Custo mínimo e complexidade da implantação.**  Como todos os componentes de saudação e dados para o OMS são armazenados no Azure, você poderá ter backup e em execução em um curto período de tempo sem complexidade hello e o investimento em local componentes.
- **Níveis de toocloud de escala.**  Você não tem tooworry sobre o pagamento de recursos de computação que você não precisa ou sobre a falta de espaço de armazenamento desde Olá nuvem permite que você toopay apenas para o que você realmente usa e prontamente dimensionará carga tooany que precisar.  Você pode gerenciar alguns tooget recursos iniciado e, em seguida, expandir tooyour todo o ambiente.
- **Aproveite os recursos mais recentes de saudação.**  Os recursos nos serviços do OMS estão sendo adicionados e atualizados constantemente.  Você tem constantemente recursos mais recentes do acesso toohello sem nenhuma atualização de toodeploy requisito.
- **Serviços integrados.**  Embora cada um dos serviços do OMS Olá fornecem valor significativo por conta própria, eles podem trabalhar juntos toosolve cenários de gerenciamento complexas.  Por exemplo, um runbook na automação do Azure pode orientar um processo de failover com o Azure Site Recovery e efetue informações tooLog análise toogenerate um alerta.
- **Conhecimento global.**  Soluções de gerenciamento do OMS continuamente tem informações mais recentes de toohello de acesso.  Olá solução segurança e auditoria, por exemplo, pode executar uma análise da ameaça detectadas ao redor Olá, mundo de ameaças mais recentes do hello.
- **Acesso de qualquer lugar.**  Acesse seu ambiente de gerenciamento em qualquer lugar com um navegador.  Instale o aplicativo OMS do hello em seu smartphone para dados de monitoramento de tooyour acesso imediato.

### <a name="is-it-just-for-hello-cloud"></a>É apenas para a nuvem Olá?
Só porque os serviços OMS são executados em nuvem Olá não significa que eles não podem gerenciar efetivamente seu ambiente local.  Colocar um agente em qualquer Windows ou computador Linux no seu data center e enviará dados tooLog Analytics onde ele pode ser analisado junto com todos os outros dados coletados dos serviços de nuvem ou local.  Use a nuvem de saudação tooleverage Backup do Azure e o Azure Site Recovery para backup e alta disponibilidade para recursos locais.  
Runbooks na nuvem Olá normalmente não é possível acessar os recursos locais, mas você pode instalar um agente em um ou mais computadores muito que hospedará os runbooks em seu data center.  Quando você inicia um runbook, você simplesmente Especifica se você deseja que ele toorun na nuvem hello, ou em um local de trabalho.

## <a name="hybrid-management-with-system-center"></a>Gerenciamento híbrido com o System Center
Se você tiver uma instalação existente do System Center, você pode integrar esses componentes com o OMS serviços tooprovide uma solução híbrida para seus locais e aproveitando especialidades de saudação relativa de cada produto de ambientes de nuvem.  Conecte seu existentes agentes do Operations Manager gerenciamento grupo tooLog análise tooanalyze gerenciado na nuvem hello.  Use o processo de backup existente com o Data Protection Manager toobackup toohello seus dados na nuvem.  


## <a name="oms-services"></a>Serviços do OMS
funcionalidade de núcleo de saudação do OMS é fornecida por um conjunto de serviços que são executados no Azure.  Cada serviço fornece uma função de gerenciamento específico, e você pode combinar os cenários de gerenciamento diferente de tooachieve de serviços.

|| O Barramento de | serviço |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | Monitorar e analisar a disponibilidade de saudação e o desempenho de recursos diferentes, incluindo físicos e máquinas virtuais. |
| ![Automação do Azure](media/operations-management-suite-overview/icon-automation.png) | Automação | Automatizar processos manuais e impor configurações de máquinas físicas e virtuais. |
| ![Serviço de Backup do Azure](media/operations-management-suite-overview/icon-backup.png) | Backup | Backup e restauração de dados críticos. |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | Recuperação de Site | Fornecer alta disponibilidade para aplicativos críticos. |

### <a name="log-analytics"></a>Log Analytics
O [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) fornece serviços de monitoramento para o OMS coletando dados de recursos gerenciados em um repositório central.  Esses dados podem incluir eventos, dados de desempenho ou dados personalizados fornecidos por meio da API de saudação. Depois de coletados, dados saudação estão disponíveis para alertas, análise e exportação.  Esse método permite tooconsolidate dados de uma variedade de fontes de forma que você pode combinar dados de seus serviços do Azure com seu ambiente local existente.  Ele também separa coleção Olá dos dados Olá pela ação de saudação executada com os dados para que todas as ações disponíveis tooall tipos de dados.  

![Visão geral do Log Analytics](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>Coletando dados
Há várias maneiras que você pode obter dados no repositório de saudação para tooanalyze de análise de Log.

- **Computadores Windows ou Linux e máquinas virtuais.**  Instalar Olá Microsoft Monitoring Agent em [Windows](../log-analytics/log-analytics-windows-agents.md) e [Linux](../log-analytics/log-analytics-linux-agents.md) computadores ou máquinas virtuais que você deseja toocollect dados.  Agente de saudação baixará automaticamente da configuração de análise de Log que define os eventos e toocollect de dados de desempenho.  Você pode instalar facilmente agente Olá em máquinas virtuais em execução no Azure usando Olá portal do Azure.  Se você tiver um ambiente existente do Operations Manager, pode conectar tooLog de grupo de gerenciamento Olá análise e iniciar automaticamente a coleta de dados em todos os agentes.
- **Serviços do Azure.**  Análise de log coleta a telemetria de [diagnóstico do Azure e o monitoramento do Azure](../log-analytics/log-analytics-azure-storage.md) no repositório de saudação para que você possa monitorar os recursos do Azure.
- **API do Coletor de Dados.**  O Log Analytics tem uma [API REST para preenchimento de dados de qualquer cliente](../log-analytics/log-analytics-data-collector-api.md).  Isso permite que os dados de toocollect aplicativos de terceiros ou implementar cenários de gerenciamento personalizado.  Um método comum é toouse um runbook em dados de toocollect de automação do Azure e, em seguida, usar Olá API do coletor de dados toowrite-toohello repositório.

#### <a name="reporting-and-analyzing-data"></a>Emissão de relatórios e análise de dados
Análise de log inclui um consulta poderosa linguagem tooextract de dados armazenado no repositório de saudação.  Como os dados de todas as fontes são armazenados como registros, você pode analisar dados de várias fontes em uma única consulta.
  
Além disso, tooad hoc análise, análise de Log fornece tooreport de várias maneiras e analisar dados de uma consulta.

- **Modos de exibição e painéis.**  [Modos de exibição](../log-analytics/log-analytics-view-designer.md) e [painéis](../log-analytics/log-analytics-dashboards.md) visualizar os resultados de saudação de uma consulta no portal de saudação.  Soluções de gerenciamento normalmente incluirá exibições que analisam dados saudação da solução hello.  Você também pode criar suas próprias exibições personalizadas tooanalyze dados e torná-lo prontamente disponível no seu portal personalizado.
- **Exportação.**  Você tem resultados de saudação do hello opção tooexport de qualquer consulta para que possa analisá-los fora da análise de Log.  Você também pode programar uma exportação regular muito[Power BI](../log-analytics/log-analytics-powerbi.md) que fornece recursos de visualização e análise significativos.
- **API da Pesquisa de Logs.**  O Log Analytics tem uma [API REST para coletar dados de qualquer cliente](../log-analytics/log-analytics-log-search-api.md).  Isso permite que você tooprogrammatically trabalho com os dados coletados no repositório de saudação ou acessá-lo de outra ferramenta de monitoramento.

#### <a name="alerting"></a>Alertas
O Log Analytics pode [alertá-lo proativamente](../log-analytics/log-analytics-alerts.md) ou tomar uma ação corretiva quando detecta um problema.  Como todas as outras análises no Log Analytics, isso é feito com uma pesquisa de logs.  Esta pesquisa é executada em um agendamento regular, e um alerta será criado se resultados Olá correspondem a critérios específicos.

![Alertas do Log Analytics](media/operations-management-suite-overview/overview-alerts.png)

Além disso toocreating um registro de alerta no repositório de análise de Log hello, alertas podem levar Olá ações a seguir.

- **Email.**  Enviar um email tooproactively notificá-lo de um problema detectado.
- **Runbook.**  Um alerta no Log Analytics pode iniciar um runbook na Automação do Azure.  Isso geralmente é feito o problema do tooattempt toocorrect Olá detectado.  Olá runbook pode ser iniciado na nuvem de saudação na Olá caso de um problema no Azure ou outra nuvem ou pôde ser iniciado em um agente local para um problema em um computador físico ou virtual.
- **Webhook.**  Um alerta pode iniciar um webhook e passar dados de resultados de saudação de pesquisa de log de saudação.  Isso permite a integração com serviços externos, como um sistema de alerta alternativo, ou ele pode tentar tootake uma ação corretiva para um site externo.

### <a name="azure-automation"></a>Automação do Azure
[Automação do Azure](http://azure.microsoft.com/documentation/services/automation) fornece tooOMS de gerenciamento de configuração e automação de processo.  Ela automatiza processos manuais e ajuda a tooenforce configurações para computadores físicos e virtuais.  

#### <a name="process-automation"></a>Automação de processos
A Automação do Azure automatiza processos manuais usando [runbooks](../automation/automation-runbook-types.md) que são baseados em script ou fluxo de trabalho do PowerShell.  Ele também inclui suporte runbooks, como variáveis que podem ser compartilhadas entre vários runbooks e as credenciais e conexões que permitem a você informações toostore criptografado que podem ser necessárias para um runbook para autenticação de ativos.
Runbooks oferecem a automação de processo para Olá outros serviços no pacote de saudação.  Desde que cada Olá outros serviços podem ser acessados com o PowerShell ou por meio de uma API REST, você pode criar runbooks tooperform funções, como coleta de dados de gerenciamento de análise de Log ou iniciar um backup com o Backup do Azure.

##### <a name="accessing-resources"></a>Acessando recursos
Como os runbooks são baseados no PowerShell, eles podem gerenciar qualquer recurso que possa ser acessado com cmdlets do PowerShell.  Quando você [carregar um módulo](../automation/automation-integration-modules.md) em sua conta de automação, ele se torna disponível tooall runbooks nessa conta. 
 
Quando executar runbooks na nuvem hello, eles podem acessar todos os recursos acessíveis da nuvem de saudação.  Isso pode ser recursos na sua assinatura do Azure, em outra nuvem, como o AWS (Amazon Web Services) ou um serviço acessível por uma API REST.  Runbooks na nuvem Olá não são executados sob as credenciais, mas eles podem aproveitar os ativos de automação, como certificados tooauthenticate tooresources acessarem, conexões e credenciais.

Recursos em seu data center provavelmente não podem ser acessados de um runbook em execução na nuvem hello.  Você pode instalar um ou mais [Hybrid Runbook Workers](../automation/automation-hybrid-runbook-worker.md) em seus dados center embora runbooks toorun que precisam acessar os recursos toolocal.  Quando você inicia um runbook, você especificar se deve ser executado na nuvem hello, ou em um trabalho específico.

![Runbooks da Automação do Azure](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>Iniciando um runbook
Os runbooks podem ser [iniciados por vários métodos](../automation/automation-starting-a-runbook.md) para que eles possam ser incluídos em vários cenários de gerenciamento.  

- **Portal do Azure.**  Como outros serviços do Azure, a automação do Azure podem ser gerenciada de saudação Portal do Azure.  Além disso toostarting runbooks, você pode importá-los ou criar seus próprios.
- **Agendado.**  Você pode agendar runbooks toostart em intervalos regulares.  Isso permite que você tooautomatically repetir um processo de gerenciamento regular ou coletar dados tooLog análise.
- **PowerShell e API.**  Você pode iniciar runbooks e passe-los necessárias informações de parâmetro de um cmdlet do PowerShell ou Olá API de REST de automação do Azure.  
- **Webhook.**  Um webhook pode ser criado para qualquer runbook que permite que ele toobe iniciado a partir de sites da web ou aplicativos externos.
- **Alerta do Log Analytics.**  Um alerta na análise de Log pode iniciar automaticamente um problema de saudação runbook tooattempt toocorrect identificado pelo alerta hello.

#### <a name="configuration-management"></a>Gerenciamento de configuração
[Configuração de estado desejado (DSC) da PowerShell](../automation/automation-dsc-overview.md) é uma plataforma de gerenciamento do Windows PowerShell que permite que você toodeploy e aplicar a configuração de saudação do físicos e máquinas virtuais.  Automação do Azure gerencia configurações DSC e fornece um servidor de pull na nuvem Olá que agentes possam acessar configurações de tooretrieve necessário.

![DSC de Automação do Azure](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Backup do Azure e Azure Site Recovery
Azure Backup e recuperação de Site do Azure contribuem toobusiness continuidade e recuperação de desastres.  Cada um deles tem recursos que ajudam você a tooensure que os aplicativos permaneçam disponíveis quando interrupções ocorrem e retornam toonormal operações quando sistemas voltam a ficar online.  Ambos os serviços de colaboração toohello objetivos de ponto de recuperação (RPOs) e objetivos de tempo de recuperação (RTOs) definidos pela sua organização. O RPO define o limite aceitável de saudação em que dados não estão disponíveis durante uma interrupção, e Olá RTO limita Olá aceitável período de tempo em que um serviço ou aplicativo não está disponível durante uma interrupção.

#### <a name="azure-backup"></a>Serviço de Backup do Azure
[O Backup do Azure](http://azure.microsoft.com/documentation/services/backup) oferece backup de dados e serviços de restauração para o OMS.  Ele protege seus dados de aplicativos e os retém por vários anos, sem nenhum investimento de capital e custos operacionais mínimos.  Ele pode fazer o backup de dados de servidores físicos e virtuais do Windows em cargas de trabalho adição tooapplication como o SQL Server e SharePoint.  Ele também pode ser usado por tooAzure de dados do System Center Data Protection Manager (DPM) tooreplicate protegido para armazenamento de longo prazo e redundância.

Os dados protegidos no Backup do Azure são armazenados em um cofre de backup localizado em uma região geográfica específica. Olá dados são replicados dentro Olá mesma região e, dependendo do tipo de saudação do cofre, também pode ser o região tooanother replicados para garantir a resiliência adicional.

O Backup do Azure apresenta três cenários fundamentais.

- **Computador com Windows com o Agente de Backup do Azure.** Fazer backup de arquivos e pastas a partir de qualquer cliente ou o Windows server diretamente tooyour Cofre de backup do Azure.<br><br>![Computador com Windows com o Agente de Backup do Azure](media/operations-management-suite-overview/overview-backup-01.png)
- **DPM (System Center Data Protection Manager) ou Servidor de Backup do Microsoft Azure.** Aproveite o DPM Microsoft Azure Backup Server toobackup arquivos e pastas ou em cargas de trabalho adição tooapplication como o armazenamento de toolocal SQL e SharePoint e, em seguida, replicar tooyour Cofre de backup do Azure. Suporte a máquinas virtuais Windows e Linux Hyper-V ou VMware.<br><br>![DPM (System Center Data Protection Manager) ou Servidor de Backup do Microsoft Azure](media/operations-management-suite-overview/overview-backup-02.png)
- **Extensões da Máquina Virtual do Azure.** Backup Windows ou Linux virtual máquinas tooyour Azure Cofre de backup do Azure.<br><br>![Extensões da Máquina Virtual do Azure](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[O Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) fornece continuidade dos negócios ao orquestrar a replicação do local virtual e máquinas físicas tooAzure ou site secundário tooa. Se seu site primário não estiver disponível, você failover local secundário toohello para que os usuários podem continuar trabalhando e failback quando sistemas retornam tooworking ordem. 

O Azure Site Recovery fornece alta disponibilidade para servidores e aplicativos.  Ele contribui com uma estratégia de recuperação (BCDR) de desastre e continuidade de negócios tooyour ao orquestrar a replicação, failover e recuperação de máquinas de virtuais de Hyper-V locais, máquinas virtuais VMware e servidores físicos do Windows/Linux. Você pode replicar máquinas tooa data center secundário ou ampliar seu datacenter ao replicá-lo tooAzure. A Recuperação de Site também fornece failover e recuperação simples para cargas de trabalho. Ela integra mecanismos de recuperação de desastre, como o SQL Server AlwaysOn, e fornece planos de recuperação para failover fácil de cargas de trabalho que são organizadas em camadas em vários computadores.

O Azure Site Recovery apresenta três cenários fundamentais de replicação.

- **Replicação de máquinas virtuais Hyper-V.**  Se as máquinas virtuais Hyper-V são gerenciadas em nuvens do VMM, você pode replicar tooa secundário data center ou tooAzure armazenamento. TooAzure de replicação é uma conexão segura de internet. Data Center secundário de tooa de replicação é Olá LAN.  Se as máquinas virtuais Hyper-V não são gerenciadas pelo VMM, você pode replicar somente o armazenamento tooAzure. TooAzure de replicação é uma conexão segura de internet.<br><br>![Replicação de máquinas virtuais Hyper-V](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **Replicação de máquinas virtuais VMWare.**  Você pode replicar VMware máquinas virtuais tooa data center secundário executando o VMware ou tooAzure de armazenamento. TooAzure de replicação pode ocorrer através de uma VPN de site a site ou rota expressa do Azure ou em uma conexão segura de Internet. Data Center secundário de tooa de replicação ocorre sobre Olá canal de dados do InMage Scout.<br><br>![Replicação de máquinas virtuais VMWare](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **Replicação de servidores físicos Windows e Linux**  Você pode replicar os servidores físicos tooa datacenter ou tooAzure armazenamento secundário. TooAzure de replicação pode ocorrer através de uma VPN de site a site ou rota expressa do Azure ou em uma conexão segura de Internet. Data Center secundário de tooa de replicação ocorre sobre Olá canal de dados do InMage Scout. O Azure Site Recovery tem uma solução do OMS que exibe algumas estatísticas, mas você deve usar o hello portal do Azure para qualquer operação.<br><br>![Replicação de servidores físicos do Windows e Linux](media/operations-management-suite-overview/overview-siterecovery-physical.png)


A Recuperação de Site armazena os metadados em cofres localizados em determinada região geográfica do Azure. Nenhum dado replicado é armazenado pelo Olá serviço de recuperação de Site.

## <a name="management-solutions"></a>Soluções de gerenciamento
[Soluções de gerenciamento](operations-management-suite-solutions.md) são conjuntos de lógica pré-empacotados que implementam um cenário de gerenciamento específico utilizando um ou mais serviços do OMS.  Soluções diferentes estão disponíveis da Microsoft e de parceiros que você pode adicionar facilmente tooyour assinatura do Azure tooincrease Olá valor seu investimento do OMS.  Como um parceiro, você pode criar sua próprias soluções toosupport seus aplicativos e serviços e fornecê-los toousers por meio de saudação do Azure Marketplace ou modelos de início rápido.

Um bom exemplo de uma solução que utiliza vários recursos adicionais de tooprovide de serviços é hello [solução de gerenciamento de atualização de](oms-solution-update-management.md).  Esta solução usa o agente de análise de Log Olá para Windows e Linux toocollect obter informações sobre as atualizações necessárias em cada agente.  Ele grava esse repositório de análise de Log de toohello dados onde você pode analisar com um painel incluído.  Quando você cria uma implantação, runbooks na automação do Azure são usados tooinstall necessárias atualizações.  Gerenciar todo o processo no portal de saudação e não é necessário tooworry sobre detalhes subjacentes hello.

![Solução](media/operations-management-suite-overview/overview-solution.png)

A maioria das soluções podem executar um ou mais dos Olá funções a seguir.

- Recolher Informações adicionais.  O Log Analytics reúne uma variedade de dados de clientes e serviços, incluindo dados de desempenho e eventos.  Uma solução de gerenciamento pode coletar informações adicionais não disponibilizadas por outras fontes de dados, geralmente usando runbooks da Automação do Azure.
- Fornecer análise adicional das informações coletadas.  As soluções de gerenciamento incluem painéis e modos de exibição que permitem a análise e a visualização dos dados.  Essas pesquisas de log de backup toopredefined link que permitem a você toodrill em hello dados detalhados.  Eles também podem executar análise em dados que já foram coletados no repositório de hello, por exemplo, pesquisa em eventos de segurança de padrões que indicam uma ameaça.
- Adicionar funcionalidade.  Algumas soluções fornecidas pela Microsoft poderão compilar suas capacidades de saudação da funcionalidade adicional do tooprovide Olá core services.  Por exemplo, mapa de serviço fornece seu próprio console toodiscover e mapeia o servidor e as dependências de processo em tempo real.
Soluções regularmente são adicionadas tooOMS pela Microsoft e parceiros, permitindo que você toocontinuously aumentam o valor de saudação do seu investimento.  Você pode procurar e instalar soluções da Microsoft por meio de saudação catálogo de soluções no portal do OMS hello ou procurar e instalar soluções de parceiros e da Microsoft por meio de hello Azure Marketplace em Olá Portal do Azure.  

![Galeria de Soluções](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Saiba mais sobre a [Automação do Azure](../automation/automation-intro.md).
* Saiba mais sobre o [Backup do Azure](http://azure.microsoft.com/documentation/services/backup).
* Saiba mais sobre o [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).
* Descobrir Olá [soluções disponíveis](../log-analytics/log-analytics-add-solutions.md) nas diferentes ofertas de OMS hello. 

