---
title: "aaaUse dados de logs e métricas de análise de armazenamento do Azure toocollect | Microsoft Docs"
description: "Análise de armazenamento permite que os dados de métricas de tootrack para todos os serviços de armazenamento e toocollect logs para o armazenamento de Blob, fila e tabela."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7894993b-ca42-4125-8f17-8f6dfe3dca76
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: aba1a236cb69fa2e60bcb8fda5d34841e36e379a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-analytics"></a>Análise de Armazenamento

A análise de armazenamento do Azure executa registro em log e fornece dados de métrica para uma conta de armazenamento. Você pode usar este tootrace as solicitações de dados, analisar tendências de uso e diagnosticar problemas com sua conta de armazenamento.

toouse análise de armazenamento, você deve habilitá-lo individualmente para cada serviço, você deseja toomonitor. Você pode habilitá-lo da saudação [Portal do Azure](https://portal.azure.com). Para obter detalhes, consulte [monitorar uma conta de armazenamento hello Azure Portal](storage-monitor-storage-account.md). Você também pode habilitar a análise de armazenamento programaticamente por meio de saudação API REST ou biblioteca de saudação do cliente. Saudação de uso [obter propriedades do serviço Blob](https://msdn.microsoft.com/library/hh452239.aspx), [obter propriedades do serviço de fila](https://msdn.microsoft.com/library/hh452243.aspx), [obter propriedades do serviço de tabela](https://msdn.microsoft.com/library/hh452238.aspx), e [obter propriedades do serviço arquivo](https://msdn.microsoft.com/library/mt427369.aspx) tooenable operações análise de armazenamento para cada serviço.

dados agregados Hello são armazenados em um blob conhecido (para registro em log) e em tabelas conhecidas (para Métrica), que podem ser acessadas usando o serviço de Blob hello e APIs do serviço de tabela.

Análise de armazenamento tem um limite de 20 TB em quantidade Olá dos dados armazenados que são independentes do limite total de saudação para sua conta de armazenamento. Para saber mais sobre cobrança e políticas de retenção de dados, consulte [Análise de armazenamento e cobrança](https://msdn.microsoft.com/library/hh360997.aspx). Para saber mais sobre limites de contas de armazenamento, consulte [Escalabilidade e metas de desempenho do armazenamento do Azure](storage-scalability-targets.md).

Para obter um guia detalhado sobre como usar a análise de armazenamento e outra ferramentas tooidentify, diagnosticar e solucionar problemas relacionados ao armazenamento do Azure, consulte [monitorar, diagnosticar e solucionar problemas de armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="about-storage-analytics-logging"></a>Sobre o registro em log da Análise de Armazenamento
Análise de armazenamento registra informações detalhadas sobre o serviço de armazenamento de tooa de solicitações bem-sucedidas e com falha. Essas informações podem ser usadas toomonitor as solicitações individuais e toodiagnose problemas com um serviço de armazenamento. As solicitações são registradas em uma base de melhor esforço.

As entradas de log são criadas somente se houver atividade de serviço de armazenamento. Por exemplo, se uma conta de armazenamento tiver atividade em seu serviço Blob, mas não em seus serviços de tabela ou fila, somente os logs referentes toohello serviço Blob serão criados.

O Log de Análise de Armazenamento não está disponível para o Armazenamento de Arquivos do Azure.

### <a name="logging-authenticated-requests"></a>Solicitações de registro em log autenticadas
Olá seguintes tipos de solicitações autenticadas é registrado:

* Solicitações bem sucedidas.
* Solicitações com falha, incluindo o tempo limite, limitação, rede, autorização e outros erros.
* Solicitações que usam uma SAS (Assinatura de Acesso Compartilhado), incluindo solicitações bem-sucedidas e com falha.
* Dados de tooanalytics solicitações.

As solicitações feitas pela própria análise de armazenamento, como criação de log ou exclusão, não estão conectadas. Uma lista completa dos dados saudação conectado está documentada em Olá [operações registradas em log de análise de armazenamento e mensagens de Status](https://msdn.microsoft.com/library/hh343260.aspx) e [formato de Log de análise de armazenamento](https://msdn.microsoft.com/library/hh343259.aspx) tópicos.

### <a name="logging-anonymous-requests"></a>Registro em log de solicitações anônimas
Olá seguintes tipos de solicitações anônimas é registrado:

* Solicitações bem sucedidas.
* Erros do servidor.
* Erros de tempo limite para o cliente e servidor.
* Solicitações GET com falha com o código de erro 304 (não modificado).

Todas as outras solicitações anônimas com falha não estão conectadas. Uma lista completa dos dados saudação conectado está documentada em Olá [operações registradas em log de análise de armazenamento e mensagens de Status](https://msdn.microsoft.com/library/hh343260.aspx) e [formato de Log de análise de armazenamento](https://msdn.microsoft.com/library/hh343259.aspx) tópicos.

### <a name="how-logs-are-stored"></a>Como os logs são armazenados
Todos os logs são armazenados em blobs de bloco em um contêiner denominado $logs, que é criado automaticamente quando a análise de armazenamento é habilitada para uma conta de armazenamento. contêiner Olá $logs está localizado no namespace de blob Olá Olá da conta de armazenamento, por exemplo: `http://<accountname>.blob.core.windows.net/$logs`. Este contêiner não pode ser excluído quando a análise de armazenamento tiver sido habilitada, embora seu conteúdo possa ser excluído.

> [!NOTE]
> contêiner de saudação $logs não é exibida quando uma operação de listagem do contêiner é executado, como Olá [ListContainers](https://msdn.microsoft.com/library/azure/dd179352.aspx) método. Ele deve ser acessado diretamente. Por exemplo, você pode usar o hello [ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx) blobs de saudação do método tooaccess em Olá `$logs` contêiner.
> Como as solicitações são registradas, a análise de armazenamento carrega resultados intermediários como blocos. Periodicamente, a análise de armazenamento confirmará esses blocos e os disponibilizará como um blob.
> 
> 

Podem existir registros duplicados para os logs criados em Olá mesma hora. Você pode determinar se um registro é uma duplicata verificando Olá **RequestId** e **operação** número.

### <a name="log-naming-conventions"></a>Convenções de nomenclatura de log
Cada log será gravado no hello formato a seguir.

    <service-name>/YYYY/MM/DD/hhmm/<counter>.log

Olá tabela a seguir descreve cada atributo no nome do log de saudação.

| Atributo | Descrição |
| --- | --- |
| <service-name> |nome de Olá Olá do serviço de armazenamento. Por exemplo: blob, tabela ou fila. |
| AAAA |ano de quatro dígitos Olá para log hello. Por exemplo: 2011. |
| MM |mês de dois dígitos Olá para log hello. Por exemplo: 07. |
| DD |mês de dois dígitos Olá para log hello. Por exemplo: 07. |
| hh |hora de dois dígitos de saudação que indica Olá iniciando hora para Olá logs no formato UTC de 24 horas. Por exemplo: 18. |
| MM |Olá dois dígitos que indica a saudação inicial minuto para logs de saudação. Esse valor não tem suporte na versão atual de saudação do Storage Analytics, e seu valor será sempre 00. |
| <counter> |Um contador com base em zero com seis dígitos que indica o número de saudação de blobs de log gerada para o serviço de armazenamento de saudação em um período de uma hora. Esse contador começa em 000000. Por exemplo: 000001. |

a seguir Olá é um nome de log de exemplo completo que combina os exemplos anteriores hello.

    blob/2011/07/31/1800/000001.log

seguir Olá é um exemplo de URI que pode ser o log anterior de saudação tooaccess usado.

    https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log

Quando uma solicitação de armazenamento estiver conectada, o nome do log resultante Olá correlaciona hora toohello quando Olá solicitada a operação foi concluída. Por exemplo, se uma solicitação GetBlob foi concluída às 18:30, em 31/7/2011, Olá log será gravado com hello após o prefixo:`blob/2011/07/31/1800/`

### <a name="log-metadata"></a>Metadados de log
Todos os blobs de log são armazenados com metadados que podem ser usado tooidentify contém o blob de Olá de dados do log. Olá, a tabela a seguir descreve cada atributo de metadados.

| Atributo | Descrição |
| --- | --- |
| LogType |Descreve se o log de saudação contém informações referentes a tooread, gravação ou operações de exclusão. Esse valor pode incluir um tipo ou uma combinação dos três, separados por vírgulas. Exemplo 1: gravar. Exemplo 2: ler, gravar. Exemplo 3: ler, gravar e excluir. |
| StartTime |Olá hora antes de uma entrada no log de hello, na forma de saudação de aaaa-MM-ddTHH. Por exemplo: 2011-07-31T18:21:46Z. |
| EndTime |Olá hora mais recente de uma entrada no log de hello, na forma de saudação de aaaa-MM-ddTHH. Por exemplo: 2011-07-31T18:22:09Z. |
| LogVersion |versão de saudação do formato de log hello. Atualmente, o valor de saudação só tem suportada é 1.0. |

Olá, lista a seguir exibe exemplos de metadados usando os exemplos anteriores hello.

* LogType=write
* StartTime=2011-07-31T18:21:46Z
* EndTime=2011-07-31T18:22:09Z
* LogVersion=1.0

### <a name="accessing-logging-data"></a>Acessando dados de log
Todos os dados em Olá `$logs` contêiner pode ser acessado por meio de APIs do serviço Blob hello, incluindo Olá APIs do .NET fornecidas pela hello Azure biblioteca gerenciada. administrador de conta de armazenamento Olá pode ler e excluir logs, mas não é possível criar ou atualizá-los. Metadados de saudação do log e nome de log podem ser usados ao consultar um log. É possível tooappear de logs de uma determinada hora fora de ordem, mas Olá metadados sempre especificam Olá timespan de entradas de log em um log. Portanto, você pode usar uma combinação de nomes de log e metadados ao procurar um log específico.

## <a name="about-storage-analytics-metrics"></a>Sobre as métricas de Análise de Armazenamento
Análise de armazenamento pode armazenar métricas que incluem dados de estatísticas e a capacidade de transações agregadas sobre o serviço de armazenamento de tooa solicitações. As transações são relatadas no nível de operação ambos Olá API, bem como no nível de serviço de armazenamento hello e capacidade é relatada no nível de serviço de armazenamento de saudação. Dados de métrica pode ser usado tooanalyze uso do serviço de armazenamento, diagnosticar problemas com solicitações feitas no serviço de armazenamento hello e desempenho de saudação tooimprove dos aplicativos que usam um serviço.

toouse análise de armazenamento, você deve habilitá-lo individualmente para cada serviço, você deseja toomonitor. Você pode habilitá-lo da saudação [Portal do Azure](https://portal.azure.com). Para obter detalhes, consulte [monitorar uma conta de armazenamento hello Azure Portal](storage-monitor-storage-account.md). Você também pode habilitar a análise de armazenamento programaticamente por meio de saudação API REST ou biblioteca de saudação do cliente. Saudação de uso **obter propriedades do serviço** operações tooenable análise de armazenamento para cada serviço.

### <a name="transaction-metrics"></a>Métricas de transação
Um conjunto robusto de dados é registrado em intervalos de horas ou minutos para cada serviço de armazenamento e operações de API solicitadas, incluindo ingresso/egresso, disponibilidade, erros e percentuais da solicitação categorizados. Você pode ver uma lista completa dos detalhes de transação Olá Olá [esquema de tabela de métricas de análise de armazenamento](https://msdn.microsoft.com/library/hh343264.aspx) tópico.

Dados de transação são registrados em dois níveis: nível de serviço hello e nível de operação da API hello. No nível de serviço Olá, as estatísticas que resumem todas solicitado operações de API são gravadas tooa tabela entidade cada hora, mesmo se nenhuma solicitação seja feita toohello serviço. No nível de operação Olá API, estatísticas são entidade tooan escrito somente se a operação de saudação foi solicitada nessa hora.

Por exemplo, se você executar uma **GetBlob** operação no serviço Blob, métricas do Storage Analytics registrará solicitação hello e incluí-lo em dados agregado de saudação para ambos Olá serviço Blob, bem como Olá **GetBlob** operação. No entanto, se nenhum **GetBlob** for solicitada durante horas hello, uma entidade não será gravada toohello `$MetricsTransactionsBlob` para essa operação.

As métricas de transações são registradas para solicitações de usuários e solicitações feitas pela própria análise de armazenamento. Por exemplo, solicitações de análise de armazenamento toowrite logs e entidades de tabela são registradas. Para saber mais sobre como essas solicitações são cobradas, consulte [Análise de armazenamento e cobrança](https://msdn.microsoft.com/library/hh360997.aspx).

### <a name="capacity-metrics"></a>Métricas de capacidade
> [!NOTE]
> Atualmente, as métricas de capacidade só estão disponíveis para Olá serviço Blob. Métricas de capacidade para o serviço de tabela de saudação e serviço de fila estarão disponíveis em versões futuras do Storage Analytics.
> 
> 

Os dados de capacidade são gravados diariamente para o serviço Blob de uma conta de armazenamento e duas entidades de tabela são gravadas. Uma entidade fornece estatísticas para dados de usuário e outros Olá fornece estatísticas sobre Olá `$logs` contêiner de blob usado pela análise de armazenamento. Olá `$MetricsCapacityBlob` tabela inclui Olá estatísticas a seguir:

* **Capacidade**: quantidade de saudação de armazenamento usada pelo serviço de Blob da conta de armazenamento hello, em bytes.
* **ContainerCount**: Olá número de contêineres de blob no serviço Blob da conta de armazenamento hello.
* **ObjectCount**: Olá número de blobs de blocos ou páginas confirmados e não confirmados no serviço Blob da conta de armazenamento hello.

Para obter mais informações sobre as métricas de capacidade hello, consulte [esquema de tabela de métricas de análise de armazenamento](https://msdn.microsoft.com/library/hh343264.aspx).

### <a name="how-metrics-are-stored"></a>Como as métricas são armazenadas
Todos os dados de métricas para cada um dos serviços de armazenamento de saudação são armazenados em três tabelas reservadas para esse serviço: uma tabela para obter informações de transação, uma tabela para obter informações de transações de minutos e outra tabela para informações de capacidade. Informações de transações de transação de minuto consistem em dados de solicitação e resposta, e informações de capacidade consistem em dados de uso de armazenamento. Métricas de hora, a métrica de minutos e a capacidade para serviço de Blob de uma conta de armazenamento podem ser acessadas nas tabelas que são nomeadas conforme descrito em Olá a tabela a seguir.

| Nível de métricas | Nomes da tabela | Versões com suporte |
| --- | --- | --- |
| Métricas por hora, local principal |$MetricsTransactionsBlob  <br/>$MetricsTransactionsTable <br/> $MetricsTransactionsQueue |Versões anteriores too2013-08-15 somente. Enquanto ainda há suporte para esses nomes, é recomendável que você alterne entre as tabelas de saudação toousing listadas abaixo. |
| Métricas por hora, local principal |$MetricsHourPrimaryTransactionsBlob <br/>$MetricsHourPrimaryTransactionsTable <br/>$MetricsHourPrimaryTransactionsQueue |Todas as versões, incluindo 15-08-2013. |
| Métricas por minuto, local principal |$MetricsMinutePrimaryTransactionsBlob <br/>$MetricsMinutePrimaryTransactionsTable <br/>$MetricsMinutePrimaryTransactionsQueue |Todas as versões, incluindo 15-08-2013. |
| Métricas por hora, local secundário |$MetricsHourSecondaryTransactionsBlob  <br/>$MetricsHourSecondaryTransactionsTable <br/>$MetricsHourSecondaryTransactionsQueue |Todas as versões, incluindo 15-08-2013. A replicação de redundância geográfica com acesso de leitura deve estar habilitada. |
| Métricas por minuto, local secundário |$MetricsMinuteSecondaryTransactionsBlob  <br/>$MetricsMinuteSecondaryTransactionsTable <br/>$MetricsMinuteSecondaryTransactionsQueue |Todas as versões, incluindo 15-08-2013. A replicação de redundância geográfica com acesso de leitura deve estar habilitada. |
| Capacidade (apenas serviço Blob) |$MetricsCapacityBlob |Todas as versões, incluindo 15-08-2013. |

Essas tabelas são criadas automaticamente quando a análise de armazenamento é habilitada para uma conta de armazenamento. Elas são acessadas por meio do namespace Olá Olá da conta de armazenamento, por exemplo:`https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`

### <a name="accessing-metrics-data"></a>Acessando dados de métrica
Todos os dados nas tabelas de métricas de saudação podem ser acessados por meio de APIs do serviço de tabela hello, incluindo Olá APIs do .NET fornecidas pela hello Azure biblioteca gerenciada. administrador de conta de armazenamento Olá pode ler e excluir entidades de tabela, mas não é possível criar ou atualizá-los.

## <a name="billing-for-storage-analytics"></a>Cobrança da análise de armazenamento
Todos os dados de métricas são gravados pelos serviços de saudação de uma conta de armazenamento. Como resultado, cada operação de gravação executada pela análise de armazenamento é faturável. Além disso, a quantidade de saudação do armazenamento usado por dados de métrica também é faturável.

Olá seguintes ações executadas pelo Storage Analytics é faturável:

* Solicitações toocreate blobs para registro em log. 
* Solicitações toocreate de entidades de tabela de métricas.

Se você configurou uma política de retenção de dados, você não é cobrado para excluir transações quando a análise de armazenamento exclui dados antigos de log e métricas. No entanto, excluir as transações de um cliente são faturáveis. Para saber mais sobre as políticas de retenção, consulte [Definindo uma política de retenção de dados de análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343263.aspx).

### <a name="understanding-billable-requests"></a>Noções básicas sobre solicitações faturáveis
Cada solicitação feita o serviço de armazenamento de tooan da conta é faturável ou não faturável. O Storage Analytics registra cada solicitação individual feita tooa serviço, incluindo uma mensagem de status que indica como a solicitação de saudação foi tratada. Da mesma forma, o Storage Analytics armazena métricas para um serviço e o hello operações de API desse serviço, incluindo os percentuais de saudação e a contagem de determinadas mensagens de status. Juntos, esses recursos podem ajudá-lo a analisar suas solicitações faturáveis, fazer melhorias em seu aplicativo e diagnosticar problemas com os serviços de tooyour solicitações. Para saber mais sobre a cobrança, confira [Noções básicas sobre cobrança no armazenamento do Azure – largura de banda, transações e capacidade](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

Ao analisar dados de análise de armazenamento, você pode usar tabelas Olá Olá [operações registradas em log de análise de armazenamento e mensagens de Status](https://msdn.microsoft.com/library/azure/hh343260.aspx) toodetermine tópico quais solicitações são faturáveis. Em seguida, você pode comparar seus logs e métricas dados toohello status mensagens toosee se houve cobrança por uma solicitação específica. Você também pode usar tabelas de saudação na disponibilidade de tooinvestigate tópico anterior Olá para um serviço de armazenamento ou a operação de API individual.

## <a name="next-steps"></a>Próximas etapas
### <a name="setting-up-storage-analytics"></a>Configurando a análise de armazenamento
* [Monitorar uma conta de armazenamento Olá Portal do Azure](storage-monitor-storage-account.md)
* [Habilitar e configurar a análise de armazenamento](https://msdn.microsoft.com/library/hh360996.aspx)

### <a name="storage-analytics-logging"></a>Registro em log da Análise de Armazenamento
* [Sobre o registro em log da análise de armazenamento](https://msdn.microsoft.com/library/hh343262.aspx)
* [Formato de Log de análise de armazenamento](https://msdn.microsoft.com/library/hh343259.aspx)
* [Mensagens de operações e status registradas de análise de armazenamento](https://msdn.microsoft.com/library/hh343260.aspx)

### <a name="storage-analytics-metrics"></a>Métricas da Análise de Armazenamento
* [Sobre as métricas de análise de armazenamento](https://msdn.microsoft.com/library/hh343258.aspx)
* [Esquema da tabela de métricas da análise de armazenamento](https://msdn.microsoft.com/library/hh343264.aspx)
* [Mensagens de operações e status registradas de análise de armazenamento](https://msdn.microsoft.com/library/hh343260.aspx)  

