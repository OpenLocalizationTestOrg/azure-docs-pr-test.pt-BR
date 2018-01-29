---
title: "Perguntas frequentes sobre a Escala Elástica SQL do Azure | Microsoft Docs"
description: "Perguntas frequentes sobre a Escala Elástico do banco de dados SQL do Azure."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4a2f73df00dd706699b20062d443af3bb88b6ef4
ms.sourcegitcommit: dfd49613fce4ce917e844d205c85359ff093bb9c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2017
---
# <a name="elastic-database-tools-faq"></a>Pergunta Frequentes das ferramentas de banco de dados elástico
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-the-sharding-key-for-the-schema-info"></a>Se eu tiver um único locatário por fragmento e nenhuma chave de fragmentação, como preencher a chave de fragmentação para as informações do esquema?
O objeto de informações de esquema só é usado para dividir os cenários de mesclagem. Se um aplicativo for basicamente o único locatário, ele não exige a ferramenta de divisão e mesclagem e, portanto, não é necessário para preencher o objeto de informações de esquema.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>Eu provisionei um banco de dados e já tenho um Gerenciador de mapa de fragmento, como registro o novo banco de dados como um fragmento?
Consulte **[Adicionar um fragmento de um aplicativo usando a biblioteca de cliente do banco de dados elástico](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>Quanto custam as ferramentas de banco de dados elástico?
Usar a biblioteca de cliente do banco de dados elástico não incorrerá em todos os custos. Custos se acumulam apenas para os bancos de dados do SQL Azure que você usa para fragmentos e o Gerenciador de mapa de fragmento, bem como as funções web/de trabalho configuradas para a ferramenta de divisão e mesclagem.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>Por que minhas credenciais não funcionam quando eu adiciono um fragmento de um servidor diferente?
Não use credenciais na forma de “ID do Usuário=username@servername”, em vez disso, basta usar “User ID = nome de usuário”.  Além disso, certifique-se de que o logon “username” tem permissões no fragmento.

#### <a name="do-i-need-to-create-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>É necessário criar um Gerenciador de mapa de fragmento e preencher os fragmentos sempre que iniciar meus aplicativos?
Não, a criação do Gerenciador de mapa de fragmento (por exemplo, **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) é uma operação única.  Seu aplicativo deve usar a chamada **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** em tempo de inicialização do aplicativo.  Deve existir apenas uma chamada por domínio de aplicativo.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>Tenho dúvidas sobre o uso das ferramentas de banco de dados elástico, como obter respostas para elas?
Vá ao [Fórum do banco de dados SQL do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-the-same-shard--is-this-by-design"></a>Quando recebo uma conexão de banco de dados usando uma chave de fragmentação, ainda posso consultar dados para outras chaves de fragmentação no mesmo fragmento.  Isso é proposital?
As API de escala elástica oferecem uma conexão com o banco de dados correto para sua chave de fragmentação, mas não fornece filtragem de chave de fragmentação.  Adicione cláusulas **WHERE** à sua consulta para restringir o escopo para a chave de fragmentação fornecidos, se necessário.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>Posso usar uma edição diferente do banco de dados do Azure para cada fragmento no meu conjunto de fragmentos?
Sim, um fragmento é um banco de dados individual e, portanto, um fragmento poderia ser uma edição Premium e o outro ser uma edição Standard. Além disso, a edição de um fragmento pode aumentar ou diminuir várias vezes durante o tempo de vida do fragmento.

#### <a name="does-the-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>O ferramenta de divisão e mesclagem provisiona (ou exclui) um banco de dados durante uma operação de divisão ou mesclagem?
Não. Para operações de **divisão** , o banco de dados de destino deve existir com o esquema apropriado e ser registrado com o Gerenciador de mapa do fragmento.  Para operações de **mesclagem** , você deve excluir o fragmento do Gerenciador do mapa de fragmento e, em seguida, excluir o banco de dados.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

