---
title: "aaaTroubleshooting diagnóstico do Azure | Microsoft Docs"
description: "Solucionar problemas ao usar o diagnóstico do Azure no Service Fabric, Serviços de Nuvem e Máquinas Virtuais do Azure."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Solução de problemas do Diagnóstico do Azure
Solução de problemas informações relevantes toousing diagnóstico do Azure. Para obter mais informações sobre o Diagnóstico do Azure, confira [Visão geral do Diagnóstico do Azure](azure-diagnostics.md).

## <a name="logical-components"></a>Componentes lógicos
**Iniciador de plug-in de diagnóstico (DiagnosticsPluginLauncher.exe)**: extensão de diagnóstico do Azure Olá é iniciado. Serve como entrada hello o processo de ponto.

**Plug-in de diagnóstico (DiagnosticsPlugin.exe)**: processo principal que é iniciado pelo iniciador da saudação acima e configura o agente de monitoramento de saudação, inicia e gerencia seu tempo de vida. 

**Agente de monitoramento (MonAgent\*.exe processos)**: esses processos Olá em massa de trabalho Olá; ou seja, o monitoramento, coleção e a transferência de Olá dados de diagnóstico.  

## <a name="logartifact-paths"></a>Caminhos de log/artefato
Aqui estão os artefatos e logs do hello caminhos toosome importantes. Vamos manter referindo-se toothese em todo o restante de saudação do documento hello:
### <a name="cloud-services"></a>Serviços de Nuvem
| Artefato | Caminho |
| --- | --- |
| **Arquivo de configuração de Diagnóstico do Microsoft Azure** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\Config.txt |
| **Arquivos de log** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\ |
| **Armazenamento local para dados de diagnóstico** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Tables |
| **Arquivo de configuração do Agente de monitoramento** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Pacote de extensão do Diagnóstico do Azure** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version> |
| **Caminho do utilitário de coleta de log** | %SystemDrive%\Packages\GuestAgent\ |
| **Arquivo de log MonAgentHost** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

### <a name="virtual-machines"></a>Máquinas Virtuais
| Artefato | Caminho |
| --- | --- |
| **Arquivo de configuração de Diagnóstico do Microsoft Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\RuntimeSettings |
| **Arquivos de log** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Logs\ |
| **Armazenamento local para dados de diagnóstico** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Tables |
| **Arquivo de configuração do Agente de monitoramento** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MaConfig.xml |
| **Arquivo de status** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Status |
| **Pacote de extensão do Diagnóstico do Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>|
| **Caminho do utilitário de coleta de log** | C:\WindowsAzure\Packages |
| **Arquivo de log MonAgentHost** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>Os dados de métrica não são exibidos no portal do Azure
O Diagnóstico do Azure fornece um conjunto de dados de métrica, que podem ser exibidos no portal do Azure. Se você tiver problemas com ver esses dados no portal, a conta de armazenamento de diagnóstico seleção Olá -> WADMetrics\* tabela toosee se existem registros correspondentes de métrica hello. Aqui, Olá PartitionKey da tabela de saudação é Olá ID do recurso de máquina virtual ou conjunto de escalas da máquina virtual e Olá RowKey é o nome da métrica hello ou seja, o nome de contador de desempenho.

Se a ID de recurso Olá estiver incorreto, verifique a configuração de diagnóstico -> métricas -> ResourceId toosee se a ID de recurso hello está definida corretamente.

Se não houver nenhum dado de métrica específica hello, verificação de configuração de diagnóstico -> PerformanceCounter toosee se a métrica de saudação (contador de desempenho) é incluída. Habilitamos Olá contadores a seguir por padrão.
- \Processador(_Total)\% Tempo do processador
- \Memória\Bytes Disponíveis
- \Aplicativos ASP.NET (__Total__)\Solicitações/s
- \Aplicativos ASP.NET (__Total__)\Total de Erros/s
- \ASP.NET\Solicitações Enfileiradas
- \ASP.NET\Solicitações Rejeitadas
- \Processador(w3wp)\% Tempo do Processador
- \Processo(w3wp)\Bytes Privados
- \Processo(WaIISHost)\% Tempo do Processador
- \Processo(WaIISHost)\Bytes Privados
- \Processo(WaWorkerHost)\% Tempo do Processador
- \Processo(WaWorkerHost)\Bytes Privados
- \Memória\Falhas de Página/s
- \.Memória CLR NET(_Global_)\% Tempo em GC
- \LogicalDisk(C:)\Bytes de Gravação de Disco/s
- \LogicalDisk(C:)\Bytes de Leitura de Disco/s
- \LogicalDisk(D:)\Bytes de Gravação de Disco/s
- \LogicalDisk(D:)\Bytes de Leitura de Disco/s

