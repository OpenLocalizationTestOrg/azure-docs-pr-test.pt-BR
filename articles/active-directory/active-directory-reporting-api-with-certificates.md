---
title: "aaaGet dados usando Olá API do Azure AD Reporting com certificados | Microsoft Docs"
description: "Explica como toouse Olá API do Azure AD relatórios com dados de tooget de credenciais do certificado de diretórios sem intervenção do usuário."
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
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="f78df-103">Obter dados usando a API de relatórios do AD do Azure Olá com certificados</span><span class="sxs-lookup"><span data-stu-id="f78df-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="f78df-104">Este artigo aborda como toouse Olá API do Azure AD relatórios com dados de tooget de credenciais do certificado de diretórios sem intervenção do usuário.</span><span class="sxs-lookup"><span data-stu-id="f78df-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="f78df-105">Use Olá API Reporting do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f78df-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="f78df-106">API do Azure AD Reporting requer que você conclua Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f78df-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="f78df-107">Instalar pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f78df-107">Install prerequisites</span></span>
 *  <span data-ttu-id="f78df-108">Defina o certificado de saudação em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f78df-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="f78df-109">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="f78df-109">Get an access token</span></span>
 *  <span data-ttu-id="f78df-110">Use Olá toocall token de acesso Olá API do Graph</span><span class="sxs-lookup"><span data-stu-id="f78df-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="f78df-111">Para saber mais sobre o código-fonte, confira [Aproveitar o módulo da API de Relatório](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span><span class="sxs-lookup"><span data-stu-id="f78df-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="f78df-112">Instalar pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f78df-112">Install prerequisites</span></span>
<span data-ttu-id="f78df-113">Você precisará toohave V2 do PowerShell do Azure AD e o módulo AzureADUtils instalado.</span><span class="sxs-lookup"><span data-stu-id="f78df-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="f78df-114">Baixe e instale o Azure AD Powershell V2, seguindo as instruções de saudação em [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="f78df-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="f78df-115">Baixar o módulo de utilitários do AD do Azure de saudação do [doWindows Azure/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="f78df-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="f78df-116">Esse módulo fornece vários cmdlets do utilitário, incluindo:</span><span class="sxs-lookup"><span data-stu-id="f78df-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="f78df-117">versão mais recente de saudação do ADAL usando o Nuget</span><span class="sxs-lookup"><span data-stu-id="f78df-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="f78df-118">Tokens de acesso do usuário, chaves de aplicativo e certificados usando ADAL</span><span class="sxs-lookup"><span data-stu-id="f78df-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="f78df-119">Resultados paginados de manipulação da API do Graph</span><span class="sxs-lookup"><span data-stu-id="f78df-119">Graph API handling paged results</span></span>

<span data-ttu-id="f78df-120">**módulo de utilitários do AD do Azure de saudação tooinstall:**</span><span class="sxs-lookup"><span data-stu-id="f78df-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="f78df-121">Criar um módulo de utilitários de saudação do diretório toosave (por exemplo, c:\azureAD) e baixar o módulo de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="f78df-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="f78df-122">Abra uma sessão do PowerShell e vá toohello diretório recém-criado.</span><span class="sxs-lookup"><span data-stu-id="f78df-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="f78df-123">Importar o módulo hello e instale-o no caminho do módulo PowerShell hello usando o cmdlet Olá AzureADUtilsModule de instalação.</span><span class="sxs-lookup"><span data-stu-id="f78df-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="f78df-124">sessão Olá deve parecer semelhante tela de toothis:</span><span class="sxs-lookup"><span data-stu-id="f78df-124">hello session should look similar toothis screen:</span></span>

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="f78df-126">Defina o certificado de saudação em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f78df-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="f78df-127">Se você já tiver um aplicativo, obtenha sua ID de objeto de saudação Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f78df-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="f78df-129">Abra uma sessão do PowerShell e conecte-se tooAzure AD usando o cmdlet Olá Connect-doWindows Azure.</span><span class="sxs-lookup"><span data-stu-id="f78df-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="f78df-131">Use Olá AzureADApplicationCertificateCredential novo cmdlet de AzureADUtils tooadd um tooit de credenciais do certificado.</span><span class="sxs-lookup"><span data-stu-id="f78df-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="f78df-132">Você precisa tooprovide Olá aplicativo ID de objeto que você capturou anteriormente, bem como Olá objeto de certificado (obter isso usando Olá Cert: unidade).</span><span class="sxs-lookup"><span data-stu-id="f78df-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Portal do Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="f78df-134">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="f78df-134">Get an access token</span></span>

<span data-ttu-id="f78df-135">tooget um token de acesso, use o cmdlet de Get-AzureADGraphAPIAccessTokenFromCert de saudação da AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="f78df-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="f78df-136">É necessário toouse Olá ID do aplicativo em vez da saudação ID de objeto que você usou na última seção do hello.</span><span class="sxs-lookup"><span data-stu-id="f78df-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="f78df-138">Use Olá toocall token de acesso Olá API do Graph</span><span class="sxs-lookup"><span data-stu-id="f78df-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="f78df-139">Agora você pode criar o script hello.</span><span class="sxs-lookup"><span data-stu-id="f78df-139">Now you can create hello script.</span></span> <span data-ttu-id="f78df-140">Abaixo está um exemplo usando o cmdlet Invoke-AzureADGraphAPIQuery de saudação da saudação AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="f78df-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="f78df-141">Esse cmdlet lida com várias páginas de resultados e, em seguida, envia o pipeline do PowerShell de toohello esses resultados.</span><span class="sxs-lookup"><span data-stu-id="f78df-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="f78df-143">Você agora está pronto tooexport tooa CSV e salva tooa SIEM sistema.</span><span class="sxs-lookup"><span data-stu-id="f78df-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="f78df-144">Você também pode quebrar seu script em uma tarefa agendada de tooget dados do AD do Azure do seu locatário periodicamente sem a necessidade de chaves do aplicativo toostore no código-fonte hello.</span><span class="sxs-lookup"><span data-stu-id="f78df-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f78df-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f78df-145">Next steps</span></span>
[<span data-ttu-id="f78df-146">conceitos básicos de saudação do gerenciamento de identidades do Azure</span><span class="sxs-lookup"><span data-stu-id="f78df-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



