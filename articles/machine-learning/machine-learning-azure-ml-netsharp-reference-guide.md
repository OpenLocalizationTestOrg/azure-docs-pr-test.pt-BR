---
title: "aaaGuide toohello linguagem Net # Neural redes especificação | Microsoft Docs"
description: "Sintaxe de saudação Net # neural redes linguagem de especificação, junto com exemplos de como toocreate uma rede neural personalizada de modelo no Microsoft Azure ML usando Net #"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 3493247ecc39ca3a1382510ad520d7017159ff62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a>Guia de linguagem de especificação de rede neural tooNet # para aprendizado de máquina do Azure
## <a name="overview"></a>Visão geral
NET # é uma linguagem desenvolvida pela Microsoft é usada toodefine arquiteturas de rede neural. Você pode usar Net# em módulos de rede neural no Microsoft Azure Machine Learning.

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

Neste artigo, você aprenderá os conceitos básicos necessários toodevelop uma rede neural personalizada: 

* Requisitos de rede neural e como toodefine Olá principais componentes
* sintaxe de saudação e palavras-chave da saudação linguagem de especificação de Net #
* Exemplos de redes neurais personalizadas criadas usando Net# 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a>Conceitos básicos de rede neural
Consiste em uma estrutura de rede neural ***nós*** que são organizados em ***camadas***e ponderada ***conexões*** (ou ***bordas***) entre nós de saudação. conexões de saudação são direcionais, e cada conexão tem uma ***fonte*** nó e um ***destino*** nó.  

Cada ***camada treinável*** (uma camada oculta ou de saída) tem um ou mais ***pacotes de conexão***. Um pacote de conexão consiste em uma camada de origem e uma especificação de conexões de saudação de camada fonte. Todas as conexões de saudação em um compartilhamento de pacote determinado Olá mesmo ***camada fonte*** e Olá mesmo ***camada destino***. Net #, um pacote de conexão é considerado como camada de destino do conjunto de toohello que pertencem.  

NET # dá suporte a vários tipos de pacotes de conexão, que permite que você personalize a forma Olá entradas são mapeadas toohidden camadas e saídas de toohello mapeada.   

padrão de saudação ou pacote padrão é um **pacote completo**, no qual cada nó Olá camada de origem é o nó de tooevery conectados na camada de destino hello.  

Além disso, Net # suporta Olá quatro tipos de pacotes avançados de conexão a seguir:  

* **Grupos filtrados**. usuário Olá pode definir um predicado usando Olá locais de nó da camada fonte hello e Olá nó da camada de destino. Nós são conectados sempre predicado Olá é True.
* **Grupos convolucionais**. usuário Olá pode definir vizinhanças pequenas de nós na camada de origem hello. Cada nó na camada de destino Olá é conectado tooone ambiente de nós na camada de origem hello.
* **Grupos de pooling** e **Grupos de normalização de resposta**. Estes são os pacotes de tooconvolutional semelhante que Olá usuário define vizinhanças pequenas de nós na camada de origem hello. diferença de saudação é pesos de saudação de bordas de saudação nesses pacotes não são trainable. Em vez disso, uma função predefinida é aplicada o nó de origem toohello valores valor do nó de destino toodetermine hello.  

Usando Net # toodefine Olá estrutura de uma rede neural torna possível toodefine estruturas complexas, como redes neurais profundas ou convoluções das dimensões arbitrárias, que são conhecidas tooimprove aprendizado nos dados, como imagens, áudio ou vídeo.  

## <a name="supported-customizations"></a>Personalizações com suporte
arquitetura de saudação de modelos de rede neural que você criar no aprendizado de máquina do Azure pode ser extensivamente personalizada usando Net #. Você pode:  

* Crie camadas ocultas e número de saudação do controle de nós em cada camada.
* Especifique como as camadas devem toobe conectado tooeach outros.
* Definir estruturas de conectividade especial, como convoluções e grupos de compartilhamento de peso.
* Especifique diferentes funções de ativação.  

