---
title: "simultaneidade de tooincrease aaaHow de um serviço web de aprendizado de máquina do Azure | Microsoft Docs"
description: "Saiba como tooincrease simultaneidade de um aprendizado de máquina do Azure de serviço web com a adição de pontos de extremidade adicionais."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "aprendizado de máquina do azure, serviços Web, operacionalização, dimensionamento, ponto de extremidade, simultaneidade"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>Dimensionando um serviço Web do Azure Machine Learning adicionando mais pontos de extremidade
> [!NOTE]
> Este tópico descreve tooa aplicável técnicas **clássico** serviço Web de aprendizado de máquina. 
> 
> 

Por padrão, cada serviço Web publicado é configurado toosupport 20 solicitações simultâneas e pode ser de até 200 solicitações simultâneas. Enquanto Olá portal clássico do Azure fornece uma maneira tooset esse valor, aprendizado de máquina do Azure automaticamente otimiza Olá configuração tooprovide Olá melhor desempenho para o serviço web e valor portal Olá será ignorado. 

Se você planejar toocall Olá API com uma carga maior que dará suporte a um valor de chamadas simultâneas máx de 200, você deve criar vários pontos de extremidade em Olá mesmo serviço da Web. Você pode, então, distribuir a carga aleatoriamente entre todos eles.

Olá a expansão de um serviço Web é uma tarefa comum. Alguns motivos tooscale são toosupport mais de 200 solicitações simultâneas, aumentar a disponibilidade por meio de vários pontos de extremidade ou fornecer pontos de extremidade separados para o serviço web de saudação. Você pode aumentar a escala Olá adicionando pontos de extremidade adicionais para Olá mesmo serviço da Web por meio de [portal clássico do Azure](https://manage.windowsazure.com/) ou hello [serviço de Web de aprendizado de máquina do Azure](https://services.azureml.net/) portal.

Para saber mais sobre a adição de novos pontos de extremidade, consulte [Criando pontos de extremidade](machine-learning-create-endpoint.md).

Tenha em mente que pode ser prejudicial, se você não estiver chamando Olá API com uma taxa alta de forma correspondente usando uma contagem de alta simultaneidade. Talvez você veja esporádica tempos limite de e/ou picos na latência Olá se você colocar uma carga relativamente baixa em uma API configurada para alta carga.

Olá que APIs síncronas são geralmente usados em situações onde uma baixa latência é desejada. Latência aqui implica em tempo de saudação que demora para uma solicitação de toocomplete Olá API e não se responsabiliza por quaisquer atrasos de rede. Digamos que você tenha uma API com uma latência de 50 ms. toofully consomem a capacidade disponível Olá com alto nível de limitação e chamadas simultâneas máx. = 20, você precisa toocall essa API 20 * 1000 / 400 = 50 vezes por segundo. Um máximo de chamadas simultâneas de 200 estendendo isso ainda mais, permite que você toocall Olá API 4000 vezes por segundo, supondo que uma latência de 50 ms.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
