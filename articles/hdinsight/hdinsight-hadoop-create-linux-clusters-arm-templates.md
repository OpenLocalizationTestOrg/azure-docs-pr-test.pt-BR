---
title: clusters de aaaCreate Hadoop usando modelos - HDInsight do Azure | Microsoft Docs
description: Saiba como toocreate clusters de HDInsight usando modelos do Gerenciador de recursos
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>Criar clusters Hadoop no HDInsight usando modelos do Resource Manager
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Neste artigo, você aprenderá várias maneiras toocreate HDInsight do Azure clusters com modelos do Gerenciador de recursos do Azure. Para saber mais, confira [Implantar um aplicativo com o modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-template-deploy.md). toolearn sobre outras ferramentas de criação de cluster e recursos, clique no seletor de guia Olá na parte superior da saudação dessa página ou consulte [métodos de criação de Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

instruções de saudação toofollow neste artigo, você precisará:

* Uma [assinatura do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell e/ou CLI do Azure.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a>Modelos do Gerenciador de Recursos
Um modelo do Gerenciador de recursos torna fácil toocreate Olá a seguir para seu aplicativo em uma única operação coordenado:
* Clusters HDInsight e seus recursos dependentes (como a conta de armazenamento padrão Olá)
* Outros recursos (como o banco de dados do Azure SQL toouse Apache Sqoop)

No modelo de hello, você define os recursos de saudação que são necessários para o aplicativo hello. Você também pode especificar valores de tooinput de parâmetros de implantação para ambientes diferentes. Olá modelo consiste em JSON e expressões que você use tooconstruct valores para sua implantação.

É possível encontrar amostras de modelo do HDInsight em [Modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight). Usar da plataforma cruzada [código do Visual Studio](https://code.visualstudio.com/#alt-downloads) com hello [extensão do Gerenciador de recursos](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) ou um modelo do hello de toosave do editor de texto em um arquivo na estação de trabalho. Você aprenderá como toocall Olá modelo usando métodos diferentes.

Para obter mais informações sobre modelos do Gerenciador de recursos, consulte Olá artigos a seguir:

* [Criar modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Implantar um aplicativo com o modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>Gerar modelos

Usando Olá portal do Azure, você pode configurar todas as propriedades de saudação de um cluster e, em seguida, salve o modelo de saudação antes de implantá-lo. Em seguida, você pode reutilizar o modelo hello.

**toogenerate um modelo usando Olá portal do Azure**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **novo** no menu esquerdo Olá **Intelligence + análise**e, em seguida, clique em **HDInsight**.
3. Seguem Olá instruções tooenter propriedades. Você pode usar o hello **criação rápida** ou hello **personalizado** opção.
4. Em Olá **resumo** , clique em **baixar modelo e parâmetros de**:

    ![Criação de cluster de Download do modelo do Resource Manager pelo Hadoop HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    Você verá uma lista de arquivo de modelo hello, arquivo de parâmetros e código amostras usadas toodeploy Olá modelo:

    ![Criação de cluster de Opções de download do modelo do Resource Manager pelo Hadoop HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    A partir daqui, baixar modelo hello, salvá-lo tooyour biblioteca de modelos ou implantar o modelo de saudação.

    tooaccess um modelo de biblioteca, clique em **mais serviços** no menu esquerdo hello e clique **modelos** (em Olá **outros** categoria).

    > [!Note]
    > arquivo de modelo e parâmetros de saudação deve ser usado juntas. Caso contrário, você poderá obter resultados inesperados. Por exemplo, Olá padrão **clusterKind** o valor da propriedade é sempre **hadoop**, apesar do que você especificar antes de baixar o modelo de saudação.



## <a name="deploy-with-powershell"></a>Implantação com o PowerShell

Esse procedimento cria um cluster Hadoop no HDInsight.

1. Salve o arquivo JSON de saudação em Olá [apêndice](#appx-a-arm-template) tooyour estação de trabalho. Olá script do PowerShell, nome de arquivo hello é `C:\HDITutorials-ARM\hdinsight-arm-template.json`.
2. Defina as variáveis e parâmetros de saudação se necessário.
3. Execute o modelo hello usando Olá script do PowerShell a seguir:

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    saudação de script do PowerShell configura apenas o nome de cluster hello. o nome de conta de armazenamento Olá é embutido no modelo de saudação. Você está senha de usuário de cluster de saudação tooenter solicitada. (nome de usuário saudação padrão é **admin**.) Você também é senha de usuário solicitada tooenter Olá SSH. (nome de usuário do SSH saudação padrão é **sshuser**.)  

Para obter mais informações, veja [Implantar com o PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).

## <a name="deploy-with-cli"></a>Implantar com a CLI
saudação de exemplo a seguir usa a interface de linha de comando (CLI) do Azure. Ele cria um cluster e os respectivos contêiner e conta de armazenamento dependente chamando um modelo do Resource Manager:

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

Você está tooenter solicitada:
* nome do cluster Hello.
* senha de usuário de cluster Hello. (nome de usuário saudação padrão é **admin**.)
* senha de usuário SSH Hello. (nome de usuário do SSH saudação padrão é **sshuser**.)

saudação de código a seguir fornece parâmetros embutido:

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a>Implantar com hello API REST
Consulte [implantar com a API REST de saudação](../azure-resource-manager/resource-group-template-deploy-rest.md).

## <a name="deploy-with-visual-studio"></a>Implantação com o Visual Studio
 Use o Visual Studio toocreate um projeto do grupo de recursos e implantá-lo tooAzure por meio da interface do usuário hello. Selecione o tipo de saudação de tooinclude de recursos em seu projeto. Esses recursos são adicionados automaticamente o modelo do Gerenciador de recursos de toohello. projeto Olá também fornece um modelo de saudação do toodeploy de script do PowerShell.

Para uma introdução toousing Visual Studio com grupos de recursos, consulte [criando e implantando grupos de recursos do Azure com o Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu um cluster HDInsight toocreate de várias maneiras. toolearn mais, consulte Olá artigos a seguir:

* Para obter um exemplo de implantação de recursos por meio da biblioteca de cliente .NET hello, consulte [implantar recursos usando as bibliotecas .NET e um modelo](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Para obter um exemplo detalhado de implantação de um aplicativo, confira [Provisionar e implantar microsserviços de forma previsível no Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).
* Para obter orientação sobre a implantação de ambientes de toodifferent sua solução, consulte [ambientes de desenvolvimento e teste no Microsoft Azure](../solution-dev-test-environments.md).
* toolearn sobre seções de saudação do modelo do Azure Resource Manager hello, consulte [criar modelos](../azure-resource-manager/resource-group-authoring-templates.md).
* Para obter uma lista de funções de saudação, você pode usar em um modelo do Gerenciador de recursos do Azure, consulte [funções de modelo](../azure-resource-manager/resource-group-template-functions.md).

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a>Apêndice: Gerenciador de recursos modelo toocreate um cluster Hadoop
Hello seguinte modelo do Azure Resource Manager cria um cluster Hadoop baseado em Linux com conta de armazenamento do Azure dependentes hello.

> [!NOTE]
> Este exemplo inclui informações de configuração para o metastore do Hive e o metastore do Oozie. Remover seção hello ou configurar a seção Olá antes de usar o modelo de saudação.
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a>Apêndice: Gerenciador de recursos modelo toocreate um cluster Spark

Esta seção fornece um modelo do Gerenciador de recursos que você pode usar toocreate um cluster HDInsight Spark. Esse modelo inclui configurações para `spark-defaults` e `spark-thrift-sparkconf` (para clusters Spark 1.6) e `spark2-defaults` e `spark2-thrift-sparkconf` (para clusters Spark 2). Além disso, toothis, HDInsight calcula e define as configurações como `spark.executor.instances`, `spark.executor.memory`, e `spark.executor.cores` com base no tamanho do cluster hello. 

Se você definir qualquer um parâmetro em uma seção como parte do próprio modelo hello, HDInsight não calcular e definir Olá outros parâmetros de saudação mesma seção. Por exemplo, o parâmetro `spark.executor.instances` está em Olá `spark-defaults` configuração. Se você definir outro parâmetro (por exemplo, `spark.yarn.exector.memoryOverhead`) no hello `spark-defaults` configuração HDInsight não calcular e definir Olá `spark.executor.instances` parâmetro também.

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
