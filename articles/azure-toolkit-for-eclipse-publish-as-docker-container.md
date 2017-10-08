---
title: "Olá de aaaPublish um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse | Microsoft Docs"
description: "Saiba como toopublish uma tooMicrosoft de aplicativo web do Azure como um contêiner do Docker usando Olá Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Publicar um aplicativo web como um contêiner do Docker usando Olá Kit de ferramentas do Azure para Eclipse

Contêineres do Docker são um método amplamente usado para implantar aplicativos Web. Usando contêineres do Docker, os desenvolvedores podem consolidar todos os seus arquivos de projeto e dependências em um único pacote para o servidor de implantação tooa. Olá Kit de ferramentas do Azure para Eclipse simplifica esse processo para desenvolvedores de Java adicionando *Publicar como contêiner Docker* recursos para tooMicrosoft de implantação do Azure. Este artigo orienta Olá etapas necessárias toopublish tooAzure seus aplicativos como contêineres do Docker.

> [!NOTE]
> Para obter mais informações sobre o Docker estão disponíveis no hello [site Docker].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar seu tooAzure de aplicativo web usando um contêiner do Docker

1. Abra seu projeto de aplicativo Web no Eclipse.

2. Olá toostart **Publicar como contêiner Docker** assistente, faça o seguinte de saudação:

   * Em Olá **navegador** exibir, clique com o botão direito, clique em **Azure**e, em seguida, clique em **Publicar como contêiner Docker**.

      ![Comando Publicar como Contêiner do Docker da exibição Navegador][PUB01]

   * Na barra de ferramentas do Eclipse hello, clique em Olá **publicar** botão e, em seguida, clique em **Publicar como contêiner Docker**.

      ![Comando Publicar como Contêiner do Docker da barra de ferramentas do Eclipse][PUB02]
      
    Olá **implantar o contêiner do Docker no Azure** assistente é aberto.

    ![Olá implantar o contêiner do Docker no Assistente do Azure][PUB03]

3. Em Olá **digite um nome de imagem, selecione o caminho do artefato hello e verificar um toobe de host do Docker usado** janela, Olá a seguir:

    a. Em Olá **nome de imagem do Docker** , digite um nome exclusivo para o host do Docker. (Olá criará automaticamente um nome, mas você pode modificá-la.)

    b. Olá **Hosts** área exibe os hosts de Docker que você criou. Siga um destes procedimentos hello:

    * Se você tiver um host Docker existente, você pode implantar seu tooit de aplicativo web.
    * Clique em toocreate um novo host do Docker, **adicionar**.  
      
    Olá **criar Host do Docker** caixa de diálogo é aberta.

    ![Assistente para Implantar o Contêiner do Docker no Azure][PUB04a]

4. Em Olá **configurar nova máquina de virtual Olá** janela, especificar Olá para o host do Docker as opções a seguir. (Assistente de saudação gera automaticamente a maioria das opções de saudação para você, mas você pode modificar qualquer um deles.)

   a. **Nome**: insira um nome exclusivo para o host do Docker hello. (É não Olá mesmo Olá nome de imagem do Docker que você especificou anteriormente.)

   b. **Assinatura**: insira Olá assinatura do Azure que você usa para o host.

   c. **Região**: Inserir Olá região geográfica em que o host está localizado.

   d. Em Olá **sistema operacional do Host e o tamanho** guia:
     * **Sistema operacional do host**: insira o sistema operacional de saudação para a máquina virtual Olá que contém seu host.
     * **Tamanho**: insira o tamanho da máquina virtual Olá para o host.

   e. Em Olá **grupo de recursos** guia:
     * **Novo grupo de recursos**: crie um novo grupo de recursos para o host.
     * **Grupo de recursos existente**: insira um grupo de recursos existente de sua conta do Azure.

   f. Em Olá **rede** guia:
     * **Nova rede virtual**: crie uma nova rede virtual para o host.
     * **Rede virtual existente**: insira uma rede virtual existente de sua conta do Azure.

   g. Em Olá **armazenamento** guia:
     * **Nova conta de armazenamento**: crie uma nova conta de armazenamento para o host.
     * **Conta de armazenamento existente**: insira uma conta de armazenamento existente da sua conta do Azure.

5. Clique em **Avançar**.

