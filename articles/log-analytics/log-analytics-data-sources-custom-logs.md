---
title: "aaaCollect personalizado registra na análise de logs do OMS | Microsoft Docs"
description: "O Log Analytics pode coletar eventos de arquivos de texto em computadores com Windows e Linux.  Este artigo descreve como toodefine um novo log personalizado e detalhes de registros de saudação criado no repositório do OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a>Logs personalizados no Log Analytics
fonte de dados de Logs personalizados Olá na análise de Log permite que você toocollect eventos dos arquivos de texto em computadores Windows e Linux. Muitos aplicativos log arquivos tootext de informações em vez de serviços padrão do log como Syslog ou de log de eventos do Windows.  Depois de coletar, você pode analisar cada registro em log Olá nos campos tooindividual usando Olá [campos personalizados](log-analytics-custom-fields.md) recurso de análise de Log.

![Coleta de log personalizado](media/log-analytics-data-sources-custom-logs/overview.png)

Olá toobe de arquivos de log coletado deve corresponder Olá critérios a seguir.

- log de saudação deve ter uma única entrada por linha ou usar um carimbo de hora correspondência Olá seguinte formatos no início de saudação de cada entrada.

    AAAA-MM-DD HH:MM:SS <br>M/D/AAAA HH:MM:SS AM/PM <br>Mês DD,AAAA HH:MM:SS

- arquivo de log de saudação não deve permitir atualizações circulares onde o arquivo hello é substituído por novas entradas.
- o arquivo de log Olá deve usar a codificação ASCII ou UTF-8.  Não há suporte para outros formatos, como UTF-16.

>[!NOTE]
>Se houver entradas duplicadas no arquivo de log hello, análise de Log coletará-los.  No entanto, os resultados da pesquisa Olá será inconsistente onde resultados do filtro Olá mostram mais eventos do que a contagem de resultados de saudação.  É importante validar Olá log toodetermine se o aplicativo hello que cria está causando o problema e abordá-lo se possível, antes de criar a definição de coleção de log personalizado hello.  
>
  
## <a name="defining-a-custom-log"></a>Definindo um log personalizado
Use Olá seguindo o procedimento toodefine um arquivo de log personalizado.  Rolagem toohello final deste artigo para obter uma explicação de um exemplo de adição de um log personalizado.

### <a name="step-1-open-hello-custom-log-wizard"></a>Etapa 1. Abrir Olá Assistente de Log personalizado
Olá assistente personalizado do Log é executado no portal do OMS hello e permite que você toodefine um novo toocollect de log personalizado.

1. No portal do OMS hello, vá muito**configurações**.
2. Clique em **Dados** e em **Custom logs**.
3. Por padrão, todas as alterações de configuração são enviadas automaticamente tooall agentes.  Para agentes do Linux, um arquivo de configuração é enviado toohello Fluentd de Coletores de dados.  Se você quiser toomodify esse arquivo manualmente em cada agente do Linux, em seguida, desmarque a caixa de saudação *aplicar abaixo máquinas de Linux toomy configuração*.
4. Clique em **adicionar +** tooopen Olá Assistente de Log personalizado.

### <a name="step-2-upload-and-parse-a-sample-log"></a>Etapa 2. Carregar e analisar um log de exemplo
Iniciar carregando um exemplo de log personalizado hello.  Assistente de saudação analisar e exibir entradas de saudação nesse arquivo para você toovalidate.  Análise de log usará o delimitador de saudação que você especifique tooidentify cada registro.

**Nova linha** é o delimitador padrão de saudação e é usado para arquivos de log que têm uma única entrada por linha.  Se a linha hello começa com uma data e hora em um dos formatos disponíveis hello, então você pode especificar um **Timestamp** delimitador que dá suporte a entradas que se estendem por mais de uma linha.

Se um delimitador de carimbo de hora é usado, então a propriedade TimeGenerated de saudação de cada registro armazenado no OMS será preenchida com hello especificada para a entrada no arquivo de log de saudação de data/hora.  Se um novo delimitador de linha for usado, TimeGenerated é preenchida com a data e hora em que a análise de Log coletados entrada hello.

> [!NOTE]
> Análise de log atualmente trata Olá coletada de um log usando um delimitador de carimbo de hora como UTC de data/hora.  Esse será o fuso horário Olá toouse alterados no agente de saudação em breve.
>
>

1. Clique em **procurar** e procurar o arquivo de exemplo tooa.  Observe que esse botão pode ser rotulado como **Escolher Arquivo** em alguns navegadores.
2. Clique em **Avançar**.
3. Olá Assistente de Log personalizado carregará Olá arquivo lista Olá registros e que ela identifica.
4. Alterar delimitador de saudação que é usado tooidentify um novo registro e o delimitador de saudação select que melhor identifica registros Olá no arquivo de log.
5. Clique em **Avançar**.

