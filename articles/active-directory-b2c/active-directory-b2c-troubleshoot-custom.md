---
title: "Application Insights para solucionar problemas de Políticas Personalizadas – Azure AD B2C | Microsoft Docs"
description: "como configurar o Application Insights para rastrear a execução de políticas personalizadas"
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
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="70c33-103">Azure Active Directory B2C: Coleta de logs</span><span class="sxs-lookup"><span data-stu-id="70c33-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="70c33-104">Este artigo fornece etapas para coletar logs do Azure AD B2C para que você possa diagnosticar problemas com suas políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="70c33-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="70c33-105">Atualmente, os logs de atividade detalhados descritos aqui são projetados **APENAS** para ajudar no desenvolvimento de políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="70c33-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="70c33-106">Não use o modo de desenvolvimento em produção.</span><span class="sxs-lookup"><span data-stu-id="70c33-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="70c33-107">Os logs coletam todas as declarações enviadas entre os provedores de identidade durante o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="70c33-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="70c33-108">Se for usado em produção, o desenvolvedor assumirá a responsabilidade pela PII (Informações de identificação particular) coletadas no log do App Insights que ele possui.</span><span class="sxs-lookup"><span data-stu-id="70c33-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="70c33-109">Esses logs detalhados são coletados apenas quando a política é colocada em **MODO DE DESENVOLVIMENTO**.</span><span class="sxs-lookup"><span data-stu-id="70c33-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="70c33-110">Usar o Application insights</span><span class="sxs-lookup"><span data-stu-id="70c33-110">Use Application Insights</span></span>

<span data-ttu-id="70c33-111">O Azure AD B2C oferece suporte a um recurso para envio de dados ao Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70c33-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="70c33-112">O Application Insights fornece uma maneira de diagnosticar exceções e visualizar os problemas de desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70c33-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="70c33-113">Configurar o Application Insights</span><span class="sxs-lookup"><span data-stu-id="70c33-113">Setup Application Insights</span></span>

