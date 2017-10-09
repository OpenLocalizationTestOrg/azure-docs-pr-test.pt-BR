---
title: "aaaAzure perguntas Frequentes de dimensionamento Elástico SQL | Microsoft Docs"
description: "Perguntas frequentes sobre a Escala Elástico do banco de dados SQL do Azure."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>Pergunta Frequentes das ferramentas de banco de dados elástico
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>Se um único locatário por fragmento e nenhuma chave de fragmentação, como preencher chave de fragmentação Olá para obter informações de esquema Olá?
objeto de informações de esquema de saudação é apenas os cenários de mesclagem toosplit usado. Se um aplicativo é inerentemente único locatário, não exige a ferramenta de mesclagem de divisão de Olá, e, portanto, não há nenhum objeto de informações de esquema do necessidade toopopulate hello.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>Eu provisionei um banco de dados e já tenho um Gerenciador de mapa de fragmento, como registro o novo banco de dados como um fragmento?
Consulte  **[adicionar um aplicativo de tooan do fragmento usando a biblioteca de cliente do banco de dados Elástico Olá](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>Quanto custam as ferramentas de banco de dados elástico?
Usando a biblioteca de cliente do banco de dados Elástico Olá não incorrerá em todos os custos. Os custos se acumulam apenas para bancos de dados de SQL do Azure de saudação que você usa para fragmentos e hello Gerenciador do mapa de fragmentos, bem como funções de web/trabalhador Olá que provisionar para a ferramenta de mesclagem de divisão de saudação.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>Por que minhas credenciais não funcionam quando eu adiciono um fragmento de um servidor diferente?
Não usar credenciais na forma de saudação de "ID de usuário =username@servername", em vez disso, basta usar "ID de usuário = nome de usuário".  Além disso, certifique-se de que o logon "username" hello tem permissões no fragmento hello.

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>Precisa toocreate um Gerenciador de mapa do fragmento e preencher os fragmentos sempre que iniciar meus aplicativos?
Não — Olá criação de saudação Gerenciador do mapa de fragmentos (por exemplo,  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) é uma operação única.  Seu aplicativo deve usar chamada hello  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  em tempo de inicialização do aplicativo.  Deve existir apenas uma chamada por domínio de aplicativo.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>Tenho dúvidas sobre o uso das ferramentas de banco de dados elástico, como obter respostas para elas?
Entre em contato toous em Olá [Fórum do banco de dados do Azure SQL](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>Quando receber uma conexão de banco de dados usando uma chave de fragmentação, ainda pode consultar dados para outros fragmentação chaves em Olá mesmo fragmento.  Isso é proposital?
Olá APIs de dimensionamento Elástico oferecem um banco de dados conexão toohello correto para sua chave de fragmentação, mas não fornecer filtragem de chave de fragmentação.  Adicionar **onde** cláusulas tooyour consulta toorestrict Olá escopo toohello fornecido a chave de fragmentação, se necessário.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>Posso usar uma edição diferente do banco de dados do Azure para cada fragmento no meu conjunto de fragmentos?
Sim, um fragmento é um banco de dados individual e, portanto, um fragmento poderia ser uma edição Premium e o outro ser uma edição Standard. Além disso, edição de saudação de um fragmento pode expandir ou reduzir várias vezes durante o tempo de vida de saudação do fragmento hello.

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>Olá provisionar da ferramenta de mesclagem de divisão (ou excluir) um banco de dados durante uma operação de divisão ou mesclagem?
Não. Para **dividir** operações, o banco de dados de destino Olá deve existir com o esquema apropriado da saudação e ser registrado com o Gerenciador do mapa de fragmentos de saudação.  Para **mesclagem** operações, você deve excluir fragmentos de saudação do Gerenciador do mapa de fragmentos hello e, em seguida, exclua o banco de dados de saudação.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

