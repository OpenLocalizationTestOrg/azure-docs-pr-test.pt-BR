---
title: "esquema de configuração 1.3 e posterior da extensão de diagnóstico aaaAzure | Microsoft Docs"
description: "A versão de esquema 1.3 e posterior diagnóstico do Azure fornecido como parte do hello Microsoft Azure SDK 2.4 e posterior."
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
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>Esquema de configuração 1.3 e posterior do Diagnóstico do Azure
> [!NOTE]
> Olá extensão de diagnóstico do Azure é o componente Olá usado toocollect contadores de desempenho e outras estatísticas de:
> - Máquinas Virtuais do Azure 
> - Conjuntos de Escala de Máquina Virtual
> - Service Fabric 
> - Serviços de Nuvem 
> - Grupos de segurança de rede
> 
> Esta página só é relevante se você estiver usando um desses serviços.

Esta página é válida para as versões 1.3 e mais recentes (SDK 2.4 e mais recente do Azure). As seções de configuração mais recentes são comentada tooshow no qual eles foram adicionados a versão.  

arquivo de configuração de saudação descrito aqui é definições de configuração de diagnóstico de tooset usada quando inicia do monitor de diagnósticos de saudação.  

extensão de saudação é usada em conjunto com outros produtos da Microsoft diagnóstico como Monitor do Azure, Application Insights e análise de Log.



Baixe a definição de esquema de arquivo de configuração pública Olá executando Olá comando PowerShell a seguir:  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

Para saber mais sobre como usar o Diagnóstico do Azure, confira [Extensão do Diagnóstico do Azure](azure-diagnostics.md).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Exemplo de arquivo de configuração de diagnóstico Olá  
 saudação de exemplo a seguir mostra um arquivo de configuração de diagnóstico típico:  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
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
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
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

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

Equivalente JSON do arquivo de configuração XML anterior hello. 

Olá PublicConfig e PrivateConfig são separadas porque na maioria dos casos de uso de json, eles são passados como variáveis diferentes. Esses casos incluem modelos do Resource Manager, conjunto de dimensionamento de máquinas virtuais, PowerShell e Visual Studio. 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "ApplicationInsights",
                    "ApplicationInsights": "{Insert InstrumentationKey}",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a>Leitura desta página  
 Olá marcas a seguir são aproximadamente na ordem mostrada na saudação anterior de exemplo.  Se você não vir uma descrição completa em que você espera, pesquise página Olá Olá elemento ou atributo.  

## <a name="common-attribute-types"></a>Tipos comuns de atributo  
 O atributo **scheduledTransferPeriod** aparece em vários elementos. É o intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>Elemento DiagnosticsConfiguration  
 *Árvore: Raiz - DiagnosticsConfiguration*

Adicionado na versão 1.3.  

elemento de nível superior de saudação do arquivo de configuração de diagnóstico de saudação.  

**Atributo** xmlns - Olá namespace XML para o arquivo de configuração de diagnóstico Olá é:  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  


|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**PublicConfig**|Obrigatório. Veja a descrição em outro lugar nesta página.|  
|**PrivateConfig**|Opcional. Veja a descrição em outro lugar nesta página.|  
|**IsEnabled**|Booliano. Veja a descrição em outro lugar nesta página.|  

## <a name="publicconfig-element"></a>Elemento PublicConfig  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig*

 Descreve a configuração de diagnóstico pública hello.  

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**WadCfg**|Obrigatório. Veja a descrição em outro lugar nesta página.|  
|**StorageAccount**|nome de Olá Olá armazenamento do Azure toostore Olá de dados de conta no. Também pode ser especificado como um parâmetro ao executar o cmdlet Olá AzureServiceDiagnosticsExtension conjunto.|  
|**StorageType**|Pode ser *Table*, *Blob* ou *TableAndBlob*. Tabela é o padrão. Quando TableAndBlob for escolhido, dados de diagnóstico são gravados duas vezes, uma vez tooeach tipo.|  
|**LocalResourceDirectory**|diretório de saudação na máquina virtual de saudação onde hello Monitoring Agent armazena dados de evento. Se não, o diretório padrão de saudação definido, é usado:<br /><br /> Para uma função de Trabalho/da Web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Para uma Máquina Virtual: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Os atributos obrigatórios são:<br /><br /> - **caminho** - Olá do hello sistema toobe usado pelo diagnóstico do Azure.<br /><br /> - **expandEnvironment** -controla se as variáveis de ambiente são expandidas no nome do caminho de saudação.|  

