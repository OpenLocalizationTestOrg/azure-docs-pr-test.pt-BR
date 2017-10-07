---
title: "aaaConfigure microservices confiável do Azure | Microsoft Docs"
description: Saiba como configurar o Reliable Services com estado no Service Fabric do Azure.
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: vturecek
ms.assetid: 9f72373d-31dd-41e3-8504-6e0320a11f0e
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 1e9c2890b62890a777561f25c04dc0fd11db9f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-stateful-reliable-services"></a>Configurar serviços confiáveis com estado
Há dois conjuntos de definições de configuração para Reliable Services. Um conjunto é global para todos os serviços confiáveis em cluster Olá enquanto outro conjunto hello é um serviço confiável específico tooa específico.

## <a name="global-configuration"></a>Configuração Global
configuração de serviço confiável global Olá é especificada no manifesto do cluster Olá para cluster Olá em Olá KtlLogger seção. Ele permite a configuração de Olá compartilhado log local e tamanho mais Olá global limites de memória usada pelo agente de saudação. manifesto do cluster Olá é um único arquivo XML que contém definições e configurações que se aplicam a nós tooall e serviços em cluster hello. arquivo Hello normalmente é chamado ClusterManifest.xml. Você pode ver manifesto do cluster Olá para o cluster usando o comando do powershell Olá ServiceFabricClusterManifest Get.

### <a name="configuration-names"></a>Nomes da configuração
| Nome | Unidade | Valor padrão | Comentários |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Quilobytes |8388608 |Número mínimo de KB tooallocate no modo de kernel para o agente de log Olá pool de memória do buffer de gravação. Este pool de memória é usado para armazenar em cache informações de estado antes de gravar toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Quilobytes |Sem limite |Pool de memória do tamanho máximo toowhich Olá agente gravação buffer pode crescer. |
| SharedLogId |GUID |"" |Especifica um toouse GUID exclusivo para identificar Olá compartilhado arquivo de log padrão usado por todos os serviços confiáveis em todos os nós no cluster de saudação que não especificam Olá SharedLogId em sua configuração específica do serviço. Se SharedLogId for especificada, SharedLogPath também deverá ser especificada. |
| SharedLogPath |Nome de caminho totalmente qualificado |"" |Especifica o caminho totalmente qualificado do hello onde Olá compartilhada usado por todos os serviços confiáveis em todos os nós no cluster de saudação que não especificam Olá SharedLogPath em sua configuração específica do serviço de arquivo de log. No entanto, se SharedLogPath for especificado, SharedLogId também deverá ser especificado. |
| SharedLogSizeInMB |Megabytes |8192 |Especifica o número de saudação de MB de espaço em disco toostatically alocar para log compartilhado hello. valor de saudação deve ser 2.048 ou maior. |

No Azure ARM ou modelo JSON de local, exemplo hello abaixo mostra como toochange Olá Olá compartilhado log de transações que obtém criados tooback todas as coleções confiáveis para serviços com monitoração de estado.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="sample-local-developer-cluster-manifest-section"></a>Exemplo de seção de manifesto do cluster de desenvolvedor local
Se você quiser toochange isso em seu ambiente de desenvolvimento local, é necessário o arquivo de local clustermanifest.xml de saudação do tooedit.

```xml
   <Section Name="KtlLogger">
     <Parameter Name="SharedLogSizeInMB" Value="4096"/>
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
   </Section>
```

### <a name="remarks"></a>Comentários
Agente de log de saudação tem um pool global de memória alocada da memória do kernel não paginável serviços confiáveis tooall disponível em um nó para o cache de dados de estado antes de serem gravados toohello log dedicado associado com a réplica de um serviço confiável hello. tamanho do pool de saudação é controlado pelo Olá WriteBufferMemoryPoolMinimumInKB e WriteBufferMemoryPoolMaximumInKB configurações. WriteBufferMemoryPoolMinimumInKB especifica ambos Olá tamanho inicial desse pool de memória e pode reduzir Olá menor tamanho toowhich Olá pool de memória. WriteBufferMemoryPoolMaximumInKB é Olá maior tamanho toowhich Olá pool de memória pode atingir. Cada réplica de um serviço confiável que é aberta pode aumentar o tamanho de Olá Olá do pool de memória por um valor de sistema determinado backup tooWriteBufferMemoryPoolMaximumInKB. Se for necessário mais memória do pool de memória Olá que está disponível, solicitações de memória serão adiadas até que a memória está disponível. Portanto, se o pool de memória de buffer de gravação de saudação é muito pequeno para uma configuração específica, em seguida, o desempenho pode sofrer.

