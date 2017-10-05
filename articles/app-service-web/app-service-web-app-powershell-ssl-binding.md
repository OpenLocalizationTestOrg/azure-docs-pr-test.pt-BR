---
title: "Associação de certificados SSL usando o PowerShell"
description: Saiba como associar certificados SSL ao seu aplicativo Web usando o PowerShell.
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
ms.openlocfilehash: a1fcc618fb0c68778e39cc227368a60b008f9401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="69b1c-103">Associação de certificado SSL do Serviço de Aplicativo do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="69b1c-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="69b1c-104">Com o lançamento do Microsoft Azure PowerShell versão 1.1.0, um novo cmdlet foi adicionado para dar ao usuário a capacidade de associar certificados SSL novos ou existentes a um aplicativo Web existente.</span><span class="sxs-lookup"><span data-stu-id="69b1c-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give the user the ability to bind existing or new SSL certificates to an existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="69b1c-105">Para saber mais sobre como usar os cmdlets do Azure PowerShell baseados no Azure Resource Manager para gerenciar Aplicativos Web, confira [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="69b1c-105">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="69b1c-106">Carregando e associando um novo certificado SSL</span><span class="sxs-lookup"><span data-stu-id="69b1c-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="69b1c-107">Cenário: o usuário gostaria de associar um certificado SSL a um dos seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="69b1c-107">Scenario: The user would like to bind an SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="69b1c-108">Se soubermos o nome do grupo de recursos que contém o aplicativo Web, o nome do aplicativo Web, o caminho de arquivo. pfx de certificado no computador do usuário, a senha para o certificado e o nome de host personalizado, poderemos usar o seguinte comando do PowerShell para criar essa associação de SSL:</span><span class="sxs-lookup"><span data-stu-id="69b1c-108">Knowing the resource group name that contains the web app, the web app name, the certificate .pfx file path on the user machine, the password for the certificate, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="69b1c-109">Observe que antes de adicionar uma associação SSL a um aplicativo Web, você já deverá ter configurado um nome de host (domínio personalizado).</span><span class="sxs-lookup"><span data-stu-id="69b1c-109">Note that before adding a SSL binding to a web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="69b1c-110">Se o nome de host não estiver configurado, você receberá um erro dizendo que o ‘nome de host’ não existe durante a execução de New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="69b1c-110">If the host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="69b1c-111">Você pode adicionar um nome de host diretamente do portal ou usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69b1c-111">You can add a hostname directly from the portal or using Azure PowerShell.</span></span> <span data-ttu-id="69b1c-112">O seguinte trecho do PowerShell pode ser usado para configurar o nome do host antes de executar o New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="69b1c-112">The following PowerShell snippet can be to configure the hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="69b1c-113">É importante entender que o cmdlet Set-AzureRmWebApp substitui o nome de host do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="69b1c-113">It is important to understand that the Set-AzureRmWebApp cmdlet overwrites the hostnames for the web app.</span></span> <span data-ttu-id="69b1c-114">Portanto, o trecho do PowerShell acima é anexado à lista existente de nomes de host para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="69b1c-114">Hence the above PowerShell snippet is appending to the existing list of the host names for the web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="69b1c-115">Carregando e associando um certificado SSL existente</span><span class="sxs-lookup"><span data-stu-id="69b1c-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="69b1c-116">Cenário: o usuário gostaria de associar um certificado SSL carregado anteriormente a um dos seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="69b1c-116">Scenario: The user would like to bind a previously uploaded SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="69b1c-117">Podemos obter a lista de certificados já carregados para um grupo de recursos específico usando o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="69b1c-117">We can get the list of certificates already uploaded to a specific resource group by using the following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="69b1c-118">Observe que os certificados são locais para localidade e grupo de recursos específicos. O usuário precisará carregar novamente o certificado se o aplicativo Web configurado estiver em local e recurso de grupo diferentes do certificado necessário</span><span class="sxs-lookup"><span data-stu-id="69b1c-118">Note that the certificates are local to a specific location and resource group, the user need to re-upload the certificate if the configured web app is in a different location and resource group other that that of the needed certificate</span></span> 

<span data-ttu-id="69b1c-119">Se soubermos o nome do grupo de recursos que contém o aplicativo Web, o nome do aplicativo Web, a impressão digital do certificado e o nome de host personalizado, poderemos usar o seguinte comando do PowerShell para criar essa associação de SSL:</span><span class="sxs-lookup"><span data-stu-id="69b1c-119">Knowing the resource group name that contains the web app, the web app name, the certificate thumbprint, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="69b1c-120">Excluindo uma associação SSL existente</span><span class="sxs-lookup"><span data-stu-id="69b1c-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="69b1c-121">Cenário: o usuário deseja excluir uma associação SSL existente.</span><span class="sxs-lookup"><span data-stu-id="69b1c-121">Scenario: The user would like to delete an existing SSL binding.</span></span>

<span data-ttu-id="69b1c-122">Se soubermos o nome do grupo de recursos que contém o aplicativo Web, o nome do aplicativo Web e o nome de host personalizado, poderemos usar o seguinte comando do PowerShell para criar essa associação de SSL:</span><span class="sxs-lookup"><span data-stu-id="69b1c-122">Knowing the resource group name that contains the web app, the web app name, and the custom hostname, we can use the following PowerShell command to remove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="69b1c-123">Observe que, se a associação de SSL removida for a última associação que usar esse certificado naquele local, por padrão o certificado será excluído. Se o usuário desejar manter o certificado, ele poderá usar a opção DeleteCertificate para mantê-lo</span><span class="sxs-lookup"><span data-stu-id="69b1c-123">Note that if the removed SSL binding was the last binding using that certificate in that location, by default the certificate will be deleted, if the user want to keep the certificate he can use the DeleteCertificate option to keep the certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="69b1c-124">Referências</span><span class="sxs-lookup"><span data-stu-id="69b1c-124">References</span></span>
* [<span data-ttu-id="69b1c-125">Azure Resource Manager based PowerShell commands for Azure Web App</span><span class="sxs-lookup"><span data-stu-id="69b1c-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="69b1c-126">Introdução ao ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="69b1c-126">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="69b1c-127">Usando o Azure PowerShell com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="69b1c-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

