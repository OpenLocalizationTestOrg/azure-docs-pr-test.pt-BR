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
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Especificar uma versão do Node.js em um aplicativo do Azure
Ao hospedar um aplicativo Node. js, talvez você queira tooensure que o aplicativo usa uma versão específica do Node. js. Há várias tooaccomplish de maneiras isso para aplicativos hospedados no Azure.

## <a name="default-versions"></a>Versões padrão
versões do Node. js Olá fornecidas pelo Azure são constantemente atualizadas. A menos que especificado o contrário, Olá versão padrão que é especificado no hello `WEBSITE_NODE_DEFAULT_VERSION` variável de ambiente será usada. toooverride esse valor padrão, siga as etapas de saudação nas seguintes seções deste artigo

> [!NOTE]
> Se você estiver hospedando seu aplicativo em um serviço de nuvem do Azure (função web ou de trabalho), e é Olá primeira vez que você implantou o aplicativo hello, Azure tentará toouse Olá a mesma versão do Node. js que você instalou no seu ambiente de desenvolvimento, se ele corresponde a uma das versões de padrão de saudação disponíveis no Azure.
>
>

## <a name="versioning-with-packagejson"></a>Controle de versão com o package.json
Você pode especificar a versão de saudação do Node. js toobe usado adicionando Olá tooyour a seguir **Package. JSON** arquivo:

    "engines":{"node":version}

Onde *versão* é toouse de número de versão específica de saudação. Você pode especificar condições mais complexas de versão, como:

    "engines":{"node": "0.6.22 || 0.8.x"}

Como 0.6.22 não é uma das versões de saudação disponíveis no ambiente de hospedagem de Olá, hello versão mais recente do hello 0,8 série disponível será usado em vez disso, - 0.8.4.

## <a name="versioning-websites-with-app-settings"></a>Sites de controle de versão com configurações de aplicativo
Se você estiver hospedando o aplicativo hello em um site, você pode definir a variável de ambiente Olá **WEBSITE_NODE_DEFAULT_VERSION** versão desejada de toohello.

## <a name="versioning-cloud-services-with-powershell"></a>Controle de versão dos Serviços de Nuvem com o PowerShell
Se você estiver hospedando o aplicativo hello em um serviço de nuvem e implantar o aplicativo hello usando o PowerShell do Azure, você pode substituir a versão de Node. js padrão Olá usando Olá **AzureServiceProjectRole conjunto** cmdlet do PowerShell. Por exemplo:

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

Observação parâmetros Olá Olá acima instrução diferenciam maiusculas de minúsculas.  Você pode verificar a versão correta de saudação do Node. js foi selecionada verificando Olá **mecanismos** propriedade na sua função **Package. JSON**.

Você também pode usar o hello **Get-AzureServiceProjectRoleRuntime** tooretrieve uma lista das versões do Node. js disponíveis para aplicativos hospedados como um serviço de nuvem.  Sempre verificar a versão de saudação do Node. js depende de seu projeto está na lista.

## <a name="using-a-custom-version-with-azure-websites"></a>Usando uma versão personalizada com Sites do Azure
Enquanto o Azure fornece várias versões padrão do Node. js, talvez você queira toouse uma versão que não é fornecida por padrão. Se seu aplicativo for hospedado como um site do Azure, você pode fazer isso usando Olá **iisnode.yml** arquivo. Olá etapas a seguir conduzem pelo processo de saudação do uso de uma versão personalizada do Node. js com um site do Azure:

1. Criar um novo diretório e, em seguida, criar um **server.js** arquivo no diretório de saudação. Olá **server.js** arquivo deve conter o seguinte hello:

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    Versão do Node. js hello está sendo usado quando você procurar o site Olá será exibido.
2. Crie um novo site e um nome de saudação de observação do site de saudação. Por exemplo, o seguinte Olá usa Olá [as ferramentas de linha de comando do Azure] toocreate um novo site do Azure denominado **meuwebsite**e, em seguida, habilitar um repositório Git para o site de saudação.

        azure site create mywebsite --git
3. Crie um novo diretório chamado **bin** como um filho do diretório de saudação contendo Olá **server.js** arquivo.
4. Baixar a versão específica de saudação do **node.exe** (versão do Windows hello) que você deseja toouse com seu aplicativo. Por exemplo, Olá a seguir usa **curl** versão toodownload 0.8.1:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Salvar Olá **node.exe** arquivo hello **bin** pasta criada anteriormente.
5. Criar um **iisnode.yml** arquivo hello mesmo diretório como Olá **server.js** de arquivo e depois adicione Olá toohello conteúdo a seguir **iisnode.yml** arquivo:

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    Esse caminho é onde hello **node.exe** arquivo dentro de seu projeto será localizado depois de publicar seu site do Azure de toohello do aplicativo.
6. Publique o aplicativo. Por exemplo, desde que criei um novo site com o parâmetro – git Olá anteriormente, hello comandos a seguir serão adicionar Olá aplicativo arquivos toomy repositório Git local e, em seguida, enviá-las toohello repositório de site:

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Após ter publicado o aplicativo hello, abra o site de saudação em um navegador. Você deve ver uma mensagem dizendo "Olá da versão do nó que executa o Azure: v0.8.1".

## <a name="next-steps"></a>Próximas etapas
Agora que você sabe como toospecify versão de saudação do Node. js usada pelo seu aplicativo, saber como muito[funcionam com módulos], [criar e implantar um Site Node.js](app-service-web/app-service-web-get-started-nodejs.md), e [como toouse hello Azure Ferramentas de linha de comando para Mac e Linux].

Para obter mais informações, consulte Olá [Node. js Developer Center](https://azure.microsoft.com/develop/nodejs/).

[como toouse hello Azure Ferramentas de linha de comando para Mac e Linux]:cli-install-nodejs.md
[as ferramentas de linha de comando do Azure]:cli-install-nodejs.md
[funcionam com módulos]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
