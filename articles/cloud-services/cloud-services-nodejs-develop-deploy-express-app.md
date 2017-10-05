---
title: Aplicativo Web com Express (Node.js) | Microsoft Docs
description: "Um tutorial que complementa o tutorial de serviço de nuvem e demonstra como usar o módulo Express."
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
ms.openlocfilehash: 54b715695e24786ec4e8dfcabefc648d76179c8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="bb6ce-103">Criar um aplicativo web do Node.js usando o Express em um Serviço de Nuvem do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bb6ce-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="bb6ce-104">O Node.js inclui um conjunto mínimo de funcionalidades em tempo de execução básico.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="bb6ce-105">Os desenvolvedores normalmente usam módulos de terceiros para fornecer funcionalidade adicional ao desenvolver um aplicativo do Node.js.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="bb6ce-106">Neste tutorial, você vai criar um novo aplicativo usando o módulo [Express][Express], que fornece uma estrutura MVC para criar aplicativos web do Node.js.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="bb6ce-107">Abaixo, uma captura de tela do aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="bb6ce-107">A screenshot of the completed application is below:</span></span>

![Um navegador da web exibindo Bem-vindo ao Express no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="bb6ce-109">Criar um projeto de Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="bb6ce-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="bb6ce-110">Execute as seguintes etapas para criar um novo projeto de serviço de nuvem chamado 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="bb6ce-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="bb6ce-111">Do **Menu Iniciar** ou na **Tela Iniciar**, procure **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="bb6ce-112">Por fim, clique com botão direito em **Windows PowerShell** e selecione **Executar Como Administrador**.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Ícone PowerShell do Azure](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="bb6ce-114">Altere os diretórios para o diretório **c:\\node** e digite os seguintes comandos para criar uma nova solução denominada **expressapp** e uma função web denominada **WebRole1**:</span><span class="sxs-lookup"><span data-stu-id="bb6ce-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="bb6ce-115">Por padrão, o **Add-AzureNodeWebRole** usa uma versão mais antiga do Node.js.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="bb6ce-116">A instrução **Set-AzureServiceProjectRole** acima instrui o Azure usar a versão v0.10.21 do Node.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="bb6ce-117">Observe que os parâmetros diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="bb6ce-118">Você pode verificar se a versão correta do Node.js foi selecionada verificando a propriedade **engines** em **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="bb6ce-119">Instalar o Express</span><span class="sxs-lookup"><span data-stu-id="bb6ce-119">Install Express</span></span>
1. <span data-ttu-id="bb6ce-120">Instale o gerador Express emitindo o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb6ce-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="bb6ce-121">A saída do comando npm deve ser semelhante ao resultado abaixo.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![Windows PowerShell exibindo a saída do comando npm install express.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="bb6ce-123">Altere os diretórios para o diretório **WebRole1** e use o comando express para gerar um novo aplicativo:</span><span class="sxs-lookup"><span data-stu-id="bb6ce-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="bb6ce-124">Você será solicitado a substituir o aplicativo anterior.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="bb6ce-125">Digite **s** ou **sim** para continuar.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="bb6ce-126">O Express gerará o arquivo app.js e uma estrutura de pastas para criar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![A saída do comando express](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="bb6ce-128">Para instalar dependências adicionais definidas no arquivo package.json, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bb6ce-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![A saída do comando npm install](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="bb6ce-130">Use o seguinte comando para copiar o arquivo **bin/www** no **server.js**.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="bb6ce-131">Isso é para que o serviço de nuvem possa encontrar o ponto de entrada para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="bb6ce-132">Após este comando tiver concluído, você deve ter um arquivo **server.js** no diretório WebRole1.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="bb6ce-133">Modifique o **server.js** para remover um dos caracteres '.' da seguinte linha.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="bb6ce-134">Após fazer esta modificação, a linha deve aparecer da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="bb6ce-135">Esta alteração é requerida porque movemos o arquivo (anteriormente **bin/www**,) ao mesmo diretório conforme o arquivo do aplicativo seja requerido.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="bb6ce-136">Após fazer de fazer essa alteração, salve o arquivo **server.js** .</span><span class="sxs-lookup"><span data-stu-id="bb6ce-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="bb6ce-137">Use o seguinte comando para executar o aplicativo no emulador do Azure:</span><span class="sxs-lookup"><span data-stu-id="bb6ce-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Uma página da web que contém as boas-vindas ao express.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="bb6ce-139">Modificando a exibição</span><span class="sxs-lookup"><span data-stu-id="bb6ce-139">Modifying the View</span></span>
<span data-ttu-id="bb6ce-140">Agora modifique a exibição para exibir a mensagem “Bem-vindo ao Express no Azure”.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="bb6ce-141">Digite o comando a seguir para abrir o arquivo index.jade:</span><span class="sxs-lookup"><span data-stu-id="bb6ce-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![O conteúdo do arquivo index.jade.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="bb6ce-143">Jade é o mecanismo de exibição padrão usado por aplicativos do Express.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="bb6ce-144">Para obter mais informações sobre o mecanismo de exibição Jade, confira [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="bb6ce-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="bb6ce-145">Modifique a última linha de texto acrescentando **no Azure**.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![No arquivo index.jade, a última linha diz: p Bem-vindo ao \#{título} no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="bb6ce-147">Salve o arquivo e saia do Bloco de Notas.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="bb6ce-148">Atualize o navegador para ver as alterações.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Uma janela do navegador, a página contém Bem-vindo ao Express no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="bb6ce-150">Depois de testar o aplicativo, use o cmdlet **Stop-AzureEmulator** para parar o emulador.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="bb6ce-151">Publicar o Aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="bb6ce-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="bb6ce-152">Na janela PowerShell do Azure, use o cmdlet **Publish-AzureServiceProject** para implantar o aplicativo em um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="bb6ce-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="bb6ce-153">Quando a operação de implantação estiver concluída, o navegador será aberto e exibirá a página da web.</span><span class="sxs-lookup"><span data-stu-id="bb6ce-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![Um navegador da web exibindo a página do Express.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="bb6ce-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb6ce-156">Next steps</span></span>
<span data-ttu-id="bb6ce-157">Para saber mais, confira o [Centro de desenvolvedores do Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="bb6ce-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


