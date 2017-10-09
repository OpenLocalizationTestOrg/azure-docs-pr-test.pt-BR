---
title: "aaaBuild de aplicativos móveis com o Xamarin e Azure Cosmos DB | Microsoft Docs"
description: "Um tutorial que cria um aplicativo iOS, Android ou Forms do Xamarin usando o Azure Cosmos DB. O Azure Cosmos DB é um banco de dados na nuvem para aplicativos móveis rápido e em escala mundial."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>Criar aplicativos móveis com o Xamarin e o Azure Cosmos DB
A maioria dos aplicativos precisam toostore dados na nuvem hello e o banco de dados do Azure Cosmos é um banco de dados de nuvem para aplicativos móveis. Ele tem tudo o que um desenvolvedor móvel precisa. Ele é um banco de dados como serviço totalmente gerenciado que é dimensionado sob demanda. Ele pode colocar seu aplicativo tooyour de dados transparente, onde quer que seus usuários estão localizados em todo o mundo de saudação. Usando Olá [SDK do Azure Cosmos DB .NET Core](documentdb-sdk-dotnet-core.md), você pode habilitar toointeract de aplicativos móveis Xamarin diretamente com o Azure Cosmos banco de dados, sem uma camada intermediária.

Este artigo fornece um tutorial para a criação de aplicativos móveis com o Xamarin e o Azure Cosmos DB. Você pode encontrar o código-fonte completo Olá para tutorial Olá em [Xamarin e Azure Cosmos DB no GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin), incluindo como toomanage usuários e permissões.

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>Funcionalidades do Azure Cosmos DB para aplicativos móveis
Banco de dados do Azure Cosmos fornece Olá a seguir os principais recursos para desenvolvedores de aplicativos móveis:

