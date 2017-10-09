---
title: "relatórios de integridade de malha de serviço personalizados aaaAdd | Microsoft Docs"
description: "Descreve como os relatórios de integridade personalizado toosend tooAzure entidades de integridade de malha do serviço. Fornece recomendações para projetar e implementar relatórios de integridade de qualidade."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>Adicionar relatórios de integridade personalizados do Service Fabric
Malha do serviço do Azure apresenta um [modelo de integridade](service-fabric-health-introduction.md) projetado cluster não íntegro tooflag e condições de aplicativo em entidades específicas. usa o modelo de integridade Olá **relatórios de integridade** (componentes do sistema e watchdogs). meta de saudação é fácil e rápido de diagnóstico e reparo. Gravadores de serviço necessário toothink antecipadamente sobre integridade. Qualquer condição que pode afetar a integridade deve ser relatada, especialmente se ele pode ajudar a problemas de sinalizador fechar toohello raiz. informações de integridade Olá podem economizar tempo e esforço na investigação e depuração. Olá utilidade é especialmente clara depois que o serviço hello está em execução em grande escala na nuvem hello (particular ou do Azure).

monitor de recursos do Service Fabric Olá identificado condições de interesse. Eles informam essas condições com base na respectiva exibição local. Olá [repositório de integridade](service-fabric-health-introduction.md#health-store) agrega dados de integridade enviados por toodetermine de Relatores todas as entidades estão íntegros globalmente. modelo de saudação é toouse avançados, flexíveis e fáceis de toobe pretendido. qualidade Olá Olá de relatórios de integridade determina a precisão de saudação do modo de exibição de integridade de saudação do cluster de saudação. Falsos positivos que mostram incorretamente problemas de integridade podem afetar negativamente atualizações ou outros serviços que usam dados de integridade. Exemplos de tais serviços são os serviços de reparo e os mecanismos de alerta. Portanto, alguns pensamento é relatórios tooprovide necessários que capturam as condições de interesse em Olá melhor maneira possível.

toodesign e implementar integridade reporting, watchdogs e componentes do sistema devem:

* Definir condição Olá estão interessados, forma Olá que é monitorado e hello impacto sobre a funcionalidade do cluster ou o aplicativo hello. Com base nessas informações, decida no estado de integridade e a propriedade de relatório de integridade do hello.
* Determinar Olá [entidade](service-fabric-health-introduction.md#health-entities-and-hierarchy) relatório Olá aplica-se a.
* Determinar onde Olá reporting é feita, no hello watchdog de serviço ou de interno ou externo.
* Defina um Relator de saudação tooidentify fonte usada.
* Escolher uma estratégia de relatório: periodicamente ou nas transições. Olá recomendado maneira é periodicamente, como ele requer código mais simples e diminui a probabilidade de tooerrors.
* Determine quanto tempo relatório de saudação para não íntegro condições devem permanecer no repositório de integridade hello e como ela deve ser desmarcada. Usando essas informações, decida o comportamento de toolive e remover na expiração do tempo do relatório hello.

Conforme mencionado, o relatório pode ser gerado:

* Olá monitorado réplicas do serviço do Service Fabric.
* De watchdogs internos implantados como um serviço do Service Fabric (por exemplo, um serviço sem estado do Service Fabric que monitora as condições e emite relatórios). watchdogs Olá podem ser implantado um todos os nós ou pode ser serviço de afinidade toohello monitorado.
* Watchdogs internos que executar em nós do Service Fabric hello, mas são *não* implementado como serviços do Service Fabric.
* Externa watchdogs esse recurso de saudação de investigação de *fora* cluster do Service Fabric de saudação (por exemplo, serviço de monitoramento como Gomez).

> [!NOTE]
> Sem necessidade de saudação cluster Olá é populada com relatórios de integridade enviados pelos componentes do sistema hello. Leia mais em [Usando relatórios de integridade do sistema para solução de problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md). Olá relatórios do usuário devem ser enviados [entidades de integridade](service-fabric-health-introduction.md#health-entities-and-hierarchy) que já foram criados pelo sistema hello.
> 
> 

Uma vez hello design de relatório de integridade é claro, relatórios de integridade podem ser enviados facilmente. Você pode usar [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) tooreport integridade se Olá cluster não está [segura](service-fabric-cluster-security.md) ou se o cliente de malha Olá tem privilégios de administrador. Emissão de relatórios pode ser feito por meio Olá API por usando [FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth), por meio do PowerShell ou por meio do REST. Botões de configuração que dividem os relatórios em lotes para melhor desempenho.

> [!NOTE]
> Relatório de integridade é síncrona e representa apenas Olá trabalho de validação no lado do cliente de saudação. Olá fato Olá relatório é aceito pelo cliente de integridade de saudação ou hello `Partition` ou `CodePackageActivationContext` objetos não significa que ela é aplicada no repositório de saudação. Ele será enviado de forma assíncrona e, possivelmente, em lote com outros relatórios. saudação de processamento no servidor de saudação ainda pode falhar: número de sequência de saudação poderia estar obsoleto, entidade Olá no qual Olá relatório deve ser aplicado foi excluído, etc.
> 
> 

## <a name="health-client"></a>Cliente de integridade
Olá relatórios de integridade são enviados toohello repositório de integridade através de um cliente de integridade, que reside dentro de cliente de malha hello. cliente de integridade Olá pode ser configurado com hello configurações a seguir:

* **HealthReportSendInterval**: atraso Olá entre o relatório de saudação do tempo de saudação é adicionado toohello cliente e tempo de saudação toohello repositório de integridade é enviado. Relatórios de toobatch usado em uma única mensagem, em vez de enviar uma mensagem para cada relatório. Olá envio em lote melhora o desempenho. Padrão: 30 segundos.
* **HealthReportRetrySendInterval**: intervalo de saudação em qual Olá cliente integridade reenvia a integridade acumulada relatórios toohello repositório de integridade. Padrão: 30 segundos.
* **HealthOperationTimeout**: período de tempo limite de saudação para uma mensagem de relatório enviada toohello repositório de integridade. Se uma mensagem de tempo limite, Olá integridade cliente tentará novamente a ele até que o repositório de integridade Olá confirma que o relatório de saudação foi processado. Padrão: dois minutos.

> [!NOTE]
> Quando Olá relatórios são em lote, cliente de malha de saudação deve ser mantida ativa pelo menos Olá tooensure HealthReportSendInterval que eles são enviados. Se a mensagem de saudação é perdida ou repositório de integridade de saudação não é possível aplicar devido a erros de tootransient, cliente de malha Olá deve ser mantido toogive mais atividade-tooretry uma possibilidade.
> 
> 

saudação de buffer no cliente de saudação leva exclusividade Olá Olá relatórios em consideração. Por exemplo, se um determinado Relator incorreto estiver se comunicando 100 relatórios por segundo em Olá mesmo propriedade Olá Olá relatórios são substituídos com a última versão de saudação de mesma entidade. No máximo um tal relatório existe na fila de cliente hello. Se o envio em lote estiver configurado, o número de saudação de relatórios enviados toohello repositório de integridade é apenas uma por intervalo de envio. Esse relatório é Olá último adicionado, que refletem o estado mais atual do hello da entidade de saudação.
Especificar parâmetros de configuração quando `FabricClient` é criado, passando [FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) com hello desejado valores para entradas de integridade.

Olá exemplo a seguir cria um cliente de malha e especifica que os relatórios de saudação devem ser enviados quando eles são adicionados. Em tempos limite e erros que podem ser recuperados, as repetições ocorrem a cada 40 segundos.

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

É recomendável manter a malha de padrão de saudação configurações do cliente, definir `HealthReportSendInterval` too30 segundos. Essa configuração garante que o desempenho ideal devido toobatching. Para relatórios importantes que devem ser enviados o quanto antes, use `HealthReportSendOptions` com `true` imediato na API do [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth). Relatórios imediatos ignoram Olá intervalo de processamento em lotes. Use este sinalizador com cuidado. queremos tootake vantagem do cliente de integridade Olá envio em lote sempre que possível. Envio imediato também é útil quando está fechando o cliente de malha hello (por exemplo, o processo de saudação determinou estado inválido e precisa tooshut para baixo tooprevent efeito colateral). Isso garante que um envio de melhor esforço de relatórios Olá acumulado. Quando um relatório é adicionado com o sinalizador de imediato, o cliente da integridade de saudação lotes todos os relatórios de saudação acumulado desde o último envio.

Os mesmos parâmetros podem ser especificados quando um cluster de tooa de conexão é criado por meio do PowerShell. saudação de exemplo a seguir inicia um cluster local do tooa de conexão:

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

Da mesma forma tooAPI, relatórios podem ser enviados usando `-Immediate` alternar toobe enviada imediatamente, independentemente de saudação `HealthReportSendInterval` valor.

Para REST, Olá relatórios são enviados gateway do Service Fabric toohello, que tem um cliente de malha interna. Por padrão, esse cliente estiver configurado toosend relatórios em lote a cada 30 segundos. Você pode alterar o intervalo de lote de saudação com configuração de cluster Olá `HttpGatewayHealthReportSendInterval` em `HttpGateway`. Conforme mencionado, a melhor opção é toosend Olá relatórios com `Immediate` true. 

> [!NOTE]
> tooensure não autorizados de serviços não pode relatar a integridade em relação a entidades de saudação em cluster hello, configurar tooaccept solicitações Olá somente de clientes protegidos. Olá `FabricClient` usado para o relatório deve ter segurança habilitada toocommunicate capaz de toobe com cluster hello (por exemplo, com a autenticação Kerberos ou certificado). Leia mais sobre [segurança de cluster](service-fabric-cluster-security.md).
> 
> 

## <a name="report-from-within-low-privilege-services"></a>Relatório nos serviços de baixo privilégio
Se os serviços do Service Fabric não tiver um cluster de toohello de acesso de administrador, você poderá relatar integridade de entidades de contexto atual por meio de saudação `Partition` ou `CodePackageActivationContext`.

* Para serviços sem monitoração de estado, use [IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport na instância de serviço atual hello.
* Para serviços com monitoração de estado, use [IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport na réplica atual.
* Use [IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport na entidade de partição atual hello.
* Use [CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport no aplicativo atual.
* Use [CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport no aplicativo atual de saudação implantado no nó atual hello.
* Use [CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport em um pacote de serviço para o aplicativo hello implantado no nó atual hello.

> [!NOTE]
> Internamente, Olá `Partition` e hello `CodePackageActivationContext` mantenha um cliente de integridade configurado com as configurações padrão. Conforme explicado para Olá [cliente integridade](service-fabric-report-health.md#health-client), relatórios são reunidos e enviados em um timer. Olá objetos devem ser mantidos toohave ativa um relatório de saudação toosend chance.
> 
> 

Você pode especificar `HealthReportSendOptions` durante o envio de relatórios por meio de APIs de integridade de`Partition` e `CodePackageActivationContext`. Se você tiver relatórios importantes que devem ser enviados assim que possível, use `HealthReportSendOptions` com `true` imediato. Relatórios imediatos ignoram Olá intervalo do cliente do hello interna de integridade de envio em lote. Como mencionado anteriormente, use este sinalizador com cuidado. queremos tootake vantagem do cliente de integridade Olá envio em lote sempre que possível.

## <a name="design-health-reporting"></a>Projetar relatórios de integridade
Olá primeira etapa na geração de relatórios de alta qualidade é identificar condições de saudação que podem afetar a integridade de saudação do serviço de saudação. Qualquer condição que pode ajudar a problemas de sinalizador em cluster ou serviço hello quando ele for – ou melhor ainda, antes de um problema ocorre, poderá salvar bilhões de dólares. benefícios de saudação incluem menor tempo de inatividade, menos horas noite gastaram analisar e reparar problemas e maior satisfação do cliente.

Depois de condições de saudação são identificadas, gravadores de watchdog necessário toofigure out Olá melhor maneira toomonitor-los para o equilíbrio entre sobrecarga e utilidade. Por exemplo, pense em um serviço que faça cálculos complexos usando alguns arquivos temporários em um compartilhamento. Um watchdog pode monitorar Olá compartilhamento tooensure que espaço suficiente está disponível. Ele pode escutar notificações de alterações em arquivo ou diretório. Ele poderia relatar um aviso se um limite inicial for alcançado e relatará um erro se o compartilhamento de saudação está cheio. Em um aviso, um sistema de reparo foi possível iniciar a limpeza dos arquivos mais antigos no compartilhamento de saudação. Em um erro, um sistema de reparo podia se mover tooanother nó da réplica de serviço hello. Observe como os estados de condição Olá estão descritos em termos de integridade: Olá estado de saudação condição que pode ser considerada íntegra (okey) ou não íntegro (aviso ou erro).

Depois de definir os detalhes de monitoramento de saudação, um gravador de watchdog precisa toofigure out como tooimplement Olá watchdog. Se condições Olá podem ser determinadas no serviço hello, watchdog Olá pode ser parte do próprio serviço Olá monitorado. Por exemplo, código de serviço de Olá pode verificar o uso de compartilhamento de saudação e relatar toda vez que ele tenta toowrite um arquivo. Olá vantagem dessa abordagem é reporting simple. Tome cuidado tooprevent bugs de watchdog de afetar a funcionalidade do serviço hello.

Emissão de relatórios do serviço Olá monitorado nem sempre é uma opção. Um watchdog no serviço de saudação não pode ser capaz de toodetect condições de saudação. Ele pode não ter Olá lógica ou dados toomake Olá determinação. sobrecarga de saudação do monitoramento de condições de saudação poderá ser alta. Olá condições também podem não ser tooa específico de serviço, mas em vez disso, afetam as interações entre serviços. Outra opção é toohave watchdogs cluster hello como processos separados. watchdogs Olá monitoram condições hello e relatório, sem afetar os principais serviços Olá de qualquer forma. Por exemplo, esses watchdogs podem ser implementados como serviços sem monitoração de estado no hello mesmo aplicativo, implantado em todos os nós ou Olá mesmos nós como serviço hello.

Às vezes, uma vigia em execução no cluster de saudação não é uma opção. Se condição Olá monitorado for disponibilidade hello ou a funcionalidade do serviço de saudação como os usuários o vejam, é melhor watchdogs de saudação toohave em Olá mesmo local como clientes do usuário Olá. Lá, eles podem testar operações Olá Olá mesmo modo como os usuários chamá-los. Por exemplo, você pode ter um watchdog que reside fora de cluster hello, emite solicitações de serviço toohello e verifica a latência de saudação e a exatidão dos resultados de saudação. (Para um serviço de calculadora, por exemplo, 2+2 retorna 4 em um período de tempo razoável?)

Depois que os detalhes de watchdog Olá forem concluídas, você deve escolher uma ID de origem que identifica com exclusividade. Se vários watchdogs de saudação mesmo tipo são mora em hello cluster, eles devem relatar entidades diferentes ou, se eles relatam Olá mesma entidade, ID de origem diferente do uso ou propriedade. Dessa forma, os relatórios poderão coexistir. propriedade de saudação do relatório de integridade Olá deve capturar condição Olá monitorado. (Para o exemplo hello acima, a propriedade Olá poderia ser **ShareSize**.) Se vários relatórios aplicam toohello mesma condição, hello propriedade deve conter algumas informações dinâmicas que permite toocoexist de relatórios. Por exemplo, se precisarem de vários compartilhamentos toobe monitorado, pode ser o nome da propriedade Olá **ShareSize sharename**.

> [!NOTE]
> Fazer *não* use informações de status tookeep do repositório de integridade hello. Somente as informações relacionadas à integridade devem ser relatadas como integridade, como esta avaliação de integridade de saudação impactos informações de uma entidade. repositório de integridade de saudação não foi projetado como um repositório de finalidade geral. Ele usa todos os dados tooaggregate de lógica de avaliação de integridade para o estado de integridade de saudação. Envio de informações não relacionada toohealth (como o relatório de status com um estado de integridade de Okey) não afeta a saudação agregado estado de integridade, mas isso pode afetar negativamente o desempenho de saudação do repositório de integridade de saudação.
> 
> 

Olá próximo ponto de decisão seja tooreport qual entidade no. A maioria de tempo de saudação, condição Olá claramente idetifies Olá entidade. Escolha a entidade de saudação com melhor granularidade possíveis. Se uma condição afeta todas as réplicas de uma partição, relate partição hello, não no serviço de saudação. Porém, há situações extremas em que é preciso ter mais cuidado. Se condição Olá afeta uma entidade, como uma réplica, mas Olá desejo é toohave Olá condição sinalizada para mais de duração de saudação da vida útil da réplica, em seguida, ele deve ser relatado na partição de saudação. Caso contrário, quando Olá réplica for excluída, o repositório de integridade Olá limpa todos os seus relatórios. Gravadores de watchdog devem pensar em tempos de vida de saudação de entidade hello e relatório hello. Deve ficar claro quando um relatório deverá ser eliminado de um repositório (por exemplo, quando um erro relatado em uma entidade não for mais aplicável).

Vejamos um exemplo que reúna pontos Olá descrito. Considere um aplicativo do Service Fabric composto por um serviço persistente com estado mestre e serviços sem estado secundários implantados em todos os nós (um tipo de serviço secundário para cada tipo de tarefa). mestre de saudação tem uma fila de processamento que contém comandos toobe executado pelo secundários. secundários Olá executar solicitações de entrada hello e enviar confirmação back sinais. Uma condição que pode ser monitorada é o comprimento de saudação da fila de processamento mestre hello. Se o comprimento de fila mestre Olá atinge um limite, um aviso é relatado. Aviso de saudação indica que secundários Olá não podem lidar com a carga de saudação. Se fila Olá atinge o tamanho máximo de saudação e comandos são descartados, um erro for relatado, como Olá não é possível recuperar o serviço. Olá os relatórios podem ser propriedade de saudação **QueueStatus**. watchdog Olá reside no serviço hello e são enviada periodicamente na réplica primária do mestre hello. tempo de saudação toolive é 2 minutos e é enviado periodicamente a cada 30 segundos. Se Olá primário falhar, relatório de saudação é limpa automaticamente da loja. Se a réplica de serviço Olá estiver ativo, mas ele está bloqueado ou outros problemas, Olá relatório expira no repositório de integridade de saudação. Nesse caso, a entidade de saudação é avaliada em erro.

Outra condição que pode ser monitorada é o tempo de execução da tarefa. Olá, mestre distribui tarefas toohello secundários com base no tipo de tarefa de saudação. Dependendo do design de saudação mestre Olá pode sondar secundários Olá para o status da tarefa. Ele também pode aguardar secundários toosend confirmação back sinais quando eles são feitos. No segundo caso de Olá, tome cuidado toodetect situações em que o chip secundários ou mensagens sejam perdidas. Uma opção é para Olá mestre toosend um toohello de solicitação de ping mesmo secundário, que envia seu status. Se nenhum status for recebida, o mestre de saudação considera uma falha e reagenda tarefas hello. Esse comportamento assume que tarefas de saudação são idempotentes.

condição Olá monitorado pode ser traduzida como um aviso se a tarefa de saudação não é feita em uma determinada hora (**t1**, por exemplo, 10 minutos). Se a tarefa de saudação não foi concluída no tempo (**t2**, por exemplo, 20 minutos), condição Olá monitorado pode ser traduzida como o erro. Esse relatório pode ser gerado de várias maneiras:

* réplica primária do mestre Olá relata periodicamente em si mesmo. Você pode ter uma propriedade para todas as tarefas pendentes na fila de saudação. Se pelo menos uma tarefa leva mais tempo, relatar o status do hello na propriedade Olá **PendingTasks** é um aviso ou erro, conforme apropriado. Se não existem tarefas pendentes ou todas as tarefas iniciou a execução, o status do relatório Olá é Okey. tarefas de saudação são persistentes. Se Olá primário falhar, primário Olá promovido recentemente pode continuar tooreport corretamente.
* Outro processo de watchdog (na nuvem hello ou externa) verifica tarefas hello (de fora, com base no resultado da tarefa Olá desejado) toosee se eles são concluídos. Se eles não respeitam os limites de saudação, um relatório é enviado no serviço mestre hello. Um relatório também é enviado em cada tarefa que inclui o identificador de tarefa hello, como **PendingTask + taskId**. Os relatórios devem ser enviados somente em estados não íntegros. Defina tooa toolive tempo alguns minutos e marcar Olá relatórios toobe removido quando eles expiram tooensure limpeza.
* Olá secundária que está executando uma tarefa informa quando leva mais tempo do que esperado toorun-lo. Informa na instância de serviço Olá na propriedade Olá **PendingTasks**. relatório Olá identifica a instância de serviço de saudação que tem problemas, mas ele não captura situação Olá onde a instância de saudação falhar. Olá relatórios são limpos depois. Ele pode relatar serviço secundário hello. Se Olá secundário tiver concluído a tarefa hello, instância secundária Olá limpa relatório de saudação do repositório de saudação. relatório de saudação não captura situação Olá onde mensagem de confirmação de saudação é perdida e tarefa Olá não ainda terminou de ponto de vista do mestre de saudação.

Mas Olá reporting é feito em casos Olá descritos acima, Olá relatórios são capturados na integridade do aplicativo quando a integridade é avaliada.

## <a name="report-periodically-vs-on-transition"></a>Relatar periodicamente x na transição
Usando o modelo de relatório de integridade de hello, watchdogs podem enviar relatórios periodicamente ou transições. Olá recomendado maneira de watchdog reporting periodicamente, é porque o código de saudação é muito mais simples e menos propenso tooerrors. watchdogs Olá devem buscar toobe tão simple quanto possível tooavoid bugs que disparam relatórios incorretos. Relatórios *não íntegro* incorretos afetam as avaliações de integridade e os cenários com base na integridade, incluindo atualizações. Incorreto *Íntegro* relatórios ocultar problemas no cluster hello, que não é desejado.

Para relatórios periódica, watchdog Olá pode ser implementado com um temporizador. Em um retorno de chamada do timer, watchdog Olá pode verificar o estado de saudação e enviar um relatório com base no estado atual da saudação. Não há nenhum toosee necessidade que o relatório foi enviada anteriormente ou fazer qualquer otimizações em termos de mensagens. cliente de integridade de saudação tem lógica toohelp com o desempenho de processamento em lotes. Enquanto o cliente da integridade de saudação é mantida ativa, ele tenta novamente internamente até relatório Olá é confirmado pelo repositório de integridade de saudação ou watchdog hello gera um relatório mais recente com hello mesma entidade, propriedade e fonte.

Relatórios sobre transições exigem tratamento cuidadoso do estado. watchdog Olá monitora algumas condições e relata somente quando alterar condições hello. Olá cabeça dessa abordagem é que menos relatórios são necessários. desvantagem de Olá é que a lógica de saudação do watchdog Olá é complexa. watchdog Olá deve manter condições hello ou Olá relatórios, para que eles possam ser inspecionados toodetermine alterações de estado. Durante o failover, deve-se ter cuidado com relatórios adicionados, mas ainda não enviadas toohello repositório de integridade. número de sequência de saudação deve ser crescente. Caso contrário, Olá relatórios são rejeitados como obsoleto. Em casos raros Olá onde ocorre a perda de dados, sincronização pode ser necessário entre o estado de saudação do Relator de saudação e estado de saudação do repositório de integridade de saudação.

Relatar transições faz sentido para serviços que relatam a si próprios, por meio de `Partition` ou `CodePackageActivationContext`. Olá quando o objeto local (réplica ou um pacote de serviço implantado / aplicativo implantado) é removido, todos os seus relatórios também serão removidos. A limpeza automática alivia a necessidade de saudação para sincronização entre Relator e repositório de integridade. Se o relatório de saudação é para a partição pai ou o aplicativo pai, deve ter cuidado em failover tooavoid obsoletos relatórios no repositório de integridade de saudação. Lógica deve ser adicionada estado correto do toomaintain hello e relatório Olá clara do armazenamento quando não é necessário mais.

## <a name="implement-health-reporting"></a>Implementar relatório de integridade
Depois de hello a entidade e o relatório de detalhes estão desmarcados, enviar relatórios de integridade pode ser feito por meio da API de hello, PowerShell ou REST.

### <a name="api"></a>API
tooreport por meio de saudação API, você precisa toocreate um tipo de entidade integridade relatório toohello específicas que quiserem tooreport. Dê o cliente de integridade de tooa Olá relatórios. Como alternativa, crie uma informações de integridade e passá-lo toocorrect reporting métodos em `Partition` ou `CodePackageActivationContext` tooreport em entidades atuais.

Olá a exemplo a seguir mostra periódico de relatórios a partir de um watchdog em cluster hello. watchdog Olá verifica se um recurso externo pode ser acessado de dentro de um nó. recurso de saudação é necessária para um manifesto do serviço de aplicativo hello. Se o recurso de saudação não estiver disponível, hello outros serviços no aplicativo hello ainda funcionarão corretamente. Portanto, Olá relatório é enviado na entidade de pacote de serviço Olá implantado a cada 30 segundos.

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
Enviar relatórios de integridade com **Send-ServiceFabric*EntityType*HealthReport**.

Olá a exemplo a seguir mostra periódico de relatórios em valores de CPU em um nó. Olá relatórios devem ser enviados a cada 30 segundos, e que têm um tempo toolive de dois minutos. Se eles expiram, Relator Olá tem problemas, para que o nó de saudação é avaliado em erro. Quando a saudação da CPU estiver acima de um limite, o relatório de saudação tem um estado de integridade de aviso. Quando a saudação da CPU permanece acima de um limite mais de tempo de saudação configurado, ele é relatado como um erro. Caso contrário, Relator Olá envia um estado de integridade de Okey.

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

Olá exemplo a seguir relata um aviso transitório em uma réplica. Ele primeiro obtém a ID de partição hello e hello, em seguida, a ID de réplica para o serviço de saudação em que está interessada. Em seguida, envia um relatório de **PowershellWatcher** na propriedade Olá **ResourceDependency**. relatório de saudação é de interesse para apenas dois minutos e ele será removido do repositório de saudação automaticamente.

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
Envie relatórios de integridade usando REST com solicitações POST que vá entidade toohello desejado e tem na descrição do relatório de integridade do hello corpo hello. Por exemplo, consulte como toosend REST [relatórios de integridade do cluster](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster) ou [relatórios de integridade do serviço](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service). Todas as entidades têm suporte.

## <a name="next-steps"></a>Próximas etapas
Com base nos dados de integridade de saudação, gravadores de serviço e administradores de aplicativo/cluster podem pensar informações de saudação tooconsume maneiras. Por exemplo, eles podem configurar alertas com base em problemas graves de toocatch de status de integridade antes que provocam interrupções. Os administradores também podem definir automaticamente reparar problemas de toofix de sistemas.

[Introdução tooService integridade da malha monitoramento](service-fabric-health-introduction.md)

[Como exibir relatórios de integridade do Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Como tooreport e verificação de integridade do serviço](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Usar relatórios de integridade do sistema para solução de problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Monitorar e diagnosticar serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md)

