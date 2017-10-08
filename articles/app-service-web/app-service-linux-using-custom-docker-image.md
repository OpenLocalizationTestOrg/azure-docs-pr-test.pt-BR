---
title: aaaHow toouse uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux | Microsoft Docs
description: Como toouse um Docker personalizado de imagem para o aplicativo Web do Azure no Linux.
keywords: "serviço de aplicativo do azure, aplicativo web, linux, docker, contêiner"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


O Serviço de Aplicativo fornece pilhas de aplicativos predefinidas no Linux com suporte para versões específicas, como PHP 7.0 e Node.js 4.5. Serviço de aplicativo no Linux usa contêineres do Docker toohost esses pré-criadas pilhas de aplicativos. Você também pode usar um toodeploy de imagem personalizada do Docker sua pilha de aplicativos de tooan de aplicativo web que não ainda esteja definida no Azure. As imagens personalizadas do Docker podem ser hospedadas em um repositório público ou privado do Docker.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Como definir uma imagem personalizada do Docker para um aplicativo Web
Você pode definir a imagem personalizada do Docker Olá para os novos e aplicativos de webs existentes. Quando você cria um aplicativo web no Linux no hello [portal do Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), clique em **configurar contêiner** tooset uma imagem personalizada do Docker:

![Imagem personalizada do Docker para um novo aplicativo Web no Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Como usar uma imagem personalizada do Docker no Hub do Docker ##
toouse uma imagem personalizada do Docker do Hub do Docker:

1. Em hello [portal do Azure](https://portal.azure.com), localize o aplicativo web no Linux, em seguida, na **configurações** clique **contêiner Docker**.

2.  Selecione **Hub do Docker** como Olá **origem da imagem**, em seguida, clique em **pública** ou **privada** e tipo hello **imagem e o nome da marca opcional**, como `node:4.5`. Olá **comando de inicialização** é conjunto automaticamente com base no que é definido no arquivo de imagem do Docker hello, mas você pode definir seus próprios comandos.  

    ![Configurar a imagem do repositório público do Hub do Docker][2]

    Quando a imagem for de um repositório privado, você também precisa ter credenciais de Hub do Docker do tooenter hello como (**nome de usuário de logon** e **senha**) para repositório de Hub do Docker particular hello.

    ![Configurar a imagem do repositório privado do Hub do Docker][3]

3. Depois que você tiver configurado o contêiner de saudação, clique em **salvar**.

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a>Como a imagem de um registro da imagem privada toouse um Docker ##
toouse uma imagem personalizada do Docker de um registro da imagem privada:

1. Em hello [portal do Azure](https://portal.azure.com), localize o aplicativo web no Linux, em seguida, na **configurações** clique **contêiner Docker**.

2.  Clique em **registro privado** como Olá **origem da imagem**. Digite hello **imagem e o nome de marca opcional**, **URL do servidor** para registro privada hello, juntamente com as credenciais da saudação (**nome de usuário de logon** e **senha** ). Clique em **Salvar**.

    ![Configurar a imagem de Docker a partir do registro privado][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a>Como: definir Olá porta usada pela sua imagem de Docker ##

Quando você usar uma imagem personalizada do Docker para seu aplicativo web, você pode usar o hello `WEBSITES_PORT` variável de ambiente no Dockerfile, o que é adicionado contêiner toohello gerado. Considere Olá exemplo de um arquivo de docker para um aplicativo Ruby a seguir:

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

Na última linha de comando hello, você pode ver que essa variável de ambiente WEBSITES_PORT Olá é passado em tempo de execução. Lembre-se de que as diferenças entre maiúsculas e minúsculas importam nos comandos.

Plataforma Olá foi usando previamente `PORT` aplicativo configuração, podemos estiver planejando toodeprecate Olá use essa configuração de aplicativo e mover toousing `WEBSITES_PORT` exclusivamente.

Quando você usar uma imagem do Docker existente criada por outra pessoa, talvez seja necessário toospecify uma porta diferente da porta 80 para o aplicativo hello. tooconfigure Olá porta, adicione um configuração de aplicativo denominada `WEBSITES_PORT` com valor de saudação conforme mostrado abaixo:

![Definir a configuração de aplicativo PORT para a imagem personalizada do Docker][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a>Como: definir o tempo de inicialização de saudação para a imagem do Docker ##

Por padrão, se o contêiner não for iniciado antes de 230 segundos, plataforma Olá reiniciará seu contêiner. Se sua imagem personalizada do Docker é iniciado em mais de 230 segundos, você pode usar o hello `WEBSITES_CONTAINER_START_TIME_LIMIT` aplicativo definindo, valor Olá para essa configuração é em segundos, isso permitirá Olá plataforma manter seu contêiner em execução antes de reiniciá-lo. valor padrão de saudação é 230 segundos e Olá máximo permitido para valor é de 600 segundos.

## <a name="how-to-unmount-hello-platform-provided-storage"></a>Como: desmontar o armazenamento de plataforma fornecido Olá ##

Por padrão, a plataforma de saudação montará toohello de compartilhamento de um armazenamento persistente `\home\` directory. Se sua imagem de contêiner não precisa de um compartilhamento persistente, você pode desabilitar a montagem que o armazenamento por configuração Olá `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplicativo configuração muito`false`. Você ainda terá acesso toothat armazenamento do site de scm hello e todos os logs de Docker (se habilitado) serão gravados toohello arquivos de log gerados pela plataforma de saudação.

## <a name="how-to-switch-back-toousing-a-built-in-image"></a>Como: retorne toousing uma imagem interna ##

tooswitch de usar uma imagem personalizada de toousing uma imagem interna:

1. Em Olá [portal do Azure](https://portal.azure.com), localize o aplicativo web no Linux, em seguida, na **configurações** clique **do serviço de aplicativo**.

2. Selecione seu **pilha de tempo de execução** toouse para imagem interna do hello, em seguida, clique em **salvar**. 

![Configurar a imagem interna do Docker][5]


## <a name="troubleshooting"></a>Solucionar problemas ##

Quando o aplicativo falhar toostart com sua imagem personalizada do Docker, verifique Olá que docker registra no diretório de arquivos de log de saudação. Acesse esse diretório por meio de seu site SCM ou via FTP.
Olá toolog `stdout` e `stderr` de seu contêiner, você precisa tooenable **log do contêiner do Docker** em **Logs de diagnóstico**.

![Habilitando o log][8]

![Usando logs de Docker tooview Kudu][7]

Você pode acessar o site SCM saudação do **ferramentas avançadas de** em Olá **ferramentas de desenvolvimento** menu.

## <a name="next-steps"></a>Próximas etapas ##

Siga Olá tooget links de Introdução ao aplicativo Web no Linux a seguir.   

* [Introdução tooAzure Web App no Linux](./app-service-linux-intro.md)
* [Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux](./app-service-linux-using-nodejs-pm2.md)
* [Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux](app-service-linux-faq.md)

Poste perguntas e preocupações em [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
