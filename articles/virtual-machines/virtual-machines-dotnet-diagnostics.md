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
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="4d063-103">Habilitando o diagnóstico em Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="4d063-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="4d063-104">Confira [Visão geral do Diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md) para obter informações preliminares sobre o Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d063-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="4d063-105">Como tooEnable diagnósticos em uma máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="4d063-105">How tooEnable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="4d063-106">Este passo a passo descreve como tooremotely instalar diagnóstico tooan máquina virtual do Azure em um computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="4d063-106">This walk through describes how tooremotely install Diagnostics tooan Azure virtual machine from a development computer.</span></span> <span data-ttu-id="4d063-107">Você também aprenderá como tooimplement um aplicativo que é executado na máquina virtual do Azure e emite os dados de telemetria usando Olá .NET [classe EventSource][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="4d063-107">You also learn how tooimplement an application that runs on that Azure virtual machine and emits telemetry data using hello .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="4d063-108">Diagnóstico do Azure é usado toocollect Olá telemetria e armazená-lo em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d063-108">Azure Diagnostics is used toocollect hello telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="4d063-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4d063-109">Pre-requisites</span></span>
<span data-ttu-id="4d063-110">Este passo a passo pressupõe que você tem uma assinatura do Azure e estiver usando o Visual Studio de 2017 com Olá SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d063-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with hello Azure SDK.</span></span> <span data-ttu-id="4d063-111">Se você não tiver uma assinatura do Azure, você pode se inscrever para Olá [avaliação gratuita][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="4d063-111">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="4d063-112">Certifique-se muito[instalar e configurar o Azure PowerShell versão 0.8.7 ou posterior][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="4d063-112">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="4d063-113">Etapa 1: Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4d063-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="4d063-114">No computador de desenvolvimento, inicialize o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4d063-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="4d063-115">No Visual Studio de saudação **Server Explorer** expanda **Azure**, clique com botão direito **máquinas virtuais** , em seguida, selecione **criar Máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="4d063-115">In hello Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="4d063-116">Selecione sua assinatura do Azure no hello **escolher uma assinatura** caixa de diálogo e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4d063-116">Select your Azure subscription in hello **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="4d063-117">Selecione **Windows Server 2012 R2 Datacenter, junho de 2017** em Olá **selecionar uma imagem de máquina Virtual** caixa de diálogo e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4d063-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in hello **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="4d063-118">Em Olá **configurações básicas de máquina Virtual**, defina o nome da máquina virtual Olá muito "wadexample".</span><span class="sxs-lookup"><span data-stu-id="4d063-118">In hello **Virtual Machine Basic Settings**, set hello virtual machine name too"wadexample".</span></span> <span data-ttu-id="4d063-119">Defina o nome de usuário e senha do Administrador clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4d063-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="4d063-120">Em Olá **as configurações de serviço de nuvem** caixa de diálogo Criar um novo serviço de nuvem chamado "wadexampleVM".</span><span class="sxs-lookup"><span data-stu-id="4d063-120">In hello **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="4d063-121">Crie uma nova conta de Armazenamento chamada "wadexample" e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4d063-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="4d063-122">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4d063-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="4d063-123">Etapa 2: Criar o seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="4d063-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="4d063-124">No computador de desenvolvimento, inicialize o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4d063-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="4d063-125">Crie um novo aplicativo de console do Visual C# que se destina ao .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="4d063-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="4d063-126">Nomeie o projeto de hello "WadExampleVM".</span><span class="sxs-lookup"><span data-stu-id="4d063-126">Name hello project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="4d063-128">Substitua o conteúdo de saudação do Program.cs com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="4d063-128">Replace hello contents of Program.cs with hello following code.</span></span> <span data-ttu-id="4d063-129">Olá classe **SampleEventSourceWriter** implementa quatro métodos de registro em log: **SendEnums**, **MessageMethod**, **SetOther** e  **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="4d063-129">hello class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="4d063-130">saudação de primeiro parâmetro toohello método WriteEvent define a ID de Olá para evento respectivos hello.</span><span class="sxs-lookup"><span data-stu-id="4d063-130">hello first parameter toohello WriteEvent method defines hello ID for hello respective event.</span></span> <span data-ttu-id="4d063-131">Olá método Run implementa um loop infinito que chama cada Olá log métodos implementados em Olá **SampleEventSourceWriter** classe a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="4d063-131">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

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
4. <span data-ttu-id="4d063-132">Salvar arquivo hello e selecione **compilar solução** de saudação **criar** menu toobuild seu código.</span><span class="sxs-lookup"><span data-stu-id="4d063-132">Save hello file and select **Build Solution** from hello **Build** menu toobuild your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="4d063-133">Etapa 3: Implantar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="4d063-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="4d063-134">Clique duas vezes em Olá **WadExampleVM** project no **Solution Explorer** e escolha **Abrir pasta no Explorador de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="4d063-134">Right-click on hello **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="4d063-135">Navegue toohello *bin\Debug* pasta e cópia Olá a todos os arquivos (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="4d063-135">Navigate toohello *bin\Debug* folder and copy all hello files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="4d063-136">Em **Server Explorer** com o botão direito na máquina virtual de saudação e escolha **conectar usando a área de trabalho remota**.</span><span class="sxs-lookup"><span data-stu-id="4d063-136">In **Server Explorer** right-click on hello virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="4d063-137">Uma vez conectado toohello VM crie uma pasta chamada WadExampleVM e cole os arquivos do aplicativo na pasta de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d063-137">Once connected toohello VM create a folder named WadExampleVM and paste your application files into hello folder.</span></span>
5. <span data-ttu-id="4d063-138">Inicie o aplicativo hello WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="4d063-138">Launch hello application WadExampleVM.exe.</span></span> <span data-ttu-id="4d063-139">Você verá uma janela de console em branco.</span><span class="sxs-lookup"><span data-stu-id="4d063-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a><span data-ttu-id="4d063-140">Etapa 4: Criar a configuração de diagnóstico e instalar Olá extensão</span><span class="sxs-lookup"><span data-stu-id="4d063-140">Step 4: Create your Diagnostics configuration and install hello Extension</span></span>
1. <span data-ttu-id="4d063-141">Baixe o computador de desenvolvimento Olá configuração pública arquivo esquema definição tooyour executando Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d063-141">Download hello public configuration file schema definition tooyour development computer by executing hello following PowerShell command:</span></span>

     <span data-ttu-id="4d063-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="4d063-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="4d063-143">Abra um novo arquivo XML no Visua Studio, seja em um projeto que você já abriu, ou em uma instância do Visual Studio com nenhum projeto aberto.</span><span class="sxs-lookup"><span data-stu-id="4d063-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="4d063-144">No Visual Studio, selecione **Adicionar** -> **Novo Item…**</span><span class="sxs-lookup"><span data-stu-id="4d063-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="4d063-145"> -> **Itens do Visual C#** -> **Dados** -> **Arquivo XML**.</span><span class="sxs-lookup"><span data-stu-id="4d063-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="4d063-146">Nome de arquivo hello "WadExample.xml"</span><span class="sxs-lookup"><span data-stu-id="4d063-146">Name hello file "WadExample.xml"</span></span>
3. <span data-ttu-id="4d063-147">Associe Olá WadConfig.xsd com o arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d063-147">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="4d063-148">Certifique-se de janela do editor de WadExample.xml de saudação é a janela ativa de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d063-148">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="4d063-149">Pressione **F4** tooopen Olá **propriedades** janela.</span><span class="sxs-lookup"><span data-stu-id="4d063-149">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="4d063-150">Clique em Olá **esquemas** propriedade Olá **propriedades** janela.</span><span class="sxs-lookup"><span data-stu-id="4d063-150">Click on hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="4d063-151">Clique em Olá **...**</span><span class="sxs-lookup"><span data-stu-id="4d063-151">Click hello **…**</span></span> <span data-ttu-id="4d063-152">em Olá **esquemas** propriedade.</span><span class="sxs-lookup"><span data-stu-id="4d063-152">in hello **Schemas** property.</span></span> <span data-ttu-id="4d063-153">Clique em Olá **adicionar...**</span><span class="sxs-lookup"><span data-stu-id="4d063-153">Click hello **Add…**</span></span> <span data-ttu-id="4d063-154">botão e navegue toohello local onde você salvou o arquivo XSD de saudação e arquivo hello selecione WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="4d063-154">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="4d063-155">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d063-155">Click **OK**.</span></span>
4. <span data-ttu-id="4d063-156">Substitua o conteúdo de Olá Olá WadExample.xml do arquivo de configuração com hello XML a seguir e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4d063-156">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="4d063-157">Esse arquivo de configuração define algumas toocollect de contadores de desempenho: uma para a utilização da CPU e uma utilização de memória.</span><span class="sxs-lookup"><span data-stu-id="4d063-157">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="4d063-158">Configuração de saudação define quatro eventos de saudação correspondente toohello métodos na classe SampleEventSourceWriter de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d063-158">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="4d063-159">Etapa 5: instalar remotamente o Diagnostics na sua Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="4d063-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="4d063-160">Olá cmdlets do PowerShell para gerenciar o diagnóstico em uma máquina virtual são: Set AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension e AzureVMDiagnosticsExtension remover.</span><span class="sxs-lookup"><span data-stu-id="4d063-160">hello PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="4d063-161">No computador do desenvolvedor, abra o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d063-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="4d063-162">Execute a instalação tooremotely de script hello diagnóstico na sua VM (substitua `<user>` com seu nome de diretório do usuário.</span><span class="sxs-lookup"><span data-stu-id="4d063-162">Execute hello script tooremotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="4d063-163">Substituir `<StorageAccountKey>` com chave de conta de armazenamento Olá para sua conta de armazenamento wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="4d063-163">Replace `<StorageAccountKey>` with hello storage account key for your wadexamplevm storage account):</span></span>
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
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="4d063-164">Etapa 6: Examinar os dados de telemetria</span><span class="sxs-lookup"><span data-stu-id="4d063-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="4d063-165">No Visual Studio de saudação **Server Explorer** navegar a conta de armazenamento do toohello wadexample.</span><span class="sxs-lookup"><span data-stu-id="4d063-165">In hello Visual Studio **Server Explorer** navigate toohello wadexample storage account.</span></span> <span data-ttu-id="4d063-166">Depois Olá VM está em execução cerca de 5 minutos, você deverá ver tabelas Olá **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** e **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="4d063-166">After hello VM has been running about 5 minutes you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="4d063-167">Clique duas vezes em uma saudação tabelas tooview Olá da telemetria que foram coletada.</span><span class="sxs-lookup"><span data-stu-id="4d063-167">Double-click on one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="4d063-169">Esquema de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="4d063-169">Configuration file schema</span></span>
<span data-ttu-id="4d063-170">o arquivo de configuração de diagnóstico Olá define os valores que são parâmetros de configuração de diagnóstico de tooinitialize usado quando o agente de diagnóstico Olá é iniciado.</span><span class="sxs-lookup"><span data-stu-id="4d063-170">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="4d063-171">Consulte Olá [referência de esquema mais recente](https://msdn.microsoft.com/library/azure/mt634524.aspx) para os valores válidos e exemplos.</span><span class="sxs-lookup"><span data-stu-id="4d063-171">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4d063-172">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="4d063-172">Troubleshooting</span></span>
<span data-ttu-id="4d063-173">Veja [Solucionando problemas do Diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="4d063-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d063-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d063-174">Next steps</span></span>
<span data-ttu-id="4d063-175">[Consulte uma lista de máquina virtual relacionados a artigos de diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) dados de saudação toochange está coletando, solucionar problemas ou saber mais sobre o diagnóstico em geral.</span><span class="sxs-lookup"><span data-stu-id="4d063-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
