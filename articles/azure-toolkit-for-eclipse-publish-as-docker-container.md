---
title: "Publicar um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse | Microsoft Docs"
description: "Saiba como publicar um aplicativo Web para o Microsoft Azure como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse."
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
ms.openlocfilehash: 746bb0a073396b84fa8592adda6748a2a5692ee8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Publicar um aplicativo Web como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse

Contêineres do Docker são um método amplamente usado para implantar aplicativos Web. Com os contêineres do Docker, os desenvolvedores podem consolidar todos os arquivos de projeto e dependências em um único pacote para implantação em um servidor. O Kit de Ferramentas do Azure para Eclipse simplifica o processo para desenvolvedores de Java adicionando recursos de *Publicar como Contêiner do Docker* para implantação no Microsoft Azure. Este artigo explica as etapas necessárias para publicar seus aplicativos no Azure como contêineres do Docker.

> [!NOTE]
> Saiba mais sobre o Docker no [site do Docker].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publicar seu aplicativo Web no Azure usando um contêiner do Docker

1. Abra seu projeto de aplicativo Web no Eclipse.

2. Para iniciar o assistente **Publicar como Contêiner do Docker**, execute um dos seguintes procedimentos:

   * Na exibição **Navegador**, clique com o botão direito do mouse em seu projeto, clique em **Azure** e clique em **Publicar como Contêiner do Docker**.

      ![Comando Publicar como Contêiner do Docker da exibição Navegador][PUB01]

   * Na barra de ferramentas do Eclipse, clique no botão **Publicar** e clique em **Publicar como Contêiner do Docker**.

      ![Comando Publicar como Contêiner do Docker da barra de ferramentas do Eclipse][PUB02]
      
    O assistente para **Implantar Contêiner do Docker no Azure** é aberto.

    ![O assistente para Implantar o Contêiner do Docker no Azure][PUB03]

3. Na janela **Digite um nome de imagem, selecione o caminho do artefato e marque um host do Docker a ser usado**, faça o seguinte:

    a. Na caixa **Nome da imagem do Docker**, insira um nome exclusivo para o host do Docker. (O assistente cria automaticamente um nome, mas você pode modificá-lo.)

    b. A área **Hosts** exibe quaisquer hosts do Docker que você já criou. Faça uma das opções a seguir:

    * Se você tiver um host do Docker existente, poderá implantar seu aplicativo Web nele.
    * Para criar um novo host do Docker, clique em **Adicionar**.  
      
    A caixa de diálogo **Criar Host do Docker** é aberta.

    ![Assistente para Implantar o Contêiner do Docker no Azure][PUB04a]

4. Na janela **Configurar a nova máquina virtual**, especifique as seguintes opções para o host do Docker. (O assistente gera automaticamente a maioria das opções para você, mas você pode modificar qualquer uma delas.)

   a. **Nome**: insira um nome exclusivo para o host do Docker. (Não é o mesmo que o nome da imagem do Docker que você especificou anteriormente.)

   b. **Assinatura**: insira a assinatura do Azure que você usa para o host.

   c. **Região**: insira a região geográfica na qual o host está localizado.

   d. Na guia **Sistema Operacional de Host e Tamanho**:
     * **Sistema Operacional de Host**: insira o sistema operacional da máquina virtual que contém seu host.
     * **Tamanho**: insira o tamanho da máquina virtual de seu host.

   e. Na guia **Grupo de Recursos**:
     * **Novo grupo de recursos**: crie um novo grupo de recursos para o host.
     * **Grupo de recursos existente**: insira um grupo de recursos existente de sua conta do Azure.

   f. Na guia **Rede**:
     * **Nova rede virtual**: crie uma nova rede virtual para o host.
     * **Rede virtual existente**: insira uma rede virtual existente de sua conta do Azure.

   g. Sobre na guia **Armazenamento**:
     * **Nova conta de armazenamento**: crie uma nova conta de armazenamento para o host.
     * **Conta de armazenamento existente**: insira uma conta de armazenamento existente da sua conta do Azure.

5. Clique em **Avançar**.

