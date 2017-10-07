---
title: "aaaUpdate solução de gerenciamento do OMS | Microsoft Docs"
description: "Este artigo é pretendido toohelp você entender como toouse toomanage essa solução de atualizações para os computadores Windows e Linux."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>Solução Gerenciamento de Atualizações no OMS

![Símbolo de Gerenciamento de Atualizações](./media/oms-solution-update-management/update-management-symbol.png)

saudação de solução de gerenciamento de atualizações no OMS permite que você toomanage atualizações de segurança do sistema operacional para os computadores Windows e Linux implantados no Azure, no local ambientes ou outros provedores de nuvem.  Você pode avaliar Olá status de atualizações disponíveis em todos os computadores de agente e gerenciar Olá o processo de instalação das atualizações necessárias para os servidores rapidamente.


## <a name="solution-overview"></a>Visão geral da solução
Computadores gerenciados pelo OMS usam seguinte Olá para realizar implantações de avaliação e atualização:

* Agente do OMS para Windows ou Linux
* DSC (PowerShell Desired State Configuration) para Linux
* Hybrid Runbook Worker de Automação
* Microsoft Update ou Windows Server Update Services para computadores Windows

Olá diagramas a seguir mostra uma exibição conceitual do fluxo de dados e comportamento de saudação com como solução Olá avalia e aplica tooall de atualizações de segurança conectados do Windows Server e computadores Linux em um espaço de trabalho.    

