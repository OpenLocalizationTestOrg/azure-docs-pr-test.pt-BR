---
title: "aaaFix um erro de conexão do SQL, erro transitório | Microsoft Docs"
description: "Saiba como tootroubleshoot, diagnosticar e evitar que um erro de conexão do SQL ou transitórias no banco de dados do SQL Azure. "
keywords: "conexão do sql, cadeia de conexão, problemas de conectividade, erro transitório, erro de conexão"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a>Solucionar problemas, diagnosticar e evitar erros de conexão SQL e erros transitórios para o Banco de Dados SQL
Este artigo descreve como tooprevent, solucionar problemas, diagnosticar e reduzir os erros de conexão e erros transitórios que seu aplicativo cliente encontra quando ele interage com o banco de dados do SQL Azure. Saiba como tooconfigure lógica de repetição, criar cadeia de caracteres de conexão hello e ajuste outras configurações de conexão.

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a>Erros transitórios (falhas transitórias)
Um erro transitório (também chamado de falha transitória) tem uma causa que, em breve, será resolvida. Uma causa ocasional erros transitórios é quando Olá sistema Azure rapidamente desloca balanceamento de carga de toobetter de recursos de hardware várias cargas de trabalho. A maioria desses eventos de reconfiguração normalmente é concluída em menos de 60 segundos. Durante esse período de tempo de reconfiguração, você pode ter conectividade emite tooAzure banco de dados SQL. Aplicativos que se conectam tooAzure banco de dados SQL deve ser compilado tooexpect esses erros transitórios, identificador-los com a implementação de lógica de repetição em seu código em vez de tê-los toousers como erros de aplicativo.

Se seu programa cliente estiver usando ADO.NET, seu programa é informado sobre o erro transitório Olá por throw saudação de um **SqlException**. Olá **número** propriedade pode ser comparada com a lista de saudação de erros transitórios superior de saudação do tópico Olá: [códigos de erro SQL para aplicativos de cliente do banco de dados SQL](sql-database-develop-error-messages.md).

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Conexão versus comando
Você repetir a conexão de SQL hello ou selecioná-lo novamente, dependendo do seguinte hello:

* **Um erro transitório ocorre durante uma tentativa de conexão**: conexão Olá deverá ser repetida após o atraso de alguns segundos.
* **Um erro transitório ocorre durante um comando de consulta SQL**: comando Olá não deve ser repetido imediatamente. Em vez disso, após um atraso, conexão Olá deve ser recentemente estabelecida. Comando Olá pode ser tentada novamente.

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a>Lógica de repetição para erros transitórios
Os programas cliente que ocasionalmente encontram um erro transitório são mais eficientes quando contêm lógica de repetição.

Quando seu programa se comunica com o banco de dados do SQL Azure por meio de um middleware de terceiros 3ª, consulte com o fornecedor de saudação se Olá middleware contém a lógica de repetição para erros transitórios.

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a>Princípios de repetição
* Tooopen uma tentativa de uma conexão deve ser repetida se o erro de saudação é temporário.
* Uma instrução SQL SELECT que falhe com um erro transitório não deverá ser repetida diretamente.
  
  * Em vez disso, estabelecer uma nova conexão e tente novamente Olá SELECT.
* Quando uma instrução SQL UPDATE falhará com um erro transitório, uma nova conexão deve ser estabelecida antes Olá que nova tentativa de atualização.
  
  * lógica de repetição Olá deve garantir que transação de banco de dados inteiro Olá concluída ou transação Olá inteira é revertida.

#### <a name="other-considerations-for-retry"></a>Outras considerações sobre tentativas de repetição
* Um arquivo em lotes que é iniciado automaticamente depois do horário comercial e que será concluída antes da manhã, pode ter toovery paciente com tempo intervalos de tempo entre as tentativas de repetição.
* Um programa de interface do usuário deve conta para Olá tendência humana toogive após uma espera longa demais.
  
  * No entanto, solução de saudação não deve ser tooretry em alguns segundos, porque essa política pode sobrecarregar o sistema Olá com solicitações.

