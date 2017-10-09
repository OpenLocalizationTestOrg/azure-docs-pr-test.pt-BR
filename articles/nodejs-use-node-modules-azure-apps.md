---
title: "aaaWorking com módulos de Node. js"
description: "Saiba como toowork com módulos Node.js ao usar o serviço de aplicativo do Azure ou serviços de nuvem."
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
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Usando Módulos no Node.js com aplicativos do Microsoft Azure
Este documento fornece orientação sobre como usar módulos no Node.js com aplicativos hospedados no Microsoft Azure. Fornece orientação para garantir que seu aplicativo use uma versão específica do módulo, bem como para usar módulos nativos com o Microsoft Azure.

Se você já estiver familiarizado com o uso de módulos Node.js, **Package. JSON** e **shrinkwrap.json npm** arquivos, Olá informações a seguir fornece um resumo de como o que é discutido neste artigo:

* O Serviço de Aplicativo do Azure compreende arquivos **package.json** e **npm-shrinkwrap.json** e podem instalar módulos com base em entradas nestes arquivos.

* Serviços de nuvem do Azure espera que todos os toobe de módulos instalados no ambiente de desenvolvimento hello e hello **nó\_módulos** toobe directory incluído como parte do pacote de implantação de saudação. É possível tooenable suporte para a instalação de módulos usando **Package. JSON** ou **shrinkwrap.json npm** arquivos nos serviços de nuvem; no entanto, essa configuração requer a personalização do padrão de saudação scripts usados por projetos de serviço de nuvem. Para obter um exemplo de como tooconfigure nesse ambiente, consulte [inicialização Azure tarefa toorun npm instalar tooavoid Implantando módulos de nó](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> Máquinas virtuais do Azure não são abordados neste artigo, pois Olá experiência de implantação em uma VM depende do sistema de operacional Olá hospedado pelo Olá Máquina Virtual.
> 
> 

## <a name="nodejs-modules"></a>Módulos no Node.js
Os módulos são pacotes carregáveis do JavaScript que fornecem funcionalidade específica para seu aplicativo. Módulos são geralmente instalados usando Olá **npm** de linha de comando ferramenta, no entanto alguns módulos (por exemplo, o módulo http do hello) são fornecidos como parte do pacote hello core Node. js.

Quando os módulos são instalados, eles são armazenados no hello **nó\_módulos** diretório raiz de saudação da sua estrutura de diretório de aplicativo. Cada módulo dentro de saudação **nó\_módulos** directory mantém seu próprio **nó\_módulos** diretório que contém todos os módulos que ela depende e esse comportamento se repete para cada módulo todo caminho de saudação para baixo de cadeia de dependência de saudação. Esse ambiente permite que cada módulo instalado toohave seus próprios requisitos de versão para os módulos de saudação depende, no entanto, isso pode resultar em uma estrutura de diretório grande.

Implantando Olá **nó\_módulos** diretório como parte do seu aplicativo aumenta o tamanho de saudação da implantação de saudação quando comparado toousing um **Package. JSON** ou  **NPM shrinkwrap.json** arquivo; no entanto, ele garante que versões Olá dos módulos de saudação usadas na produção são Olá mesmo como módulos Olá usados no desenvolvimento.

### <a name="native-modules"></a>Módulos Nativos
Enquanto a maioria dos módulos são simples arquivos de texto JavaScript, outros são imagens binárias específicas de plataforma. Estes módulos são compilados no momento da instalação, geralmente usando o Python e o node-gyp. Como os serviços de nuvem do Azure dependem de saudação **nó\_módulos** pasta que está sendo implantada como parte do aplicativo hello, qualquer módulo nativo incluído como parte dos módulos Olá instalado deve funcionar em um serviço de nuvem, desde que ele foi instalado e compilado em um sistema de desenvolvimento do Windows.

O Serviço de Aplicativo do Azure não dá suporte a todos os módulos nativos e pode falhar ao compilar módulos com pré-requisitos específicos. Embora alguns módulos populares como o MongoDB tenham dependências nativas opcionais e funcionem bem sem elas, duas soluções alternativas foram comprovadamente bem-sucedidas com quase todos os módulos nativos disponíveis hoje:

* Executar **de instalação de npm** em um computador Windows que tenha os pré-requisitos de todos os Olá nativo do módulo instalados. Em seguida, implante Olá criado **nó\_módulos** pasta como parte da saudação tooAzure de aplicativo do serviço de aplicativo.

  * Antes de compilar, verifique se sua instalação local do Node. js tem correspondentes de arquitetura e versão hello está mais próximo possível toohello usado no Azure (valores atuais Olá podem ser verificados em tempo de execução das propriedades **process.arch**e **process.version**).

* Serviço de aplicativo do Azure pode ser bash personalizados tooexecute configurado ou scripts de shell durante a implantação, fornecendo Olá comandos personalizados de tooexecute oportunidade e configurar precisamente Olá maneira **de instalação de npm** está sendo executado. Para um vídeo mostrando como tooconfigure nesse ambiente, consulte [Scripts de implantação de site personalizado com Kudu].

### <a name="using-a-packagejson-file"></a>Usando um arquivo package.json
Olá **Package. JSON** arquivo é uma maneira toospecify Olá nível superior dependências seu aplicativo exige para que hello plataforma de hospedagem pode instalar dependências hello, em vez de exigir que você tooinclude Olá **nó \_pacotes** pasta como parte da implantação de saudação. Após a implantação de aplicativo hello, Olá **npm instalar** comando é usado tooparse Olá **Package. JSON** de arquivo e instalar todas as dependências de saudação listadas.

Durante o desenvolvimento, você pode usar o hello **– salvar**, **-dev salvar**, ou **– opcional a save** parâmetros durante a instalação de módulos tooadd uma entrada para o módulo de saudação tooyour **Package. JSON** arquivos automaticamente. Para obter mais informações, consulte [instalar-npm](https://docs.npmjs.com/cli/install).

Um problema potencial com hello **Package. JSON** arquivo é que ela especifica apenas versão Olá para dependências de nível superior. Cada módulo instalado pode ou não pode especificar a versão de saudação dos módulos Olá depende, e assim, é possível que você pode acabar com uma cadeia de dependência diferentes que Olá usado no desenvolvimento.

> [!NOTE]
> Ao implantar tooAzure do serviço de aplicativo, se seu <b>Package. JSON</b> arquivo faz referência a um módulo nativo, talvez você veja uma toohello semelhante erro exemplo a seguir ao publicar o aplicativo hello usando Git:
> 
> npm ERR! Instalar module-name@0.6.0: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp rebuild"' falhou com 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>Usando um arquivo npm-shrinkwrap.json
Olá **npm shrinkwrap.json** arquivo é uma tentativa de tooaddress Olá módulo controle de versão limitações Olá **Package. JSON** arquivo. Durante a saudação **Package. JSON** arquivo inclui somente versões para módulos de nível superior hello, hello **shrinkwrap.json npm** arquivo contém requisitos de versão de saudação para cadeia de dependência de módulo completo hello.

Quando seu aplicativo está pronto para produção, você pode bloquear os requisitos de versão e criar um **npm shrinkwrap.json** arquivo usando Olá **shrinkwrap npm** comando. Este comando usará versões Olá atualmente instaladas no hello **nó\_módulos** pasta e registrar essas versões toohello **shrinkwrap.json npm** arquivo. Depois que o aplicativo hello tenha sido implantado toohello ambiente de hospedagem, Olá **npm instalar** comando é usado tooparse Olá **shrinkwrap.json npm** de arquivo e instalar todas as dependências de saudação listadas. Para obter mais informações, consulte [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

> [!NOTE]
> Ao implantar tooAzure do serviço de aplicativo, se seu <b>shrinkwrap.json npm</b> arquivo faz referência a um módulo nativo, talvez você veja uma toohello semelhante erro exemplo a seguir ao publicar o aplicativo hello usando Git:
> 
> npm ERR! Instalar module-name@0.6.0: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp rebuild"' falhou com 1
> 
> 

## <a name="next-steps"></a>Próximas etapas
Agora que você sabe como toouse Node. js módulos com o Azure, saiba como muito[especificar Olá Node. js versão], [criar e implantar um aplicativo de web Node.js](app-service-web/app-service-web-get-started-nodejs.md), e [como toouse Olá de linha de comando do Azure Interface para Mac e Linux].

Para obter mais informações, consulte Olá [Node. js Developer Center](/nodejs/azure/).

[especificar Olá Node. js versão]: nodejs-specify-node-version-azure-apps.md
[como toouse Olá de linha de comando do Azure Interface para Mac e Linux]:cli-install-nodejs.md
[Scripts de implantação de site personalizado com Kudu]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
