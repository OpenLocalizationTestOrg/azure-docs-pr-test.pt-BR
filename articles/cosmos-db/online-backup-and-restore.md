---
title: "aaaOnline backup e restauração com o banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como tooperform automático de backup e restauração em um banco de dados do banco de dados do Azure Cosmos."
keywords: "backup e restauração, backup online"
services: cosmos-db
documentationcenter: 
author: RahulPrasad16
manager: jhubbard
editor: monicar
ms.assetid: 98eade4a-7ef4-4667-b167-6603ecd80b79
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/11/2017
ms.author: raprasa
ms.openlocfilehash: a0b464c95681dfc7b5462b02bf04c2c43d6bc16f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>Backup e restauração online automáticos com o Azure Cosmos DB
O Azure Cosmos DB faz backup automaticamente de todos os seus dados em intervalos regulares. backups automáticos de saudação são feitos sem afetar o desempenho de saudação ou disponibilidade de suas operações de banco de dados. Todos os backups são armazenados separadamente em outro serviço de armazenamento, e esses backups são replicados globalmente para resiliência contra desastres regionais. backups automáticos Olá destinam-se para cenários quando você acidentalmente excluir o contêiner de banco de dados Comos e posteriores exige a recuperação de dados ou uma solução de recuperação de desastres.  

Este artigo começa com uma recapitulação rápida de redundância de dados hello e a disponibilidade de banco de dados do Cosmos e discute backups. 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Alta disponibilidade com o Cosmos DB – recapitulação
Cosmos banco de dados é projetado toobe [globalmente distribuídos](distribute-data-globally.md) – permite a você tooscale taxa de transferência em várias regiões do Azure junto com a política controlada por failover e as APIs de hospedagem múltipla transparentes. Como uma oferta de sistema de banco de dados [disponibilidade de 99,99% SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db), todas as gravações Olá no banco de dados do Cosmos são discos toolocal permanentemente confirmado por um quorum de réplicas dentro de um data center local antes de confirmar toohello cliente. Observe que a alta disponibilidade de saudação do Cosmos DB depende do armazenamento local e não depende de qualquer tecnologia de armazenamento externo. Além disso, se sua conta de banco de dados está associada a mais de uma região do Azure, suas gravações são replicadas em outras regiões também. tooscale seus dados em latências de baixas taxa de transferência e acesso, você pode ter muitos ler regiões associados à sua conta de banco de dados como desejar. Em cada região de leitura, dados saudação (replicada) forma durável são mantidos em um conjunto de réplicas.  

Conforme ilustrado no diagrama a seguir de saudação, é um único contêiner de banco de dados do Cosmos [particionado horizontalmente](partition-data.md). Uma partição"" é indicada por um círculo em Olá diagrama a seguir, e cada partição é feita altamente disponível por meio de um conjunto de réplicas. Isso é a distribuição local hello dentro de uma única região do Azure (indicada pelo eixo X de saudação). Além disso, cada partição (com seu conjunto de réplica correspondente) globalmente, em seguida, é distribuída entre várias regiões associados à sua conta de banco de dados (por exemplo, nesta ilustração Olá três regiões – Leste dos EUA, oeste dos EUA e Índia Central). Olá "conjunto de partições" é distribuída globalmente entidade que consiste de várias cópias de seus dados em cada região (indicado pelo eixo Y da saudação). Você pode atribuir prioridade regiões toohello associados à sua conta de banco de dados e banco de dados do Cosmos será transparente failover toohello próxima área em caso de desastre. Manualmente, você pode simular disponibilidade de ponta a ponta do failover tootest saudação do seu aplicativo.  

Olá imagem a seguir ilustra alto grau de saudação de redundância de banco de dados do Cosmos.

![Alto grau de redundância com o Cosmos DB](./media/online-backup-and-restore/redundancy.png)

