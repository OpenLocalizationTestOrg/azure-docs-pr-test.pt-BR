---
title: "clusters de HDInsight aaaCustomize usando as ações de script - Azure | Microsoft Docs"
description: "Adicione componentes personalizados, que clusters de HDInsight com base em tooLinux usando ações de Script. Ações de script são scripts de Bash que podem ser toocustomize usado Olá cluster configuração ou adicionar mais serviços e utilitários, como o matiz, Solr ou R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Personalizar clusters HDInsight baseados em Linux usando a Ação de Script

HDInsight fornece uma opção de configuração chamada **ação de Script** que chama scripts personalizados que personalizar Olá cluster. Esses scripts são usado tooinstall componentes adicionais e alterar as definições de configuração. Ações de script podem ser usadas durante ou após a criação do cluster.

> [!IMPORTANT]
> ações de script Hello capacidade toouse em um cluster já em execução está disponível somente para clusters HDInsight baseados em Linux.
>
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Ações de script também podem ser publicado toohello Marketplace do Azure como um aplicativo de HDInsight. Alguns exemplos de saudação neste documento mostram como você pode instalar um aplicativo de HDInsight usando comandos de ação de script do PowerShell e hello .NET SDK. Para obter mais informações sobre aplicativos de HDInsight, consulte [HDInsight publicar aplicativos em hello Azure Marketplace](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>Permissões

Se você estiver usando um cluster de HDInsight ingressado no domínio, há duas permissões Ambari que são necessárias para usar ações de script com cluster hello:

* **AMBARI. EXECUTAR\_personalizado\_comando**: função de administrador do Ambari Olá tem essa permissão por padrão.
* **CLUSTER. EXECUTAR\_personalizado\_comando**: ambos Olá administrador de Cluster HDInsight e Ambari administrador têm essa permissão por padrão.

Para obter mais informações sobre como trabalhar com permissões com o HDInsight de domínio, consulte [gerenciar clusters de HDInsight de domínio](hdinsight-domain-joined-manage.md).

## <a name="access-control"></a>Controle de acesso

Se você não estiver Olá administrador/proprietário da assinatura do Azure, sua conta deve ter pelo menos **Colaborador** grupo de recursos do acesso toohello que contém o cluster do HDInsight hello.

Além disso, se você estiver criando um cluster HDInsight, alguém com pelo menos **Colaborador** acesso toohello assinatura do Azure deve ter registrado anteriormente provedor Olá para HDInsight. Registro de provedor ocorre quando um usuário com a assinatura do Colaborador acesso toohello cria um recurso de saudação primeira vez na assinatura de saudação. Isso também pode ser feito sem criar um recurso, [registrando um provedor com o uso de REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).

Para obter mais informações sobre como trabalhar com o gerenciamento de acesso, consulte Olá documentos a seguir:

* [Introdução ao gerenciamento de acesso no hello portal do Azure](../active-directory/role-based-access-control-what-is.md)
* [Usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Noções básicas sobre Ações de Script

Uma Ação de Script é simplesmente um script Bash para o qual você fornecer um URI e parâmetros. script de saudação é executado em nós de cluster do HDInsight hello. Olá seguem características e recursos de ações de script.

* Deve ser armazenado em um URI que é acessível pelo cluster do HDInsight hello. Olá seguem possíveis locais de armazenamento:

    * Um **repositório Azure Data Lake** conta que seja acessível pelo cluster do HDInsight hello. Para obter mais informações sobre o uso do Azure Data Lake Store com o HDInsight, veja [Criar um cluster HDInsight com o Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Ao usar um script armazenado no repositório Data Lake, formato URI de saudação é `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > Olá serviço principal HDInsight usa tooaccess repositório Data Lake deve ter acesso de leitura toohello script.

    * Um blob em um **conta de armazenamento do Azure** é qualquer uma das contas de armazenamento principal ou adicionais Olá para o cluster do HDInsight hello. HDInsight é concedido acesso tooboth desses tipos de contas de armazenamento durante a criação do cluster.

    * Um serviço de compartilhamento de arquivos público como o Blob do Azure, o GitHub, o OneDrive, o Dropbox, etc.

        Por exemplo, URIs, consulte Olá [scripts de ação de script de exemplo](#example-script-action-scripts) seção.

        > [!WARNING]
        > O HDInsight suporta apenas contas do Azure Storage de __Uso geral__. Ele não oferece suporte a saudação __armazenamento de Blob__ tipo de conta.

* Pode ser restringido muito**executado em apenas alguns tipos de nó**, para nós de cabeçalho de exemplo ou nós de trabalho.

  > [!NOTE]
  > Quando usado com o HDInsight Premium, você pode especificar que o script hello deve ser usado no nó de borda hello.

* Pode ser **persistente** ou **ad hoc**.

    **Persistente** scripts são cluster de toohello adicionado nós tooworker aplicado após a execução do script hello. Por exemplo, ao dimensionar o cluster hello.

    Um script persistido também pode ser aplicadas alterações o tipo de nó tooanother, como um nó principal.

  > [!IMPORTANT]
  > As ações de script persistentes devem ter um nome exclusivo.

    Scripts **Ad hoc** não são persistentes. Eles não são cluster de toohello adicionado nós tooworker aplicado após a execução da script hello. Posteriormente, você pode promover um tooa do script ad-hoc persistentes script ou rebaixar um script ad hoc de tooan script persistentes.

  > [!IMPORTANT]
  > As ações de script usadas durante a criação do cluster são mantidas automaticamente.
  >
  > Os scripts que falham não são persistentes, mesmo que você indique especificamente que eles devem ser.

* Pode aceitar **parâmetros** que são usados pelo script hello durante a execução.
* Executar com **privilégios em nível de raiz** em nós de cluster de saudação.
* Pode ser usada por meio de saudação **portal do Azure**, **Azure PowerShell**, **CLI do Azure**, ou **HDInsight .NET SDK**

cluster Olá mantém um histórico de todos os scripts que tenha sido executado. histórico de saudação é útil quando você precisa toofind Olá ID de um script para operações de promoção ou rebaixamento.

> [!IMPORTANT]
> Não há nenhuma forma automática tooundo Olá alterações feitas por uma ação de script. Ou manualmente, reverter alterações de saudação ou fornecer um script que reverte-los.


### <a name="script-action-in-hello-cluster-creation-process"></a>Ação de script no processo de criação de cluster Olá

As ações de script usadas durante a criação do cluster são ligeiramente diferentes das ações de script executadas em um cluster existente:

* script Hello é **automaticamente persistente**.
* Um **falha** em Olá script pode causar Olá toofail de processo de criação de cluster.

Olá seguinte diagrama ilustra quando a ação de Script é executada durante o processo de criação de saudação:

![Personalização do cluster HDInsight e estágios durante a criação de cluster][img-hdi-cluster-states]

script Hello executa enquanto o HDInsight está sendo configurado. Neste estágio, Olá script será executado em paralelo em todos os Olá nós especificados no cluster hello e é executado com privilégios de raiz em nós de saudação.

> [!NOTE]
> Porque o script hello é executado com privilégios de nível raiz em nós de cluster hello, você pode executar operações como parar e iniciar serviços, incluindo serviços relacionados ao Hadoop. Se você parar serviços, certifique-se de que serviço do Ambari hello e outros serviços relacionados ao Hadoop estão funcionando antes que o script hello terminar a execução. Esses serviços são necessários toosuccessfully determinar Olá integridade e o estado do cluster Olá enquanto ele está sendo criado.


Durante a criação do cluster, você pode usar várias ações de script simultaneamente. Esses scripts são invocados em ordem de saudação na qual eles foram especificados.

> [!IMPORTANT]
> Ações de script devem ser concluídas em 60 minutos ou atingirão o tempo limite. Durante o provisionamento de cluster, o script hello é executado simultaneamente com outros processos de instalação e configuração. Competição por recursos, como largura de banda rede ou tempo de CPU pode provocar Olá script tootake mais toofinish do que no ambiente de desenvolvimento.
>
> Olá toominimize tempo que demora toorun Olá script, evite tarefas como baixar e compilar aplicativos de origem. Pré-compile aplicativos e armazenar binário Olá no armazenamento do Azure.


### <a name="script-action-on-a-running-cluster"></a>Ação de script em um cluster em execução

Ao contrário de ações usadas durante a criação do cluster, uma falha em um script foi executadas em um cluster já em execução do script não automaticamente causa Olá cluster toochange tooa falhado estado. Após a conclusão de um script, o cluster Olá deve retornar tooa estado "em execução".

> [!IMPORTANT]
> Mesmo que o cluster de saudação tem um estado 'em execução', hello script com falha pode desfeito coisas. Por exemplo, um script pode excluir arquivos necessários ao cluster hello.
>
> Ações de scripts executados com privilégios de raiz, portanto, assegure-se de que você entenda o que faz um script antes de aplicá-la tooyour cluster.

Ao aplicar um cluster de tooa do script, estado do cluster Olá altera toofrom **executando** muito**aceito**, em seguida, **configuração do HDInsight**e finalmente fazer muito**Executando** para scripts com êxito. status do script Hello é registrado no histórico de ação de script hello, e você pode usar este toodetermine informações se o script hello teve êxito ou falhou. Por exemplo, Olá `Get-AzureRmHDInsightScriptActionHistory` cmdlet do PowerShell pode ser usado tooview Olá status de um script. Ele retorna informações toohello semelhante texto a seguir:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Se você alterou a senha de usuário (admin) do cluster Olá depois Olá cluster foi criado, script ações executadas em relação a esse cluster poderá falhar. Se você tiver quaisquer ações de script persistentes que nós de trabalho de destino, esses scripts podem falhar quando você dimensionar o cluster hello.

## <a name="example-script-action-scripts"></a>Scripts de exemplo de Ação de Script

Scripts de ação de script podem ser usados por meio de saudação utilitários a seguir:

* Portal do Azure
* Azure PowerShell
* CLI do Azure
* SDK do .NET do HDInsight

HDInsight fornece Olá tooinstall de scripts a seguir de componentes em clusters de HDInsight:

| Nome | Script |
| --- | --- |
| **Adicionar uma conta de armazenamento do Azure** |https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Consulte [cluster do HDInsight adicionar armazenamento adicional tooan](hdinsight-hadoop-add-storage.md). |
| **Instalar o Hue** |https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Veja [Instalar e usar o Hue em clusters HDInsight](hdinsight-hadoop-hue-linux.md). |
| **Instalar o Presto** |https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Veja [Instalar e usar o Presto em clusters HDInsight](hdinsight-hadoop-install-presto.md). |
| **Instalar Solr** |https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Consulte [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md). |
| **Instalar o Giraph** |https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Consulte [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md). |
| **Pré-carregar bibliotecas Hive** |https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Veja [Adicionar bibliotecas do Hive em clusters HDInsight](hdinsight-hadoop-add-hive-libraries.md). |
| **Instalar ou atualizar Mono** | https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash. Veja [Instalar ou atualizar o Mono no HDInsight](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Usar uma Ação de Script durante a criação do cluster

Esta seção fornece exemplos sobre maneiras diferentes hello, que você pode usar ações de script ao criar um cluster HDInsight.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>Usar uma ação de Script durante a criação do cluster de saudação portal do Azure

1. Comece criando um cluster como descrito em [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Pare quando chegar Olá __resumo do Cluster__ seção.

2. De saudação __resumo do Cluster__ seção, selecione Olá __editar__ link para __configurações avançadas__.

    ![Link Configurações avançadas](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. De saudação __configurações avançadas__ seção, selecione __ações de Script__. De saudação __ações de Script__ seção, selecione __+ novo envio__

    ![Enviar uma nova ação de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Saudação de uso __selecionar um script__ entrada tooselect um script predefinido. toouse um script personalizado, selecione __personalizado__ e, em seguida, fornecer Olá __nome__ e __Bash script URI__ para o seu script.

    ![Adicionar um script na forma de selecione script hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Olá a tabela a seguir descreve elementos Olá Olá formulário:

    | Propriedade | Valor |
    | --- | --- |
    | Selecionar um script | toouse seu próprio script, selecione __personalizado__. Caso contrário, selecione um dos scripts de saudação fornecida. |
    | Nome |Especifique um nome para a ação de script hello. |
    | URI do script Bash |Especifique Olá URI toohello script que é invocado toocustomize Olá cluster. |
    | Cabeçalho/Trabalho/Zookeeper |Especificar nós de saudação (**Head**, **trabalho**, ou **ZooKeeper**) no qual personalização Olá script é executado. |
    | parâmetros |Especifica parâmetros de hello, se exigido pelo script hello. |

    Saudação de uso __manter essa ação de script__ tooensure de entrada que Olá script é aplicada durante operações de dimensionamento.

5. Selecione __criar__ toosave script de saudação. Você pode usar __+ Enviar nova__ tooadd outro script.

    ![Várias ações de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Quando você terminar de adicionar scripts, use Olá __selecione__ botão e, em seguida, Olá __próximo__ botão tooreturn toohello __resumo do Cluster__ seção.

3. cluster de saudação toocreate, selecione __criar__ de saudação __resumo do Cluster__ seleção.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Usar uma Ação de Script em modelos do Gerenciador de Recursos do Azure

Olá exemplos nesta seção demonstram como toouse scripts ações com modelos do Gerenciador de recursos do Azure.

#### <a name="before-you-begin"></a>Antes de começar

* Para obter informações sobre como configurar uma estação de trabalho toorun HDInsight Powershell cmdlets, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).
* Para obter instruções sobre como toocreate modelos, consulte [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Se você ainda não utilizou o PowerShell do Azure com o Gerenciador de recursos, consulte [Uso do PowerShell do Azure com o Gerenciador de recursos do Azure](../azure-resource-manager/powershell-azure-resource-manager.md).

#### <a name="create-clusters-using-script-action"></a>Criar clusters usando a Ação de Script

1. Saudação de cópia local do modelo tooa a seguir em seu computador. Este modelo instala Giraph em nós headnodes e de trabalho Olá Olá cluster. Você também pode verificar se o modelo JSON Olá é válido. Cole o conteúdo do modelo no [JSONLint](http://jsonlint.com/), uma ferramenta online para validação de JSON.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Inicie o PowerShell do Azure e faça logon tooyour conta do Azure. Depois de fornecer suas credenciais, o comando Olá retorna informações sobre sua conta.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Se você tiver várias assinaturas, forneça a ID da assinatura Olá desejar toouse para implantação.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > Você pode usar `Get-AzureRmSubscription` tooget uma lista de todas as assinaturas associadas à sua conta, o que inclui a saudação ID da assinatura para cada um.

4. Se você não tiver um grupo de recursos existente, crie um grupo de recursos. Forneça o nome de saudação do grupo de recursos de saudação e local que você precisa para sua solução. Um resumo do novo grupo de recursos Olá é retornado.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. toocreate uma implantação para seu grupo de recursos, execute Olá **AzureRmResourceGroupDeployment novo** de comando e forneça os parâmetros necessários hello. os parâmetros de saudação incluem hello seguintes dados:

    * Um nome para sua implantação
    * nome de saudação do seu grupo de recursos
    * caminho de saudação ou modelo toohello URL que você criou.

  Se seu modelo exige quaisquer parâmetros, você deve passar esses parâmetros também. Nesse caso, tooinstall de ação de script hello R no cluster Olá não requer parâmetros.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    Você é valores de tooprovide solicitadas para parâmetros de saudação definidos no modelo de saudação.

1. Quando o grupo de recursos Olá tiver sido implantado, é exibido um resumo de implantação de saudação.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Se sua implantação falhar, você pode usar o hello cmdlets tooget informações sobre falhas de saudação a seguir.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Usar uma Ação de Script durante a criação do cluster no Azure PowerShell

Nesta seção, usamos Olá [AzureRmHDInsightScriptAction adicionar](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts usando a ação de Script toocustomize um cluster. Antes de prosseguir, verifique se você instalou e configurou o PowerShell do Azure. Para obter informações sobre como configurar uma estação de trabalho toorun HDInsight PowerShell cmdlets, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).

Olá script a seguir demonstra como tooapply uma ação de script ao criar um cluster usando o PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Pode levar vários minutos antes de saudação cluster é criado.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>Usar uma ação de Script durante a criação do cluster de saudação HDInsight .NET SDK

Olá HDInsight .NET SDK fornece bibliotecas de cliente que torna mais fácil toowork com HDInsight de um aplicativo .NET. Para obter um exemplo de código, consulte [baseados em Linux criar clusters HDInsight usando Olá .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-tooa-running-cluster"></a>Aplicar um tooa de ação de Script executando cluster

Nesta seção, Aprenda como tooapply script tooa ações executando o cluster.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Aplicar um tooa de ação de Script executando o cluster de saudação portal do Azure

1. De saudação [portal do Azure](https://portal.azure.com), selecione o cluster HDInsight.

2. Visão geral sobre cluster de HDInsight hello, selecione Olá **ações de Script** lado a lado.

    ![Bloco Ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Você também pode selecionar **todas as configurações** e, em seguida, selecione **ações de Script** da seção configurações da saudação.

3. Na parte superior de saudação da saudação seção ações de Script, selecione **enviar novo**.

    ![Adicionar um tooa de script executando cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Saudação de uso __selecionar um script__ entrada tooselect um script predefinido. toouse um script personalizado, selecione __personalizado__ e, em seguida, fornecer Olá __nome__ e __Bash script URI__ para o seu script.

    ![Adicionar um script na forma de selecione script hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Olá a tabela a seguir descreve elementos Olá Olá formulário:

    | Propriedade | Valor |
    | --- | --- |
    | Selecionar um script | toouse seu próprio script, selecione __personalizado__. Caso contrário, selecione um script fornecido. |
    | Nome |Especifique um nome para a ação de script hello. |
    | URI do script Bash |Especifique Olá URI toohello script que é invocado toocustomize Olá cluster. |
    | Cabeçalho/Trabalho/Zookeeper |Especificar nós de saudação (**Head**, **trabalho**, ou **ZooKeeper**) no qual personalização Olá script é executado. |
    | parâmetros |Especifica parâmetros de hello, se exigido pelo script hello. |

    Saudação de uso __manter essa ação de script__ script de saudação entrada toomake-se de que é aplicada durante operações de dimensionamento.

5. Por fim, use Olá **criar** cluster toohello do botão tooapply Olá script.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Aplicar um tooa de ação de Script que executa o cluster do Azure PowerShell

Antes de prosseguir, verifique se você instalou e configurou o PowerShell do Azure. Para obter informações sobre como configurar uma estação de trabalho toorun HDInsight PowerShell cmdlets, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).

Olá exemplo a seguir demonstra como tooapply um cluster em execução do script ação tooa:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Após a conclusão da operação de saudação, você receberá informações toohello semelhante texto a seguir:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Aplicar um tooa de ação de Script executando o cluster de saudação CLI do Azure

Antes de prosseguir, certifique-se de ter instalado e configurado Olá CLI do Azure. Para obter mais informações, consulte [instalação Olá CLI do Azure](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure modo do Gerenciador de recursos, use Olá na linha de comando Olá a seguir:

        azure config mode arm

2. Use Olá tooauthenticate tooyour assinatura do Azure a seguir.

        azure login

3. Use Olá tooapply de comando a seguir um tooa de ação de script executando cluster

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    Se você omitir parâmetros para esse comando, você será solicitado a fornecê-los. Se Olá script que você especificar com `-u` aceita parâmetros, você pode especificá-los usando Olá `-p` parâmetro.

    Os tipos de nós válidos são `headnode`, `workernode` e `zookeeper`. Se o script hello deve ser aplicada toomultiple tipos de nós, especificar os tipos de saudação separados por um ';'. Por exemplo: `-n headnode;workernode`.

    toopersist Olá script, adicione Olá `--persistOnSuccess`. Você também pode persistir script hello mais tarde usando `azure hdinsight script-action persisted set`.

    Após a conclusão do trabalho hello, você recebe saída toohello semelhante texto a seguir:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>Aplicar um tooa de ação do Script em execução usando a API REST do cluster

Consulte [Executar Ações de Script em um cluster em execução](https://msdn.microsoft.com/library/azure/mt668441.aspx).

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Aplicar um tooa de ação de Script executando o cluster de saudação HDInsight .NET SDK

Para obter um exemplo do uso de cluster de tooa Olá .NET SDK tooapply scripts, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Exibir o histórico, promover e rebaixar Ações de Script

### <a name="using-hello-azure-portal"></a>Usando Olá portal do Azure

1. De saudação [portal do Azure](https://portal.azure.com), selecione o cluster HDInsight.

2. Visão geral sobre cluster de HDInsight hello, selecione Olá **ações de Script** lado a lado.

    ![Bloco Ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Você também pode selecionar **todas as configurações** e, em seguida, selecione **ações de Script** da seção configurações da saudação.

4. Um histórico de scripts para este cluster é exibido na seção ações de Script de saudação. Essas informações incluem uma lista de scripts persistentes. Olá captura de tela abaixo, você verá que Olá Solr script foi executado nesse cluster. captura de tela de saudação não mostra todos os scripts persistentes.

    ![Seção Ações de Script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. A seleção de um script do histórico de saudação exibe a seção de propriedades de saudação para esse script. Da parte superior de saudação da tela hello, você pode executar novamente o script hello ou promovê-la.

    ![Propriedades de Ações de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. Você também pode usar o hello **...**  toohello à direita de entradas em ações de tooperform de seção Olá ações de Script.

    ![Ações de script... uso](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Usando o PowerShell do Azure

| Use a seguinte hello... | muito... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Recuperar informações sobre as ações de script persistentes |
| Get-AzureRmHDInsightScriptActionHistory |Recuperar um histórico de script ações aplicadas toohello cluster ou detalhes de um script específico |
| Set-AzureRmHDInsightPersistedScriptAction |Promova um ad hoc tooa de ação de script persistentes ação de script |
| Remove-AzureRmHDInsightPersistedScriptAction |Rebaixa uma ação do script persistidas ação tooan ad hoc |

> [!IMPORTANT]
> Usando `Remove-AzureRmHDInsightPersistedScriptAction` não desfaz ações Olá executadas por um script. Esse cmdlet remove apenas o sinalizador persistente hello.

Olá, script de exemplo a seguir demonstra como usar o hello cmdlets toopromote e rebaixar um script.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>Usando Olá CLI do Azure

| Use a seguinte hello... | muito... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Recuperar uma lista de ações de script persistente |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Recuperar informações sobre uma ação de script persistente específica |
| `azure hdinsight script-action history list <clustername>` |Recuperar um histórico de script ações aplicadas toohello cluster |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Recuperar informações sobre uma ação de script específica |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Promova um ad hoc tooa de ação de script persistentes ação de script |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Rebaixa uma ação do script persistidas ação tooan ad hoc |

> [!IMPORTANT]
> Usando `azure hdinsight script-action persisted delete` não desfaz ações Olá executadas por um script. Esse cmdlet remove apenas o sinalizador persistente hello.

### <a name="using-hello-hdinsight-net-sdk"></a>Usando Olá HDInsight .NET SDK

Para obter um exemplo de como usar o histórico do script tooretrieve Olá SDK .NET de um cluster, promover ou rebaixar scripts, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> Este exemplo também demonstra como tooinstall um aplicativo de HDInsight usando Olá .NET SDK.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Suporte para software livre utilizado em clusters do HDInsight

saudação de serviço do Microsoft Azure HDInsight usa um ecossistema de tecnologias de código-fonte aberto formado em torno do Hadoop. O Microsoft Azure fornece um nível geral de suporte para tecnologias de software livre. Para obter mais informações, consulte Olá **suporte escopo** seção Olá [site de perguntas frequentes sobre o suporte do Azure](https://azure.microsoft.com/support/faq/). Olá serviço HDInsight fornece um nível adicional de suporte para componentes internos.

Há dois tipos de componentes de código-fonte aberto que estão disponíveis no hello serviço HDInsight:

* **Componentes internos** -esses componentes são pré-instaladas em clusters de HDInsight e fornecem funcionalidade principal do cluster hello. Por exemplo, o ResourceManager YARN, linguagem de consulta de Hive hello (HiveQL) e biblioteca de Mahout Olá pertencem toothis categoria. Uma lista completa dos componentes do cluster está disponível em [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight](hdinsight-component-versioning.md).
* **Componentes personalizados** -você, como um usuário de cluster hello, instalar ou usar em sua carga de trabalho qualquer componente criado por você ou disponível na comunidade de saudação.

> [!WARNING]
> Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados. Microsoft Support ajuda tooisolate e resolver problemas relacionados toothese componentes.
>
> Componentes personalizados recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação. O suporte da Microsoft pode ser capaz de tooresolve problema de saudação ou eles podem solicitar que você canais disponíveis tooengage para tecnologias do código-fonte aberto Olá onde profundo conhecimento para que a tecnologia é encontrado. Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).

Olá serviço HDInsight fornece várias maneiras de componentes personalizados toouse. Olá se aplica mesmo nível de suporte, independentemente de como um componente é usado ou instalado em um cluster de saudação. Olá, lista a seguir descreve formas mais comuns de saudação que componentes personalizados podem ser usados em clusters de HDInsight:

1. Envio de trabalho - Hadoop ou outros tipos de trabalhos em execução ou usam componentes personalizados pode ser enviado toohello cluster.

2. Personalização de cluster - durante a criação do cluster, você pode especificar configurações adicionais e componentes personalizados que são instalados em nós de cluster de saudação.

3. Exemplos - para os componentes personalizados, Microsoft e outros podem fornecer exemplos de como esses componentes podem ser usados em clusters de HDInsight hello. Esses exemplos são fornecidos sem suporte.

## <a name="troubleshooting"></a>Solucionar problemas

Você pode usar informações de tooview Ambari web da interface do usuário conectadas por ações de script. Se o script hello falhar durante a criação do cluster, Olá logs também estão disponíveis na conta de armazenamento padrão de saudação associada Olá cluster. Esta seção fornece informações sobre como tooretrieve Olá registra usando ambas as opções.

### <a name="using-hello-ambari-web-ui"></a>Usando Olá Ambari Web UI

1. No seu navegador, navegue toohttps://CLUSTERNAME.azurehdinsight.net. Substitua CLUSTERNAME pelo nome de saudação do seu cluster HDInsight.

    Quando solicitado, insira o nome de conta de administrador de saudação (administrador) e a senha para o cluster de saudação. Você pode ter credenciais de administrador Olá tooreenter em um formulário da web.

2. Na barra de saudação na parte superior de saudação da página hello, selecione Olá **ops** entrada. É exibida uma lista das operações atuais e anteriores executada no cluster Olá por meio do Ambari.

    ![Barra de interface do usuário da Web do Ambari com o item "ops" selecionado](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Localizar entradas Olá com **executar\_customscriptaction** em Olá **operações** coluna. Essas entradas são criadas ao executar ações de Script hello.

    ![Captura de tela de operações](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    Olá tooview STDOUT e STDERR saída selecione Olá run\customscriptaction e fazer drill down em links de saudação. Esta saída é gerada quando a execução do script hello e pode conter informações úteis.

### <a name="access-logs-from-hello-default-storage-account"></a>Logs de acesso da conta de armazenamento saudação padrão

Se a criação do cluster Olá falhar devido a erro de ação de script tooa, Olá logs podem ser acessados de conta de armazenamento de cluster hello.

* Olá logs de armazenamento estão disponíveis em `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![Captura de tela de operações](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    Nesse diretório, Olá logs são organizados separadamente para o nó principal, workernode e zookeeper nós. Alguns exemplos incluem:

    * **Nó de cabeçalho** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Nó de trabalho** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Nó zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Todos os stdout e stderr de host correspondente Olá é carregado toohello conta de armazenamento. Há um **output-\*.txt** e um **errors-\*.txt** para cada ação de script. arquivo de saída-*. txt Olá contém informações sobre Olá URI do script de saudação que foi executado no host de saudação. Por exemplo,

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* É possível criar repetidamente um cluster de ação de script hello com o mesmo nome. Nesse caso, você pode distinguir logs relevantes de saudação com base no nome da pasta Data hello. Por exemplo, a estrutura de pasta de saudação para um cluster (mycluster) criado em datas diferentes aparece semelhante toohello entradas de log a seguir:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Se você criar um cluster de ação de script com hello mesmo nome no hello mesmo dia, você pode usar arquivos de log relevantes Olá exclusivo do prefixo tooidentify hello.

* Se você criar um cluster próximo 12:00 AM (meia-noite), é possível que os arquivos de log Olá abrangem em dois dias. Nesses casos, você ver duas pastas de datas diferentes para Olá mesmo cluster.

* Carregando contêiner padrão arquivos toohello de log pode demorar até minutos too5, especialmente para grandes clusters. Portanto, se desejar que os logs de saudação tooaccess, você não deve imediatamente Excluir cluster Olá se uma ação de script falhar.

### <a name="ambari-watchdog"></a>Ambari Watchdog

> [!WARNING]
> Não altere a senha de saudação do hello Ambari Watchdog (hdinsightwatchdog) no seu cluster HDInsight baseados em Linux. A alteração de senha Olá para esta conta quebra Olá capacidade toorun novo script de ações no cluster do HDInsight hello.

### <a name="cant-import-name-blobservice"></a>Não é possível importar o BlobService de nome

__Sintomas__: Olá falha da ação de script. Texto toohello semelhante erro a seguir é exibida quando você exibir operação Olá no Ambari:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Causa__: este erro ocorre se você atualizar o cliente de armazenamento do Azure Python Olá que está incluído no cluster do HDInsight hello. O HDInsight espera o cliente de Armazenamento do Azure 0.20.0.

__Resolução__: tooresolve esse erro, conectar-se manualmente usando de nó de cluster tooeach `ssh` e use Olá seguindo a versão do cliente de armazenamento correta do comando tooreinstall hello:

```
sudo pip install azure-storage==0.20.0
```

Para obter informações sobre conexão cluster toohello com SSH, consulte [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>O histórico de não mostra os scripts usados durante a criação do cluster

Se o cluster tiver sido criado antes de 15 de março de 2016, talvez você não veja uma entrada no histórico de Ação de Script. Se você redimensionar cluster Olá após 15 de março de 2016, Olá scripts usando durante a criação de cluster são exibidos no histórico conforme elas são aplicadas toonew nós no cluster hello como parte da saudação de operação de redimensionamento.

Há duas exceções:

* Se o cluster tiver sido criado antes de 1º de setembro de 2015. Esta data é quando as Ações de Script foram introduzidas. Qualquer cluster criado antes dessa data não poderia ter usado as Ações de Script para a criação do cluster.

* Se você usou várias ações de Script durante a criação do cluster e usado Olá mesmo nome para vários scripts ou Olá mesmo nome, mesmo URI, mas diferentes parâmetros para vários scripts. Nesses casos, você receberá Olá erro a seguir:

    Nenhum script de novas ações podem ser executado nesse cluster devido a nomes de script tooconflicting nos scripts existentes. Os nomes de script fornecidos na criação do cluster devem ser exclusivos. Os scripts existentes são executados no redimensionamento.

## <a name="next-steps"></a>Próximas etapas

* [Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions-linux.md)
* [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Adicionar o cluster do HDInsight tooan armazenamento adicional](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Estágios durante a criação de cluster"
