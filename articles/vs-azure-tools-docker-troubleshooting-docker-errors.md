---
title: erros de cliente de Docker aaaTroubleshooting no Windows usando o Visual Studio | Microsoft Docs
description: Solucionar problemas encontrados ao usar o Visual Studio toocreate e implantar tooDocker de aplicativos web no Windows usando o Visual Studio.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a>Solucionar problemas de desenvolvimento do Docker no Visual Studio

Quando você estiver trabalhando com o Visual Studio Tools para Docker Preview, você pode encontrar alguns problemas devido à natureza de saudação da visualização de saudação.
Veja a seguir alguns problemas comuns e suas resoluções.  

## <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

### <a name="linux-containers"></a>**Contêineres do Linux**

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a>Os erros de compilação ocorrem durante a depuração de um aplicativo Web ou de um console do .NET Core  

Isso pode ser relacionado toonot unidade Olá onde reside o projeto de saudação de compartilhamento com o Docker para Windows.  Você pode receber um erro como Olá seguinte:

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
tooresolve esse problema:

1. Clique com botão direito **Docker para Windows** Olá área de notificação e, em seguida, selecione **configurações**.  
2. Selecione **unidades compartilhadas** e compartilhar Olá unidade onde o projeto Olá reside.

### <a name="windows-containers"></a>**Contêineres do Windows**

Olá problemas a seguir são toodebugging específico do .NET Framework web e console de aplicativos em contêineres do Windows.

#### <a name="prerequisites"></a>Pré-requisitos

1. Visual Studio 2017 RC (ou posterior) com hello .NET Core e carga de trabalho de visualização de Docker deve ser instalada.
2. Atualização de Aniversário do Windows 10 com os últimos patches do Windows Update. Especificamente, o [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) deve ser instalado. 
3. O [Docker para Windows](https://docs.docker.com/docker-for-windows/) (compilação 1.13.0 ou posterior) deve ser instalado.
4. **Alternar contêineres tooWindows** deve ser selecionado. Na área de notificação de saudação, clique em **Docker para Windows**e, em seguida, selecione **alternar contêineres tooWindows**. Depois de reinicia a máquina hello, certifique-se de que essa configuração é mantida.

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a>A saída do console não é exibida na janela de saída do Visual Studio durante a depuração de um aplicativo de console

Este é um problema conhecido com o depurador do Visual Studio hello (msvsmon.exe), que atualmente não é projetado para este cenário. Suporte para esse cenário pode ser incluído em uma versão futura. saída de toosee do aplicativo de console hello no Visual Studio, use **Docker: Iniciar projeto**, que é equivalente a muito**iniciar sem depuração**.

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a>Depurando aplicativos web com hello versão de configuração falha com erro de proibido (403)

toowork esse problema, abra web.release.config na solução hello e comentar ou excluir Olá linhas seguintes:

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a>Visual Studio 2015

### <a name="linux-containers"></a>**Contêineres do Linux**

#### <a name="unable-toovalidate-volume-mapping"></a>Mapeamento do volume não é possível toovalidate
Mapeamento do volume é o código-fonte necessário tooshare hello e binários do seu aplicativo com a pasta de aplicativo hello no contêiner de saudação.  Os mapeamentos de volume específico estão contidos em docker-compose.dev.debug.yml e docker-compose.dev.release.yml. Como os arquivos são alterados na sua máquina host, contêineres de saudação refletem essas alterações em uma estrutura de pasta semelhante.

mapeamento do volume tooenable:

1. Clique em **Moby** na área de notificação hello e selecione **configurações**.
2. Selecione **Unidades Compartilhadas**.
3. Selecione a unidade de saudação que hospeda sua unidade de projeto e hello onde % USERPROFILE % reside.
4. Clique em **Aplicar**.

tootest se o mapeamento do volume estiver funcionando, recriar e selecione F5 de dentro do Visual Studio depois de uma ou mais unidades foram compartilhadas ou executadas Olá código a seguir em um prompt de comando.

> [!NOTE]
> Este exemplo pressupõe que a pasta Usuários esteja localizada na unidade C e que ela foi compartilhada.
> Examine, conforme necessário, se você compartilhou outra unidade.

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

Execute Olá código no contêiner do hello Linux a seguir.

```
/ # ls
```

Você deve ver uma lista de saudação usuários/pasta pública de pastas. Se nenhum arquivo for exibido e sua pasta /c/Usuários/Público não estiver vazia, o mapeamento de volume não estará configurado corretamente.

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

Alterar toohello fenda espacial diretório toosee Olá conteúdo de saudação `/c/Users/Public` diretório:

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> Quando você está trabalhando com VMs do Linux, o sistema de arquivos de contêiner Olá diferencia maiusculas de minúsculas.

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a>Compilação: a tarefa "PrepareForBuild" falhou inesperadamente

Microsoft.DotNet.Docker.CommandLine.ClientException: Erro ao tentar tooconnect.

Verifique se o que host Docker saudação padrão está em execução. Abra um prompt de comando e execute:

```
docker info
```

Se isso retornar um erro, em seguida, tente Olá toostart **Docker para Windows** aplicativo de área de trabalho. Se o aplicativo de área de trabalho Olá estiver em execução, em seguida, **Moby** devem ser visíveis na área de notificação de saudação. Clique com botão direito em **Moby** e abra **configurações**. Clique em **Redefinir** e reinicie o Docker.

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a>Uma caixa de diálogo de erro ocorre ao tentar tooadd Docker suporte ou depurar um aplicativo ASP.NET Core em um contêiner de (F5)

Depois de desinstalar e instalar extensões, Olá cache Managed Extensibility Framework (MEF) no Visual Studio pode ficar corrompida. Quando isso ocorrer, ele pode causar várias mensagens de erro quando você estiver adicionando suporte de Docker e/ou tentar toorun ou depuração (F5) o aplicativo ASP.NET Core. Como solução temporária, use Olá seguindo as etapas toodelete e regenerar Olá MEF o cache.

1. Feche todas as instâncias do Visual Studio.
1. Abra %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.
1. Exclua Olá pastas a seguir:
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. Abra o Visual Studio.
1. Repita o cenário de saudação.