#### <a name="interval-increase-between-retries"></a>Aumento do intervalo entre tentativas de repetição
É recomendável que você aguarde 5 segundos antes de sua primeira tentativa. Repetir após um intervalo menor do que 5 segundos corre o risco de serviço de nuvem Olá imenso. Para cada repetição subsequente atraso Olá deve crescer exponencialmente, tooa máximo de 60 segundos.

Uma discussão de saudação *período de bloqueio* para clientes que usam o ADO.NET está disponível em [Pooling de Conexão do SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

Você também poderá tooset um número máximo de tentativas antes de programa hello se encerra.

#### <a name="code-samples-with-retry-logic"></a>Exemplos de código com lógica de repetição
Os exemplos de código com lógica de repetição, em uma variedade de linguagens de programação, estão disponíveis em:

* [Bibliotecas de conexão para Banco de Dados SQL e SQL Server](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a>Testar sua lógica de repetição
tootest sua lógica de repetição, você deve simular ou causar um erro que pode ser corrigido enquanto seu programa ainda está em execução.

##### <a name="test-by-disconnecting-from-hello-network"></a>Teste se desconectar da rede Olá
Uma maneira que você pode testar sua lógica de repetição é toodisconnect computador cliente da saudação de rede durante execução do programa de saudação. Erro de saudação será:

* **SqlException.Number** = 11001
* Mensagem: "Este host não é conhecido"

Como parte da saudação primeiro tentativa de repetição, seu programa pode corrigir erros de ortografia hello e, em seguida, tente tooconnect.

toomake nesse prático, você desconecte o computador da rede Olá antes de iniciar o programa. Em seguida, seu programa reconhece um parâmetro de tempo de execução que faz com que o programa hello:

1. Adicione temporariamente 11001 lista tooits de erros tooconsider como transitório.
2. Tente fazer sua primeira conexão como de costume.
3. Depois que o erro Olá é capturado, remova 11001 da lista de hello.
4. Exiba uma mensagem informando Olá usuário tooplug Olá computador em rede hello.
   * Pausar a execução ainda mais usando o hello **ReadLine** método ou uma caixa de diálogo com um botão Okey. usuário Olá pressiona a tecla de Enter de saudação depois que o computador Olá conectado em rede hello.
5. Tente novamente tooconnect, esperando sucesso.

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a>Ao conectar-se de teste por nome de banco de dados de saudação do erro de ortografia
Seu programa pode propositadamente errar nome de usuário de saudação antes da primeira tentativa de conexão hello. Erro de saudação será:

* **SqlException.Number** = 18456
* Mensagem: "Falha de logon para o usuário 'WRONG_MyUserName'."

Como parte da saudação primeiro tentativa de repetição, seu programa pode corrigir erros de ortografia hello e, em seguida, tente tooconnect.

toomake nesse prático, seu programa pode reconhecer um parâmetro de tempo de execução que faz com que o programa hello:

1. Adicione temporariamente 18456 lista tooits de erros tooconsider como transitório.
2. Propositadamente Adicione nome de usuário toohello 'WRONG_'.
3. Depois que o erro Olá é capturado, remova 18456 da lista de hello.
4. Remova 'WRONG_' hello do nome do usuário.
5. Tente novamente tooconnect, esperando sucesso.

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a>Parâmetros SqlConnection .NET para repetição de conexão
Se seu programa cliente se conecta a tootooAzure banco de dados SQL usando a classe do .NET Framework Olá **SqlConnection**, você deve usar o .NET 4.6.1 ou posterior (ou .NET Core) para que você pode aproveitar o recurso de repetição de conexão. Detalhes do recurso Olá [aqui](http://go.microsoft.com/fwlink/?linkid=393996).

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


Quando você cria Olá [cadeia de caracteres de conexão](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) para sua **SqlConnection** do objeto, você deve coordenar valores hello entre Olá parâmetros a seguir:

* ConnectRetryCount &nbsp;&nbsp;*(o Padrão é 1. O intervalo vai de 0 a 255).*
* ConnectRetryInterval &nbsp;&nbsp;*(o Padrão é 1 segundo. O intervalo vai de 1 a 60).*
* Connection Timeout &nbsp;&nbsp;*(o Padrão é 15 segundos. O intervalo vai de 0 a 2147483647)*

Especificamente, os valores escolhidos devem ter Olá true igualdade a seguir:

* Connection Timeout = ConnectRetryCount * ConnectionRetryInterval

Por exemplo, se hello contar = 3 e intervalo = 10 segundos, um tempo limite de somente 29 segundos não bastante daria sistema Olá tempo suficiente para sua repetição 3º e final na conexão: 29 < 3 * 10.

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Conexão versus comando
Olá **ConnectRetryCount** e **ConnectRetryInterval** parâmetros permitem que seu **SqlConnection** Olá de repetição de objeto a operação de conexão sem informando ou incomodar seu programa, como retornar o programa de controle de tooyour. tentativas de saudação podem ocorrer em Olá situações a seguir:

* Chamada ao método mySqlConnection.Open
* Chamada ao método mySqlConnection.Execute

Mas há uma sutileza aqui. Se ocorrer um erro transitório enquanto seu *consulta* está sendo executado, o **SqlConnection** não Olá de repetir a operação de conexão, e ele certamente não repita a consulta do objeto. No entanto, **SqlConnection** rapidamente verificações Olá conexão antes de enviar sua consulta para execução. Se a verificação rápida Olá detectar um problema de conexão, **SqlConnection** Olá repetições a operação de conexão. Se a repetição de saudação for bem-sucedida, você consulta é enviada para execução.

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a>ConnectRetryCount deve ser combinada à lógica de repetição de aplicativo?
Suponha que seu aplicativo tenha lógica de repetição personalizada robusta. Ele pode repetir Olá 4 vezes a operação de conexão. Se você adicionar **ConnectRetryInterval** e **ConnectRetryCount** = cadeia de caracteres de conexão de tooyour 3, aumenta a too4 de contagem de repetição hello * 3 = 12 tentativas. Talvez você não queira um número tão alto de repetições.

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a>Conexões tooAzure banco de dados SQL
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a>Conexão: cadeia de conexão
cadeia de caracteres de conexão do Hello necessária para conectar-se tooAzure banco de dados SQL é ligeiramente diferente da cadeia de caracteres de saudação para conectar-se tooMicrosoft do SQL Server. Você pode copiar cadeia de caracteres de conexão de saudação do banco de dados de saudação [portal do Azure](https://portal.azure.com/).

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a>Conexão: endereço IP
Você deve configurar a saudação banco de dados SQL server tooaccept comunicação do endereço IP de saudação do computador de saudação que hospeda o programa cliente. Você pode fazer isso editando as configurações de firewall Olá por meio de saudação [portal do Azure](https://portal.azure.com/).

Se você esquecer o endereço IP tooconfigure hello, seu programa falhará com uma mensagem de erro úteis que declara o endereço IP hello necessário.

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

Para saber mais, consulte [Como definir as configurações de firewall no Banco de Dados SQL](sql-database-configure-firewall-settings.md)

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a>Conexão: portas
Normalmente, você só precisa tooensure que a porta 1433 está aberta para comunicação de saída, no computador de saudação que hospeda a você o programa cliente.

Por exemplo, quando o programa cliente está hospedado em um computador com Windows, Olá Firewall do Windows no host Olá permite que você tooopen a porta 1433:

1. Abrir o painel de controle de saudação
2. &gt; Todos os Itens do Painel de Controle
3. &gt; Firewall do Windows
4. &gt; Configurações Avançadas
5. &gt; Regras de Saída
6. &gt; Ações
7. &gt; Nova Regra

Se seu programa cliente estiver hospedado em uma máquina virtual do Azure (VM), você deverá ler:<br/>[Portas acima da 1433 para o ADO.NET 4.5 e o Banco de Dados SQL](sql-database-develop-direct-route-ports-adonet-v12.md).

Para saber mais sobre a configuração de portas e de endereços IP, consulte: [Firewall do Banco de Dados SQL do Azure](sql-database-firewall-configure.md)

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a>Conexão: ADO.NET 4.6.1
Se seu programa usa as classes ADO.NET como **SqlConnection** tooconnect tooAzure banco de dados SQL, é recomendável que você use o .NET Framework versão 4.6.1 ou superior.

ADO.NET 4.6.1:

* Para o banco de dados SQL Azure, há maior confiabilidade quando você abrir uma conexão usando Olá **SqlConnection. Open** método. Olá **abrir** método agora incorpora melhor esforço repetição mecanismos em falhas de tootransient de resposta, para determinados erros dentro do período de tempo limite de Conexão de saudação.
* Dá suporte ao pool de conexões. Isso inclui uma verificação eficiente que Olá conexão objeto assim que o programa está funcionando.

Quando você usa um objeto de conexão de um pool de conexão, é recomendável que seu programa temporariamente fechar conexão hello quando usá-lo não imediatamente. Abrir novamente uma conexão não é caro Olá maneira criando uma nova conexão é.

Se você estiver usando o ADO.NET 4.0 ou anterior, é recomendável que você atualize toohello ADO.NET mais recente.

* Desde novembro de 2015, você pode [baixar o ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a>Diagnostics
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a>Diagnóstico: testar se os utilitários podem se conectar
Se o programa estiver falhando tooconnect tooAzure banco de dados SQL, uma opção de diagnóstica é tooconnect tootry com um programa utilitário. Idealmente utilitário Olá conectaria usando Olá mesma biblioteca que usa o programa.

Em qualquer computador Windows, você pode experimentar estes utilitários:

* SQL Server Management Studio (ssms.exe), que se conecta usando ADO.NET.
* sqlcmd.exe, que se conecta usando [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).

Uma vez conectado, teste se uma consulta SQL SELECT curta funciona.

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a>Diagnóstico: Portas abertas de saudação seleção
Suponha que você suspeita de que as tentativas de conexão estão falhando devido a problemas de tooport. Em seu computador, você pode executar um utilitário que relatórios sobre configurações de porta de saudação.

No Linux Olá utilitários a seguir podem ser úteis:

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * (Alterar toobe de valor do exemplo hello seu endereço IP.)

No Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utilitário pode ser útil. Aqui está uma execução de exemplo que consultados situação de porta de saudação em um servidor de banco de dados SQL, e que foi executado em um computador laptop:

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a>Diagnóstico: registrar seus erros em log
Às vezes, um problema intermitente é mais bem diagnosticado pela detecção de um padrão geral ao longo de dias ou de semanas.

O cliente pode auxiliar em um diagnóstico ao registrar em log todos os erros encontrados. Pode ser capaz de toocorrelate entradas de log de Olá com dados de erro que o banco de dados do Azure SQL registra próprio internamente.

Enterprise Library 6 (EntLib60) oferece tooassist de classes .NET gerenciado com o log:

* [5 - como fácil como cair fora de um Log: usando Olá Logging Application Block](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a>Diagnóstico: examinar logs de erros do sistema
Aqui estão algumas instruções Transact-SQL SELECT que a consulta registra em log os erros e outras informações.

| Consulta de log | Descrição |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |Olá [sys. event_log](http://msdn.microsoft.com/library/dn270018.aspx) exibição oferece informações sobre os eventos individuais, incluindo alguns que podem causar erros transitórios ou falhas de conectividade.<br/><br/>Idealmente, você pode correlacionar Olá **start_time** ou **end_time** valores com informações sobre quando o programa cliente apresentar problemas.<br/><br/>**Dica:** você deve se conectar toohello **mestre** de banco de dados toorun isso. |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |Olá [sys. database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) exibição oferece contagens agregadas dos tipos de evento de diagnóstico adicional.<br/><br/>**Dica:** você deve se conectar toohello **mestre** de banco de dados toorun isso. |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a>Diagnóstico: Pesquisa eventos de problema no log de banco de dados SQL de saudação
Você pode procurar entradas sobre problema eventos no log de saudação do banco de dados do SQL Azure. Tente Olá após a instrução SELECT Transact-SQL em Olá **mestre** banco de dados:

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a>Algumas linhas retornadas de sys.fn_xe_telemetry_blob_target_read_file
A seguir, como seria a aparência de uma linha retornada. valores nulos de saudação mostrados geralmente não são nulos em outras linhas.

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a>Enterprise Library 6
Enterprise Library 6 (EntLib60) é uma estrutura de classes .NET que ajuda a implementar robustos clientes dos serviços de nuvem, um dos quais é o serviço de banco de dados do Azure SQL hello. Você pode localizar a área de tooeach dedicado de tópicos no qual EntLib60 podem ajudá-lo visitando primeiro:

* [A Enterprise Library 6 – abril de 2013](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

A lógica de repetição para tratar erros transitórios é uma área em que EntLib60 pode auxiliar:

* [4 - perseverance, o segredo de todos os Triumphs: usando Olá Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> Olá código-fonte para a EntLib60 está disponível para o público [baixar](http://go.microsoft.com/fwlink/p/?LinkID=290898). A Microsoft não tem nenhum recurso adicional de toomake planos tooEntLib de atualizações de manutenção ou atualizações.
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a>Classes do EntLib60 para erros transitórios e tentativas de repetição
Olá EntLib60 classes a seguir é particularmente úteis para lógica de repetição. Todos eles estão na ou são posteriormente, Olá namespace **transientfaulthandling**:

*Olá namespace **transientfaulthandling**:*

* **RetryPolicy** 
  
  * **ExecuteAction** 
* **ExponentialBackoff** 
* **SqlDatabaseTransientErrorDetectionStrategy** 
* **ReliableSqlConnection** 
  
  * **ExecuteCommand** 

Olá namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:

* **AlwaysTransientErrorDetectionStrategy** 
* **NeverTransientErrorDetectionStrategy** 

Aqui estão os links tooinformation sobre o EntLib60:

* Livre [Download do livro: tooMicrosoft do guia do desenvolvedor Enterprise Library, 2ª edição](http://www.microsoft.com/download/details.aspx?id=41145)
* Práticas recomendadas: [Diretrizes gerais para tentativas de repetição](../best-practices-retry-general.md) tem uma excelente discussão detalhada sobre lógica de repetição.
* Download NuGet de [Enterprise Library - bloqueio de aplicativos de manipulação de falhas transitórias 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a>EntLib60: bloco de log de saudação
* bloco de log Olá é uma solução altamente configurável e flexível que permite que você:
  
  * Crie e armazene mensagens de log em uma grande variedade de locais.
  * Categorize e filtre as mensagens.
  * Colete informações contextuais que sejam úteis para depuração e rastreamento, bem como para requisitos de auditoria e de log geral.
* bloco de log Olá abstrai Olá log funcionalidade do destino de log hello, para que o código do aplicativo hello seja consistente, independentemente do local hello e o tipo de armazenamento de log de destino hello.

Para obter detalhes, consulte: [5 - como fácil como cair fora de um Log: usando Olá Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a>O EntLib60 é o código-fonte do método IsTransient
Em seguida, de saudação **SqlDatabaseTransientErrorDetectionStrategy** classe, é o código-fonte para Olá Olá c# **IsTransient** método. código-fonte Olá esclarece que os erros foram considerados toobe transitório e pena repetir, a partir de abril de 2013.

Vários **//comment** linhas foram removidas da leitura de tooemphasize cópia.

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a>Próximas etapas
* Para solucionar outros problemas comuns de conexão de banco de dados de SQL do Azure, visite [tooAzure banco de dados SQL de problemas de solução de problemas conexão](sql-database-troubleshoot-common-connection-issues.md).
* [Pool de conexões do SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [*Repetindo* é de finalidade geral de repetir a biblioteca, escrita em uma licença do Apache 2.0 **Python**, tarefa de saudação do toosimplify de adicionar toojust de comportamento de repetição sobre qualquer coisa.](https://pypi.python.org/pypi/retrying)

