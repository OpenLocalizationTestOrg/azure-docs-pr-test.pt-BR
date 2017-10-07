---
title: "Azure Active Directory B2C: definições e exemplos de API de relatório de uso | Microsoft Docs"
description: "Guia e exemplos de como obter relatórios sobre usuários de locatário, autenticações e autenticações multifator do Azure AD B2C"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>Acessando os relatórios de uso do Azure AD B2C via Olá API de relatório

O Azure AD B2C (Azure Active Directory B2C) fornece autenticação com base na entrada do usuário e na Autenticação Multifator do Azure. A autenticação é fornecida para usuários finais da sua família de aplicativos em provedores de identidade. Quando você souber o número de saudação de usuários registrados no locatário hello, provedores de saudação usavam tooregister e número de autenticações de saudação por tipo, você pode responder a perguntas como:
* Quantos usuários de cada tipo de provedor de identidade (por exemplo, uma conta da Microsoft ou LinkedIn) foram registrados no hello últimos 10 dias?
* Quantas autenticações usando a autenticação multifator foram concluídos com êxito no Olá no último mês?
* Quantas autenticações baseadas em início de sessão foram concluídas neste mês? Por dia? Por aplicativo?
* Como estimar Olá esperado custo mensal da minha atividade de locatário do Azure AD B2C?

Este artigo se concentra na atividade de toobilling relatórios vinculados, que é baseada no número de saudação de usuários, autenticações de entrada no baseado faturáveis e autenticação multifator.


## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, você precisa de etapas Olá toocomplete [tooaccess pré-requisitos Olá relatórios do Azure AD APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/). Criar um aplicativo, obter um segredo para ele e conceder acesso a ele direitos relatórios tooyour do Azure AD B2C do locatário. Também são fornecidos aqui os exemplos de *script Bash* e de *script Python*. 

## <a name="powershell-script"></a>Script do PowerShell
Este script demonstra a criação de saudação de quatro relatórios de uso usando Olá `TimeStamp` parâmetro e hello `ApplicationId` filtro.

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a>Definições de relatório de uso
* **tenantUserCount**: Olá número de usuários no locatário Olá por tipo de provedor de identidade por dia em Olá últimos 30 dias. (Opcionalmente, um `TimeStamp` filtro fornece a contagem de usuários de uma data especificada toohello data atual). relatório de saudação fornece:
  * **TotalUserCount**: Olá número de todos os objetos de usuário.
  * **OtherUserCount**: Olá o número de usuários do Active Directory do Azure (não o Azure AD B2C usuários).
  * **LocalUserCount**: Olá número de contas de usuário do Azure AD B2C criadas com locatário de toohello local do Azure AD B2C credenciais.

* **AlternateIdUserCount**: número de saudação do Azure AD B2C usuários registrados com provedores de identidade externa (por exemplo, Facebook, uma conta da Microsoft ou outro locatário do Active Directory do Azure, também chamado tooas um `OrgId`).

* **b2cAuthenticationCountSummary**: Resumo do número de diário Olá de autenticações faturáveis sobre Olá últimos 30 dias, por dia e o tipo de fluxo de autenticação.

* **b2cAuthenticationCount**: Olá número de autenticações dentro de um período de tempo. padrão de saudação é hello últimos 30 dias.  (Opcional: saudação inicial e final `TimeStamp` parâmetros definem um período de tempo específico.) Olá saída inclui `StartTimeStamp` (data mais antiga de atividade para este Locatário) e `EndTimeStamp` (atualização mais recente).

* **b2cMfaRequestCountSummary**: Resumo do número de diário de saudação de autenticações de vários fatores, por dia e o tipo (SMS ou voz).


## <a name="limitations"></a>Limitações
Dados de contagem de usuário são atualizados a cada 24 horas too48. As autenticações são atualizadas várias vezes ao dia. Ao usar o hello `ApplicationId` filtro, uma resposta de relatório vazio pode ser devida tooone das seguintes condições:
  * ID do aplicativo Hello não existe no locatário hello. Verifique se que ele está correto.
  * ID do aplicativo Hello existe, mas nenhum dado foi encontrado no hello período do relatório. Examine seus parâmetros de data/hora.


## <a name="next-steps"></a>Próximas etapas
### <a name="monthly-bill-estimates-for-azure-ad"></a>Estimativas de cobrança mensal do Azure AD
Quando combinado com [hello mais atual do Azure AD B2C preços disponíveis](https://azure.microsoft.com/pricing/details/active-directory-b2c/), você pode estimar diários, semana e mensal consumo do Azure.  Uma estimativa é especialmente útil ao planejar alterações no comportamento do locatário que possam afetar o custo geral. Você pode examinar os custos reais na sua [assinatura vinculada do Azure](active-directory-b2c-how-to-enable-billing.md).

### <a name="options-for-other-output-formats"></a>Opções para outros formatos de saída
Olá código a seguir mostra exemplos de enviar a saída tooJSON e uma lista de valores de nome XML:
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
