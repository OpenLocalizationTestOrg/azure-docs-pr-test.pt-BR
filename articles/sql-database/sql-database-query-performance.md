---
title: "aaaQuery informações de desempenho para o banco de dados do SQL Azure | Microsoft Docs"
description: "Monitoramento do desempenho de consulta identifica Olá consumo da CPU a maioria das consultas para um banco de dados do SQL Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>Visão do desempenho de consulta de Banco de Dados SQL do Azure
Gerenciamento e ajuste de desempenho de saudação de bancos de dados relacionais são uma tarefa desafiadora que requer conhecimento significativo e o investimento de tempo. Análise de desempenho de consulta permite que você toospend menos tempo Solucionando problemas de desempenho de banco de dados, fornecendo a seguir hello:

* Mais informações sobre o consumo de recursos de bancos de dados (DTU). 
* principais consultas por contagem de duração/CPU/execução, que potencialmente podem ser ajustadas para melhorar o desempenho Hello.
* Olá toodrill de capacidade para baixo em detalhes de saudação de uma consulta, exibir seu texto e o histórico de utilização de recursos. 
* Anotações de ajuste de desempenho que mostram as ações executadas [Advisor do Banco de Dados SQL Azure](sql-database-advisor.md)  



## <a name="prerequisites"></a>Pré-requisitos
* A Análise de Desempenho de Consultas exige a execução do [Repositório de Consultas](https://msdn.microsoft.com/library/dn817826.aspx) em seu banco de dados. Se o repositório de consultas não está em execução, o portal Olá solicita tooturn-la no.

## <a name="permissions"></a>Permissões
a seguir Olá [controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md) permissões são necessária toouse análise de desempenho de consulta: 

* **Leitor**, **proprietário**, **Colaborador**, **Colaborador de banco de dados SQL**, ou **Colaborador do SQL Server** permissões são necessário tooview Olá maior consumo de recursos gráficos e consultas. 
* **Proprietário**, **Colaborador**, **Colaborador de banco de dados SQL**, ou **Colaborador do SQL Server** permissões são necessárias tooview texto da consulta.

## <a name="using-query-performance-insight"></a>Usando a Visão de Desempenho de Consulta
Análise de desempenho de consulta é fácil toouse:

* Abra [portal do Azure](https://portal.azure.com/) e banco de dados de localização que você deseja tooexamine. 
  * No menu do lado esquerdo, em suporte e solução de problemas, selecione "Análise de Desempenho de Consultas".
* Na guia da primeira hello, examine a lista de saudação das principais consultas de consumo de recursos.
* Selecione uma consulta individual tooview seus detalhes.
* Abra o [Advisor do Banco de Dados do SQL Azure](sql-database-advisor.md) e verifique se há alguma recomendação disponível.
* Use os controles deslizantes ou ícones toochange observado o intervalo de zoom.
  
    ![painel de desempenho](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> Algumas horas de dados precisa toobe capturado pelo repositório de consultas de análise de desempenho de consulta do banco de dados SQL tooprovide. Se o banco de dados de saudação não tem atividades ou repositório de consultas não estava ativo durante um determinado período de tempo, gráficos de saudação estará vazios ao exibir o período de tempo. Você pode habilitar o Armazenamento de Consulta a qualquer momento se ele não estiver em execução.   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>Examinar as consultas que mais consomem CPU
Em Olá [portal](http://portal.azure.com) Olá a seguir:

1. Procurar tooa banco de dados SQL e clique em **todas as configurações** > **suporte + solução de problemas** > **análise de desempenho de consulta**. 
   
    ![Análise de desempenho de consultas][1]
   
    Abre o modo de exibição do Hello principais consultas e principais consultas de consumo da CPU Olá são listadas.
2. Clique em torno do gráfico de saudação para obter detalhes.<br>Hello linha superior mostra % DTU geral do banco de dados Olá, enquanto as barras Olá mostram % de CPU consumida por consultas de saudação selecionada durante o intervalo selecionado hello (por exemplo, se **semana passada** está selecionado cada barra representa um dia).
   
    ![principais consultas][2]
   
    grade inferior de saudação representa informações agregadas para consultas de saudação visível.
   
   * ID da consulta: identificador exclusivo da consulta no banco de dados.
   * CPU por consulta durante o intervalo observável (depende da função de agregação).
   * Duração por consulta (depende da função de agregação).
   * Número total de execuções para uma consulta específica.
     
     Selecione ou desmarque tooinclude consultas individuais ou excluí-los do gráfico de saudação usando as caixas de seleção.
3. Se seus dados se torna obsoletos, clique em Olá **atualização** botão.
4. Você pode usar os controles deslizantes e intervalo de observação de toochange de botões de zoom e investigar picos: ![configurações](./media/sql-database-query-performance/zoom.png)
5. Opcionalmente, se você quiser uma exibição diferente, você pode selecionar a guia **Personalizar** e definir:
   
   * Métrica (CPU, duração, contagem de execução)
   * Intervalo de tempo (Últimas 24 horas, Última semana, Mês passado). 
   * Número de consultas.
   * Função de agregação.
     
     ![Configurações](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>Exibindo detalhes de uma consulta individual
detalhes da consulta tooview:

1. Clique em qualquer consulta na lista de saudação das principais consultas.
   
    ![detalhes](./media/sql-database-query-performance/details.png)
2. modo de exibição de detalhes de saudação é aberto e contagem de duração/consumo/execução Olá consultas de CPU é dividida ao longo do tempo.
3. Clique em torno do gráfico de saudação para obter detalhes.
   
   * Gráfico superior mostra a linha com o banco de dados DTU % geral e barras de saudação são % de CPU consumida pela consulta selecionada hello.
   * Segundo gráfico mostra a duração total pela consulta selecionada hello.
   * Gráfico de inferior mostra o número total de execuções pela consulta selecionada hello.
     
     ![detalhes da consulta][3]
4. Opcionalmente, use os controles deslizantes, botões de zoom ou clique em **configurações** toocustomize como dados de consulta são exibidos ou toopick um período de tempo diferentes.

## <a name="review-top-queries-per-duration"></a>Analise as principais consultas por duração
Na atualização recente de saudação de análise de desempenho de consulta, apresentamos duas novas métricas que podem ajudá-lo a identificar gargalos potenciais: contagem de duração e a execução.<br>

Consultas de longa execução têm potencial de maior Olá para bloquear recursos mais longo, bloqueando outros usuários e limitar a escalabilidade. Eles também são melhores candidatos Olá para otimização.<br>

tooidentify consultas de longa execução:

1. Abra a guia **Personalizar** na Análise de Desempenho de Consultas do banco de dados selecionado
2. Alterar as métricas toobe **duração**
3. Selecione o número de consultas e o intervalo de observação
4. Selecione a função de agregação
   
   * **Soma** adiciona todo o tempo de execução de consulta durante todo o intervalo de observação.
   * **Máximo** localiza consultas para as quais tempo de execução foi máximo no intervalo inteiro de observação.
   * **AVG** localiza o tempo médio de execução de todas as execuções de consulta e exibir hello superior fora essas médias. 
     
     ![duração da consulta][4]

## <a name="review-top-queries-per-execution-count"></a>Analise as principais consultas por contagem de execução
Um alto número de execuções pode não estar afetando o banco de dados propriamente dito e o uso de recursos pode ser baixo, mas o aplicativo pode ficar lento no geral.

Em alguns casos, a contagem de execução muito alto pode levar tooincrease da rede viagens de ida e volta. Viagens de ida e afetam o desempenho de forma significativa. Eles são latência de toonetwork de assunto e latência de servidor toodownstream. 

Por exemplo, muitos sites controlados por dados muito acessar banco de dados de saudação para cada solicitação de usuário. Durante a conexão pooling ajuda, hello aumentada tráfego de rede e a carga de processamento no servidor de banco de dados de saudação podem afetar desempenho.  Recomendação geral é tookeep round viagens tooan nível mínimo absoluto.

tooidentify executados com frequência as consultas de consultas ("tagarelas"):

1. Abra a guia **Personalizar** na Análise de Desempenho de Consultas do banco de dados selecionado
2. Alterar as métricas toobe **contagem de execução**
3. Selecione o número de consultas e o intervalo de observação
   
    ![contagem de execução da consulta][5]

## <a name="understanding-performance-tuning-annotations"></a>Noções básicas sobre anotações de ajuste de desempenho
Ao explorar a carga de trabalho de análise de desempenho de consulta, você poderá notar ícones com uma linha vertical na parte superior do gráfico de saudação.<br>

Esses ícones são anotações; eles representam as ações que afetam o desempenho executadas pelo [Advisor do Banco de Dados SQL Azure](sql-database-advisor.md). Ao focalização anotação, você obtém informações básicas sobre a ação de saudação:

![anotação da consulta][6]

Se você quiser tooknow mais ou aplica a recomendação do orientador, clique o ícone de saudação. O ícone abrirá os detalhes da ação. Se for uma recomendação ativa, você pode aplicar imediatamente usando o comando.

![detalhes de anotação de consulta][7]

### <a name="multiple-annotations"></a>Várias anotações.
É possível que devido ao nível de zoom, anotações são tooeach fechar outros irá obter recolhidas em uma. Isso será representado por um ícone especial, clicar nele irá abrirá uma nova folha onde a lista de anotações agrupadas será mostrada.
Correlacionando consultas e ações de ajuste de desempenho pode ajudar a toobetter a entender sua carga de trabalho. 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>Otimizando a configuração do repositório de consultas Olá para análise de desempenho de consulta
Durante o uso de análise de desempenho de consulta, você pode encontrar hello mensagens do repositório de consultas a seguir:

* "O Repositório de Consulta não está corretamente configurado neste banco de dados. Clique aqui toolearn mais."
* "O Repositório de Consulta não está corretamente configurado neste banco de dados. Clique aqui toochange configurações". 

Normalmente, essas mensagens aparecem ao repositório de consultas não é capaz de toocollect novos dados. 

O primeiro caso ocorre quando o Repositório de Consultas está em estado somente leitura e os parâmetros são definidos de forma ideal. Você pode corrigir isso, aumentando o tamanho do Repositório de Consultas ou desmarcando o Repositório de Consultas.

![botão qds][8]

O segundo caso acontece quando o Repositório de Consultas está Desligado ou parâmetros não estão definidos de forma ideal. <br>Você pode alterar Olá retenção e a captura de política e habilitar repositório de consultas, executando os comandos abaixo ou diretamente do portal:

![botão qds][9]

### <a name="recommended-retention-and-capture-policy"></a>Política recomendada de retenção e captura
Há dois tipos de política de retenção:

* Tamanho base - se conjunto tooAUTO ele limpará os dados automaticamente quando quase o tamanho máximo for atingido.
* Tempo com base - por padrão, definirá too30 dias, que significa que, se o repositório de consultas será executado sem espaço, ele excluirá consultar informações mais de 30 dias

A política de captura pode ser definida para:

* **Todas**: captura todas as consultas.
* **Automática**: consultas pouco frequentes e consultas com duração de execução e compilação insignificantes são ignoradas. Os limites da duração de contagem de execução, compilação e tempo de execução são determinados internamente. Essa é a opção de padrão de saudação.
* **Nenhuma** – o Repositório de Consultas interrompe a captura de novas consultas, porém, as estatísticas de tempo de execução para consultas já capturadas ainda são coletadas.

É recomendável definir todas as políticas tooAUTO e limpar política too30 dias:

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

Aumente o tamanho do Repositório de Consultas. Isso pode ser executada pelo banco de dados tooa conexão e emitindo a seguinte consulta:

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

Aplicar essas configurações, eventualmente, fará o repositório de consultas coleta consultas novas, no entanto, se você não quiser toowait você pode limpar o repositório de consultas. 

> [!NOTE]
> Executando consulta a seguir excluirá todas as informações atuais de saudação repositório de consultas. 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>Resumo
Análise de desempenho de consulta ajuda a entender o impacto de saudação de sua carga de trabalho de consulta e como ele se relaciona toodatabase o consumo de recursos. Com esse recurso, você saiba mais sobre Olá consultas mais desgastantes e identificar facilmente Olá aqueles toofix antes de se tornarem um problema.

## <a name="next-steps"></a>Próximas etapas
Para obter recomendações adicionais sobre como melhorar o desempenho de saudação do banco de dados SQL, clique em [recomendações](sql-database-advisor.md) em Olá **Query Performance Insight** folha.

![Performance Advisor](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