Para obter detalhes sobre a sintaxe de linguagem de especificação de hello, consulte [especificação de estrutura](#Structure-specifications).  

Para obter exemplos de definição de redes neurais alguns comuns do aprendizado de máquina tarefas do toocomplex simples, consulte [exemplos](#Examples-of-Net#-usage).  

## <a name="general-requirements"></a>Requisitos gerais
* É preciso que haja exatamente uma camada de saída, pelo menos uma camada de entrada e nenhuma ou mais camadas ocultas. 
* Cada camada tem um número fixo de nós, arranjados conceitualmente em uma matriz retangular de dimensões arbitrárias. 
* Camadas de entrada não tem associados treinados parâmetros e representam Olá ponto onde os dados de instância entram rede Olá. 
* Trainable camadas (Olá camadas ocultas e saídas) associou treinados parâmetros, conhecidos como pesos e tendências. 
* nós de origem e destino Olá devem estar em camadas separadas. 
* As conexões devem ser acíclicas; em outras palavras, não pode ser uma cadeia de conexões à esquerda toohello back nó de origem inicial.
* Olá camada de saída não pode ser uma camada de origem de um pacote de conexão.  

## <a name="structure-specifications"></a>Especificações de estrutura
Uma especificação de estrutura de rede neural é composta por três seções: Olá **declaração de constante**, Olá **camada declaração**, Olá **declaração de conexão**. Há também uma seção **declaração de compartilhamento** opcional. seções de saudação podem ser especificadas em qualquer ordem.  

## <a name="constant-declaration"></a>Declaração de constante
Uma declaração de constante é opcional. Ele fornece um meio toodefine valores usados em outro lugar na definição de rede neural hello. declaração Olá consiste em um identificador seguido por um sinal de igual e uma expressão de valor.   

Por exemplo, Olá instrução a seguir define uma constante **x**:  

    Const X = 28;  

toodefine duas ou mais constantes simultaneamente, coloque valores e nomes de identificador de saudação entre chaves e separe-as usando ponto e vírgula. Por exemplo:  

    Const { X = 28; Y = 4; }  

lado direito de saudação de cada expressão de atribuição pode ser um número inteiro, um número real, um valor booliano (verdadeiro ou falso) ou uma expressão matemática. Por exemplo:  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a>Declaração de camada
declaração de camada de saudação é necessária. Ele define o tamanho de saudação e origem da camada de hello, incluindo seus pacotes de conexão e atributos. Olá inicia de instrução de declaração com nome de saudação da camada de saudação (de entrada, oculto ou de saída), seguido por dimensões de saudação da camada de saudação (uma tupla de números inteiros positivos). Por exemplo:  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* produto Olá das dimensões de saudação é o número de saudação de nós na camada de saudação. Neste exemplo, há duas dimensões [5,20], que significa que há 100 nós na camada de saudação.
* camadas de saudação podem ser declaradas em qualquer ordem, com uma exceção: se mais de uma camada de entrada é definida, ordem de saudação na qual eles são declarados deve coincidir com a ordem de saudação de recursos nos dados de entrada hello.  

toospecify Olá o número de nós em uma camada de ser determinado automaticamente, use Olá **automática** palavra-chave. Olá **automática** palavra-chave tem efeitos diferentes, dependendo da camada de saudação:  

* Em uma declaração de camada de entrada, o número de saudação de nós é número Olá de recursos nos dados de entrada hello.
* Em uma declaração de camada oculta, o número de Olá de nós é número Olá especificado pelo valor de parâmetro de saudação do **número de nós ocultos**. 
* Em uma declaração de camada de saída, o número de saudação de nós é 2 para classificação de duas classes, 1 de regressão e toohello igual número de nós de saída de classificação multiclasse.   

Por exemplo, hello seguinte definição de rede permite Olá tamanho de todos os toobe camadas determinado automaticamente:  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


Uma declaração de camada para uma camada trainable (Olá camadas ocultas ou saídas) opcionalmente pode incluir a função de saída de hello (também chamada de uma função de ativação), cujo padrão é muito**sigmoide** para modelos de classificação e **linear** para modelos de regressão. (Mesmo se você usar o padrão de saudação, você pode declarar explicitamente função de ativação de hello, se desejado para fins de esclarecimento.)

Olá funções saída a seguir têm suporte:  

* sigmoid
* linear
* softmax
* rlinear
* square
* sqrt
* srlinear
* abs
* tanh 
* brlinear  

Por exemplo, a saudação declaração a seguir usa Olá **softmax** função:  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a>Declaração de conexão
Imediatamente depois de definir a camada trainable hello, você deve declarar conexões entre camadas Olá que você definiu. declaração de pacote de conexão Olá começa com a palavra-chave de saudação **de**, seguido pelo nome de saudação do tipo de camada e hello de origem do pacote de saudação de toocreate do pacote de conexão.   

Atualmente, há suporte para cinco tipos de grupos de conexão:  

* **Completo** pacotes, indicados pela palavra-chave de saudação **todos**
* **Filtrado** pacotes, indicados pela palavra-chave de saudação **onde**, seguido por uma expressão de predicado
* **Convolutional** pacotes, indicados pela palavra-chave de saudação **convolve**, seguido por atributos de convolução Olá
* **Pool** pacotes, indicados por palavras-chave de saudação **max pool** ou **significa pool**
* **Normalização de resposta** pacotes, indicados pela palavra-chave de saudação **norma de resposta**      

## <a name="full-bundles"></a>Grupos completos
Um pacote de conexão completa inclui uma conexão de cada nó no nó da saudação fonte camada tooeach na camada de destino hello. Esse é o tipo de conexão de rede de padrão de saudação.  

## <a name="filtered-bundles"></a>Grupos filtrados
Uma especificação grupo de conexões filtrado inclui um predicado, expresso sintaticamente de modo muito similar a uma expressão lambda em C#. Olá, exemplo a seguir define dois pacotes filtrados:  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* No predicado Olá para *ByRow*, **s** é um parâmetro que representa um índice em uma matriz retangular de saudação de nós da camada de entrada hello, *Pixels*, e **d**  é um parâmetro que representa um índice em uma matriz de saudação de nós da camada oculta do hello, *ByRow*. Olá tipo dos dois **s** e **d** é uma tupla de comprimento dois inteiros. Conceitualmente, **s** abrange todos os pares de números inteiros com *0 <= s[0] < 10* e *0 <= s[1] < 20*, e **d** abrange todos os pares de números inteiros com *0 <= d[0] < 10* e *0 <= d[1] < 12*. 
* No lado direito de saudação da expressão de predicado hello, há uma condição. Neste exemplo, para cada valor de **s** e **d** , de modo que a condição Olá for True, há uma borda do nó de camada Olá origem camada nó toohello destino. Assim, essa expressão de filtro indica que esse pacote de saudação inclui uma conexão do nó Olá definido pelo **s** toohello nó definido por **d** em todos os casos em que [0] é igual tood [0].  

Opcionalmente, você pode especificar um conjunto de pesos para um grupo filtrado. Olá valor Olá **pesos** atributo deve ser uma tupla de valores com um comprimento que corresponda a saudação número de conexões definidas pelo pacote de saudação de ponto flutuante. Por padrão, os pesos são gerados de modo aleatório.  

Valores de peso são agrupados por índice Olá de nó de destino. Ou seja, se estiver conectado primeiro nó de destino Olá levou nós de origem, Olá primeiro *K* elementos de saudação **pesos** tupla são pesos Olá para o primeiro nó de destino hello, em ordem de índice de origem. Olá que mesmo se aplica a saudação nós de destino restantes.  

É possível toospecify pesos diretamente como valores de constante. Por exemplo, se você aprendeu pesos Olá anteriormente, você pode especificá-los como constantes usando esta sintaxe:

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a>Grupos convolucionais
Quando os dados de treinamento Olá tem uma estrutura homogênea, convolutional conexões são usadas toolearn recursos de alto nível dos dados de saudação. Por exemplo, para dados de imagem, áudio ou vídeo, a dimensionalidade espacial ou temporal pode ser bastante uniforme.  

Pacotes convolutional empregam retangular **kernels** que são deslize para dimensões de saudação. Essencialmente, cada núcleo define um conjunto de pesos aplicado no locais vizinhanças, chamado tooas **aplicativos kernel**. Cada aplicativo de kernel corresponde tooa nó na camada de origem hello, que é referida tooas hello **nó central**. os pesos de saudação do kernel são compartilhados entre várias conexões. Em um pacote convolutional, cada núcleo é retangular e todos os aplicativos de kernel estão Olá mesmo tamanho.  

Saudação de suporte de pacotes convolutional seguintes atributos:

**InputShape** define dimensionalidade Olá da camada de origem Olá para fins de saudação deste pacote convolutional. valor de saudação deve ser uma tupla de números inteiros positivos. produto Olá de inteiros Olá deve ser igual Olá número de nós na camada de origem hello, mas caso contrário, ele não precisa dimensionalidade de saudação toomatch declarada para a camada de fonte de saudação. comprimento de saudação dessa tupla se torna Olá **arity** valor para o pacote convolutional hello. (Normalmente arity refere-se toohello o número de argumentos ou operandos que pode levar a uma função.)  

forma de saudação toodefine e locais de kernels hello, use atributos Olá **KernelShape**, **Stride**, **preenchimento**, **LowerPad**, e **UpperPad**:   

* **KernelShape**: dimensionalidade de saudação define (obrigatório) de cada núcleo para pacote convolutional hello. valor de saudação deve ser uma tupla de inteiros positivos com um comprimento igual a saudação arity do pacote de saudação. Cada componente dessa tupla deve ter mais do que o componente correspondente de saudação do **InputShape**. 
* **STRIDE**: (opcional) Olá define deslizante tamanhos de etapa de convolução hello (tamanho de uma etapa para cada dimensão), Olá distância entre os nós de saudação central. valor de saudação deve ser uma tupla de inteiros positivos com um comprimento Olá arity do pacote de saudação. Cada componente dessa tupla deve ter mais do que o componente correspondente de saudação do **KernelShape**. valor padrão de saudação é uma tupla com todos os componentes e igual tooone. 
* **Compartilhamento**: peso de hello (opcional) define o compartilhamento para cada dimensão de convolução hello. valor de saudação pode ser um único valor booliano ou uma tupla de valores booleanos com um comprimento Olá arity do pacote de saudação. Um único valor booliano é estendido toobe uma tupla de tamanho correto de saudação com todos os componentes do valor especificado de toohello igual. valor padrão de saudação é uma tupla que consiste em todos os valores True. 
* **MapCount**: (opcional) define Olá número de recurso mapeia para o pacote convolutional hello. valor de saudação pode ser um inteiro positivo único ou uma tupla de inteiros positivos com um comprimento Olá arity do pacote de saudação. Um único valor inteiro é estendido toobe uma tupla de comprimento correto Olá Olá primeiro componentes igual toohello especificado valor e todos os Olá tooone igual de componentes restantes. valor padrão de saudação é um. número total de saudação de mapas de recurso é produto Olá dos componentes de saudação do hello tupla. Olá fatorar desse número total em componentes de saudação determina como os valores de mapa de recursos de saudação são agrupados em nós de destino hello. 
* **Pesos**: (opcional) define saudação inicial os pesos para o pacote de saudação. valor de saudação deve ser uma tupla de valores com um comprimento que é o número de saudação de kernels vezes Olá número de pesos por núcleo, conforme definido neste artigo de ponto flutuante. níveis de importância saudação padrão são gerados aleatoriamente.  

Há dois conjuntos de propriedades que controlam o preenchimento propriedades Olá sendo mutuamente exclusivos:

* **Preenchimento**: (opcional) determina se Olá de entrada deve ser preenchida usando um **esquema padrão do preenchimento**. valor de saudação pode ser um único valor booliano, ou pode ser uma tupla de valores booleanos com um comprimento Olá arity do pacote de saudação. Um único valor booliano é estendido toobe uma tupla de tamanho correto de saudação com todos os componentes do valor especificado de toohello igual. Se o valor de saudação para uma dimensão for True, origem Olá logicamente é preenchida nessa dimensão com aplicativos de kernel adicionais de toosupport células com valor zero, de modo que nós de central de saudação de kernels de primeiro e últimos Olá nessa dimensão são nós de primeiro e últimos Olá nessa dimensão na camada de origem hello. Assim, o número de saudação de nós "fictícios" em cada dimensão é determinado automaticamente, toofit exatamente *(InputShape d - 1) / Stride [d] + 1* kernels na camada de origem Olá preenchida. Se o valor Olá para uma dimensão for False, Olá kernels são definidos para que seja de número de saudação de nós em cada lado que ficam fora Olá mesmo (backup tooa diferença de 1). Olá valor padrão desse atributo é uma tupla com todos os componentes e igual tooFalse.
* **UpperPad** e **LowerPad**: (opcional) fornecer maior controle sobre o valor de saudação do preenchimento toouse. **Importante:** esses atributos podem ser definidos se e somente se hello **preenchimento** é de propriedade acima ***não*** definido. valores de Olá devem ser números inteiros tuplas com comprimentos de arity saudação do pacote de saudação. Quando esses atributos são especificados, nós "fictícios" são adicionados toohello inferior e superiores extremidades de cada dimensão da saudação camada de entrada. número de nós Hello adicionado toohello inferior e superior termina em cada dimensão é determinada pelo **LowerPad**[i] e **UpperPad**[i] respectivamente. tooensure que kernels correspondem nós somente muito "reais" e não muito "" fictício, hello condições a seguir deve ser atendido:
  * Cada componente de **LowerPad** precisa ser estritamente menor que KernelShape[d]/2. 
  * Cada componente de **UpperPad** não pode ser maior que KernelShape[d]/2. 
  * valor padrão de saudação desses atributos é uma tupla com todos os componentes e igual too0. 

configuração de saudação **preenchimento** = true permite conforme a quantidade de preenchimento é necessário tookeep hello "Centro" do kernel hello dentro hello "real" de entrada. Isso altera matemática Olá um pouco para calcular o tamanho da saída de hello. Em geral, o tamanho de saída Olá *D* é calculada como *D = (I - K) / S + 1*, onde *,* é o tamanho de entrada hello, *K* é o tamanho de kernel hello, *S* é stride Olá, e  */*  é uma divisão de inteiro (round em direção a zero). Se você definir UpperPad = [1, 1], tamanho de entrada hello *,* é efetivamente 29 e, portanto, *D = (29-5) / 2 + 1 = 13*. No entanto, quando **Padding** = true, essencialmente *I* e aumentado por *K - 1*; com isso, *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*. Especificando valores para **UpperPad** e **LowerPad** obter muito mais controle sobre Olá preenchimento que se você configurou **preenchimento** = true.

Para mais informações sobre redes convolucionais e seus aplicativos, consulte esses artigos:  

* [http://deeplearning.net/tutorial/lenet.html](http://deeplearning.net/tutorial/lenet.html)
* [http://research.microsoft.com/pubs/68920/icdar03.pdf](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a>Grupos de pooling
Um **pooling pacote** aplica-se a conectividade de tooconvolutional semelhante geometry, mas usa funções predefinidas toosource nó valores tooderive Olá nó valor de destino. Assim, os grupos de pooling não têm estado treinável (pesos ou vieses). Suporte de pacotes para todas as Olá convolutional atributos, exceto pool **compartilhamento**, **MapCount**, e **pesos**.  

Normalmente, kernels Olá resumidos por unidades adjacentes de pool não se sobrepõem. Se Stride [d] é igual tooKernelShape [d] em cada dimensão, camada Olá obtida é Olá local pooling camada tradicional, que geralmente é utilizada no convolutional redes neurais. Cada nó de destino calcula Olá máximo ou média de saudação de atividades de saudação do seu kernel na camada de origem hello.  

saudação de exemplo a seguir ilustra um pacote do pool: 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* Olá arity do pacote de saudação é 3 (Olá comprimento de tuplas Olá **InputShape**, **KernelShape**, e **Stride**). 
* Olá número de nós na camada de origem Olá é *5 * 24 * 24 = 2880*. 
* Essa é uma camada de pooling local tradicional porque **KernelShape** e **Stride** são iguais. 
* Olá número de nós na camada de destino Olá é *5 * 12 * 12 = 1440*.  

Para mais informações sobre camadas de pooling, consulte esses artigos:  

* [http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Seção 3.4)
* [http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a>Grupos de normalização de resposta
**Normalização de resposta** é um esquema de normalização local que foi introduzido por Geoffrey Hinton, et al, documento hello [ImageNet Classiﬁcation com Convolutional as redes neurais profundas](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf). Normalização de resposta é generalização tooaid usado em redes neurais. Quando um neurônio está acionando em um nível muito alto de ativação, uma camada de normalização de resposta local suprime o nível de ativação de saudação de Olá ao redor de neurônios. Isso é feito usando três parâmetros (***α***, ***β*** e ***k***) e uma estrutura convolucional (ou forma de zona próxima). Cada neurônio na camada de destino Olá ***y*** corresponde neurônio tooa ***x*** na camada de origem hello. Olá nível de ativação de ***y*** é determinado pelo Olá seguinte fórmula, onde ***f*** é o nível de ativação de saudação de um neurônio e ***Nx*** é kernel hello (ou conjunto de saudação que contém Olá neurônios no ambiente de saudação do ***x***), conforme definido pelo Olá convolutional estrutura a seguir:  

![][1]  

Pacotes de normalização de resposta oferecer suporte a todos os atributos de convolutional Olá exceto **compartilhamento**, **MapCount**, e **pesos**.  

* Se o kernel Olá contém neurônios na Olá mesmo mapear como ***x***, esquema de normalização de saudação é chamado tooas **mesmo mapear normalização**. toodefine mesmo mapear normalização, coordenada primeiro Olá **InputShape** deve ter valor Olá 1.
* Se kernel Olá contém neurônios na Olá mesma posição espacial ***x***, mas neurônios Olá estão em outros mapas, Olá normalização esquema é chamado de **em mapas normalização**. Esse tipo de normalização de resposta implementa uma forma de inhibition lateral inspirada Olá tipo encontrado no neurônios reais, criando a competição por níveis de ativação grande entre saídas neurônio computadas em mapas diferentes. toodefine em mapas de normalização, coordenada primeiro Olá deve ser um inteiro maior que um e não maior que o número de saudação de mapas e restante Olá Olá coordenadas deve ter o valor de saudação 1.  

Como pacotes de normalização de resposta se aplicam a um função predefinida toosource nó valores toodetermine Olá nó valor de destino, eles têm sem estado trainable (pesos ou propensões).   

**Alerta**: nós Olá na camada de destino Olá correspondem tooneurons que são nós de saudação central de kernels hello. Por exemplo, se KernelShape [d] for ímpar, em seguida, *KernelShape [d] / 2* corresponde o nó de kernel central toohello. Se *KernelShape [d]* for par, nó central hello está no *KernelShape [d] / 2-1*. Portanto, se **preenchimento**[d] é False, Olá primeiro e último Olá *KernelShape [d] / 2* nós não possuem os nós correspondentes na camada de destino hello. tooavoid nessa situação, defina **preenchimento** como [true, true,..., true].  

Além disso toohello quatro atributos descritos anteriormente, pacotes de normalização de resposta também suporte Olá seguintes atributos:  

* **Alpha**: (obrigatório) especifica um valor de ponto flutuante que corresponde muito***α*** na fórmula anterior hello. 
* **Beta**: (obrigatório) especifica um valor de ponto flutuante que corresponde muito***β*** na fórmula anterior hello. 
* **Deslocamento**: (opcional) especifica um valor de ponto flutuante que corresponde muito***k*** na fórmula anterior hello. O padrão é too1.  

Olá, exemplo a seguir define um conjunto de normalização de resposta usando estes atributos:  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* camada de origem Olá inclui cinco mapas, cada um com a dimensão aof de 12 x 12, totalizando em nós de 1440. 
* Olá valor **KernelShape** indica que se trata de uma mesma camada de normalização de mapa, onde o ambiente de saudação é um retângulo de 3x3. 
* Olá valor padrão de **preenchimento** é False, assim, camada de destino Olá tem somente 10 nós em cada dimensão. tooinclude um nó na camada de destino Olá correspondente tooevery nó na camada de origem hello, adicionar preenchimento = [true, true, true]; e alterar o tamanho de saudação do RN1 muito [5, 12, 12].  

## <a name="share-declaration"></a>Declaração de compartilhamento
Net# dá suporte, opcionalmente, a definição de múltiplos grupos com pesos compartilhados. os pesos de saudação de quaisquer dois pacotes podem ser compartilhados se suas estruturas são Olá mesmo. Olá sintaxe a seguir define os pacotes com pesos compartilhados:  

    share-declaration:
        share    {    layer-list    }
        share    {    bundle-list    }
       share    {    bias-list    }

    layer-list:
        layer-name    ,    layer-name
        layer-list    ,    layer-name

    bundle-list:
       bundle-spec    ,    bundle-spec
        bundle-list    ,    bundle-spec

    bundle-spec:
       layer-name    =>     layer-name

    bias-list:
        bias-spec    ,    bias-spec
        bias-list    ,    bias-spec

    bias-spec:
        1    =>    layer-name

    layer-name:
        identifier  

Por exemplo, hello compartilhamento-declaração a seguir especifica os nomes de camada hello, indicando que os pesos e tendências devem ser compartilhadas:  

    Const {
      InputSize = 37;
      HiddenSize = 50;
    }
    input {
      Data1 [InputSize];
      Data2 [InputSize];
    }
    hidden {
      H1 [HiddenSize] from Data1 all;
      H2 [HiddenSize] from Data2 all;
    }
    output Result [2] {
      from H1 all;
      from H2 all;
    }
    share { H1, H2 } // share both weights and biases  

* recursos de entrada Hello são particionados em duas camadas de entrada tamanhos iguais. 
* camadas de saudação ocultada de computação, em seguida, recursos de nível superior em duas camadas de entrada hello. 
* declaração de compartilhamento Olá Especifica que *H1* e *H2* devem ser computadas em Olá mesmo modo de seus respectivos entradas.  

Alternativamente, isso pode ser especificado com duas declarações de compartilhamento separadas, como descrito a seguir:  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

Você pode usar a forma abreviada Olá somente quando as camadas de saudação contêm um único pacote. Em geral, compartilhamento é possível somente quando a estrutura relevante Olá é idêntica, o que significa que eles têm Olá mesmo tamanho, mesmo geometria convolutional e assim por diante.  

## <a name="examples-of-net-usage"></a>Exemplos de uso do Net#
Esta seção fornece alguns exemplos de como você pode usar Net # tooadd oculto camadas, definir forma de saudação que camadas ocultas interagem com outras camadas e criar redes convolutional.   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a>Defina uma rede neural personalizada simples: exemplo "Olá mundo"
Esse exemplo simples demonstra como toocreate um neural rede modelo que tem uma única camada oculta.  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

exemplo Hello ilustra alguns comandos básicos da seguinte maneira:  

* primeira linha Hello define camada de entrada hello (denominado *dados*). Quando você usa Olá **automática** palavra-chave, rede neural Olá inclui automaticamente todas as colunas de recurso nos exemplos de entrada hello. 
* Olá segunda linha cria a camada oculta hello. nome da saudação *H* é atribuído a camada oculta toohello, que tem 200 nós. Essa camada é a camada de entrada toohello totalmente conectados.
* terceira linha de saudação define a camada de saída da saudação (denominado *O*), que contém 10 nós de saída. Se a rede neural Olá é usado para classificação, há um nó de saída por classe. Olá palavra-chave **sigmoide** indica Olá saída função é aplicada toohello camada de saída.   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a>Definir várias camadas ocultas: exemplo de visão do computador
Olá exemplo a seguir demonstra como toodefine uma rede neural um pouco mais complexa, com várias camadas ocultas personalizadas.  

    // Define hello input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define hello first two hidden layers, using data only from hello Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define hello third hidden layer, which uses as source hello hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define hello output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

Este exemplo ilustra vários recursos de linguagem de especificação de redes neurais hello:  

* estrutura Olá tem duas camadas de entrada, *Pixels* e *metadados*.
* Olá *Pixels* camada é uma camada de origem para dois pacotes de conexão, com camadas de destino, *ByRow* e *ByCol*.
* Olá camadas *coletar* e *resultados* são camadas de destino em vários pacotes de conexão.
* camada de saída de Hello, *resultados*, é uma camada de destino em dois pacotes de conexão, uma com hello de segundo nível oculta (coleta) como uma camada de destino e Olá outra camada de entrada hello (metadados) como uma camada de destino.
* Olá camadas ocultas, *ByRow* e *ByCol*, especifique conectividade filtrada usando expressões de predicado. Mais precisamente, Olá nó *ByRow* em [x, y] é nós conectados toohello *Pixels* com x de coordenada, primeiro Olá primeiro índice toohello igual coordenada do nó. Da mesma forma, Olá nó *ByCol em [x, y] é nós conectados toohello _Pixels* que têm coordenadas de índice segundo hello dentro de uma coordenada de segundo do nó hello, y.  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a>Definir uma rede convolucional para classificação multiclasse: exemplo de reconhecimento de dígitos
definição Olá Olá rede a seguir é projetado toorecognize números, e ele ilustra algumas técnicas avançadas para personalizar uma rede neural.  

    input Image [29, 29];
    hidden Conv1 [5, 13, 13] from Image convolve 
    {
       InputShape  = [29, 29];
       KernelShape = [ 5,  5];
       Stride      = [ 2,  2];
       MapCount    = 5;
    }
    hidden Conv2 [50, 5, 5]
    from Conv1 convolve 
    {
       InputShape  = [ 5, 13, 13];
       KernelShape = [ 1,  5,  5];
       Stride      = [ 1,  2,  2];
       Sharing     = [false, true, true];
       MapCount    = 10;
    }
    hidden Hid3 [100] from Conv2 all;
    output Digit [10] from Hid3 all;  


* estrutura Olá tem uma única camada de entrada, *imagem*.
* Olá palavra-chave **convolve** indica que as camadas de saudação nomeados *Conv1* e *Conv2* convolutional camadas. Cada essas declarações de camada é seguida por uma lista de atributos de convolução hello.
* Olá net tem uma terceira oculto camada, *Hid3*, que é totalmente conectada toohello segunda camada oculta, *Conv2*.
* camada de saída de Hello, *dígitos*, é conectada toohello somente terceira camada oculta, *Hid3*. Olá palavra-chave **todos os** indica essa camada de saída Olá é totalmente conectada muito*Hid3*.
* Olá arity de convolução Olá é três (Olá comprimento de tuplas Olá **InputShape**, **KernelShape**, **Stride**, e **compartilhamento**). 
* número de saudação de pesos por núcleo é *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26. Ou 26 * 50 = 1300*.
* Você pode calcular nós de saudação em cada camada oculta da seguinte maneira:
  * **NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.
  * **NodeCount**\[1] = (13 - 5) / 2 + 1 = 5. 
  * **NodeCount**\[2] = (13 - 5) / 2 + 1 = 5. 
* Olá número total de nós pode ser calculado usando Olá declarado dimensionalidade de saudação da camada, [50, 5, 5], da seguinte maneira:  ***MapCount** * **NodeCount** \[ 0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*
* Porque **compartilhamento**[d] é False apenas para *d = = 0*, número de saudação de kernels é  ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*. 

## <a name="acknowledgements"></a>Confirmações
Olá linguagem Net # para personalizar a arquitetura de saudação de redes neurais foi desenvolvido na Microsoft pela Shon Katzenberger (arquiteto, aprendizado de máquina) e Alexey Kamenev (engenheiro de Software, Microsoft Research). Ela é usada internamente para projetos e aplicativos de análise de tootext de detecção de imagem de aprendizado de máquina. Para obter mais informações, consulte [redes neurais no Azure ML - Introdução tooNet #](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

