---
title: "aaaAzure ciclo de vida de processo do Team dados ciência | Microsoft Docs"
description: "As etapas necessárias tooexecute seus projetos de ciência de dados."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 58114a1c2d3289d1c4b2781219d0bf9647dbccd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-lifecycle"></a>Ciclo de vida do Processo de Ciência de Dados de Equipe

Olá processo de ciência de dados da equipe (TDSP) fornece um ciclo de vida recomendado que você pode usar toostructure seus projetos de ciência de dados. ciclo de vida de saudação descreve as etapas de hello, do início toofinish, que projetos normalmente seguem quando eles são executados. Se você estiver usando outro ciclo de ciência de dados, como [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) ou o processo personalizado da organização, você ainda pode usar Olá baseado em tarefa TDSP com esses ciclos de vida de desenvolvimento. 

Esse ciclo de vida foi projetado para projetos de ciência de dados que são planejado tooship como parte de aplicativos inteligentes. Esses aplicativos implantam modelos de machine learning ou de inteligência artificial para análise preditiva. Os projetos de ciência de dados exploratórios e os projetos de análise ad hoc também podem se beneficiar do uso desse processo. Mas, nesses casos, algumas etapas descritas podem não ser necessárias.    

Aqui está uma representação visual de saudação **ciclo de vida do processo de ciência de dados de equipe**. 

