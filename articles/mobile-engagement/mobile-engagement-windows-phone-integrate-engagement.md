---
title: "Integração do SDK do Windows Phone Silverlight para o Engagement"
description: Como integrar o Azure Mobile Engagement com aplicativos do Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="f1958-103">Integração do SDK do Windows Phone Silverlight para o Engagement</span><span class="sxs-lookup"><span data-stu-id="f1958-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1958-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="f1958-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="f1958-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f1958-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="f1958-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f1958-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="f1958-107">Android</span><span class="sxs-lookup"><span data-stu-id="f1958-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="f1958-108">Este procedimento descreve a maneira mais simples para ativar as funções de monitoramento e de análise do Azure Mobile Engagement em seu aplicativo do Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="f1958-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="f1958-109">As etapas a seguir são suficientes para ativar o relatório de logs necessários para calcular todas as estatísticas sobre usuários, sessões, atividades, falhas e técnicas.</span><span class="sxs-lookup"><span data-stu-id="f1958-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="f1958-110">O relatório de logs necessário para calcular outras estatísticas, como eventos, erros e trabalhos deve ser feito manualmente usando a API do Engagement (consulte [Como usar a marcação avançada de API do Mobile Engagement no aplicativo Windows Phone](mobile-engagement-windows-phone-use-engagement-api.md) abaixo) já que essas estatísticas são dependentes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1958-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="f1958-111">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="f1958-111">Supported versions</span></span>
<span data-ttu-id="f1958-112">O SDK do Mobile Engagement do Windows Silverlight só pode ser integrado a aplicativos destinados ao:</span><span class="sxs-lookup"><span data-stu-id="f1958-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="f1958-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="f1958-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="f1958-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="f1958-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="f1958-115">Se o destino for o Windows Phone 8.1 (sem Silverlight), então consulte o [procedimento de integração do Windows Universal](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="f1958-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="f1958-116">Instalação do SDK do Silverlight do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f1958-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="f1958-117">O SDK do Mobile Engagement Windows Silverlight está disponível como um pacote do Nuget chamado *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="f1958-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="f1958-118">Você pode instalá-lo do Visual Studio Nuget Package Manager.</span><span class="sxs-lookup"><span data-stu-id="f1958-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="f1958-119">Adicione recursos</span><span class="sxs-lookup"><span data-stu-id="f1958-119">Add the capabilities</span></span>
<span data-ttu-id="f1958-120">O SDK do Engagement precisa de alguns recursos do SDK do Windows Phone Silverlight para funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="f1958-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="f1958-121">Abra o seu arquivo `WMAppManifest.xml` e certifique-se de que os seguintes recursos estão declarados no painel `Capabilities`:</span><span class="sxs-lookup"><span data-stu-id="f1958-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="f1958-122">Inicialize o SDK do Engagement</span><span class="sxs-lookup"><span data-stu-id="f1958-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="f1958-123">Configuração do Engagement</span><span class="sxs-lookup"><span data-stu-id="f1958-123">Engagement configuration</span></span>
<span data-ttu-id="f1958-124">A configuração do Engagement está centralizada no arquivo `Resources\EngagementConfiguration.xml` do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f1958-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="f1958-125">Edite esse arquivo para especificar :</span><span class="sxs-lookup"><span data-stu-id="f1958-125">Edit this file to specify :</span></span>