6. Na janela **Configurar credenciais de logon e configurações de porta**, selecione uma das opções a seguir:

    * **Importar credenciais do Azure Key Vault**: especifica um conjunto de credenciais salvas anteriormente que são armazenadas em sua assinatura do Azure.

      >[!NOTE]
      >Um Azure Key Vault que é criado com uma conta ou entidade de serviço específica não poderá ser acessado automaticamente por outra conta ou entidade de serviço que compartilhe a assinatura. Para permitir que outra conta ou entidade de serviço use o Key Vault, você deve usar o Portal do Azure para adicionar a conta ou a entidade de serviço.

    * **Novas credenciais de logon**: cria um novo conjunto de credenciais de logon. Se você selecionar essa opção, faça o seguinte:
    
      * Na guia **Credenciais de VM**, escolha uma das opções a seguir para as credenciais de logon de máquina virtual do host do Docker:

          * **Nome de usuário**: insira o nome de usuário para as credenciais de logon de máquina virtual.
          * **Senha** e **Confirmar**: especifica a senha para as credenciais de logon da máquina virtual.
          * **SSH**: insira as configurações de SSH (Secure Shell) para o host do Docker. É possível escolher um das seguintes opções:
            * **Nenhum**: especifica que a sua máquina virtual não permitirá conexões SSH.
            * **Gerar automaticamente**: cria automaticamente as configurações necessárias para conectar-se via SSH.
            * **Importar do diretório**: especifica um diretório que contém um conjunto de configurações de SSH salvas anteriormente. O diretório deve conter os dois arquivos a seguir:
                * *id_rsa*: contém a identificação da RSA para um usuário.
                * *id_rsa.pub*: contém a chave pública RSA que é usada para autenticação.
        
        ![Criar host do Docker][PUB05]

      * Na guia **Credenciais de Daemon do Docker**, especifique as seguintes opções:

          * **Porta de Daemon do Docker**: insira a porta TCP exclusiva para o host do Docker.
          * **Segurança de TLS**: insira as configurações de protocolo TLS para o host do Docker. É possível escolher um das seguintes opções:
            * **Nenhum**: especifica que a sua máquina virtual não permitirá conexões TLS.
            * **Gerar automaticamente**: cria automaticamente as configurações necessárias para conectar-se via TLS.
            * **Importar do diretório**: especifica um diretório que contém um conjunto de configurações de TLS salvas anteriormente. Mais especificamente, o diretório deve conter os seis arquivos a seguir:
                * *ca.pem* e *ca-key.pem*: contêm o certificado e a chave pública da autoridade de certificado TLS.
                * *cert.pem* e *key.pem*: contêm o certificado do cliente e a chave pública que é usada para autenticação TLS.
                * *server.pem* e *server-key.pem*: contêm o certificado do servidor e a chave pública para o host.

        ![Criar host do Docker][PUB06]

7. Depois de inserir todas as informações anteriores, clique em **Concluir**.

8. No assistente **Implantar Contêiner do Docker no Azure**, clique em **Avançar**.

   ![O assistente para Implantar o Contêiner do Docker no Azure][PUB07]

9. Na janela **Configurar o contêiner do Docker a ser criado**, faça o seguinte:

   a. Na caixa **Nome do contêiner do Docker**, insira um nome exclusivo do contêiner do Docker.

   b. Escolha uma das seguintes imagens do Docker:
     * **Imagem do Docker predefinida**: especifica uma imagem já existente do Docker do Azure.

       >[!NOTE]
       >A lista de imagens do Docker nessa caixa é composta por várias imagens às quais o Kit de Ferramentas do Azure foi configurado para aplicar patches, de modo que o artefato seja implantado automaticamente.

     * **Dockerfile personalizado**: especifica um Dockerfile salvo anteriormente do computador local.

       >[!NOTE]
       >Esse é um recurso mais avançado para desenvolvedores que desejam implantar um Dockerfile próprio. No entanto, cabe aos desenvolvedores que usam essa opção garantir que o Dockerfile seja compilado corretamente. O Kit de ferramentas do Azure não valida o conteúdo em um Dockerfile personalizado, portanto, a implantação poderá falhar se o Dockerfile tiver problemas. Além disso, o Kit de Ferramentas do Azure espera que o Dockerfile personalizado contenha um artefato de aplicativo Web e ele tentará abrir uma conexão HTTP. Se os desenvolvedores publicarem um tipo diferente de artefato, eles poderão receber erros inócuos após a implantação.

   c. **Configurações de porta**: insira a associação de porta TCP exclusiva para seu contêiner do Docker.

     ![A janela Configurar o contêiner do Docker a ser criado][PUB08]

10. Depois de concluir todas as etapas anteriores, clique em **Concluir**.

O Kit de ferramentas do Azure começa a implantar seu aplicativo Web no Azure em um contêiner do Docker. 

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
  * [Criar um aplicativo Web Hello World para o Azure no IntelliJ]

Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].

Para obter recursos adicionais para o Docker, consulte o [site do Docker] oficial.

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalação do Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de entrada para o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Kit de Ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/

[site do Docker]: https://www.docker.com/

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