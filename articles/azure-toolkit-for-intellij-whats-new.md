---
title: Novidades do Kit de Ferramentas do Azure para IntelliJ | Microsoft Docs
description: Saiba mais sobre os recursos mais recentes do Kit de Ferramentas do Azure para IntelliJ.
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
ms.openlocfilehash: 23714856f0f778be04cf321e0726b53ade430f57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-intellij"></a>Novidades no Kit de Ferramentas do Azure para IntelliJ
## <a name="azure-toolkit-for-intellij-releases"></a>Lançamentos do Kit de Ferramentas do Azure para IntelliJ
Este artigo contém informações sobre as várias versões e atualizações mais recentes do Kit de Ferramentas do Azure para IntelliJ.

> [!NOTE]
> Há também um kit de ferramentas do Azure para o Eclipse IDE. Para saber mais, confira [Kit de ferramentas do Azure para Eclipse].
> 
> 

### <a name="april-14-2017"></a>14 de abril de 2017
O Kit de Ferramentas do Azure para IntelliJ, versão de abril de 2017, inclui as seguintes melhorias:

* **Experiência aprimorada de entrada no Azure**: o Kit de Ferramentas do Azure para IntelliJ agora dá suporte a dois métodos para fazer logon em sua conta do Azure: *Interativo* e *Automatizado*. Para obter mais informações, consulte [Instruções de entrada no Azure para o Kit de Ferramentas do Azure para IntelliJ].
* **Publicando usando contêineres do Docker**: agora você pode publicar seus aplicativos Web como contêineres do Docker usando o Kit de ferramentas do Azure para IntelliJ. Para obter mais informações, consulte [Como publicar um aplicativo Web como um contêiner do Docker usando o Kit de ferramentas do Azure para IntelliJ].
* **Gerenciamento de Conta de Armazenamento**: o Kit de ferramentas do Azure para IntelliJ agora dá suporte ao gerenciamento de suas contas de armazenamento na Exibição do Azure Explorer. Para obter mais informações, consulte [Gerenciar contas de armazenamento usando o Azure Explorer para IntelliJ].
* **Gerenciamento de Máquina Virtual**: o Kit de ferramentas do Azure para IntelliJ agora dá suporte ao gerenciamento de suas máquinas virtuais da janela de ferramentas do Azure Explorer. Para obter mais informações, consulte [Gerenciar Máquinas Virtuais usando o Azure Explorer para IntelliJ].
* **Remoção de suporte a depuração remota**. A depuração remota de aplicativos Web Java no Serviço de Aplicativo do Azure em Java foi removida do Kit de ferramentas do Azure para IntelliJ; isso foi necessário para resolver alguns problemas que os clientes estavam tendo ao usar o Kit de ferramentas.

### <a name="august-26-2016"></a>26 de agosto de 2016
O Kit de Ferramentas do Azure para IntelliJ, versão de agosto de 2016, inclui as seguintes melhorias:

* **Distribuições personalizadas do JDK**. Agora, o Kit de Ferramentas do Azure para IntelliJ oferece suporte a especificação e implantação de uma versão JDK arbitrária para o contêiner WebApp do Azure:
  * Além dos JDKs fornecidos pelo Azure, também é possível escolher dentre uma ampla seleção de versões do Zulu OpenJDK disponibilizadas no Azure pelo Azul Systems.
  * Você também pode especificar sua própria distribuição JDK se carregar um arquivo ZIP em sua conta de armazenamento.
* **Aprimoramentos no modo de exibição do Azure Explorer**:
  * Suporte para gerenciamento de máquinas virtuais usando o novo modelo de Resource Manager do Azure: você pode listar, criar e excluir máquinas virtuais baseadas no resource manager sem sair do IDE.
  * Suporte para gerenciamento de blobs da Conta de armazenamento usando o Resource Manager do Azure, que complementa a funcionalidade existente para gerenciar contas de armazenamento "clássico".
* **Microsoft JDBC Driver 6.0 para SQL Server**. Esta atualização inclui o driver JDBC do Microsoft SQL Server (v 6.0), que é agora incluído como uma biblioteca que você pode adicionar facilmente aos seus projetos Java, substituindo a versão mais antiga.

