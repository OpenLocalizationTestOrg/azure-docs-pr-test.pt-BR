---
title: Implantar um aplicativo Web usando o MSDeploy com um nome de host e um certificado ssl
description: Use um modelo do Gerenciador de Recursos do Azure para implantar um aplicativo Web usando o MSDeploy e configurando um nome de host personalizado e um certificado SSL
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="668a5-103">Implantar um aplicativo Web com o MSDeploy, um nome de host personalizado e um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="668a5-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="668a5-104">Este guia orienta você durante a criação de uma implantação ponta a ponta para um Aplicativo Web do Azure usando o MSDeploy e adicionando um nome de host personalizado e um certificado SSL ao modelo ARM.</span><span class="sxs-lookup"><span data-stu-id="668a5-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span></span>

<span data-ttu-id="668a5-105">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="668a5-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="668a5-106">Criar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="668a5-106">Create Sample Application</span></span>
<span data-ttu-id="668a5-107">Você implantará um aplicativo Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="668a5-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="668a5-108">A primeira etapa é criar um aplicativo Web simples (ou você pode optar por usar um existente — nesse caso, ignore esta etapa).</span><span class="sxs-lookup"><span data-stu-id="668a5-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="668a5-109">Abra o Visual Studio 2015 e escolha Arquivo > Novo Projeto.</span><span class="sxs-lookup"><span data-stu-id="668a5-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="668a5-110">Na caixa de diálogo que aparecer, escolha Web > aplicativo Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="668a5-110">On the dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="668a5-111">Em Modelos, escolha Web e escolha o modelo MVC.</span><span class="sxs-lookup"><span data-stu-id="668a5-111">Under Templates choose Web and choose the MVC template.</span></span> <span data-ttu-id="668a5-112">Selecione *Alterar tipo de autenticação* para *Sem Autenticação*.</span><span class="sxs-lookup"><span data-stu-id="668a5-112">Select *Change authentication type* to *No Authentication*.</span></span> <span data-ttu-id="668a5-113">Isso é apenas para simplificar ao máximo o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="668a5-113">This is just to make the sample application as simple as possible.</span></span>

<span data-ttu-id="668a5-114">Neste ponto, você terá um aplicativo Web ASP.Net básico pronto para uso como parte do processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="668a5-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="668a5-115">Criar um pacote do MSDeploy</span><span class="sxs-lookup"><span data-stu-id="668a5-115">Create MSDeploy package</span></span>
<span data-ttu-id="668a5-116">A próxima etapa será criar o pacote para implantar o aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="668a5-116">Next step is to create the package to deploy the web app to Azure.</span></span> <span data-ttu-id="668a5-117">Para fazer isso, salve seu projeto e execute o seguinte na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="668a5-117">To do this, save your project and then run the following from the command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="668a5-118">Isso criará um pacote compactado na pasta PackageLocation.</span><span class="sxs-lookup"><span data-stu-id="668a5-118">This will create a zipped package under the PackageLocation folder.</span></span> <span data-ttu-id="668a5-119">O aplicativo está pronto para ser implantado; agora você pode compilar um modelo do Gerenciador de Recursos do Azure para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="668a5-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="668a5-120">Criar um modelo ARM</span><span class="sxs-lookup"><span data-stu-id="668a5-120">Create ARM Template</span></span>
<span data-ttu-id="668a5-121">Primeiro, vamos começar com um modelo ARM básico que criará um aplicativo Web e um plano de hospedagem (observe que os parâmetros e as variáveis não serão mostrados para tudo ficar mais conciso).</span><span class="sxs-lookup"><span data-stu-id="668a5-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

<span data-ttu-id="668a5-122">Em seguida, você precisará modificar o recurso de aplicativo Web para que ele obtenha um recurso aninhado do MSDeploy.</span><span class="sxs-lookup"><span data-stu-id="668a5-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span></span> <span data-ttu-id="668a5-123">Isso permitirá que você referencie o pacote criado anteriormente e diga ao Gerenciador de Recursos do Azure para usar o MSDeploy para implantar o pacote no Aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="668a5-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span></span> <span data-ttu-id="668a5-124">A seguir, o recurso Microsoft.Web/sites com o recurso aninhado do MSDeploy:</span><span class="sxs-lookup"><span data-stu-id="668a5-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span></span>

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

