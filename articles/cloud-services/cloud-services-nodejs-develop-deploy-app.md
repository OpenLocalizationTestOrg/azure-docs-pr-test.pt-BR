---
title: "Guia de Introdução ao aaaNode.js | Microsoft Docs"
description: "Saiba como toocreate Node.js um simples aplicativo web e implantá-lo tooan serviço de nuvem do Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>Criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure

Este tutorial mostra como toocreate Node.js um simples aplicativo em execução em um serviço de nuvem do Azure. Serviços de nuvem são blocos de construção de saudação de aplicativos de nuvem escalonáveis no Azure. Eles permitem a separação de saudação e gerenciamento independente e expansão dos componentes front-end e back-end do seu aplicativo.  Os serviços de nuvem fornecem uma máquina virtual exclusiva robusta para hospedar cada função confiável.

Para obter mais informações sobre serviços de nuvem e como eles se comparam tooAzure sites e máquinas virtuais, consulte [comparação de sites do Azure, serviços de nuvem e máquinas virtuais].

> [!TIP]
> Procurando toobuild um site simples? Se o seu cenário envolve apenas um site de front-end simples, considere [usar um aplicativo Web leve]. É possível atualizar facilmente tooa serviço de nuvem que seu aplicativo web cresce e suas necessidades mudam.

Seguindo este tutorial, você irá criar um aplicativo da Web simples hospedado dentro de uma função Web. Você usará tootest de emulador de computação Olá seu aplicativo localmente e implantá-lo usando ferramentas de linha de comando do PowerShell.

aplicativo Hello é um aplicativo simples "hello world":