![Funcionalidades do Azure Cosmos DB para aplicativos móveis](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* Consultas avançados sobre o repositório de dados. O Azure Cosmos DB armazena dados como documentos JSON sem esquemas em coleções heterogêneas. Ele oferece [consultas rápidas e avançadas](documentdb-sql-query.md) sem Olá necessário tooworry sobre esquemas ou índices.
* Taxa de transferência rápida. Leva apenas alguns milissegundos tooread e gravar documentos com o banco de dados do Azure Cosmos. Os desenvolvedores podem especificar a taxa de transferência Olá precisam e o banco de dados do Azure Cosmos respeita-lo com SLAs de 99,99%.
* Escala ilimitada. Suas coleções do Azure Cosmos DB [aumentam conforme seu aplicativo cresce](partition-data.md). Você pode iniciar com tamanho de dados pequeno e taxa de transferência de centenas de solicitações por segundo. As coleções podem crescer toopetabytes de dados e a taxa de transferência arbitrariamente grande com centenas de milhões de solicitações por segundo.
* Distribuído globalmente. Aplicativo móvel, os usuários estiverem Olá atravessar, geralmente Olá, mundo. O Azure Cosmos DB é um [banco de dados distribuído globalmente](distribute-data-globally.md). Clique em Olá mapa toomake seus usuários tooyour acessível de dados.
* Autorização interna avançada. Com o Azure Cosmos DB, você pode implementar facilmente padrões populares como [dados por usuário](https://aka.ms/documentdb-xamarin-todouser) ou dados compartilhados por vários usuários, sem códigos de autorização personalizados complexos.
* Consultas geoespaciais. Hoje, muitos aplicativos móveis oferecem experiências geográficas contextuais. Com suporte de primeira classe para [tipos geoespaciais](geospatial.md), torna o banco de dados do Azure Cosmos criando tooaccomplish de fácil essas experiências.
* Anexos binários. Os dados de aplicativo geralmente incluem blobs binários. O suporte nativo para anexos torna mais fácil toouse o banco de dados do Azure Cosmos como uma loja de conveniência para seus dados de aplicativo.

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Tutorial do Xamarin e do Azure Cosmos DB
Olá seguinte tutorial mostra como toobuild um aplicativo móvel usando o Xamarin e Azure Cosmos DB. Você pode encontrar o código-fonte completo Olá para tutorial Olá em [Xamarin e Azure Cosmos DB no GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).

### <a name="get-started"></a>Introdução
É fácil tooget iniciado com o banco de dados do Azure Cosmos. Vá toohello portal do Azure e criar uma nova conta de banco de dados do Azure Cosmos. Clique em Olá **início rápido** guia. Download Xamarin Forms tarefas lista exemplo hello que já está conectado a conta de banco de dados do Azure Cosmos tooyour. 

![Início rápido do Azure Cosmos DB para aplicativos móveis](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

Ou se você tiver um aplicativo Xamarin existente, você pode adicionar Olá [pacote NuGet de banco de dados do Azure Cosmos](documentdb-sdk-dotnet-core.md). O Azure Cosmos DB dá suporte às bibliotecas compartilhadas do Xamarin.IOS, Xamarin.Android e Xamarin Forms.

### <a name="work-with-data"></a>Trabalhar com dados
Seus registros de dados são armazenados no Azure Cosmos DB como documentos JSON sem esquemas em coleções heterogêneas. Você pode armazenar documentos com estruturas diferentes em Olá mesma coleção:

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

No seus projetos do Xamarin, você pode usar consultas integradas à linguagem para dados sem esquema:

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>Adicionar usuários
Como muitos obtém exemplos de Introdução, o exemplo de banco de dados do Azure Cosmos hello baixado autentica toohello serviço usando um chave mestra codificados no código do aplicativo hello. Esse padrão não é uma prática recomendada para um aplicativo que você pretende toorun em qualquer lugar, exceto em um emulador local. Se um usuário não autorizado obtido Olá master key, todos os dados de saudação em sua conta do banco de dados do Azure Cosmos poderiam ser comprometidos. Em vez disso, você deseja que seu aplicativo tooaccess apenas Olá registros para o usuário conectado hello. Banco de dados do Azure Cosmos permite aos desenvolvedores toogrant aplicativo leitura ou leitura/gravação no conjunto de tooa de permissão, um conjunto de documentos, agrupados por uma chave de partição ou um documento específico. 

Siga estas etapas toomodify Olá tarefas lista aplicativo tooa tarefas multiusuário lista aplicativo: 

  1. Adicione logon tooyour aplicativo usando o Facebook, do Active Directory ou qualquer outro provedor.

  2. Criar uma coleção de UserItems de banco de dados do Azure Cosmos com **/userId** como chave de partição hello. Especificando a chave de partição Olá para sua coleção permite que o banco de dados do Azure Cosmos tooscale infinitamente como número de saudação de seus usuários do aplicativo cresce, enquanto continua consultas rápidas toooffer.

  3. Adicione o Agente de Token de Recurso do Azure Cosmos DB. Essa API da Web simples autentica os usuários e emite tokens de curta duração toosigned os usuários com acesso somente documentos toohello dentro de sua partição. Neste exemplo, o Agente de Token de Recurso é hospedado no Serviço de Aplicativo.

  4. Modificar Olá aplicativo tooauthenticate tooResource Broker Token com o Facebook e solicitar tokens de recurso Olá para Olá Facebook usuários conectados. Você pode acessar seus dados no hello UserItems coleção.  

Você pode encontrar um exemplo de código completo desse padrão em [Agente de Token de Recurso no GitHub](http://aka.ms/documentdb-xamarin-todouser). Este diagrama ilustra a solução hello:

![Agente de usuários e permissões do Azure Cosmos DB](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

Se você quiser que dois usuários toohave acesso toohello mesma lista de tarefas, você pode adicionar o token de acesso de toohello permissões adicionais no agente de Token de recurso.

### <a name="scale-on-demand"></a>Dimensionar sob demanda
O Azure Cosmos DB é um banco de dados como serviço gerenciado. À medida que aumenta a sua base de usuários, você não precisa tooworry sobre o provisionamento de máquinas virtuais ou aumentar núcleos. Você só precisa tootell Azure Cosmos DB é quantas operações por segundo (taxa de transferência) seu aplicativo precisa. Você pode especificar a taxa de transferência Olá via Olá **escala** guia usando uma medida de taxa de transferência chamada de unidades de solicitação (RUs) por segundo. Por exemplo, uma operação de leitura em um documento de 1 KB exige 1 RU. Você também pode adicionar alertas toohello **taxa de transferência** toomonitor métrica Olá aumento de tráfego e alterar programaticamente a taxa de transferência Olá alertas disparados.

![Produtividade de escala do Azure Cosmos DB sob demanda](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>Escala mundial
Como popularidade de ganhos seu aplicativo, você pode ter usuários globo hello. Ou talvez você queira toobe preparado para imprevistos. Vá toohello portal do Azure e abra sua conta de banco de dados do Azure Cosmos. Clique em Olá mapa toomake seu número de tooany continuamente replicar dados de regiões Olá, mundo. Essa funcionalidade torna os dados disponíveis, onde quer que os usuários estejam. Você também pode adicionar toobe de políticas de failover preparado para contingências.

![Escala do Azure Cosmos DB entre regiões geográficas](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

Parabéns. Você concluiu a solução hello e tiver um aplicativo móvel com o Xamarin e Azure Cosmos DB. Execute aplicativos de Cordova de toobuild etapas semelhantes usando hello Azure Cosmos DB JavaScript SDK e aplicativos do iOS/Android nativo por meio de APIs de REST do Azure Cosmos banco de dados.

## <a name="next-steps"></a>Próximas etapas
* Exibir código-fonte Olá [Xamarin e Azure Cosmos DB no GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).
* Baixar Olá [SDK do Azure Cosmos DB .NET Core](documentdb-sdk-dotnet-core.md).
* Encontre mais exemplos de código para [aplicativos .NET](documentdb-dotnet-samples.md).
* Saiba mais sobre as [funcionalidades de consulta avançadas do Azure Cosmos DB](documentdb-sql-query.md).
* Saiba mais sobre o [suporte geoespacial no Azure Cosmos DB](geospatial.md).



