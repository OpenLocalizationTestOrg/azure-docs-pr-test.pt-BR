---
title: "implantação de aaaContinuous para funções do Azure | Microsoft Docs"
description: "Use recursos de implantação contínua do serviço de aplicativo do Azure toopublish funções do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a>Implantação contínua para Azure Functions
As funções do Azure torna fácil toodeploy seu aplicativo de função usando a integração contínua do serviço de aplicativo. Funções integram BitBucket, Dropbox, GitHub e Visual Studio Team Services (VSTS). Isso permite que um fluxo de trabalho em que o código de função atualizações feito usando um tooAzure de implantação de disparador esses serviços integrados. Se você estiver novas funções tooAzure, começar com [visão geral de funções do Azure](functions-overview.md).

A implantação contínua é uma ótima opção para projetos nos quais várias contribuições frequentes são integradas. Ele também permite manter o controle do código-fonte no código de funções. Olá origens de implantação a seguir é atualmente suportado:

* [Bitbucket](https://bitbucket.org/)
* [Dropbox](https://www.dropbox.com/)
* Repositório externo (Git ou Mercurial)
* [Repositório local Git](../app-service-web/app-service-deploy-local-git.md)
* [GitHub](https://github.com)
* [OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

As implantações são configuradas para cada aplicativo de função. Após a implantação contínua está habilitada, o código de toofunction de acesso no portal de saudação está definido muito*somente leitura*.

## <a name="continuous-deployment-requirements"></a>Requisitos de implantação contínua

Você deve ter sua origem de implantação configurada e seu código de funções na origem de implantação de saudação antes de configurar a implantação contínua. Em uma implantação de aplicativo de determinada função, cada função reside em um subdiretório nomeado, onde o nome do diretório Olá é o nome de saudação do função hello.  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>Configurar a implantação contínua
Use esta implantação contínua do procedimento tooconfigure para um aplicativo de função existente. Essas etapas demonstram a integração com um repositório GitHub, porém etapas semelhantes se aplicam para serviços do Visual Studio Team Services ou outros serviços de implantação.

1. Em seu aplicativo de função no hello [portal do Azure](https://portal.azure.com), clique em **recursos de plataforma** e **opções de implantação**. 
   
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Em seguida, em Olá **implantações** folha clique **instalação**.
 
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Em Olá **origem de implantação** folha, clique em **Escolher fonte**, preencha as informações de saudação para sua fonte de implantação escolhida e clique em **Okey**.
   
    ![Escolher a fonte de implantação](./media/functions-continuous-deployment/choose-deployment-source.png)

Após a configuração de implantação contínua, todas as alterações de arquivo na fonte de implantação são copiados toohello função aplicativo e uma implantação completa do site é acionada. site de saudação for reimplantado quando os arquivos na fonte de saudação são atualizados.

## <a name="deployment-options"></a>Opções de implantação

Olá seguem alguns cenários comuns de implantação:

- [Criar uma implantação de preparo](#staging)
- [Mover a implantação de toocontinuous funções existentes](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>Criar uma implantação de preparo

Aplicativos de Função ainda não dão suporte a slots de implantação. No entanto, você ainda pode gerenciar implantações de produção e preparo separadas usando a integração contínua.

Olá tooconfigure de processo e trabalhar com uma implantação de preparo geralmente tem esta aparência:

1. Crie dois aplicativos de função em sua assinatura, uma para o código de produção de hello e outra para preparação. 

2. Crie uma fonte de implantação, se você ainda não tiver uma. Este exemplo usa [GitHub].

3. Para seu aplicativo de função de produção, Olá completo anterior etapas **configurar implantação contínua** e conjunto Olá implantação ramificação toohello mestre ramificação do repositório GitHub.
   
    ![Escolher a ramificação de implantação](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. Repita essa etapa para Olá função de aplicativo de teste, mas escolha Olá Preparando ramificação em vez disso, no seu repositório GitHub. Se sua fonte de implantação não der suporte à ramificação, use uma pasta diferente.
    
5. Faça atualizações tooyour código em Olá branch ou pasta de preparo e verificar se essas alterações são refletidas na implantação de preparo de saudação.

6. Depois de testes, mesclar alterações do branch de preparo Olá no branch mestre hello. Essa mesclagem gatilhos implantação toohello função aplicativo de produção. Se sua fonte de implantação não oferece suporte a ramificações, substitua arquivos de saudação na pasta de produção de hello com arquivos Olá Olá pasta temporária.

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a>Mover a implantação de toocontinuous funções existentes
Quando você tem funções existentes que você tenha criado e mantido no portal de saudação, você precisa toodownload existente função arquivos de código usando FTP ou hello repositório Git local antes de configurar a implantação contínua conforme descrito acima. Você pode fazer isso no hello configurações de serviço de aplicativo para seu aplicativo de função. Depois que os arquivos são baixados, você poderá carregá-los origem de implantação contínua tooyour escolhido.

> [!NOTE]
> Depois de configurar a integração contínua, não será capaz de tooedit sua fonte de arquivos no portal de funções hello.

- [Como configurar credenciais de implantação](#credentials)
- [Como baixar arquivos usando FTP](#downftp)
- [Como: baixar os arquivos usando o repositório do Git local Olá](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>Como: configurar credenciais de implantação
Antes de baixar arquivos de seu aplicativo de função com FTP ou repositório Git local, você deve configurar seu site de saudação tooaccess credenciais. As credenciais são definidas no nível de aplicativo de função hello. As etapas a seguir de saudação do uso tooset credenciais de implantação no portal do Azure de saudação:

1. Em seu aplicativo de função no hello [portal do Azure](https://portal.azure.com), clique em **recursos de plataforma** e **credenciais de implantação**.
   
    ![Definir credenciais de implantação local](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. Digite um nome de usuário e senha e clique em **Salvar**. Agora você pode usar essas credenciais tooaccess seu aplicativo de função do FTP ou hello repositório Git interno.

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>Como: baixar arquivos usando FTP

1. Em seu aplicativo de função no hello [portal do Azure](https://portal.azure.com), clique em **recursos de plataforma** e **propriedades**, em seguida, copie os valores hello para **dousuáriodeFTP/implantação**, **Nome do Host do FTP**, e **nome de Host FTPS**.  

    **Usuário de FTP/implantação** deve ser inserido como exibido no portal de hello, incluindo o nome do aplicativo hello, tooprovide o contexto apropriado para o servidor de saudação FTP.
   
    ![Obter as informações de implantação](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. De seu cliente FTP, use informações de conexão Olá coletadas tooconnect tooyour aplicativo e baixar arquivos de origem Olá para suas funções.

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a>Como: baixar arquivos usando o repositório Git local

1. Em seu aplicativo de função no hello [portal do Azure](https://portal.azure.com), clique em **recursos de plataforma** e **opções de implantação**. 
   
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Em seguida, em Olá **implantações** folha clique **instalação**.
 
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Em Olá **origem de implantação** folha, clique em **repositório Git Local** e, em seguida, clique em **Okey**.

3. Em **recursos de plataforma**, clique em **propriedades** e observe o valor de saudação da URL de Git. 
   
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. Repositório de saudação do clone em seu computador local usando um prompt de comando com reconhecimento de Git ou sua ferramenta favorita do Git. Olá comando de clone de Git tem esta aparência:
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. Obter arquivos do seu clone de toohello do aplicativo de função no computador local, como no exemplo a seguir de saudação:
   
        git pull origin master
   
    Se solicitado, forneça as [credenciais de implantação configuradas](#credentials).  

[GitHub]: https://github.com/
