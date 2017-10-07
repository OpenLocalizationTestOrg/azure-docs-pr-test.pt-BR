---
title: "Application Insights tootroubleshoot políticas personalizadas - Azure AD B2C | Microsoft Docs"
description: "como toosetup Application Insights tootrace Olá a execução de políticas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="0f38d-103">Azure Active Directory B2C: Coleta de logs</span><span class="sxs-lookup"><span data-stu-id="0f38d-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="0f38d-104">Este artigo fornece etapas para coletar logs do Azure AD B2C para que você possa diagnosticar problemas com suas políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0f38d-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="0f38d-105">Atualmente, hello logs de atividade detalhados descritos aqui são projetados **somente** tooaid no desenvolvimento de políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0f38d-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="0f38d-106">Não use o modo de desenvolvimento em produção.</span><span class="sxs-lookup"><span data-stu-id="0f38d-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="0f38d-107">Logs de coletam todas as declarações enviadas tooand Olá dos provedores de identidade durante o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="0f38d-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="0f38d-108">Se usado em produção, o desenvolvedor Olá assume a responsabilidade de PII (informações de identificação em particular) coletada no log de aplicativo Insights Olá que possuem.</span><span class="sxs-lookup"><span data-stu-id="0f38d-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="0f38d-109">Esses logs detalhados são coletados apenas quando a política de saudação é colocada em **modo de desenvolvimento**.</span><span class="sxs-lookup"><span data-stu-id="0f38d-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="0f38d-110">Usar o Application insights</span><span class="sxs-lookup"><span data-stu-id="0f38d-110">Use Application Insights</span></span>

<span data-ttu-id="0f38d-111">B2C do Azure AD oferece suporte a um recurso para enviar dados tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="0f38d-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="0f38d-112">Fornece uma maneira toodiagnose exceções do Application Insights e visualizar os problemas de desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0f38d-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="0f38d-113">Configurar o Application Insights</span><span class="sxs-lookup"><span data-stu-id="0f38d-113">Setup Application Insights</span></span>

