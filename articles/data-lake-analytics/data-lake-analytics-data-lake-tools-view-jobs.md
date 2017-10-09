---
title: "aaaUse navegador de trabalho e o modo de trabalho para trabalhos de análise do Azure Data Lake | Microsoft Docs"
description: "Saiba como toouse navegador de trabalho e o modo de trabalho para trabalhos de análise do Azure Data Lake. "
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>Usar o Navegador de Trabalhos e a Exibição de Trabalho para trabalhos do Azure Data Lake Analytics
arquivos do serviço de análise do Azure Data Lake Hello enviada trabalhos em uma [repositório de consultas](#query-store). Neste artigo, você aprenderá como toouse navegador de trabalho e modo de trabalho no Azure Data Lake Tools para saudação de toofind do Visual Studio histórica de trabalho informações. 

Por padrão, Olá serviço de análise Data Lake arquiva trabalhos Olá por 30 dias. período de validade da saudação pode ser configurado no hello portal do Azure ao configurar a política de expiração de saudação personalizada. Você não será capaz de tooaccess informações de trabalho Olá após a expiração. 

## <a name="prerequisites"></a>Pré-requisitos
Veja [Pré-requisitos das Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md#prerequisites).

## <a name="open-hello-job-browser"></a>Olá abrir o navegador de trabalho
Acesso Olá navegador de trabalho por meio de **Gerenciador de servidores > Azure > análise Data Lake > trabalhos** no Visual Studio.  Usando Olá navegador de trabalho, você pode acessar o repositório de consultas de saudação de uma conta da análise Data Lake. Navegador de trabalho exibe o repositório de consultas no saudação à esquerda, mostrando as informações de trabalho básico e trabalho exibição mostrando direita Olá informações detalhadas do trabalho.

## <a name="job-view"></a>Exibição de Trabalho
Exibição do trabalho mostra Olá informações detalhadas de um trabalho. tooopen um trabalho, clique duas vezes em um trabalho em Olá trabalho navegador ou abri-lo no menu do Data Lake Olá clicando em Exibir trabalho. Você deve ver uma caixa de diálogo preenchida com hello trabalho URL.

![Navegador de Trabalhos das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

A Exibição de Trabalho contém:

* Resumo do trabalho
  
    Atualizar Olá exibição trabalho toosee Olá informações mais recentes de trabalhos em execução.
  
  * Status do Trabalho (gráfico):
    
      Status do trabalho descreve fases de trabalho hello:
    
      ![Status das fases do trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * Preparação: Carregar sua nuvem toohello script, compilação e otimização script hello usando o serviço de compilação de saudação.
    * Em fila: Trabalhos estão ocorre em fila que estão aguardando recursos suficientes, ou trabalhos Olá excederem trabalhos simultâneos max de saudação por limitação de conta. configuração de prioridade de saudação determina a sequência de saudação de trabalhos em fila - Olá Olá menor, Olá Olá prioridade.
    * Está em execução: trabalho hello está realmente em execução em sua conta da análise Data Lake.
    * Finalizando: trabalho hello está sendo concluída (por exemplo, finalizando arquivo hello).
      
      trabalho Olá pode falhar em cada fase. Por exemplo, erros de compilação na fase de preparação de hello, erros de tempo limite na fase de enfileirado hello e erros de execução na fase de execução hello, etc.
  * Informações Básicas
    
      mostram informações de trabalho básico de saudação na parte inferior de saudação do painel de resumo do trabalho de saudação.
    
      ![Status das fases do trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * Resultado do Trabalho: êxito ou falha. trabalho de saudação pode falhar em cada fase.
    * Duração Total: a hora do relógio (duração) entre a hora do envio e a hora de término.
    * Tempo total de computação: soma de saudação cada vértice de tempo de execução, você pode considerar como Olá tempo trabalho Olá for executado em apenas um vértice. Consulte tooTotal vértices toofind obter mais informações sobre o vértice.
    * Enviar/início/término: tempo de saudação quando Olá serviço de análise Data Lake recebe saudação do trabalho envio/inicia toorun trabalho/termina trabalho Olá com êxito ou não.
    * Na fila/compilação/execução: Tempo do relógio gasto durante a fase de na fila/preparação/execução hello.
    * : Olá análise Data Lake conta usada para executar o trabalho de saudação.
    * Autor: usuário de saudação que enviou o trabalho Olá, pode ser uma conta do sistema ou conta da pessoa real.
    * Prioridade: Olá prioridade trabalho hello. Olá Olá número menor, Olá Olá prioridade. Ela afeta apenas a sequência de saudação de trabalhos de saudação na fila de saudação. Definir uma prioridade mais alta não impede trabalhos em execução.
    * Paralelismo: Olá solicitou o número máximo de simultâneas Azure Lake análise de unidades de dados (ADLAUs), também conhecido como vértices. No momento, um vértice é igual tooone VM com dois núcleos virtuais e seis GB de RAM, embora isso pôde ser atualizado no futuro de análise Data Lake atualizações.
    * Bytes restantes: Bytes que precisam toobe processada até Olá trabalho for concluído.
    * Bytes lidos/gravados: Bytes que foram lidos/gravados desde Olá trabalho começou a ser executado.
    * Total de vértices: trabalho Olá é dividido em várias partes do trabalho, cada trabalho é chamado de um vértice. Esse valor descreve consiste em quantos trabalho saudação de trabalhos. Você pode considerar um vértice como uma unidade de processo básico, também conhecido como ADLAU (Unidade do Azure Data Lake Analytics), sendo que vértices podem ser executados em paralelismo. 
    * Concluído/execução/falha: Olá contagem dos vértices concluída/execução/falha. Vértices podem falhar devido a falhas de sistema e de código de usuário tooboth, mas novas tentativas de sistema Olá falhou vértices automaticamente algumas vezes. Se o vértice Olá ainda falhou após tentar novamente, trabalho inteiro Olá irá falhar.
* Gráfico do Trabalho
  
    Um script U-SQL representa a lógica de saudação de transformação de dados de entrada toooutput dados. script Hello é compilada e otimizada tooa plano de execução física na fase de preparação de saudação. Gráfico de trabalho é plano de execução física Olá tooshow.  Olá diagrama a seguir ilustra o processo de saudação:
  
    ![Status das fases do trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    Um trabalho é dividido em várias partes de trabalho. Cada parte de trabalho é chamada de um vértice. vértices Olá são agrupados como Super vértice (também conhecido como estágio) e visualizados como gráfico de trabalho. Olá estágio verde placards no gráfico de trabalho Olá mostram estágios hello.
  
    Cada vértice em um estágio está fazendo Olá mesmo tipo de trabalhar com partes diferentes de saudação mesmo dados. Por exemplo, se você tiver um arquivo com 1 TB de dados e houver centenas de vértices lendo tal arquivo, cada um deles estará lendo uma parte. Os vértices são agrupados em Olá mesmo estágio e fazer o mesmo trabalho em partes diferentes do mesmo arquivo de entrada.
  
  * <a name="state-information"></a>Informações do estágio
    
      Em um estágio específico, alguns números são mostrados no letreiro hello.
    
      ![Estágio no gráfico de trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 Extrair: nome de saudação do estágio, chamado por um método de operação de número e hello.
    * 84 vértices: Olá contagem total de vértices neste estágio. Figura Olá indica quantas partes do trabalho é dividido neste estágio.
    * s/vértice 12.90: Olá tempo de execução de vértice média para este estágio. Esse número é calculado pela SOMA (tempo de execução de todos os vértices) / (contagem total de vértices). Que significa que se você pode atribuir todos os vértices de saudação executados no paralelismo, estágio todo hello está concluído em 12.90 s. Isso também significa que se todos Olá trabalho neste estágio é feito em série, Olá custo seria #vertices * tempo médio.
    * 850.895 linhas gravadas: contagem total de linhas gravadas nesse estágio.
    * L/G: a quantidade de dados lidos/gravados nesse estágio, em bytes.
    * Cores: Cores forem utilizadas no status do hello estágio tooindicate vértice diferentes.
      
      * Verde indica vértice Olá é bem-sucedida.
      * Laranja indica vértice Olá é repetida. vértice Olá repetida falhou mas será repetida automaticamente e com êxito pelo sistema hello e Olá geral fase é concluída com êxito. Se vértice Olá repetida, mas ainda falha, cor Olá ativa vermelho e hello inteira falha no trabalho.
      * Vermelho indica falha, que significa que um determinado vértice tinha foi repetida algumas vezes pelo sistema hello, mas ainda falhou. Esse cenário provocará Olá todo trabalho toofail.
      * Azul significa que um determinado vértice está em execução.
      * Branco indica Olá vértice está esperando. vértice Olá pode ser toobe espera agendada depois que um ADLAU se torna disponível, ou ele pode estar esperando por entrada como seus dados de entrada talvez não esteja prontos.
      
      Você pode encontrar mais detalhes para o estágio de saudação passando o cursor do mouse por um estado:
      
      ![Detalhes do gráfico de trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * Vértices: Descreve detalhes de vértices hello, por exemplo, quantos vértices no total, vértices quantas forem concluídas, são eles falharam ou ainda em execução/em espera, etc.
  * Dados lidos entre pods/dentro de um pod: arquivos e dados são armazenados em vários pods no sistema de arquivos distribuído. valor de saudação aqui descreve a quantidade de dados for lido Olá mesmo pod ou cruzada pod.
  * Total de tempo de computação: soma de saudação do tempo de execução cada vértice no estágio de hello, pode ser considerado como tempo de saudação levaria se todos eles funcionam no estágio de saudação é executado em apenas um vértice.
  * Dados e as linhas gravadas/leitura: indica quanto dados linhas foram lidos/gravados ou precisam toobe ler.
  * Falhas de leitura de vértice: descreve quantos vértices falharam durante a leitura de dados.
  * Descarta vértice duplicado: se um vértice estiver muito lento, sistema Olá pode agendar várias vértices toorun Olá mesmo trabalho. Vértices reductant serão descartadas quando um dos vértices Olá concluída com êxito. Vértice duplicado descarta o número de saudação de registros de vértices são descartados como duplicações no estágio de saudação.
  * Revogações de vértice: vértice Olá foi bem-sucedida, mas obter novamente mais tarde devido a motivos de toosome. Por exemplo, se vértice downstream perder dados de entrada intermediário, ele solicitará Olá vértice upstream toorerun.
  * Execuções de agendamento de vértice: tempo total de saudação vértices Olá tenham sido agendadas.
  * Dados de vértice média/Min/Max lidos: Olá mínimo/média/máximo de cada vértice ler dados.
  * Duração: Olá tempo do relógio que entra em um estágio, você precisa tooload perfil toosee esse valor.
  * Reprodução do Trabalho
    
      Análise data Lake executa trabalhos e arquivos Olá vértices executando informações dos trabalhos de saudação, como quando os vértices de saudação são iniciados, interrompidos, falha e como eles são repetidos, etc. Todas as informações de saudação é automaticamente registrado no repositório de consultas de saudação e armazenadas no seu perfil de trabalho. Você pode baixar Olá perfil de trabalho por meio de "Carregar perfil" na exibição trabalho e você pode exibir hello reprodução de trabalho após o download Olá perfil de trabalho.
    
      Reprodução de trabalho é uma visualização de resumo do que aconteceu em cluster hello. Ela ajuda você a assistir ao andamento da execução do trabalho e detecte visualmente os gargalos e anomalias no desempenho em um tempo muito curto (geralmente menos de 30s).
  * Exibição de Mapa de Calor do Trabalho 
    
      Mapa de calor de trabalho podem ser selecionado por meio do menu suspenso de exibição Olá no gráfico de trabalho. 
    
      ![Modo de exibição do mapa de heap do gráfico do trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      Ele mostra o mapa de calor e/s, a hora e a taxa de transferência de saudação de um trabalho, por meio do qual você pode encontrar onde trabalho Olá passa a maior parte do tempo de saudação ou se o seu trabalho é um trabalho de limite de e/s e assim por diante.
    
      ![Exemplo de mapa de heap do gráfico do trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * Progresso: Olá progresso da execução de trabalho, consulte informações [estágio informações](#stage-information).
    * Dados lidos/gravados: mapa de calor de saudação do total de dados lidos/gravados em cada estágio.
    * Tempo de computação: mapa de calor de saudação da soma (tempo de execução cada vértice), você pode considerar isso como quanto tempo levaria se todo o trabalho no estágio de saudação for executado com somente 1 vértice.
    * Tempo médio de execução por nó: mapa de calor de saudação da soma (tempo de execução cada vértice) / (número de vértice). O que significa que se você pode atribuir todos os vértices de saudação executados no paralelismo, estágio todo Olá será feito nesse intervalo.
    * Taxa de transferência de entrada/saída: mapa de calor de saudação de taxa de transferência de entrada/saída de cada estágio, você pode confirmar se o trabalho é um trabalho de e/s associado por meio.
* Operações de Metadados
  
    Você pode executar algumas operações de metadados em seu script U-SQL, como criar um banco de dados, remover uma tabela, etc. Essas operações são mostradas na Operação de Metadados após a compilação. Aqui você pode encontrar asserções, além de criar e remover entidades.
  
    ![Operações de metadados de Exibição de Trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* Histórico de Estado
  
    Olá histórico de estado também é visualizado no resumo do trabalho, mas você pode obter mais detalhes aqui. Você pode encontrar hello detalhada informações como quando o trabalho hello está preparado, enfileiradas, foi iniciada, encerrada. Também, você pode encontrar quantas vezes trabalho Olá foi compilado (Olá CcsAttempts: 1), quando é cluster do hello trabalho toohello despachada realmente (Olá detalhes: expedir toocluster de trabalho), etc.
  
    ![Histórico de Estado de Exibição de Trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* Diagnostics
  
    ferramenta Olá diagnostica automaticamente a execução do trabalho. Você receberá alertas quando houver algum erro ou problemas de desempenho em seus trabalhos. Observe que você precisa toodownload perfil tooget informações completas aqui. 
  
    ![Diagnóstico da Exibição de Trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * Avisos: um alerta aparece aqui com aviso do compilador. Você pode clicar em "problemas de x" link toohave mais detalhes quando Olá alerta é exibido.
  * Vértice executado por tempo demais: se qualquer vértice for executado além do tempo limite para execução (digamos, por 5 horas), haverá problemas.
  * Uso de recursos: se você tiver alocado mais paralelismo do que necessário ou paralelismo insuficiente, haverá problemas. Também é possível clique toosee de uso de recursos em mais detalhes e executar cenários hipotéticos toofind uma melhor alocação de recursos (para obter mais detalhes, consulte neste guia).
  * Verificação de memória: se qualquer um deles usar mais de 5 GB de memória, haverá problemas. Se o trabalho usar mais memória do que a limitação do sistema, o próprio sistema poderá interromper sua execução.

## <a name="job-detail"></a>Detalhes do Trabalho
Detalhes do trabalho mostra Olá informações detalhadas do trabalho hello, incluindo o Script, recursos e o modo de execução de vértice.

![Detalhes do trabalho do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* Script
  
    Olá script U-SQL de trabalho Olá é armazenado no repositório de consultas de saudação. Você pode exibir o script U-SQL original de saudação e enviá-lo novamente se necessário.
* Recursos
  
    Você pode encontrar as saídas de compilação do hello trabalho armazenadas no repositório de consultas Olá por meio de recursos. Por exemplo, você pode encontrar "algebra.xml", que é usado tooshow hello trabalho gráfico, assemblies Olá registrado, etc. aqui.
* Modo de exibição de execução de vértice
  
    Mostra detalhes de execução de vértices. Olá perfil de trabalho arquivos de log de execução cada vértice, como total dos dados lidos/gravados, tempo de execução, o estado, etc. Por meio desse modo de exibição, você pode obter mais detalhes sobre como um trabalho foi executado. Para obter mais informações, consulte [Olá Use exibição de execuções de vértice no Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).

## <a name="next-steps"></a>Próximas etapas
* toolog informações de diagnóstico, consulte [acessar logs de diagnóstico para análise do Azure Data Lake](data-lake-analytics-diagnostic-logs.md)
* toosee uma consulta mais complexa, consulte [site analisar logs usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* modo de execução de vértice toouse, consulte [Olá Use exibição de execuções de vértice no Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)