## <a name="wadcfg-element"></a>Elemento WadCFG  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG*
 
 Identifica e configura Olá toobe de dados de telemetria coletado.  


## <a name="diagnosticmonitorconfiguration-element"></a>Elemento DiagnosticMonitorConfiguration 
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*

 Obrigatório 

|Atributos|Descrição|  
|----------------|-----------------|  
| **overallQuotaInMB** | quantidade máxima de saudação do espaço em disco local que pode ser consumido por Olá vários tipos de dados de diagnóstico coletados pelo diagnóstico do Azure. configuração do saudação padrão é 5120 MB.<br />
|**useProxyServer** | Defina configurações de servidor de proxy do diagnóstico do Azure toouse Olá conforme definido nas configurações do IE.|  

<br /> <br />

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**CrashDumps**|Veja a descrição em outro lugar nesta página.|  
|**DiagnosticInfrastructureLogs**|Habilite a coleta de logs gerados pelo Diagnóstico do Azure. Olá logs de infraestrutura de diagnóstico são úteis para solucionar Olá sistema de diagnóstico. Os atributos opcionais são:<br /><br /> - **scheduledTransferLogLevelFilter** -configura o nível de severidade mínimo Olá Olá logs coletados.<br /><br /> - **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Diretórios**|Veja a descrição em outro lugar nesta página.|  
|**EtwProviders**|Veja a descrição em outro lugar nesta página.|  
|**Métricas**|Veja a descrição em outro lugar nesta página.|  
|**PerformanceCounters**|Veja a descrição em outro lugar nesta página.|  
|**WindowsEventLog**|Veja a descrição em outro lugar nesta página.| 
|**DockerSources**|Veja a descrição em outro lugar nesta página. | 



## <a name="crashdumps-element"></a>Elemento CrashDumps  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*
 
 Habilite a coleta de saudação de despejos de memória.  

|Atributos|Descrição|  
|----------------|-----------------|  
|**containerName**|Opcional. nome de Olá Olá do contêiner de blob em sua toobe de conta de armazenamento do Azure usado toostore despejos de memória.|  
|**crashDumpType**|Opcional.  Configura o diagnóstico do Azure toocollect completo ou mini despejos de memória.|  
|**directoryQuotaPercentage**|Opcional.  Configura o percentual de saudação do **overallQuotaInMB** toobe reservado para despejos de memória em Olá VM.|  

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|Obrigatório. Define os valores de configuração para cada processo.<br /><br /> Olá atributos a seguir também é necessário:<br /><br /> **processName** - Olá nome do processo de saudação deseja toocollect de diagnóstico do Azure um despejo de memória para.|  

## <a name="directories-element"></a>Elemento Directories 
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories*

 Habilita Olá coleção de conteúdo de saudação de um diretório, os logs de solicitação de acesso e/ou os logs do IIS com falha do IIS.  

 Atributo **scheduledTransferPeriod** opcional. Veja a explicação anterior.  

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**IISLogs**|Incluindo esse elemento na configuração de saudação habilita a coleta de saudação de logs do IIS:<br /><br /> **containerName** -nome Olá Olá do contêiner de blob em sua toobe de conta de armazenamento do Azure usado logs do IIS Olá toostore.|   
|**FailedRequestLogs**|Incluindo esse elemento na configuração de saudação habilita a coleta de logs de aplicativo ou site do IIS tooan solicitações com falha. Você também deve habilitar as opções de rastreamento em **system.WebServer** em **Web.config**.|  
|**DataSources**|Uma lista de diretórios toomonitor.| 




## <a name="datasources-element"></a>Elemento DataSources  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*

 Uma lista de diretórios toomonitor.  

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|Obrigatório. Atributo obrigatório:<br /><br /> **containerName** - Olá nome saudação do contêiner de blob em sua conta de armazenamento do Azure que toobe usados arquivos de log toostore hello.|  





## <a name="directoryconfiguration-element"></a>Elemento DirectoryConfiguration  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*

 Pode incluir qualquer Olá **absoluto** ou **LocalResource** elemento, mas não ambos.  

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**Absolute**|Olá caminho absoluto toohello diretório toomonitor. Olá seguintes atributos é necessário:<br /><br /> - **Caminho** -Olá caminho absoluto toohello diretório toomonitor.<br /><br /> - **expandEnvironment** - configura se as variáveis de ambiente em Path são expandidas ou não.|  
|**LocalResource**|Olá toomonitor do caminho relativo tooa recurso local. Os atributos obrigatórios são:<br /><br /> - **Nome** -Olá recurso local que contém a saudação diretório toomonitor<br /><br /> - **relativePath** -Olá tooName relativo de caminho que contém a saudação diretório toomonitor|  



