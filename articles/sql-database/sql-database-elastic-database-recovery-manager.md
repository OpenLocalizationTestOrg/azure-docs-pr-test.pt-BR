---
title: "aaaUsing toofix do Gerenciador de recuperação do fragmento mapear problemas | Microsoft Docs"
description: "Use Olá RecoveryManager classe toosolve problemas mapas de fragmento"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>Usando os problemas de mapa de fragmento Olá RecoveryManager classe toofix
Olá [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) classe fornece aplicativos ADO.Net Olá capacidade tooeasily detectar e corrigir as inconsistências entre o mapa do fragmento global de saudação (GSM) e o mapa de fragmentos de local de saudação (LSM) em um ambiente de banco de dados fragmentado. 

Olá GSM LSM acompanhar Olá mapeamento e de cada banco de dados em um ambiente fragmentado. Ocasionalmente, uma quebra ocorre entre Olá GSM e hello LSM. Nesse caso, use Olá RecoveryManager classe toodetect e reparar quebra hello.

Olá RecoveryManager classe faz parte da saudação [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md). 

![Mapa de fragmentos][1]

Para obter definições de termos, consulte o [Glossário de ferramentas do Banco de Dados Elástico](sql-database-elastic-scale-glossary.md). como Olá toounderstand **ShardMapManager** toomanage usados dados em uma solução fragmentada, consulte [gerenciamento de mapa do fragmento](sql-database-elastic-scale-shard-map-management.md).

## <a name="why-use-hello-recovery-manager"></a>Por que usar o Gerenciador de recuperação Olá?
Em um ambiente de banco de dados fragmentado, há um locatário por banco de dados e muitos bancos de dados por servidor. Também pode haver vários servidores no ambiente de saudação. Cada banco de dados está mapeado no mapa do fragmento hello, para que chamadas possam ser banco de dados e o servidor correto toohello roteadas. Bancos de dados são controlados de acordo com o tooa **chave de fragmentação**, e cada fragmento é atribuído um **intervalo de valores de chave**. Por exemplo, uma chave de fragmentação pode representar os nomes de clientes de saudação de "D" muito "f" Olá mapeamento de todos os fragmentos (também conhecido como bancos de dados) e seus intervalos de mapeamento estão contidos em Olá **mapa do fragmento global (GSM)**. Cada banco de dados também contém um mapa de intervalos de saudação contidos no fragmento de saudação que é conhecido como Olá **mapa do fragmento local (LSM)**. Quando um aplicativo se conecta tooa fragmento, mapeamento de saudação é armazenado em cache com o aplicativo hello para recuperação rápida. Olá LSM é usado toovalidate em cache dados. 

Olá GSM e LSM podem se tornar fora de sincronia para Olá motivos a seguir:

1. exclusão de saudação de um fragmento cujo intervalo considerado toono mais estar em uso ou a renomeação de um fragmento. A exclusão de um fragmento resulta em um **mapeamento de fragmento órfão**. De modo semelhante, um banco de dados renomeado pode causar um mapeamento de fragmentos órfãos. Dependendo da intenção de saudação de alteração hello, fragmento de saudação pode precisar toobe removido ou local de fragmento de saudação precisa toobe atualizado. toorecover um banco de dados excluído, consulte [restaurar um banco de dados excluído](sql-database-recovery-using-backups.md).
2. Ocorre um evento de failover geográfico. toocontinue, um deve atualizar o nome do servidor de saudação e nome de banco de dados do Gerenciador do mapa de fragmentos no aplicativo hello e, em seguida, detalhes de mapeamento de fragmentos de saudação atualização para todos os fragmentos em um mapa do fragmento. Se houver um failover geográfico, uma lógica de recuperação deve ser automatizada de fluxo de trabalho de failover de saudação. A automação das ações de recuperação proporciona capacidade de gerenciamento ininterrupta para bancos de dados habilitados geograficamente e evita ações humanas manuais. toolearn sobre opções toorecover um banco de dados se houver uma interrupção de centro de dados, consulte [continuidade dos negócios](sql-database-business-continuity.md) e [a recuperação de desastres](sql-database-disaster-recovery.md).
3. Banco de dados ShardMapManager um fragmento ou Olá é restaurado tooan ponto no tempo anterior. toolearn sobre recuperação pontual usando backups, consulte [recuperação usando backups](sql-database-recovery-using-backups.md).

Para obter mais informações sobre ferramentas de banco de dados Elástico banco de dados SQL, a replicação geográfica e restauração, consulte o seguinte hello: 

