---
title: "dados de aaaAnalyze com o aprendizado de máquina do Azure | Microsoft Docs"
description: "Use um modelo com base nos dados armazenados no Azure SQL Data Warehouse de aprendizado de máquina previsão de toobuild de aprendizado de máquina do Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Analisar dados com o Azure Machine Learning
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * 
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Este tutorial usa um modelo com base nos dados armazenados no Azure SQL Data Warehouse de aprendizado de máquina previsão de toobuild de aprendizado de máquina do Azure. Especificamente, isso cria uma campanha de marketing para a Adventure Works, loja de bicicletas hello, por prever se um cliente é provavelmente toobuy uma bicicleta ou não.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toostep este tutorial, você precisa:

* Um SQL Data Warehouse pré-carregado com os dados de exemplo do AdventureWorksDW. tooprovision isso, consulte [criar um SQL Data Warehouse] [ Create a SQL Data Warehouse] e escolha dados de exemplo hello tooload. Se você já tiver um data warehouse, mas não tiver dados de exemplo, poderá [carregar dados de exemplo manualmente][load sample data manually].

## <a name="1-get-hello-data"></a>1. Obter dados de saudação
dados saudação estão no modo de dbo.vTargetMail de saudação no banco de dados do hello AdventureWorksDW. tooread esses dados:

1. Entre no [Azure Machine Learning Studio][Azure Machine Learning studio] e clique em Meus Testes.
2. Clique em **+NOVO** e selecione **Teste em Branco**.
3. Insira um nome para o seu teste: Marketing Direcionado.
4. Saudação de arrastar **leitor** módulo no painel de módulos de saudação na tela hello.
5. Especifique os detalhes de saudação do banco de dados SQL Data Warehouse no painel de propriedades de saudação.
6. Especifique o banco de dados de saudação **consulta** tooread dados de saudação de interesse.

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

Executar o teste de saudação clicando **executar** em tela de experimento hello.
![Executar teste Olá][1]

Após a conclusão da experiência de saudação em execução com êxito, clique Olá a porta de saída na parte inferior de saudação do módulo do leitor de saudação e selecione **visualizar** toosee Olá importou dados.
![Exibir dados importados][3]

## <a name="2-clean-hello-data"></a>2. Dados saudação normal
dados de saudação tooclean, remova algumas colunas que não são relevantes para o modelo de saudação. toodo isso:

1. Saudação de arrastar **colunas do projeto** módulo na tela hello.
2. Clique em **seletor de coluna iniciar** no toospecify de painel de propriedades Olá quais colunas você deseja toodrop.
   ![Colunas do Projeto][4]
3. Exclua duas colunas: CustomerAlternateKey e GeographyKey.
   ![Remover colunas desnecessárias][5]

## <a name="3-build-hello-model"></a>3. Criar modelo Olá
Podemos dividirá Olá dados 80-20: 80% tootrain um modelo de aprendizado de máquina e 20% tootest Olá modelo. Faremos usa algoritmos de "Duas classes" Olá para esse problema de classificação binária.

1. Saudação de arrastar **divisão** módulo na tela hello.
2. Insira 0,8 da fração de linhas no primeiro conjunto de saída hello, no painel de propriedades de saudação.
   ![Dividir os dados em conjuntos de treinamento e teste][6]
3. Saudação de arrastar **árvore de decisão ampliada de duas classes** módulo na tela hello.
4. Saudação de arrastar **treinar modelo** módulo em Olá tela e especificar Olá entradas. Em seguida, clique em **seletor de coluna iniciar** no painel de propriedades de saudação.
   * Primeira entrada: algoritmo de ML.
   * Segundo de entrada: algoritmo de saudação tootrain dados em.
     ![Conecte-se o módulo treinar modelo de saudação][7]
5. Selecione Olá **BikeBuyer** coluna como Olá toopredict de coluna.
   ![Selecione a coluna toopredict][8]

## <a name="4-score-hello-model"></a>4. Modelo de saudação de pontuação
Agora, vamos testar como o modelo de saudação executa em dados de teste. Podemos comparará algoritmo Olá nossa escolha com toosee um algoritmo diferente que tem um desempenho melhor.

1. Arraste **modelo de pontuação** módulo na tela hello.
    Primeiro de entrada: treinado modelo segunda entrada: dados de teste ![modelo Olá de pontuação][9]
2. Saudação de arrastar **máquina do ponto de Bayes de duas classes** na tela de experimento hello. Podemos comparará como esse algoritmo executa na comparação toohello árvore de decisão ampliada de duas classes.
3. Copiar e colar Olá módulos treinar modelo e o modelo de classificação no hello tela.
4. Saudação de arrastar **avaliar modelo** módulo em algoritmos de saudação dois Olá tela toocompare.
5. **Executar** Olá experimento.
   ![Executar teste Olá][10]
6. Clique em Olá a porta de saída na parte inferior de Olá Olá avaliar do módulo do modelo e clique em Visualizar.
   ![Visualizar os resultados de avaliação][11]

métricas de saudação fornecidas são curva de ROC hello, lembre-se de precisão de diagrama e levante curva. Observando essas métricas, podemos ver esse modelo primeiro Olá executado melhor do que Olá segundo. toolook em Olá que Olá primeiro modelo previsto, clique na porta de saída do hello modelo de classificação e clique em Visualizar.
![Visualizar os resultados da pontuação][12]

Você verá que mais duas colunas adicionadas tooyour conjunto de dados de teste.

* Das probabilidades pontuadas: probabilidade de saudação que um cliente é um comprador de bicicletas.
* Rótulos de pontuação: Olá classificação feita pelo modelo hello – comprador de bicicleta (1) ou não (0). Esse limite de probabilidade para rotular é definida too50% e pode ser ajustado.

Comparando coluna Olá comprador de bicicleta (real) com rótulos de pontuação de saudação (previsão), você pode ver como o modelo Olá executou. Próximas etapas, você pode usar previsões de toomake este modelo para novos clientes e publicar este modelo como um serviço web ou gravar resultados back tooSQL Data Warehouse.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre como criar modelos de aprendizado de máquina previsão consulte muito[tooMachine introdução de aprendizagem no Azure][Introduction tooMachine Learning on Azure].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
