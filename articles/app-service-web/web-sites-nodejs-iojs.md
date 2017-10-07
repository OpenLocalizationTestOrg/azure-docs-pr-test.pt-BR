---
title: "aaaHow toouse io.js com aplicativos de Web do serviço de aplicativo do Azure"
description: "Saiba como toouse um aplicativo web no serviço de aplicativo do Azure com io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>Como io.js toouse com aplicativos de Web do serviço de aplicativo do Azure
bifurcação de nó popular Olá [io.js] recursos de projeto de Node.js do várias diferenças tooJoyent, incluindo um modelo de controle mais aberto, um ciclo de lançamento mais rápido e uma adoção mais rápida de novo e experimentais recursos de JavaScript.

Embora os Aplicativos Web do [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) tenham várias versões de Node.js pré-instaladas, também é possível usar um binário de Node.js fornecido pelo usuário. Este artigo descreve dois métodos habilitar uso de saudação do io.js em aplicativos de Web do serviço de aplicativo: Olá o uso de um script de implantação estendida, que configura automaticamente a versão mais recente de io.js disponíveis do Azure toouse hello, bem como carregamento manual de saudação de um binário io.js. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Usando um Script de implantação
Após a implantação de um aplicativo Node. js, aplicativos de Web do serviço de aplicativo executa uma série de comandos pequenos tooensure que Olá ambiente está configurado corretamente. Usando um script de implantação, esse processo pode ser personalizado tooinclude download de saudação e a configuração de io.js.

Olá [io.js Script de implantação](https://github.com/felixrieseberg/iojs-azure) está disponível no GitHub. io.js tooenable em seu aplicativo web, basta copiar **.deployment**, **Deploy** e **IISNode.yml** toohello pasta raiz do seu aplicativo e implante aplicativos tooWeb.  

primeiro arquivo de saudação, **.deployment**, instrui a aplicativos Web toorun **Deploy** após a implantação. Esse script é executado todas as etapas de saudação normal para um aplicativo Node. js, mas também baixa a versão mais recente de saudação do io.js. Por fim, **IISNode.yml** configura aplicativos Web toouse apenas Olá baixado io.js binário em vez de um binário Node. js pré-instalados.

> [!NOTE]
> Olá tooupdate usada io.js binário, apenas reimplante o aplicativo - script hello baixará uma nova versão do io.js que cada aplicativo de saudação única vez é implantado.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Usando a instalação manual
instalação manual de saudação de uma versão personalizada io.js inclui apenas duas etapas. Primeiro, baixe o hello **win-x64** binário diretamente da saudação [io.js distribuição]. São necessários dois arquivos: **iojs.exe** e **iojs.lib**. Salvar os dois arquivos tooa pasta dentro de seu aplicativo web, por exemplo **bin/iojs**.

tooconfigure aplicativos Web toouse **iojs.exe** em vez de uma versão previamente instalada do nó, cria um **IISNode.yml** arquivo na raiz de saudação do seu aplicativo e adicionar a seguinte linha de saudação.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como io.js toouse com aplicativos de Web do serviço de aplicativo, usando os dois fornecidos scripts de implantação, bem como instalação manual. 

> [!NOTE]
> O io.js está em desenvolvimento e mais atualizado do que o Node.js. Vários módulos de Node.js talvez não funcionem com io.js. Confira [io.js no GitHub] para a solução de problemas.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

[io.js]: https://iojs.org
[io.js distribuição]: https://iojs.org/dist/
[io.js no GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
