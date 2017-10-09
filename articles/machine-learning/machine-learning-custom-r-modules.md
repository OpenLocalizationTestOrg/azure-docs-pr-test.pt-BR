---
title: "aaaAuthor os módulos R personalizados no aprendizado de máquina do Azure | Microsoft Docs"
description: "Início rápido para a criação de módulos R personalizados no Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a>Criar módulos R personalizados no Azure Machine Learning
Este tópico descreve como tooauthor e implantar um módulo personalizado de R no aprendizado de máquina do Azure. Ele explica o que são módulos R personalizados e quais arquivos são usado toodefine-los. Ele ilustra como tooconstruct Olá arquivos que definem um módulo e como tooregister Olá módulo para implantação em um espaço de trabalho do aprendizado de máquina. Olá elementos e atributos usados na definição de saudação do módulo personalizado hello, em seguida, descritos mais detalhadamente. Como a funcionalidade auxiliar toouse arquivos e várias saídas também é abordado. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a>O que é um módulo R personalizado?
Um **módulo personalizado de** é um módulo definido pelo usuário que pode ser carregados tooyour espaço de trabalho e executado como parte de uma experiência de aprendizado de máquina do Azure. Um **módulo R personalizado** é um módulo personalizado que executa uma função R definida pelo usuário. **R** é uma linguagem de programação para a computação estatística e gráficos que é amplamente usada por cientistas estatísticos e para implementar algoritmos estatísticos. No momento, R é o único idioma de saudação tem suportado em módulos personalizados, mas o suporte para idiomas adicionais está programada para versões futuras.

Módulos personalizados têm **status de primeira classe** no aprendizado de máquina do Azure no sentido de saudação que podem ser usados apenas como qualquer outro módulo. Eles podem ser executados com outros módulos, incluídos em visualizações ou em experimentos publicados. Tem controle sobre o algoritmo Olá implementado pelo módulo de saudação, Olá toobe portas de entrada e saída usado, Olá parâmetros de modelagem e outros vários comportamentos de tempo de execução. Uma experiência que contém módulos personalizados também pode ser publicada em Olá Cortana Intelligence Galeria para facilitar o compartilhamento.

## <a name="files-in-a-custom-r-module"></a>Arquivos em um módulo R personalizado
Um módulo R personalizado é definido por um arquivo .zip que contém, no mínimo, dois arquivos:

* Um **arquivo de origem** que implementa a função hello R exposta pelo módulo Olá
* Um **arquivo de definição XML** que descreve a interface de módulo personalizado de saudação

Arquivos auxiliares adicionais também podem ser incluídos no arquivo. zip Olá que fornece a funcionalidade que pode ser acessada pelo módulo personalizado de saudação. Essa opção é discutida em Olá **argumentos** parte da seção de referência Olá **elementos no arquivo de definição de XML Olá** Olá quickstart exemplo a seguir.

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a>Exemplo de início rápido: definir, empacotar e registrar um módulo R personalizado
Este exemplo ilustra como tooconstruct Olá arquivos necessários para um módulo personalizado de R, empacotá-las em um arquivo zip e, em seguida, registre Olá módulo no seu espaço de trabalho do aprendizado de máquina. Olá arquivos de exemplo e o pacote zip exemplo podem ser baixados do [CustomAddRows.zip baixar arquivo](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).

## <a name="hello-source-file"></a>arquivo de origem Olá
Considere o exemplo hello de um **personalizado adicionar linhas** módulo que modifica a implementação padrão de saudação do hello **adicionar linhas** módulo usado tooconcatenate linhas (Observações) de dois conjuntos de dados (quadros de dados). saudação padrão **adicionar linhas** módulo acrescenta linhas Olá Olá segundo conjunto de dados de entrada toohello de end da saudação primeira entrada conjunto de dados usando Olá `rbind` algoritmo. Olá personalizado `CustomAddRows` função da mesma forma aceita dois conjuntos de dados, mas também aceita um parâmetro booliano de permuta como uma entrada adicional. Se o parâmetro de permuta hello está definido muito**FALSE**, ele retorna Olá mesmo conjunto de dados como Olá implementação padrão. Mas, se o parâmetro de troca de saudação é **TRUE**, função hello acrescenta linhas do primeiro conjunto de dados de entrada toohello-end do segundo conjunto de dados de saudação em vez disso. arquivo de CustomAddRows.R Olá que contém a implementação de saudação do hello R `CustomAddRows` função exposta pelo Olá **personalizado adicionar linhas** módulo tem Olá código R a seguir.

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a>arquivo de definição de XML Olá
tooexpose isso `CustomAddRows` função como um módulo de aprendizado de máquina do Azure, um arquivo de definição XML deve ser criada toospecify como Olá **personalizado adicionar linhas** módulo deve aparência e o comportamento. 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


