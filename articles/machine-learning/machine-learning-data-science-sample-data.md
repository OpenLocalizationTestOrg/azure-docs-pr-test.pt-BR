---
title: "aaaSample dados no Azure blob contêineres, SQL Server e tabelas de Hive | Microsoft Docs"
description: "Como os dados de tooexplore armazenados em vários enviromnents do Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="dfe18-103"><a name="heading"></a>Amostra de dados em contêineres de blob do Azure, SQL Server e tabelas Hive</span><span class="sxs-lookup"><span data-stu-id="dfe18-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="dfe18-104">Este documento contém links tootopics aborda como toosample dados armazenados em um dos três diferentes locais do Azure:</span><span class="sxs-lookup"><span data-stu-id="dfe18-104">This document links tootopics that covers how toosample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="dfe18-105">**dados no contêiner de blobs do Azure** é realizada baixando-os programaticamente e realizando a amostragem com um exemplo de código Python.</span><span class="sxs-lookup"><span data-stu-id="dfe18-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="dfe18-106">**Dados do SQL Server** são amostrados usando SQL e Olá linguagem de programação Python.</span><span class="sxs-lookup"><span data-stu-id="dfe18-106">**SQL Server data** is sampled using both SQL and hello Python Programming Language.</span></span> 
* <span data-ttu-id="dfe18-107">**dados da tabela do Hive** é realizada usando consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="dfe18-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="dfe18-108">a seguir Olá **menu** links toohello tópicos que descrevem como dados toosample de cada um desses ambientes de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfe18-108">hello following **menu** links toohello topics that describe how toosample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="dfe18-109">Esta tarefa de amostragem é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="dfe18-109">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="dfe18-110">**Por que fazer a amostragem de dados?**</span><span class="sxs-lookup"><span data-stu-id="dfe18-110">**Why sample data?**</span></span>

<span data-ttu-id="dfe18-111">Se dataset Olá planejar tooanalyze for grande, normalmente é um tooreduce de dados de exemplo toodown Olá boa ideia-tooa menor, mas representativo e mais fácil de gerenciar o tamanho.</span><span class="sxs-lookup"><span data-stu-id="dfe18-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="dfe18-112">Isso facilita a compreensão de dados, exploração e engenharia de recursos.</span><span class="sxs-lookup"><span data-stu-id="dfe18-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="dfe18-113">Sua função no hello o processo de análise do Cortana é tooenable rápida criação de protótipos de funções de processamento de dados de saudação e modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="dfe18-113">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

