---
title: "atualizações de aplicativo aaaRolling - banco de dados do SQL Azure | Microsoft Docs"
description: "Saiba como toouse replicação geográfica do Azure SQL Database toosupport online atualizações do seu aplicativo na nuvem."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 58f42859-1e37-463c-a3d8-a3ca2e867148
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/16/2016
ms.author: sashan
ms.openlocfilehash: 18c56300916d129bff141624cc5c416b500408d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-rolling-upgrades-of-cloud-applications-using-sql-database-active-geo-replication"></a>Gerenciando a rolagem de atualizações de aplicativos na nuvem usando a replicação geográfica ativa do Banco de dados SQL
> [!NOTE]
> A [replicação geográfica ativa](sql-database-geo-replication-overview.md) agora está disponível para todos os bancos de dados em todas as camadas.
> 

Saiba como toouse [georeplicação](sql-database-geo-replication-overview.md) no banco de dados SQL tooenable as atualizações sem interrupção do seu aplicativo na nuvem. Como a atualização é uma operação com interrupção, ele deve fazer parte de seu design e planejamento de continuidade dos negócios. Neste artigo, que vamos examinar dois métodos diferentes de orquestração Olá processo de atualização e discutir os benefícios de saudação e vantagens e desvantagens de cada opção. Para fins de saudação deste artigo, usaremos um aplicativo simples que consiste em um site da web conectados tooa banco de dados como sua camada de dados. Nosso objetivo é tooupgrade versão 1 do hello aplicativo tooversion 2 sem qualquer impacto significativo na experiência do usuário final de saudação. 

Ao avaliar as opções de atualização Olá considere Olá fatores a seguir:

* Impacto na disponibilidade do aplicativo durante atualizações. A função de aplicativo hello quanto tempo pode ser limitada ou degradada.
* Capacidade tooroll novamente em caso de uma falha de atualização.
* Vulnerabilidade do aplicativo hello se ocorrer uma falha catastrófica relacionada durante a atualização de saudação.
* Custo total em dólares.  Isso inclui a redundância adicional e custos incrementais dos componentes de temporário Olá usados pelo processo de atualização de saudação. 

## <a name="upgrading-applications-that-rely-on-database-backups-for-disaster-recovery"></a>Atualizando aplicativos que dependem de backups de banco de dados para recuperação de desastre
Se seu aplicativo depende de backups de banco de dados automática e usa a restauração geográfica para recuperação de desastres, é normalmente implantado tooa única região do Azure. Nesse caso o processo de atualização Olá envolve a criação de uma implantação de todos os componentes do aplicativo de backup envolvidos na atualização de saudação. interrupção do toominimize saudação do usuário final você aproveitará o Azure Traffic Manager (WATM) com o perfil de failover de saudação.  Olá diagrama a seguir ilustra o processo de atualização do hello ambiente operacional toohello anterior. ponto de extremidade de Olá <i>1.azurewebsites.net contoso</i> representa um slot de produção do aplicativo hello que precisa toobe atualizado. tooenable Olá capacidade tooroll volta Olá atualização, você precisa criar um slot de estágio com uma cópia totalmente sincronizada do aplicativo hello. Olá etapas a seguir são necessárias tooprepare Olá aplicativo para atualização de saudação:

1. Crie um slot de estágio para atualização de saudação. toodo que criar um banco de dados secundário (1) e implantar um site idêntico em Olá mesma região do Azure. Monitorar toosee secundário Olá se Olá processo de preparação foi concluída.
2. Crie um perfil de failover no WATM com <i>contoso-1.azurewebsites.net</i> como ponto de extremidade online e <i>contoso-2.azurewebsites.net</i> como offline. 

> [!NOTE]
> Etapas de preparação de saudação Observação não terá impacto sobre o aplicativo hello no slot de produção de hello e ele pode funcionar em modo de acesso completo.
>  