Se a configuração hello está definida corretamente, mas você não pode ver dados de métrica hello, diretrizes Olá abaixo para investigação futura hello.


## <a name="azure-diagnostics-is-not-starting"></a>Azure Diagnostics não está iniciando
Examinar **DiagnosticsPluginLauncher.log** e **DiagnosticsPlugin.log** arquivos de log de arquivos do local de saudação do hello fornecido acima para obter informações sobre por que diagnóstico falha toostart. 

Se esses logs indicam `Monitoring Agent not reporting success after launch`, isso significa que houve uma falha ao iniciar MonAgentHost.exe. Examine os logs de saudação para que no local de saudação indicado para `MonAgentHost log file` na seção de saudação acima.

a última linha Olá Olá dos arquivos de log contém código de saída de hello.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Se você encontrar um **negativo** código de saída, consulte toohello [tabela de código de saída](#azure-diagnostics-plugin-exit-codes) em Olá [referências](#references).

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>Dados de diagnóstico estão conectado não tooAzure armazenamento
Determine se nenhum dado é exibido ou apenas alguns dos dados de saudação não estão aparecendo.

### <a name="diagnostics-infrastructure-logs"></a>Logs de infraestrutura de diagnósticos
Logs da Infraestrutura de diagnóstico é onde o diagnóstico do Azure registra quaisquer erros que são encontrados. Verifique se você habilitou ([como?](#how-to-check-diagnostics-extension-configuration)) captura de logs de infraestrutura de diagnóstico em sua configuração e rapidamente procure erros relevantes que aparecem no hello `DiagnosticInfrastructureLogsTable` tabela em sua conta de armazenamento configurado.

### <a name="no-data-is-showing-up"></a>Nenhum dado está sendo exibido
Olá causa mais comum de dados de evento totalmente ausente é informações da conta de armazenamento definida incorretamente.

Solução: corrija sua configuração do Diagnóstico e o reinstale.

Se a conta de armazenamento de saudação está configurado corretamente, remoto da área de trabalho em make e máquina Olá se DiagnosticsPlugin.exe e MonAgentCore.exe estão em execução. Se eles não estiverem em execução, siga [Diagnóstico do Azure não está iniciando](#azure-diagnostics-is-not-starting). Se estiver executando processos hello, ir muito[dados obtendo capturados localmente](#is-data-getting-captured-locally) e siga este guia de lá.

### <a name="part-of-hello-data-is-missing"></a>Parte dos dados hello está ausente
Se você estiver obtendo alguns dados, mas não outros. Isso significa que a coleta de dados Olá / pipeline de transferência está definida corretamente. Siga subseções Olá aqui toonarrow o problema de saudação é:
#### <a name="is-collection-configured"></a>A coleção foi configurada: 
Configuração de diagnóstico contém parte Olá que instrui para um tipo específico de toobe dados coletado. [Examine a configuração](#how-to-check-diagnostics-extension-configuration) toomake-se de que você não está procurando dados você não tiver configurado para a coleção.
#### <a name="is-hello-host-generating-data"></a>É o host Olá gerando dados:
- **Contadores de desempenho**: Abra o perfmon e verifique o contador de saudação.
- **Logs de rastreamento**: área de trabalho remota Olá VM e adicione o arquivo de configuração do aplicativo de toohello um TextWriterTraceListener.  Consulte tooset http://msdn.microsoft.com/library/sk36c28t.aspx o ouvinte de texto de saudação.  Verifique se Olá `<trace>` tem elemento `<trace autoflush="true">`.<br />
Se você não vir os logs de rastreamento sendo gerados, execute [Mais sobre logs de rastreamento ausentes](#more-about-trace-logs-missing).
- **Rastreamentos ETW**: área de trabalho remota Olá VM e instalar PerfView.  No PerfView, execute Arquivo -> Comando de Usuário -> Escutar etwprovder1,etwprovider2,etc.  Observe que o comando de escuta Olá diferencia maiusculas de minúsculas e não pode haver espaços entre a lista separada por vírgulas Olá dos provedores do ETW.  Se o comando Olá falhar toorun, você pode clicar botão de 'Log' hello na parte inferior direita Olá da Olá Perfview ferramenta toosee que qual foi tentada toorun e o resultado de saudação foi.  Supondo que a entrada hello está correta, em seguida, uma nova janela será exibida para cima e em alguns segundos, você começará ver rastreamentos ETW.
- **Logs de eventos**: área de trabalho remota Olá VM. Abra `Event Viewer` e certifique-se de que existem Olá eventos.
#### <a name="is-data-getting-captured-locally"></a>Os dados estão sendo capturados localmente:
Em seguida, certifique-se de dados saudação obtendo capturados localmente.
dados de saudação são armazenados localmente em `*.tsf` arquivos [repositório local de saudação para dados de diagnóstico](#log-artifacts-path). Diferentes tipos de logs coletados em diferentes arquivos `.tsf`. nomes de saudação são nomes de tabela toohello semelhantes no armazenamento do azure. Por exemplo `Performance Counters` é coletado no `PerformanceCountersTable.tsf`, Logs de eventos coletados no `WindowsEventLogsTable.tsf`. Use instruções de saudação em [extração de Log Local](#local-log-extraction) tooopen Olá coleta local arquivos da seção e verifique se você vê-los obtendo coletados no disco.

Se você não ver logs obtendo coletados localmente e já tiver verificado que o host hello está gerando dados, você provavelmente tem um problema de configuração. Examine a configuração cuidadosamente para seção apropriada de saudação. Revise também a configuração de saudação gerada para MonitoringAgent [MaConfig.xml](#log-artifacts-path) e verifique se há alguma seção que descreve a origem de log relevantes hello e que não sejam perdido em conversão entre a configuração de diagnóstico do azure e configuração do agente de monitoramento.
#### <a name="is-data-getting-transferred"></a>Os dados estão sendo transferidos:
Se você tiver verificado dados saudação obtendo capturados localmente, mas você ainda não estiver visível na sua conta de armazenamento: 
- Primeiramente, verifique se você forneceu uma conta de armazenamento correta e que você não rodado chaves etc.for Olá considerando a conta de armazenamento. Para serviços de nuvem, às vezes, podemos ver que as pessoas não atualizam seus `useDevelopmentStorage=true`.
- Se a conta de armazenamento fornecida está correta. Verifique se que você não tem algumas restrições de rede que não permitem componentes Olá tooreach pontos de extremidade de armazenamento público. Toodo unidirecional que é a área de trabalho tooremote saudação do computador e tente toowrite algo toohello mesmo armazenamento de conta por conta própria.
- Por fim, você pode tentar e ver quais falhas estão sendo relatadas pelo Agente de monitoramento. Agente de monitoramento grava logs `maeventtable.tsf` localizado em [repositório local para dados de diagnóstico de Olá](#log-artifacts-path). Siga as instruções em [extração de Log Local](#local-log-extraction) seção tooopen esse arquivo e tente e descobrir se há `errors` indicando arquivos locais do tooread falhas ou gravar toostorage.

### <a name="capturing--archiving-logs"></a>Capturando/arquivando logs
Você passou pelo Olá acima etapas, mas não foi possível calcular o que estava incorreto e estão pensando sobre como contatar o suporte. Olá primeiro podem pedir que você é toocollect logs em seu computador. Você pode poupar tempo fazendo isso você mesmo. Executar Olá `CollectGuestLogs.exe` utilitário em [caminho de utilitário de coleta de Log](#log-artifacts-path) e gera um arquivo zip com todos os logs do azure relevantes no hello mesma pasta.

## <a name="diagnostics-data-tables-not-found"></a>Tabelas dos dados de diagnósticos não encontradas
tabelas de Olá no armazenamento do Azure, mantendo eventos ETW são nomeadas usando Olá código a seguir:

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

Aqui está um exemplo:

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
Isso gera quatro tabelas:

| Evento | Nome da tabela |
| --- | --- |
| provider=”prov1” &lt;Event id=”1” /&gt; |WADEvent+MD5("prov1")+"1" |
| provider=”prov1” &lt;Event id=”2” eventDestination=”dest1” /&gt; |WADdest1 |
| provider=”prov1” &lt;DefaultEvents /&gt; |WADDefault+MD5("prov1") |
| provider=”prov2” &lt;DefaultEvents eventDestination=”dest2” /&gt; |WADdest2 |

## <a name="references"></a>Referências

### <a name="how-toocheck-diagnostics-extension-configuration"></a>Como toocheck configuração de extensão de diagnóstico
Olá toocheck de maneira mais fácil a configuração de extensão toonavigate toohttp://resources.azure.com, navegar toohello virtual machine ou serviço em nuvem na qual extensão de diagnóstico do Azure hello (IaaSDiagnostics / PaaDiagnostics) em questão.

Como alternativa, área de trabalho remota na máquina hello e examine o arquivo de configuração de diagnóstico do Azure Olá descrito na seção apropriada de saudação [aqui](#log-artifacts-path).

No caso procurar **Microsoft.Azure.Diagnostics** , em seguida, para Olá **xmlCfg** ou **WadCfg** campo. 

No caso de máquinas virtuais, se Olá WadCfg campo não estiver presente, isso significa Olá configuração está em JSON. Se houver um campo de xmlCfg Olá, isso significa Olá config é em XML e é codificada em base64. É necessário muito[decodificá-la](http://www.bing.com/search?q=base64+decoder) toosee Olá XML que foi carregado pelo diagnóstico.

Para função de serviço de nuvem, se você escolher a configuração de saudação do disco, dados de saudação serão codificação base64 para que você precisará de muito[decodificá-la](http://www.bing.com/search?q=base64+decoder) toosee Olá XML que foi carregado pelo diagnóstico.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Códigos de saída do plug-in do Diagnóstico do Microsoft Azure
plug-in de saudação retorna Olá códigos de saída a seguir:

| Código de Saída | Descrição |
| --- | --- |
| 0 |Sucesso. |
| -1 |Erro genérico. |
| -2 |Arquivo de rcf de saudação tooload não é possível.<p>Esse erro interno só deve acontecer se o iniciador de plug-in do agente de convidado Olá é invocada manualmente, incorretamente, em Olá VM. |
| -3 |Não é possível carregar o arquivo de configuração de diagnóstico de saudação.<p><p>Solução: causado por um arquivo de configuração que não passa pela validação do esquema. solução de saudação é tooprovide um arquivo de configuração que esteja em conformidade com o esquema de saudação. |
| -4 |Outra instância do hello diagnóstico de agente de monitoramento já está usando o diretório do recurso local hello.<p><p>Solução: especifique um valor diferente para **LocalResourceDirectory**. |
| -6 |iniciador de plug-in do agente de convidado Olá tentativa toolaunch diagnóstico com uma linha de comando inválida.<p><p>Esse erro interno só deve acontecer se o iniciador de plug-in do agente de convidado Olá é invocada manualmente, incorretamente, em Olá VM. |
| -10 |Olá plug-in de diagnóstico foi encerrado com uma exceção sem tratamento. |
| -11 |o agente convidado Olá era o processo de saudação de toocreate não é possível responsável por iniciar e monitorar Olá agente de monitoramento.<p><p>Solução: Verifique se os recursos de sistema suficientes disponíveis toolaunch novos processos.<p> |
| -101 |Argumentos inválidos ao chamar hello plug-in de diagnóstico.<p><p>Esse erro interno só deve acontecer se o iniciador de plug-in do agente de convidado Olá é invocada manualmente, incorretamente, em Olá VM. |
| -102 |processo do plug-in de saudação é tooinitialize não é possível em si.<p><p>Solução: Verifique se os recursos de sistema suficientes disponíveis toolaunch novos processos. |
| -103 |processo do plug-in de saudação é tooinitialize não é possível em si. Especificamente, é objeto de agente de log Olá toocreate não é possível.<p><p>Solução: Verifique se os recursos de sistema suficientes disponíveis toolaunch novos processos. |
| -104 |Tooload não é possível Olá rcf o arquivo fornecido pelo agente de convidado hello.<p><p>Esse erro interno só deve acontecer se o iniciador de plug-in do agente de convidado Olá é invocada manualmente, incorretamente, em Olá VM. |
| -105 |plug-in de diagnóstico de saudação não é possível abrir o arquivo de configuração de diagnóstico de saudação.<p><p>Esse erro interno só deve acontecer se o plug-in de diagnóstico de saudação é invocada manualmente, incorretamente, em Olá VM. |
| -106 |Não é possível ler o arquivo de configuração de diagnóstico de saudação.<p><p>Solução: causado por um arquivo de configuração que não passa pela validação do esquema. Portanto, solução Olá é tooprovide um arquivo de configuração que esteja em conformidade com o esquema de saudação. Consulte [como toocheck configuração de extensão de diagnóstico](#how-to-check-diagnostics-extension-configuration). |
| -107 |Olá recurso directory passagem toohello agente de monitoramento é inválido.<p><p>Esse erro interno só deve acontecer se Olá agente de monitoramento é invocada manualmente, incorretamente, em Olá VM.</p> |
| -108 |Não é possível tooconvert o arquivo de configuração de diagnóstico de saudação em Olá arquivo de configuração do agente de monitoramento.<p><p>Esse erro interno deve ocorrer somente se o plug-in de diagnóstico Olá manualmente é invocado com um arquivo de configuração inválido. |
| -110 |Erro de configuração de diagnóstico geral.<p><p>Esse erro interno deve ocorrer somente se o plug-in de diagnóstico Olá manualmente é invocado com um arquivo de configuração inválido. |
| -111 |Agente de monitoramento não é possível toostart hello.<p><p>Solução: verifique se há recursos de sistema suficientes disponíveis para iniciar novos processos. |
| -112 |Erro geral |

### <a name="local-log-extraction"></a>Extração de log local
Olá, agente de monitoramento coleta logs e artefatos como `.tsf` arquivos. O arquivo `.tsf` não está legível, mas você pode convertê-lo em um `.csv` da seguinte maneira: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Um novo arquivo chamado `<relevantLogFile>.csv` será criado no hello mesmo caminho como Olá correspondente `.tsf` arquivo.

**Observação**: basta toorun este utilitário em arquivo tsf principal de saudação (por exemplo, PerformanceCountersTable.tsf). Olá arquivos complementares (por exemplo, PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002. tsf etc.) será processado automaticamente.

### <a name="more-about-trace-logs-missing"></a>Mais informações sobre Logs de rastreamento ausentes

**Observação:** principalmente aplica-se serviços toocloud somente a menos que você configurou Olá DiagnosticsMonitorTraceListener em um aplicativo em execução na sua VM IaaS. 

- Verifique se Olá que diagnosticmonitortracelistener está configurado no Olá Web. config ou App. config.  Isso é configurado por padrão em projetos de serviço de nuvem, mas alguns clientes de comentário fora que fará com que a saudação toonot de instruções de rastreamento seja coletado pelo diagnóstico. 
- Se não estão obtendo gravados logs de Olá OnStart ou executar método Certifique-se de que Olá que diagnosticmonitortracelistener está em Olá App. config.  Por padrão, ele está em Olá Web. config, mas que se aplica apenas toocode em execução no w3wp.exe; Portanto, você precisa-lo em App. config toocapture rastreamentos em execução no WaIISHost.exe.
- Certifique-se de que você está usando Diagnostics.Trace.TraceXXX em vez de Diagnostics.Debug.WriteXXX.  Olá instruções de depuração serão removidas de uma compilação de versão.
- Verifique se o código compilado de saudação realmente tem linhas de trace hello (use tooverify Reflector, ildasm ou ILSpy).  Trace comandos são removidos do binário Olá compilado, a menos que você usar o símbolo de compilação condicional Olá rastreamento.  Se usar o projeto do msbuild toobuild Olá, esta será uma toorun problema comum em.

## <a name="known-issues-and-mitigations"></a>Problemas e mitigações conhecidos
Aqui está uma lista dos problemas conhecidos com mitigações conhecidas:

**1. Dependência do .NET 4.5:**

WAD tem uma dependência de tempo de execução no .NET framework 4.5 ou superior. Em tempo de saudação de gravação de isso, todos os computadores provisionados para os serviços de nuvem, bem como todos os oficial do azure base imagens da máquina Virtual tem o .NET 4.5 ou acima instalado. É possível ainda porém tooland em uma situação em que você tente toorun WAD em um computador que não tem o .NET 4.5 ou superior. Isso acontece quando você cria seu computador fora de uma imagem antiga ou instantâneo; ou traz seu próprio disco personalizado.

Isso geralmente se manifesta como um código de saída **255** ao executar o DiagnosticsPluginLauncher.exe. Falha ocorre devido a toohello sem tratamento de exceção: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Mitigação:** instala o .NET 4.5 ou superior no seu computador.

**2. Dados de Contadores de desempenho estão disponíveis no armazenamento, mas não são mostrados no portal**

A experiência do portal de máquinas virtuais mostra determinados contadores de desempenho por padrão. Se você não vê-los e você sabe que estão sendo gerados dados saudação porque ele está disponível no armazenamento. Verificação:
- Se dados Olá no armazenamento possui nomes de contador em inglês. Se os nomes de contadores de saudação não estão em inglês, portal gráfico de métrica não será capaz de toorecognize-lo.
- Se você estiver usando caracteres curinga (\*) em seus nomes de contador de desempenho, o portal de Olá não será capaz de toocorrelate Olá configurado e coletados contador.

**Mitigação**: alterar tooEnglish de idioma do computador Olá para contas do sistema. Painel de controle -> região -> administrativo -> configurações de cópia -> desmarque "Bem-vindo ao sistema e tela contas" para que não seja de idioma personalizado Olá aplicado toosystem conta. Verifique também se que você não usar curingas, se você quiser toobe portal sua experiência de consumo principal.
