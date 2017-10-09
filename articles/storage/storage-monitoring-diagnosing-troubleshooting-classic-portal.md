---
title: aaaMonitor, diagnosticar e solucionar problemas de armazenamento | Microsoft Docs
description: "Use recursos, como análise de armazenamento, o log de cliente e tooidentify outras ferramentas de terceiros, diagnosticar e solucionar problemas relacionados ao armazenamento do Azure."
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: da57e844-705d-449d-8ed5-5607d2a6170b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: fhryo-msft
ms.openlocfilehash: 294a0bd27bd03913e01a719c0175cab827d58225
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>Monitoramento, diagnóstico e solução de problemas de Armazenamento do Microsoft Azure
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>Visão geral
Questões de diagnóstico e de solução de problemas em um aplicativo distribuído hospedado em um ambiente de nuvem podem ser mais complexas que em ambientes tradicionais. Aplicativos podem ser implantados em infraestrutura PaaS ou IaaS, no local, em um dispositivo móvel ou em uma dessas combinações. Normalmente, o tráfego de rede do seu aplicativo pode atravessar redes públicas e privadas e seu aplicativo pode usar várias tecnologias de armazenamento, como tabelas de armazenamento do Microsoft Azure, Blobs, filas ou arquivos de dados de tooother adição armazena como como relacional e bancos de dados de documento.

toomanage esses aplicativos com êxito você deve monitorá-los de forma proativa e entender como toodiagnose e solucionar problemas de todos os aspectos e as tecnologias dependentes. Como um usuário de serviços de armazenamento do Azure, você deve continuamente monitorar serviços de armazenamento Olá seu aplicativo usa para inesperado alterações no comportamento (como mais lento do que os tempos de resposta comum) e usar toocollect de log mais detalhado de dados e tooanalyze um problema em profundidade. informações de diagnóstico Olá obtidas monitoramento e registro em log ajudará você toodetermine Olá causa raiz da saudação execute seu aplicativo encontrado. Você pode solucionar o problema de saudação e determinar Olá apropriado etapas tooremediate-lo. Armazenamento do Azure é um serviço do Azure básico e faz uma parte importante de maioria de saudação de soluções que os clientes implantar toohello infraestrutura do Azure. Armazenamento do Azure inclui recursos toosimplify monitoramento, diagnóstico e solução de problemas de armazenamento em seus aplicativos baseados em nuvem.

> [!NOTE]
> Contas de armazenamento com um tipo de replicação de armazenamento com redundância de zona (ZRS) não têm métricas hello ou recurso de log habilitado no momento. 
> 
> 

Para uma guia prático tooend a fim de solução de problemas em aplicativos de armazenamento do Azure, consulte [-ponta a solução de problemas usando as métricas de armazenamento do Azure e registro em log, AzCopy e analisador de mensagem](storage-e2e-troubleshooting.md).

* [Introdução]
  * [Como esse guia está organizado]
* [seu serviço de armazenamento de monitoramento]
  * [Monitoramento da integridade do serviço]
  * [Monitoramento de capacidade]
  * [Monitoramento de disponibilidade]
  * [Monitoramento de desempenho]
* [diagnosticar problemas de armazenamento]
  * [Problemas de integridade do serviço]
  * [Problemas de desempenho]
  * [Diagnóstico de erros]
  * [Problemas de emulador de armazenamento]
  * [Ferramentas de log de armazenamento]
  * [Uso de ferramentas de log de rede]
* [rastreamento ponta a ponta]
  * [Correlacionamento de dados de log]
  * [ID de solicitação do cliente]
  * [ID de solicitação do servidor]
  * [Carimbos de data/hora]
* [guia de solução de problemas]
  * [métricas mostram AverageE2ELatency alta e baixa AverageServerLatency]
  * [Métricas mostram AverageE2ELatency baixa e baixa AverageServerLatency mas cliente hello está apresentando alta latência]
  * [As métricas mostram alta AverageServerLatency]
  * [Você está sofrendo atrasos inesperados na entrega de mensagens na fila]
  * [métricas mostram um aumento no PercentThrottlingError]
  * [métricas mostram um aumento no PercentTimeoutError]
  * [As métricas mostram um aumento em PercentNetworkError]
  * [Olá está recebendo mensagens HTTP 403 (proibido)]
  * [Olá está recebendo mensagens HTTP 404 (não encontrado)]
  * [Olá está recebendo mensagens HTTP 409 (conflito)]
  * [métricas mostram PercentSuccess baixa ou entradas de log de análise possuem operações com status de transação de ClientOtherErrors]
  * [As métricas de capacidade mostram um aumento inesperado em uso de capacidade de armazenamento]
  * [Você está enfrentando reinicializações inesperadas das máquinas virtuais que contêm um grande número de VHDs anexados]
  * [O problema surge de usar o emulador de armazenamento Olá para desenvolvimento ou teste]
  * [Você está encontrando problemas na instalação hello Azure SDK para .NET]
  * [Você tem um problema diferente com um serviço de armazenamento]
* [apêndices]
  * [Apêndice 1: tráfego HTTP e HTTPS toocapture usando Fiddler]
  * [Apêndice 2: tráfego de rede usando o Wireshark toocapture]
  * [apêndice 3: tráfego de rede usando o Microsoft Message Analyzer toocapture]
  * [Apêndice 4: Usando dados de log e métricas de tooview do Excel]
  * [apêndice 5: monitoramento com o Application Insights para Visual Studio Team Services]

## <a name="introduction"></a>Introdução
Problemas relacionados ao mostra este guia, você como toouse recursos como análise de armazenamento do Azure, o log de cliente em Olá biblioteca de cliente de armazenamento do Azure e tooidentify outras ferramentas de terceiros, Diagnostica e solucionar problemas de armazenamento do Azure.

![][1]

*Figura 1: Monitoramento, Diagnósticos e Solução de Problemas*

Este guia é pretendido toobe ler principalmente por desenvolvedores de serviços online que usam os serviços de armazenamento do Azure e profissionais de TI responsáveis por gerenciar tais serviços on-line. Olá objetivos deste guia são:

* toohelp manter a integridade de saudação e o desempenho de suas contas de armazenamento do Azure.
* tooprovide processos necessário hello e toohelp ferramentas você decidir se um problema em um aplicativo ou um problema relacionado tooAzure armazenamento.
* tooprovide acionáveis orientação para solucionar problemas relacionados ao tooAzure armazenamento.

### <a name="how-this-guide-is-organized"></a>Como esse guia está organizado
Olá a seção "[seu serviço de armazenamento de monitoramento]" descreve como toomonitor Olá integridade e o desempenho de seus serviços de armazenamento do Azure usando as métricas da análise de armazenamento do Azure (métricas de armazenamento).

Olá a seção "[diagnosticar problemas de armazenamento]" descreve como toodiagnose problemas usando o Azure Storage Analytics log (log de armazenamento). Ele também descreve como tooenable log no lado do cliente usando hello instalações em uma das bibliotecas de cliente hello como Olá biblioteca de cliente de armazenamento para .NET ou Olá SDK do Azure para Java.

Olá a seção "[rastreamento ponta a ponta]" descreve como você pode correlacionar informações Olá contidas em vários arquivos de log e dados de métricas.

Olá a seção "[guia de solução de problemas]" fornece orientação para solução de problemas para algumas das Olá relacionados ao armazenamento problemas comuns que podem ser encontrados.

Olá "[apêndices]" incluem informações sobre como usar outras ferramentas como Wireshark e Netmon para analisar dados de pacote, o Fiddler para analisar mensagens HTTP/HTTPS, de rede e o Microsoft Message Analyzer para correlacionar dados de log.