## <a name="etwproviders-element"></a>Elemento EtwProviders  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*

 Configura a coleta de eventos ETW do EventSource e/ou os provedores baseados no Manifesto ETW.  

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Configura a coleta de eventos gerados desde a [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Atributo obrigatório:<br /><br /> **provedor** -nome da classe de saudação do evento de EventSource hello.<br /><br /> Os atributos opcionais são:<br /><br /> - **scheduledTransferLogLevelFilter** -Olá conta de armazenamento de tooyour de tootransfer nível de severidade mínimo.<br /><br /> - **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|Atributo obrigatório:<br /><br /> **provedor** -Olá GUID do provedor de eventos de saudação<br /><br /> Os atributos opcionais são:<br /><br /> - **scheduledTransferLogLevelFilter** -Olá conta de armazenamento de tooyour de tootransfer nível de severidade mínimo.<br /><br /> - **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>Elemento EtwEventSourceProviderConfiguration  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*

 Configura a coleta de eventos gerados desde a [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).  

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**DefaultEvents**|Atributo opcional:<br/><br/> **eventDestination** - Olá nome hello toostore Olá eventos de tabela em|  
|**Evento**|Atributo obrigatório:<br /><br /> **ID** -id de saudação do evento de saudação.<br /><br /> Atributo opcional:<br /><br /> **eventDestination** - Olá nome hello toostore Olá eventos de tabela em|  



## <a name="etwmanifestproviderconfiguration-element"></a>Elemento EtwManifestProviderConfiguration  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**DefaultEvents**|Atributo opcional:<br /><br /> **eventDestination** - Olá nome hello toostore Olá eventos de tabela em|  
|**Evento**|Atributo obrigatório:<br /><br /> **ID** -id de saudação do evento de saudação.<br /><br /> Atributo opcional:<br /><br /> **eventDestination** - Olá nome hello toostore Olá eventos de tabela em|  



## <a name="metrics-element"></a>Elemento Metrics  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*

 Permite que você toogenerate uma tabela de contador de desempenho é otimizada para consultas rápidas. Cada contador de desempenho que é definido em Olá **PerformanceCounters** elemento é armazenado na tabela de métricas de saudação na tabela de contador de desempenho toohello adição.  

 Olá **resourceId** atributo é necessário.  ID de recurso de saudação do hello Máquina Virtual que você está implantando o diagnóstico do Azure. Obter Olá **resourceID** de saudação [portal do Azure](https://portal.azure.com). Selecione **Procurar** -> **Grupos de Recursos** -> **<Nome\>**. Clique em Olá **propriedades** lado a lado e copie o valor de saudação da saudação **ID** campo.  

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**MetricAggregation**|Atributo obrigatório:<br /><br /> **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto. Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>Elemento PerformanceCounters  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*

 Habilita a coleta de saudação de contadores de desempenho.  

 Atributo opcional:  

 Atributo **scheduledTransferPeriod** opcional. Veja a explicação anterior.

|Elemento filho|Descrição|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|Olá seguintes atributos é necessário:<br /><br /> - **counterSpecifier** - Olá nome saudação do contador de desempenho. Por exemplo: `\Processor(_Total)\% Processor Time`. tooget contadores de uma lista de desempenho em seu host, execute o comando de saudação `typeperf`.<br /><br /> - **sampleRate** -frequência hello contador deve ser testado.<br /><br /> Atributo opcional:<br /><br /> **unidade** -unidade de medida de contador de saudação de saudação.|  




## <a name="windowseventlog-element"></a>Elemento WindowsEventLog
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*
 
 Habilita a coleta de saudação de Logs de eventos do Windows.  

 Atributo **scheduledTransferPeriod** opcional. Veja a explicação anterior.  

|Elemento filho|Descrição|  
|-------------------|-----------------|  
|**DataSource**|toocollect de logs de eventos do Windows Hello. Atributo obrigatório:<br /><br /> **nome** -coletados de consulta do XPath Olá descrevendo toobe de eventos do windows hello. Por exemplo:<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> toocollect todos os eventos, especifique "*"|  




## <a name="logs-element"></a>Elemento Logs  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*

 Presente na versão 1.0 e 1.1. Ausente na 1.2. Adicionado novamente na versão 1.3.  

 Define a configuração de buffer de saudação para logs básicos do Azure.  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|Opcional. Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.<br /><br /> saudação padrão é 0.|  
|**scheduledTransferLogLevelFilterr**|**string**|Opcional. Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos. valor padrão de saudação é **indefinido**, que transfere todos os logs. Outros possíveis valores (na ordem da maioria das informações de tooleast) são **detalhado**, **informações**, **aviso**, **erro**e **Crítico**.|  
|**scheduledTransferPeriod**|**duration**|Opcional. Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.<br /><br /> padrão de saudação é PT0S.|  
|**coletores** Adicionados na 1.5|**string**|Opcional. Pontos tooa coletor local tooalso enviar dados de diagnóstico. Por exemplo, o Application Insights.|  

## <a name="dockersources"></a>DockerSources
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*

 Adicionado na versão 1.9.

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**Stats**|Informa ao sistema Olá toocollect estatísticas para contêineres do Docker|  

## <a name="sinksconfig-element"></a>Elemento SinksConfig  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*

 Uma lista de locais toosend dados tooand Olá configuração de diagnóstico associada nesses locais.  

|Nome do elemento|Descrição|  
|------------------|-----------------|  
|**Coletor**|Veja a descrição em outro lugar nesta página.|  

## <a name="sink-element"></a>Elemento Sink
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*

 Adicionado na versão 1.5.  

 Define os locais toosend dados de diagnóstico. Por exemplo, hello serviço Application Insights.  

|Atributo|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**name**|string|Uma cadeia de caracteres identificação Olá sinkname.|  

|Elemento|Tipo|Descrição|  
|-------------|----------|-----------------|  
|**Application Insights**|string|Usado somente durante o envio de dados tooApplication Insights. Conter Olá chave de instrumentação para uma conta ativa do Application Insights que você tem acesso ao.|  
|**Channels**|string|Uma para cada filtragem adicional que o fluxo que você|  

## <a name="channels-element"></a>Elemento Channels  
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*

 Adicionado na versão 1.5.  

 Define filtros para fluxos de dados de log que passam por um coletor.  

|Elemento|Tipo|Descrição|  
|-------------|----------|-----------------|  
|**Canal**|string|Veja a descrição em outro lugar nesta página.|  

## <a name="channel-element"></a>Elemento Channel
 *Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*

 Adicionado na versão 1.5.  

 Define os locais toosend dados de diagnóstico. Por exemplo, hello serviço Application Insights.  

|Atributos|Tipo|Descrição|  
|----------------|----------|-----------------|  
|**logLevel**|**string**|Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos. valor padrão de saudação é **indefinido**, que transfere todos os logs. Outros possíveis valores (na ordem da maioria das informações de tooleast) são **detalhado**, **informações**, **aviso**, **erro**e **Crítico**.|  
|**name**|**string**|Um nome exclusivo da saudação canal toorefer para|  


## <a name="privateconfig-element"></a>Elemento PrivateConfig 
 *Árvore: Raiz - DiagnosticsConfiguration - PrivateConfig*

 Adicionado na versão 1.3.  

 Opcional  

 Armazena detalhes de privada Olá Olá da conta de armazenamento (nome da chave e ponto de extremidade). Essas informações são enviadas a máquina virtual de toohello, mas não podem ser recuperadas.  

|Elementos filho|Descrição|  
|--------------------|-----------------|  
|**StorageAccount**|Olá toouse de conta de armazenamento. Olá seguintes atributos é necessário<br /><br /> - **nome** - Olá nome hello da conta de armazenamento.<br /><br /> - **chave** - Olá toohello conta de armazenamento de chave.<br /><br /> - **ponto de extremidade** -tooaccess de ponto de extremidade Olá Olá conta de armazenamento. <br /><br /> -**sasToken** (adicionado 1.8.1)-, você pode especificar um token SAS em vez de uma chave de conta de armazenamento na configuração privada hello. Se fornecido, a chave de conta de armazenamento Olá é ignorado. <br />Requisitos para Olá Token SAS: <br />– Oferece suporte apenas ao token SAS da conta <br />Os tipos de serviço - *b*, *t* são obrigatórios. <br /> As permissões - *a*, *c*, *u*, *w* são obrigatórias. <br /> Os tipos de recurso - *c*, *o* são obrigatórios. <br /> -Oferece suporte ao protocolo HTTPS de saudação apenas <br /> – A hora de início e de expiração deve ser válida.|  


## <a name="isenabled-element"></a>Elemento IsEnabled  
 *Árvore: Raiz - DiagnosticsConfiguration - IsEnabled*

 Booliano. Use `true` tooenable diagnóstico de saudação ou `false` toodisable diagnóstico de saudação.