<span data-ttu-id="668a5-125">Agora você observará que o recurso do MSDeploy obtém uma propriedade **packageUri** , definida desta forma:</span><span class="sxs-lookup"><span data-stu-id="668a5-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="668a5-126">Essa **packageUri** obtém o uri da conta de armazenamento que aponta para a conta de armazenamento para onde você carregará o pacote compactado.</span><span class="sxs-lookup"><span data-stu-id="668a5-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span></span> <span data-ttu-id="668a5-127">O Gerenciador de Recursos do Azure aproveitará as [Assinaturas de Acesso Compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para obter o pacote localmente da conta de armazenamento durante a implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="668a5-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span></span> <span data-ttu-id="668a5-128">Este processo será automatizado por meio de um script do PowerShell que carregará o pacote e chamará a API de Gerenciamento do Azure para criar as chaves necessárias e passá-las para o modelo como parâmetros (*_artifactsLocation* e *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="668a5-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="668a5-129">Será necessário definir parâmetros para a pasta em que o pacote será carregado no contêiner de armazenamento e para o nome de arquivo desse pacote.</span><span class="sxs-lookup"><span data-stu-id="668a5-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span></span>

<span data-ttu-id="668a5-130">Em seguida, adicione outro recurso aninhado para configurar as associações de nome de host para aproveitar um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="668a5-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span></span> <span data-ttu-id="668a5-131">Primeiro, você precisará garantir que você possui o nome de host e configurá-lo para que o Azure verifique você o possui - consulte [Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="668a5-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="668a5-132">Depois disso, você poderá adicionar o seguinte ao seu modelo na seção do recurso Microsoft.Web/sites:</span><span class="sxs-lookup"><span data-stu-id="668a5-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span></span>

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

<span data-ttu-id="668a5-133">Por fim, adicione outro recurso de nível superior, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="668a5-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="668a5-134">Esse recurso conterá o certificado SSL e existirá no mesmo nível do aplicativo Web e do plano de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="668a5-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span></span>

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

<span data-ttu-id="668a5-135">Você precisará ter um certificado SSL válido para configurar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="668a5-135">You will need to have a valid SSL certificate in order to set up this resource.</span></span> <span data-ttu-id="668a5-136">Quando você tiver um certificado válido, será necessário extrair os bytes pfx como uma cadeia de caracteres de base64.</span><span class="sxs-lookup"><span data-stu-id="668a5-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span></span> <span data-ttu-id="668a5-137">Uma opção para extrair isso é usar o seguinte comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="668a5-137">One option to extract this is to use the following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="668a5-138">Em seguida, você poderia passar isso como um parâmetro para o modelo de implantação ARM.</span><span class="sxs-lookup"><span data-stu-id="668a5-138">You could then pass this as a parameter to your ARM deployment template.</span></span>

<span data-ttu-id="668a5-139">Neste ponto, o modelo ARM estará pronto.</span><span class="sxs-lookup"><span data-stu-id="668a5-139">At this point the ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="668a5-140">Implantar o modelo</span><span class="sxs-lookup"><span data-stu-id="668a5-140">Deploy Template</span></span>
<span data-ttu-id="668a5-141">As etapas finais são juntar tudo isso em uma implantação completa ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="668a5-141">The final steps are to piece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="668a5-142">Para facilitar a implantação, você pode aproveitar o script **Deploy-AzureResourceGroup.ps1** do PowerShell adicionado durante a criação de um projeto do Grupo de Recursos do Azure no Visual Studio para ajudar no carregamento de todos os artefatos necessários ao modelo.</span><span class="sxs-lookup"><span data-stu-id="668a5-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span></span> <span data-ttu-id="668a5-143">Ele exige a criação prévia de uma conta de armazenamento que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="668a5-143">It requires you to have created a storage account you want to use ahead of time.</span></span> <span data-ttu-id="668a5-144">Neste exemplo, criei uma conta de armazenamento compartilhada para o pacote.zip a ser carregado.</span><span class="sxs-lookup"><span data-stu-id="668a5-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span></span> <span data-ttu-id="668a5-145">O script utilizará o AzCopy para carregar o pacote para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="668a5-145">The script will leverage AzCopy to upload the package to the storage account.</span></span> <span data-ttu-id="668a5-146">Você passa o local da pasta do artefato e o script carregará automaticamente todos os arquivos desse diretório para o contêiner de armazenamento nomeado.</span><span class="sxs-lookup"><span data-stu-id="668a5-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span></span> <span data-ttu-id="668a5-147">Depois de chamar Deploy-AzureResourceGroup.ps1, você deverá atualizar as associações SSL para mapear o nome de host personalizado com o certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="668a5-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="668a5-148">O PowerShell a seguir mostra a implantação completa chamando Deploy-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="668a5-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="668a5-149">Neste ponto, seu aplicativo deve ter sido implantado e você deve ser capaz de localizá-lo por meio de https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="668a5-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span></span>

