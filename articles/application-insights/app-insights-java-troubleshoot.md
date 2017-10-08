---
title: aaaTroubleshoot Application Insights em um projeto da web de Java
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
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="6cbf5-103">Solução de problemas e perguntas e respostas para o Application Insights para Java</span><span class="sxs-lookup"><span data-stu-id="6cbf5-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="6cbf5-104">Dúvidas ou problemas com o [Azure Application Insights em Java][java]?</span><span class="sxs-lookup"><span data-stu-id="6cbf5-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="6cbf5-105">Aqui estão algumas dicas.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="6cbf5-106">Erros de compilação</span><span class="sxs-lookup"><span data-stu-id="6cbf5-106">Build errors</span></span>
<span data-ttu-id="6cbf5-107">**No Eclipse, quando adicionar Olá SDK do Application Insights via Maven ou Gradle, recebo compilação ou a soma de verificação de erros de validação.**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="6cbf5-108">Se Olá dependência <version> elemento está usando um padrão com caracteres curinga (por exemplo, (Maven) `<version>[1.0,)</version>` ou (Gradle) `version:'1.0.+'`), tente especificar uma versão específica em vez disso, como `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="6cbf5-109">Consulte Olá [notas de versão](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) para a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="6cbf5-110">Sem dados</span><span class="sxs-lookup"><span data-stu-id="6cbf5-110">No data</span></span>
<span data-ttu-id="6cbf5-111">**Adicionei com êxito o Application Insights e executou meu aplicativo, mas nunca vi dados no portal de saudação.**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="6cbf5-112">Espere um minuto e clique em Atualizar.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="6cbf5-113">gráficos de saudação se atualizar periodicamente, mas você também pode atualizar manualmente.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="6cbf5-114">intervalo de atualização de saudação depende do intervalo de tempo de saudação do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="6cbf5-115">Verifique se você tem uma chave de instrumentação definida no arquivo de ApplicationInsights.xml hello (na pasta de recursos de saudação em seu projeto)</span><span class="sxs-lookup"><span data-stu-id="6cbf5-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="6cbf5-116">Verifique se não há nenhum `<DisableTelemetry>true</DisableTelemetry>` nó no arquivo xml de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="6cbf5-117">Em seu firewall, você pode ter tooopen as portas TCP 80 e 443 para toodc.services.visualstudio.com de tráfego de saída. Consulte Olá [lista completa de exceções do firewall](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="6cbf5-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="6cbf5-118">Olá Microsoft Azure inicia quadro, examine o mapa de status do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="6cbf5-119">Se houver algum alertas indicações, aguarde até que eles retornaram tooOK e, em seguida, feche e reabra a folha de aplicativos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="6cbf5-120">Ative o log de janela de console do IDE toohello, adicionando um `<SDKLogger />` elemento no nó de raiz de saudação no arquivo de ApplicationInsights.xml hello (na pasta de recursos de saudação em seu projeto) e verificar se há entradas precedidos de [Erro].</span><span class="sxs-lookup"><span data-stu-id="6cbf5-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="6cbf5-121">Certifique-se de que Olá correto ApplicationInsights.xml arquivo tem foi carregado com êxito pelo Olá Java SDK, observando mensagens de saída do console Olá para uma instrução "arquivo de configuração foi localizou com êxito".</span><span class="sxs-lookup"><span data-stu-id="6cbf5-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="6cbf5-122">Se o arquivo de configuração de saudação não for encontrado, verifique Olá toosee de mensagens de saída em que o arquivo de configuração hello está sendo pesquisado e certifique-se de que Olá que applicationinsights.XML está localizado em um desses locais de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="6cbf5-123">Como regra geral, você pode colocar o arquivo de configuração de Olá próximo JARs do hello Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="6cbf5-124">Por exemplo: Tomcat, isso significaria Olá pasta WEB-INF/lib.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="6cbf5-125">Usei toosee dados, mas foi interrompido</span><span class="sxs-lookup"><span data-stu-id="6cbf5-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="6cbf5-126">Verificar Olá [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="6cbf5-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="6cbf5-127">Você atingiu sua cota mensal de pontos de dados?</span><span class="sxs-lookup"><span data-stu-id="6cbf5-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="6cbf5-128">Abra configurações/cotas e preços toofind out. Nesse caso, você pode atualizar seu plano ou então pagar por capacidade adicional.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="6cbf5-129">Consulte Olá [preços esquema](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="6cbf5-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="6cbf5-130">Não vejo todos os dados de saudação que eu estou esperando</span><span class="sxs-lookup"><span data-stu-id="6cbf5-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="6cbf5-131">Abrir hello cotas e preços de folha e verifique se [amostragem](app-insights-sampling.md) está em operação.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="6cbf5-132">(transmissão de 100% significa que a amostragem não está em operação.) Olá serviço Application Insights pode ser conjunto tooaccept apenas uma fração de telemetria Olá que chega de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="6cbf5-133">Isso o ajuda a se manter dentro de sua cota mensal de telemetria.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="6cbf5-134">Sem dados de uso</span><span class="sxs-lookup"><span data-stu-id="6cbf5-134">No usage data</span></span>
<span data-ttu-id="6cbf5-135">**Vejo dados sobre solicitações e tempos de resposta, mas não há dados de exibição de página, de navegador ou de usuário.**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="6cbf5-136">Você configurar com êxito o telemetria do toosend seu aplicativo do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="6cbf5-137">Agora, a próxima etapa é muito[configurar sua telemetria toosend de páginas da web no navegador da web de saudação][usage].</span><span class="sxs-lookup"><span data-stu-id="6cbf5-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="6cbf5-138">Como alternativa, se o cliente for um aplicativo em um [telefone ou outro dispositivo][platforms], você poderá enviar telemetria por meio dele.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="6cbf5-139">Use Olá mesmo tooset de chave de instrumentação a telemetria de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="6cbf5-140">dados saudação aparecerá em Olá mesmo recurso Application Insights, e você será capaz de toocorrelate eventos do cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="6cbf5-141">Desabilitando a telemetria</span><span class="sxs-lookup"><span data-stu-id="6cbf5-141">Disabling telemetry</span></span>
<span data-ttu-id="6cbf5-142">**Como desabilitar a coleta da telemetria?**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="6cbf5-143">No código:</span><span class="sxs-lookup"><span data-stu-id="6cbf5-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="6cbf5-144">**Ou**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-144">**Or**</span></span> 

<span data-ttu-id="6cbf5-145">Atualize ApplicationInsights.xml (na pasta de recursos de saudação em seu projeto).</span><span class="sxs-lookup"><span data-stu-id="6cbf5-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="6cbf5-146">Adicione a seguinte Olá sob o nó raiz de saudação:</span><span class="sxs-lookup"><span data-stu-id="6cbf5-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="6cbf5-147">Usando o método XML hello, você tem toorestart aplicativo de hello quando você altera o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="6cbf5-148">Alterando o destino de saudação</span><span class="sxs-lookup"><span data-stu-id="6cbf5-148">Changing hello target</span></span>
<span data-ttu-id="6cbf5-149">**Como alterar o recurso do Azure ao qual meu projeto envia dados?**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="6cbf5-150">[Obter a chave de instrumentação de saudação do novo recurso de saudação.][java]</span><span class="sxs-lookup"><span data-stu-id="6cbf5-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="6cbf5-151">Se você adicionou o projeto do Application Insights tooyour usando Olá Kit de ferramentas do Azure para Eclipse, clique com botão direito seu projeto da web, selecione **Azure**, **configurar o Application Insights**e alterar a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="6cbf5-152">Caso contrário, atualize a chave de saudação na ApplicationInsights.xml na pasta de recursos de saudação em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="6cbf5-153">Dados de saudação SDK de depuração</span><span class="sxs-lookup"><span data-stu-id="6cbf5-153">Debug data from hello SDK</span></span>

<span data-ttu-id="6cbf5-154">**Como posso descobrir qual Olá SDK está fazendo?**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="6cbf5-155">tooget obter mais informações sobre o que está acontecendo em Olá API, adicione `<SDKLogger/>` sob o nó de raiz Olá Olá ApplicationInsights.xml do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="6cbf5-156">Você também pode instruir o arquivo do hello agente toooutput tooa:</span><span class="sxs-lookup"><span data-stu-id="6cbf5-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="6cbf5-157">Olá arquivos podem ser encontrados em `%temp%\javasdklogs` ou `java.io.tmpdir` no caso do servidor Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="6cbf5-158">tela de início do Azure Hello</span><span class="sxs-lookup"><span data-stu-id="6cbf5-158">hello Azure start screen</span></span>
<span data-ttu-id="6cbf5-159">**Estou olhando [Olá portal do Azure](https://portal.azure.com). Mapa Olá conte-me algo sobre meu aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="6cbf5-160">Não, ele mostra a integridade de saudação dos servidores do Azure ao redor Olá, mundo.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="6cbf5-161">*Da placa de início do Azure hello (tela inicial), como localizar dados sobre meu aplicativo?*</span><span class="sxs-lookup"><span data-stu-id="6cbf5-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="6cbf5-162">Supondo que você [configurar seu aplicativo para o Application Insights][java], clique em Procurar, selecione Application Insights e selecione o recurso de aplicativo hello criado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="6cbf5-163">tooget há mais rápido no futuro, você pode fixar sua placa de início do aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="6cbf5-164">Servidores de intranet</span><span class="sxs-lookup"><span data-stu-id="6cbf5-164">Intranet servers</span></span>
<span data-ttu-id="6cbf5-165">**Posso monitorar um servidor em minha intranet?**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="6cbf5-166">Sim, desde que o servidor pode enviar o portal do Application Insights telemetria toohello por meio de Olá internet pública.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="6cbf5-167">Em seu firewall, você pode ter tooopen as portas TCP 80 e 443 para toodc.services.visualstudio.com de tráfego de saída e f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="6cbf5-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="6cbf5-168">Retenção de dados</span><span class="sxs-lookup"><span data-stu-id="6cbf5-168">Data retention</span></span>
<span data-ttu-id="6cbf5-169">**Quanto tempo os dados são retidos no portal de Olá? É seguro?**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="6cbf5-170">Consulte [Privacidade e retenção de dados][data].</span><span class="sxs-lookup"><span data-stu-id="6cbf5-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cbf5-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6cbf5-171">Next steps</span></span>
<span data-ttu-id="6cbf5-172">**Configurei o Application Insights para meu aplicativo de servidor Java. O que mais posso fazer?**</span><span class="sxs-lookup"><span data-stu-id="6cbf5-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="6cbf5-173">[Monitorar a disponibilidade de suas páginas da Web][availability]</span><span class="sxs-lookup"><span data-stu-id="6cbf5-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="6cbf5-174">[Monitorar o uso da página da Web][usage]</span><span class="sxs-lookup"><span data-stu-id="6cbf5-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="6cbf5-175">[Acompanhar o uso e diagnosticar problemas em seus aplicativos de dispositivos][platforms]</span><span class="sxs-lookup"><span data-stu-id="6cbf5-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="6cbf5-176">[Gravar o uso de tootrack de código do aplicativo][track]</span><span class="sxs-lookup"><span data-stu-id="6cbf5-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="6cbf5-177">[Capturar logs de diagnóstico][javalogs]</span><span class="sxs-lookup"><span data-stu-id="6cbf5-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="6cbf5-178">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="6cbf5-178">Get help</span></span>
* [<span data-ttu-id="6cbf5-179">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="6cbf5-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

