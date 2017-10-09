---
title: "aaaUse vazio de nós de borda em clusters de Hadoop no HDInsight - Azure | Microsoft Docs"
description: "Como tooadd um nó de borda vazia tooan HDInsight cluster que pode ser usado como um cliente e, em seguida, os aplicativos de HDInsight de teste/host."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>Usar nós de borda vazios em clusters Hadoop no HDInsight

Saiba como o cluster do nó tooan HDInsight de borda tooadd vazio. Um nó de borda vazia é uma máquina virtual do Linux com hello mesmas ferramentas de cliente instalado e configurado como headnodes hello, mas nenhum serviço de Hadoop em execução. Você pode usar o nó de borda Olá para acessar o cluster hello, testar seus aplicativos de cliente e hospedagem de aplicativos cliente. 

Você pode adicionar um cluster tooan HDInsight existente nó borda vazia, tooa novo cluster ao criar cluster hello. A adição de um nó de borda vazio é feita usando o modelo Azure Resource Manager.  Olá exemplo a seguir demonstra como é feito usando um modelo:

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Conforme mostrado no exemplo hello, opcionalmente, você pode chamar um [ação de script](hdinsight-hadoop-customize-cluster-linux.md) configuração adicional tooperform, como ao instalar [Apache matiz](hdinsight-hadoop-hue-linux.md) no nó de borda hello. script de ação de script Hello deve estar publicamente acessível na web hello.  Por exemplo, se o script hello é armazenado no armazenamento do Azure, use contêineres do públicos ou blobs públicos.

o tamanho de máquina virtual do nó de borda Olá deve atender aos requisitos de tamanho Olá HDInsight cluster trabalho nó vm. Para Olá recomendado trabalho tamanhos de vm do nó, consulte [Hadoop criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).

Depois de criar um nó de borda, você pode conectar toohello borda nó usando o SSH e executar cluster de Hadoop ferramentas tooaccess saudação do cliente no HDInsight.

