---
title: "suplemento aaaExcel para serviços Web de aprendizado de máquina | Microsoft Docs"
description: "Como toouse da Web de aprendizado de máquina do Azure services diretamente no Excel sem gravar qualquer código."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a>Suplemento do Excel para serviços Web de Azure Machine Learning
Excel torna fácil toocall os serviços da web diretamente sem Olá necessidade toowrite qualquer código.

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a>Etapas tooUse um serviço da web existente na pasta de trabalho de saudação

1. Olá abrir [arquivo do Excel de exemplo](http://aka.ms/amlexcel-sample-2), que contém Olá complemento do Excel e dados sobre em detrimento de passageiros Olá Titanic.
2. Escolha o serviço web de saudação clicando nele-"Titanic sobrevivente indicador (suplemento do Excel exemplo) [pontuação]" neste exemplo.
   
    ![Selecionar o serviço Web][01]
3. Isso leva você toohello **prever** seção.  Esta pasta de trabalho já contém dados de exemplo, mas para uma pasta de trabalho em branco você pode selecionar uma célula no Excel e clicar em **Usar dados de exemplo**.
4. Selecionar dados de saudação com cabeçalhos e clique em ícone de intervalo de dados de entrada hello.  Certifique-se de hello "Meus dados têm cabeçalhos" caixa está marcada.
5. Em **saída**, insira o número de célula Olá onde você deseja Olá toobe de saída, por exemplo "H1" aqui.
6. Clique em **Prever**.
   
    ![Seção Prever][02]

Implante um serviço Web ou use um serviço Web existente. Para obter mais informações sobre como implantar um serviço web, consulte [passo a passo etapa 5: implantar o serviço de Web de aprendizado de máquina do Azure Olá](machine-learning-walkthrough-5-publish-web-service.md).

Obter chave de API de saudação para o serviço web. O local em que você executa essa ação depende se você publicou um serviço Web Clássico do Machine Learning ou um Novo serviço Web do Machine Learning.

**Usar um serviço Web Clássico** 

1. No estúdio de aprendizado de máquina, clique em Olá **serviços WEB** seção no painel esquerdo do hello e, em seguida, selecione Olá web service.
   
    ![Selecione um serviço Web do Studio][04]
2. Copie a chave de API de Olá para o serviço da web de saudação.
   
    ![Chave de API do Studio][05]
3. Em Olá **painel** para serviço web de saudação, clique em Olá **solicitação/resposta** link.
4. Procure Olá **URI da solicitação** seção.  Copie e salve a URL de saudação.

> [!NOTE]
> Agora é possível toosign em Olá [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net) tooobtain portal chave de API de saudação para um serviço web de aprendizado de máquina clássico.
> 
> 

**Usar um Novo serviço Web**

1. Em Olá [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net) portal, clique **serviços Web**, em seguida, selecione o serviço da web. 
2. Clique em **Consumo**.
3. Procure Olá **informações básicas de consumo** seção. Copie e salve Olá **chave primária** e hello **solicitação-resposta** URL.

## <a name="steps-tooadd-a-new-web-service"></a>Etapas tooAdd um novo serviço da web

1. Implante um serviço Web ou use um serviço Web existente. Para obter mais informações sobre como implantar um serviço web, consulte [passo a passo etapa 5: implantar o serviço de Web de aprendizado de máquina do Azure Olá](machine-learning-walkthrough-5-publish-web-service.md).
2. Clique em **Consumo**.
3. Procure Olá **informações básicas de consumo** seção. Copie e salve Olá **chave primária** e hello **solicitação-resposta** URL.
4. No Excel, vá toohello **serviços Web** seção (se você estiver no hello **prever** seção, clique em Olá seta Voltar toogo toohello lista de serviços da web).
   
    ![Vá tooWeb seleção de serviço][03]
5. Clique em **Adicionar Serviço Web**.
6. Cole URL Olá Olá rotulada de caixa de texto de suplemento do Excel **URL**.
7. Chave de API/primário Olá colar na caixa de texto de saudação rotulada **chave API**.
8. Clique em **Adicionar**.
   
    ![URL e chave de API para um serviço Web clássico.][06]
9. toouse serviço de web Olá, siga Olá anterior direções, "Etapas tooUse um serviço da web do existente."

## <a name="sharing-your-workbook"></a>Compartilhar sua pasta de trabalho
Se você salvar sua pasta de trabalho, chave de API/primário Olá Olá serviços da web que você adicionou também serão salvos. Isso significa que você somente deve compartilhar pasta de trabalho de saudação com pessoas que confiáveis.

Qualquer perguntas em Olá seguinte seção de comentários ou, no nosso [fórum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
