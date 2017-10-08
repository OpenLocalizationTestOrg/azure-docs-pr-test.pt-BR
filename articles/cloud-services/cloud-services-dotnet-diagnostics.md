---
title: "aaaHow toouse diagnóstico do Azure (.NET) com serviços de nuvem | Microsoft Docs"
description: "Usando o diagnóstico do Azure toogather dados do Azure serviços de nuvem para depuração, medir o desempenho, monitoramento, análise de tráfego e muito mais."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>Habilitando o Diagnóstico do Azure nos Serviços de Nuvem do Azure
Confira [Visão geral do Diagnóstico do Azure](../azure-diagnostics.md) para obter informações preliminares sobre o Diagnóstico do Azure.

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>Como tooEnable diagnósticos em uma função de trabalho
Este passo a passo descreve como tooimplement uma função de trabalho do Azure que emite os dados de telemetria usando Olá classe EventSource .NET. Diagnóstico do Azure é usado toocollect Olá os dados de telemetria e armazená-lo em uma conta de armazenamento do Azure. Ao criar uma função de trabalho, o Visual Studio permite automaticamente Diagnostics 1.0 como parte da solução Olá SDKs do Azure para .NET 2.4 e anterior. Olá instruções a seguir descrevem o processo de saudação para criar função de trabalho hello, desabilitando Diagnostics 1.0 da solução hello e implantando Diagnostics 1.2 ou função de trabalho tooyour 1.3.

### <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você tenha uma assinatura do Azure e estiver usando o Visual Studio com hello SDK do Azure. Se você não tiver uma assinatura do Azure, você pode se inscrever para Olá [avaliação gratuita][Free Trial]. Certifique-se muito[instalar e configurar o Azure PowerShell versão 0.8.7 ou posterior][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-worker-role"></a>Etapa 1: criar uma função de trabalho
1. Inicie o **Visual Studio**.
2. Criar um **serviço de nuvem do Azure** projeto da saudação **nuvem** modelo que tem como alvo o .NET Framework 4.5.  Nomeie o projeto de hello "WadExample" e clique em Okey.
3. Selecione **Função de Trabalho** e clique em Ok. Olá projeto será criado.
4. Em **Solution Explorer**, clique duas vezes em Olá **WorkerRole1** arquivo de propriedades.
5. Em Olá **configuração** guia, desmarque a opção **habilitar o diagnóstico** toodisable Diagnostics 1.0 (SDK do Azure 2.4 e anterior).
6. Criar sua solução tooverify que ter nenhum erro.

### <a name="step-2-instrument-your-code"></a>Etapa 2: Instrumentalizar seu código
Substitua o conteúdo de saudação do WorkerRole.cs com hello código a seguir. Olá classe SampleEventSourceWriter, herdado de saudação [classe EventSource][EventSource Class], implementa quatro métodos de registro em log: **SendEnums**, **MessageMethod** , **SetOther** e **HighFreq**. Olá toohello do primeiro parâmetro **WriteEvent** método define Olá ID para o evento respectivos hello. Olá método Run implementa um loop infinito que chama cada Olá log métodos implementados em Olá **SampleEventSourceWriter** classe a cada 10 segundos.

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a>Etapa 3: Implantar sua Função de Trabalho

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. Implantar seu tooAzure da função de trabalho de dentro do Visual Studio selecionando Olá **WadExample** projeto no hello, em seguida, no Gerenciador de soluções **publicar** de saudação **criar** menu.
2. Escolha sua assinatura.
3. Em Olá **configurações de publicação do Microsoft Azure** caixa de diálogo, selecione **criar novo...** .
4. Em Olá **criar serviço de nuvem e a conta de armazenamento** caixa de diálogo, insira um **nome** (por exemplo, "WadExample") e selecione uma região ou grupo de afinidade.
5. Saudação de conjunto **ambiente** muito**preparo**.
6. Modifique quaisquer outras **Configurações** como for apropriado e clique em **Publicar**.
7. Após a implantação for concluída, verifique se no hello portal do Azure que seu serviço de nuvem está em um **executando** estado.

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>Etapa 4: Criar o arquivo de configuração de diagnóstico e instalar extensão Olá
1. Baixe a definição de esquema de arquivo de configuração pública Olá executando Olá comando PowerShell a seguir:

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. Adicionar um tooyour do arquivo XML **WorkerRole1** projeto clicando em Olá **WorkerRole1** do projeto e selecione **adicionar** -> **Novo Item...** -> **Itens do Visual C#** -> **Dados** -> **Arquivo XML**. Nome de arquivo hello "WadExample.xml".

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Associe Olá WadConfig.xsd com o arquivo de configuração de saudação. Certifique-se de janela do editor de WadExample.xml de saudação é a janela ativa de saudação. Pressione **F4** tooopen Olá **propriedades** janela. Clique em Olá **esquemas** propriedade Olá **propriedades** janela. Clique em Olá **...** em Olá **esquemas** propriedade. Clique em Olá **adicionar...** botão e navegue toohello local onde você salvou o arquivo XSD de saudação e arquivo hello selecione WadConfig.xsd. Clique em **OK**.

4. Substitua o conteúdo de Olá Olá WadExample.xml do arquivo de configuração com hello XML a seguir e salve o arquivo hello. Esse arquivo de configuração define algumas toocollect de contadores de desempenho: uma para a utilização da CPU e uma utilização de memória. Configuração de saudação define quatro eventos de saudação correspondente toohello métodos na classe SampleEventSourceWriter de saudação.

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>Etapa 5: instalar o Diagnostics em sua Função de Trabalho
Olá cmdlets do PowerShell para gerenciar o diagnóstico em uma função web ou de trabalho são: Set AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension e AzureServiceDiagnosticsExtension remover.

1. Abra o PowerShell do Azure.
2. Executar Olá script tooinstall diagnóstico em sua função de trabalho (substitua *StorageAccountKey* com chave de conta de armazenamento Olá para sua conta de armazenamento wadexample e *config_path* com caminho Olá toohello *WadExample.xml* arquivo):

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>Etapa 6: Examinar os dados de telemetria
No Visual Studio de saudação **Server Explorer**, navegar a conta de armazenamento do toohello wadexample. Após o serviço de nuvem Olá execução cerca de cinco (5) minutos, você deverá ver tabelas Olá **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** e **WADSetOtherTable**. Clique duas vezes em uma saudação tabelas tooview Olá da telemetria que foram coletada.

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>Esquema de arquivo de configuração
o arquivo de configuração de diagnóstico Olá define os valores que são parâmetros de configuração de diagnóstico de tooinitialize usado quando o agente de diagnóstico Olá é iniciado. Consulte Olá [referência de esquema mais recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) para os valores válidos e exemplos.

## <a name="troubleshooting"></a>Solucionar problemas
Caso tenha problemas, veja [Solucionando problemas do Diagnóstico do Azure](../azure-diagnostics-troubleshooting.md) para obter ajuda com problemas comuns.

## <a name="next-steps"></a>Próximas etapas
[Consulte uma lista de artigos diagnósticos de máquina virtual do Azure relacionados](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) dados de saudação toochange está coletando, solucionar problemas ou saber mais sobre o diagnóstico em geral.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
