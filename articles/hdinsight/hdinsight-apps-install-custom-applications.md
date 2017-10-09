---
title: "aaaInstall seus próprios aplicativos personalizados do Hadoop no HDInsight do Azure | Microsoft Docs"
description: Saiba como aplicativos de HDInsight tooinstall em aplicativos de HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Instale aplicativos personalizados do Hadoop no Azure HDInsight

Neste artigo, você aprenderá como tooinstall um aplicativo de Hadoop em HDInsight do Azure, que não foi publicada toohello portal do Azure. aplicativo Hello irá instalar este artigo é [matiz](http://gethue.com/).

Um aplicativo do HDInsight é um aplicativo que os usuários podem instalar em um cluster HDInsight baseado em Linux.  Esses aplicativos podem ser desenvolvidos pela Microsoft, por ISVs (fornecedores independentes de software) ou por conta própria.  

Outros artigos relacionados:

* [Instalar aplicativos de HDInsight](hdinsight-apps-install-applications.md): Saiba como clusters de tooinstall um tooyour de aplicativo do HDInsight.
* [Publicar aplicativos HDInsight](hdinsight-apps-publish-applications.md): Saiba como toopublish seu tooAzure de aplicativos personalizado do HDInsight Marketplace.
* [MSDN: Instalar um aplicativo de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Saiba como toodefine HDInsight aplicativos.

## <a name="prerequisites"></a>Pré-requisitos
Se você quiser tooinstall HDInsight aplicativos em um cluster HDInsight existente, você deve ter um cluster HDInsight. toocreate um, consulte [criar clusters](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Você também pode instalar aplicativos do HDInsight quando cria um cluster HDInsight.

## <a name="install-hdinsight-applications"></a>Instalar aplicativos do HDInsight
Aplicativos de HDInsight podem ser instalados quando você criar um cluster ou tooan existente HDInsight. Para definir modelos do Azure Resource Manager, confira [MSDN: instalar um aplicativo do HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).

arquivos de saudação necessários para implantar esse aplicativo (matiz):

* [azuredeploy.JSON](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): modelo do Gerenciador de recursos de saudação para instalar o aplicativo de HDInsight. Confira [MSDN: instalar um aplicativo do HDInsight](https://msdn.microsoft.com/library/mt706515.aspx) para desenvolver seu próprio modelo do Resource Manager.
* [matiz install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): Olá ação de Script que está sendo chamada pelo modelo do Gerenciador de recursos de saudação para configurar o nó de borda hello.
* [matiz binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): arquivo binário de matiz Olá hui install_v0.sh sendo chamado.
* [matiz binários-14 04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): arquivo binário de matiz Olá hui install_v0.sh sendo chamado.
* [webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz): um aplicativo Web de exemplo (Tomcat) sendo chamado de hui-install_v0.sh.

**tooinstall matiz tooan existente cluster do HDInsight**

1. Clique em Olá após a imagem toosign no tooAzure de modelo do Gerenciador de recursos de saudação aberta no hello Portal do Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Esse botão abre um modelo do Gerenciador de recursos no hello portal do Azure.  Olá modelo do Gerenciador de recursos está localizado em [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).  toolearn como toowrite neste modelo do Gerenciador de recursos, consulte [MSDN: instalar um aplicativo de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. De saudação **parâmetros** folha, digite Olá seguinte:

   * **ClusterName**: Insira nome de saudação do cluster de saudação onde você deseja que o aplicativo de hello tooinstall. Esse cluster deve ser um cluster existente.
3. Clique em **Okey** toosave parâmetros de saudação.
4. De saudação **implantação personalizada** folha, digite **grupo de recursos**.  grupo de recursos de saudação é um contêiner que agrupa cluster hello, conta de armazenamento dependente de saudação e outros recursos. É necessário toouse Olá mesmo grupo de recursos como cluster hello.
5. Clique em **Termos legais** e em **Criar**.
6. Verifique se Olá **Pin toodashboard** caixa de seleção está selecionada e, em seguida, clique em **criar**. Você pode ver o status de instalação de saudação do painel de portal do hello bloco toohello fixado e notificação no portal de saudação (clique ícone de sino Olá na parte superior de saudação do portal de saudação).  Ele usa o aplicativo de hello tooinstall cerca de 10 minutos.

**tooinstall matiz durante a criação de um cluster**

1. Clique em Olá após a imagem toosign no tooAzure de modelo do Gerenciador de recursos de saudação aberta no hello Portal do Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Esse botão abre um modelo do Gerenciador de recursos no hello portal do Azure.  Olá modelo do Gerenciador de recursos está localizado em [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).  toolearn como toowrite neste modelo do Gerenciador de recursos, consulte [MSDN: instalar um aplicativo de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Seguir Olá instrução toocreate cluster e instale o matiz. Para saber mais sobre a criação de clusters HDInsight, confira [Criar clusters Hadoop baseados em Linux no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

Além disso toohello portal do Azure, você também pode usar [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) e [CLI do Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall modelos de Gerenciador de recursos.

## <a name="validate-hello-installation"></a>Validar a instalação Olá
Você pode verificar o status do aplicativo de saudação em Olá a instalação do aplicativo hello toovalidate portal do Azure. Além disso, também é possível validar todas as provém de pontos de extremidade HTTP backup conforme esperado e páginas da Web de saudação se houver um:

**portal de matiz Olá tooopen**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Clusters HDInsight** no menu esquerdo hello.  Se você não conseguir ver a opção, clique em **Procurar** e clique em **Clusters HDInsight**.
3. Clique em cluster Olá onde você instalou o aplicativo hello.
4. De saudação **configurações** folha, clique em **aplicativos** em Olá **geral** categoria. Você deverá ver **matiz** listados no hello **aplicativos instalados** folha.
5. Clique em **matiz** de propriedades de Olá Olá lista toolist.  
6. Clique em Olá página da Web link toovalidate Olá site; Abra o ponto de extremidade de saudação HTTP em um navegador toovalidate Olá matiz interface da web, ponto de extremidade SSH Olá aberto usando o SSH. Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="troubleshoot-hello-installation"></a>Solucionar problemas de instalação de saudação
Você pode verificar o status de instalação de aplicativo hello de notificação no portal de saudação (clique ícone de sino Olá na parte superior de saudação do portal de saudação).

Se a falha na instalação de um aplicativo, você pode ver as mensagens de erro de saudação e informações de 3 locais de depuração:

* Aplicativos do HDInsight: informações de erro geral.

    Abrir o cluster de saudação do portal de saudação e clique em aplicativos da folha de configurações de saudação do:

    ![erro de instalação do aplicativo aplicativos hdinsight](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* Ação de script do HDInsight: se a mensagem de erro Olá HDInsight aplicativos indica uma falha na ação de script, para obter mais detalhes sobre a falha de script hello aparecerá no painel de ações de script hello.

    Clique em ação de Script de folha de configurações de saudação. Histórico de ação de script mostra mensagens de erro de saudação

    ![erro de ação de script aplicativos hdinsight](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Ambari Web da interface do usuário: Se o script de instalação Olá causa falha Olá Olá, use logs completos do Ambari Web UI toocheck sobre scripts de instalação hello.

    Para saber mais, confira [Solução de problemas](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).

## <a name="remove-hdinsight-applications"></a>Remover aplicativos do HDInsight
Há várias maneiras toodelete HDInsight aplicativos.

### <a name="use-portal"></a>Usar o portal
**tooremove um aplicativo usando o portal de saudação**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Clusters HDInsight** no menu esquerdo hello.  Se você não conseguir ver a opção, clique em **Procurar** e clique em **Clusters HDInsight**.
3. Clique em cluster Olá onde você instalou o aplicativo hello.
4. De saudação **configurações** folha, clique em **aplicativos** em Olá **geral** categoria. Você deverá ver uma lista de aplicativos instalados. Para este tutorial, **matiz** listados no hello **aplicativos instalados** folha.
5. Clique com botão direito aplicativo hello você deseja tooremove e, em seguida, clique em **excluir**.
6. Clique em **Sim** tooconfirm.

No portal de hello, você pode também excluir Olá cluster ou excluir grupo de recursos de saudação que contém o aplicativo hello.

### <a name="use-azure-powershell"></a>Usar PowerShell do Azure
Usando o PowerShell do Azure, você pode excluir o cluster hello ou excluir o grupo de recursos de saudação. Veja [Excluir clusters usando o Azure PowerShell](hdinsight-administer-use-powershell.md#delete-clusters).

### <a name="use-azure-cli"></a>Usar a CLI do Azure
Usando a CLI do Azure, você pode excluir o cluster hello ou excluir o grupo de recursos de saudação. Veja [Excluir clusters usando a CLI do Azure](hdinsight-administer-use-command-line.md#delete-clusters).

## <a name="next-steps"></a>Próximas etapas
* [MSDN: Instalar um aplicativo de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Saiba como toodevelop modelos de Gerenciador de recursos para implantar aplicativos de HDInsight.
* [Instalar aplicativos de HDInsight](hdinsight-apps-install-applications.md): Saiba como clusters de tooinstall um tooyour de aplicativo do HDInsight.
* [Publicar aplicativos HDInsight](hdinsight-apps-publish-applications.md): Saiba como toopublish seu tooAzure de aplicativos personalizado do HDInsight Marketplace.
* [Personalizar clusters HDInsight baseados em Linux usando a ação de Script](hdinsight-hadoop-customize-cluster-linux.md): Saiba como aplicativos adicionais do tooinstall toouse ação de Script.
* [Criar clusters baseados em Linux Hadoop no HDInsight usando modelos do Gerenciador de recursos](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Saiba como clusters de toocall Gerenciador de recursos modelos toocreate HDInsight.
* [Use nós de borda vazia no HDInsight](hdinsight-apps-use-edge-node.md): Saiba como toouse vazio de borda nó para acessar o cluster HDInsight, teste de aplicativos de HDInsight e hospedagem de aplicativos de HDInsight.