1. <span data-ttu-id="70c33-114">Vá para o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70c33-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="70c33-115">Certifique-se de que você esteja no locatário com sua assinatura do Azure (não no locatário do Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="70c33-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="70c33-116">Clique em **+ Novo** no menu de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="70c33-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="70c33-117">Pesquise e selecione **Application Insights** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="70c33-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="70c33-118">Preencha o formulário e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="70c33-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="70c33-119">Selecione **Geral** para o **Tipo de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="70c33-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="70c33-120">Após a criação do recurso, abra o recurso Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70c33-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="70c33-121">Localize **Propriedades** no menu à esquerda e clique nele.</span><span class="sxs-lookup"><span data-stu-id="70c33-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="70c33-122">Copie a **Chave de Instrumentação** e salve-a na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="70c33-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="70c33-123">Configurar a política personalizada</span><span class="sxs-lookup"><span data-stu-id="70c33-123">Set up the custom policy</span></span>

1. <span data-ttu-id="70c33-124">Abra o arquivo RP (por exemplo, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="70c33-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="70c33-125">Adicione os atributos a seguir ao elemento `<TrustFrameworkPolicy>`:</span><span class="sxs-lookup"><span data-stu-id="70c33-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="70c33-126">Se ele ainda não existir, adicione um nó filho `<UserJourneyBehaviors>` ao nó `<RelyingParty>`.</span><span class="sxs-lookup"><span data-stu-id="70c33-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="70c33-127">Ele deve estar localizado imediatamente após o `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="70c33-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="70c33-128">Adicione o seguinte nó como um filho do elemento `<UserJourneyBehaviors>`.</span><span class="sxs-lookup"><span data-stu-id="70c33-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="70c33-129">Substitua `{Your Application Insights Key}` pela **Chave de Instrumentação** que você obteve do Application Insights na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="70c33-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="70c33-130">`DeveloperMode="true"` informa ao ApplicationInsights para agilizar a telemetria por meio do pipeline de processamento, bom para o desenvolvimento, mas com restrição em grandes volumes.</span><span class="sxs-lookup"><span data-stu-id="70c33-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="70c33-131">`ClientEnabled="true"` envia o script do lado do cliente do ApplicationInsights para rastrear erros de exibição de página e do lado do cliente (não é necessário).</span><span class="sxs-lookup"><span data-stu-id="70c33-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="70c33-132">`ServerEnabled="true"` envia o JSON UserJourneyRecorder existente como um evento personalizado para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70c33-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="70c33-133">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="70c33-133">Sample:</span></span>

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

3. <span data-ttu-id="70c33-134">Carregue a política.</span><span class="sxs-lookup"><span data-stu-id="70c33-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="70c33-135">Veja os logs de no Application Insights</span><span class="sxs-lookup"><span data-stu-id="70c33-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="70c33-136">Há um breve atraso (menos de cinco minutos) antes que você possa ver novos logs no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70c33-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="70c33-137">Abra o recurso do Application Insights que você criou no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70c33-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="70c33-138">No menu **Visão geral**, clique em **Análise**.</span><span class="sxs-lookup"><span data-stu-id="70c33-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="70c33-139">Abra uma nova guia no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70c33-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="70c33-140">Aqui está uma lista de consultas que você pode usar para ver os logs</span><span class="sxs-lookup"><span data-stu-id="70c33-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="70c33-141">Consultar</span><span class="sxs-lookup"><span data-stu-id="70c33-141">Query</span></span> | <span data-ttu-id="70c33-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="70c33-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="70c33-143">traces</span><span class="sxs-lookup"><span data-stu-id="70c33-143">traces</span></span> | <span data-ttu-id="70c33-144">Veja todos os logs gerados pelo Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="70c33-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="70c33-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="70c33-145">traces \\</span></span>| <span data-ttu-id="70c33-146">em que timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="70c33-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="70c33-147">Veja todos os logs gerados pelo Azure AD B2C para o último dia</span><span class="sxs-lookup"><span data-stu-id="70c33-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="70c33-148">As entradas podem ser longas.</span><span class="sxs-lookup"><span data-stu-id="70c33-148">The entries may be long.</span></span>  <span data-ttu-id="70c33-149">Exporte para CSV para uma análise mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="70c33-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="70c33-150">Saiba mais sobre essa ferramentas de análise [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="70c33-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="70c33-151">A comunidade desenvolveu um visualizador userjourney para ajudar os desenvolvedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="70c33-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="70c33-152">Não tem suporte da Microsoft e é disponibilizado estritamente como está.</span><span class="sxs-lookup"><span data-stu-id="70c33-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="70c33-153">Ele lê na sua instância do Application Insights e fornece uma exibição bem estruturada dos eventos userjourney.</span><span class="sxs-lookup"><span data-stu-id="70c33-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="70c33-154">Obtenha o código-fonte e o implante em sua própria solução.</span><span class="sxs-lookup"><span data-stu-id="70c33-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="70c33-155">Atualmente, os logs de atividade detalhados descritos aqui são projetados **APENAS** para ajudar no desenvolvimento de políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="70c33-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="70c33-156">Não use o modo de desenvolvimento em produção.</span><span class="sxs-lookup"><span data-stu-id="70c33-156">Do not use development mode in production.</span></span>  <span data-ttu-id="70c33-157">Os logs coletam todas as declarações enviadas entre os provedores de identidade durante o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="70c33-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="70c33-158">Se for usado em produção, o desenvolvedor assumirá a responsabilidade pela PII (Informações de identificação particular) coletadas no log do App Insights que ele possui.</span><span class="sxs-lookup"><span data-stu-id="70c33-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="70c33-159">Esses logs detalhados são coletados apenas quando a política é colocada em **MODO DE DESENVOLVIMENTO**.</span><span class="sxs-lookup"><span data-stu-id="70c33-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="70c33-160">Repositório Github para obter exemplos de política personalizada sem suporte e ferramentas relacionadas</span><span class="sxs-lookup"><span data-stu-id="70c33-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="70c33-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70c33-161">Next Steps</span></span>

<span data-ttu-id="70c33-162">Explore os dados no Application Insights para ajudar a entender como o Identity Experience Framework por trás do B2C trabalha para fornecer suas próprias experiências de identidade.</span><span class="sxs-lookup"><span data-stu-id="70c33-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
