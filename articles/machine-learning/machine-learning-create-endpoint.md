---
title: "pontos de extremidade de serviço Web de aaaCreating no aprendizado de máquina | Microsoft Docs"
description: "Criando pontos de extremidade de serviço Web no Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>Criando pontos de extremidade
> [!NOTE]
>  Este tópico descreve tooa aplicável técnicas **clássico** serviço Web de aprendizado de máquina.
> 
> 

Quando você cria serviços Web que vende forward tooyour clientes, é necessário ao tooeach cliente tooprovide modelos treinados que são ainda vinculado toohello experimento de quais Olá Web serviço foi criado. Além disso, todas as atualizações experimento toohello deve ser aplicadas seletivamente tooan de ponto de extremidade sem substituir personalizações hello.

tooaccomplish, aprendizado de máquina do Azure permite que você toocreate vários pontos de extremidade para um serviço Web implantado. Cada ponto de extremidade no hello serviço Web é abordado, limitado e gerenciado independentemente. Cada ponto de extremidade é uma chave exclusiva de autorização e a URL que você pode distribuir tooyour clientes.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>Adicionando pontos de extremidade tooa Web serviço
Há três tooadd de maneiras tooa um ponto de extremidade serviço da Web.

* Programaticamente
* Portal de serviços de Web de aprendizado de máquina do Azure Olá
* Embora Olá portal clássico do Azure

Depois que o ponto de extremidade de saudação é criado, você pode consumi-lo por meio de APIs síncrono, o lote APIs e planilhas do excel. Além disso tooadding pontos de extremidade por meio desta interface do usuário, você também pode usar Olá APIs de gerenciamento do ponto de extremidade tooprogrammatically adicionar pontos de extremidade.

> [!NOTE]
> Se você adicionar mais pontos de extremidade toohello serviço da Web, você não pode excluir o ponto de extremidade do saudação padrão.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Adicionando um ponto de extremidade programaticamente
Você pode adicionar um serviço Web de tooyour de ponto de extremidade programaticamente usando Olá [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de exemplo.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Adicionar um ponto de extremidade usando o portal de serviços de Web de aprendizado de máquina do Azure Olá
1. No estúdio de aprendizado de máquina, na coluna de navegação à esquerda do hello, clique em serviços da Web.
2. Na parte inferior de saudação do painel de serviço Web hello, clique em **gerenciar pontos de extremidade**. portal de serviços de Web de aprendizado de máquina do Azure Olá abre a página de pontos de extremidade de toohello de saudação serviço da Web.
3. Clique em **Novo**.
4. Digite um nome e uma descrição para o novo ponto de extremidade de saudação. Os nomes dos pontos de extremidade devem ter 24 caracteres ou menos e devem ser compostos de letras minúsculas ou números. Selecione o nível de log hello e se os dados de exemplo estão habilitados. Para obter mais informações sobre registro em log, veja [Habilitar o log de serviços Web de Machine Learning](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Adicionar um ponto de extremidade usando Olá portal clássico do Azure
1. Entrar toohello [portal clássico do Azure](http://manage.windowsazure.com), clique em **aprendizado de máquina** na coluna esquerda hello. Clique em espaço de trabalho de saudação que contém o serviço Web de saudação no qual você está interessado.
   
    ![Navegue tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. Clique em **Serviços Web**.
   
    ![Navegue tooWeb serviços](./media/machine-learning-create-endpoint/figure-2.png)
3. Clique em Olá Web service estiver interessado na lista de saudação toosee de pontos de extremidade disponíveis.
   
    ![Navegue tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. Final Olá Olá página, clique em **Adicionar ponto de extremidade**. Digite um nome e descrição, certifique-se de que não há nenhum outros pontos de extremidade com hello mesmo nome neste serviço da Web. Deixe o nível de limitação de saudação com seu valor padrão a menos que você tenha requisitos especiais. toolearn mais sobre a limitação, consulte [pontos de extremidade de API de dimensionamento](machine-learning-scaling-webservice.md).
   
    ![Criar ponto de extremidade](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Próximas etapas
[Como um serviço Web de aprendizado de máquina do Azure de tooconsume](machine-learning-consume-web-services.md).

