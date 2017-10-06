---
title: "tutorial aaaQuickstart linguagem R para o aprendizado de máquina | Microsoft Docs"
description: "Use este tutorial tooget iniciado rapidamente usando o idioma Olá R com o estúdio de aprendizado de máquina do Azure toocreate uma solução de previsão de programação de R."
keywords: "guia de início rápido, linguagem r, linguagem de programação r, tutorial de programação r"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Tutorial de início rápido para a linguagem de programação Olá R para o aprendizado de máquina do Azure

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>Introdução
Este tutorial de início rápido ajuda você a iniciar rapidamente estendendo o aprendizado de máquina do Azure usando a linguagem de programação Olá R. Siga este tutorial toocreate de programação de R, teste e execute o código R no aprendizado de máquina do Azure. Conforme você trabalha com tutorial, você criará uma solução completa de previsão usando linguagem Olá R no aprendizado de máquina do Azure.  

O Microsoft Azure Machine Learning contém muitos módulos poderosos de aprendizado de máquina e de manipulação de dados. linguagem R avançada de saudação tem sido descrita como Olá linguagem internacional de análise. Felizmente, análise e manipulação de dados no aprendizado de máquina do Azure pode ser estendida por meio de R. Essa combinação fornece escalabilidade hello e facilidade de implantação de aprendizado de máquina do Azure com flexibilidade hello e análise detalhada do R.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>Conjunto de dados de previsão e hello
A previsão é um método analítico amplamente empregado e bastante útil. Intervalo de prever vendas sazonais, determinar níveis de estoque ideal variáveis macroeconomic toopredicting de usos comuns. A previsão normalmente é feita com modelos de série de tempo.

Dados de série temporal são a data em que os valores hello tem um índice de tempo. índice de tempo de saudação pode ser normal, por exemplo, a cada mês ou a cada minuto, ou irregulares. Um modelo de série de tempo se baseia em dados de série de tempo. linguagem de programação Olá R contém uma estrutura flexível e análise abrangente para dados de série temporal.

Neste guia de início rápido, trabalharemos com a produção de derivados de leite e dados de preços na Califórnia. Esses dados incluem informações mensais na produção de hello de vários Laticínios e preço Olá fat leite mercadoria um parâmetro de comparação.

Olá usados neste artigo, juntamente com scripts de R, os dados podem ser [baixado em][download]. Esses dados foi originalmente sintetizados das informações disponíveis da saudação Universidade de Wisconsin em http://future.aae.wisc.edu/tab/production.html.

### <a name="organization"></a>Organização
Podemos será andamento por meio de várias etapas, você aprenderá como toocreate, testar e executar análises e dados de código de manipulação de R no ambiente de aprendizado de máquina do Azure Olá.  

* Primeiro, exploraremos Olá Noções básicas sobre usando linguagem de saudação R no ambiente do hello estúdio de aprendizado de máquina do Azure.
* Em seguida, podemos progresso toodiscussing vários aspectos de e/s de dados, o código R e elementos gráficos no ambiente de aprendizado de máquina do Azure Olá.
* É, em seguida, criará a primeira parte Olá da nossa solução previsão criando código para limpeza de dados e a transformação.
* Com nossos dados preparados vamos realizar uma análise de correlações Olá entre várias variáveis de saudação em nosso conjunto de dados.
* Por fim, criaremos um modelo de previsão de série de tempos sazonais da produção de leite.

## 
            <a id="mlstudio">
            </a>Interagir com a linguagem R no Studio de Machine Learning
Esta seção descreve alguns aspectos de interação com a linguagem de programação Olá R no ambiente do estúdio de aprendizado de máquina hello. linguagem de saudação R fornece uma ferramenta poderosa toocreate personalizado análises e dados de manipulação módulos no ambiente de aprendizado de máquina do Azure hello.

Vou usar RStudio toodevelop, testar e depurar código de R em pequena escala. Esse código é, em seguida, recortar e colar em um [Executar Script R] [ execute-r-script] módulo no toorun pronto do estúdio de aprendizado de máquina.  

### <a name="hello-execute-r-script-module"></a>módulo de executar Script R Olá
No estúdio de aprendizado de máquina, scripts de R são executados dentro de saudação [Executar Script R] [ execute-r-script] módulo. Um exemplo de hello [Executar Script R] [ execute-r-script] módulo no estúdio de aprendizado de máquina é mostrado na Figura 1.

 ![Linguagem de programação R: módulo Executar Script R de saudação selecionado no estúdio de aprendizado de máquina][1]

*Figura 1. ambiente de estúdio de aprendizado de máquina Olá mostrando Olá Executar Script R módulo selecionado.*

Consultando tooFigure 1, vamos examinar algumas das partes principais de saudação do ambiente do estúdio de aprendizado de máquina Olá para trabalhar com hello [Executar Script R] [ execute-r-script] módulo.

* módulos Olá experimento Olá são mostrados no painel de centro de saudação.
* parte superior de saudação do painel direito da saudação contém um tooview de janela e editar seus scripts de R.  
* parte inferior de saudação do painel direito mostra algumas propriedades de saudação [Executar Script R][execute-r-script]. Você pode exibir os logs de erro e a saída de hello clicando em pontos de saudação apropriado deste painel.

Obviamente, abordaremos Olá [Executar Script R] [ execute-r-script] mais detalhadamente no restante deste documento hello.

Ao trabalhar com funções R complexas, é recomendável que você edite, teste e depure no RStudio. Assim como acontece com qualquer desenvolvimento de software, estenda o código de forma incremental e teste-o em pequenos casos de teste simples. Recorte e cole as funções na janela de script hello R de saudação [Executar Script R] [ execute-r-script] módulo. Essa abordagem permite que você tooharness Olá RStudio ambiente de desenvolvimento integrado (IDE) tanto Olá potência de aprendizado de máquina do Azure.  

#### <a name="execute-r-code"></a>Executar código R
Qualquer código de R Olá [Executar Script R] [ execute-r-script] módulo será executado quando você executar o teste de saudação clicando em Olá **executar** botão. Quando a execução for concluída, uma marca de seleção aparecerá em Olá [Executar Script R] [ execute-r-script] ícone.

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Codificação R defensiva para o Azure Machine Learning
Se, por exemplo, estiver desenvolvendo código R para um serviço Web que usa o Azure Machine Learning, você definitivamente deverá planejar como seu código lidará com exceções e com entrada de dados inesperados. toomaintain clareza, não incluí quase Olá forma de verificação ou a maioria dos exemplos de código Olá mostrados de tratamento de exceção. No entanto, ao prosseguirmos, darei vários exemplos de funções usando o recurso de tratamento de exceção do R.  