É toonote crítico que Olá valor Olá **id** atributos de saudação **entrada** e **Arg** elementos no arquivo XML de saudação devem corresponder a nomes de parâmetro de função hello da saudação R o código no arquivo de CustomAddRows.R Olá exatamente: (*dataset1*, *dataset2*, e *permuta* no exemplo hello). Olá da mesma forma, o valor de saudação **entryPoint** atributo de saudação **idioma** elemento deve corresponder exatamente Olá nome da função hello no script hello R: (*CustomAddRows* exemplo hello). 

Por outro lado, Olá **id** atributo Olá **saída** elemento não corresponde tooany variáveis no script hello R. Quando mais de uma saída é necessária, basta retornar uma lista de função hello R com resultados colocados *em Olá mesma ordem* como **saídas** elementos são declarados no arquivo XML de saudação.

### <a name="package-and-register-hello-module"></a>Pacote e registrar o módulo de saudação
Salvar esses dois arquivos como *CustomAddRows.R* e *CustomAddRows.xml* e, em seguida, zip Olá dois arquivos juntos em uma *CustomAddRows.zip* arquivo.

tooregistê-los em seu espaço de trabalho do aprendizado de máquina, espaço de trabalho tooyour vá Olá estúdio de aprendizado de máquina, clique em Olá **+ novo** botão na parte inferior do hello e escolha **módulo -> do pacote ZIP** tooupload Olá novo **personalizado adicionar linhas** módulo.

