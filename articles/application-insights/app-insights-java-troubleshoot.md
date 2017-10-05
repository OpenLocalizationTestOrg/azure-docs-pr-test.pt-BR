---
title: Solucionar problemas do Application Insights em um projeto Web Java
description: "Guia de solução de problemas: monitoramento em tempo real aplicativos Java com o Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="3317b-103">Solução de problemas e perguntas e respostas para o Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="3317b-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="3317b-104">Dúvidas ou problemas com o [Azure Application Insights em Java][java]?</span><span class="sxs-lookup"><span data-stu-id="3317b-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="3317b-105">Aqui estão algumas dicas.</span><span class="sxs-lookup"><span data-stu-id="3317b-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="3317b-106">Erros de compilação</span><span class="sxs-lookup"><span data-stu-id="3317b-106">Build errors</span></span>
<span data-ttu-id="3317b-107">**No Eclipse, ao adicionar o SDK do Application Insights por meio de Maven ou Gradle, recebo erros de validação de soma de verificação ou de compilação.**</span><span class="sxs-lookup"><span data-stu-id="3317b-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="3317b-108">Se o elemento <version> de dependência estiver usando um padrão com caracteres curinga (ex.: Maven `<version>[1.0,)</version>` ou Gradle `version:'1.0.+'`), tente definir uma versão específica, como `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="3317b-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="3317b-109">Veja as [notas de versão](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) da versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="3317b-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="3317b-110">Sem dados</span><span class="sxs-lookup"><span data-stu-id="3317b-110">No data</span></span>
<span data-ttu-id="3317b-111">**Adicionei o Application Insights com êxito e executei meu aplicativo, mas nunca vi dados no portal.**</span><span class="sxs-lookup"><span data-stu-id="3317b-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="3317b-112">Espere um minuto e clique em Atualizar.</span><span class="sxs-lookup"><span data-stu-id="3317b-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="3317b-113">Os gráficos são atualizados periodicamente, mas você também pode atualizá-los manualmente.</span><span class="sxs-lookup"><span data-stu-id="3317b-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="3317b-114">O intervalo de atualização depende do intervalo de tempo do gráfico.</span><span class="sxs-lookup"><span data-stu-id="3317b-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="3317b-115">Verifique se você tem uma chave de instrumentação definida no arquivo ApplicationInsights.xml (na pasta de recursos em seu projeto)</span><span class="sxs-lookup"><span data-stu-id="3317b-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="3317b-116">Verifique se não há um nó `<DisableTelemetry>true</DisableTelemetry>` no arquivo xml.</span><span class="sxs-lookup"><span data-stu-id="3317b-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="3317b-117">Em seu firewall, talvez você precise abrir as portas TCP 80 e 443 para o tráfego de saída de dc.services.visualstudio.com. Consulte a [lista completa de exceções do firewall](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="3317b-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com. See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="3317b-118">No painel inicial do Microsoft Azure, veja o mapa de status de serviço.</span><span class="sxs-lookup"><span data-stu-id="3317b-118">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="3317b-119">Se houver indicações de alerta, espere até que elas tenham voltado a OK; então, feche e abra novamente a folha do Application Insights de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3317b-119">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="3317b-120">Ative o log para a janela de console do IDE adicionando um elemento `<SDKLogger />` sob o nó raiz no arquivo ApplicationInsights.xml (na pasta de recursos em seu projeto) e verifique se há entradas precedidas com [Erro].</span><span class="sxs-lookup"><span data-stu-id="3317b-120">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="3317b-121">Certifique-se de que o arquivo ApplicationInsights.xml correto foi carregado com êxito pelo SDK do Java, examinando as mensagens de saída do console para uma instrução "Arquivo de configuração foi descoberto com êxito".</span><span class="sxs-lookup"><span data-stu-id="3317b-121">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="3317b-122">Se não for encontrado no arquivo de configuração, verifique as mensagens de saída para ver onde o arquivo de configuração está sendo procurado e certifique-se de que o ApplicationInsights.xml seja localizado em um desses locais de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3317b-122">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="3317b-123">Como regra geral, você pode colocar o arquivo de configuração perto dos JARs do SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3317b-123">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="3317b-124">Por exemplo: no Tomcat, isso poderia significar que a pasta WEB-INF/lib.</span><span class="sxs-lookup"><span data-stu-id="3317b-124">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="3317b-125">Eu costumava ver os dados, mas eles foram interrompidos</span><span class="sxs-lookup"><span data-stu-id="3317b-125">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="3317b-126">Verifique o [blog de status](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="3317b-126">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="3317b-127">Você atingiu sua cota mensal de pontos de dados?</span><span class="sxs-lookup"><span data-stu-id="3317b-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="3317b-128">Abra Configurações/Cota e Preços para descobrir. Nesse caso, você pode atualizar seu plano ou então pagar por capacidade adicional.</span><span class="sxs-lookup"><span data-stu-id="3317b-128">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="3317b-129">Consulte o [esquema de preços](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="3317b-129">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="3317b-130">Não vejo todos os dados que eu esperava</span><span class="sxs-lookup"><span data-stu-id="3317b-130">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="3317b-131">Abra a folha Cotas e Preço e verifique se a [amostragem](app-insights-sampling.md) está funcionando.</span><span class="sxs-lookup"><span data-stu-id="3317b-131">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="3317b-132">(Transmissão de 100% significa que a amostragem não está funcionando.) O serviço do Application Insights pode ser definido para aceitar apenas uma fração da telemetria que chega de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3317b-132">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="3317b-133">Isso o ajuda a se manter dentro de sua cota mensal de telemetria.</span><span class="sxs-lookup"><span data-stu-id="3317b-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="3317b-134">Sem dados de uso</span><span class="sxs-lookup"><span data-stu-id="3317b-134">No usage data</span></span>
<span data-ttu-id="3317b-135">**Vejo dados sobre solicitações e tempos de resposta, mas não há dados de exibição de página, de navegador ou de usuário.**</span><span class="sxs-lookup"><span data-stu-id="3317b-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="3317b-136">Você configurou com êxito seu aplicativo para enviar telemetria do servidor.</span><span class="sxs-lookup"><span data-stu-id="3317b-136">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="3317b-137">Agora, a próxima etapa é [configurar suas páginas da Web para enviar telemetria por meio do navegador da Web][usage].</span><span class="sxs-lookup"><span data-stu-id="3317b-137">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="3317b-138">Como alternativa, se o cliente for um aplicativo em um [telefone ou outro dispositivo][platforms], você poderá enviar telemetria por meio dele.</span><span class="sxs-lookup"><span data-stu-id="3317b-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="3317b-139">Use a mesma chave de instrumentação para configurar a telemetria de seu cliente e do servidor.</span><span class="sxs-lookup"><span data-stu-id="3317b-139">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="3317b-140">Os dados serão exibidos no mesmo recurso do Application Insights, e você poderá correlacionar eventos do cliente e do servidor.</span><span class="sxs-lookup"><span data-stu-id="3317b-140">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="3317b-141">Desabilitando a telemetria</span><span class="sxs-lookup"><span data-stu-id="3317b-141">Disabling telemetry</span></span>
<span data-ttu-id="3317b-142">**Como desabilitar a coleta da telemetria?**</span><span class="sxs-lookup"><span data-stu-id="3317b-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="3317b-143">No código:</span><span class="sxs-lookup"><span data-stu-id="3317b-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="3317b-144">**Ou**</span><span class="sxs-lookup"><span data-stu-id="3317b-144">**Or**</span></span> 

<span data-ttu-id="3317b-145">Atualize o arquivo ApplicationInsights.xml (na pasta de recursos em seu projeto).</span><span class="sxs-lookup"><span data-stu-id="3317b-145">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="3317b-146">Adicione o seguinte sob o nó raiz:</span><span class="sxs-lookup"><span data-stu-id="3317b-146">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="3317b-147">Usando o método XML, você precisa reiniciar o aplicativo ao alterar o valor.</span><span class="sxs-lookup"><span data-stu-id="3317b-147">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="3317b-148">Alterando o destino</span><span class="sxs-lookup"><span data-stu-id="3317b-148">Changing the target</span></span>
<span data-ttu-id="3317b-149">**Como alterar o recurso do Azure ao qual meu projeto envia dados?**</span><span class="sxs-lookup"><span data-stu-id="3317b-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="3317b-150">[Obtenha a chave de instrumentação do novo recurso.][java]</span><span class="sxs-lookup"><span data-stu-id="3317b-150">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="3317b-151">Se você tiver adicionado o Application Insights a seu projeto usando o Kit de Ferramentas do Azure para Eclipse, clique com o botão direito do mouse em seu projeto Web, selecione **Azure**, **Configurar Application Insights** e altere a chave.</span><span class="sxs-lookup"><span data-stu-id="3317b-151">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="3317b-152">Caso contrário, atualize a chave em ApplicationInsights.xml na pasta de recursos em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="3317b-152">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="3317b-153">Depurar dados do SDK</span><span class="sxs-lookup"><span data-stu-id="3317b-153">Debug data from the SDK</span></span>

<span data-ttu-id="3317b-154">**Como descobrir o que o SDK está fazendo?**</span><span class="sxs-lookup"><span data-stu-id="3317b-154">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="3317b-155">Para saber mais sobre o que está acontecendo na API, adicione `<SDKLogger/>` ao nó raiz do arquivo de configuração Applicationinsights.xml.</span><span class="sxs-lookup"><span data-stu-id="3317b-155">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="3317b-156">Você também pode instruir o agente para enviar a saída para um arquivo:</span><span class="sxs-lookup"><span data-stu-id="3317b-156">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="3317b-157">Os arquivos podem ser encontrados em `%temp%\javasdklogs` ou `java.io.tmpdir` no caso do servidor Tomcat.</span><span class="sxs-lookup"><span data-stu-id="3317b-157">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="3317b-158">A tela inicial do Azure</span><span class="sxs-lookup"><span data-stu-id="3317b-158">The Azure start screen</span></span>
<span data-ttu-id="3317b-159">**Estou examinando o [portal do Azure](https://portal.azure.com). O mapa me diz algo sobre meu aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="3317b-159">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="3317b-160">Não, ele mostra a integridade dos servidores do Azure em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="3317b-160">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="3317b-161">*No painel inicial do Azure (tela inicial), como localizar dados sobre meu aplicativo?*</span><span class="sxs-lookup"><span data-stu-id="3317b-161">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="3317b-162">Supondo que você tenha [configurado seu aplicativo para o Application Insights][java], clique em Procurar, selecione Application Insights e selecione o recurso de aplicativo criado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3317b-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="3317b-163">Para acessar essa opção mais rapidamente no futuro, você pode fixar o aplicativo no painel inicial.</span><span class="sxs-lookup"><span data-stu-id="3317b-163">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="3317b-164">Servidores de intranet</span><span class="sxs-lookup"><span data-stu-id="3317b-164">Intranet servers</span></span>
<span data-ttu-id="3317b-165">**Posso monitorar um servidor em minha intranet?**</span><span class="sxs-lookup"><span data-stu-id="3317b-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="3317b-166">Sim, desde que o servidor possa enviar telemetria para o portal do Application Insights pela Internet pública.</span><span class="sxs-lookup"><span data-stu-id="3317b-166">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="3317b-167">Em seu firewall, você terá que abrir as portas TCP 80 e 443 para tráfego de saída de dc.services.visualstudio.com e f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="3317b-167">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="3317b-168">Retenção de dados</span><span class="sxs-lookup"><span data-stu-id="3317b-168">Data retention</span></span>
<span data-ttu-id="3317b-169">**Por quanto tempo os dados são mantidos no portal? É seguro?**</span><span class="sxs-lookup"><span data-stu-id="3317b-169">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="3317b-170">Consulte [Privacidade e retenção de dados][data].</span><span class="sxs-lookup"><span data-stu-id="3317b-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="3317b-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3317b-171">Next steps</span></span>
<span data-ttu-id="3317b-172">**Configurei o Application Insights para meu aplicativo de servidor Java. O que mais posso fazer?**</span><span class="sxs-lookup"><span data-stu-id="3317b-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="3317b-173">[Monitorar a disponibilidade de suas páginas da Web][availability]</span><span class="sxs-lookup"><span data-stu-id="3317b-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="3317b-174">[Monitorar o uso da página da Web][usage]</span><span class="sxs-lookup"><span data-stu-id="3317b-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="3317b-175">[Acompanhar o uso e diagnosticar problemas em seus aplicativos de dispositivos][platforms]</span><span class="sxs-lookup"><span data-stu-id="3317b-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="3317b-176">[Escrever código para acompanhar o uso de seu aplicativo][track]</span><span class="sxs-lookup"><span data-stu-id="3317b-176">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="3317b-177">[Capturar logs de diagnóstico][javalogs]</span><span class="sxs-lookup"><span data-stu-id="3317b-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="3317b-178">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="3317b-178">Get help</span></span>
* [<span data-ttu-id="3317b-179">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="3317b-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

