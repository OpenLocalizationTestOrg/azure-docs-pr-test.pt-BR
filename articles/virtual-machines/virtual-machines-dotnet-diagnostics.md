---
title: "Como usar o diagnóstico do Azure em Máquinas Virtuais | Microsoft Docs"
description: "Usando o diagnóstico do Azure para coletar dados de Máquinas Virtuais do Azure para depuração, medição de desempenho, monitoramento, análise de tráfego e muito mais."
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
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="80405-103">Habilitando o diagnóstico em Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="80405-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="80405-104">Confira [Visão geral do Diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md) para obter informações preliminares sobre o Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="80405-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="80405-105">Como habilitar o Diagnostics em uma Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="80405-105">How to Enable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="80405-106">Esse passo a passo descreve como instalar remotamente o Diagnostics em uma máquina virtual do Azure a partir de um computador de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="80405-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span></span> <span data-ttu-id="80405-107">Você também aprende como implementar um aplicativo que executa nesta máquina virtual do Azure e emite dados de telemetria usando o .NET [EventSource Class][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="80405-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="80405-108">O Diagnóstico do Azure é usado para coletar a telemetria e armazená-la em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="80405-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="80405-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80405-109">Pre-requisites</span></span>
<span data-ttu-id="80405-110">Este passo a passo presume que você tenha uma assinatura do Azure e esteja usando o Visual Studio 2017 com o SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="80405-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with the Azure SDK.</span></span> <span data-ttu-id="80405-111">Se você não tiver uma assinatura do Azure, será possível se inscrever para uma [Avaliação Gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="80405-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="80405-112">Certifique-se de [Instalar e configurar o Azure PowerShell, versão 0.8.7 ou posterior][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="80405-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="80405-113">Etapa 1: Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="80405-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="80405-114">No computador de desenvolvimento, inicialize o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="80405-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="80405-115">No **Gerenciador de Servidores** do Visual Studio, expanda o **Azure**, clique com botão direito do mouse em **Máquinas Virtuais** e, em seguida, selecione **Criar Máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="80405-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="80405-116">Selecione sua assinatura do Azure na caixa de diálogo **Escolha uma assinatura** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="80405-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="80405-117">Selecione **Windows Server 2012 R2 Datacenter, junho de 2017** na caixa de diálogo **Selecionar uma Imagem da Máquina Virtual** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="80405-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in the **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="80405-118">Nas **Configurações Básicas da Máquina Virtual**, defina o nome da máquina virtual para "wadexample".</span><span class="sxs-lookup"><span data-stu-id="80405-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span></span> <span data-ttu-id="80405-119">Defina o nome de usuário e senha do Administrador clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="80405-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="80405-120">Na caixa de diálogo **Configurações de Serviço de Nuvem** , crie um novo serviço de nuvem chamado "wadexampleVM".</span><span class="sxs-lookup"><span data-stu-id="80405-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="80405-121">Crie uma nova conta de Armazenamento chamada "wadexample" e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="80405-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="80405-122">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="80405-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="80405-123">Etapa 2: Criar o seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="80405-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="80405-124">No computador de desenvolvimento, inicialize o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="80405-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="80405-125">Crie um novo aplicativo de console do Visual C# que se destina ao .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="80405-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="80405-126">Atribua o nome “WadExampleVM” ao projeto.</span><span class="sxs-lookup"><span data-stu-id="80405-126">Name the project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="80405-128">Substitua os conteúdos do Program.cs pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="80405-128">Replace the contents of Program.cs with the following code.</span></span> <span data-ttu-id="80405-129">A classe **SampleEventSourceWriter** implementa quatro métodos de registro em log: **SendEnums**, **MessageMethod**, **SetOther** e **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="80405-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="80405-130">O primeiro parâmetro para o método WriteEvent define a ID para o respectivo evento.</span><span class="sxs-lookup"><span data-stu-id="80405-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span></span> <span data-ttu-id="80405-131">O método Executar implementa um loop infinito que chama cada um dos métodos de registro implementados na classe **SampleEventSourceWriter** a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="80405-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
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

             // Emit several events every time we go through the loop
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
4. <span data-ttu-id="80405-132">Salve o arquivo e selecione **Compilar Solução** no menu **Compilar** para compilar seu código.</span><span class="sxs-lookup"><span data-stu-id="80405-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="80405-133">Etapa 3: Implantar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="80405-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="80405-134">Clique com o botão direito do mouse no projeto **WadExampleVM** no **Gerenciador de Soluções** e selecione **Abrir Pasta no Explorador de Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="80405-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="80405-135">Navegue para a pasta *bin\Debug* e copie todos os arquivos (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="80405-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="80405-136">No **Gerenciador de Servidores**, clique com o botão direito do mouse na máquina virtual e selecione **Conectar usando a Área de Trabalho Remota**.</span><span class="sxs-lookup"><span data-stu-id="80405-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="80405-137">Após conectado ao VM, crie uma pasta com o nome de WadExampleVM e cole seus arquivos do aplicativo na pasta.</span><span class="sxs-lookup"><span data-stu-id="80405-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span></span>
5. <span data-ttu-id="80405-138">Inicie o aplicativo WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="80405-138">Launch the application WadExampleVM.exe.</span></span> <span data-ttu-id="80405-139">Você verá uma janela de console em branco.</span><span class="sxs-lookup"><span data-stu-id="80405-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a><span data-ttu-id="80405-140">Etapa 4: Criar sua configuração do Diagnostics e instalar a extensão</span><span class="sxs-lookup"><span data-stu-id="80405-140">Step 4: Create your Diagnostics configuration and install the Extension</span></span>
1. <span data-ttu-id="80405-141">Baixe a definição do esquema do arquivo de configuração pública para seu computador de desenvolvimento ao executar o seguinte comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="80405-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span></span>

     <span data-ttu-id="80405-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="80405-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="80405-143">Abra um novo arquivo XML no Visua Studio, seja em um projeto que você já abriu, ou em uma instância do Visual Studio com nenhum projeto aberto.</span><span class="sxs-lookup"><span data-stu-id="80405-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="80405-144">No Visual Studio, selecione **Adicionar** -> **Novo Item…**</span><span class="sxs-lookup"><span data-stu-id="80405-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="80405-145"> -> **Itens do Visual C#** -> **Dados** -> **Arquivo XML**.</span><span class="sxs-lookup"><span data-stu-id="80405-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="80405-146">Nomeie o arquivo como "WadExample.xml"</span><span class="sxs-lookup"><span data-stu-id="80405-146">Name the file "WadExample.xml"</span></span>
3. <span data-ttu-id="80405-147">Associe o WadConfig.xsd com o arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="80405-147">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="80405-148">Certifique-se de que a janela do editor WadExample.xml é uma janela ativa.</span><span class="sxs-lookup"><span data-stu-id="80405-148">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="80405-149">Pressione **F4** para abrir a janela **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="80405-149">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="80405-150">Clique na propriedade **Schemas** da janela **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="80405-150">Click on the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="80405-151">Clique em**...**</span><span class="sxs-lookup"><span data-stu-id="80405-151">Click the **…**</span></span> <span data-ttu-id="80405-152">in the **Esquemas** .</span><span class="sxs-lookup"><span data-stu-id="80405-152">in the **Schemas** property.</span></span> <span data-ttu-id="80405-153">Clique em **Adicionar…**</span><span class="sxs-lookup"><span data-stu-id="80405-153">Click the **Add…**</span></span> <span data-ttu-id="80405-154">e navegue até o local onde você salvou o arquivo XSD e selecione o arquivo WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="80405-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="80405-155">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="80405-155">Click **OK**.</span></span>
4. <span data-ttu-id="80405-156">Substitua os conteíudos do arquivo de configuração WadExample.xml com o seguinte XML e salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="80405-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="80405-157">Este arquivo de configuração define dois contadores de desempenho a serem coletados: um relacionado à utilização da CPU e um ao uso de memória.</span><span class="sxs-lookup"><span data-stu-id="80405-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="80405-158">Após a configuração, defina os quatro eventos correspondentes aos métodos na classe SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="80405-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="80405-159">Etapa 5: instalar remotamente o Diagnostics na sua Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="80405-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="80405-160">Os cmdlets do PowerShell para gerenciar Diagnostics em uma máquina virtual são: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension e Remove-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="80405-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="80405-161">No computador do desenvolvedor, abra o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="80405-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="80405-162">Execute o script para instalar remotamente o Diagnóstico em sua VM (substitua `<user>` pelo nome do diretório do usuário.</span><span class="sxs-lookup"><span data-stu-id="80405-162">Execute the script to remotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="80405-163">Substitua `<StorageAccountKey>` pela chave de conta de armazenamento para sua conta de armazenamento wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="80405-163">Replace `<StorageAccountKey>` with the storage account key for your wadexamplevm storage account):</span></span>
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
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="80405-164">Etapa 6: Examinar os dados de telemetria</span><span class="sxs-lookup"><span data-stu-id="80405-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="80405-165">No **Gerenciador de Servidores** do Visual Studio, navegue até a conta de armazenamento wadexample.</span><span class="sxs-lookup"><span data-stu-id="80405-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span></span> <span data-ttu-id="80405-166">Depois que a VM estiver em execução por cerca de 5 minutos, você deve ver as tabelas **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** e **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="80405-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="80405-167">Clique duas vezes em uma das tabelas para exibir a telemetria que foi coletada.</span><span class="sxs-lookup"><span data-stu-id="80405-167">Double-click on one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="80405-169">Esquema de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="80405-169">Configuration file schema</span></span>
<span data-ttu-id="80405-170">O arquivo de configuração do Diagnóstico define valores que são usados para inicializar as definições de configurações do diagnóstico quando o agente de diagnóstico é iniciado.</span><span class="sxs-lookup"><span data-stu-id="80405-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="80405-171">Veja a [referência de esquema mais recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) para obter valores válidos e exemplos.</span><span class="sxs-lookup"><span data-stu-id="80405-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="80405-172">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="80405-172">Troubleshooting</span></span>
<span data-ttu-id="80405-173">Veja [Solucionando problemas do Diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="80405-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80405-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80405-174">Next steps</span></span>
<span data-ttu-id="80405-175">[Ver uma lista de artigos sobre o Diagnóstico do Azure relacionados a máquinas virtuais](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) para alterar os dados coletados, solucionar problemas ou saber mais sobre o diagnóstico em geral.</span><span class="sxs-lookup"><span data-stu-id="80405-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
