---
title: Estender o teste com R | Microsoft Docs
description: "Como estender a funcionalidade do Azure Machine Learning Studio por meio da linguagem R usando o módulo Executar o Script R."
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
ms.openlocfilehash: fe207ef917980be8b554ad9c08176d108b19fb71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="2ffd5-103">Estender seu experimento com R</span><span class="sxs-lookup"><span data-stu-id="2ffd5-103">Extend your experiment with R</span></span>
<span data-ttu-id="2ffd5-104">Você pode estender a funcionalidade do Machine Learning Studio do Azure por meio da linguagem R, usando o módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="2ffd5-104">You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="2ffd5-105">Esse módulo aceita vários conjuntos de dados de entrada e produz um único conjunto de dados como saída.</span><span class="sxs-lookup"><span data-stu-id="2ffd5-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="2ffd5-106">Você pode digitar um script R no parâmetro **Script R** do módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="2ffd5-106">You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="2ffd5-107">Você pode acessar cada porta de entrada do módulo usando código semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="2ffd5-107">You access each input port of the module by using code similar to the following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="2ffd5-108">Listando todos os pacotes instalados no momento</span><span class="sxs-lookup"><span data-stu-id="2ffd5-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="2ffd5-109">A lista de pacotes instalados pode mudar.</span><span class="sxs-lookup"><span data-stu-id="2ffd5-109">The list of installed packages can change.</span></span> <span data-ttu-id="2ffd5-110">Uma lista de pacotes atualmente instalados pode ser encontrada em [Pacotes R com suporte pelo Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ffd5-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="2ffd5-111">Obtenha também uma lista completa e atual dos pacotes instalados, digitando o seguinte código no módulo [Executar Script R][execute-r-script]:</span><span class="sxs-lookup"><span data-stu-id="2ffd5-111">You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="2ffd5-112">Isso envia a lista de pacotes para a porta de saída do módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="2ffd5-112">This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="2ffd5-113">Para exibir a lista de pacotes, conecte um módulo de conversão, como o [Converter para CSV][convert-to-csv] na saída à esquerda do módulo [Executar Script R][execute-r-script], execute o experimento e, então, clique na saída do módulo de conversão e selecione **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="2ffd5-113">To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**.</span></span> 

![Baixar saída do módulo “Converter para CSV”](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is the [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="2ffd5-115">Importando pacotes</span><span class="sxs-lookup"><span data-stu-id="2ffd5-115">Importing packages</span></span>
<span data-ttu-id="2ffd5-116">Você pode importar pacotes ainda não instalados usando os seguintes comandos no módulo [Executar Script R][execute-r-script] :</span><span class="sxs-lookup"><span data-stu-id="2ffd5-116">You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="2ffd5-117">onde o arquivo `my_favorite_package.zip` contém o pacote.</span><span class="sxs-lookup"><span data-stu-id="2ffd5-117">where the `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