* <span data-ttu-id="f1958-126">A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="f1958-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="f1958-127">Se você quiser especificá-lo em tempo de execução, você pode chamar o método a seguir antes da inicialização do agente do Engagement:</span><span class="sxs-lookup"><span data-stu-id="f1958-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="f1958-128">A cadeia de conexão do seu aplicativo é exibida no Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1958-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="f1958-129">Inicialização do Engagement</span><span class="sxs-lookup"><span data-stu-id="f1958-129">Engagement initialization</span></span>
<span data-ttu-id="f1958-130">Quando você cria um novo projeto, um arquivo `App.xaml.cs` é gerado.</span><span class="sxs-lookup"><span data-stu-id="f1958-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="f1958-131">Essa classe herda de `Application` e contém vários métodos importantes.</span><span class="sxs-lookup"><span data-stu-id="f1958-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="f1958-132">Também poderá ser usado para inicializar o SDK do Engagement.</span><span class="sxs-lookup"><span data-stu-id="f1958-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="f1958-133">Modifique o `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="f1958-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="f1958-134">Adicione às suas instruções `using`:</span><span class="sxs-lookup"><span data-stu-id="f1958-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="f1958-135">Insira `EngagementAgent.Instance.Init` no método `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="f1958-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="f1958-136">Insira `EngagementAgent.Instance.OnActivated` no método `Application_Activated` :</span><span class="sxs-lookup"><span data-stu-id="f1958-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="f1958-137">Nós não recomendamos adicionar a inicialização do Engagement em outro lugar do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1958-137">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span> <span data-ttu-id="f1958-138">No entanto, lembre-se que o método `EngagementAgent.Instance.Init` é executado em um thread dedicado e não no thread da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="f1958-138">However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="f1958-139">Relatórios básicos</span><span class="sxs-lookup"><span data-stu-id="f1958-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="f1958-140">Método recomendado: sobrecarregar suas classes `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="f1958-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="f1958-141">Para ativar o relatório de todos os logs exigidos pelo Engagement para os usuários, sessões, atividades, falhas e das estatísticas técnicas de computação, você pode simplesmente fazer todas as suas subclasses `PhoneApplicationPage` herdarem das classes `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="f1958-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="f1958-142">Este é um exemplo de como fazer isso em uma página do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1958-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="f1958-143">Você pode fazer a mesma coisa em todas as páginas do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1958-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="f1958-144">Arquivo de código-fonte C#</span><span class="sxs-lookup"><span data-stu-id="f1958-144">C# Source file</span></span>
<span data-ttu-id="f1958-145">Modifique o arquivo `.xaml.cs` de paginação :</span><span class="sxs-lookup"><span data-stu-id="f1958-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="f1958-146">Adicione às suas instruções `using`:</span><span class="sxs-lookup"><span data-stu-id="f1958-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="f1958-147">Substituir `PhoneApplicationPage` por `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="f1958-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="f1958-148">**Sem o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="f1958-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="f1958-149">**Com o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="f1958-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="f1958-150">Se sua página herdar o método `OnNavigatedTo`, lembre-se de permitir a chamada `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="f1958-150">If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="f1958-151">Caso contrário, a atividade não será registrada.</span><span class="sxs-lookup"><span data-stu-id="f1958-151">Otherwise, the activity will not be reported.</span></span> <span data-ttu-id="f1958-152">Na verdade, o `EngagementPage` está chamando `StartActivity` dentro do método `OnNavigatedTo`.</span><span class="sxs-lookup"><span data-stu-id="f1958-152">Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="f1958-153">Arquivo XAML</span><span class="sxs-lookup"><span data-stu-id="f1958-153">XAML file</span></span>
<span data-ttu-id="f1958-154">Modifique o arquivo `.xaml` de paginação :</span><span class="sxs-lookup"><span data-stu-id="f1958-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="f1958-155">Adicione às suas declarações de namespaces :</span><span class="sxs-lookup"><span data-stu-id="f1958-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="f1958-156">Substituir `phone:PhoneApplicationPage` por `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="f1958-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="f1958-157">**Sem o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="f1958-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="f1958-158">**Com o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="f1958-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="f1958-159">Substitua o comportamento padrão</span><span class="sxs-lookup"><span data-stu-id="f1958-159">Override the default behavior</span></span>
<span data-ttu-id="f1958-160">Por padrão, o nome da classe da página é relatado como o nome da atividade, com e sem extras.</span><span class="sxs-lookup"><span data-stu-id="f1958-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="f1958-161">Se a classe usa o sufixo "Página", o Engagement irá removê-lo também.</span><span class="sxs-lookup"><span data-stu-id="f1958-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="f1958-162">Se você quiser substituir o comportamento padrão para o nome, basta adicionar isso ao seu código:</span><span class="sxs-lookup"><span data-stu-id="f1958-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="f1958-163">Se você desejar relatar algumas informações adicionais com a sua atividade, você pode adicionar isso ao seu código:</span><span class="sxs-lookup"><span data-stu-id="f1958-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="f1958-164">Esses métodos são chamados de dentro do método `OnNavigatedTo` da página.</span><span class="sxs-lookup"><span data-stu-id="f1958-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="f1958-165">Método alternativo: chame `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="f1958-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="f1958-166">Se você não pode ou não quer sobrecarregar as classes `PhoneApplicationPage`, em vez disso, você pode iniciar suas atividades chamando os métodos `EngagementAgent` diretamente.</span><span class="sxs-lookup"><span data-stu-id="f1958-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="f1958-167">Recomendamos chamar `StartActivity` dentro do método `OnNavigatedTo` da sua PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="f1958-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="f1958-168">Certifique-se de encerrar a sua sessão corretamente.</span><span class="sxs-lookup"><span data-stu-id="f1958-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="f1958-169">O SDK do iOS chama automaticamente o método `EndActivity` quando o aplicativo é fechado.</span><span class="sxs-lookup"><span data-stu-id="f1958-169">The SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="f1958-170">Portanto, é **ALTAMENTE** recomendado chamar o método `StartActivity` sempre que a atividade do usuário for alterada e **NUNCA** chamar o método `EndActivity`.</span><span class="sxs-lookup"><span data-stu-id="f1958-170">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="f1958-171">Esse método envia uma mensagem para o servidor Engagement que o usuário atual tenha deixado o aplicativo e isso afeta todos os logs de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1958-171">This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="f1958-172">Relatórios avançados</span><span class="sxs-lookup"><span data-stu-id="f1958-172">Advanced reporting</span></span>
<span data-ttu-id="f1958-173">Opcionalmente, convém relatar eventos específicos do aplicativo, erros e trabalhos, para fazer isso, use os outros métodos encontrados na classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="f1958-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="f1958-174">A API do Engagement permite usar todos os recursos avançados do Engagement.</span><span class="sxs-lookup"><span data-stu-id="f1958-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="f1958-175">Para obter mais informações, consulte [Como usar a API de marcação avançada do Mobile Engagement em seu aplicativo da Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="f1958-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="f1958-176">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="f1958-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="f1958-177">Desabilitar o relatório de falhas automático</span><span class="sxs-lookup"><span data-stu-id="f1958-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="f1958-178">Você pode desabilitar a recurso relatório de falhas automático do Engagement.</span><span class="sxs-lookup"><span data-stu-id="f1958-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="f1958-179">Então, quando uma exceção não tratada ocorrer, o Engagement não fará nada.</span><span class="sxs-lookup"><span data-stu-id="f1958-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="f1958-180">Se você planeja desabilitar esse recurso, lembre-se de que, quando uma falha não tratada ocorrer em seu aplicativo, o Engagement não enviará a falha **E** ele não fechará a sessão e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="f1958-180">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="f1958-181">Para desativar o relatório de falhas automático, apenas personalize a configuração dependendo de como você o declarou :</span><span class="sxs-lookup"><span data-stu-id="f1958-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="f1958-182">No arquivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="f1958-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="f1958-183">Defina a falha do relatório para `false` entre as marcas `<reportCrash>` e `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="f1958-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="f1958-184">No objeto `EngagementConfiguration` em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="f1958-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="f1958-185">Defina a falha do relatório como false usando o objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="f1958-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="f1958-186">Modo intermitente</span><span class="sxs-lookup"><span data-stu-id="f1958-186">Burst mode</span></span>
<span data-ttu-id="f1958-187">Por padrão, o serviço Engagement reporta logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="f1958-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="f1958-188">Se seu aplicativo relata logs com muita frequência, é melhor armazenar em buffer os logs e relatá-los todos de uma vez regularmente (isso é chamado de "modo intermitente").</span><span class="sxs-lookup"><span data-stu-id="f1958-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="f1958-189">Para fazer isso, chame o método:</span><span class="sxs-lookup"><span data-stu-id="f1958-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="f1958-190">O argumento é um valor em **milissegundos**.</span><span class="sxs-lookup"><span data-stu-id="f1958-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="f1958-191">A qualquer momento, se você deseja reativar o registro em log em tempo real, basta chamar o método sem nenhum parâmetro, ou com o valor 0.</span><span class="sxs-lookup"><span data-stu-id="f1958-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="f1958-192">O modo de intermitência aumenta ligeiramente a vida útil da bateria, mas tem um impacto no Monitor do Engagement: a duração de todas as sessões e trabalhos será arredondada para o limite de intermitência (portanto, as sessões e trabalhos mais curtos do que o limite de intermitência podem não estar visíveis).</span><span class="sxs-lookup"><span data-stu-id="f1958-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="f1958-193">É recomendável usar um limite de intermitência não maior que 30.000 (30s).</span><span class="sxs-lookup"><span data-stu-id="f1958-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="f1958-194">Você deve estar ciente de que os logs salvos são limitados a 300 itens.</span><span class="sxs-lookup"><span data-stu-id="f1958-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="f1958-195">Se o envio for muito longo, você poderá perder alguns logs.</span><span class="sxs-lookup"><span data-stu-id="f1958-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="f1958-196">O limite de intermitência não pode ser configurado para um período menor que um segundo.</span><span class="sxs-lookup"><span data-stu-id="f1958-196">The burst threshold cannot be configured to a period lesser than one second.</span></span> <span data-ttu-id="f1958-197">Se você tentar fazer isso, o SDK mostrará um rastreamento com o erro e será redefinido automaticamente como o valor padrão, que é de, zero segundo.</span><span class="sxs-lookup"><span data-stu-id="f1958-197">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds.</span></span> <span data-ttu-id="f1958-198">Isso irá disparar o SDK para relatar os logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="f1958-198">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