![Um navegador da web exibindo a página de web do Olá Olá, mundo][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>Pré-requisitos
> [!NOTE]
> Este tutorial usa o PowerShell do Azure, que requer o Windows.

* Instalar e configurar o [Powershell do Azure].
* Baixe e instale Olá [SDK do Azure para .NET 2.7]. Olá instalar o programa de instalação, selecione:
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Criar um projeto de Serviço de Nuvem do Azure
Execute Olá tarefas toocreate um novo projeto de serviço de nuvem do Azure, juntamente com a estrutura básica do Node. js a seguir:

1. Executar **do Windows PowerShell** como administrador; da saudação **Menu Iniciar** ou **tela inicial**, procure **do Windows PowerShell**.
2. [Conectar o PowerShell] tooyour assinatura.
3. Digite hello projeto saudação do PowerShell cmdlet toocreate toocreate a seguir:

        New-AzureServiceProject helloworld

    ![resultado de saudação do comando de helloworld Olá New-AzureService][hello result of hello New-AzureService helloworld command]

    Olá **AzureServiceProject novo** cmdlet gera uma estrutura básica para publicar um aplicativo de Node. js tooa serviço de nuvem. Ele contém arquivos de configuração necessários para a publicação tooAzure. Olá cmdlet também altera o diretório de serviço Olá toohello de diretório de trabalho.

    Olá cria Olá seguintes arquivos:

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** e **ServiceDefinition.csdef**: são arquivos específicos do Azure necessários para publicar seu aplicativo. Para saber mais, consulte [Visão geral da criação de um serviço hospedado para o Azure].
   * **Deploymentsettings**: armazena as configurações locais que são usadas por Olá cmdlets de implantação do Azure PowerShell.
4. Digite hello comando tooadd uma nova função web a seguir:

       Add-AzureNodeWebRole

   ![saída de saudação do hello comando Add-AzureNodeWebRole][hello output of hello Add-AzureNodeWebRole command]

   Olá **Add-AzureNodeWebRole** cmdlet cria um aplicativo básico do Node. js. Ele também modifica Olá **. csfg** e **. csdef** arquivos tooadd entradas de configuração para a nova função de saudação.

   > [!NOTE]
   > Se você não especificar um nome de função, um nome padrão será usado. Você pode fornecer um nome como primeiro parâmetro de cmdlet hello:`Add-AzureNodeWebRole MyRole`

Olá Node. js aplicativo é definido no arquivo hello **server.js**, localizado no diretório Olá para função de web hello (**WebRole1** por padrão). Aqui está o código de saudação:

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Esse código é essencialmente Olá mesmo hello "Hello World" de exemplo no hello [nodejs.org] site, exceto que ele usa o número da porta Olá atribuído pelo ambiente de nuvem hello.

## <a name="deploy-hello-application-tooazure"></a>Implantar Olá aplicativo tooAzure

> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Azure. Você pode [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ou [se inscrever para fazer uma conta gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-hello-azure-publishing-settings"></a>Baixar hello Azure configurações de publicação
toodeploy tooAzure seu aplicativo, você deve primeiro baixar Olá publicar configurações para sua assinatura do Azure.

1. Execute hello Azure PowerShell cmdlet a seguir:

       Get-AzurePublishSettingsFile

   Isso usará seu navegador toonavigate toohello página de download de configurações de publicação. Você pode ser solicitado toolog com um Account da Microsoft. Nesse caso, use conta Olá associada à sua assinatura do Azure.

   Salve o local do arquivo hello baixado perfil tooa você pode acessar facilmente.
2. Execute o seguinte cmdlet tooimport Olá baixado do perfil de publicação:

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > Depois de importar Olá configurações de publicação, considere excluir Olá baixou o arquivo. publishsettings, porque ele contém informações que podem permitir que alguém tooaccess sua conta.

### <a name="publish-hello-application"></a>Publicar o aplicativo hello
toopublish, execute Olá comandos a seguir:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** especifica nome Olá para implantação de saudação. Isso deve ser um nome exclusivo, caso contrário, o processo de publicação Olá falhará. Olá **Get-Date** comando move em uma cadeia de caracteres de data/hora deve tornar o nome de saudação exclusivo.
* **-Local** Especifica Olá datacenter que será hospedado no aplicativo hello. toosee uma lista de centros de dados disponíveis, use Olá **AzureLocation Get** cmdlet.
* **-Inicie** abre uma janela do navegador e navega toohello hospedado serviço após a implantação.

Após a publicação será bem-sucedida, você verá uma resposta semelhante toohello a seguir:

![saída de saudação do hello comando Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> Ele pode levar vários minutos para toodeploy de aplicativo hello e ficam disponível quando publicado pela primeira vez.

Depois de saudação implantação for concluída, uma janela do navegador será aberto e navegue toohello serviço de nuvem.

![Uma janela do navegador exibindo Olá Olá mundo página; Olá URL indica a página Olá é hospedada no Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

Seu aplicativo está em execução no Azure.

Olá **AzureServiceProject publicar** cmdlet executa Olá etapas a seguir:

1. Cria um pacote toodeploy. pacote de saudação contém todos os arquivos de saudação na pasta de seu aplicativo.
2. Cria uma nova **conta de armazenamento** se não existir. Olá conta de armazenamento do Azure é o pacote de aplicativo hello toostore usado durante a implantação. Você pode excluir com segurança conta de armazenamento Olá após a conclusão da implantação.
3. Cria um novo **serviço de nuvem** se não existir. Um **serviço de nuvem** é Olá contêiner no qual o aplicativo está hospedado quando ele é implantado tooAzure. Para saber mais, consulte [Visão geral da criação de um serviço hospedado para o Azure].
4. Publica Olá tooAzure de pacote de implantação.

## <a name="stopping-and-deleting-your-application"></a>Parando e excluindo seu aplicativo
Depois de implantar seu aplicativo, convém toodisable isso, você pode evitar custos extras. O Azure cobra as instâncias de função web por hora de acordo com o tempo consumido do servidor. Hora do servidor é consumida quando seu aplicativo é implantado, mesmo se as instâncias de saudação não estão em execução e estão em estado de parado de saudação.

1. Na janela do Windows PowerShell hello, interrompa a implantação do serviço Olá criada na seção anterior Olá com hello cmdlet a seguir:

       Stop-AzureService

   Parar serviço Olá pode levar vários minutos. Quando a saudação serviço for interrompido, você recebe uma mensagem indicando que ele foi interrompido.

   ![status de saudação do comando Olá Stop-AzureService][hello status of hello Stop-AzureService command]
2. serviço de saudação toodelete, chamada hello cmdlet a seguir:

       Remove-AzureService

   Quando solicitado, insira **Y** toodelete serviço de saudação.

   Excluindo serviço Olá pode levar vários minutos. Após a exclusão de serviço Olá você receberá uma mensagem indicando que o serviço de saudação foi excluído.

   ![status de saudação do comando Olá Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > Excluindo serviço Olá não excluir conta de armazenamento de saudação que foi criada quando o serviço de saudação foi inicialmente publicado e você continuará toobe cobrado pelo armazenamento usado. Se nada mais é usar o armazenamento de saudação, talvez você queira toodelete-lo.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Node. js Developer Center].

<!-- URL List -->

[comparação de sites do Azure, serviços de nuvem e máquinas virtuais]: ../app-service-web/choose-web-site-cloud-service-vm.md
[usar um aplicativo Web leve]: ../app-service-web/app-service-web-get-started-nodejs.md
[Powershell do Azure]: /powershell/azureps-cmdlets-docs
[SDK do Azure para .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Conectar o PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Visão geral da criação de um serviço hospedado para o Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node. js Developer Center]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
