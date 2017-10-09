---
title: "aaaManage experimentar iterações no estúdio de aprendizado de máquina | Microsoft Docs"
description: "Como toomanage experimentar iterações no estúdio de aprendizado de máquina do Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>Gerenciar iterações de teste no Machine Learning Studio do Microsoft Azure
Desenvolvendo um modelo de análise de previsão é um processo iterativo - conforme você modificar Olá várias funções e os parâmetros de sua experiência, seus resultados convergirem até ficar satisfeito que você tenha um modelo treinado e eficiente. Processo de toothis da chave é controle Olá várias iterações de seus parâmetros de teste e configurações.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Você pode examinar as execuções anteriores de suas experiências a qualquer momento na ordem toochallenge, revisitar e, por fim, confirme ou refinar suposições anteriores. Quando você executa um teste, o estúdio de aprendizado de máquina mantém um histórico dos Olá executar, incluindo o conjunto de dados, o módulo e conexões de porta e parâmetros. Esse histórico também captura resultados, informações de tempo de execução, como tempos de início e parada, mensagens de log e status de execução. Você pode examinar novamente qualquer uma dessas execuções em qualquer ordem cronológica a saudação tempo tooreview de sua experiência e os resultados intermediários. Você pode até usar uma execução anterior toolaunch sua experiência em uma nova fase da consulta e a descoberta em seu caminho toocreating simples, complexos ou até mesmo de ensemble soluções de modelagem.

> [!NOTE]
> Quando você exibir uma execução anterior de um experimento, essa versão do experimento hello está bloqueado e não pode ser editado. No entanto, você pode salvar uma cópia dele clicando **Salvar como** e fornecendo um novo nome para a cópia de saudação. O estúdio de aprendizado de máquina abre Olá nova cópia, o que você pode editar e executar. Esta cópia do seu teste está disponível no hello **experiências** lista juntamente com todas as suas experiências.
> 
> 

## <a name="viewing-hello-prior-run"></a>Exibindo Olá executar anterior
Quando você abriu um experimento que você tiver executado pelo menos uma vez, você pode exibir hello anterior a execução de teste de saudação clicando **anteriores executar** no painel de propriedades de saudação.

Por exemplo, suponha que você crie um teste e execute versões dele às 11h23 11h42 e 11h55. Se você abrir a última execução de saudação do experimento hello (11:55) e clique em **anteriores executar**, versão Olá executou em 11:42 é aberto.

## <a name="viewing-hello-run-history"></a>Olá exibindo histórico de execução
Você pode exibir todas as execuções de saudação anterior de um experimento clicando **exibir o histórico de execução** em um experimento aberto.

Por exemplo, suponha que você crie uma experiência com hello [Regressão Linear] [ linear-regression] módulo e você desejar tooobserve efeito de saudação de alterar o valor de saudação do **taxa de aprendizagem** em os resultados de teste. Você executar Olá teste várias vezes com valores diferentes para esse parâmetro, da seguinte maneira:

| Valor da Taxa de aprendizado | Hora de início da execução |
| --- | --- |
| 0,1 |11/09/2014 16h18min58s |
| 0,2 |11/09/2014 16h24min33s |
| 0,4 |11/09/2014 16h28min36s |
| 0,5 |11/09/2014 16h33min31s |

Se clicar em **EXIBIR O HISTÓRICO DE EXECUÇÃO**, você verá uma lista de todas essas execuções:

![Exemplo de histórico de execução][runhistory]

Clique em qualquer um desses tooview executa um instantâneo de saudação experiências em tempo de saudação você executou. Hello configuração, os valores de parâmetro, comentários e resultados são todos preservado toogive é um registro completo de executados de sua experiência.

> [!TIP]
> toodocument seu iterações de teste hello, você pode modificar Olá título cada vez que você executá-lo, você pode atualizar Olá **resumo** de saudação experimentar no painel de propriedades Olá, e você pode adicionar ou atualizar os comentários em módulos individuais toorecord suas alterações. comentários de título, o resumo e o módulo de saudação são salvos com cada execução de teste de saudação.
> 
> 

lista de saudação de experiências na Olá **experiências** guia no estúdio de aprendizado de máquina sempre exibe a versão mais recente de saudação de um experimento. Se você abrir uma execução anterior do experimento hello (usando **anteriores executar** ou **exibir o histórico de execução**), você pode retornar a versão de rascunho toohello clicando **exibir o histórico de execução** e selecionando Olá iteração que tem um **estado** de **editável**.

## <a name="iterating-on-a-previous-run"></a>Iterando sobre uma Execução anterior
Quando clicar em **Execução anterior** ou em **EXIBIR O HISTÓRICO DE EXECUÇÃO** e abrir uma execução anterior, você poderá exibir um teste concluído no modo somente leitura.

Se você quiser toobegin uma iteração de sua experiência, começando com a forma de saudação configurado para uma execução anterior, você pode fazer isso abrindo Olá executar e clicando em **Salvar como**. Isso cria um novo teste, com um novo título, um histórico de execução vazio e todos os componentes de saudação e valores de parâmetro de saudação anterior executar. Esse novo teste é listado na Olá **experiências** guia na home page do hello estúdio de aprendizado de máquina e você pode modificar e histórico para essa iteração de sua experiência de executá-lo, iniciando uma nova execução. 

Por exemplo, suponha que você tiver experiência Olá mostrado na seção anterior de saudação do histórico de execução. Você deseja tooobserve o que acontece quando você definir Olá **taxa de aprendizagem** too0.4 de parâmetro e tente diferentes valores para Olá **número de épocas de treinamento** parâmetro.

1. Clique em **exibir o histórico de execução** e abra a iteração de saudação do experimento Olá executado às 4:28:36 (no qual você define Olá too0.4 de valor de parâmetro).
2. Clique em **SALVAR COMO**.
3. Digite um novo título e clique em Olá **Okey** marca de seleção. Uma nova cópia do experimento Olá é criada.
4. Modificar Olá **número de épocas de treinamento** parâmetro.
5. Clique em **EXECUTAR**.

Agora você pode continuar toomodify e executar essa versão de sua experiência, criando um novo toorecord de histórico de execução de seu trabalho.

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
