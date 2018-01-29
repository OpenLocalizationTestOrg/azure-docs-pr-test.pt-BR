---
title: "Trabalhando com módulos de Node.js"
description: "Aprenda a trabalhar com os módulos de Node.js ao usar o Serviço de Aplicativo ou Serviços de Nuvem do Azure."
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 76679ea0ff2c1e88d1923488717a245351437165
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Usando Módulos no Node.js com aplicativos do Microsoft Azure
Este documento fornece orientação sobre como usar módulos no Node.js com aplicativos hospedados no Microsoft Azure. Fornece orientação para garantir que seu aplicativo use uma versão específica do módulo, bem como para usar módulos nativos com o Microsoft Azure.

Se já estiver acostumado a usar os módulos no Node.js e os arquivos **package.json** e **npm-shrinkwrap.json**, as informações a seguir apresentam um rápido resumo do que será discutido neste artigo:

* O Serviço de Aplicativo do Azure compreende arquivos **package.json** e **npm-shrinkwrap.json** e podem instalar módulos com base em entradas nestes arquivos.

* Os Serviços de Nuvem do Microsoft Azure esperam que todos os módulos sejam instalados no ambiente de desenvolvimento e que o diretório **node\_modules** seja incluído como parte do pacote de implantação. É possível habilitar o suporte para instalar módulos usando arquivos **package.json** ou **npm-shrinkwrap.json** nos Serviços de Nuvem; no entanto, essa configuração requer uma personalização dos scripts padrão usados por projetos do Serviço de Nuvem. Para um exemplo de como configurar esse ambiente, consulte [Tarefa de Inicialização do Azure para executar npm install e evitar a implantação de módulos de nó](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> As Máquinas Virtuais do Azure não são discutidas neste artigo, já que a experiência de implantação em uma VM depende do sistema operacional hospedado pela Máquina Virtual.
> 
> 

## <a name="nodejs-modules"></a>Módulos no Node.js
Os módulos são pacotes carregáveis do JavaScript que fornecem funcionalidade específica para seu aplicativo. Em geral, instalam-se módulos com a ferramenta de linha de comando **npm**. Porém, alguns módulos (como http) são fornecidos como parte do pacote central do Node.js.

Quando os módulos são instalados, são armazenados no diretório **node\_modules**, na raiz da estrutura do diretório de seu aplicativo. Cada módulo dentro do diretório **node\_modules** mantém seu próprio diretório **node\_modules**, que contém todos os módulos dos quais ele depende. Esse comportamento se repete para cada módulo em toda a cadeia de dependência. Esse ambiente permite que cada módulo instalado tenha seus próprios requisitos de versão para os módulos dos quais depende, porém, o resultado pode ser uma estrutura de diretório muito grande.

Implantar o diretório **node\_modules** como parte de seu aplicativo aumenta o tamanho da implantação em comparação ao uso de um arquivo **package.json** ou **npm-shrinkwrap.json**, mas assegura que a versão dos módulos usados na produção seja igual à dos módulos usados no desenvolvimento.

### <a name="native-modules"></a>Módulos Nativos
Enquanto a maioria dos módulos são simples arquivos de texto JavaScript, outros são imagens binárias específicas de plataforma. Estes módulos são compilados no momento da instalação, geralmente usando o Python e o node-gyp. Uma vez que os Serviços de Nuvem do Microsoft Azure contam com a pasta **node\_modules** sendo implantada como parte do aplicativo, qualquer módulo nativo incluído como parte dos módulos instalados deve funcionar em um serviço de nuvem, desde que tenha sido instalado e compilado em um sistema de desenvolvimento do Windows.

O Serviço de Aplicativo do Azure não dá suporte a todos os módulos nativos e pode falhar ao compilar módulos com pré-requisitos específicos. Embora alguns módulos populares como o MongoDB tenham dependências nativas opcionais e funcionem bem sem elas, duas soluções alternativas foram comprovadamente bem-sucedidas com quase todos os módulos nativos disponíveis hoje:

* Execute a **npm install** em uma máquina do Windows que tenha todos os pré-requisitos do módulo nativo. Em seguida, implante a pasta **node\_modules** criada como parte do aplicativo no Serviço de Aplicativo do Azure.

  * Antes de compilar, verifique se sua instalação local do Node.js tem arquitetura correspondente e se a versão é a mais próxima possível da usada no Azure (os valores atuais podem ser verificados no tempo de execução das propriedades **process.arch** e **process.version**).

* O Serviço de Aplicativo do Azure podem ser configurados para executar scripts bash ou de shell personalizados durante a implantação, oferecendo a você a oportunidade de executar comandos personalizados e configurar com precisão a maneira como o **npm install** é executado. Para obter um vídeo mostrando como configurar esse ambiente, consulte [Scripts de implantação de site personalizado com Kudu].

### <a name="using-a-packagejson-file"></a>Usando um arquivo package.json

O arquivo **package.json** é uma maneira de especificar as dependências de nível superior que seu aplicativo requer para que a plataforma de hospedagem possa instalar as dependências, em vez de exigir a inclusão da pasta **node\_modules** como parte da implantação. Após o aplicativo ser implantado, o comando **instalar npm** é usado para analisar o arquivo **package.json** e instalar todas as dependências listadas.

Ao instalar módulos durante o desenvolvimento, você pode usar os parâmetros **--save**, **--save-dev** ou **--save-optional** para adicionar, automaticamente, uma entrada para o módulo de seu arquivo **package.json**. Para obter mais informações, consulte [instalar-npm](https://docs.npmjs.com/cli/install).

Um problema potencial com o arquivo **package.json** é que este só especifica a versão para dependências de nível superior. Cada módulo instalado pode ou não especificar a versão dos módulos da qual depende e, desta forma, é possível que você acabe com uma cadeia de dependências diferente daquele usada no desenvolvimento.

> [!NOTE]
> Quando estiver implantando no Serviço de Aplicativo do Azure, se o seu arquivo <b>package.json</b> fizer referência a um módulo nativo, você poderá ver um erro semelhante ao exemplo a seguir ao publicar o aplicativo usando Git:
> 
> npm ERR! Instalar module-name@0.6.0: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp rebuild"' falhou com 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>Usando um arquivo npm-shrinkwrap.json
O arquivo **npm-shrinkwrap.json** é uma tentativa de resolver as limitações da versão do módulo do arquivo **package.json**. Enquanto o arquivo **package.json** inclui apenas versões para os módulos de nível superior, o arquivo **npm-shrinkwrap.json** contém os requisitos de versão para a cadeia de dependências de módulo completo.

Quando seu aplicativo estiver pronto para produção, você poderá bloquear os requisitos de versão e criar um arquivo **npm-shrinkwrap.json** usando o comando **npm shrinkwrap**. Esse comando usará as versões atualmente instaladas na pasta **node\_modules** e registrará essas versões no arquivo **npm-shrinkwrap.json**. Após o aplicativo ser implantado no ambiente de hospedagem, o comando **instalar npm** é usado para analisar o arquivo **npm-shrinkwrap.json** e instalar todas as dependências listadas. Para obter mais informações, consulte [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

> [!NOTE]
> Quando estiver implantando no Serviço de Aplicativo do Azure, se o seu arquivo <b>npm-shrinkwrap.json</b> fizer referência a um módulo nativo, você poderá ver um erro semelhante ao exemplo a seguir ao publicar o aplicativo usando Git:
> 
> npm ERR! Instalar module-name@0.6.0: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp rebuild"' falhou com 1
> 
> 

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu como usar os módulos no Node.js com o Azure, aprenda como [especificar a versão do Node.js], [compilar e implantar um aplicativo Web Node.js](app-service/app-service-web-get-started-nodejs.md) e [Como usar a Interface de Linha de Comando do Azure para Mac e Linux].

Para saber mais, confira o [Centro de desenvolvedores do Node.js](/nodejs/azure/).

[especificar a versão do Node.js]: nodejs-specify-node-version-azure-apps.md
[Como usar a Interface de Linha de Comando do Azure para Mac e Linux]:cli-install-nodejs.md
[Scripts de implantação de site personalizado com Kudu]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
