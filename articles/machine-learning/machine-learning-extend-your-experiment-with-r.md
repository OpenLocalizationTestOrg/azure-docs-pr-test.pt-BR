---
title: "aaaExtend sua experiência com R | Microsoft Docs"
description: "Como tooextend a funcionalidade de saudação do estúdio de aprendizado de máquina do Azure por meio da linguagem Olá R usando Olá módulo Executar Script R."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="598c3-103">Estender seu experimento com R</span><span class="sxs-lookup"><span data-stu-id="598c3-103">Extend your experiment with R</span></span>
<span data-ttu-id="598c3-104">Você pode estender a funcionalidade de saudação do estúdio de aprendizado de máquina do Azure por meio da linguagem Olá R usando Olá [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="598c3-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="598c3-105">Esse módulo aceita vários conjuntos de dados de entrada e produz um único conjunto de dados como saída.</span><span class="sxs-lookup"><span data-stu-id="598c3-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="598c3-106">Você pode digitar um script R em Olá **Script R** parâmetro hello [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="598c3-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="598c3-107">Você pode acessar cada porta de entrada do módulo hello usando código semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="598c3-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="598c3-108">Listando todos os pacotes instalados no momento</span><span class="sxs-lookup"><span data-stu-id="598c3-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="598c3-109">pode alterar a lista de saudação de pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="598c3-109">hello list of installed packages can change.</span></span> <span data-ttu-id="598c3-110">Uma lista de pacotes atualmente instalados pode ser encontrada em [Pacotes R com suporte pelo Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span><span class="sxs-lookup"><span data-stu-id="598c3-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="598c3-111">Você também pode obter lista de completa e atual de saudação de pacotes instalados inserindo Olá código a seguir em Olá [Executar Script R] [ execute-r-script] módulo:</span><span class="sxs-lookup"><span data-stu-id="598c3-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="598c3-112">Isso envia a lista de saudação da porta de saída de toohello pacotes da saudação [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="598c3-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="598c3-113">pacote de saudação tooview lista, conecte-se a um módulo de conversão como [converter tooCSV] [ convert-to-csv] toohello esquerda a saída de hello [Executar Script R] [ execute-r-script]módulo, execute o experimento Olá, clique em saída de saudação do módulo de conversão hello e selecione **baixar**.</span><span class="sxs-lookup"><span data-stu-id="598c3-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

![Baixar a saída do módulo "Converter tooCSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="598c3-115">Importando pacotes</span><span class="sxs-lookup"><span data-stu-id="598c3-115">Importing packages</span></span>
<span data-ttu-id="598c3-116">Você pode importar os pacotes que não ainda estiverem instalados usando Olá Olá comandos a seguir [Executar Script R] [ execute-r-script] módulo:</span><span class="sxs-lookup"><span data-stu-id="598c3-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="598c3-117">Olá onde `my_favorite_package.zip` arquivo contém o pacote.</span><span class="sxs-lookup"><span data-stu-id="598c3-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
