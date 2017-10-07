---
title: "soluções de gerenciamento de aaaCreating no OMS Operations Management Suite () | Microsoft Docs"
description: "Soluções de gerenciamento de estendem a funcionalidade de saudação do Operations Management Suite (OMS), fornecendo os cenários de pacotes de gerenciamento que os clientes podem adicionar tootheir espaço de trabalho do OMS.  Este artigo fornece detalhes sobre como você pode criar toobe de soluções de gerenciamento usados em seu próprio ambiente ou feitas clientes tooyour disponíveis."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>Criando um arquivo de solução de gerenciamento no OMS (Operations Management Suite) (Versão prévia)
> [!NOTE]
> Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização. Qualquer esquema descrita abaixo é toochange de assunto.  

As soluções de gerenciamento do OMS (Operations Management Suite) são implementadas como [modelos do Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).  tarefa principal de saudação em aprender como soluções de gerenciamento tooauthor é necessário saber como muito[criar um modelo de](../azure-resource-manager/resource-group-authoring-templates.md).  Este artigo fornece detalhes exclusivos dos modelos usados para soluções e como recursos de solução típica tooconfigure.


## <a name="tools"></a>Ferramentas

Você pode usar qualquer toowork do editor de texto com arquivos de solução, mas é recomendável aproveitar os recursos de saudação fornecidos no Visual Studio ou o código do Visual Studio, conforme descrito em Olá artigos a seguir.

