---
title: "aaaSpecifying uma versão de Node. js"
description: "Saiba como toospecify Olá versão do Node. js usados por Sites do Azure e serviços de nuvem"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="6ebf5-103">Especificar uma versão do Node.js em um aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="6ebf5-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="6ebf5-104">Ao hospedar um aplicativo Node. js, talvez você queira tooensure que o aplicativo usa uma versão específica do Node. js.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="6ebf5-105">Há várias tooaccomplish de maneiras isso para aplicativos hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="6ebf5-106">Versões padrão</span><span class="sxs-lookup"><span data-stu-id="6ebf5-106">Default versions</span></span>
<span data-ttu-id="6ebf5-107">versões do Node. js Olá fornecidas pelo Azure são constantemente atualizadas.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="6ebf5-108">A menos que especificado o contrário, Olá versão padrão que é especificado no hello `WEBSITE_NODE_DEFAULT_VERSION` variável de ambiente será usada.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="6ebf5-109">toooverride esse valor padrão, siga as etapas de saudação nas seguintes seções deste artigo</span><span class="sxs-lookup"><span data-stu-id="6ebf5-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="6ebf5-110">Se você estiver hospedando seu aplicativo em um serviço de nuvem do Azure (função web ou de trabalho), e é Olá primeira vez que você implantou o aplicativo hello, Azure tentará toouse Olá a mesma versão do Node. js que você instalou no seu ambiente de desenvolvimento, se ele corresponde a uma das versões de padrão de saudação disponíveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="6ebf5-111">Controle de versão com o package.json</span><span class="sxs-lookup"><span data-stu-id="6ebf5-111">Versioning with package.json</span></span>
<span data-ttu-id="6ebf5-112">Você pode especificar a versão de saudação do Node. js toobe usado adicionando Olá tooyour a seguir **Package. JSON** arquivo:</span><span class="sxs-lookup"><span data-stu-id="6ebf5-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="6ebf5-113">Onde *versão* é toouse de número de versão específica de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="6ebf5-114">Você pode especificar condições mais complexas de versão, como:</span><span class="sxs-lookup"><span data-stu-id="6ebf5-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="6ebf5-115">Como 0.6.22 não é uma das versões de saudação disponíveis no ambiente de hospedagem de Olá, hello versão mais recente do hello 0,8 série disponível será usado em vez disso, - 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="6ebf5-116">Sites de controle de versão com configurações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="6ebf5-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="6ebf5-117">Se você estiver hospedando o aplicativo hello em um site, você pode definir a variável de ambiente Olá **WEBSITE_NODE_DEFAULT_VERSION** versão desejada de toohello.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="6ebf5-118">Controle de versão dos Serviços de Nuvem com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ebf5-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="6ebf5-119">Se você estiver hospedando o aplicativo hello em um serviço de nuvem e implantar o aplicativo hello usando o PowerShell do Azure, você pode substituir a versão de Node. js padrão Olá usando Olá **AzureServiceProjectRole conjunto** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="6ebf5-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6ebf5-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="6ebf5-121">Observação parâmetros Olá Olá acima instrução diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="6ebf5-122">Você pode verificar a versão correta de saudação do Node. js foi selecionada verificando Olá **mecanismos** propriedade na sua função **Package. JSON**.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="6ebf5-123">Você também pode usar o hello **Get-AzureServiceProjectRoleRuntime** tooretrieve uma lista das versões do Node. js disponíveis para aplicativos hospedados como um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="6ebf5-124">Sempre verificar a versão de saudação do Node. js depende de seu projeto está na lista.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="6ebf5-125">Usando uma versão personalizada com Sites do Azure</span><span class="sxs-lookup"><span data-stu-id="6ebf5-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="6ebf5-126">Enquanto o Azure fornece várias versões padrão do Node. js, talvez você queira toouse uma versão que não é fornecida por padrão.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="6ebf5-127">Se seu aplicativo for hospedado como um site do Azure, você pode fazer isso usando Olá **iisnode.yml** arquivo.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="6ebf5-128">Olá etapas a seguir conduzem pelo processo de saudação do uso de uma versão personalizada do Node. js com um site do Azure:</span><span class="sxs-lookup"><span data-stu-id="6ebf5-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="6ebf5-129">Criar um novo diretório e, em seguida, criar um **server.js** arquivo no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="6ebf5-130">Olá **server.js** arquivo deve conter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="6ebf5-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="6ebf5-131">Versão do Node. js hello está sendo usado quando você procurar o site Olá será exibido.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="6ebf5-132">Crie um novo site e um nome de saudação de observação do site de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="6ebf5-133">Por exemplo, o seguinte Olá usa Olá [as ferramentas de linha de comando do Azure] toocreate um novo site do Azure denominado **meuwebsite**e, em seguida, habilitar um repositório Git para o site de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="6ebf5-134">Crie um novo diretório chamado **bin** como um filho do diretório de saudação contendo Olá **server.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="6ebf5-135">Baixar a versão específica de saudação do **node.exe** (versão do Windows hello) que você deseja toouse com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="6ebf5-136">Por exemplo, Olá a seguir usa **curl** versão toodownload 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="6ebf5-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="6ebf5-137">Salvar Olá **node.exe** arquivo hello **bin** pasta criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="6ebf5-138">Criar um **iisnode.yml** arquivo hello mesmo diretório como Olá **server.js** de arquivo e depois adicione Olá toohello conteúdo a seguir **iisnode.yml** arquivo:</span><span class="sxs-lookup"><span data-stu-id="6ebf5-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="6ebf5-139">Esse caminho é onde hello **node.exe** arquivo dentro de seu projeto será localizado depois de publicar seu site do Azure de toohello do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="6ebf5-140">Publique o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-140">Publish your application.</span></span> <span data-ttu-id="6ebf5-141">Por exemplo, desde que criei um novo site com o parâmetro – git Olá anteriormente, hello comandos a seguir serão adicionar Olá aplicativo arquivos toomy repositório Git local e, em seguida, enviá-las toohello repositório de site:</span><span class="sxs-lookup"><span data-stu-id="6ebf5-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="6ebf5-142">Após ter publicado o aplicativo hello, abra o site de saudação em um navegador.</span><span class="sxs-lookup"><span data-stu-id="6ebf5-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="6ebf5-143">Você deve ver uma mensagem dizendo "Olá da versão do nó que executa o Azure: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="6ebf5-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ebf5-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ebf5-144">Next Steps</span></span>
<span data-ttu-id="6ebf5-145">Agora que você sabe como toospecify versão de saudação do Node. js usada pelo seu aplicativo, saber como muito[funcionam com módulos], [criar e implantar um Site Node.js](app-service-web/app-service-web-get-started-nodejs.md), e [como toouse hello Azure Ferramentas de linha de comando para Mac e Linux].</span><span class="sxs-lookup"><span data-stu-id="6ebf5-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="6ebf5-146">Para obter mais informações, consulte Olá [Node. js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="6ebf5-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[como toouse hello Azure Ferramentas de linha de comando para Mac e Linux]:cli-install-nodejs.md
[as ferramentas de linha de comando do Azure]:cli-install-nodejs.md
[funcionam com módulos]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