6. Em Olá **configurar log de credenciais e configurações de porta** janela, selecione uma das Olá as opções a seguir:

    * **Importar credenciais do Azure Key Vault**: especifica um conjunto de credenciais salvas anteriormente que são armazenadas em sua assinatura do Azure.

      >[!NOTE]
      >Um cofre de chaves do Azure que é criada com uma conta específica ou entidade de serviço não é automaticamente acessível por outra conta ou entidade de serviço que compartilha assinatura hello. tooallow outra conta ou serviço toouse principal Olá Cofre de chaves, você deve usar o hello conta de saudação tooadd portal do Azure ou entidade de serviço.

    * **Novas credenciais de logon**: cria um novo conjunto de credenciais de logon. Se você selecionar essa opção, Olá a seguir:
    
      * Em Olá **VM credenciais** guia, escolha uma das seguintes Olá opções para credenciais de logon de máquina virtual de saudação do seu host do Docker:

          * **Nome de usuário**: insira o nome de usuário de saudação suas credenciais de logon de máquina virtual.
          * **Senha** e **confirmar**: insira a senha de saudação suas credenciais de logon de máquina virtual.
          * **SSH**: insira as configurações do hello Secure Shell (SSH) para o host do Docker. Você pode escolher Olá as opções a seguir:
            * **Nenhum**: especifica que a sua máquina virtual não permitirá conexões SSH.
            * **Gerar automaticamente**: cria automaticamente Olá configurações necessárias para conectar-se via SSH.
            * **Importar do diretório**: especifica um diretório que contém um conjunto de configurações de SSH salvas anteriormente. diretório de saudação deve conter Olá dois arquivos a seguir:
                * *id_rsa*: contém a identificação de RSA Olá para um usuário.
                * *id_rsa.pub*: contém Olá chave pública RSA que é usado para autenticação.
        
        ![Criar host do Docker][PUB05]

      * Em Olá **Docker Daemon credenciais** especifique Olá as opções a seguir:

          * **Porta de Daemon do docker**: insira a porta TCP exclusiva Olá para o host do Docker.
          * **Segurança de TLS**: insira Olá Transport Layer Security configurações para o host do Docker. Você pode escolher Olá as opções a seguir:
            * **Nenhum**: especifica que a sua máquina virtual não permitirá conexões TLS.
            * **Gerar automaticamente**: cria automaticamente Olá configurações necessárias para se conectar por meio de TLS.
            * **Importar do diretório**: especifica um diretório que contém um conjunto de configurações de TLS salvas anteriormente. Mais especificamente, o diretório de saudação deve conter Olá seis arquivos a seguir:
                * *CA. PEM* e *key.pem ca*: contêm o certificado hello e uma chave pública para Olá autoridade de certificação de TLS.
                * *cert.PEM* e *key.pem*: contêm o certificado do cliente hello e uma chave pública que é usado para autenticação de TLS.
                * *Server.PEM* e *key.pem server*: contêm o certificado do servidor de saudação e a chave pública para o host de saudação.

        ![Criar host do Docker][PUB06]

7. Depois que você inseriu todos Olá informações anteriores, clique em **concluir**.

8. Em Olá **implantar o contêiner do Docker no Azure** assistente, clique em **próximo**.

   ![Olá implantar o contêiner do Docker no Assistente do Azure][PUB07]

9. Em Olá **configurar Olá Docker contêiner toobe criado** janela, Olá a seguir:

   a. Em Olá **nome do contêiner Docker** , digite um nome exclusivo para o contêiner do Docker.

   b. Escolha uma saudação imagens do Docker a seguir:
     * **Imagem do Docker predefinida**: especifica uma imagem já existente do Docker do Azure.

       >[!NOTE]
       >Olá lista de imagens do Docker nesta caixa consiste em várias imagens que Olá Kit de ferramentas do Azure foi configurado toopatch de forma que o artefato é implantado automaticamente.

     * **Dockerfile personalizado**: especifica um Dockerfile salvo anteriormente do computador local.

       >[!NOTE]
       >Esse é um recurso mais avançado para desenvolvedores que querem toodeploy seu próprios Dockerfile. No entanto, ele é toodevelopers que usam essa tooensure de opção seu Dockerfile é criado corretamente. Olá Kit de ferramentas do Azure não validar o conteúdo de saudação em um Dockerfile personalizado, para que implantação Olá poderá falhar se Olá Dockerfile tem problemas. Além disso, Olá Kit de ferramentas do Azure espera Olá personalizado toocontain de Dockerfile um artefato de aplicativo web, e ele tentará tooopen uma conexão HTTP. Se os desenvolvedores publicarem um tipo diferente de artefato, eles poderão receber erros inócuos após a implantação.

   c. **Configurações de porta**: insira associação porta TCP de saudação exclusiva para o contêiner do Docker.

     ![janela de toobe criado Olá configurar Olá Docker contêiner][PUB08]

10. Depois de concluir todas Olá etapas anteriores, clique em **concluir**.

Olá Kit de ferramentas do Azure começa a implantar seu tooAzure de aplicativo web em um contêiner do Docker. 

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá recursos a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [O que há de novo no hello Kit de ferramentas do Azure para Eclipse]
  * [Saudação de instalar o Kit de ferramentas do Azure para Eclipse]
  * [Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]
  * [Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]
* [Kit de Ferramentas do Azure para IntelliJ]
  * [O que há de novo no hello Azure Toolkit for IntelliJ]
  * [Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]
  * [Instruções entrar para hello Azure Toolkit for IntelliJ]
  * [Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]

Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].

Para obter recursos adicionais do Docker, consulte oficial Olá [site Docker].

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instruções entrar para hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[O que há de novo no hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/

[site Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png