1. <span data-ttu-id="0f38d-114">Vá toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f38d-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0f38d-115">Certifique-se de que você está no locatário Olá com sua assinatura do Azure (e não em seu locatário do Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="0f38d-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="0f38d-116">Clique em **+ novo** no menu de navegação à esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f38d-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="0f38d-117">Pesquise e selecione **Application Insights** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0f38d-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="0f38d-118">Preencha o formulário de saudação e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="0f38d-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="0f38d-119">Selecione **geral** para Olá **tipo de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="0f38d-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="0f38d-120">Depois de Olá recurso foi criado, abra o recurso do Application Insights Olá.</span><span class="sxs-lookup"><span data-stu-id="0f38d-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="0f38d-121">Localizar **propriedades** em Olá menu à esquerda e clique nele.</span><span class="sxs-lookup"><span data-stu-id="0f38d-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="0f38d-122">Saudação de cópia **chave de instrumentação** e salvá-lo para a próxima seção de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f38d-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="0f38d-123">Configurar a política personalizada de saudação</span><span class="sxs-lookup"><span data-stu-id="0f38d-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="0f38d-124">Abrir o arquivo RP hello (por exemplo, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="0f38d-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="0f38d-125">Adicionar Olá toohello atributos a seguir `<TrustFrameworkPolicy>` elemento:</span><span class="sxs-lookup"><span data-stu-id="0f38d-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="0f38d-126">Se ele não existir, adicione um nó filho `<UserJourneyBehaviors>` toohello `<RelyingParty>` nó.</span><span class="sxs-lookup"><span data-stu-id="0f38d-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="0f38d-127">Ela deve estar localizada imediatamente após Olá`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="0f38d-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="0f38d-128">Adicionar Olá após o nó como um filho do hello `<UserJourneyBehaviors>` elemento.</span><span class="sxs-lookup"><span data-stu-id="0f38d-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="0f38d-129">Certifique-se de que tooreplace `{Your Application Insights Key}` com hello **chave de instrumentação** que você obteve do Application Insights na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="0f38d-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="0f38d-130">`DeveloperMode="true"`informa a telemetria ApplicationInsights tooexpedite Olá por meio do pipeline de processamento de Olá, BOM para o desenvolvimento, mas restrito em grandes volumes.</span><span class="sxs-lookup"><span data-stu-id="0f38d-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="0f38d-131">`ClientEnabled="true"`envia o script do lado do cliente de ApplicationInsights Olá para rastrear erros de cliente e de exibição de página (não necessários).</span><span class="sxs-lookup"><span data-stu-id="0f38d-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="0f38d-132">`ServerEnabled="true"`envia Olá existente UserJourneyRecorder JSON como tooApplication um evento personalizado Insights.</span><span class="sxs-lookup"><span data-stu-id="0f38d-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="0f38d-133">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0f38d-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="0f38d-134">Carregar política hello.</span><span class="sxs-lookup"><span data-stu-id="0f38d-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="0f38d-135">Consulte Olá registra em log no Application Insights</span><span class="sxs-lookup"><span data-stu-id="0f38d-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="0f38d-136">Há um breve atraso (menos de cinco minutos) antes que você possa ver novos logs no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0f38d-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="0f38d-137">Abrir o recurso do Application Insights Olá que você criou no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f38d-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="0f38d-138">Em Olá **visão geral** menu, clique na **análise**.</span><span class="sxs-lookup"><span data-stu-id="0f38d-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="0f38d-139">Abra uma nova guia no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0f38d-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="0f38d-140">Aqui está uma lista de consultas, que você pode usar os logs de saudação do toosee</span><span class="sxs-lookup"><span data-stu-id="0f38d-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="0f38d-141">Consultar</span><span class="sxs-lookup"><span data-stu-id="0f38d-141">Query</span></span> | <span data-ttu-id="0f38d-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="0f38d-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="0f38d-143">traces</span><span class="sxs-lookup"><span data-stu-id="0f38d-143">traces</span></span> | <span data-ttu-id="0f38d-144">Ver todos os logs de saudação gerados pelo Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="0f38d-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="0f38d-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="0f38d-145">traces \\</span></span>| <span data-ttu-id="0f38d-146">em que timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="0f38d-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="0f38d-147">Ver todos os logs de saudação gerados pelo Azure AD B2C para Olá último dia</span><span class="sxs-lookup"><span data-stu-id="0f38d-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="0f38d-148">entradas de saudação podem ser longos.</span><span class="sxs-lookup"><span data-stu-id="0f38d-148">hello entries may be long.</span></span>  <span data-ttu-id="0f38d-149">Exporte tooCSV para uma análise mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="0f38d-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="0f38d-150">Você pode aprender mais sobre a ferramenta de análise de saudação [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="0f38d-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="0f38d-151">comunidade de saudação desenvolveu um desenvolvedores de identidade do usuário jornada visualizador toohelp.</span><span class="sxs-lookup"><span data-stu-id="0f38d-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="0f38d-152">Não tem suporte da Microsoft e é disponibilizado estritamente como está.</span><span class="sxs-lookup"><span data-stu-id="0f38d-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="0f38d-153">Ele lê da sua instância do Application Insights e fornece uma exibição de estrutura bem Olá jornada de eventos do usuário.</span><span class="sxs-lookup"><span data-stu-id="0f38d-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="0f38d-154">Obter o código-fonte hello e implantá-lo em sua própria solução.</span><span class="sxs-lookup"><span data-stu-id="0f38d-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="0f38d-155">Atualmente, hello logs de atividade detalhados descritos aqui são projetados **somente** tooaid no desenvolvimento de políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0f38d-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="0f38d-156">Não use o modo de desenvolvimento em produção.</span><span class="sxs-lookup"><span data-stu-id="0f38d-156">Do not use development mode in production.</span></span>  <span data-ttu-id="0f38d-157">Logs de coletam todas as declarações enviadas tooand Olá dos provedores de identidade durante o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="0f38d-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="0f38d-158">Se usado em produção, o desenvolvedor Olá assume a responsabilidade de PII (informações de identificação em particular) coletada no log de aplicativo Insights Olá que possuem.</span><span class="sxs-lookup"><span data-stu-id="0f38d-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="0f38d-159">Esses logs detalhados são coletados apenas quando a política de saudação é colocada em **modo de desenvolvimento**.</span><span class="sxs-lookup"><span data-stu-id="0f38d-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="0f38d-160">Repositório Github para obter exemplos de política personalizada sem suporte e ferramentas relacionadas</span><span class="sxs-lookup"><span data-stu-id="0f38d-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="0f38d-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f38d-161">Next Steps</span></span>

<span data-ttu-id="0f38d-162">Explorar dados Olá no Application Insights toohelp você entender como Olá identidade experiência Framework B2C subjacente funciona toodeliver passa por sua própria identidade.</span><span class="sxs-lookup"><span data-stu-id="0f38d-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
