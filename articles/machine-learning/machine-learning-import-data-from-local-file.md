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
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="a87df-105">Importar dados de treinamento de um arquivo no disco rígido para o Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="a87df-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="a87df-106">Saiba como tooupload dados de um arquivo de sua unidade de disco rígido toouse como dados de treinamento no estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="a87df-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="a87df-107">Importando o arquivo de dados hello, você tem um módulo de conjunto de dados pronto para uso no seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a87df-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="a87df-108">Dados de tooimport de etapas de um arquivo local</span><span class="sxs-lookup"><span data-stu-id="a87df-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="a87df-109">tooimport dados de uma unidade de disco rígido local, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a87df-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="a87df-110">Clique em **+ novo** na parte inferior da saudação da janela do estúdio de aprendizado de máquina hello.</span><span class="sxs-lookup"><span data-stu-id="a87df-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="a87df-111">Selecione **CONJUNTO DE DADOS** e **DO ARQUIVO LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="a87df-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="a87df-112">Em Olá **carregar um novo conjunto de dados** caixa de diálogo, procurar toohello arquivo a ser tooupload</span><span class="sxs-lookup"><span data-stu-id="a87df-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="a87df-113">Insira um nome, identifique o tipo de dados hello e, opcionalmente, insira uma descrição.</span><span class="sxs-lookup"><span data-stu-id="a87df-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="a87df-114">Uma descrição é recomendada - permite que você toorecord quaisquer características sobre dados Olá que você deseja tooremember quando usando dados Olá Olá futuro.</span><span class="sxs-lookup"><span data-stu-id="a87df-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="a87df-115">Olá a caixa de seleção **isso é Olá nova versão de um conjunto de dados existente** permite que você tooupdate um conjunto de dados existente com novos dados.</span><span class="sxs-lookup"><span data-stu-id="a87df-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="a87df-116">Clique nesta caixa de seleção e, em seguida, digite o nome de saudação de um conjunto de dados existente.</span><span class="sxs-lookup"><span data-stu-id="a87df-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![Carregar um novo conjunto de dados](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="a87df-118">Durante o upload, você verá uma mensagem informando que seu arquivo está sendo carregado.</span><span class="sxs-lookup"><span data-stu-id="a87df-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="a87df-119">Carregar tempo depende do tamanho de saudação de seu dados e Olá a velocidade de seu serviço de toohello de conexão.</span><span class="sxs-lookup"><span data-stu-id="a87df-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="a87df-120">Se você souber que o arquivo hello levará um longo tempo, você pode fazer outras coisas dentro do estúdio de aprendizado de máquina enquanto você espera.</span><span class="sxs-lookup"><span data-stu-id="a87df-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="a87df-121">No entanto, fechar o navegador Olá faz com que o hello toofail de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="a87df-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="a87df-122">O módulo do conjunto de dados está pronto para uso</span><span class="sxs-lookup"><span data-stu-id="a87df-122">Dataset module is ready for use</span></span>
<span data-ttu-id="a87df-123">Depois que seus dados são carregados, ele é armazenado em um módulo de conjunto de dados e é experiência tooany disponíveis no espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a87df-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="a87df-124">Quando você estiver editando um experimento, você pode encontrar hello conjuntos de dados que você criou no hello **Meus conjuntos de dados** lista sob Olá **conjuntos de dados salvos** lista na paleta de módulo hello.</span><span class="sxs-lookup"><span data-stu-id="a87df-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="a87df-125">Você pode arrastar e soltar dataset de saudação em tela de experimento hello quando você desejar toouse Olá dataset para análise adicional e aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="a87df-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
