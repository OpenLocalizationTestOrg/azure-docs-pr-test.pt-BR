---
title: "Como usar o diagnóstico do Azure (.NET) com os Serviços de Nuvem | Microsoft Docs"
description: "Usando o diagnóstico do Azure para coletar dados dos Serviços de Nuvem do Azure para depuração, medição de desempenho, monitoramento, análise de tráfego e muito mais."
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
ms.openlocfilehash: 333d2f26ce043a167fb84858c8327cb39e868ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="bdc40-103">Habilitando o Diagnóstico do Azure nos Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="bdc40-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="bdc40-104">Confira [Visão geral do Diagnóstico do Azure](../azure-diagnostics.md) para obter informações preliminares sobre o Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc40-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-worker-role"></a><span data-ttu-id="bdc40-105">Como habilitar o Diagnostics em uma Função do Trabalho</span><span class="sxs-lookup"><span data-stu-id="bdc40-105">How to Enable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="bdc40-106">Este passo a passo descreve como implementar uma função de trabalho do Azure que emite dados de telemetria usando o .NET EventSource Class.</span><span class="sxs-lookup"><span data-stu-id="bdc40-106">This walkthrough describes how to implement an Azure worker role that emits telemetry data using the .NET EventSource class.</span></span> <span data-ttu-id="bdc40-107">O Diagnóstico do Azure é usado para coletar os dados de telemetria e armazená-los em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc40-107">Azure Diagnostics is used to collect the telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="bdc40-108">Ao criar uma função de trabalho, o Visual Studio permite automaticamente O Diagnóstico 1.0 como parte da solução em SDKs do Azure para .NET 2.4 e versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="bdc40-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of the solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="bdc40-109">As instruções a seguir descrevem o processo de criação da função de trabalho, desabilitando o Diagnóstico 1.0 por meio da solução e implantando o Diagnóstico 1.2 ou 1.3 para sua função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="bdc40-109">The following instructions describe the process for creating the worker role, disabling Diagnostics 1.0 from the solution, and deploying Diagnostics 1.2 or 1.3 to your worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bdc40-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bdc40-110">Prerequisites</span></span>
<span data-ttu-id="bdc40-111">Esse artigo assume que você tem uma assinatura do Azure e está usando o Visual Studio com o SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc40-111">This article assumes you have an Azure subscription and are using Visual Studio with the Azure SDK.</span></span> <span data-ttu-id="bdc40-112">Se você não tiver uma assinatura do Azure, será possível se inscrever para uma [Avaliação Gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="bdc40-112">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="bdc40-113">Certifique-se de [Instalar e configurar o Azure PowerShell, versão 0.8.7 ou posterior][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="bdc40-113">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="bdc40-114">Etapa 1: criar uma função de trabalho</span><span class="sxs-lookup"><span data-stu-id="bdc40-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="bdc40-115">Inicie o **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="bdc40-116">Crie um projeto **Serviço de Nuvem do Azure** no modelo **Nuvem** destinado ao .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="bdc40-116">Create an **Azure Cloud Service** project from the **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="bdc40-117">Atribua o nome "WadExample" ao projeto e clique em Ok.</span><span class="sxs-lookup"><span data-stu-id="bdc40-117">Name the project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="bdc40-118">Selecione **Função de Trabalho** e clique em Ok.</span><span class="sxs-lookup"><span data-stu-id="bdc40-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="bdc40-119">O projeto será criado.</span><span class="sxs-lookup"><span data-stu-id="bdc40-119">The project will be created.</span></span>
4. <span data-ttu-id="bdc40-120">No **Gerenciador de Soluções**, clique duas vezes no arquivo de propriedades **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-120">In **Solution Explorer**, double-click the **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="bdc40-121">Na guia **Configuração**, desmarque **Habilitar Diagnóstico** para desabilitar o Diagnostics 1.0 (SDK 2.4 do Azure e mais recente).</span><span class="sxs-lookup"><span data-stu-id="bdc40-121">In the **Configuration** tab, un-check **Enable Diagnostics** to disable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="bdc40-122">Compile sua solução para verificar que você não tem erros.</span><span class="sxs-lookup"><span data-stu-id="bdc40-122">Build your solution to verify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="bdc40-123">Etapa 2: Instrumentalizar seu código</span><span class="sxs-lookup"><span data-stu-id="bdc40-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="bdc40-124">Substitua os conteúdos do WorkerRole.cs pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="bdc40-124">Replace the contents of WorkerRole.cs with the following code.</span></span> <span data-ttu-id="bdc40-125">A classe SampleEventSourceWriter, herdada da [classe EventSource][EventSource Class], implementa quatro métodos de registro em log: **SendEnums**, **MessageMethod**, **SetOther** e **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-125">The class SampleEventSourceWriter, inherited from the [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="bdc40-126">O primeiro parâmetro para o método **WriteEvent** define a ID para o respectivo evento.</span><span class="sxs-lookup"><span data-stu-id="bdc40-126">The first parameter to the **WriteEvent** method defines the ID for the respective event.</span></span> <span data-ttu-id="bdc40-127">O método Executar implementa um loop infinito que chama cada um dos métodos de registro implementados na classe **SampleEventSourceWriter** a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="bdc40-127">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

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
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums to int for efficient logging.
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

                // Emit several events every time we go through the loop
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
            // Set the maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="bdc40-128">Etapa 3: Implantar sua Função de Trabalho</span><span class="sxs-lookup"><span data-stu-id="bdc40-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="bdc40-129">Implante sua função de trabalho para o Azure no Visual Studio selecionando o projeto **WadExample** no Gerenciador de Soluções, em seguida, **Publicar** no menu **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-129">Deploy your worker role to Azure from within Visual Studio by selecting the **WadExample** project in the Solution Explorer then **Publish** from the **Build** menu.</span></span>