### <a name="step-3-add-log-collection-paths"></a>Etapa 3. Adicionar caminhos de coleta de log
Você deve definir um ou mais caminhos no agente Olá onde ele possa localizar o log personalizado hello.  Você pode fornecer um caminho específico e um nome para o arquivo de log hello, ou você pode especificar um caminho com um caractere curinga para o nome da saudação.  Isso dá suporte a aplicativos que criam um novo arquivo por dia ou quando um arquivo atinge um determinado tamanho.  Você também pode fornecer vários caminhos para um único arquivo de log.

Por exemplo, um aplicativo pode criar um arquivo de log diariamente com data de saudação incluída no nome hello como log20100316.txt. Um padrão de tais logs pode ser *log\*. txt* que seria aplicar o arquivo de log de tooany após o aplicativo hello do esquema de nomenclatura.

Olá tabela a seguir fornece exemplos de padrões válidos toospecify diferentes arquivos de log.

| Descrição | Caminho |
|:--- |:--- |
| Todos os arquivos em *C:\Logs* com extensão .txt no agente do Windows |C:\Logs\\\*.txt |
| Todos os arquivos em *C:\Logs* cujo nome começa com log e uma extensão .txt no agente do Windows |C:\Logs\log\*.txt |
| Todos os arquivos em */var/log/audit* com extensão .txt no agente do Linux |/var/log/audit/*.txt |
| Todos os arquivos em */var/log/audit* cujo nome começa com log e uma extensão .txt no agente do Linux |/var/log/audit/log\*.txt |

1. Selecione toospecify Windows ou Linux, qual formato de caminho que você está adicionando.
2. Digite o caminho de saudação e clique em Olá  **+**  botão.
3. Repita o processo de Olá para todos os caminhos adicionais.

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a>Etapa 4. Forneça um nome e uma descrição para o log de saudação
Olá nome que você especificar será usado para o tipo de log Olá conforme descrito acima.  Sempre terminará com _CL toodistinguish-lo como um log personalizado.

1. Digite um nome para o log de saudação.  Olá  **\_CL** sufixo é fornecido automaticamente.
2. Adicione uma **Descrição**opcional.
3. Clique em **próximo** toosave definição de log personalizado de saudação.

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a>Etapa 5. Validar que estão sendo coletados logs personalizados Olá
Pode levar até horas tooan para dados de saudação inicial de um novo tooappear de log personalizado na análise de Log.  Ele começará a coletar entradas do hello logs encontrado no caminho de saudação especificado do ponto de saudação que você Olá definido log personalizado.  Não manterá entradas Olá carregado durante a criação de log personalizado hello, mas ele irá coletar entradas já existentes nos arquivos de log de saudação que ele localiza.

Depois que a análise de Log inicia a coleta de log personalizado Olá, seus registros estará disponíveis com uma pesquisa de Log.  Use o nome de saudação que você deu a log personalizado hello como Olá **tipo** em sua consulta.

> [!NOTE]
> Se Olá RawData propriedade está ausente da pesquisa hello, poderá precisar tooclose e reabra o navegador.
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a>Etapa 6. Analisar as entradas de log personalizado Olá
entrada de log inteiro Hello será armazenada em uma única propriedade chamada **RawData**.  Você provavelmente desejarão tooseparate Olá diferentes partes de informações em cada entrada em propriedades individuais armazenados no registro de saudação.  Fazer isso usando Olá [campos personalizados](log-analytics-custom-fields.md) recurso de análise de Log.

Etapas detalhadas para analisar a entrada de log personalizada da saudação não são fornecidas aqui.  Consulte toohello [campos personalizados](log-analytics-custom-fields.md) documentação para obter essas informações.

## <a name="disabling-a-custom-log"></a>Desabilitar um log personalizado
Você não pode remover uma definição de log personalizado depois de ele ter sido criado, mas pode desabilitá-lo, removendo todos os seus caminhos de coleção.

1. No portal do OMS hello, vá muito**configurações**.
2. Clique em **Dados** e em **Custom logs**.
3. Clique em **detalhes** toodisable de definição de log personalizado toohello Avançar.
4. Remova cada um dos caminhos de coleção Olá para definição de log personalizado hello.

