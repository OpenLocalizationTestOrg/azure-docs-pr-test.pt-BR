---
title: "aaaSQL (PaaS) vs do banco de dados. SQL Server na nuvem de saudação em máquinas virtuais (IaaS) | Microsoft Docs"
description: "Saiba quais nuvem do SQL Server opção se ajusta ao seu aplicativo: banco de dados do SQL Azure (PaaS) ou o SQL Server na nuvem de saudação em máquinas virtuais do Azure."
services: sql-database, virtual-machines
keywords: Nuvem de nuvem do SQL Server, SQL Server na nuvem hello, banco de dados de PaaS, SQL Server, DBaaS
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cjgronlund
ms.assetid: 7467f422-b77d-4b60-9cb5-0f1ec17ec565
ms.service: sql-database
ms.custom: DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: carlrab
ms.openlocfilehash: 1b462a9a822d04dc5deb8422ed505a5d09279253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-cloud-sql-server-option-azure-sql-paas-database-or-sql-server-on-azure-vms-iaas"></a>Escolher uma opção do SQL Server de nuvem: Banco de Dados do SQL Azure (PaaS) ou SQL Server em VMs do Azure (IaaS)
O Azure tem duas opções para hospedar cargas de trabalho do SQL Server no Microsoft Azure:

* [Banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/): nuvem de toohello nativo do SQL de um banco de dados, também conhecido como uma plataforma como um banco de dados de serviço (PaaS) ou um banco de dados como um serviço (DBaaS) que é otimizado para desenvolvimento de aplicativos do software como serviço (SaaS). Ele oferece compatibilidade com a maioria dos recursos do SQL Server. Para obter mais informações sobre o PaaS, consulte [O que é PaaS](https://azure.microsoft.com/overview/what-is-paas/).
* [SQL Server em máquinas virtuais Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/): SQL Server instalado e hospedados na nuvem Olá no Windows Server máquinas virtuais () em execução no Azure, também conhecido como uma infraestrutura como serviço (IaaS).
  O SQL Server nas máquinas virtuais do Azure é otimizado para migrar os aplicativos existentes do SQL Server. Todos os Olá versões e edições do SQL Server estão disponíveis. Ele oferece compatibilidade de 100% com o SQL Server, permitindo que você toohost como muitos bancos de dados como transações de bancos de dados necessárias e em execução. Ele oferece total controle sobre o SQL Server e o Windows.

Saiba como cada opção se adapta a plataforma de dados do Microsoft hello e obter ajuda correspondente Olá opção direita tooyour requisitos de negócios. Se você priorizar economias de custo ou administração mínima à frente de tudo, este artigo pode ajudá-lo a decidir qual abordagem cumpre os requisitos de negócios hello mais importantes para você.

## <a name="microsofts-data-platform"></a>Plataforma de dados da Microsoft
Uma saudação primeiro coisas toounderstand qualquer discussão do Azure versus bancos de dados local do SQL Server é que você pode usar tudo. A Plataforma de Dados da Microsoft aproveita a tecnologia do SQL Server e o torna disponível em computadores locais físicos, ambientes de nuvem privada, ambientes de nuvem privada hospedados por terceiros e nuvem pública. SQL Server em máquinas virtuais do Azure permite que você toomeet exclusivos e diferentes necessidades por meio de uma combinação de local e implantações hospedados em nuvem, enquanto usando Olá o mesmo conjunto de produtos de servidor, ferramentas de desenvolvimento e experiência entre eles ambientes.

   ![Nuvem opções do SQL Server: SQL server no IaaS ou SaaS SQL de banco de dados na nuvem hello.](./media/sql-database-paas-vs-sql-server-iaas/SQLIAAS_SQL_Server_Cloud_Continuum.png)

Conforme visto no diagrama hello, cada oferta pode ser caracterizada por nível de saudação de administração, que você tem sobre infra-estrutura de saudação (no eixo X da saudação) e pelo grau de saudação de economia obtida com a consolidação de nível de banco de dados e automação (no eixo Y da saudação).

Ao criar um aplicativo, quatro opções básicas estão disponíveis para hospedar a parte do SQL Server de saudação do aplicativo hello:

* SQL Server em computadores físicos não virtualizados
* SQL Server em computadores virtualizados locais (nuvem privada)
* SQL Server na Máquina Virtual do Azure (nuvem pública da Microsoft)
* Banco de Dados SQL do Azure (nuvem pública da Microsoft)

Olá seções a seguir, você aprenderá sobre o SQL Server no hello nuvem pública da Microsoft: banco de dados do SQL Azure e SQL Server em máquinas virtuais do Azure. Além disso, irá explorar os motivadores comerciais comuns para determinar qual opção funciona melhor para seu aplicativo.

## <a name="a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms"></a>Uma análise mais aprofundada do Banco de Dados SQL do Azure e do SQL Server em VMs do Azure
**Banco de dados do SQL Azure** é um relacional banco de dados-como um serviço (DBaaS) hospedado no hello nuvem do Azure que se enquadra em categorias de setor de saudação do *Software-como um serviço (SaaS)* e *plataforma como serviço (PaaS)* . [banco de dados SQL](sql-database-technical-overview.md) baseia-se no hardware e software padronizados da Microsoft, hospedados e mantidos por ela. Com o banco de dados SQL, você pode desenvolver diretamente no serviço hello usando a funcionalidade e recursos internos. Ao usar o banco de dados SQL, você pré-pago com opções tooscale ou de maior capacidade sem interrupção.

**SQL Server em máquinas virtuais do Azure (VMs)** se enquadra em categoria do setor Olá *infraestrutura-como-um-serviço (IaaS)* e permite que você toorun do SQL Server em uma máquina virtual na nuvem hello. TooSQL semelhante banco de dados, ele é criado no hardware padronizado que é de propriedade, hospedado e mantido pela Microsoft. Ao usar o SQL Server em uma VM, você pode pagar previamente por uma licença do SQL Server já incluída em uma imagem do SQL Server ou usar facilmente uma licença existente. Você também pode facilmente escala-up/down e pausar ou retomar Olá VM conforme necessário.

Em geral, essas duas opções de SQL são otimizadas para finalidades diferentes:

* **Banco de dados do SQL Azure** é otimizada tooreduce os custos gerais toohello mínimo para provisionar e gerenciar vários bancos de dados. Isso reduz os custos de administração em andamento porque você não tem toomanage quaisquer máquinas virtuais, o sistema operacional ou o software de banco de dados. Você não tem atualizações toomanage, alta disponibilidade, ou [backups](sql-database-automated-backups.md). Em geral, o banco de dados do Azure SQL podem aumentar significativamente o número de saudação de bancos de dados gerenciados por um único IT ou recursos de desenvolvimento.
* **SQL Server em execução em VMs do Azure** é otimizado para migrar existente tooAzure aplicativos ou estender locais existentes de nuvem de toohello aplicativos em implantações híbridas. Além disso, você pode usar o SQL Server em uma máquina virtual toodevelop e testar aplicativos tradicionais do SQL Server. Com o SQL Server em VMs do Azure, você tem direitos administrativos completos Olá sobre uma instância dedicada do SQL Server e uma VM com base em nuvem. É uma opção ideal quando uma organização já tem máquinas virtuais de TI recursos disponíveis toomaintain hello. Esses recursos permitem que você toobuild tooaddress um sistema altamente personalizados específicos de desempenho e os requisitos de disponibilidade do seu aplicativo.

Olá a tabela a seguir resume as principais características de saudação do banco de dados SQL e SQL Server em VMs do Azure:

| **Mais adequado para:** | **Banco de Dados SQL do Azure** | **SQL Server em uma Máquina Virtual do Azure** |
| --- | --- | --- |
|  |Novos aplicativos baseados em nuvem que têm restrições de tempo no desenvolvimento e marketing. |Aplicativos existentes que exigem a nuvem de toohello migração rápida com alterações mínimas. Desenvolvimento e teste cenários rápido quando você não deseja que o hardware do toobuy local não seja de produção do SQL Server. |
|  | Equipes que precisam de atualização, a recuperação de desastres e alta disponibilidade interna para o banco de dados de saudação. |Equipes que podem configurar e gerenciar a alta disponibilidade, recuperação de desastres e aplicação de patch para o SQL Server. Alguns recursos automatizados fornecidos simplificam muito isso. | |
|  | Equipes que não deseja que o sistema operacional subjacente no hello toomanage e definições de configuração. |Você precisa de um ambiente personalizado com direitos administrativos completos. | |
|  | Bancos de dados de até too4 TB ou bancos de dados maiores que podem ser [horizontalmente ou verticalmente particionado](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling) usando um padrão de expansão. |Instâncias de SQL Server com até too64 TB de armazenamento. instância de saudação pode oferecer suporte a quantos bancos de dados conforme necessário. | |
|  | [Compilar aplicativos SaaS (Software como Serviço)](sql-database-design-patterns-multi-tenancy-saas-applications.md). |Migrar e compilar aplicativos híbridos e corporativos. | |
|  | | |
| **Recursos:** |Você não quiser tooemploy IT recursos de configuração e gerenciamento de saudação subjacente de infraestrutura, mas deseja toofocus na camada de aplicativo hello. |Você tem alguns recursos de TI para a configuração e o gerenciamento. Alguns recursos automatizados fornecidos simplificam muito isso. |
| **Custo total de propriedade:** |Elimina os custos de hardware e reduz os custos administrativos. |Elimina os custos de hardware. |
| **Continuidade dos negócios:** |Recursos de infraestrutura de tolerância de falhas toobuilt em adição, banco de dados do SQL Azure fornece recursos, como [backups automatizados](sql-database-automated-backups.md), [restauraçãoPoint-In-Time](sql-database-recovery-using-backups.md#point-in-time-restore), [arestauraçãogeográfica](sql-database-recovery-using-backups.md#geo-restore), e [replicação geográfica ativa](sql-database-geo-replication-overview.md) tooincrease continuidade de negócios. Para saber mais, confira a [Visão geral da continuidade de negócios do Banco de Dados SQL](sql-database-business-continuity.md). |O SQL Server nas VMs do Azure permite que você configure uma solução de alta disponibilidade e recuperação de desastres para as necessidades específicas de seu banco de dados. Portanto, você pode ter um sistema altamente otimizado para seu aplicativo. Você pode testar e executar failovers por conta própria, quando necessário. Para saber mais, consulte [Alta disponibilidade e recuperação de desastre para o SQL Server em máquinas virtuais do Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md). |
| **Nuvem híbrida:** |Seu aplicativo local pode acessar dados no Banco de Dados SQL do Azure. |Com o SQL Server em VMs do Azure, você pode ter aplicativos que executam parcialmente na nuvem hello e parcialmente no local. Por exemplo, você pode estender sua rede local e a nuvem de toohello de domínio do Active Directory por meio de [rede Virtual do Azure](../virtual-network/virtual-networks-overview.md). Além disso, você pode armazenar arquivos de dados locais no Armazenamento do Azure usando os [Arquivos de Dados do SQL Server no Azure](http://msdn.microsoft.com/library/dn385720.aspx). Para obter mais informações, consulte [tooSQL Introdução nuvem híbrida do Server 2014](http://msdn.microsoft.com/library/dn606154.aspx). |
|  | Dá suporte a [replicação transacional do SQL Server](https://msdn.microsoft.com/library/mt589530.aspx) como um tooreplicate de dados do assinante. |Dá suporte total ao [replicação transacional do SQL Server](https://msdn.microsoft.com/library/mt589530.aspx), [grupos de disponibilidade do AlwaysOn](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md), Integration Services e o envio de logs tooreplicate dados. Além disso, os backups tradicionais do SQL Server são totalmente suportados | |
|  | | |

## <a name="business-motivations-for-choosing-azure-sql-database-or-sql-server-on-azure-vms"></a>Motivações de negócios para escolher o Banco de Dados SQL do Azure ou o SQL Server em VMs do Azure
### <a name="cost"></a>Custo
Se você está uma inicialização que está com poucos em dinheiro, ou uma equipe de uma empresa estabelecida que opera com orçamento restrições, limitadas financiamento geralmente é driver primário Olá ao decidir como toohost seus bancos de dados. Nesta seção, você aprenderá sobre cobrança hello e licenciamento Noções básicas no Azure com considera as duas opções de banco de dados relacional toothese: banco de dados SQL e SQL Server em máquinas virtuais do Azure. Você também aprenderá sobre como calcular o custo total do aplicativo de hello.

#### <a name="billing-and-licensing-basics"></a>Noções básicas de licenciamento e cobrança
**Banco de dados SQL** vendido toocustomers como um serviço, não com uma licença.  [SQL Server nas VMs do Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md) é vendido com uma licença incluída que você paga por minuto. Se você tiver uma licença existente, também poderá usá-la.  

Atualmente, **banco de dados SQL** está disponível em várias camadas de serviço, que são cobradas por hora a uma taxa fixa com base em produtos de nível de desempenho e da camada de serviço Olá você escolher. Além disso, você será cobrado pelo tráfego de Internet de saída a [taxas de transferência de dados](https://azure.microsoft.com/pricing/details/data-transfers/)regulares. Olá Basic, Standard e Premium e serviço Premium RS camadas são projetados toodeliver um desempenho previsível com vários toomatch níveis de desempenho requisitos de pico do seu aplicativo. Você pode alterar entre as camadas de serviço e toomatch de níveis de desempenho que taxa de transferência variadas do seu aplicativo precisa. Se seu banco de dados tem alta toosupport transacional de volume e necessidades de muitos usuários simultâneos, recomendamos a camada de serviço Premium Olá. Para obter informações mais recentes do hello nas camadas de serviço Olá atual com suporte, consulte [camadas de serviço de banco de dados SQL do Azure](sql-database-service-tiers.md). Você também pode criar [pools Elásticos](sql-database-elastic-pool.md) tooshare recursos de desempenho entre instâncias de banco de dados.

Com **banco de dados SQL**, software de banco de dados de saudação é automaticamente configurado, corrigido e atualizado pela Microsoft, o que reduz os custos de administração. Além disso, seus recursos de [backup interno](sql-database-automated-backups.md) o ajudam a obter economia significativa, principalmente quando você tem um grande número de bancos de dados.

Com **do SQL Server em máquinas virtuais do Azure**, você pode usar qualquer um dos Olá fornecida pela plataforma imagens do SQL Server (que inclui uma licença) ou colocar sua licença do SQL Server. Olá todas as versões do SQL Server (2008R2, 2012, 2014, 2016) e edições (Developer, Express, Web, Standard, Enterprise) estão disponíveis. Além disso, versões de trazer seu-proprietário-licença (BYOL) de imagens de saudação estão disponíveis. Ao usar o hello que Azure fornecido imagens, custo operacional Olá depende de tamanho da VM hello e edição de saudação do SQL Server que você escolher. Independentemente do tamanho da VM ou edição do SQL Server, você paga o custo de licenciamento por minuto do SQL Server e Windows Server, juntamente com hello custo de armazenamento do Azure para discos de VM hello. opção de cobrança do Hello por minuto permite toouse do SQL Server para desde que você precisa sem adquirir licenças do SQL Server de adição. Se você colocar sua própria tooAzure de licença do SQL Server, você é cobrado para Windows Server e apenas os custos de armazenamento. Para obter mais informações sobre como utilizar seu próprio licenciamento, consulte [Mobilidade de Licenças por meio do Software Assurance no Azure](https://azure.microsoft.com/pricing/license-mobility/).

#### <a name="calculating-hello-total-application-cost"></a>Calcular custo total do aplicativo de saudação
Quando você começar a usar uma plataforma de nuvem, o custo de saudação de execução do aplicativo inclui desenvolvimento hello e os custos de administração, além de custos de serviço de plataforma de nuvem pública hello.

Aqui está o hello cálculo de custos detalhadas para seu aplicativo em execução no banco de dados SQL e SQL Server em VMs do Azure:

**Ao usar o Banco de Dados SQL do Azure:**

*Custo total do aplicativo = custos administrativos altamente minimizados + custos de desenvolvimento de software + custos de serviço do Banco de Dados SQL*

**Ao usar o SQL Server em VMs do Azure:**

*Custo total do aplicativo = Custos altamente minimizados de desenvolvimento do software + custos de administração + custos de licenciamento do SQL Server e do Windows Server + custos do Armazenamento do Azure*

Para obter mais informações sobre preços, consulte Olá recursos a seguir:

* [Preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/)
* [Preços de Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/) para [SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#sql) e [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#windows)
* [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/)

> [!NOTE]
> Há um pequeno subconjunto de recursos no SQL Server que não são aplicáveis ou não estão disponíveis com o Banco de Dados SQL. Consulte [Recursos do Banco de Dados SQL](sql-database-features.md) e [Informações de Transact-SQL do Banco de Dados SQL](sql-database-transact-sql-information.md) para obter mais informações. Se você estiver movendo uma nuvem de toohello de solução existente do SQL Server, consulte [migrando um banco de dados de SQL Server tooAzure banco de dados SQL](sql-database-cloud-migrate.md). Quando você migra um aplicativo SQL Server local existente tooSQL banco de dados, considere atualizar Olá aplicativo tootake aproveitar recursos de saudação que oferecem serviços de nuvem. Por exemplo, você pode considerar o uso [do serviço de aplicativo Web do Azure](https://azure.microsoft.com/services/app-service/web/) ou [serviços de nuvem do Azure](https://azure.microsoft.com/services/cloud-services/) toohost benefícios de custos do seu tooincrease de camada de aplicativo.
> 
> 

### <a name="administration"></a>Administração
Para muitas empresas, o serviço de nuvem do hello decisão tootransition tooa é como muito sobre descarregamento de complexidade de administração como custo. Com **banco de dados SQL**, Microsoft administra Olá hardware subjacente. Microsoft automaticamente replica todos os dados tooprovide alta disponibilidade, configura e atualiza o software de banco de dados hello, gerencia o balanceamento de carga e faz failover transparente, se houver uma falha de servidor. Você pode continuar tooadminister seu banco de dados, mas você não precisa mais toomanage Olá database engine, sistema operacional ou hardware.  Exemplos de itens que você pode continuar tooadminister incluem bancos de dados e logons, índice e ajuste de consulta e auditoria e segurança.

Com **do SQL Server em máquinas virtuais do Azure**, você tem controle total sobre o sistema operacional de saudação e configuração da instância do SQL Server. Com uma VM, cabe tooyou toodecide quando tooupdate/atualização Olá software de banco de dados e do sistema operacional e ao tooinstall qualquer software adicional, como software antivírus. Alguns recursos automatizados são fornecidas toodramatically simplificar a aplicação de patch, backup e alta disponibilidade. Além disso, você pode controlar o tamanho de saudação do hello VM, número de saudação de discos e das configurações de armazenamento. O Azure permite toochange tamanho de saudação de uma VM conforme necessário. Para obter informações, consulte [Tamanhos de Máquinas Virtuais e Serviço de Nuvem do Azure](../virtual-machines/windows/sizes.md). 

### <a name="service-level-agreement-sla"></a>Contrato de nível de serviço (SLA)
Para vários departamentos de TI, atender às obrigações de tempo de atividade de um SLA (Contrato de Nível de Serviço) é uma grande prioridade. Nesta seção, vamos examinar se aplica SLA tooeach bancos de dados de opção.

Para as camadas de serviço Básico, Standard, Premium e Premium RS do **Banco de Dados SQL**, a Microsoft fornece um SLA com 99,99% de disponibilidade. Para obter informações mais recentes do hello, consulte [contrato de nível de serviço](https://azure.microsoft.com/support/legal/sla/sql-database/). Para obter informações mais recentes do hello em camadas de serviço do banco de dados SQL e planos de continuidade de negócios Olá com suporte, consulte [camadas de serviço](sql-database-service-tiers.md).

Para **SQL Server em execução em VMs do Azure**, a Microsoft fornece um SLA de 99,95% de disponibilidade que abrange Olá apenas a máquina Virtual. Este SLA não abrange processos hello (como o SQL Server) em execução no hello VM e requer que você hospede pelo menos duas instâncias VM em um conjunto de disponibilidade. Para obter informações mais recentes do hello, consulte Olá [SLA de VM](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Para o banco de dados alta disponibilidade (HA) em máquinas virtuais, você deve configurar uma das opções de alta disponibilidade Olá com suporte no SQL Server, como [grupos de disponibilidade do AlwaysOn](http://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx). Usando a opção de alta disponibilidade com suporte não fornecem um SLA adicional, mas permite que você tooachieve > 99,99% de disponibilidade de banco de dados.

### <a name="market"></a>Tempo toomarket
**Banco de dados SQL** é Olá melhor solução para aplicativos de nuvem criados quando a produtividade do desenvolvedor e tempo de entrega rápida são essenciais. Com a funcionalidade programática de DBA semelhante, é perfeito para desenvolvedores e arquitetos de nuvem como ela reduz a necessidade de saudação de gerenciamento de banco de dados e sistema operacional subjacente de saudação. Por exemplo, você pode usar o hello [API REST](http://msdn.microsoft.com/library/azure/dn505719.aspx) e [Cmdlets do PowerShell](http://msdn.microsoft.com/library/mt740629.aspx) tooautomate e gerenciar as operações administrativas para milhares de bancos de dados. Recursos como [pools Elásticos](sql-database-elastic-pool.md) permitem toofocus na camada de aplicativo hello e entregar seu mercado de toohello solução mais rápida.

**SQL Server em execução em VMs do Azure** é perfeito se seus aplicativos novos ou existentes exigem grandes bancos de dados, bancos de dados relacionados, ou acessar recursos tooall no SQL Server ou do Windows. Também é uma boa opção quando desejar toomigrate existente tooAzure aplicativos e bancos de dados como local-é. Como camadas de dados, aplicativo e apresentação de saudação toochange não é necessário, você economiza tempo e dinheiro em rearchitecting sua solução existente. Em vez disso, você pode se concentrar na migração de todos os seu tooAzure de soluções e algumas otimizações de desempenho que podem ser exigidas por Olá plataforma Windows Azure. Para obter mais informações, veja [Práticas Recomendadas de Desempenho para o SQL Server em Máquinas Virtuais do Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md).

## <a name="summary"></a>Resumo
Este artigo explorou o Banco de Dados SQL e o SQL Server em VMs (Máquinas Virtuais) do Azure e discutiu motivadores comerciais comuns que podem afetar sua decisão. a seguir Olá é um resumo de sugestões para você tooconsider:

Escolha o **Banco de Dados SQL do Azure** se:

* São criando aplicativos de baseado em nuvem novo fornecer tootake aproveitar Olá custo economia e otimização de desempenho que os serviços de nuvem. Essa abordagem oferece benefícios de saudação de um serviço de nuvem totalmente gerenciado, ajuda a inferior inicial tempo de entrega e pode fornecer a otimização de custo de longo prazo.
* Você deseja toohave Microsoft executar operações comuns de gerenciamento em seus bancos de dados e exigem mais forte disponibilidade SLAs para bancos de dados.

Escolha **SQL Server em VMs do Azure** se:

* Você tem aplicativos locais existentes que você deseja toomigrate ou estende a nuvem toohello, ou se você quiser aplicativos corporativos de toobuild maiores que 4 TB. Essa abordagem oferece o benefício de saudação do SQL compatibilidade de 100%, capacidade de banco de dados grande, controle total sobre o SQL Server e o Windows e o local tooon encapsulamento seguro. A abordagem reduz os custos de desenvolvimento e modificações dos aplicativos existentes.
* Você tem recursos de TI existentes e pode ter basicamente patches, backups e alta disponibilidade do banco de dados. Observe que alguns recursos automatizados simplificam muito essas operações. 

## <a name="next-steps"></a>Próximas etapas
* Consulte [seu banco de dados do SQL Azure primeiro](sql-database-get-started-portal.md) tooget iniciado com o banco de dados SQL.
* Confira [Preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/).
* Consulte [provisionar uma máquina de virtual do SQL Server no Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md) tooget iniciado com o SQL Server em VMs do Azure.

