---
title: "recursos de automação de aaaAzure em soluções do OMS | Microsoft Docs"
description: "Soluções do OMS normalmente incluirá runbooks na automação do Azure tooautomate processos, como a coleta e processamento de dados de monitoramento.  Este artigo descreve como tooinclude runbooks e seus recursos relacionados em uma solução."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>Adicionando a solução de gerenciamento de OMS para tooan de recursos automação do Azure (visualização)
> [!NOTE]
> Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização. Qualquer esquema descrita abaixo é toochange de assunto.   


[Soluções de gerenciamento do OMS](operations-management-suite-solutions.md) geralmente inclui runbooks na automação do Azure tooautomate processos, como a coleta e processamento de dados de monitoramento.  Além disso toorunbooks, contas de automação inclui ativos como variáveis e agendas que dão suporte a runbooks Olá usado na solução de saudação.  Este artigo descreve como tooinclude runbooks e seus recursos relacionados em uma solução.

> [!NOTE]
> Olá exemplos neste artigo usam parâmetros e variáveis que são ambos soluções toomanagement necessárias ou comuns e descritos na [criando soluções de gerenciamento no OMS Operations Management Suite ()](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você já estiver familiarizado com hello informações a seguir.

- Como muito[criar uma solução de gerenciamento](operations-management-suite-solutions-creating.md).
- Olá a estrutura de um [arquivo de solução](operations-management-suite-solutions-solution-file.md).
- Como muito[criar modelos do Gerenciador de recursos](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>Conta de automação
Todos os recursos na Automação do Azure estão contidos em um [Conta de automação](../automation/automation-security-overview.md#automation-account-overview).  Conforme descrito em [OMS espaço de trabalho e a conta de automação](operations-management-suite-solutions.md#oms-workspace-and-automation-account) Olá conta de automação não está incluído na solução de gerenciamento de hello, mas deve existir antes de saudação solução estiver instalada.  Se não estiver disponível, Olá solução instalação falhará.

nome de saudação de cada recurso de automação inclui nome de saudação de sua conta de automação.  Isso é feito na solução de saudação com hello **accountName** parâmetro como Olá exemplo de um recurso de runbook a seguir.

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Runbooks
Você deve incluir todos os runbooks usados pela solução de saudação no arquivo de solução Olá para que eles são criados quando Olá solução estiver instalada.  Você não pode conter o corpo de saudação do runbook Olá no modelo de saudação, para que você deve publicar Olá runbook tooa local público em que ele possa ser acessado por qualquer usuário que instalar sua solução.

[Runbook de automação do Azure](../automation/automation-runbook-types.md) recursos têm um tipo de **Microsoft.Automation/automationAccounts/runbooks** e ter Olá estrutura a seguir. Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello. 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


Propriedades de saudação para runbooks são descritas Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| runbookType |Especifica os tipos de saudação de runbook hello. <br><br> Script – Script do PowerShell <br>PowerShell – Fluxo de trabalho do PowerShell <br> GraphPowerShell – Runbook de script do PowerShell gráfico <br> GraphPowerShellWorkflow – Runbook de fluxo de trabalho do PowerShell gráfico |
| logProgress |Especifica se [registros de progresso](../automation/automation-runbook-output-and-messages.md) devem ser gerados para Olá runbook. |
| logVerbose |Especifica se [registros detalhados](../automation/automation-runbook-output-and-messages.md) devem ser gerados para Olá runbook. |
| description |Descrição opcional para o runbook hello. |
| publishContentLink |Especifica o conteúdo de saudação do runbook hello. <br><br>URI - Uri toohello conteúdo de runbook hello.  Ele será um arquivo .ps1 para runbooks do PowerShell e Script e um arquivo de runbook gráfico exportado para um runbook gráfico.  <br> versão - versão de runbook Olá para o seu próprio controle. |


## <a name="automation-jobs"></a>Trabalhos de automação
Quando você inicia um runbook na Automação do Azure, isso cria um trabalho de automação.  Você pode adicionar um automação trabalho tooyour solução tooautomatically início um runbook quando a solução de gerenciamento de saudação está instalada.  Esse método é geralmente usados toostart runbooks que são usados para a configuração inicial de solução de saudação.  toostart um runbook em intervalos regulares, criar um [agenda](#schedules) e um [agenda de trabalho](#job-schedules)

Recursos de trabalho têm um tipo de **Microsoft.Automation/automationAccounts/jobs** e ter Olá estrutura a seguir.  Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello. 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

Propriedades de saudação para trabalhos de automação são descritas Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| runbook |Entidade de nome único com o nome de saudação do hello runbook toostart. |
| parâmetros |Entidade para cada valor de parâmetro exigido pelo runbook hello. |

trabalho de saudação inclui nome do runbook hello e qualquer toobe de valores de parâmetro enviado toohello runbook.  trabalho de saudação deve [dependem](operations-management-suite-solutions-solution-file.md#resources) runbook Olá que ele está sendo iniciado desde Olá runbook deve ser criado antes do trabalho de saudação.  Caso tenha vários runbooks que devam ser iniciados, você pode definir a ordem deles com um trabalho que dependa de qualquer outro trabalho que deva ser executado primeiro.

nome de saudação de um recurso de trabalho deve conter um GUID que normalmente é atribuído por um parâmetro.  Você pode ler mais sobre os parâmetros GUID em [Criando soluções no OMS (Operations Management Suite)](operations-management-suite-solutions-solution-file.md#parameters).  


## <a name="certificates"></a>Certificados
[Certificados de automação do Azure](../automation/automation-certificates.md) têm um tipo de **Microsoft.Automation/automationAccounts/certificates** e ter Olá estrutura a seguir. Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



Propriedades de saudação para recursos de certificados são descritas Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| base64Value |Valor de base 64 para o certificado de saudação. |
| impressão digital |Impressão digital do certificado de saudação. |



## <a name="credentials"></a>Credenciais
[As credenciais de automação do Azure](../automation/automation-credentials.md) têm um tipo de **Microsoft.Automation/automationAccounts/credentials** e ter Olá estrutura a seguir.  Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello. 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

Propriedades de saudação para recursos de credencial são descritas Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| userName |Nome de usuário para credencial hello. |
| Senha |Senha da credencial de saudação. |


## <a name="schedules"></a>Agendas
[Agendas de automação do Azure](../automation/automation-schedules.md) têm um tipo de **Microsoft.Automation/automationAccounts/schedules** e ter Olá Olá estrutura a seguir. Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

Propriedades de saudação para recursos de agendamento são descritas Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| description |Descrição opcional para a agenda de saudação. |
| startTime |Especifica a hora de início de saudação de uma agenda como um objeto DateTime. Uma cadeia de caracteres pode ser fornecida se ele puder ser convertido tooa DateTime válido. |
| isEnabled |Especifica se Olá agenda está habilitada. |
| intervalo |tipo de saudação do intervalo de agendamento de saudação.<br><br>dia<br>hora |
| frequência |Frequência de Olá agenda deve ser disparada no número de dias ou horas. |

As agendas devem ter uma hora de início com um valor maior que Olá hora atual.  Você não pode fornecer esse valor com uma variável, desde que você teria que não há como saber quando ele é toobe será instalado.

Use uma das duas estratégias a seguir ao usar os recursos de agendamento em uma solução de saudação.

- Use um parâmetro de hora de início de saudação da agenda de saudação.  Essa ação solicitará Olá usuário tooprovide um valor ao instalar a solução de saudação.  Caso tenha vários agendamentos, você poderá usar um único valor de parâmetro para mais de um deles.
- Crie agendas hello usando um runbook que é iniciado quando Olá solução estiver instalada.  Isso elimina a necessidade de saudação do hello usuário toospecify uma hora, mas você não pode conter agenda Olá em sua solução para que ela será removida quando a solução de saudação é removida.


### <a name="job-schedules"></a>Agendas de trabalho
Os recursos de agendamento vinculam um runbook a um agendamento.  Eles têm um tipo de **Microsoft.Automation/automationAccounts/jobSchedules** e ter Olá Olá estrutura a seguir.  Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


Propriedades de saudação para agendas de trabalho são descritas Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| nome do agendamento |Único **nome** entidade com o nome de saudação da agenda de saudação. |
| nome do runbook  |Único **nome** entidade com o nome de saudação do runbook hello.  |



## <a name="variables"></a>variáveis
[As variáveis de automação do Azure](../automation/automation-variables.md) têm um tipo de **Microsoft.Automation/automationAccounts/variables** e ter Olá estrutura a seguir.  Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

Propriedades de saudação para recursos variáveis são descritas Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| description | Descrição opcional para a variável de saudação. |
| isEncrypted | Especifica se a variável de saudação deve ser criptografado. |
| type | Essa propriedade atualmente está sem efeito.  tipo de dados de saudação da variável Olá será determinado pelo valor de saudação inicial. |
| valor | Valor de variável de saudação. |

> [!NOTE]
> Olá **tipo** propriedade atualmente não tem nenhum efeito na variável hello está sendo criado.  saudação de tipo de dados para a variável de saudação será determinado pelo valor de saudação.  

Se você definir o valor inicial de saudação de variável Olá, ela deve ser definida como Olá tipo de dados correto.  Olá, a tabela a seguir fornece Olá diferentes tipos de dados permitidos e sua sintaxe.  Observe que os valores em JSON são esperados tooalways ser colocado entre aspas com caracteres especiais entre aspas hello.  Por exemplo, um valor de cadeia de caracteres deve ser especificado pela cadeia de caracteres hello aspas (usando o caractere de escape de saudação (\\)) enquanto um valor numérico deve ser especificado com um conjunto de aspas.

| Tipo de dados | Descrição | Exemplo | Resolve muito|
|:--|:--|:--|:--|
| string   | Coloque o valor entre aspas duplas.  | "\"Olá, Mundo\"" | "Olá, Mundo" |
| numérico  | Valor numérico com aspas simples.| "64" | 64 |
| Booliano  | **true** ou **false** entre aspas.  Observe que esse valor deve estar em minúsculas. | "true" | verdadeiro |
| datetime | Valor de data serializada.<br>Você pode usar o cmdlet ConvertTo-Json Olá toogenerate PowerShell esse valor para uma determinada data.<br>Exemplo: get-date "5/24/2017 13:14:57" \| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>Módulos
Sua solução de gerenciamento não precisa toodefine [módulos global](../automation/automation-integration-modules.md) usado por seus runbooks porque sempre estarão disponíveis em sua conta de automação.  É necessário tooinclude um recurso para qualquer outro módulo usado por seus runbooks.

[Módulos de integração](../automation/automation-integration-modules.md) têm um tipo de **Microsoft.Automation/automationAccounts/modules** e ter Olá estrutura a seguir.  Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


Propriedades de saudação para recursos do módulo são descritas Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| contentLink |Especifica o conteúdo de saudação do módulo de saudação. <br><br>URI - Uri toohello conteúdo Olá módulo.  Ele será um arquivo .ps1 para runbooks do PowerShell e Script e um arquivo de runbook gráfico exportado para um runbook gráfico.  <br> versão - versão do módulo de saudação para seu próprio controle. |

Olá runbook deve depender Olá tooensure de recurso de módulo que foi criado antes de runbook hello.

### <a name="updating-modules"></a>Atualizando módulos
Se você atualizar uma solução de gerenciamento que inclui um runbook que usa uma agenda e Olá nova versão da solução tem um novo módulo usado por esse runbook, runbook Olá pode usar a versão antiga saudação do módulo de saudação.  Você deve incluir Olá runbooks em sua solução a seguir e criar um trabalho toorun-as antes de quaisquer outros runbooks.  Isso garantirá que todos os módulos são atualizados como Olá necessária antes de carregar os runbooks.

* [Atualização ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) garantirá que todos os módulos de saudação usados por runbooks em sua solução estão na versão mais recente hello.  
* [ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) registrar novamente todos Olá agenda recursos tooensure Olá runbooks vinculados toothem com módulos mais recentes do uso hello.




## <a name="sample"></a>Amostra
A seguir está um exemplo de uma solução que incluem que inclui Olá recursos a seguir:

- Runbook.  É um exemplo de runbook armazenado em um repositório público do GitHub.
- Trabalho de automação que inicia o runbook hello quando Olá solução estiver instalada.
- Agenda e trabalho de agendamento toostart Olá runbook em intervalos regulares.
- Certificado.
- Credencial.
- Variável.
- Módulo.  Isso é hello [OMSIngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) para gravar dados tooLog análise. 

Olá exemplo usa [parâmetros de solução padrão](operations-management-suite-solutions-solution-file.md#parameters) variáveis que normalmente seriam usados em uma solução como oposição toohardcoding valores nas definições de recursos de saudação.


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a>Próximas etapas
* [Adicionar uma solução do modo de exibição tooyour](operations-management-suite-solutions-resources-views.md) toovisualize coletados dados.