![Configuração da Replicação Geográfica do Banco de Dados SQL. Recuperação de desastre em nuvem.](media/sql-database-manage-application-rolling-upgrade/Option1-1.png)

Depois que as etapas de preparação Olá forem concluídas aplicativo hello está pronto para atualização real hello. Olá diagrama a seguir ilustra as etapas de Olá envolvidas no processo de atualização de saudação. 

1. Definir banco de dados primário Olá no hello slot tooread somente modo de produção (3). Isso garantirá que Olá instância de produção do aplicativo hello (V1) permanecerá somente leitura durante a atualização de saudação impedindo divergência de dados Olá entre hello V1 e V2 instâncias de banco de dados.  
2. Desconecte o banco de dados secundário hello usando o modo de encerramento planejado hello (4). Ele criará uma cópia independente totalmente sincronizada do banco de dados primário hello. Este banco de dados será atualizado.
3. Ativar o modo de gravação tooread Olá banco de dados primário e execute o script de atualização de saudação no slot de estágio da saudação (5).     

![Configuração da replicação geográfica do banco de dados SQL. Recuperação de desastre em nuvem.](media/sql-database-manage-application-rolling-upgrade/Option1-2.png)

Se Olá atualização concluída com êxito você, são agora pronto tooswitch Olá os usuários finais toohello preparado cópia Olá aplicativos. Agora, ela ficará slot de produção de hello do aplicativo hello.  Isso envolve algumas etapas mais conforme ilustrado no diagrama a seguir de saudação.

1. Alternar ponto de extremidade online Olá no perfil do WATM Olá muito<i>2.azurewebsites.net contoso</i>, qual versão de toohello V2 pontos do site da web de saudação (6). Agora se torna slot de produção de hello com hello V2 aplicativo e o tráfego do usuário final Olá é tooit direcionado.  
2. Se você não precisar mais componentes do aplicativo hello V1 forma você poderá removê-los (7).   

![Configuração da replicação geográfica do banco de dados SQL. Recuperação de desastre em nuvem.](media/sql-database-manage-application-rolling-upgrade/Option1-3.png)

Se o processo de atualização de saudação for bem-sucedida, por exemplo devido a erro tooan no script de atualização hello, slot de estágio Olá deve ser considerada comprometida. tooroll fazer Olá toohello pré-atualização o estado do aplicativo simplesmente reverter o aplicativo hello no acesso de toofull de slot de produção de hello. etapas de Olá envolvidas são mostradas no diagrama seguinte hello.    

1. Definir o modo de gravação tooread de cópia do hello banco de dados (8). Isso irá restaurar Olá V1 completo funcionalmente no slot de produção de hello.
2. Executar a análise da causa raiz hello e remover componentes Olá comprometido no slot de estágio da saudação (9). 

Neste ponto aplicativo hello é totalmente funcional e etapas de atualização de saudação podem ser repetidas.

> [!NOTE]
> Olá reversão não requer alterações no perfil do WATM como aponta já muito<i>1.azurewebsites.net contoso</i> como Olá ponto de extremidade ativo.
> 
> 

![Configuração da replicação geográfica do banco de dados SQL. Recuperação de desastre em nuvem.](media/sql-database-manage-application-rolling-upgrade/Option1-4.png)

chave de saudação **vantagem** dessa opção é que você pode atualizar um aplicativo em uma única região usando um conjunto de etapas simples. custo de dólar Olá de atualização de saudação é relativamente baixo. Olá principal **compensação** é que se ocorrer uma falha catastrófica durante o estado anterior à atualização do toohello Olá Olá atualização recuperação envolve a reimplantação do aplicativo hello em uma região diferente e restaurando banco de dados de saudação do backup usando a restauração geográfica. Esse processo resultará em um tempo de inatividade significativo.   