Olá SharedLogId e SharedLogPath as configurações são sempre usados toodefine juntos Olá GUID e o local padrão de saudação compartilhado log para todos os nós no cluster de saudação. saudação padrão compartilhado do log é usado para todos os serviços confiáveis que não especificam configurações Olá Olá settings.xml para serviço específico hello. Para melhor desempenho, os arquivos de log compartilhados devem ser colocados em discos que são usados exclusivamente para contenção de tooreduce de arquivo de log Olá compartilhado.

SharedLogSizeInMB Especifica Olá toopreallocate de espaço em disco para log compartilhado do saudação padrão em todos os nós.  SharedLogId e SharedLogPath não é necessário toobe especificado para toobe SharedLogSizeInMB especificado.

## <a name="service-specific-configuration"></a>Configuração específica de serviço
Você pode modificar as configurações padrão de monitoração de estado confiável dos serviços usando o pacote de configuração da saudação (configuração) ou Olá a implementação de serviço (código).

* **Configuração** -configuração por meio do pacote de configuração de saudação é feito alterando o arquivo Settings.xml Olá gerado na raiz do pacote de saudação Microsoft Visual Studio na pasta de configuração Olá para cada serviço de aplicativo hello.
* **Código** -configuração por meio de código é feito criando um ReliableStateManager usando um objeto ReliableStateManagerConfiguration com conjunto de opções apropriadas de saudação.

Por padrão, hello Azure Service Fabric runtime procura nomes de seção predefinida no arquivo Settings.xml de saudação e consome os valores de configuração de saudação ao criar hello subjacente de componentes de tempo de execução.

> [!NOTE]
> Fazer **não** excluir nomes de seção de saudação do hello configurações no arquivo Settings.xml de saudação que é gerado na solução do Visual Studio hello, a menos que você planeje tooconfigure seu serviço por meio de código a seguir.
> Renomear os nomes de pacote ou uma seção de configuração Olá exigirá uma alteração de código ao configurar Olá ReliableStateManager.
> 
> 

### <a name="replicator-security-configuration"></a>Configuração de segurança do replicador
As configurações de segurança do replicador são canal de comunicação do hello toosecure usado é usado durante a replicação. Isso significa que serviços não será capaz de toosee do outro tráfego de replicação, garantindo que dados Olá estará altamente disponíveis também são seguro. Por padrão, uma seção de configuração de segurança vazia evita a segurança de replicação.

### <a name="default-section-name"></a>Nome padrão da seção
ReplicatorSecurityConfig

> [!NOTE]
> toochange o nome da seção, substituição Olá replicatorSecuritySectionName toohello ReliableStateManagerConfiguration construtor de parâmetro ao criar hello ReliableStateManager para esse serviço.
> 
> 

### <a name="replicator-configuration"></a>Configuração do replicador
Configurações de replicador configurar replicador de saudação que é responsável por verificar Olá com monitoração de estado do estado do serviço confiável altamente confiáveis, replicação e persistência de estado de saudação localmente.
configuração padrão de saudação é gerada pelo modelo do Visual Studio hello e deve ser suficiente. Esta seção fala sobre as configurações adicionais que são replicador de saudação tootune disponíveis.

### <a name="default-section-name"></a>Nome padrão da seção
ReplicatorConfig

> [!NOTE]
> toochange o nome da seção, substituição Olá replicatorSettingsSectionName toohello ReliableStateManagerConfiguration construtor de parâmetro ao criar hello ReliableStateManager para esse serviço.
> 
> 

