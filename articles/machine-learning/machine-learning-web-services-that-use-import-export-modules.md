---
title: "aaaUsing importação/exportação de dados nos serviços web do aprendizado de máquina do Azure | Microsoft Docs"
description: "Saiba como toouse Olá toosend de módulos de importação de dados e exportar dados e receber dados de um serviço web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a>Implantação de serviços Web do Azure AM que usam módulos Importar Dados e Exportar Dados

Quando você cria um experimento de previsão, normalmente adiciona uma entrada e uma saída de serviço Web. Quando você implanta um experimento hello, os consumidores podem enviar e receber dados do serviço web de saudação por meio de saudação entradas e saídas. Para alguns aplicativos, os dados do cliente podem estar disponíveis a partir de um feed de dados ou já residirem em uma fonte de dados externa, como o armazenamento de Blobs do Azure. Nesses casos, eles não precisam de dados de leitura e gravação usando saídas e entradas do serviço Web. Em vez disso, eles podem usar dados de tooread do serviço de execução de lote (BES) saudação da fonte de dados hello usando um módulo de importação de dados e gravar Olá tooa outro local de dados usando um módulo de exportar dados de resultados de pontuação.

Olá dados de importação e exportação módulos de dados, pode ler e gravar dados toovarious fornecem locais, como uma URL da Web via HTTP, uma consulta de Hive, um banco de dados SQL do Azure, armazenamento de tabela do Azure, armazenamento de BLOBs do Azure, um Feed de dados ou um banco de dados do SQL no local.

Este tópico usa hello "exemplo 5: avaliar de treinamento, teste, para classificação binária: conjunto de dados adulto" de exemplo e pressupõe Olá dataset já foi carregado em uma tabela do SQL Azure denominada censusdata.

## <a name="create-hello-training-experiment"></a>Criar um teste de treinamento Olá
Quando você abre hello "exemplo 5: avaliar de treinamento, teste, para classificação binária: conjunto de dados adulto" exemplo de conjunto de dados do usa Olá exemplo adulto classificação binária de renda de censo. E experiência Olá na tela hello terá aparência semelhante toohello imagem a seguir:

![Configuração inicial do experimento hello.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

dados de saudação tooread da tabela do SQL Azure hello:

1. Exclua Olá módulo de conjunto de dados.
2. Na caixa de pesquisa de componentes hello, tipo de importação.
3. Saudação da lista de resultados, adicionar um *importar dados* toohello módulo experimentar a tela.
4. Conecte a saída de hello *importar dados* entrada de saudação do módulo de saudação *limpar dados ausentes* módulo.
5. No painel Propriedades, selecione **banco de dados do SQL Azure** em Olá **fonte de dados** lista suspensa.
6. Em Olá **nome do servidor de banco de dados**, **nome do banco de dados**, **nome de usuário**, e **senha** campos, insira as informações adequadas para Olá o banco de dados.
7. No campo de consulta de banco de dados hello, digite Olá consulta a seguir.
   
     select [age],
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     from dbo.censusdata;
8. Na parte inferior de saudação da tela de experimento hello, clique em **executar**.

## <a name="create-hello-predictive-experiment"></a>Criar experiência previsível Olá
Em seguida Configure experimento previsão de saudação do qual você implanta o serviço da web.

1. Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web** e selecione **serviço Web de previsão [recomendado]**.
2. Remover Olá *entrada de serviço Web* e *módulos de saída do serviço Web* de experiência de previsão hello. 
3. Na caixa de pesquisa de componentes hello, tipo de exportação.
4. Saudação da lista de resultados, adicionar um *exportar dados* toohello módulo experimentar a tela.
5. Conecte a saída de hello *modelo de pontuação* entrada de saudação do módulo de saudação *exportar dados* módulo. 
6. No painel Propriedades, selecione **banco de dados do SQL Azure** na lista suspensa de destino de dados hello.
7. Em Olá **nome do servidor de banco de dados**, **nome do banco de dados**, **nome de conta de usuário do servidor**, e **senha de conta de usuário do servidor** campos, digite informações adequadas Olá para seu banco de dados.
8. Em Olá **lista de colunas toobe salvada separada por vírgulas** , digite os rótulos de pontuação.
9. Em Olá **campo de nome de tabela de dados**, digite dbo. ScoredLabels. Se a tabela de saudação não existir, ele é criado quando o experimento hello está em execução ou serviço da web de saudação é chamado.
10. Em Olá **lista de colunas da datatable separada por vírgulas** campo, digite ScoredLabels.

Quando você escreve um aplicativo que chama Olá serviço web final, talvez você queira toospecify uma tabela diferente e entrada de consulta ou de destino em tempo de execução. tooconfigure essas entradas e saídas, use Olá Olá de tooset de recurso de parâmetros do Web Service *importar dados* módulo *fonte de dados* propriedade e hello *exportar dados* modo propriedade de destino de dados.  Para obter mais informações sobre parâmetros de serviço da Web, consulte Olá [entrada de parâmetros de serviço Web AzureML](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) em hello Intelligence Cortana e o Blog de aprendizado de máquina.

Olá tooconfigure parâmetros de serviço da Web para consulta de importação de saudação e a tabela de destino de saudação:

1. No painel de propriedades de saudação de saudação *importar dados* módulo, clique ícone Olá no hello parte superior direita da saudação **consulta de banco de dados** campo e selecione **definido como parâmetro de serviço web**.
2. No painel de propriedades de saudação de saudação *exportar dados* módulo, clique ícone Olá no hello parte superior direita da saudação **nome da tabela de dados** campo e selecione **definido como parâmetro de serviço web**.
3. Na parte inferior de saudação do hello *exportar dados* painel de propriedades do módulo, no hello **parâmetros de serviço Web** seção, clique em consulta de banco de dados e renomeie-a consulta.
4. Clique em **Nome da tabela de dados** e troque seu nome para **Tabela**.

Quando terminar, sua experiência deve ter aparência semelhante toohello imagem a seguir:

![Aparência final do experimento.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

Agora você pode implantar Olá experiência como um serviço web.

## <a name="deploy-hello-web-service"></a>Implantar o serviço web de saudação
Você pode implantar um serviço web clássico ou novo tooeither.

### <a name="deploy-a-classic-web-service"></a>Implantar um Serviço Web Clássico
toodeploy como um serviço Web clássico e criar um aplicativo tooconsume-lo:

1. Na parte inferior de saudação da tela de experimento hello, clique em executar.
2. Quando a saudação executar for concluída, clique em **implantar o serviço da Web** e selecione **implantar o serviço Web [clássico]**.
3. No painel de serviço web hello, localize sua chave de API. Copiar e salvar toouse mais tarde.
4. Em hello **ponto de extremidade padrão** da tabela, clique em Olá **Batch Execution** Olá tooopen de link a página de ajuda de API.
5. No Visual Studio, crie um aplicativo de console C#: **Novo** > **Projeto** > **Visual C#** > **Área de Trabalho Clássica do Windows** > **Aplicativo de Console (.NET Framework)**.
6. Na página de Ajuda da API do hello, localize Olá **código de exemplo** seção final Olá Olá página.
7. Copie e cole Olá código c# de exemplo no arquivo Program.cs e remover todas as referências toohello blob storage.
8. Atualizar o valor Olá Olá *apiKey* variável com chave Olá API salvo anteriormente.
9. Localizar Olá solicitação declaração e atualização Olá valores de parâmetros de serviço da Web que são passados toohello *importar dados* e *exportar dados* módulos. Nesse caso, use a consulta original hello, mas definir um novo nome de tabela.
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. Execute o aplicativo hello. 

Após a conclusão da saudação executar, uma nova tabela será adicionada toohello banco de dados que contém a saudação resultados de pontuação.

### <a name="deploy-a-new-web-service"></a>Implantar um serviço Web Novo

> [!NOTE] 
> toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação. Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md). 

toodeploy como um novo serviço da Web e criar um aplicativo tooconsume-lo:

1. Na parte inferior de saudação da tela de experimento hello, clique em **executar**.
2. Quando a saudação executar for concluída, clique em **implantar o serviço da Web** e selecione **implantar o serviço de Web [novo]**.
3. Na página de teste implantar hello, insira um nome para o serviço web, selecione um plano de preços e clique em **implantar**.
4. Em Olá **Quickstart** , clique em **consumir**.
5. Em Olá **código de exemplo** seção, clique em **lote**.
6. No Visual Studio, crie um aplicativo de console C#: **Novo** > **Projeto** > **Visual C#** > **Área de Trabalho Clássica do Windows** > **Aplicativo de Console (.NET Framework)**.
7. Copie e cole o código de exemplo hello c# em seu arquivo Program.cs.
8. Atualizar o valor Olá Olá *apiKey* variável com hello **chave primária** localizado em Olá **informações básicas de consumo** seção.
9. Localizar Olá *scoreRequest* declaração e atualizar valores de saudação de parâmetros de serviço da Web que são passados toohello *importar dados* e *exportar dados* módulos. Nesse caso, use a consulta original hello, mas definir um novo nome de tabela.
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. Execute o aplicativo hello. 

