---
title: aaaDeploy um aplicativo web usando MSDeploy com certificado de nome de host e ssl
description: Usar um aplicativo web usando MSDeploy e configurando o nome do host personalizado e um certificado SSL de uma toodeploy de modelo do Gerenciador de recursos do Azure
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
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="05225-103">Implantar um aplicativo Web com o MSDeploy, um nome de host personalizado e um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="05225-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="05225-104">Este guia aborda a criação de uma implantação de ponta a ponta para um aplicativo Web do Azure, aproveitando MSDeploy, bem como adiciona um nome de host personalizado e um modelo do ARM SSL certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="05225-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="05225-105">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="05225-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="05225-106">Criar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="05225-106">Create Sample Application</span></span>
<span data-ttu-id="05225-107">Você implantará um aplicativo Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="05225-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="05225-108">Olá primeira etapa é toocreate um aplicativo web simples (ou você pode escolher um existente toouse - nesse caso, você pode ignorar esta etapa).</span><span class="sxs-lookup"><span data-stu-id="05225-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="05225-109">Abra o Visual Studio 2015 e escolha Arquivo > Novo Projeto.</span><span class="sxs-lookup"><span data-stu-id="05225-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="05225-110">Na caixa de diálogo de saudação que aparece, escolha Web > aplicativo Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="05225-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="05225-111">Em modelos de escolha da Web e escolha o modelo MVC de saudação.</span><span class="sxs-lookup"><span data-stu-id="05225-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="05225-112">Selecione *alterar o tipo de autenticação* muito*sem autenticação*.</span><span class="sxs-lookup"><span data-stu-id="05225-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="05225-113">Isso é apenas toomake exemplo aplicativo hello mais simple possível.</span><span class="sxs-lookup"><span data-stu-id="05225-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="05225-114">Neste ponto, você terá um toouse pronto básica do ASP.Net web aplicativo como parte do processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="05225-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="05225-115">Criar um pacote do MSDeploy</span><span class="sxs-lookup"><span data-stu-id="05225-115">Create MSDeploy package</span></span>
<span data-ttu-id="05225-116">Próxima etapa é toocreate Olá pacote toodeploy Olá web aplicativo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="05225-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="05225-117">toodo isso, salvar o projeto e, em seguida, execute Olá seguinte da linha de comando de saudação:</span><span class="sxs-lookup"><span data-stu-id="05225-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="05225-118">Isso criará um pacote compactado na pasta de PackageLocation hello.</span><span class="sxs-lookup"><span data-stu-id="05225-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="05225-119">Olá aplicativo está agora pronto toobe implantado, que agora você pode criar um toodo de modelo do Gerenciador de recursos do Azure que.</span><span class="sxs-lookup"><span data-stu-id="05225-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="05225-120">Criar um modelo ARM</span><span class="sxs-lookup"><span data-stu-id="05225-120">Create ARM Template</span></span>
<span data-ttu-id="05225-121">Primeiro, vamos começar com um modelo ARM básico que criará um aplicativo Web e um plano de hospedagem (observe que os parâmetros e as variáveis não serão mostrados para tudo ficar mais conciso).</span><span class="sxs-lookup"><span data-stu-id="05225-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="05225-122">Em seguida, você precisará toomodify Olá web app recursos tootake um recurso MSDeploy aninhado.</span><span class="sxs-lookup"><span data-stu-id="05225-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="05225-123">Isso permitir que você tooreference Olá pacote criado anteriormente e informar o Azure Resource Manager toouse MSDeploy toodeploy Olá pacote toohello WebApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="05225-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="05225-124">seguinte Olá mostra recurso Microsoft.Web/sites Olá Olá aninhado MSDeploy recursos:</span><span class="sxs-lookup"><span data-stu-id="05225-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

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

