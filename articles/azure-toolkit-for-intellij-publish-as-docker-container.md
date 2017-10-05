---
title: "Publicar um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ | Microsoft Docs"
description: "Saiba como publicar um aplicativo Web para o Microsoft Azure como um contêiner do Docker usando o Kit de ferramentas do Azure para IntelliJ."
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
ms.openlocfilehash: 96680319a6c4c0f0a4673cd6303a5b172f428797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Publicar um aplicativo Web como um contêiner do Docker usando o Kit de ferramentas do Azure para IntelliJ

Contêineres do Docker são um método amplamente usado para implantar aplicativos Web. Com os contêineres do Docker, os desenvolvedores podem consolidar todos os arquivos de projeto e dependências em um único pacote para implantação em um servidor. O Kit de Ferramentas do Azure para IntelliJ simplifica o processo para desenvolvedores de Java adicionando recursos de *Publicar como Contêiner do Docker* para implantação no Microsoft Azure. Este artigo explica as etapas necessárias para publicar seus aplicativos no Azure como contêineres do Docker.

> [!NOTE]
>
> Saiba mais sobre o Docker no [site do Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publicar seu aplicativo Web no Azure usando um contêiner do Docker

> [!NOTE]
> * Para publicar seu aplicativo Web, é necessário criar um artefato pronto para implantação. Para saber mais, confira a seção [Informações adicionais sobre a criação de artefatos](#artifacts).
>
> * Depois de concluir o assistente de implantação pelo menos uma vez, a maioria de suas configurações é usada como padrão na próxima execução do assistente.
>

1. Abra seu projeto de aplicativo Web no IntelliJ.

2. Para iniciar o assistente **Publicar como Contêiner do Docker**, execute um dos seguintes procedimentos:

   * Na janela de ferramentas **Projeto**, clique com o botão direito em seu projeto, clique em **Azure** e clique em **Publicar como Contêiner do Docker**:

      ![O comando Publicar como Contêiner do Docker][PUB01]

   * Na barra de ferramentas do IntelliJ, clique no botão **Publicar Grupo** e clique em **Publicar como Contêiner do Docker**:

      ![O comando Publicar como Contêiner do Docker][PUB02]  
    O assistente para **Implantar Contêiner do Docker no Azure** é aberto.

   ![O assistente para Implantar o Contêiner do Docker no Azure][PUB03]

3. Na janela **Digite um nome de imagem, selecione o caminho do artefato e marque um host do Docker a ser usado**, faça o seguinte: 

   a. Na caixa **Nome da imagem do Docker**, insira um nome exclusivo para o host do Docker. (O assistente cria automaticamente um nome, mas você pode modificá-lo.) 

   b. A área **Hosts** exibe quaisquer hosts do Docker que você já criou. Faça uma das opções a seguir: 
      * Se você tiver um host do Docker existente, poderá implantar seu aplicativo Web nele.
      * Para criar um host do Docker, clique no sinal de adição verde (**+**).  
       A caixa de diálogo **Criar Host do Docker** é aberta. 

      ![Assistente para Implantar o Contêiner do Docker no Azure][PUB04a]

4. Na janela **Configurar a nova máquina virtual**, forneça as seguintes informações sobre o host do Docker. (O assistente gera automaticamente a maioria das informações para você, mas você pode modificar qualquer uma delas.) 

   a. Na caixa **Nome**, insira um nome exclusivo para o host do Docker. (Não é o mesmo que o nome da imagem do Docker que você especificou anteriormente.) 
    
   b. Na caixa **Assinatura**, insira a assinatura do Azure que você usa para o host. 
      
   c. Na caixa **Região**, insira a região geográfica na qual o host está localizado.
      
   d. Na guia **Sistema Operacional e Tamanho**, faça o seguinte:      
      * **Sistema Operacional de Host**: insira o sistema operacional da máquina virtual que contém seu host. 
      * **Tamanho**: insira o tamanho da máquina virtual de seu host.   
       
   e. Na guia **Grupo de Recursos**, selecione uma das opções a seguir:      
      * **Novo grupo de recursos**: crie um grupo de recursos para o host.
      * **Grupo de recursos existente**: especifique um grupo de recursos existente de sua conta do Azure. 
       
   f. Na guia **Rede**, selecione uma das opções a seguir:      
      * **Nova rede virtual**: crie uma rede virtual para o host.
      * **Rede virtual existente**: especifique uma rede virtual existente de sua conta do Azure. 
       
   g. Na guia **Armazenamento**, selecione uma das opções a seguir:      
      * **Nova conta de armazenamento**: crie uma conta de armazenamento para o host.
      * **Conta de armazenamento existente**: especifique uma conta de armazenamento existente da sua conta do Azure.
       
5. Clique em **Avançar**.  
     A janela **Configurar credenciais de logon e configurações de porta** é aberta.

      ![A janela Configurar credenciais de logon e configurações de porta][PUB05]

6. Selecione uma das seguintes opções:

      * **Importar credenciais do Azure Key Vault**: especifique um conjunto de credenciais que são armazenadas em sua assinatura do Azure salva anteriormente.

          > [!NOTE]
          > Um Azure Key Vault que é criado com uma conta ou entidade de serviço específica não poderá ser acessado automaticamente por outra conta ou entidade de serviço que compartilhe a assinatura. Para permitir que outra conta ou entidade de serviço use o Key Vault, você deve usar o Portal do Azure para adicionar a conta ou a entidade de serviço.

      * **Novas credenciais de logon**: crie um novo conjunto de credenciais de logon. Se você selecionar essa opção, faça o seguinte:

        a. Na guia **Credenciais de VM** forneça as seguintes informações para as credenciais de logon da máquina virtual de seu host do Docker: * **Nome de usuário**: insira o nome de usuário para as credenciais de logon da máquina virtual.
             * **Senha** e **Confirmar**: especifica a senha para as credenciais de logon da máquina virtual.
             * **SSH**: insira as configurações de SSH (Secure Shell) para o host do Docker. Você pode selecionar uma das seguintes opções: * **Nenhum** : especifica que a sua máquina virtual não permite conexões SSH.
                * **Gerar automaticamente**: cria automaticamente as configurações necessárias para conectar-se via SSH.
                * **Importar do diretório**: permite que você especifique um diretório que contém um conjunto de configurações de SSH salvas anteriormente. O diretório deve conter os dois arquivos a seguir:
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        b. Na guia **Acesso ao Daemon do Docker** forneça as seguintes informações:

          ![Criar host do Docker][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. Depois de inserir as informações necessárias, clique em **Concluir**.  
    O assistente para **Implantar Contêiner do Docker no Azure** é aberto novamente.

   ![Assistente para Implantar o Contêiner do Docker no Azure][PUB07]

8. Clique em **Avançar**.  
    A janela **Configurar o contêiner do Docker a ser criado** é aberta.

   ![A janela Configurar o contêiner do Docker a ser criado][PUB08]

9. Na janela **Configurar o contêiner do Docker a ser criado**, forneça as seguintes informações: 

   a. Na caixa **Nome do contêiner do Docker**, insira um nome exclusivo do contêiner do Docker.

   b. Escolha uma das seguintes imagens do Docker: 

      * **Imagem do Docker predefinida**: especifique uma imagem já existente do Docker do Azure. 

        > [!NOTE]
        > A lista de imagens do Docker nessa caixa é composta por várias imagens às quais o Kit de Ferramentas do Azure foi configurado para aplicar patches, de modo que o artefato seja implantado automaticamente. 

      * **Dockerfile personalizado**: especifique um Dockerfile salvo anteriormente do computador local.

        > [!NOTE]
        > Essa é uma funcionalidade mais avançada para desenvolvedores que desejam implantar um Dockerfile próprio. No entanto, cabe aos desenvolvedores que usam essa opção garantir que o Dockerfile seja compilado corretamente. Como o Kit de Ferramentas do Azure não valida o conteúdo em um Dockerfile personalizado, a implantação pode falhar se o Dockerfile tiver problemas. Além disso, como o Kit de Ferramentas do Azure espera que o Dockerfile personalizado contenha um artefato de aplicativo Web, ele tenta abrir uma conexão HTTP. Se os desenvolvedores publicarem um tipo diferente de artefato, eles poderão receber erros inócuos após a implantação.

   c. Na caixa **Configurações de porta**, insira a associação de porta TCP exclusiva para seu contêiner do Docker. 

10. Depois de concluir as etapas anteriores, clique em **Concluir**. 

O Kit de ferramentas do Azure começa a implantar seu aplicativo Web no Azure em um contêiner do Docker. A menos que você tenha configurado o IntelliJ para ser implantado em segundo plano, uma barra de progresso **Implantação no Azure** é exibida. 

![A barra de progresso da implantação][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Informações adicionais sobre a criação de artefatos

Para criar um artefato pronto para implantação, faça o seguinte:

1. Abra seu projeto de aplicativo Web no IntelliJ.

2. Clique em **Arquivo** e depois em **Estrutura do Projeto**.

   ![O comando Estrutura do Projeto][ART01]

3. Para adicionar um artefato, clique no sinal de adição verde (**+**) e clique em **Aplicativo Web: Arquivo**.

   ![O comando "Aplicativo Web: Arquivo"][ART02]

4. Na caixa **Nome**, insira um nome para o artefato (não inclui a extensão *.war*) e clique em **OK**.

   ![A caixa Nome do artefato][ART03]

Para saber mais sobre como criar artefatos no IntelliJ, consulte [Configurar artefatos] no site da JetBrains.

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre os kits de ferramentas do Azure para Java IDEs, confira os recursos a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [Novidades no Kit de Ferramentas do Azure para Eclipse]
  * [Instalação do Kit de Ferramentas do Azure para o Eclipse]
  * [Instruções de entrada para o Kit de ferramentas do Azure para Eclipse]
  * [Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]
* [Kit de Ferramentas do Azure para IntelliJ]
  * [Novidades no Kit de Ferramentas do Azure para IntelliJ]
  * [Instalação do Kit de Ferramentas do Azure para IntelliJ]
  * [Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]
  * [Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]

Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].

Para obter recursos adicionais para o Docker, consulte o [site do Docker] oficial.

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalação do Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de entrada para o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Kit de Ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/

[site do Docker]: https://www.docker.com/
[Configurar artefatos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

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
