---
title: aaaWhat do novo no hello Azure Toolkit for IntelliJ | Microsoft Docs
description: "Saiba mais sobre os recursos mais recentes Olá Olá Kit de ferramentas do Azure para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 46ed791f-df59-416a-809e-f52345ad973c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 57599c9af1d41784941b8b363ab9089db5df98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-hello-azure-toolkit-for-intellij"></a>Novidades no Kit de ferramentas do Azure para IntelliJ de saudação
## <a name="azure-toolkit-for-intellij-releases"></a>Lançamentos do Kit de Ferramentas do Azure para IntelliJ
Este artigo contém informações sobre Olá várias versões e atualizações mais recentes toohello Kit de ferramentas do Azure para IntelliJ.

> [!NOTE]
> Também é um kit de ferramentas do Azure para Olá IDE do Eclipse. Para saber mais, confira [Kit de ferramentas do Azure para Eclipse].
> 
> 

### <a name="april-14-2017"></a>14 de abril de 2017
Olá Kit de ferramentas do Azure para IntelliJ - versão de abril de 2017 inclui Olá aprimoramentos a seguir:

* **Entrada do Azure na experiência aprimorada**: Olá Kit de ferramentas do Azure para IntelliJ agora oferece suporte a dois métodos para fazer logon em sua conta do Azure: *interativo* e *automatizada*. Para obter mais informações, consulte [Azure sinal em instruções para hello Azure Toolkit for IntelliJ].
* **Publicando usando contêineres do Docker**: agora você pode publicar seus aplicativos Web como contêineres do Docker usando o Kit de ferramentas do Azure para IntelliJ. Para obter mais informações, consulte [como toopublish um aplicativo da Web como um contêiner do Docker usando hello o Kit de ferramentas do Azure para IntelliJ].
* **Gerenciamento de conta de armazenamento**: Olá Kit de ferramentas do Azure para IntelliJ agora dá suporte ao gerenciamento de suas contas de armazenamento de saudação exibição do Explorer do Azure. Para obter mais informações, consulte [Gerenciando contas de armazenamento usando hello Azure Explorer para IntelliJ].
* **Gerenciamento de máquinas virtuais**: Olá Kit de ferramentas do Azure para IntelliJ agora dá suporte a gerenciar as máquinas virtuais de saudação janela de ferramentas do Pesquisador de objetos do Azure. Para obter mais informações, consulte [Gerenciando máquinas virtuais usando hello Azure Explorer para IntelliJ].
* **Remoção de suporte a depuração remota**. Depuração remota de aplicativos da web de Java no serviço de aplicativo do Azure foi removido do hello Kit de ferramentas do Azure para IntelliJ; foi necessário tooresolve alguns problemas que os clientes que enfrentávamos ao usar o hello Kit de ferramentas.

### <a name="august-26-2016"></a>26 de agosto de 2016
Olá Kit de ferramentas do Azure para IntelliJ - versão de agosto de 2016 inclui Olá aprimoramentos a seguir:

* **Distribuições personalizadas do JDK**. Olá Kit de ferramentas do Azure para IntelliJ agora dá suporte a especificação e implantar um contêiner de Azure WebApp tooyour arbitrário JDK versão:
  * Além disso toohello JDKs fornecida pelo Azure, também é possível de uma ampla seleção de Zulu OpenJDK versões disponibilizadas no Azure por sistemas Azul.
  * Você também pode especificar sua distribuição JDK, se você carregá-lo como uma conta de armazenamento do tooyour de arquivo ZIP.
* **Aprimoramentos toohello exibição do Explorer do Azure**:
  * Suporte para gerenciamento de máquina Virtual usando o novo modelo de Gerenciador de recursos do Azure: listar, criar e excluir as máquinas virtuais com base no Gerenciador de recursos sem deixar Olá IDE.
  * Suporte para gerenciamento de blob de conta de armazenamento usando o Gerenciador de recursos do Azure, que complementa a funcionalidade existente para gerenciar contas de armazenamento "clássico" hello.
