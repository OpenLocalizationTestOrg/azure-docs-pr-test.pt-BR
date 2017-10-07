---
title: "aaaService malha Backup e restauração | Microsoft Docs"
description: "Documentação conceitual de backup e restauração do Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: subramar,jessebenson
ms.assetid: 91ea6ca4-cc2a-4155-9823-dcbd0b996349
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: mcoskun
ms.openlocfilehash: e502b59c84999c3fe825167383f00a5ebd70c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a>Fazer backup e restaurar Reliable Services e Reliable Actors
Malha do serviço do Azure é uma plataforma de alta disponibilidade que replica estado Olá entre vários toomaintain de nós esta alta disponibilidade.  Assim, mesmo se um nó no cluster Olá falha, os serviços de saudação continuam toobe disponível. Embora essa redundância integrados fornecida pela plataforma de saudação pode ser suficiente para alguns, em certos casos é desejável para Olá serviço tooback backup de dados (tooan repositório externo).

> [!NOTE]
> É crítico toobackup e restaurar seus dados (e teste funciona conforme o esperado) para que possa se recuperar de cenários de perda de dados.
> 
> 

Por exemplo, um serviço pode querer tooback backup de dados em ordem tooprotect de saudação os seguintes cenários:

- No evento de saudação do perda permanente de saudação de um cluster do Service Fabric inteiro.
- Perda permanente da maioria das réplicas de saudação de uma partição de serviço
- Erros administrativos no qual estado Olá acidentalmente obtém excluído ou corrompido. Por exemplo, isso pode ocorrer se um administrador com privilégios suficientes erroneamente exclui o serviço de saudação.
- Erros no serviço Olá corromper os dados. Por exemplo, isso pode acontecer quando uma atualização do serviço de código começa a gravar dados defeituoso tooa coleção confiável. Nesse caso, ambos Olá código e dados de saudação podem ter toobe revertido tooan estado anterior.
- Processamento de dados offline. Talvez seja conveniente toohave o processamento offline de dados de business intelligence que acontece separadamente do serviço de saudação que gera dados saudação.

o recurso de Backup/restauração Olá permite que os serviços criados na Olá confiável API de serviços toocreate e restaurar backups. Olá APIs de backup fornecidas pela plataforma Olá permitem que um ou mais backups de estado de uma partição de serviço, sem bloqueio de leitura ou de operações de gravação. APIs de restauração Olá permitir toobe de estado de uma partição serviço restaurado de um backup escolhido.

## <a name="types-of-backup"></a>Tipos de Backup
Há duas opções de backup: Completo e Incremental.
Um backup completo é um backup que contém todos os dados necessários Olá toorecreate Olá a estado da réplica Olá: pontos de verificação e todos os registros de log.
Desde que ele tem pontos de verificação hello e log hello, um backup completo pode ser restaurado por si só.

problema de saudação com backups completos surge quando os pontos de verificação de saudação são grandes.
Por exemplo, uma réplica com 16 GB de estado terá pontos de verificação que somam aproximadamente too16 GB.
Se houver um objetivo de ponto de recuperação de cinco minutos, a réplica de saudação precisa toobe backup a cada cinco minutos.
Cada vez que ele faz o backup precisa toocopy 16 GB de pontos de verificação Além disso too50 MB (configurável usando `CheckpointThresholdInMB`) a partir de logs.

