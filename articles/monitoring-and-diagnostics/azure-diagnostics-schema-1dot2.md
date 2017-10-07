---
title: "aaaAzure esquema de configuração do diagnóstico 1.2 | Microsoft Docs"
description: "Relevante APENAS se você estiver usando o SDK do Azure 2.5 com Máquinas Virtuais do Azure, conjuntos de dimensionamento de máquinas virtuais, Service Fabric ou Serviços de Nuvem."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Esquema de configuração do Azure Diagnostics 1.2
> [!NOTE]
> Diagnóstico do Azure é Olá componente usado toocollect os contadores de desempenho e outras estatísticas de máquinas virtuais do Azure, conjuntos de escala de máquina Virtual, serviço de malha e serviços de nuvem.  Esta página só é relevante se você estiver usando um desses serviços.
>

O Diagnóstico do Azure é usado com outros produtos de diagnóstico da Microsoft, como Azure Monitor, Application Insights e Log Analytics.

Esse esquema define valores possíveis hello, você pode usar as definições de configuração de diagnóstico de tooinitialize quando o monitor de diagnóstico Olá é iniciado.  


 Baixe a definição de esquema de arquivo de configuração pública Olá executando Olá comando PowerShell a seguir:  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 Para saber mais sobre o uso do Diagnóstico do Azure, confira [Habilitando o Diagnóstico nos Serviços de Nuvem do Azure](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Exemplo de arquivo de configuração de diagnóstico Olá  
 saudação de exemplo a seguir mostra um arquivo de configuração de diagnóstico típico:  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
  <WadCfg>  
    <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  
      <PerformanceCounters scheduledTransferPeriod="PT1M">  
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
      </PerformanceCounters>  
      <Directories scheduledTransferPeriod="PT5M">  
        <IISLogs containerName="iislogs" />  
        <FailedRequestLogs containerName="iisfailed" />  
        <DataSources>  
          <DirectoryConfiguration containerName="mynewprocess">  
            <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
          </DirectoryConfiguration>  
          <DirectoryConfiguration containerName="badapp">  
            <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
          </DirectoryConfiguration>  
          <DirectoryConfiguration containerName="goodapp">  
            <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
          </DirectoryConfiguration>  
        </DataSources>  
      </Directories>  
      <EtwProviders>  
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
          <Event id="0"/>  
          <Event id="1" eventDestination="errorTable"/>  
          <DefaultEvents />  
        </EtwEventSourceProviderConfiguration>  
        <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
          <Event id="0"/>  
          <DefaultEvents eventDestination="defaultTable"/>  
        </EtwManifestProviderConfiguration>  
      </EtwProviders>  
      <WindowsEventLog scheduledTransferPeriod="PT5M">  
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
        <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
        <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
      </WindowsEventLog>  
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>Namespace de Configuração de Diagnóstico  
 Olá namespace XML para o arquivo de configuração de diagnóstico Olá é:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>Elemento PublicConfig  
 Elemento de nível superior do arquivo de configuração de diagnóstico de saudação. Olá tabela a seguir descreve os elementos de Olá Olá do arquivo de configuração.  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**WadCfg**|Obrigatório. Definições de configuração para Olá toobe de dados de telemetria coletados.|  
|**StorageAccount**|nome de Olá Olá armazenamento do Azure toostore Olá de dados de conta no. Isso também pode ser especificado como um parâmetro ao executar o cmdlet Olá AzureServiceDiagnosticsExtension conjunto.|  
|**LocalResourceDirectory**|diretório Olá Olá toobe de máquina virtual usada pelo Olá dados de eventos do agente de monitoramento toostore. Se não for definido, o diretório padrão de saudação é usado:<br /><br /> Para uma função de Trabalho/da Web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Para uma Máquina Virtual: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Os atributos obrigatórios são:<br /><br /> -                      **caminho** - Olá do hello sistema toobe usado pelo diagnóstico do Azure.<br /><br /> -                      **expandEnvironment** -controla se as variáveis de ambiente são expandidas no nome do caminho de saudação.|  

## <a name="wadcfg-element"></a>Elemento WadCFG  
Define as configurações de saudação toobe de dados de telemetria coletados. Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|Obrigatório. Os atributos opcionais são:<br /><br /> -                     **overallQuotaInMB** -quantidade máxima de saudação do espaço em disco local que pode ser consumido por Olá vários tipos de dados de diagnóstico coletados pelo diagnóstico do Azure. configuração do saudação padrão é 5120MB.<br /><br /> -                     **useProxyServer** -configurar o diagnóstico do Azure toouse Olá servidor proxy conforme definido nas configurações do IE.|  
|**CrashDumps**|Habilite a coleta de despejos de memória. Os atributos opcionais são:<br /><br /> -                     **containerName** -nome Olá Olá do contêiner de blob em sua toobe de conta de armazenamento do Azure usado toostore despejos de memória.<br /><br /> -                     **crashDumpType** -toocollect configura o diagnóstico do Azure ou completo do Mini despejos de memória.<br /><br /> -                     **directoryQuotaPercentage**-configura a porcentagem de saudação do **overallQuotaInMB** toobe reservado para despejos de memória em Olá VM.|  
|**DiagnosticInfrastructureLogs**|Habilite a coleta de logs gerados pelo Diagnóstico do Azure. Olá logs de infraestrutura de diagnóstico são úteis para solucionar Olá sistema de diagnóstico. Os atributos opcionais são:<br /><br /> -                     **scheduledTransferLogLevelFilter** -configura o nível de severidade mínimo Olá Olá logs coletados.<br /><br /> -                     **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Diretórios**|Habilita Olá coleção de conteúdo de saudação de um diretório, os logs de solicitação de acesso e/ou os logs do IIS com falha do IIS. Atributo opcional:<br /><br /> **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|Configura a coleta de eventos ETW do EventSource e/ou os provedores baseados no Manifesto ETW.|  
|**Métricas**|Esse elemento permite que você toogenerate uma tabela de contador de desempenho é otimizada para consultas rápidas. Cada contador de desempenho que é definido em Olá **PerformanceCounters** elemento é armazenado na tabela de métricas de saudação na tabela de contador de desempenho toohello adição. Atributo obrigatório:<br /><br /> **resourceId** -este é o ID de recurso de saudação do hello Máquina Virtual que você está implantando o diagnóstico do Azure para. Obter Olá **resourceID** de saudação [portal do Azure](https://portal.azure.com). Selecione **Procurar** -> **Grupos de Recursos** -> **<Nome\>**. Clique em Olá **propriedades** lado a lado e copie o valor de saudação da saudação **ID** campo.|  
|**PerformanceCounters**|Habilita a coleta de saudação de contadores de desempenho. Atributo opcional:<br /><br /> **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. O valor é um [XML "Tipo de Dados de Duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**WindowsEventLog**|Habilita a coleta de saudação de Logs de eventos do Windows. Atributo opcional:<br /><br /> **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. O valor é um [XML "Tipo de Dados de Duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  

## <a name="crashdumps-element"></a>Elemento CrashDumps  
 Habilita a coleta de despejos de memória. Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|Obrigatório. Atributo obrigatório:<br /><br /> **processName** - Olá nome do processo de saudação deseja toocollect de diagnóstico do Azure um despejo de memória para.|  
|**crashDumpType**|Configura o diagnóstico do Azure toocollect completo ou mini despejos de memória.|  
|**directoryQuotaPercentage**|Configura o percentual de saudação do **overallQuotaInMB** toobe reservado para despejos de memória em Olá VM.|  

## <a name="directories-element"></a>Elemento Directories  
 Habilita Olá coleção de conteúdo de saudação de um diretório, os logs de solicitação de acesso e/ou os logs do IIS com falha do IIS. Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**DataSources**|Uma lista de diretórios toomonitor.|  
|**FailedRequestLogs**|Incluindo esse elemento na configuração de saudação habilita a coleta de logs de aplicativo ou site do IIS tooan solicitações com falha. Você também deve habilitar as opções de rastreamento em **system.WebServer** em **Web.config**.|  
|**IISLogs**|Incluindo esse elemento na configuração de saudação habilita a coleta de saudação de logs do IIS:<br /><br /> **containerName** -nome Olá Olá do contêiner de blob em sua toobe de conta de armazenamento do Azure usado logs do IIS Olá toostore.|  

## <a name="datasources-element"></a>Elemento DataSources  
 Uma lista de diretórios toomonitor. Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**DirectoryConfiguration**|Obrigatório. Atributo obrigatório:<br /><br /> **containerName** -nome de Olá Olá do contêiner de blob em seu armazenamento do Azure conta toostore toobe usado arquivos de log de saudação.|  

## <a name="directoryconfiguration-element"></a>Elemento DirectoryConfiguration  
 **DirectoryConfiguration** pode incluir qualquer Olá **absoluto** ou **LocalResource** elemento, mas não ambos. Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**Absolute**|Olá caminho absoluto toohello diretório toomonitor. Olá seguintes atributos é necessário:<br /><br /> -                     **Caminho** -Olá caminho absoluto toohello diretório toomonitor.<br /><br /> -                      **expandEnvironment** - configura se as variáveis de ambiente em Path são expandidas ou não.|  
|**LocalResource**|Olá toomonitor do caminho relativo tooa recurso local. Os atributos obrigatórios são:<br /><br /> -                     **Nome** -Olá recurso local que contém a saudação diretório toomonitor<br /><br /> -                     **relativePath** -Olá tooName relativo de caminho que contém a saudação diretório toomonitor|  

## <a name="etwproviders-element"></a>Elemento EtwProviders  
 Configura a coleta de eventos ETW do EventSource e/ou os provedores baseados no Manifesto ETW. Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Configura a coleta de eventos gerados desde a [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Atributo obrigatório:<br /><br /> **provedor** -nome da classe de saudação do evento de EventSource hello.<br /><br /> Os atributos opcionais são:<br /><br /> -                     **scheduledTransferLogLevelFilter** -Olá conta de armazenamento de tooyour de tootransfer nível de severidade mínimo.<br /><br /> -                     **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. O valor é um [XML Tipo de Dados de Duração](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**EtwManifestProviderConfiguration**|Atributo obrigatório:<br /><br /> **provedor** -Olá GUID do provedor de eventos de saudação<br /><br /> Os atributos opcionais são:<br /><br /> - **scheduledTransferLogLevelFilter** -Olá conta de armazenamento de tooyour de tootransfer nível de severidade mínimo.<br /><br /> -                     **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. O valor é um [XML Tipo de Dados de Duração](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="etweventsourceproviderconfiguration-element"></a>Elemento EtwEventSourceProviderConfiguration  
 Configura a coleta de eventos gerados desde a [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**DefaultEvents**|Atributo opcional:<br /><br /> **eventDestination** - Olá nome hello toostore Olá eventos de tabela em|  
|**Evento**|Atributo obrigatório:<br /><br /> **ID** -id de saudação do evento de saudação.<br /><br /> Atributo opcional:<br /><br /> **eventDestination** - Olá nome hello toostore Olá eventos de tabela em|  

## <a name="etwmanifestproviderconfiguration-element"></a>Elemento EtwManifestProviderConfiguration  
 Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**DefaultEvents**|Atributo opcional:<br /><br /> **eventDestination** - Olá nome hello toostore Olá eventos de tabela em|  
|**Evento**|Atributo obrigatório:<br /><br /> **ID** -id de saudação do evento de saudação.<br /><br /> Atributo opcional:<br /><br /> **eventDestination** - Olá nome hello toostore Olá eventos de tabela em|  

## <a name="metrics-element"></a>Elemento Metrics  
 Permite que você toogenerate uma tabela de contador de desempenho é otimizada para consultas rápidas. Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**MetricAggregation**|Atributo obrigatório:<br /><br /> **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. O valor é um [XML Tipo de Dados de Duração](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="performancecounters-element"></a>Elemento PerformanceCounters  
 Habilita a coleta de saudação de contadores de desempenho. Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|Olá seguintes atributos é necessário:<br /><br /> -                     **counterSpecifier** - Olá nome saudação do contador de desempenho. Por exemplo: `\Processor(_Total)\% Processor Time`. tooget uma lista de contadores de desempenho em seu host que execute o comando Olá `typeperf`.<br /><br /> -                     **sampleRate** -frequência hello contador deve ser testado.<br /><br /> Atributo opcional:<br /><br /> **unidade** -unidade de medida de contador de saudação de saudação.|  

## <a name="performancecounterconfiguration-element"></a>Elemento PerformanceCounterConfiguration  
 Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**anotação**|Atributo obrigatório:<br /><br /> **displayName** -nome para exibição para o contador de saudação Olá<br /><br /> Atributo opcional:<br /><br /> **localidade** -Olá toouse localidade ao exibir o nome do contador Olá|  

## <a name="windowseventlog-element"></a>Elemento WindowsEventLog  
 Olá, a tabela a seguir descreve os elementos filho:  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**DataSource**|toocollect de logs de eventos do Windows Hello. Atributo obrigatório:<br /><br /> **nome** -coletados de consulta do XPath Olá descrevendo toobe de eventos do windows hello. Por exemplo:<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> toocollect todos os eventos, especifique "*".|