* **Microsoft JDBC Driver 6.0 para SQL Server**. Esta atualização inclui o driver JDBC mais recente de saudação do Microsoft SQL Server (v 6.0), que agora é incluída como uma biblioteca que você pode facilmente adicionar projetos Java tooyour, assim, substituindo a versão mais antiga do hello.

### <a name="june-29-2016"></a>29 de junho de 2016
Olá Kit de ferramentas do Azure para IntelliJ - versão de junho de 2016 inclui Olá aprimoramentos a seguir:

* **Requisito do Java 8**. Olá Kit de ferramentas do Azure para IntelliJ agora requer Java 8, embora esse requisito é somente para o Kit de ferramentas de saudação - seus aplicativos podem continuar toouse todas as versões do Java que são suportadas pelo Azure.
* **Suporte para Olá JDKs mais recente do Java**. Agora há suporte para versões mais recentes de saudação do hello JDKs de Java por Olá Kit de ferramentas do Azure para IntelliJ.
* **Suporte para o SDK do Azure v2.9.1**. versão mais recente de saudação do hello SDK do Azure agora é Olá mínimo pré-requisitos para hello Azure Toolkit for IntelliJ.
* **Exemplos Integrados**. Olá Kit de ferramentas do Azure para IntelliJ agora apresenta vários aplicativos de exemplo que os desenvolvedores de toohelp começar.
* **Integração de Ferramentas HDInsight**. Ferramentas do HDInsight do Azure agora estão incluídas Olá Kit de ferramentas do Azure para IntelliJ. Para obter mais informações, consulte [Plug-in das Ferramentas do HDInsight para IntelliJ].
* **Depuração remota de aplicativos Web do Java**. Olá Kit de ferramentas do Azure para IntelliJ agora dá suporte a depuração remota dos aplicativos web Java do serviço de aplicativo do Azure.

### <a name="april-12-2016"></a>12 de abril de 2016
Olá Kit de ferramentas do Azure para IntelliJ - versão de abril de 2016 inclui Olá aprimoramentos a seguir:

* **Suporte para o SDK do Azure v2.9.0**. versão mais recente de saudação do hello SDK do Azure agora é Olá mínimo pré-requisitos para hello Azure Toolkit for IntelliJ.
* **Diversos aprimoramentos de usabilidade, o desempenho e capacidade de resposta relacionados ao suporte de aplicativo Web tooAzure**. Um número de otimizações de desempenho em como Olá Toolkit se comunica com o resultado do Azure em uma interface de usuário mais ágil na resposta.
* **Capacidade toodelete um contêiner existente do aplicativo Web no Azure de dentro de IntelliJ**. Olá Kit de ferramentas do Azure para IntelliJ agora permite que você toodelete um contêiner da Web do Azure existente sem deixar IntelliJ.

## <a name="see-also"></a>Consulte também
Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [Novidades no Kit de ferramentas do Azure para Eclipse de saudação]
  * [Saudação de instalar o Kit de ferramentas do Azure para Eclipse]
  * [Criar um aplicativo Web Hello World para o Azure no Eclipse]
  * [Entrada em instruções Olá Kit de ferramentas do Azure para Eclipse]
* [Kit de Ferramentas do Azure para IntelliJ]
  * *Novidades no hello Azure Toolkit for IntelliJ (Este artigo)*
  * [Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]
  * [Entrada em instruções hello Azure Toolkit for IntelliJ]
  * [Criar um aplicativo Web Hello World para o Azure no IntelliJ]

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Entrada em instruções Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Entrada em instruções hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Kit de ferramentas do Azure para Eclipse de saudação]: ./azure-toolkit-for-eclipse-whats-new.md
[What's New in hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure sinal em instruções para hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[como toopublish um aplicativo da Web como um contêiner do Docker usando hello o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Gerenciando contas de armazenamento usando hello Azure Explorer para IntelliJ]: ./azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer.md
[Gerenciando máquinas virtuais usando hello Azure Explorer para IntelliJ]: ./azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer.md

[Centro de desenvolvedores de Java do Azure]: http://go.microsoft.com/fwlink/?LinkID=699547

[Plug-in das Ferramentas do HDInsight para IntelliJ]: ./hdinsight/hdinsight-apache-spark-intellij-tool-plugin.md