2. <span data-ttu-id="bdc40-130">Escolha sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bdc40-130">Choose your subscription.</span></span>
3. <span data-ttu-id="bdc40-131">Na caixa de diálogo **Configurações de Publicação do Microsoft Azure**, selecione **Criar Novo...**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-131">In the **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="bdc40-132">Na caixa de diálogo **Criar Serviço de Nuvem e Conta de Armazenamento**, insira um **Nome** (por exemplo, "WadExample") e selecione uma região ou grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="bdc40-132">In the **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="bdc40-133">Defina o **Ambiente** para **Preparo**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-133">Set the **Environment** to **Staging**.</span></span>
6. <span data-ttu-id="bdc40-134">Modifique quaisquer outras **Configurações** como for apropriado e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="bdc40-135">Após a implantação ter sido concluída, verifique no Portal do Azure se seu serviço de nuvem está em estado de **Execução**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-135">After deployment has completed, verify in the Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-the-extension"></a><span data-ttu-id="bdc40-136">Etapa 4: Criar seu arquivo de configuração do Diagnostics e instalar a extensão</span><span class="sxs-lookup"><span data-stu-id="bdc40-136">Step 4: Create your Diagnostics configuration file and install the extension</span></span>
1. <span data-ttu-id="bdc40-137">Baixe a definição do esquema do arquivo de configuração pública ao executar o seguinte comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bdc40-137">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="bdc40-138">Adicionar um arquivo XML para sua **WorkerRole1** projeto clicando no **WorkerRole1** do projeto e selecione **adicionar** -> **Novo Item...**</span><span class="sxs-lookup"><span data-stu-id="bdc40-138">Add an XML file to your **WorkerRole1** project by right-clicking on the **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="bdc40-139"> -> **Itens do Visual C#** -> **Dados** -> **Arquivo XML**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="bdc40-140">Nomeie o arquivo como "WadExample.xml".</span><span class="sxs-lookup"><span data-stu-id="bdc40-140">Name the file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="bdc40-142">Associe o WadConfig.xsd com o arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="bdc40-142">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="bdc40-143">Certifique-se de que a janela do editor WadExample.xml é uma janela ativa.</span><span class="sxs-lookup"><span data-stu-id="bdc40-143">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="bdc40-144">Pressione **F4** para abrir a janela **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-144">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="bdc40-145">Clique na propriedade **Schemas** da janela **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-145">Click the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="bdc40-146">Clique em**...**</span><span class="sxs-lookup"><span data-stu-id="bdc40-146">Click the **…**</span></span> <span data-ttu-id="bdc40-147">in the **Esquemas** .</span><span class="sxs-lookup"><span data-stu-id="bdc40-147">in the **Schemas** property.</span></span> <span data-ttu-id="bdc40-148">Clique em **Adicionar…**</span><span class="sxs-lookup"><span data-stu-id="bdc40-148">Click the **Add…**</span></span> <span data-ttu-id="bdc40-149">e navegue até o local onde você salvou o arquivo XSD e selecione o arquivo WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="bdc40-149">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="bdc40-150">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-150">Click **OK**.</span></span>

