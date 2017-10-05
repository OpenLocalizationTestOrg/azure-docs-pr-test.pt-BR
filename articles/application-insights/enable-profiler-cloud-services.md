---
title: "Habilitar o Azure Application Insights Profiler em um recurso dos Serviços de Nuvem | Microsoft Docs"
description: "Saiba como configurar o criador de perfil em um aplicativo ASP.NET hospedado por um recurso dos Serviços de Nuvem do Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 5ff062ac81dca9d8b205cec966d2a9c11a4005b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="0ce58-103">Habilitar o Application Insights Profiler em um recurso dos Serviços de Nuvem do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0ce58-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="0ce58-104">Este passo a passo demonstra como habilitar o Azure Application Insights Profiler em um aplicativo ASP.NET hospedado por um recurso dos Serviços de Nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce58-104">This walkthrough demonstrates how to enable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="0ce58-105">Os exemplos incluem suporte para Máquinas Virtuais do Azure, conjuntos de dimensionamento de máquinas virtuais e Service Fabric do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce58-105">The examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="0ce58-106">Todos os exemplos dependem de modelos que dão suporte ao modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ce58-106">The examples all rely on templates that support the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0ce58-107">Para saber mais sobre o modelo de implantação, leia [Implantação do Azure Resource Manager versus clássica: entenda os modelos de implantação e o estado de seus recursos](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="0ce58-107">For more information about the deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="0ce58-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0ce58-108">Overview</span></span>

<span data-ttu-id="0ce58-109">O diagrama a seguir ilustra como o criador de perfil funciona para os recursos dos Serviços de Nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce58-109">The following diagram illustrates how the profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="0ce58-110">Ele usa uma máquina virtual do Azure como exemplo.</span><span class="sxs-lookup"><span data-stu-id="0ce58-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="0ce58-111">![Visão geral](./media/enable-profiler-compute/overview.png) Para coletar informações de processamento e exibição no portal do Azure, você deve instalar o componente Agente de Diagnóstico para os recursos dos Serviços de Nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce58-111">![Overview](./media/enable-profiler-compute/overview.png) To collect information for processing and display on the Azure portal, you must install the Diagnostics Agent component for the Azure Cloud Services resources.</span></span> <span data-ttu-id="0ce58-112">O restante do passo a passo apresenta diretrizes sobre como instalar e configurar o Agente de Diagnóstico para habilitar o Application Insights Profiler.</span><span class="sxs-lookup"><span data-stu-id="0ce58-112">The rest of the walkthrough provides guidance on how to install and configure the Diagnostics Agent to enable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-the-walkthrough"></a><span data-ttu-id="0ce58-113">Pré-requisitos para o passo a passo</span><span class="sxs-lookup"><span data-stu-id="0ce58-113">Prerequisites for the walkthrough</span></span>

* <span data-ttu-id="0ce58-114">Um modelo de implantação do Resource Manager que instala os agentes de criador de perfil nas VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) ou conjuntos de dimensionamento ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="0ce58-114">A deployment Resource Manager template that installs the profiler agents on the VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="0ce58-115">Uma instância do Application Insights habilitada para criação de perfil.</span><span class="sxs-lookup"><span data-stu-id="0ce58-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="0ce58-116">Para obter instruções, confira [Habilitar o criador de perfil](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="0ce58-116">For instructions, see [Enable the profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="0ce58-117">.NET Framework 4.6.1 ou posterior instalado no recurso de destino dos Serviços de Nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce58-117">.NET Framework 4.6.1 or later installed on the target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="0ce58-118">Criar um grupo de recursos em sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="0ce58-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="0ce58-119">O seguinte exemplo demonstra como criar um grupo de recursos usando um script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0ce58-119">The following example demonstrates how to create a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-the-resource-group"></a><span data-ttu-id="0ce58-120">Criar um recurso Application Insights no grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0ce58-120">Create an Application Insights resource in the resource group</span></span>
<span data-ttu-id="0ce58-121">Na folha **Application Insights**, insira as informações do recurso, conforme mostrado neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ce58-121">On the **Application Insights** blade, enter the information for your resource, as shown in this example:</span></span> 