## <a name="data-collection"></a>Coleta de dados
O Log Analytics coletará novas entradas de cada log personalizado aproximadamente a cada cinco minutos.  agente Olá registra seu lugar em cada arquivo de log que ele coleta do.  Se agente Olá ficar offline por um período de tempo, em seguida, análise de Log coletará entradas de onde parou, mesmo se as entradas foram criadas quando Olá agent estava offline.

todo o conteúdo da entrada de log Olá Olá é gravado tooa única propriedade chamada **RawData**.  Você pode analisar isso em várias propriedades que podem ser analisadas e pesquisadas separadamente definindo [campos personalizados](log-analytics-custom-fields.md) depois de ter criado o log personalizado hello.

## <a name="custom-log-record-properties"></a>Propriedades de registro do log personalizado
Registros de log personalizado tem um tipo com o nome do log de saudação que fornecem e Olá propriedades Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| TimeGenerated |Data e hora em que Olá registro foram coletados pela análise de Log.  Se o log de saudação usa um delimitador de tempo, em seguida, isso é hora de Olá coletada de entrada hello. |
| SourceSystem |Tipo de registro de saudação do agente foi coletado do. <br> OpsManager – agente do Windows, conexão direta ou System Center Operations Manager <br> Linux: todos os agentes do Linux |
| RawData |Texto completo da saudação coletados de entrada. |
| ManagementGroupName |Nome do grupo de gerenciamento de saudação para agentes de gerenciamento do System Center Operations.  Para outros agentes, ele é AOI-\<ID do espaço de trabalho\> |

## <a name="log-searches-with-custom-log-records"></a>Pesquisas de log com registros de log personalizados
Registros de logs personalizados são armazenados no repositório do OMS hello como registros de qualquer outra fonte de dados.  Eles terão um tipo correspondente Olá nome que você fornecer ao definir log hello, então você pode usar a propriedade de tipo de saudação em seus registros de tooretrieve pesquisa coletados de um log específico.

Olá, tabela a seguir fornece exemplos de diferentes de pesquisas de log que recuperam registros de logs personalizados.

| Consultar | Descrição |
|:--- |:--- |
| Type=MyApp_CL |Todos os eventos de um log personalizado chamado MyApp_CL. |
| Type=MyApp_CL Severity_CF=error |Todos os eventos de um log personalizado chamado MyApp_CL com um valor de *erro* em um campo personalizado chamado *Severity_CF*. |

>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), e em seguida, Olá acima consultas alteraria toohello a seguir.

> | Consultar | Descrição |
|:--- |:--- |
| MyApp_CL |Todos os eventos de um log personalizado chamado MyApp_CL. |
| MyApp_CL &#124; where Severity_CF=="error" |Todos os eventos de um log personalizado chamado MyApp_CL com um valor de *erro* em um campo personalizado chamado *Severity_CF*. |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>Passo a passo do exemplo de adição de um log personalizado
Olá seção a seguir apresenta um exemplo de como criar um log personalizado.  log de exemplo Hello sendo coletado tem uma única entrada em cada linha iniciando com uma data e hora e, em seguida, delimitada por vírgulas campos para código, o status e a mensagem.  Várias entradas de exemplo são mostradas abaixo.

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a>Carregar e analisar um log de exemplo
Podemos fornecer uma saudação arquivos de log e pode ver eventos de saudação que irá coletar.  Nesse caso, Nova Linha é um delimitador suficiente.  Se uma única entrada no log de saudação pode abranger várias linhas no entanto, um delimitador de carimbo de hora precisaria toobe usado.

![Carregar e analisar um log de exemplo](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>Adicionar caminhos de coleta de log
arquivos de log Olá estarão localizados em *C:\MyApp\Logs*.  Um novo arquivo será criado por dia com um nome que inclui a data de saudação padrão Olá *appYYYYMMDD.log*.  Um padrão suficiente para esse log seria *C:\MyApp\Logs\\\\*.log*.

![Caminho da coleta do log](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a>Forneça um nome e uma descrição para o log de saudação
Usamos um nome de *MyApp_CL* e digitamos uma **Descrição**.

![Nome do log](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a>Validar que estão sendo coletados logs personalizados Olá
Usamos uma consulta de *tipo = MyApp_CL* tooreturn todos os registros de log coletados hello.

![Consulta de log sem campos personalizados](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a>Analisar as entradas de log personalizado Olá
Saudação de toodefine campos personalizados, usamos *EventTime*, *código*, *Status*, e *mensagem* campos e pode ver a diferença de saudação em Olá registros que são retornados pela consulta hello.

![Consulta de log com campos personalizados](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>Próximas etapas
* Use [campos personalizados](log-analytics-custom-fields.md) entradas de saudação de tooparse no log de personalizado Olá tooindividual campos.
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.
