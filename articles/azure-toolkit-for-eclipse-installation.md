---
title: "Olá aaaInstalling Kit de ferramentas do Azure para Eclipse | Microsoft Docs"
description: "Saiba como tooinstall Olá Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6c195fab2b47fb5c42541a8cf52be4ec88d27b5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-hello-azure-toolkit-for-eclipse"></a>Saudação de instalar o Kit de ferramentas do Azure para Eclipse
Olá Kit de ferramentas do Azure para Eclipse fornece modelos e funcionalidades que permitem que você tooeasily criam, desenvolver, testar e implantar aplicativos do Azure usando o ambiente de desenvolvimento do Eclipse hello. Olá Kit de ferramentas do Azure para Eclipse é um projeto de código-fonte aberto. Olá código-fonte está disponível sob a licença do MIT de saudação do <https://github.com/microsoft/azure-tools-for-java>.

Olá, as etapas a seguir mostra como tooinstall Olá Kit de ferramentas do Azure para Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="tooinstall-hello-azure-toolkit-for-eclipse"></a>Olá tooinstall Kit de ferramentas do Azure para Eclipse
1. Inicie o Eclipse.
2. Clique em Olá **ajuda** menu e clique **instalar novo Software**, conforme mostrado na ilustração a seguir de saudação.
   
    ![Saudação de instalar o Kit de ferramentas do Azure para Eclipse][01]
3. Em Olá **Software disponível** caixa de diálogo, em Olá **trabalhar com** caixa de texto, digite `http://dl.microsoft.com/eclipse` seguido Olá **Enter** chave.
4. Em Olá **nome** painel, seleção **Kit de ferramentas do Azure para Eclipse**e desmarque **entre em contato com todos os sites de atualização durante instalar software toofind necessária**. Sua tela deve aparecer a seguir toohello semelhante:
   
    ![Saudação de instalar o Kit de ferramentas do Azure para Eclipse][02]
5. Se você expandir Olá **Kit de ferramentas do Azure para Eclipse**, você verá Olá itens a seguir:
   
   * **Plug-in do Application Insights para Java**: esse componente permite que os serviços do Azure toouse registro em log e análise de telemetria para seus aplicativos e instâncias de servidor.
   * **Filtro de serviços de controle de acesso do Azure**: esse componente oferece suporte para autenticação de usuários do aplicativo com o Azure ACS, permitindo cenários de logon único e externalização de lógica de identidade de aplicativo hello.
   * **Azure Common Plugin**: esse componente fornece funcionalidade comum de saudação necessária por outros componentes do Kit de ferramentas.
   * **Pesquisador de objetos do Azure para Eclipse**: esse componente fornece funcionalidade comum de saudação necessária por outros componentes do Kit de ferramentas.
   * **Plug-in do Azure para Eclipse com Java**: esse componente oferece suporte para o desenvolvimento de projetos que ajudam a criar, testar e implantar aplicativos Java para a nuvem do Microsoft Azure Olá no Eclipse e por meio da linha de comando.
   * **Plugin de aplicativos Web do Azure com Java**: esse componente oferece suporte para a implantação dos contêineres de aplicativo Web do Azure tooMicrosoft de aplicativos web Java.
   * **Microsoft JDBC Driver 4.2 para SQL Server**: esse componente fornece a API JDBC para SQL Server e Banco de Dados SQL do Microsoft Azure para Java Platform Enterprise Edition 8.
   * **Pacote para bibliotecas de cliente do Apache Qpid para JMS**: esse componente fornece o componente de cliente JMS Olá da saudação Apache Qpid projeto tooenable seu aplicativo toouse AMQP mensagens no Microsoft Azure.
   * **Pacote para Bibliotecas do Microsoft Azure para Java**: esse componente fornece APIs para acessar serviços do Microsoft Azure, como armazenamento, barramento de serviço, tempo de execução do serviço, etc.
6. Clique em **Avançar**. (Se você enfrentar atrasos incomuns ao instalar o Kit de ferramentas do hello, certifique-se de que **entre em contato com todos os sites de atualização durante instalar software toofind necessário** está desmarcada.)
7. Em Olá **detalhes de instalação** caixa de diálogo, clique em **próximo**.
   
    ![Revisão dos detalhes de instalação][03]
8. Em Olá **analisar licença** caixa de diálogo, leia os termos de Olá Olá de contratos de licença. Se você aceitar os termos de Olá Olá de contratos de licença, clique em **aceito os termos de Olá Olá de contratos de licença** e, em seguida, clique em **concluir**. (etapas restantes Olá supõem que você aceite os termos de Olá Olá de contratos de licença. Se você não aceitar os termos de Olá Olá de contratos de licença, sair do processo de instalação hello.)
   
    ![Examinar Licenças][04]
   
    Eclipse baixará e instalará os pacotes necessários hello.
   
    ![Progresso da Instalação][05]
9. Se solicitado a instalação de toocomplete do toorestart Eclipse, clique em **Sim**.
   
    ![Reinicie o prompt][06]

## <a name="see-also"></a>Consulte também
Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [Novidades no Kit de ferramentas do Azure para Eclipse de saudação]
  * *Saudação de instalar o Kit de ferramentas do Azure para Eclipse (Este artigo)*
  * [Entrada em instruções Olá Kit de ferramentas do Azure para Eclipse]
  * [Criar um aplicativo Web Hello World para o Azure no Eclipse]
* [Kit de Ferramentas do Azure para IntelliJ]
  * [Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]
  * [Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]
  * [Entrada em instruções hello Azure Toolkit for IntelliJ]
  * [Criar um aplicativo Web Hello World para o Azure no IntelliJ]

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Entrada em instruções Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Entrada em instruções hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Kit de ferramentas do Azure para Eclipse de saudação]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
