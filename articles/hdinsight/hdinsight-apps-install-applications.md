---
title: aplicativos de Hadoop aaaInstall de terceiros no Azure HDInsight | Microsoft Docs
description: Saiba como tooinstall aplicativos de Hadoop de terceiros no Azure HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Instale aplicativos de terceiros do Hadoop no Azure HDInsight

Neste artigo, você aprenderá como tooinstall um aplicativo de Hadoop de terceiros já publicado no Azure HDInsight. Para obter instruções sobre como instalar seu próprio aplicativo, confira [Instalar aplicativos personalizados do HDInsight](hdinsight-apps-install-custom-applications.md).

Um aplicativo do HDInsight é um aplicativo que os usuários podem instalar em um cluster HDInsight baseado em Linux. Esses aplicativos podem ser desenvolvidos pela Microsoft, por ISVs (fornecedores independentes de software) ou por conta própria.  

No momento, há quatro aplicativos publicados:

* **DATAIKU DDS no HDInsight**: Dataiku DSS (Studio de ciência de dados) é um software que permite que os dados tooprototype profissionais (cientistas de dados, os analistas de negócios, os desenvolvedores...), criar e implantar serviços altamente específicos que transformam os dados brutos em previsões de impacto de negócios.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) oferece analistas um toodiscover de maneira interativa, analisar e visualizar os resultados de saudação grandes dados. Pull em fontes de dados adicionais facilmente toodiscover novas relações e obter respostas de saudação que precisa rapidamente.
* **Coletor de dados de Streamsets para HDnsight** fornece um ambiente completo de desenvolvimento integrado (IDE) que permite que você cria, testa, implanta e gerenciar a qualquer ingestão pipelines que combinam dados de fluxo e lote e incluir uma variedade de transformações de fluxo, sem precisar de código personalizado toowrite. 
* **Cask CDAP para HDInsight** fornece Olá primeiro unificada plataforma de integração para dados grandes que reduz Olá tempo tooproduction para aplicativos de dados e Lagos dados em 80%. Este aplicativo só dá suporte a clusters HBase 3.4 padrão.
* **Inteligência de Artificial H2O para HDInsight (Beta)** H2O de água gasosa dá suporte a saudação algoritmos distribuídos a seguir: GLM, Naïve Bayes, Distributed aleatória floresta, gradiente máquina aumentando, redes neurais profundas, profundo de aprendizagem, K-means, PCA, Modelos de classificação baixos generalizados, detecção de anomalias e Autoencoders.
* **Kyligence Analytics Platform** O KAP (Kyligence Analytics Platform) é um data warehouse pronto para empresas com tecnologia Apache Kylin e Apache Hadoop; ele capacita a latência de consulta de fração de segundos em conjuntos de dados de escala, além de simplificar a análise de dados para analistas e usuários corporativos. 
* **SnapLogic Hadooplex** hello SnapLogic Hadooplex em execução no HDInsight permite tooget toobusiness insights de clientes mais rápido, fornecendo a ingestão de dados de autoatendimento e preparação de praticamente qualquer fonte de toohello nuvem do Microsoft Azure plataforma.
* **Servidor de trabalho Spark para KNIME Spark Executor** servidor Spark para KNIME Spark Executor é usado tooconnect Olá plataforma de análise de KNIME tooHDInsight clusters.

