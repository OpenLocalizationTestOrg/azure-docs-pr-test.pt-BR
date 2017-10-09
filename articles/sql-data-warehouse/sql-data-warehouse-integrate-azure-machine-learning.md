---
title: "Aprendizado de máquina do Azure SQL Data warehouse de aaaUse | Microsoft Docs"
description: "Tutorial para usar o Azure Machine Learning com o Data Warehouse do SQL Azure para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>Use o Azure Machine Learning com o SQL Data Warehouse
O aprendizado de máquina do Azure é um serviço de análise preditiva totalmente gerenciado que você pode usar modelos de previsão toocreate em relação aos dados no SQL Data Warehouse e, em seguida, publicar como serviços web pronto para consumo. Você pode Conheça os fundamentos de saudação da análise de previsão e aprendizado de máquina lendo [tooMachine Introdução aprendizado no Azure][Introduction tooMachine Learning on Azure].  Em seguida, você pode aprender como toocreate, treinamento, pontuação e testar um modelo de aprendizado de máquina usando Olá [criar experiência tutorial][Create experiment tutorial].

Neste artigo, você aprenderá como Olá toodo usando Olá a seguir [estúdio de aprendizado de máquina do Azure][Azure Machine Learning Studio]:

* Ler dados de seu banco de dados toocreate, treinar e pontuação de um modelo de previsão
* Gravar dados tooyour banco de dados

## <a name="read-data-from-sql-data-warehouse"></a>Exportar dados do SQL Data Warehouse
Podemos lê dados da tabela Produtos no banco de dados do hello AdventureWorksDW.

### <a name="step-1"></a>Etapa 1
Iniciar um novo teste, clique em + novo final Olá Olá janela estúdio de aprendizado de máquina, selecione EXPERIMENTO e experiências em branco. Padrão de Select Olá experimentar nome hello superior da tela hello e renomeie-a como toosomething significativo, por exemplo, previsão de preço de bicicleta.

### <a name="step-2"></a>Etapa 2
Procure por módulo de leitor de saudação na paleta de saudação de conjuntos de dados e módulos esquerda Olá da tela de experimento hello. Arraste a tela de experimento Olá módulo toohello.
![][drag_reader]

### <a name="step-3"></a>Etapa 3
Selecione o módulo do leitor de saudação e preencher o painel de propriedades de saudação.

1. Selecione o banco de dados do SQL Azure como Olá fonte de dados.
2. Nome do servidor de banco de dados: nome do servidor de saudação de tipo. Você pode usar o hello [portal do Azure] [ Azure portal] toofind isso.

![][server_name]

1. Nome do banco de dados: nome de saudação do tipo de banco de dados no servidor de saudação especificado.
2. Nome de conta de usuário do servidor: nome de usuário de saudação do tipo de uma conta que tenha permissões de acesso para o banco de dados de saudação.
3. Senha de conta de usuário do servidor: fornecer senha Olá Olá especificar conta de usuário.
4. Aceitar qualquer certificado de servidor: Use esta opção (menos segura), se você quiser tooskip revisando o certificado de saudação do site antes de ler os dados.
5. Consulta de banco de dados: insira uma instrução SQL que descreve dados Olá deseja tooread. Nesse caso, estamos lê dados da tabela de produto usando Olá consulta a seguir.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>Etapa 4
1. Execute o teste de saudação clicando em execução em tela de experimento hello.
2. Quando termina de experiência hello, módulo de leitor de saudação terá tooindicate uma marca de seleção verde que ela foi concluída com êxito. Observe também Olá concluído status de execução no canto superior direito de saudação.

![][run]

1. toosee Olá dados importados, clique Olá a porta de saída na parte inferior de saudação do automóvel Olá de conjunto de dados e selecione Visualizar.

## <a name="create-train-and-score-a-model"></a>Crie, treine e pontue um modelo
Agora você pode usar esse conjunto de dados para:

* Criar um modelo: processar dados e definir recursos
* Treinar modelo de saudação: escolha e aplicar um algoritmo de aprendizado
* Pontuação e teste Olá modelo: prever o novo preço de bicicleta

![][model]

mais informações sobre como toocreate, treinamento, pontuação e testar uma saudação de uso do modelo de aprendizado de máquina do toolearn [criar experiência tutorial][Create experiment tutorial].

## <a name="write-data-tooazure-sql-data-warehouse"></a>Gravar dados tooAzure SQL Data Warehouse
Podemos gravará Olá tabela de tooProductPriceForecast de conjunto de resultados no banco de dados do hello AdventureWorksDW.

### <a name="step-1"></a>Etapa 1
Procure o módulo de gravador Olá na paleta de saudação de conjuntos de dados e módulos esquerda Olá da tela de experimento hello. Arraste a tela de experimento Olá módulo toohello.

![][drag_writer]

### <a name="step-2"></a>Etapa 2
Selecione o módulo de gravador hello e preencher o painel de propriedades de saudação.

1. Selecione o banco de dados do SQL Azure como Olá destino de dados.
2. Nome do servidor de banco de dados: nome do servidor de saudação de tipo. Você pode usar o hello [portal do Azure] [ Azure portal] toofind isso.
3. Nome do banco de dados: nome de saudação do tipo de banco de dados no servidor de saudação especificado.
4. Nome de conta de usuário do servidor: nome de usuário de saudação do tipo de uma conta que tenha permissões de gravação para o banco de dados de saudação.
5. Senha de conta de usuário do servidor: fornecer senha Olá Olá especificar conta de usuário.
6. Aceitar qualquer certificado de servidor (mínimo): Selecione esta opção se você não deseja o certificado de saudação tooview.
7. Lista separada por vírgulas de colunas toobe salvada: forneça uma lista de colunas de conjunto de dados ou o resultado de saudação que você deseja toooutput.
8. Nome da tabela de dados: especifique nome Olá Olá da tabela de dados.
9. Lista separada por vírgulas de colunas da datatable: especificar Olá toouse de nomes de coluna na nova tabela de saudação. Olá nomes de coluna podem ser diferentes da saudação aqueles no conjunto de dados de origem hello, mas você deve listar Olá o mesmo número de colunas aqui que você definir para a tabela de saída de hello.
10. Número de linhas gravadas por operação do SQL Azure: você pode configurar Olá número de linhas que são gravados tooa banco de dados SQL em uma única operação.

![][writer_properties]

### <a name="step-3"></a>Etapa 3
1. Execute o teste de saudação clicando em execução em tela de experimento hello.
2. Quando termina de experiência hello, todos os módulos terá tooindicate uma marca de seleção verde que eles foi concluídos com êxito.

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
