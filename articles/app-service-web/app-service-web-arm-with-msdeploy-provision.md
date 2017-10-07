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
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>Implantar um aplicativo Web com o MSDeploy, um nome de host personalizado e um certificado SSL
Este guia aborda a criação de uma implantação de ponta a ponta para um aplicativo Web do Azure, aproveitando MSDeploy, bem como adiciona um nome de host personalizado e um modelo do ARM SSL certificado toohello.

Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Criar o aplicativo de exemplo
Você implantará um aplicativo Web ASP.NET. Olá primeira etapa é toocreate um aplicativo web simples (ou você pode escolher um existente toouse - nesse caso, você pode ignorar esta etapa).

Abra o Visual Studio 2015 e escolha Arquivo > Novo Projeto. Na caixa de diálogo de saudação que aparece, escolha Web > aplicativo Web ASP.NET. Em modelos de escolha da Web e escolha o modelo MVC de saudação. Selecione *alterar o tipo de autenticação* muito*sem autenticação*. Isso é apenas toomake exemplo aplicativo hello mais simple possível.

Neste ponto, você terá um toouse pronto básica do ASP.Net web aplicativo como parte do processo de implantação.

### <a name="create-msdeploy-package"></a>Criar um pacote do MSDeploy
Próxima etapa é toocreate Olá pacote toodeploy Olá web aplicativo tooAzure. toodo isso, salvar o projeto e, em seguida, execute Olá seguinte da linha de comando de saudação:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Isso criará um pacote compactado na pasta de PackageLocation hello. Olá aplicativo está agora pronto toobe implantado, que agora você pode criar um toodo de modelo do Gerenciador de recursos do Azure que.

### <a name="create-arm-template"></a>Criar um modelo ARM
Primeiro, vamos começar com um modelo ARM básico que criará um aplicativo Web e um plano de hospedagem (observe que os parâmetros e as variáveis não serão mostrados para tudo ficar mais conciso).

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

Em seguida, você precisará toomodify Olá web app recursos tootake um recurso MSDeploy aninhado. Isso permitir que você tooreference Olá pacote criado anteriormente e informar o Azure Resource Manager toouse MSDeploy toodeploy Olá pacote toohello WebApp do Azure. seguinte Olá mostra recurso Microsoft.Web/sites Olá Olá aninhado MSDeploy recursos:

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

Agora você vai notar que Olá MSDeploy recurso usa um **packageUri** propriedade que é definida da seguinte maneira:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

Isso **packageUri** usa Olá uri da conta de armazenamento que a conta de armazenamento toohello onde você carregará o zip do pacote para pontos. Hello Azure Resource Manager aproveitará [assinaturas de acesso compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pacote de saudação toopull para baixo localmente da conta de armazenamento de hello quando você implanta o modelo de saudação. Esse processo será automatizado por meio de um script do PowerShell que carregar pacote hello e chamar hello API de gerenciamento do Azure toocreate Olá as chaves necessárias e passar em modelo hello como parâmetros (*_artifactsLocation* e *_artifactsLocationSasToken*). Você precisará toodefine parâmetros para a pasta hello e pacote de saudação do nome de arquivo é o contêiner de armazenamento de saudação do toounder carregado.

Em seguida, você precisa tooadd em outro recurso aninhado toosetup Olá hostname associações tooleverage um domínio personalizado. Será verificado primeiro tooensure necessidade que possui o nome de host de saudação e configurá-lo toobe pelo Azure que você possui - consulte [configurar um nome de domínio personalizado no serviço de aplicativo do Azure](app-service-web-tutorial-custom-domain.md). Depois disso, você pode adicionar Olá tooyour modelo na seção de recursos Microsoft.Web/sites Olá a seguir:

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

Finalmente você precisa tooadd outro recurso de nível superior, Microsoft.Web/certificates. Esse recurso terá seu certificado SSL e existirão no plano de mesmo nível como seu aplicativo web e hospedagem de saudação.

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

Você precisará toohave um certificado SSL válido na ordem tooset esse recurso. Uma vez que esse certificado válido, em seguida, você precisa de tooextract Olá pfx bytes como uma cadeia de caracteres base64. Uma opção tooextract trata Olá toouse comando PowerShell a seguir:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

Em seguida, você poderia passar isso como um modelo de implantação do parâmetro tooyour ARM.

Agora o modelo do ARM hello está pronto.

### <a name="deploy-template"></a>Implantar o modelo
Olá etapas finais são toopiece isso juntos em uma implantação completa ponta a ponta. toomake implantação fácil, você pode aproveitar a saudação **AzureResourceGroup.ps1 implantar** script do PowerShell que é adicionado quando você cria um projeto do grupo de recursos do Azure no Visual Studio toohelp com carregamento de qualquer artefatos necessários no modelo de saudação. Ele requer toohave criada uma conta de armazenamento que você deseja toouse antecipadamente. Neste exemplo, criei uma conta de armazenamento compartilhado para Olá package.zip toobe carregado. script Hello utilizará a conta de armazenamento de toohello AzCopy tooupload Olá pacote. Você passa em seu local de pasta de artefato e script hello carregará automaticamente todos os arquivos em que toohello diretório denominado contêiner de armazenamento. Depois de chamar implantar AzureResourceGroup.ps1 tiver toothen atualização Olá SSL associações toomap Olá nome do host personalizado com seu certificado SSL.

Olá mostra PowerShell a seguir Olá Olá chamada de implantação completa Deploy-AzureResourceGroup.ps1:

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

Neste ponto seu aplicativo deve ter foi implantado e você deve ser capaz de toobrowse tooit via https://www.yourcustomdomain.com