![Carregar Zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

Olá **personalizado adicionar linhas** módulo agora está pronto toobe acessado por suas experiências de aprendizado de máquina.

## <a name="elements-in-hello-xml-definition-file"></a>Elementos no arquivo de definição de XML Olá
### <a name="module-elements"></a>Elementos de módulo
Olá **módulo** elemento é usado toodefine um módulo personalizado no arquivo XML de saudação. Vários módulos podem ser definidos em um arquivo XML usando vários elementos de **módulo** . Cada módulo no espaço de trabalho deve ter um nome exclusivo. Registrar um módulo personalizado com hello mesmo nome como um módulo personalizado existente e substitui módulo existente Olá com hello uma nova. Módulos personalizados no entanto, podem ser registrado com o mesmo nome como um módulo de aprendizado de máquina do Azure existente de saudação. Se assim, eles aparecem no hello **personalizado** categoria da paleta de módulo hello.

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


Dentro de saudação **módulo** elemento, você pode especificar dois elementos opcionais adicionais:

* um **proprietário** elemento que é incorporado em módulo Olá  
* um **descrição** elemento que contém o texto que é exibido na ajuda rápida para o módulo de saudação e quando você focaliza o módulo Olá Olá aprendizado de máquina da interface do usuário.

Regras para limites de caracteres em elementos de módulo hello:

* Olá valor Olá **nome** atributo Olá **módulo** elemento não deve exceder 64 caracteres de comprimento. 
* Olá conteúdo de saudação **descrição** elemento não deve exceder 128 caracteres.
* Olá conteúdo de saudação **proprietário** elemento não deve exceder 32 caracteres.

Resultados de um módulo podem ser determinísticos ou nondeterministic.* * por padrão, todos os módulos são considerados toobe determinística. Ou seja, dado um conjunto imutável de parâmetros de entrada e de dados, módulo Olá deve retornar Olá mesmos resultados eacRAND ou uma hora de functionh que é executado. Devido a esse comportamento, o estúdio de aprendizado de máquina do Azure repete somente módulos marcados como determinística se um parâmetro ou dados de entrada hello foi alterado. Retornando resultados de saudação em cache também fornece muito execução mais rápida de experimentos.

Há funções não determinísticas como RAND ou uma função que retorna Olá data ou hora atual. Se seu módulo usa uma função não determinística, você pode especificar que o módulo Olá é não determinística pela configuração Olá opcional **isDeterministic** atributo muito**FALSE**. Isso assegura que o módulo Olá é executado sempre que a experiência de saudação é executada, mesmo que hello módulo parâmetros de entrada e não foram alterados. 

### <a name="language-definition"></a>Definição de linguagem
Olá **idioma** elemento em seu arquivo de definição XML é o idioma de módulo personalizado de saudação do toospecify usado. Atualmente, R é Olá só tem suporte a idioma. Olá valor Olá **sourceFile** atributo deve ser o nome de saudação do arquivo de saudação R que contém Olá função toocall quando Olá módulo será executado. Esse arquivo deve ser parte do pacote de zip hello. Olá valor Olá **entryPoint** atributo é Olá nome da função hello está sendo chamada e deve corresponder a uma função válida definida com no arquivo de origem de saudação.

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a>Portas
Olá portas de entrada e saídas para um módulo personalizado são especificadas em elementos filho do hello **portas** seção do arquivo de definição XML de saudação. ordem de saudação desses elementos determina Olá layout experiente (UX) por usuários. primeiro filho de saudação **entrada** ou **saída** listados no hello **portas** elemento do arquivo XML de saudação torna-se a porta de entrada hello mais à esquerda no hello UX de aprendizado de máquina
Cada entrada e a porta de saída pode ter um opcional **descrição** elemento filho que especifica o texto de saudação mostrado quando você focaliza cursor do mouse Olá porta Olá Olá aprendizado de máquina da interface do usuário.

**Regras de portas**:

* O número máximo de **portas de entrada e saída** é de 8 para cada.

### <a name="input-elements"></a>Elementos de entrada
Portas de entrada permitem que você espaço de trabalho e a função de tooyour R toopass dados. Olá **tipos de dados** que têm suporte para portas de entrada são da seguinte maneira: 

**DataTable:** esse tipo é passado a função tooyour R como um data.frame. Na verdade, qualquer tipo (por exemplo, arquivos CSV ou arquivos ARFF) que é suportado pelo aprendizado de máquina e que é compatível com **DataTable** são data.frame tooa convertido automaticamente. 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

Olá **id** atributo associado a cada **DataTable** porta de entrada deve ter um valor exclusivo e esse valor deve corresponder com o parâmetro na função de R nomeado correspondente.
Opcional **DataTable** portas que não são transmitidas como entrada em um experimento ter valor Olá **nulo** função toohello passado R e portas de zip opcional serão ignoradas se Olá entrada não está conectada. Olá **é opcional** atributo é opcional para ambos os Olá **DataTable** e **Zip** tipos e é *false* por padrão.

**ZIP:** módulos personalizados podem aceitar um arquivo zip como entrada. Essa entrada é desempacotada no diretório de trabalho Olá R de sua função

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

Para módulos R personalizados, id de saudação para uma porta de Zip não tem toomatch quaisquer parâmetros de função hello R. Isso ocorre porque o arquivo zip de saudação é extraído automaticamente toohello R diretório de trabalho.

**Regras de entrada:**

* Olá valor Olá **id** atributo de saudação **entrada** elemento deve ser um nome de variável de R válido.
* Olá valor Olá **id** atributo de saudação **entrada** elemento não deve ser maior que 64 caracteres.
* Olá valor Olá **nome** atributo de saudação **entrada** elemento não deve ser maior que 64 caracteres.
* Olá conteúdo de saudação **descrição** elemento não deve ter mais de 128 caracteres
* Olá valor Olá **tipo** atributo de saudação **entrada** elemento deve ser *Zip* ou *DataTable*.
* Olá valor Olá **é opcional** atributo de saudação **entrada** elemento não é necessário (e é *false* por padrão quando não especificado); mas se for especificado, ele deve ser *true* ou *false*.

### <a name="output-elements"></a>Elementos de saída
**Portas de saída padrão:** portas de saída são mapeadas toohello valores de retorno de sua função de R, que pode ser usado por módulos subsequentes. *DataTable* é o tipo de porta de saída padrão somente Olá com suporte no momento. (O suporte para *Aprendizes* e *Transformações* estará disponível em breve.) Uma saída *DataTable* é definida como:

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

Para saídas em módulos R personalizados, Olá valor Olá **id** atributo não tem toocorrespond com qualquer coisa no script hello R, mas ele deve ser exclusivo. Para uma saída de módulo único, o valor de retorno de saudação do função hello R deve ser um *data.frame*. Em ordem toooutput mais de um objeto de um tipo de dados com suporte, portas de saída apropriada Olá necessário toobe especificado no arquivo de definição XML de saudação e objetos Olá necessário toobe retornado como uma lista. Olá saída objetos são atribuídos a portas toooutput em tooright esquerda, refletindo ordem Olá no qual os objetos de saudação são colocados no Olá retornada lista.

Por exemplo, se você quiser toomodify Olá **personalizado adicionar linhas** toooutput módulo Olá originais dois conjuntos de dados, *dataset1* e *dataset2*, além disso toohello novo unida conjunto de dados, *conjunto de dados*, (em ordem, da esquerda tooright, como: *dataset*, *dataset1*, *dataset2*), em seguida, defina Olá portas no arquivo de CustomAddRows.xml Olá de saída da seguinte maneira:

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


E retornar a lista de saudação de objetos em uma lista na ordem correta, Olá em 'CustomAddRows.R':

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

**Saída de visualização:** você também pode especificar uma porta de saída do tipo *visualização*, que exibe a saída de saudação da saída de console e dispositivo gráfico Olá R. Esta porta não é parte da saída da função de saudação R e não interfere em ordem de saudação do hello outros tipos de porta de saída. tooadd uma visualização porta toohello módulos personalizados, adicione um **saída** elemento com um valor de *visualização* para seus **tipo** atributo:

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

**Regras de saída:**

* Olá valor Olá **id** atributo de saudação **saída** elemento deve ser um nome de variável de R válido.
* Olá valor Olá **id** atributo de saudação **saída** elemento não deve ter mais de 32 caracteres.
* Olá valor Olá **nome** atributo de saudação **saída** elemento não deve ser maior que 64 caracteres.
* Olá valor Olá **tipo** atributo de saudação **saída** elemento deve ser *visualização*.

### <a name="arguments"></a>Argumentos
Dados adicionais podem ser passados toohello R função por meio de parâmetros do módulo que são definidos no hello **argumentos** elemento. Esses parâmetros aparecem no painel de propriedades mais à direita de saudação de saudação da interface do usuário de aprendizado de máquina quando o módulo de saudação é selecionado. Os argumentos podem ser qualquer um dos tipos de saudação com suporte ou você pode criar uma enumeração personalizada quando necessário. Semelhante toohello **portas** elementos, **argumentos** elementos podem ter um recurso opcional **descrição** elemento que especifica o texto de saudação que aparece quando você passa o mouse Olá em nome do parâmetro hello.
Propriedades opcionais para um módulo, como o valor padrão, minValue e maxValue podem ser adicionadas como argumento tooany como atributos tooa **propriedades** elemento. Propriedades válidas para Olá **propriedades** elemento dependem do tipo de argumento hello e são descritos com tipos de argumento Olá tem suporte na próxima seção, Olá. Argumentos com hello **é opcional** propriedade definida muito**"true"** não exigem Olá usuário tooenter um valor. Se um valor não for fornecido para o argumento toohello, argumento Olá não for passado a função de ponto de entrada toohello. Argumentos da função de ponto de entrada hello necessidade opcional toobe explicitamente manipulado pela função hello, por exemplo, atribuído um valor padrão de NULL na definição de função de ponto de entrada hello. Um argumento opcional só serão impostas Olá outras restrições de argumento, ou seja, min ou max, se um valor é fornecido pelo usuário hello.
Como com as entradas e saídas, é fundamental que cada um dos parâmetros de saudação tenha valores de id exclusivo associados a eles. No início rápido do nosso exemplo hello associados/parâmetro de id foi *permuta*.

### <a name="arg-element"></a>Elemento arg
Um parâmetro de módulo é definido usando Olá **Arg** elemento filho do hello **argumentos** seção do arquivo de definição XML de saudação. Assim como acontece com os elementos filho de saudação em Olá **portas** seção, Olá a ordem dos parâmetros no hello **argumentos** seção define o layout de saudação em Olá UX. Olá parâmetros aparecem de cima para baixo na saudação da interface do usuário em Olá mesma ordem em que elas são definidas no arquivo XML de saudação. suporte para o aprendizado de máquina para parâmetros de tipos de saudação são listados aqui. 

**int** – um parâmetro de tipo de número inteiro (32 bits).

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* *Propriedades opcionais*: **mín.**, **máx.**, **padrão** e **isOptional**

**double** – um parâmetro de tipo duplo.

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* *Propriedades opcionais*: **mín.**, **máx.**, **padrão** e **isOptional**

**bool** – um parâmetro booliano que é representado por uma caixa de seleção no UX.

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* *Propriedades opcionais*: **padrão** -falso se não definido

**string**: uma cadeia de caracteres padrão

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* *Propriedades opcionais*: **padrão** e **isOptional**

**ColumnPickerFor**: um parâmetro de seleção de coluna. Esse tipo é renderizado no hello UX como um seletor de coluna. Olá **propriedade** elemento é usado toospecify aqui Olá id da porta de saudação do que colunas forem selecionadas, onde o tipo de porta de destino Olá deve ser *DataTable*. resultado de saudação da seleção de coluna Olá é passado toohello R função como uma lista de cadeias de caracteres que contém os nomes de coluna Olá selecionado. 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* *Propriedades necessárias*: **portId** -correspondências Olá id de um elemento de entrada com tipo *DataTable*.
* *Propriedades opcionais*:
  
  * **allowedTypes** -tipos de coluna de saudação de filtros do qual você pode escolher. Os valores válidos incluem: 
    
    * Numérico
    * Booliano
    * Categóricos
    * string
    * Rótulo
    * Recurso
    * Pontuação
    * Todos
  * **padrão** -seleções padrão válido para o seletor de coluna Olá incluem: 
    
    * Nenhum
    * NumericFeature
    * NumericLabel
    * NumericScore
    * NumericAll
    * BooleanFeature
    * BooleanLabel
    * BooleanScore
    * BooleanAll
    * CategoricalFeature
    * CategoricalLabel
    * CategoricalScore
    * CategoricalAll
    * StringFeature
    * StringLabel
    * StringScore
    * StringAll
    * AllLabel
    * AllFeature
    * AllScore
    * Todos

**Suspensa**: uma lista (suspensa) enumerada especifica pelo usuário. itens de lista suspensa de saudação são especificadas no hello **propriedades** elemento usando um **Item** elemento. Olá **id** para cada **Item** deve ser exclusivo e uma variável de R válida. Olá valor Olá **nome** de um **Item** serve como o texto de saudação que você vê e o valor de saudação que é passado a função toohello R.

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* *Propriedades opcionais*:
  * **padrão** - Olá valor de propriedade padrão de saudação deve corresponder com um valor de id de uma saudação **Item** elementos.

### <a name="auxiliary-files"></a>Arquivos auxiliares
Qualquer arquivo que é colocado no arquivo ZIP módulo personalizado é contínuo toobe disponível para uso durante o tempo de execução. Qualquer estrutura de diretório presente é preservada. Isso significa que funciona de fornecimento de arquivo hello mesmo localmente e na execução de aprendizado de máquina do Azure. 

> [!NOTE]
> Observe que todos os arquivos são extraídos too'src' directory para que todos os caminhos devem ter ' src /' prefixo.
> 
> 

Por exemplo, digamos que você deseja tooremove nas todas as linhas do conjunto de dados hello e também remove linhas duplicadas, antes de gerá-lo em CustomAddRows, e você já escreveu uma função do R que faz isso em um arquivo RemoveDupNARows.R:

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
Pode extrair o arquivo auxiliar Olá RemoveDupNARows.R em Olá CustomAddRows função:

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

Em seguida, carregue um arquivo zip contendo “CustomAddRows.R”, “CustomAddRows.xml” e “RemoveDupNARows.R” como um módulo R personalizado.

## <a name="execution-environment"></a>Ambiente de execução
ambiente de execução Olá para script hello R usa Olá a mesma versão do R Olá **Executar Script R** módulo e pode usar Olá mesmo padrão de pacotes. Você também pode adicionar adicionais R pacotes tooyour módulo personalizado, incluindo-os no pacote de zip do módulo personalizado de saudação. Basta carregá-los no seu script R como faria em seu próprio ambiente R. 

**Limitações do ambiente de execução Olá** incluem:

* Sistema de arquivos não persistente: arquivos gravados quando o módulo personalizado de saudação é executado não são persistidos em várias execuções do hello mesmo módulo.
* Sem acesso à rede

