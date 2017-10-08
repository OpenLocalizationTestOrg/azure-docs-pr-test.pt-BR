---
title: "um aplicativo de inicialização Spring como um contêiner do Docker por meio de aaaPublish hello Kit de ferramentas do Azure para IntelliJ | Microsoft Docs"
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
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Publicar um aplicativo de inicialização de Spring como um contêiner do Docker usando Olá Kit de ferramentas do Azure para IntelliJ

Olá [Spring Framework] é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial. Um dos projetos mais populares de saudação que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para criação de aplicativos Java autônomo.

[Docker] é uma solução de software livre que ajuda os desenvolvedores a automatizar a implantação de hello, o dimensionamento e o gerenciamento de seus aplicativos que são executados em contêineres.

Este tutorial orienta Olá etapas toodeploy um aplicativo de inicialização de Spring como um contêiner de Docker tooMicrosoft do Azure usando Olá Kit de ferramentas do Azure para IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a>Clone saudação padrão Spring inicialização Docker repositório

Olá seguinte orientá-lo através da clonagem do repositório de Spring inicialização Docker hello usando IntelliJ. Se você quiser toouse uma linha de comando, consulte [implantar um aplicativo de inicialização de Spring no Linux no serviço de contêiner do Azure][Deploy Spring Boot on Linux in ACS].

1. Abra o IntelliJ.

1. Na tela de boas-vindas hello, selecione Olá **GitHub** opção Olá **Check-out do controle de versão** lista.

   ![Opção do GitHub para controle de versão][CL01]

1. Se você for solicitado toolog em, insira suas credenciais.

   * Se você estiver usando um nome de usuário/senha toolog em tooGitHub:

      ![Caixa de diálogo para inserir o nome de usuário e a senha do GitHub][CL02a]

   * Se você estiver usando um token toolog em tooGitHub:

      ![Caixa de diálogo para inserção de um token do GitHub][CL02b]

1. Digite **https://github.com/spring-guides/gs-spring-boot-docker.git** para URL do repositório hello, especifique o caminho local e informações de pasta e, em seguida, clique em **Clone**.

   ![Caixa de diálogo Clonar Repositório][CL03]

1. Quando for solicitado toocreate um projeto IntelliJ, selecione **não**.

   ![Recusar toocreate um projeto IntelliJ][CL04]

1. Na página de boas-vindas hello, clique em **Importar projeto**.

   ![Seleção Importar Projeto][CL05]

1. Localizar Olá caminho onde você clonar o repositório de inicialização Spring Olá, selecione Olá **completa** pasta sob a raiz de saudação e clique **Okey**.

   ![Selecionar uma pasta para importação][CL06]

1. Quando solicitado, selecione **Criar projeto com base nas fontes existentes**.

   ![Opção toocreate um projeto de código-fonte existente][CL07]

1. Especifique o nome do projeto ou aceite o padrão de saudação, verificar Olá caminho correto toohello **completa** pasta e depois clique em **próximo**.

   ![Especifique o nome do projeto Olá][CL08]

1. Personalize quaisquer diretórios para importação e, em seguida, clique em **Próximo**.

   ![Escolher diretórios][CL09]

1. Examine Olá bibliotecas tooimport e, em seguida, clique em **próximo**.

   ![Examine as bibliotecas do projeto][CL10]

1. Examine a estrutura do módulo hello e, em seguida, clique em **próximo**.

   ![Examinar a estrutura do módulo][CL11]

1. Especifique o seu JDK e, em seguida, clique em **Próximo**.

   ![Especificar um JDK][CL12]

1. Clique em **Concluir**.

   ![Botão Concluir][CL13]

IntelliJ importa Olá Spring inicialização aplicativo como um projeto e exibe a estrutura de saudação quando Olá importação foi concluída.

