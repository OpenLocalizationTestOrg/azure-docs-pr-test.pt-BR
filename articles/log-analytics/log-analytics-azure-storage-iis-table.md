---
title: armazenamento de blob aaaUse para IIS e a tabela de armazenamento para eventos no Azure Log Analytics | Microsoft Docs
description: "Análise de log pode ler logs Olá para serviços do Azure que gravam o armazenamento de diagnóstico tootable ou gravados tooblob armazenamento de logs do IIS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>Usar o armazenamento de blobs do Azure para IIS e armazenamento de tabelas do Azure para eventos com o Log Analytics

Análise de log pode ler os logs de saudação para Olá serviços que gravam diagnóstico tootable armazenamento ou o IIS registra tooblob escrito armazenamento a seguir:

* Clusters do Service Fabric (visualização)
* Máquinas Virtuais
* Funções Web/de Trabalho

Antes que o Log Analytics possa coletar dados para esses recursos, o diagnóstico do Azure deve ser habilitado.

Depois que os diagnósticos são habilitados, você pode usar o portal do Azure de saudação ou PowerShell configurar logs de saudação do toocollect de análise de Log.

Diagnóstico do Azure é uma extensão do Azure que permite que você toocollect dados de diagnóstico de uma função de trabalho, a função web ou a máquina virtual em execução no Azure. dados de saudação são armazenados em uma conta de armazenamento do Azure e, em seguida, podem ser coletados pela análise de Log.

Para análise de Log toocollect esses logs de diagnóstico do Azure, Olá logs devem estar no hello locais a seguir:

| Tipo de Log | Tipo de recurso | Local |
| --- | --- | --- |
| Logs IIS |Máquinas Virtuais <br> Funções da Web <br> Funções de trabalho |wad-iis-logfiles (Armazenamento de Blobs) |
| syslog |Máquinas Virtuais |LinuxsyslogVer2v0 (Armazenamento de Tabelas) |
| Eventos operacionais do Service Fabric |Nós do Service Fabric |WADServiceFabricSystemEventTable |
| Eventos dos Reliable Actors do Service Fabric |Nós do Service Fabric |WADServiceFabricReliableActorEventTable |
| Arquitetura de Serviços Confiáveis do Service Fabric |Nós do Service Fabric |WADServiceFabricReliableServiceEventTable |
| Log de eventos do Windows |Nós do Service Fabric <br> Máquinas Virtuais <br> Funções da Web <br> Funções de trabalho |WADWindowsEventLogsTable (Armazenamento de Tabelas) |
| Logs do ETW do Windows |Nós do Service Fabric <br> Máquinas Virtuais <br> Funções da Web <br> Funções de trabalho |WADETWEventTable (Armazenamento de Tabelas) |

> [!NOTE]
> Atualmente, não há suporte para logs do IIS nos sites do Azure.
>
>

Para máquinas virtuais, você tem opção de saudação da instalação Olá [agente de análise de Log](log-analytics-azure-vm-extension.md) em suas ideias adicionais de tooenable de máquina virtual. Além de logs do IIS capaz de tooanalyze toobeing e Logs de eventos, você pode executar análises adicionais, incluindo controle de alterações de configuração, avaliação de SQL e avaliação de atualização.

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>Habilitar os diagnósticos do Azure em uma máquina virtual para coleta de log de eventos e log do IIS
Saudação de uso seguindo o procedimento tooenable diagnósticos do Azure em uma máquina virtual para Log de eventos e o IIS usando o portal do Microsoft Azure Olá de coleção de log.

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>tooenable diagnósticos do Azure em uma máquina virtual com hello portal do Azure
1. Instale Olá VM Agent ao criar uma máquina virtual. Se já existir uma máquina virtual de saudação, verifique se esse Olá que VM Agent já está instalado.

   * Em Olá portal do Azure, navegue toohello virtual machine, selecione **configuração opcional**, em seguida, **diagnóstico** e defina **Status** muito**em**.

     Após a conclusão, Olá VM tem a extensão de diagnóstico do Azure Olá instalado e em execução. Essa extensão é responsável por coletar seus dados de diagnóstico.
2. Habilite o monitoramento e configure o log de eventos em uma VM existente. Você pode habilitar o diagnóstico no hello nível da VM. Diagnóstico de tooenable e, em seguida, configurar o log de eventos, execute Olá etapas a seguir:

   1. Selecione Olá VM.
   2. Clique em **Monitoramento**.
   3. Clique em **Diagnóstico**.
   4. Saudação de conjunto **Status** muito**ON**.
   5. Selecione cada log de diagnóstico que você deseja toocollect.
   6. Clique em **OK**.

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>Habilitar diagnóstico do Azure em uma função web para coleta de eventos e log do IIS
Consulte também[como tooEnable diagnóstico em um serviço de nuvem](../cloud-services/cloud-services-dotnet-diagnostics.md) para etapas gerais sobre como habilitar o diagnóstico do Azure. instruções de saudação abaixo usam essas informações e personalizá-lo para uso com a análise de Log.

