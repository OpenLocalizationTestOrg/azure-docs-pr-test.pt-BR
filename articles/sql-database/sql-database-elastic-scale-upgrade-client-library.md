---
title: "biblioteca de cliente de banco de dados Elástico mais recente do aaaUpgrade toohello | Microsoft Docs"
description: Atualizar aplicativos e bibliotecas usando o Nuget
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>Atualizar uma aplicativo toouse hello mais recente Elástico de banco de dados biblioteca de cliente
Novas versões do hello [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md) estão disponíveis por meio da interface do Gerenciador de NuGetPackage de saudação NuGetand no Visual Studio. Atualizações contêm correções de bugs e suportam para novos recursos de biblioteca de saudação do cliente.

**Para a versão mais recente do hello:** ir muito[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Recrie seu aplicativo com a nova biblioteca de hello, bem como alterar seus metadados do Gerenciador do mapa de fragmentos existentes armazenados em seus novos recursos de bancos de dados do Azure SQL toosupport.

Executar essas etapas na ordem garante que versões antigas de biblioteca de saudação do cliente não estão mais presentes no seu ambiente quando objetos de metadados são atualizados, que significa que os objetos de metadados de versão antiga não serão criados após a atualização.   

## <a name="upgrade-steps"></a>Etapas de atualização
**1. Atualize seus aplicativos.** No Visual Studio, download e referência Olá versão mais recente cliente biblioteca em todos os seus projetos de desenvolvimento que usam a biblioteca de saudação; em seguida, recriar e implantar. 

* Em sua solução do Visual Studio, selecione **Ferramentas** --> **NuGet Package Manager** -->  **Gerenciar pacotes NuGet para solução**. 
* (Visual Studio 2013) No painel esquerdo do hello, selecione **atualizações**e, em seguida, selecione Olá **atualização** botão no pacote de saudação **biblioteca de cliente do Azure SQL banco de dados Elástico escala** que aparece na Olá janela.
* (Visual Studio 2015) Defina a caixa de filtro de saudação muito**atualização disponível**. Selecione Olá tooupdate de pacote e, em seguida, clique em Olá **atualização** botão.
* (2017 do visual Studio) Na parte superior de saudação da caixa de diálogo hello, selecione **atualizações**. Selecione Olá tooupdate de pacote e, em seguida, clique em Olá **atualização** botão.
* Criar e implantar. 

**2. Atualize seus scripts.** Se você estiver usando **PowerShell** scripts toomanage fragmentos, [baixar a nova versão da biblioteca Olá](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) e copie-o no diretório de saudação do qual você pode executar scripts. 

**3. Atualize o seu serviço de mesclagem de divisão.** Se você usar o hello banco de dados Elástico ferramenta de mesclagem de divisão tooreorganize dados fragmentados, [baixar e implantar Olá a versão mais recente da ferramenta Olá](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/). Atualização etapas detalhadas para Olá serviço pode ser encontrado [aqui](sql-database-elastic-scale-overview-split-and-merge.md). 

**4. Atualizar seus bancos de dados do Gerenciador do Mapa de Fragmentos**. Atualize os metadados de saudação seus mapas de fragmento de suporte no banco de dados do SQL Azure.  Há duas maneiras que você pode fazer isso, usando o PowerShell ou C#. Ambas as opções são mostradas abaixo.

***Opção 1: Atualizar os metadados usando o PowerShell***

1. Baixar o utilitário de linha de comando mais recente Olá para NuGet do [aqui](http://nuget.org/nuget.exe) e salve a pasta de tooa. 
2. Abra um Prompt de comando, navegue toohello mesma pasta e o comando de saudação do problema:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. Navegue até a subpasta toohello contendo Olá nova DLL versão do cliente que apenas baixar, por exemplo:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. Baixar o miniscript atualização do cliente Olá Elástico de banco de dados de saudação [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), e salve-o em hello na mesma pasta que contém Olá DLL.
5. Nessa pasta, execute ".\upgrade.ps1 PowerShell" no prompt de comando do hello e siga os prompts de saudação.

***Opção 2: Atualizar os metadados usando C#***

Como alternativa, criar um aplicativo do Visual Studio que abre sua ShardMapManager, itera em todos os fragmentos e executa a atualização de metadados de saudação chamando métodos Olá [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) e [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) como neste exemplo: 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

Essas técnicas para atualizações de metadados podem ser aplicadas várias vezes sem danos. Por exemplo, se uma versão mais antiga do cliente cria inadvertidamente um fragmento depois que você atualizou, você pode executar atualização novamente em todos os tooensure de fragmentos que Olá versão mais recente de metadados está presente em toda a infraestrutura. 

**Observação:** a data de publicação de novas versões da biblioteca de cliente Olá continuar toowork com versões anteriores do hello Gerenciador do mapa de fragmentos metadados no banco de dados de SQL do Azure e vice-versa.   No entanto tootake vantagem de alguns dos novos recursos de saudação do cliente mais recente hello, metadados precisa toobe atualizado.   Observe que as atualizações de metadados não afetará quaisquer dados de usuário ou dados específicos do aplicativo, somente os objetos criados e usados por Olá Gerenciador do mapa de fragmentos.  E os aplicativos continuam toooperate por meio de sequência de atualização Olá descrita acima. 

## <a name="elastic-database-client-version-history"></a>O histórico de versões de cliente do banco de dados elástico
Para o histórico de versão, vá muito[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