4. <span data-ttu-id="bdc40-151">Substitua os conteíudos do arquivo de configuração WadExample.xml com o seguinte XML e salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="bdc40-151">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="bdc40-152">Este arquivo de configuração define dois contadores de desempenho a serem coletados: um relacionado à utilização da CPU e um ao uso de memória.</span><span class="sxs-lookup"><span data-stu-id="bdc40-152">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="bdc40-153">Após a configuração, defina os quatro eventos correspondentes aos métodos na classe SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="bdc40-153">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="bdc40-154">Etapa 5: instalar o Diagnostics em sua Função de Trabalho</span><span class="sxs-lookup"><span data-stu-id="bdc40-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="bdc40-155">Os cmdlets do PowerShell para gerenciar o diagnóstico em uma função web ou de trabalho são: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension e Remove-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="bdc40-155">The PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="bdc40-156">Abra o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc40-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="bdc40-157">Execute o script para instalar o Diagnostics na sua função de trabalho (substitua o *StorageAccountKey* com a chave de conta de armazenamento para sua conta de armazenamento wadexample e *config_path* com o caminho até o arquivo *WadExample.xml*):</span><span class="sxs-lookup"><span data-stu-id="bdc40-157">Execute the script to install Diagnostics on your worker role (replace *StorageAccountKey* with the storage account key for your wadexample storage account and *config_path* with the path to the *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="bdc40-158">Etapa 6: Examinar os dados de telemetria</span><span class="sxs-lookup"><span data-stu-id="bdc40-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="bdc40-159">No **Gerenciador de Servidores** do Visual Studio, navegue até a conta de armazenamento wadexample.</span><span class="sxs-lookup"><span data-stu-id="bdc40-159">In the Visual Studio **Server Explorer**, navigate to the wadexample storage account.</span></span> <span data-ttu-id="bdc40-160">Depois do serviço de nuvem ter sido executado por cerca de cinco (5) minutos, você deverá ver as tabelas **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** e **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="bdc40-160">After the cloud service has been running about five (5) minutes, you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="bdc40-161">Clique duas vezes em uma das tabelas para exibir a telemetria que foi coletada.</span><span class="sxs-lookup"><span data-stu-id="bdc40-161">Double-click one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="bdc40-163">Esquema de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="bdc40-163">Configuration File Schema</span></span>
<span data-ttu-id="bdc40-164">O arquivo de configuração do Diagnóstico define valores que são usados para inicializar as definições de configurações do diagnóstico quando o agente de diagnóstico é iniciado.</span><span class="sxs-lookup"><span data-stu-id="bdc40-164">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="bdc40-165">Veja a [referência de esquema mais recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) para obter valores válidos e exemplos.</span><span class="sxs-lookup"><span data-stu-id="bdc40-165">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bdc40-166">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="bdc40-166">Troubleshooting</span></span>
<span data-ttu-id="bdc40-167">Caso tenha problemas, veja [Solucionando problemas do Diagnóstico do Azure](../azure-diagnostics-troubleshooting.md) para obter ajuda com problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="bdc40-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdc40-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bdc40-168">Next Steps</span></span>
<span data-ttu-id="bdc40-169">[Veja uma lista de artigos sobre diagnóstico de máquina virtual do Azure](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) para alterar os dados coletados, solucionar problemas ou saber mais sobre o diagnóstico em geral.</span><span class="sxs-lookup"><span data-stu-id="bdc40-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