### <a name="configuration-names"></a>Nomes da configuração
| Nome | Unidade | Valor padrão | Comentários |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Segundos |0,015 |Período de tempo para o replicador Olá a esperas de saudação secundário após o recebimento de uma operação antes de enviar de volta um reconhecimento toohello primário. Outros toobe de confirmações enviada para operações processadas dentro deste intervalo são enviadas como uma resposta. |
| ReplicatorEndpoint |N/D |Nenhum parâmetro padrão obrigatório |Endereço IP e porta que Olá replicador primário/secundário usará toocommunicate com outros replicadores no conjunto de réplicas de saudação. Isso deve fazer referência a um ponto de extremidade TCP recurso no manifesto do serviço de saudação. Consulte também[recursos de manifesto do serviço](service-fabric-service-manifest-resources.md) tooread mais sobre como definir recursos de ponto de extremidade em um manifesto de serviço. |
| MaxPrimaryReplicationQueueSize |Número de operações |8192 |Número máximo de operações em fila primária hello. Uma operação é liberada após replicador primário Olá recebe uma confirmação de todos os replicadores secundário de saudação. Esse valor deve ser maior que 64 e uma potência de 2. |
| MaxSecondaryReplicationQueueSize |Número de operações |16384 |Número máximo de operações em fila secundária hello. Uma operação é liberada depois de tornar seu estado de altamente disponível por meio de persistência. Esse valor deve ser maior que 64 e uma potência de 2. |
| CheckpointThresholdInMB |MB |50 |Quantidade de espaço de arquivo de log após o qual estado Olá é marcado. |
| MaxRecordSizeInKB |KB |1024 |Maior tamanho de registro que Olá replicador pode gravar no log de saudação. Esse valor deve ser um múltiplo de 4 e maior que 16. |
| MinLogSizeInMB |MB |0 (sistema de determinado) |Tamanho mínimo do log transacional hello. log de saudação não poderão ser tootruncate tooa tamanho abaixo dessa configuração. 0 indica que replicador Olá determinará o tamanho de log mínimo hello. O aumento desse valor aumenta a possibilidade de saudação de fazer cópias parciais e backups incrementais desde as chances de registros de log relevantes sendo truncado é reduzido. |
| TruncationThresholdFactor |Fator |2 |Determina em qual o tamanho do log de Olá, truncamento será disparado. O limite de truncamento é determinado pelo MinLogSizeInMB multiplicado por TruncationThresholdFactor. TruncationThresholdFactor deve ser maior que 1. MinLogSizeInMB * TruncationThresholdFactor deve ser menor que MaxStreamSizeInMB. |
| ThrottlingThresholdFactor |Fator |4 |Determina no qual o tamanho do log de hello, réplica Olá iniciará sendo limitado. O limite da limitação (em MB) é determinado por Max((MinLogSizeInMB * ThrottlingThresholdFactor),(CheckpointThresholdInMB * ThrottlingThresholdFactor)). O limite da limitação (em MB) deve ser maior que o limite de truncamento (em MB). O limite de truncamento (em MB) deve ser menor que MaxStreamSizeInMB. |
| MaxAccumulatedBackupLogSizeInMB |MB |800 |Tamanho máximo acumulado (em MB) de logs de backup em determinada cadeia de log de backup. Um solicitações de backup incrementais falharão se o backup incremental Olá geraria um log de backup que possam causar logs de backup Olá acumulado desde a saudação relevantes backup completo toobe maior do que esse tamanho. Nesses casos, o usuário é necessária tootake um backup completo. |
| SharedLogId |GUID |"" |Especifica um toouse GUID exclusivo para identificar o arquivo de log compartilhados Olá usada com esta réplica. Normalmente, os serviços não devem usar essa configuração. No entanto, se SharedLogId for especificado, SharedLogPath também deverá ser especificado. |
| SharedLogPath |Nome de caminho totalmente qualificado |"" |Especifica o caminho totalmente qualificado do hello onde o arquivo de log compartilhado Olá para esta réplica será criado. Normalmente, os serviços não devem usar essa configuração. No entanto, se SharedLogPath for especificado, SharedLogId também deverá ser especificado. |
| SlowApiMonitoringDuration |Segundos |300 |Define Olá monitorando o intervalo para chamadas de API gerenciadas. Exemplo: o usuário fez o backup da função de callback. Após o intervalo de saudação será enviado um relatório de integridade de aviso toohello Gerenciador de integridade. |