### <a name="june-29-2016"></a>29 de junho de 2016
O Kit de Ferramentas do Azure para IntelliJ, versão de março de 2016, inclui os seguintes aprimoramentos:

* **Requisito do Java 8**. O Kit de ferramentas do Azure para IntelliJ agora exige o Java 8, embora esse requisito seja somente para o kit de ferramentas - seus aplicativos podem continuar a usar todas as versões do Java com suporte do Azure.
* **Suporte para os JDKs do Java mais recentes**. Agora há suporte para as versões mais recentes de JDKs do Java pelo Kit de Ferramentas do Azure para IntelliJ.
* **Suporte para o SDK do Azure v2.9.1**. A versão mais recente do SDK do Azure agora é o pré-requisito mínimo para o Kit de Ferramentas do Azure para IntelliJ.
* **Exemplos Integrados**. O Kit de Ferramentas do Azure para IntelliJ agora apresenta vários aplicativos de exemplo para ajudar os desenvolvedores a começar.
* **Integração de Ferramentas HDInsight**. As Ferramentas de HDInsight do Azure agora estão incluídas no Kit de Ferramentas do Azure para IntelliJ. Para obter mais informações, consulte [Plug-in das Ferramentas do HDInsight para IntelliJ].
* **Depuração remota de aplicativos Web do Java**. O Kit de Ferramentas do Azure para IntelliJ agora dá suporte a depuração remota de aplicativos Web do Java no Serviço de Aplicativo do Azure.

### <a name="april-12-2016"></a>12 de abril de 2016
O Kit de Ferramentas do Azure para IntelliJ, versão de abril de 2016, inclui as seguintes melhorias:

* **Suporte para o SDK do Azure v2.9.0**. A versão mais recente do SDK do Azure agora é o pré-requisito mínimo para o Kit de Ferramentas do Azure para IntelliJ.
* **Diversas melhorias de usabilidade, capacidade de resposta e desempenho relacionadas ao suporte do aplicativo Web do Azure**. Uma série de otimizações de desempenho na forma como o Kit de Ferramentas se comunica com o Azure resulta em uma interface do usuário mais dinâmica.
* **Capacidade de excluir um contêiner do aplicativo Web existente no Azure por meio do IntelliJ**. O Kit de Ferramentas do Azure para IntelliJ agora permite a exclusão de um contêiner da Web existente do Azure sem a necessidade de sair do IntelliJ.

## <a name="see-also"></a>Consulte também
Para obter mais informações sobre os kits de ferramentas do Azure para Java IDEs, confira os links a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [Novidades no Kit de Ferramentas do Azure para o Eclipse]
  * [Instalação do Kit de Ferramentas do Azure para o Eclipse]
  * [Criar um aplicativo Web Hello World para o Azure no Eclipse]
  * [Instruções de entrada para o Kit de ferramentas do Azure para Eclipse]
* [Kit de Ferramentas do Azure para IntelliJ]
  * *Novidades no Kit de Ferramentas do Azure para o IntelliJ (Este artigo)*
  * [Instalação do Kit de Ferramentas do Azure para IntelliJ]
  * [Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]
  * [Criar um aplicativo Web Hello World para o Azure no IntelliJ]

Para obter mais informações sobre como usar o Azure com o Java, confira a [Central de desenvolvimento Java do Azure].

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalação do Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de entrada para o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Instruções de entrada no Azure para o Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Como publicar um aplicativo Web como um contêiner do Docker usando o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Gerenciar contas de armazenamento usando o Azure Explorer para IntelliJ]: ./azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer.md
[Gerenciar Máquinas Virtuais usando o Azure Explorer para IntelliJ]: ./azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer.md

[Central de desenvolvimento Java do Azure]: http://go.microsoft.com/fwlink/?LinkID=699547

[Plug-in das Ferramentas do HDInsight para IntelliJ]: ./hdinsight/hdinsight-apache-spark-intellij-tool-plugin.md