> [!WARNING] 
> O uso de um nó de borda vazio com HDInsight está atualmente em versão prévia. Componentes personalizados que estão instalados no nó de borda Olá recebem suporte comercialmente razoável da Microsoft. Isso pode resultar na resolução de problemas encontrados. Ou pode ser chamado toocommunity recursos para obter assistência adicional. Olá seguem alguns Olá a maioria dos sites de ativo para obter ajuda da comunidade de saudação:
>
> * [Fórum do MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://stackoverflow.com](http://stackoverflow.com).
>
> Se você estiver usando uma tecnologia do Apache, você pode ser capaz de toofind assistência por meio de saudação sites de projeto do Apache no [http://apache.org](http://apache.org), como Olá [Hadoop](http://hadoop.apache.org/) site.

## <a name="add-an-edge-node-tooan-existing-cluster"></a>Adicionar um cluster existente do nó tooan de borda
Nesta seção, você deve usar um modelo de Gerenciador de recursos tooadd um cluster HDInsight existente borda nó tooan.  modelo do Gerenciador de recursos de saudação pode ser encontrado no [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/). modelo do Gerenciador de recursos de saudação chama uma ação de script localizada em https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. script Hello não executa nenhuma ação.  É toodemonstrate chamar a ação de script de um modelo do Gerenciador de recursos.

**tooadd um cluster existente do nó tooan de borda vazia**

1. Se você ainda não tem um, crie um cluster HDInsight.  Veja [Tutorial do Hadoop: Introdução ao uso do Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Clique em Olá após a imagem toosign em tooAzure de modelo do Azure Resource Manager Olá aberto no hello portal do Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configure Olá propriedades a seguir:
   
   * **Assinatura**: selecione uma assinatura do Azure usada para criar o cluster de saudação.
   * **Grupo de recursos**: grupo de recursos de saudação selecione usado para o cluster HDInsight existente de saudação.
   * **Local**: Selecionar local de saudação do cluster HDInsight existente de saudação.
   * **Nome do cluster**: insira o nome de saudação de um cluster HDInsight existente.
   * **Tamanho de nó de borda**: selecione um dos tamanhos de VM hello. tamanho da vm Olá deve atender aos requisitos de tamanho de vm de nó do hello trabalhador. Para Olá recomendado trabalho tamanhos de vm do nó, consulte [Hadoop criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).
   * **Prefixo de nó de borda**: valor de padrão de saudação é **novo**.  Usando o valor padrão de saudação, o nome do nó de borda de saudação é **edgenode novo**.  Você pode personalizar o prefixo de saudação do portal de saudação. Você também pode personalizar o nome completo de saudação do modelo de saudação.

4. Verificar **concordo toohello termos e condições declaradas acima**e, em seguida, clique em **compra** toocreate nó de borda de saudação.

>[!IMPORTANT]
> Verifique se tooselect Olá grupo de recursos Azure para o cluster HDInsight existente de saudação.  Caso contrário, você receberá o erro de saudação mensagem "não é possível executar a operação solicitada no recurso aninhado. Recurso pai '&lt;NomeDoCluster>' não encontrado".

## <a name="add-an-edge-node-when-creating-a-cluster"></a>Adicionar um nó de borda ao criar um cluster
Nesta seção, você pode usar um cluster de HDInsight do Gerenciador de recursos modelo toocreate com um nó de borda.  modelo do Gerenciador de recursos de saudação pode ser encontrado no hello [Galeria de modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/). modelo do Gerenciador de recursos de saudação chama uma ação de script localizada em https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. script Hello não executa nenhuma ação.  É toodemonstrate chamar a ação de script de um modelo do Gerenciador de recursos.

**tooadd um cluster existente do nó tooan de borda vazia**

1. Se você ainda não tem um, crie um cluster HDInsight.  Veja [Introdução ao uso do Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Clique em Olá após a imagem toosign em tooAzure de modelo do Azure Resource Manager Olá aberto no hello portal do Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Configure Olá propriedades a seguir:
   
   * **Assinatura**: selecione uma assinatura do Azure usada para criar o cluster de saudação.
   * **Grupo de recursos**: criar um novo grupo de recursos usado para o cluster de saudação.
   * **Local**: selecione um local para o grupo de recursos de saudação.
   * **Nome do cluster**: insira um nome para Olá novo cluster toocreate.
   * **Nome de usuário de logon de cluster**: Insira nome de usuário do Hadoop HTTP hello.  nome do padrão de saudação é **admin**.
   * **Senha de logon de cluster**: insira a senha do usuário Hadoop HTTP hello.
   * **SSH nome de usuário**: insira o nome de usuário SSH hello. nome do padrão de saudação é **sshuser**.
   * **SSH senha**: insira a senha de usuário SSH hello.
   * **Instalar a ação de Script**: manter o valor padrão de saudação para seguir este tutorial.
     
     Algumas propriedades foram codificados no modelo de saudação: tipo de Cluster, contagem de nós de trabalho do Cluster, tamanho de nó de borda e nome do nó de borda.
4. Verificar **concordo toohello termos e condições declaradas acima**e, em seguida, clique em **compra** toocreate cluster de saudação com nó de borda hello.

## <a name="access-an-edge-node"></a>Acessar um nó de borda
nó de borda Olá ssh ponto de extremidade é &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22.  Por exemplo, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.

nó de borda Olá aparece como um aplicativo hello portal do Azure.  Fornece de portal Olá Olá Olá de tooaccess informações de borda nó usando o SSH.

**ponto de extremidade do tooverify Olá borda nó SSH**

1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Abra o cluster do HDInsight Olá com um nó de borda.
3. Clique em **aplicativos** da folha de cluster hello. Você deverá ver o nó de borda hello.  nome do padrão de saudação é **edgenode novo**.
4. Clique no nó de borda hello. Você deverá ver o ponto de extremidade SSH hello.

**toouse Hive no nó de borda Olá**

1. Use o nó de borda do SSH tooconnect toohello. Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Depois de conectar o nó de borda toohello usando SSH, use Olá console de Hive do comando tooopen Olá a seguir:
   
        hive
3. Execute Olá comando tooshow Hive tabelas em cluster Olá seguintes:
   
        show tables;

## <a name="delete-an-edge-node"></a>Excluir um nó de borda
Você pode excluir um nó de borda da saudação portal do Azure.

**tooaccess um nó de borda**

1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Abra o cluster do HDInsight Olá com um nó de borda.
3. Clique em **aplicativos** da folha de cluster hello. Você verá uma lista de nós de borda.  
4. Nó de borda de saudação com o botão direito você deseja toodelete e, em seguida, clique em **excluir**.
5. Clique em **Sim** tooconfirm.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como tooadd um nó de borda e como tooaccess Olá nó de borda. toolearn mais, consulte Olá artigos a seguir:

* [Instalar aplicativos de HDInsight](hdinsight-apps-install-applications.md): Saiba como clusters de tooinstall um tooyour de aplicativo do HDInsight.
* [Instalar aplicativos personalizados do HDInsight](hdinsight-apps-install-custom-applications.md): Saiba como toodeploy uma tooHDInsight de aplicativo do HDInsight não publicado.
* [Publicar aplicativos HDInsight](hdinsight-apps-publish-applications.md): Saiba como toopublish seu tooAzure de aplicativos personalizado do HDInsight Marketplace.
* [MSDN: Instalar um aplicativo de HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Saiba como toodefine HDInsight aplicativos.
* [Personalizar clusters HDInsight baseados em Linux usando a ação de Script](hdinsight-hadoop-customize-cluster-linux.md): Saiba como aplicativos adicionais do tooinstall toouse ação de Script.
* [Criar clusters baseados em Linux Hadoop no HDInsight usando modelos do Gerenciador de recursos](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Saiba como clusters de toocall Gerenciador de recursos modelos toocreate HDInsight.

