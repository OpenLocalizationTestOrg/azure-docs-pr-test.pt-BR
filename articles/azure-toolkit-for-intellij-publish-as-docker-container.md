---
title: "aaaPublish um contêiner do Docker usando hello Kit de ferramentas do Azure para IntelliJ | Microsoft Docs"
description: "Saiba como toopublish uma tooMicrosoft de aplicativo web do Azure como um contêiner do Docker usando hello o Kit de ferramentas do Azure para IntelliJ."
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
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Publicar um aplicativo web como um contêiner do Docker usando Olá Kit de ferramentas do Azure para IntelliJ

Contêineres do Docker são um método amplamente usado para implantar aplicativos Web. Usando contêineres do Docker, os desenvolvedores podem consolidar todos os seus arquivos de projeto e dependências em um único pacote para o servidor de implantação tooa. Olá Kit de ferramentas do Azure para IntelliJ simplifica esse processo para desenvolvedores de Java adicionando *Publicar como contêiner Docker* recursos para tooMicrosoft de implantação do Azure. Este artigo orienta Olá etapas necessárias toopublish tooAzure seus aplicativos como contêineres do Docker.

> [!NOTE]
>
> Para obter mais informações sobre o Docker estão disponíveis no hello [site Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar seu tooAzure de aplicativo web usando um contêiner do Docker

> [!NOTE]
> * toopublish seu aplicativo web, você deve criar um artefato pronto para implantação. toolearn mais, consulte Olá [informações adicionais sobre como criar artefatos](#artifacts) seção.
>
> * Depois de concluir o Assistente de implantação Olá pelo menos uma vez, a maioria de suas configurações é usada como padrões quando você executar novamente o Assistente de saudação.
>

1. Abra seu projeto de aplicativo Web no IntelliJ.

2. Olá toostart **Publicar como contêiner Docker** assistente, faça o seguinte de saudação:

   * Em Olá **projeto** janela de ferramenta, clique com o botão direito, clique em **Azure**e, em seguida, clique em **Publicar como contêiner Docker**:

      ![Olá Publicar como comando contêiner Docker][PUB01]

   * Na barra de ferramentas de IntelliJ Olá, clique em Olá **grupo publicar** botão e, em seguida, clique em **Publicar como contêiner Docker**:

      ![Olá Publicar como comando contêiner Docker][PUB02]  
    Olá **implantar o contêiner do Docker no Azure** assistente é aberto.

   ![Olá implantar o contêiner do Docker no Assistente do Azure][PUB03]

3. Em Olá **digite um nome de imagem, selecione o caminho do artefato hello e verificar um toobe de host do Docker usado** janela, Olá a seguir: 

   a. Em Olá **nome de imagem do Docker** , digite um nome exclusivo para o host do Docker. (Olá criará automaticamente um nome, mas você pode modificá-la.) 

   b. Olá **Hosts** área exibe os hosts de Docker que você criou. Siga um destes procedimentos hello: 
      * Se você tiver um host Docker existente, você pode implantar seu tooit de aplicativo web.
      * Clique em toocreate um host Docker, sinal de adição verde hello (**+**).  
       Olá **criar Host do Docker** caixa de diálogo é aberta. 

      ![Assistente para Implantar o Contêiner do Docker no Azure][PUB04a]

4. Em Olá **configurar nova máquina de virtual Olá** janela, forneça Olá seguintes informações sobre o host do Docker. (Assistente de saudação gera automaticamente a maioria das informações de saudação para você, mas você pode modificar qualquer um deles.) 

   a. Em Olá **nome** , digite um nome exclusivo para o host do Docker hello. (É não Olá mesmo Olá nome de imagem do Docker que você especificou anteriormente.) 
    
   b. Em Olá **assinatura** , digite Olá assinatura do Azure que você usa para o host. 
      
   c. Em Olá **região** , digite região geográfica hello, onde o host está localizado.
      
   d. Em Olá **sistema operacional e o tamanho** guia, Olá a seguir:      
      * **Sistema operacional do host**: insira o sistema operacional de saudação para a máquina virtual Olá que contém seu host. 
      * **Tamanho**: insira o tamanho da máquina virtual Olá para o host.   
       
   e. Em Olá **grupo de recursos** , selecione qualquer um dos seguintes hello:      
      * **Novo grupo de recursos**: crie um grupo de recursos para o host.
      * **Grupo de recursos existente**: especifique um grupo de recursos existente de sua conta do Azure. 
       
   f. Em Olá **rede** , selecione qualquer um dos seguintes hello:      
      * **Nova rede virtual**: crie uma rede virtual para o host.
      * **Rede virtual existente**: especifique uma rede virtual existente de sua conta do Azure. 
       
   g. Em Olá **armazenamento** , selecione qualquer um dos seguintes hello:      
      * **Nova conta de armazenamento**: crie uma conta de armazenamento para o host.
      * **Conta de armazenamento existente**: especifique uma conta de armazenamento existente da sua conta do Azure.
       
5. Clique em **Avançar**.  
     Olá **configurar log de credenciais e configurações de porta** janela será aberta.

      ![log de configurar Olá na janela de configurações de porta e credenciais][PUB05]

6. Selecione uma saudação as opções a seguir:

      * **Importar credenciais do Azure Key Vault**: especifique um conjunto de credenciais que são armazenadas em sua assinatura do Azure salva anteriormente.

          > [!NOTE]
          > Um cofre de chaves do Azure que é criado com uma conta específica ou entidade de serviço não é automaticamente acessível por outra conta ou entidade de serviço que compartilha assinatura hello. tooallow outra chave de conta ou serviço de toouse principal Olá cofre, você deve usar o hello conta de saudação tooadd portal do Azure ou entidade de serviço.

      * **Novas credenciais de logon**: crie um novo conjunto de credenciais de logon. Se você selecionar essa opção, Olá a seguir:

        a. Em Olá **VM credenciais** guia, forneça Olá seguintes informações para as credenciais de logon de máquina virtual de saudação do seu host do Docker: * **Username**: insira o nome de usuário de saudação para seu logon de máquina virtual credenciais.
             * **Senha** e **confirmar**: insira a senha de saudação para suas credenciais de logon de máquina virtual.
             * **SSH**: insira as configurações do hello Secure Shell (SSH) para o host do Docker. Você pode selecionar uma saudação as opções a seguir: * **nenhum**: Especifica que a sua máquina virtual não permite conexões SSH.
                * **Gerar automaticamente**: cria automaticamente Olá configurações necessárias para conectar-se via SSH.
                * **Importar do diretório**: permite que você toospecify um diretório que contém um conjunto de configurações de SSH salvos anteriormente. diretório de saudação deve conter Olá dois arquivos a seguir:
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. Em Olá **Docker Daemon acesso** guia, forneça Olá informações a seguir:

          ![Criar host do Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. Depois que você inseriu as informações de saudação necessárias, clique em **concluir**.  
    Olá **implantar o contêiner do Docker no Azure** assistente será exibida novamente.

   ![Assistente para Implantar o Contêiner do Docker no Azure][PUB07]

8. Clique em **Avançar**.  
    Olá **configurar Olá Docker contêiner toobe criado** janela será aberta.

   ![janela de toobe criado Olá configurar Olá Docker contêiner][PUB08]

9. Em Olá **configurar Olá Docker contêiner toobe criado** janela, forneça Olá informações a seguir: 

   a. Em Olá **nome do contêiner Docker** , digite um nome exclusivo para o contêiner do Docker.

   b. Escolha uma saudação imagens do Docker a seguir: 

      * **Imagem do Docker predefinida**: especifique uma imagem já existente do Docker do Azure. 

        > [!NOTE]
        > Olá lista de imagens do Docker nesta caixa consiste em várias imagens que Olá Kit de ferramentas do Azure foi configurado toopatch de forma que o artefato é implantado automaticamente. 

      * **Dockerfile personalizado**: especifique um Dockerfile salvo anteriormente do computador local.

        > [!NOTE]
        > Esse é um recurso mais avançado para desenvolvedores que querem toodeploy seu próprios Dockerfile. No entanto, ele é toodevelopers que usam essa tooensure de opção seu Dockerfile é criado corretamente. Porque Olá Kit de ferramentas do Azure não validam o conteúdo de saudação em um Dockerfile personalizado, implantação de saudação poderá falhar se Olá Dockerfile tem problemas. Além disso, porque Olá Kit de ferramentas do Azure espera Olá personalizado toocontain de Dockerfile um artefato de aplicativo web, ele tenta tooopen uma conexão HTTP. Se os desenvolvedores publicarem um tipo diferente de artefato, eles poderão receber erros inócuos após a implantação.

   c. Em Olá **as configurações de porta** , digite associação porta TCP de saudação exclusiva para o contêiner do Docker. 

10. Depois de concluir Olá etapas anteriores, clique em **concluir**. 

Olá Kit de ferramentas do Azure começa a implantar seu tooAzure de aplicativo web em um contêiner do Docker. A menos que você configurou toobe IntelliJ implantado no plano de fundo hello, um **Implantando tooAzure** barra de progresso é exibida. 

![barra de progresso de implantação Olá][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Informações adicionais sobre a criação de artefatos

toocreate artefato um pronto para implantação, Olá a seguir:

1. Abra seu projeto de aplicativo Web no IntelliJ.

2. Clique em **Arquivo** e depois em **Estrutura do Projeto**.

   ![Olá comando estrutura do projeto][ART01]

3. tooadd um artefato, clique em sinal de adição verde hello (**+**) e, em seguida, clique em **aplicativo Web: arquivo**.

   ![Olá comando ": arquivo do aplicativo Web"][ART02]

4. Em Olá **nome** , digite um nome para o artefato (não inclua Olá *. war* extensão) e, em seguida, clique em **Okey**.

   ![caixa de nome de artefato Olá][ART03]

Para obter mais informações sobre como criar artefatos no IntelliJ, consulte [Configurando artefatos] no site de JetBrains hello.

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

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].

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

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/

[site Docker]: https://www.docker.com/
[Configurando artefatos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
