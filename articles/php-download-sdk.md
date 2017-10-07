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
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="bd853-103">Baixar hello Azure SDK para PHP</span><span class="sxs-lookup"><span data-stu-id="bd853-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="bd853-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="bd853-104">Overview</span></span>
<span data-ttu-id="bd853-105">Hello Azure SDK para PHP inclui componentes que permitem que você toodevelop, implantar e gerenciam aplicativos PHP para o Azure.</span><span class="sxs-lookup"><span data-stu-id="bd853-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="bd853-106">Especificamente, hello Azure SDK para PHP inclui o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="bd853-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="bd853-107">**Olá bibliotecas de cliente do PHP para o Azure**.</span><span class="sxs-lookup"><span data-stu-id="bd853-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="bd853-108">Essas bibliotecas de classe fornecem uma interface para acessar recursos do Azure, como serviços de gerenciamento de dados e serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bd853-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="bd853-109">**saudação de Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)**.</span><span class="sxs-lookup"><span data-stu-id="bd853-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="bd853-110">Esse é um conjunto de ferramentas de linha de comando para implantar e gerenciar serviços do Azure, como os Sites do Azure e Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd853-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="bd853-111">Olá trabalho CLI do Azure em qualquer plataforma, inclusive Windows, Linux e Mac.</span><span class="sxs-lookup"><span data-stu-id="bd853-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="bd853-112">**PowerShell para Azure (somente Windows)**.</span><span class="sxs-lookup"><span data-stu-id="bd853-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="bd853-113">Esse é um conjunto de cmdlets do PowerShell para implantar e gerenciar serviços do Microsoft Azure, como Serviços de Nuvem e Máquinas Virtuais.</span><span class="sxs-lookup"><span data-stu-id="bd853-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="bd853-114">**Olá emuladores do Azure (somente Windows)**.</span><span class="sxs-lookup"><span data-stu-id="bd853-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="bd853-115">emuladores de computação e armazenamento Olá são emuladores locais dos serviços de nuvem e serviços de gerenciamento de dados que permitem que você tootest um aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="bd853-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="bd853-116">Hello Azure emuladores executados apenas no Windows.</span><span class="sxs-lookup"><span data-stu-id="bd853-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="bd853-117">Olá seções a seguir descrevem como toodownload e instale Olá componentes descritos acima.</span><span class="sxs-lookup"><span data-stu-id="bd853-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="bd853-118">Olá instruções neste tópico pressupõem que você tenha [PHP] [ install-php] instalado.</span><span class="sxs-lookup"><span data-stu-id="bd853-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="bd853-119">Você deve ter o PHP 5.5 ou superior bibliotecas de cliente toouse Olá PHP do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd853-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="bd853-120">As bibliotecas de cliente PHP para Azure.</span><span class="sxs-lookup"><span data-stu-id="bd853-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="bd853-121">Olá PHP bibliotecas de cliente do Azure fornecem uma interface para acessar os recursos do Azure, como os serviços de gerenciamento de dados e serviços de nuvem, de qualquer sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="bd853-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="bd853-122">Essas bibliotecas podem ser instaladas por meio de saudação criador.</span><span class="sxs-lookup"><span data-stu-id="bd853-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="bd853-123">Para obter informações sobre como toouse Olá bibliotecas de cliente do PHP para o Azure, consulte [como tooUse Olá serviço Blob][blob-service], [como tooUse Olá serviço tabela] [ table-service] e [como tooUse Olá serviço fila][queue-service].</span><span class="sxs-lookup"><span data-stu-id="bd853-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="bd853-124">Instalar por meio do Composer</span><span class="sxs-lookup"><span data-stu-id="bd853-124">Install via Composer</span></span>
1. <span data-ttu-id="bd853-125">[Instale o Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="bd853-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="bd853-126">No Windows, você também precisará variável de ambiente de caminho tooadd Olá Git tooyour executável.</span><span class="sxs-lookup"><span data-stu-id="bd853-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="bd853-127">Crie um arquivo chamado **composer.json** em Olá raiz do seu projeto e adicionar Olá tooit de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd853-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="bd853-128">Baixe **[composer.phar][composer-phar]** na raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="bd853-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="bd853-129">Abra um prompt de comando e execute esta função na raiz do projeto</span><span class="sxs-lookup"><span data-stu-id="bd853-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="bd853-130">O PowerShell do Azure e o Emuladores do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd853-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="bd853-131">O PowerShell do Azure é um conjunto de cmdlets do PowerShell para implantar e gerenciar serviços do Azure (como Serviços de Nuvem e Máquinas Virtuais).</span><span class="sxs-lookup"><span data-stu-id="bd853-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="bd853-132">Olá emuladores do Azure são emuladores de serviços de nuvem e serviços de gerenciamento de dados que permitem que você tootest um aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="bd853-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="bd853-133">Esses componentes recebem suporte apenas no Windows.</span><span class="sxs-lookup"><span data-stu-id="bd853-133">These components are supported Windows only.</span></span>

<span data-ttu-id="bd853-134">Olá tooinstall de maneira recomendada do Azure PowerShell e Olá emuladores do Azure é Olá toouse [Microsoft Web Platform Installer][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="bd853-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="bd853-135">Observe que você também pode escolher tooinstall outros componentes de desenvolvimento, como PHP, SQL Server, Olá Drivers da Microsoft para SQL Server para PHP e o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="bd853-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="bd853-136">Para obter informações sobre como toouse Azure PowerShell, consulte [como tooUse do Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="bd853-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="bd853-137">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bd853-137">Azure CLI</span></span>
<span data-ttu-id="bd853-138">Olá CLI do Azure é um conjunto de comandos para implantar e gerenciar serviços do Azure, como sites do Azure e máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd853-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="bd853-139">Para obter informações sobre como instalar a CLI do Azure, consulte [instalação Olá CLI do Azure](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="bd853-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd853-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd853-140">Next steps</span></span>
<span data-ttu-id="bd853-141">Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="bd853-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
