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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Habilitar o Application Insights Profiler em um recurso dos Serviços de Nuvem do Microsoft Azure

Este passo a passo demonstra como tooenable criador de perfil de informações de aplicativo do Azure em um aplicativo ASP.NET hospedado por um recurso de serviços de nuvem do Azure. exemplos de saudação incluem suporte para máquinas virtuais do Azure e conjuntos de escala de máquina virtual do Azure Service Fabric. todos os exemplos de saudação confiam nos modelos que oferecem suporte ao modelo de implantação do Azure Resource Manager hello. Para obter mais informações sobre o modelo de implantação hello, examine [do Azure Resource Manager versus implantação clássica: entender os modelos de implantação e Olá estado de seus recursos](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Visão geral

Olá diagrama a seguir ilustra como o criador de perfil Olá funciona para os recursos de serviços de nuvem do Azure. Ele usa uma máquina virtual do Azure como exemplo.

![Visão geral](./media/enable-profiler-compute/overview.png) toocollect informações para processamento e exibição em Olá portal do Azure, você deve instalar o componente do agente de diagnóstico Olá para recursos de serviços de nuvem do Azure hello. Olá rest Olá passo a passo fornece orientação sobre como tooinstall e configurar Olá agente de diagnóstico tooenable criador de perfil do Application Insights.

## <a name="prerequisites-for-hello-walkthrough"></a>Pré-requisitos para Olá passo a passo

* Um modelo do Gerenciador de recursos de implantação que instala agentes do criador de perfil de saudação em Olá VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) ou conjuntos de escala ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Uma instância do Application Insights habilitada para criação de perfil. Para obter instruções, consulte [habilitar perfil Olá](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* Recursos de serviços de nuvem do Azure de destino do .NET framework 4.6.1 ou posterior instalado em hello.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Criar um grupo de recursos em sua assinatura do Azure
saudação de exemplo a seguir demonstra como toocreate um recurso de grupo usando um script do PowerShell:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a>Criar um recurso do Application Insights no grupo de recursos de saudação
Em Olá **Application Insights** folha, insira as informações de Olá para o recurso, conforme mostrado neste exemplo: 

![Folha Application Insights](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a>Aplicar uma chave de instrumentação do Application Insights no modelo do Azure Resource Manager Olá

1. Se você ainda não baixou modelo Olá ainda, baixe-o do [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Localize a chave do Application Insights hello.
   
   ![Local da chave de saudação](./media/enable-profiler-compute/copyaikey.png)

3. Substitua o valor do modelo de saudação.
   
   ![Valor substituído no modelo de saudação](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a>Criar um aplicativo web do Azure VM toohost Olá
1. Crie uma senha de saudação do toosave de cadeia de caracteres segura.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Implante o modelo do Azure Resource Manager hello.

   Alterar diretório Olá Olá console toohello pasta do PowerShell que contém o modelo do Gerenciador de recursos. modelo de saudação toodeploy, execute Olá comando a seguir:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Depois que o script hello é executado com êxito, você deve encontrar uma VM denominada **MyWindowsVM** em seu grupo de recursos.

## <a name="configure-web-deploy-on-hello-vm"></a>Configurar a implantação da Web em Olá VM
Verifique se a Implantação da Web está habilitada na sua VM para que você possa publicar o aplicativo Web usando o Visual Studio.

tooinstall implantação da Web em uma máquina virtual manualmente por meio do WebPI, consulte [instalando e configurando o implantação da Web no IIS 8.0 ou posterior](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Para obter um exemplo de como tooautomate instalar a implantação da Web usando um modelo do Gerenciador de recursos do Azure, consulte [criar, configurar e implantar um aplicativo de web tooan VM do Azure](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Se você estiver implantando um aplicativo ASP.NET MVC, vá tooServer Manager, selecione **adicionar funções e recursos** > **servidor Web (IIS)** > **Web Server**  >  **Desenvolvimento de aplicativos**e habilitar o ASP.NET 4.5 no servidor.

![Adicionar ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a>Instalar hello Azure SDK do Application Insights para seu projeto
1. Abra o aplicativo Web ASP.NET no Visual Studio.

2. Clique com botão direito hello e selecione **adicionar** > **serviços conectados**.

3. Selecione **Application Insights**.

4. Siga as instruções de saudação na página de saudação. Selecione o recurso do Application Insights Olá que você criou anteriormente.

5. Selecione Olá **registrar** botão.


## <a name="publish-hello-project-tooan-azure-vm"></a>Publicar Olá projeto tooan VM do Azure
Há várias toopublish de maneiras tooan um aplicativo do Azure VM. Uma maneira é toouse 2017 do Visual Studio.

1. Clique com botão direito hello e selecione **publicar**.

2. Selecione **máquinas virtuais do Microsoft Azure** como Olá publicar destino e siga as etapas de saudação.

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. Execute um teste de carga no seu aplicativo. Você deve ver resultados Olá Application Insights instância portal página da Web.


## <a name="enable-hello-profiler"></a>Habilitar o criador de perfil de saudação
1. Vá tooyour Application Insights **desempenho** folha e selecione **configurar**.
   
   ![Ícone Configurar](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Selecione **Habilitar o Criador de Perfil**.
   
   ![Ícone Habilitar o Criador de Perfil](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a>Adicionar um aplicativo de tooyour de teste de desempenho
Para que possamos coletar algumas toobe de dados de exemplo exibido no criador de perfil do Application Insights, siga estas etapas:

1. Procure o recurso do Application Insights toohello que você criou anteriormente. 

2. Vá toohello **disponibilidade** folha e adicione um teste de desempenho que envia a URL do aplicativo web solicitações tooyour. 

   ![Adicionar teste de desempenho](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>Exibir seus dados de desempenho

1. Aguarde 10 a 15 minutos para Olá profiler toocollect e analisar dados de saudação. 

2. Vá toohello **desempenho** folha no recurso do Application Insights e exibição de desempenho do seu aplicativo quando ele está sob carga.

   ![Exibição do desempenho](./media/enable-profiler-compute/aiperformance.png)

3. Ícone de saudação selecione **exemplos** tooopen Olá **exibição de rastreamento** folha.

   ![Abrir a folha de exibição de rastreamento Olá](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Trabalhar com um modelo existente

1. Localize a declaração de recursos de diagnóstico do Azure Olá em seu modelo de implantação.
   
   Se você não tiver uma declaração, você pode criar um que é semelhante a declaração de saudação em Olá exemplo a seguir. Você pode atualizar o modelo de saudação do hello [site do Gerenciador de recursos do Azure](https://resources.azure.com).

2. Editor de alteração de saudação do `Microsoft.Azure.Diagnostics` muito`AIP.Diagnostics.Test`.

3. Para `typeHandlerVersion`, use `0.0`.

4. Verifique se `autoUpgradeMinorVersion` está definido muito`true`.

5. Adicionar Olá novo `ApplicationInsightsProfiler` instância do coletor no hello `WadCfg` objeto de configurações, conforme mostrado no exemplo a seguir de saudação:

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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a>Habilitar o criador de perfil de saudação em conjuntos de escala de máquinas virtuais
toosee como tooenable Olá profiler, download Olá [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) modelo. Aplica Olá mesmo alterações em um recurso de extensão VM modelo toohello diagnóstico para o conjunto de escalas da máquina virtual hello.

Certifique-se de que cada instância no conjunto de escala Olá tem toohello de acesso à internet. Olá criador de perfil de agente, em seguida, pode enviar amostras de saudação coletada tooApplication Insights para exibição e análise.

## <a name="enable-hello-profiler-on-service-fabric-applications"></a>Habilitar o criador de perfil de saudação em aplicativos do Service Fabric
1. Saudação de provisionar Service Fabric cluster toohave Olá diagnóstico do Azure extensão que instala Olá criador de perfil de agente.

2. Instalar Olá SDK do Application Insights no projeto de saudação e configurar a chave do Application Insights hello.

3. Adicione telemetria de tooinstrument de código do aplicativo.

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a>Provisionar Olá Service Fabric cluster toohave Olá extensão de diagnóstico do Azure que instala Olá criador de perfil de agente
Um cluster do Service Fabric, que pode ser seguro ou não. Você pode definir um toobe de cluster de gateway não seguro para que ele não requer um certificado para o acesso. Clusters que hospedam lógica de negócios e dados devem ser seguros. Você pode habilitar o criador de perfil de saudação em clusters de malha do serviço seguras e não seguras. Este passo a passo usa um cluster de não seguro como um exemplo tooexplain as alterações que são necessárias tooenable Olá profiler. Você pode provisionar um cluster seguro no hello mesma maneira.

1. Baixe o [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json). Assim como feito nas VMs e nos conjuntos de dimensionamento de máquinas virtuais, substitua `Application_Insights_Key` pela chave do Application Insights:

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

2. Implante o modelo hello usando um script do PowerShell:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a>Instalar Olá SDK do Application Insights no projeto hello e configurar a chave do Application Insights Olá
Instalar Olá SDK do Application Insights do hello [pacote NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Certifique-se de instalar uma versão estável 2.3 ou posterior. 

Para obter informações sobre como configurar o Application Insights em seus projetos, confira [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md) (Usando o Service Fabric com o Application Insights).

### <a name="add-application-code-tooinstrument-telemetry"></a>Adicionar telemetria de tooinstrument de código do aplicativo
1. Para qualquer parte do código que você deseja tooinstrument, adicione um usando a instrução ao redor dele. 

   Em Olá exemplo a seguir, Olá `RunAsync` método é realizar algum trabalho e Olá `telemetryClient` classe captura telemetria Olá após ele ser iniciado. evento Olá precisa de um nome exclusivo em um aplicativo hello.

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

2. Implante o cluster do aplicativo toohello Service Fabric. Aguarde Olá aplicativo toorun por 10 minutos. Para obter melhor efeito, você pode executar um teste de carga no aplicativo hello. Do portal do Application Insights vá toohello **desempenho** folha e você deverá ver exemplos de rastreamentos de criação de perfil.

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Próximas etapas

- Encontre ajuda para solução de problemas do criador de perfil em [Solução de problemas do criador de perfil](app-insights-profiler.md#troubleshooting).

- Leia mais sobre o criador de perfil de saudação em [criador de perfil do aplicativo Insights](app-insights-profiler.md).
