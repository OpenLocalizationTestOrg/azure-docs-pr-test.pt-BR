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
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a>Configurar e gerenciar a segurança do Banco de Dados SQL para restauração geográfica ou failover 

> [!NOTE]
> A [Replicação geográfica ativa](sql-database-geo-replication-overview.md) agora está disponível para todos os bancos de dados em todas as camadas de serviço.
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a>Visão geral dos requisitos de autenticação para a recuperação de desastre
Este tópico descreve Olá tooconfigure de requisitos de autenticação e controle [replicação geográfica ativa](sql-database-geo-replication-overview.md) e Olá etapas necessária tooset usuário acesso toohello banco de dados secundário. Ele também descreve como habilitar o banco de dados do access toohello recuperados depois de usar [restauração geográfica](sql-database-recovery-using-backups.md#geo-restore). Para obter mais informações sobre as opções de recuperação, confira [Visão geral de continuidade dos negócios](sql-database-business-continuity.md).

## <a name="disaster-recovery-with-contained-users"></a>Recuperação de desastre com usuários independentes
Ao contrário de usuários tradicionais, que deve ser mapeado toologins no banco de dados mestre hello, um usuário independente é totalmente gerenciado pelo Olá próprio banco de dados. Isso oferece dois benefícios. No cenário de recuperação de desastres hello, os usuários de Olá podem continuar tooconnect toohello novo principal banco de dados ou Olá recuperado usando a restauração geográfica sem qualquer configuração adicional, como o banco de dados de saudação gerencia usuários hello. Também há possíveis benefícios de desempenho e escalabilidade com esta configuração de uma perspectiva de logon. Para obter mais informações, consulte [Usuários do banco de dados independente - Tornando o banco de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx). 

compensação principal Olá é que é mais difícil gerenciar o processo de recuperação de desastres Olá em escala. Quando você tiver vários bancos de dados que Olá use mesmo logon, manter credenciais hello usando contido usuários em vários bancos de dados podem invalidar os benefícios de saudação do usuários contidos. Por exemplo, a política de rotação de senha Olá requer que fazer alterações consistentemente em bancos de dados de vários em vez da alteração de senha Olá para logon Olá uma vez no banco de dados mestre hello. Por esse motivo, se você tiver vários bancos de dados que use Olá mesmo nome de usuário e senha, não é recomendável usar usuários contidos. 

## <a name="how-tooconfigure-logins-and-users"></a>Como tooconfigure logons e usuários
Se você estiver usando os logons e usuários (em vez dos usuários independentes), você deve tomar tooinsure etapas adicionais que Olá existem mesmos logons no banco de dados mestre hello. Olá seções a seguir descrevem Olá etapas envolvidas adicionais considerações sobre e.

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a>Configurar usuário acesso tooa secundária ou recuperado banco de dados
Para toobe de banco de dados secundário Olá utilizável como um banco de dados secundário somente leitura e tooensure acesso adequado toohello novo banco de dados ou hello banco de dados primário recuperado usando a restauração geográfica, Olá mestre saudação do servidor de destino do banco de dados deve ter Olá configuração de segurança apropriadas em vigor antes da recuperação de saudação.

permissões específicas de saudação para cada etapa são descritas posteriormente neste tópico.

Preparando tooa de acesso do usuário a replicação geográfica secundária deve ser executada como parte de configurar a replicação geográfica. Preparar toohello bancos de dados restaurados de replicação geográfica de acesso do usuário deve ser executada a qualquer momento quando o servidor original hello está online (por exemplo, como parte da análise Olá DR).

> [!NOTE]
> Se você não o failover ou restauração geográfica server tooa que não tenha configurados corretamente logons, acesso tooit será limitado toohello conta de administrador de servidor.
> 
> 

Configuração de logons no servidor de destino Olá envolve três etapas descritas a seguir:

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a>1. Determine os logons com o banco de dados do access toohello primário:
Olá primeira etapa do processo de saudação é toodetermine quais logons devem ser duplicados no servidor de destino de saudação. Isso é feito com um par de instruções SELECT, em Olá lógico banco de dados mestre no servidor de origem hello e no banco de dados primário do hello em si.

Olá somente o administrador do servidor ou um membro da saudação **LoginManager** função de servidor pode determinar os logons de saudação no servidor de origem Olá com hello instrução SELECT a seguir. 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

Somente um membro da função de banco de dados db_owner hello, o usuário de dbo hello ou o administrador do servidor, pode determinar todas Olá banco de dados entidades do usuário no banco de dados primário hello.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a>2. Localize Olá SID para logons de saudação identificados na etapa 1:
Comparando a saída de saudação de consultas de saudação da seção anterior hello e correspondência hello SIDs, você pode mapear Olá toodatabase usuário do logon. Logons que têm um usuário de banco de dados com um SID correspondente têm o banco de dados do usuário acesso toothat como esse usuário de banco de dados principal. 

Olá consulta a seguir pode ser usado toosee todos os objetos de usuário hello e seus SIDs em um banco de dados. Somente um membro da saudação db_owner administração de função ou um servidor do banco de dados pode executar essa consulta.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> Olá **INFORMATION_SCHEMA** e **sys** os usuários têm *nulo* SIDs e hello **convidado** SID é **0x00**. Olá **dbo** SID pode começar com *0x01060000000001648000000000048454*, se o criador de banco de dados de saudação foi Olá administrador de servidor, em vez de um membro de **DbManager**.
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a>3. Crie logons Olá no servidor de destino hello:
Olá última etapa é o servidor de destino toohello toogo ou servidores e gerar Olá logons com hello apropriado SIDs. sintaxe básica de saudação é da seguinte maneira.

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> Se você quiser toogrant usuário acesso toohello secundário, mas não toohello primário, você pode fazer isso alterando o logon do usuário Olá no servidor primário hello usando Olá sintaxe a seguir.
> 
> ALTER LOGIN <login name> DISABLE
> 
> Desabilitar não altera a senha de hello, para que você sempre pode habilitá-lo se necessário.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Para saber mais sobre como gerenciar o acesso ao banco de dados e os logons, veja [Segurança do Banco de Dados SQL: gerenciar a segurança de acesso e de logon do banco de dados](sql-database-manage-logins.md).
* Para saber mais sobre usuários de bancos de dados independentes, confira [Usuários de bancos de dados independentes - Tornando seu banco de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx).
* Para saber como usar e configurar a replicação geográfica ativa, confira [replicação geográfica ativa](sql-database-geo-replication-overview.md)
* Para obter informações sobre como usar a restauração geográfica, confira [restauração geográfica](sql-database-recovery-using-backups.md#geo-restore)

