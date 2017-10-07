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
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: Coleta de logs

Este artigo fornece etapas para coletar logs do Azure AD B2C para que você possa diagnosticar problemas com suas políticas personalizadas.

>[!NOTE]
>Atualmente, hello logs de atividade detalhados descritos aqui são projetados **somente** tooaid no desenvolvimento de políticas personalizadas. Não use o modo de desenvolvimento em produção.  Logs de coletam todas as declarações enviadas tooand Olá dos provedores de identidade durante o desenvolvimento.  Se usado em produção, o desenvolvedor Olá assume a responsabilidade de PII (informações de identificação em particular) coletada no log de aplicativo Insights Olá que possuem.  Esses logs detalhados são coletados apenas quando a política de saudação é colocada em **modo de desenvolvimento**.


## <a name="use-application-insights"></a>Usar o Application insights

B2C do Azure AD oferece suporte a um recurso para enviar dados tooApplication Insights.  Fornece uma maneira toodiagnose exceções do Application Insights e visualizar os problemas de desempenho do aplicativo.

### <a name="setup-application-insights"></a>Configurar o Application Insights

1. Vá toohello [portal do Azure](https://portal.azure.com). Certifique-se de que você está no locatário Olá com sua assinatura do Azure (e não em seu locatário do Azure AD B2C).
1. Clique em **+ novo** no menu de navegação à esquerda de saudação.
1. Pesquise e selecione **Application Insights** e clique em **Criar**.
1. Preencha o formulário de saudação e clique em **criar**. Selecione **geral** para Olá **tipo de aplicativo**.
1. Depois de Olá recurso foi criado, abra o recurso do Application Insights Olá.
1. Localizar **propriedades** em Olá menu à esquerda e clique nele.
1. Saudação de cópia **chave de instrumentação** e salvá-lo para a próxima seção de saudação.

### <a name="set-up-hello-custom-policy"></a>Configurar a política personalizada de saudação

1. Abrir o arquivo RP hello (por exemplo, SignUpOrSignin.xml).
1. Adicionar Olá toohello atributos a seguir `<TrustFrameworkPolicy>` elemento:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Se ele não existir, adicione um nó filho `<UserJourneyBehaviors>` toohello `<RelyingParty>` nó. Ela deve estar localizada imediatamente após Olá`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Adicionar Olá após o nó como um filho do hello `<UserJourneyBehaviors>` elemento. Certifique-se de que tooreplace `{Your Application Insights Key}` com hello **chave de instrumentação** que você obteve do Application Insights na seção anterior hello.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`informa a telemetria ApplicationInsights tooexpedite Olá por meio do pipeline de processamento de Olá, BOM para o desenvolvimento, mas restrito em grandes volumes.
  * `ClientEnabled="true"`envia o script do lado do cliente de ApplicationInsights Olá para rastrear erros de cliente e de exibição de página (não necessários).
  * `ServerEnabled="true"`envia Olá existente UserJourneyRecorder JSON como tooApplication um evento personalizado Insights.
Exemplo:

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

3. Carregar política hello.

### <a name="see-hello-logs-in-application-insights"></a>Consulte Olá registra em log no Application Insights

>[!NOTE]
> Há um breve atraso (menos de cinco minutos) antes que você possa ver novos logs no Application Insights.

1. Abrir o recurso do Application Insights Olá que você criou no hello [portal do Azure](https://portal.azure.com).
1. Em Olá **visão geral** menu, clique na **análise**.
1. Abra uma nova guia no Application Insights.
1. Aqui está uma lista de consultas, que você pode usar os logs de saudação do toosee

| Consultar | Descrição |
|---------------------|--------------------|
traces | Ver todos os logs de saudação gerados pelo Azure AD B2C |
traces \| em que timestamp > ago(1d) | Ver todos os logs de saudação gerados pelo Azure AD B2C para Olá último dia

entradas de saudação podem ser longos.  Exporte tooCSV para uma análise mais detalhada.

Você pode aprender mais sobre a ferramenta de análise de saudação [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>comunidade de saudação desenvolveu um desenvolvedores de identidade do usuário jornada visualizador toohelp.  Não tem suporte da Microsoft e é disponibilizado estritamente como está.  Ele lê da sua instância do Application Insights e fornece uma exibição de estrutura bem Olá jornada de eventos do usuário.  Obter o código-fonte hello e implantá-lo em sua própria solução.

>[!NOTE]
>Atualmente, hello logs de atividade detalhados descritos aqui são projetados **somente** tooaid no desenvolvimento de políticas personalizadas. Não use o modo de desenvolvimento em produção.  Logs de coletam todas as declarações enviadas tooand Olá dos provedores de identidade durante o desenvolvimento.  Se usado em produção, o desenvolvedor Olá assume a responsabilidade de PII (informações de identificação em particular) coletada no log de aplicativo Insights Olá que possuem.  Esses logs detalhados são coletados apenas quando a política de saudação é colocada em **modo de desenvolvimento**.

[Repositório Github para obter exemplos de política personalizada sem suporte e ferramentas relacionadas](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Próximas etapas

Explorar dados Olá no Application Insights toohelp você entender como Olá identidade experiência Framework B2C subjacente funciona toodeliver passa por sua própria identidade.