instruções de saudação fornecidas neste artigo usam o portal do Azure. Você também pode exportar o modelo do Azure Resource Manager Olá do portal de saudação ou obtenha uma cópia do modelo do Gerenciador de recursos de saudação de fornecedores e usar o PowerShell do Azure e o modelo de saudação toodeploy CLI do Azure.  Confira [Criar clusters Hadoop baseados em Linux no HDInsight usando modelos do Gerenciador de Recursos](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

## <a name="prerequisites"></a>Pré-requisitos
Se você quiser tooinstall HDInsight aplicativos em um cluster HDInsight existente, você deve ter um cluster HDInsight. toocreate um, consulte [criar clusters](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Você também pode instalar aplicativos do HDInsight quando cria um cluster HDInsight.

## <a name="install-applications-tooexisting-clusters"></a>Instalar clusters de tooexisting de aplicativos
Olá procedimento a seguir mostra como tooinstall HDInsight aplicativos tooan cluster HDInsight existente.

**tooinstall um aplicativo de HDInsight**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Clusters HDInsight** no menu esquerdo hello.  Se você não conseguir ver a opção, clique em **Mais Serviços** e clique em **Clusters HDInsight**.
3. Clique em um cluster HDInsight.  Se não tiver um, você deverá criá-lo primeiro.  Confira [Criar clusters](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).
4. Clique em **aplicativos** em Olá **configurações** categoria. Você pode ver uma lista de aplicativos instalados. Se você não encontrar aplicativos, isso significa que não há nenhum aplicativo para esta versão do cluster do HDInsight hello.
   
    ![Menu do portal de aplicativos do HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. Clique em **adicionar** no menu de folha de saudação. 
   
    ![Aplicativos instalados de aplicativos do HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    Você poderá ver uma lista de aplicativos existentes do HDInsight.
   
    ![Aplicativos disponíveis de aplicativos HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Clique em um dos aplicativos hello, aceite os termos legais hello e, em seguida, clique em **selecione**.

Você pode ver o status de instalação de saudação de notificações do portal de saudação (clique ícone de sino Olá na parte superior de saudação do portal de saudação). Após a saudação aplicativo estiver instalado, o aplicativo hello serão exibidos na folha de aplicativos instalado hello.

## <a name="install-applications-during-cluster-creation"></a>Instalar aplicativos durante a criação do cluster
Você tem aplicativos de HDInsight Olá opção tooinstall quando você cria um cluster. Durante o processo de saudação HDInsight aplicativos instalados após cluster Olá é criado e está em estado de execução de saudação. Olá procedimento a seguir mostra como tooinstall HDInsight aplicativos quando você cria um cluster.

**tooinstall um aplicativo de HDInsight**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **NOVO**, em **Análises de Dados** e em **HDInsight**.
3. Insira o **Nome do Cluster**: esse nome deve ser globalmente exclusivo.
4. Clique em **assinatura** tooselect Olá assinatura do Azure que é usada para o cluster de saudação.
5. Clique em **Selecionar Tipo de cluster**, e, em seguida, selecione:
   
   * **Tipo de cluster**: se você não souber quais toochoose, selecione **Hadoop**. É do tipo de cluster mais popular hello.
   * **Sistema Operacional**: selecione **Linux**.
   * **Versão**: usar a versão padrão de saudação se você não souber quais toochoose. Para obter mais informações, consulte [Versões de cluster do HDInsight](hdinsight-component-versioning.md).
   * **Nível de cluster**: HDInsight do Azure fornece ofertas de nuvem Olá grandes dados em duas categorias: camadas Standard e Premium. Para obter mais informações, consulte [Camadas de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).
6. Clique em **aplicativos**, clique em uma saudação aplicativos publicados e, em seguida, clique em **selecione**.
7. Clique em **credenciais** e, em seguida, digite uma senha para o usuário administrador hello. Você também precisa tooenter um **nome de usuário SSH** e um **senha** ou **chave pública**, que é o usuário SSH Olá tooauthenticate usado. Usar uma chave pública é hello abordagem recomendada. Clique em **selecione** em configuração de credenciais de Olá Olá inferior toosave.
8. Clique em **fonte de dados**, selecione uma saudação existente contas de armazenamento ou criar um novo toobe de conta de armazenamento usada como conta de armazenamento padrão Olá para cluster hello.
9. Clique em **grupo de recursos** tooselect um recurso existente do grupo, ou clique em **novo** toocreate um novo grupo de recursos
10. Em Olá **novo HDInsight Cluster** folha, certifique-se de que **Pin tooStartboard** está selecionado e, em seguida, clique em **criar**. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>Listar os aplicativos do HDInsight instalados e as propriedades
portal de saudação mostra que uma lista de saudação instalado HDInsight aplicativos para um cluster e propriedades de saudação de cada aplicativo instalado.

**Propriedades de aplicativo e a exibição de HDInsight toolist**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Clusters HDInsight** no menu esquerdo hello.  Se você não conseguir ver a opção, clique em **Procurar** e clique em **Clusters HDInsight**.
3. Clique em um cluster HDInsight.
4. De saudação **configurações** folha, clique em **aplicativos** em Olá **geral** categoria. folha de aplicativos instalado Olá lista todos os aplicativos de saudação instalado. 
   
    ![Aplicativos instalados de aplicativos do HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Clique em uma saudação instalada aplicativos tooshow Olá propriedade. Olá listas de folha de propriedades:
   
   * Nome do aplicativo: nome do aplicativo.
   * Status: status do aplicativo. 
   * Página da Web: Olá URL do aplicativo web de saudação que você implantou o nó de borda toohello. credencial Olá é hello igual à saudação HTTP as credenciais do usuário que você configurou para o cluster hello.
   * Ponto de extremidade HTTP: credencial Olá é hello igual à saudação HTTP as credenciais do usuário que você configurou para o cluster hello. 
   * Ponto de extremidade SSH: você pode usar o nó de borda do SSH tooconnect toohello. credenciais SSH Olá são Olá igual à saudação SSH as credenciais do usuário que você configurou para o cluster hello. Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
6. toodelete um aplicativo, clique no aplicativo hello e clique **excluir** Olá no menu de contexto.

## <a name="connect-toohello-edge-node"></a>Conecte-se o nó de borda toohello
Você pode conectar o nó de borda toohello usando HTTP e SSH. podem ser encontradas informações de ponto de extremidade de saudação do hello [portal](#list-installed-hdinsight-apps-and-properties). Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

credenciais de ponto de extremidade HTTP Olá são credenciais do usuário do hello HTTP que você configurou para o cluster do HDInsight Olá; credenciais de ponto de extremidade SSH Olá são credenciais SSH Olá que você configurou para o cluster do HDInsight hello.

## <a name="troubleshoot"></a>Solucionar problemas
Consulte [solucionar problemas de instalação de saudação](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation).

## <a name="next-steps"></a>Próximas etapas
* [Instalar aplicativos personalizados do HDInsight](hdinsight-apps-install-custom-applications.md): Saiba como toodeploy uma tooHDInsight de aplicativo do HDInsight não publicado.
* [Publicar aplicativos HDInsight](hdinsight-apps-publish-applications.md): Saiba como toopublish seu tooAzure de aplicativos personalizado do HDInsight Marketplace.
* [MSDN: Instalar um aplicativo de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Saiba como toodefine HDInsight aplicativos.
* [Personalizar clusters HDInsight baseados em Linux usando a ação de Script](hdinsight-hadoop-customize-cluster-linux.md): Saiba como aplicativos adicionais do tooinstall toouse ação de Script.
* [Criar clusters baseados em Linux Hadoop no HDInsight usando modelos do Gerenciador de recursos](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Saiba como clusters de toocall Gerenciador de recursos modelos toocreate HDInsight.
* [Use nós de borda vazia no HDInsight](hdinsight-apps-use-edge-node.md): Saiba como toouse vazio de borda nó para acessar o cluster HDInsight, teste de aplicativos de HDInsight e hospedagem de aplicativos de HDInsight.

