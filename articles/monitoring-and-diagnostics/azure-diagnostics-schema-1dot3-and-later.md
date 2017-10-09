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
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="b373b-103">Esquema de configuração 1.3 e posterior do Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="b373b-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="b373b-104">Olá extensão de diagnóstico do Azure é o componente Olá usado toocollect contadores de desempenho e outras estatísticas de:</span><span class="sxs-lookup"><span data-stu-id="b373b-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="b373b-105">Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="b373b-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="b373b-106">Conjuntos de Escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="b373b-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="b373b-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b373b-107">Service Fabric</span></span> 
> - <span data-ttu-id="b373b-108">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="b373b-108">Cloud Services</span></span> 
> - <span data-ttu-id="b373b-109">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="b373b-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="b373b-110">Esta página só é relevante se você estiver usando um desses serviços.</span><span class="sxs-lookup"><span data-stu-id="b373b-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="b373b-111">Esta página é válida para as versões 1.3 e mais recentes (SDK 2.4 e mais recente do Azure).</span><span class="sxs-lookup"><span data-stu-id="b373b-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="b373b-112">As seções de configuração mais recentes são comentada tooshow no qual eles foram adicionados a versão.</span><span class="sxs-lookup"><span data-stu-id="b373b-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="b373b-113">arquivo de configuração de saudação descrito aqui é definições de configuração de diagnóstico de tooset usada quando inicia do monitor de diagnósticos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b373b-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="b373b-114">extensão de saudação é usada em conjunto com outros produtos da Microsoft diagnóstico como Monitor do Azure, Application Insights e análise de Log.</span><span class="sxs-lookup"><span data-stu-id="b373b-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="b373b-115">Baixe a definição de esquema de arquivo de configuração pública Olá executando Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="b373b-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="b373b-116">Para saber mais sobre como usar o Diagnóstico do Azure, confira [Extensão do Diagnóstico do Azure](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b373b-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="b373b-117">Exemplo de arquivo de configuração de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="b373b-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="b373b-118">saudação de exemplo a seguir mostra um arquivo de configuração de diagnóstico típico:</span><span class="sxs-lookup"><span data-stu-id="b373b-118">hello following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="b373b-119">Equivalente JSON do arquivo de configuração XML anterior hello.</span><span class="sxs-lookup"><span data-stu-id="b373b-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="b373b-120">Olá PublicConfig e PrivateConfig são separadas porque na maioria dos casos de uso de json, eles são passados como variáveis diferentes.</span><span class="sxs-lookup"><span data-stu-id="b373b-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="b373b-121">Esses casos incluem modelos do Resource Manager, conjunto de dimensionamento de máquinas virtuais, PowerShell e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b373b-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="b373b-122">Leitura desta página</span><span class="sxs-lookup"><span data-stu-id="b373b-122">Reading this page</span></span>  
 <span data-ttu-id="b373b-123">Olá marcas a seguir são aproximadamente na ordem mostrada na saudação anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b373b-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="b373b-124">Se você não vir uma descrição completa em que você espera, pesquise página Olá Olá elemento ou atributo.</span><span class="sxs-lookup"><span data-stu-id="b373b-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="b373b-125">Tipos comuns de atributo</span><span class="sxs-lookup"><span data-stu-id="b373b-125">Common Attribute Types</span></span>  
 <span data-ttu-id="b373b-126">O atributo **scheduledTransferPeriod** aparece em vários elementos.</span><span class="sxs-lookup"><span data-stu-id="b373b-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="b373b-127">É o intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="b373b-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="b373b-128">Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="b373b-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="b373b-129">Elemento DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="b373b-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="b373b-130">*Árvore: Raiz - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="b373b-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="b373b-131">Adicionado na versão 1.3.</span><span class="sxs-lookup"><span data-stu-id="b373b-131">Added in version 1.3.</span></span>  

<span data-ttu-id="b373b-132">elemento de nível superior de saudação do arquivo de configuração de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="b373b-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="b373b-133">**Atributo** xmlns - Olá namespace XML para o arquivo de configuração de diagnóstico Olá é:</span><span class="sxs-lookup"><span data-stu-id="b373b-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="b373b-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="b373b-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="b373b-135">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-135">Child Elements</span></span>|<span data-ttu-id="b373b-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="b373b-137">**PublicConfig**</span></span>|<span data-ttu-id="b373b-138">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b373b-138">Required.</span></span> <span data-ttu-id="b373b-139">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="b373b-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="b373b-140">**PrivateConfig**</span></span>|<span data-ttu-id="b373b-141">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-141">Optional.</span></span> <span data-ttu-id="b373b-142">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="b373b-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="b373b-143">**IsEnabled**</span></span>|<span data-ttu-id="b373b-144">Booliano.</span><span class="sxs-lookup"><span data-stu-id="b373b-144">Boolean.</span></span> <span data-ttu-id="b373b-145">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="b373b-146">Elemento PublicConfig</span><span class="sxs-lookup"><span data-stu-id="b373b-146">PublicConfig Element</span></span>  
 <span data-ttu-id="b373b-147">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="b373b-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="b373b-148">Descreve a configuração de diagnóstico pública hello.</span><span class="sxs-lookup"><span data-stu-id="b373b-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="b373b-149">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-149">Child Elements</span></span>|<span data-ttu-id="b373b-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="b373b-151">**WadCfg**</span></span>|<span data-ttu-id="b373b-152">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b373b-152">Required.</span></span> <span data-ttu-id="b373b-153">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="b373b-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="b373b-154">**StorageAccount**</span></span>|<span data-ttu-id="b373b-155">nome de Olá Olá armazenamento do Azure toostore Olá de dados de conta no.</span><span class="sxs-lookup"><span data-stu-id="b373b-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="b373b-156">Também pode ser especificado como um parâmetro ao executar o cmdlet Olá AzureServiceDiagnosticsExtension conjunto.</span><span class="sxs-lookup"><span data-stu-id="b373b-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="b373b-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="b373b-157">**StorageType**</span></span>|<span data-ttu-id="b373b-158">Pode ser *Table*, *Blob* ou *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="b373b-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="b373b-159">Tabela é o padrão.</span><span class="sxs-lookup"><span data-stu-id="b373b-159">Table is default.</span></span> <span data-ttu-id="b373b-160">Quando TableAndBlob for escolhido, dados de diagnóstico são gravados duas vezes, uma vez tooeach tipo.</span><span class="sxs-lookup"><span data-stu-id="b373b-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="b373b-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="b373b-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="b373b-162">diretório de saudação na máquina virtual de saudação onde hello Monitoring Agent armazena dados de evento.</span><span class="sxs-lookup"><span data-stu-id="b373b-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="b373b-163">Se não, o diretório padrão de saudação definido, é usado:</span><span class="sxs-lookup"><span data-stu-id="b373b-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="b373b-164">Para uma função de Trabalho/da Web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="b373b-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="b373b-165">Para uma Máquina Virtual: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="b373b-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="b373b-166">Os atributos obrigatórios são:</span><span class="sxs-lookup"><span data-stu-id="b373b-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="b373b-167">- **caminho** - Olá do hello sistema toobe usado pelo diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="b373b-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="b373b-168">- **expandEnvironment** -controla se as variáveis de ambiente são expandidas no nome do caminho de saudação.</span><span class="sxs-lookup"><span data-stu-id="b373b-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="b373b-169">Elemento WadCFG</span><span class="sxs-lookup"><span data-stu-id="b373b-169">WadCFG Element</span></span>  
 <span data-ttu-id="b373b-170">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="b373b-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="b373b-171">Identifica e configura Olá toobe de dados de telemetria coletado.</span><span class="sxs-lookup"><span data-stu-id="b373b-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="b373b-172">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="b373b-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="b373b-173">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="b373b-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="b373b-174">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b373b-174">Required</span></span> 

|<span data-ttu-id="b373b-175">Atributos</span><span class="sxs-lookup"><span data-stu-id="b373b-175">Attributes</span></span>|<span data-ttu-id="b373b-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="b373b-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="b373b-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="b373b-178">quantidade máxima de saudação do espaço em disco local que pode ser consumido por Olá vários tipos de dados de diagnóstico coletados pelo diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="b373b-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="b373b-179">configuração do saudação padrão é 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="b373b-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="b373b-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="b373b-180">**useProxyServer**</span></span> | <span data-ttu-id="b373b-181">Defina configurações de servidor de proxy do diagnóstico do Azure toouse Olá conforme definido nas configurações do IE.</span><span class="sxs-lookup"><span data-stu-id="b373b-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="b373b-182">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-182">Child Elements</span></span>|<span data-ttu-id="b373b-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="b373b-184">**CrashDumps**</span></span>|<span data-ttu-id="b373b-185">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="b373b-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="b373b-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="b373b-187">Habilite a coleta de logs gerados pelo Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="b373b-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="b373b-188">Olá logs de infraestrutura de diagnóstico são úteis para solucionar Olá sistema de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b373b-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="b373b-189">Os atributos opcionais são:</span><span class="sxs-lookup"><span data-stu-id="b373b-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="b373b-190">- **scheduledTransferLogLevelFilter** -configura o nível de severidade mínimo Olá Olá logs coletados.</span><span class="sxs-lookup"><span data-stu-id="b373b-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="b373b-191">- **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="b373b-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="b373b-192">Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="b373b-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="b373b-193">**Diretórios**</span><span class="sxs-lookup"><span data-stu-id="b373b-193">**Directories**</span></span>|<span data-ttu-id="b373b-194">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="b373b-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="b373b-195">**EtwProviders**</span></span>|<span data-ttu-id="b373b-196">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="b373b-197">**Métricas**</span><span class="sxs-lookup"><span data-stu-id="b373b-197">**Metrics**</span></span>|<span data-ttu-id="b373b-198">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="b373b-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="b373b-199">**PerformanceCounters**</span></span>|<span data-ttu-id="b373b-200">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="b373b-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="b373b-201">**WindowsEventLog**</span></span>|<span data-ttu-id="b373b-202">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="b373b-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="b373b-203">**DockerSources**</span></span>|<span data-ttu-id="b373b-204">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="b373b-205">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="b373b-205">CrashDumps Element</span></span>  
 <span data-ttu-id="b373b-206">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="b373b-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="b373b-207">Habilite a coleta de saudação de despejos de memória.</span><span class="sxs-lookup"><span data-stu-id="b373b-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="b373b-208">Atributos</span><span class="sxs-lookup"><span data-stu-id="b373b-208">Attributes</span></span>|<span data-ttu-id="b373b-209">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="b373b-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="b373b-210">**containerName**</span></span>|<span data-ttu-id="b373b-211">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-211">Optional.</span></span> <span data-ttu-id="b373b-212">nome de Olá Olá do contêiner de blob em sua toobe de conta de armazenamento do Azure usado toostore despejos de memória.</span><span class="sxs-lookup"><span data-stu-id="b373b-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="b373b-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="b373b-213">**crashDumpType**</span></span>|<span data-ttu-id="b373b-214">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-214">Optional.</span></span>  <span data-ttu-id="b373b-215">Configura o diagnóstico do Azure toocollect completo ou mini despejos de memória.</span><span class="sxs-lookup"><span data-stu-id="b373b-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="b373b-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="b373b-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="b373b-217">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-217">Optional.</span></span>  <span data-ttu-id="b373b-218">Configura o percentual de saudação do **overallQuotaInMB** toobe reservado para despejos de memória em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b373b-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="b373b-219">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-219">Child Elements</span></span>|<span data-ttu-id="b373b-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="b373b-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="b373b-222">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b373b-222">Required.</span></span> <span data-ttu-id="b373b-223">Define os valores de configuração para cada processo.</span><span class="sxs-lookup"><span data-stu-id="b373b-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="b373b-224">Olá atributos a seguir também é necessário:</span><span class="sxs-lookup"><span data-stu-id="b373b-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="b373b-225">**processName** - Olá nome do processo de saudação deseja toocollect de diagnóstico do Azure um despejo de memória para.</span><span class="sxs-lookup"><span data-stu-id="b373b-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="b373b-226">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="b373b-226">Directories Element</span></span> 
 <span data-ttu-id="b373b-227">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories*</span><span class="sxs-lookup"><span data-stu-id="b373b-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="b373b-228">Habilita Olá coleção de conteúdo de saudação de um diretório, os logs de solicitação de acesso e/ou os logs do IIS com falha do IIS.</span><span class="sxs-lookup"><span data-stu-id="b373b-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="b373b-229">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="b373b-230">Veja a explicação anterior.</span><span class="sxs-lookup"><span data-stu-id="b373b-230">See explanation earlier.</span></span>  

|<span data-ttu-id="b373b-231">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-231">Child Elements</span></span>|<span data-ttu-id="b373b-232">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="b373b-233">**IISLogs**</span></span>|<span data-ttu-id="b373b-234">Incluindo esse elemento na configuração de saudação habilita a coleta de saudação de logs do IIS:</span><span class="sxs-lookup"><span data-stu-id="b373b-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="b373b-235">**containerName** -nome Olá Olá do contêiner de blob em sua toobe de conta de armazenamento do Azure usado logs do IIS Olá toostore.</span><span class="sxs-lookup"><span data-stu-id="b373b-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="b373b-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="b373b-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="b373b-237">Incluindo esse elemento na configuração de saudação habilita a coleta de logs de aplicativo ou site do IIS tooan solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="b373b-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="b373b-238">Você também deve habilitar as opções de rastreamento em **system.WebServer** em **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="b373b-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="b373b-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="b373b-239">**DataSources**</span></span>|<span data-ttu-id="b373b-240">Uma lista de diretórios toomonitor.</span><span class="sxs-lookup"><span data-stu-id="b373b-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="b373b-241">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="b373b-241">DataSources Element</span></span>  
 <span data-ttu-id="b373b-242">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="b373b-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="b373b-243">Uma lista de diretórios toomonitor.</span><span class="sxs-lookup"><span data-stu-id="b373b-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="b373b-244">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-244">Child Elements</span></span>|<span data-ttu-id="b373b-245">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="b373b-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="b373b-247">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b373b-247">Required.</span></span> <span data-ttu-id="b373b-248">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="b373b-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="b373b-249">**containerName** - Olá nome saudação do contêiner de blob em sua conta de armazenamento do Azure que toobe usados arquivos de log toostore hello.</span><span class="sxs-lookup"><span data-stu-id="b373b-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="b373b-250">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="b373b-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="b373b-251">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="b373b-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="b373b-252">Pode incluir qualquer Olá **absoluto** ou **LocalResource** elemento, mas não ambos.</span><span class="sxs-lookup"><span data-stu-id="b373b-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="b373b-253">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-253">Child Elements</span></span>|<span data-ttu-id="b373b-254">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="b373b-255">**Absolute**</span></span>|<span data-ttu-id="b373b-256">Olá caminho absoluto toohello diretório toomonitor.</span><span class="sxs-lookup"><span data-stu-id="b373b-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="b373b-257">Olá seguintes atributos é necessário:</span><span class="sxs-lookup"><span data-stu-id="b373b-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="b373b-258">- **Caminho** -Olá caminho absoluto toohello diretório toomonitor.</span><span class="sxs-lookup"><span data-stu-id="b373b-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="b373b-259">- **expandEnvironment** - configura se as variáveis de ambiente em Path são expandidas ou não.</span><span class="sxs-lookup"><span data-stu-id="b373b-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="b373b-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="b373b-260">**LocalResource**</span></span>|<span data-ttu-id="b373b-261">Olá toomonitor do caminho relativo tooa recurso local.</span><span class="sxs-lookup"><span data-stu-id="b373b-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="b373b-262">Os atributos obrigatórios são:</span><span class="sxs-lookup"><span data-stu-id="b373b-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="b373b-263">- **Nome** -Olá recurso local que contém a saudação diretório toomonitor</span><span class="sxs-lookup"><span data-stu-id="b373b-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="b373b-264">- **relativePath** -Olá tooName relativo de caminho que contém a saudação diretório toomonitor</span><span class="sxs-lookup"><span data-stu-id="b373b-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="b373b-265">Elemento EtwProviders</span><span class="sxs-lookup"><span data-stu-id="b373b-265">EtwProviders Element</span></span>  
 <span data-ttu-id="b373b-266">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="b373b-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="b373b-267">Configura a coleta de eventos ETW do EventSource e/ou os provedores baseados no Manifesto ETW.</span><span class="sxs-lookup"><span data-stu-id="b373b-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="b373b-268">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-268">Child Elements</span></span>|<span data-ttu-id="b373b-269">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="b373b-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="b373b-271">Configura a coleta de eventos gerados desde a [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="b373b-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="b373b-272">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="b373b-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="b373b-273">**provedor** -nome da classe de saudação do evento de EventSource hello.</span><span class="sxs-lookup"><span data-stu-id="b373b-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="b373b-274">Os atributos opcionais são:</span><span class="sxs-lookup"><span data-stu-id="b373b-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="b373b-275">- **scheduledTransferLogLevelFilter** -Olá conta de armazenamento de tooyour de tootransfer nível de severidade mínimo.</span><span class="sxs-lookup"><span data-stu-id="b373b-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="b373b-276">- **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="b373b-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="b373b-277">Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="b373b-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="b373b-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="b373b-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="b373b-279">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="b373b-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="b373b-280">**provedor** -Olá GUID do provedor de eventos de saudação</span><span class="sxs-lookup"><span data-stu-id="b373b-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="b373b-281">Os atributos opcionais são:</span><span class="sxs-lookup"><span data-stu-id="b373b-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="b373b-282">- **scheduledTransferLogLevelFilter** -Olá conta de armazenamento de tooyour de tootransfer nível de severidade mínimo.</span><span class="sxs-lookup"><span data-stu-id="b373b-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="b373b-283">- **scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="b373b-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="b373b-284">Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="b373b-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="b373b-285">Elemento EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="b373b-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="b373b-286">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="b373b-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="b373b-287">Configura a coleta de eventos gerados desde a [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="b373b-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="b373b-288">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-288">Child Elements</span></span>|<span data-ttu-id="b373b-289">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="b373b-290">**DefaultEvents**</span></span>|<span data-ttu-id="b373b-291">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="b373b-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="b373b-292">**eventDestination** - Olá nome hello toostore Olá eventos de tabela em</span><span class="sxs-lookup"><span data-stu-id="b373b-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="b373b-293">**Evento**</span><span class="sxs-lookup"><span data-stu-id="b373b-293">**Event**</span></span>|<span data-ttu-id="b373b-294">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="b373b-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="b373b-295">**ID** -id de saudação do evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="b373b-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="b373b-296">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="b373b-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="b373b-297">**eventDestination** - Olá nome hello toostore Olá eventos de tabela em</span><span class="sxs-lookup"><span data-stu-id="b373b-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="b373b-298">Elemento EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="b373b-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="b373b-299">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="b373b-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="b373b-300">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-300">Child Elements</span></span>|<span data-ttu-id="b373b-301">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="b373b-302">**DefaultEvents**</span></span>|<span data-ttu-id="b373b-303">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="b373b-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="b373b-304">**eventDestination** - Olá nome hello toostore Olá eventos de tabela em</span><span class="sxs-lookup"><span data-stu-id="b373b-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="b373b-305">**Evento**</span><span class="sxs-lookup"><span data-stu-id="b373b-305">**Event**</span></span>|<span data-ttu-id="b373b-306">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="b373b-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="b373b-307">**ID** -id de saudação do evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="b373b-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="b373b-308">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="b373b-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="b373b-309">**eventDestination** - Olá nome hello toostore Olá eventos de tabela em</span><span class="sxs-lookup"><span data-stu-id="b373b-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="b373b-310">Elemento Metrics</span><span class="sxs-lookup"><span data-stu-id="b373b-310">Metrics Element</span></span>  
 <span data-ttu-id="b373b-311">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="b373b-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="b373b-312">Permite que você toogenerate uma tabela de contador de desempenho é otimizada para consultas rápidas.</span><span class="sxs-lookup"><span data-stu-id="b373b-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="b373b-313">Cada contador de desempenho que é definido em Olá **PerformanceCounters** elemento é armazenado na tabela de métricas de saudação na tabela de contador de desempenho toohello adição.</span><span class="sxs-lookup"><span data-stu-id="b373b-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="b373b-314">Olá **resourceId** atributo é necessário.</span><span class="sxs-lookup"><span data-stu-id="b373b-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="b373b-315">ID de recurso de saudação do hello Máquina Virtual que você está implantando o diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="b373b-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="b373b-316">Obter Olá **resourceID** de saudação [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b373b-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b373b-317">Selecione **Procurar** -> **Grupos de Recursos** -> **<Nome\>**.</span><span class="sxs-lookup"><span data-stu-id="b373b-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="b373b-318">Clique em Olá **propriedades** lado a lado e copie o valor de saudação da saudação **ID** campo.</span><span class="sxs-lookup"><span data-stu-id="b373b-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="b373b-319">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-319">Child Elements</span></span>|<span data-ttu-id="b373b-320">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="b373b-321">**MetricAggregation**</span></span>|<span data-ttu-id="b373b-322">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="b373b-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="b373b-323">**scheduledTransferPeriod** -intervalo de saudação entre transferências agendadas toostorage arredondado toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="b373b-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="b373b-324">Olá valor é um [XML "Tipo de dados de duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="b373b-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="b373b-325">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="b373b-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="b373b-326">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="b373b-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="b373b-327">Habilita a coleta de saudação de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="b373b-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="b373b-328">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="b373b-328">Optional attribute:</span></span>  

 <span data-ttu-id="b373b-329">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="b373b-330">Veja a explicação anterior.</span><span class="sxs-lookup"><span data-stu-id="b373b-330">See explanation earlier.</span></span>

|<span data-ttu-id="b373b-331">Elemento filho</span><span class="sxs-lookup"><span data-stu-id="b373b-331">Child Element</span></span>|<span data-ttu-id="b373b-332">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="b373b-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="b373b-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="b373b-334">Olá seguintes atributos é necessário:</span><span class="sxs-lookup"><span data-stu-id="b373b-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="b373b-335">- **counterSpecifier** - Olá nome saudação do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="b373b-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="b373b-336">Por exemplo: `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="b373b-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="b373b-337">tooget contadores de uma lista de desempenho em seu host, execute o comando de saudação `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="b373b-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="b373b-338">- **sampleRate** -frequência hello contador deve ser testado.</span><span class="sxs-lookup"><span data-stu-id="b373b-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="b373b-339">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="b373b-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="b373b-340">**unidade** -unidade de medida de contador de saudação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b373b-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="b373b-341">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="b373b-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="b373b-342">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="b373b-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="b373b-343">Habilita a coleta de saudação de Logs de eventos do Windows.</span><span class="sxs-lookup"><span data-stu-id="b373b-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="b373b-344">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="b373b-345">Veja a explicação anterior.</span><span class="sxs-lookup"><span data-stu-id="b373b-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="b373b-346">Elemento filho</span><span class="sxs-lookup"><span data-stu-id="b373b-346">Child Element</span></span>|<span data-ttu-id="b373b-347">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="b373b-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="b373b-348">**DataSource**</span></span>|<span data-ttu-id="b373b-349">toocollect de logs de eventos do Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="b373b-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="b373b-350">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="b373b-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="b373b-351">**nome** -coletados de consulta do XPath Olá descrevendo toobe de eventos do windows hello.</span><span class="sxs-lookup"><span data-stu-id="b373b-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="b373b-352">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b373b-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="b373b-353">toocollect todos os eventos, especifique "*"</span><span class="sxs-lookup"><span data-stu-id="b373b-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="b373b-354">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="b373b-354">Logs Element</span></span>  
 <span data-ttu-id="b373b-355">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="b373b-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="b373b-356">Presente na versão 1.0 e 1.1.</span><span class="sxs-lookup"><span data-stu-id="b373b-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="b373b-357">Ausente na 1.2.</span><span class="sxs-lookup"><span data-stu-id="b373b-357">Missing in 1.2.</span></span> <span data-ttu-id="b373b-358">Adicionado novamente na versão 1.3.</span><span class="sxs-lookup"><span data-stu-id="b373b-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="b373b-359">Define a configuração de buffer de saudação para logs básicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b373b-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="b373b-360">Atributo</span><span class="sxs-lookup"><span data-stu-id="b373b-360">Attribute</span></span>|<span data-ttu-id="b373b-361">Tipo</span><span class="sxs-lookup"><span data-stu-id="b373b-361">Type</span></span>|<span data-ttu-id="b373b-362">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="b373b-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="b373b-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="b373b-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="b373b-364">**unsignedInt**</span></span>|<span data-ttu-id="b373b-365">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-365">Optional.</span></span> <span data-ttu-id="b373b-366">Especifica a quantidade máxima de saudação do armazenamento de sistema de arquivos está disponível para Olá especificado dados.</span><span class="sxs-lookup"><span data-stu-id="b373b-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="b373b-367">saudação padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="b373b-367">hello default is 0.</span></span>|  
|<span data-ttu-id="b373b-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="b373b-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="b373b-369">**string**</span><span class="sxs-lookup"><span data-stu-id="b373b-369">**string**</span></span>|<span data-ttu-id="b373b-370">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-370">Optional.</span></span> <span data-ttu-id="b373b-371">Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos.</span><span class="sxs-lookup"><span data-stu-id="b373b-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="b373b-372">valor padrão de saudação é **indefinido**, que transfere todos os logs.</span><span class="sxs-lookup"><span data-stu-id="b373b-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="b373b-373">Outros possíveis valores (na ordem da maioria das informações de tooleast) são **detalhado**, **informações**, **aviso**, **erro**e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="b373b-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="b373b-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="b373b-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="b373b-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="b373b-375">**duration**</span></span>|<span data-ttu-id="b373b-376">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-376">Optional.</span></span> <span data-ttu-id="b373b-377">Especifica o intervalo de saudação entre transferências agendadas de dados, arredondados para cima toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="b373b-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="b373b-378">padrão de saudação é PT0S.</span><span class="sxs-lookup"><span data-stu-id="b373b-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="b373b-379">**coletores** Adicionados na 1.5</span><span class="sxs-lookup"><span data-stu-id="b373b-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="b373b-380">**string**</span><span class="sxs-lookup"><span data-stu-id="b373b-380">**string**</span></span>|<span data-ttu-id="b373b-381">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b373b-381">Optional.</span></span> <span data-ttu-id="b373b-382">Pontos tooa coletor local tooalso enviar dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b373b-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="b373b-383">Por exemplo, o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b373b-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="b373b-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="b373b-384">DockerSources</span></span>
 <span data-ttu-id="b373b-385">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="b373b-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="b373b-386">Adicionado na versão 1.9.</span><span class="sxs-lookup"><span data-stu-id="b373b-386">Added in 1.9.</span></span>

|<span data-ttu-id="b373b-387">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="b373b-387">Element Name</span></span>|<span data-ttu-id="b373b-388">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="b373b-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="b373b-389">**Stats**</span></span>|<span data-ttu-id="b373b-390">Informa ao sistema Olá toocollect estatísticas para contêineres do Docker</span><span class="sxs-lookup"><span data-stu-id="b373b-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="b373b-391">Elemento SinksConfig</span><span class="sxs-lookup"><span data-stu-id="b373b-391">SinksConfig Element</span></span>  
 <span data-ttu-id="b373b-392">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="b373b-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="b373b-393">Uma lista de locais toosend dados tooand Olá configuração de diagnóstico associada nesses locais.</span><span class="sxs-lookup"><span data-stu-id="b373b-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="b373b-394">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="b373b-394">Element Name</span></span>|<span data-ttu-id="b373b-395">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="b373b-396">**Coletor**</span><span class="sxs-lookup"><span data-stu-id="b373b-396">**Sink**</span></span>|<span data-ttu-id="b373b-397">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="b373b-398">Elemento Sink</span><span class="sxs-lookup"><span data-stu-id="b373b-398">Sink Element</span></span>
 <span data-ttu-id="b373b-399">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="b373b-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="b373b-400">Adicionado na versão 1.5.</span><span class="sxs-lookup"><span data-stu-id="b373b-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="b373b-401">Define os locais toosend dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b373b-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="b373b-402">Por exemplo, hello serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b373b-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="b373b-403">Atributo</span><span class="sxs-lookup"><span data-stu-id="b373b-403">Attribute</span></span>|<span data-ttu-id="b373b-404">Tipo</span><span class="sxs-lookup"><span data-stu-id="b373b-404">Type</span></span>|<span data-ttu-id="b373b-405">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="b373b-406">**name**</span><span class="sxs-lookup"><span data-stu-id="b373b-406">**name**</span></span>|<span data-ttu-id="b373b-407">string</span><span class="sxs-lookup"><span data-stu-id="b373b-407">string</span></span>|<span data-ttu-id="b373b-408">Uma cadeia de caracteres identificação Olá sinkname.</span><span class="sxs-lookup"><span data-stu-id="b373b-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="b373b-409">Elemento</span><span class="sxs-lookup"><span data-stu-id="b373b-409">Element</span></span>|<span data-ttu-id="b373b-410">Tipo</span><span class="sxs-lookup"><span data-stu-id="b373b-410">Type</span></span>|<span data-ttu-id="b373b-411">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="b373b-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="b373b-412">**Application Insights**</span></span>|<span data-ttu-id="b373b-413">string</span><span class="sxs-lookup"><span data-stu-id="b373b-413">string</span></span>|<span data-ttu-id="b373b-414">Usado somente durante o envio de dados tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="b373b-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="b373b-415">Conter Olá chave de instrumentação para uma conta ativa do Application Insights que você tem acesso ao.</span><span class="sxs-lookup"><span data-stu-id="b373b-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="b373b-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="b373b-416">**Channels**</span></span>|<span data-ttu-id="b373b-417">string</span><span class="sxs-lookup"><span data-stu-id="b373b-417">string</span></span>|<span data-ttu-id="b373b-418">Uma para cada filtragem adicional que o fluxo que você</span><span class="sxs-lookup"><span data-stu-id="b373b-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="b373b-419">Elemento Channels</span><span class="sxs-lookup"><span data-stu-id="b373b-419">Channels Element</span></span>  
 <span data-ttu-id="b373b-420">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="b373b-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="b373b-421">Adicionado na versão 1.5.</span><span class="sxs-lookup"><span data-stu-id="b373b-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="b373b-422">Define filtros para fluxos de dados de log que passam por um coletor.</span><span class="sxs-lookup"><span data-stu-id="b373b-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="b373b-423">Elemento</span><span class="sxs-lookup"><span data-stu-id="b373b-423">Element</span></span>|<span data-ttu-id="b373b-424">Tipo</span><span class="sxs-lookup"><span data-stu-id="b373b-424">Type</span></span>|<span data-ttu-id="b373b-425">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="b373b-426">**Canal**</span><span class="sxs-lookup"><span data-stu-id="b373b-426">**Channel**</span></span>|<span data-ttu-id="b373b-427">string</span><span class="sxs-lookup"><span data-stu-id="b373b-427">string</span></span>|<span data-ttu-id="b373b-428">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="b373b-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="b373b-429">Elemento Channel</span><span class="sxs-lookup"><span data-stu-id="b373b-429">Channel Element</span></span>
 <span data-ttu-id="b373b-430">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="b373b-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="b373b-431">Adicionado na versão 1.5.</span><span class="sxs-lookup"><span data-stu-id="b373b-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="b373b-432">Define os locais toosend dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b373b-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="b373b-433">Por exemplo, hello serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b373b-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="b373b-434">Atributos</span><span class="sxs-lookup"><span data-stu-id="b373b-434">Attributes</span></span>|<span data-ttu-id="b373b-435">Tipo</span><span class="sxs-lookup"><span data-stu-id="b373b-435">Type</span></span>|<span data-ttu-id="b373b-436">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="b373b-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="b373b-437">**logLevel**</span></span>|<span data-ttu-id="b373b-438">**string**</span><span class="sxs-lookup"><span data-stu-id="b373b-438">**string**</span></span>|<span data-ttu-id="b373b-439">Especifica o nível de severidade mínimo Olá para entradas de log que são transferidos.</span><span class="sxs-lookup"><span data-stu-id="b373b-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="b373b-440">valor padrão de saudação é **indefinido**, que transfere todos os logs.</span><span class="sxs-lookup"><span data-stu-id="b373b-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="b373b-441">Outros possíveis valores (na ordem da maioria das informações de tooleast) são **detalhado**, **informações**, **aviso**, **erro**e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="b373b-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="b373b-442">**name**</span><span class="sxs-lookup"><span data-stu-id="b373b-442">**name**</span></span>|<span data-ttu-id="b373b-443">**string**</span><span class="sxs-lookup"><span data-stu-id="b373b-443">**string**</span></span>|<span data-ttu-id="b373b-444">Um nome exclusivo da saudação canal toorefer para</span><span class="sxs-lookup"><span data-stu-id="b373b-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="b373b-445">Elemento PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="b373b-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="b373b-446">*Árvore: Raiz - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="b373b-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="b373b-447">Adicionado na versão 1.3.</span><span class="sxs-lookup"><span data-stu-id="b373b-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="b373b-448">Opcional</span><span class="sxs-lookup"><span data-stu-id="b373b-448">Optional</span></span>  

 <span data-ttu-id="b373b-449">Armazena detalhes de privada Olá Olá da conta de armazenamento (nome da chave e ponto de extremidade).</span><span class="sxs-lookup"><span data-stu-id="b373b-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="b373b-450">Essas informações são enviadas a máquina virtual de toohello, mas não podem ser recuperadas.</span><span class="sxs-lookup"><span data-stu-id="b373b-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="b373b-451">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="b373b-451">Child Elements</span></span>|<span data-ttu-id="b373b-452">Descrição</span><span class="sxs-lookup"><span data-stu-id="b373b-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="b373b-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="b373b-453">**StorageAccount**</span></span>|<span data-ttu-id="b373b-454">Olá toouse de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b373b-454">hello storage account toouse.</span></span> <span data-ttu-id="b373b-455">Olá seguintes atributos é necessário</span><span class="sxs-lookup"><span data-stu-id="b373b-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="b373b-456">- **nome** - Olá nome hello da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b373b-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="b373b-457">- **chave** - Olá toohello conta de armazenamento de chave.</span><span class="sxs-lookup"><span data-stu-id="b373b-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="b373b-458">- **ponto de extremidade** -tooaccess de ponto de extremidade Olá Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b373b-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="b373b-459">-**sasToken** (adicionado 1.8.1)-, você pode especificar um token SAS em vez de uma chave de conta de armazenamento na configuração privada hello. Se fornecido, a chave de conta de armazenamento Olá é ignorado.</span><span class="sxs-lookup"><span data-stu-id="b373b-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="b373b-460">Requisitos para Olá Token SAS:</span><span class="sxs-lookup"><span data-stu-id="b373b-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="b373b-461">– Oferece suporte apenas ao token SAS da conta</span><span class="sxs-lookup"><span data-stu-id="b373b-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="b373b-462">Os tipos de serviço - *b*, *t* são obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="b373b-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="b373b-463">As permissões - *a*, *c*, *u*, *w* são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="b373b-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="b373b-464">Os tipos de recurso - *c*, *o* são obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="b373b-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="b373b-465">-Oferece suporte ao protocolo HTTPS de saudação apenas</span><span class="sxs-lookup"><span data-stu-id="b373b-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="b373b-466">– A hora de início e de expiração deve ser válida.</span><span class="sxs-lookup"><span data-stu-id="b373b-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="b373b-467">Elemento IsEnabled</span><span class="sxs-lookup"><span data-stu-id="b373b-467">IsEnabled Element</span></span>  
 <span data-ttu-id="b373b-468">*Árvore: Raiz - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="b373b-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="b373b-469">Booliano.</span><span class="sxs-lookup"><span data-stu-id="b373b-469">Boolean.</span></span> <span data-ttu-id="b373b-470">Use `true` tooenable diagnóstico de saudação ou `false` toodisable diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="b373b-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
