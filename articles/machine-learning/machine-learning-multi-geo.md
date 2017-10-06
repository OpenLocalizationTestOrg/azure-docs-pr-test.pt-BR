---
title: "documentação da Ajuda aaaMulti geográfica | Microsoft Docs"
description: "Saiba como toocreate um espaço de trabalho e publicar um serviço da web em uma região do Azure diferente da saudação Sul Central dos Estados Unidos (SCUS) região do Azure."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a>Documentação da Ajuda para diversas áreas geográficas
Este artigo descreve como você pode criar um espaço de trabalho e publicar um serviço Web em diferentes regiões do Azure.  Olá [produtos do Azure pela página de região](https://azure.microsoft.com/en-us/regions/services/) lista de regiões em que o aprendizado de máquina do Azure está disponível.

## <a name="create-a-workspace"></a>Criar um espaço de trabalho
1. Entrar toohello Portal clássico do Azure.
2. Clique em **+ NOVO** > **SERVIÇOS DE DADOS** > **ACHINE LEARNING** > **CRIAÇÃO RÁPIDA**.  Em **LOCAL**, selecione outra região, como **Sudeste Asiático**.
   ![Imagem de Ajuda de várias áreas geográficas 1][1]
3. Selecione o espaço de trabalho hello e, em seguida, clique em **tooML entrar Studio**.
   ![Imagem de Ajuda de várias áreas geográficas 2][2]
4. Agora você tem um espaço de trabalho em outra região que pode usar como qualquer outro espaço de trabalho. tooswitch entre seus espaços de trabalho, procure toohello superior direito da tela. Clique em Olá suspensa, selecione Olá região e espaço de trabalho, em seguida, selecione Olá. Tudo o que é a região de espaço de trabalho de toohello local.  Por exemplo, todos os serviços web criados a partir de um espaço de trabalho será em Olá mesmo espaço de trabalho de saudação de região está localizado em.
   ![Imagem de Ajuda de várias áreas geográficas 3][3]

## <a name="open-an-experiment-from-gallery"></a>Abrir um experimento da Galeria
Se você abrir um experimento da galeria, você também pode selecionar a região que você deseja toocopy Olá experimento.

![Imagem de Ajuda de várias áreas geográficas 4][4a]

## <a name="web-service-management"></a>Gerenciamento de serviço Web
tooprogrammatically gerenciar serviços da web, como para treinamento, usar Olá específica da região endereço:

* https://asiasoutheast.management.azureml.net
* https://europewest.management.azureml.net

### <a name="things-toonote"></a>Coisas toonote
1. Você só pode copiar experiências entre espaços de trabalho que pertencem a toohello mesma região dessa maneira. Se você precisar de experiência de toocopy em espaços de trabalho em regiões diferentes, você pode usar o hello [PowerShell](http://aka.ms/amlps) commandlet [ *cópia AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish que. Outra solução alternativa é toopublish Olá experiência na galeria no modo não listado, abri-lo no espaço de trabalho de saudação do hello outra região.
2. seletor de região Olá mostrará apenas os espaços de trabalho para uma região de cada vez.  
3. Um espaço de trabalho livre ou de acesso de convidado (anônimo) será criado e hospedado no Centro-Sul dos EUA  
4. Os serviços Web implantados por meio de um espaço de trabalho no Sudeste Asiático também serão hospedados no Sudeste Asiático.  

## <a name="more-information"></a>Mais informações
Fazer uma pergunta sobre Olá [Fórum de aprendizado de máquina do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
