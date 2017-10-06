---
title: "aaaDeploy tooAzure seu aplicativo do serviço de aplicativo usando o FTP/S | Microsoft Docs"
description: "Saiba como toodeploy tooAzure seu aplicativo do serviço de aplicativo usando FTP ou FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>Implantar seu tooAzure de aplicativo do serviço de aplicativo usando o FTP/S

Este artigo mostra como toouse FTP ou FTPS toodeploy seu aplicativo web, o back-end do aplicativo móvel ou o aplicativo de API muito[do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

ponto de extremidade FTP/S de saudação para seu aplicativo já está ativo. Nenhuma configuração é necessária tooenable implantação de FTP/S.

> [!IMPORTANT]
> Estamos continuamente realizando as etapas tooimprove segurança da plataforma Microsoft Azure. Como parte desse esforço contínuo, um upgrade dos Aplicativos Web está planejado para as regiões Central e Nordeste da Alemanha. Durante esse aplicativos Web serão desativar uso de saudação do protocolo de texto sem formatação FTP para implantações. Clientes de tooour nossa recomendação é tooFTPS tooswitch para implantações. Não esperamos que qualquer serviço de tooyour de interrupção durante esta atualização que está planejada para 9/5. Agradecemos sua compreensão.

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>Etapa 1: Definir credenciais de implantação

servidor de saudação FTP tooaccess para seu aplicativo, primeiro é necessário credenciais de implantação. 

tooset ou redefinir suas credenciais de implantação, consulte [credenciais de implantação de serviço de aplicativo do Azure](app-service-deployment-credentials.md). Este tutorial demonstra o uso de saudação de credenciais de nível de usuário.

## <a name="step-2-get-ftp-connection-information"></a>Etapa 2: Obter informações de conexão de FTP

1. Em Olá [portal do Azure](https://portal.azure.com), abra o aplicativo [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Selecione **visão geral** no menu da esquerda hello, observe os valores hello para **usuário de FTP/implantação**, **nome de Host do FTP**, e **FTPS nome de Host**. 

    ![Informações de conexão de FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > Olá **usuário de FTP/implantação** valor usuário conforme exibido pelo Portal do Azure incluindo o nome do aplicativo hello em contexto apropriado do tooprovide de ordem para o servidor FTP de Olá Olá.
    > Você pode encontrar hello as mesmas informações quando você seleciona **propriedades** no menu esquerdo hello. 
    >
    > Além disso, a senha de implantação Olá nunca é mostrada. Se você esquecer sua senha de implantação, volte muito[etapa 1](#step1) e redefinir a senha de implantação.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>Etapa 3: Implantar arquivos tooAzure

1. Seu cliente FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use informações de conexão Olá coletadas tooconnect tooyour aplicativo.
3. Copie os arquivos e sua toohello de estrutura de diretório do respectivos [ **/site/wwwroot** diretório](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) no Azure (ou hello **/site/wwwroot/App_Data/trabalhos/** diretório para WebJobs).
4. Aplicativo de saudação do aplicativo do procurar tooyour URL tooverify está sendo executado corretamente. 

> [!NOTE] 
> Ao contrário de [implantações com base no Git](app-service-deploy-local-git.md), implantação de FTP não dá suporte a saudação automações de implantação a seguir: 
>
> - restauração de dependência (como automações NuGet, NPM, PIP e criador)
> - compilação de binários do .NET
> - geração de Web. config (eis uma [Node. js exemplo](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))
> 
> Você deve restaurar, criar e gerar esses arquivos necessários manualmente no computador local e implantá-los junto com seu aplicativo.
>
>

## <a name="next-steps"></a>Próximas etapas

Para cenários de implantação mais avançados, tente [Implantando tooAzure com Git](app-service-deploy-local-git.md). Implantação baseada em Git tooAzure habilita o controle de versão, a restauração do pacote, MSBuild e muito mais.

## <a name="more-resources"></a>Mais Recursos

* [Criar um aplicativo Web do PHP-MySQL e implantá-lo usando o FTP](web-sites-php-mysql-deploy-use-ftp.md).
* [Credenciais de implantação do Serviço de Aplicativo do Azure](app-service-deploy-ftp.md)