Com o diagnóstico do Azure habilitado:

* Logs do IIS são armazenados por padrão, com dados de log transferidos no intervalo de transferência de scheduledTransferPeriod hello.
* Logs de eventos do Windows não são transferidos por padrão.

### <a name="tooenable-diagnostics"></a>Diagnóstico de tooenable
tooenable Logs de eventos do Windows ou toochange Olá scheduledTransferPeriod, configure o diagnóstico do Azure usando o arquivo de configuração do hello XML (Diagnostics. wadcfg), conforme mostrado no [etapa 4: criar o arquivo de configuração de diagnóstico e instalar Olá extensão](../cloud-services/cloud-services-dotnet-diagnostics.md)

Olá seguinte arquivo de configuração de exemplo coleta Logs do IIS e todos os eventos de saudação aplicativos e logs do sistema:

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

Certifique-se de que seu ConfigurationSettings Especifica uma conta de armazenamento, como no exemplo a seguir de saudação:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

Olá **AccountName** e **AccountKey** valores são encontrados na Olá portal do Azure no painel de conta de armazenamento hello, em gerenciar chaves de acesso. protocolo de saudação para cadeia de caracteres de conexão Olá deve ser **https**.

Depois que a configuração de diagnóstico atualizada Olá é aplicada tooyour serviço de nuvem e está gravando diagnóstico tooAzure armazenamento, e em seguida, você está pronto tooconfigure análise de Log.

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>Usar os logs de toocollect portal do Azure de saudação do armazenamento do Azure
Você pode usar logs de Olá Olá tooconfigure portal do Azure Log Analytics toocollect para Olá serviços do Azure a seguir:

* Clusters do Service Fabric
* Máquinas Virtuais
* Funções Web/de Trabalho

No portal do Azure de Olá, navegar espaço de trabalho de análise de Log tooyour e executar Olá tarefas a seguir:

1. Clique em *Logs das contas de armazenamento*
2. Clique em Olá *adicionar* tarefa
3. Selecionar conta de armazenamento Olá que contém os logs de diagnóstico Olá
   * Essa conta pode ser uma conta de armazenamento clássica ou uma conta de armazenamento do Azure Resource Manager
4. Selecione Olá tipo de dados que você deseja toocollect logs para
   * Opções de saudação são Logs do IIS; Eventos; Syslog (Linux); Logs do ETW; Eventos do serviço do Fabric
5. valor de saudação de origem é preenchido automaticamente com base em hello, tipo de dados e não podem ser alterados
6. Clique em configuração de saudação toosave Okey

Repita as etapas 2 a 6 para tipos de dados e contas de armazenamento adicional que você deseja toocollect de análise de Log.

Em aproximadamente 30 minutos, você está toosee capaz de dados da conta de armazenamento Olá na análise de Log. Você verá apenas os dados gravados toostorage depois Olá configuração é aplicada. Análise de log não lê dados preexistentes Olá Olá da conta de armazenamento.

> [!NOTE]
> portal de saudação não valida que Olá origem existe na conta de armazenamento hello ou se novos dados está sendo gravados.
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>Habilitar o diagnóstico do Azure em uma máquina virtual para coleta de log de eventos e log do IIS usando o PowerShell
Olá Use as etapas em [tooindex de análise de Log de configuração de diagnóstico do Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread do diagnóstico do Azure que é gravado tootable armazenamento.

Usando o Azure PowerShell você pode especificar mais precisamente os eventos de saudação que são gravados tooAzure armazenamento.
Para obter mais informações, consulte [Habilitando o diagnóstico em Máquinas Virtuais do Azure](../virtual-machines-dotnet-diagnostics.md).

Você pode habilitar e atualizar o diagnóstico do Azure usando Olá script do PowerShell a seguir.
Você também pode usar esse script com uma configuração de log personalizada.
Modificar a conta de armazenamento Olá script tooset Olá, nome do serviço e nome da máquina virtual.
script Hello usa cmdlets para máquinas virtuais clássicas.

Examine Olá exemplo de script a seguir, copiá-lo, modifique conforme necessário, salve o exemplo hello como um arquivo de script do PowerShell e, em seguida, execute o script hello.

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>Próximas etapas
* [Coletar logs e métricas para serviços do Azure](log-analytics-azure-storage.md) para serviços do Azure com suporte.
* [Habilitar soluções](log-analytics-add-solutions.md) tooprovide ideias sobre dados de saudação.
* [Usar consultas de pesquisa](log-analytics-log-searches.md) tooanalyze dados de saudação.
