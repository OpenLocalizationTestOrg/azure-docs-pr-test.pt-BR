---
title: "aaaAzure esquema de configuração do diagnóstico 1.0 | Microsoft Docs"
description: "Relevante APENAS se você estiver usando o SDK do Azure 2.4 e abaixo com Máquinas Virtuais do Azure, conjuntos de dimensionamento de máquinas virtuais, Service Fabric ou Serviços de Nuvem."
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a>Esquema de Configuração do Azure Diagnostics 1.0
> [!NOTE]
> Diagnóstico do Azure é Olá componente usado toocollect os contadores de desempenho e outras estatísticas de máquinas virtuais do Azure, conjuntos de escala de máquina Virtual, serviço de malha e serviços de nuvem.  Esta página só é relevante se você estiver usando um desses serviços.
>

O Diagnóstico do Azure é usado com outros produtos de diagnóstico da Microsoft, como Azure Monitor, Application Insights e Log Analytics.

arquivo de configuração de diagnóstico do Azure Olá define os valores que são usados tooinitialize Olá Monitor de diagnóstico. Esse arquivo é definições de configuração de diagnóstico de tooinitialize usada quando inicia do monitor de diagnósticos de saudação.  

 Por padrão, o arquivo de esquema de configuração de diagnóstico do Azure Olá é instalado toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory. Substituir `<version>` com versão de hello instalado do hello [SDK do Azure](http://www.windowsazure.com/develop/downloads/).  

> [!NOTE]
>  o arquivo de configuração de diagnóstico Olá normalmente é usado com tarefas de inicialização que exigem toobe de dados de diagnóstico coletada anteriormente no processo de inicialização de saudação. Para obter mais informações sobre como usar o Diagnóstico do Azure, consulte [Coletar dados do log usando o Diagnóstico do Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Exemplo de arquivo de configuração de diagnóstico Olá  
 saudação de exemplo a seguir mostra um arquivo de configuração de diagnóstico típico:  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a>Namespace DiagnosticsConfiguration  
 Olá namespace XML para o arquivo de configuração de diagnóstico Olá é:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>Elementos de esquema  
 arquivo de configuração de diagnóstico de saudação inclui Olá elementos a seguir.


## <a name="diagnosticmonitorconfiguration-element"></a>Elemento DiagnosticMonitorConfiguration  
elemento de nível superior de saudação do arquivo de configuração de diagnóstico de saudação.  

Atributos:

|Atributo  |Tipo   |Obrigatório| Padrão | Descrição|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|duration|Opcional | PT1M| Especifica o intervalo de saudação em pesquisas de monitor de diagnóstico que Olá para alterações de configuração de diagnóstico.|  
|**overallQuotaInMB**|unsignedInt|Opcional| 4000 MB. Se você fornecer um valor, ele não deverá exceder esse valor |Olá total de armazenamento do sistema de arquivos alocado para todos os buffers de log.|  

## <a name="diagnosticinfrastructurelogs-element"></a>Elemento DiagnosticInfrastructureLogs  
Define a configuração de buffer de saudação para logs de saudação que são gerados pela infraestrutura de diagnóstico subjacente hello.

Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Atributos:

|Atributo|Tipo|Descrição|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.<br /><br /> saudação padrão é 0.|  
|**scheduledTransferLogLevelFilter**|string|Opcional. Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos. valor padrão de saudação é **indefinido**. Outros possíveis valores são **Detalhado**, **Informação**, **Aviso**, **Erro** e **Crítico**.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.<br /><br /> padrão de saudação é PT0S.|  

## <a name="logs-element"></a>Elemento Logs  
 Define a configuração de buffer de saudação para logs básicos do Azure.

 Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Atributos:  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.<br /><br /> saudação padrão é 0.|  
|**scheduledTransferLogLevelFilter**|string|Opcional. Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos. valor padrão de saudação é **indefinido**. Outros possíveis valores são **Detalhado**, **Informação**, **Aviso**, **Erro** e **Crítico**.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.<br /><br /> padrão de saudação é PT0S.|  

## <a name="directories-element"></a>Elemento Directories  
Define a configuração de buffer de saudação para logs baseados em arquivo que você pode definir.

Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  


Atributos:  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.<br /><br /> saudação padrão é 0.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.<br /><br /> padrão de saudação é PT0S.|  

## <a name="crashdumps-element"></a>Elemento CrashDumps  
 Define o diretório de despejos de falhas de saudação.

 Elemento pai: [elemento Directories](#Directories).  

Atributos:  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**contêiner**|string|nome de saudação do contêiner de saudação onde o conteúdo de saudação do diretório de saudação é toobe transferidos.|  
|**directoryQuotaInMB**|unsignedInt|Opcional. Especifica o tamanho máximo de saudação do diretório de saudação em megabytes.<br /><br /> saudação padrão é 0.|  

## <a name="failedrequestlogs-element"></a>Elemento FailedRequestLogs  
 Define o diretório de log de solicitação com falha de saudação.

 Elemento pai [elemento Directories](#Directories).  

Atributos:  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**contêiner**|string|nome de saudação do contêiner de saudação onde o conteúdo de saudação do diretório de saudação é toobe transferidos.|  
|**directoryQuotaInMB**|unsignedInt|Opcional. Especifica o tamanho máximo de saudação do diretório de saudação em megabytes.<br /><br /> saudação padrão é 0.|  

##  <a name="iislogs-element"></a>Elemento IISLogs  
 Define o diretório de log do IIS de saudação.

 Elemento pai [elemento Directories](#Directories).  

Atributos:  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**contêiner**|string|nome de saudação do contêiner de saudação onde o conteúdo de saudação do diretório de saudação é toobe transferidos.|  
|**directoryQuotaInMB**|unsignedInt|Opcional. Especifica o tamanho máximo de saudação do diretório de saudação em megabytes.<br /><br /> saudação padrão é 0.|  

## <a name="datasources-element"></a>Elemento DataSources  
 Define zero ou mais diretórios de log adicionais.

 Elemento pai: [elemento Directories](#Directories).

## <a name="directoryconfiguration-element"></a>Elemento DirectoryConfiguration  
 Define o diretório de saudação do toomonitor de arquivos de log.

 Elemento pai: [elemento DataSources](#DataSources).

Atributos:

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**contêiner**|string|nome de saudação do contêiner de saudação onde o conteúdo de saudação do diretório de saudação é toobe transferidos.|  
|**directoryQuotaInMB**|unsignedInt|Opcional. Especifica o tamanho máximo de saudação do diretório de saudação em megabytes.<br /><br /> saudação padrão é 0.|  

## <a name="absolute-element"></a>Elemento Absolute  
 Define um caminho absoluto do hello diretório toomonitor com expansão de ambiente opcional.

 Elemento pai: [elemento DirectoryConfiguration](#DirectoryConfiguration).  

Atributos:  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**path**|string|Obrigatório. Olá caminho absoluto toohello diretório toomonitor.|  
|**expandEnvironment**|Booliano|Obrigatório. Se definir muito**true**, variáveis de ambiente no caminho de saudação são expandidas.|  

## <a name="localresource-element"></a>Elemento LocalResource  
 Define um recurso de local relativo tooa caminho definido na definição de serviço hello.

 Elemento pai: [elemento DirectoryConfiguration](#DirectoryConfiguration).  

Atributos:  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**name**|string|Obrigatório. nome de saudação do recurso de local de Olá que contém a saudação diretório toomonitor.|  
|**relativePath**|string|Obrigatório. Olá toomonitor do caminho relativo toohello recurso local.|  

## <a name="performancecounters-element"></a>Elemento PerformanceCounters  
 Define toocollect de contador de desempenho do hello caminho toohello.

 Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).


 Atributos:  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.<br /><br /> saudação padrão é 0.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.<br /><br /> padrão de saudação é PT0S.|  

## <a name="performancecounterconfiguration-element"></a>Elemento PerformanceCounterConfiguration  
 Define Olá toocollect de contador de desempenho.

 Elemento pai: [elemento PerformanceCounters](#PerformanceCounters).  

 Atributos:  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**counterSpecifier**|string|Obrigatório. Olá toocollect de contador de desempenho do caminho toohello.|  
|**sampleRate**|duration|Obrigatório. taxa de saudação no qual Olá contador de desempenho deve ser coletado.|  

## <a name="windowseventlog-element"></a>Elemento WindowsEventLog  
 Define Olá toomonitor de logs de eventos.

 Elemento pai: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).

  Atributos:

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcional. Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.<br /><br /> saudação padrão é 0.|  
|**scheduledTransferLogLevelFilter**|string|Opcional. Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos. valor padrão de saudação é **indefinido**. Outros possíveis valores são **Detalhado**, **Informação**, **Aviso**, **Erro** e **Crítico**.|  
|**scheduledTransferPeriod**|duration|Opcional. Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.<br /><br /> padrão de saudação é PT0S.|  

## <a name="datasource-element"></a>Elemento DataSource  
 Define Olá toomonitor de log de eventos.

 Elemento pai: [elemento WindowsEventLog](#windowsEventLog).  

 Atributos:

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**name**|string|Obrigatório. Uma expressão XPath especificando Olá toocollect de log.|  
