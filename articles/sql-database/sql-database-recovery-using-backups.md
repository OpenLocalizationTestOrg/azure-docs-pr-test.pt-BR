---
title: um banco de dados do SQL Azure de um backup de aaaRestore | Microsoft Docs
description: "Saiba mais sobre restauração Point-in-Time, que permite voltar tooroll um ponto anterior do banco de dados do Azure SQL tooa no tempo (backup too35 dias)."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>Recuperar um banco de dados SQL do Azure usando backups de banco de dados automatizados
O Banco de Dados SQL fornece essas opções para recuperação de banco de dados usando [backups automáticos de banco de dados](sql-database-automated-backups.md) e [backups de retenção de longo prazo](sql-database-long-term-retention.md). Você pode restaurar de um backup de banco de dados para:

* Um novo banco de dados Olá recuperado do mesmo servidor lógico tooa especificado ponto no tempo dentro do período de retenção de saudação. 
* Um banco de dados Olá mesmo servidor lógico recuperado toohello tempo de exclusão para um banco de dados excluído.
* Um novo banco de dados em qualquer servidor lógico em qualquer região recuperado ponto toohello de backups diários mais recentes do hello no armazenamento de blob de replicação geográfica (RA-GRS).

> [!IMPORTANT]
> Não é possível substituir um banco de dados existente durante a restauração.
>

Você também pode usar [automatizada de backups de banco de dados](sql-database-automated-backups.md) toocreate um [cópia de banco de dados](sql-database-copy.md) em qualquer servidor lógico em qualquer região. 

## <a name="recovery-time"></a>Tempo de recuperação
Olá toorestore de tempo de recuperação, um banco de dados usando backups de banco de dados automatizada é afetado por vários fatores: 

* tamanho de saudação do banco de dados de saudação
* nível de desempenho de saudação do banco de dados de saudação
* número de saudação dos logs de transação envolvidos
* Olá quantidade de atividades que precisa toobe reproduzidos ponto de restauração toohello toorecover
* largura de banda de rede Olá se Olá restaurar é tooa uma região diferente 
* número de saudação de solicitações de restauração simultâneos estão sendo processadas na região de destino de saudação. 
  
  Para um banco de dados muito grande e ativo, a restauração de saudação pode levar várias horas. Caso haja uma interrupção prolongada em uma região, é possível que haja muitas solicitações de restauração geográfica sendo processadas por outras regiões. Quando há muitas solicitações, o tempo de recuperação de saudação pode aumentar para bancos de dados nessa região. A maioria das restaurações de banco de dados é concluída em 12 horas.
  
Não há nenhuma restauração de massa toodo funcionalidade interna. Olá [banco de dados do SQL Azure: recuperação de servidor completo](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) script é um exemplo de uma maneira de realizar essa tarefa.

> [!IMPORTANT]
> toorecover usando backups automáticos, você deve ser um membro da função de Colaborador do SQL Server Olá na assinatura de saudação ou ser o proprietário da assinatura hello. Você pode recuperar usando Olá portal do Azure, PowerShell ou Olá API REST. Você não pode usar o Transact-SQL. 
> 

## <a name="point-in-time-restore"></a>Restauração pontual