#### <a name="windows-server"></a>Windows Server
![Fluxo de processo de gerenciamento de atualização do Windows Server](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Fluxo do processo de gerenciamento de atualização do Linux](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

Depois que o computador Olá executa uma verificação de conformidade da atualização, o agente do OMS Olá encaminha as informações de Olá em tooOMS em massa. Em um computador de janela, verificação de conformidade de saudação é executada a cada 12 horas por padrão.  Além disso toohello agendamento da verificação, verificação Olá para conformidade de atualização é iniciado dentro de 15 minutos se Olá agente de monitoramento da Microsoft (MMA) é a instalação de tooupdate reiniciados, antes e após a instalação da atualização.  Com um computador Linux, verificação de conformidade de saudação é executada a cada três horas por padrão e uma verificação de conformidade é iniciada dentro de 15 minutos se Olá MMA agent será reiniciado.  

Olá informações de conformidade são processadas e resumidas em painéis de saudação incluídos na solução hello ou pesquisável usando definido pelo usuário ou pré-definidas pelo consultas.  solução Hello relatórios atualizado como Olá computador está com base em qual fonte que estiver configurado toosynchronize com.  Se o computador com Windows hello for tooWSUS tooreport configurado, dependendo de quando o WSUS última sincronização com o Microsoft Update, resultados de saudação podem diferir das que mostra o Microsoft Updates.  Olá mesmo para computadores Linux que estão configuradas tooreport tooa local repositório versus um repositório público.   

Você pode implantar e instalar atualizações de software em computadores que exigem atualizações Olá criando uma implantação agendada.  As atualizações classificadas como *opcional* não são incluídos no escopo da implantação Olá para computadores Windows, somente as atualizações necessárias.  Olá agendado da implantação define quais computadores de destino receberá atualizações aplicáveis hello, explicitamente especificando computadores ou selecionando um [grupo de computadores](../log-analytics/log-analytics-computer-groups.md) que baseia pesquisas de log de um conjunto específico de computadores.  Você também especifica um agendamento tooapprove e designa um período de tempo quando as atualizações são permitidas toobe instalado em.  As atualizações são instaladas por runbooks na Automação do Azure.  Você não consegue exibir esses runbooks e eles não exigem nenhuma configuração.  Quando uma implantação de atualização é criada, ele cria uma agenda que inicia um runbook mestre de atualização em Olá especificado tempo para computadores Olá incluído.  Esse runbook mestre inicia um runbook filho em cada agente que executa a instalação de atualizações necessárias.       

Na data de saudação e hora especificadas na implantação de atualizações de saudação, computadores de destino Olá executa a implantação de saudação em paralelo.  Uma verificação é primeiro tooverify executada Olá ainda são necessárias e instala-os.  É importante toonote para computadores de clientes do WSUS, se Olá atualizações não foram aprovadas no WSUS, implantação de atualização de saudação falhará.  resultados de saudação de atualizações de saudação aplicada são encaminhados tooOMS toobe processados e resumidos em painéis de saudação ou por Olá Pesquisar eventos de saudação.     

## <a name="prerequisites"></a>Pré-requisitos
* Olá solução dá suporte ao executar avaliações de atualização no Windows Server 2008 e superior e no Windows Server 2008 R2 SP1 e superior de implantações de atualização.  Não há suporte para as opções de instalação Server Core e Nano Server.

    > [!NOTE]
    > Suporte para implantação de atualizações tooWindows Server 2008 R2 SP1 requer o .NET Framework 4.5 e WMF 5.0 ou posterior.
    >  
* Não há suporte para sistemas operacionais clientes do Windows.  
* Agentes do Windows devem ser toocommunicate configurado com um servidor Windows Server Update Services (WSUS) ou deve ter acesso tooMicrosoft atualização.  

    > [!NOTE]
    > Olá Windows não pode ser gerenciado por agente simultaneamente pelo System Center Configuration Manager.  
    >
* CentOS 6 (x86/x64) e 7 (x64)  
* Red Hat Enterprise 6 (x86/x64) e 7 (x64)  
* SUSE Linux Enterprise Server 11 (x86/x64) e 12 (x64)  
* Ubuntu 12.04 LTS e posterior x86/x64   
    > [!NOTE]  
    > tooavoid atualizações sendo aplicadas fora da janela de manutenção no Ubuntu, reconfigure as atualizações automáticas de toodisable de pacote de atualização automática. Para obter informações sobre como tooconfigure isso, consulte [tópico atualizações automáticas em Olá Ubuntu Server guia](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).

* Agentes do Linux devem ter o repositório de atualização de tooan de acesso.  

    > [!NOTE]
    > Um agente do OMS para Linux configurado espaços de trabalho do OMS tooreport toomultiple não é suportado com essa solução.  
    >

Para obter informações adicionais sobre como tooinstall hello agente do OMS para Linux e baixar a versão mais recente do hello, consulte muito[Operations Management Suite Agent para Linux](https://github.com/microsoft/oms-agent-for-linux).  Para obter informações sobre como tooinstall Olá agente do OMS para Windows, examine [Operations Management Suite Agent para Windows](../log-analytics/log-analytics-windows-agents.md).  

### <a name="permissions"></a>Permissões
Ordem toocreate atualizar implantações, é necessário toobe função de Colaborador Olá em sua conta de automação e o espaço de trabalho de análise de Log.  

## <a name="solution-components"></a>Componentes da solução
Essa solução consiste em Olá recursos que são adicionados a conta de automação tooyour e agentes conectados diretamente ou grupo de gerenciamento conectados do Operations Manager a seguir.

### <a name="management-packs"></a>Pacotes de gerenciamento
Se o grupo de gerenciamento do System Center Operations Manager for conectado tooan espaço de trabalho do OMS, Olá pacotes de gerenciamento a seguir é instalado no Operations Manager.  Esses pacotes de gerenciamento também são instalados em computadores com Windows conectados diretamente após a adição dessa solução. Não há nada tooconfigure ou gerenciar esses pacotes de gerenciamento.

* Microsoft System Center Advisor Update Assessment Intelligence Pack (Microsoft.IntelligencePacks.UpdateAssessment)
* Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)
* MP de Implantação de Atualizações

Para obter mais informações sobre como os pacotes de gerenciamento da solução são atualizados, consulte [tooLog conectar o Operations Manager análise](../log-analytics/log-analytics-om-agents.md).

### <a name="hybrid-worker-groups"></a>Grupos de Hybrid Worker
Depois de habilitar essa solução, qualquer computador com Windows conectado diretamente tooyour espaço de trabalho do OMS é automaticamente configurado como um Hybrid Runbook Worker toosupport Olá runbooks que incluído nesta solução.  Para cada computador com Windows gerenciado por solução hello, ele será listado na folha de grupos de trabalho de Runbook híbrido Olá Olá da conta de automação seguindo a convenção de nomenclatura Olá *Hostname FQDN_GUID*.  Não é possível direcionar esses grupos com runbooks em sua conta, caso contrário, haverá falha. Esses grupos são apenas pretendido toosupport solução de gerenciamento de saudação.   

No entanto, você pode adicionar o grupo de Hybrid Runbook Worker de tooa do hello Windows computadores em sua conta de automação toosupport runbooks de automação enquanto você estiver usando Olá a mesma conta para solução de saudação e associação de grupo do Hybrid Runbook Worker.  Essa funcionalidade foi adicionada tooversion 7.2.12024.0 de saudação Hybrid Runbook Worker.  

## <a name="configuration"></a>Configuração
Executar Olá etapas tooadd Olá Update Management solution tooyour OMS espaço de trabalho a seguir e confirme os agentes estão se comunicando. Espaço de trabalho do Windows agentes tooyour já conectado são adicionados automaticamente sem nenhuma configuração adicional.

Você pode implantar a solução hello usando Olá métodos a seguir:

* Do Azure Marketplace em Olá portal do Azure, selecionando a oferta de controle e automação hello ou solução de gerenciamento de atualizações
* De saudação Galeria de soluções do OMS no seu espaço de trabalho do OMS

Se você já tiver uma conta de automação e o espaço de trabalho do OMS vinculado juntos em hello mesmo grupo de recursos e região, selecionando o controle e automação serão verificar sua configuração de somente instalar Olá solução e configurá-lo em ambos os serviços.  Selecionar a solução de gerenciamento de atualização de saudação do Azure Marketplace oferece Olá mesmo comportamento.  Se você não tiver os serviços implantados na sua assinatura, siga as etapas de Olá Olá **criar nova solução** folha e confirme que você deseja tooinstall Olá outras selecionado previamente as soluções recomendadas.  Opcionalmente, você pode adicionar tooyour de solução de gerenciamento de atualizações Olá espaço de trabalho do OMS usando Olá etapas descrito em [soluções do OMS adicionar](../log-analytics/log-analytics-add-solutions.md) de saudação Galeria de soluções.  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>Confirme os agentes do OMS e tooOMS de grupo conectado de gerenciamento do Operations Manager

tooconfirm conectado diretamente o agente do OMS para Linux e Windows estão se comunicando com o OMS, após alguns minutos execute Olá pesquisa de log a seguir:

* Linux - `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Windows - `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`

Em um computador com Windows, você pode examinar Olá tooverify conectividade do agente com o OMS a seguir:

1.  Abra o Microsoft Monitoring Agent no painel de controle e, em Olá **Azure Log Analytics (OMS)** guia, hello agent exibirá uma mensagem dizendo: **Olá Microsoft Monitoring Agent se conectou com êxito toohello Microsoft Serviço do consultor**.   
2.  Abra Olá Log de eventos do Windows, navegue muito**aplicativo e o Gerenciador de serviços de Logs\Operations** e procure 3000 de ID de evento e 5002 de fonte de conector de serviço.  Esses eventos indicam computador Olá foi registrado com o espaço de trabalho do hello OMS e está recebendo a configuração.  

Se o agente Olá não é capaz de toocommunicate com hello serviço OMS e é configurado toocommunicate com hello internet através de um servidor proxy ou firewall, confirme Olá firewall ou servidor proxy está configurado corretamente, revisando [rede configuração de agente do Windows](../log-analytics/log-analytics-windows-agents.md#network) ou [configuração de rede para o agente do Linux](../log-analytics/log-analytics-agent-linux.md#network).

> [!NOTE]
> Se seus sistemas Linux são toocommunicate configurado com um proxy ou Gateway do OMS e integração nesta solução, atualize Olá *proxy.conf* grupo de omiuser permissões toogrant Olá permissão de leitura no arquivo hello executar Olá comandos a seguir:  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


Agentes do Linux recém-adicionados mostrarão um status de **Atualizado** após ter sido realizada uma avaliação.  Esse processo pode demorar até too6 horas.

tooconfirm um Gerenciador de operações de grupo de gerenciamento está se comunicando com o OMS, consulte [validar a integração do Operations Manager com OMS](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms).

## <a name="data-collection"></a>Coleta de dados
### <a name="supported-agents"></a>Agentes com suporte
Olá, a tabela a seguir descreve Olá conectado fontes que são suportadas por essa solução.

| Fonte Conectada | Suportado | Descrição |
| --- | --- | --- |
| Agentes do Windows |Sim |solução de saudação coleta informações sobre atualizações do sistema de agentes do Windows e inicia a instalação de atualizações necessárias. |
| Agentes do Linux |Sim |solução de saudação coleta informações sobre atualizações do sistema de agentes Linux e inicia a instalação de atualizações necessárias em distribuições com suporte. |
| Grupo de gerenciamento do Operations Manager |Sim |solução de saudação coleta informações sobre atualizações do sistema de agentes em um grupo de gerenciamento conectados.<br>Uma conexão direta de saudação do Operations Manager agent tooLog análise não é necessária. Dados são encaminhados do repositório de OMS toohello do grupo de gerenciamento de saudação. |
| Conta de Armazenamento do Azure |Não |O armazenamento do Azure não inclui informações sobre atualizações do sistema. |

### <a name="collection-frequency"></a>Frequência de coleta
Para cada computador gerenciado do Windows, uma verificação é executada duas vezes por dia. Olá cada 15 minutos API do Windows é chamada tooquery para Olá última atualização tempo toodetermine se o status mudou e, nesse caso uma verificação de conformidade é iniciada.  Para cada computador Linux gerenciado, uma verificação é executada a cada três horas.

Ele pode levar de 30 minutos a horas too6 dados toodisplay atualizado do painel de saudação de computadores gerenciados.   

## <a name="using-hello-solution"></a>Usando a solução de saudação
Quando você adiciona o espaço de trabalho do hello Update Management solution tooyour OMS, Olá **Update Management** bloco será adicionado tooyour painel do OMS. Este bloco exibe uma contagem e a representação gráfica do número de saudação de computadores em seu ambiente e sua conformidade de atualização.<br><br>
![Bloco de resumo do Gerenciamento de Atualizações](media/oms-solution-update-management/update-management-summary-tile.png)  


## <a name="viewing-update-assessments"></a>Exibição de avaliações de atualização
Clique em Olá **Update Management** bloco tooopen Olá **gerenciamento de atualizações** painel.<br><br> ![Painel Resumo de Gerenciamento de Atualizações](./media/oms-solution-update-management/update-management-dashboard.png)<br>

Esse painel fornece uma análise detalhada do status de atualização categorizado por tipo de sistema operacional e a classificação da atualização: crítica, de segurança ou outros (como uma atualização de definição). resultados de saudação em cada bloco neste painel refletem somente as atualizações aprovadas para implantação, que baseia-se com base na origem de sincronização de computadores hello.   Olá **implantações de atualização** bloco quando selecionado, redireciona toohello página de implantações de atualização em que você pode exibir agendas, implantações em execução no momento, implantações concluídas, ou agendar uma nova implantação.  

Você pode executar uma pesquisa de log que retorna todos os registros clicando no bloco hello ou toorun uma consulta de uma categoria específica e critérios predefinidos, selecione um na lista de saudação disponível em Olá **consultas comuns de atualização** coluna.    

## <a name="installing-updates"></a>Instalação de atualizações
Depois de tem foi avaliadas atualizações para todos os Olá Linux e computadores com Windows em seu espaço de trabalho, você pode ter atualizações necessárias instaladas com a criação de um *implantação de atualização*.  Uma Implantação de Atualizações é uma instalação agendada de atualizações necessárias para um ou mais computadores.  Especifique Olá data e a hora para a implantação de saudação além tooa computador ou grupo de computadores que devem ser incluídos no escopo de saudação de uma implantação.  toolearn mais sobre grupos de computadores, consulte [grupos de computadores na análise de Log](../log-analytics/log-analytics-computer-groups.md).  Quando você incluir grupos de computadores em sua implantação de atualização, memnbership de grupo é avaliada apenas uma vez em tempo de saudação da criação da agenda.  Grupo de tooa alterações subsequentes não serão refletidas.  toowork como alternativa, excluir a implantação de atualização de saudação agendada e recriá-lo.

> [!NOTE]
> Máquinas virtuais do Windows implantada a partir do hello Azure Marketplace por padrão são definidas as atualizações automáticas tooreceive do serviço Windows Update.  Esse comportamento não é alterado depois de adicionar essa solução ou o espaço de trabalho de tooyour de máquinas virtuais do Windows.  Se você fizer atualizações não ativamente gerenciadas com essa solução, Olá comportamento padrão (aplicar automaticamente as atualizações) será aplicada.  

Para máquinas virtuais criadas a partir Olá sob demanda Red Hat Enterprise Linux (RHEL) imagens disponíveis no Azure Marketplace, eles são registrados tooaccess Olá [Red Hat atualização de infraestrutura (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) implantado no Azure.  Qualquer distribuição do Linux deve ser atualizada do repositório de arquivo online de distribuições Olá seus métodos com suporte a seguir.  

### <a name="viewing-update-deployments"></a>Exibição de implantações de atualização
Clique em Olá **implantação de atualização** bloco tooview Olá lista de implantações de atualizações existentes.  Elas são agrupadas por status – **Agendadas**, **Em Execução** e **Concluídas**.<br><br> ![Página de Agendamento de Implantações de Atualizações](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

Propriedades de saudação exibidas para cada implantação de atualização são descritas Olá a tabela a seguir.

| Propriedade | Descrição |
| --- | --- |
| Nome |Nome da saudação implantação de atualização. |
| Agenda |Tipo de agenda.  As opções disponíveis são *Uma Vez*, *Recorrente Semanal* ou *Recorrente Mensal*. |
| Hora de Início |Data e hora que Olá implantação de atualização é toostart agendado. |
| Duration |Número de minutos Olá implantação de atualização é permitido toorun.  Se todas as atualizações não estiverem instaladas dentro desta duração, em seguida, Olá restantes atualizações deve esperar até Olá próxima implantação de atualização. |
| Servidores |Número de computadores afetados por Olá implantação de atualização.  |
| Status |Status atual da saudação implantação de atualização.<br><br>Os valores possíveis são:<br>- Não iniciado<br>- Executando<br>- Concluído |

Selecione uma concluído implantação de atualização tooview Olá detalhes tela que inclui colunas Olá Olá a tabela a seguir.  Essas colunas não serão preenchidas se Olá implantação de atualização não tiver ainda iniciadas.<br><br> ![Visão geral dos resultados da Implantação de Atualizações](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| Coluna | Descrição |
| --- | --- |
| **Exibição de Computadores** | |
| Computadores com Windows |Lista o número de saudação de computadores Windows hello implantação de atualização por status.  Clique em um status toorun uma pesquisa de log retornando que todos os registros de atualização com esse status de implantação de atualização de saudação. |
| Computadores Linux |Lista o número de saudação de computadores Linux no hello implantação de atualização por status.  Clique em um status toorun uma pesquisa de log retornando que todos os registros de atualização com esse status de implantação de atualização de saudação. |
| Status de Instalação do Computador |Lista computadores de saudação envolvidos na Olá implantação de atualização e percentual de saudação de atualizações que instalaram com êxito. Clique em uma saudação entradas toorun uma pesquisa de log retornando todas as atualizações ausentes e críticas. |
| **Exibição de Atualizações** | |
| Atualizações do Windows |Lista as atualizações do Windows incluídas no hello implantação de atualização e seu status de instalação por cada atualização.  Selecione uma atualização toorun uma pesquisa de log retornando todos os atualizam os registros de atualização específica ou clique em Olá status toorun uma pesquisa de log retornando que todos os registros para a implantação de saudação de atualização. |
| Atualizações do Linux |Lista as atualizações de Linux incluídas no hello implantação de atualização e seu status de instalação por cada atualização.  Selecione uma atualização toorun uma pesquisa de log retornando todos os atualizam os registros de atualização específica ou clique em Olá status toorun uma pesquisa de log retornando que todos os registros para a implantação de saudação de atualização. |

### <a name="creating-an-update-deployment"></a>Criação de uma Implantação de Atualizações
Crie uma nova implantação de atualização clicando Olá **adicionar** botão na parte superior da saudação de saudação do hello tela tooopen **nova implantação de atualização** página.  Você deve fornecer valores para propriedades Olá Olá a tabela a seguir.

| Propriedade | Descrição |
| --- | --- |
| Nome |Implantação de atualização de saudação do tooidentify de nome exclusivo. |
| Fuso horário |Toouse de fuso horário para a hora de início da saudação. |
| Tipo de Agenda | Tipo de agenda.  As opções disponíveis são *Uma Vez*, *Recorrente Semanal* ou *Recorrente Mensal*.  
| Hora de Início |Data e hora toostart Olá implantação de atualização. **Observação:** Olá primeiro pode executar uma implantação é de 30 minutos da hora atual se você precisar toodeploy imediatamente. |
| Duration |Número de minutos Olá implantação de atualização é permitido toorun.  Se todas as atualizações não estiverem instaladas dentro desta duração, em seguida, Olá restantes atualizações deve esperar até Olá próxima implantação de atualização. |
| Computadores |Nomes de computadores ou tooinclude de grupos de computador e de destino no hello implantação de atualização.  Selecione uma ou mais entradas na lista suspensa de saudação. |

<br><br> ![Página Nova Implantação de Atualizações](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>Intervalo de tempo
Por padrão, o escopo Olá dados Olá analisados Olá solução de gerenciamento de atualizações é de todos os grupos de gerenciamento conectados gerados em Olá último dia.

intervalo de tempo de saudação toochange de dados hello, selecione **dados com base em** na parte superior de saudação do painel de saudação. Você pode selecionar registros criados ou atualizados em Olá últimos 7 dias, o dia ou 6 horas. Outra opção é selecionar **Personalizado** e especificar um intervalo de datas personalizado.

## <a name="log-analytics-records"></a>Registros do Log Analytics
saudação de solução de gerenciamento de atualização cria dois tipos de registros no repositório do OMS hello.

### <a name="update-records"></a>Registros de atualização
Um registro com um tipo **Update** é criado para cada atualização instalada ou necessária em cada computador. Atualizar registros têm propriedades de saudação no Olá a tabela a seguir.

| Propriedade | Descrição |
| --- | --- |
| Tipo |*Atualização* |
| SourceSystem |fonte de saudação que aprovou a instalação da atualização de saudação.<br>Os valores possíveis são:<br>- Microsoft Update<br>- Windows Update<br>- SCCM<br>- Servidores Linux (buscados de Gerenciadores de Pacotes) |
| Aprovado |Especifica se atualização Olá foi aprovada para instalação.<br> Para os servidores Linux, atualmente isso é opcional, já que a aplicação de patch não é gerenciada pelo OMS. |
| Classificação para o Windows |Classificação de atualização de saudação.<br>Os valores possíveis são:<br>- Aplicativos<br>- Atualizações Críticas<br>- Atualizações de Definição<br>- Feature Packs<br>- Atualizações de Segurança<br>- Service Packs<br>- Pacotes Cumulativos de Atualização<br>- Atualizações |
| Classificação para Linux |Cassification de atualização de saudação.<br>Os valores possíveis são:<br>- Atualizações Críticas<br>- Atualizações de Segurança<br>- Outras Atualizações |
| Computador |Nome do computador de saudação. |
| InstallTimeAvailable |Especifica se o tempo de instalação hello está disponível de outros agentes instalados Olá mesmo atualizar. |
| InstallTimePredictionSeconds |Tempo estimado para instalação em segundos, com base em outros agentes instalados Olá a mesma atualização. |
| KBID |ID do artigo Olá KB que descreve a atualização de saudação. |
| ManagementGroupName |Nome do grupo de gerenciamento de saudação para agentes SCOM.  Para outros agentes, é o AOI-<workspace ID>. |
| MSRCBulletinID |ID do boletim de segurança da Microsoft de saudação que descreve a atualização de saudação. |
| MSRCSeverity |Severidade do boletim de segurança da Microsoft hello.<br>Os valores possíveis são:<br>- Crítico<br>- Importante<br>- Moderado |
| Opcional |Especifica se a atualização de saudação é opcional. |
| Produto |Nome Olá Olá da atualização de produto é para.  Clique em **exibição** tooopen artigo de saudação em um navegador. |
| PackageSeverity |severidade de saudação de vulnerabilidade Olá corrigida nesta atualização, conforme relatado por fornecedores de distribuição de Linux hello. |
| PublishDate |Data e hora em que Olá atualização foi instalado. |
| RebootBehavior |Especifica se a atualização de saudação força uma reinicialização.<br>Os valores possíveis são:<br>- canrequestreboot<br>- neverreboots |
| RevisionNumber |Número de revisão de atualização de saudação. |
| SourceComputerId |GUID toouniquely identificar computador hello. |
| TimeGenerated |Data e hora em que Olá registro última atualização. |
| Title |Título da atualização de saudação. |
| UpdateID |GUID toouniquely identificar atualização hello. |
| UpdateState |Especifica se a atualização de saudação está instalada neste computador.<br>Os valores possíveis são:<br>-Instalado - atualização hello está instalado neste computador.<br>-Necessária - atualização de saudação não está instalado e é necessária neste computador. |

Quando você executa qualquer pesquisa de log que retorna registros com um tipo de **atualização** você pode selecionar Olá **atualizações** exibição que exibe um conjunto de quadros de resumo de atualizações de saudação retornadas pela pesquisa de saudação. Você pode clicar nas entradas Olá Olá **ausente e atualizações aplicadas** e **atualizações obrigatórias e opcionais** blocos tooscope Olá exibir toothat definir das atualizações. Selecione Olá **lista** ou **tabela** exibir registros individuais de saudação tooreturn.<br>

![Exibição de atualização de pesquisa de log com a atualização do tipo de registro](./media/oms-solution-update-management/update-la-view-updates.png)  

Em Olá **tabela** exibição, você pode clicar em Olá **KBID** para qualquer registro tooopen um navegador com o artigo Olá KB. Isso permite que você tooquickly ler informações sobre detalhes de saudação de atualização específica hello.<br>

![Exibição de tabela de pesquisa de log com atualizações do tipo de registro de blocos](./media/oms-solution-update-management/update-la-view-table.png)

Em Olá **lista** exibição, clique Olá **exibição** link próximo toohello KBID tooopen Olá KB artigo.<br>

![Exibição de lista de pesquisa de log com atualizações do tipo de registro de blocos](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>Registros de UpdateSummary
Um registro com um tipo **UpdateSummary** é criado para cada computador de agente do Windows. Esse registro é atualizado toda vez que computador Olá é verificado para atualizações. **UpdateSummary** registros têm propriedades Olá em Olá a tabela a seguir.

| Propriedade | Descrição |
| --- | --- |
| Tipo |UpdateSummary |
| SourceSystem |OpsManager |
| Computador |Nome do computador de saudação. |
| CriticalUpdatesMissing |Número de atualizações críticas ausentes no computador de saudação. |
| ManagementGroupName |Nome do grupo de gerenciamento de saudação para agentes SCOM. Para outros agentes, é o AOI-<workspace ID>. |
| NETRuntimeVersion |Versão do tempo de execução do .NET Olá instalado no computador de saudação. |
| OldestMissingSecurityUpdateBucket |Bucket toocategorize Olá tempo desde que foi publicada hello mais antiga atualização de segurança faltando neste computador.<br>Os valores possíveis são:<br>- Mais antigos<br>- Há 180 dias<br>- Há 150 dias<br>- Há 120 dias<br>- Há 90 dias<br>- Há 60 dias<br>- Há 30 dias<br>- Recente |
| OldestMissingSecurityUpdateInDays |Número de dias desde que foi publicada hello mais antiga atualização de segurança faltando neste computador. |
| OsVersion |Versão do sistema de operacional Olá instalado no computador de saudação. |
| OtherUpdatesMissing |Número de outras atualizações ausentes no computador de saudação. |
| SecurityUpdatesMissing |Número de atualizações de segurança ausentes no computador de saudação. |
| SourceComputerId |GUID toouniquely identificar computador hello. |
| TimeGenerated |Data e hora em que Olá registro última atualização. |
| TotalUpdatesMissing |Número total de atualizações ausentes no computador de saudação. |
| WindowsUpdateAgentVersion |Número de versão do agente de atualização do Windows hello no computador de saudação. |
| WindowsUpdateSetting |Configuração de como o computador Olá instalará as atualizações importantes.<br>Os valores possíveis são:<br>- Desabilitado<br>- Notificar antes da instalação<br>- Instalação agendada |
| WSUSServer |Servidor de URL do WSUS se Olá computador estiver configurado toouse um. |

## <a name="sample-log-searches"></a>Pesquisas de log de exemplo
Olá, a tabela a seguir fornece as pesquisas de log de exemplo para atualizar registros coletados por essa solução.

| Consultar | Descrição |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |Computadores baseados no Windows Server que precisam de atualizações |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |Servidores Linux que precisam de atualizações | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Todos os computadores com atualizações ausentes |
| Type=Update UpdateState=Needed Optional=false Computer="COMPUTER01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |Atualizações ausentes para um computador específico (substitua o valor pelo nome de seu próprio computador)|
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") |Todos os computadores com atualizações críticas ou de segurança ausentes | 
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |Atualizações críticas ou de segurança necessárias para computadores em que as atualizações são aplicadas manualmente |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Security Updates" OR Classification="Critical Updates") UpdateState=Needed Optional=false &#124; Distinct Computer} |Eventos de erro para computadores sem as atualizações críticas ou de segurança obrigatórias |
| Type=Update Optional=false Classification="Update Rollups" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Todos os computadores com pacotes cumulativos de atualização ausentes | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |Atualizações ausentes distintas em todos os computadores | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |Computador baseado no Windows Server com atualizações que falharam em uma execução de atualização | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |Servidor Linux com atualizações que falharam em uma execução de atualização | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |Associação de computadores ao WSUS | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |Configuração de atualização automática | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |Computadores com atualizações automáticas desabilitadas | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" &#124; measure count() by Computer |Lista de todas as máquinas do Linux Olá que têm uma atualização de pacote disponível | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") &#124; measure count() by Computer |Lista de todas as máquinas do Linux Olá que têm uma atualização de pacote disponível que trata de vulnerabilidade de segurança ou crítico | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" |Lista de todos os pacotes que tenham uma atualização disponível | 
| Type=Update  and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") |Lista de todos os pacotes que tenham uma atualização disponível para uma vulnerabilidade Crítica ou de Segurança | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |Listar as implantações de atualização que modificaram computadores | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |Computadores que foram atualizados nesta atualização executam (substitua o valor pelo nome de sua implantação de atualização | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |Lista de todas as máquinas de "Ubuntu" hello com qualquer atualização disponível | 

## <a name="troubleshooting"></a>Solucionar problemas

Esta seção fornece informações toohelp solucionar problemas com hello solução de gerenciamento de atualizações.  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>Como solucionar problemas de integração?
Se você encontrar problemas durante a tentativa de solução de saudação tooonboard ou uma máquina virtual, verifique Olá **aplicativo e o Gerenciador de serviços de Logs\Operations** log de eventos para eventos com evento ID 4502 e evento mensagem contendo **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.  Olá a tabela a seguir realça as mensagens de erro específicas e uma possível resolução para cada.  

| Mensagem | Motivo | Solução |   
|----------|----------|----------|  
| Não é possível tooRegister máquina para gerenciamento de patches<br>Falha no registro com exceção<br>System.InvalidOperationException: {"Message":"A máquina já está<br>registrado tooa outra conta. "} | Máquina já está incorporada tooanother espaço de trabalho para gerenciamento de atualizações | Executar a limpeza dos artefatos antigos por [excluir grupo do hybrid runbook Olá](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| Não é possível registrar muito máquina para gerenciamento de patches<br>Falha no registro com exceção<br>System.Net.Http.HttpRequestException: Ocorreu um erro ao enviar solicitação de saudação. ---><br>System.NET. WebException: conexão subjacente de saudação<br>foi fechada: ocorreu um erro<br>inesperado em um recebimento. ---> System.ComponentModel.Win32Exception:<br>saudação de cliente e servidor não podem se comunicar,<br>pois não possuem um algoritmo em comum | Proxy/Gateway/Firewall está bloqueando a comunicação | [Revisar os requisitos de rede](../automation/automation-offering-get-started.md#network-planning)|  
| Não é possível tooRegister máquina para gerenciamento de patches<br>Falha no registro com exceção<br>Newtonsoft.Json.JsonReaderException: Erro ao analisar um valor infinito positivo. | Proxy/Gateway/Firewall está bloqueando a comunicação | [Revisar os requisitos de rede](../automation/automation-offering-get-started.md#network-planning)| 
| certificado de saudação apresentado pelo serviço Olá <wsid>. oms.opinsights.azure.com<br>não foi emitido por uma autoridade de certificação<br>usado para serviços da Microsoft. Entre em contato com<br>o toosee do administrador de rede se eles estiverem executando um proxy que intercepta<br>a comunicação TLS/SSL. |Proxy/Gateway/Firewall está bloqueando a comunicação | [Revisar os requisitos de rede](../automation/automation-offering-get-started.md#network-planning)|  
| Não é possível tooRegister máquina para gerenciamento de patches<br>Falha no registro com exceção<br>AgentService.HybridRegistration.<br>PowerShell.Certificates.CertificateCreationException:<br>Falha ao toocreate um certificado autoassinado. ---><br>System.UnauthorizedAccessException: acesso negado. | Falha ao gerar certificado autoassinado | Verifique se a conta do sistema tem<br>acesso de leitura toofolder:<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>Como solucionar problemas de implantações de atualização?
Você pode exibir resultados Olá Olá runbook responsável por implantar atualizações de saudação incluídas na implantação de atualizações de saudação agendada da folha de trabalhos de saudação da sua conta de automação que está vinculada ao espaço de trabalho do OMS Olá dando suporte a essa solução.  Olá runbook **MicrosoftOMSComputer Patch** é um runbook filho que tem como destino um computador gerenciado específico e revisar o fluxo detalhado Olá apresentará informações detalhadas para essa implantação.  saída de Hello serão exibir quais as atualizações necessárias estão aplicáveis, baixe o status, o status da instalação e detalhes adicionais.<br><br> ![Atualizar status de trabalho de Implantação](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

Para obter mais informações, confira [Mensagens e saída de runbook de automação](../automation/automation-runbook-output-and-messages.md).   

## <a name="next-steps"></a>Próximas etapas
* Usar pesquisas de Log no [análise de Log](../log-analytics/log-analytics-log-searches.md) tooview detalhadas de atualização de dados.
* [Crie seus próprios painéis](../log-analytics/log-analytics-dashboards.md) mostrando a conformidade da atualização dos computadores gerenciados.
* [Crie alertas](../log-analytics/log-analytics-alerts.md) quando atualizações críticas forem detectadas como ausentes de um computador ou quando um computador tiver as atualizações automáticas desabilitadas.  