![Exemplo de Backup Completo.](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

problema de toothis solução Olá é backups incrementais, onde backup contém apenas registros de log Olá alterado desde o último backup de saudação.

![Exemplo de Backup Incremental.](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

Como os backups incrementais são apenas as alterações feitas desde o último backup de saudação (não inclui pontos de verificação de saudação), eles tendem a toobe mais rápido, mas eles não podem ser restaurados por conta própria.
toorestore um backup incremental, toda a cadeia de backup Olá é necessária.
Uma cadeia de backup é uma cadeia de backups, começando com um backup completo e seguido por um número de backups incrementais contíguos.

## <a name="backup-reliable-services"></a>Fazer backup de Reliable Services
Olá, autor de serviço tem controle total sobre quando toomake backups e onde os backups serão armazenados.

toostart um backup, Olá serviço precisa de função de membro Olá herdada tooinvoke `BackupAsync`.  
Os backups podem ser feitos somente de réplicas primárias e eles requerem toobe de status de gravação concedido.

Conforme mostrado abaixo, `BackupAsync` assume um `BackupDescription` objeto, onde um pode especificar um backup completo ou incremental, bem como uma função de retorno de chamada, `Func<< BackupInfo, CancellationToken, Task<bool>>>` que é invocada quando a pasta de backup Olá foi criada localmente e está pronto toobe movido toosome armazenamento externo.

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

Solicitação tootake um backup incremental pode falhar com `FabricMissingFullBackupException`. Esta exceção indica que uma saudação coisas a seguir está ocorrendo:

- réplica Olá nunca tem feito um backup completo desde que ele se tornou primário,
- alguns dos Olá registros de log desde o último backup de saudação foi truncado ou
- réplica passada Olá `MaxAccumulatedBackupLogSizeInMB` limite.

Os usuários podem aumentar a probabilidade de saudação de ser capaz de toodo backups incrementais, configurando `MinLogSizeInMB` ou `TruncationThresholdFactor`.
Observe que esses valores de aumento aumenta Olá por uso de disco de réplica.
Para mais informações, confira [Configuração do Reliable Services](service-fabric-reliable-services-configuration.md)

`BackupInfo`Fornece informações sobre backup hello, incluindo a localização da pasta Olá onde o tempo de execução de saudação salvo backup Olá Olá (`BackupInfo.Directory`). função de retorno de chamada Hello pode mover Olá `BackupInfo.Directory` tooan repositório externo ou em outro local.  Essa função também retorna um booleano que indica se ele foi o local de destino de tooits toosuccessfully capaz de mover Olá pasta de backup.

Olá código a seguir demonstra como Olá `BackupCallbackAsync` método pode ser usado tooupload de saudação backup tooAzure armazenamento:

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

No exemplo anterior de hello, `ExternalBackupStore` é Olá exemplo toointerface usado com o armazenamento de BLOBs do Azure, e `UploadBackupFolderAsync` é o método hello que compacta pasta hello e coloca-o no repositório de Blob do Azure hello.

Observe que:

  - Pode haver apenas uma operação de backup em execução por réplica em um determinado momento. Mais de um `BackupAsync` chamada em um momento lançará `FabricBackupInProgressException` toolimit inflight backups tooone.
  - Se uma réplica falhar enquanto um backup está em andamento, backup Olá pode não ter sido completada. Portanto, quando Olá failover termina, é backup de saudação do serviço Olá responsabilidade toorestart invocando `BackupAsync` conforme necessário.

## <a name="restore-reliable-services"></a>Restaurar Reliable Services
Em geral, casos hello quando tooperform uma operação de restauração pode ser necessário se encaixam em uma dessas categorias:

  - serviço de saudação particionar dados perdidos. Por exemplo, disco Olá para dois dos três réplicas para uma partição (inclusive a réplica primária Olá) obtém corrompido ou apagado. novo primário de saudação talvez seja necessário toorestore dados de um backup.
  - todo o serviço Olá será perdido. Por exemplo, um administrador remove todo o serviço hello e dessa forma, o serviço hello e dados saudação precisam toobe restaurado.
  - serviço de saudação replicado dados corrompidos de aplicativo (por exemplo, devido a um erro de aplicativo). Nesse caso, Olá serviço toobe atualizado ou tooremove revertido Olá causa danos hello e dados corrompidos não tem toobe restaurado.

Embora muitas abordagens são possíveis, oferecemos alguns exemplos sobre como usar `RestoreAsync` toorecover de saudação acima cenários.

## <a name="partition-data-loss-in-reliable-services"></a>Perda de dados de partição em Reliable Services
Nesse caso, o tempo de execução de saudação seria automaticamente detectar a perda de dados hello e invocar Olá `OnDataLossAsync` API.

autor de serviço Olá precisa Olá tooperform toorecover a seguir:

  - Substituir o método da classe base virtual hello `OnDataLossAsync`.
  - Encontre hello mais recente backup no local de externo de saudação que contém os backups do serviço de saudação.
  - Baixar o backup mais recente da saudação (e descompactar backup Olá na pasta de backup Olá se ela foi compactada).
  - Olá `OnDataLossAsync` método fornece uma `RestoreContext`. Chamar hello `RestoreAsync` API em Olá fornecido `RestoreContext`.
  - Retorna VERDADEIRO se a restauração Olá tiver êxito.

A seguir está um exemplo de implementação de saudação `OnDataLossAsync` método:

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

`RestoreDescription`passado toohello `RestoreContext.RestoreAsync` chamada contém um membro chamado `BackupFolderPath`.
Ao restaurar um backup completo único, isso `BackupFolderPath` toohello o caminho local da pasta de saudação que contém o backup completo deve ser definido.
Ao restaurar um backup completo e um número de backups incrementais, `BackupFolderPath` deve ser definido como toohello o caminho local da pasta de saudação que contém não apenas o backup completo do hello, mas também todos os Olá backups incrementais.
`RestoreAsync`chamada pode lançar `FabricMissingFullBackupException` se hello `BackupFolderPath` fornecido não contém um backup completo.
Ela também poderá lançar `ArgumentException` se `BackupFolderPath` tiver uma cadeia quebrada de backups incrementais.
Por exemplo, se ele contiver Olá backup completo, primeiro Olá incremental e Olá terceiro backup incremental, mas nenhum backup incremental segundo de saudação.

> [!NOTE]
> Olá RestorePolicy é definido tooSafe por padrão.  Isso significa que Olá `RestoreAsync` API falhará com ArgumentException se ele detectar a pasta backup Olá contiver um estado que é o estado de toohello mais antigos do que ou igual contido nesta réplica.  `RestorePolicy.Force`pode ser usado tooskip essa verificação de segurança. Isso é especificado como parte de `RestoreDescription`.
> 

## <a name="deleted-or-lost-service"></a>Serviço perdido ou excluído
Se um serviço for removido, você deve primeiro novamente criar hello serviço antes de saudação dados podem ser restaurados.  É importante toocreate Olá serviço com hello a mesma configuração, por exemplo, o particionamento de esquema, para que Olá dados pode ser restaurada perfeitamente.  Após o serviço de hello, Olá dados toorestore de API (`OnDataLossAsync` acima) tem toobe invocado em todas as partições deste serviço. Uma maneira de fazer isso é usar `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` em cada partição.  

Desse ponto, a implementação é Olá igual a saudação acima cenário. Cada partição deve toorestore hello mais recente relevantes backup do armazenamento externo hello. Uma limitação é partição Olá que ID pode agora alterou, como tempo de execução Olá cria IDs de partição dinamicamente. Assim, Olá serviço precisa de informações de partição apropriado Olá toostore e serviço nome tooidentify Olá correta mais recente backup toorestore de para cada partição.

> [!NOTE]
> Não é recomendável toouse `FabricClient.ServiceManager.InvokeDataLossAsync` em cada partição toorestore Olá todo o serviço, desde que pode corromper o estado do cluster.
> 

## <a name="replication-of-corrupt-application-data"></a>Replicação de dados de aplicativo corrompidos
Se a atualização de aplicativo hello recentemente implantado tem um bug, que podem causar corrupção de dados. Por exemplo, uma atualização de aplicativo pode iniciar tooupdate cada registro do número de telefone em um dicionário confiável com o código de área é inválido.  Nesse caso, os números de telefone inválidos hello serão replicados pois Service Fabric não está ciente da natureza de saudação do dados Olá que estão sendo armazenados.

Olá primeiro toodo após detectar tal um bug atribuiremos que faz com que a corrupção de dados é toofreeze Olá serviço no nível do aplicativo hello e, se possível, atualize a versão toohello saudação do código do aplicativo que não tenha o bug hello.  No entanto, mesmo depois que o código de serviço Olá é fixo, dados saudação ainda podem estar corrompidos e, portanto, os dados podem ter toobe restaurado.  Nesses casos, pode não ser suficiente toorestore Olá backup mais recente, desde que os backups mais recentes Olá também podem estar corrompidos.  Portanto, você tem toofind Olá último backup feito antes Olá dados foi corrompido.

Se você não tiver certeza de que os backups estão corrompidos, você pode implantar um novo cluster do Service Fabric e restaure os backups de saudação de partições afetadas como Olá acima "Serviço perdido ou excluído" cenário.  Para cada partição, inicie a restauração de backups de saudação do toohello mais recente Olá menos. Depois de encontrar um backup que não possui corrupção hello, mover/excluir todos os backups que estavam mais recentes (que esse backup) dessa partição. Repita esse processo para cada partição. Agora, quando `OnDataLossAsync` é chamado na partição de saudação em cluster de produção de hello, Olá último backup encontrado em Olá externo repositório será Olá um separado por Olá acima de processo.

Agora, Olá etapas hello "Serviço perdido ou excluído" seção pode ser usada toorestore estado de saudação do estado do serviço de saudação toohello antes de um código com bug Olá corrompido estado hello.

Observe que:

  - Quando você restaurar, é a possibilidade de Olá backup está sendo restaurado há mais antigo do que o estado de saudação da partição Olá antes Olá dados foram perdidos. Por isso, você deve restaurar apenas como um último toorecover de recurso como a quantidade de dados possível.
  - Olá a cadeia de caracteres que representa o caminho da pasta de backup de saudação e hello caminhos de arquivos dentro da pasta de backup Olá podem ser maiores que 255 caracteres, dependendo do caminho de FabricDataRoot hello e o comprimento do nome do tipo de aplicativo. Isso pode causar alguns métodos do .NET, como `Directory.Move`, Olá toothrow `PathTooLongException` exceção. Uma solução alternativa é toodirectly chamar APIs kernel32, como `CopyFile`.

## <a name="backup-and-restore-reliable-actors"></a>Fazer backup e restaurar Reliable Actors


A Estrutura Reliable Actors foi criada com base nos Reliable Services. Olá ActorService que hospeda Olá actor(s) é um serviço confiável com monitoração de estado. Portanto, todos Olá backup e restauração funcionalidade disponível nos serviços confiáveis também atores tooReliable disponíveis (exceto comportamentos que são específicas do provedor de estado). Uma vez que os backups serão usados por partição, será feito backup dos estados de todos os atores nessa partição (e a restauração é semelhante e acontecerá de acordo com a partição). tooperform backup/restauração, o proprietário do serviço Olá deve criar uma classe de serviço de ator personalizado que deriva da classe ActorService e, em seguida, backup/restauração tooReliable semelhante serviços, conforme descritos nas seções anteriores.

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo)
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Quando você cria uma classe de serviço de ator personalizado, é necessário tooregister que também ao registrar o ator hello.

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

provedor de estado saudação padrão para Reliable Actors é `KvsActorStateProvider`. O backup incremental não é habilitado por padrão para `KvsActorStateProvider`. Você pode habilitar o backup incremental criando `KvsActorStateProvider` com hello adequado definindo no seu construtor e, em seguida, passando-o construtor tooActorService conforme mostrado no trecho de código a seguir:

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo, null, null, new KvsActorStateProvider(true)) // Enable incremental backup
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Após a habilitação do backup incremental, fazer um backup incremental pode falhar com FabricMissingFullBackupException por um dos seguintes motivos e você precisará tootake um backup completo antes de colocar um ou mais backups incremental:

  - réplica Olá nunca obteve um backup completo quando ele se tornou primário.
  - Alguns dos registros de log Olá foram truncadas desde o último backup foi feito.