* [Visão geral: continuidade de negócios em nuvem e recuperação de desastre do banco de dados com o banco de dados SQL](sql-database-business-continuity.md) 
* [Comece com ferramentas de banco de dados elástico](sql-database-elastic-scale-get-started.md)  
* [Gerenciamento de ShardMap](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>Recuperando o RecoveryManager de um ShardMapManager
Olá primeira etapa é toocreate uma instância de RecoveryManager. Olá [GetRecoveryManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) retorna Olá Gerenciador de recuperação para Olá atual [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) instância. tooaddress quaisquer inconsistências no fragmento de saudação do mapa, primeiro você deve recuperar hello RecoveryManager para mapa do fragmento específico de saudação. 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

Neste exemplo, Olá RecoveryManager é inicializada de saudação ShardMapManager. Olá ShardMapManager que contém um ShardMap também já foi inicializado. 

Desde que este código de aplicativo manipula o mapa do fragmento Olá em si, Olá credenciais usadas no método de fábrica hello (em Olá anterior como exemplo, smmConnectionString) devem ser credenciais que têm permissões de leitura e gravação no banco de dados do GSM Olá referenciado por Olá cadeia de caracteres de conexão. Essas credenciais são normalmente diferentes das credenciais usadas tooopen conexões de roteamento dependente de dados. Para obter mais informações, consulte [usando as credenciais no cliente de banco de dados Elástico Olá](sql-database-elastic-scale-manage-credentials.md).

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>Removendo um fragmento de saudação ShardMap depois que um fragmento é excluído
Olá [DetachShard método](https://msdn.microsoft.com/library/azure/dn842083.aspx) desanexa Olá fornecida fragmento do mapa do fragmento hello e exclui os mapeamentos associados a fragmentos de saudação.  

* parâmetro de local de saudação é o local de fragmento de hello, especificamente o nome do servidor e o nome do banco de dados de fragmento hello está sendo desanexado. 
* parâmetro de shardMapName Hello é nome do mapa de fragmentos hello. Isso só é necessária quando vários mapas de fragmento são gerenciados pelo Olá mesmo Gerenciador de mapa do fragmento. Opcional. 


> [!IMPORTANT]
> Use essa técnica somente se você tiver certeza de que o intervalo de saudação para mapeamento de saudação atualizado é vazio. métodos de saudação acima não verificam dados para o intervalo de saudação que está sendo movido, portanto, é melhor tooinclude verifica no seu código.
>

Este exemplo remove os fragmentos de mapa do fragmento hello. 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

mapa do fragmento Olá reflete o local de fragmento Olá Olá GSM antes da exclusão de saudação do fragmento hello. Como fragmentos Olá foi excluído, será considerado foi intencional e intervalo de chave de fragmentação Olá não está mais em uso. Se esse não for o caso, você poderá executar a restauração pontual. fragmento de saudação toorecover de um point-in-time anterior. (Nesse caso, examine Olá inconsistências de fragmento de toodetect seção a seguir). toorecover, consulte [recuperação pontual](sql-database-recovery-using-backups.md).

Considerando a exclusão de banco de dados Olá tenha sido intencional, hello ação de limpeza administrativas final é fragmento do toodelete Olá entrada toohello no Gerenciador do mapa de fragmento de saudação. Isso impede que o aplicativo hello inadvertidamente gravar o intervalo de tooa informações que não é esperado.

## <a name="toodetect-mapping-differences"></a>diferenças de mapeamento de toodetect
Olá [DetectMappingDifferences método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) seleciona e retorna um dos mapas de fragmento da saudação (locais ou globais) como fonte de saudação da verdade e reconcilia os mapeamentos de ambos os mapas de fragmento (GSM e LSM).

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* Olá *local* Especifica o nome do servidor de saudação e o nome do banco de dados. 
* Olá *shardMapName* parâmetro é o nome do mapa de fragmentos hello. Isso só é necessário se vários mapas de fragmento são gerenciados pelo Olá mesmo Gerenciador de mapa do fragmento. Opcional. 

## <a name="tooresolve-mapping-differences"></a>diferenças de mapeamento de tooresolve
Olá [ResolveMappingDifferences método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) seleciona um dos mapas de fragmento da saudação (locais ou globais) como fonte de saudação da verdade e reconcilia os mapeamentos de ambos os mapas de fragmento (GSM e LSM).

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* Olá *RecoveryToken* parâmetro enumera Olá diferenças mapeamentos de saudação hello GSM e hello LSM para fragmentos específicos hello. 
* Olá [MappingDifferenceResolution enumeração](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) é usado tooindicate Olá método para resolver a diferença de saudação entre mapeamentos de fragmento de saudação. 
* **MappingDifferenceResolution.KeepShardMapping** é recomendável que, quando Olá LSM contém mapeamento precisas hello e, portanto, o mapeamento de saudação no fragmento de saudação deve ser usado. Isso acontece normalmente Olá se houver um failover: fragmento Olá agora reside em um novo servidor. Desde que o fragmento de saudação deve ser removido da saudação GSM (usando o método de RecoveryManager.DetachShard hello), um mapeamento não existe mais no hello GSM. Portanto, Olá LSM deve ser usado toore-estabelecer Olá mapeamento de fragmentos.

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>Anexar um fragmento de toohello ShardMap depois que um fragmento é restaurado
Olá [AttachShard método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) anexa Olá mapa do fragmento toohello fragmento especificado. Ele detecta as inconsistências de mapa do fragmento e atualiza o fragmento de saudação do hello mapeamentos toomatch no ponto de saudação da restauração de fragmento de saudação. Presume-se que esse banco de dados de saudação é também tooreflect renomeado Olá banco de dados nome original (antes de fragmento de saudação foi restaurado), desde que a restauração pontual de saudação padrões tooa novo banco de dados anexado com carimbo de hora hello. 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* Olá *local* parâmetro é o nome do servidor de saudação e o nome do banco de dados de fragmento Olá que está sendo anexado. 
* Olá *shardMapName* parâmetro é o nome do mapa de fragmentos hello. Isso só é necessária quando vários mapas de fragmento são gerenciados pelo Olá mesmo Gerenciador de mapa do fragmento. Opcional. 

Este exemplo adiciona um mapa do fragmento toohello fragmento que foram restaurado recentemente de um tempo de ponto anterior. Como o fragmento hello (ou seja, Olá mapeamento de fragmentos de saudação em Olá LSM) tiver sido restaurado, é potencialmente inconsistente com entrada de fragmento Olá Olá GSM. Fora do código de exemplo, o fragmento de saudação foi restaurado e renomeado toohello o nome original do banco de dados de saudação. Desde que ele foi restaurado, presume-se mapeamento de saudação no hello LSM é mapeamento confiável hello. 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>Atualizar locais de fragmento após um failover geográfico (Restaurar) de fragmentos de saudação
Se houver um failover geográfico, o banco de dados secundário Olá é disponibilizado de gravação e se torna Olá novo principal banco de dados. Olá nome do servidor de saudação e, potencialmente, banco de dados de saudação (dependendo da configuração), pode ser diferente do primário original hello. Olá, portanto, as entradas de mapeamento de fragmento de saudação em Olá GSM e LSM deve ser corrigido. Da mesma forma, se hello banco de dados é restaurado tooa outro nome ou local ou tooan ponto anterior no tempo, isso pode causar inconsistências no hello mapas de fragmento. Olá Gerenciador do mapa de fragmentos lida com a distribuição de saudação do banco de dados correto do toohello conexões abertas. Distribuição baseia-se em dados de saudação no mapa do fragmento hello e valor de saudação da chave de fragmentação Olá Olá destino da solicitação de aplicativos de saudação. Após um failover geográfico, essas informações devem ser atualizadas com o nome do servidor precisa de saudação, nome do banco de dados e mapeamento de fragmentos de banco de dados recuperado Olá. 

## <a name="best-practices"></a>Práticas recomendadas
Failover de replicação geográfica e recuperação são operações que normalmente são gerenciadas por um administrador de nuvem do aplicativo hello intencionalmente utilizando um dos recursos de continuidade de negócios de bancos de dados do Azure SQL. Planejamento de continuidade de negócios exige processos, procedimentos e medidas tooensure que operações comerciais possam continuar sem interrupções. Olá métodos disponíveis como parte do hello RecoveryManager classe deve ser usada nessa saudação de tooensure de fluxo de trabalho GSM e LSM são mantidos atualizados com base na ação de recuperação Olá realizada. Há cinco etapas básicas tooproperly garantindo Olá GSM e LSM refletem informações precisas de saudação após um evento de failover. Olá tooexecute de código de aplicativo, que essas etapas podem ser integradas no fluxo de trabalho e as ferramentas existentes. 

1. Recupere Olá RecoveryManager de saudação ShardMapManager. 
2. Desanexe o fragmento antigo de saudação do mapa do fragmento hello.
3. Anexe Olá novo fragmento toohello mapa do fragmento, incluindo o novo local de fragmento hello.
4. Detecte inconsistências no hello mapeamento entre hello GSM e LSM. 
5. Resolva as diferenças entre Olá GSM e hello LSM, Olá confiante LSM. 

Este exemplo executa Olá etapas a seguir:

1. Remove fragmentos Olá mapa do fragmento que refletem os locais de fragmento antes do evento de failover de saudação.
2. Anexa fragmentos toohello mapa do fragmento refletindo Olá novos fragmentos locais (parâmetro hello "Configuration.SecondaryServer" é o novo nome do servidor Olá mas Olá mesmo nome de banco de dados).
3. Recupera os tokens de recuperação Olá detectando diferenças de mapeamento entre hello GSM e hello LSM para cada fragmento. 
4. Resolve inconsistências Olá mapeando confiante Olá da saudação LSM de cada fragmento. 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