<span data-ttu-id="05225-125">Agora você vai notar que Olá MSDeploy recurso usa um **packageUri** propriedade que é definida da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="05225-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="05225-126">Isso **packageUri** usa Olá uri da conta de armazenamento que a conta de armazenamento toohello onde você carregará o zip do pacote para pontos.</span><span class="sxs-lookup"><span data-stu-id="05225-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="05225-127">Hello Azure Resource Manager aproveitará [assinaturas de acesso compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pacote de saudação toopull para baixo localmente da conta de armazenamento de hello quando você implanta o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="05225-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="05225-128">Esse processo será automatizado por meio de um script do PowerShell que carregar pacote hello e chamar hello API de gerenciamento do Azure toocreate Olá as chaves necessárias e passar em modelo hello como parâmetros (*_artifactsLocation* e *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="05225-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="05225-129">Você precisará toodefine parâmetros para a pasta hello e pacote de saudação do nome de arquivo é o contêiner de armazenamento de saudação do toounder carregado.</span><span class="sxs-lookup"><span data-stu-id="05225-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="05225-130">Em seguida, você precisa tooadd em outro recurso aninhado toosetup Olá hostname associações tooleverage um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="05225-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="05225-131">Será verificado primeiro tooensure necessidade que possui o nome de host de saudação e configurá-lo toobe pelo Azure que você possui - consulte [configurar um nome de domínio personalizado no serviço de aplicativo do Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="05225-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="05225-132">Depois disso, você pode adicionar Olá tooyour modelo na seção de recursos Microsoft.Web/sites Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="05225-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="05225-133">Finalmente você precisa tooadd outro recurso de nível superior, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="05225-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="05225-134">Esse recurso terá seu certificado SSL e existirão no plano de mesmo nível como seu aplicativo web e hospedagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="05225-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="05225-135">Você precisará toohave um certificado SSL válido na ordem tooset esse recurso.</span><span class="sxs-lookup"><span data-stu-id="05225-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="05225-136">Uma vez que esse certificado válido, em seguida, você precisa de tooextract Olá pfx bytes como uma cadeia de caracteres base64.</span><span class="sxs-lookup"><span data-stu-id="05225-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="05225-137">Uma opção tooextract trata Olá toouse comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="05225-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="05225-138">Em seguida, você poderia passar isso como um modelo de implantação do parâmetro tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="05225-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="05225-139">Agora o modelo do ARM hello está pronto.</span><span class="sxs-lookup"><span data-stu-id="05225-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="05225-140">Implantar o modelo</span><span class="sxs-lookup"><span data-stu-id="05225-140">Deploy Template</span></span>
<span data-ttu-id="05225-141">Olá etapas finais são toopiece isso juntos em uma implantação completa ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="05225-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="05225-142">toomake implantação fácil, você pode aproveitar a saudação **AzureResourceGroup.ps1 implantar** script do PowerShell que é adicionado quando você cria um projeto do grupo de recursos do Azure no Visual Studio toohelp com carregamento de qualquer artefatos necessários no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="05225-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="05225-143">Ele requer toohave criada uma conta de armazenamento que você deseja toouse antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="05225-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="05225-144">Neste exemplo, criei uma conta de armazenamento compartilhado para Olá package.zip toobe carregado.</span><span class="sxs-lookup"><span data-stu-id="05225-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="05225-145">script Hello utilizará a conta de armazenamento de toohello AzCopy tooupload Olá pacote.</span><span class="sxs-lookup"><span data-stu-id="05225-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="05225-146">Você passa em seu local de pasta de artefato e script hello carregará automaticamente todos os arquivos em que toohello diretório denominado contêiner de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="05225-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="05225-147">Depois de chamar implantar AzureResourceGroup.ps1 tiver toothen atualização Olá SSL associações toomap Olá nome do host personalizado com seu certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="05225-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="05225-148">Olá mostra PowerShell a seguir Olá Olá chamada de implantação completa Deploy-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="05225-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="05225-149">Neste ponto seu aplicativo deve ter foi implantado e você deve ser capaz de toobrowse tooit via https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="05225-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

