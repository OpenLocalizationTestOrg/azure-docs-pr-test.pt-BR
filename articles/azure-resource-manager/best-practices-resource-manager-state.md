---
title: valores complexos de aaaPass entre modelos do Azure | Microsoft Docs
description: Mostra recomendado abordagens para usar dados de estado de tooshare objetos complexos com modelos de Gerenciador de recursos do Azure e vinculado.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>Tooand de estado de compartilhamento de modelos do Gerenciador de recursos do Azure
Este tópico mostra as melhores práticas para gerenciar e compartilhar o estado em modelos. Olá parâmetros e variáveis mostrados neste tópico são exemplos de tipo de saudação de objetos que você pode definir tooconveniently organizar seus requisitos de implantação. A partir desses exemplos, você pode implementar seus próprios objetos com valores de propriedade que façam sentido para o seu ambiente.

Este tópico faz parte de um whitepaper mais amplo. baixar tooread Olá completo papel, [World classe recurso Gerenciador de modelos de considerações e práticas comprovadas](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

## <a name="provide-standard-configuration-settings"></a>Fornecer configurações padrão
Em vez de oferecer um modelo que oferece total flexibilidade e inúmeras variações, um padrão comum é tooprovide uma seleção de configurações conhecidas. Na verdade, os usuários podem selecionar tamanhos de camiseta padrão, como área restrita, pequeno, médio e grande. Outros exemplos de tamanhos de camiseta são ofertas de produtos, como community edition ou enterprise edition. Em outros casos, podem se tratar de configurações de uma tecnologia específicas para uma determinada carga de trabalho - como mapear/reduzir ou no SQL.

Com objetos complexos, você pode criar variáveis que contêm conjuntos de dados, às vezes conhecidos como "recipientes de propriedade" e usar essa declaração de recurso Olá dados toodrive em seu modelo. Essa abordagem fornece boas configurações conhecidas, de tamanhos variados que são pré-configurados para os clientes. Sem configurações conhecidas, os usuários do modelo de saudação devem determinar dimensionamento do cluster em seu próprios, fator em restrições de recursos de plataforma e fazer matemática tooidentify Olá resultante de contas de armazenamento e outros recursos de particionamento (devido tamanho toocluster e restrições de recursos). Além disso toomaking uma melhor experiência de cliente hello, algumas configurações conhecidas são toosupport mais fácil e podem ajudar a fornecer um nível mais alto de densidade.

Olá mostrado no exemplo a seguir como toodefine variáveis que contêm objetos complexos para representar os conjuntos de dados. coleções de saudação definem valores que são usados para o tamanho da máquina virtual, as configurações de rede, configurações do sistema operacional e configurações de disponibilidade.

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

Observe que Olá **tshirtSize** variável concatena o tamanho de camisa Olá fornecido por meio de um parâmetro (**pequeno**, **médio**, **grande**) texto toohello **tshirtSize**. Você pode usar essa variável de objeto complexo associado Olá tooretrieve variável para que o tamanho do camisa.

Você pode fazer referência a essas variáveis posteriormente no modelo de saudação. Olá capacidade tooreference chamado variáveis e suas propriedades simplifica a sintaxe do modelo hello e torna fácil toounderstand contexto. saudação de exemplo a seguir define toodeploy um recurso por meio de objetos de saudação mostrados anteriormente tooset valores. Por exemplo, Olá tamanho da VM é definido pela recuperação do valor de saudação de `variables('tshirtSize').vmSize` enquanto o valor de saudação para o tamanho do disco Olá é recuperado do `variables('tshirtSize').diskSize`. Além disso, Olá URI para um modelo vinculado é definido com valor de saudação para `variables('tshirtSize').vmTemplate`.

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a>Passar o modelo de tooa de estado
Você pode compartilhar o estado em um modelo por meio de parâmetros fornecidos diretamente durante a implantação.

Olá tabela parâmetros de listas usadas nos modelos a seguir.

| Nome | Valor | Descrição |
| --- | --- | --- |
| location |Cadeia de caracteres de uma lista restrita de regiões do Azure |local de saudação onde os recursos de saudação são implantados. |
| storageAccountNamePrefix |Cadeia de caracteres |Nome DNS exclusivo para Olá conta de armazenamento em que os discos da VM Olá são colocados |
| domainName |Cadeia de caracteres |Nome de domínio do hello jumpbox VM publicamente acessível no formato Olá: **{domainName}. { local}.cloudapp.com** por exemplo: **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |Cadeia de caracteres |Nome de usuário para Olá VMs |
| adminPassword |Cadeia de caracteres |Senha de saudação VMs |
| tshirtSize |Cadeia de caracteres de uma lista restrita de tamanhos de camiseta oferecidos |Olá denominado tooprovision de tamanho de unidade de escala. Por exemplo, "Pequeno", "Médio", "Grande" |
| virtualNetworkName |Cadeia de caracteres |Nome de rede virtual Olá Olá consumidor deseja toouse. |
| enableJumpbox |Cadeia de caracteres de uma lista restrita (habilitada/desabilitada) |Parâmetro identifica se tooenable um jumpbox para o ambiente de saudação. Valores: "habilitado", "desabilitado" |

Olá **tshirtSize** parâmetro usado na seção anterior Olá é definido como:

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a>Passar modelos de toolinked de estado
Ao se conectar toolinked modelos, você geralmente usa uma combinação de estático e gerado variáveis.

### <a name="static-variables"></a>Variáveis estáticas
Variáveis estáticas geralmente são valores de base de tooprovide usadas, como URLs, que são usados em um modelo.

Em Olá seguinte trecho do modelo, `templateBaseUrl` Especifica o local de raiz de saudação para modelo Olá no GitHub. linha seguinte Olá cria uma nova variável `sharedTemplateUrl` que concatena a URL base Olá com nome conhecido de saudação do modelo de recursos compartilhados hello. Abaixo da linha, uma variável de objeto complexo toostore usado um tamanho de camisa, onde é URL base Olá toohello concatenado conhecido local do modelo de configuração e armazenadas em Olá `vmTemplate` propriedade.

benefício de saudação dessa abordagem é que se Olá modelo local será alterado, basta variável estática do hello toochange em um único local, que passa em modelos Olá vinculado.

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a>Variáveis geradas
Em variáveis de toostatic de adição, diversas variáveis são geradas dinamicamente. Esta seção identifica alguns dos tipos comuns de saudação de variáveis gerados.

#### <a name="tshirtsize"></a>tshirtSize
Você está familiarizado com essa variável gerado de exemplos de saudação acima.

#### <a name="networksettings"></a>networkSettings
Em uma saudação de capacidade, recurso ou modelo de solução de ponta a ponta no escopo, vinculados modelos normalmente criam recursos que existem em uma rede. Uma abordagem simples é toouse as configurações de rede objeto complexo toostore e passá-las toolinked modelos.

Um exemplo de configurações de rede de comunicação pode ser visto abaixo.

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a>availabilitySettings
Recursos criados em modelos vinculados geralmente são colocados em um conjunto de disponibilidade. Em Olá exemplo a seguir, Olá nome do conjunto de disponibilidade for especificado e também Olá domínio de falha e toouse de contagem de domínio de atualização.

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

Se você precisar de vários conjuntos de disponibilidade (por exemplo, um de nós mestres) e outro para os nós de dados, você pode usar um nome como um prefixo, especifique vários conjuntos de disponibilidade ou siga modelo Olá mostrado anteriormente para a criação de uma variável para um tamanho de camisa específico.

#### <a name="storagesettings"></a>storageSettings
Detalhes de armazenamento geralmente são compartilhados com modelos vinculados. No exemplo abaixo, a saudação um *storageSettings* objeto fornece detalhes sobre Olá nomes de conta e o contêiner de armazenamento.

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
Com modelos vinculados, talvez seja necessário toopass configurações de sistema operacional toovarious tipos de nós em todos os tipos de configuração diferentes. Um objeto complexo é uma informações do sistema operacional toostore e compartilhamento de maneira fácil e também torna mais fácil toosupport várias opções de sistema operacional para implantação.

Olá, exemplo a seguir mostra um objeto para *osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
Variável gerada, *machineSettings* é um objeto complexo que contém uma mistura de variáveis principais para criar uma VM. variáveis de saudação incluem o nome de usuário administrador e senha, um prefixo para nomes VM hello e uma referência de imagem do sistema operacional.

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

Observe que *osImageReference* recupera Olá valores de saudação *osSettings* variável definida no modelo principal hello. Isso significa que você pode facilmente alterar o sistema operacional de saudação para uma VM — completamente ou com base na preferência de saudação de um consumidor de modelo.

#### <a name="vmscripts"></a>vmScripts
Olá *vmScripts* contém detalhes sobre toodownload de scripts de saudação do objeto e executar em uma instância VM, incluindo referências externas e internas. Fora de referências incluem infraestrutura hello.
Referências internas incluem hello instalado software instalado e configuração.

Use Olá *scriptsToDownload* toodownload toohello VM de scripts de saudação do toolist de propriedade. Esse objeto também contém argumentos de linha de toocommand de referências para diferentes tipos de ações. Essas ações incluem executar saudação padrão instalação para cada nó individual, uma instalação que é executado depois que todos os nós são implantados e quaisquer scripts adicionais que podem ser tooa específico, considerando o modelo.

Este exemplo é de um toodeploy MongoDB, que exige uma arbitrador toodeliver alta disponibilidade do modelo usado. Olá *arbiterNodeInstallCommand* foi adicionado muito*vmScripts* tooinstall arbitrador de saudação.

seção de variáveis de saudação é onde você pode encontrar variáveis Olá que definem o script de saudação de tooexecute Olá texto específico com valores adequados hello.

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>Retornar o estado de um modelo
Não só pode transmitir dados em um modelo, você também pode compartilhar dados toohello back chamada modelo. Em Olá **gera** seção de um modelo vinculado, você pode fornecer os pares chave/valor que podem ser consumidos pelo modelo de origem de saudação.

Olá exemplo a seguir mostra como toopass Olá endereço IP privado gerado em um modelo vinculado.

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

No modelo principal do hello, você pode usar esses dados com hello sintaxe a seguir:

    "[reference('master-node').outputs.masterip.value]"

Você pode usar essa expressão em Olá saídas seção ou seção de recursos de saudação do modelo principal hello. Você não pode usar a expressão Olá na seção de variáveis de saudação porque ele se baseia no estado de tempo de execução de saudação. tooreturn este valor de modelo principal hello, use:

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

Para um exemplo de como usar o hello gera seção um modelo vinculado tooreturn de discos de dados para uma máquina virtual, consulte [criando vários discos de dados para uma máquina Virtual](resource-group-create-multiple.md).

## <a name="define-authentication-settings-for-virtual-machine"></a>Definir configurações de autenticação para uma máquina virtual
Você pode usar o hello mesmo padrão mostrado anteriormente configurações toospecify Olá autenticação as definições de configuração para uma máquina virtual. Você pode criar um parâmetro para passar no tipo de saudação de autenticação.

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

Você adicionar variáveis de saudação diferentes tipos de autenticação e uma variável toostore o tipo usado para essa implantação com base no valor de saudação do parâmetro hello.

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

Ao definir a máquina virtual de saudação, você definir Olá **osProfile** toohello variável que você criou.

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>Próximas etapas
* toolearn sobre seções de saudação do modelo hello, consulte [criação de modelos de Gerenciador de recursos do Azure](resource-group-authoring-templates.md)
* toosee Olá funções que estão disponíveis em um modelo, consulte [funções de modelo do Gerenciador de recursos do Azure](resource-group-template-functions.md)
