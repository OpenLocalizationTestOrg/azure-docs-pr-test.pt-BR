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
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>Criar um aplicativo web do Node.js usando o Express em um Serviço de Nuvem do Microsoft Azure
Node. js inclui um conjunto mínimo de funcionalidade em tempo de execução do hello core.
Os desenvolvedores geralmente usam 3ª parte módulos tooprovide funcionalidade adicional ao desenvolver um aplicativo Node. js. Neste tutorial, você criará um novo aplicativo usando Olá [Express] [ Express] módulo, que fornece uma estrutura MVC para criação de aplicativos web Node. js.

É uma captura de tela do aplicativo hello concluída abaixo:

![Um navegador da web exibindo tooExpress boas-vindas no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>Criar um projeto de Serviço de Nuvem
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

Executar o seguinte Olá etapas toocreate um novo projeto de serviço de nuvem chamado 'expressapp':

1. De saudação **Menu Iniciar** ou **tela inicial**, procure **do Windows PowerShell**. Por fim, clique com botão direito em **Windows PowerShell** e selecione **Executar Como Administrador**.
   
    ![Ícone PowerShell do Azure](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. Altere os diretórios toohello **c:\\nó** diretório e, em seguida, digite Olá comandos toocreate uma nova solução chamada a seguir **expressapp** e uma função web chamada **WebRole1** :
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > Por padrão, o **Add-AzureNodeWebRole** usa uma versão mais antiga do Node.js. Olá **AzureServiceProjectRole conjunto** instrução acima instrui v0.10.21 toouse do Azure do nó.  Observação Olá parâmetros diferenciam maiusculas de minúsculas.  Você pode verificar a versão correta de saudação do Node. js foi selecionada verificando Olá **mecanismos** propriedade **WebRole1\package.json**.
    > 
    > 

## <a name="install-express"></a>Instalar o Express
1. Instale o gerador de Express Olá emitindo o comando a seguir de saudação:
   
        PS C:\node\expressapp> npm install express-generator -g
   
    saída de saudação do comando de npm Olá deve ter aparência semelhante resultado toohello abaixo. 
   
    ![Exibindo saída de saudação do Windows PowerShell de npm Olá instalar comando express.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. Altere os diretórios toohello **WebRole1** directory e uso Olá comando express toogenerate um novo aplicativo:
   
        PS C:\node\expressapp\WebRole1> express
   
    Você será solicitado toooverwrite seu aplicativo anterior. Digite **y** ou **Sim** toocontinue. Express irá gerar arquivo de app.js hello e uma estrutura de pasta para criar seu aplicativo.
   
    ![saída de saudação do comando express Olá](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. tooinstall dependências adicionais definidas no arquivo de Package. JSON hello, digite Olá comando a seguir:
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![comando de instalação de saída de saudação do npm Olá](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. Olá toocopy do comando de uso a seguir de saudação **bin/www** arquivo muito**server.js**. Isso é para que o serviço de nuvem Olá pode encontrar o ponto de entrada hello para este aplicativo.
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   Depois que esse comando for concluído, você deve ter uma **server.js** arquivo no diretório Olá WebRole1.
5. Modificar Olá **server.js** tooremove uma saudação '.' caracteres de saudação linha a seguir.
   
       var app = require('../app');
   
   Depois de fazer essa modificação, linha hello deve aparecer da seguinte maneira.
   
       var app = require('./app');
   
   Essa alteração é necessária, pois mudamos arquivo hello (anteriormente conhecida como **bin/www**,) toohello mesmo diretório do arquivo de aplicativo hello sendo solicitado. Depois de fazer essa alteração, salve Olá **server.js** arquivo.
6. Use Olá após o aplicativo do comando toorun hello em Olá emulador do Azure:
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Uma página da web que contém tooexpress boas-vindas.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>Modificando Olá exibição
Modificar exibição toodisplay Olá mensagem de saudação do "Bem-vindo tooExpress no Azure".

1. Digite hello seguir comando tooopen Olá Jade arquivo:
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Olá conteúdo do hello Jade arquivo.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade é o mecanismo de exibição padrão de Olá usado por aplicativos Express. Para obter mais informações sobre o mecanismo de exibição Jade hello, consulte [http://jade-lang.com][http://jade-lang.com].
2. Modificar a última linha de saudação do texto acrescentando **no Azure**.
   
   ![arquivo de Jade Hello, última linha de saudação lê: p bem-vindo muito\#{título} no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. Salve o arquivo hello e sair do bloco de notas.
4. Atualize o navegador para ver as alterações.
   
   ![Uma janela do navegador, a página de saudação contém tooExpress boas-vindas no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

Após a aplicação de saudação do teste, use Olá **AzureEmulator Stop** emulador do cmdlet toostop hello.

## <a name="publishing-hello-application-tooazure"></a>Publicação tooAzure de aplicativo hello
Na janela do PowerShell do Azure hello, use Olá **AzureServiceProject publicar** serviço de nuvem do cmdlet toodeploy Olá aplicativo tooa

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

Após a conclusão da operação de implantação hello, seu navegador será aberto e exibir a página da web de saudação.

![Um navegador da web exibindo Olá Express página. URL de saudação indica que agora está hospedado no Azure.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Node. js Developer Center](/develop/nodejs/).

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


