---
title: "configurações de cluster do Azure Service Fabric aaaChange | Microsoft Docs"
description: "Este artigo descreve as configurações de malha hello e Olá malha atualização políticas que você pode personalizar."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 7ced36bf-bd3f-474f-a03a-6ebdbc9677e2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: chackdan
ms.openlocfilehash: a8b125f7b4a02547cf4bcf2c936d0c7f1686c1a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-service-fabric-cluster-settings-and-fabric-upgrade-policy"></a>Personalizar as configurações de cluster de Service Fabric e a política de Atualização da Malha
Este documento mostra como toocustomize Olá várias configurações de malha e política de atualização de malha Olá para o cluster do Service Fabric. Você pode personalizá-los no portal de saudação ou usando um modelo do Gerenciador de recursos do Azure.

> [!NOTE]
> Nem todas as configurações podem estar disponíveis por meio do portal de saudação. No caso de uma configuração listada abaixo não está disponível por meio do portal Olá personalizá-lo usando um modelo do Gerenciador de recursos do Azure.
> 

## <a name="customizing-service-fabric-cluster-settings-using-azure-resource-manager-templates"></a>Personalizar configurações de cluster do Service Fabric usando modelos do Azure Resource Manager
Olá as etapas a seguir ilustram como uma nova configuração de tooadd *MaxDiskQuotaInMB* toohello *diagnóstico* seção.

1. Vá toohttps://resources.azure.com
2. Navegue tooyour assinatura expandindo assinaturas -> recursos grupos -> Microsoft.ServiceFabric -> seu nome de Cluster
3. No canto direito superior de hello, selecione "Leitura/gravação"
4. Selecione Editar e atualizar Olá `fabricSettings` elemento JSON e adicionar um novo elemento