### <a name="sample-configuration-via-code"></a>Amostra de configuração via código
```csharp
class Program
{
    /// <summary>
    /// This is hello entry point of hello service host process.
    /// </summary>
    static void Main()
    {
        ServiceRuntime.RegisterServiceAsync("HelloWorldStatefulType",
            context => new HelloWorldStateful(context, 
                new ReliableStateManager(context, 
        new ReliableStateManagerConfiguration(
                        new ReliableStateManagerReplicatorSettings()
            {
                RetryInterval = TimeSpan.FromSeconds(3)
                        }
            )))).GetAwaiter().GetResult();
    }
}    
```
```csharp
class MyStatefulService : StatefulService
{
    public MyStatefulService(StatefulServiceContext context, IReliableStateManagerReplica stateManager)
        : base(context, stateManager)
    { }
    ...
}
```


### <a name="sample-configuration-file"></a>Arquivo de exemplo de configuração
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="ReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="ReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="512" />
   </Section>
   <Section Name="ReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```


### <a name="remarks"></a>Comentários
BatchAcknowledgementInterval controla a latência de replicação. Um valor de '0' resulta em Olá menor latência possível, ao custo de saudação de taxa de transferência (conforme mais mensagens de confirmação devem ser enviadas e processadas, cada uma contendo confirmações menos).
Olá maior valor de saudação do BatchAcknowledgementInterval, Olá Olá superior geral produtividade de replicação, ao custo de saudação de maior latência de operação. Isso se traduz diretamente toohello latência de confirmações de transações.

valor Olá por quantidade de saudação CheckpointThresholdInMB controles de espaço em disco que Olá replicador pode usar toostore informações de estado no arquivo de log dedicado da réplica hello. Aumento do valor mais alto tooa de padrão de saudação pode resultar em tempos mais rápidos de reconfiguração quando uma nova réplica é adicionada toohello conjunto. Isso é devido a transferência de estado parcial toohello que ocorre devido a disponibilidade de toohello de histórico mais de operações no log de saudação. Potencialmente, isso pode aumentar o tempo de recuperação de saudação de uma réplica após uma falha.

configuração MaxRecordSizeInKB de saudação define o tamanho máximo de saudação de um registro que pode ser gravado pelo replicador Olá no arquivo de log de saudação. Na maioria dos casos, o tamanho de registro de 1024 KB saudação padrão é ideal. No entanto, se o serviço de saudação está causando a maior parte de toobe itens de dados de informações de estado hello, esse valor talvez seja necessário toobe aumentado. Há pouco benefício fazer MaxRecordSizeInKB menor que 1024, registros menores usam apenas espaço Olá necessário para registro menor hello. Esperamos que esse valor seria necessário toobe alterado apenas raramente.

configurações de SharedLogId e SharedLogPath Olá são sempre toomake usado junto um um log compartilhado separado do log compartilhado do saudação padrão o uso do serviço para o nó de saudação. Para obter uma maior eficiência, como muitos serviços possível devem especificar Olá mesmo compartilhado log. Compartilhado arquivos de log devem ser colocados em discos que são usados exclusivamente para contenção de movimento do cabeçalho tooreduce do arquivo de log Olá compartilhado. Esperamos que esse valor seria necessário toobe alterado apenas raramente.

## <a name="next-steps"></a>Próximas etapas
* [Depurar seu aplicativo do Service Fabric usando o Visual Studio](service-fabric-debugging-your-application.md)
* [Referência do desenvolvedor para Reliable Services](https://msdn.microsoft.com/library/azure/dn706529.aspx)

