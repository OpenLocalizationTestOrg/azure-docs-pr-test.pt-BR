---
title: "aaaHow toouse o diagnóstico do Azure em máquinas virtuais | Microsoft Docs"
description: "Usando dados do diagnóstico do Azure toogather de máquinas virtuais do Azure para depuração, medir o desempenho, monitoramento, análise de tráfego e muito mais."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Habilitando o diagnóstico em Máquinas Virtuais do Azure
Confira [Visão geral do Diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md) para obter informações preliminares sobre o Diagnóstico do Azure.

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>Como tooEnable diagnósticos em uma máquina Virtual
Este passo a passo descreve como tooremotely instalar diagnóstico tooan máquina virtual do Azure em um computador de desenvolvimento. Você também aprenderá como tooimplement um aplicativo que é executado na máquina virtual do Azure e emite os dados de telemetria usando Olá .NET [classe EventSource][EventSource Class]. Diagnóstico do Azure é usado toocollect Olá telemetria e armazená-lo em uma conta de armazenamento do Azure.

### <a name="pre-requisites"></a>Pré-requisitos
Este passo a passo pressupõe que você tem uma assinatura do Azure e estiver usando o Visual Studio de 2017 com Olá SDK do Azure. Se você não tiver uma assinatura do Azure, você pode se inscrever para Olá [avaliação gratuita][Free Trial]. Certifique-se muito[instalar e configurar o Azure PowerShell versão 0.8.7 ou posterior][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>Etapa 1: Criar uma máquina virtual
1. No computador de desenvolvimento, inicialize o Visual Studio 2017.
2. No Visual Studio de saudação **Server Explorer** expanda **Azure**, clique com botão direito **máquinas virtuais** , em seguida, selecione **criar Máquina Virtual**.
3. Selecione sua assinatura do Azure no hello **escolher uma assinatura** caixa de diálogo e clique em **próximo**.
4. Selecione **Windows Server 2012 R2 Datacenter, junho de 2017** em Olá **selecionar uma imagem de máquina Virtual** caixa de diálogo e clique em **próximo**.
5. Em Olá **configurações básicas de máquina Virtual**, defina o nome da máquina virtual Olá muito "wadexample". Defina o nome de usuário e senha do Administrador clique em **Avançar**.
6. Em Olá **as configurações de serviço de nuvem** caixa de diálogo Criar um novo serviço de nuvem chamado "wadexampleVM". Crie uma nova conta de Armazenamento chamada "wadexample" e clique em **Avançar**.
7. Clique em **Criar**.

### <a name="step-2-create-your-application"></a>Etapa 2: Criar o seu aplicativo
1. No computador de desenvolvimento, inicialize o Visual Studio 2017.
2. Crie um novo aplicativo de console do Visual C# que se destina ao .NET Framework 4.5. Nomeie o projeto de hello "WadExampleVM".

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Substitua o conteúdo de saudação do Program.cs com hello código a seguir. Olá classe **SampleEventSourceWriter** implementa quatro métodos de registro em log: **SendEnums**, **MessageMethod**, **SetOther** e  **HighFreq**. saudação de primeiro parâmetro toohello método WriteEvent define a ID de Olá para evento respectivos hello. Olá método Run implementa um loop infinito que chama cada Olá log métodos implementados em Olá **SampleEventSourceWriter** classe a cada 10 segundos.

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. Salvar arquivo hello e selecione **compilar solução** de saudação **criar** menu toobuild seu código.

### <a name="step-3-deploy-your-application"></a>Etapa 3: Implantar seu aplicativo
1. Clique duas vezes em Olá **WadExampleVM** project no **Solution Explorer** e escolha **Abrir pasta no Explorador de arquivos**.
2. Navegue toohello *bin\Debug* pasta e cópia Olá a todos os arquivos (WadExampleVM.*)
3. Em **Server Explorer** com o botão direito na máquina virtual de saudação e escolha **conectar usando a área de trabalho remota**.
4. Uma vez conectado toohello VM crie uma pasta chamada WadExampleVM e cole os arquivos do aplicativo na pasta de saudação.
5. Inicie o aplicativo hello WadExampleVM.exe. Você verá uma janela de console em branco.

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>Etapa 4: Criar a configuração de diagnóstico e instalar Olá extensão
1. Baixe o computador de desenvolvimento Olá configuração pública arquivo esquema definição tooyour executando Olá comando PowerShell a seguir:

     (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
2. Abra um novo arquivo XML no Visua Studio, seja em um projeto que você já abriu, ou em uma instância do Visual Studio com nenhum projeto aberto. No Visual Studio, selecione **Adicionar** -> **Novo Item…** -> **Itens do Visual C#** -> **Dados** -> **Arquivo XML**. Nome de arquivo hello "WadExample.xml"
3. Associe Olá WadConfig.xsd com o arquivo de configuração de saudação. Certifique-se de janela do editor de WadExample.xml de saudação é a janela ativa de saudação. Pressione **F4** tooopen Olá **propriedades** janela. Clique em Olá **esquemas** propriedade Olá **propriedades** janela. Clique em Olá **...** em Olá **esquemas** propriedade. Clique em Olá **adicionar...** botão e navegue toohello local onde você salvou o arquivo XSD de saudação e arquivo hello selecione WadConfig.xsd. Clique em **OK**.
4. Substitua o conteúdo de Olá Olá WadExample.xml do arquivo de configuração com hello XML a seguir e salve o arquivo hello. Esse arquivo de configuração define algumas toocollect de contadores de desempenho: uma para a utilização da CPU e uma utilização de memória. Configuração de saudação define quatro eventos de saudação correspondente toohello métodos na classe SampleEventSourceWriter de saudação.

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>Etapa 5: instalar remotamente o Diagnostics na sua Máquina Virtual do Azure
Olá cmdlets do PowerShell para gerenciar o diagnóstico em uma máquina virtual são: Set AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension e AzureVMDiagnosticsExtension remover.

1. No computador do desenvolvedor, abra o PowerShell do Azure.
2. Execute a instalação tooremotely de script hello diagnóstico na sua VM (substitua `<user>` com seu nome de diretório do usuário. Substituir `<StorageAccountKey>` com chave de conta de armazenamento Olá para sua conta de armazenamento wadexamplevm):
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a>Etapa 6: Examinar os dados de telemetria
No Visual Studio de saudação **Server Explorer** navegar a conta de armazenamento do toohello wadexample. Depois Olá VM está em execução cerca de 5 minutos, você deverá ver tabelas Olá **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** e **WADSetOtherTable**. Clique duas vezes em uma saudação tabelas tooview Olá da telemetria que foram coletada.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Esquema de arquivo de configuração
o arquivo de configuração de diagnóstico Olá define os valores que são parâmetros de configuração de diagnóstico de tooinitialize usado quando o agente de diagnóstico Olá é iniciado. Consulte Olá [referência de esquema mais recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) para os valores válidos e exemplos.

## <a name="troubleshooting"></a>Solucionar problemas
Veja [Solucionando problemas do Diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) para obter mais informações.

## <a name="next-steps"></a>Próximas etapas
[Consulte uma lista de máquina virtual relacionados a artigos de diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) dados de saudação toochange está coletando, solucionar problemas ou saber mais sobre o diagnóstico em geral.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
