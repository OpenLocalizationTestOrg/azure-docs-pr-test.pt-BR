---
title: "Olá de aaaPublish um aplicativo de inicialização de Spring como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse | Microsoft Docs"
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
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Publicar um aplicativo de inicialização de Spring como um contêiner do Docker usando Olá Kit de ferramentas do Azure para Eclipse

Olá [Spring Framework] é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial. Um dos projetos mais populares de saudação que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para criação de aplicativos Java autônomo.

[Docker] é uma solução de software livre que ajuda os desenvolvedores a automatizar a implantação de hello, o dimensionamento e o gerenciamento de seus aplicativos que são executados em contêineres.

Este tutorial orienta Olá etapas toodeploy um aplicativo de inicialização de Spring como um contêiner de Docker tooMicrosoft do Azure usando Olá Kit de ferramentas do Azure para Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>Clonar saudação padrão Spring inicialização Docker repositório

### <a name="import-hello-public-repository"></a>Repositório público de saudação de importação

Olá etapas a seguir orientam você durante a clonagem do computador local do hello Spring inicialização Docker repositório tooyour usando IntelliJ. Se você quiser toouse uma linha de comando, consulte [implantar um aplicativo de inicialização de Spring no Linux no serviço de contêiner do Azure][Deploy Spring Boot on Linux in ACS].

1. Abra o Eclipse.

1. Clique em **Arquivo** > **Importar**.

   ![Menu de Importação de Arquivo][CL01]

1. Olá quando **importação** abre a caixa de diálogo:

   a. Expanda **Git**.

   b. Selecione **Projetos do Git**.
   
   c. Clique em **Avançar**.

   ![Caixa de diálogo de Importação][CL02]

1. Em Olá **Selecionar origem de repositório** página:

   a. Selecione **Clonar URI**.
   
   b. Clique em **Avançar**.

   ![Página Selecionar Origem do Repositório][CL03]

1. Em Olá **repositório Git de origem** página:

   a. Em **URI**, insira `https://github.com/spring-guides/gs-spring-boot-docker.git`. Esta etapa deve preencher automaticamente Olá **Host** e **caminho do repositório** campos com hello corrigir os valores.
   
   b. repositório de inicialização Spring Olá é público, para que você não deve ter tooenter seu nome de usuário do Git e a senha.
   
   c. Clique em **Avançar**.

   ![Página Repositório Git de Origem][CL04]

1. Em Olá **seleção ramificação** , clique em **próximo**.

   ![Página Seleção de Branch][CL05]

1. Em Olá **destino Local** página:

   a. Especifique Olá pasta local onde você deseja que seu repositório local.
   
   b. Clique em **Avançar**.

   ![Página Destino Local][CL06]

1. Em Olá **selecione toouse um Assistente para importar projetos** página:

   a. Selecione **Importar como um projeto geral**.
   
   b. Clique em **Avançar**.

   ![Página "Selecionar toouse um Assistente para importar projetos"][CL07]

1. Em Olá **importar projetos** página:

   a. Especifique o nome do projeto.
   
   b. Clique em **Concluir**.

   ![Página Importar Projetos][CL08]