Quando o backup incremental é habilitado, `KvsActorStateProvider` não usa buffer circular toomanage seu log de registros e trunca periodicamente. Se nenhum backup é feito por usuário por um período de 45 minutos, o sistema Olá trunca automaticamente registros de log de saudação. Esse intervalo pode ser configurado com a especificação de `logTrunctationIntervalInMinutes` na `KvsActorStateProvider` construtor (semelhante toowhen habilitar o backup incremental). registros de log Olá também podem obter truncados se a réplica primária precisa toobuild outra réplica enviando todos os seus dados.

Ao fazer a restauração a partir de uma cadeia de backup, serviços tooReliable semelhantes, Olá BackupFolderPath deve conter subdiretórios com um subdiretório contendo backup completo e outros subdiretórios que contém um ou mais backups incremental. API de restauração Olá lançará FabricException com a mensagem de erro apropriada se houver falha na validação da cadeia de backup de saudação. 

> [!NOTE]
> `KvsActorStateProvider`Atualmente, ignora a opção de saudação RestorePolicy.Safe. O suporte a esse recurso está planejado para uma versão futura.
> 

## <a name="testing-backup-and-restore"></a>Testando o backup e a restauração
É importante tooensure que dados críticos está sendo feitos e podem ser restaurados. Isso pode ser feito por meio de invocação Olá `Start-ServiceFabricPartitionDataLoss` cmdlet do PowerShell que pode provocar perda de dados em uma determinada partição tootest se dados saudação de backup e restaurar a funcionalidade para o serviço está funcionando conforme o esperado.  Também é possível tooprogrammatically invocar a perda de dados e restaurar a partir desse evento também.

