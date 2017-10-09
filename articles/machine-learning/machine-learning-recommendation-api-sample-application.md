---
title: "aaaCommon operações na API de recomendações de aprendizado de máquina da saudação | Microsoft Docs"
description: "Aplicativo de exemplo de recomendação do Azure ML"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>Passo a passo do aplicativo de exemplo da API de Recomendações
> [!NOTE]
> Deve começar a usar o hello recomendações API cognitivas serviço em vez de nesta versão. Olá serviço cognitivas recomendações será substituído por esse serviço e todos os novos recursos de saudação serão desenvolvidos existe. Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.
> Saiba mais sobre [toohello migrando novo serviço cognitivas](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>Finalidade
Este documento mostra o uso de saudação de hello Azure recomendações de aprendizado de máquina API por meio de um [aplicativo de exemplo](https://code.msdn.microsoft.com/Recommendations-144df403).

Este aplicativo não é pretendido tooinclude a funcionalidade completa, nem usa Olá todas as APIs. Ele demonstra alguns tooperform operações comuns quando desejar primeiro tooplay com hello serviço de recomendação de aprendizado de máquina. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a>Introdução tooMachine serviço de recomendação de aprendizado
Recomendações via Olá serviço de recomendação de aprendizado de máquina são habilitadas quando você cria um modelo de recomendação com base em Olá seguintes dados:

* Um repositório de itens de saudação desejado toorecommend, também conhecido como um catálogo
* Dados que representa o uso de saudação de itens por usuário ou sessão (Isso pode ser adquirido ao longo do tempo por meio de aquisição de dados, não como parte do aplicativo de exemplo hello)

Depois que um modelo de recomendação é criado, você pode usá-lo toopredict itens que um usuário pode ser interessantes, de acordo com tooa Usuári de saudação do conjunto de itens (ou um único item).

tooenable Olá cenário anterior, faça seguinte Olá Olá serviço de recomendação de aprendizado de máquina:

* Criar um modelo: Este é um contêiner lógico que contém dados de saudação (catálogo e uso) e modelos de previsão de saudação. Cada contêiner do modelo é identificado por uma ID exclusiva, que é alocada quando ele é criado. Essa ID é chamada hello ID de modelo e ele é usado pela maioria dos Olá APIs. 
* Carregar toocatalog: quando um contêiner de modelo é criado, você pode associar tooit um catálogo.

**Observação**: criar um modelo e carregar o catálogo tooa normalmente são executadas uma vez para o ciclo de vida do hello modelo.

* Carregar uso: Isso adiciona o contêiner do modelo de toohello de dados de uso.
* Criar um modelo de recomendação: depois que você tem dados suficientes, você pode criar o modelo de recomendação de saudação. Essa operação usa toocreate de algoritmos de aprendizado de máquina superior do hello um modelo de recomendação. Cada compilação está associada a uma ID exclusiva. É necessário tookeep um registro dessa ID porque ele é necessário para a funcionalidade de saudação de algumas APIs.
* Processo de criação de saudação de monitor: uma compilação do modelo de recomendação é uma operação assíncrona, e pode levar de minutos tooseveral horas, dependendo da quantidade de saudação de dados (catálogo e uso) e Olá parâmetros de compilação. Portanto, você precisa de compilação de saudação toomonitor. Um modelo de recomendação será criado apenas se sua compilação associada for concluída com êxito.
* (Opcional) Escolha uma compilação de modelo de recomendação ativa. Essa etapa será necessária apenas se você tiver mais de um modelo de recomendação integrado a seu contêiner do modelo. Solicitação tooget recomendações sem indicando que o modelo de recomendação active Olá será redirecionado automaticamente pela compilação active do hello sistema toohello padrão. 

**Observação**: um modelo de recomendação ativo está pronto para produção e foi projetado para cargas de trabalho de produção. Isso difere de um modelo de recomendação inativo, que permanece em um ambiente de teste (às vezes chamado de preparo).

* Obtenha recomendações: depois que tiver um modelo de recomendação, você poderá disparar recomendações para um único item ou uma lista de itens selecionados. 

Você normalmente invocará Obter Recomendação por determinado período de tempo. Durante esse período de tempo, você pode redirecionar os dados de uso toohello sistema de recomendação de aprendizado de máquina, o que adiciona esse contêiner de modelo especificado de toohello de dados. Quando você tem dados suficientes uso, você pode criar um novo modelo de recomendação que incorpora os dados de uso adicional de saudação. 

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2013 ou posterior.
* Acesso à Internet 
* Assinatura toohello recomendações API (https://datamarket.azure.com/dataset/amla/recommendations).

## <a name="azure-machine-learning-sample-app-solution"></a>Solução de aplicativo de exemplo do Azure Machine Learning
Esta solução contém o código-fonte hello, exemplo de uso, o arquivo de catálogo e diretivas toodownload Olá pacotes que são necessários para a compilação.

## <a name="hello-apis-used"></a>Olá APIs usadas
aplicativo Hello usa a funcionalidade de recomendação de aprendizado de máquina por meio de um subconjunto das APIs disponíveis. Olá que APIs a seguir são demonstradas no aplicativo hello:

* Criar modelo: criar um contêiner lógico toohold modelos de dados e a recomendação. Um modelo é identificado por um nome, e você não pode criar mais de um modelo com hello mesmo nome.
* Carregar arquivo de catálogo: usar dados de catálogo tooupload.
* Carregar arquivo de uso: dados de uso de tooupload.
* Disparar build: usar toocreate um modelo de recomendação.
* Monitorar a execução de compilação: usar toomonitor Olá status de uma versão de modelo de recomendação.
* Escolha um modelo interno de recomendação: usar tooindicate quais toouse de modelo de recomendação por padrão para um determinado contêiner de modelo. Essa etapa é necessária somente se você tiver mais de um modelo de recomendação e você desejar tooactivate não ativo de compilação como modelo de recomendação active hello.
* Obter recomendação: usar tooretrieve itens de acordo com o tooa determinado item único ou um conjunto de itens recomendado. 

Para obter uma descrição completa da saudação APIs, consulte a documentação do Microsoft Azure Marketplace de hello. 

**Observação**: um modelo pode ter várias compilações ao longo do tempo (não simultaneamente). Cada compilação foi criada com hello mesmo ou atualizada catálogo e dados de uso adicionais.

## <a name="common-pitfalls"></a>Armadilhas comuns
* Você precisará tooprovide seu nome de usuário e o aplicativo de exemplo do Microsoft Azure Marketplace conta primária toorun chave hello.
* Aplicativo de exemplo hello em execução consecutivamente falhará. fluxo do aplicativo Hello inclui criar, carregamento, criação de monitor de saudação e obter recomendações de um modelo predefinido; Portanto, haverá falha na execução consecutiva se você não alterar o nome do modelo Olá entre invocações.
* Recomendações podem ser retornadas sem dados. aplicativo de exemplo Hello usa um arquivo de catálogo e uso muito pequeno. Portanto, alguns itens do catálogo de saudação não terá nenhum itens recomendados.

## <a name="disclaimer"></a>Isenção de responsabilidade
aplicativo de exemplo Hello não é pretendido toobe executado em um ambiente de produção. dados Olá fornecidos no catálogo de saudação são muito pequenos, e não fornecerá um modelo de recomendação significativo. dados de saudação são fornecidos como uma demonstração. 