1. Quando o repositório Olá for clonado com êxito, você verá todos os arquivos de saudação listados no Eclipse.

   ![Repositório local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Criar um projeto do Maven por meio do repositório local

repositório de Spring inicialização Docker Olá contém um projeto Maven completo, que você usará para este tutorial. 

1. Clique em **Arquivo** > **Importar**.

   ![Comando no menu de arquivo hello importar][CL01]

1. Olá quando **importação** abre a caixa de diálogo:

   a. Expanda **Maven**.
   
   b. Selecione **Projetos Existentes do Maven**.
   
   c. Clique em **Avançar**.

   ![Caixa de diálogo de Importação][MV01]

1. Em Olá **projetos Maven** página:

   a. Para **diretório raiz**, especifique Olá **completa** pasta no seu repositório local.
   
   b. Expanda Olá **avançado** seção e insira um nome personalizado para **modelo de nome**.
   
   c. Caixa de seleção Olá Olá **pom.xml** arquivo no projeto de saudação.
   
   d. Clique em **Concluir**.

   ![Página Projetos do Maven][MV02]

1. Quando o projeto Maven Olá é aberto com êxito, você verá um segundo projeto listado no Eclipse.

   ![Projeto do Maven local][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Criar o aplicativo Spring Boot usando o Maven

1. No hello Explorador de projeto do Eclipse, selecione o projeto Maven hello.

1. Clique em **Executar** > **Executar Como** > **Build do Maven**.

   ![Comandos toorun como build Maven][BU01]

1. Quando seu aplicativo é criado com êxito, a janela do console de saudação mostra o status de saudação.

   ![Build bem-sucedido do Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar seu tooAzure de aplicativo web usando um contêiner do Docker

1. No hello Explorador de projeto do Eclipse, selecione o projeto Maven hello.

1. Clique em hello Azure **publicar** menu e clique **Publicar como contêiner Docker**.

   ![Comando Publicar como Contêiner do Docker][PU01]

1. Olá quando **implantação de contêiner do Docker no Azure** caixa de diálogo aparece:

   a. Insira um nome de imagem do Docker personalizado.
   
   b. Para **artefato toodeploy**, especifique Olá caminho toohello **gs-spring-inicialização-docker-0.1.0.jar** arquivo que você acabou de criar.

   ![Especificar opções do Docker][PU02]

   Os hosts existentes do Docker são exibidos. 

1. Se você escolher toodeploy tooan do host existente, você poderá ignorar toostep 5. Caso contrário, use Olá etapas toocreate um host a seguir:

   a. Clique em **Adicionar**.

      ![Adicionar um novo host do Docker][PU03]

   b. Olá quando **criar Host do Docker** caixa de diálogo é exibida, você pode escolher os padrões de saudação tooaccept ou você pode especificar quaisquer configurações personalizadas para o novo host do Docker. (Para obter descrições detalhadas de saudação várias configurações, consulte [publicar um aplicativo web como um contêiner do Docker usando Olá Kit de ferramentas do Azure para IntelliJ][Publish Container with Azure Toolkit].) Clique em **próximo** quando você especificou qual toouse configurações.

      ![Especificar opções de host do Docker][PU04]

   c. Você pode escolher toouse credenciais de logon existente de um cofre de chaves do Azure, ou você pode escolher tooenter novas credenciais de logon do Docker. Clique em **Concluir** quando tiver especificado suas opções.

      ![Especificar as credenciais de host do Docker][PU05]

1. Selecione o host do Docker e, em seguida, clique em **Avançar**.

   ![Selecione toouse de host do Docker][PU06]

1. Na última página Olá Olá **implantação de contêiner do Docker no Azure** caixa de diálogo, especifique Olá as opções a seguir:

   a. Você pode escolher um nome personalizado para o contêiner de saudação que hospedará o contêiner do Docker toospecify, ou você pode aceitar o padrão de saudação.

   b. Insira as portas TCP Olá para o host do docker usando Olá sintaxe a seguir: *[porta externa]*:*[porta interna]*. Por exemplo, **80:8080** Especifica uma porta externa de 80 e saudação padrão interno Spring inicialização porta 8080.
   
      Se você tiver personalizado sua porta interna (por exemplo, editando o arquivo de application.yml Olá), você precisa número da porta toospecify Olá para Olá toooccur correto de roteamento no Azure.

   c. Depois de configurar essas opções, clique em **Concluir**.

   ![Implantar um contêiner do Docker no Azure][PU07]

1. Quando termina a publicação Olá Kit de ferramentas do Azure, Olá exibe o Log de atividades do Azure **publicado** status hello.

   ![Host do Docker implantado com êxito][PU08]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring inicialização]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
