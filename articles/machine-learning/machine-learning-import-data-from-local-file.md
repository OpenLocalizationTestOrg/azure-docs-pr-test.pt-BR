---
title: "aaaImport dados de um arquivo para o estúdio de aprendizado de máquina do Azure | Microsoft Docs"
description: "Saiba como tooupload um dados de treinamento do arquivo de sua unidade de disco rígido de tooAzure estúdio de aprendizado de máquina. Isso cria um módulo de conjunto de dados no espaço de trabalho de saudação."
keywords: importar dados, formato de dados, tipos de dados, fontes de dados, dados de treinamento
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>Importar dados de treinamento de um arquivo no disco rígido para o Machine Learning Studio
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Saiba como tooupload dados de um arquivo de sua unidade de disco rígido toouse como dados de treinamento no estúdio de aprendizado de máquina do Azure. Importando o arquivo de dados hello, você tem um módulo de conjunto de dados pronto para uso no seu espaço de trabalho.

## <a name="steps-tooimport-data-from-a-local-file"></a>Dados de tooimport de etapas de um arquivo local
tooimport dados de uma unidade de disco rígido local, Olá a seguir:

1. Clique em **+ novo** na parte inferior da saudação da janela do estúdio de aprendizado de máquina hello.
2. Selecione **CONJUNTO DE DADOS** e **DO ARQUIVO LOCAL**.
3. Em Olá **carregar um novo conjunto de dados** caixa de diálogo, procurar toohello arquivo a ser tooupload
4. Insira um nome, identifique o tipo de dados hello e, opcionalmente, insira uma descrição. Uma descrição é recomendada - permite que você toorecord quaisquer características sobre dados Olá que você deseja tooremember quando usando dados Olá Olá futuro.
5. Olá a caixa de seleção **isso é Olá nova versão de um conjunto de dados existente** permite que você tooupdate um conjunto de dados existente com novos dados. Clique nesta caixa de seleção e, em seguida, digite o nome de saudação de um conjunto de dados existente.

![Carregar um novo conjunto de dados](media/machine-learning-import-data-from-local-file/upload-dataset.png)

Durante o upload, você verá uma mensagem informando que seu arquivo está sendo carregado. Carregar tempo depende do tamanho de saudação de seu dados e Olá a velocidade de seu serviço de toohello de conexão. Se você souber que o arquivo hello levará um longo tempo, você pode fazer outras coisas dentro do estúdio de aprendizado de máquina enquanto você espera. No entanto, fechar o navegador Olá faz com que o hello toofail de carregamento de dados.

## <a name="dataset-module-is-ready-for-use"></a>O módulo do conjunto de dados está pronto para uso
Depois que seus dados são carregados, ele é armazenado em um módulo de conjunto de dados e é experiência tooany disponíveis no espaço de trabalho.

Quando você estiver editando um experimento, você pode encontrar hello conjuntos de dados que você criou no hello **Meus conjuntos de dados** lista sob Olá **conjuntos de dados salvos** lista na paleta de módulo hello. Você pode arrastar e soltar dataset de saudação em tela de experimento hello quando você desejar toouse Olá dataset para análise adicional e aprendizado de máquina.
