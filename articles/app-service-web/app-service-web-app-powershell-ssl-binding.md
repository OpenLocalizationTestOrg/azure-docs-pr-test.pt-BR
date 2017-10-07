---
title: "Certificados aaaSSL associação usando o PowerShell"
description: Saiba como toobind SSL certificados tooyour web app usando o PowerShell.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="4649a-103">Associação de certificado SSL do Serviço de Aplicativo do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4649a-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="4649a-104">Com a versão de saudação do Microsoft Azure PowerShell versão 1.1.0 foi adicionado um novo cmdlet que daria Olá usuário Olá capacidade toobind nova ou existente SSL certificados tooan aplicativo Web existente.</span><span class="sxs-lookup"><span data-stu-id="4649a-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="4649a-105">toolearn sobre como usar o Gerenciador de recursos do Azure com base em toomanage de cmdlets do PowerShell do Azure sua seleção de aplicativos Web [Gerenciador de recursos do Azure com base em comandos do PowerShell para o aplicativo Web do Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="4649a-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="4649a-106">Carregando e associando um novo certificado SSL</span><span class="sxs-lookup"><span data-stu-id="4649a-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="4649a-107">Cenário: usuário Olá que toobind um tooone de certificado SSL de seus aplicativos da web.</span><span class="sxs-lookup"><span data-stu-id="4649a-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="4649a-108">Saber o nome do grupo de recursos Olá que contém o aplicativo de web Olá, nome do aplicativo web hello, caminho do arquivo. pfx Olá certificado no computador do usuário Olá, Olá senha certificado hello e Olá nome do host personalizado, podemos usar o hello toocreate de comando do PowerShell a seguir que Associação de SSL:</span><span class="sxs-lookup"><span data-stu-id="4649a-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="4649a-109">Observe que, antes de adicionar um aplicativo web de tooa de associação de SSL, você deve ter um nome de host (domínio personalizado) já configurado.</span><span class="sxs-lookup"><span data-stu-id="4649a-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="4649a-110">Se o nome de host Olá não está configurado, você obterá um erro 'hostname' não existe durante a execução AzureRmWebAppSSLBinding de novo.</span><span class="sxs-lookup"><span data-stu-id="4649a-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="4649a-111">Você pode adicionar um nome de host diretamente do portal de saudação ou usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="4649a-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="4649a-112">Hello seguinte trecho do PowerShell pode ser o nome de host do tooconfigure Olá antes de executar o New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="4649a-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="4649a-113">É importante toounderstand que Olá cmdlet Set-AzureRmWebApp substitui Olá nomes de host para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="4649a-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="4649a-114">Portanto, Olá acima trecho do PowerShell estiver anexando lista existente de toohello Olá de nomes de host para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="4649a-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="4649a-115">Carregando e associando um certificado SSL existente</span><span class="sxs-lookup"><span data-stu-id="4649a-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="4649a-116">Cenário: usuário Olá que toobind um tooone previamente carregado de certificado SSL de seus aplicativos da web.</span><span class="sxs-lookup"><span data-stu-id="4649a-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="4649a-117">Podemos obter lista de saudação de certificados já carregado tooa grupo de recursos específicos usando o comando a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="4649a-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="4649a-118">Observe que os certificados Olá são tooa local específico local e grupo de recursos, hello usuário precisa carregar toore Olá certificado se o aplicativo de web de saudação configurado está em um local diferente e recurso grupo outros que de saudação necessário certificado</span><span class="sxs-lookup"><span data-stu-id="4649a-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="4649a-119">Saber o nome do grupo de recursos Olá que contém o aplicativo de web hello, Olá nome do aplicativo web, Olá a impressão digital do certificado e Olá nome do host personalizado, podemos usar Olá toocreate de comando do PowerShell a seguir essa associação de SSL:</span><span class="sxs-lookup"><span data-stu-id="4649a-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="4649a-120">Excluindo uma associação SSL existente</span><span class="sxs-lookup"><span data-stu-id="4649a-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="4649a-121">Cenário: usuário Olá que toodelete uma associação SSL existente.</span><span class="sxs-lookup"><span data-stu-id="4649a-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="4649a-122">Saber o nome do grupo de recursos Olá que contém o aplicativo de web hello, Olá nome do aplicativo web e Olá nome do host personalizado, podemos usar Olá tooremove de comando do PowerShell a seguir essa associação de SSL:</span><span class="sxs-lookup"><span data-stu-id="4649a-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="4649a-123">Observe que se Olá removido associação SSL foi Olá última associação usando esse certificado no local pelo certificado de saudação padrão será excluída, usuário Olá tookeep certificado de saudação ele pode usar o certificado de saudação do hello DeleteCertificate opção tookeep</span><span class="sxs-lookup"><span data-stu-id="4649a-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="4649a-124">Referências</span><span class="sxs-lookup"><span data-stu-id="4649a-124">References</span></span>
* [<span data-ttu-id="4649a-125">Azure Resource Manager based PowerShell commands for Azure Web App</span><span class="sxs-lookup"><span data-stu-id="4649a-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="4649a-126">Introdução tooApp ambiente de serviço</span><span class="sxs-lookup"><span data-stu-id="4649a-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="4649a-127">Usando o Azure PowerShell com o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="4649a-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

