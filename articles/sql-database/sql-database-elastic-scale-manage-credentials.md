---
title: "credenciais aaaManaging na biblioteca de cliente do banco de dados Elástico Olá | Microsoft Docs"
description: "Como tooset Olá nível certo de credenciais de administrador somente para tooread, para aplicativos de banco de dados Elástico"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>As credenciais usadas biblioteca de cliente de banco de dados Elástico tooaccess Olá
Olá [biblioteca de cliente do banco de dados Elástico](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) usa três tipos diferentes de saudação do credenciais tooaccess [Gerenciador do mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md). Dependendo da necessidade de Olá, use credencial Olá com nível mais baixo de saudação de possíveis de acesso.

* **Credenciais de gerenciamento**: para criar ou manipular um gerenciador de mapa de fragmentos. (Consulte Olá [glossário](sql-database-elastic-scale-glossary.md).) 
* **Credenciais de acesso**: tooaccess um fragmento existente mapear manager tooobtain informações sobre fragmentos.
* **Credenciais de Conexão**: tooconnect tooshards. 

Consulte [Gerenciamento de bancos de dados e logons no Banco de Dados SQL do Azure](sql-database-manage-logins.md) 

## <a name="about-management-credentials"></a>Sobre as credenciais de gerenciamento
Credenciais de gerenciamento são usado toocreate um [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) objeto para aplicativos que manipulam os mapas de fragmento. (Por exemplo, consulte [adicionando um fragmento usando as ferramentas de banco de dados Elástico](sql-database-elastic-scale-add-a-shard.md) e [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md)) usuário Olá Olá escala elástica da biblioteca de cliente cria usuários do SQL hello e logons do SQL Server e garante que cada um é concedidas permissões de leitura/gravação da saudação no fragmento global Olá mapeiam banco de dados e todos os fragmentos bancos de dados também. Essas credenciais são mapa de fragmento global Olá toomaintain usado e mapas de fragmento de local de saudação ao mapa do fragmento toohello alterações são executadas. Por exemplo, usar Olá gerenciamento credenciais toocreate Olá fragmento mapa manager objeto (usando [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

variável de saudação **smmAdminConnectionString** é uma cadeia de conexão que contém as credenciais de gerenciamento de saudação. Olá ID de usuário e senha fornece banco de dados de leitura/gravação acesso tooboth fragmento mapa e fragmentos individuais. a cadeia de conexão Olá gerenciamento também inclui Olá server nome e o banco de dados nome tooidentify Olá fragmento global mapa banco de dados. Aqui está uma cadeia de conexão típica para essa finalidade:

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

Não utilize valores no formulário de saudação do "username@server" — em vez disso, usar apenas o valor de "username" hello.  Isso ocorre porque as credenciais devem funcionar em relação ao banco de dados do fragmento mapa manager hello e fragmentos individuais, que podem estar em servidores diferentes.

## <a name="access-credentials"></a>Credenciais de acesso
Ao criar um fragmento do Gerenciador do mapa em um aplicativo que não administrar mapas de fragmento, use as credenciais que têm permissões somente leitura no mapa do fragmento global de saudação. Olá informações recuperadas do mapa do fragmento global de saudação com essas credenciais são usadas para [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) e fragmentos de saudação toopopulate cache no cliente de saudação do mapa. Olá credenciais são fornecidas por meio de saudação mesma chamada padrão muito**GetSqlShardMapManager** como mostrado acima: 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Observe o uso de saudação do hello **smmReadOnlyConnectionString** tooreflect uso de saudação de credenciais diferentes para esse acesso em nome de **não-administrador** usuários: essas credenciais não devem fornecer a gravação permissões no mapa do fragmento global de saudação. 

## <a name="connection-credentials"></a>As credenciais de conexão
Credenciais adicionais são necessárias ao usar Olá [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) método tooaccess um fragmento associado com uma chave de fragmentação. Essas credenciais precisam de permissões de tooprovide para tabelas de mapa de fragmento local toohello acesso somente leitura que reside no fragmento hello. Isso é necessário tooperform validação de conexão para roteamento dependente de dados no fragmento de saudação. Este trecho de código permite que o acesso a dados no contexto de saudação do roteamento dependente de dados: 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

Neste exemplo, **smmUserConnectionString** contém a cadeia de caracteres de conexão de saudação para Olá as credenciais do usuário. Para o banco de dados SQL Azure, eis uma cadeia de conexão típica para as credenciais do usuário: 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Como com credenciais de administrador Olá, não valores em forma de saudação de "username@server". Em vez disso, use "username".  Observe também que a cadeia de caracteres de conexão de saudação não contém um nome de servidor e nome do banco de dados. Isso ocorre porque Olá **OpenConnectionForKey** chamada direcionará automaticamente Olá conexão toohello correta de fragmentação com base na chave de saudação. Portanto, nome do banco de dados de saudação e o nome do servidor não são fornecidos. 

## <a name="see-also"></a>Consulte também
[Gerenciamento de bancos de dados e logons no Banco de Dados SQL do Azure](sql-database-manage-logins.md)

[Protegendo o Banco de Dados SQL](sql-database-security-overview.md)

[Introdução a trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

