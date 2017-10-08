---
title: "Azure Cosmos DB: compilar um aplicativo Web com autenticação do Xamarin e do Facebook | Microsoft Docs"
description: "Apresenta um exemplo de código do .NET podem usar tooconnect tooand consultar o banco de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure Cosmos DB: compilar um aplicativo Web com autenticação do Xamarin, do Facebook e do .NET

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure. Você, em seguida, criar e implantar um aplicativo da web lista todo baseado Olá [API .NET do DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)e o mecanismo de autorização do Azure Cosmos DB hello. aplicativo de web de lista de tarefas Olá implementa um padrão de dados por usuário que permite que os usuários toologin usando o Facebook Auth e gerenciar seus próprios itens toodo.

## <a name="prerequisites"></a>Pré-requisitos

Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Criar uma conta de banco de dados

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Adicionar uma coleção

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos clone uma API de documentos de aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo. Você verá como é fácil toowork com dados programaticamente. 

1. Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. Em seguida, abra o arquivo de DocumentDBTodo.sln de saudação da pasta de samples/xamarin/UserItems/xamarin.forms de saudação no Visual Studio. 

## <a name="review-hello-code"></a>Examine o código de saudação

código de saudação na pasta de Xamarin Olá contém:

* aplicativo Xamarin. aplicativo Hello armazena itens de tarefas do usuário Olá em uma coleção particionada chamada UserItems.
* API do agente de token de recurso. Um recurso de banco de dados do Azure Cosmos toobroker API da Web ASP.NET simples tokens toohello os usuários do aplicativo hello conectado. Tokens de recurso são tokens de acesso de curta duração que fornecem aplicativo Olá Olá acesso toohello registrada nos dados do usuário.

Olá autenticação e fluxo de dados é ilustrado no diagrama de saudação abaixo.

* Olá UserItems coleção é criada com a chave de partição Olá ' / userid'. Especificar uma chave de partição para uma coleção permite que o banco de dados do Azure Cosmos tooscale infinitamente como número de saudação de usuários e itens cresce.
* Olá Xamarin aplicativo permite toologin de usuários com credenciais do Facebook.
* Olá Xamarin aplicativo usa tooauthenticate de token de acesso do Facebook com o API ResourceTokenBroker
* broker API do token de recurso de Olá autentica Olá solicitação usando o recurso de autenticação do serviço de aplicativo e solicita um token de recurso do banco de dados do Azure Cosmos com documentos de tooall de acesso de leitura/gravação compartilhar a chave de partição de saudação do usuário autenticado.
* Agente de token de recurso retorna Olá recurso token toohello cliente aplicativo.
* aplicativo Hello acessa os itens de tarefas do usuário hello usando o token de recurso hello.

![Aplicativo de tarefas pendentes com os dados de exemplo](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.

1. Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**. Você usará botões de cópia Olá Olá direita da saudação toocopy da tela hello URI e a chave primária no arquivo Web. config de saudação na próxima etapa do hello.

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-xamarin-dotnet/keys.png)

2. No Visual Studio de 2017, abra Web. config Olá na pasta do azure-documentdb-dotnet/exemplos/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker hello. 

3. Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá valor Olá accountUrl em Web. config. 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. Em seguida, copie o valor de chave primária do portal de saudação e torná-lo Olá valor Olá accountKey em Web.congif. 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos. 

## <a name="build-and-deploy-hello-web-app"></a>Criar e implantar o aplicativo da web de saudação

1. No portal do Azure de Olá, crie um serviço de aplicativo site toohost Olá recurso token broker API.
2. No hello portal do Azure, abra a folha de configurações do aplicativo de saudação do broker site da API do token de recurso de hello. Preencha Olá configurações do aplicativo a seguir:

    * accountUrl - URL de conta de banco de dados do Azure Cosmos Olá na guia de chaves de saudação da sua conta de banco de dados do Azure Cosmos.
    * accountKey - chave de mestre de guia de chaves de saudação da sua conta de banco de dados do Azure Cosmos do hello Azure Cosmos DB conta.
    * databaseId e collectionId do seu banco de dados e coleção criados

3. Publica Olá ResourceTokenBroker solução tooyour criado site da Web.

4. Abra o projeto do Xamarin hello e navegue tooTodoItemManager.cs. Preencha valores hello para accountURL, collectionId, databaseId, bem como resourceTokenBrokerURL como Olá base https url para o site de broker token de recurso hello.

5. Olá completa [como tooconfigure seu logon do Facebook do serviço de aplicativo aplicativo toouse](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup tutorial a autenticação do Facebook e configurar Olá ResourceTokenBroker site.

    Execute o aplicativo Xamarin de saudação.

## <a name="review-slas-in-hello-azure-portal"></a>Examine os SLAs em Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir: 

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação você acabou de criar. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie uma coleção usando Olá Explorador de dados e criar e implantar um aplicativo Xamarin. Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais. 

> [!div class="nextstepaction"]
> [Importar dados no Azure Cosmos DB](import-data.md)
