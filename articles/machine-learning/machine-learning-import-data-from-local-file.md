---
title: Importar dados de um arquivo para o Azure Machine Learning Studio | Microsoft Docs
description: "Saiba como carregar um arquivo de dados de treinamento do disco rígido para o Azure Machine Learning Studio. Isso cria um módulo de conjunto de dados no espaço de trabalho."
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
ms.openlocfilehash: 18010864160ceb2d76aea37196e6944bbe426457
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="162e7-105">Importar dados de treinamento de um arquivo no disco rígido para o Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="162e7-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="162e7-106">Saiba como carregar um arquivo de dados do disco rígido a fim de usar como dados de treinamento no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="162e7-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="162e7-107">Ao importar o arquivo de dados, você terá um módulo de conjunto de dados pronto para uso em seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="162e7-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="162e7-108">Etapas para importar dados de um arquivo local</span><span class="sxs-lookup"><span data-stu-id="162e7-108">Steps to import data from a local file</span></span>
<span data-ttu-id="162e7-109">Para importar dados de um disco rígido local, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="162e7-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="162e7-110">clique em **+NOVO** na parte inferior da janela do Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="162e7-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="162e7-111">Selecione **CONJUNTO DE DADOS** e **DO ARQUIVO LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="162e7-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="162e7-112">Na caixa de diálogo **Carregar um novo conjunto de dados** , navegue até o arquivo que deseja carregar</span><span class="sxs-lookup"><span data-stu-id="162e7-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="162e7-113">Digite um nome, identifique o tipo de dados e, opcionalmente, insira uma descrição.</span><span class="sxs-lookup"><span data-stu-id="162e7-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="162e7-114">Uma descrição é recomendada – ela permite registrar características sobre os dados que você deseja lembrar ao usar os dados no futuro.</span><span class="sxs-lookup"><span data-stu-id="162e7-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="162e7-115">A caixa de seleção **Esta é a nova versão de um conjunto de dados existente** permite que você atualize um conjunto de dados existente com novos dados.</span><span class="sxs-lookup"><span data-stu-id="162e7-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="162e7-116">Clique nesta caixa de seleção e digite o nome de um conjunto de dados existente.</span><span class="sxs-lookup"><span data-stu-id="162e7-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![Carregar um novo conjunto de dados](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="162e7-118">Durante o upload, você verá uma mensagem informando que seu arquivo está sendo carregado.</span><span class="sxs-lookup"><span data-stu-id="162e7-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="162e7-119">O tempo de upload depende do tamanho dos dados e da velocidade da conexão com o serviço.</span><span class="sxs-lookup"><span data-stu-id="162e7-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="162e7-120">Se souber que o arquivo levará muito tempo, você pode fazer outras coisas dentro do Machine Learning Studio enquanto espera.</span><span class="sxs-lookup"><span data-stu-id="162e7-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="162e7-121">No entanto, fechar o navegador fará com que o upload de dados falhe.</span><span class="sxs-lookup"><span data-stu-id="162e7-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="162e7-122">O módulo do conjunto de dados está pronto para uso</span><span class="sxs-lookup"><span data-stu-id="162e7-122">Dataset module is ready for use</span></span>
<span data-ttu-id="162e7-123">Uma vez carregados, seus dados são armazenados em um módulo de conjunto de dados e ficam disponíveis para qualquer experimento em seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="162e7-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="162e7-124">Quando estiver editando um experimento, você pode encontrar os conjuntos de dados criados na lista **Meus Conjuntos de Dados**, na lista **Conjuntos de Dados Salvos** na paleta de módulos.</span><span class="sxs-lookup"><span data-stu-id="162e7-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="162e7-125">É possível arrastar e soltar o conjunto de dados na tela de teste quando você desejar usá-lo para outras análises e aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="162e7-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