Você pode restaurar um banco de dados tooan anteriormente ponto no tempo como um novo banco de dados Olá mesmo servidor lógico usando Olá portal do Azure, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), ou hello [API REST](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Para um script do PowerShell de exemplo mostrando como tooperform uma restauração point-in-time de um banco de dados, consulte [restaurar um banco de dados SQL usando o PowerShell](scripts/sql-database-restore-database-powershell.md).
>

banco de dados de saudação pode ser restaurado tooany camada de serviço ou desempenho nível e como um único banco de dados ou em um pool Elástico. Certifique-se de ter recursos suficientes no servidor lógico hello ou em Olá pool Elástico toowhich você está restaurando banco de dados de saudação. Uma vez concluído, o banco de dados de saudação restaurado é um banco de dados normal, totalmente acessível on-line. banco de dados restaurado de saudação é cobrado a taxas normais com base em seu nível de desempenho e da camada de serviço. Você não incorrer em encargos até que a restauração de banco de dados de saudação for concluída.

Restaurar um banco de dados tooan geralmente anteriormente aponte para fins de recuperação. Ao fazer isso, você pode tratar hello restaurou o banco de dados como uma substituição para o banco de dados original hello ou usá-lo tooretrieve dados do e, em seguida, atualizar o banco de dados original hello. 

* ***Substituição de banco de dados:*** se o banco de dados restaurado de saudação destina-se como um substituto para o banco de dados original hello, você deve verificar o nível de desempenho hello e/ou camada de serviço são apropriada e dimensionar o banco de dados de saudação se necessário. Você pode renomear o banco de dados original hello e, em seguida, nomeie Olá restaurado banco de dados Olá original usando o comando ALTER DATABASE de saudação em T-SQL. 
* ***Recuperação de dados:*** se você planejar tooretrieve dados Olá restaurado toorecover de banco de dados de um erro de usuário ou aplicativo, você precisa toowrite e executar Olá necessário recuperação scripts tooextract dados de saudação restaurada toohello de banco de dados o banco de dados original. Embora a operação de restauração Olá pode levar um longo tempo toocomplete, Olá restaurar banco de dados estiver visível na lista de banco de dados de saudação em todo o processo de restauração de saudação. Se você excluir o banco de dados de saudação durante a restauração de hello, Olá a operação de restauração é cancelada e não será cobrado para banco de dados de saudação que não concluíram o processo de restauração de saudação. 

### <a name="azure-portal"></a>Portal do Azure

toorecover tooa ponto no tempo usando Olá portal do Azure, a página aberta Olá para o banco de dados e clique em **restaurar** na barra de ferramentas de saudação.

![restauração pontual](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a>Restauração de banco de dados excluído
Você pode restaurar um tempo de toohello excluído do banco de dados para um banco de dados excluído hello usando o mesmo servidor lógico Olá portal do Azure, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), ou hello [REST (createMode = restaurar)](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Para obter um exemplo do PowerShell script mostrando como toorestore um banco de dados excluído, consulte [restaurar um banco de dados SQL usando o PowerShell](scripts/sql-database-restore-database-powershell.md).
>

> [!IMPORTANT]
> Se você excluir uma instância de servidor de Banco de Dados SQL do Azure, todos os seus bancos de dados também serão excluídos e não poderão ser recuperados. No momento, não há suporte para restaurar um servidor excluído.
> 

### <a name="azure-portal"></a>Portal do Azure

toorecover excluído do banco de dados durante sua [período de retenção](sql-database-service-tiers.md) usando Olá portal do Azure, página Olá aberta para o servidor e na área de operações hello, clique em **bancos de dados excluídos**.

![deleted-database-restore-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![deleted-database-restore-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a>Restauração geográfica
Você pode restaurar um banco de dados SQL em qualquer servidor em qualquer região do Azure de hello mais recente replicado geograficamente backups completos e diferenciais. Restauração geográfica usa um backup com redundância geográfica como sua fonte e pode ser toorecover usado um banco de dados mesmo se o banco de dados de saudação ou datacenter estiver inacessível devido a interrupção tooan. 

A restauração geográfica é a opção de recuperação de padrão de saudação quando seu banco de dados não está disponível devido a um incidente na região Olá onde o banco de dados de saudação está hospedado. Se um incidente de grande escala nos resultados de uma região em indisponibilidade do seu aplicativo de banco de dados, você pode restaurar um banco de dados do servidor de tooa Olá backups replicados geograficamente em qualquer outra região. Há um atraso entre quando um backup diferencial é obtido e quando for replicada geograficamente tooan Azure blob em uma região diferente. Esse atraso pode ser a hora de tooan, portanto, se ocorrer um desastre, pode haver a perda de dados de hora tooone. Olá ilustração a seguir mostra a restauração do banco de dados de saudação do último backup disponível Olá em outra região.

![Restauração geográfica](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> Para obter um exemplo do PowerShell script mostrando como tooperform uma restauração geográfica, consulte [restaurar um banco de dados SQL usando o PowerShell](scripts/sql-database-restore-database-powershell.md).
> 

Atualmente, não há suporte para a restauração pontual em uma área geográfica secundária. A restauração pontual pode ser feita somente em um banco de dados primário. Para obter informações detalhadas sobre como usar a restauração geográfica toorecover de uma interrupção, consulte [recuperar de uma paralisação](sql-database-disaster-recovery.md).

> [!IMPORTANT]
> Recuperação de backups é hello mais básico do desastre Olá soluções de recuperação disponíveis no banco de dados SQL com hello RPO mais longo e tempo de recuperação estimado (ERTER). Para soluções que usam os bancos de dados básicos, a restauração geográfica é uma solução frequentemente razoável de recuperação de desastres com um ERT de 12 horas. Para soluções que usam bancos de dados Standard ou Premium maiores que exigem tempos de recuperação menores, você deve considerar o uso da [replicação geográfica ativa](sql-database-geo-replication-overview.md). Replicação geográfica oferece um RPO bem menor e a ERTER conforme ele exige somente que você iniciar um secundário de tooa é continuamente replicada de failover. Para obter mais informações sobre as opções de continuidade dos negócios, consulte [Recuperação da continuidade de negócios](sql-database-business-continuity.md).
> 

### <a name="azure-portal"></a>Portal do Azure

um banco de dados durante a restauração toogeo seu [período de retenção](sql-database-service-tiers.md) usando Olá portal do Azure, abra a página de bancos de dados SQL hello e, em seguida, clique em **adicionar**. Em Olá **Selecione origem** caixa de texto, selecione **Backup**. Especifica o backup de saudação da recuperação de saudação que tooperform na região hello e no servidor de saudação de sua escolha. 

## <a name="programmatically-performing-recovery-using-automated-backups"></a>Executar recuperação programaticamente usando backups automatizados
Como discutido anteriormente, além de toohello portal do Azure, a recuperação de banco de dados pode ser executada programaticamente usando o Azure PowerShell ou Olá API REST. Olá tabelas seguintes descreve o conjunto de saudação de comandos disponíveis.

### <a name="powershell"></a>PowerShell
| Cmdlet | Descrição |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Obtém um ou mais bancos de dados. |
| [Get-AzureRMSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | Obtém um banco de dados excluído que você pode restaurar. |
| [Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |Obtém um backup com redundância geográfica de um banco de dados. |
| [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |Restaura um banco de dados SQL. |
|  | |

### <a name="rest-api"></a>API REST
| API | Descrição |
| --- | --- |
| [REST (createMode=Recovery)](https://msdn.microsoft.com/library/azure/mt163685.aspx) |Restaura um banco de dados |
| [Obter, Criar ou Atualizar o Status de um Banco de Dados](https://msdn.microsoft.com/library/azure/mt643934.aspx) |Retorna o status de saudação durante uma operação de restauração |
|  | |

## <a name="summary"></a>Resumo
Backups automáticos protegem seus bancos de dados contra erros de usuário e de aplicativo, exclusão acidental do banco de dados e interrupções prolongadas. Essa funcionalidade interna está disponível para todas as camadas de serviço e níveis de desempenho. 

## <a name="next-steps"></a>Próximas etapas
* Para obter uma visão geral e os cenários de continuidade dos negócios, confira [Visão geral da continuidade dos negócios](sql-database-business-continuity.md)
* toolearn sobre backups de banco de dados do SQL Azure automatizadas, consulte [backups automatizados de banco de dados SQL](sql-database-automated-backups.md)
* toolearn sobre retenção de backup de longo prazo, consulte [retenção de backup de longo prazo](sql-database-long-term-retention.md)
* tooconfigure, gerenciem e restaurem de retenção de longo prazo de backups automáticos em um cofre de serviços de recuperação do Azure usando hello Azure portal, consulte [configurar e usar a longo prazo de retenção de backup](sql-database-long-term-backup-retention-configure.md). 
* toolearn sobre as opções de recuperação mais rápidas, consulte [replicação geográfica ativa](sql-database-geo-replication-overview.md)  