## <a name="upgrading-applications-that-rely-on-database-geo-replication-for-disaster-recovery"></a>Atualizando aplicativos que dependem de replicação geográfica de banco de dados para recuperação de desastre
Se seu aplicativo utiliza a replicação geográfica para continuidade de negócios, é tooat implantado pelo menos dois diferentes regiões com uma implantação ativa na região primária e uma implantação em espera na região de Backup. Além disso toohello fatores mencionado anteriormente, o processo de atualização Olá deve garantir que:

* aplicativo Hello permanece protegido contra falhas catastróficas em todos os momentos durante o processo de atualização Olá
* componentes com redundância geográfica de saudação do aplicativo hello são atualizados em paralelo com componentes ativos Olá

tooachieve esses objetivos otimizará o Traffic Manager WATM (Azure) usando failover Olá perfil com uma ativa e três pontos de extremidade de backup.  Olá diagrama a seguir ilustra o processo de atualização do hello ambiente operacional toohello anterior. Olá sites da web <i>contoso 1.azurewebsites.net</i> e <i>dr.azurewebsites.net contoso</i> representar um slot de produção do aplicativo hello com redundância geográfica. tooenable Olá capacidade tooroll volta Olá atualização, você precisa criar um slot de estágio com uma cópia totalmente sincronizada do aplicativo hello. Porque você precisa tooensure aplicativo hello pode recuperar rapidamente no caso de uma falha catastrófica ocorre durante o processo de atualização hello, slot de estágio Olá precisa toobe com redundância geográfica também. Olá etapas a seguir são necessárias tooprepare Olá aplicativo para atualização de saudação:

1. Crie um slot de estágio para atualização de saudação. toodo que criar um banco de dados secundário (1) e implantar uma cópia idêntica de site da web Olá Olá mesma região do Azure. Monitorar toosee secundário Olá se Olá processo de preparação foi concluída.
2. Criar um banco de dados secundário com redundância geográfica no slot de estágio Olá por replicação geográfica Olá banco de dados secundário toohello backup região (Isso é chamado de "encadeados replicação geográfica"). Monitorar toosee secundária do backup Olá se Olá propagação processo for concluído (3).
3. Criar uma cópia em espera do site Olá na região backup hello e vinculá-lo toohello com redundância geográfica secundário (4).  
4. Adicionar pontos de extremidade adicionais Olá <i>contoso 2.azurewebsites.net</i> e <i>3.azurewebsites.net contoso</i> toohello perfil de failover no WATM como pontos de extremidade offline (5). 

> [!NOTE]
> Etapas de preparação de saudação Observação não terá impacto sobre o aplicativo hello no slot de produção de hello e ele pode funcionar em modo de acesso completo.
> 
> 

![Configuração da replicação geográfica do banco de dados SQL. Recuperação de desastre em nuvem.](media/sql-database-manage-application-rolling-upgrade/Option2-1.png)

Depois que as etapas de preparação Olá forem concluídas, slot de estágio hello está pronto para atualização de saudação. Olá diagrama a seguir ilustra as etapas de atualização hello.

1. Definir banco de dados primário Olá no hello slot tooread somente modo de produção (6). Isso garantirá que Olá instância de produção do aplicativo hello (V1) permanecerá somente leitura durante a atualização de saudação impedindo divergência de dados Olá entre hello V1 e V2 instâncias de banco de dados.  
2. Desconecte o banco de dados secundário Olá no hello mesmo região usando Olá modo de encerramento planejado (7). Ele cria uma cópia independente totalmente sincronizada Olá banco de dados primário, que se tornará automaticamente um primário após o encerramento de saudação. Este banco de dados será atualizado.
3. Ativar o banco de dados primário Olá no modo de gravação tooread de slot de estágio hello e execute o script de atualização de saudação (8).    

![Configuração da replicação geográfica do banco de dados SQL. Recuperação de desastre em nuvem.](media/sql-database-manage-application-rolling-upgrade/Option2-2.png)

