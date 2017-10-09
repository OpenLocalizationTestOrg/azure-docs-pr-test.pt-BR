---
title: "um serviço de Web do aprendizado de máquina do Excel de aaaConsume | Microsoft Docs"
description: "Consumir um serviço Web de Azure Machine Learning do Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Consumindo um Serviço Web de Azure Machine Learning do Excel
 O estúdio de aprendizado de máquina do Azure torna fácil toocall os serviços da web diretamente do Excel sem Olá necessidade toowrite qualquer código.

Se você estiver usando o Excel 2013 (ou posterior) ou o Excel Online, recomendamos que você use Olá Excel [suplemento Excel](machine-learning-excel-add-in-for-web-services.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>Etapas
Publicar um serviço Web. [Esta página](machine-learning-walkthrough-5-publish-web-service.md) explica como toodo-lo. Atualmente o recurso de pasta de trabalho do Excel Olá só tem suporte para serviços de solicitação/resposta que têm uma única saída (ou seja, uma pontuação rótulo único). 

Uma vez que um serviço web, clique em Olá **serviços WEB** seção esquerda de saudação do studio hello e selecione Olá web serviço tooconsume do Excel.

**Serviço Web Clássico**

1. Em Olá **painel** guia para o serviço web de saudação é uma linha para Olá **solicitação/resposta** serviço. Se esse serviço tinha uma única saída, você deve ver Olá **baixar pasta de trabalho do Excel** link nessa linha.
   
    ![][1]
2. Clique em **Baixar Pasta de Trabalho do Excel**.

**Novo serviço Web**

1. No portal de serviço de Web de aprendizado de máquina do Azure hello, selecione **consumir**.
2. Na página de consumir hello, em Olá **opções de consumo do serviço da Web** seção, clique no ícone do Excel hello.

**Usando a pasta de trabalho Olá**

1. Pasta de trabalho aberta hello.
2. É exibido um aviso de segurança; Clique em Olá **habilitar edição** botão.
   
    ![][2]
3. Será exibido um Aviso de Segurança. Clique em Olá **Habilitar conteúdo** botão toorun macros na planilha.
   
    ![][3]
4. Depois que as macros estiverem habilitadas, uma tabela será gerada. Colunas em azul tem como entrada no hello RRS web serviço necessário, ou **parâmetros**. Observe a saída Olá Olá serviço RRS, **valores previstos** em verde. Quando todas as colunas para uma determinada linha são preenchidas, pasta de trabalho do hello automaticamente chama Olá API de pontuação e exibe o saudação resultados classificada.
   
    ![][4]
5. tooscore mais de uma linha, preenchimento Olá segunda linha com dados e hello prevista valores são gerados. Você pode até mesmo colar várias linhas ao mesmo tempo.

Você pode usar qualquer um dos recursos do Excel hello (gráficos, mapa de energia, condicional, formatação, etc.) com hello previsto valores toohelp visualizar dados saudação.    

## <a name="sharing-your-workbook"></a>Compartilhar sua pasta de trabalho
Para Olá macros toowork, sua chave de API deve ser parte da planilha de saudação. Isso significa que você deve compartilhar pasta de trabalho de saudação apenas com entidades/pessoas que confiáveis.

## <a name="automatic-updates"></a>Atualizações automáticas
É feita uma chamada RRS nessas duas situações:

1. Olá a primeira vez que uma linha tem o conteúdo em todas as suas **parâmetros**
2. Sempre que qualquer Olá **parâmetros** alterações em uma linha que tenha todos os seus **parâmetros** inserido.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
