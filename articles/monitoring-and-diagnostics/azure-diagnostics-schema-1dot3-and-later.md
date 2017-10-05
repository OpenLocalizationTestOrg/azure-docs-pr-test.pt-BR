---
title: "Extensão 1.3 do Diagnóstico do Azure e esquema de configuração mais recente | Microsoft Docs"
description: "A versão de esquema 1.3 e posterior do Diagnóstico do Azure é fornecida como parte do SDK 2.4 e posteriores do Microsoft Azure."
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
ms.openlocfilehash: 0d814825fb08452238a254ccd30bde230380c74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="ae65f-103">Esquema de configuração 1.3 e posterior do Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="ae65f-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="ae65f-104">A extensão do Diagnóstico do Azure é o componente usado para coletar contadores de desempenho e outras estatísticas de:</span><span class="sxs-lookup"><span data-stu-id="ae65f-104">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="ae65f-105">Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="ae65f-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="ae65f-106">Conjuntos de Escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="ae65f-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="ae65f-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ae65f-107">Service Fabric</span></span> 
> - <span data-ttu-id="ae65f-108">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="ae65f-108">Cloud Services</span></span> 
> - <span data-ttu-id="ae65f-109">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="ae65f-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="ae65f-110">Esta página só é relevante se você estiver usando um desses serviços.</span><span class="sxs-lookup"><span data-stu-id="ae65f-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="ae65f-111">Esta página é válida para as versões 1.3 e mais recentes (SDK 2.4 e mais recente do Azure).</span><span class="sxs-lookup"><span data-stu-id="ae65f-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="ae65f-112">As seções de configuração mais recentes são comentadas para mostrar em qual versão eles foram adicionados.</span><span class="sxs-lookup"><span data-stu-id="ae65f-112">Newer configuration sections are commented to show in what version they were added.</span></span>  

