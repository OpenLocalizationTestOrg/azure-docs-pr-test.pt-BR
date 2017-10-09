---
title: "segurança de banco de dados SQL para recuperação de desastres de aaaConfigure | Microsoft Docs"
description: "Este tópico explica as considerações de segurança para configurar e gerenciar a segurança após uma restauração de banco de dados ou um failover tooa o servidor secundário em caso de saudação de uma paralisação do data center ou outros desastres"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="b7e9f-103">Configurar e gerenciar a segurança do Banco de Dados SQL para restauração geográfica ou failover</span><span class="sxs-lookup"><span data-stu-id="b7e9f-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="b7e9f-104">A [Replicação geográfica ativa](sql-database-geo-replication-overview.md) agora está disponível para todos os bancos de dados em todas as camadas de serviço.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="b7e9f-105">Visão geral dos requisitos de autenticação para a recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="b7e9f-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="b7e9f-106">Este tópico descreve Olá tooconfigure de requisitos de autenticação e controle [replicação geográfica ativa](sql-database-geo-replication-overview.md) e Olá etapas necessária tooset usuário acesso toohello banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="b7e9f-107">Ele também descreve como habilitar o banco de dados do access toohello recuperados depois de usar [restauração geográfica](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="b7e9f-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="b7e9f-108">Para obter mais informações sobre as opções de recuperação, confira [Visão geral de continuidade dos negócios](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="b7e9f-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="b7e9f-109">Recuperação de desastre com usuários independentes</span><span class="sxs-lookup"><span data-stu-id="b7e9f-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="b7e9f-110">Ao contrário de usuários tradicionais, que deve ser mapeado toologins no banco de dados mestre hello, um usuário independente é totalmente gerenciado pelo Olá próprio banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="b7e9f-111">Isso oferece dois benefícios.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-111">This has two benefits.</span></span> <span data-ttu-id="b7e9f-112">No cenário de recuperação de desastres hello, os usuários de Olá podem continuar tooconnect toohello novo principal banco de dados ou Olá recuperado usando a restauração geográfica sem qualquer configuração adicional, como o banco de dados de saudação gerencia usuários hello.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="b7e9f-113">Também há possíveis benefícios de desempenho e escalabilidade com esta configuração de uma perspectiva de logon.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="b7e9f-114">Para obter mais informações, consulte [Usuários do banco de dados independente - Tornando o banco de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7e9f-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="b7e9f-115">compensação principal Olá é que é mais difícil gerenciar o processo de recuperação de desastres Olá em escala.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="b7e9f-116">Quando você tiver vários bancos de dados que Olá use mesmo logon, manter credenciais hello usando contido usuários em vários bancos de dados podem invalidar os benefícios de saudação do usuários contidos.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="b7e9f-117">Por exemplo, a política de rotação de senha Olá requer que fazer alterações consistentemente em bancos de dados de vários em vez da alteração de senha Olá para logon Olá uma vez no banco de dados mestre hello.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="b7e9f-118">Por esse motivo, se você tiver vários bancos de dados que use Olá mesmo nome de usuário e senha, não é recomendável usar usuários contidos.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="b7e9f-119">Como tooconfigure logons e usuários</span><span class="sxs-lookup"><span data-stu-id="b7e9f-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="b7e9f-120">Se você estiver usando os logons e usuários (em vez dos usuários independentes), você deve tomar tooinsure etapas adicionais que Olá existem mesmos logons no banco de dados mestre hello.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="b7e9f-121">Olá seções a seguir descrevem Olá etapas envolvidas adicionais considerações sobre e.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="b7e9f-122">Configurar usuário acesso tooa secundária ou recuperado banco de dados</span><span class="sxs-lookup"><span data-stu-id="b7e9f-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="b7e9f-123">Para toobe de banco de dados secundário Olá utilizável como um banco de dados secundário somente leitura e tooensure acesso adequado toohello novo banco de dados ou hello banco de dados primário recuperado usando a restauração geográfica, Olá mestre saudação do servidor de destino do banco de dados deve ter Olá configuração de segurança apropriadas em vigor antes da recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="b7e9f-124">permissões específicas de saudação para cada etapa são descritas posteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="b7e9f-125">Preparando tooa de acesso do usuário a replicação geográfica secundária deve ser executada como parte de configurar a replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="b7e9f-126">Preparar toohello bancos de dados restaurados de replicação geográfica de acesso do usuário deve ser executada a qualquer momento quando o servidor original hello está online (por exemplo, como parte da análise Olá DR).</span><span class="sxs-lookup"><span data-stu-id="b7e9f-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="b7e9f-127">Se você não o failover ou restauração geográfica server tooa que não tenha configurados corretamente logons, acesso tooit será limitado toohello conta de administrador de servidor.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="b7e9f-128">Configuração de logons no servidor de destino Olá envolve três etapas descritas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7e9f-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="b7e9f-129">1. Determine os logons com o banco de dados do access toohello primário:</span><span class="sxs-lookup"><span data-stu-id="b7e9f-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="b7e9f-130">Olá primeira etapa do processo de saudação é toodetermine quais logons devem ser duplicados no servidor de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="b7e9f-131">Isso é feito com um par de instruções SELECT, em Olá lógico banco de dados mestre no servidor de origem hello e no banco de dados primário do hello em si.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="b7e9f-132">Olá somente o administrador do servidor ou um membro da saudação **LoginManager** função de servidor pode determinar os logons de saudação no servidor de origem Olá com hello instrução SELECT a seguir.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="b7e9f-133">Somente um membro da função de banco de dados db_owner hello, o usuário de dbo hello ou o administrador do servidor, pode determinar todas Olá banco de dados entidades do usuário no banco de dados primário hello.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="b7e9f-134">2. Localize Olá SID para logons de saudação identificados na etapa 1:</span><span class="sxs-lookup"><span data-stu-id="b7e9f-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="b7e9f-135">Comparando a saída de saudação de consultas de saudação da seção anterior hello e correspondência hello SIDs, você pode mapear Olá toodatabase usuário do logon.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="b7e9f-136">Logons que têm um usuário de banco de dados com um SID correspondente têm o banco de dados do usuário acesso toothat como esse usuário de banco de dados principal.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="b7e9f-137">Olá consulta a seguir pode ser usado toosee todos os objetos de usuário hello e seus SIDs em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="b7e9f-138">Somente um membro da saudação db_owner administração de função ou um servidor do banco de dados pode executar essa consulta.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="b7e9f-139">Olá **INFORMATION_SCHEMA** e **sys** os usuários têm *nulo* SIDs e hello **convidado** SID é **0x00**.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="b7e9f-140">Olá **dbo** SID pode começar com *0x01060000000001648000000000048454*, se o criador de banco de dados de saudação foi Olá administrador de servidor, em vez de um membro de **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="b7e9f-141">3. Crie logons Olá no servidor de destino hello:</span><span class="sxs-lookup"><span data-stu-id="b7e9f-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="b7e9f-142">Olá última etapa é o servidor de destino toohello toogo ou servidores e gerar Olá logons com hello apropriado SIDs.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="b7e9f-143">sintaxe básica de saudação é da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="b7e9f-144">Se você quiser toogrant usuário acesso toohello secundário, mas não toohello primário, você pode fazer isso alterando o logon do usuário Olá no servidor primário hello usando Olá sintaxe a seguir.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="b7e9f-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="b7e9f-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="b7e9f-146">Desabilitar não altera a senha de hello, para que você sempre pode habilitá-lo se necessário.</span><span class="sxs-lookup"><span data-stu-id="b7e9f-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b7e9f-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7e9f-147">Next steps</span></span>
* <span data-ttu-id="b7e9f-148">Para saber mais sobre como gerenciar o acesso ao banco de dados e os logons, veja [Segurança do Banco de Dados SQL: gerenciar a segurança de acesso e de logon do banco de dados](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="b7e9f-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="b7e9f-149">Para saber mais sobre usuários de bancos de dados independentes, confira [Usuários de bancos de dados independentes - Tornando seu banco de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7e9f-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="b7e9f-150">Para saber como usar e configurar a replicação geográfica ativa, confira [replicação geográfica ativa](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b7e9f-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="b7e9f-151">Para obter informações sobre como usar a restauração geográfica, confira [restauração geográfica](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="b7e9f-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

