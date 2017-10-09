---
title: Perguntas frequentes sobre o banco de dados SQL do aaaAzure | Microsoft Docs
description: "Os clientes do respostas toocommon perguntas perguntarem sobre bancos de dados de nuvem e banco de dados do SQL Azure, sistema de gerenciamento de banco de dados relacional (RDBMS) da Microsoft e banco de dados como um serviço em nuvem Olá."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 1da12abc-0646-43ba-b564-e3b049a6487f
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 02/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 04c02f96e6e91cf314221134ee0ef6d24217ef45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-faq"></a>Perguntas frequentes sobre o Banco de Dados SQL

## <a name="what-is-hello-current-version-of-sql-database"></a>O que é a versão atual de saudação do banco de dados SQL?
versão atual de saudação do banco de dados SQL é V12. Versão V11 foi desativado.

## <a name="what-is-hello-sla-for-sql-database"></a>O que é o SLA de saudação do banco de dados SQL?
Garantimos pelo menos 99,99% de clientes de tempo de saudação terá conectividade entre seu único ou Elástico Basic, Standard, ou banco de dados do Microsoft Azure SQL Premium e nosso gateway de Internet. Para saber mais, veja [SLA](http://azure.microsoft.com/support/legal/sla/).

## <a name="how-do-i-reset-hello-password-for-hello-server-admin"></a>Como redefinir senha Olá Olá administrador de servidor?
Em Olá [portal do Azure](https://portal.azure.com) clique **SQL Servers**, selecione servidor Olá Olá lista e, em seguida, clique em **Redefinir senha**.

## <a name="how-do-i-manage-databases-and-logins"></a>Como gerenciar logons e bancos de dados?
Consulte [gerenciamento de bancos de dados e logons](sql-database-manage-logins.md).

## <a name="how-do-i-make-sure-only-authorized-ip-addresses-are-allowed-tooaccess-a-server"></a>Como verificar se os endereços IP autorizados somente são permitidos tooaccess um servidor?
Confira [Como definir as configurações de firewall no Banco de Dados SQL](sql-database-configure-firewall-settings.md).

## <a name="how-does-hello-usage-of-sql-database-show-up-on-my-bill"></a>Como uso de saudação do banco de dados SQL aparece na minha fatura?
Listas de banco de dados SQL em uma taxa horária previsível com base na camada de serviço Olá + desempenho nível para bancos de dados único ou eDTUs por pool Elástico. O uso real é calculado e rateado por hora, de modo que sua fatura poderá mostrar frações de hora. Por exemplo, se um banco de dados existir por 12 horas em um mês, sua fatura mostrará a utilização de 0,5 dia. Além disso, as camadas de serviço + o nível de desempenho e eDTUs por pool são quebrados out em Olá fatura toomake-lo mais fácil toosee Olá quantos dias de banco de dados usado para cada um em um único mês.

## <a name="what-if-a-single-database-is-active-for-less-than-an-hour-or-uses-a-higher-service-tier-for-less-than-an-hour"></a>E se um banco de dados único ficar ativo por menos de uma hora ou usar uma camada de serviço mais alta por menos de uma hora?
Você será cobrado para cada hora de que um banco de dados existe usando hello mais alto nível de serviço + desempenho nível que são aplicadas durante essa hora, independentemente do uso ou o banco de dados de saudação estava ativo para menos de uma hora. Por exemplo, se você criar um banco de dados individual e o excluir depois de cinco minutos, sua fatura apresentará uma cobrança referente a uma hora de banco de dados. 

Exemplos

* Se você criar um banco de dados básico e, em seguida, imediatamente atualizá-lo tooStandard S1, são cobradas a taxa de Standard S1 de saudação para Olá primeira hora.
* Se você atualizar um banco de dados do tooPremium básica às 10:00. e a atualização for concluída à 1h35, em Olá dia a seguir, você é cobrado na taxa de Premium Olá começando em 1:00 a.m. 
* Se você fazer o downgrade de um banco de dados Premium tooBasic às 11:00. concluído na 14:15, e banco de dados de saudação é cobrado na taxa de Premium Olá até 3:00 p.m., após o qual são cobrados em taxas básicas hello.

## <a name="how-does-elastic-pool-usage-show-up-on-my-bill-and-what-happens-when-i-change-edtus-per-pool"></a>Como o uso do pool elástico é mostrado em minha fatura e o que acontece se eu alterar as eDTUs por pool?
Pool Elástico cobra Mostrar backup na sua conta como DTUs Elástico (eDTUs) em incrementos de saudação mostrados em eDTUs por pool em [Olá página de preços](https://azure.microsoft.com/pricing/details/sql-database/). Não há cobrança por banco de dados para pools elásticos. Você será cobrado por cada hora de que um pool existe no eDTU mais alto hello, independentemente do uso ou pool Olá estava ativa para menos de uma hora. 

Exemplos

* Se você criar um pool Elástico padrão com 200 eDTUs às 11:18:00, adicionando cinco pool de toohello de bancos de dados, você é cobrado pela 200 eDTUs por hora inteira do hello, começando às 11. por meio do restante da saudação do dia de saudação.
* No dia 2, 5:05 a.m. 1 do banco de dados começa a consumir 50 eDTUs e mantém constante dia hello. Os Bancos de Dados 2 a 5 flutuam entre 0 e 80 eDTUs. Durante o dia hello, você adiciona cinco outros bancos de dados que consomem eDTUs variados durante o dia de saudação. O Dia 2 é um dia inteiro cobrado a 200 eDTUs. 
* No Dia 3, às 5h,  você adiciona mais 15 bancos de dados. Aumenta o uso do banco de dados em todo o ponto de toohello do hello dia em que você decide tooincrease eDTUs de pool de saudação de 200 too400 às 8:05 p.m. Encargos no nível de eDTU Olá 200 estavam em vigor até 8 pm e aumenta too400 eDTUs para Olá restantes de quatro horas. 

## <a name="elastic-pool-billing-and-pricing-information"></a>Informações sobre preços e cobrança do pool elástico
Pools Elásticos são cobrados por Olá características a seguir:

* Um pool Elástico é cobrado após sua criação, mesmo quando não houver nenhum banco de dados no pool de saudação.
* Um pool elástico é cobrado por hora. Isso é Olá mesmo medição frequência para níveis de desempenho de bancos de dados único.
* Se um pool Elástico é redimensionado tooa novo número de eDTUs, em seguida, pool de saudação não é cobrado toohello novo valor de eDTUS de acordo com até que Olá redimensionando a operação seja concluída. Isso segue o mesmo padrão que alterar o nível de desempenho de saudação do bancos de dados único de saudação.
* preço de saudação de um pool Elástico é baseado no número de saudação do eDTUs de pool de saudação. preço de saudação de um pool Elástico é independente do número de saudação e a utilização de bancos de dados Elástico nele Olá.
* O preço é calculado por (número de eDTUs do pool) x (preço unitário por eDTU).

eDTU preço unitário Olá um pool Elástico for maior do que Olá DTU preço unitário um único banco de dados em Olá mesma camada de serviço. Para obter detalhes, confira [Preços de Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/). 

toounderstand Olá eDTUs e serviço de camadas, consulte [opções de banco de dados SQL e desempenho](sql-database-service-tiers.md).

## <a name="how-does-hello-use-of-active-geo-replication-in-an-elastic-pool-show-up-on-my-bill"></a>Como usa os Olá de replicação geográfica ativa em um pool Elástico aparecem na minha conta?
Ao contrário dos bancos de dados únicos, o uso da [replicação geográfica ativa](sql-database-geo-replication-overview.md) com bancos de dados elásticos não tem um impacto direto no faturamento.  Você é cobrado apenas pelo eDTUs Olá provisionado para cada um dos pools de saudação (primário e secundário)

## <a name="how-does-hello-use-of-hello-auditing-feature-impact-my-bill"></a>Como Olá usa do impacto do recurso de auditoria de saudação minha fatura?
A auditoria é criada em Olá serviço de banco de dados SQL sem adicional e é tooBasic disponível, Standard, Premium e Premium RS bancos de dados. No entanto, toostore Olá logs de auditoria, Olá auditoria utilizações de recurso aplicam-se uma conta de armazenamento do Azure e taxas de tabelas e filas no armazenamento do Azure com base no tamanho de saudação de seu log de auditoria.

## <a name="how-do-i-find-hello-right-service-tier-and-performance-level-for-single-databases-and-elastic-pools"></a>Como localizar o nível de desempenho e da camada de serviço certo Olá para bancos de dados único e de pools Elásticos?
Há alguns tooyou disponíveis de ferramentas. 

* Para bancos de dados local, use Olá [Supervisor de dimensionamento de DTU](http://dtucalculator.azurewebsites.net/) toorecommend Olá DTUs necessárias e os bancos de dados e avaliar vários bancos de dados de pools elásticos.
* Se um banco de dados individual puder se beneficiar de estar em um pool, o mecanismo inteligente do Azure recomendará um pool elástico se perceber um padrão de uso histórico que garanta isso. Consulte [monitorar e gerenciar um pool Elástico com hello portal do Azure](sql-database-elastic-pool-manage-portal.md). Para obter detalhes sobre como toodo Olá matemática por conta própria, consulte [considerações de preço e desempenho para um pool Elástico](sql-database-elastic-pool.md)
* toosee se você precisa de um único banco de dados de toodial para cima ou para baixo, consulte [orientação sobre desempenho para bancos de dados único](sql-database-performance-guidance.md).

## <a name="how-often-can-i-change-hello-service-tier-or-performance-level-of-a-single-database"></a>Frequência alterar Olá serviço da camada ou nível de desempenho de um único banco de dados?
Você pode alterar a camada de serviço hello (entre Basic, Standard, Premium e Premium RS) ou Olá o nível de desempenho dentro de uma camada de serviço (por exemplo, S1 tooS2) sempre que desejar. Para bancos de dados de versão anteriores, você pode alterar nível de desempenho ou da camada de serviço de Olá um total de quatro vezes em um período de 24 horas.

## <a name="how-often-can-i-adjust-hello-edtus-per-pool"></a>Frequência ajustar Olá eDTUs por pool?
Quantas vezes desejar.

## <a name="how-long-does-it-take-toochange-hello-service-tier-or-performance-level-of-a-single-database-or-move-a-database-in-and-out-of-an-elastic-pool"></a>Quanto tempo ele levar toochange Olá serviço da camada ou nível de desempenho de um único banco de dados ou mover um banco de dados dentro e fora de um pool Elástico?
Alterar a camada de serviço de saudação de um banco de dados e mover e sair de um pool requer Olá toobe de banco de dados copiado na plataforma hello como uma operação em segundo plano. Camada de serviço Olá alteração pode levar de alguns minutos tooseveral horas dependendo do tamanho de saudação de bancos de dados de saudação. Em ambos os casos, bancos de dados Olá permanecem online e disponível durante a saudação move. Para obter detalhes sobre como alterar os bancos de dados único, consulte [camada de serviço de saudação de alteração de um banco de dados](sql-database-service-tiers.md). 

## <a name="when-should-i-use-a-single-database-vs-elastic-databases"></a>Quando eu devo usar um banco de dados únicos em vez de bancos de dados elásticos?
Em geral, os pools elásticos são projetados para um típico [padrão de aplicativo de software como serviço (SaaS)](sql-database-design-patterns-multi-tenancy-saas-applications.md), em que há um banco de dados por cliente ou locatário. Compras de bancos de dados individuais e variável de saudação toomeet excesso de provisionamento e horário de pico demandam para cada banco de dados é geralmente não econômica. Com os pools, gerenciar o desempenho coletivo de saudação do pool de saudação e bancos de dados Olá aumentar e diminuir automaticamente. O mecanismo inteligente do Azure recomendará um pool para bancos de dados quando perceber um padrão de uso que o garanta. Para obter detalhes, consulte [Diretrizes de pool elástico](sql-database-elastic-pool.md).

## <a name="what-does-it-mean-toohave-up-too200-of-your-maximum-provisioned-database-storage-for-backup-storage"></a>O que significa toohave too200% do armazenamento máximo de banco de dados provisionado para armazenamento de backup?
Armazenamento de backup é o armazenamento de saudação associado com os backups de banco de dados automatizado que são usados para [ponto-em-tempo restauração](sql-database-recovery-using-backups.md#point-in-time-restore) e [restauração geográfica](sql-database-recovery-using-backups.md#geo-restore). Banco de dados SQL do Microsoft Azure fornece o too200% de seu armazenamento de banco de dados provisionado máximo de armazenamento de backup sem custo adicional. Por exemplo, se você tiver uma instância de banco de dados Standard com tamanho provisionado de 250 GB, serão oferecidos a você 500 GB de espaço de armazenamento para backup sem custo adicional. Se seu banco de dados exceder Olá fornecido o armazenamento de backup, você pode escolher o período de retenção de saudação tooreduce entrando em contato com o suporte do Azure ou pagar Olá extra para armazenamento de backup cobrado na taxa padrão de acesso de leitura geograficamente redundantes (RA-GRS). Para saber mais sobre a cobrança de RA-GRS, consulte Detalhes de preços de armazenamento.

## <a name="im-moving-from-webbusiness-toohello-new-service-tiers-what-do-i-need-tooknow"></a>Estou migrando de Web/Business toohello novas camadas de serviço, o que eu preciso tooknow?
Os bancos de dados SQL Business e Web do Azure foram desativados. Olá camadas Basic, Standard, Premium, RS Premium e elástica substituem Olá desativar bancos de dados Web e Business. 

## <a name="what-is-an-expected-replication-lag-when-geo-replicating-a-database-between-two-regions-within-hello-same-azure-geography"></a>O que é um atraso de replicação esperado quando a replicação geográfica de um banco de dados entre duas regiões dentro de Olá mesma localização geográfica do Azure?
Estamos atualmente oferece suporte a um RPO de cinco segundos e latência de replicação Olá foi menor do que a quando Olá geo-secundário estiver hospedado em hello que Azure recomendado região emparelhada e em Olá mesma camada de serviço.

## <a name="what-is-an-expected-replication-lag-when-geo-secondary-is-created-in-hello-same-region-as-hello-primary-database"></a>O que é um atraso de replicação esperado quando geográfica secundário é criado no hello mesma região do banco de dados primário Olá?
Com base nos dados empíricos, não há muita diferença entre regiões dentro e latência de replicação entre região quando hello que Azure recomendado região emparelhada é usado. 

## <a name="if-there-is-a-network-failure-between-two-regions-how-does-hello-retry-logic-work-when-geo-replication-is-set-up"></a>Se houver uma falha de rede entre as duas regiões, como a lógica de repetição Olá funciona quando a replicação geográfica é configurada?
Se houver uma desconexão, repetido toore cada 10 segundos-estabelecer conexões.

## <a name="what-can-i-do-tooguarantee-that-a-critical-change-on-hello-primary-database-is-replicated"></a>O que fazer tooguarantee que uma alteração no banco de dados primário Olá é replicada?
Olá geo-secundário é uma réplica assíncrona e não tentaremos tookeep na sincronização completa com hello primário. Mas fornecemos um método tooforce sincronização tooensure Olá de replicação de alterações importantes (por exemplo, as atualizações de senha). Sincronização forçada afeta o desempenho porque ele bloqueia o thread de chamada hello até que todas as transações confirmadas sejam replicadas. Para obter detalhes, veja [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx). 

## <a name="what-tools-are-available-toomonitor-hello-replication-lag-between-hello-primary-database-and-geo-secondary"></a>As ferramentas que estão disponíveis toomonitor Olá atraso de replicação entre o banco de dados primário hello e replicação geográfica secundária?
Expomos Olá latência de replicação em tempo real entre o banco de dados primário hello e replicação geográfica secundária por meio de uma DMV. Para obter detalhes, veja [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx).

## <a name="toomove-a-database-tooa-different-server-in-hello-same-subscription"></a>toomove um servidor diferente do banco de dados tooa no hello mesma assinatura
* Em Olá [portal do Azure](https://portal.azure.com), clique em **bancos de dados SQL**, selecione um banco de dados na lista de saudação e, em seguida, clique em **cópia**. Para obter mais detalhes, consulte [Copiar um Banco de Dados SQL do Azure](sql-database-copy.md) .

## <a name="toomove-a-database-between-subscriptions"></a>toomove um banco de dados entre as assinaturas
* Em Olá [portal do Azure](https://portal.azure.com), clique em **servidores SQL** e selecione Olá servidor que hospeda seu banco de dados da lista de saudação. Clique em **mover**e, em seguida, selecione Olá recursos toomove e Olá toomove de assinatura para.