![Aplicativo Spring Boot no IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Criar seu aplicativo Spring Boot

### <a name="build-hello-app-by-using-hello-maven-pom"></a>Criar o aplicativo hello usando Olá POM Maven

1. Abra a janela da ferramenta Maven Olá se já não estiver aberto. Clique em **Exibir** > **Janelas de Ferramentas** > **Projetos do Maven**.

   ![Comandos da Janela de Ferramentas e Projetos do Maven][BU01]

1. Na janela de ferramenta Maven hello, clique com botão direito **pacote** e selecione **executar Maven criar**. (Se seu projeto Maven não aparecer automaticamente, clique em Olá **reimportar** ícone na barra de ferramentas do hello Maven.)

   ![Executar o comando de Build do Maven][BU02]

1. O IntelliJ deverá exibir uma mensagem **ÊXITO NO BUILD** quando o aplicativo Spring Boot for criado com êxito.

   ![Mensagem ÊXITO NO BUILD][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Criar um artefato pronto para implantação

toopublish seu aplicativo de inicialização de Spring, você precisa toocreate um artefato pronto para implantação. Olá Use as etapas a seguir:

1. Abra seu projeto de aplicativo Web no IntelliJ.

1. Clique em **Arquivo** e depois em **Estrutura do Projeto**.

   ![Comando Estrutura do Projeto][ART01]

1. Clique em Olá verde mais (**+**) tooadd um artefato do símbolo, clique em **JAR**e, em seguida, clique em **vazio**.

   ![Adicionar um artefato][ART02]

1. Nome de seu artefato enquanto se certifica-se de que não tooadd Olá ". jar" extensão e especifique a pasta de destino de saudação para Olá Maven de saída.

   ![Especificar as propriedades do artefato][ART03]

1. Crie um manifesto para o artefato (opcional):

   a. Clique em **Criar Manifesto**.

      ![Botão Olá criar manifesto][ART04a]

   b. Escolha saudação padrão caminho para artefato hello e, em seguida, clique em **Okey**.

      ![Especificar o caminho do artefato][ART04b]

   c. Clique nas reticências da saudação (**...** ) classe principal do toolocate hello.

      ![Localizar a classe principal][ART04c]

   d. Escolha sua classe principal e, em seguida, clique em **OK**.

      ![Especificar a classe principal][ART04d]

1. Clique em **OK**.

   ![Fechar a caixa de diálogo Olá estrutura do projeto][ART05]

> [!NOTE]
> Para obter mais informações sobre como criar artefatos no IntelliJ, consulte [artefatos configurando] no site de JetBrains hello.
>

### <a name="build-hello-artifact-for-deployment"></a>Criar artefato Olá para implantação

1. Clique em **Criar** e, em seguida, clique em **Artefatos**.

   ![Comando Criar Artefatos][BU04]

1. Olá quando **criar artefato** menu de contexto for exibida, clique em **criar**.

   ![Menu de contexto Criar Artefato][BU05]

IntelliJ deve exibir o artefato Olá concluída para o aplicativo de inicialização de Spring na janela de ferramenta do projeto hello.

   ![Artefato criado][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar seu tooAzure de aplicativo web usando um contêiner do Docker

1. Se você não estiver inscrito no tooyour conta do Azure, siga as etapas de saudação em [instruções entrar para hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].

1. Na janela de ferramenta do hello Explorador de projeto, clique com botão direito hello e, em seguida, selecione **Azure** > **Publicar como contêiner Docker**.

   ![Comando Publicar como Contêiner do Docker][PU01]

1. Olá quando **implantar o contêiner do Docker no Azure** caixa de diálogo é exibida, quaisquer hosts de Docker existentes são exibidas. Se você escolher toodeploy tooan do host existente, você poderá ignorar toostep 4. Caso contrário, use Olá etapas toocreate um host a seguir:

   a. Clique em Olá verde mais (**+**) símbolo.

      ![Adicionar um novo host do Docker][PU02]

   b. Olá quando **criar Host do Docker** caixa de diálogo é exibida, você pode escolher os padrões de saudação tooaccept ou você pode especificar quaisquer configurações personalizadas para o novo host do Docker. (Para obter descrições detalhadas de saudação várias configurações, consulte [publicar um aplicativo web como um contêiner do Docker usando Olá Kit de ferramentas do Azure para IntelliJ][Publish Container with Azure Toolkit].) Clique em **próximo** quando você especificou qual toouse configurações.

      ![Especificar opções de host do Docker][PU03a]

   c. Você pode escolher toouse credenciais de logon existente de um cofre de chaves do Azure, ou você pode escolher tooenter novas credenciais de logon do Docker. Clique em **Concluir** quando tiver especificado suas opções.

      ![Especificar as credenciais de host do Docker][PU03b]

1. Selecione o host do Docker e, em seguida, clique em **Avançar**.

   ![Selecione Olá Docker host toouse][PU04]

1. Na última página Olá Olá **implantar o contêiner do Docker no Azure** caixa de diálogo, especifique Olá as opções a seguir:

   a. Você pode escolher um nome personalizado para o contêiner de saudação que hospedará o contêiner do Docker toospecify, ou você pode aceitar o padrão de saudação.

   b. Insira as portas TCP Olá para o host do docker usando Olá sintaxe a seguir: *[porta externa]*:*[porta interna]*. Por exemplo, **80:8080** Especifica uma porta externa de 80 e saudação padrão interno Spring inicialização porta 8080.
   
      Se você tiver personalizado sua porta interna (por exemplo, editando o arquivo de application.yml Olá), você precisa número da porta toospecify Olá para Olá toooccur correto de roteamento no Azure.

   c. Depois de configurar essas opções, clique em **Concluir**.

   ![Implantar um contêiner do Docker no Azure][PU05]

1. Quando termina a publicação Olá Kit de ferramentas do Azure, Olá exibe o Log de atividades do Azure **publicado** status hello.

   ![Host do Docker implantado com êxito][PU06]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

toolearn sobre métodos adicionais para a criação de aplicativos de inicialização Spring usando IntelliJ, consulte [criar projetos de inicialização Spring](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) no site de JetBrains hello.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[artefatos configurando]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring inicialização]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