![Ciclo de vida do TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

ciclo de vida do Hello TDSP é composto de cinco etapas principais que são executadas de forma iterativa. Estão incluídos:

* **Noções básicas sobre negócios**
* **Aquisição de dados e reconhecimento**
* **Modelagem**
* **Implantação**
* **Aceitação do cliente**

Para cada estágio, fornecemos Olá informações a seguir:

* **Metas**: Olá objetivos específicos.
* **Como toodo-**: Olá tarefas específicas descritas e orientação fornecidos na conclusão-los.
* **Artefatos**: hello e resultados de saudação suportam para produção.


## <a name="1-business-understanding"></a>1. Noções básicas sobre negócios

### <a name="goals"></a>Metas
* Olá **chave variáveis** especificados que estão tooserve como Olá **destinos de modelo** e cujas as métricas relacionadas são usadas determinar Olá sucesso para o projeto de saudação.
* Olá relevante **fontes de dados** são identificados business Olá tem acesso tooor necessidades tooobtain.

### <a name="how-toodo-it"></a>Como toodo-lo
Há duas tarefas principais abordadas neste estágio: 

* **Definir objetivos**: trabalhar com o cliente e outros participantes toounderstand e identificar problemas de negócios hello. Formule as perguntas que definem que técnicas de ciência de dados podem direcionar e metas de negócios de saudação.
* **Identificar as fontes de dados**: localizar Olá dados relevantes que o ajuda a responder perguntas de saudação que definem os objetivos de saudação do projeto de saudação.

#### <a name="11-define-objectives"></a>1.1 Definir os objetivos

1. Um objetivo central desta etapa é a chave de saudação do tooidentify **variáveis de negócios** que as necessidades de análise de saudação toopredict. Essas variáveis são chamados tooas Olá **modelo destinos** e métricas de saudação associadas a eles são usados toodetermine Olá sucesso Olá projeto. Dois exemplos de tais destinos são a probabilidade de previsão ou hello vendas de um pedido sendo fraudulentas.

2. Definir Olá **metas do projeto** solicitando e refinar as perguntas "nitidez" específicas que são relevantes e não ambígua. Ciência de dados é o processo de saudação do uso de nomes e números tooanswer essas perguntas. Para obter mais informações sobre como fazer perguntas curva, consulte [como toodo ciência de dados](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/) blog. Ciência de dados / aprendizado de máquina é normalmente usada tooanswer cinco tipos de perguntas:
 
   * Quanto custa ou quantos? (regressão)
   * Qual categoria? (classificação)
   * Qual grupo? (clustering)
   * Isso é estranho? (detecção de anomalias)
   * Qual opção deve ser escolhida? (recomendação)

    Determine quais dessas perguntas você está fazendo e como suas respostas alcançam suas metas de negócios.

3. Definir Olá **projeto de equipe** especificando Olá de funções e responsabilidades de seus membros. Desenvolva um plano de marcos de alto nível que pode ser usado para iteração, conforme mais informações são descobertas.  

4. **Defina as métricas de sucesso**. Por exemplo: conseguir cliente variação de precisão da previsão X % final Olá deste projeto de 3 meses, de forma que podemos oferecer promoções tooreduce variação. métricas de saudação devem ser **inteligente**: 
   * E**S**pecíficas 
   * **M**ensuráveis
   * **A**lcançáveis 
   * **R**elevantes 
   * Com limite de **T**empo 

#### <a name="12-identify-data-sources"></a>1.2 Identificar as fontes de dados
Identificar as fontes de dados que contêm exemplos conhecidos de perguntas de curva de tooyour respostas. Procure Olá seguintes dados:

* Dados **relevantes** toohello pergunta. Temos medidas de destino hello e recursos que estão relacionadas toohello destino?
* Dados que é um **medida precisa** dos nossos recursos de destino e hello do modelo de interesse.

Não é incomum, por exemplo, o toofind que sistemas existentes necessário toocollect e tipos adicionais de tooaddress de dados de log Olá problema e alcançar as metas do projeto hello. Nesse caso, você pode desejar toolook para fontes de dados externas ou atualizar os dados de novo toocollect sistemas.

### <a name="artifacts"></a>Artefatos
Aqui estão os resultados de saudação neste estágio:

* [**Compromisso de documento**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): um modelo padrão é fornecido no hello definição de estrutura de projeto TDSP. Este é um documento dinâmico que é atualizado em todo o projeto de saudação conforme como de negócios mudanças nos requisitos e novas descobertas feitas. chave de saudação é tooiterate após neste documento, adicionando mais detalhadamente, conforme você avança em processo de descoberta de saudação. Manter Olá cliente e outros participantes envolvidos em alterações de saudação e comunicam claramente motivos Olá Olá alterações toothem.  
* [**Fontes de dados**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources): isso é hello **fontes de dados brutos** seção Olá **definições de dados** relatório foi encontrado no projeto do hello TDSP **relatório de dados**  pasta. Ele especifica hello original e locais de destino para dados brutos de saudação. Em etapas posteriores, preencha detalhes adicionais, como scripts toomove Olá dados tooyour ambiente analítico.  
* [**Os dicionários de dados**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries): este documento fornece descrições de dados de saudação que são fornecidos pelo cliente hello. Essas descrições incluem informações sobre o esquema de saudação (tipos de dados, informações sobre regras de validação, se houver) e Olá diagramas de relação de entidade, se disponível.


## <a name="2-data-acquisition-and-understanding"></a>2. Compreensão e aquisição de dados

### <a name="goals"></a>Metas
* Um limpo de alta qualidade conjunto de dados variáveis de destino de toohello cujas relações são entendidas estão localizados no ambiente de análise apropriado hello, toomodel pronto.
* Uma arquitetura de solução de saudação dados pipeline toorefresh e pontuação dados regularmente foi desenvolvidos.

### <a name="how-toodo-it"></a>Como toodo-lo
Há três tarefas principais abordadas neste estágio:

* **Ingestão de dados saudação** para ambiente de análise de destino hello.
* **Explorar dados saudação** toodetermine se Olá qualidade dos dados é pergunta de saudação tooanswer adequado. 
* **Configurar um pipeline de dados** tooscore new ou regularmente dados atualizados.

#### <a name="21-ingest-hello-data"></a>2.1 ingestão dados saudação
Configure Olá processo toomove Olá dados de locais de origem toohello locais de destino em que as operações de análise como treinamento e previsões são toobe executado. Para detalhes técnicos e opções como toodo com vários serviços de dados do Azure, consulte [carregar dados em ambientes de armazenamento para análise](machine-learning-data-science-ingest-data.md). 

#### <a name="22-explore-hello-data"></a>2.2 explorar dados saudação
Antes de treinar os modelos, você precisa toodevelop um conhecimento detalhado de dados de saudação. Em geral, conjuntos de dados do mundo real apresentam ruído, são valores ausentes ou têm uma série de outras discrepâncias. Visualização e o resumo de dados podem ser usado tooaudit Olá qualidade de seus dados e fornecer informações Olá necessário tooprocess Olá dados antes que ele esteja pronto para modelagem. Esse processo costuma ser iterativo.

TDSP fornece um utilitário automatizado chamado [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) toohelp visualizar dados hello e preparar relatórios de resumo de dados. É recomendável começar com IDEAR primeiro tooexplore Olá dados toohelp desenvolver Noções básicas sobre os dados iniciais interativamente com nenhuma codificação e, em seguida, escrever código personalizado para exploração de dados e visualização. Para obter diretrizes sobre a limpeza de dados hello, consulte [tarefas tooprepare dados para o aprendizado de máquina avançada](machine-learning-data-science-prepare-data.md).  

Quando estiver satisfeito com qualidade Olá dos dados Olá limpo, Olá próxima etapa é toobetter compreender os padrões de saudação inerentes dados Olá ajudarão-lo a escolherem e desenvolvem um modelo de previsão apropriado para o seu destino. Procure as evidências para como dados saudação conectado são toohello destino e se há suficiente toomove de dados para a frente com etapas modelagem hello. Novamente, esse processo costuma ser iterativo. Talvez seja necessário toofind novas fontes de dados com mais precisos ou mais relevante dados tooaugment Olá dataset inicialmente identificado na etapa anterior hello.  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 Configuração de um pipeline de dados
Além de inclusão de toohello inicial e a limpeza de Olá dados, normalmente é necessário tooset um processar tooscore novos dados ou saudação de atualização de dados regularmente como parte de um processo de aprendizado contínuo. Faça isso configurando um pipeline de dados ou um fluxo de trabalho. Aqui está uma [exemplo](machine-learning-data-science-move-sql-azure-adf.md) de como tooset a um pipeline com [do Azure Data Factory](https://azure.microsoft.com/services/data-factory/). 

Uma arquitetura de solução do pipeline de dados Olá é desenvolvida neste estágio. pipeline de saudação também é desenvolvida em paralelo com hello estágios de projeto de ciência de dados Olá a seguir. pipeline de saudação pode ser baseado em lote ou streaming/real-tempo ou híbridos dependendo de sua empresa precisam e Olá restrições dos seus sistemas em que esta solução está sendo integrada. 

### <a name="artifacts"></a>Artefatos
Olá seguem Olá produtos neste estágio.

* [**Relatório de qualidade de dados**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md): este relatório contém resumos de dados, relações entre cada atributo e o destino, a variável de classificação Olá etc. [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) ferramenta fornecida como parte do TDSP pode gerar rapidamente Este relatório em qualquer conjunto de dados tabular como um arquivo CSV ou de uma tabela relacional. 
* **Arquitetura da solução**: isso pode ser um diagrama ou a descrição do previsões sobre os novos dados ou dados pipeline usado toorun pontuação depois de você ter criado um modelo. Ele também contém Olá pipeline tooretrain seu modelo com base em dados novos. Olá documento é armazenado no hello [projeto](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project) diretório ao usar o modelo de estrutura de diretório Olá TDSP.
* **Decisão de ponto de verificação**: antes de começar a construção de modelo e de engenharia de recurso completo, você pode reavaliar Olá projeto toodetermine se valor Olá esperado é suficiente toocontinue pursing-lo. Você pode, por exemplo, ser tooproceed pronto, necessidade toocollect mais dados ou abandonar projeto hello como dados saudação não existem tooanswer pergunta de saudação.


## <a name="3-modeling"></a>3. Modelagem

### <a name="goals"></a>Metas
* Recursos de dados ideal para o modelo de aprendizado de máquina hello.
* Um modelo ML informativo que prevê o destino de saudação com mais precisão.
* Um modelo de ML adequado para a produção.

### <a name="how-toodo-it"></a>Como toodo-lo
Há três tarefas principais abordadas neste estágio:

* **Recurso engenharia**: criar recursos de dados de treinamento do modelo de toofacilitate Olá dados brutos.
* **Treinamento de modelo**: localizar modelo Olá pergunta Olá respostas com mais precisão comparando suas métricas de sucesso.
* Determine se o modelo é **adequado para produção**.

#### <a name="31-feature-engineering"></a>3.1 Engenharia de recursos
Recurso engenharia envolve a inclusão, agregação e transformação de variáveis bruto toocreate Olá recursos usados na análise de saudação. Se você quiser informações sobre o que está gerando um modelo, em seguida, você precisa toounderstand como os recursos estão relacionada tooeach outros e como algoritmos de aprendizagem de máquina Olá estão toouse esses recursos. Esta etapa requer uma combinação creative insights obtido na etapa de exploração de dados hello e domínio. Esse é um equilíbrio entre encontrar e incluir variáveis informativas, evitando o excesso de variáveis não relacionadas. Variáveis informativos melhorar nossos resultados; variáveis não relacionados introduzem ruído desnecessário no modelo de saudação. Você também precisará toogenerate esses recursos para novos dados obtidos durante a pontuação. Portanto geração Olá desses recursos pode depender apenas dados que estão disponíveis no tempo de saudação de pontuação. Para orientação técnica de engenharia de recurso ao usar várias tecnologias de dados do Azure, consulte [engenharia no hello processo de ciência de dados de recurso](machine-learning-data-science-create-features.md). 

#### <a name="32-model-training"></a>3.2 Treinamento do modelo
Dependendo do tipo da pergunta que você está tentando responder, há vários algoritmos de modelagem disponíveis. Para obter orientação sobre como escolher algoritmos hello, consulte [como toochoose algoritmos de aprendizado de máquina do Microsoft Azure](machine-learning-algorithm-choice.md). Embora este artigo foi escrito para o aprendizado de máquina do Azure, Olá orientação é útil para qualquer projetos de aprendizado de máquina. 

processo de saudação para treinamento de modelo inclui Olá etapas a seguir: 

* **Dados de entrada hello divisão** aleatoriamente para modelagem em um conjunto de dados de treinamento e um conjunto de dados de teste.
* **Criar modelos de saudação** usando o conjunto de dados de treinamento hello.
* **Avaliar** (conjunto de dados treinamento e teste) uma série de concorrente algoritmos aprendizado de máquina com hello vários ajustes parâmetros associados (conhecidos como varredura de parâmetro) que são direcionados a responder a pergunta de saudação de interesse com hello dados atuais.
* **Determinar a solução "recomendada" hello** tooanswer pergunta de saudação comparando a métrica de sucesso de saudação entre métodos alternativos.

> [!NOTE]
> **Evitar o vazamento**: vazamento de dados pode ser causado pela inclusão de saudação de dados do conjunto de treinamento Olá externa que permite que um modelo ou o algoritmo de aprendizado de máquina previsões inacreditavelmente bom toomake de. Vazamento é um motivo comum por cientistas de dados ficam preocupar quando recebem resultados de previsão que parecem muito bom toobe true. Essas dependências podem ser toodetect de disco rígido. vazamento de tooavoid geralmente requer a iteração entre criando um conjunto de dados de análise, criando um modelo e avaliar a precisão de saudação. 
> 
> 

Fornecemos um [ferramenta automatizada de modelagem e relatório](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) com TDSP, que é capaz de toorun por meio de vários algoritmos e parâmetro varre tooproduce um modelo de linha de base. Ela também produz um relatório de modelagem de linha de base, que fornece um resumo do desempenho de cada combinação de modelo e parâmetro, incluindo a importância da variável. Esse processo também é iterativo, pois pode gerar mais engenharia de recursos. 

### <a name="artifacts"></a>Artefatos
artefatos de saudação produzidos neste estágio incluem:

* [**Conjuntos de recursos**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): Olá recursos desenvolvidos para modelagem de saudação são descritos Olá **conjuntos de recursos** seção Olá **definição de dados** relatório. Ele contém recursos de saudação ponteiros toohello código toogenerate e a descrição como o recurso de saudação foi gerado.
* [**Relatório de Modelo**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): para cada modelo testado, é produzido um relatório padrão baseado em modelo que fornece detalhes sobre cada experimento.
* **Decisão de ponto de verificação**: avaliar se o modelo hello está sendo executado também suficiente toodeploy-tooa sistema de produção. Tooask algumas perguntas mais importantes são:
  * Pergunta com Olá Olá modelo resposta com confiança suficiente recebe dados de teste Olá? 
  * Experimente abordagens alternativas: coletar dados adicionais, realizar mais engenharia de recursos ou fazer experimentos com outros algoritmos?


## <a name="4-deployment"></a>4. Implantação

### <a name="goal"></a>Objetivo
* Os modelos com um pipeline de dados são implantados tooa produção ou ambiente de produção para aceitação do usuário final. 

### <a name="how-toodo-it"></a>Como toodo-lo
tarefa principal de saudação abordada neste estágio:

* **Utilizar o modelo de saudação**: implantar a produção de hello modelo e pipeline tooa ou ambiente de produção para consumo do aplicativo.

#### <a name="41-operationalize-a-model"></a>4.1 Operacionalizar um modelo
Depois que você tiver um conjunto de modelos que funcionam bem, eles podem ser operacionalizados para outros aplicativos tooconsume. Dependendo dos requisitos de negócios hello, as previsões são feitas em tempo real ou em uma base de lote. toobe operacionalizada, os modelos de saudação têm toobe exposto com uma interface de API aberta que seja consumida facilmente a partir de vários aplicativos, como sites online, planilhas, painéis de controle ou de linha de aplicativos de negócios e de back-end. Para obter exemplos de operacionalização de modelos com um serviço Web do Azure Machine Learning, consulte [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md). Também é uma telemetria de toobuild de prática recomendada e monitoramento em modelo de produção de hello e Olá dados pipeline implantado toohelp com o status do sistema subsequentes reporting e solução de problemas.  

### <a name="artifacts"></a>Artefatos
* Painel de status de principais métricas e integridade do sistema.
* Relatório de modelagem final com detalhes da implantação.
* Documento da arquitetura da solução final.

## <a name="5-customer-acceptance"></a>5. Aceitação do cliente

### <a name="goal"></a>Objetivo
* **Finalizar os resultados do projeto Olá**: Confirme se o pipeline hello, Olá modelo e sua implantação em um ambiente de produção são os objetivos do cliente satisfatório.

### <a name="how-toodo-it"></a>Como toodo-lo
Há duas tarefas principais abordadas neste estágio:

* **Validação do sistema**: Confirmar modelo Olá implantado e pipeline estão atendendo às necessidades de clientes.
* **Início do projeto**: toohello entidade que é toorun saudação do sistema em produção.

Prezado cliente deve validar que o sistema Olá atende às suas necessidades de negócios e respostas Olá Olá perguntas com precisão aceitável toodeploy Olá sistema tooproduction para uso pelo aplicativo cliente. Toda a documentação Olá é finalizada e analisada. Um logoff da entidade de toohello de projeto de saudação responsável pelas operações está concluída. Esta entidade poderia ser, por exemplo, uma TI ou equipe de ciência de dados do cliente ou um agente de cliente de saudação que é responsável pela execução de sistema Olá em produção. 

### <a name="artifacts"></a>Artefatos
artefato principal de saudação produzido neste estágio final é hello **saída do projeto de relatório para o cliente**. Isso é Olá relatório técnico que contém todos os detalhes do projeto de saudação que toolearn úteis sobre e operar o sistema hello. Um modelo [Sair do Relatório](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) é fornecido pelo TDSP, que pode ser usado no estado em que se encontra ou personalizado, para as necessidades específicas do cliente. 

## <a name="summary"></a>Resumo
Olá [ciclo de vida do processo de ciência de dados de equipe](http://aka.ms/datascienceprocess) é modelada como uma sequência de etapas repetidas que fornecem orientação sobre tarefas de saudação necessário toouse modelos de previsão. Esses modelos podem ser implantados em uma produção ambiente toobe aproveitada toobuild inteligente aplicativos. meta de saudação desse ciclo de vida do processo é toocontinue toomove um projeto de ciência de dados para a frente até um ponto de extremidade do contrato limpar. Embora seja verdade que ciência de dados é um exercício de pesquisa e a descoberta, sendo tooclearly capaz de se comunicar equipe de tooyour essas tarefas e seus clientes usando um conjunto bem definido de artefatos modelos padronizados de funcionários podem ajudar a evitar o erro e aumentar as chances de saudação de uma execução bem-sucedida de um projeto de ciência de dados complexos.

## <a name="next-steps"></a>Próximas etapas
Completo orientações de ponta a ponta que demonstram todas as etapas de saudação no processo de saudação para **cenários específicos** também são fornecidos. Elas são listadas e vinculadas com descrições em miniatura no hello [explicações passo a passo do processo de ciência de dados de equipe](data-science-process-walkthroughs.md) tópico.