<span data-ttu-id="ae65f-113">O arquivo de configuração descrito aqui é usado para definir as configurações de diagnóstico quando o monitor de diagnóstico é iniciado.</span><span class="sxs-lookup"><span data-stu-id="ae65f-113">The configuration file described here is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="ae65f-114">A extensão é usada em conjunto com outros produtos de diagnóstico da Microsoft, como o Azure Monitor, o Application Insights e o Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ae65f-114">The extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="ae65f-115">Baixe a definição do esquema do arquivo de configuração pública ao executar o seguinte comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ae65f-115">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="ae65f-116">Para saber mais sobre como usar o Diagnóstico do Azure, confira [Extensão do Diagnóstico do Azure](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ae65f-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="ae65f-117">Exemplo do arquivo de configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ae65f-117">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="ae65f-118">O exemplo a seguir mostra um arquivo de configuração de diagnóstico típico:</span><span class="sxs-lookup"><span data-stu-id="ae65f-118">The following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="ae65f-119">Equivalente em JSON do arquivo de configuração XML anterior.</span><span class="sxs-lookup"><span data-stu-id="ae65f-119">JSON equivalent of the previous XML configuration file.</span></span> 

<span data-ttu-id="ae65f-120">O PublicConfig e PrivateConfig são separados, pois na maioria dos casos de uso de json, eles são passados como variáveis diferentes.</span><span class="sxs-lookup"><span data-stu-id="ae65f-120">The PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="ae65f-121">Esses casos incluem modelos do Resource Manager, conjunto de dimensionamento de máquinas virtuais, PowerShell e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae65f-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="ae65f-122">Leitura desta página</span><span class="sxs-lookup"><span data-stu-id="ae65f-122">Reading this page</span></span>  
 <span data-ttu-id="ae65f-123">As marcas a seguir estão aproximadamente na ordem mostrada no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="ae65f-123">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="ae65f-124">Se você não vir uma descrição completa onde você espera, procure a página para o elemento ou atributo.</span><span class="sxs-lookup"><span data-stu-id="ae65f-124">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="ae65f-125">Tipos comuns de atributo</span><span class="sxs-lookup"><span data-stu-id="ae65f-125">Common Attribute Types</span></span>  
 <span data-ttu-id="ae65f-126">O atributo **scheduledTransferPeriod** aparece em vários elementos.</span><span class="sxs-lookup"><span data-stu-id="ae65f-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="ae65f-127">É o intervalo entre transferências agendadas para armazenamento arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="ae65f-127">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ae65f-128">O valor é um [XML "Tipo de Dados de Duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ae65f-128">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="ae65f-129">Elemento DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="ae65f-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="ae65f-130">*Árvore: Raiz - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ae65f-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="ae65f-131">Adicionado na versão 1.3.</span><span class="sxs-lookup"><span data-stu-id="ae65f-131">Added in version 1.3.</span></span>  

<span data-ttu-id="ae65f-132">O elemento de nível superior do arquivo de configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ae65f-132">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="ae65f-133">**Atributo** xmlns - O namespace XML para o arquivo de configuração de diagnóstico é:</span><span class="sxs-lookup"><span data-stu-id="ae65f-133">**Attribute**  xmlns - The XML namespace for the diagnostics configuration file is:</span></span>  
<span data-ttu-id="ae65f-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="ae65f-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="ae65f-135">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-135">Child Elements</span></span>|<span data-ttu-id="ae65f-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="ae65f-137">**PublicConfig**</span></span>|<span data-ttu-id="ae65f-138">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="ae65f-138">Required.</span></span> <span data-ttu-id="ae65f-139">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ae65f-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="ae65f-140">**PrivateConfig**</span></span>|<span data-ttu-id="ae65f-141">Opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-141">Optional.</span></span> <span data-ttu-id="ae65f-142">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ae65f-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="ae65f-143">**IsEnabled**</span></span>|<span data-ttu-id="ae65f-144">Booliano.</span><span class="sxs-lookup"><span data-stu-id="ae65f-144">Boolean.</span></span> <span data-ttu-id="ae65f-145">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="ae65f-146">Elemento PublicConfig</span><span class="sxs-lookup"><span data-stu-id="ae65f-146">PublicConfig Element</span></span>  
 <span data-ttu-id="ae65f-147">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="ae65f-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="ae65f-148">Descreve a configuração de diagnóstico pública.</span><span class="sxs-lookup"><span data-stu-id="ae65f-148">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="ae65f-149">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-149">Child Elements</span></span>|<span data-ttu-id="ae65f-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="ae65f-151">**WadCfg**</span></span>|<span data-ttu-id="ae65f-152">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="ae65f-152">Required.</span></span> <span data-ttu-id="ae65f-153">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ae65f-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="ae65f-154">**StorageAccount**</span></span>|<span data-ttu-id="ae65f-155">O nome da conta do Armazenamento do Azure para armazenar os dados.</span><span class="sxs-lookup"><span data-stu-id="ae65f-155">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="ae65f-156">Pode ser especificado como um parâmetro ao executar o cmdlet Set-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="ae65f-156">May also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="ae65f-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="ae65f-157">**StorageType**</span></span>|<span data-ttu-id="ae65f-158">Pode ser *Table*, *Blob* ou *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="ae65f-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="ae65f-159">Tabela é o padrão.</span><span class="sxs-lookup"><span data-stu-id="ae65f-159">Table is default.</span></span> <span data-ttu-id="ae65f-160">Quando TableAndBlob for escolhido, os dados de diagnóstico serão gravados duas vezes, uma vez para cada tipo.</span><span class="sxs-lookup"><span data-stu-id="ae65f-160">When TableAndBlob is chosen, diagnostic data is written twice -- once to each type.</span></span>|  
|<span data-ttu-id="ae65f-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="ae65f-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="ae65f-162">O diretório na máquina virtual em que o Agente de Monitoramento armazena dados de evento.</span><span class="sxs-lookup"><span data-stu-id="ae65f-162">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="ae65f-163">Caso contrário, o diretório padrão definido será usado:</span><span class="sxs-lookup"><span data-stu-id="ae65f-163">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="ae65f-164">Para uma função de Trabalho/da Web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="ae65f-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="ae65f-165">Para uma Máquina Virtual: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="ae65f-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="ae65f-166">Os atributos obrigatórios são:</span><span class="sxs-lookup"><span data-stu-id="ae65f-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="ae65f-167">- **path** - o diretório no sistema a ser usado pelo Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae65f-167">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="ae65f-168">- **expandEnvironment** - controla se as variáveis de ambiente estão expandidas ou não no nome do caminho.</span><span class="sxs-lookup"><span data-stu-id="ae65f-168">- **expandEnvironment** - Controls whether environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="ae65f-169">Elemento WadCFG</span><span class="sxs-lookup"><span data-stu-id="ae65f-169">WadCFG Element</span></span>  
 <span data-ttu-id="ae65f-170">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="ae65f-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="ae65f-171">Identifica e configura os dados de telemetria a serem coletados.</span><span class="sxs-lookup"><span data-stu-id="ae65f-171">Identifies and configures the telemetry data to be collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="ae65f-172">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="ae65f-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="ae65f-173">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ae65f-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="ae65f-174">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ae65f-174">Required</span></span> 

|<span data-ttu-id="ae65f-175">Atributos</span><span class="sxs-lookup"><span data-stu-id="ae65f-175">Attributes</span></span>|<span data-ttu-id="ae65f-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="ae65f-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="ae65f-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="ae65f-178">A quantidade máxima de espaço em disco local que pode ser consumido pelos diversos tipos de dados de diagnóstico coletados pelo Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae65f-178">The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="ae65f-179">A configuração padrão é 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="ae65f-179">The default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="ae65f-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="ae65f-180">**useProxyServer**</span></span> | <span data-ttu-id="ae65f-181">Configure o Diagnóstico do Azure para usar as configurações de servidor proxy como definido nas configurações do IE.</span><span class="sxs-lookup"><span data-stu-id="ae65f-181">Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="ae65f-182">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-182">Child Elements</span></span>|<span data-ttu-id="ae65f-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="ae65f-184">**CrashDumps**</span></span>|<span data-ttu-id="ae65f-185">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ae65f-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="ae65f-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="ae65f-187">Habilite a coleta de logs gerados pelo Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae65f-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="ae65f-188">Os logs de infraestrutura de diagnóstico são úteis para solucionar problemas de sistema de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ae65f-188">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="ae65f-189">Os atributos opcionais são:</span><span class="sxs-lookup"><span data-stu-id="ae65f-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="ae65f-190">- **scheduledTransferLogLevelFilter** - configura o nível de severidade mínimo dos logs coletados.</span><span class="sxs-lookup"><span data-stu-id="ae65f-190">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="ae65f-191">- **scheduledTransferPeriod** - o intervalo entre transferências agendadas para o armazenamento, arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="ae65f-191">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ae65f-192">O valor é um [XML "Tipo de Dados de Duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ae65f-192">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="ae65f-193">**Diretórios**</span><span class="sxs-lookup"><span data-stu-id="ae65f-193">**Directories**</span></span>|<span data-ttu-id="ae65f-194">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ae65f-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="ae65f-195">**EtwProviders**</span></span>|<span data-ttu-id="ae65f-196">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ae65f-197">**Métricas**</span><span class="sxs-lookup"><span data-stu-id="ae65f-197">**Metrics**</span></span>|<span data-ttu-id="ae65f-198">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ae65f-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="ae65f-199">**PerformanceCounters**</span></span>|<span data-ttu-id="ae65f-200">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ae65f-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="ae65f-201">**WindowsEventLog**</span></span>|<span data-ttu-id="ae65f-202">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="ae65f-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="ae65f-203">**DockerSources**</span></span>|<span data-ttu-id="ae65f-204">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="ae65f-205">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="ae65f-205">CrashDumps Element</span></span>  
 <span data-ttu-id="ae65f-206">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="ae65f-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="ae65f-207">Habilite a coleção de despejos de memória.</span><span class="sxs-lookup"><span data-stu-id="ae65f-207">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="ae65f-208">Atributos</span><span class="sxs-lookup"><span data-stu-id="ae65f-208">Attributes</span></span>|<span data-ttu-id="ae65f-209">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="ae65f-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="ae65f-210">**containerName**</span></span>|<span data-ttu-id="ae65f-211">Opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-211">Optional.</span></span> <span data-ttu-id="ae65f-212">O nome do contêiner de blobs em sua conta do Armazenamento do Azure para ser usado para armazenar despejos de memória.</span><span class="sxs-lookup"><span data-stu-id="ae65f-212">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="ae65f-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="ae65f-213">**crashDumpType**</span></span>|<span data-ttu-id="ae65f-214">Opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-214">Optional.</span></span>  <span data-ttu-id="ae65f-215">Configura o Diagnóstico do Azure para coletar minidespejos de memória ou despejos de memória completos.</span><span class="sxs-lookup"><span data-stu-id="ae65f-215">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="ae65f-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="ae65f-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="ae65f-217">Opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-217">Optional.</span></span>  <span data-ttu-id="ae65f-218">Configura o percentual de **overallQuotaInMB** a ser reservado para despejos de memória na VM.</span><span class="sxs-lookup"><span data-stu-id="ae65f-218">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="ae65f-219">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-219">Child Elements</span></span>|<span data-ttu-id="ae65f-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ae65f-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="ae65f-222">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="ae65f-222">Required.</span></span> <span data-ttu-id="ae65f-223">Define os valores de configuração para cada processo.</span><span class="sxs-lookup"><span data-stu-id="ae65f-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="ae65f-224">O atributo a seguir também é obrigatório:</span><span class="sxs-lookup"><span data-stu-id="ae65f-224">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="ae65f-225">**processName** - o nome do processo para o qual você deseja que o Diagnóstico do Azure colete um despejo de memória.</span><span class="sxs-lookup"><span data-stu-id="ae65f-225">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="ae65f-226">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="ae65f-226">Directories Element</span></span> 
 <span data-ttu-id="ae65f-227">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories*</span><span class="sxs-lookup"><span data-stu-id="ae65f-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="ae65f-228">Habilita a coleta do conteúdo de um diretório, logs de solicitação de acesso com falha do IIS e/ou logs do IIS.</span><span class="sxs-lookup"><span data-stu-id="ae65f-228">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="ae65f-229">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="ae65f-230">Veja a explicação anterior.</span><span class="sxs-lookup"><span data-stu-id="ae65f-230">See explanation earlier.</span></span>  

|<span data-ttu-id="ae65f-231">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-231">Child Elements</span></span>|<span data-ttu-id="ae65f-232">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="ae65f-233">**IISLogs**</span></span>|<span data-ttu-id="ae65f-234">A inclusão deste elemento na configuração habilita a coleta de logs do IIS:</span><span class="sxs-lookup"><span data-stu-id="ae65f-234">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="ae65f-235">**containerName** - o nome do contêiner de blobs na sua conta do Armazenamento do Azure a ser usado para armazenar os logs do IIS.</span><span class="sxs-lookup"><span data-stu-id="ae65f-235">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|   
|<span data-ttu-id="ae65f-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="ae65f-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="ae65f-237">A inclusão desse elemento na configuração habilita a coleta de logs sobre solicitações com falha para um site ou aplicativo do IIS.</span><span class="sxs-lookup"><span data-stu-id="ae65f-237">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="ae65f-238">Você também deve habilitar as opções de rastreamento em **system.WebServer** em **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="ae65f-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="ae65f-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="ae65f-239">**DataSources**</span></span>|<span data-ttu-id="ae65f-240">Uma lista de diretórios para monitorar.</span><span class="sxs-lookup"><span data-stu-id="ae65f-240">A list of directories to monitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="ae65f-241">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="ae65f-241">DataSources Element</span></span>  
 <span data-ttu-id="ae65f-242">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="ae65f-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="ae65f-243">Uma lista de diretórios para monitorar.</span><span class="sxs-lookup"><span data-stu-id="ae65f-243">A list of directories to monitor.</span></span>  

|<span data-ttu-id="ae65f-244">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-244">Child Elements</span></span>|<span data-ttu-id="ae65f-245">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ae65f-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="ae65f-247">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="ae65f-247">Required.</span></span> <span data-ttu-id="ae65f-248">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="ae65f-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-249">**containerName** - o nome do contêiner de blob no armazenamento do Azure na conta a ser usada para armazenar os arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="ae65f-249">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="ae65f-250">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="ae65f-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="ae65f-251">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ae65f-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="ae65f-252">Pode incluir o elemento **Absolute** ou **LocalResource**, mas não ambos.</span><span class="sxs-lookup"><span data-stu-id="ae65f-252">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="ae65f-253">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-253">Child Elements</span></span>|<span data-ttu-id="ae65f-254">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="ae65f-255">**Absolute**</span></span>|<span data-ttu-id="ae65f-256">O caminho absoluto para o diretório a ser monitorado.</span><span class="sxs-lookup"><span data-stu-id="ae65f-256">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="ae65f-257">Os atributos a seguir são obrigatórios:</span><span class="sxs-lookup"><span data-stu-id="ae65f-257">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="ae65f-258">- **Path** - o caminho absoluto para o diretório a ser monitorado.</span><span class="sxs-lookup"><span data-stu-id="ae65f-258">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="ae65f-259">- **expandEnvironment** - configura se as variáveis de ambiente em Path são expandidas ou não.</span><span class="sxs-lookup"><span data-stu-id="ae65f-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="ae65f-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="ae65f-260">**LocalResource**</span></span>|<span data-ttu-id="ae65f-261">O caminho relativo a um recurso local a ser monitorado.</span><span class="sxs-lookup"><span data-stu-id="ae65f-261">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="ae65f-262">Os atributos obrigatórios são:</span><span class="sxs-lookup"><span data-stu-id="ae65f-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="ae65f-263">- **Name** - o recurso local que contém o diretório a ser monitorado</span><span class="sxs-lookup"><span data-stu-id="ae65f-263">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="ae65f-264">- **relativePath** - o caminho relativo a Name que contém o diretório a ser monitorado</span><span class="sxs-lookup"><span data-stu-id="ae65f-264">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="ae65f-265">Elemento EtwProviders</span><span class="sxs-lookup"><span data-stu-id="ae65f-265">EtwProviders Element</span></span>  
 <span data-ttu-id="ae65f-266">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="ae65f-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="ae65f-267">Configura a coleta de eventos ETW do EventSource e/ou os provedores baseados no Manifesto ETW.</span><span class="sxs-lookup"><span data-stu-id="ae65f-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="ae65f-268">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-268">Child Elements</span></span>|<span data-ttu-id="ae65f-269">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ae65f-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="ae65f-271">Configura a coleta de eventos gerados desde a [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="ae65f-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="ae65f-272">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="ae65f-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-273">**provider** - o nome da classe do evento EventSource.</span><span class="sxs-lookup"><span data-stu-id="ae65f-273">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="ae65f-274">Os atributos opcionais são:</span><span class="sxs-lookup"><span data-stu-id="ae65f-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="ae65f-275">- **scheduledTransferLogLevelFilter** - o nível mínimo de severidade a transferir para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ae65f-275">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="ae65f-276">- **scheduledTransferPeriod** - o intervalo entre transferências agendadas para o Armazenamento do Azure arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="ae65f-276">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ae65f-277">O valor é um [XML "Tipo de Dados de Duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ae65f-277">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="ae65f-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ae65f-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="ae65f-279">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="ae65f-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-280">**provider** - o GUID do provedor de eventos</span><span class="sxs-lookup"><span data-stu-id="ae65f-280">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="ae65f-281">Os atributos opcionais são:</span><span class="sxs-lookup"><span data-stu-id="ae65f-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="ae65f-282">- **scheduledTransferLogLevelFilter** - o nível mínimo de severidade a transferir para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ae65f-282">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="ae65f-283">- **scheduledTransferPeriod** - o intervalo entre transferências agendadas para o Armazenamento do Azure arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="ae65f-283">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ae65f-284">O valor é um [XML "Tipo de Dados de Duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ae65f-284">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="ae65f-285">Elemento EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="ae65f-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="ae65f-286">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ae65f-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="ae65f-287">Configura a coleta de eventos gerados desde a [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="ae65f-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="ae65f-288">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-288">Child Elements</span></span>|<span data-ttu-id="ae65f-289">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="ae65f-290">**DefaultEvents**</span></span>|<span data-ttu-id="ae65f-291">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="ae65f-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="ae65f-292">**eventDestination** - o nome da tabela para armazenar os eventos</span><span class="sxs-lookup"><span data-stu-id="ae65f-292">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="ae65f-293">**Evento**</span><span class="sxs-lookup"><span data-stu-id="ae65f-293">**Event**</span></span>|<span data-ttu-id="ae65f-294">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="ae65f-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-295">**id** - a id do evento.</span><span class="sxs-lookup"><span data-stu-id="ae65f-295">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="ae65f-296">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="ae65f-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-297">**eventDestination** - o nome da tabela para armazenar os eventos</span><span class="sxs-lookup"><span data-stu-id="ae65f-297">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="ae65f-298">Elemento EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="ae65f-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="ae65f-299">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ae65f-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="ae65f-300">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-300">Child Elements</span></span>|<span data-ttu-id="ae65f-301">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="ae65f-302">**DefaultEvents**</span></span>|<span data-ttu-id="ae65f-303">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="ae65f-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-304">**eventDestination** - o nome da tabela para armazenar os eventos</span><span class="sxs-lookup"><span data-stu-id="ae65f-304">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="ae65f-305">**Evento**</span><span class="sxs-lookup"><span data-stu-id="ae65f-305">**Event**</span></span>|<span data-ttu-id="ae65f-306">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="ae65f-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-307">**id** - a id do evento.</span><span class="sxs-lookup"><span data-stu-id="ae65f-307">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="ae65f-308">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="ae65f-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-309">**eventDestination** - o nome da tabela para armazenar os eventos</span><span class="sxs-lookup"><span data-stu-id="ae65f-309">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="ae65f-310">Elemento Metrics</span><span class="sxs-lookup"><span data-stu-id="ae65f-310">Metrics Element</span></span>  
 <span data-ttu-id="ae65f-311">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="ae65f-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="ae65f-312">Permite gerar uma tabela de contador de desempenho otimizada para consultas rápidas.</span><span class="sxs-lookup"><span data-stu-id="ae65f-312">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="ae65f-313">Cada contador de desempenho definido no elemento **PerformanceCounters** é armazenado na tabela Métricas, além de na tabela Contador de Desempenho.</span><span class="sxs-lookup"><span data-stu-id="ae65f-313">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="ae65f-314">O atributo **resourceId** é necessário.</span><span class="sxs-lookup"><span data-stu-id="ae65f-314">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="ae65f-315">A ID de recurso da Máquina Virtual na qual você está implantando o Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae65f-315">The resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="ae65f-316">Obtenha o **resourceID** do [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ae65f-316">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ae65f-317">Selecione **Procurar** -> **Grupos de Recursos** -> **<Nome\>**.</span><span class="sxs-lookup"><span data-stu-id="ae65f-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="ae65f-318">Clique no bloco **Propriedades** e copie o valor do campo **ID**.</span><span class="sxs-lookup"><span data-stu-id="ae65f-318">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="ae65f-319">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-319">Child Elements</span></span>|<span data-ttu-id="ae65f-320">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="ae65f-321">**MetricAggregation**</span></span>|<span data-ttu-id="ae65f-322">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="ae65f-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-323">**scheduledTransferPeriod** - o intervalo entre transferências agendadas para o armazenamento, arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="ae65f-323">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ae65f-324">O valor é um [XML "Tipo de Dados de Duração".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ae65f-324">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="ae65f-325">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="ae65f-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="ae65f-326">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="ae65f-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="ae65f-327">Habilita a coleta de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ae65f-327">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="ae65f-328">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="ae65f-328">Optional attribute:</span></span>  

 <span data-ttu-id="ae65f-329">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="ae65f-330">Veja a explicação anterior.</span><span class="sxs-lookup"><span data-stu-id="ae65f-330">See explanation earlier.</span></span>

|<span data-ttu-id="ae65f-331">Elemento filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-331">Child Element</span></span>|<span data-ttu-id="ae65f-332">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="ae65f-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ae65f-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="ae65f-334">Os atributos a seguir são obrigatórios:</span><span class="sxs-lookup"><span data-stu-id="ae65f-334">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="ae65f-335">- **counterSpecifier** - o nome do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ae65f-335">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="ae65f-336">Por exemplo: `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="ae65f-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="ae65f-337">Para obter uma lista de contadores de desempenho no seu host, execute o comando `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="ae65f-337">To get a list of performance counters on your host, run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="ae65f-338">- **sampleRate** - Com que frequência o contador deve ser testado.</span><span class="sxs-lookup"><span data-stu-id="ae65f-338">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="ae65f-339">Atributo opcional:</span><span class="sxs-lookup"><span data-stu-id="ae65f-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-340">**unidade** - a unidade de medida do contador.</span><span class="sxs-lookup"><span data-stu-id="ae65f-340">**unit** - The unit of measure of the counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="ae65f-341">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="ae65f-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="ae65f-342">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="ae65f-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="ae65f-343">Habilita a coleta de Logs de Eventos do Windows.</span><span class="sxs-lookup"><span data-stu-id="ae65f-343">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="ae65f-344">Atributo **scheduledTransferPeriod** opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="ae65f-345">Veja a explicação anterior.</span><span class="sxs-lookup"><span data-stu-id="ae65f-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="ae65f-346">Elemento filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-346">Child Element</span></span>|<span data-ttu-id="ae65f-347">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="ae65f-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="ae65f-348">**DataSource**</span></span>|<span data-ttu-id="ae65f-349">Os logs de Eventos do Windows a serem coletados.</span><span class="sxs-lookup"><span data-stu-id="ae65f-349">The Windows Event logs to collect.</span></span> <span data-ttu-id="ae65f-350">Atributo obrigatório:</span><span class="sxs-lookup"><span data-stu-id="ae65f-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="ae65f-351">**name** - a consulta XPath que descreve os eventos do windows a serem coletados.</span><span class="sxs-lookup"><span data-stu-id="ae65f-351">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="ae65f-352">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ae65f-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="ae65f-353">Para coletar todos os eventos, especifique "*"</span><span class="sxs-lookup"><span data-stu-id="ae65f-353">To collect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="ae65f-354">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="ae65f-354">Logs Element</span></span>  
 <span data-ttu-id="ae65f-355">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="ae65f-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="ae65f-356">Presente na versão 1.0 e 1.1.</span><span class="sxs-lookup"><span data-stu-id="ae65f-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="ae65f-357">Ausente na 1.2.</span><span class="sxs-lookup"><span data-stu-id="ae65f-357">Missing in 1.2.</span></span> <span data-ttu-id="ae65f-358">Adicionado novamente na versão 1.3.</span><span class="sxs-lookup"><span data-stu-id="ae65f-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="ae65f-359">Define a configuração de buffer para logs básicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae65f-359">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="ae65f-360">Atributo</span><span class="sxs-lookup"><span data-stu-id="ae65f-360">Attribute</span></span>|<span data-ttu-id="ae65f-361">Tipo</span><span class="sxs-lookup"><span data-stu-id="ae65f-361">Type</span></span>|<span data-ttu-id="ae65f-362">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="ae65f-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="ae65f-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="ae65f-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="ae65f-364">**unsignedInt**</span></span>|<span data-ttu-id="ae65f-365">Opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-365">Optional.</span></span> <span data-ttu-id="ae65f-366">Especifica a quantidade máxima de armazenamento do sistema de arquivos disponível para os dados especificados.</span><span class="sxs-lookup"><span data-stu-id="ae65f-366">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="ae65f-367">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="ae65f-367">The default is 0.</span></span>|  
|<span data-ttu-id="ae65f-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="ae65f-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="ae65f-369">**string**</span><span class="sxs-lookup"><span data-stu-id="ae65f-369">**string**</span></span>|<span data-ttu-id="ae65f-370">Opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-370">Optional.</span></span> <span data-ttu-id="ae65f-371">Especifica o nível de severidade mínimo para as entradas de log transferidas.</span><span class="sxs-lookup"><span data-stu-id="ae65f-371">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="ae65f-372">O valor padrão é **Indefinido**, que transfere todos os logs.</span><span class="sxs-lookup"><span data-stu-id="ae65f-372">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="ae65f-373">Outros possíveis valores (na ordem de mais informações para menos) são **Detalhado**, **Informações**, **Aviso**, **Erro**, e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="ae65f-373">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="ae65f-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="ae65f-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="ae65f-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="ae65f-375">**duration**</span></span>|<span data-ttu-id="ae65f-376">Opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-376">Optional.</span></span> <span data-ttu-id="ae65f-377">Especifica o intervalo entre as transferências agendadas de dados, arredondado para o minuto mais próximo.</span><span class="sxs-lookup"><span data-stu-id="ae65f-377">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="ae65f-378">O padrão é PT0S.</span><span class="sxs-lookup"><span data-stu-id="ae65f-378">The default is PT0S.</span></span>|  
|<span data-ttu-id="ae65f-379">**coletores** Adicionados na 1.5</span><span class="sxs-lookup"><span data-stu-id="ae65f-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="ae65f-380">**string**</span><span class="sxs-lookup"><span data-stu-id="ae65f-380">**string**</span></span>|<span data-ttu-id="ae65f-381">Opcional.</span><span class="sxs-lookup"><span data-stu-id="ae65f-381">Optional.</span></span> <span data-ttu-id="ae65f-382">Aponta para um local de coletor para também enviar dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ae65f-382">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="ae65f-383">Por exemplo, o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae65f-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="ae65f-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="ae65f-384">DockerSources</span></span>
 <span data-ttu-id="ae65f-385">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="ae65f-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="ae65f-386">Adicionado na versão 1.9.</span><span class="sxs-lookup"><span data-stu-id="ae65f-386">Added in 1.9.</span></span>

|<span data-ttu-id="ae65f-387">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ae65f-387">Element Name</span></span>|<span data-ttu-id="ae65f-388">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="ae65f-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="ae65f-389">**Stats**</span></span>|<span data-ttu-id="ae65f-390">Informa ao sistema para coletar estatísticas para contêineres do Docker</span><span class="sxs-lookup"><span data-stu-id="ae65f-390">Tells the system to collect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="ae65f-391">Elemento SinksConfig</span><span class="sxs-lookup"><span data-stu-id="ae65f-391">SinksConfig Element</span></span>  
 <span data-ttu-id="ae65f-392">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="ae65f-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="ae65f-393">Uma lista de locais para enviar dados de diagnóstico e a configuração associada a esses locais.</span><span class="sxs-lookup"><span data-stu-id="ae65f-393">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="ae65f-394">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="ae65f-394">Element Name</span></span>|<span data-ttu-id="ae65f-395">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="ae65f-396">**Coletor**</span><span class="sxs-lookup"><span data-stu-id="ae65f-396">**Sink**</span></span>|<span data-ttu-id="ae65f-397">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="ae65f-398">Elemento Sink</span><span class="sxs-lookup"><span data-stu-id="ae65f-398">Sink Element</span></span>
 <span data-ttu-id="ae65f-399">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="ae65f-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="ae65f-400">Adicionado na versão 1.5.</span><span class="sxs-lookup"><span data-stu-id="ae65f-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="ae65f-401">Define os locais para os quais os dados de diagnóstico devem ser enviados.</span><span class="sxs-lookup"><span data-stu-id="ae65f-401">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="ae65f-402">Por exemplo, o serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae65f-402">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="ae65f-403">Atributo</span><span class="sxs-lookup"><span data-stu-id="ae65f-403">Attribute</span></span>|<span data-ttu-id="ae65f-404">Tipo</span><span class="sxs-lookup"><span data-stu-id="ae65f-404">Type</span></span>|<span data-ttu-id="ae65f-405">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="ae65f-406">**name**</span><span class="sxs-lookup"><span data-stu-id="ae65f-406">**name**</span></span>|<span data-ttu-id="ae65f-407">string</span><span class="sxs-lookup"><span data-stu-id="ae65f-407">string</span></span>|<span data-ttu-id="ae65f-408">Uma cadeia de caracteres que identifica o nome do coletor.</span><span class="sxs-lookup"><span data-stu-id="ae65f-408">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="ae65f-409">Elemento</span><span class="sxs-lookup"><span data-stu-id="ae65f-409">Element</span></span>|<span data-ttu-id="ae65f-410">Tipo</span><span class="sxs-lookup"><span data-stu-id="ae65f-410">Type</span></span>|<span data-ttu-id="ae65f-411">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="ae65f-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="ae65f-412">**Application Insights**</span></span>|<span data-ttu-id="ae65f-413">string</span><span class="sxs-lookup"><span data-stu-id="ae65f-413">string</span></span>|<span data-ttu-id="ae65f-414">Usado somente durante o envio de dados para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae65f-414">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="ae65f-415">Contém a Chave de Instrumentação para uma conta ativa do Application Insights a que você tem acesso.</span><span class="sxs-lookup"><span data-stu-id="ae65f-415">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="ae65f-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="ae65f-416">**Channels**</span></span>|<span data-ttu-id="ae65f-417">string</span><span class="sxs-lookup"><span data-stu-id="ae65f-417">string</span></span>|<span data-ttu-id="ae65f-418">Uma para cada filtragem adicional que o fluxo que você</span><span class="sxs-lookup"><span data-stu-id="ae65f-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="ae65f-419">Elemento Channels</span><span class="sxs-lookup"><span data-stu-id="ae65f-419">Channels Element</span></span>  
 <span data-ttu-id="ae65f-420">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="ae65f-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="ae65f-421">Adicionado na versão 1.5.</span><span class="sxs-lookup"><span data-stu-id="ae65f-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="ae65f-422">Define filtros para fluxos de dados de log que passam por um coletor.</span><span class="sxs-lookup"><span data-stu-id="ae65f-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="ae65f-423">Elemento</span><span class="sxs-lookup"><span data-stu-id="ae65f-423">Element</span></span>|<span data-ttu-id="ae65f-424">Tipo</span><span class="sxs-lookup"><span data-stu-id="ae65f-424">Type</span></span>|<span data-ttu-id="ae65f-425">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="ae65f-426">**Canal**</span><span class="sxs-lookup"><span data-stu-id="ae65f-426">**Channel**</span></span>|<span data-ttu-id="ae65f-427">string</span><span class="sxs-lookup"><span data-stu-id="ae65f-427">string</span></span>|<span data-ttu-id="ae65f-428">Veja a descrição em outro lugar nesta página.</span><span class="sxs-lookup"><span data-stu-id="ae65f-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="ae65f-429">Elemento Channel</span><span class="sxs-lookup"><span data-stu-id="ae65f-429">Channel Element</span></span>
 <span data-ttu-id="ae65f-430">*Árvore: Raiz - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="ae65f-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="ae65f-431">Adicionado na versão 1.5.</span><span class="sxs-lookup"><span data-stu-id="ae65f-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="ae65f-432">Define os locais para os quais os dados de diagnóstico devem ser enviados.</span><span class="sxs-lookup"><span data-stu-id="ae65f-432">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="ae65f-433">Por exemplo, o serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae65f-433">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="ae65f-434">Atributos</span><span class="sxs-lookup"><span data-stu-id="ae65f-434">Attributes</span></span>|<span data-ttu-id="ae65f-435">Tipo</span><span class="sxs-lookup"><span data-stu-id="ae65f-435">Type</span></span>|<span data-ttu-id="ae65f-436">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="ae65f-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="ae65f-437">**logLevel**</span></span>|<span data-ttu-id="ae65f-438">**string**</span><span class="sxs-lookup"><span data-stu-id="ae65f-438">**string**</span></span>|<span data-ttu-id="ae65f-439">Especifica o nível de severidade mínimo para as entradas de log transferidas.</span><span class="sxs-lookup"><span data-stu-id="ae65f-439">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="ae65f-440">O valor padrão é **Indefinido**, que transfere todos os logs.</span><span class="sxs-lookup"><span data-stu-id="ae65f-440">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="ae65f-441">Outros possíveis valores (na ordem de mais informações para menos) são **Detalhado**, **Informações**, **Aviso**, **Erro**, e **Crítico**.</span><span class="sxs-lookup"><span data-stu-id="ae65f-441">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="ae65f-442">**name**</span><span class="sxs-lookup"><span data-stu-id="ae65f-442">**name**</span></span>|<span data-ttu-id="ae65f-443">**string**</span><span class="sxs-lookup"><span data-stu-id="ae65f-443">**string**</span></span>|<span data-ttu-id="ae65f-444">Um nome exclusivo do canal que será mencionado</span><span class="sxs-lookup"><span data-stu-id="ae65f-444">A unique name of the channel to refer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="ae65f-445">Elemento PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="ae65f-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="ae65f-446">*Árvore: Raiz - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="ae65f-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="ae65f-447">Adicionado na versão 1.3.</span><span class="sxs-lookup"><span data-stu-id="ae65f-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="ae65f-448">Opcional</span><span class="sxs-lookup"><span data-stu-id="ae65f-448">Optional</span></span>  

 <span data-ttu-id="ae65f-449">Armazena os detalhes privados da conta de armazenamento (nome, chave e ponto de extremidade).</span><span class="sxs-lookup"><span data-stu-id="ae65f-449">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="ae65f-450">Essa informação é enviada para a máquina virtual, mas não pode ser recuperada dela.</span><span class="sxs-lookup"><span data-stu-id="ae65f-450">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="ae65f-451">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ae65f-451">Child Elements</span></span>|<span data-ttu-id="ae65f-452">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae65f-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ae65f-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="ae65f-453">**StorageAccount**</span></span>|<span data-ttu-id="ae65f-454">A conta de armazenamento a ser usada.</span><span class="sxs-lookup"><span data-stu-id="ae65f-454">The storage account to use.</span></span> <span data-ttu-id="ae65f-455">Os atributos a seguir são necessários</span><span class="sxs-lookup"><span data-stu-id="ae65f-455">The following attributes are required</span></span><br /><br /> <span data-ttu-id="ae65f-456">- **name** - o nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ae65f-456">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="ae65f-457">- **chave** - a chave para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ae65f-457">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="ae65f-458">- **ponto de extremidade** - o ponto de extremidade para acessar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ae65f-458">- **endpoint** - The endpoint to access the storage account.</span></span> <br /><br /> <span data-ttu-id="ae65f-459">-**sasToken** (adicionado na versão 1.8.1)- Você pode especificar um token SAS em vez de uma chave de conta de armazenamento na configuração privada.</span><span class="sxs-lookup"><span data-stu-id="ae65f-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="ae65f-460">Se for fornecida, a chave da conta de armazenamento será ignorada.</span><span class="sxs-lookup"><span data-stu-id="ae65f-460">If provided, the storage account key is ignored.</span></span> <br /><span data-ttu-id="ae65f-461">Requisitos para o Token SAS:</span><span class="sxs-lookup"><span data-stu-id="ae65f-461">Requirements for the SAS Token:</span></span> <br /><span data-ttu-id="ae65f-462">– Oferece suporte apenas ao token SAS da conta</span><span class="sxs-lookup"><span data-stu-id="ae65f-462">- Supports account SAS token only</span></span> <br /><span data-ttu-id="ae65f-463">Os tipos de serviço - *b*, *t* são obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="ae65f-463">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="ae65f-464">As permissões - *a*, *c*, *u*, *w* são obrigatórias.</span><span class="sxs-lookup"><span data-stu-id="ae65f-464">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="ae65f-465">Os tipos de recurso - *c*, *o* são obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="ae65f-465">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="ae65f-466">– Oferece suporte somente ao protocolo HTTPS</span><span class="sxs-lookup"><span data-stu-id="ae65f-466">- Supports the HTTPS protocol only</span></span> <br /> <span data-ttu-id="ae65f-467">– A hora de início e de expiração deve ser válida.</span><span class="sxs-lookup"><span data-stu-id="ae65f-467">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="ae65f-468">Elemento IsEnabled</span><span class="sxs-lookup"><span data-stu-id="ae65f-468">IsEnabled Element</span></span>  
 <span data-ttu-id="ae65f-469">*Árvore: Raiz - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="ae65f-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="ae65f-470">Booliano.</span><span class="sxs-lookup"><span data-stu-id="ae65f-470">Boolean.</span></span> <span data-ttu-id="ae65f-471">Use `true` para habilitar o diagnóstico ou `false` para desabilitar o diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ae65f-471">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