> [!NOTE]
> Você pode encontrar um exemplo da implementação de backup e restaurar a funcionalidade em Olá aplicativo de referência da Web no GitHub. Examine a saudação `Inventory.Service` serviço para obter mais detalhes.
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a>Bastidores Olá: para obter mais detalhes sobre o backup e restauração
Veja mais alguns detalhes sobre backup e restauração.

### <a name="backup"></a>Backup
Olá Gerenciador de estado confiável fornece backups consistentes do hello capacidade toocreate sem bloquear qualquer ler ou gravar operações. toodo assim, ele utiliza um mecanismo de persistência do ponto de verificação e log.  Olá Gerenciador de estado confiável usa difusas pontos de verificação (lightweight) em determinados pressão de toorelieve pontos do log transacional hello e melhorar os tempos de recuperação.  Quando `BackupAsync` é chamado, Olá Gerenciador de estado confiável instrui toocopy de todos os objetos confiável seu último ponto de verificação arquivos tooa pasta backup local.  Em seguida, Olá Gerenciador de estado confiável copia todos os registros de log, começando pela hello "iniciar o ponteiro" toohello último registro de log na pasta de backup hello.  Como todos os registros de log Olá toohello registro de log mais recente são incluídos no backup hello e Gerenciador de estado confiável de saudação preserva o log write-ahead, Olá Gerenciador de estado confiável garante que todas as transações que são confirmadas (`CommitAsync` retornou com êxito) são incluídos no backup de saudação.

