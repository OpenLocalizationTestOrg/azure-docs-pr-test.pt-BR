---
title: "aaaHow toodebug um aplicativo da web Node. js no serviço de aplicativo do Azure"
description: "Saiba como toodebug um Node. js web app no serviço de aplicativo do Azure."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a>Como toodebug um Node. js web app no serviço de aplicativo do Azure
O Azure fornece tooassist diagnóstico interno com depuração Node. js aplicativos hospedados em [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicativos Web. Neste artigo, você aprenderá como log tooenable de stdout e stderr, exibir informações de erro no navegador hello e como toodownload e exibir arquivos de log.

O diagnóstico para aplicativos do Node.js hospedados no Azure é fornecido por [IISNode]. Embora este artigo aborda as configurações mais comuns de saudação para reunir informações de diagnóstico, ele não fornece uma referência completa para trabalhar com IISNode. Para obter mais informações sobre como trabalhar com IISNode, consulte Olá [IISNode Readme] no GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Habilitar o registro em log
Por padrão, um aplicativo Web do Serviço de Aplicativo captura somente informações de diagnóstico sobre implantações, como quando você implanta um aplicativo Web usando Git. Essas informações são úteis se você estiver tendo problemas durante a implantação, como uma falha durante a instalação de um módulo referenciado na **package.json**, ou se você estiver usando um script de implantação personalizada.

Olá tooenable log de fluxos stdout e stderr, você deve criar um **IISNode.yml** arquivo na raiz de saudação do seu aplicativo Node. js e adicione o seguinte hello:

    loggingEnabled: true

Isso habilita o log de saudação do stderr e stdout do seu aplicativo Node. js.

Olá **IISNode.yml** arquivo também pode ser usado toocontrol se erros amigáveis ou desenvolvedor são retornados toohello navegador quando ocorre uma falha. erros de desenvolvedor tooenable, adicionar Olá toohello linha a seguir **IISNode.yml** arquivo:

    devErrorsEnabled: true

Quando essa opção é habilitada, IISNode retornará Olá última 64K de informações enviadas toostderr em vez de um erro amigável, como "Ocorreu um erro interno do servidor".

> [!NOTE]
> Enquanto devErrorsEnabled é útil para diagnosticar problemas durante o desenvolvimento, habilitá-la em um ambiente de produção pode resultar em erros de desenvolvimento que está sendo enviados tooend usuários.
> 
> 

Se hello **IISNode.yml** arquivo ainda não existia no seu aplicativo, você deve reiniciar seu aplicativo web depois de publicar o aplicativo hello atualizado. Se você estiver simplesmente alterando as configurações em um arquivo **IISNode.yml** arquivo que tenha sido publicado anteriormente, não é necessário reiniciar.

> [!NOTE]
> Se seu aplicativo web foi criado usando as ferramentas de linha de comando do Azure hello ou Cmdlets do PowerShell do Azure, um padrão **IISNode.yml** arquivo será criado automaticamente.
> 
> 

aplicativo web do hello toorestart, aplicativo web de select Olá Olá [Portal do Azure](https://portal.azure.com)e, em seguida, clique em **reiniciar** botão:

![botão de reinicialização][restart-button]

Se Olá ferramentas de linha de comando do Azure estão instaladas em seu ambiente de desenvolvimento, você pode usar Olá comando toorestart Olá web aplicativo a seguir:

    azure site restart [sitename]

> [!NOTE]
> Enquanto loggingEnabled e devErrorsEnabled são opções de configuração de IISNode.yml hello mais comumente usado para capturar informações de diagnóstico, IISNode.yml pode ser usado tooconfigure uma variedade de opções para o seu ambiente de hospedagem. Para obter uma lista completa das opções de configuração de hello, consulte Olá [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) arquivo.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Acessando os logs
Logs de diagnóstico que podem ser acessados de três maneiras; Usando Olá protocolo FTP (File Transfer), baixar um arquivo Zip, ou como um dinâmica atualizado o fluxo de log da saudação (também conhecido como a parte final). Baixando o arquivo Zip Olá Olá dos arquivos de log ou exibindo o fluxo ao vivo Olá exigem Olá ferramentas de linha de comando do Azure. Elas podem ser instaladas usando Olá comando a seguir:

    npm install azure-cli -g

Uma vez instalado, ferramentas de saudação podem ser acessadas usando o comando Olá 'do azure'. Olá ferramentas de linha de comando deve ser configurado toouse sua assinatura do Azure. Para obter informações sobre como tooaccomplish essa tarefa, consulte Olá **como toodownload e importar configurações de publicação** seção Olá [como tooUse Olá ferramentas de linha de comando do Azure](../xplat-cli-connect.md) artigo.

### <a name="ftp"></a>FTP
informações de diagnóstico Olá tooaccess por meio de FTP, visite Olá [Portal do Azure](https://portal.azure.com), selecione seu aplicativo web e, em seguida, selecione Olá **painel**. Em Olá **links rápidos** seção, hello **LOGS de diagnóstico de FTP** e **LOGS de diagnóstico de FTPS** links fornecem acesso toohello logs usando o protocolo de saudação FTP.

> [!NOTE]
> Se você não tiver configurado anteriormente o nome de usuário e senha de FTP ou implantação, você pode fazer isso de saudação **Quickstart** página de gerenciamento selecionando **configurar credenciais de implantação**.
> 
> 

Hello FTP URL retornada no painel de saudação é de saudação **LogFiles** diretório, que irá conter Olá subdiretórios a seguir:

* [Método de implantação](web-sites-deploy.md) -se você usar um método de implantação, como o Git, um diretório de saudação mesmo nome será criado e conterá informações relacionadas toodeployments.
* nodejs - Stdout e stderr informações capturadas de todas as instâncias do seu aplicativo (quando loggingEnabled for true.)

### <a name="zip-archive"></a>Arquivo Zip
toodownload um arquivo Zip dos logs de diagnóstico hello, Olá uso a seguir de comando de ferramentas de linha de comando do hello Azure:

    azure site log download [sitename]

Isso baixará uma **diagnostics.zip** no diretório atual hello. Este arquivo contém Olá estrutura de diretórios a seguir:

* implantações - de um log de informações sobre a implantação do seu aplicativo
* arquivos de log
  
  * [Método de implantação](web-sites-deploy.md) -se você usar um método de implantação, como o Git, um diretório de saudação mesmo nome será criado e conterá informações relacionadas toodeployments.
  * nodejs - Stdout e stderr informações capturadas de todas as instâncias do seu aplicativo (quando loggingEnabled for true.)

### <a name="live-stream-tail"></a>Fluxo ao vivo (final)
tooview uma transmissão ao vivo de informações de log de diagnóstico, Olá uso a seguir de comando de ferramentas de linha de comando do hello Azure:

    azure site log tail [sitename]

Isso retorna um fluxo de eventos de log que são atualizadas à medida que ocorrem no servidor de saudação. Este fluxo irá retornar informações sobre a implantação, bem como informações de stdout e stderr (quando loggingEnabled for true.)

<a id="nextsteps"></a>

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como tooenable e acessar as informações de diagnóstico do Azure. Enquanto essas informações são úteis em Noções básicas sobre problemas ocorridos com seu aplicativo, ele pode apontar tooa problema com um módulo que você está usando ou versão saudação do Node. js usado pelo serviço de aplicativo Web de aplicativos é diferente de saudação usado na sua implantação ambiente.

Para obter informações no trabalho com módulos no Azure, consulte [usando o Node. js módulos com aplicativos do Azure](../nodejs-use-node-modules-azure-apps.md)

Para obter informações sobre como especificar uma versão do Node.js para seu aplicativo, consulte [Especificar uma versão do Node.js em um aplicativo do Azure].

Para obter mais informações, consulte também Olá [Node. js Developer Center](/develop/nodejs/).

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Especificar uma versão do Node.js em um aplicativo do Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