- [Criando e implantando grupos de recursos do Azure por meio do Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Trabalhando com Modelos do Azure Resource Manager no Visual Studio Code](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>Estrutura
estrutura básica de saudação de um arquivo de solução de gerenciamento é Olá mesmo que um [Gerenciador de recursos de modelo](../azure-resource-manager/resource-group-authoring-templates.md#template-format) que é da seguinte maneira.  Cada uma das seções de saudação abaixo descreve os elementos de nível superior de saudação e e seu conteúdo em uma solução.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>parâmetros
[Parâmetros](../azure-resource-manager/resource-group-authoring-templates.md#parameters) são valores que você precisa de usuário Olá ao instalar a solução de gerenciamento de saudação.  Eles são parâmetros padrão que todas as soluções terão; além disso, você pode adicionar parâmetros adicionais conforme necessário para sua solução específica.  Como os usuários fornecerá valores de parâmetro ao instalar a solução dependem parâmetro específico hello e como solução hello está sendo instalada.

Quando um usuário instala a solução de gerenciamento por meio de saudação [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) ou [modelos de início rápido do Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) são solicitada tooselect um [OMS espaço de trabalho e a conta de automação ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  Estes são valores de saudação toopopulate usados de cada um dos parâmetros de saudação padrão.  não é solicitado ao usuário de saudação toodirectly fornecer valores para parâmetros de saudação padrão, mas são solicitadas tooprovide valores para parâmetros adicionais.

Quando o usuário Olá instala sua solução [outro método](operations-management-suite-solutions.md#finding-and-installing-management-solutions), eles devem fornecer um valor para todos os parâmetros padrão e todos os parâmetros adicionais.

Um parâmetro de exemplo é mostrado abaixo.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

Olá, a tabela a seguir descreve os atributos de saudação de um parâmetro.

| Atributo | Descrição |
|:--- |:--- |
| type |Tipo de dados para o parâmetro hello. controle de entrada Hello exibido para o usuário Olá depende Olá tipo de dados.<br><br>bool – Caixa suspensa<br>cadeia de caracteres – caixa de texto<br>int – Caixa de texto<br>securestring – Campo de senha<br> |
| categoria |Categoria opcional para o parâmetro hello.  Parâmetros no hello mesma categoria são agrupados juntos. |
| controle |Funcionalidade adicional para parâmetros de cadeia de caracteres.<br><br>datetime – O controle datetime é exibido.<br>GUID - valor Guid é gerado automaticamente e o parâmetro hello não é exibido. |
| description |Descrição opcional para o parâmetro hello.  Exibido em um parâmetro de toohello informações balão Avançar. |

### <a name="standard-parameters"></a>Parâmetros padrão
Olá tabela a seguir lista os parâmetros padrão do hello todas as soluções de gerenciamento.  Esses valores são populados para usuário Olá em vez de solicitar para eles quando sua solução é instalada da saudação Azure Marketplace ou Quickstart modelos.  usuário Olá deve fornecer valores para que eles se solução Olá é instalada com o outro método.

> [!NOTE]
> interface do usuário Olá em modelos do Azure Marketplace e Quickstart hello está esperando nomes de parâmetro hello na tabela de saudação.  Se você usar nomes de parâmetros diferentes, em seguida, Olá usuário será solicitado para eles, e eles não serão preenchidos automaticamente.
>
>

| Parâmetro | Tipo | Descrição |
|:--- |:--- |:--- |
| accountName |string |Nome da conta de Automação do Azure. |
| pricingTier |string |Tipo de preço do espaço de trabalho do Log Analytics e da conta de Automação do Azure. |
| regionId |string |Região do hello conta de automação do Azure. |
| solutionName |string |Nome da solução de saudação.  Se você estiver implantando sua solução por meio de modelos de início rápido, em seguida, você deve definir solutionName como um parâmetro para que você pode definir uma cadeia de caracteres em vez disso, exigindo Olá usuário toospecify um. |
| workspaceName |string |O nome do espaço de trabalho do Log Analytics. |
| workspaceRegionId |string |Região do espaço de trabalho de análise de Log de saudação. |


A seguir está a estrutura Olá Olá padrão de parâmetros de que você pode copiar e colar no arquivo de solução.  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


Consulte tooparameter valores em outros elementos de solução de saudação com sintaxe Olá **parâmetros ('nome do parâmetro')**.  Por exemplo, tooaccess Olá nome do espaço de trabalho, você usaria **parameters('workspaceName')**

## <a name="variables"></a>variáveis
[Variáveis](../azure-resource-manager/resource-group-authoring-templates.md#variables) são valores que você usará no restante da saudação de solução de gerenciamento de saudação.  Esses valores não são toohello exposto usuário instalar Olá solução.  Eles são autor, Olá tooprovide pretendida com um único local onde eles podem gerenciar os valores que podem ser usados várias vezes em toda a solução de saudação. Você deve colocar qualquer solução de tooyour específico de valores em variáveis como toohard contrário codificá-los em Olá **recursos** elemento.  Isso torna o código hello mais legível e permite que você tooeasily alterar esses valores em versões posteriores.

A seguir está um exemplo de um elemento **variables** com parâmetros típicos usado em soluções.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Consulte toovariable valores por meio da solução de saudação com sintaxe Olá **variáveis ('nome da variável')**.  Por exemplo, tooaccess Olá SolutionName variável, você usaria **variables('SolutionName')**.

Você também pode definir variáveis complexas que têm vários conjuntos de valores.  Elas são particularmente úteis em soluções de gerenciamento, quando você estiver definindo várias propriedades para diferentes tipos de recursos.  Por exemplo, você poderia reestruturar variáveis de solução Olá mostrados acima toohello a seguir.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Nesse caso, você pode consultar toovariable valores por meio da solução de saudação com sintaxe Olá **variables('variable name').property**.  Por exemplo, tooaccess Olá variável do nome da solução, você usaria **variables('Solution'). Nome**.

## <a name="resources"></a>Recursos
[Recursos](../azure-resource-manager/resource-group-authoring-templates.md#resources) definir Olá recursos diferentes que instalará e configurará sua solução de gerenciamento.  Isso será Olá maior e mais complexo parte do modelo de saudação.  Você pode obter estrutura hello e uma descrição completa dos elementos de recurso no [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).  Recursos diferentes que normalmente são definidos são detalhados em outros artigos desta documentação. 


### <a name="dependencies"></a>Dependências
Olá **dependsOn** elementos especifica um [dependência](../azure-resource-manager/resource-group-define-dependencies.md) em outro recurso.  Quando Olá solução estiver instalada, um recurso não é criado até que todas as suas dependências foram criadas.  Por exemplo, sua solução pode [iniciar um runbook](operations-management-suite-solutions-resources-automation.md#runbooks) quando ele é instalado usando um [recurso de trabalho](operations-management-suite-solutions-resources-automation.md#automation-jobs).  recursos de trabalho Olá são dependentes Olá runbook recurso toomake se que esse runbook Olá foi criado antes de saudação trabalho é criado.

### <a name="oms-workspace-and-automation-account"></a>Espaço de trabalho do OMS e Conta de automação
Soluções de gerenciamento exigem um [espaço de trabalho do OMS](../log-analytics/log-analytics-manage-access.md) toocontain modos de exibição e um [conta de automação](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks e recursos relacionados.  Eles devem estar disponíveis antes Olá recursos na solução de saudação são criados e não devem ser definidos na solução de saudação em si.  usuário Olá será [especificar um espaço de trabalho e a conta](operations-management-suite-solutions.md#oms-workspace-and-automation-account) quando eles implantar sua solução, mas como autor hello, você deve considerar Olá pontos a seguir.

## <a name="solution-resource"></a>Recurso da solução
Cada solução requer uma entrada de recurso no hello **recursos** elemento que define a solução de saudação em si.  Isso terá um tipo de **Microsoft.OperationsManagement/solutions** e ter Olá estrutura a seguir. Isso inclui [parâmetros padrão](#parameters) e [variáveis](#variables) que são propriedades de toodefine geralmente usados da solução hello.


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a>Dependências
recursos de solução de saudação devem ter uma [dependência](../azure-resource-manager/resource-group-define-dependencies.md) em todos os outros recursos na solução Olá porque eles precisão tooexist antes da criação de solução de saudação.  Faça isso adicionando uma entrada para cada recurso no hello **dependsOn** elemento.

### <a name="properties"></a>Propriedades
recursos de solução de saudação tem propriedades de saudação em Olá a tabela a seguir.  Isso inclui recursos de saudação referenciado e contido por solução Olá que define como os recursos de saudação é gerenciado depois Olá solução estiver instalada.  Cada recurso na solução Olá deve ser listado na qualquer Olá **referencedResources** ou hello **containedResources** propriedade.

| Propriedade | Descrição |
|:--- |:--- |
| workspaceResourceId |ID do espaço de trabalho de análise de Log de saudação na forma de saudação  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nome do espaço de trabalho\>*. |
| referencedResources |Lista de recursos na solução de saudação que não devem ser removidos quando Olá solução é removida. |
| containedResources |Lista de recursos na solução de saudação que deve ser removido quando a solução de saudação é removida. |

exemplo Hello acima é uma solução com um runbook, um agendamento e exibição.  agenda Hello e runbook são *referenciado* em Olá **propriedades** elemento para que eles não são removidos quando Olá solução é removida.  Olá exibição é *contidos* para que ele será removido quando a solução de saudação é removida.

### <a name="plan"></a>Plano
Olá **plano** entidade do recurso de solução de saudação tem propriedades de saudação em Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| name |Nome da solução de saudação. |
| version |Versão da solução Olá conforme determinado pelo autor da saudação. |
| product |Solução de saudação do tooidentify de cadeia de caracteres exclusiva. |
| publicador |Editor do Gerenciador de saudação. |



## <a name="sample"></a>Amostra
Você pode exibir exemplos de arquivos de solução com um recurso de solução a saudação locais a seguir.

- [Recursos de automação](operations-management-suite-solutions-resources-automation.md#sample)
- [Recursos de pesquisa e alerta](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>Próximas etapas
* [Adicionar alertas e pesquisas salvas](operations-management-suite-solutions-resources-searches-alerts.md) tooyour solução de gerenciamento.
* [Adicionar modos de exibição](operations-management-suite-solutions-resources-views.md) tooyour solução de gerenciamento.
* [Adicionar runbooks e outros recursos de automação](operations-management-suite-solutions-resources-automation.md) tooyour solução de gerenciamento.
* Obter detalhes de saudação do [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Pesquise entre os [Modelos de Início Rápido do Azure](https://azure.microsoft.com/documentation/templates) para obter exemplos de diferentes modelos do Resource Manager.