![Folha Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-the-azure-resource-manager-template"></a><span data-ttu-id="0ce58-123">Aplicar uma chave de instrumentação do Application Insights no modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0ce58-123">Apply an Application Insights instrumentation key in the Azure Resource Manager template</span></span>

1. <span data-ttu-id="0ce58-124">Caso ainda não tenha baixado o modelo, baixe-o do [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="0ce58-124">If you haven't downloaded the template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="0ce58-125">Localize a chave do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0ce58-125">Find the Application Insights key.</span></span>
   
   ![Local da chave](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="0ce58-127">Substitua o valor do modelo.</span><span class="sxs-lookup"><span data-stu-id="0ce58-127">Replace the template value.</span></span>
   
   ![Valor substituído no modelo](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-to-host-the-web-application"></a><span data-ttu-id="0ce58-129">Criar uma VM do Azure para hospedar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="0ce58-129">Create an Azure VM to host the web application</span></span>
1. <span data-ttu-id="0ce58-130">Crie uma cadeia de caracteres segura para salvar a senha.</span><span class="sxs-lookup"><span data-stu-id="0ce58-130">Create a secure string to save the password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="0ce58-131">Implante o modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ce58-131">Deploy the Azure Resource Manager template.</span></span>

   <span data-ttu-id="0ce58-132">Altere o diretório no console do PowerShell para a pasta que contém o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ce58-132">Change the directory in the PowerShell console to the folder that contains your Resource Manager template.</span></span> <span data-ttu-id="0ce58-133">Para implantar o modelo, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0ce58-133">To deploy the template, run the following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="0ce58-134">Depois que o script for executado com êxito, você deverá encontrar uma VM denominada **MyWindowsVM** em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0ce58-134">After the script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-the-vm"></a><span data-ttu-id="0ce58-135">Configurar Implantação da Web na VM</span><span class="sxs-lookup"><span data-stu-id="0ce58-135">Configure Web Deploy on the VM</span></span>
<span data-ttu-id="0ce58-136">Verifique se a Implantação da Web está habilitada na sua VM para que você possa publicar o aplicativo Web usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ce58-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="0ce58-137">Para instalar a Implantação da Web em uma VM manualmente por meio do WebPI, confira [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later) (Instalar e configurar a Implantação da Web no IIS 8.0 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="0ce58-137">To install Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="0ce58-138">Para obter um exemplo de como automatizar a instalação da Implantação da Web usando um modelo do Azure Resource Manager, confira [Create, configure, and deploy a web application to an Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/) (Criar, configurar e implantar um aplicativo Web em uma VM do Azure).</span><span class="sxs-lookup"><span data-stu-id="0ce58-138">For an example of how to automate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application to an Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="0ce58-139">Se você estiver implantando um aplicativo MVC ASP.NET, vá para o Gerenciador do Servidor, escolha **Adicionar Funções e Recursos** > **Servidor Web (IIS)** > **Servidor Web** > **Desenvolvimento de Aplicativo** e habilite o ASP.NET 4.5 no servidor.</span><span class="sxs-lookup"><span data-stu-id="0ce58-139">If you are deploying an ASP.NET MVC application, go to Server Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![Adicionar ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-the-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="0ce58-141">Instalar o SDK do Azure Application Insights para seu projeto</span><span class="sxs-lookup"><span data-stu-id="0ce58-141">Install the Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="0ce58-142">Abra o aplicativo Web ASP.NET no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ce58-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="0ce58-143">Clique com o botão direito do mouse no projeto e escolha **Adicionar** > **Serviços Conectados**.</span><span class="sxs-lookup"><span data-stu-id="0ce58-143">Right-click the project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="0ce58-144">Selecione **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="0ce58-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="0ce58-145">Siga as instruções na página.</span><span class="sxs-lookup"><span data-stu-id="0ce58-145">Follow the instructions on the page.</span></span> <span data-ttu-id="0ce58-146">Selecione o recurso Application Insights que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0ce58-146">Select the Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="0ce58-147">Escolha o botão **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="0ce58-147">Select the **Register** button.</span></span>


## <a name="publish-the-project-to-an-azure-vm"></a><span data-ttu-id="0ce58-148">Publicar o projeto em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="0ce58-148">Publish the project to an Azure VM</span></span>
<span data-ttu-id="0ce58-149">Há várias maneiras de publicar um aplicativo para uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce58-149">There are several ways to publish an application to an Azure VM.</span></span> <span data-ttu-id="0ce58-150">Uma delas é usar o Virtual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="0ce58-150">One way is to use Visual Studio 2017.</span></span>

1. <span data-ttu-id="0ce58-151">Clique com o botão direito do mouse no projeto e escolha **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="0ce58-151">Right-click the project and select **Publish**.</span></span>

2. <span data-ttu-id="0ce58-152">Escolha **Máquinas Virtuais do Microsoft Azure** como o destino de publicação e siga as etapas.</span><span class="sxs-lookup"><span data-stu-id="0ce58-152">Select **Microsoft Azure Virtual Machines** as the publish target and follow the steps.</span></span>

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="0ce58-154">Execute um teste de carga no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ce58-154">Run a load test against your application.</span></span> <span data-ttu-id="0ce58-155">Você deve ver os resultados na página da Web do portal da instância do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0ce58-155">You should see results on the Application Insights instance portal webpage.</span></span>


## <a name="enable-the-profiler"></a><span data-ttu-id="0ce58-156">Habilitar o criador de perfil</span><span class="sxs-lookup"><span data-stu-id="0ce58-156">Enable the profiler</span></span>
1. <span data-ttu-id="0ce58-157">Vá para a folha **Desempenho** do Application Insights e escolha **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="0ce58-157">Go to your Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Ícone Configurar](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="0ce58-159">Selecione **Habilitar o Criador de Perfil**.</span><span class="sxs-lookup"><span data-stu-id="0ce58-159">Select **Enable Profiler**.</span></span>
   
   ![Ícone Habilitar o Criador de Perfil](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-to-your-application"></a><span data-ttu-id="0ce58-161">Adicionar um teste de desempenho para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="0ce58-161">Add a performance test to your application</span></span>
<span data-ttu-id="0ce58-162">Siga estas etapas para que seja possível coletar alguns dados de exemplo a serem exibidos no Application Insights Profiler:</span><span class="sxs-lookup"><span data-stu-id="0ce58-162">Follow these steps so we can collect some sample data to be displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="0ce58-163">Navegue até o recurso Application Insights que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0ce58-163">Browse to the Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="0ce58-164">Vá para a folha **Disponibilidade** e adicione um teste de desempenho que envie solicitações da Web para a URL do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ce58-164">Go to the **Availability** blade and add a performance test that sends web requests to your application URL.</span></span> 

   ![Adicionar teste de desempenho](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="0ce58-166">Exibir seus dados de desempenho</span><span class="sxs-lookup"><span data-stu-id="0ce58-166">View your performance data</span></span>

1. <span data-ttu-id="0ce58-167">Aguarde de 10 a 15 minutos para que o criador de perfil colete e analise os dados.</span><span class="sxs-lookup"><span data-stu-id="0ce58-167">Wait 10-15 minutes for the profiler to collect and analyze the data.</span></span> 

2. <span data-ttu-id="0ce58-168">Vá para a folha **Desempenho** em seu recurso Application Insights e veja o desempenho do aplicativo quando ele está sob carga.</span><span class="sxs-lookup"><span data-stu-id="0ce58-168">Go to the **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Exibição do desempenho](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="0ce58-170">Escolha o ícone em **Exemplos** para abrir a folha **Exibição de Rastreamento**.</span><span class="sxs-lookup"><span data-stu-id="0ce58-170">Select the icon under **Examples** to open the **Trace View** blade.</span></span>

   ![Abrindo a folha Exibição de Rastreamento](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="0ce58-172">Trabalhar com um modelo existente</span><span class="sxs-lookup"><span data-stu-id="0ce58-172">Work with an existing template</span></span>

1. <span data-ttu-id="0ce58-173">Localize a declaração do recurso Diagnóstico do Azure em seu modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="0ce58-173">Locate the Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="0ce58-174">Caso não tenha uma declaração, você poderá criar uma semelhante à declaração no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="0ce58-174">If you don't have a declaration, you can create one that resembles the declaration in the following example.</span></span> <span data-ttu-id="0ce58-175">Você pode atualizar o modelo no [site do Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ce58-175">You can update the template from the [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="0ce58-176">Altere o editor de `Microsoft.Azure.Diagnostics` para `AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="0ce58-176">Change the publisher from `Microsoft.Azure.Diagnostics` to `AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="0ce58-177">Para `typeHandlerVersion`, use `0.0`.</span><span class="sxs-lookup"><span data-stu-id="0ce58-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="0ce58-178">Verifique se `autoUpgradeMinorVersion` está definido como `true`.</span><span class="sxs-lookup"><span data-stu-id="0ce58-178">Make sure that `autoUpgradeMinorVersion` is set to `true`.</span></span>

5. <span data-ttu-id="0ce58-179">Adicione a nova instância do coletor `ApplicationInsightsProfiler` no objeto de configurações `WadCfg`, conforme mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ce58-179">Add the new `ApplicationInsightsProfiler` sink instance in the `WadCfg` settings object, as shown in the following example:</span></span>

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter the Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-the-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="0ce58-180">Habilitar o criador de perfil em conjuntos de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="0ce58-180">Enable the profiler on virtual machine scale sets</span></span>
<span data-ttu-id="0ce58-181">Para ver como habilitar o criador de perfil, baixe o modelo [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json).</span><span class="sxs-lookup"><span data-stu-id="0ce58-181">To see how to enable the profiler, download the [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="0ce58-182">Aplique as mesmas alterações em um modelo de VM ao recurso de extensão de diagnóstico para o conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0ce58-182">Apply the same changes in a VM template to the diagnostics extension resource for the virtual machine scale set.</span></span>

<span data-ttu-id="0ce58-183">Verifique se cada instância no conjunto de dimensionamento tem acesso à Internet.</span><span class="sxs-lookup"><span data-stu-id="0ce58-183">Make sure that each instance in the scale set has access to the internet.</span></span> <span data-ttu-id="0ce58-184">O Agente do Criador de Perfil pode enviar as amostras coletadas ao Application Insights para exibição e análise.</span><span class="sxs-lookup"><span data-stu-id="0ce58-184">The Profiler Agent can then send the collected samples to Application Insights for display and analysis.</span></span>

## <a name="enable-the-profiler-on-service-fabric-applications"></a><span data-ttu-id="0ce58-185">Habilitar o criador de perfil em aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0ce58-185">Enable the profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="0ce58-186">Provisione o cluster do Service Fabric para que ele tenha a extensão do Diagnóstico do Azure que instala o Agente do Criador de Perfil.</span><span class="sxs-lookup"><span data-stu-id="0ce58-186">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent.</span></span>

2. <span data-ttu-id="0ce58-187">Instale o SDK do Application Insights no projeto e configure a chave do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0ce58-187">Install the Application Insights SDK in the project and configure the Application Insights key.</span></span>

3. <span data-ttu-id="0ce58-188">Adicione o código do aplicativo à telemetria de instrumento.</span><span class="sxs-lookup"><span data-stu-id="0ce58-188">Add application code to instrument telemetry.</span></span>

### <a name="provision-the-service-fabric-cluster-to-have-the-azure-diagnostics-extension-that-installs-the-profiler-agent"></a><span data-ttu-id="0ce58-189">Provisionar o cluster do Service Fabric para que ele tenha a extensão do Diagnóstico do Azure que instala o Agente do Criador de Perfil</span><span class="sxs-lookup"><span data-stu-id="0ce58-189">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent</span></span>
<span data-ttu-id="0ce58-190">Um cluster do Service Fabric, que pode ser seguro ou não.</span><span class="sxs-lookup"><span data-stu-id="0ce58-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="0ce58-191">Você pode definir um cluster de gateway como não seguro, de modo que ele não exija um certificado para o acesso.</span><span class="sxs-lookup"><span data-stu-id="0ce58-191">You can set one gateway cluster to be non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="0ce58-192">Clusters que hospedam lógica de negócios e dados devem ser seguros.</span><span class="sxs-lookup"><span data-stu-id="0ce58-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="0ce58-193">Você pode habilitar o criador de perfil em clusters seguros e não seguros do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0ce58-193">You can enable the profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="0ce58-194">Este passo a passo usa um cluster não seguro como um exemplo para explicar as alterações necessárias para habilitar o criador de perfil.</span><span class="sxs-lookup"><span data-stu-id="0ce58-194">This walkthrough uses a non-secure cluster as an example to explain what changes are required to enable the profiler.</span></span> <span data-ttu-id="0ce58-195">Você pode provisionar um cluster seguro da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="0ce58-195">You can provision a secure cluster in the same way.</span></span>

1. <span data-ttu-id="0ce58-196">Baixe o [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="0ce58-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="0ce58-197">Assim como feito nas VMs e nos conjuntos de dimensionamento de máquinas virtuais, substitua `Application_Insights_Key` pela chave do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="0ce58-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. <span data-ttu-id="0ce58-198">Implante o modelo usando um script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0ce58-198">Deploy the template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-the-application-insights-sdk-in-the-project-and-configure-the-application-insights-key"></a><span data-ttu-id="0ce58-199">Instalar o SDK do Application Insights no projeto e configurar a chave do Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ce58-199">Install the Application Insights SDK in the project and configure the Application Insights key</span></span>
<span data-ttu-id="0ce58-200">Instale o SDK do Application Insights do [pacote do NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="0ce58-200">Install the Application Insights SDK from the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="0ce58-201">Certifique-se de instalar uma versão estável 2.3 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0ce58-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="0ce58-202">Para obter informações sobre como configurar o Application Insights em seus projetos, confira [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Usando o Service Fabric com o Application Insights).</span><span class="sxs-lookup"><span data-stu-id="0ce58-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-to-instrument-telemetry"></a><span data-ttu-id="0ce58-203">Adicionar o código do aplicativo à telemetria de instrumento</span><span class="sxs-lookup"><span data-stu-id="0ce58-203">Add application code to instrument telemetry</span></span>
1. <span data-ttu-id="0ce58-204">Em qualquer parte de código que você queira instrumentar, adicione uma instrução de uso em torno dele.</span><span class="sxs-lookup"><span data-stu-id="0ce58-204">For any piece of code that you want to instrument, add a using statement around it.</span></span> 

   <span data-ttu-id="0ce58-205">No exemplo a seguir, o método `RunAsync` está desempenhando seu papel e a classe `telemetryClient` captura a telemetria depois que ela é iniciada.</span><span class="sxs-lookup"><span data-stu-id="0ce58-205">In the following  example, the `RunAsync` method is doing some work, and the `telemetryClient` class captures the telemetry after it starts.</span></span> <span data-ttu-id="0ce58-206">O evento precisa de um nome exclusivo no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ce58-206">The event needs a unique name across the application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace the following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. <span data-ttu-id="0ce58-207">Implante seu aplicativo para o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0ce58-207">Deploy your application to the Service Fabric cluster.</span></span> <span data-ttu-id="0ce58-208">Aguarde por 10 minutos até o aplicativo ser executado.</span><span class="sxs-lookup"><span data-stu-id="0ce58-208">Wait for the app to run for 10 minutes.</span></span> <span data-ttu-id="0ce58-209">Para obter melhor efeito, você pode executar um teste de carga no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ce58-209">For better effect, you can run a load test on the app.</span></span> <span data-ttu-id="0ce58-210">Vá para a folha **Desempenho** do portal do Application Insights e aparecerão exemplos de rastreamentos de criação de perfil.</span><span class="sxs-lookup"><span data-stu-id="0ce58-210">Go to the Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable the Profiler on Cloud Services applications
[TODO]
## Enable the Profiler on classic Azure Virtual Machines
[TODO]
## Enable the Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="0ce58-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ce58-211">Next steps</span></span>

- <span data-ttu-id="0ce58-212">Encontre ajuda para solução de problemas do criador de perfil em [Solução de problemas do criador de perfil](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="0ce58-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="0ce58-213">Leia mais sobre o criador de perfil em [Application Insights Profiler](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="0ce58-213">Read more about the profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
