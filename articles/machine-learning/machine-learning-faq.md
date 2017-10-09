---
title: "Perguntas frequentes (FAQs) de aprendizado de máquina do aaaAzure | Microsoft Docs"
description: "Introdução ao Azure Machine Learning: perguntas frequentes sobre cobrança, recursos e limitações de um serviço de nuvem para modelagem preditiva simplificada."
keywords: "introdução ao aprendizado de máquina, modelagem preditiva, o que é aprendizado de máquina"
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a>Perguntas frequentes (FAQ) sobre o Azure Machine Learning: cobrança, recursos, limitações e suporte
Aqui estão algumas perguntas frequentes e as respostas correspondentes sobre o Azure Machine Learning, um serviço de nuvem para o desenvolvimento de modelos de previsão e soluções de operacionalização por meio de serviços Web. Essas perguntas frequentes fornecem perguntas sobre como toouse Olá serviço, que inclui a saudação modelo, recursos, limitações e suporte de cobrança.

**Tem alguma pergunta que você não encontrou aqui?**

O aprendizado de máquina do Azure tem um fórum do MSDN, onde os membros da comunidade de ciência de dados Olá poderá fazer perguntas sobre o aprendizado de máquina do Azure. equipe de aprendizado de máquina do Azure Olá monitora fórum hello. Vá toohello [Fórum de aprendizado de máquina do Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toosearch para respostas ou toopost uma nova pergunta de sua preferência.

## <a name="general-questions"></a>Perguntas gerais
**O que é Azure Machine Learning?**

O aprendizado de máquina do Azure é um serviço totalmente gerenciado que você pode usar toocreate, testar, operar e gerenciar soluções analíticas previsão na nuvem hello. Com apenas um navegador, agora você pode entrar, fazer upload de dados e iniciar imediatamente experimentos de aprendizado de máquina. Modelagem de previsão do tipo "arrastar e soltar", um grande palete de módulos e uma biblioteca de modelos de início tornam as tarefas comuns de Aprendizado de Máquina algo rápido e simples. Para obter mais informações, consulte Olá [visão geral do serviço de aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/). Para um aprendizado toomachine Introdução que explica os conceitos e terminologia importantes, consulte [tooAzure Introdução aprendizado de máquina](machine-learning-what-is-machine-learning.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**O que é o Machine Learning Studio?**

O Machine Learning Studio é um ambiente de trabalho que você acessa usando um navegador da Web. O estúdio de aprendizado de máquina hospeda uma paleta de módulos em uma interface de composição visual que ajuda a criar uma ponta a ponta, o fluxo de trabalho de ciência de dados na forma de saudação de um experimento.

Para saber mais sobre o Estúdio do Machine Learning, confira [O que é o Machine Learning Studio](machine-learning-what-is-ml-studio.md)

**O que é o serviço de API de aprendizado de máquina Olá?**

Olá serviço de API de aprendizado de máquina permite toodeploy modelos de previsão, como aqueles que são criados no estúdio de aprendizado de máquina, como serviços web escalonáveis e tolerantes a falhas. Olá web services que o serviço de API de aprendizado de máquina Olá cria são APIs de REST que fornecem uma interface para a comunicação entre aplicativos externos e seus modelos de análise de previsão.

Para obter mais informações, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).

**Onde estão listados os meus serviços Web clássicos? Onde estão listados os meus novos serviços da Web do Azure Resource Manager?**

Serviços Web criados usando Olá clássico implantação modelo e os serviços web criados usando o modelo de implantação do novo Azure Resource Manager Olá são listados na Olá [serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net/) portal.

Serviços web clássico também estão listados no [estúdio de aprendizado de máquina](http://studio.azureml.net) em Olá **serviços Web** guia.

## <a name="azure-machine-learning-questions"></a>Perguntas sobre o Azure Machine Learning
**O que são Serviços Web do Azure Machine Learning?**

Os Serviços Web do Machine Learning fornecem uma interface entre um aplicativo e um modelo de pontuação do fluxo de trabalho do Machine Learning. Um aplicativo externo pode usar toocommunicate de aprendizado de máquina do Azure com um modelo de pontuação de fluxo de trabalho do aprendizado de máquina em tempo real. Tooa uma chamada de serviço web de aprendizado de máquina retorna um aplicativo externo de tooan de resultados de previsão. toomake um serviço de web chamada tooa, você passar uma chave de API que foi criada quando você implantou o serviço web de saudação. Um serviço Web do Machine Learning baseia-se em REST, uma opção popular de arquitetura para projetos de programação da Web.

O Azure Machine Learning tem dois tipos de serviços Web:

* Serviço de solicitação-resposta (RR): Uma serviço altamente escalonável que fornece uma interface toohello modelos sem monitoração de estado de baixa latência criado e implantado usando o estúdio de aprendizado de máquina.
* Serviço de Execução de Lote (BES) – Um serviço assíncrono que pontua um lote de registros de dados.

Há várias maneiras de tooconsume Olá API REST do serviço e acesso Olá web. Por exemplo, você pode escrever um aplicativo em c#, R ou Python usando o código de exemplo hello que é gerado para você quando você implantou o serviço web de saudação.

o código de exemplo Hello está disponível em:
- página de consumir Olá para serviço web de saudação no portal de serviços de Web de aprendizado de máquina do Azure Olá
- Página de Ajuda da API de saudação no painel de serviço web Olá no estúdio de aprendizado de máquina

Você também pode usar a pasta de trabalho do hello exemplo Microsoft Excel que é criada e está disponível no painel de serviço web Olá no estúdio de aprendizado de máquina.

**Quais são Olá atualizações principal tooAzure aprendizado de máquina?**

Atualizações mais recentes do hello, consulte [o que há de novo no aprendizado de máquina do Azure](machine-learning-whats-new.md).

## <a name="machine-learning-studio-questions"></a>Perguntas sobre o Machine Learning Studio
### <a name="import-and-export-data-for-machine-learning"></a>Importar e exportar dados para o Machine Learning
**Para quais fontes de dados o Machine Learning dá suporte?**

Você pode baixar dados tooa experimento do estúdio de aprendizado de máquina de três maneiras:

- Carregar um arquivo local como um conjunto de dados
- Use um módulo tooimport os dados de serviços de dados de nuvem
- Importar um conjunto de dados salvo de outro experimento

toolearn mais sobre suporte para formatos de arquivo, consulte [importar dados de treinamento para o estúdio de aprendizado de máquina](machine-learning-data-science-import-data.md).

#### <a id="ModuleLimit"></a>Quão grande conjunto de dados de saudação possível para meu módulos?
Módulos no estúdio de aprendizado de máquina suportam conjuntos de dados de backup too10 GB de dados numéricos densos para casos de uso comuns. Se um módulo usa mais de uma entrada, hello valor de 10 GB é Olá total de entrada de todos os tamanhos. Você também pode conjuntos de dados de exemplo maiores usando consultas do Hive ou de banco de dados Azure SQL ou pode usar o Learning por meio contagens de pré-processamento antes da ingestão.  

Hello seguintes tipos de dados podem expandir toolarger conjuntos de dados durante a normalização do recurso e são limitados tooless que 10 GB:

* Esparsos
* Categóricos
* Cadeias de caracteres
* Dados binários

Olá módulos a seguir é limitados toodatasets com menos de 10 GB:

* Módulos de recomendação
* Módulo SMOTE (Técnica de Sobreamostragem Minoritária Sintética)
* Módulos de script: R, Python, SQL
* Módulos onde o tamanho dos dados de saída Olá podem ser maiores que o tamanho de dados de entrada, como Join ou hash de recurso
* Validação cruzada, ajustar o modelo Hiperparâmetros, regressão Ordinal e Multiclasse um-vs-todos, quando Olá número de iterações é muito grande

#### <a id="UploadLimit"></a>Quais são os limites de saudação para dados carregar?
Para conjuntos de dados que são maiores do que alguns GBs, carregar dados tooAzure armazenamento ou banco de dados SQL Azure, ou usar o Azure HDInsight em vez de carregar diretamente de um arquivo local.

**Eu posso ler dados da Amazon S3?**

Se você tiver uma pequena quantidade de dados e quiser tooexpose-los por meio de uma URL HTTP, em seguida, você pode usar o hello [importar dados] [ import-data] módulo. Para grandes quantidades de dados, transfira-tooAzure armazenamento primeiro e, em seguida, usar o hello [importar dados] [ import-data] toobring do módulo na sua experiência.
<!--

<SEE CLOUD DS PROCESS>
-->

**Há uma funcionalidade interna de entrada de imagem?**

Você pode aprender sobre a funcionalidade de entrada de imagem no hello [importar imagens] [ image-reader] referência.

### <a name="modules"></a>Módulos
**algoritmo de Hello, fonte de dados, o formato de dados ou operação de transformação de dados que estou procurando não está no estúdio de aprendizado de máquina do Azure. Quais são minhas opções?**

Você pode ir toohello [Fórum de comentários do usuário](http://go.microsoft.com/fwlink/?LinkId=404231) toosee recurso que estamos acompanhando as solicitações. Adicione sua solicitação de votação de tooa se um recurso que você está procurando já foi solicitado. Se o recurso de saudação que você está procurando não existir, crie uma nova solicitação. Você pode exibir status de saudação de sua solicitação neste fórum muito. Nós manterá essa lista de controle e atualizar o status de saudação da disponibilidade de recursos com frequência. Além disso, você pode usar o suporte interno a saudação de R e Python toocreate transformações personalizadas quando necessário.

**Posso trazer meu código existente para o Machine Learning Studio?**

Sim, você pode colocar seu código R ou Python existente no estúdio de aprendizado de máquina, executá-lo no hello mesmo experimentar aprendizes de aprendizado de máquina do Azure e implantar a solução hello como um serviço web por meio de aprendizado de máquina do Azure. Para obter mais informações, consulte [Estender seu experimento com R](machine-learning-extend-your-experiment-with-r.md) e [Executar scripts Python de aprendizado de máquina no Azure Machine Learning Studio](machine-learning-execute-python-scripts.md).

**É possível toouse algo como [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine um modelo?**

Não, não há suporte para PMML (Predictive Model Markup Language). Você pode usar o R personalizado e toodefine um módulo de código do Python.

**Quantos módulos posso executar em paralelo em meu experimento?**  

Você pode executar os módulos de toofour em paralelo em um experimento.

### <a name="data-processing"></a>Processamento de dados
**Há um capacidade toovisualize de dados (além de visualizações de R) interativamente no experimento Olá?**

Clique em saída Olá de um módulo toovisualize Olá de dados e obter estatísticas.

**Ao visualizar os resultados ou dados em um navegador, o número de saudação de linhas e colunas é limitado. Por quê?**

Porque grandes quantidades de dados podem ser enviadas tooa navegador, o tamanho dos dados é limitado tooprevent lentidão estúdio de aprendizado de máquina. toovisualize todos Olá/resultados de dados, é melhor toodownload Olá dados e usar o Excel ou outra ferramenta.

### <a name="algorithms"></a>Algoritmos

            **Quais algoritmos existentes têm suporte no Machine Learning Studio?**

O Machine Learning Studio fornece algoritmos de última geração, como Árvores de Decisão Aumentadas Escalonáveis, sistemas de Recomendação Bayesiana, Redes Neurais Profundas e Selvas de Decisão desenvolvidos na Microsoft Research. Pacotes de aprendizado de máquina escalonáveis de software livre, como Vowpal Wabbit, também estão incluídos. O Machine Learning Studio dá suporte a algoritmos de aprendizado de máquina para classificação binária e de múltiplas classes, de regressão e de clustering. Consulte a lista completa de saudação do [módulos de aprendizado de máquina][machine-learning-modules].

**Automaticamente sugere Olá direita aprendizado de máquina algoritmo toouse meus dados?**

Não, mas o estúdio de aprendizado de máquina tem várias maneiras toocompare resultados de saudação de cada algoritmo toodetermine Olá um certo para o seu problema.

**Você tem todas as orientações de separação de um algoritmo em detrimento de outro para os algoritmos de saudação fornecido?**

Consulte [como toochoose um algoritmo](machine-learning-algorithm-choice.md).

**Algoritmos de saudação fornecida são escritos em R ou Python?**

Não, esses algoritmos geralmente são gravados em um desempenho melhor tooprovide linguagens compiladas.

**São todos os detalhes dos algoritmos de saudação fornecidos?**

documentação de saudação fornece algumas informações sobre algoritmos de saudação e parâmetros para ajuste são algoritmo de saudação toooptimize descrito para seu uso.  

**Há algum suporte para aprendizado online?**

Não, atualmente há suporte apenas para treinamento programático.

**Pode visualizar as camadas de saudação de um modelo de rede Neural usando o módulo interno de Olá?**

Não.

**Posso criar meus próprio módulos em C# ou em outra linguagem?**

No momento, você pode usar somente módulos personalizados de R toocreate novo.

### <a name="r-module"></a>Módulo R
**Quais pacotes de R estão disponíveis no Machine Learning Studio?**

Estúdio de aprendizado de máquina dá suporte a mais de 400 CRAN R pacotes atualmente e aqui está o hello [lista atual](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) de todos os pacotes incluídos. Além disso, consulte [estender sua experiência com R](machine-learning-extend-your-experiment-with-r.md) toolearn como tooretrieve esta lista por conta própria. Se o pacote de saudação que você deseja não estiver nesta lista, forneça o nome de saudação do pacote de saudação em Olá [Fórum de comentários do usuário](http://go.microsoft.com/fwlink/?LinkId=404231).

**É possível toobuild um R personalizado módulo?**

Sim, consulte [Criar módulos personalizados em R no Azure Machine Learning](machine-learning-custom-r-modules.md) para saber mais.

**Há um ambiente REPL para R?**

Não há nenhum ambiente leitura Eval-impressão-Loop REPL () para R no studio hello.

### <a name="python-module"></a>Módulo de Python
**É possível toobuild um módulo personalizado de Python?**

Não no momento, mas você pode usar um ou mais [Executar Script Python] [ python] tooget módulos Olá mesmo resultado.

**Há um ambiente REPL para Python?**

Você pode usar anotações do Jupyter Olá no estúdio de aprendizado de máquina. Para saber mais, confira [Introdução aos blocos de notas Jupyter no Azure Machine Learning Studio](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).

## <a name="web-service"></a>Serviço Web
### <a name="retrain"></a>Treinar novamente
**Como posso readaptar os modelos de Machine Learning de forma programática?**

Use Olá APIs de treinamento. Para obter mais informações, consulte [Treinar novamente os modelos de Machine Learning de forma programática](machine-learning-retrain-models-programmatically.md). Exemplo de código também está disponível no hello [demonstração de treinamento do Microsoft Azure aprendizado de máquina](https://azuremlretrain.codeplex.com/).

### <a name="create"></a>Criar
**Pode implantar o modelo de saudação localmente ou em um aplicativo que não tenha uma conexão de Internet?**

Não.

**Há uma latência de linha de base que é esperada para todos os serviços Web?**

Consulte Olá [limites de assinatura do Azure](../azure-subscription-service-limits.md).

### <a name="use"></a>Uso
**Quando devo toorun meu modelo de previsão como um serviço de execução em lotes em vez de um serviço de resposta da solicitação?**

saudação (RR) de serviço de resposta da solicitação é uma baixa latência, modelos de serviço web de grande escala que é usado tooprovide toostateless uma interface que são criados e implantados do ambiente de experimentação hello. saudação (BES) de serviço de execução de lote é um serviço que pontuações de maneira assíncrona um lote de registros de dados. Olá para BES é de entrada como entrada de dados que usa registros de recursos. Olá principal diferença é que o BES lê um bloco de registros de uma variedade de fontes, como o armazenamento de BLOBs do Azure, armazenamento de tabela do Azure, banco de dados do SQL Azure, HDInsight (consulta de hive) e fontes HTTP. Para obter mais informações, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).

**Como atualizar o modelo Olá para o serviço web de saudação implantado?**

tooupdate um modelo de previsão para um serviço já implantado, modificar e executar novamente o teste Olá que você usou tooauthor e salvar o modelo treinado hello. Depois de instalar uma nova versão do modelo treinado de saudação disponível, o estúdio de aprendizado de máquina perguntando se deseja tooupdate seu serviço web. Para obter detalhes sobre como tooupdate um serviço da web implantados, consulte [implantar um serviço web de aprendizado de máquina](machine-learning-publish-a-machine-learning-web-service.md).

Você também pode usar o hello Retraining APIs.
Para obter mais informações, consulte [Treinar novamente os modelos de Machine Learning de forma programática](machine-learning-retrain-models-programmatically.md). Exemplo de código também está disponível no hello [demonstração de treinamento do Microsoft Azure aprendizado de máquina](https://azuremlretrain.codeplex.com/).

**Como posso monitorar meu serviço Web implantado na produção?**

Depois de implantar um modelo de previsão, você pode monitorá-lo da saudação clássico do Azure portal (serviços web clássico somente) ou o portal de serviços de Web de aprendizado de máquina do Azure hello. Cada serviço implantado tem seu próprio painel, onde você pode ver informações de monitoramento do serviço. Para obter mais informações sobre como toomanage seus serviços web implantados, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md) e [gerenciar um espaço de trabalho do aprendizado de máquina do Azure](machine-learning-manage-workspace.md).

**Há um lugar onde posso ver saída de saudação do meu RRS/BES?**

Registros de recursos, resposta do serviço da web hello normalmente é onde você pode ver o resultado de saudação. Você também pode escrever-tooAzure o armazenamento de Blob. Para BES, saída de hello é escrita blob tooa por padrão. Você também pode escrever a tabela ou banco de dados do hello saída tooa usando Olá [exportar dados] [ export-data] módulo.

**Posso criar serviços Web apenas de modelos criados no Machine Learning Studio?**

Não, você também pode criar serviços Web diretamente usando blocos de anotações do Jupyter e RStudio.

**Onde posso encontrar informações sobre códigos de erro?**

Confira [Códigos de erro do módulo de Machine Learning](https://msdn.microsoft.com/library/azure/dn905910.aspx) para obter uma lista dos códigos de erro e descrições.

## <a name="scalability"></a>Escalabilidade
**O que é a escalabilidade de saudação do serviço web de Olá?**

No momento, o ponto de extremidade saudação padrão é configurado com 20 solicitações RRS simultâneas por ponto de extremidade. Você pode expandir esse solicitações simultâneas de too200 por ponto de extremidade, e você pode dimensionar cada too10 de serviço web, pontos de extremidade 000 por serviço da web, conforme descrito em [dimensionamento de um serviço Web](machine-learning-scaling-webservice.md). Para BES, cada ponto de extremidade pode processar 40 solicitações por vez. Acima de 40 solicitações, as restantes são enfileiradas. Essas solicitações em fila executado automaticamente como Olá sai de fila.

**Trabalhos em R são distribuídos entre nós?**

Nº  

**Quantos dados posso usar para treinamento?**

Módulos no estúdio de aprendizado de máquina suportam conjuntos de dados de backup too10 GB de dados numéricos densos para casos de uso comuns. Se um módulo usa total Olá de entrada, mais de um tamanho de todas as entradas é 10 GB. Você também pode criar amostras de conjuntos de dados maiores por meio de consultas Hive, por meio de consultas ao Banco de Dados SQL do Azure ou fazer o pré-processamento com módulos [Aprendizado por contagens][counts] antes do uso.  

Hello seguintes tipos de dados podem expandir toolarger conjuntos de dados durante a normalização do recurso e são limitados tooless que 10 GB:

* Esparsos
* Categóricos
* Cadeias de caracteres
* Dados binários

Olá módulos a seguir é limitados toodatasets com menos de 10 GB:

* Módulos de recomendação
* Módulo SMOTE (Técnica de Sobreamostragem Minoritária Sintética)
* Módulos de script: R, Python, SQL
* Módulos onde o tamanho dos dados de saída Olá podem ser maiores que o tamanho de dados de entrada, como Join ou hash de recurso
* Validação Cruzada, Hiperparâmetros de Modelo de Ajuste, Regressão Ordinal e Classes Múltiplas, um versos todos, quando o número de iterações é muito grande

Para conjuntos de dados que são maiores do que alguns GBs, carregar dados tooAzure armazenamento ou banco de dados SQL Azure, ou use HDInsight em vez de carregar diretamente de um arquivo local.

**Há qualquer limitação de tamanho de vetores?**

Linhas e colunas são cada limitação de .NET toohello limitado de Max Int: 2.147.483.647.

**Pode ajustar Olá tamanho da saudação máquina virtual que executa o serviço web de Olá?**

Não.  

## <a name="security-and-availability"></a>Segurança e disponibilidade
**Quem pode acessar o ponto de extremidade de http de saudação do serviço web de saudação por padrão? Como restringir o acesso toohello endpoint?**

Depois que um serviço Web for implantado, criaremos um ponto de extremidade padrão para esse serviço. ponto de extremidade saudação padrão pode ser chamado usando sua chave de API. Você pode adicionar que mais pontos de extremidade com suas próprias chaves de saudação portal clássico do Azure ou programaticamente usando Olá APIs de gerenciamento de serviço da Web. Chaves de acesso são chamadas de toomake necessária toohello serviço de web. Para obter mais informações, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).

**O que acontece se minha conta de armazenamento do Azure não puder ser encontrada?**

Estúdio de aprendizado de máquina depende de um armazenamento do Azure fornecido pelo usuário conta toosave intermediário de dados quando ele executa o fluxo de trabalho de saudação. Esta conta de armazenamento é fornecida tooMachine estúdio de aprendizado quando é criado um espaço de trabalho. Depois de saudação espaço de trabalho é criado, se a conta de armazenamento Olá é excluída e não pode mais ser encontrada, espaço de trabalho Olá deixarão de funcionar e todas as experiências em que o espaço de trabalho falhará.

Se você acidentalmente excluir conta de armazenamento Olá, recrie a conta de armazenamento Olá com hello mesmo nome no hello mesma região Olá excluir conta de armazenamento. Depois disso, ressincronizar a chave de acesso de saudação.

**O que acontecerá se a chave de acesso da minha conta de armazenamento não estiver sincronizada?**

Estúdio de aprendizado de máquina depende de um armazenamento do Azure fornecido pelo usuário conta toostore intermediário de dados quando ele executa o fluxo de trabalho de saudação. Esta conta de armazenamento é fornecida tooMachine estúdio de aprendizado, quando um espaço de trabalho é criado, e chaves de acesso Olá estão associadas esse espaço de trabalho. Se as chaves de acesso de saudação são alteradas após a criação do espaço de trabalho Olá, espaço de trabalho de saudação não pode acessar a conta de armazenamento de saudação. Ele deixará de funcionar e todos os testes no espaço de trabalho falharão.

Se você alterou as chaves de acesso da conta de armazenamento, a ressincronização Olá chaves de acesso no espaço de trabalho hello usando Olá portal clássico do Azure.  

## <a name="support-and-training"></a>Suporte e treinamento
**Onde posso obter treinamento para o Azure Machine Learning?**

Olá [Centro de documentação do aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) hospeda tutoriais em vídeo e como tooguides. Essas guias passo a passo apresentam Olá serviços e explicam o ciclo de vida de ciência de dados de Olá de importação de dados, limpeza de dados, criação de modelos de previsão e implantá-las na produção usando o aprendizado de máquina do Azure.

Adicionamos toohello material novo centro de aprendizado de máquina em uma base contínua. Você pode enviar solicitações para material de aprendizagem adicionais no Centro de aprendizado de máquina em Olá [Fórum de comentários do usuário](https://windowsazure.uservoice.com/forums/257792-machine-learning).

Você também pode encontrar treinamento na [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning).

**Como fazer para obter suporte ao Azure Machine Learning?**

o suporte técnico tooget para aprendizado de máquina do Azure, vá muito[suporte do Azure](/support/options/)e selecione **aprendizado de máquina**.

O Azure Machine Learning também possui um fórum de comunidade no MSDN, em que é possível fazer perguntas sobre o Azure Machine Learning. equipe de aprendizado de máquina do Azure Olá monitora fórum hello. Vá muito[Fórum do Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).

## <a name="billing-questions"></a>Perguntas sobre cobrança

            **Como a cobrança do Machine Learning funciona?**

O Azure Machine Learning tem dois componentes: Machine Learning e serviços Web do Machine Learning Studio.

Enquanto você estiver avaliando o estúdio de aprendizado de máquina, você pode usar a camada gratuita de cobrança hello. camada gratuita Olá também permite que você implante um serviço web clássico que tem a capacidade limitada.

Se você decidir que o aprendizado de máquina do Azure atende às suas necessidades, você pode se inscrever para Olá camada padrão. toosign backup, você deve ter uma assinatura Microsoft Azure.

Na camada padrão do hello, você será cobrado mensal para cada espaço de trabalho que você define no estúdio de aprendizado de máquina. Quando você executa um teste no studio hello, você será cobrado por recursos de computação quando você estiver executando um experimento. Quando você implanta um serviço web de clássico, transações e horas são cobradas individualmente pré-pago Olá de computação.

Novos serviços Web (baseados no Gerenciador de Recursos) introduzem planos de cobranças que permitem maior previsibilidade nos custos. Preços hierárquico oferece toocustomers descontos que precisam de uma grande quantidade de capacidade.

Quando você cria um plano, você pode confirmar tooa custo vem com uma quantidade incluída de horas de computação de API e transações de API fixo. Se você precisar de mais quantidades incluídas, você pode adicionar instâncias tooyour plano. Se precisar de muito mais quantidades incluídas, você poderá escolher um plano de camada superior que tenha quantidades incluídas ainda maiores e uma melhor taxa de desconto.

Depois hello quantidades incluídas em instâncias existentes são usadas, uso adicional de é cobrado a taxa de excedentes Olá associado à camada de plano de cobrança de saudação.

> [!NOTE]
Quantidades incluídas são realocadas a cada 30 dias e quantidades incluídas não usadas não passam toohello próximo período.

Para saber mais sobre preços e cobrança, confira [Preços do Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).


            **O Machine Learning tem uma avaliação gratuita?**

 O Azure Machine Learning tem uma opção de assinatura gratuita que é explicada em [Preços do Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/). O estúdio de aprendizado de máquina tem uma versão de avaliação de oito horas avaliação que está disponível quando você entrar no muito[estúdio de aprendizado de máquina](https://studio.azureml.net/?selectAccess=true&o=2).

 Além disso, quando você se inscrever em uma avaliação gratuita do Azure, poderá experimentar qualquer serviço do Azure por um mês. toolearn mais sobre Olá avaliação gratuita do Azure, visite [perguntas Frequentes avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial-faq/).

**O que é uma transação?**

Uma transação representa uma chamada à API a qual responde o Azure Machine Learning. AS chamadas RRS (Serviço de solicitação-resposta) e BES (Serviço de execução em lote) são agregadas e cobradas em seu plano de cobrança.

**Posso usar quantidades de transação Olá incluído em um plano para transações RRS e BES?**

Sim, as transações dos RRS e BES são agregadas e cobradas em seu plano de cobrança.

**O que é uma hora de computação de API?**

Uma hora de computação de API é a unidade de cobrança de saudação para recursos de computação toorun de realizar chamadas API usando o aprendizado de máquina do tempo de saudação. Todas as chamadas são agregadas para fins de cobrança.

**Quanto tempo demora uma chamada típica à API de produção?**

Tempos de chamada de API de produção podem variar significativamente, geralmente, variando de centenas de milissegundos tooa alguns segundos. Algumas chamadas de API podem exigir minutos, dependendo da complexidade de saudação do modelo de aprendizado de máquina e processamento de dados de saudação. Olá melhor maneira tooestimate API de produção chamada vezes é toobenchmark um modelo em Olá service de aprendizado de máquina.

**O que é uma hora de computação do Studio?**

Uma hora de computação Studio é a unidade de cobrança de saudação para tempo de agregação de saudação que suas experiências usam recursos de computação no studio.

**De novos serviços web (baseados no Gerenciador de recursos do Azure), o que nível de desenvolvimento/teste Olá destina?**

Serviços web baseados em Gerenciador de recursos fornecem várias camadas que você pode usar tooprovision seu plano de cobrança. Olá preço de desenvolvimento/teste fornece quantidades limitadas, incluídas que permitem que você tootest sua experiência como um serviço web sem incorrer em custos. Você tem Olá oportunidade toosee como ele funciona.

**Existem encargos de armazenamento separados?**

camada gratuita de aprendizado de máquina Olá não exige ou permitir o armazenamento separado. camada padrão de aprendizado de máquina Olá requer usuários toohave uma conta de armazenamento do Azure. O Armazenamento do Azure [é cobrado separadamente](https://azure.microsoft.com/pricing/details/storage/).

**O Machine Learning dá suporte a alta disponibilidade?**

Sim. Para obter detalhes, consulte [preços de aprendizado de máquina](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) para obter uma descrição do contrato de nível de serviço (SLA) do hello.

**Em quais tipos específicos de recursos de computação minhas chamadas à API de produção serão executadas?**

Olá service de aprendizado de máquina é um serviço multilocatário. Recursos de computação real que são usados no back-end Olá variam e são otimizados para desempenho e previsibilidade.

### <a name="management-of-new-resource-manager-based-web-services"></a>Gerenciamento de novos serviços Web (com base no Gerenciador de Recursos)
**O que acontece se eu excluir meu plano?**

Olá plano é removido de sua assinatura, e você será cobrado por uso especial.

> [!NOTE]
Você não pode excluir um plano que um serviço Web está usando. plano de saudação toodelete, você deve atribuir um novo plano de serviço da web de toohello ou excluir o serviço web de saudação.

**O que é uma instância de plano?**

Uma instância de plano é uma unidade de quantidades incluídas que você pode adicionar tooyour plano de cobrança. Quando você seleciona uma camada de cobrança para o plano de cobrança, ela vem com uma instância. Se você precisar de mais quantidades incluídas, você pode adicionar instâncias de saudação selecionado camada tooyour plano de cobrança.

**Quantas instâncias do plano posso adicionar?**

Você pode ter uma instância da camada de preços de desenvolvimento/teste Olá em uma assinatura.

Para as camadas Standard S1, Standard S2 e Standard S3, você pode adicionar tantas quantas forem necessárias.

> [!NOTE]
Dependendo de seu uso antecipado, ele pode ser mais econômica camada tooa tooupgrade mais incluído quantidades em vez de adicionar instâncias toohello atual camada.

**O que acontece quando eu mudo de camadas de plano (atualização/downgrade)?**

plano antigo Olá é excluído e o uso atual de saudação é cobrado em uma base pro rata. É criado um novo plano com quantidades de incluído completo Olá da camada de upgrade/downgrade Olá restante de saudação do período de saudação.

> [!NOTE]
As quantidades incluídas são alocadas por período e as quantidades não usadas não são transferidas para o período seguinte.

**O que acontece quando aumentar as instâncias de saudação em um plano?**

Quantidades são incluídas em uma base pro rata e podem demorar 24 horas toobe efetivo.

**O que acontece quando eu excluo uma instância de um plano?**

Olá instância é removida de sua assinatura, e você será cobrado por uso especial.

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a>Inscrever-se em novos planos de serviços Web (com base no Gerenciador de Recursos)
**Como faço para assinar um plano?**

Você tem dois planos de cobrança de toocreate de maneiras.

Ao implantar pela primeira vez um serviço Web baseado no Gerenciador de Recursos, você pode escolher um plano existente ou criar um novo.

Os planos criados dessa maneira são em sua região padrão e o serviço da web será implantado toothat região.

Se você quiser toodeploy serviços tooregions diferente de sua região padrão, convém toodefine seus planos de cobrança antes de implantar seu serviço.

Nesse caso, você pode entrar no portal de serviços de Web de aprendizado de máquina do Azure toohello e acesse a página de planos toohello. A partir daí, você pode adicionar e excluir planos e modificar os existentes.

**Plano que devo escolher toostart desativado com?**

É recomendável que começam com hello Standard S1 camada e monitorar seu serviço para uso. Se você achar que você está usando suas quantidades incluídas rapidamente, você pode adicionar instâncias ou mover a camada superior tooa e obter melhor descontos. Você pode ajustar seu plano de cobrança conforme o necessário em todo seu ciclo de cobrança.

**Quais regiões estão disponíveis na novos planos de saudação?**

novos planos de cobrança Olá estão disponíveis em Olá três produção regiões em que há suporte para serviços web da nova hello:

* Centro-Sul dos Estados Unidos
* Europa Ocidental
* Sudeste da Ásia

**Tenho serviços Web em várias regiões. Preciso de um plano para cada região?**

Sim. Os preços de planos variam para cada região. Quando você implanta uma região de tooanother de serviço da web, você precisa tooassign it um plano que é a região toothat específico. Para obter mais informações, veja [Produtos disponíveis por região]( https://azure.microsoft.com/regions/services/).

### <a name="new-web-services-overages"></a>Novos serviços Web: Excedentes
**Como verificar se excedi o uso do serviço Web?**

Você pode exibir o uso de saudação em todos os seus planos na página de planos de saudação no portal de serviços de Web de aprendizado de máquina do Azure hello. Entrar no portal de toohello e, em seguida, clique em Olá **planos** opção de menu.

Em Olá **transações** e **de computação** colunas de tabela hello, você pode ver quantidades Olá incluído do plano hello e percentual usado da saudação.

**O que acontece quando eu uso a saudação incluir quantidades na camada de preços de desenvolvimento/teste Olá?**

Serviços que têm um preço toothem nível atribuído de desenvolvimento/teste são interrompidos até Olá próximo período ou até que você mova camada tooa pago.

**Para os serviços Web Clássico e excedentes de serviços Web Novos (com base no Gerenciador de Recursos), como os preços são calculados para cargas de trabalho de RRS (Solicitação de Resposta) e BES (Lote)?**

Para uma carga de trabalho de registros de recursos, você é cobrado para cada chamada de transações de API que você faz em tempo de computação Olá associada a essas solicitações. Os custos de transações de API de produção RRS são calculados como o número total de saudação de chamadas de API que você fizer multiplicada pelo preço de saudação por 1.000 transações (divididos pelas transações individuais). Os custos de hora de computação de API de produção RRS API são calculados como valor de saudação do tempo necessário para cada toorun de chamada de API, multiplicado pelo número total de saudação de transações de API, multiplicada pelo Olá preço por hora de computação de API de produção.

Por exemplo, para a média do Standard S1, 1.000.000 transações de API que levam segundos 0.72 cada toorun resultaria em (1.000.000 * US $0,50 / 1K transações de API) de US $500 em custos de transações de API de produção e (1.000.000 * 0.72 s * $2 / h) $400 em computação de API de produção horas, para um total de US $900.

Para uma carga de trabalho do BES, você será cobrado no hello mesma maneira. No entanto, os custos de transações de API Olá representam o número de saudação de trabalhos em lotes que você enviar, e os custos de computação Olá representam o tempo de computação Olá associada a esses trabalhos em lotes. Os custos de transações de API de produção BES são calculados como o número total de saudação de trabalhos enviados multiplicada pelo preço de saudação por 1.000 transações (divididos pelas transações individuais). Os custos de horas de computação de API de produção BES API são calculados como valor de saudação do tempo necessário para cada linha na sua toorun trabalho multiplicado pelo número total de saudação de linhas no seu trabalho multiplicado pelo número total de saudação de trabalhos multiplicada pelo preço de saudação por API de produção horas de computação. Quando você usa Olá Calculadora de aprendizado de máquina, Olá transação medidor representa Olá número de trabalhos que você planejar toosubmit e campo de hora por transação Olá representa Olá combinados tempo que é necessário para todas as linhas em cada toorun de trabalho.

Por exemplo, suponha que Standard S1 seja excedente e você envie 100 trabalhos por dia, cada um consistindo em 500 linhas que utilizam 0,72 segundo. Os custos mensais excedentes seriam (100 trabalhos por dia = 3.100 trabalhos/mês * US$ 0,50/1K transações de API) US$ 1,55 em custos de transação de API de produção e (500 linhas * 0,72 s * 3.100 trabalhos * US$ 2/hora) US$ 620 em horas de computação de API de produção, para um total de US$ 621,55.

### <a name="azure-machine-learning-classic-web-services"></a>Serviços Web Clássicos do Azure Machine Learning
**O pré-pago ainda está disponível?**

Sim, os serviços Web clássicos ainda estão disponíveis no Azure Machine Learning.  

### <a name="azure-machine-learning-free-and-standard-tier"></a>Camadas Gratuita e Standard do Machine Learning
**O que está incluído na camada gratuita de aprendizado de máquina do Azure Olá?**

camada gratuita de aprendizado de máquina do Azure Olá é pretendido tooprovide toohello uma introdução detalhada estúdio de aprendizado de máquina do Azure. Tudo o que você precisa é um toosign de conta da Microsoft. Olá camada gratuita inclui o espaço de trabalho do acesso livre tooone estúdio de aprendizado de máquina do Azure por [conta da Microsoft](https://www.microsoft.com/account/default.aspx). Nesse nível, você pode usar a too10 GB de armazenamento e utilizar modelos como as APIs de preparo. Cargas de trabalho de camada gratuita não são cobertas por um SLA e destinam-se ao desenvolvimento e uso pessoal. 

Espaços de trabalho de camada gratuita tem Olá seguintes limitações:

* Cargas de trabalho não podem acessar dados conectando o servidor de local de tooan que executa o SQL Server.
* Não é possível implantar os serviços Web base do Novo Gerenciador de Recursos.


**O que está incluído no nível padrão de aprendizado de máquina do Azure hello e planos?**

camada de saudação padrão de aprendizado de máquina do Azure é uma versão de produção paga do estúdio de aprendizado de máquina do Azure. Olá estúdio de aprendizado de máquina do Azure taxa mensal é cobrada em um por base do espaço de trabalho por mês e rateados meses parcial. Horas de experimento do Azure Machine Learning Studio são cobradas por hora de computação por experimento ativo. A cobrança é rateada em horas parciais.  

Olá serviço de API de aprendizado de máquina do Azure é cobrado dependendo se é um serviço da web clássico ou um novo serviço da web (com base em Gerenciador de recursos).

Olá encargos a seguir é agregada por espaço de trabalho para a sua assinatura.

* Assinatura de espaço de trabalho do aprendizado de máquina: Olá assinatura de espaço de trabalho do aprendizado de máquina é uma taxa mensal que fornece espaço de trabalho do access tooa estúdio de aprendizado de máquina. assinatura de saudação é toorun necessário experiências em Olá studio tooutilize Olá produção e APIs.
* Horas de teste no Studio: Esse medidor agrega todos os encargos de computação que são acumulados executando experiências no estúdio de aprendizado de máquina e chamadas de API de produção em execução no ambiente de preparo de saudação.
* Acessar dados conectando-se o servidor de local de tooan que executa o SQL Server em seus modelos para o treinamento e pontuação.
* Para serviços Web clássicos:
  * Horas de Computação da API de Produção: esse medidor inclui cobranças de computação vencidas por serviços Web em execução na produção.
  * Transações de API de produção (por 1000): Esse medidor inclui encargos serão acumulados por serviço de web chamada tooyour de produção.

Além de saudação anterior encargos, no caso de saudação do serviço web baseado em Gerenciador de recursos, os encargos são plano selecionado toohello agregado:

* Planejar padrão do API de S2/S1/S3 (unidades): Esse medidor representa o tipo hello da instância selecionada para serviços web baseados em Gerenciador de recursos.
* Padrão horas excedente de computação de API de S2/S1/S3: Esse medidor inclui encargos de computação que são acumulados pelos serviços web baseados em Gerenciador de recursos que são executados em produção depois que as quantidades de saudação incluída nas instâncias existentes são usadas. uso de saudação adicional é cobrado nos Olá overate taxa associada à camada de plano de S2/S1/S3.
* Padrão transações de API excedentes S2/S1/S3 (por 1000): Esse medidor inclui os encargos serão acumulados por chamada tooyour produção serviço web baseado em Gerenciador de recursos depois Olá incluída quantidades em instâncias existentes sejam usados. Olá uso adicional é cobrado nos Olá overate taxa associada à camada de plano de S2/S1/S3.
* Incluído quantidade de horas de computação de API: Com serviços da web com base no Gerenciador de recursos, esse medidor representa quantidade Olá incluída de horas de computação de API.
* Incluído a quantidade de transações de API (por 1000): serviços web baseados em com o Gerenciador de recursos, esse medidor representa a quantidade de saudação incluída de transações de API.

**Como assinar a camada gratuita do Azure Machine Learning?**

Tudo o que você precisa é de uma conta da Microsoft. Vá muito[inicial de aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/)e, em seguida, clique em **iniciar agora**. Entre com sua conta da Microsoft e um espaço de trabalho na camada Gratuita será criado para você. Você pode iniciar tooexplore e criar experiências de aprendizado de máquina imediatamente.

**Como assinar a camada Standard do Azure Machine Learning?**

Primeiro você deve ter acesso tooan assinatura do Azure toocreate um espaço de trabalho do aprendizado de máquina padrão. Você pode se inscrever para uma assinatura de Azure avaliação gratuita da 30 dias e tooa atualização posterior paga a assinatura do Azure, ou você pode comprar uma assinatura paga do Azure imediatamente. Você pode criar um espaço de trabalho do aprendizado de máquina do portal clássico do Microsoft Azure Olá depois de obter acesso toohello assinatura. Saudação de exibição [instruções passo a passo](https://azure.microsoft.com/trial/get-started-machine-learning-b/).

Como alternativa, você pode ser convidado por espaço de trabalho de um padrão de aprendizado de máquina espaço de trabalho proprietário tooaccess saudação do proprietário.

**Pode especificar meu próprio toouse de conta de armazenamento de BLOBs do Azure com a camada gratuita Olá?**

Não, camada de saudação padrão é versão toohello equivalente Olá service de aprendizado de máquina que estava disponível antes de saudação camadas foram introduzidas.

**Posso implantar minha máquina aprender os modelos como APIs na camada gratuita Olá?**

Sim, você pode colocar em operação modelos de aprendizado de máquina toostaging API serviços como parte da camada gratuita hello. tooput Olá preparo do serviço de API em produção e obter um ponto de extremidade de produção para o serviço de saudação operacionalizada, você deve usar a camada padrão hello.

**Qual é a diferença Olá entre avaliação gratuita do Azure e a camada gratuita de aprendizado de máquina do Azure?**

Olá [avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/free/) oferece que você pode aplicar tooany Azure os créditos de serviço por um mês. Olá livre de aprendizado de máquina do Azure camada ofertas contínua acessar especificamente tooAzure aprendizado de máquina para cargas de trabalho de não produção.

**Como mover um experimento de camada padrão da saudação camada gratuita toohello?**

toocopy suas experiências de camada padrão da saudação camada gratuita toohello:

1. Entrar no estúdio de aprendizado de máquina do tooAzure e certifique-se de que você pode ver o espaço de trabalho grátis hello e espaço de trabalho padrão no seletor de espaço de trabalho de saudação na barra de navegação superior Olá Olá.
2. Alternar tooFree espaço de trabalho se você está no espaço de trabalho padrão hello.
3. Na exibição de lista do experimento hello, selecione um experimento que seria como toocopy e, em seguida, clique em Olá **cópia** botão de comando.
4. Selecione o espaço de trabalho padrão do Olá Olá caixa de diálogo que é aberta e clique em Olá **cópia** botão.
   Todos os Olá conjuntos de dados associados, treinado, etc. são copiadas junto com a experiência Olá no espaço de trabalho padrão Olá.
5. Você precisa toorerun Olá experimento e republicar o serviço da web no espaço de trabalho padrão hello.

### <a name="studio-workspace"></a>Espaço de trabalho do Studio
**Existem faturas diferentes para espaços de trabalho diferentes?**

As cobranças referentes a espaços de trabalho são divididas em separado para cada medidor aplicável em uma única fatura.

**Em quais tipos de recursos de computação específicos meus testes serão executados?**

Olá service de aprendizado de máquina é um serviço multilocatário. Recursos de computação real que são usados no back-end Olá variam e são otimizados para desempenho e previsibilidade.

### <a name="guest-access"></a>Acesso de Convidado
**O que é o acesso de convidado tooAzure estúdio de aprendizado de máquina?**

O Acesso de Convidado é uma experiência de avaliação restrita. Você pode criar e executar experimentos no Azure Machine Learning Studio sem custo adicional e sem autenticação. Sessões de convidado são não persistentes (não é possível salvar) e limitado tooeight horas. Outras limitações incluem falta de suporte para R e Python, falta de APIs de preparo e capacidade de armazenamento e tamanho restritos do conjunto de dados. Por comparação, os usuários que optam toosign com uma conta da Microsoft tem acesso completo toohello grátis de máquina estúdio de aprendizado que é descrita anteriormente, que inclui um espaço de trabalho persistente e recursos mais abrangentes. toochoose o aprendizado de máquina livre experiência, clique em **começar** na [https://studio.azureml.net](https://studio.azureml.net)e, em seguida, selecione **acesso adivinhar** ou entre com um Microsoft conta.

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
