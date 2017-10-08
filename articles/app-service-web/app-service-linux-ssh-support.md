---
title: "suporte a aaaSSH Azure serviço de aplicativo Web App no Linux | Microsoft Docs"
description: Saiba como usar SSH com o Aplicativo Web do Azure no Linux.
keywords: "serviço de aplicativo do azure, aplicativo web, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Suporte de SSH para o Aplicativo Web do Azure no Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Visão geral

O [SSH (Secure Shell)](https://en.wikipedia.org/wiki/Secure_Shell) é um protocolo de rede criptográfico para usar serviços de rede de forma segura. É toolog mais comumente usado em um sistema remotamente com segurança de uma linha de comando e executar comandos administrativos remotamente.

Web App no Linux fornece suporte SSH no contêiner do aplicativo hello com cada uma das imagens do Docker internas Olá usadas para Olá pilha de tempo de execução de novos aplicativos web. 

![Pilhas de tempo de execução](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

Você também pode usar SSH com as imagens do Docker personalizadas, incluindo o servidor SSH hello como parte da imagem hello e configurá-lo, conforme descrito neste tópico.



## <a name="making-a-client-connection"></a>Estabelecendo uma conexão de cliente

toomake uma conexão de cliente SSH, o site principal Olá deve ser iniciado. 

Cole o ponto de extremidade de gerenciamento de controle de origem (SCM) de saudação para seu aplicativo web no seu navegador usando Olá formulário a seguir:

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Se você não estiver autenticado, será necessário tooauthenticate com sua assinatura do Azure tooconnect.

![Conexão SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Suporte de SSH com imagens personalizadas do Docker

Em ordem para uma personalizado Docker imagem toosupport SSH comunicação entre o contêiner de saudação e cliente Olá Olá portal do Azure, execute Olá seguindo as etapas para a imagem do Docker. 

Essas etapas são mostrados na Olá repositório do serviço de aplicativo do Azure como um exemplo [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Incluir Olá `openssh-server` instalação [ `RUN` instrução](https://docs.docker.com/engine/reference/builder/#run) em hello Dockerfile para sua imagem e definir a senha de saudação para conta de raiz de saudação muito`"Docker!"`. 

    > [!NOTE] 
    > Essa configuração não permite que o contêiner de toohello conexões externas. SSH só pode ser acessado por meio de saudação Kudu / Site de SCM, que é autenticado usando Olá credenciais de publicação.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Adicionar um [ `COPY` instrução](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy um [sshd_config](http://man.openbsd.org/sshd_config) arquivo toohello */etc/ssh/* directory. O arquivo de configuração deve ser baseado em nosso arquivo sshd_config no repositório do GitHub do serviço de aplicativo do Azure Olá [aqui](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Olá *sshd_config* arquivo deve incluir o seguinte hello ou falha de conexão hello: 
    > * `Ciphers`deve incluir pelo menos um dos seguintes Olá: `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`deve incluir pelo menos um dos seguintes Olá: `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Incluir porta 2222 na Olá [ `EXPOSE` instrução](https://docs.docker.com/engine/reference/builder/#expose) para Olá Dockerfile. Embora a senha de raiz de saudação for conhecida, porta 2222 não pode ser acessada de saudação à internet. É uma única porta interna acessível somente por contêineres dentro da rede de ponte de saudação de uma rede virtual privada.

    ```docker
    EXPOSE 2222 80
    ```

4. Certifique-se de toostart Olá ssh de serviço. exemplo Hello [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) usa um script de shell em */bin* directory.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Olá Dockerfile usa Olá [ `CMD` instrução](https://docs.docker.com/engine/reference/builder/#cmd) toorun script de saudação.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Próximas etapas
Consulte Olá seguindo os links para obter mais informações sobre o aplicativo Web no Linux. Você pode postar perguntas e problemas no [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Como toouse um Docker personalizado da imagem para o aplicativo Web do Azure no Linux](app-service-linux-using-custom-docker-image.md)
* [Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux](app-service-linux-using-nodejs-pm2.md)
* [Usando o .NET Core no Aplicativo Web do Azure no Linux](app-service-linux-using-dotnetcore.md)
* [Usando Ruby no Aplicativo Web do Azure no Linux](app-service-linux-ruby-get-started.md)
* [Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux](app-service-linux-faq.md)

