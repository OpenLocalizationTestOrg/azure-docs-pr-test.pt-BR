---
title: "aaaConnect tooa serviço de Web de aprendizado de máquina | Microsoft Docs"
description: "Com o c# ou Python, conecte-se tooan serviço da Web de aprendizado de máquina do Azure usando uma chave de autorização."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a>Conecte-se tooan serviço de Web de aprendizado de máquina do Azure
Olá experiência do desenvolvedor de aprendizado de máquina do Azure é um previsões de toomake de API de serviço Web de dados de entrada em tempo real ou em modo de lote. Use previsões de toocreate do estúdio de aprendizado de máquina do Azure e implantar um serviço Web de aprendizado de máquina do Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

toolearn sobre como toocreate e implantar um serviço Web de aprendizado de máquina usando o estúdio de aprendizado de máquina:

* Para obter um tutorial sobre como toocreate um experimento no estúdio de aprendizado de máquina, consulte [criar sua primeira experiência](machine-learning-create-experiment.md).
* Para obter detalhes sobre como toodeploy um serviço Web, consulte [implantar um serviço Web de aprendizado de máquina](machine-learning-publish-a-machine-learning-web-service.md).
* Para obter mais informações sobre o aprendizado de máquina em geral, visite Olá [Centro de documentação de aprendizado de máquina](https://azure.microsoft.com/documentation/services/machine-learning/).

## <a name="azure-machine-learning-web-service"></a>Serviço Web do Azure Machine Learning
Com hello serviço da Web de aprendizado de máquina do Azure, um aplicativo externo se comunica com um modelo de pontuação de fluxo de trabalho do aprendizado de máquina em tempo real. Uma chamada de serviço Web de aprendizado de máquina retorna resultados da previsão aplicativo externo tooan. toomake uma chamada de serviço Web de aprendizado de máquina, você passar uma chave de API que é criada quando você implanta uma previsão. Olá serviço Web de aprendizado de máquina é baseado em REST, uma opção de populares de arquitetura para projetos de programação da web.

O Azure Machine Learning tem dois tipos de serviços:

* Serviço de solicitação-resposta (RR) – uma baixa latência, um serviço altamente escalonável que fornece uma interface modelos sem monitoração de estado de toohello criado e implantado a partir de saudação estúdio de aprendizado de máquina.
* Serviço de Execução de Lote (BES) – Um serviço assíncrono que pontua um lote de registros de dados.

Para obter mais informações sobre os serviços Web do Machine Learning, confira [Implantar um serviço Web do Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Obtenha uma chave de autorização de Azure Machine Learning
Quando você implanta sua experiência, chaves de API são geradas para Olá serviço da Web. Você pode recuperar chaves de saudação em vários locais.

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>No portal de serviços Web de aprendizado de máquina do Microsoft Azure Olá
Entrar toohello [serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net) portal.

chave de API de saudação tooretrieve para um serviço Web de aprendizado de máquina novo:

1. No portal de serviços de Web de aprendizado de máquina do Azure hello, clique em **serviços Web** menu superior hello.
2. Clique em Olá Web service para o qual deseja que o tooretrieve Olá da chave.
3. Clique no menu superior Olá **consumir**.
4. Copie e salve Olá **chave primária**.

chave de API de saudação tooretrieve para um serviço Web de aprendizado de máquina clássico:

1. No portal de serviços de Web de aprendizado de máquina do Azure hello, clique em **Web Services clássico** menu superior hello.
2. Clique em Olá Web service com a qual você está trabalhando.
3. Clique em ponto de extremidade de saudação do qual você deseja tooretrieve chave de saudação.
4. Clique no menu superior Olá **consumir**.
5. Copie e salve Olá **chave primária**.

### <a name="classic-web-service"></a>Serviço Web Clássico
 Você também pode recuperar uma chave para um serviço Web clássico do estúdio de aprendizado de máquina ou hello portal clássico do Azure.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. No estúdio de aprendizado de máquina, clique em **serviços WEB** Olá esquerda.
2. Clique em um serviço Web. Olá **chave API** está em Olá **painel** guia.

#### <a name="azure-classic-portal"></a>portal clássico do Azure
1. Clique em **APRENDIZADO de máquina** Olá esquerda.
2. Clique em espaço de trabalho de saudação em que o serviço da Web está localizado.
3. Clique em **SERVIÇOS WEB**.
4. Clique em um serviço Web.
5. Clique em um ponto de extremidade. Olá "Chave de API" está inativo no hello inferior direito.

## <a id="connect"></a>Conecte-se o serviço da Web de aprendizado de máquina de tooa
Você pode conectar tooa serviço Web de aprendizado de máquina usando qualquer linguagem de programação que dá suporte à resposta e solicitação HTTP. Você pode exibir exemplos em C#, Python e R de uma página de ajuda do serviço Web do Machine Learning.

**Ajuda da API do Machine Learning** Uma ajuda de API do Machine Learning é criada quando você implanta um serviço Web. Confira [Passo a passo do Azure Machine Learning – Implantar serviço Web](machine-learning-walkthrough-5-publish-web-service.md).
Olá ajuda da API de aprendizado de máquina contém detalhes sobre um serviço Web de previsão.

1. Clique em Olá Web service com a qual você está trabalhando.
2. Clique em ponto de extremidade de saudação do qual você deseja tooview Olá a página de ajuda de API.
3. Clique no menu superior Olá **consumir**.
4. Clique em **página de Ajuda da API** em Olá solicitação-resposta ou pontos de extremidade de execução de lote.

**ajudar a API de aprendizado de máquina tooview para um serviço Web de novo**

Em hello Azure Machine Learning Web Services Portal:

1. Clique em **serviços WEB** no menu superior hello.
2. Clique em Olá Web service para o qual deseja que o tooretrieve Olá da chave.

Clique em **consumir** tooget hello URIs para hello Reposonse de solicitação e serviços de execução de lote e código de exemplo em c#, R e Python.

Clique em **Swagger API** tooget Swagger documentação com base para Olá APIs chamada de hello fornecido URIs.

### <a name="c-sample"></a>Exemplo de C#
tooconnect tooa serviço Web de aprendizado de máquina, use uma **HttpClient** passando ScoreData. ScoreData contém um FeatureVector, um vetor de n-dimensional de recursos numéricos que representa Olá ScoreData. Autenticar o serviço de aprendizado de máquina toohello com uma chave de API.

Olá tooconnect tooa serviço Web de aprendizado de máquina, **Microsoft.AspNet.WebApi.Client** pacote NuGet deve ser instalado.

**Instalar o Nuget Microsoft.AspNet.WebApi.Client no Visual Studio**

1. Publicar o conjunto de dados de Download de saudação do UCI: 2 adulto classe dataset serviço da Web.
2. Clique em **Ferramentas** > **Gerenciador de Pacotes do NuGet** > **Console do Gerenciador de Pacotes**.
3. Escolha **Install-Package Microsoft.AspNet.WebApi.Client**.

**exemplo de código toorun Olá**

1. Publicar "exemplo 1: baixar o conjunto de dados do UCI: conjunto de dados de classe adulto 2" experimento, parte da saudação coleção de aprendizado de máquina de exemplo.
2. Atribua apiKey com chave de saudação de um serviço Web. Confira a seção acima **Obter uma chave de autorização de Azure Machine Learning** .
3. Atribua serviceUri com hello URI da solicitação.

### <a name="python-sample"></a>Exemplo de Python
tooconnect tooa serviço Web de aprendizado de máquina, use Olá **urllib2** passando ScoreData de biblioteca. ScoreData contém um FeatureVector, um vetor de n-dimensional de recursos numéricos que representa Olá ScoreData. Autenticar o serviço de aprendizado de máquina toohello com uma chave de API.

**exemplo de código toorun Olá**

1. Implantar "exemplo 1: baixar o conjunto de dados do UCI: conjunto de dados de classe adulto 2" experimento, parte da saudação coleção de aprendizado de máquina de exemplo.
2. Atribua apiKey com chave de saudação de um serviço Web. Consulte Olá **obter uma chave de autorização de aprendizado de máquina do Azure** seção próximo início Olá deste artigo.
3. Atribua serviceUri com hello URI da solicitação.