Qualquer transação confirmada após `BackupAsync` foi chamado pode ou não estejam no backup hello.  Depois que a pasta de backup local Olá foi preenchida pela plataforma hello (ou seja, o backup local é concluído pelo tempo de execução de saudação), retorno de chamada de backup do serviço de saudação é invocado.  Esse retorno de chamada é responsável por mover Olá pasta de backup tooan local externo, como o armazenamento do Azure.

### <a name="restore"></a>Restaurar
Olá Gerenciador de estado confiável fornece Olá toorestore de capacidade de um backup usando Olá `RestoreAsync` API.  
Olá `RestoreAsync` método `RestoreContext` pode ser chamado somente no hello `OnDataLossAsync` método.
Olá bool retornado por `OnDataLossAsync` indica se o serviço de saudação restaurado a seu estado de uma fonte externa.
Se hello `OnDataLossAsync` retorna true, o Service Fabric reconstruirá todas as outras réplicas desse primário. Service Fabric garante que receberão as réplicas `OnDataLossAsync` chamar a função primária do primeiro transição toohello, mas não são legíveis concedeu status ou gravar o status.
Isso significa que, para os implementadores de StatefulService, `RunAsync` não será chamado até que `OnDataLossAsync` seja concluído com êxito.
Em seguida, `OnDataLossAsync` será invocado no novo primário de saudação.
Até que um serviço é concluída essa API com êxito (retornando true ou false) e conclusão da reconfiguração relevantes Olá, Olá API será manter sendo chamado um de cada vez.

`RestoreAsync`primeiro descarta todos os estados existentes na réplica primária de saudação que ele foi chamado em.  
Olá Gerenciador de estado confiável cria todos os objetos de saudação confiável que existem na pasta de backup hello.  
Em seguida, objetos confiável Olá são instruções toorestore dos seus pontos de verificação na pasta de backup hello.  
Por fim, Olá Gerenciador de estado confiável recupera seu próprio estado Olá dos registros de log na pasta de backup hello e executa a recuperação.  
Como parte do processo de recuperação Olá, hello "ponto de partida" a partir de operações que têm registros de log de confirmação na pasta de backup de saudação são objetos confiável toohello reproduzido.  
Essa etapa garante que Olá estado recuperado é consistente.

## <a name="next-steps"></a>Próximas etapas
  - [Coleções Confiáveis](service-fabric-work-with-reliable-collections.md)
  - [Início Rápido dos Serviços Confiáveis](service-fabric-reliable-services-quick-start.md)
  - [Notificações do Reliable Services](service-fabric-reliable-services-notifications.md)
  - [Configuração do Reliable Services](service-fabric-reliable-services-configuration.md)
  - [Referência do desenvolvedor para Coleções Confiáveis](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