## <a name="monitoring-your-storage-service"></a>Monitoramento do seu serviço de armazenamento
Se você está acostumado com o monitoramento de desempenho do Windows, é possível entender as Métricas de Armazenamento como equivalentes aos contadores do Monitor de Desempenho do Windows. As métricas de armazenamento, você encontrará um conjunto abrangente de métricas (contadores na terminologia do Monitor de desempenho do Windows), como a disponibilidade do serviço, o número total de solicitações tooservice ou porcentagem de solicitações bem sucedidas tooservice (para obter uma lista completa de saudação métricas disponíveis, consulte <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">esquema de tabela de métricas de análise de armazenamento</a> no MSDN). Você pode especificar se deseja Olá toocollect de serviço de armazenamento e as métricas agregadas a cada hora ou a cada minuto. Para obter mais informações sobre como tooenable métricas e monitorar suas contas de armazenamento, consulte <a href="http://go.microsoft.com/fwlink/?LinkId=510865" target="_blank">habilitando métricas de armazenamento</a> no MSDN.

Você pode escolher quais métricas de hora que você deseja toodisplay no hello Portal clássico do Azure e configure as regras que notificar os administradores por email sempre que uma métrica de hora em hora excede um determinado limite (para obter mais informações, consulte a página de saudação <a href="http://msdn.microsoft.com/library/azure/dn306638.aspx" target="_blank">como: Receber notificações de alerta e gerenciar regras de alerta no Azure</a>). o serviço de armazenamento Olá coleta métricas usando um melhor esforço, mas não é possível registrar cada operação de armazenamento.

Figura 2 a seguir mostra a página de Monitor de saudação em Olá Portal clássico do Azure, onde você pode exibir métricas, como disponibilidade, o total de solicitações e números de latência média para uma conta de armazenamento. Uma regra de notificação tem também foi configurada tooalert administrador se disponibilidade cair abaixo de um determinado nível. Exibam esses dados, uma área possíveis para investigação é percentagem de sucesso de serviço tabela Olá sendo abaixo de 100% (para obter mais informações, consulte a seção hello "[métricas mostram PercentSuccess baixa ou entradas de log de análise possuem operações com status de transação de ClientOtherErrors]").

![][2]

*Figura 2 exibir as métricas de armazenamento no hello Portal clássico do Azure*

Monitore continuamente o tooensure de aplicativos do Azure estiverem íntegros e executado como esperado:

* Estabelecer algumas métricas de linha de base para o aplicativo que permitem dados atuais toocompare e identificar quaisquer alterações significativas no comportamento de saudação do armazenamento do Azure e o seu aplicativo. Olá os valores de suas métricas de linha de base, em muitos casos, serão específica do aplicativo e você deve estabelecê-los quando você estiver testando seu aplicativo de desempenho.
* Gravação de métricas de minutos e usá-los toomonitor ativamente para erros inesperados e anomalias como picos de contagens de erros ou taxas de solicitação.
* Gravação de métricas de hora e usá-los valores médios toomonitor como contagens de erro da média e taxas de solicitação.
* Investigando possíveis problemas usando as ferramentas de diagnóstico como discutido posteriormente na seção de hello "[diagnosticar problemas de armazenamento]."

gráficos de saudação na Figura 3 abaixo ilustram como Olá média que ocorre para métricas de hora pode ocultar picos de atividade. métricas de hora Olá aparecem tooshow uma taxa contínua de solicitações, ao minuto Olá métricas revelam flutuações Olá realmente em andamento.

![][3]

Olá, restante desta seção descreve quais métricas, você deve monitorar e por quê.

### <a name="monitoring-service-health"></a>Monitoramento da integridade do serviço
Você pode usar o hello [Portal clássico do Azure](https://manage.windowsazure.com) Olá de tooview integridade de saudação do serviço de armazenamento de saudação (e outros serviços do Azure) em todas as regiões do Azure ao redor Olá, mundo. Isso permite que você toosee imediatamente se um problema fora de seu controle está afetando Olá serviço de armazenamento na região Olá que usar para seu aplicativo.

Olá Portal clássico do Azure também pode fornecer notificações de incidentes que afetam Olá vários serviços do Azure.
Observação: Essas informações estavam disponíveis anteriormente, juntamente com os dados históricos, em Olá painel de serviço do Azure em <a href="http://status.azure.com" target="_blank">http://status.azure.com</a>.

Enquanto Olá Portal clássico do Azure coleta informações de integridade de dentro de saudação datacenters do Azure (monitoramento de dentro para fora), você pode optar por adotando uma abordagem de dentro para fora toogenerate as transações sintéticas que periodicamente acessar seu hospedado no Azure aplicativo Web de vários locais. Olá serviços oferecidos pelo <a href="http://www.keynote.com/solutions/monitoring/web-monitoring" target="_blank">Keynote</a>, <a href="https://www.gomeznetworks.com/?g=1" target="_blank">Gomez</a>, e o Application Insights para Visual Studio Team Services são exemplos de como essa abordagem de dentro para fora. Para obter mais informações sobre o Application Insights para Visual Studio Team Services, consulte o apêndice de hello "[apêndice 5: monitoramento com o Application Insights para Visual Studio Team Services]."

### <a name="monitoring-capacity"></a>Monitoramento de capacidade
As métricas de armazenamento armazena apenas as métricas de capacidade para o serviço de blob Olá porque blobs normalmente conta a proporção maior Olá dos dados armazenados (no momento da saudação de gravação, ele não é toouse possíveis as métricas de armazenamento toomonitor Olá capacidade de suas tabelas e filas) . Você pode encontrar esses dados no hello **$MetricsCapacityBlob** tabela se você tiver habilitado o monitoramento para Olá serviço Blob. As métricas de armazenamento registra dados uma vez por dia, e você pode usar o valor Olá Olá **RowKey** toodetermine se a linha hello contém uma entidade que relaciona dados toouser (valor **dados**) ou (de dados de análise valor **análise**). Cada entidade armazenada contém informações sobre a quantidade de saudação do armazenamento usado (**capacidade** medido em bytes) e o número atual de recipientes de hello (**ContainerCount**) e blobs ( **ObjectCount**) em uso na conta de armazenamento hello. Para obter mais informações sobre as métricas de capacidade de saudação armazenadas em Olá **$MetricsCapacityBlob** de tabela, consulte <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">esquema de tabela de métricas de análise de armazenamento</a> no MSDN.

> [!NOTE]
> Você deve monitorar esses valores para um aviso antecipado que estão se aproximando os limites de capacidade de saudação da sua conta de armazenamento. Em Olá Portal clássico do Azure, em Olá **Monitor** página da sua conta de armazenamento, você pode adicionar regras de alerta toonotify se exceder o uso de agregação do armazenamento ou abaixo de limites que você especificar.
> 
> 

Para obter ajuda Estimando o tamanho de saudação de vários objetos de armazenamento como blobs, consulte Olá postagem de blog <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx" target="_blank">entendimento do Azure de cobrança de armazenamento – largura de banda, transações e capacidade</a>.

### <a name="monitoring-availability"></a>Monitoramento de disponibilidade
Você deve monitorar disponibilidade Olá Olá de serviços de armazenamento em sua conta de armazenamento pelo monitoramento valor Olá Olá **disponibilidade** coluna Olá tabelas de métricas de horas ou minutos — **$ MetricsHourPrimaryTransactionsBlob**, **$MetricsHourPrimaryTransactionsTable**, **$MetricsHourPrimaryTransactionsQueue**, **$ MetricsMinutePrimaryTransactionsBlob**, **$MetricsMinutePrimaryTransactionsTable**, **$MetricsMinutePrimaryTransactionsQueue**, **$ MetricsCapacityBlob**. Olá **disponibilidade** coluna contém um valor de porcentagem que indica a disponibilidade de saudação do serviço de saudação ou operação Olá API representado pela linha hello (Olá **RowKey** mostra se a linha hello contém métricas para serviço hello como um todo ou para uma operação específica de API).

Qualquer valor inferior a 100% indica que houve falha em algumas solicitações de armazenamento. Você pode ver por que eles estão falhando examinando Olá outras colunas nos dados de métricas de saudação que mostram os números de saudação de solicitações com tipos de erro diferentes, como **ServerTimeoutError**. Você deve esperar toosee **disponibilidade** estão temporariamente abaixo de 100% por motivos como transitório tempos limite do servidor enquanto o serviço Olá move a solicitação de partições de balanceamento de carga toobetter; Olá lógica de repetição em seu aplicativo cliente deve lidar com tais condições intermitentes. página Olá <a href="http://msdn.microsoft.com/library/azure/hh343260.aspx" target="_blank"> </a> listas Olá tipos de transação que inclui as métricas de armazenamento em seu **disponibilidade** cálculo.

Em Olá Portal clássico do Azure, em Olá **Monitor** página conta de armazenamento, você pode adicionar regras de alerta toonotify você se **disponibilidade** para um serviço fica abaixo do limite especificado por você.

Olá "[guia de solução de problemas]" deste guia descreve alguns tooavailability relacionados comuns do armazenamento serviço problemas.

### <a name="monitoring-performance"></a>Monitoramento de desempenho
desempenho de saudação toomonitor Olá de serviços de armazenamento, você pode usar o hello seguindo as métricas da saudação por hora e tabelas de métricas de minuto.

* Olá valores hello **AverageE2ELatency** e **AverageServerLatency** mostram o serviço de armazenamento de saudação de tempo médio de saudação ou tipo de operação da API está demorando tooprocess solicitações. **AverageE2ELatency** é uma medida de latência de ponta a ponta que inclui o tempo Olá tooread solicitação de saudação e enviar resposta Olá na solicitação de saudação adição toohello tempo tooprocess (portanto inclui latência de rede depois que a solicitação de saudação atingir o serviço de armazenamento de saudação); **AverageServerLatency** é uma medida de tempo de processamento de saudação apenas e, portanto, exclui uma latência de rede relacionada toocommunicating com cliente hello. Consulte a seção hello "[métricas mostram AverageE2ELatency alta e baixa AverageServerLatency]" neste documento para uma discussão sobre por que pode haver uma diferença significativa entre esses dois valores.
* Olá valores hello **TotalIngress** e **TotalEgress** colunas mostram a quantidade total de saudação de dados, em bytes, chegando tooand vai fora de seu serviço de armazenamento ou por meio de um tipo específico de operação de API.
* Olá valores hello **TotalRequests** coluna Mostrar Olá total de solicitações que Olá o serviço de armazenamento de operação da API está recebendo. **TotalRequests** Olá o número total de solicitações de serviço de armazenamento de saudação recebe.

Normalmente, você irá monitorar as mudanças inesperadas em qualquer um desses valores como indicador de que você tem um problema que requer uma investigação.

Em Olá Portal clássico do Azure, em Olá **Monitor** página conta de armazenamento, você pode adicionar regras de alerta toonotify se qualquer uma das métricas de desempenho de saudação para este serviço cair ou excede um limite que você especificar.

Olá "[guia de solução de problemas]" deste guia descreve alguns tooperformance relacionados comuns do armazenamento serviço problemas.

## <a name="diagnosing-storage-issues"></a>Diagnóstico de problemas de armazenamento
Há inúmero caminhos que você pode ter para ficar ciente de um problema em seu aplicativo, entre eles:

* Uma falha grave que faz com que o trabalho de toocrash ou toostop aplicativo hello.
* Alterações significativas em valores de linha de base em métricas de saudação do monitoramento conforme descrito na seção anterior hello "[seu serviço de armazenamento de monitoramento]."
* Relatórios de usuários do seu aplicativo informando que uma operação em particular não foi concluída como esperado ou que algum recurso não está funcionando.
* Erros gerados dentro do seu aplicativo que aparecem nos arquivos de log ou em outros métodos de notificação.

Normalmente, os serviços de armazenamento relacionados tooAzure problemas cairá em uma das quatro amplas categorias:

* Seu aplicativo tem um problema de desempenho, ou relatados pelos usuários ou reveladas por mudanças nas métricas de desempenho de saudação.
* Há um problema com a infraestrutura de armazenamento do Azure Olá em uma ou mais regiões.
* Seu aplicativo está encontrando um erro, ou relatados pelos usuários ou reveladas por um aumento de uma das métricas de contagem de erro Olá que você monitorar.
* Durante o desenvolvimento e teste, você pode estar usando o emulador de armazenamento local Olá; Você pode encontrar alguns problemas relacionados especificamente toousage do emulador de armazenamento hello.

Olá seções a seguir descrevem as etapas Olá deve seguir toodiagnose e solucionar problemas em cada uma destas quatro categorias. Olá a seção "[guia de solução de problemas]" mais adiante neste guia fornece mais detalhes para alguns problemas comuns que podem ser encontrados.

### <a name="service-health-issues"></a>Problemas de integridade do serviço
Problemas de integridade do serviço são normalmente fora do seu controle. Olá Portal clássico do Azure fornece informações sobre os problemas em andamento com os serviços do Azure, incluindo serviços de armazenamento. Se você tiver optado por armazenamento com redundância geográfica com acesso de leitura quando você criou sua conta de armazenamento, no evento de saudação de dados está indisponível no local principal do hello, seu aplicativo pode alternar temporariamente toohello a cópia somente leitura no local secundário hello. toodo isso, seu aplicativo deve ser capaz de tooswitch entre usar os locais de armazenamento primário e secundário hello e ser capaz de toowork em um modo de funcionalidade reduzida com dados somente leitura. bibliotecas de cliente de armazenamento do Azure Olá permitem que você toodefine uma política de repetição pode ler do armazenamento secundário no caso de falha de uma leitura do armazenamento principal. Seu aplicativo deve também toobe ciente de que dados Olá no local secundário Olá finalmente consistentes. Para obter mais informações, consulte Olá postagem de blog <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/04/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx" target="_blank">opções de redundância de armazenamento do Azure e armazenamento geograficamente redundante de acesso de leitura</a>.

### <a name="performance-issues"></a>Problemas de desempenho
desempenho de saudação de um aplicativo pode ser subjetivo, especialmente a partir de uma perspectiva do usuário. Portanto, é importante toohave da linha de base métricas disponíveis toohelp identificar qual pode haver um problema de desempenho. Muitos fatores podem afetar o desempenho de saudação de um serviço de armazenamento do Azure da perspectiva de aplicativo cliente hello. Esses fatores podem operar no serviço de armazenamento hello, no cliente de saudação ou na infraestrutura de rede Olá; Portanto, é importante toohave uma estratégia para identificar a origem de saudação do problema de desempenho de saudação.

Depois de ter identificado o local de Olá provável causa de saudação do problema de desempenho de saudação de métricas de saudação, você pode então toofind de arquivos de log do uso Olá detalhadas toodiagnose informações e solucionar o problema hello.

Olá a seção "[guia de solução de problemas]" mais adiante neste guia fornece mais informações sobre alguns comuns de desempenho relacionado problemas que você pode encontrar.

### <a name="diagnosing-errors"></a>Diagnóstico de erros
Os usuários do seu aplicativo podem notificá-lo de erros relatados pelo aplicativo de cliente hello. Métricas de armazenamento também registram contagens de diferentes tipos de erros do seus serviços de armazenamento, tais como **NetworkError**, **ClientTimeoutError** ou **AuthorizationError**. Enquanto as métricas de armazenamento apenas registram as contagens de diferentes tipos de erros, você obter mais detalhes sobre solicitações individuais ao examinar os logs do servidor, do cliente e da rede. Normalmente, o código de status HTTP Olá retornado pelo serviço de armazenamento de saudação darão uma indicação de por que houve falha na solicitação de saudação.

> [!NOTE]
> Lembre-se de que você deve esperar toosee alguns erros intermitentes: por exemplo, erros devido a condições da rede tootransient ou erros de aplicativo.
> 
> 

Olá a recursos a seguir no MSDN são úteis para entender os códigos de status e erro relacionados ao armazenamento:

* <a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">Códigos de erro comuns da API REST</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179439.aspx" target="_blank">Códigos de erro do serviço Blob</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179446.aspx" target="_blank">Códigos de erro do serviço Fila</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179438.aspx" target="_blank">Códigos de erro do serviço Tabela</a>

### <a name="storage-emulator-issues"></a>Problemas de emulador de armazenamento
Olá SDK do Azure inclui um emulador de armazenamento que você pode executar em uma estação de trabalho de desenvolvimento. Este emulador simula a maior parte do comportamento de saudação de serviços de armazenamento do Azure hello e é útil durante o desenvolvimento e teste, permitindo que você toorun aplicativos que usam serviços de armazenamento do Azure sem Olá precisam de uma assinatura do Azure e uma conta de armazenamento do Azure.

Olá "[guia de solução de problemas]" deste guia descreve alguns problemas comuns encontrados usando o emulador de armazenamento hello.

### <a name="storage-logging-tools"></a>Ferramentas de log de armazenamento
O log de armazenamento oferece o log do lado do servidor para solicitações de armazenamento na sua conta de armazenamento do Azure. Para obter mais informações sobre como o log do servidor tooenable e Olá acesso dados do log, consulte <a href="http://go.microsoft.com/fwlink/?LinkId=510867" target="_blank">usando o registro do servidor</a> no MSDN.

Olá biblioteca de cliente de armazenamento para .NET permite que dados de log do lado do cliente toocollect que relaciona toostorage operações executadas pelo seu aplicativo. Para obter mais informações sobre como o log de cliente tooenable e Olá acesso dados do log, consulte <a href="http://go.microsoft.com/fwlink/?LinkId=510868" target="_blank">do lado do cliente usando o registro em log Olá a biblioteca de cliente de armazenamento</a> no MSDN.

> [!NOTE]
> Em algumas circunstâncias (como falhas de autorização SAS), um usuário pode relatar um erro para o qual você não pode encontrar nenhum dado de solicitação no hello logs de armazenamento do servidor. Você pode usar recursos de log de saudação do hello biblioteca de cliente de armazenamento tooinvestigate se causa Olá problema Olá é no cliente de saudação ou usar a rede de saudação tooinvestigate ferramentas de monitoramento de rede.
> 
> 

### <a name="using-network-logging-tools"></a>Uso de ferramentas de log de rede
Você pode capturar o tráfego de saudação entre tooprovide de cliente e servidor de saudação detalhada informações sobre Olá dados Olá cliente e servidor são trocando e hello subjacente condições da rede. Ferramentas úteis de log de rede incluem:

* Fiddler (<a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a>) é uma web gratuita que permite que você os cabeçalhos de saudação tooexamine e dados de carga de mensagens de solicitação e resposta HTTP e HTTPS de proxy de depuração. Para obter mais informações, consulte "[Apêndice 1: tráfego HTTP e HTTPS toocapture usando Fiddler]".
* Monitor de rede (Netmon) do Microsoft (<a href="http://www.microsoft.com/download/details.aspx?id=4865" target="_blank">http://www.microsoft.com/download/details.aspx?id=4865</a>) e o Wireshark (<a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a>) é analisadores de protocolo que permitem que a rede livre Você tooview pacote informações detalhadas para uma ampla variedade de protocolos de rede. Para obter mais informações sobre o Wireshark, consulte "[Apêndice 2: tráfego de rede usando o Wireshark toocapture]".
* Microsoft Message Analyzer é uma ferramenta da Microsoft que substitui o Netmon e que, além de toocapturing rede dados do pacote, ajuda você a tooview e analisar dados de log Olá capturados a partir de outras ferramentas. Para obter mais informações, consulte "[apêndice 3: tráfego de rede usando o Microsoft Message Analyzer toocapture]".
* Se você quiser tooperform um toocheck de teste de conectividade básica se o computador cliente pode se conectar a toohello serviço de armazenamento do Azure pela rede Olá, você não pode fazer isso usando o padrão de saudação **ping** ferramenta no cliente de saudação. No entanto, você pode usar o hello **tcping** ferramenta toocheck conectividade. O **Tcping** está disponível para download em <a href="http://www.elifulkerson.com/projects/tcping.php" target="_blank">http://www.elifulkerson.com/projects/tcping.php</a>.

Em muitos casos, os dados de log de saudação do log de armazenamento e biblioteca de cliente de armazenamento de hello serão suficiente toodiagnose um problema, mas em alguns cenários, talvez seja necessário Olá que essas ferramentas de log de rede podem fornecer informações mais detalhadas. Por exemplo, usando o Fiddler tooview permite mensagens HTTP e HTTPS, os dados de cabeçalho e carga tooview enviadas tooand da saudação serviços de armazenamento, que poderia permitir a você tooexamine como um aplicativo cliente repete as operações de armazenamento. Analisadores de protocolo, como o Wireshark operam no nível de pacote de saudação permitindo que dados TCP tooview, que permitem que você tootroubleshoot perda de pacotes e problemas de conectividade. O Message Analyzer pode operar tanto em camadas HTTP como TCP.

## <a name="end-to-end-tracing"></a>Rastreamento de ponta a ponta
O rastreamento de ponta a ponta usando uma variedade de arquivos de log é uma técnica útil para a investigação de potenciais problemas. Você pode usar as informações de data/hora de saudação de seus dados de métricas como uma indicação de qual toostart procurando nos arquivos de log Olá Olá detalhadas informações que ajudarão você a solucionar o problema de saudação.

### <a name="correlating-log-data"></a>Correlacionamento de dados de log
Ao exibir os logs de aplicativos cliente, rastreamentos de rede e armazenamento do lado do servidor efetuá-lo é crítico toobe toocorrelate capaz de solicitações em Olá diferentes arquivos de log. arquivos de log de saudação incluem um número de campos diferentes que são úteis como identificadores de correlação. id de solicitação do cliente Olá é hello mais úteis campo toouse toocorrelate entradas nos logs de saudação diferente. No entanto às vezes, pode ser útil toouse id de solicitação do servidor de saudação ou os carimbos de hora. Olá seções a seguir fornecem mais detalhes sobre essas opções.

### <a name="client-request-id"></a>ID de solicitação do cliente
Olá biblioteca de cliente de armazenamento gera automaticamente uma id de solicitação de cliente exclusivos para cada solicitação.

* Olá log do lado do cliente que Olá biblioteca de cliente de armazenamento cria, id de solicitação do cliente Olá aparece no hello **ID de solicitação do cliente** campo de cada entrada de log relacionadas toohello solicitação.
* Em um rastreamento de rede, como um capturados pelo Fiddler, id de solicitação do cliente Olá é visível em mensagens de solicitação como Olá **x-ms-client-request-id** valor do cabeçalho HTTP.
* No log do log de armazenamento do saudação do servidor, a id de solicitação do cliente de saudação aparece na coluna de ID de solicitação de cliente de saudação.

> [!NOTE]
> É possível tooshare de várias solicitações Olá a mesma id de solicitação do cliente porque o cliente Olá pode atribuir esse valor (embora Olá biblioteca de cliente de armazenamento atribui um novo valor automaticamente). No caso de saudação de repetições de cliente Olá, todas as tentativas de compartilham Olá mesmo id de solicitação do cliente. No caso de saudação de um lote enviado do cliente hello, lote Olá tem uma id de solicitação do cliente individual.
> 
> 

### <a name="server-request-id"></a>ID de solicitação do servidor
o serviço de armazenamento Hello gera automaticamente as ids de solicitação do servidor.

* No log do log de armazenamento do saudação do servidor, a id de solicitação do servidor de saudação aparece Olá **cabeçalho Request ID** coluna.
* Em um rastreamento de rede, como um capturados pelo Fiddler, id de solicitação do servidor de saudação aparece em mensagens de resposta como Olá **x-ms-request-id** valor do cabeçalho HTTP.
* Olá log do lado do cliente que Olá biblioteca de cliente de armazenamento cria, id de solicitação do servidor de saudação aparece no hello **operação texto** coluna de entrada de log Olá mostrando os detalhes da resposta do servidor de saudação.

> [!NOTE]
> serviço de armazenamento de saudação sempre atribui um único servidor solicitação id tooevery solicitação que for recebida, para que cada tentativa de repetição do cliente hello e cada operação incluídas em um lote tem uma id de solicitação exclusiva do servidor.
> 
> 

Se hello biblioteca de cliente de armazenamento gera um **StorageException** no cliente de Olá Olá **RequestInformation** propriedade contém um **RequestResult** objeto que inclui um **ServiceRequestID** propriedade. Você também pode acessar um objeto **RequestResult** a partir de uma instância de **OperationContext**.

Olá código de exemplo abaixo demonstra como tooset um personalizado **ClientRequestId** valor anexando um **OperationContext** serviço de armazenamento de toohello de solicitação de saudação do objeto. Ele também mostra como Olá tooretrieve **ServerRequestId** valor da mensagem de resposta de saudação.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>Carimbos de data/hora
Você também pode usar os carimbos de hora toolocate as entradas de log relacionadas, mas lembre-se de qualquer pela defasagem horária entre o cliente de saudação e servidor que possam existir. Você deve pesquisar mais ou menos de 15 minutos para entradas do servidor com base em carimbo de hora Olá no cliente Olá correspondentes. Lembre-se de que metadados de blob Olá para blobs Olá métricas contendo indicam o intervalo de tempo de saudação para métricas de saudação armazenados no blob Olá; Isso é útil se você tiver muitos blobs métricas para Olá mesmo horas ou minutos.

## <a name="troubleshooting-guidance"></a>Diretrizes de solução de problemas
Nesta seção ajudam com diagnóstico hello e solução de problemas de alguns dos problemas comuns de saudação seu aplicativo pode encontrar ao usar os serviços de armazenamento do Azure hello. Use a lista de saudação abaixo toolocate Olá informações relevantes tooyour determinado problema.

**Árvore de decisão de solução de problemas**

- - -
O problema se relacionam toohello o desempenho de um dos serviços de armazenamento Olá?

* [métricas mostram AverageE2ELatency alta e baixa AverageServerLatency]
* [Métricas mostram AverageE2ELatency baixa e baixa AverageServerLatency mas cliente hello está apresentando alta latência]
* [As métricas mostram alta AverageServerLatency]
* [Você está sofrendo atrasos inesperados na entrega de mensagens na fila]

- - -
O problema está relacionado a toohello disponibilidade de um dos serviços de armazenamento Olá?

* [métricas mostram um aumento no PercentThrottlingError]
* [métricas mostram um aumento no PercentTimeoutError]
* [As métricas mostram um aumento em PercentNetworkError]

- - -
O seu aplicativo do cliente está recebendo uma resposta HTTP 4XX (tal como 404) de um serviço de armazenamento?

* [Olá está recebendo mensagens HTTP 403 (proibido)]
* [Olá está recebendo mensagens HTTP 404 (não encontrado)]
* [Olá está recebendo mensagens HTTP 409 (conflito)]

- - -
[métricas mostram PercentSuccess baixa ou entradas de log de análise possuem operações com status de transação de ClientOtherErrors]

- - -
[As métricas de capacidade mostram um aumento inesperado em uso de capacidade de armazenamento]

- - -
[Você está enfrentando reinicializações inesperadas das máquinas virtuais que contêm um grande número de VHDs anexados]

- - -
[O problema surge de usar o emulador de armazenamento Olá para desenvolvimento ou teste]

- - -
[Você está encontrando problemas na instalação hello Azure SDK para .NET]

- - -
[Você tem um problema diferente com um serviço de armazenamento]

- - -
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>As métricas mostram alta AverageE2ELatency e baixa AverageServerLatency
Olá remover ilustração da ferramenta de monitoramento do hello Portal clássico do Azure mostra um exemplo onde hello **AverageE2ELatency** é significativamente maior do que Olá **AverageServerLatency**.

![][4]

Observe que o serviço de armazenamento Olá calcula apenas métrica Olá **AverageE2ELatency** para solicitações bem-sucedidas e, ao contrário de **AverageServerLatency**, inclui Olá tempo cliente Olá Olá toosend dados e receber a confirmação do serviço de armazenamento de saudação. Portanto, uma diferença entre **AverageE2ELatency** e **AverageServerLatency** pode ser devido a toohello cliente aplicativo sendo demoram toorespond ou tooconditions devido na rede de saudação.

> [!NOTE]
> Você também pode exibir **E2ELatency** e **ServerLatency** para operações de armazenamento individuais no log de armazenamento de saudação dados de log.
> 
> 

#### <a name="investigating-client-performance-issues"></a>Investigação dos problemas de desempenho do cliente
Possíveis razões para o cliente Olá respondendo lentamente incluem um número limitado de conexões disponíveis ou threads. É possível problema de saudação tooresolve capaz modificando Olá cliente código toobe mais eficiente (por exemplo, usando o serviço de armazenamento de toohello chamadas assíncronas) ou por meio de uma máquina Virtual maiores (com mais núcleos e memória).

Para serviços tabela e fila hello, algoritmo de Nagle Olá também pode causar alta **AverageE2ELatency** comparado muito**AverageServerLatency**: para obter mais informações consulte Olá postagem <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx" target="_blank">do Nagle O algoritmo não é amigável para solicitações de pequenas</a> em Olá Blog da equipe de armazenamento do Microsoft Azure. Você pode desabilitar o algoritmo de Nagle Olá no código usando Olá **ServicePointManager** classe Olá **System.Net** namespace. Você deve fazer isso antes de fazer qualquer tabela de toohello chamadas ou serviços de fila em seu aplicativo, já que isso não afeta as conexões que já estão abrir. Olá exemplo a seguir é proveniente Olá **Application_Start** método em uma função de trabalho.

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

Você deve verificar a saudação do cliente logs toosee quantas solicitações de envio de seu aplicativo cliente e procure .NET gerais relacionados afunilamentos de desempenho no seu cliente, como CPU, coleta de lixo do .NET, utilização de rede ou de memória (como um valor inicial aponte para solucionar problemas de aplicativos de cliente .NET, consulte <a href="http://msdn.microsoft.com/library/7fe0dd2y(v=vs.110).aspx" target="_blank">criação de perfil de depuração e rastreamento</a> no MSDN).

#### <a name="investigating-network-latency-issues"></a>Investigando os problemas de latência de rede
Normalmente, alta latência de ponta a ponta causada por rede Olá é devido a condições tootransient. Você pode investigar tantos os problemas de rede persistentes ou transitórios, tais como pacotes ignorados ao usar ferramentas, tais como Wireshark ou Microsoft Message Analyzer.

Para obter mais informações sobre como usar o Wireshark tootroubleshoot problemas na rede, consulte "[Apêndice 2: tráfego de rede usando o Wireshark toocapture]."

Para obter mais informações sobre problemas de rede do Microsoft Message Analyzer tootroubleshoot, consulte "[apêndice 3: tráfego de rede usando o Microsoft Message Analyzer toocapture]."

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>Métricas mostram AverageE2ELatency baixa e baixa AverageServerLatency mas cliente hello está apresentando alta latência
Nesse cenário, causa mais provável Olá é um atraso nas solicitações de armazenamento Olá alcançar o serviço de armazenamento de saudação. Você deve investigar por que solicitações de cliente Olá não estiver fazendo-lo por meio do serviço de blob toohello.

Possíveis razões para atrasar a enviar solicitações de cliente de saudação incluem um número limitado de conexões disponíveis ou threads. Você também deve verificar se o cliente de saudação estiver executando várias tentativas e investigue o motivo de saudação se esse for o caso de saudação. Você pode fazer isso programaticamente através do hello **OperationContext** objeto associado à solicitação hello e recuperar Olá **ServerRequestId** valor. Para obter mais informações, consulte o exemplo de código de saudação na seção hello "[ID de solicitação do servidor]."

Se não houver nenhum problema no cliente hello, você deve investigar possíveis problemas de rede, como perda de pacotes. Você pode usar ferramentas como o Wireshark ou Microsoft Message Analyzer tooinvestigate problemas de rede.

Para obter mais informações sobre como usar o Wireshark tootroubleshoot problemas na rede, consulte "[Apêndice 2: tráfego de rede usando o Wireshark toocapture]."

Para obter mais informações sobre problemas de rede do Microsoft Message Analyzer tootroubleshoot, consulte "[apêndice 3: tráfego de rede usando o Microsoft Message Analyzer toocapture]."

### <a name="metrics-show-high-AverageServerLatency"></a>As métricas mostram alta AverageServerLatency
No caso de Olá alta **AverageServerLatency** para solicitações de download de blob, você deve usar o hello log de armazenamento registra toosee se não houver solicitações repetidas de saudação mesmo blob (ou conjunto de blobs). Solicitações de carregamento de blob, você deve investigar o bloco está usando o cliente de saudação do tamanho (por exemplo, blocos menor do que 64K de tamanho pode resultar em custos, a menos que lê Olá também estão em menos de 64 mil blocos), e se vários clientes estão carregando bloqueia toohello mesmo BLOB em paralelo. Você também deve verificar as métricas por minuto de Olá picos de número de saudação de solicitações que resultam em exceder Olá por segundo metas de escalabilidade: Consulte também "[métricas mostram um aumento no PercentTimeoutError]."

Se você estiver vendo alto **AverageServerLatency** para solicitações de download de blob quando há são repetidas solicitações Olá mesmo blob ou conjunto de blobs, em seguida, considere cache esses blobs usando o Cache do Azure ou Olá fornecimento de conteúdo do Azure CDN (rede). Para solicitações de carregamento, você pode melhorar a taxa de transferência hello usando um tamanho de bloco maior. Para consultas tootables, é também possível tooimplement cache do cliente nos clientes que executam Olá mesmo operações de consulta e onde Olá dados não são alterados com frequência.

Alta **AverageServerLatency** valores também podem ser um sintoma de tabelas criados inadequadamente ou acrescentam/precedem um padrão de consultas que resultam em operações de verificação ou que siga hello. Consulte "[métricas mostram um aumento no PercentThrottlingError]" para obter mais informações.

> [!NOTE]
> É possível encontrar uma lista de verificação de desempenho abrangente aqui: [Lista de verificação de escalabilidade e desempenho do Armazenamento do Microsoft Azure](storage-performance-checklist.md).
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>Você está sofrendo atrasos inesperados na entrega de mensagens na fila
Se houver um atraso entre o tempo de saudação um aplicativo adiciona um mensagem tooa fila e tempo de saudação torna-se disponível tooread da fila de saudação, você deve tomar Olá problema de saudação do toodiagnose as etapas a seguir:

* Verifique se o aplicativo hello com êxito é adicionando toohello fila de mensagens de saudação. Verifique se o aplicativo hello não está repetindo Olá **AddMessage** método várias vezes antes de ter êxito. logs de biblioteca de cliente de armazenamento Olá mostrará qualquer várias tentativas de operações de armazenamento.
* Verifique não se há nenhum relógio distorção entre as funções de trabalho Olá que adiciona a fila de toohello de mensagens de saudação e função de trabalho de saudação que lê a mensagem de saudação da fila de saudação que torna aparecem como se houver um atraso no processamento.
* Verifique se a função de trabalho Olá que lê mensagens de saudação Olá fila está falhando. Se um cliente de fila chama Olá **GetMessage** método falhar mas toorespond com uma confirmação, mensagem de saudação permanecerão visíveis em fila Olá até Olá **invisibilityTimeout** expirar. Neste ponto, a mensagem de saudação ficarão disponível para processar novamente.
* Verifique se o comprimento da fila de saudação está aumentando ao longo do tempo. Isso pode ocorrer se você não tem suficiente tooprocess de trabalhadores disponíveis todos Olá mensagens que outros trabalhadores estão colocando na fila de saudação. Você também deve verificar Olá métricas toosee se excluir solicitações estão falhando e hello dequeue contagem de mensagens, que pode indicar repetidos mensagem de saudação toodelete tentativas com falha.
* Examine os logs de log de armazenamento Olá para qualquer operação de fila que têm maior do que o esperado **E2ELatency** e **ServerLatency** valores ao longo de um período de tempo maior que o normal.

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>As métricas mostram um aumento em PercentThrottlingError
Erros de restrição ocorrem ao exceder os destinos de escalabilidade de saudação de um serviço de armazenamento. serviço de armazenamento de saudação faz essa tooensure que nenhum cliente único ou Locatário pode usar o serviço de saudação à custa de saudação de outras pessoas. Para saber mais, consulte <a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">Metas de desempenho e de escalabilidade do Armazenamento do Azure</a> para obter detalhes sobre alvos de escalabilidade para contas de armazenamento e alvos de desempenho para partições dentro de contas de armazenamento.

Se hello **PercentThrottlingError** métrica mostrar um aumento na porcentagem de saudação de solicitações que falham com um erro de limitação, é necessário tooinvestigate um destes dois cenários:

* [Aumento transitório em PercentThrottlingError]
* [Aumento permanente em erro de PercentThrottlingError]

Um aumento no **PercentThrottlingError** geralmente ocorre em Olá ao mesmo tempo como um aumento no número de saudação de solicitações de armazenamento ou quando você estiver inicialmente carregar testar seu aplicativo. Isso pode também se manifestar no cliente hello como "503 servidor ocupado" ou mensagens de status HTTP "500 tempo limite da operação" de operações de armazenamento.

#### <a name="transient-increase-in-PercentThrottlingError"></a>Aumento transitório em PercentThrottlingError
Se você estiver vendo picos no valor de saudação do **PercentThrottlingError** que coincidam com períodos de alta atividade para o aplicativo hello, você deve implementar uma (não linear) de retirada exponencial estratégia para repetições no seu cliente: isso irá reduzir a carga de imediato saudação na partição hello e ajudar a toosmooth seu aplicativo os picos no tráfego. Para obter mais informações sobre como as políticas de repetição de tooimplement usando Olá biblioteca de cliente de armazenamento, consulte <a href="http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx" target="_blank">Microsoft.WindowsAzure.Storage.RetryPolicies Namespace</a> no MSDN.

> [!NOTE]
> Você também poderá ver picos no valor de saudação do **PercentThrottlingError** que não coincidem com períodos de alta atividade para o aplicativo hello: causa mais provável Olá aqui é o serviço de armazenamento de saudação mover partições tooimprove carga balanceamento.
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>Aumento permanente em erro de PercentThrottlingError
Se você estiver vendo um valor consistentemente alto **PercentThrottlingError** um aumento permanente em seus volumes de transações, ou quando você está executando a carga inicial a seguir testa seu aplicativo, você precisará tooevaluate como o seu aplicativo estiver usando partições de armazenamento e se ele está se aproximando alvos de escalabilidade de saudação para uma conta de armazenamento. Por exemplo, se você estiver vendo limitação de erros em uma fila (o que conta como uma única partição), em seguida, você deve considerar usando transações de saudação toospread filas adicionais por várias partições. Se você estiver vendo limitação de erros em uma tabela, você precisa tooconsider usando um toospread de esquema de particionamento diferente suas transações por várias partições usando uma grande variedade de valores de chave de partição. Uma causa comum desse problema é Olá preceda/anexar um padrão onde selecione date de hello como chave de partição hello e, em seguida, todos os dados em um determinado dia é gravado partição tooone: sob carga, isso pode resultar em um afunilamento de gravação. Considere um design de partição diferente ou avalie se usando um armazenamento de blob pode ser uma solução melhor. Você também deve verificar se Olá limitação está ocorrendo como resultado de picos no seu tráfego e investigar maneiras de suavização padrão de solicitações.

Se você distribuir as transações por várias partições, você ainda deve estar atento a limites de escalabilidade Olá definido para a conta de armazenamento hello. Por exemplo, se você usou dez filas cada máximo de saudação do processamento de 2.000 mensagens de 1KB por segundo, você correrá Olá limite total de 20.000 mensagens por segundo Olá conta de armazenamento. Se você precisar de mais de 20.000 entidades por segundo tooprocess, considere a possibilidade de usar várias contas de armazenamento. Você também tenha em mente esse tamanho de saudação de suas solicitações e entidades tem um impacto no quando o serviço de armazenamento de saudação limita seus clientes: se você tem maior de solicitações e entidades, você pode ser limitada mais cedo.

Design de consulta ineficiente também pode causar toohit limites de escalabilidade Olá para partições de tabela. Por exemplo, uma consulta com um filtro que seleciona apenas um por cento de entidades de saudação em uma partição, mas que examina todas as entidades de saudação em uma partição precisará tooaccess cada entidade. Cada entidade ler contará até número total de saudação de transações nessa partição; Portanto, você pode acessar facilmente os destinos de escalabilidade de saudação.

> [!NOTE]
> Seu teste de desempenho deve revelar qualquer design de consulta ineficiente em sua partição.
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>As métricas mostram um aumento em PercentTimeoutError
Suas métricas mostram um aumento em **PercentTimeoutError** para um dos seus serviços de armazenamento. A saudação mesmo momento, hello cliente recebe um alto volume de mensagens de status HTTP "500 tempo limite da operação" de operações de armazenamento.

> [!NOTE]
> Você pode ver erros de tempo limite temporariamente como serviço de armazenamento de saudação carregar solicitações de saldos movendo um novo servidor de partição tooa.
> 
> 

Olá **PercentTimeoutError** métrica é uma agregação de saudação métricas a seguir: **ClientTimeoutError**, **AnonymousClientTimeoutError**,  **SASClientTimeoutError**, **ServerTimeoutError**, **AnonymousServerTimeoutError**, e **SASServerTimeoutError**.

tempos limite do servidor de saudação é causado por um erro no servidor de saudação. tempos limite do cliente Olá acontece porque uma operação no servidor de saudação excedeu o tempo limite de saudação especificado pelo cliente Olá; Por exemplo, um cliente usando Olá biblioteca de cliente de armazenamento pode definir um tempo limite para uma operação usando Olá **Servertimeou** propriedade Olá **QueueRequestOptions** classe.

Tempos limite do servidor indica um problema com o serviço de armazenamento de saudação que exige a investigação. Você pode usar métricas toosee se está atingindo os limites de escalabilidade Olá para o serviço de saudação e tooidentify qualquer picos no tráfego que possam estar causando o problema. Se o problema de saudação intermitente, pode ser devido balanceamento tooload atividade no serviço de saudação. Se o problema de saudação é persistente e não é provocado por seu aplicativo atingindo os limites de escalabilidade de saudação do serviço hello, você deve gerar um problema de suporte. Para tempos limite do cliente, você deve decidir se Olá timeout estiver definido como valor adequado tooan no cliente de saudação ou valor de tempo limite de saudação alteração definido no cliente de saudação ou investigar como você pode melhorar o desempenho de saudação das operações de saudação no serviço de armazenamento de saudação para exemplo otimizar suas consultas de tabela ou reduzindo o tamanho de saudação das mensagens.

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>As métricas mostram um aumento em PercentNetworkError
Suas métricas mostram um aumento em **PercentNetworkError** para um dos seus serviços de armazenamento. Olá **PercentNetworkError** métrica é uma agregação de saudação métricas a seguir: **NetworkError**, **AnonymousNetworkError**, e  **SASNetworkError**. Elas ocorrem quando o serviço de armazenamento de saudação detecta um erro de rede quando Olá cliente faz uma solicitação de armazenamento.

Olá, a causa mais comum desse erro é um cliente desconectando antes de um tempo limite expira no serviço de armazenamento de saudação. Você deve investigar código Olá no seu toounderstand de cliente por que e quando cliente Olá desconecta do serviço de armazenamento de saudação. Você também pode usar o Wireshark, Microsoft Message Analyzer ou Tcping tooinvestigate problemas de conectividade de rede de cliente hello. Essas ferramentas são descritas no hello [apêndices].

### <a name="the-client-is-receiving-403-messages"></a>Olá está recebendo mensagens HTTP 403 (proibido)
Se seu aplicativo cliente está gerando erros HTTP 403 (proibido), uma causa provável é que o cliente hello está usando um expiradas SAS Shared Access Signature () quando ele envia uma solicitação de armazenamento (embora outras causas possíveis incluem chaves inválido, distorção do relógio e vazia cabeçalhos). Se uma chave SAS expirada for causa hello, você não verá as entradas nos dados do log de log de armazenamento do servidor de saudação. Olá tabela a seguir mostra um exemplo de log de cliente de Olá gerado pelo Olá biblioteca de cliente de armazenamento que ilustra este problema ocorrendo:

| Fonte | Detalhamento | Detalhamento | ID de solicitação do cliente | Texto de operação |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab-… |Inicialização da operação com o local principal por modo de local PrimaryOnly. |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab -… |Iniciando síncrona solicitação toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14&amp;sr = c&amp;si = mypolicy&amp;sig = OFnd4Rd7z01fIvh % 2BmcR6zbudIH2F5Ikm % 2FyhNYZEmJNQ % 3D&amp;api-version = 2014-02-14. |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab -… |Esperando uma resposta. |
| Microsoft.WindowsAzure.Storage |Aviso |2 |85d077ab -… |Exceção acionada ao aguardar resposta: servidor de saudação remoto retornou um erro: proibido (403). |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab -… |Resposta recebida. Status code = 403, Request ID = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d, Content-MD5 = , ETag = . |
| Microsoft.WindowsAzure.Storage |Aviso |2 |85d077ab -… |Exceção lançada durante a operação de saudação: servidor de saudação remoto retornou um erro: proibido (403). |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab -… |Verificando se a operação de saudação deve ser repetida. Contagem de repetições = 0, o código de status HTTP = 403, exceção = Olá no servidor remoto retornada um erro: proibido (403). |
| Microsoft.WindowsAzure.Storage |Informações |3 |85d077ab -… |próximo local de saudação definiu tooPrimary, com base no modo do local de saudação. |
| Microsoft.WindowsAzure.Storage |Erro |1 |85d077ab -… |A política de repetição não permitiu uma nova tentativa. Falha com o servidor remoto Olá retornou um erro: proibido (403). |

Nesse cenário, você deve investigar por que Olá SAS token irá expirar antes do cliente Olá envia server de token toohello hello:

* Normalmente, você não deve definir uma hora de início, quando você cria um SAS para um cliente toouse imediatamente. Se há pequenas diferenças de relógio entre o host de saudação gerando Olá SAS usando Olá hora atual e o serviço de armazenamento Olá, em seguida, é possível tooreceive de serviço de armazenamento de saudação uma SAS que ainda não é válida.
* Não defina um tempo de expiração muito curto na SAS. Novamente, diferenças pequeno relógio entre o host de saudação gerando Olá SAS e o serviço de armazenamento Olá pode levar tooa SAS aparentemente expirar antes que o antecipado.
* Olá parâmetro de versão na chave SAS hello (por exemplo **VA = 2012-02-12**) versão correspondência Olá Olá biblioteca de cliente de armazenamento, você está usando. Você sempre deve usar a versão mais recente de saudação do hello biblioteca de cliente de armazenamento. Para obter mais informações sobre controle de versão token SAS, consulte [Novidades para o Armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/14/what-s-new-for-microsoft-azure-storage-at-teched-2014.aspx).
* * Se você regenerar suas chaves de acesso de armazenamento (clique **gerenciar chaves de acesso** em qualquer página de sua conta de armazenamento Olá Portal clássico do Azure) isso pode invalidar todos os tokens SAS existentes. Isso pode ser um problema se você gerar tokens SAS com um tempo de expiração do tempo para toocache de aplicativos cliente.

Se você estiver usando tokens SAS de toogenerate Olá biblioteca de cliente de armazenamento, é fácil toobuild um token válido. No entanto, se você estiver usando Olá API REST de armazenamento e criar tokens SAS Olá manualmente cuidadosamente leia o tópico de saudação <a href="http://msdn.microsoft.com/library/azure/ee395415.aspx" target="_blank">delegando acesso com uma assinatura de acesso compartilhado</a> no MSDN.

### <a name="the-client-is-receiving-404-messages"></a>Olá está recebendo mensagens HTTP 404 (não encontrado)
Se o aplicativo de cliente hello recebe uma mensagem HTTP 404 (não encontrado) do servidor de saudação, isso implica que Olá objeto Olá o cliente tentava toouse (como uma entidade, tabela, blob, contêiner ou fila) não existe no serviço de armazenamento de saudação. Existem muitas razões para isso, tais como:

* [cliente de saudação ou outro objeto de saudação do processo excluído anteriormente]
* [Um problema de autorização de assinatura de acesso compartilhado (SAS)]
* [Código de JavaScript do lado do cliente não tem objeto de permissão do hello tooaccess]
* [Falha de rede]

#### <a name="client-previously-deleted-the-object"></a>cliente de saudação ou outro objeto de saudação do processo excluído anteriormente
Em cenários em que o cliente do hello está tentando tooread, atualização ou exclusão de dados em um serviço de armazenamento normalmente é fácil tooidentify no lado do servidor de saudação registra uma operação anterior que excluiu o objeto de saudação em questão no serviço de armazenamento de saudação. Com frequência, dados de log de saudação mostram outro usuário ou processo objeto Olá excluído. No log do log de armazenamento do saudação do servidor, hello tipo de operação e as colunas de chave solicitado de objeto mostram quando um cliente excluiu um objeto.

Cenário de saudação onde um cliente está tentando tooinsert um objeto, ele pode não ser imediatamente óbvio por que isso resulta em uma resposta HTTP 404 (não encontrado), considerando que hello cliente está criando um novo objeto. No entanto, se o cliente de saudação é a criação de um blob que ele deve ser toofind capaz de contêiner de blob hello, se o cliente hello está criando uma mensagem deve ser capaz de toofind uma fila, e se o cliente hello está adicionando uma linha deve ser capaz de toofind Olá tabela.

Você pode usar o log de cliente de saudação do hello biblioteca de cliente de armazenamento toogain que uma mais detalhada sobre o quando o cliente Olá envia solicitações específicas toohello serviço de armazenamento.

Hello seguinte log do lado do cliente gerado pela biblioteca de cliente de armazenamento Olá ilustra Olá problema quando o cliente Olá não é possível localizar o contêiner de saudação blob hello está criando. Esse log inclui detalhes de saudação operações de armazenamento a seguir:

| ID de solicitação | Operação |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists** contêiner de blob de saudação do método toodelete. Observe que essa operação inclui um **HEAD** toocheck existência de saudação do contêiner de saudação de solicitação. |
| e2d06d78… |**CreateIfNotExists** contêiner de blob de saudação do método toocreate. Observe que essa operação inclui um **HEAD** solicitação que verifica a existência de saudação do contêiner de saudação. Olá **HEAD** retorna uma mensagem 404, mas continua. |
| de8b1c3c-... |**UploadFromStream** blob de saudação do método toocreate. Olá **colocar** solicitação falha com uma mensagem 404 |

Entradas de log:

| ID de solicitação | Texto de operação |
| --- | --- |
| 07b26a5d-... |Iniciando toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer solicitação síncrona. |
| 07b26a5d-... |StringToSign = HEAD............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Esperando uma resposta. |
| 07b26a5d-... |Resposta recebida. Status code = 200, Request ID = eeead849-...Content-MD5 = , ETag =    &quot;0x8D14D2DC63D059B&quot;. |
| 07b26a5d-... |Cabeçalhos de resposta foram processados com êxito, continuando com o restante da saudação da operação de saudação. |
| 07b26a5d-... |Baixar o corpo da resposta. |
| 07b26a5d-... |Operação concluída com sucesso. |
| 07b26a5d-... |Iniciando toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer solicitação síncrona. |
| 07b26a5d-... |StringToSign = DELETE............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:12    GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Esperando uma resposta. |
| 07b26a5d-... |Resposta recebida. Status code = 202, Request ID = 6ab2a4cf-..., Content-MD5 = , ETag = . |
| 07b26a5d-... |Cabeçalhos de resposta foram processados com êxito, continuando com o restante da saudação da operação de saudação. |
| 07b26a5d-... |Baixar o corpo da resposta. |
| 07b26a5d-... |Operação concluída com sucesso. |
| e2d06d78-... |Iniciando toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer solicitação assíncrona.</td> |
| e2d06d78-... |StringToSign = HEAD............x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Esperando uma resposta. |
| de8b1c3c-... |Iniciando toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt solicitação síncrona. |
| de8b1c3c-... |StringToSign = PUT...64.qCmF+TQLPhq/YYK50mP9ZQ==........x-ms-blob-type:BlockBlob.x-ms-client-request-id:de8b1c3c-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |Preparando dados de solicitação toowrite. |
| e2d06d78-... |Exceção acionada ao aguardar resposta: servidor de saudação remoto retornou um erro: (404) não encontrado. |
| e2d06d78-... |Resposta recebida. Status code = 404, Request ID = 353ae3bc-..., Content-MD5 = , ETag = . |
| e2d06d78-... |Cabeçalhos de resposta foram processados com êxito, continuando com o restante da saudação da operação de saudação. |
| e2d06d78-... |Baixar o corpo da resposta. |
| e2d06d78-... |Operação concluída com sucesso. |
| e2d06d78-... |Iniciando toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer solicitação assíncrona. |
| e2d06d78-... |StringToSign = PUT...0.........x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Esperando uma resposta. |
| de8b1c3c-... |Gravação dos dados solicitados. |
| de8b1c3c-... |Esperando uma resposta. |
| e2d06d78-... |Exceção acionada ao aguardar resposta: servidor de saudação remoto retornou um erro: (409) conflito. |
| e2d06d78-... |Resposta recebida. Status code = 409, Request ID = c27da20e-..., Content-MD5 = , ETag = . |
| e2d06d78-... |Erro ao baixar o corpo da resposta. |
| de8b1c3c-... |Exceção acionada ao aguardar resposta: servidor de saudação remoto retornou um erro: (404) não encontrado. |
| de8b1c3c-... |Resposta recebida. Status code = 404, Request ID = 0eaeab3e-..., Content-MD5 = , ETag = . |
| de8b1c3c-... |Exceção lançada durante a operação de saudação: servidor de saudação remoto retornou um erro: (404) não encontrado. |
| de8b1c3c-... |A política de repetição não permitiu uma nova tentativa. Falha com o servidor remoto Olá retornou um erro: (404) não encontrado. |
| e2d06d78-... |A política de repetição não permitiu uma nova tentativa. Falha com o servidor remoto Olá retornou um erro: (409) conflito. |

Neste exemplo, o log de saudação mostra que o cliente Olá é intercalação solicitações de saudação **CreateIfNotExists** método (solicitação id e2d06d78...) com solicitações de saudação do hello **UploadFromStream** (método: de8b1c3c-...); Isso ocorre porque o aplicativo de cliente hello é chamar esses métodos assincronamente. Você deve modificar o código assíncrono Olá Olá cliente tooensure que ele cria o contêiner de saudação antes de tentar tooupload qualquer blob de tooa dados nesse contêiner. Idealmente, crie todos os contêineres antes.

#### <a name="SAS-authorization-issue"></a>Um problema de autorização de assinatura de acesso compartilhado (SAS)
Se o aplicativo de cliente hello tentativas toouse uma chave SAS que não tem as permissões necessárias para a operação de Olá Olá, o serviço de armazenamento de saudação retorna um cliente de toohello de mensagem HTTP 404 (não encontrado). A saudação mesmo momento, você também verá um valor diferente de zero para **SASAuthorizationError** em métricas de saudação.

Olá, a tabela a seguir mostra um exemplo de mensagem de log do servidor de arquivo de log de log de armazenamento hello:

| Nome | Valor |
| --- | --- |
| Hora de início da solicitação | 2014-05-30T06:17:48.4473697Z |
| Tipo de operação     | GetBlobProperties            |
| Status da solicitação     | SASAuthorizationError        |
| Código de status HTTP   | 404                          |
| Tipo de autenticação.| Sas                          |
| Tipo de serviço       | Blob                         |
| URL de Solicitação        | https://domemaildist.blob.core.windows.net/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ?sv=2014-02-14&sr=c&si=mypolicy&sig=XXXXX&;api-version=2014-02-14 |
| Cabeçalho da id de solicitação do   | a1f348d5-8032-4912-93ef-b393e5252a3b |
| ID de solicitação do cliente  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |

Você deve investigar por que o aplicativo cliente está tentando tooperform uma operação que não foram concedida permissões.

#### <a name="JavaScript-code-does-not-have-permission"></a>Código de JavaScript do lado do cliente não tem objeto de permissão do hello tooaccess
Se você estiver usando um cliente JavaScript e o serviço de armazenamento hello está retornando mensagens HTTP 404, você verificar Olá erros de JavaScript no navegador Olá a seguir:

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> Você pode usar as ferramentas de desenvolvedor F12 Olá no Internet Explorer tootrace Olá mensagens trocadas entre o navegador hello e serviço de armazenamento hello quando você estiver solucionando problemas de JavaScript do lado do cliente.
> 
> 

Esses erros ocorrem porque o navegador da web de saudação implementa Olá <a href="http://www.w3.org/Security/wiki/Same_Origin_Policy" target="_blank">política de mesma origem</a> proveniente de restrição de segurança que impede que uma página da web chamar uma API em um domínio diferente da página de saudação do domínio hello.

toowork em torno de saudação problema de JavaScript, você pode configurar CORS recursos entre origens de compartilhamento () para o cliente de saudação do serviço de armazenamento de saudação está acessando. Para saber mais, veja <a href="http://msdn.microsoft.com/library/azure/dn535601.aspx" target="_blank">Suporte de CORS (Compartilhamento de Recursos entre Origens) para os Serviços de Armazenamento do Azure</a> no MSDN.

saudação de exemplo de código a seguir mostra como tooconfigure o serviço blob tooallow JavaScript em execução no hello tooaccess do domínio Contoso um blob em seu serviço de armazenamento de blob:

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>Falha de rede
Em algumas circunstâncias, os pacotes de rede perdida podem levar o serviço de armazenamento toohello retornando o cliente de toohello de mensagens HTTP 404. Por exemplo, ao seu aplicativo cliente é excluir uma entidade de serviço de tabela de saudação você ver cliente Olá lançar uma exceção de armazenamento reporting um "HTTP 404 (não encontrado)" mensagem de status do serviço tabela hello. Ao examinar a tabela Olá no serviço de armazenamento de tabela Olá, você verá que o serviço de saudação excluir entidade Olá conforme solicitado.

detalhes da exceção Olá no cliente Olá incluem a id de solicitação de saudação (7e84f12d...) atribuída pelo serviço de tabela Olá para solicitação de saudação: você pode usar este detalhes da solicitação de saudação toolocate informações nos logs de armazenamento no servidor de saudação pesquisando no hello  **cabeçalho da id de solicitação** coluna no arquivo de log de saudação. Você também pode usar o hello métricas tooidentify quando as falhas de como isso pode ocorrer e procure os arquivos de log Olá com base nas métricas de saudação do tempo Olá registradas esse erro. Este mostra de entrada de log que Olá delete falha com uma mensagem de status "Cliente outro erro HTTP (404)". Olá mesma entrada de log também inclui id da solicitação Olá gerado pelo cliente Olá Olá **client-request-id** coluna (813ea74f...).

log do lado do servidor de saudação também inclui outra entrada com hello mesmo **client-request-id** operação para excluir o valor (813ea74f...) para o sucesso Olá mesma entidade e de Olá mesmo cliente. Esta operação de exclusão bem-sucedida ocorreu muito pouco antes de solicitação de exclusão com falha hello.

Olá deste cenário é provável que o cliente Olá enviado uma solicitação de exclusão para o serviço tabela do hello entidade toohello, que foi bem-sucedida, mas não recebeu uma confirmação do servidor de saudação (talvez devido a problema de rede temporários tooa). cliente Olá automaticamente tentada novamente a operação de saudação (usando Olá mesmo **client-request-id**), e essa nova tentativa falhou porque a entidade de saudação já foi excluída.

Se esse problema ocorrer com frequência, você deve investigar por que o cliente hello está falhando tooreceive confirmações do serviço tabela hello. Se o problema de saudação intermitente, você deve interceptar a mensagem de erro "HTTP (404) não encontrado" hello e efetuar login cliente hello, mas permitir Olá toocontinue de cliente.

### <a name="the-client-is-receiving-409-messages"></a>Olá está recebendo mensagens HTTP 409 (conflito)
Olá, tabela a seguir mostra um extrato do log do lado do servidor Olá duas operações de cliente: **DeleteIfExists** seguido imediatamente por **CreateIfNotExists** usando Olá o mesmo nome de contêiner de blob. Observe que cada operação de cliente resulta em duas solicitações enviadas toohello server, primeiro um **GetContainerProperties** toocheck solicitação se o contêiner de saudação existe, seguido por Olá **DeleteContainer** ou  **CreateContainer** solicitação.

| Timestamp | Operação | Result | Nome do contêiner | ID de solicitação do cliente |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-… |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-… |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-… |
| 05:10:14.2147723 |CreateContainer |409 |mmcont |bc881924-… |

Hello código no aplicativo de cliente hello exclui e depois recria imediatamente um contêiner de blob usando Olá mesmo nome: Olá **CreateIfNotExists** método (cliente solicitar ID bc881924-...), eventualmente, falha com hello HTTP 409 (conflito) erro. Quando um cliente exclui contêineres de blob, tabelas ou filas que há um breve período antes de nome hello fica disponível novamente.

aplicativo de cliente Hello deve usar nomes de contêiner exclusivo sempre que ele cria novos contêineres se Olá Excluir/recriar padrão é comum.

### <a name="metrics-show-low-percent-success"></a>As métricas mostram uma baixa PercentSuccess ou as entradas de log analíticas têm operações com status de transação de ClientOtherErrors
Olá **PercentSuccess** métrica captura a porcentagem de saudação de operações foram bem-sucedidas, com base em seu código de Status HTTP. Operações com códigos de status de 2XX contam com êxito, enquanto as operações com códigos de status em intervalos de 3XX, 4XX e 5XX são contadas como Olá malsucedida e inferior **PercentSucess** valor de métrica. Nos arquivos de log de armazenamento no servidor de saudação, essas operações são registradas com um status de transação **ClientOtherErrors**.

É importante toonote que essas operações forem concluídas com êxito e, portanto, não afetam outras métricas como disponibilidade. Alguns exemplos de operações que executam com sucesso, mas que podem resultar em códigos de status HTTP sem sucesso incluem:

* **ResourceNotFound** (não encontrado 404), por exemplo de um GET solicitação tooa blob que não existe.
* **ResouceAlreadyExists** (409 Conflito), por exemplo, de um **CreateIfNotExist** operação em que o recurso de saudação já existe.
* **ConditionNotMet** (não modificados 304), por exemplo, de uma operação condicional, como quando um cliente envia uma **ETag** valor e um HTTP **If-None-Match** toorequest cabeçalho somente-se uma imagem ele foi atualizado desde a última operação de saudação.

Você pode encontrar uma lista de códigos de erro comuns API REST que retornam os serviços de armazenamento de saudação na página Olá <a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">códigos de erro de API REST comuns</a>.

### <a name="capacity-metrics-show-an-unexpected-increase"></a>As métricas de capacidade mostram um aumento inesperado em uso de capacidade de armazenamento
Se você vir repentinas, alterações inesperadas na capacidade de uso em sua conta de armazenamento, você pode investigar motivos Olá examinando primeiro suas métricas de disponibilidade; Por exemplo, um aumento no número de saudação de solicitações de exclusão com falha pode levar tooan aumento na quantidade de saudação do armazenamento de blob que você está usando como operações de limpeza específico de aplicativo, para que você talvez esperasse toobe liberando espaço pode não estar funcionando conforme o esperado ( exemplo, porque os tokens SAS Olá usados para liberar espaço expiraram).

### <a name="you-are-experiencing-unexpected-reboots"></a>Você está enfrentando reinicializações inesperadas das máquinas virtuais do Azure que contêm um grande número de VHDs anexados
Se uma máquina Virtual (VM) do Azure tem um grande número de VHDs anexados que estão em Olá mesma conta de armazenamento, você poderá exceder os destinos de escalabilidade Olá para uma conta de armazenamento individual causando Olá VM toofail. Você deve verificar as métricas de minuto Olá Olá conta de armazenamento (**TotalRequests**/**TotalIngress**/**TotalEgress**) para picos que exceder os destinos de escalabilidade Olá para uma conta de armazenamento. Consulte a seção hello "[métricas mostram um aumento no PercentThrottlingError]" para a assistência para determinar se a limitação ocorreu em sua conta de armazenamento.

Em geral, cada entrada individual ou a operação de saída em um VHD de uma máquina Virtual converte muito**página obter** ou **Put Page** operações em Olá subjacente de blob de página. Portanto, você pode usar Olá estimado IOPS para seu ambiente tootune quantos VHDs, você pode ter em uma única conta de armazenamento com base no comportamento específico de saudação do seu aplicativo. Não recomendamos ter mais do que 40 discos em uma única conta de armazenamento. Consulte <a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">escalabilidade do armazenamento do Azure e metas de desempenho</a> para obter detalhes de saudação atual metas da escalabilidade para contas de armazenamento, em particular Olá solicitação total taxa total de largura de banda e para o tipo de saudação da conta de armazenamento você está usando .
Se você está excedendo metas de escalabilidade Olá para sua conta de armazenamento, você deve colocar seus VHDs em vários armazenamento diferentes contas tooreduce hello atividade em cada conta individual.

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>O problema surge de usar o emulador de armazenamento Olá para desenvolvimento ou teste
Normalmente, você usa o emulador de armazenamento de saudação durante o desenvolvimento e teste o requisito de saudação tooavoid para uma conta de armazenamento do Azure. Olá problemas comuns que podem ocorrer quando você estiver usando o emulador de armazenamento Olá são:

* [Recurso "X" não está funcionando no emulador de armazenamento Olá]
* [Erro de "valor Olá para um dos cabeçalhos de saudação HTTP não está no formato correto hello" quando usando Olá emulador de armazenamento]
* [Emulador de armazenamento em execução Olá requer privilégios administrativos]

#### <a name="feature-X-is-not-working"></a>Recurso "X" não está funcionando no emulador de armazenamento Olá
emulador de armazenamento Olá não dá suporte a todos os recursos de saudação do serviços de armazenamento do Azure Olá como o serviço de arquivo hello. Para obter mais informações, consulte <a href="http://msdn.microsoft.com/library/azure/gg433135.aspx" target="_blank">Olá diferenças entre o emulador de armazenamento e serviços de armazenamento do Azure</a> no MSDN.

Para os recursos que Olá armazenamento emulador não dá suporte, usar o serviço de armazenamento do Azure Olá na nuvem hello.

#### <a name="error-HTTP-header-not-correct-format"></a>Erro de "valor Olá para um dos cabeçalhos de saudação HTTP não está no formato correto hello" quando usando Olá emulador de armazenamento
Você está testando seu aplicativo que usa Olá biblioteca de cliente de armazenamento em chamadas de emulador e o método de armazenamento local hello como **CreateIfNotExists** falha com erro Olá mensagem "hello valor para um dos cabeçalhos HTTP da saudação não pertence Olá formato correto." Isso indica que Olá versão do emulador de armazenamento Olá você está usando não oferece suporte para a versão de saudação da biblioteca de cliente de armazenamento Olá você está usando. Olá biblioteca de cliente de armazenamento adiciona o cabeçalho de saudação **x-ms-version** tooall Olá solicitações faz. Se o emulador de armazenamento Olá não reconhece o valor de saudação em Olá **x-ms-version** cabeçalho, ele rejeita a solicitação de saudação.

Você pode usar Olá cliente de biblioteca de armazenamento logs toosee Olá valor Olá **cabeçalho x-ms-version** está enviando. Você também pode ver o valor Olá Olá **cabeçalho x-ms-version** se você usar solicitações de saudação do Fiddler tootrace de seu aplicativo cliente.

Isso normalmente ocorre se você instala e usar a versão mais recente de saudação do hello biblioteca de cliente de armazenamento sem atualizar o emulador de armazenamento hello. Você deve instalar a versão mais recente saudação do emulador de armazenamento hello ou use armazenamento em nuvem em vez de emulador Olá para desenvolvimento e teste.

#### <a name="storage-emulator-requires-administrative-privileges"></a>Emulador de armazenamento em execução Olá requer privilégios administrativos
Quando você executar o emulador de armazenamento hello, você será solicitado para credenciais de administrador. Isso ocorre apenas quando estiver inicializando o emulador de armazenamento Olá para Olá primeira vez. Depois que inicializou o emulador de armazenamento hello, não é necessário privilégios administrativos toorun-a novamente.

Para obter mais informações, consulte <a href="http://msdn.microsoft.com/library/azure/gg433132.aspx" target="_blank">inicializar Olá emulador de armazenamento por hello usando a ferramenta de linha de comando</a> no MSDN (você também pode inicializar emulador de armazenamento Olá no Visual Studio, que também exige privilégios administrativos).

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>Você está encontrando problemas na instalação hello Azure SDK para .NET
Quando você tenta tooinstall Olá SDK, ele falha tentando emulador de armazenamento Olá tooinstall em seu computador local. log de instalação Olá contém uma das seguintes mensagens de saudação:

* CAQuietExec: Erro: não é possível tooaccess instância do SQL
* CAQuietExec: Erro: não é possível toocreate banco de dados

causa Olá é um problema com a instalação existente do LocalDB. Por padrão, o emulador de armazenamento Olá usa LocalDB toopersist dados quando ele simula os serviços de armazenamento do Azure hello. Você pode redefinir a sua instância do LocalDB executando Olá comandos em uma janela de prompt de comando a seguir antes de tentar tooinstall Olá SDK.

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

Olá **excluir** comando remove os arquivos de banco de dados antigos de instalações anteriores do emulador de armazenamento hello.

### <a name="you-have-a-different-issue-with-a-storage-service"></a>Você tem um problema diferente com um serviço de armazenamento
Se seções de solução de problemas anteriores Olá não incluir problema Olá com um serviço de armazenamento, você deve adotar Olá toodiagnosing abordagem a seguir e solucionar o problema.

* Verifique seu toosee de métricas se houver qualquer alteração de seu comportamento esperado de linha de base. De métricas de Olá, pode ser capaz de toodetermine se o problema de saudação é temporário ou permanente e as operações de armazenamento Olá problema está afetando.
* Você pode usar informações de métricas de saudação toohelp você pesquisar os dados de log do servidor para obter mais informações sobre os erros que estão ocorrendo. Essas informações podem ajudá-lo a solucionar problemas e resolver o problema de saudação.
* Se informações Olá nos logs do saudação do servidor não for suficiente tootroubleshoot Olá problema com êxito, você pode usar o comportamento de saudação do tooinvestigate do hello biblioteca de cliente de armazenamento logs do lado do cliente de seu aplicativo cliente e ferramentas como o Fiddler, o Wireshark, e o Microsoft Message Analyzer tooinvestigate sua rede.

Para obter mais informações sobre como usar o Fiddler, consulte "[Apêndice 1: tráfego HTTP e HTTPS toocapture usando Fiddler]."

Para obter mais informações sobre como usar o Wireshark, consulte "[Apêndice 2: tráfego de rede usando o Wireshark toocapture]."

Para obter mais informações sobre como usar o Microsoft Message Analyzer, consulte "[apêndice 3: tráfego de rede usando o Microsoft Message Analyzer toocapture]."

## <a name="appendices"></a>Anexos
Apêndices Olá descrevem várias ferramentas que podem ser úteis ao diagnosticar e solucionar problemas com o armazenamento do Azure (e outros serviços). Essas ferramentas não são parte do armazenamento do Azure e alguns são produtos de terceiros. Como tal, ferramentas Olá abordadas nesses apêndices não são cobertas por um contrato de suporte que você possa ter com o Microsoft Azure ou armazenamento do Azure e, portanto, como parte do processo de avaliação, você deve examinar opções de licenciamento e suporte de saudação disponíveis do provedores de saudação dessas ferramentas.

### <a name="appendix-1"></a>Apêndice 1: Usando o Fiddler toocapture HTTP e o tráfego HTTPS
O Fiddler é uma ferramenta útil para analisar o tráfego HTTP e HTTPS Olá entre o aplicativo cliente e Olá serviço de armazenamento do Azure que você está usando. É possível baixar o Fiddler no site <a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a>.

> [!NOTE]
> Fiddler pode decodificar o tráfego HTTPS; Você deve ler a documentação do Fiddler Olá cuidadosamente toounderstand como ele faz isso e as implicações de segurança do toounderstand hello.
> 
> 

Este apêndice fornece uma breve explicação passo a passo de como tooconfigure Fiddler toocapture tráfego entre o computador de saudação local onde você instalou o Fiddler e Olá serviços de armazenamento do Azure.

Após você ter iniciado o Fiddler, ele começará capturar o tráfego HTTP e HTTPS da sua máquina local. Olá seguem alguns comandos úteis para controlar o Fiddler:

* Parar e iniciar a captura de tráfego. No menu principal do hello, vá muito**arquivo** e, em seguida, clique em **capturar tráfego** tootoggle capturando e desativar.
* Salve os dados de tráfego capturados. No menu principal do hello, vá muito**arquivo**, clique em **salvar**e, em seguida, clique em **todas as sessões**: Isso permite o tráfego de saudação toosave em um arquivo de sessão. Você pode recarregar um arquivo de sessão mais tarde para análise ou enviá-los se a solicitação de suporte de tooMicrosoft.

quantidade de saudação toolimit de tráfego que captura o Fiddler, você pode usar filtros que você configurar no hello **filtros** Olá guia captura de tela a seguir mostra um filtro que captura somente toohello de tráfego enviado  **contosoemaildist.Table.Core.Windows.NET** ponto de extremidade de armazenamento:

![][5]

### <a name="appendix-2"></a>Apêndice 2: Usando o Wireshark toocapture o tráfego de rede
O Wireshark é um analisador de protocolo de rede que permite que você tooview pacote informações detalhadas para uma ampla variedade de protocolos de rede. É possível baixar o Wireshark no site <a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a>.

Olá procedimento a seguir mostra como toocapture pacote informações detalhadas sobre o tráfego de máquina local Olá onde você instalou o serviço de tabela Wireshark toohello em sua conta de armazenamento do Azure.

1. Habilite o Wireshark no seu computador local.
2. Em Olá **iniciar** seção, interface de rede local Olá select ou interfaces que são toohello conectado à internet.
3. Clique em **Opções de Captura**.
4. Adicionar um filtro toohello **filtro de captura** caixa de texto. Por exemplo, **host contosoemaildist.table.core.windows.net** configurará o Wireshark toocapture somente pacotes enviados tooor do ponto de extremidade do serviço de tabela de saudação em hello **contosoemaildist** armazenamento conta. Para obter uma lista completa de Filtros de Captura, veja <a href="http://wiki.wireshark.org/CaptureFilters" target="_blank">http://wiki.wireshark.org/CaptureFilters</a>.
   
   ![][6]
5. Clique em **Iniciar**. Wireshark agora irá capturar todos os tooor de envio de pacotes Olá do ponto de extremidade de serviço de tabela Olá como usar o aplicativo cliente no computador local.
6. Quando terminar, Olá menu principal, clique em **capturar** e **parar**.
7. Olá toosave capturados dados em arquivo de captura Wireshark, Olá menu principal, clique em **arquivo** e **salvar**.

WireShark realçará os erros que existem no hello **packetlist** janela. Você também pode usar o hello **informações de especialistas** janela (clique **analisar**, em seguida, **especialista em informações**) tooview um resumo de erros e avisos.

![][7]

Você também poderá dados TCP tooview hello como camada de aplicativo hello vê-lo clicando duas vezes em Olá dados TCP e selecionando **siga o fluxo TCP**. Isso é bastante útil se você capturou o seu despejo sem o filtro de captura. Clique <a href="http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html" target="_blank">aqui</a> para saber mais.

![][8]

> [!NOTE]
> Para obter mais informações sobre como usar o Wireshark, consulte Olá <a href="http://www.wireshark.org/docs/wsug_html_chunked/" target="_blank">guia do usuário Wireshark</a>.
> 
> 

### <a name="appendix-3"></a>Apêndice 3: Usando o tráfego de rede do Microsoft Message Analyzer toocapture
Você pode usar o Microsoft Message Analyzer toocapture HTTP e o tráfego HTTPS em um tooFiddler de maneira semelhante e capturar o tráfego de rede em um tooWireshark de maneira semelhante.

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>Configure a sessão de rastreamento Web usando o Microsoft Message Analyzer
tooconfigure uma sessão de rastreamento da web para o tráfego HTTP e HTTPS usando o Microsoft Message Analyzer, execute o aplicativo do Microsoft Message Analyzer hello e, em seguida, em Olá **arquivo** menu, clique em **/rastreamento de captura**. Na lista de saudação de cenários de rastreamento disponíveis, selecione **Proxy da Web**. Em seguida no hello **configuração de cenário de rastreamento** painel Olá **HostnameFilter** caixa de texto, adicione nomes de saudação dos seus pontos de extremidade de armazenamento (você pode procurar esses nomes Olá Portal clássico do Azure). Por exemplo, se hello nome da sua conta de armazenamento do Azure é **contosodata**, você deve adicionar Olá após toohello **HostnameFilter** caixa de texto:

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> Um caractere de espaço separa Olá nomes de host.
> 
> 

Quando você estiver pronto toostart coletando dados de rastreamento, clique em Olá **Start With** botão.

Para obter mais informações sobre Olá Microsoft Message Analyzer **Proxy Web** de rastreamento, consulte <a href="http://technet.microsoft.com/library/jj674814.aspx" target="_blank">provedor PEF WebProxy</a> no TechNet.

Olá interna **Proxy Web** rastreamento no Microsoft Message Analyzer se baseia o Fiddler; ele pode capturar o tráfego HTTPS do lado do cliente e exibir mensagens HTTPS não criptografadas. Olá **Proxy Web** funciona por meio da configuração de proxy local para todos os tráfego HTTP e HTTPS que concede acesso toounencrypted mensagens de rastreamento.

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>Diagnóstico dos problemas de rede usando o Microsoft Message Analyzer
Além disso, toousing Olá Microsoft Message Analyzer **Proxy Web** detalhes de toocapture de rastreamento de Olá tráfego HTTP/HTTPs entre o aplicativo de cliente Olá Olá serviço de armazenamento, você também pode usar internas Olá  **Camada de Link local** toocapture informações de pacotes de rede de rastreamento. Isso permite que você toocapture dados semelhantes toothat que podem ser capturados com o Wireshark e diagnosticar problemas de rede, como pacotes eliminados.

Olá, seguinte captura de tela mostra um exemplo **camada de Link Local** rastreamento com alguns **informativa** mensagens de saudação **DiagnosisTypes** coluna. Clicar em um ícone na Olá **DiagnosisTypes** coluna mostra detalhes de saudação de mensagem de saudação. Neste exemplo, servidor de saudação retransmitido mensagem #305 porque não recebeu uma confirmação de cliente hello:

![][9]

Quando você cria a sessão de rastreamento Olá no Microsoft Message Analyzer, você pode especificar a quantidade de saudação de tooreduce de filtros de ruído no rastreamento de saudação. Em Olá **capturar / rastreamento** página na qual definir o rastreamento de saudação, clique em Olá **configurar** próximo link muito**Microsoft-Windows-NDIS-PacketCapture**. Olá captura de tela a seguir mostra uma configuração que filtra o tráfego TCP para endereços IP hello dos três serviços de armazenamento:

![][10]

Para obter mais informações sobre Olá rastreamento de camada de Link Local do Microsoft mensagem analisador, consulte <a href="http://technet.microsoft.com/library/jj659264.aspx" target="_blank">provedor PEF-NDIS-PacketCapture</a> no TechNet.

### <a name="appendix-4"></a>Apêndice 4: Usando dados de log e métricas de tooview do Excel
Muitas ferramentas Ativar dados de métricas de armazenamento toodownload saudação do armazenamento de tabela do Azure em um formato delimitado que torna mais dados de saudação tooload fácil para o Excel para exibição e análise. Os dados de log de armazenamento do armazenamento de blob do Azure já estão em um formato delimitado que pode ser carregado no Excel. No entanto, você precisará tooadd títulos de coluna apropriada com base nas informações de saudação em <a href="http://msdn.microsoft.com/library/azure/hh343259.aspx" target="_blank">formato de Log de análise de armazenamento</a> e <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">esquema de tabela de métricas de análise de armazenamento</a>.

tooimport seus dados de log de armazenamento para o Excel depois de baixá-lo do armazenamento de blob:

* Em Olá **dados** menu, clique em **de texto**.
* Procurar arquivo de log toohello você deseja tooview e clique em **importação**.
* Na etapa 1 de saudação **Assistente de importação de texto**, selecione **delimitado**.

Na etapa 1 de saudação **Assistente de importação de texto**, selecione **-e-vírgula** como Olá somente delimitador e escolha aspas duplas como Olá **qualificador de texto**. Em seguida, clique em **concluir** e escolha onde tooplace Olá dados na pasta de trabalho.

### <a name="appendix-5"></a>Anexo 5: Monitoramento com o Application Insights no Visual Studio Team Services
Você também pode usar o recurso do Application Insights Olá para Visual Studio Team Services como parte de seu monitoramento de desempenho e disponibilidade. Essa ferramenta pode:

* Garantir que seu aplicativo da Web esteja disponível e respondendo. Se seu aplicativo é um site da web ou um aplicativo de dispositivo que usa um serviço web, ele pode testar a URL de tempos em tempos de locais Olá mundo e permitem que você saiba se há um problema.
* Diagnostique rapidamente qualquer problema de desempenho ou exceções no seu serviço da Web. Descubra se a CPU ou outros recursos estão sendo alongados, receba rastreamento de linhas de exceções e pesquise facilmente pelos rastreamentos de log. Se hello descartes de desempenho do aplicativo abaixo dos limites aceitáveis, nós podemos lhe enviar um email. Você pode monitorar os serviços Web .NET e Java.

Em Olá tempo de gravação do Application Insights está em visualização. Você pode encontrar mais informações no <a href="http://msdn.microsoft.com/library/azure/dn481095.aspx" target="_blank">Application Insights para Visual Studio Team Services</a> no MSDN.

<!--Anchors-->
[Introdução]: #introduction
[Como esse guia está organizado]: #how-this-guide-is-organized

[seu serviço de armazenamento de monitoramento]: #monitoring-your-storage-service
[Monitoramento da integridade do serviço]: #monitoring-service-health
[Monitoramento de capacidade]: #monitoring-capacity
[Monitoramento de disponibilidade]: #monitoring-availability
[Monitoramento de desempenho]: #monitoring-performance

[diagnosticar problemas de armazenamento]: #diagnosing-storage-issues
[Problemas de integridade do serviço]: #service-health-issues
[Problemas de desempenho]: #performance-issues
[Diagnóstico de erros]: #diagnosing-errors
[Problemas de emulador de armazenamento]: #storage-emulator-issues
[Ferramentas de log de armazenamento]: #storage-logging-tools
[Uso de ferramentas de log de rede]: #using-network-logging-tools

[rastreamento ponta a ponta]: #end-to-end-tracing
[Correlacionamento de dados de log]: #correlating-log-data
[ID de solicitação do cliente]: #client-request-id
[ID de solicitação do servidor]: #server-request-id
[Carimbos de data/hora]: #timestamps

[guia de solução de problemas]: #troubleshooting-guidance
[métricas mostram AverageE2ELatency alta e baixa AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[Métricas mostram AverageE2ELatency baixa e baixa AverageServerLatency mas cliente hello está apresentando alta latência]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[As métricas mostram alta AverageServerLatency]: #metrics-show-high-AverageServerLatency
[Você está sofrendo atrasos inesperados na entrega de mensagens na fila]: #you-are-experiencing-unexpected-delays-in-message-delivery

[métricas mostram um aumento no PercentThrottlingError]: #metrics-show-an-increase-in-PercentThrottlingError
[Aumento transitório em PercentThrottlingError]: #transient-increase-in-PercentThrottlingError
[Aumento permanente em erro de PercentThrottlingError]: #permanent-increase-in-PercentThrottlingError
[métricas mostram um aumento no PercentTimeoutError]: #metrics-show-an-increase-in-PercentTimeoutError
[As métricas mostram um aumento em PercentNetworkError]: #metrics-show-an-increase-in-PercentNetworkError

[Olá está recebendo mensagens HTTP 403 (proibido)]: #the-client-is-receiving-403-messages
[Olá está recebendo mensagens HTTP 404 (não encontrado)]: #the-client-is-receiving-404-messages
[cliente de saudação ou outro objeto de saudação do processo excluído anteriormente]: #client-previously-deleted-the-object
[Um problema de autorização de assinatura de acesso compartilhado (SAS)]: #SAS-authorization-issue
[Código de JavaScript do lado do cliente não tem objeto de permissão do hello tooaccess]: #JavaScript-code-does-not-have-permission
[Falha de rede]: #network-failure
[Olá está recebendo mensagens HTTP 409 (conflito)]: #the-client-is-receiving-409-messages

[métricas mostram PercentSuccess baixa ou entradas de log de análise possuem operações com status de transação de ClientOtherErrors]: #metrics-show-low-percent-success
[As métricas de capacidade mostram um aumento inesperado em uso de capacidade de armazenamento]: #capacity-metrics-show-an-unexpected-increase
[Você está enfrentando reinicializações inesperadas das máquinas virtuais que contêm um grande número de VHDs anexados]: #you-are-experiencing-unexpected-reboots
[O problema surge de usar o emulador de armazenamento Olá para desenvolvimento ou teste]: #your-issue-arises-from-using-the-storage-emulator
[Recurso "X" não está funcionando no emulador de armazenamento Olá]: #feature-X-is-not-working
[Erro de "valor Olá para um dos cabeçalhos de saudação HTTP não está no formato correto hello" quando usando Olá emulador de armazenamento]: #error-HTTP-header-not-correct-format
[Emulador de armazenamento em execução Olá requer privilégios administrativos]: #storage-emulator-requires-administrative-privileges
[Você está encontrando problemas na instalação hello Azure SDK para .NET]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[Você tem um problema diferente com um serviço de armazenamento]: #you-have-a-different-issue-with-a-storage-service

[apêndices]: #appendices
[Apêndice 1: tráfego HTTP e HTTPS toocapture usando Fiddler]: #appendix-1
[Apêndice 2: tráfego de rede usando o Wireshark toocapture]: #appendix-2
[apêndice 3: tráfego de rede usando o Microsoft Message Analyzer toocapture]: #appendix-3
[Apêndice 4: Usando dados de log e métricas de tooview do Excel]: #appendix-4
[apêndice 5: monitoramento com o Application Insights para Visual Studio Team Services]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/overview.png
[2]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/portal-screenshot.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-2.png
