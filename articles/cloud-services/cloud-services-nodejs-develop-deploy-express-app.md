---
title: aaaWeb aplicativo com o Express (Node. js) | Microsoft Docs
description: "Um tutorial que se baseia no tutorial de serviço de nuvem hello e demonstra como toouse Olá módulo Express."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="0627f-103">Criar um aplicativo web do Node.js usando o Express em um Serviço de Nuvem do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0627f-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="0627f-104">Node. js inclui um conjunto mínimo de funcionalidade em tempo de execução do hello core.</span><span class="sxs-lookup"><span data-stu-id="0627f-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="0627f-105">Os desenvolvedores geralmente usam 3ª parte módulos tooprovide funcionalidade adicional ao desenvolver um aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="0627f-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="0627f-106">Neste tutorial, você criará um novo aplicativo usando Olá [Express] [ Express] módulo, que fornece uma estrutura MVC para criação de aplicativos web Node. js.</span><span class="sxs-lookup"><span data-stu-id="0627f-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="0627f-107">É uma captura de tela do aplicativo hello concluída abaixo:</span><span class="sxs-lookup"><span data-stu-id="0627f-107">A screenshot of hello completed application is below:</span></span>

![Um navegador da web exibindo tooExpress boas-vindas no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="0627f-109">Criar um projeto de Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="0627f-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="0627f-110">Executar o seguinte Olá etapas toocreate um novo projeto de serviço de nuvem chamado 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="0627f-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="0627f-111">De saudação **Menu Iniciar** ou **tela inicial**, procure **do Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0627f-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="0627f-112">Por fim, clique com botão direito em **Windows PowerShell** e selecione **Executar Como Administrador**.</span><span class="sxs-lookup"><span data-stu-id="0627f-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ícone PowerShell do Azure](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="0627f-114">Altere os diretórios toohello **c:\\nó** diretório e, em seguida, digite Olá comandos toocreate uma nova solução chamada a seguir **expressapp** e uma função web chamada **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="0627f-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="0627f-115">Por padrão, o **Add-AzureNodeWebRole** usa uma versão mais antiga do Node.js.</span><span class="sxs-lookup"><span data-stu-id="0627f-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="0627f-116">Olá **AzureServiceProjectRole conjunto** instrução acima instrui v0.10.21 toouse do Azure do nó.</span><span class="sxs-lookup"><span data-stu-id="0627f-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="0627f-117">Observação Olá parâmetros diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0627f-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="0627f-118">Você pode verificar a versão correta de saudação do Node. js foi selecionada verificando Olá **mecanismos** propriedade **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="0627f-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="0627f-119">Instalar o Express</span><span class="sxs-lookup"><span data-stu-id="0627f-119">Install Express</span></span>
1. <span data-ttu-id="0627f-120">Instale o gerador de Express Olá emitindo o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="0627f-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="0627f-121">saída de saudação do comando de npm Olá deve ter aparência semelhante resultado toohello abaixo.</span><span class="sxs-lookup"><span data-stu-id="0627f-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Exibindo saída de saudação do Windows PowerShell de npm Olá instalar comando express.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="0627f-123">Altere os diretórios toohello **WebRole1** directory e uso Olá comando express toogenerate um novo aplicativo:</span><span class="sxs-lookup"><span data-stu-id="0627f-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="0627f-124">Você será solicitado toooverwrite seu aplicativo anterior.</span><span class="sxs-lookup"><span data-stu-id="0627f-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="0627f-125">Digite **y** ou **Sim** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0627f-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="0627f-126">Express irá gerar arquivo de app.js hello e uma estrutura de pasta para criar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0627f-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![saída de saudação do comando express Olá](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="0627f-128">tooinstall dependências adicionais definidas no arquivo de Package. JSON hello, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0627f-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![comando de instalação de saída de saudação do npm Olá](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="0627f-130">Olá toocopy do comando de uso a seguir de saudação **bin/www** arquivo muito**server.js**.</span><span class="sxs-lookup"><span data-stu-id="0627f-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="0627f-131">Isso é para que o serviço de nuvem Olá pode encontrar o ponto de entrada hello para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0627f-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="0627f-132">Depois que esse comando for concluído, você deve ter uma **server.js** arquivo no diretório Olá WebRole1.</span><span class="sxs-lookup"><span data-stu-id="0627f-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="0627f-133">Modificar Olá **server.js** tooremove uma saudação '.' caracteres de saudação linha a seguir.</span><span class="sxs-lookup"><span data-stu-id="0627f-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="0627f-134">Depois de fazer essa modificação, linha hello deve aparecer da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="0627f-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="0627f-135">Essa alteração é necessária, pois mudamos arquivo hello (anteriormente conhecida como **bin/www**,) toohello mesmo diretório do arquivo de aplicativo hello sendo solicitado.</span><span class="sxs-lookup"><span data-stu-id="0627f-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="0627f-136">Depois de fazer essa alteração, salve Olá **server.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="0627f-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="0627f-137">Use Olá após o aplicativo do comando toorun hello em Olá emulador do Azure:</span><span class="sxs-lookup"><span data-stu-id="0627f-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Uma página da web que contém tooexpress boas-vindas.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="0627f-139">Modificando Olá exibição</span><span class="sxs-lookup"><span data-stu-id="0627f-139">Modifying hello View</span></span>
<span data-ttu-id="0627f-140">Modificar exibição toodisplay Olá mensagem de saudação do "Bem-vindo tooExpress no Azure".</span><span class="sxs-lookup"><span data-stu-id="0627f-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="0627f-141">Digite hello seguir comando tooopen Olá Jade arquivo:</span><span class="sxs-lookup"><span data-stu-id="0627f-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Olá conteúdo do hello Jade arquivo.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="0627f-143">Jade é o mecanismo de exibição padrão de Olá usado por aplicativos Express.</span><span class="sxs-lookup"><span data-stu-id="0627f-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="0627f-144">Para obter mais informações sobre o mecanismo de exibição Jade hello, consulte [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="0627f-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="0627f-145">Modificar a última linha de saudação do texto acrescentando **no Azure**.</span><span class="sxs-lookup"><span data-stu-id="0627f-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![arquivo de Jade Hello, última linha de saudação lê: p bem-vindo muito\#{título} no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="0627f-147">Salve o arquivo hello e sair do bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="0627f-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="0627f-148">Atualize o navegador para ver as alterações.</span><span class="sxs-lookup"><span data-stu-id="0627f-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Uma janela do navegador, a página de saudação contém tooExpress boas-vindas no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="0627f-150">Após a aplicação de saudação do teste, use Olá **AzureEmulator Stop** emulador do cmdlet toostop hello.</span><span class="sxs-lookup"><span data-stu-id="0627f-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="0627f-151">Publicação tooAzure de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="0627f-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="0627f-152">Na janela do PowerShell do Azure hello, use Olá **AzureServiceProject publicar** serviço de nuvem do cmdlet toodeploy Olá aplicativo tooa</span><span class="sxs-lookup"><span data-stu-id="0627f-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="0627f-153">Após a conclusão da operação de implantação hello, seu navegador será aberto e exibir a página da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="0627f-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![Um navegador da web exibindo Olá Express página.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="0627f-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0627f-156">Next steps</span></span>
<span data-ttu-id="0627f-157">Para obter mais informações, consulte Olá [Node. js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="0627f-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