![Alto grau de redundância com o Cosmos DB](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>Backups online completos, automáticos
Opa, excluí meu contêiner ou banco de dados! Com o banco de dados do Cosmos, não apenas a dados, mas backups Olá dos seus dados também são feitas desastres tooregional altamente resiliente e redundantes. Esses backups automatizados são feitos atualmente a cada quatro horas, aproximadamente, e os últimos 2 backups são armazenados o tempo todo. Se os dados de saudação acidentalmente descartado ou corrompido [entre em contato com o suporte do Azure](https://azure.microsoft.com/support/options/) dentro de 8 horas. 

Olá backups são feitos sem afetar o desempenho de saudação ou disponibilidade de suas operações de banco de dados. Cosmos banco de dados faz backup de saudação no plano de fundo de saudação sem consumindo os RUs provisionados ou afetar o desempenho da saudação e sem afetar a disponibilidade de saudação do banco de dados. 

Ao contrário de seus dados são armazenados no banco de dados do Cosmos, backups automáticos Olá são armazenados no serviço de armazenamento de BLOBs do Azure. carregamento de latência baixa/eficiente de saudação tooguarantee, instantâneo de saudação do backup é instância tooan carregados do armazenamento de BLOBs do Azure em Olá mesma região que a região de gravação atual Olá da sua conta de banco de dados do banco de dados do Cosmos. Para garantir a resiliência contra desastres regionais, cada instantâneo de seus dados de backup no armazenamento de BLOBs do Azure é replicado novamente por meio de região de tooanother de armazenamento com redundância geográfica (GRS). Olá diagrama a seguir mostra que todo banco de dados do Cosmos contêiner hello (com todas as três partições primárias no Oeste dos EUA, neste exemplo) é feito em uma conta de armazenamento de BLOBs do Azure remota no Oeste dos EUA e, em seguida, GRS replicados tooEast nós. 

Olá imagem a seguir ilustra a backups completos periódicos de todas as entidades de banco de dados do Cosmos no armazenamento do Azure GRS.

![Backups completos periódicos de todas as entidades do Cosmos DB no Armazenamento do Azure GRS](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>Período de retenção do backup
Conforme descrito acima, o banco de dados do Azure Cosmos usa instantâneos dos seus dados a cada quatro horas e retém os últimos dois instantâneos Olá de todas as partições por 30 dias. De acordo com nossas regulamentações de conformidade, os instantâneos são limpos após 90 dias.

Se você quiser toomaintain seus próprios instantâneos, você pode usar tooJSON opção de exportação de saudação em hello Azure Cosmos DB [ferramenta de migração de dados](import-data.md#export-to-json-file) tooschedule outros backups. 

## <a name="restoring-a-database-from-an-online-backup"></a>Restauração de um banco de dados de um backup online
Se você acidentalmente excluir seu banco de dados ou uma coleção, você pode [um tíquete de suporte de arquivo](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ou [ligar para o suporte do Azure](https://azure.microsoft.com/support/options/) toorestore dados de saudação do último backup automático de saudação. Se você precisar toorestore seu banco de dados devido a problema de corrupção de dados, consulte [tratamento corrupção de dados](#handling-data-corruption) precisar tootake adicional etapas tooprevent Olá corrompido dados de backups de penetração hello. Para obter um instantâneo específico do seu toobe backup restaurado, Cosmos DB requer dados saudação estavam disponíveis para a duração de saudação do ciclo de backup Olá para esse instantâneo.

## <a name="handling-data-corruption"></a>Manipulação de dados corrompidos
Banco de dados do Azure Cosmos retém backups de dois últimos de saudação de todas as partições no sistema de saudação. Esse modelo funciona muito bem quando um contêiner (coleção de documentos, gráfico, tabela) ou um banco de dados forem excluído acidentalmente desde que uma das versões do último Olá pode ser restaurada. No entanto, em hello quando quando os usuários podem apresentar um problema de corrupção de dados, o banco de dados do Azure Cosmos pode não estar ciente Olá corrupção de dados, e é possível que o hello corrupção pode entram backups hello. Assim que estiver corrompido, você deve excluir o contêiner Olá corrompido (coleção/gráfico/tabela) para que os backups sejam protegidos sejam substituídos com dados corrompidos. Desde o último backup de saudação pode ser antiga de quatro horas, o usuário Olá pode empregar [alterar feed](change-feed.md) toocapture e repositório Olá últimas quatro horas vale a pena de dados antes de excluir o contêiner de saudação.

## <a name="next-steps"></a>Próximas etapas

tooreplicate seu banco de dados em vários data centers, consulte [distribuir os dados global com o banco de dados do Cosmos](distribute-data-globally.md). 

toofile entre em contato com o suporte do Azure, [emitir um ticket de saudação do portal Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

