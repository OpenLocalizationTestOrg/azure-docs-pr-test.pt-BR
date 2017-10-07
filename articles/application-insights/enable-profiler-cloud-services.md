---
title: "aaaEnable criador de perfil de informações de aplicativo do Azure em um recurso de serviços de nuvem | Microsoft Docs"
description: "Saiba como tooset o criador de perfil de saudação em um aplicativo ASP.NET hospedado por um recurso de serviços de nuvem do Azure."
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
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="8b425-103">Habilitar o Application Insights Profiler em um recurso dos Serviços de Nuvem do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8b425-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="8b425-104">Este passo a passo demonstra como tooenable criador de perfil de informações de aplicativo do Azure em um aplicativo ASP.NET hospedado por um recurso de serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b425-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="8b425-105">exemplos de saudação incluem suporte para máquinas virtuais do Azure e conjuntos de escala de máquina virtual do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8b425-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="8b425-106">todos os exemplos de saudação confiam nos modelos que oferecem suporte ao modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="8b425-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="8b425-107">Para obter mais informações sobre o modelo de implantação hello, examine [do Azure Resource Manager versus implantação clássica: entender os modelos de implantação e Olá estado de seus recursos](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="8b425-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="8b425-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8b425-108">Overview</span></span>

<span data-ttu-id="8b425-109">Olá diagrama a seguir ilustra como o criador de perfil Olá funciona para os recursos de serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b425-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="8b425-110">Ele usa uma máquina virtual do Azure como exemplo.</span><span class="sxs-lookup"><span data-stu-id="8b425-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="8b425-111">![Visão geral](./media/enable-profiler-compute/overview.png) toocollect informações para processamento e exibição em Olá portal do Azure, você deve instalar o componente do agente de diagnóstico Olá para recursos de serviços de nuvem do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8b425-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="8b425-112">Olá rest Olá passo a passo fornece orientação sobre como tooinstall e configurar Olá agente de diagnóstico tooenable criador de perfil do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8b425-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="8b425-113">Pré-requisitos para Olá passo a passo</span><span class="sxs-lookup"><span data-stu-id="8b425-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="8b425-114">Um modelo do Gerenciador de recursos de implantação que instala agentes do criador de perfil de saudação em Olá VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) ou conjuntos de escala ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="8b425-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="8b425-115">Uma instância do Application Insights habilitada para criação de perfil.</span><span class="sxs-lookup"><span data-stu-id="8b425-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="8b425-116">Para obter instruções, consulte [habilitar perfil Olá](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="8b425-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="8b425-117">Recursos de serviços de nuvem do Azure de destino do .NET framework 4.6.1 ou posterior instalado em hello.</span><span class="sxs-lookup"><span data-stu-id="8b425-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="8b425-118">Criar um grupo de recursos em sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="8b425-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="8b425-119">saudação de exemplo a seguir demonstra como toocreate um recurso de grupo usando um script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8b425-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="8b425-120">Criar um recurso do Application Insights no grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="8b425-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="8b425-121">Em Olá **Application Insights** folha, insira as informações de Olá para o recurso, conforme mostrado neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="8b425-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![Folha Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="8b425-123">Aplicar uma chave de instrumentação do Application Insights no modelo do Azure Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="8b425-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="8b425-124">Se você ainda não baixou modelo Olá ainda, baixe-o do [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="8b425-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="8b425-125">Localize a chave do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="8b425-125">Find hello Application Insights key.</span></span>
   
   ![Local da chave de saudação](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="8b425-127">Substitua o valor do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b425-127">Replace hello template value.</span></span>
   
   ![Valor substituído no modelo de saudação](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="8b425-129">Criar um aplicativo web do Azure VM toohost Olá</span><span class="sxs-lookup"><span data-stu-id="8b425-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="8b425-130">Crie uma senha de saudação do toosave de cadeia de caracteres segura.</span><span class="sxs-lookup"><span data-stu-id="8b425-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="8b425-131">Implante o modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="8b425-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="8b425-132">Alterar diretório Olá Olá console toohello pasta do PowerShell que contém o modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8b425-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="8b425-133">modelo de saudação toodeploy, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b425-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="8b425-134">Depois que o script hello é executado com êxito, você deve encontrar uma VM denominada **MyWindowsVM** em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8b425-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="8b425-135">Configurar a implantação da Web em Olá VM</span><span class="sxs-lookup"><span data-stu-id="8b425-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="8b425-136">Verifique se a Implantação da Web está habilitada na sua VM para que você possa publicar o aplicativo Web usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b425-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="8b425-137">tooinstall implantação da Web em uma máquina virtual manualmente por meio do WebPI, consulte [instalando e configurando o implantação da Web no IIS 8.0 ou posterior](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="8b425-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="8b425-138">Para obter um exemplo de como tooautomate instalar a implantação da Web usando um modelo do Gerenciador de recursos do Azure, consulte [criar, configurar e implantar um aplicativo de web tooan VM do Azure](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="8b425-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="8b425-139">Se você estiver implantando um aplicativo ASP.NET MVC, vá tooServer Manager, selecione **adicionar funções e recursos** > **servidor Web (IIS)** > **Web Server**  >  **Desenvolvimento de aplicativos**e habilitar o ASP.NET 4.5 no servidor.</span><span class="sxs-lookup"><span data-stu-id="8b425-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![Adicionar ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="8b425-141">Instalar hello Azure SDK do Application Insights para seu projeto</span><span class="sxs-lookup"><span data-stu-id="8b425-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="8b425-142">Abra o aplicativo Web ASP.NET no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b425-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="8b425-143">Clique com botão direito hello e selecione **adicionar** > **serviços conectados**.</span><span class="sxs-lookup"><span data-stu-id="8b425-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="8b425-144">Selecione **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="8b425-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="8b425-145">Siga as instruções de saudação na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b425-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="8b425-146">Selecione o recurso do Application Insights Olá que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8b425-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="8b425-147">Selecione Olá **registrar** botão.</span><span class="sxs-lookup"><span data-stu-id="8b425-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="8b425-148">Publicar Olá projeto tooan VM do Azure</span><span class="sxs-lookup"><span data-stu-id="8b425-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="8b425-149">Há várias toopublish de maneiras tooan um aplicativo do Azure VM.</span><span class="sxs-lookup"><span data-stu-id="8b425-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="8b425-150">Uma maneira é toouse 2017 do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b425-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="8b425-151">Clique com botão direito hello e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8b425-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="8b425-152">Selecione **máquinas virtuais do Microsoft Azure** como Olá publicar destino e siga as etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b425-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="8b425-154">Execute um teste de carga no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b425-154">Run a load test against your application.</span></span> <span data-ttu-id="8b425-155">Você deve ver resultados Olá Application Insights instância portal página da Web.</span><span class="sxs-lookup"><span data-stu-id="8b425-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="8b425-156">Habilitar o criador de perfil de saudação</span><span class="sxs-lookup"><span data-stu-id="8b425-156">Enable hello profiler</span></span>
1. <span data-ttu-id="8b425-157">Vá tooyour Application Insights **desempenho** folha e selecione **configurar**.</span><span class="sxs-lookup"><span data-stu-id="8b425-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Ícone Configurar](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="8b425-159">Selecione **Habilitar o Criador de Perfil**.</span><span class="sxs-lookup"><span data-stu-id="8b425-159">Select **Enable Profiler**.</span></span>
   
   ![Ícone Habilitar o Criador de Perfil](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="8b425-161">Adicionar um aplicativo de tooyour de teste de desempenho</span><span class="sxs-lookup"><span data-stu-id="8b425-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="8b425-162">Para que possamos coletar algumas toobe de dados de exemplo exibido no criador de perfil do Application Insights, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8b425-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="8b425-163">Procure o recurso do Application Insights toohello que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8b425-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="8b425-164">Vá toohello **disponibilidade** folha e adicione um teste de desempenho que envia a URL do aplicativo web solicitações tooyour.</span><span class="sxs-lookup"><span data-stu-id="8b425-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![Adicionar teste de desempenho](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="8b425-166">Exibir seus dados de desempenho</span><span class="sxs-lookup"><span data-stu-id="8b425-166">View your performance data</span></span>

1. <span data-ttu-id="8b425-167">Aguarde 10 a 15 minutos para Olá profiler toocollect e analisar dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b425-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="8b425-168">Vá toohello **desempenho** folha no recurso do Application Insights e exibição de desempenho do seu aplicativo quando ele está sob carga.</span><span class="sxs-lookup"><span data-stu-id="8b425-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Exibição do desempenho](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="8b425-170">Ícone de saudação selecione **exemplos** tooopen Olá **exibição de rastreamento** folha.</span><span class="sxs-lookup"><span data-stu-id="8b425-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![Abrir a folha de exibição de rastreamento Olá](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="8b425-172">Trabalhar com um modelo existente</span><span class="sxs-lookup"><span data-stu-id="8b425-172">Work with an existing template</span></span>

1. <span data-ttu-id="8b425-173">Localize a declaração de recursos de diagnóstico do Azure Olá em seu modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="8b425-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="8b425-174">Se você não tiver uma declaração, você pode criar um que é semelhante a declaração de saudação em Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="8b425-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="8b425-175">Você pode atualizar o modelo de saudação do hello [site do Gerenciador de recursos do Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b425-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="8b425-176">Editor de alteração de saudação do `Microsoft.Azure.Diagnostics` muito`AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="8b425-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="8b425-177">Para `typeHandlerVersion`, use `0.0`.</span><span class="sxs-lookup"><span data-stu-id="8b425-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="8b425-178">Verifique se `autoUpgradeMinorVersion` está definido muito`true`.</span><span class="sxs-lookup"><span data-stu-id="8b425-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="8b425-179">Adicionar Olá novo `ApplicationInsightsProfiler` instância do coletor no hello `WadCfg` objeto de configurações, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="8b425-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

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
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="8b425-180">Habilitar o criador de perfil de saudação em conjuntos de escala de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8b425-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="8b425-181">toosee como tooenable Olá profiler, download Olá [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) modelo.</span><span class="sxs-lookup"><span data-stu-id="8b425-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="8b425-182">Aplica Olá mesmo alterações em um recurso de extensão VM modelo toohello diagnóstico para o conjunto de escalas da máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="8b425-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="8b425-183">Certifique-se de que cada instância no conjunto de escala Olá tem toohello de acesso à internet.</span><span class="sxs-lookup"><span data-stu-id="8b425-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="8b425-184">Olá criador de perfil de agente, em seguida, pode enviar amostras de saudação coletada tooApplication Insights para exibição e análise.</span><span class="sxs-lookup"><span data-stu-id="8b425-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="8b425-185">Habilitar o criador de perfil de saudação em aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8b425-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="8b425-186">Saudação de provisionar Service Fabric cluster toohave Olá diagnóstico do Azure extensão que instala Olá criador de perfil de agente.</span><span class="sxs-lookup"><span data-stu-id="8b425-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="8b425-187">Instalar Olá SDK do Application Insights no projeto de saudação e configurar a chave do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="8b425-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="8b425-188">Adicione telemetria de tooinstrument de código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b425-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="8b425-189">Provisionar Olá Service Fabric cluster toohave Olá extensão de diagnóstico do Azure que instala Olá criador de perfil de agente</span><span class="sxs-lookup"><span data-stu-id="8b425-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="8b425-190">Um cluster do Service Fabric, que pode ser seguro ou não.</span><span class="sxs-lookup"><span data-stu-id="8b425-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="8b425-191">Você pode definir um toobe de cluster de gateway não seguro para que ele não requer um certificado para o acesso.</span><span class="sxs-lookup"><span data-stu-id="8b425-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="8b425-192">Clusters que hospedam lógica de negócios e dados devem ser seguros.</span><span class="sxs-lookup"><span data-stu-id="8b425-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="8b425-193">Você pode habilitar o criador de perfil de saudação em clusters de malha do serviço seguras e não seguras.</span><span class="sxs-lookup"><span data-stu-id="8b425-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="8b425-194">Este passo a passo usa um cluster de não seguro como um exemplo tooexplain as alterações que são necessárias tooenable Olá profiler.</span><span class="sxs-lookup"><span data-stu-id="8b425-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="8b425-195">Você pode provisionar um cluster seguro no hello mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="8b425-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="8b425-196">Baixe o [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="8b425-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="8b425-197">Assim como feito nas VMs e nos conjuntos de dimensionamento de máquinas virtuais, substitua `Application_Insights_Key` pela chave do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="8b425-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

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

2. <span data-ttu-id="8b425-198">Implante o modelo hello usando um script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8b425-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="8b425-199">Instalar Olá SDK do Application Insights no projeto hello e configurar a chave do Application Insights Olá</span><span class="sxs-lookup"><span data-stu-id="8b425-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="8b425-200">Instalar Olá SDK do Application Insights do hello [pacote NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="8b425-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="8b425-201">Certifique-se de instalar uma versão estável 2.3 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8b425-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="8b425-202">Para obter informações sobre como configurar o Application Insights em seus projetos, confira [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Usando o Service Fabric com o Application Insights).</span><span class="sxs-lookup"><span data-stu-id="8b425-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="8b425-203">Adicionar telemetria de tooinstrument de código do aplicativo</span><span class="sxs-lookup"><span data-stu-id="8b425-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="8b425-204">Para qualquer parte do código que você deseja tooinstrument, adicione um usando a instrução ao redor dele.</span><span class="sxs-lookup"><span data-stu-id="8b425-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="8b425-205">Em Olá exemplo a seguir, Olá `RunAsync` método é realizar algum trabalho e Olá `telemetryClient` classe captura telemetria Olá após ele ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="8b425-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="8b425-206">evento Olá precisa de um nome exclusivo em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8b425-206">hello event needs a unique name across hello application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
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

2. <span data-ttu-id="8b425-207">Implante o cluster do aplicativo toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8b425-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="8b425-208">Aguarde Olá aplicativo toorun por 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="8b425-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="8b425-209">Para obter melhor efeito, você pode executar um teste de carga no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8b425-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="8b425-210">Do portal do Application Insights vá toohello **desempenho** folha e você deverá ver exemplos de rastreamentos de criação de perfil.</span><span class="sxs-lookup"><span data-stu-id="8b425-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="8b425-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b425-211">Next steps</span></span>

- <span data-ttu-id="8b425-212">Encontre ajuda para solução de problemas do criador de perfil em [Solução de problemas do criador de perfil](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="8b425-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="8b425-213">Leia mais sobre o criador de perfil de saudação em [criador de perfil do aplicativo Insights](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="8b425-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