Se Olá atualização concluída com êxito agora você está pronto tooswitch Olá os usuários finais toohello V2 versão Olá aplicativo. Olá diagrama a seguir ilustra as etapas de saudação envolvidas.

1. Alternar ponto de extremidade ativo Olá no perfil do WATM Olá muito<i>2.azurewebsites.net contoso</i>, que agora aponta toohello V2 versão do site da web de saudação (9). Agora se torna um slot de produção com hello V2 aplicativo e o tráfego do usuário final é tooit direcionado. 
2. Se você não precisar mais aplicativos de V1 Olá para que você possa com segurança removido (10 e 11).  

![Configuração da replicação geográfica do banco de dados SQL. Recuperação de desastre em nuvem.](media/sql-database-manage-application-rolling-upgrade/Option2-3.png)

Se o processo de atualização de saudação for bem-sucedida, por exemplo devido a erro tooan no script de atualização hello, slot de estágio Olá deve ser considerada comprometida. tooroll fazer Olá toohello pré-atualização o estado do aplicativo simplesmente reverter o aplicativo de hello toousing no slot de produção de hello com acesso completo. etapas de Olá envolvidas são mostradas no diagrama seguinte hello.    

1. Conjunto Olá cópia de banco de dados primário no modo de gravação de tooread de slot de produção de hello (12). Isso irá restaurar Olá V1 completo funcionalmente no slot de produção de hello.
2. Executar a análise da causa raiz hello e remover componentes do hello comprometido no slot de estágio da saudação (13 e 14). 

Neste ponto aplicativo hello é totalmente funcional e etapas de atualização de saudação podem ser repetidas.

> [!NOTE]
> Olá reversão não requer alterações no perfil do WATM como aponta já muito <i>1.azurewebsites.net contoso</i> como Olá ponto de extremidade ativo.
> 
> 

![Configuração da replicação geográfica do banco de dados SQL. Recuperação de desastre em nuvem.](media/sql-database-manage-application-rolling-upgrade/Option2-4.png)

chave de saudação **vantagem** dessa opção é que você pode atualizar o aplicativo hello e sua cópia com redundância geográfica em paralelo sem comprometer a continuidade dos negócios durante a atualização de saudação. Olá principal **compensação** é que ele requer redundância dupla de cada componente do aplicativo e, portanto, incorre em custo mais alto de dólares. Ele também envolve um fluxo de trabalho mais complicado. 

## <a name="summary"></a>Resumo
métodos de atualização Olá dois descritos no artigo Olá diferem em dólar hello e complexidade de custo, mas ambos se concentrar na minimização de tempo de saudação quando o usuário final de saudação é limitado de operações somente tooread. Esse tempo é definido diretamente por duração Olá Olá do script de atualização. Ele não depende de tamanho de banco de dados hello, Olá de camada de serviço você escolher, configuração de site da web hello e outros fatores que você não pode controlar facilmente. Isso ocorre porque todas as etapas de preparação de saudação são desacopladas etapas de atualização de saudação e podem ser feitas sem afetar o aplicativo de produção de hello. eficiência de Olá Olá do script de atualização é Olá fator-chave que determina a experiência do usuário final de saudação durante as atualizações. Portanto, Olá melhor maneira aprimorá-la é concentrando seus esforços em tornar o script de atualização hello mais eficiente possível.  

## <a name="next-steps"></a>Próximas etapas
* Para obter uma visão geral e os cenários de continuidade dos negócios, consulte [Visão geral da continuidade dos negócios](sql-database-business-continuity.md).
* toolearn sobre backups de banco de dados do SQL Azure automatizadas, consulte [backups automatizados de banco de dados SQL](sql-database-automated-backups.md).
* toolearn sobre como usar backups automatizados para recuperação, consulte [restaurar um banco de dados de backups automatizados](sql-database-recovery-using-backups.md).
* toolearn sobre as opções de recuperação mais rápidas, consulte [replicação geográfica ativa](sql-database-geo-replication-overview.md).


