---
title: "Olá aaaDownload Azure SDK para PHP"
description: Saiba como toodownload e instale hello Azure SDK para PHP.
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a>Baixar hello Azure SDK para PHP
## <a name="overview"></a>Visão geral
Hello Azure SDK para PHP inclui componentes que permitem que você toodevelop, implantar e gerenciam aplicativos PHP para o Azure. Especificamente, hello Azure SDK para PHP inclui o seguinte hello:

* **Olá bibliotecas de cliente do PHP para o Azure**. Essas bibliotecas de classe fornecem uma interface para acessar recursos do Azure, como serviços de gerenciamento de dados e serviços de nuvem.  
* **saudação de Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)**. Esse é um conjunto de ferramentas de linha de comando para implantar e gerenciar serviços do Azure, como os Sites do Azure e Máquinas Virtuais do Azure. Olá trabalho CLI do Azure em qualquer plataforma, inclusive Windows, Linux e Mac.
* **PowerShell para Azure (somente Windows)**. Esse é um conjunto de cmdlets do PowerShell para implantar e gerenciar serviços do Microsoft Azure, como Serviços de Nuvem e Máquinas Virtuais.
* **Olá emuladores do Azure (somente Windows)**. emuladores de computação e armazenamento Olá são emuladores locais dos serviços de nuvem e serviços de gerenciamento de dados que permitem que você tootest um aplicativo localmente. Hello Azure emuladores executados apenas no Windows.

Olá seções a seguir descrevem como toodownload e instale Olá componentes descritos acima.

Olá instruções neste tópico pressupõem que você tenha [PHP] [ install-php] instalado.

> [!NOTE]
> Você deve ter o PHP 5.5 ou superior bibliotecas de cliente toouse Olá PHP do Azure.
> 
> 

## <a name="php-client-libraries-for-azure"></a>As bibliotecas de cliente PHP para Azure.
Olá PHP bibliotecas de cliente do Azure fornecem uma interface para acessar os recursos do Azure, como os serviços de gerenciamento de dados e serviços de nuvem, de qualquer sistema operacional. Essas bibliotecas podem ser instaladas por meio de saudação criador.

Para obter informações sobre como toouse Olá bibliotecas de cliente do PHP para o Azure, consulte [como tooUse Olá serviço Blob][blob-service], [como tooUse Olá serviço tabela] [ table-service] e [como tooUse Olá serviço fila][queue-service].

### <a name="install-via-composer"></a>Instalar por meio do Composer
1. [Instale o Git][install-git].

    > [AZURE.NOTE] No Windows, você também precisará variável de ambiente de caminho tooadd Olá Git tooyour executável.

1. Crie um arquivo chamado **composer.json** em Olá raiz do seu projeto e adicionar Olá tooit de código a seguir:
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. Baixe **[composer.phar][composer-phar]** na raiz do projeto.
3. Abra um prompt de comando e execute esta função na raiz do projeto
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a>O PowerShell do Azure e o Emuladores do Azure.
O PowerShell do Azure é um conjunto de cmdlets do PowerShell para implantar e gerenciar serviços do Azure (como Serviços de Nuvem e Máquinas Virtuais). Olá emuladores do Azure são emuladores de serviços de nuvem e serviços de gerenciamento de dados que permitem que você tootest um aplicativo localmente. Esses componentes recebem suporte apenas no Windows.

Olá tooinstall de maneira recomendada do Azure PowerShell e Olá emuladores do Azure é Olá toouse [Microsoft Web Platform Installer][download-wpi]. Observe que você também pode escolher tooinstall outros componentes de desenvolvimento, como PHP, SQL Server, Olá Drivers da Microsoft para SQL Server para PHP e o WebMatrix.

Para obter informações sobre como toouse Azure PowerShell, consulte [como tooUse do Azure PowerShell][powershell-tools].

## <a name="azure-cli"></a>CLI do Azure
Olá CLI do Azure é um conjunto de comandos para implantar e gerenciar serviços do Azure, como sites do Azure e máquinas virtuais do Azure. Para obter informações sobre como instalar a CLI do Azure, consulte [instalação Olá CLI do Azure](cli-install-nodejs.md).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