```
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

## <a name="fabric-settings-that-you-can-customize"></a>Configurações de malha que você pode personalizar
Aqui estão as configurações de malha de saudação que você pode personalizar:

### <a name="section-name-diagnostics"></a>Nome da seção: diagnósticos
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| ConsumerInstances |Cadeia de caracteres |lista de saudação de instâncias de consumidor DCA. |
| ProducerInstances |Cadeia de caracteres |lista de saudação de instâncias de produtor DCA. |
| AppEtwTraceDeletionAgeInDays |Int, o padrão é 3 |O número de dias após os quais é possível excluir arquivos ETL antigos que contêm rastreamentos ETW do aplicativo. |
| AppDiagnosticStoreAccessRequiresImpersonation |Bool, o padrão é true |Ou não representação é necessária quando acessar diagnóstico armazena em nome do aplicativo hello. |
| MaxDiskQuotaInMB |Int, o padrão é 65536 |Cota de disco em MB para arquivos de log do Windows Fabric. |
| DiskFullSafetySpaceInMB |Int, o padrão é 1024 |Espaço restante em disco em MB tooprotect de uso por DCA. |
| ApplicationLogsFormatVersion |Int, o padrão é 0 |A versão do formato de logs de aplicativo. Os valores com suporte são 0 e 1. Versão 1 inclui mais campos de saudação registro de evento ETW que versão 0. |
| ClusterId |Cadeia de caracteres |id exclusiva de saudação do cluster hello. Isso é gerado quando a saudação cluster é criado. |
| EnableTelemetry |Bool, o padrão é true |Isso vai tooenable ou desabilitar telemetria. |
| EnableCircularTraceSession |Bool, o padrão é false |O sinalizador indica se as sessões de rastreamento circular devem ser usadas. |

### <a name="section-name-traceetw"></a>Nome da seção: rastreamento/Etw
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| Nível |Int, o padrão é 4 |O nível de Rastreamento de Eventos para Windows pode assumir os valores 1, 2, 3 e 4. suportada de toobe deve manter o nível de rastreamento de saudação em 4 |

### <a name="section-name-performancecounterlocalstore"></a>Nome da seção: PerformanceCounterLocalStore
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| IsEnabled |Bool, o padrão é true |O sinalizador indica se a coleta do contador de desempenho no nó local está habilitada. |
| SamplingIntervalInSeconds |Int, o padrão é 60 |Intervalo de amostragem dos contadores de desempenho que estão sendo coletados. |
| Contadores |Cadeia de caracteres |Lista separada por vírgulas de toocollect de contadores de desempenho. |
| MaxCounterBinaryFileSizeInMB |Int, o padrão é 1 |Tamanho máximo (em MB) para cada arquivo binário de contador de desempenho. |
| NewCounterBinaryFileCreationIntervalInMinutes |Int, o padrão é 10 |Intervalo máximo (em segundos) após o qual um novo arquivo binário de contador de desempenho é criado. |

### <a name="section-name-setup"></a>Nome da Seção: instalação
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| FabricDataRoot |string |Diretório raiz de dados do Service Fabric. O padrão para o Azure é d:\svcfab |
| FabricLogRoot |Cadeia de caracteres |Diretório raiz de log do Service Fabric. É nele que logs e os rastreamentos do SF são colocados. |
| ServiceRunAsAccountName |Cadeia de caracteres |nome da conta sob a qual serviço de host de malha toorun Hello. |
| ServiceStartupType |Cadeia de caracteres |tipo de inicialização de saudação do serviço de host de malha hello. |
| SkipFirewallConfiguration |Bool, o padrão é false |Especifica se as configurações do firewall necessário toobe definido pelo sistema de saudação ou não. Isso se aplicará apenas se você estiver usando o Firewall do Windows. Se você estiver usando firewalls de terceiros, em seguida, você deve abrir portas Olá para Olá toouse de sistema e de aplicativos |

### <a name="section-name-transactionalreplicator"></a>Nome da seção: TransactionalReplicator
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| MaxCopyQueueSize |Uint, o padrão é 16384 |Este é o valor máximo de saudação define o tamanho inicial de saudação de fila de saudação que mantém as operações de replicação. Observe que ele deve ser uma potência de 2. Se durante o tempo de execução aumenta fila Olá toothis operações de tamanho serão limitadas entre duplicadores de saudação primários e secundários. |
| BatchAcknowledgementInterval | Tempo em segundos, o padrão é 0,015 | Especifique o intervalo de tempo em segundos. Determina a quantidade de saudação de tempo que Olá esperas replicador após o recebimento de uma operação antes de enviar uma confirmação de volta. Outras operações recebidas durante esse período de tempo terão suas confirmações enviadas de volta em uma única mensagem -> reduzindo o tráfego de rede, mas potencialmente reduzindo taxa de transferência de saudação do replicador hello. |
| MaxReplicationMessageSize |Uint, o padrão é 52428800 | Tamanho máximo da mensagem das operações de replicação. O padrão é 50 MB. |
| ReplicatorAddress |cadeia de caracteres, o padrão é "localhost:0" | ponto de extremidade de saudação na forma de uma cadeia de caracteres-'IP: porta', que é usado por conexões de tooestablish replicador de malha do Windows hello com outras réplicas em operações de recebimento/toosend de ordem. |
| InitialPrimaryReplicationQueueSize |Uint, o padrão é 64 | Esse valor define o tamanho inicial de saudação para fila de saudação que mantém as operações de replicação de saudação em Olá primário. Observe que ele deve ser uma potência de 2.|
| MaxPrimaryReplicationQueueSize |Uint, o padrão é 8192 |Este é o número máximo de saudação de operações que podem existir na fila de replicação primária Olá. Observe que ele deve ser uma potência de 2. |
| MaxPrimaryReplicationQueueMemorySize |Uint, o padrão é 0 |Este é o valor máximo de Olá Olá primário da fila de replicação em bytes. |
| InitialSecondaryReplicationQueueSize |Uint, o padrão é 64 |Esse valor define o tamanho inicial de saudação para fila de saudação que mantém as operações de replicação de saudação em Olá secundário. Observe que ele deve ser uma potência de 2. |
| MaxSecondaryReplicationQueueSize |Uint, o padrão é 16384 |Este é o número máximo de saudação de operações que podem existir na fila de replicação secundária Olá. Observe que ele deve ser uma potência de 2. |
| MaxSecondaryReplicationQueueMemorySize |Uint, o padrão é 0 |Este é o valor máximo de Olá Olá secundária da fila de replicação em bytes. |
| SecondaryClearAcknowledgedOperations |Bool, o padrão é false |Booleano que controla se operações Olá replicador secundário Olá serão limpo depois de serem reconhecidos toohello primária (disco toohello liberado). Configurações que neste tooTRUE pode resultar em Leituras de disco adicional no novo primário de hello, ao mesmo ritmo réplicas após um failover. |
| MaxMetadataSizeInKB |Int, o padrão é 4 |Tamanho máximo de saudação metadados de fluxo de log. |
| MaxRecordSizeInKB |Uint, o padrão é 1024 | Tamanho máximo de um registro de transmissão de log. |
| CheckpointThresholdInMB |Int, o padrão é 50 |Um ponto de verificação será iniciado quando o uso de log Olá excede esse valor. |
| MaxAccumulatedBackupLogSizeInMB |Int, o padrão é 800 |Tamanho máximo acumulado (em MB) de logs de backup em determinada cadeia de log de backup. Um solicitações de backup incrementais falharão se o backup incremental Olá geraria um log de backup que possam causar logs de backup Olá acumulado desde a saudação relevantes backup completo toobe maior do que esse tamanho. Nesses casos, o usuário é necessária tootake um backup completo. |
| MaxWriteQueueDepthInKB |Int, o padrão é 0 | Int máximo a profundidade da fila de gravação esse agente de núcleo Olá pode usar conforme especificado em kilobytes para log Olá associado esta réplica. Esse valor é o número de máximo de saudação de bytes que pode estar pendente durante as atualizações de agente de log de núcleo. Ele pode ser 0 para Olá principal agente de log toocompute um valor apropriado ou um múltiplo de 4. |
| SharedLogId |Cadeia de caracteres |Identificador de log compartilhado. Isso é um guid e deve ser único para cada log compartilhado. |
| SharedLogPath |Cadeia de caracteres |Log compartilhada de toohello de caminho. Se esse valor for vazio de log compartilhados saudação padrão é usado. |
| SlowApiMonitoringDuration |Tempo em segundos, o padrão é de 300 | Especifica a duração para a API antes que o evento de integridade do aviso seja acionado.|
| MinLogSizeInMB |Int, o padrão é 0 |Tamanho mínimo do log transacional hello. log de saudação não poderão ser tootruncate tooa tamanho abaixo dessa configuração. 0 indica que replicador Olá determinará o tamanho mínimo do log de saudação de acordo com as configurações de tooother. O aumento desse valor aumenta a possibilidade de saudação de fazer cópias parciais e backups incrementais desde as chances de registros de log relevantes sendo truncado é reduzido. |

### <a name="section-name-fabricclient"></a>Nome da seção: FabricClient
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| NodeAddresses |cadeia de caracteres, o padrão é "" |Uma coleção de endereços (cadeias de caracteres de conexão) em nós diferentes que podem ser usado toocommunicate com Olá Olá Naming Service. Inicialmente, hello que cliente conecta-se selecionar um dos endereços de saudação aleatoriamente. Se mais de uma cadeia de caracteres de conexão é fornecida e uma conexão falha devido a um erro de tempo limite; ou de comunicação Olá cliente muda próximo endereço de saudação toouse sequencialmente. Consulte a seção de repetição de endereço do serviço de nomenclatura Olá para obter detalhes na semântica de novas tentativas. |
| ConnectionInitializationTimeout |Tempo em segundos, o padrão é 2 |Especifique o intervalo de tempo em segundos. Intervalo de tempo limite de Conexão para cada cliente de tempo tenta tooopen um gateway de toohello de conexão. |
| PartitionLocationCacheLimit |Int, o padrão é 100000 |Número de partições armazenadas em cache para a resolução de serviço (definir too0 para sem limite). |
| ServiceChangePollInterval |Tempo em segundos, o padrão é 120 |Especifique o intervalo de tempo em segundos. intervalo de saudação entre as sondagens consecutivas para o serviço é alterado de saudação cliente toohello gateway para retornos de chamada de notificações de alteração de serviço registrado. |
| KeepAliveIntervalInSeconds |Int, o padrão é 20 |intervalo de saudação em qual Olá FabricClient transporte envia o gateway de toohello mensagens keep-alive. Para 0, keepAlive está desabilitado. Deve ser um valor positivo. |
| HealthOperationTimeout |Tempo em segundos, o padrão é 120 |Especifique o intervalo de tempo em segundos. tempo limite de saudação para uma mensagem de relatório enviada tooHealth Manager. |
| HealthReportSendInterval |Tempo em segundos, o padrão é de 30 |Especifique o intervalo de tempo em segundos. intervalo de saudação em qual componente de relatório envia acumulados integridade informa tooHealth Manager. |
| HealthReportRetrySendInterval |Tempo em segundos, o padrão é de 30 |Especifique o intervalo de tempo em segundos. intervalo de saudação em qual componente reporting reenvia acumulados integridade informa tooHealth Manager. |
| RetryBackoffInterval |Tempo em segundos, o padrão é 3 |Especifique o intervalo de tempo em segundos. Olá intervalo de retirada antes de tentar novamente a operação de saudação. |
| MaxFileSenderThreads |Uint, o padrão é 10 |número máximo de saudação de arquivos que são transferidos em paralelo. |

### <a name="section-name-common"></a>Nome da Seção: comum
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| PerfMonitorInterval |Tempo em segundos, o padrão é 1 |Especifique o intervalo de tempo em segundos. Intervalo de monitoramento de desempenho. Valor negativo ou too0 configuração desabilita o monitoramento. |

### <a name="section-name-healthmanager"></a>Nome da seção: HealthManager
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| EnableApplicationTypeHealthEvaluation |Bool, o padrão é false |Política de avaliação de integridade do cluster: habilitar avaliação de integridade de tipo por aplicativo. |

### <a name="section-name-fabricnode"></a>Nome da seção: FabricNode
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| StateTraceInterval |Tempo em segundos, o padrão é de 300 |Especifique o intervalo de tempo em segundos. intervalo de saudação para rastreamento de status de nó em cada nó e se nós no FM/FMM. |

### <a name="section-name-nodedomainids"></a>Nome da seção: NodeDomainIds
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| UpgradeDomainId |cadeia de caracteres, o padrão é "" |Descreve o domínio de atualização Olá que nó pertence. |
| PropertyGroup |NodeFaultDomainIdCollection |Descreve os domínios de falha Olá que nó pertence. domínio de falha de saudação é definido por meio de um URI que descreve o local de saudação do nó de Olá Olá Datacenter.  URIs de domínio de falha são de saudação Formatar fd: / fd/seguido de um segmento de caminho do URI.|

### <a name="section-name-nodeproperties"></a>Nome da seção: NodeProperties
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| PropertyGroup |NodePropertyCollectionMap |Uma coleção de pares chave-valor da cadeia de caracteres para propriedades do nó. |

### <a name="section-name-nodecapacities"></a>Nome da seção: NodeCapacities
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| PropertyGroup |NodeCapacityCollectionMap |Uma coleção de capacidades de nó para diferentes métricas. |

### <a name="section-name-fabricnode"></a>Nome da seção: FabricNode
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| StartApplicationPortRange |Int, o padrão é 0 |Início da saudação portas de aplicativo gerenciado pelo subsistema de hospedagem. Necessário se EndpointFilteringEnabled for true na hospedagem. |
| EndApplicationPortRange |Int, o padrão é 0 |End (não inclusivo) de saudação portas de aplicativo gerenciado pelo subsistema de hospedagem. Necessário se EndpointFilteringEnabled for true na hospedagem. |
| ClusterX509StoreName |cadeia de caracteres, o padrão é "My" |Nome do repositório de certificados X.509 que contém o certificado do cluster para proteger a comunicação dentro do cluster. |
| ClusterX509FindType |cadeia de caracteres, o padrão é "FindByThumbprint" |Indica como toosearch para o certificado de cluster no repositório de saudação especificado pelos valores de suporte ClusterX509StoreName: "FindByThumbprint"; "FindBySubjectName" com "FindBySubjectName"; Quando há várias correspondências; Olá com data de validade mais distante Olá é usado. |
| ClusterX509FindValue |cadeia de caracteres, o padrão é "" |Valor de filtro de pesquisa usado toolocate certificado de cluster. |
| ClusterX509FindValueSecondary |cadeia de caracteres, o padrão é "" |Valor de filtro de pesquisa usado toolocate certificado de cluster. |
| ServerAuthX509StoreName |cadeia de caracteres, o padrão é "My" |Nome do repositório de certificados X.509 que contém o certificado do servidor para o serviço de entrada. |
| ServerAuthX509FindType |cadeia de caracteres, o padrão é "FindByThumbprint" |Indica como toosearch para o certificado de servidor no repositório de saudação especificado pelo valor de suporte ServerAuthX509StoreName: FindByThumbprint; FindBySubjectName. |
| ServerAuthX509FindValue |cadeia de caracteres, o padrão é "" |Valor de filtro de pesquisa usado toolocate certificado do servidor. |
| ServerAuthX509FindValueSecondary |cadeia de caracteres, o padrão é "" |Valor de filtro de pesquisa usado toolocate certificado do servidor. |
| ClientAuthX509StoreName |cadeia de caracteres, o padrão é "My" |Nome do repositório de certificados x. 509 de saudação que contém o certificado para a função de administrador padrão FabricClient. |
| ClientAuthX509FindType |cadeia de caracteres, o padrão é "FindByThumbprint" |Indica como toosearch para o certificado no repositório de saudação especificado pelo valor de suporte ClientAuthX509StoreName: FindByThumbprint; FindBySubjectName. |
| ClientAuthX509FindValue |cadeia de caracteres, o padrão é "" | Valor de filtro de pesquisa usado toolocate certificado para a função de administrador padrão FabricClient. |
| ClientAuthX509FindValueSecondary |cadeia de caracteres, o padrão é "" |Valor de filtro de pesquisa usado toolocate certificado para a função de administrador padrão FabricClient. |
| UserRoleClientX509StoreName |cadeia de caracteres, o padrão é "My" |Nome do repositório de certificados x. 509 de saudação que contém o certificado para a função de usuário padrão FabricClient. |
| UserRoleClientX509FindType |cadeia de caracteres, o padrão é "FindByThumbprint" |Indica como toosearch para o certificado no repositório de saudação especificado pelo valor de suporte UserRoleClientX509StoreName: FindByThumbprint; FindBySubjectName. |
| UserRoleClientX509FindValue |cadeia de caracteres, o padrão é "" |Valor de filtro de pesquisa usado toolocate certificado para a função de usuário padrão FabricClient. |
| UserRoleClientX509FindValueSecondary |cadeia de caracteres, o padrão é "" |Valor de filtro de pesquisa usado toolocate certificado para a função de usuário padrão FabricClient. |

### <a name="section-name-paas"></a>Nome da seção: Paas
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| ClusterId |cadeia de caracteres, o padrão é "" |Repositório de certificados X509 usado pela malha para proteção da configuração. |

### <a name="section-name-fabrichost"></a>Nome da seção: FabricHost
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| StopTimeout |Tempo em segundos, o padrão é de 300 |Especifique o intervalo de tempo em segundos. tempo limite de saudação de ativação do serviço hospedado; a desativação e atualização. |
| StartTimeout |Tempo em segundos, o padrão é de 300 |Especifique o intervalo de tempo em segundos. Tempo limite para inicialização do fabricactivationmanager. |
| ActivationRetryBackoffInterval |Tempo em segundos, o padrão é 5 |Especifique o intervalo de tempo em segundos. Intervalo de retirada em cada falha de ativação; cada ativação contínua falha Olá sistema tenta novamente ativação Olá para backup toohello MaxActivationFailureCount. intervalo de repetição de saudação em cada tentativa é um produto de ativação contínua falha e hello retirada intervalo de ativação. |
| ActivationMaxRetryInterval |Tempo em segundos, o padrão é de 300 |Especifique o intervalo de tempo em segundos. Máx. intervalo de repetição de ativação. Em cada tentativa de saudação falha contínua no intervalo é calculado como Min (ActivationMaxRetryInterval; Contagem de falhas contínuas * ActivationRetryBackoffInterval). |
| ActivationMaxFailureCount |Int, o padrão é 10 |Isso é a contagem máxima de saudação para o qual o sistema tentará novamente a ativação com falha antes de desistir. |
| EnableServiceFabricAutomaticUpdates |Bool, o padrão é false |Isso é a atualização automática do tooenable malha por meio do Windows Update. |
| EnableServiceFabricBaseUpgrade |Bool, o padrão é false |Esta é a atualização base tooenable para o servidor. |
| EnableRestartManagement |Bool, o padrão é false |Isso é tooenable reinicialização do servidor. |


### <a name="section-name-failovermanager"></a>Nome da Seção: FailoverManager
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| UserReplicaRestartWaitDuration |Tempo em segundos, o padrão é 60,0 * 30 |Especifique o intervalo de tempo em segundos. Quando uma réplica persistente abaixar; Malha do Windows aguarda esta duração para Olá réplica toocome backup antes de criar novas réplicas de substituição (que exigem uma cópia do estado de saudação). |
| QuorumLossWaitDuration |Tempo em segundos, o padrão é MaxValue |Especifique o intervalo de tempo em segundos. Isso é para o qual permitimos que toobe uma partição em um estado de perda de quorum de duração máxima do hello. Se a partição Olá ainda está em perda de quorum após esta duração; partição de saudação é recuperada da perda de quorum Olá considerado inativo réplicas como perdida. Observe que isso eventualmente pode resultar em perda de dados. |
| UserStandByReplicaKeepDuration |Tempo em segundos, o padrão é 3600,0 * 24 * 7 |Especifique o intervalo de tempo em segundos. Quando uma réplica persistente voltar de um estado inativo, talvez ela já tenha sido substituída. O temporizador determina quanto tempo Olá FM manterá a réplica em espera Olá antes de descartá-lo. |
| UserMaxStandByReplicaCount |Int, o padrão é 1 |número máximo de padrão de saudação de réplicas StandBy que mantém o sistema de saudação para serviços do usuário. |

### <a name="section-name-namingservice"></a>Nome da seção: NamingService
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, o padrão é 7 |número de saudação da réplica conjuntos para cada partição de armazenamento do serviço de nomeação de hello. Aumentar número de saudação de nível da réplica conjuntos aumenta saudação de confiabilidade para informações Olá Olá armazenamento do serviço de nomenclatura; diminuindo a alteração de Olá Olá informações serão perdida como resultado de falhas de nó; ao custo de uma carga maior no Windows Fabric e Olá tempo que leva tooperform atualizações toohello dados de nomenclatura.|
|MinReplicaSetSize | Int, o padrão é 3 | número mínimo de saudação de réplicas do serviço de nomes necessário toowrite em toocomplete uma atualização. Se houver menos de réplicas que esse ativo no Olá Olá do sistema sistema confiabilidade nega atualizações toohello Naming Service repositório até que as réplicas são restauradas. Esse valor nunca deve ser maior que Olá TargetReplicaSetSize. |
|ReplicaRestartWaitDuration | Tempo em segundos, o padrão é (60,0 * 30)| Especifique o intervalo de tempo em segundos. Quando uma réplica do Serviço de Cadastramento ficar inativa, esse temporizador será iniciado.  Quando ele expirar Olá FM começará a réplicas de saudação tooreplace que estão inativos (ele não ainda considerá-las perdido). |
|QuorumLossWaitDuration | Tempo em segundos, o padrão é MaxValue | Especifique o intervalo de tempo em segundos. Quando um Serviço de Cadastramento entra em perda de quorum, esse temporizador é iniciado.  Quando ele expirar Olá FM considerará Olá para baixo de réplicas como perdida; e tente toorecover quorum. Observe que isso pode resultar em perda de dados. |
|StandByReplicaKeepDuration | Tempo em segundos, o padrão é 3600,0 * 2 | Especifique o intervalo de tempo em segundos. Quando uma réplica do Serviço de Cadastramento volta de um estado inativo, talvez ela já tenha sido substituída.  O temporizador determina quanto tempo Olá FM manterá a réplica em espera Olá antes de descartá-lo. |
|PlacementConstraints | cadeia de caracteres, o padrão é "" | Restrição de posicionamento para Olá Naming Service. |
|ServiceDescriptionCacheLimit | Int, o padrão é 0 | número máximo de saudação de entradas mantidas no cache de descrição de serviço Olá LRU no hello serviço de nomes de repositório (definir too0 para sem limite). |
|RepairInterval | Tempo em segundos, o padrão é 5 | Especifique o intervalo de tempo em segundos. Intervalo no qual Olá nomenclatura reparo inconsistência entre Olá autoridade proprietário e nome será iniciado. |
|MaxNamingServiceHealthReports | Int, o padrão é 10 | número máximo de saudação de operações lentas nomenclatura armazenar relatórios não íntegro do serviço ao mesmo tempo. Se for 0, todas as operações lentas serão enviadas. |
| MaxMessageSize |Int, o padrão é 4*1024*1024 |tamanho máximo da mensagem de saudação para comunicação de nó do cliente durante o uso de nomenclatura. Atenuação do ataque ao DOS, o valor padrão é 4 MB. |
| MaxFileOperationTimeout |Tempo em segundos, o padrão é de 30 |Especifique o intervalo de tempo em segundos. Olá tempo limite máximo permitido para a operação de serviço de repositório de arquivo. As solicitações que especificarem um tempo limite maior serão rejeitadas. |
| MaxOperationTimeout |Tempo em segundos, o padrão é 600 |Especifique o intervalo de tempo em segundos. Olá tempo limite máximo permitido para operações do cliente. As solicitações que especificarem um tempo limite maior serão rejeitadas. |
| MaxClientConnections |Int, o padrão é 1000 |Olá número máximo permitido de conexões de cliente por gateway. |
| ServiceNotificationTimeout |Tempo em segundos, o padrão é de 30 |Especifique o intervalo de tempo em segundos. tempo limite de saudação usado durante a entrega de cliente do serviço de notificações toohello. |
| MaxOutstandingNotificationsPerClient |Int, o padrão é 1000 |número máximo de saudação de notificações pendentes antes de um registro de cliente é fechado forçadamente pelo gateway hello. |
| MaxIndexedEmptyPartitions |Int, o padrão é 1000 |número máximo de saudação de partições vazias permanecerá indexados no cache de notificação Olá para clientes reconectar-se a sincronização. Nenhuma partição vazia acima desse limite será removida do índice de saudação em pesquisa versão ordem crescente. Reconexão de clientes pode ainda sincronizar e receber atualizações perdidas partição vazia; mas o protocolo de sincronização de saudação se torna mais caro. |
| GatewayServiceDescriptionCacheLimit |Int, o padrão é 0 |número máximo de saudação de entradas mantidas no cache de descrição de serviço Olá LRU no hello Gateway de nomenclatura (definir too0 para sem limite). |
| PartitionCount |Int, o padrão é 3 |número de saudação de partições de saudação Naming Service repositório toobe criado. Cada partição possui uma chave de partição única que corresponde a tooits índice; chaves de partição caso [0; PartitionCount) existe. Número de saudação crescentes de aumentos de partições de serviço de cadastramento na escala de Olá Olá Naming Service pode executar a diminuindo o tempo médio de saudação de dados mantidos por qualquer réplica de backup definido; ao custo de maior utilização de recursos (desde PartitionCount * ReplicaSetSize réplicas de serviço devem ser mantidas).|

### <a name="section-name-runas"></a>Nome da seção: RunAs
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| RunAsAccountName |cadeia de caracteres, o padrão é "" |Indica o nome da conta RunAs hello. Isso só é necessário para o tipo de conta "DomainUser" ou "ManagedServiceAccount". Os valores válidos são "domínio\usuário" ou "user@domain". |
|RunAsAccountType|cadeia de caracteres, o padrão é "" |Indica o tipo de conta de RunAs hello. Isso é necessário para qualquer seção RunAs Os valores válidos são "DomainUser/NetworkService/ManagedServiceAccount/LocalSystem".|
|RunAsPassword|cadeia de caracteres, o padrão é "" |Indica a senha da conta RunAs hello. Isso só é necessário para o tipo de conta "DomainUser". |

### <a name="section-name-runasfabric"></a>Nome da seção: RunAs_Fabric
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| RunAsAccountName |cadeia de caracteres, o padrão é "" |Indica o nome da conta RunAs hello. Isso só é necessário para o tipo de conta "DomainUser" ou "ManagedServiceAccount". Os valores válidos são "domínio\usuário" ou "user@domain". |
|RunAsAccountType|cadeia de caracteres, o padrão é "" |Indica o tipo de conta de RunAs hello. Isso é necessário para qualquer seção RunAs Os valores válidos são "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|RunAsPassword|cadeia de caracteres, o padrão é "" |Indica a senha da conta RunAs hello. Isso só é necessário para o tipo de conta "DomainUser". |

### <a name="section-name-runashttpgateway"></a>Nome da seção: RunAs_HttpGateway
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| RunAsAccountName |cadeia de caracteres, o padrão é "" |Indica o nome da conta RunAs hello. Isso só é necessário para o tipo de conta "DomainUser" ou "ManagedServiceAccount". Os valores válidos são "domínio\usuário" ou "user@domain". |
|RunAsAccountType|cadeia de caracteres, o padrão é "" |Indica o tipo de conta de RunAs hello. Isso é necessário para qualquer seção RunAs Os valores válidos são "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|RunAsPassword|cadeia de caracteres, o padrão é "" |Indica a senha da conta RunAs hello. Isso só é necessário para o tipo de conta "DomainUser". |

### <a name="section-name-runasdca"></a>Nome da seção: RunAs_DCA
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| RunAsAccountName |cadeia de caracteres, o padrão é "" |Indica o nome da conta RunAs hello. Isso só é necessário para o tipo de conta "DomainUser" ou "ManagedServiceAccount". Os valores válidos são "domínio\usuário" ou "user@domain". |
|RunAsAccountType|cadeia de caracteres, o padrão é "" |Indica o tipo de conta de RunAs hello. Isso é necessário para qualquer seção RunAs Os valores válidos são "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|RunAsPassword|cadeia de caracteres, o padrão é "" |Indica a senha da conta RunAs hello. Isso só é necessário para o tipo de conta "DomainUser". |

### <a name="section-name-httpgateway"></a>Nome da seção: HttpGateway
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
|IsEnabled|Bool, o padrão é false | Habilita/desabilita Olá httpgateway. Httpgateway é desabilitada por padrão e essa configuração precisa toobe conjunto tooenable-lo. |
|ActiveListeners |Uint, o padrão é 50 | Número de fila do servidor leituras toopost toohello http. Isso controla o número de saudação de solicitações simultâneas que podem ser atendidas pelo Olá HttpGateway. |
|MaxEntityBodySize |Uint, o padrão é 4194304 |  Retorna o tamanho máximo de saudação do corpo de saudação que pode ser esperado de uma solicitação http. O valor padrão é 4 MB. Uma solicitação falhará no httpgateway se ele tiver um corpo de tamanho maior que esse valor. O tamanho mínimo da parte de leitura é 4096 bytes. Portanto, isso tem toobe > = 4096. |
|HttpGatewayHealthReportSendInterval |Tempo em segundos, o padrão é de 30 | Especifique o intervalo de tempo em segundos. intervalo de saudação em qual Olá Http Gateway envia acumulados relatórios de integridade tooHealth Manager. |

### <a name="section-name-ktllogger"></a>Nome da seção: KtlLogger
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
|AutomaticMemoryConfiguration |Int, o padrão é 1 | Sinalizador que indica se as configurações de memória Olá devem ser automática e dinâmica configuradas. Se zero, em seguida, definições de configuração de memória hello são usadas diretamente e não são alterados com base nas condições do sistema. Se uma memória Olá configurações são definidas automaticamente e podem ser alteradas com base nas condições de sistema. |
|WriteBufferMemoryPoolMinimumInKB |Int, o padrão é 8388608 |número de saudação do KB tooinitially alocar para o pool de memória de buffer de gravação de saudação. Use 0 tooindicate nenhum limite padrão deve ser consistente com SharedLogSizeInMB abaixo. |
|WriteBufferMemoryPoolMaximumInKB | Int, o padrão é 0 |número de saudação do KB tooallow Olá gravação toogrow de pool de memória de buffer até. Não use 0 tooindicate nenhum limite. |
|MaximumDestagingWriteOutstandingInKB | Int, o padrão é 0 | número de saudação do KB tooallow Olá compartilhado tooadvance log à frente do log dedicado hello. Não use 0 tooindicate nenhum limite.
|SharedLogPath |cadeia de caracteres, o padrão é "" | Caminho e nome toolocation tooplace compartilhado contêiner de log. Use "" para usar o caminho padrão na raiz de dados de malha. |
|SharedLogId |cadeia de caracteres, o padrão é "" |Guid exclusivo para o contêiner de log compartilhado. Use "" se usar o caminho padrão na raiz de dados de malha. |
|SharedLogSizeInMB |Int, o padrão é 8192 | número de saudação de tooallocate MB no contêiner de log compartilhados hello. |

### <a name="section-name-applicationgatewayhttp"></a>Nome da seção: ApplicationGateway/Http
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
|IsEnabled |Bool, o padrão é false | Habilita/desabilita Olá HttpApplicationGateway. HttpApplicationGateway é desabilitada por padrão e essa configuração precisa toobe conjunto tooenable-lo. |
|NumberOfParallelOperations | Uint, o padrão é 5000 | Número de fila do servidor leituras toopost toohello http. Isso controla o número de saudação de solicitações simultâneas que podem ser atendidas pelo Olá HttpGateway. |
|DefaultHttpRequestTimeout |Tempo em segundos. O padrão é 120 |Especifique o intervalo de tempo em segundos.  Fornece Olá tempo limite da solicitação padrão para solicitações de http Olá sendo processadas no gateway de aplicativo hello http. |
|ResolveServiceBackoffInterval |Tempo em segundos, o padrão é 5 |Especifique o intervalo de tempo em segundos.  Fornece o intervalo padrão de retirada Olá antes de tentar novamente uma operação de serviço de resolução com falha. |
|BodyChunkSize |Uint, o padrão é 16384 |  Fornece Olá tamanho para Olá bloco em bytes usado tooread corpo de saudação. |
|GatewayAuthCredentialType |cadeia de caracteres, o padrão é "None" | Indica o tipo de saudação do toouse de credenciais de segurança em valores válidos do ponto de extremidade de gateway de aplicativo do hello http são "None / X509. |
|GatewayX509CertificateStoreName |cadeia de caracteres, o padrão é "My" | Nome do repositório de certificados X.509 que contém o certificado do gateway de aplicativo http. |
|GatewayX509CertificateFindType |cadeia de caracteres, o padrão é "FindByThumbprint" | Indica como toosearch para o certificado no repositório de saudação especificado pelo valor de suporte GatewayX509CertificateStoreName: FindByThumbprint; FindBySubjectName. |
|GatewayX509CertificateFindValue | cadeia de caracteres, o padrão é "" | Valor de filtro de pesquisa usado o certificado de gateway do aplicativo http toolocate hello. Esse certificado estiver configurado no ponto de extremidade de https hello e também pode ser usado tooverify Olá identidade do aplicativo hello se necessário pelos serviços de saudação. FindValue é pesquisado primeiro; se ele não existir, FindValueSecondary será pesquisado. |
|GatewayX509CertificateFindValueSecondary | cadeia de caracteres, o padrão é "" |Valor de filtro de pesquisa usado o certificado de gateway do aplicativo http toolocate hello. Esse certificado estiver configurado no ponto de extremidade de https hello e também pode ser usado tooverify Olá identidade do aplicativo hello se necessário pelos serviços de saudação. FindValue é pesquisado primeiro; se ele não existir, FindValueSecondary será pesquisado.|

### <a name="section-name-management"></a>Nome da seção: gerenciamento
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| ImageStoreConnectionString |SecureString | Cadeia de caracteres de Conexão toohello raiz para o repositório de imagens. |
| ImageStoreMinimumTransferBPS | Int, o padrão é 1024 |taxa de transferência mínima Olá entre cluster hello e ImageStore. Esse valor é usado toodetermine Olá timeout quando acessar Olá repositório de imagens externo. Altere este valor somente se a latência de saudação entre cluster hello e ImageStore for alta tooallow mais tempo para toodownload de cluster de saudação do hello repositório de imagens externo. |
|AzureStorageMaxWorkerThreads | Int, o padrão é 25 | número máximo de saudação de threads de trabalho em paralelo. |
|AzureStorageMaxConnections | Int, o padrão é 5000 | número máximo de saudação do armazenamento de tooazure de conexões simultâneas. |
|AzureStorageOperationTimeout | Tempo em segundos, o padrão é 6000 | Especifique o intervalo de tempo em segundos. Tempo limite de xstore toocomplete de operação. |
|ImageCachingEnabled | Bool, o padrão é true | Essa configuração permite tooenable ou desabilitar o cache. |
|DisableChecksumValidation | Bool, o padrão é false | Essa configuração permite tooenable ou desabilitar a validação de soma de verificação durante o provisionamento de aplicativo. |
|DisableServerSideCopy | Bool, o padrão é false | Essa configuração habilita ou desabilita a cópia do lado do servidor do pacote de aplicativo no repositório de imagens de saudação durante o provisionamento de aplicativo. |

### <a name="section-name-healthmanagerclusterhealthpolicy"></a>Nome da seção: HealthManager/ClusterHealthPolicy
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| ConsiderWarningAsError |Bool, o padrão é false |Política de avaliação de integridade do cluster: os avisos são tratados como erros. |
| MaxPercentUnhealthyNodes | Int, o padrão é 0 |Política de avaliação de integridade do cluster: a porcentagem máxima de nós problemáticos permitidos para Olá cluster toobe íntegra. |
| MaxPercentUnhealthyApplications | Int, o padrão é 0 |Política de avaliação de integridade do cluster: a porcentagem máxima de aplicativos problemáticos permitidos para Olá cluster toobe íntegra. |
|MaxPercentDeltaUnhealthyNodes | Int, o padrão é 10 |Política de avaliação de integridade de atualização de cluster: a porcentagem máxima de nós problemáticos delta permitidos para Olá cluster toobe íntegra. |
|MaxPercentUpgradeDomainDeltaUnhealthyNodes | Int, o padrão é 15 |Política de avaliação de integridade de atualização de cluster: a porcentagem máxima de delta de nós problemáticos em um domínio de atualização permitido para Olá cluster toobe íntegra.|

### <a name="section-name-faultanalysisservice"></a>Nome da seção: FaultAnalysisService
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, o padrão é 0 |Olá NOT_PLATFORM_UNIX_START TargetReplicaSetSize para FaultAnalysisService. |
| MinReplicaSetSize |Int, o padrão é 0 |Olá MinReplicaSetSize para FaultAnalysisService. |
| ReplicaRestartWaitDuration |Tempo em segundos, o padrão é 60 minutos|Especifique o intervalo de tempo em segundos. Olá ReplicaRestartWaitDuration para FaultAnalysisService. |
| QuorumLossWaitDuration | Tempo em segundos, o padrão é MaxValue |Especifique o intervalo de tempo em segundos. Olá QuorumLossWaitDuration para FaultAnalysisService. |
| StandByReplicaKeepDuration| Tempo em segundos, o padrão é (60*24*7) minutos |Especifique o intervalo de tempo em segundos. Olá StandByReplicaKeepDuration para FaultAnalysisService. |
| PlacementConstraints | cadeia de caracteres, o padrão é ""| Olá PlacementConstraints para FaultAnalysisService. |
| StoredActionCleanupIntervalInSeconds | Int, o padrão é 3600 |Essa é a frequência hello repositório será limpo.  Somente ações em um estado terminal; e a concluída há pelo menos CompletedActionKeepDurationInSeconds será removida. |
| CompletedActionKeepDurationInSeconds | Int, o padrão é 604800 | Isso é aproximadamente quanto tempo tookeep ações em um estado terminal.  Isso também depende StoredActionCleanupIntervalInSeconds; como Olá trabalho toocleanup é feita apenas no intervalo. 604800 é 7 dias. |
| StoredChaosEventCleanupIntervalInSeconds | Int, o padrão é 3600 |Isso é a frequência hello repositório será auditado para limpeza; Se o número de saudação de eventos for mais de 30000; Limpeza de saudação será iniciada. |

### <a name="section-name-filestoreservice"></a>Nome da seção: FileStoreService
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| NamingOperationTimeout |Tempo em segundos, o padrão é de 60 |Especifique o intervalo de tempo em segundos. tempo limite de saudação para executar a operação de nomenclatura. |
| QueryOperationTimeout | Tempo em segundos, o padrão é de 60 |Especifique o intervalo de tempo em segundos. tempo limite de saudação para executar a operação de consulta. |
| MaxCopyOperationThreads | Uint, o padrão é 0 | número máximo de saudação de arquivos paralelos que secundário pode copiar do primário. '0' == número de núcleos. |
| MaxFileOperationThreads | Uint, o padrão é 100 | número máximo de saudação de threads paralelos tooperform FileOperations (copiar/mover) permitido na Olá primário. '0' == número de núcleos. |
| MaxStoreOperations | Uint, o padrão é 4096 |número máximo de saudação de repositório paralela da transação operações permitidas no primário. '0' == número de núcleos. |
| MaxRequestProcessingThreads | Uint, o padrão é 200 |Olá número máximo de threads paralelos permitido tooprocess solicitações em Olá primário. '0' == número de núcleos. |
| MaxSecondaryFileCopyFailureThreshold | Uint, o padrão é 25| número máximo de saudação de repetições de cópia de arquivo em Olá secundário antes de desistir. |
| AnonymousAccessEnabled | Bool, o padrão é true |Habilitar/desabilitar o acesso anônimo toohello que filestoreservice compartilha. |
| PrimaryAccountType | cadeia de caracteres, o padrão é "" |Olá primário AccountType dos Olá tooACL principal Olá FileStoreService compartilha. |
| PrimaryAccountUserName | cadeia de caracteres, o padrão é "" |Olá conta primária nome de usuário da saudação tooACL principal Olá FileStoreService compartilhamentos. |
| PrimaryAccountUserPassword | SecureString, o padrão é vazio |senha de conta primária Olá de Olá tooACL principal Olá FileStoreService compartilha. |
| FileStoreService | PrimaryAccountNTLMPasswordSecret | SecureString, o padrão é vazio | segredo de senha de saudação que usado como semente toogenerated mesma senha ao usar a autenticação NTLM. |
| PrimaryAccountNTLMX509StoreLocation | cadeia de caracteres, o padrão é "LocalMachine"| local do repositório de saudação do certificado Olá X509 usado toogenerate HMAC em Olá PrimaryAccountNTLMPasswordSecret ao usar a autenticação NTLM. |
| PrimaryAccountNTLMX509StoreName | cadeia de caracteres, o padrão é "MY"| nome do repositório de saudação do certificado Olá X509 usado toogenerate HMAC em Olá PrimaryAccountNTLMPasswordSecret ao usar a autenticação NTLM. |
| PrimaryAccountNTLMX509Thumbprint | cadeia de caracteres, o padrão é ""|impressão digital de saudação do certificado Olá X509 usado toogenerate HMAC em Olá PrimaryAccountNTLMPasswordSecret ao usar a autenticação NTLM. |
| SecondaryAccountType | cadeia de caracteres, o padrão é ""| Olá secundário AccountType dos Olá tooACL principal Olá FileStoreService compartilha. |
| SecondaryAccountUserName | cadeia de caracteres, o padrão é ""| Olá conta secundária nome de usuário da saudação tooACL principal Olá FileStoreService compartilhamentos. |
| SecondaryAccountUserPassword | SecureString, o padrão é vazio |senha de conta secundária Olá de Olá tooACL principal Olá FileStoreService compartilha.  |
| SecondaryAccountNTLMPasswordSecret | SecureString, o padrão é vazio | segredo de senha de saudação que usado como semente toogenerated mesma senha ao usar a autenticação NTLM. |
| SecondaryAccountNTLMX509StoreLocation | cadeia de caracteres, o padrão é "LocalMachine" |local do repositório de saudação do certificado Olá X509 usado toogenerate HMAC em Olá SecondaryAccountNTLMPasswordSecret ao usar a autenticação NTLM. |
| SecondaryAccountNTLMX509StoreName | cadeia de caracteres, o padrão é "MY" |nome do repositório de saudação do certificado Olá X509 usado toogenerate HMAC em Olá SecondaryAccountNTLMPasswordSecret ao usar a autenticação NTLM. |
| SecondaryAccountNTLMX509Thumbprint | cadeia de caracteres, o padrão é ""| impressão digital de saudação do certificado Olá X509 usado toogenerate HMAC em Olá SecondaryAccountNTLMPasswordSecret ao usar a autenticação NTLM. |

### <a name="section-name-imagestoreservice"></a>Nome da seção: ImageStoreService
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| Habilitado |Bool, o padrão é false |Olá sinalizador habilitado para ImageStoreService. |
| TargetReplicaSetSize | Int, o padrão é 7 |Olá TargetReplicaSetSize para ImageStoreService. |
| MinReplicaSetSize | Int, o padrão é 3 |Olá MinReplicaSetSize para ImageStoreService. |
| ReplicaRestartWaitDuration | Tempo em segundos, o padrão é 60,0 * 30 | Especifique o intervalo de tempo em segundos. Olá ReplicaRestartWaitDuration para ImageStoreService. |
| QuorumLossWaitDuration | Tempo em segundos, o padrão é MaxValue | Especifique o intervalo de tempo em segundos. Olá QuorumLossWaitDuration para ImageStoreService. |
| StandByReplicaKeepDuration | Tempo em segundos, o padrão é 3600,0 * 2 | Especifique o intervalo de tempo em segundos. Olá StandByReplicaKeepDuration para ImageStoreService. |
| PlacementConstraints | cadeia de caracteres, o padrão é "" | Olá PlacementConstraints para ImageStoreService. |
| ClientUploadTimeout | Tempo em segundos, o padrão é 1800 |Especifique o intervalo de tempo em segundos. Valor de tempo limite de carregamento de nível superior solicitar o serviço de armazenamento tooImage. |
| ClientCopyTimeout | Tempo em segundos, o padrão é 1800 | Especifique o intervalo de tempo em segundos. Valor de tempo limite de cópia de nível superior solicitar o serviço de armazenamento tooImage. |
| ClientDownloadTimeout | Tempo em segundos, o padrão é 1800 | Especifique o intervalo de tempo em segundos. Valor de tempo limite para download de nível superior solicitar o serviço de armazenamento tooImage |
| ClientListTimeout | Tempo em segundos, o padrão é 600 | Especifique o intervalo de tempo em segundos. Valor de tempo limite de nível superior da lista solicitar o serviço de armazenamento tooImage. |
| ClientDefaultTimeout | Tempo em segundos, o padrão é 180 | Especifique o intervalo de tempo em segundos. Valor de tempo limite para todas as solicitações não carregar/não download (por exemplo, existe; excluir) tooImage serviço de armazenamento. |

### <a name="section-name-imagestoreclient"></a>Nome da seção: ImageStoreClient
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| ClientUploadTimeout |Tempo em segundos, o padrão é 1800 | Especifique o intervalo de tempo em segundos. Valor de tempo limite de carregamento de nível superior solicitar o serviço de armazenamento tooImage. |
| ClientCopyTimeout | Tempo em segundos, o padrão é 1800 | Especifique o intervalo de tempo em segundos. Valor de tempo limite de cópia de nível superior solicitar o serviço de armazenamento tooImage. |
|ClientDownloadTimeout | Tempo em segundos, o padrão é 1800 | Especifique o intervalo de tempo em segundos. Valor de tempo limite para download de nível superior solicitar o serviço de armazenamento tooImage. |
|ClientListTimeout | Tempo em segundos, o padrão é 600 |Especifique o intervalo de tempo em segundos. Valor de tempo limite de nível superior da lista solicitar o serviço de armazenamento tooImage. |
|ClientDefaultTimeout | Tempo em segundos, o padrão é 180 | Especifique o intervalo de tempo em segundos. Valor de tempo limite para todas as solicitações não carregar/não download (por exemplo, existe; excluir) tooImage serviço de armazenamento. |

### <a name="section-name-tokenvalidationservice"></a>Nome da seção: TokenValidationService
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| Provedores |cadeia de caracteres, o padrão é "DSTS" |Lista separada por vírgulas de tooenable de provedores de validação de token (provedores válidas são: DSTS; AAD). No momento, somente um provedor pode ser habilitado a qualquer momento. |

### <a name="section-name-upgradeorchestrationservice"></a>Nome da seção: UpgradeOrchestrationService
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, o padrão é 0 |Olá TargetReplicaSetSize para UpgradeOrchestrationService. |
| MinReplicaSetSize |Int, o padrão é 0 | Olá MinReplicaSetSize para UpgradeOrchestrationService.
| ReplicaRestartWaitDuration | Tempo em segundos, o padrão é 60 minutos| Especifique o intervalo de tempo em segundos. Olá ReplicaRestartWaitDuration para UpgradeOrchestrationService. |
| QuorumLossWaitDuration | Tempo em segundos, o padrão é MaxValue | Especifique o intervalo de tempo em segundos. Olá QuorumLossWaitDuration para UpgradeOrchestrationService. |
| StandByReplicaKeepDuration | Tempo em segundos, o padrão é 60*24*7 minutos | Especifique o intervalo de tempo em segundos. Olá StandByReplicaKeepDuration para UpgradeOrchestrationService. |
| PlacementConstraints | cadeia de caracteres, o padrão é "" | Olá PlacementConstraints para UpgradeOrchestrationService. |
| AutoupgradeEnabled | Bool, o padrão é true | Sondagem automática e ação de atualização baseadas em um arquivo de estado de meta. |
| UpgradeApprovalRequired | Bool, o padrão é false | Atualização de código toomake configuração exigir aprovação do administrador antes de continuar. |

### <a name="section-name-upgradeservice"></a>Nome da seção: UpgradeService
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| PlacementConstraints |cadeia de caracteres, o padrão é "" |Olá PlacementConstraints para o serviço de atualização. |
| TargetReplicaSetSize | Int, o padrão é 3 | Olá TargetReplicaSetSize para UpgradeService. |
| MinReplicaSetSize | Int, o padrão é 2 | Olá MinReplicaSetSize para UpgradeService. |
| CoordinatorType | cadeia de caracteres, o padrão é "WUTest"| Olá CoordinatorType para UpgradeService. |
| BaseUrl | cadeia de caracteres, o padrão é "" |BaseUrl para UpgradeService. |
| ClusterId | cadeia de caracteres, o padrão é "" | ClusterId para UpgradeService. |
| X509StoreName | cadeia de caracteres, o padrão é "My"| X509StoreName para UpgradeService. |
| X509StoreLocation | cadeia de caracteres, o padrão é "" | X509StoreLocation para UpgradeService. |
| X509FindType | cadeia de caracteres, o padrão é ""| X509FindType para UpgradeService. |
| X509FindValue | cadeia de caracteres, o padrão é "" | X509FindValue para UpgradeService. |
| X509SecondaryFindValue | cadeia de caracteres, o padrão é "" | X509SecondaryFindValue para UpgradeService. |
| OnlyBaseUpgrade | Bool, o padrão é false | OnlyBaseUpgrade para UpgradeService. |
| TestCabFolder | cadeia de caracteres, o padrão é "" | TestCabFolder para UpgradeService. |

### <a name="section-name-securityclientaccess"></a>Nome da seção: segurança/ClientAccess
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| CreateName |cadeia de caracteres, o padrão é "Admin" |Configuração de segurança para a criação do URI de nomenclatura. |
| DeleteName |cadeia de caracteres, o padrão é "Admin" |Configuração de segurança para a exclusão do URI de nomenclatura. |
| PropertyWriteBatch |cadeia de caracteres, o padrão é "Admin" |Configuração de segurança para operações de gravação da propriedade de Nomenclatura. |
| CreateService |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para a criação do serviço. |
| CreateServiceFromTemplate |cadeia de caracteres, o padrão é "Admin" |Configuração de segurança para a criação do serviço com base no modelo. |
| UpdateService |cadeia de caracteres, o padrão é "Admin" |Configuração de segurança para atualizações de serviço. |
| DeleteService  |cadeia de caracteres, o padrão é "Admin" |Configuração de segurança para a exclusão do serviço. |
| ProvisionApplicationType |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para provisionamento de tipo de aplicativo. |
| CreateApplication |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para a criação de aplicativos. |
| DeleteApplication |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para a exclusão de aplicativos. |
| UpgradeApplication |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para iniciar ou interromper atualizações do aplicativo. |
| RollbackApplicationUpgrade |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para reverter atualizações do aplicativo. |
| UnprovisionApplicationType |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para desprovisionamento de tipo de aplicativo. |
| MoveNextUpgradeDomain |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para retomar as atualizações do aplicativo com um domínio de atualização explícito. |
| ReportUpgradeHealth |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para retomar as atualizações de aplicativo com o progresso de atualização atual hello. |
| ReportHealth |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para relatar integridade. |
| ProvisionFabric |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para MSI e/ou provisionamento de manifesto do cluster. |
| UpgradeFabric |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para iniciar atualizações do cluster. |
| RollbackFabricUpgrade |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para reverter atualizações do cluster. |
| UnprovisionFabric |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para MSI e/ou desprovisionamento de manifesto do cluster. |
| MoveNextFabricUpgradeDomain |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para retomar as atualizações do cluster com um domínio de atualização explícito. |
| ReportFabricUpgradeHealth |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para retomar as atualizações de cluster com o progresso de atualização atual hello. |
| StartInfrastructureTask |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para iniciar tarefas de infraestrutura. |
| FinishInfrastructureTask |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para encerrar tarefas de infraestrutura. |
| ActivateNode |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para ativar um nó. |
| DeactivateNode |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para desativar um nó. |
| DeactivateNodesBatch |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para desativar vários nós. |
| RemoveNodeDeactivations |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para reverter a desativação de vários nós. |
| GetNodeDeactivationStatus |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para verificar o status de desativação. |
| NodeStateRemoved |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para relatar o estado do nó removido. |
| RecoverPartition |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para recuperar uma partição. |
| RecoverPartitions |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para recuperar partições. |
| RecoverServicePartitions |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para recuperar partições de serviço. |
| RecoverSystemPartitions |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para recuperar partições de serviço de sistema. |
| ReportFault |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para falha de relatório. |
| InvokeInfrastructureCommand |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para comandos de gerenciamento de tarefa de infraestrutura. |
| FileContent |cadeia de caracteres, o padrão é "Admin" | Transferência de arquivos do cliente (toocluster externo) do repositório de configurações de segurança para imagem. |
| FileDownload |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para o início do download de arquivo cliente imagem repositório (toocluster externo). |
| InternalList |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para operação da lista de arquivos do cliente do repositório de imagens (interno). |
| Excluir |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para operação de exclusão do repositório de imagens. |
| Carregar |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para operação de upload do repositório de imagens. |
| GetStagingLocation |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para recuperação do local de preparo do cliente do repositório de imagens. |
| GetStoreLocation |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para recuperação do local de repositório do cliente do repositório de imagens. |
| NodeControl |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para iniciar, interromper e reiniciar nós. |
| CodePackageControl |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para reiniciar pacotes de códigos. |
| UnreliableTransportControl |cadeia de caracteres, o padrão é "Admin" | Transporte não confiável para adicionar e remover comportamentos. |
| MoveReplicaControl |cadeia de caracteres, o padrão é "Admin" | Mova a réplica. |
| PredeployPackageToNode |cadeia de caracteres, o padrão é "Admin" | Predeployment api. |
| StartPartitionDataLoss |cadeia de caracteres, o padrão é "Admin" | Induz a perda de dados em uma partição. |
| StartPartitionQuorumLoss |cadeia de caracteres, o padrão é "Admin" | Induz a perda de quorum em uma partição. |
| StartPartitionRestart |cadeia de caracteres, o padrão é "Admin" | Reinicia simultaneamente algumas ou todas as réplicas de saudação de uma partição. |
| CancelTestCommand |cadeia de caracteres, o padrão é "Admin" | Cancelará um TestCommand específico se ele estiver em trânsito. |
| StartChaos |cadeia de caracteres, o padrão é "Admin" | Iniciará o caos se ele não tiver sido iniciado ainda. |
| StopChaos |cadeia de caracteres, o padrão é "Admin" | Interromperá o caos se ele já tiver sido iniciado. |
| StartNodeTransition |cadeia de caracteres, o padrão é "Admin" | Configuração de segurança para iniciar a transição de um nó. |
| StartClusterConfigurationUpgrade |cadeia de caracteres, o padrão é "Admin" | Induz StartClusterConfigurationUpgrade em uma partição. |
| GetUpgradesPendingApproval |cadeia de caracteres, o padrão é "Admin" | Induz GetUpgradesPendingApproval em uma partição. |
| StartApprovedUpgrades |cadeia de caracteres, o padrão é "Admin" | Induz StartApprovedUpgrades em uma partição. |
| Ping |cadeia de caracteres, o padrão é "Admin\|\|User" | Configurações de segurança para pings de clientes. |
| Consultar |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para consultas. |
| NameExists |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para verificações de existência do URI de Nomenclatura. |
| EnumerateSubnames |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para a enumeração do URI de Nomenclatura. |
| EnumerateProperties |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para a enumeração da propriedade de Nomenclatura. |
| PropertyReadBatch |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para operações de leitura da propriedade de Nomenclatura. |
| GetServiceDescription |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para notificações de serviço de sondagem longa e descrições de serviço de leitura. |
| ResolveService |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para a resolução do serviço de reclamação. |
| ResolveNameOwner |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para determinar o proprietário do URI de Nomenclatura. |
| ResolvePartition |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para determinar os serviços de sistema. |
| ServiceNotifications |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para notificações de serviço baseadas em evento. |
| PrefixResolveService |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para resolução de prefixo do serviço de reclamação. |
| GetUpgradeStatus |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para sondar o status de atualização do aplicativo. |
| GetFabricUpgradeStatus |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para sondar o status de atualização do cluster. |
| InvokeInfrastructureQuery |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para consultar tarefas de infraestrutura. |
| Listar |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para operação da lista de arquivos do cliente do repositório de imagens. |
| ResetPartitionLoad |cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para carga de redefinição para um failoverUnit. |
| ToggleVerboseServicePlacementHealthReporting | cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para alternar o ServicePlacement HealthReporting detalhado. |
| GetPartitionDataLossProgress | cadeia de caracteres, o padrão é "Admin\|\|User" | Busca o andamento de saudação para uma chamada de api de perda de dados de invoke. |
| GetPartitionQuorumLossProgress | cadeia de caracteres, o padrão é "Admin\|\|User" | Busca o andamento de saudação para uma chamada de api de perda de quorum invoke. |
| GetPartitionRestartProgress | cadeia de caracteres, o padrão é "Admin\|\|User" | Busca o progresso de saudação para uma chamada de api de partição de reinicialização. |
| GetChaosReport | cadeia de caracteres, o padrão é "Admin\|\|User" | Busca o status de saudação do caos dentro de um intervalo de tempo determinado. |
| GetNodeTransitionProgress | cadeia de caracteres, o padrão é "Admin\|\|User" | Configuração de segurança para obter o andamento em um comando de transição do nó. |
| GetClusterConfigurationUpgradeStatus | cadeia de caracteres, o padrão é "Admin\|\|User" | Induz GetClusterConfigurationUpgradeStatus em uma partição. |
| GetClusterConfiguration | cadeia de caracteres, o padrão é "Admin\|\|User" | Induz GetClusterConfiguration em uma partição. |

### <a name="section-name-reconfigurationagent"></a>Nome da seção: ReconfigurationAgent
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| ApplicationUpgradeMaxReplicaCloseDuration | Tempo em segundos, o padrão é 900 |Especifique o intervalo de tempo em segundos. duração de saudação quais Olá sistema aguardará antes de encerrar os hosts de serviço com réplicas que estão presos em Fechar. |
| ServiceApiHealthDuration | Tempo em segundos, o padrão é 30 minutos | Especifique o intervalo de tempo em segundos. ServiceApiHealthDuration define quanto tempo é esperar um toorun da API de serviço antes de nós relatá-lo não íntegro. |
| ServiceReconfigurationApiHealthDuration | Tempo em segundos, o padrão é de 30 | Especifique o intervalo de tempo em segundos. ServiceReconfigurationApiHealthDuration define quanto tempo Olá antes de um serviço na reconfiguração é relatado como não íntegro. |
| PeriodicApiSlowTraceInterval | Tempo em segundos, o padrão é 5 minutos | Especifique o intervalo de tempo em segundos. PeriodicApiSlowTraceInterval define o intervalo de saudação durante o qual chamadas lentas do API serão redesenhadas pelo monitor de API de saudação. |
| NodeDeactivationMaxReplicaCloseDuration | Tempo em segundos, o padrão é 900 | Especifique o intervalo de tempo em segundos. Olá toowait de tempo máximo antes de encerrar um host de serviço que está bloqueando a desativação do nó. |
| FabricUpgradeMaxReplicaCloseDuration | Tempo em segundos, o padrão é 900 | Especifique o intervalo de tempo em segundos. Olá duração máxima RA aguardará antes de encerrar o host de serviço de réplica que não está sendo fechado. |
| IsDeactivationInfoEnabled | Bool, o padrão é true | Determina se a RA usará as informações de desativação para executar eleição nova primária para essa configuração deve ser definida como tootrue para clusters existentes que estão sendo atualizadas de novos clusters Consulte as notas de versão de hello sobre como tooenable isso. |

### <a name="section-name-placementandloadbalancing"></a>Nome da seção: PlacementAndLoadBalancing
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| TraceCRMReasons |Bool, o padrão é true |Especifica se tootrace motivos para CRM emitido canal de eventos operacionais toohello movimentações. |
| ValidatePlacementConstraint | Bool, o padrão é true | Especifica se ou não Olá PlacementConstraint expressão para um serviço é validado quando ServiceDescription um serviço é atualizado. |
| PlacementConstraintValidationCacheSize | Int, o padrão é 10000 | Limites Olá tamanho da tabela de saudação usados para validação rápida e cache de expressões de restrição de posicionamento. |
|VerboseHealthReportLimit | Int, o padrão é 20 | Define o número de saudação de vezes que uma réplica tem toogo não inserido antes de um aviso de integridade é relatado para ela (se o relatório de integridade detalhada estiver habilitado). |
|ConstraintViolationHealthReportLimit | Int, o padrão é 50 | Define o número de saudação de tempos de restrição violando réplica tem toobe persistentemente unfixed antes de diagnóstico é conduzido e relatórios de integridade são emitidos. |
|DetailedConstraintViolationHealthReportLimit | Int, o padrão é 200 | Define o número de saudação de tempos de restrição violando réplica tem toobe persistentemente unfixed antes de diagnóstico é conduzido e relatórios de integridade detalhadas são emitidos. |
|DetailedVerboseHealthReportLimit | Int, o padrão é 200 | Define o número de saudação de vezes que uma réplica não alocada tem toobe persistente não alocado antes de relatórios são emitidos detalhadas de integridade. |
|ConsecutiveDroppedMovementsHealthReportLimit | Int, o padrão é 20 | Define o número de saudação de vezes consecutivas que movimentações emitido ResourceBalancer são descartadas antes de diagnóstico é conduzido e avisos de integridade são emitidos. Negativo: nenhum aviso emitido sob essa condição. |
|DetailedNodeListLimit | Int, o padrão é 15 | Define o número de saudação de nós por restrição tooinclude antes de truncamento no hello que relatórios de réplica não alocados. |
|DetailedPartitionListLimit | Int, o padrão é 15 | Define o número de saudação de partições por entrada de diagnóstica para um tooinclude restrição antes de truncamento no diagnóstico. |
|DetailedDiagnosticsInfoListLimit | Int, o padrão é 15 | Define o número de saudação de entradas de diagnóstico (com informações detalhadas) por restrição tooinclude antes de truncamento no diagnóstico.|
|PLBRefreshGap | Tempo em segundos, o padrão é 1 | Especifique o intervalo de tempo em segundos. Define a quantidade mínima de saudação de tempo que deve decorrer antes PLB atualiza o estado novamente. |
|MinPlacementInterval | Tempo em segundos, o padrão é 1 | Especifique o intervalo de tempo em segundos. Define a quantidade mínima de saudação de tempo que deve decorrer antes de dois turnos de posicionamento consecutivos. |
|MinConstraintCheckInterval | Tempo em segundos, o padrão é 1 | Especifique o intervalo de tempo em segundos. Define a quantidade mínima de saudação de tempo que deve decorrer antes da restrição consecutivas dois verificar turnos. |
|MinLoadBalancingInterval | Tempo em segundos, o padrão é 5 | Especifique o intervalo de tempo em segundos. Define a quantidade mínima de saudação de tempo que deve decorrer antes de dois turnos balanceamento consecutivos. |
|BalancingDelayAfterNodeDown | Tempo em segundos, o padrão é 120 |Especifique o intervalo de tempo em segundos. Não inicie atividades de balanceamento nesse período depois de um evento de nó inativo. |
|BalancingDelayAfterNewNode | Tempo em segundos, o padrão é 120 |Especifique o intervalo de tempo em segundos. Não inicie atividades de balanceamento nesse período depois de adicionar um novo nó. |
|ConstraintFixPartialDelayAfterNodeDown | Tempo em segundos, o padrão é 120 | Especifique o intervalo de tempo em segundos. Não corrija violações de restrição FaultDomain e UpgradeDomain nesse período depois de um evento de nó inativo. |
|ConstraintFixPartialDelayAfterNewNode | Tempo em segundos, o padrão é 120 | Especifique o intervalo de tempo em segundos. Não corrija as violações de restrições FaultDomain e UpgradeDomain nesse período depois de adicionar um novo nó. |
|GlobalMovementThrottleThreshold | Uint, o padrão é 1000 | Número máximo de movimentações permitidos em Olá fase balanceamento em Olá últimos intervalo indicado pelo GlobalMovementThrottleCountingInterval. |
|GlobalMovementThrottleThresholdForPlacement | Uint, o padrão é 0 | Número máximo de movimentações permitido na fase de posicionamento no hello últimos intervalo indicado pelo GlobalMovementThrottleCountingInterval.0 não indica nenhum limite.|
|GlobalMovementThrottleThresholdForBalancing | Uint, o padrão é 0 | Número máximo de movimentações permitido na fase de balanceamento no hello últimos intervalo indicado pelo GlobalMovementThrottleCountingInterval. 0 indica nenhum limite. |
|GlobalMovementThrottleCountingInterval | Tempo em segundos, o padrão é 600 | Especifique o intervalo de tempo em segundos. Indicar o comprimento de saudação do hello após o intervalo para qual tootrack por movimentos de réplica do domínio (usado junto com GlobalMovementThrottleThreshold). Pode ser definido too0 tooignore global limitação completamente. |
|MovementPerPartitionThrottleThreshold | Uint, o padrão é 50 | Sem balanceamento de relacionadas a movimentação ocorrerá para uma partição se o número de saudação do balanceamento de movimentações relacionadas para réplicas dessa partição atingiu ou excedeu MovementPerFailoverUnitThrottleThreshold em Olá últimos intervalo indicado por MovementPerPartitionThrottleCountingInterval. |
|MovementPerPartitionThrottleCountingInterval | Tempo em segundos, o padrão é 600 | Especifique o intervalo de tempo em segundos. Indicar o comprimento de saudação do hello após o intervalo para qual movimentos de réplica tootrack para cada partição (usado junto com MovementPerPartitionThrottleThreshold). |
|PlacementSearchTimeout | Tempo em segundos, o padrão é 0,5 | Especifique o intervalo de tempo em segundos. Ao posicionar os serviços, pesquise por, no máximo, essa duração antes de retornar um resultado. |
|UseMoveCostReports | Bool, o padrão é false | Instrui o elemento de custo de Olá Olá LB tooignore de saudação pontuação função; número possivelmente grande resultante será movida para melhor posicionamento equilibrado. |
|PreventTransientOvercommit | Bool, o padrão é false | Determina se deve PLB imediatamente contar com recursos serão liberados por move Olá iniciada. Por padrão. PLB pode iniciar movimentação out e mover em Olá superalocar mesmo nó que pode criar transitório. Configuração tootrue esse parâmetro impede que os tipos de overcommits e desfragmentação sob demanda (também conhecido como placementWithMove) será desabilitada. |
|InBuildThrottlingEnabled | Bool, o padrão é false | Determine se a limitação do hello na compilação está habilitado. |
|InBuildThrottlingAssociatedMetric | cadeia de caracteres, o padrão é "" | Olá associados nome de métrica para essa limitação. |
|InBuildThrottlingGlobalMaxValue | Int, o padrão é 0 |número máximo de saudação de réplicas no build permitido globalmente. |
|SwapPrimaryThrottlingEnabled | Bool, o padrão é false| Determine se a limitação de permuta primário hello está habilitado. |
|SwapPrimaryThrottlingAssociatedMetric | cadeia de caracteres, o padrão é ""| Olá associados nome de métrica para essa limitação. |
|SwapPrimaryThrottlingGlobalMaxValue | Int, o padrão é 0 | número máximo de saudação de réplicas de permuta primário permitido globalmente. |
|PlacementConstraintPriority | Int, o padrão é 0 | Determina a prioridade de saudação da restrição de posicionamento: 0: rígido; 1: flexível; negativo: ignorar. |
|PreferredLocationConstraintPriority | Int, o padrão é 2| Determina a prioridade de saudação da restrição de local preferencial: 0: rígido; 1: flexível; 2: otimização; negativo: ignorar |
|CapacityConstraintPriority | Int, o padrão é 0 | Determina a prioridade de saudação da restrição de capacidade: 0: rígido; 1: flexível; negativo: ignorar. |
|AffinityConstraintPriority | Int, o padrão é 0 | Determina a prioridade de saudação da restrição de afinidade: 0: rígido; 1: flexível; negativo: ignorar. |
|FaultDomainConstraintPriority | Int, o padrão é 0 | Determina a prioridade de saudação de restrição de domínio de falha: 0: rígido; 1: flexível; negativo: ignorar. |
|UpgradeDomainConstraintPriority | Int, o padrão é 1| Determina a prioridade de saudação de restrição de domínio de atualização: 0: rígido; 1: flexível; negativo: ignorar. |
|ScaleoutCountConstraintPriority | Int, o padrão é 0 | Determina a prioridade de saudação da restrição da contagem de expansão: 0: rígido; 1: flexível; negativo: ignorar. |
|ApplicationCapacityConstraintPriority | Int, o padrão é 0 | Determina a prioridade de saudação da restrição de capacidade: 0: rígido; 1: flexível; negativo: ignorar. |
|MoveParentToFixAffinityViolation | Bool, o padrão é false | Configuração que determina se as réplicas do pai podem ser movido toofix restrições de afinidade.|
|MoveExistingReplicaForPlacement | Bool, o padrão é true |Configuração que determina se a réplica existente toomove durante o posicionamento. |
|UseSeparateSecondaryLoad | Bool, o padrão é true | Configuração que determina se uma carga secundária diferente será usada. |
|PlaceChildWithoutParent | Bool, o padrão é true | Configuração que determinará se a réplica de serviço filho poderá ser posicionada se nenhuma réplica pai estiver ativa. |
|PartiallyPlaceServices | Bool, o padrão é true | Determina se todas as réplicas de serviço no cluster serão posicionadas em “tudo ou nada” dados os nós adequados limitados para elas.|
|InterruptBalancingForAllFailoverUnitUpdates | Bool, o padrão é false | Determina se qualquer tipo de atualização de unidade de failover deve interromper a execução de balanceamento rápida ou lenta. Com o balanceamento “false” especificado, a execução será interrompida se FailoverUnit: for criado/excluído; tiver réplicas ausentes; o local de réplica primário tiver sido alterado ou a quantidade de réplicas tiver sido alterada. A execução de balanceamento NÃO será interrompida em outros casos – se FailoverUnit: tiver réplicas extras; qualquer outro sinalizador de réplica tiver sido alterado; somente a versão de partição ou qualquer outro caso tiver sido alterado. |

### <a name="section-name-security"></a>Nome da Seção: Segurança
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| ClusterProtectionLevel |None ou EncryptAndSign |None (padrão) para clusters não seguros, EncryptAndSign para clusters seguros. |

### <a name="section-name-hosting"></a>Nome da Seção: Hospedagem
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| ServiceTypeRegistrationTimeout |Tempo em segundos, o padrão é de 300 |Tempo máximo permitido para Olá ServiceType toobe registrado com a malha |
| ServiceTypeDisableFailureThreshold |Número inteiro, o padrão é 1 |Esse é o limite de saudação hello, contagem de falhas após o qual FailoverManager (FM) é notificado toodisable Olá tipo de serviço nesse nó e tente um nó diferente para posicionamento. |
| ActivationRetryBackoffInterval |Tempo em segundos, o padrão é de 5 |Intervalo de retirada em cada falha de ativação; Em cada caso de falha de ativação contínua, tentativas de sistema Olá Olá ativação para o toohello MaxActivationFailureCount. intervalo de repetição de saudação em cada tentativa é um produto de ativação contínua falha e hello retirada intervalo de ativação. |
| ActivationMaxRetryInterval |Tempo em segundos, o padrão é de 300 |Em cada caso de falha de ativação contínua, tentativas de sistema Olá Olá ativação para o tooActivationMaxFailureCount. ActivationMaxRetryInterval especifica o intervalo de tempo de espera antes de tentar novamente após cada falha de ativação |
| ActivationMaxFailureCount |Número inteiro, o padrão é 10 |Número de vezes que o sistema tenta realizar novamente a ativação que falhou antes de desistir |

### <a name="section-name-failovermanager"></a>Nome da Seção: FailoverManager
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| PeriodicLoadPersistInterval |Tempo em segundos, o padrão é de 10 |Isso determina a frequência Olá seleção FM de novos relatórios de carga |

### <a name="section-name-federation"></a>Nome da Seção: Federação
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| LeaseDuration |Tempo em segundos, o padrão é de 30 |Duração de uma concessão entre um nó e seus vizinhos. |
| LeaseDurationAcrossFaultDomain |Tempo em segundos, o padrão é de 30 |Duração de uma concessão entre um nó e seus vizinhos entre domínios de falha. |

### <a name="section-name-clustermanager"></a>Nome da Seção: ClusterManager
| **Parâmetro** | **Valores permitidos** | **Diretrizes ou Descrição resumida** |
| --- | --- | --- |
| UpgradeStatusPollInterval |Tempo em segundos, o padrão é de 60 |frequência de saudação de sondagem para status de atualização do aplicativo. Este valor determina a taxa de saudação da atualização para qualquer chamada GetApplicationUpgradeProgress |
| UpgradeHealthCheckInterval |Tempo em segundos, o padrão é de 60 |frequência de saudação do status de integridade verifica durante as atualizações de um aplicativo monitorado |
| FabricUpgradeStatusPollInterval |Tempo em segundos, o padrão é de 60 |frequência de saudação de sondagem para status de atualização de malha. Este valor determina a taxa de saudação da atualização para qualquer chamada GetFabricUpgradeProgress |
| FabricUpgradeHealthCheckInterval |Tempo em segundos, o padrão é de 60 |frequência de saudação da verificação do status de integridade durante uma atualização do Fabric monitorada |
|InfrastructureTaskProcessingInterval | Tempo em segundos, o padrão é de 10 |Especifique o intervalo de tempo em segundos. intervalo de processamento Olá usado por máquina de estado de processamento de tarefas da infraestrutura de saudação. |
|TargetReplicaSetSize |Int, o padrão é 7 |Olá TargetReplicaSetSize para ClusterManager. |
|MinReplicaSetSize |Int, o padrão é 3 |Olá MinReplicaSetSize para ClusterManager. |
|ReplicaRestartWaitDuration |Tempo em segundos, o padrão é (60,0 * 30)|Especifique o intervalo de tempo em segundos. Olá ReplicaRestartWaitDuration para ClusterManager. |
|QuorumLossWaitDuration |Tempo em segundos, o padrão é MaxValue | Especifique o intervalo de tempo em segundos. Olá QuorumLossWaitDuration para ClusterManager. |
|StandByReplicaKeepDuration | Tempo em segundos, o padrão é (3600,0 * 2)|Especifique o intervalo de tempo em segundos. Olá StandByReplicaKeepDuration para ClusterManager. |
|PlacementConstraints | cadeia de caracteres, o padrão é "" |Olá PlacementConstraints para ClusterManager. |
|SkipRollbackUpdateDefaultService | Bool, o padrão é false |Olá CM ignorará os serviços padrão atualizado reversão durante a reversão de atualização do aplicativo. |
|EnableDefaultServicesUpgrade | Bool, o padrão é false |Habilite a atualização de serviços padrão durante a atualização do aplicativo. Descrições de serviço padrão serão substituídas após a atualização. |
|InfrastructureTaskHealthCheckWaitDuration |Tempo em segundos, o padrão é 0| Especifique o intervalo de tempo em segundos. quantidade de saudação de toowait de tempo antes de iniciar as verificações de integridade depois de uma tarefa de infraestrutura de pós-processamento. |
|InfrastructureTaskHealthCheckStableDuration | Tempo em segundos, o padrão é 0| Especifique o intervalo de tempo em segundos. quantidade de saudação de integridade passado do tempo tooobserve consecutivas verifica antes de pós-processamento de uma tarefa de infraestrutura é concluída com êxito. Observar uma verificação de integridade com falha redefinirá esse temporizador. |
|InfrastructureTaskHealthCheckRetryTimeout | Tempo em segundos, o padrão é de 60 |Especifique o intervalo de tempo em segundos. quantidade de saudação de tempo toospend repetindo verificações de integridade falhou ao pós-processamento de uma tarefa de infraestrutura. Observar uma verificação de integridade aprovada redefinirá esse temporizador. |
|ImageBuilderTimeoutBuffer |Tempo em segundos, o padrão é 3 |Especifique o intervalo de tempo em segundos. quantidade de saudação do tooallow de tempo para o cliente do Image Builder tempo limite específicos erros tooreturn toohello. Se esse buffer é muito pequeno. então o cliente de saudação expira antes que o servidor de saudação e obtém um erro de tempo limite genérico. |
|MinOperationTimeout | Tempo em segundos, o padrão é de 60 |Especifique o intervalo de tempo em segundos. Olá mínimo tempo limite global internamente operações de processamento em ClusterManager. |
|MaxOperationTimeout |Tempo em segundos, o padrão é MaxValue | Especifique o intervalo de tempo em segundos. Olá global tempo limite máximo para operações em ClusterManager de processamento internamente. |
|MaxTimeoutRetryBuffer | Tempo em segundos, o padrão é 600 |Especifique o intervalo de tempo em segundos. Olá tempo limite da operação máximo quando internamente repetindo vencimento tootimeouts é <Original Timeout>  +  <MaxTimeoutRetryBuffer>. Tempo limite adicional é adicionado em incrementos de MinOperationTimeout. |
|MaxCommunicationTimeout |Tempo em segundos, o padrão é 600 |Especifique o intervalo de tempo em segundos. Olá tempo limite máximo para as comunicações internas entre ClusterManager e outros serviços do sistema (ou seja, Serviço de nomes; Gerenciador de failover e etc). Esse tempo limite deve ser menor que MaxOperationTimeout global (como pode haver várias comunicações entre componentes do sistema para cada operação de cliente). |
|MaxDataMigrationTimeout |Tempo em segundos, o padrão é 600 |Especifique o intervalo de tempo em segundos. Olá tempo limite máximo para operações de recuperação de migração de dados após uma atualização do Fabric. |
|MaxOperationRetryDelay |Tempo em segundos, o padrão é 5| Especifique o intervalo de tempo em segundos. atraso máximo de saudação para repetições internas quando falhas são encontradas. |
|ReplicaSetCheckTimeoutRollbackOverride |Tempo em segundos, o padrão é 1200 | Especifique o intervalo de tempo em segundos. Se ReplicaSetCheckTimeout estiver definido como toohello o valor máximo de DWORD; em seguida, ele é substituído com valor de saudação dessa configuração para fins de saudação de reversão. valor de saudação usado para avanço nunca é substituído. |
|ImageBuilderJobQueueThrottle |Int, o padrão é 10 |Restrição de contagem de threads para a fila de trabalho do proxy do Image Builder em solicitações do aplicativo. |

## <a name="next-steps"></a>Próximas etapas
Leia estes artigos para obter mais informações sobre gerenciamento de cluster:

[Adicionar, transferir e remover certificados do cluster do Azure ](service-fabric-cluster-security-update-certs-azure.md) 