Se for necessário um tratamento mais completo de tratamento de exceção de R, recomendo ler seções aplicáveis de saudação de livro de saudação do Wickham listada na [Apêndice B - leitura adicional](#appendixb).

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>Depurar e testar R no Studio de Machine Learning
tooreiterate, é recomendável testar e depurar seu código R em pequena escala no RStudio. No entanto, há casos em que você precisará tootrack problemas de código R no hello [Executar Script R] [ execute-r-script] em si. Além disso, é uma boa prática toocheck os resultados no estúdio de aprendizado de máquina.

Saída da execução de saudação do seu código R e na plataforma de aprendizado de máquina do Azure Olá encontra-se principalmente na saída. log. Algumas informações adicionais serão vistas no arquivo error.log.  

Se ocorrer um erro no estúdio de aprendizado de máquina durante a execução do seu código R, o primeiro curso de ação deve ser toolook em Error. Esse arquivo pode conter toohelp de mensagens de erro útil compreender e corrija o erro. Error tooview, clique em **Exibir log do erro** em Olá **painel propriedades** para Olá [Executar Script R] [ execute-r-script] que contém o erro de saudação.

Por exemplo, executei Olá seguinte código R, com uma variável y indefinido, em um [Executar Script R] [ execute-r-script] módulo:

    x <- 1.0
    z <- x + y

Este código falhará tooexecute, resultando em uma condição de erro. Clicando em **Exibir log do erro** em Olá **painel propriedades** produz Olá exibição mostrada na Figura 2.

  ![A mensagem de erro é exibida][2]

*Figura 2. Mensagem de erro pop-up.*

Parece que precisamos toolook na mensagem de erro la toosee Olá R. Clique em Olá [Executar Script R] [ execute-r-script] e, em seguida, clique em Olá **exibi-la** item Olá **painel propriedades** toohello direita. Abre uma nova janela do navegador e consulte o seguinte hello.

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

Essa mensagem de erro contém sem surpresas e identifica claramente o problema de saudação.

valor de saudação tooinspect de qualquer objeto em R, você pode imprimir o arquivo de saída. log esses valores toohello. regras de saudação para examinar o objeto valores são essencialmente Olá mesmo como em uma sessão interativa de R. Por exemplo, se você digitar um nome de variável em uma linha, o valor de saudação do objeto Olá será impressa toohello la arquivo.  

#### <a name="packages-in-machine-learning-studio"></a>Pacotes no Machine Learning Studio
O Azure Machine Learning vem com mais de 350 pacotes de linguagem R pré-instalados. Você pode usar Olá Olá código a seguir [Executar Script R] [ execute-r-script] módulo tooretrieve uma lista de saudação pré-instalado pacotes.

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

Se você não entender a última linha hello deste código momento Olá, leia sobre. No restante deste documento hello, discutiremos extensivamente usando R no ambiente de aprendizado de máquina do Azure hello.

### <a name="introduction-toorstudio"></a>Introdução tooRStudio
RStudio é um IDE amplamente utilizado para R. Vou usar RStudio para editar, testar e depurar algum código Olá R usado neste guia de início rápido. Depois que o código de R é testado e pronto, você simplesmente recortar e colar do editor de RStudio Olá em um estúdio de aprendizado de máquina [Executar Script R] [ execute-r-script] módulo.  

Se você não tiver a linguagem de programação Olá R instalada em seu computador desktop, é recomendável que você faça isso agora. Downloads gratuitos da linguagem R de software livre estão disponíveis em Olá rede de arquivamento abrangente de R (CRAN) em [http://www.r-project.org/](http://www.r-project.org/). Há downloads disponíveis para Windows, Mac OS e Linux/UNIX. Escolha um espelho próximo e siga as instruções de download de saudação. Além disso, CRAN contém uma grande quantidade de pacotes de manipulação de dados e análise úteis.

Se você for novo tooRStudio, deve baixar e instalar a versão de área de trabalho de saudação. Você pode encontrar hello que rstudio downloads do Windows, Mac OS e UNIX/Linux em http://www.rstudio.com/products/RStudio/. Siga as direções de saudação fornecidas tooinstall RStudio em seu computador desktop.  

Uma introdução ao tutorial tooRStudio está disponível em https://support.rstudio.com/hc/sections/200107586-Using-RStudio.

Forneço algumas informações adicionais sobre como usar o RStudio no [Apêndice A][appendixa].  

## <a id="scriptmodule"></a>Obter dados dentro e fora do módulo Executar Script R de saudação
Nesta seção, discutiremos como obter dados dentro e fora de saudação [Executar Script R] [ execute-r-script] módulo. Analisaremos como toohandle vários tipos de dados de leitura dentro e fora de saudação [Executar Script R] [ execute-r-script] módulo.

código completo Olá desta seção é no arquivo zip de saudação que você baixou anteriormente.

### <a name="load-and-check-data-in-machine-learning-studio"></a>Carregar e verificar dados no Studio de Machine Learning
#### <a id="loading"></a>Carregar conjunto de dados Olá
Começaremos Carregando Olá **csdairydata.csv** arquivo no estúdio de aprendizado de máquina do Azure.

* Inicie seu ambiente do Azure Machine Learning Studio.
* Clique em **+ novo** em Olá inferior esquerdo da tela e selecione **conjunto de dados**.
* Selecione **do arquivo Local**e, em seguida, **procurar** tooselect arquivo de saudação.
* Verifique se você selecionou **arquivo CSV genérico com cabeçalho (. csv)** como tipo Olá Olá conjunto de dados.
* Clique em marca de seleção de saudação.
* Após Olá conjunto de dados foi carregado, você deve ver Olá novo conjunto de dados clicando em Olá **conjuntos de dados** guia.  

#### <a name="create-an-experiment"></a>Criar uma experiência
Agora que temos alguns dados no estúdio de aprendizado de máquina, é preciso toocreate uma análise de saudação do experimento toodo.  

* Clique em **+ novo** em Olá inferior esquerda e selecione **experimento**, em seguida, **experiência em branco**.
* Você pode nomear sua experiência selecionando e modificando, Olá **experimento criado em...**  título na parte superior de saudação da página de saudação. Por exemplo, a alteração muito**AC Laticínios Analysis**.
* Esquerda de saudação da página de teste hello, expanda **conjuntos de dados salvos**e, em seguida, **Meus conjuntos de dados**. Você deve ver Olá **cadairydata.csv** que você carregou anteriormente.
* Saudação de arrastar e soltar **csdairydata.csv dataset** no experimento hello.
* Em Olá **pesquisa experimentar itens** caixa na parte superior de saudação do painel esquerdo hello, tipo [Executar Script R][execute-r-script]. Você verá o módulo de saudação aparecem na lista de pesquisa de saudação.
* Saudação de arrastar e soltar [Executar Script R] [ execute-r-script] módulo na sua paleta.  
* Conecte a saída de saudação do hello **csdairydata.csv dataset** entrada mais à esquerda do toohello (**Dataset1**) de saudação [Executar Script R][execute-r-script].
* **Não se esqueça de tooclick em 'Salvar'!**  

Agora seu teste deve ser similar a Figura 3.

![Olá AC Laticínios análise fazer experiências com o conjunto de dados e o módulo Executar Script R][3]

*Figura 3. Olá AC Laticínios análise fazer experiências com o conjunto de dados e o módulo Executar Script R.*

#### <a name="check-on-hello-data"></a>Verificar dados saudação
Vamos dar uma olhada nos dados de saudação que carregou em nossa experiência. Na experiência de hello, clique em saída Olá Olá **cadairydata.csv dataset** e selecione **visualizar**. Você deve ver algo semelhante à Figura 4.  

![Resumo do conjunto de dados de cadairydata.csv Olá][4]

*Figura 4. Resumo do conjunto de dados de cadairydata.csv hello.*

Nessa exibição, vemos muitas informações úteis. Podemos ver Olá primeiro várias linhas de conjunto de dados. Se selecionamos uma coluna, Olá seção de estatísticas mostra mais informações sobre a coluna de saudação. Por exemplo, linha de tipo de recurso Olá mostra quais tipos de dados no estúdio de aprendizado de máquina do Azure atribuída toohello coluna. É ter uma olhada rápida assim uma verificação de integridade válida antes de começar toodo qualquer trabalho sério.

### <a name="first-r-script"></a>Primeiro script R
Vamos criar um simple tooexperiment de script R primeiro no estúdio de aprendizado de máquina do Azure. Posso ter criado e testado Olá RStudio script a seguir.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Agora, preciso tootransfer tooAzure esse script estúdio de aprendizado de máquina. Eu poderia simplesmente recortar e colar. No entanto, nesse caso, eu vou transferir o meu script R por meio de um arquivo zip.

### <a name="data-input-toohello-execute-r-script-module"></a>Módulo de executar Script R de toohello de entrada de dados
Vamos dar uma olhada nos Olá entradas toohello [Executar Script R] [ execute-r-script] módulo. Neste exemplo, lê dados Laticínios do hello Califórnia em Olá [Executar Script R] [ execute-r-script] módulo.  

Há três entradas possíveis para Olá [Executar Script R] [ execute-r-script] módulo. Você pode usar qualquer uma ou todas essas entradas, dependendo do seu aplicativo. Também é perfeitamente razoável toouse um R script que não precisa de entrada em todos os.  

Vamos dar uma olhada em cada um desses inputs, indo de tooright à esquerda. Você pode ver os nomes de saudação de cada uma das entradas de saudação colocando o cursor sobre entrada hello e lendo a dica de ferramenta hello.  

#### <a name="script-bundle"></a>Pacote de script
Olá entrada de pacote de Script permite que você toopass Olá conteúdo de um arquivo zip em [Executar Script R] [ execute-r-script] módulo. Você pode usar uma saudação comandos tooread Olá conteúdo Olá zip arquivo a seguir em seu código R.

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> O aprendizado de máquina do Azure trata arquivos ZIP hello como se eles estão em Olá src / diretório, portanto, você precisa tooprefix nomeia o arquivo com este nome de diretório. Por exemplo, se hello zip contém arquivos Olá `yourfile.R` e `yourData.rdata` na raiz de saudação do zip hello, endereço como `src/yourfile.R` e `src/yourData.rdata` ao usar `source` e `load`.
> 
> 

Já discutimos conjuntos de dados de carregamento no [Carregando conjunto de dados Olá](#loading). Depois de ter criado e testado o script hello R mostrado na seção anterior hello, Olá a seguir:

1. Salve o script hello R em um. Arquivo de R. Eu chamo meu arquivo script "simpleplot.R". Aqui está o conteúdo de saudação.
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. Crie um arquivo zip e copie o script no arquivo zip. No Windows, clique com botão direito no arquivo hello e selecione **enviar para**e, em seguida, **pasta compactada**. Isso criará um novo arquivo zip que contém hello "simpleplot. Arquivo de R".
3. Adicionar seu arquivo toohello **conjuntos de dados** no estúdio de aprendizado de máquina, especificando o tipo hello como **zip**. Agora você deve ver o arquivo zip de saudação em seus conjuntos de dados.
4. Arrastar e soltar Olá zip no **conjuntos de dados** para Olá **tela ML Studio**.
5. Conecte a saída de saudação do hello **zip dados** ícone toohello **pacote de Script** entrada de saudação [Executar Script R] [ execute-r-script] módulo.
6. Saudação de tipo `source()` função com o nome do arquivo zip na janela de código Olá para Olá [Executar Script R] [ execute-r-script] módulo. No meu caso, digitei `source("src/simpleplot.R")`.  
7. Lembre-se de clicar em **Salvar**.

Quando essas etapas forem concluídas, Olá [Executar Script R] [ execute-r-script] módulo executará Olá R script no arquivo zip de saudação quando experimento Olá é executado. Agora seu teste deve ser semelhante à Figura 5.

![Teste usando o script de R compactado][6]

*Figura 5. Experimente usar o R script compactado.*

#### <a name="dataset1"></a>Dataset1
Você pode passar uma tabela retangular de código de tooyour R dados usando entrada hello Dataset1. Em nosso Olá script simples `maml.mapInputPort(1)` função lê dados saudação da porta 1. Esses dados, em seguida, são atribuídos o nome da variável dataframe tooa em seu código. Em nosso script simple a primeira linha hello de código executa atribuição hello.

    cadairydata <- maml.mapInputPort(1)

Execute seu teste clicando no hello **executar** botão. Ao término da execução de saudação, clique em Olá [Executar Script R] [ execute-r-script] módulo e depois clique em **Exibir log de saída** no painel de propriedades de saudação. Uma nova página deve aparecer em seu navegador mostrando o conteúdo de saudação do arquivo de saída. log hello. Quando você rolar para baixo, você verá algo parecido com hello seguinte.

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

Mais para baixo Olá página é informações mais detalhadas sobre colunas de saudação, que será parecida com a seguinte hello.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

Esses resultados são principalmente conforme o esperado, com 228 observações e 9 colunas no dataframe de saudação. Podemos ver os nomes de coluna hello, tipo de dados de saudação R e um exemplo de cada coluna.

> [!NOTE]
> Essa mesma impressão há convenientemente da saudação saída dispositivo R Olá [Executar Script R] [ execute-r-script] módulo. Vamos discutir as saídas de saudação do hello [Executar Script R] [ execute-r-script] módulo na próxima seção, Olá.  
> 
> 

#### <a name="dataset2"></a>Dataset2
Olá, comportamento de entrada hello Dataset2 é idêntico toothat de Dataset1. Usando essa entrada, você pode passar uma segunda tabela retangular de dados para o seu código R. Olá função `maml.mapInputPort(2)`, com argumento Olá 2, é usado toopass esses dados.  

### <a name="execute-r-script-outputs"></a>Execute as saídas do Script R
#### <a name="output-a-dataframe"></a>Exibir um dataframe
Você pode extrair conteúdo de saudação de um dataframe de R como uma tabela retangular pela porta Olá Dataset1 resultado usando Olá `maml.mapOutputPort()` função. Em nosso script R simple, isso é feito por Olá linha a seguir.

    maml.mapOutputPort('cadairydata')

Após a experiência de saudação em execução, clique em Olá porta de saída de resultado Dataset1 e, em seguida, clique em **visualizar**. Você deve ver algo como na Figura 6.

![visualização de saudação da saída de saudação do hello dados Laticínios Califórnia][7]

*Figura 6. visualização de saudação da saída de saudação do hello dados Laticínios Califórnia.*

Esta saída é entrada toohello idênticos, exatamente como esperado.  

### <a name="r-device-output"></a>Saída do Dispositivo R
Olá saída de dispositivo de hello [Executar Script R] [ execute-r-script] módulo contém a saída de mensagens e elementos gráficos. As duas mensagens de erro padrão e de saída padrão de R são enviadas toohello dispositivo R porta de saída.  

Olá tooview R dispositivo de saída, clique na porta hello e, em seguida, em **visualizar**. Podemos ver a saída de saudação padrão e erro padrão do script hello R na Figura 7.

![Saída padrão e erro padrão de saudação porta dispositivo R][8]

*Figura 7. Saída padrão e erro padrão de saudação porta do dispositivo de R.*

Rolando para baixo, consulte a saída de gráficos de saudação do nosso script R na Figura 8.  

![Saída de elementos gráficos da saudação porta dispositivo R][9]

*Figura 8. Gráficos de saída de hello porta do dispositivo de R.*  

## <a id="filtering"></a>Filtragem de dados e transformação
Nesta seção vamos realizar algumas filtragem básica de dados e operações de transformação em Olá dados Laticínios Califórnia. Ao final desta seção Olá teremos dados em um formato adequado para a criação de um modelo analítico.  

Mais especificamente, nesta seção vamos executar várias tarefas de transformação e de limpeza de dados comuns: transformação de tipo, filtragem por dataframes, adição de novas colunas computadas e transformações de valor. Este plano de fundo deve ajudá-lo a lidar com hello muitas variações em problemas do mundo real.

código de R completo Olá para essa seção está disponível no arquivo zip de saudação que você baixou anteriormente.

### <a name="type-transformations"></a>Transformações de tipo
Agora que nós pode ler dados de laticínios de Califórnia de Olá em código Olá Olá R [Executar Script R] [ execute-r-script] módulo, precisamos tooensure que dados Olá nas colunas de saudação tem tipo hello pretendido e o formato.  

R é uma linguagem tipada dinamicamente, o que significa que os tipos de dados são forçados de um tooanother conforme necessário. tipos de dados atômico de saudação em R incluem numérica, lógica e de caractere. tipo de fator de saudação é toocompactly usado armazenar dados categóricos. Você pode encontrar mais informações sobre tipos de dados em referências de saudação em [Apêndice B - leituras](#appendixb).

Quando dados de tabela é lido em R de uma fonte externa, é sempre uma saudação de toocheck boa ideia resultante tipos nas colunas de saudação. Você pode desejar uma coluna de tipo de caractere, mas em muitos casos isso aparecerá como fator ou vice-versa. Em outros casos, uma coluna que você acha que deve ser numérica é representada por dados de caracteres, por exemplo, '1,23' em vez de 1,23 como número de ponto flutuante.  

Felizmente, é fácil tooconvert um tipo tooanother, desde que o mapeamento é possível. Por exemplo, não é possível converter 'Nevada' em um valor numérico, mas você pode converter tooa fator (variável categórica). Um outro exemplo, você pode converter um numérico 1 em um caractere “1” ou um fator.  

sintaxe de saudação para qualquer uma dessas conversões é simple: `as.datatype()`. Essas funções de conversão de tipo incluem o seguinte hello.

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

Observando os tipos de dados Olá Olá de colunas de nós entrada na seção anterior Olá: todas as colunas são do tipo numérico, exceto Olá coluna rotulada 'Month', que é o caractere de tipo. Vamos converter esse fator tooa e Olá resultados de teste.  

Posso ter excluído linha hello que criou a matriz de scatterplot hello e adicionou uma linha convertendo o fator de tooa de coluna de 'Month' hello. Em minha experiência, apenas será recortar e colar o código Olá R na janela de código de saudação do hello [Executar Script R] [ execute-r-script] módulo. Você também pode atualizar o arquivo zip de saudação e carregá-lo tooAzure estúdio de aprendizado de máquina, mas isso leva várias etapas.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Vamos executar esse código e examinar o log de saída Olá para Olá script R. dados relevantes de saudação do log de saudação são mostrados na Figura 9.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 9. Resumo de dataframe de saudação com uma variável de fator.*

tipo de saudação do mês deve agora dizer '**fator com 14 níveis**'. Este é um problema, já que há somente 12 meses no ano de saudação. Você também pode verificar toosee que Olá tipo em **visualizar** de conjunto de dados de resultado de hello porta é '**categórico**'.

problema de saudação é que hello 'Month', coluna sistematicamente não foi codificada. Em alguns casos, um mês é chamado de abril e, em outros, é abreviado como abril. É possível resolver esse problema, cortar caracteres de too3 de cadeia de caracteres de saudação. linha de saudação de código agora Olá seguinte aparência:

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

Execute novamente o teste de saudação e exibir o log de saída de hello. Olá esperado de resultados são mostrados na Figura 10.  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 10. Resumo de dataframe de saudação com o número correto de níveis de fator.*

Nossa variável fator agora tem 12 níveis de saudação desejado.

### <a name="basic-data-frame-filtering"></a>Filtragem de dataframe básico
Os dataframes R oferecem suporte a recursos avançados de filtragem. Conjuntos de dados podem ser subdivididos usando filtros lógicos em linhas ou colunas. Em muitos casos, serão necessários critérios complexos de filtro. Olá referências em [Apêndice B - leituras](#appendixb) contêm exemplos abrangentes de filtragem de quadros de dados.  

Há algumas filtragens que devemos fazer em nosso conjunto de dados. Se você observar colunas Olá Olá cadairydata dataframe, você verá duas colunas desnecessárias. coluna primeiro Olá contém apenas um número de linha, que não é muito útil. Olá segunda coluna, Year.Month, contém informações redundantes. Podemos facilmente pode excluir essas colunas usando Olá código R a seguir.

> [!NOTE]
> De agora nesta seção, vou apenas Mostrar você Olá código adicional que estou adicionando Olá [Executar Script R] [ execute-r-script] módulo. Vou adicionar cada nova linha **antes de** Olá `str()` função. Posso usar esta função tooverify os resultados no estúdio de aprendizado de máquina do Azure.
> 
> 

Adicionar Olá após linha toomy R código em Olá [Executar Script R] [ execute-r-script] módulo.

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

Executar esse código em sua experiência e verificar o resultado de saudação do log de saída de hello. Esses resultados são mostrados na Figura 11.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 11. Resumo de dataframe de saudação com duas colunas é removido.*

Boas notícias! Podemos obter resultados Olá esperado.

### <a name="add-a-new-column"></a>Adicionar uma nova coluna
modelos de série temporal toocreate será conveniente toohave uma coluna que contém Olá meses desde o início de saudação do MTS hello. Criaremos uma nova coluna “Month.Count”.

toohelp organizar código Olá vamos criar nossa primeira função simple, `num.month()`. Em seguida, aplicaremos toocreate essa função uma nova coluna em dataframe de saudação. Olá novo código é da seguinte maneira.

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

Agora execute experimento Olá atualizado e use Olá log tooview Olá resultados. Esses resultados são mostrados na Figura 12.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 12. Resumo de dataframe de saudação com coluna adicional hello.*

Parece que tudo está funcionando. Temos a nova coluna Olá com valores esperados de saudação em nosso dataframe.

### <a name="value-transformations"></a>Transformações de valor
Nesta seção vamos realizar algumas transformações simples nos valores hello algumas das colunas de saudação do nosso dataframe. idioma Olá R suporta transformações de valor quase arbitrário. Olá referências em [Apêndice B - leitura adicional](#appendixb) contêm exemplos extensivos.

Se você examinar os valores hello em resumos de saudação do nosso dataframe você verá algo ímpar aqui. Há mais sorvetes do que leite produzido na Califórnia? Não, claro não, pois isso faz sentido, sad como esse fato pode ser toosome de nós amantes sorvete. unidades de saudação são diferentes. preço Hello está em unidades de nós libras, leite é em unidades de 1 milhão libras dos EUA, sorvete é em unidades de 1.000 nos galões e madeira de casa cheese está em unidades de libra de 1.000 dos EUA. Supondo que sorvete pondera cerca de 6,5 libras por galão, podemos facilmente Olá multiplicação tooconvert esses valores para que eles estão todos em unidades iguais de libra 1.000.

Para nosso modelo de previsão, usamos um modelo de multiplicação para tendência e ajuste sazonal desses dados. Uma transformação de log nos permite toouse um modelo linear, simplificar esse processo. É possível aplicar transformação de log Olá no hello mesma função onde multiplicador Olá é aplicado.

Em Olá código a seguir, definir uma nova função, `log.transform()`e aplicá-lo toohello linhas contendo valores numéricos de saudação. Olá R `Map()` função é usada tooapply Olá `log.transform()` função toohello selecionar colunas de dataframe de saudação. `Map()`é muito semelhante`apply()` , mas permite que mais de uma lista de função de toohello de argumentos. Observe que uma lista de multiplicadores fornece Olá segundo argumento toohello `log.transform()` função. Olá `na.omit()` função é usada como um pouco de limpeza tooensure não temos ausente ou indefinidos valores hello dataframe.

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

Há bastante aconteça bit no hello `log.transform()` função. A maioria desse código está verificando problemas potenciais com argumentos de saudação ou lidar com exceções, que ainda podem surgir durante os cálculos de saudação. Apenas algumas linhas do código realmente Olá cálculos.

Olá objetivo programação defesa Olá é falha de saudação tooprevent de uma única função que impede o processamento de continuar. Uma falha abrupta de uma análise de execução longa pode ser muito frustrante para os usuários. tooavoid nessa situação, o padrão de valores de retorno devem ser escolhidos que limitará danificar toodownstream processamento. Uma mensagem também é produzido tooalert usuários que algo deu errado.

Se você não estiver programação toodefensive usados em R, todo esse código pode parecer um pouco difícil. Eu orientará você pelas etapas principais hello:

1. Um vetor de quatro mensagens é definido. Essas mensagens são usadas toocommunicate informações sobre alguns Olá possíveis erros e exceções que podem ocorrer com este código.
2. Posso retornar um valor NA para cada caso. Há muitas outras possibilidades que podem ter menos efeitos colaterais. Pode retornar um vetor de zeros ou vetor de entrada original hello, por exemplo.
3. Verificações são executadas na função de toohello hello argumentos. Em cada caso, se for detectado um erro, será retornado um valor padrão e uma mensagem é produzida pelo Olá `warning()` função. Estou usando `warning()` em vez de `stop()` como Olá último terminará em execução, exatamente o que estou tentando tooavoid. Observe que eu escrevi este código em um estilo de procedimento, pois nesse caso uma abordagem funcional me parece complexa e obscura.
4. cálculos de log Olá são encapsulados em `tryCatch()` para que as exceções não causará uma interrupção abrupto tooprocessing. Sem `tryCatch()` , a maioria dos erros gerada pelas funções de R resulta em um sinal de interrupção, que faz exatamente isso.

Execute esse código R em sua experiência e examinar Olá impressas saída no arquivo de saída. log hello. Agora você verá valores hello transformado Olá quatro colunas na saudação de log, conforme mostrado na Figura 13.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 13. Resumo da saudação transformados valores hello dataframe.*

Podemos ver que foram transformados valores hello. Agora, a produção de leite excede bastante a produção de todos os outros produtos derivados do leite, lembrando que agora estamos analisando uma escala logarítmica.

Neste momento, os dados são limpos e estamos prontos para a modelagem. Observando a visualização de saudação resumida de Olá saído do conjunto de dados de resultado de nossa [Executar Script R] [ execute-r-script] módulo, você verá a coluna de 'Mês' hello é 'Categórico' com 12 valores exclusivos, novamente, assim como queremos .

## <a id="timeseries"></a>Análise de correlação e objetos de série temporal
Nesta seção explorar alguns objetos básicos de série de tempo de R e analisar correlações Olá entre algumas das variáveis de saudação. Nosso objetivo é toooutput um dataframe contendo Olá correlação emparelhadas informações em vários atrasos.

código de R completo Olá desta seção é no arquivo zip de saudação que você baixou anteriormente.

### <a name="time-series-objects-in-r"></a>Objetos de série temporal em R
Como já mencionado, as série de tempo são uma série de valores de dados indexados por tempo. Objetos de série de tempo de R são usada toocreate e gerenciar o índice de tempo de saudação. Há várias vantagens toousing tempo série objetos. Objetos de série de tempo de liberá-lo da saudação muitos detalhes de gerenciamento Olá série índice valores de hora são encapsulados no objeto de saudação. Além disso, objetos de série de tempo permitem que você toouse Olá muitos métodos de série de tempo para plotar, impressão, modelagem, etc.

Olá POSIXct classe de série de tempo é comumente usado e é relativamente simple. Essa classe de série de tempo mede o tempo do início de saudação da época hello, 1º de janeiro de 1970. Vamos usar objetos de série de tempo POSIXct neste exemplo. Outras classes de objeto de série de tempo amplamente utilizados em R incluem zoo e xts, série temporal extensível.
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>Exemplo de objeto de série temporal
Vamos começar com o nosso exemplo. Arraste e solte um **novo** módulo [Executar Script R][execute-r-script] em seu experimento. Conectar porta de saída Olá Dataset1 de resultado de saudação existentes [Executar Script R] [ execute-r-script] Olá nova porta de entrada do módulo toohello Dataset1 [Executar Script R] [ execute-r-script] módulo.

Como fiz exemplos primeiro Olá, como podemos andamento por meio do exemplo hello, alguns momentos, vou mostrar apenas Olá incrementais mais linhas de código R em cada etapa.  

#### <a name="reading-hello-dataframe"></a>Olá dataframe de leitura
Como uma primeira etapa, vamos um dataframe de leitura e assegure-se de que podemos obter resultados de saudação esperado. Olá código a seguir deve fazer o trabalho de saudação.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

Agora, execute o teste de saudação. log de saudação da nova forma de executar Script R Olá deve parecer com a Figura 14.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

*Figura 14. Resumo de dataframe de saudação no módulo Executar Script R de saudação.*

Esses dados são de formato e tipos de saudação esperado. Observe que a coluna de 'Month' hello é do fator de tipo e tem Olá esperado um número de níveis.

#### <a name="creating-a-time-series-object"></a>Criando um objeto de série temporal
Precisamos tooadd um dataframe de tooour de objeto de série de tempo. Substitua o código de atual de saudação pelo seguinte hello, que adiciona uma nova coluna de classe POSIXct.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

Agora, verifique o log de saudação. Deve se parecer com a Figura 15.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Figura 15. Resumo de dataframe de saudação com um objeto de série de tempo.*

Podemos ver da saudação resumida que coluna nova Olá na verdade é da classe POSIXct.

### <a name="exploring-and-transforming-hello-data"></a>Explorar e transformar dados Olá
Vamos explorar algumas das variáveis de saudação deste conjunto de dados. Uma matriz de scatterplot é uma boa maneira tooproduce uma olhada rápida. Eu estou substituindo Olá `str()` função no código de R anterior Olá com a seguinte linha de saudação.

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

Execute esse código e veja o que acontece. plotagem Olá produzida em Olá porta dispositivo R deve parecer com a Figura 16.

![Matriz de dispersão de variáveis selecionadas][17]

*Figura 16. Matriz de dispersão de variáveis selecionadas.*

Há algumas estruturas estranha em relações de saudação entre essas variáveis. Talvez isso surge de tendências nos dados de saudação e de fato Olá que não adotaram variáveis hello.

### <a name="correlation-analysis"></a>Análise de correlação
análise de correlação tooperform precisamos tooboth eliminação de tendência e padronizar variáveis hello. Podemos simplesmente usar Olá R `scale()` função, que centraliza tanto dimensiona variáveis. Essa função também pode ser executada mais rapidamente. No entanto, quero tooshow é um exemplo de programação defesa em R.

Olá `ts.detrend()` função abaixo executa ambas essas operações. Hello seguintes duas linhas de código da tendência dados saudação e, em seguida, padronizar valores de saudação.

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

Há bastante aconteça bit no hello `ts.detrend()` função. A maioria desse código está verificando problemas potenciais com argumentos de saudação ou lidar com exceções, que ainda podem surgir durante os cálculos de saudação. Apenas algumas linhas do código realmente Olá cálculos.

Já abordamos a um exemplo de programação defensiva em [Transformações de valor](#valuetransformations). Os dois blocos de computação estão encapsulados em `tryCatch()`. Para alguns erros faz sentido tooreturn Olá entrada vetor original e em outros casos, retornar um vetor de zeros.  

Observe que a regressão linear de saudação usado para eliminação de tendência é uma regressão de série de tempo. variável de indicador de saudação é um objeto de série de tempo.  

Uma vez `ts.detrend()` definido aplicá-lo toohello variáveis de interesse em nosso dataframe. Nós deve forçar a lista resultante de saudação criada pelo `lapply()` dataframe toodata usando `as.data.frame()`. Devido a defesa aspectos de `ts.detrend()`, processamento de saudação de corrigir a tooprocess falha uma das variáveis de saudação não impedirá que outros.  

a linha final Olá de código cria um par scatterplot. Depois de executar código Olá R, resultados Olá Olá scatterplot são mostrados na Figura 17.

![Emparelhar a dispersão da série temporal padronizada e sem tendências][18]

*Figura 17. Emparelhe o scatterplot da séries de tempo padronizada e sem tendências.*

Você pode comparar esses toothose resultados mostrado na Figura 16. Com hello tendência removido e Olá variáveis padronizados, podemos ver muito menos estrutura em relações de saudação entre essas variáveis.

correlações de saudação do Hello código toocompute como objetos de R ccf é da seguinte maneira.

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

Executar esse código produz log Olá mostrado na Figura 18.

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

*Figura 18. Lista de ccf objetos da análise de correlação de pares de saudação.*

Há um valor de correlação para cada intervalo. Nenhum desses valores de correlação é grande o suficiente toobe significativa. Podemos, portanto, concluir que é possível modelar cada variável de forma independente.

### <a name="output-a-dataframe"></a>Exibir um dataframe
Podemos ter computada correlações emparelhadas hello como uma lista de objetos de R ccf. Isso apresenta um pequeno problema como Olá porta de saída do conjunto de dados de resultado realmente requer um dataframe. Além disso, Olá ccf próprio objeto for uma lista e queremos apenas os valores hello no primeiro elemento Olá desta lista, correlações Olá no hello atrasos vários.

Olá código extrai Olá latência valores a seguir da lista de saudação de objetos de ccf, que são listas.

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

Olá primeira linha de código é um pouco confusa e alguma explicação pode ajudá-lo a entender a ele. Trabalhando dentro para fora da saudação temos seguinte hello:

1. Olá '**[[**'operator com argumento de saudação'**1**' selecionará Olá vetor de correlações em atrasos de saudação do primeiro elemento de saudação da lista de objetos ccf hello.
2. Olá `do.call()` função se aplica a saudação `rbind()` função sobre os elementos de saudação da lista de saudação retorna ao `lapply()`.
3. Olá `data.frame()` função converte o resultado de saudação produzido por `do.call()` tooa dataframe.

Observe que os nomes de linha de saudação em uma coluna de dataframe de saudação. Isso preserva a nomes de linha hello quando eles são produzidos por Olá [Executar Script R][execute-r-script].

A execução de código Olá produz saída de hello mostrada na Figura 19 quando eu **visualizar** Olá saída em Olá porta do conjunto de dados de resultado. nomes de linha de saudação estão na primeira coluna de hello, conforme o esperado.

![Resultados da análise de correlação de saudação][20]

*Figura 19. Resultados da análise de correlação de saudação de saída.*

## <a id="seasonalforecasting"></a>Exemplo de série temporal: previsão sazonal
Nossos dados agora estão em um formato adequado para análise e determinamos que não há nenhum significativas correlações entre variáveis de saudação. Vamos continuar e criar um modelo de previsão de série de tempo. Usando esse modelo preveja a produção de leite Califórnia para Olá 12 meses de 2013.

Nosso modelo de previsão terá dois componentes, um componente de tendência e um componente sazonal. Previsão concluída Olá é produto Olá esses dois componentes. Esse tipo de modelo é conhecido como modelo de multiplicação. alternativa de saudação é um modelo aditivo. Nós já aplicou um variáveis de toohello de transformação de log de interesse, o que torna essa análise manejável.

código de R completo Olá desta seção é no arquivo zip de saudação que você baixou anteriormente.

### <a name="creating-hello-dataframe-for-analysis"></a>Criando dataframe Olá para análise
Comece adicionando um **novo** [Executar Script R] [ execute-r-script] experimento de tooyour do módulo. Conectar Olá **conjunto de dados de resultado** saída de hello existentes [Executar Script R] [ execute-r-script] módulo toohello **Dataset1** entrada do novo módulo de saudação. resultado de saudação deve ser semelhante a Figura 20.

![Olá experimentar Olá novo Executar Script R módulo adicionado][21]

*Figura 20. Olá experimentar Olá novo Executar Script R módulo adicionado.*

Como com a análise de correlação de saudação que acabou de concluir, é preciso tooadd uma coluna com um objeto de série de tempo de POSIXct. saudação de código a seguir vai fazer exatamente isso.

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

Execute este código e examinar o log de saudação. resultado de saudação deve parecer com a Figura 21.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Figura 21. Um resumo de dataframe de saudação.*

Com esse resultado, estamos pronto toostart nossa análise.

### <a name="create-a-training-dataset"></a>Criar um conjunto de dados de treinamento
Com o dataframe de saudação construída, é preciso toocreate um conjunto de dados de treinamento. Esses dados incluirá todas observações Olá exceto Olá últimas 12, do ano Olá 2013, o que é o nosso conjunto de dados de teste. seguir Olá subconjuntos Olá dataframe de código e cria gráficos de variáveis de produção e preço Laticínios hello. Em seguida, criar gráficos de saudação quatro variáveis de produção e preço. Uma função anônima é usado toodefine alguns amplia a plotagem e, em seguida, iterar pela lista de saudação de saudação outros dois argumentos com `Map()`. Se você estiver pensando que um loop funcionaria bem aqui, você está certo. Mas, como R é uma linguagem funcional, estou lhe mostrando uma abordagem funcional.

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

Executar código Olá produz Olá plota série de série temporal da saída de dispositivo R Olá mostrada na Figura 22. Observe que eixo de tempo de saudação em unidades de datas, um benefício interessante do tempo de saudação série plotar método.

![Primeira das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Segunda das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Terceira das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Quarta das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*Figura 22. Plotagens de série temporal dos dados de produção e preço de derivados do leite da Califórnia.*

### <a name="a-trend-model"></a>Um modelo de tendência
Tendo criado um objeto de série de tempo e tendo uma olhada em dados Olá, vamos começar tooconstruct um modelo de tendência para Olá dados de produção leite Califórnia. Podemos fazer isso com uma regressão da série de tempo. No entanto, é claro de plotagem Olá que iremos precisa de mais de um coeficiente e interceptar tooaccurately modelar Olá observado tendências nos dados de treinamento de saudação.

Considerando pequena escala Olá dos dados hello, será criar modelo Olá tendência em RStudio e, em seguida, recorte e cole o modelo resultante Olá em aprendizado de máquina do Azure. O RStudio fornece um ambiente adequado para esse tipo de análise interativa.

Como a primeira tentativa, tentarei uma regressão polinomial com too3 é inicializado. Existe um perigo real de sobreajuste desses tipos de modelos. Portanto, é melhor termos de ordem alta tooavoid. Olá `I()` função inibe a interpretação de conteúdo da saudação (interpreta conteúdo Olá 'como está') e permite que você toowrite uma função interpretada literalmente em uma equação de regressão.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

Isso gera o seguinte hello.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

Dos valores de P (Pr (> | t |)) na saída, podemos ver que Olá quadrado termo não pode ser significativo. Vou usar Olá `update()` função toomodify esse modelo por descartar Olá quadrado termo.

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

Isso gera o seguinte hello.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

Assim parece melhor. Todos os termos de saudação são significativos. No entanto, o valor de 2e-16 de saudação é um valor padrão e não deve ser tomada muito sério.  

Como um teste de integridade, vamos fazer um gráfico de série de tempo de saudação dados de produção Laticínios Califórnia com curva de tendência Olá mostrada. Adicionei Olá código Olá aprendizado de máquina a seguir [Executar Script R] [ execute-r-script] toocreate de modelo (não RStudio) Olá modelo e faça um gráfico. Olá resultado é mostrado na Figura 23.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Dados de produção de leite da Califórnia com o modelo de tendência mostrado](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*Figura 23. Dados de produção leite da Califórnia com o modelo de tendência mostrado.*

Parece que o modelo de tendência Olá se adapta a saudação dados muito bem. Além disso, não parece toobe evidência de ajuste excessivo, como ímpar wiggles na curva do modelo de saudação.  

### <a name="seasonal-model"></a>Modelo sazonal
Com um modelo de tendência em mãos, precisamos toopush em e incluir efeitos sazonais hello. Usaremos o mês de saudação do ano de saudação como uma variável fictícia em vigor do hello modelo linear toocapture Olá mês a mês. Observe que quando você introduzir variáveis fator em um modelo, interceptação Olá não deve computada. Se você não fizer isso, fórmula Olá é excessivamente especificada e R descartará uma saudação desejado fatores, mas manter o termo de interceptação hello.

Como temos um modelo de tendência satisfatório podemos usar Olá `update()` Olá de tooadd função novo modelo existente toohello de termos. Olá -1 na fórmula de atualização Olá descarta o termo de interceptação hello. Continuar em RStudio momento hello:

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

Isso gera o seguinte hello.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

Podemos ver o modelo Olá não tem um termo de interceptação e tem 12 fatores significativos mês. Isso é exatamente o que queremos toosee.

Vamos fazer outra plotagem de série de tempo de saudação Califórnia produção Laticínios dados toosee como modelo sazonais hello está funcionando. Adicionei Olá código Olá aprendizado de máquina a seguir [Executar Script R] [ execute-r-script] toocreate Olá modelo e faça um gráfico.

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

Executar esse código no aprendizado de máquina do Azure produz plotagem Olá mostrada na Figura 24.

![Produção de leite da Califórnia com o modelo, incluindo efeitos sazonais](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*Figura 24. Produção de leite na Califórnia com o modelo dos efeitos sazonais.*

Olá, ajustar toohello dados mostrados na Figura 24 são incentivando em vez disso. Tendência de saudação e efeito sazonais de saudação (variação mensal) procure razoáveis.

Como outra verificação em nosso modelo, vamos dar uma olhada em restos Olá. Olá exemplo código a seguir calcula Olá valores previstos de nosso dois modelos, calcula restos Olá para modelo sazonais hello e plota, em seguida, dos resíduos para dados de treinamento de saudação.

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

plotagem residual Olá é mostrada na Figura 25.

![Restos de modelo de sazonais Olá para dados de treinamento Olá](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*Figura 25. Restos de modelo de sazonais Olá para dados de treinamento de saudação.*

Esses resíduos parecem razoáveis. Não há nenhuma estrutura específica, exceto o efeito de saudação do recessão Olá 2008 e 2009, o que nosso modelo não leva em conta particularmente bem.

plotagem de saudação mostrada na Figura 25 é útil para detectar qualquer padrões dependentes de tempo em restos Olá. abordagem de saudação explícita de computação e plotar resíduos Olá usei coloca restos Olá na ordem de tempo no gráfico de saudação. Se, em Olá outro lado, tinha plotados `milk.lm$residuals`, plotagem Olá não teria sido na ordem de tempo.

Você também pode usar `plot.lm()` tooproduce uma série de gráficos de diagnósticos.

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

Esse código gera uma série de gráficos de diagnóstico mostrados na Figura 26.

![Primeiro de diagnósticos gráficos para modelo sazonais Olá](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Segundo de gráficos de diagnósticos para o modelo sazonais Olá](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Terceiros de diagnósticos gráficos para modelo sazonais Olá](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Quarto de diagnósticos gráficos para modelo sazonais Olá](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*Figura 26. Diagnóstico plota para modelo sazonais hello.*

Há alguns pontos altamente influentes identificados nesses gráficos, mas nada toocause grande preocupação. Além disso, podemos ver de plotagem de Q-Q Normal Olá restos Olá são toonormally fechar distribuído, uma suposição importante para os modelos lineares.

### <a name="forecasting-and-model-evaluation"></a>Avaliação de previsão e modelo
Há apenas um toocomplete de toodo coisa mais nosso exemplo. Precisamos toocompute previsões e medir o erro de saudação em relação aos dados reais de saudação. Nossa previsão será usado para Olá 12 meses de 2013. Podemos pode computar uma medida de erro para essa previsão toohello real de dados que não faz parte de nosso conjunto de dados de treinamento. Além disso, é possível comparar o desempenho em Olá 18 anos de toohello de dados de treinamento 12 meses de dados de teste.  

São usadas várias métricas de desempenho de saudação toomeasure de modelos de série temporal. Em nosso caso, usaremos erro de raiz quadrada média (RMS) hello. Olá função a seguir calcula o hello RMS erro entre duas séries.  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

Assim como acontece com hello `log.transform()` função discutimos em hello "Valor transformações" seção, há muito código de recuperação a verificação e a exceção de erro nesta função. Princípios de saudação empregados são Olá mesmo. Olá o trabalho é realizado em dois lugares encapsulados em `tryCatch()`. Primeiro, série de tempo de saudação é exponentiated, já que temos trabalhado com logs de saudação de valores de saudação. Segundo, o erro real RMS Olá é computado.  

Vamos equipado com uma saudação de toomeasure função erro RMS, compilação e um dataframe contendo Olá RMS erros de saída. Podemos incluirá termos de modelo de tendência Olá sozinho e modelo completo de saudação com fatores sazonais. Olá código a seguir Olá trabalho usando modelos lineares dois Olá construímos.

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

Executando este código produz saída de hello mostrada na Figura 27 no hello porta de saída do conjunto de dados de resultado.

![Comparação de erros do RMS para modelos de saudação][26]

*Figura 27. Comparação de erros do RMS para modelos de saudação.*

A partir desses resultados, podemos ver que adicionando Olá fatores sazonais toohello modelo reduz o erro de RMS Olá significativamente. Não é muito surpreendente, erro Olá RMS para Olá dados de treinamento é um pouco menor que para saudação de previsão.

## <a id="appendixa"></a>Apêndice a: Guia tooRStudio
RStudio muito bem documentada, portanto neste apêndice fornecerei alguns links toohello seções principais da saudação RStudio documentação tooget que é iniciado.

1. Criando projetos
   
   Você pode organizar e gerenciar seu código R em projetos usando o RStudio. documentação de saudação que usa projetos pode ser encontrada em https://support.rstudio.com/hc/articles/200526207-Using-Projects.
   
   É recomendável que você siga estas instruções e cria um projeto para obter exemplos de código Olá R neste documento.  
2. Editar e executar código R
   
   O RStudio fornece um ambiente integrado para editar e executar código R. A documentação pode ser encontrada em https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.
3. Depurando
   
   O RStudio inclui recursos avançados de depuração. A documentação para esses recursos estão em https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.
   
   recursos de solução de problemas de ponto de interrupção de saudação são documentados em https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.

## <a id="appendixb"></a>APÊNDICE B: Leitura adicional
Este tutorial aborda Olá básico da programação de R de que você precisa toouse Olá linguagem R com o estúdio de aprendizado de máquina do Azure. Se você não estiver familiarizado com R, duas introduções estão disponíveis no CRAN:

* R para iniciantes por Emmanuel Paradis é toostart um bom lugar no http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.  
* Um tooR Introdução por W. N. Venables et. al. se aprofunda um pouco mais em http://cran.r-project.org/doc/manuals/R-intro.html.

Existem muitos livros sobre R que podem ajudá-lo a começar. Aqui estão alguns que considero úteis:

* Olá arte de programação R: um Tour de estatística Design de Software por Norman Matloff é tooprogramming uma excelente introdução em R.  
* Livro de receitas R por Paul Teetor fornece toousing uma abordagem problema e a solução R.  
* R in Action, por Robert Kabacoff, é outro livro introdutório útil. site do Hello complementar R rápida é um recurso útil em http://www.statmethods.net/.
* R Inferno por Patrick Burns é surpreendentemente divertido livros que lida com uma série de tópicos complicados e difícil que podem ser encontrados durante a programação no catálogo de r. hello estão disponível gratuitamente em http://www.burns-stat.com/documents/books/the-r-inferno/.
* Se você quiser um mergulho no tópicos avançados em R, dê uma olhada no catálogo Olá avançado R por Hadley Wickham. a versão online Olá deste livro está disponível gratuitamente em http://adv-r.had.co.nz/.

Um catálogo de pacotes de série de tempo de R pode ser encontrado no hello CRAN modo de exibição de tarefa para análise de série temporal: http://cran.r-project.org/web/views/TimeSeries.html. Para obter informações sobre pacotes de objeto de série de tempo específico, consulte a documentação toohello para que o pacote.

Catálogo de Olá MTS introdutório R por Paul Cowpertwait e Andrew Metcalfe fornece uma introdução toousing R para análise de série temporal. Muitos textos mais teóricos fornecem exemplos de R.

Alguns ótimos recursos na Internet:

* DataCamp: DataCamp ensina R no conforto de saudação do seu navegador com vídeos lições e exercícios de codificação. Há interativos tutoriais sobre técnicas de R mais recentes hello e pacotes. Consulte o tutorial de R livre interativo para o hello em https://www.datacamp.com/courses/introduction-to-r
* Um guia de Introdução ao R de Programiz https://www.programiz.com/r-programming
* A quick R tutorial, por Kelly Black, da Clarkson University, http://www.cyclismo.org/tutorial/R/
* Mais de 60 recursos de R listados em http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
