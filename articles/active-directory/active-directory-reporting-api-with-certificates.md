---
title: "Obter dados usando a API de Relatório do Azure AD com certificados | Microsoft Docs"
description: "Explica como usar a API de Relatório do Azure AD com credenciais de certificado para obter dados de diretórios sem intervenção do usuário."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: c1345dcda6e52267a8037ffd7207e6bc3b0d3b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-data-using-the-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="25c76-103">Obter dados usando a API de Relatório do Azure AD com certificados</span><span class="sxs-lookup"><span data-stu-id="25c76-103">Get data using the Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="25c76-104">Este artigo explica como usar a API de Relatório do Azure AD com credenciais de certificado para obter dados de diretórios sem intervenção do usuário.</span><span class="sxs-lookup"><span data-stu-id="25c76-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span></span> 

## <a name="use-the-azure-ad-reporting-api"></a><span data-ttu-id="25c76-105">Usar a API de Relatório do Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c76-105">Use the Azure AD Reporting API</span></span> 
<span data-ttu-id="25c76-106">A API de Relatório do Azure AD exige que você conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="25c76-106">Azure AD Reporting API requires that you complete the following steps:</span></span>
 *  <span data-ttu-id="25c76-107">Instalar pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="25c76-107">Install prerequisites</span></span>
 *  <span data-ttu-id="25c76-108">Definir o certificado em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="25c76-108">Set the certificate in your app</span></span>
 *  <span data-ttu-id="25c76-109">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="25c76-109">Get an access token</span></span>
 *  <span data-ttu-id="25c76-110">Usar o token de acesso para chamar a API do Graph</span><span class="sxs-lookup"><span data-stu-id="25c76-110">Use the access token to call the Graph API</span></span>

<span data-ttu-id="25c76-111">Para saber mais sobre o código-fonte, confira [Aproveitar o módulo da API de Relatório](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span><span class="sxs-lookup"><span data-stu-id="25c76-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="25c76-112">Instalar pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="25c76-112">Install prerequisites</span></span>
<span data-ttu-id="25c76-113">Você precisará ter o Azure AD PowerShell V2 e o módulo AzureADUtils instalados.</span><span class="sxs-lookup"><span data-stu-id="25c76-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="25c76-114">Baixe e instale o Azure AD Powershell V2, seguindo as instruções em [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="25c76-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="25c76-115">Baixe o módulo Azure AD Utils em [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="25c76-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="25c76-116">Esse módulo fornece vários cmdlets do utilitário, incluindo:</span><span class="sxs-lookup"><span data-stu-id="25c76-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="25c76-117">A versão mais recente do ADAL usando o Nuget</span><span class="sxs-lookup"><span data-stu-id="25c76-117">The latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="25c76-118">Tokens de acesso do usuário, chaves de aplicativo e certificados usando ADAL</span><span class="sxs-lookup"><span data-stu-id="25c76-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="25c76-119">Resultados paginados de manipulação da API do Graph</span><span class="sxs-lookup"><span data-stu-id="25c76-119">Graph API handling paged results</span></span>

<span data-ttu-id="25c76-120">**Para instalar o módulo Azure AD Utils:**</span><span class="sxs-lookup"><span data-stu-id="25c76-120">**To install the Azure AD Utils module:**</span></span>

1. <span data-ttu-id="25c76-121">Crie um diretório para salvar o módulo de utilitários (por exemplo, c:\azureAD) e baixe o módulo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="25c76-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span></span>
2. <span data-ttu-id="25c76-122">Abra uma sessão do PowerShell e vá para o diretório que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="25c76-122">Open a PowerShell session, and go to the directory you just created.</span></span> 
3. <span data-ttu-id="25c76-123">Importe o módulo e instale-o no caminho do módulo do PowerShell usando o cmdlet Install-AzureADUtilsModule.</span><span class="sxs-lookup"><span data-stu-id="25c76-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="25c76-124">A sessão deve fica mais ou menos como esta tela:</span><span class="sxs-lookup"><span data-stu-id="25c76-124">The session should look similar to this screen:</span></span>

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-the-certificate-in-your-app"></a><span data-ttu-id="25c76-126">Definir o certificado em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="25c76-126">Set the certificate in your app</span></span>
1. <span data-ttu-id="25c76-127">Se você já tiver um aplicativo, obtenha a ID do objeto do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="25c76-127">If you already have an app, get its Object ID from the Azure Portal.</span></span> 

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="25c76-129">Abra uma sessão do PowerShell e conecte-se ao Azure AD usando o cmdlet Connect-AzureAD.</span><span class="sxs-lookup"><span data-stu-id="25c76-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span></span>

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="25c76-131">Use o cmdlet New-AzureADApplicationCertificateCredential de AzureADUtils para adicionar uma credencial de certificado a ele.</span><span class="sxs-lookup"><span data-stu-id="25c76-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span></span> 

>[!Note]
><span data-ttu-id="25c76-132">Você precisa fornecer a ID de objeto capturada anteriormente, bem como o objeto de certificado do aplicativo (obter isso usando a unidade Cert:).</span><span class="sxs-lookup"><span data-stu-id="25c76-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span></span>
>


  ![Portal do Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="25c76-134">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="25c76-134">Get an access token</span></span>

<span data-ttu-id="25c76-135">Para obter um token de acesso, use o cmdlet Get-AzureADGraphAPIAccessTokenFromCert de AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="25c76-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="25c76-136">Você precisa usar a ID do aplicativo em vez da ID de objeto que você usou na última seção.</span><span class="sxs-lookup"><span data-stu-id="25c76-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span></span>
>

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="25c76-138">Usar o token de acesso para chamar a API do Graph</span><span class="sxs-lookup"><span data-stu-id="25c76-138">Use the access token to call the Graph API</span></span>

<span data-ttu-id="25c76-139">Agora, você pode criar o script.</span><span class="sxs-lookup"><span data-stu-id="25c76-139">Now you can create the script.</span></span> <span data-ttu-id="25c76-140">Abaixo vemos um exemplo usando o cmdlet Invoke-AzureADGraphAPIQuery do AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="25c76-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span></span> <span data-ttu-id="25c76-141">Esse cmdlet lida com várias páginas de resultados e os envia para o pipeline do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25c76-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span> 

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="25c76-143">Agora você está pronto para exportar para um CSV e salvar em um sistema SIEM.</span><span class="sxs-lookup"><span data-stu-id="25c76-143">You are now ready to export to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="25c76-144">Você pode também encapsular o script em uma tarefa agendada para obter dados do Azure AD do seu locatário periodicamente sem a necessidade de armazenar as chaves de aplicativo no código-fonte.</span><span class="sxs-lookup"><span data-stu-id="25c76-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="25c76-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25c76-145">Next steps</span></span>
[<span data-ttu-id="25c76-146">Os fundamentos do gerenciamento de identidades do Azure</span><span class="sxs-lookup"><span data-stu-id="25c76-146">The fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



