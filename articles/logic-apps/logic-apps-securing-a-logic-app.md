---
title: "aaaSecure acessar os aplicativos lógicos tooAzure | Microsoft Docs"
description: "Adicione a segurança para proteger o acesso tootriggers, entradas e saídas, parâmetros de ação e serviços usados com fluxos de trabalho em aplicativos do Azure lógica."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>Proteger o acesso a aplicativos de lógica de tooyour

Há muitos toohelp disponíveis ferramentas proteger seu aplicativo lógico.

* Protegendo o acesso tootrigger um lógica de aplicativo (gatilho de solicitação de HTTP)
* Segurança de acesso toomanage, editar ou ler uma lógica de aplicativo
* Protegendo o acesso toocontents de entradas e saídas para uma execução
* Proteger parâmetros ou entradas em ações em um fluxo de trabalho
* Protegendo o acesso tooservices que recebe solicitações de um fluxo de trabalho

## <a name="secure-access-tootrigger"></a>Acesso seguro tootrigger

Quando você trabalha com um aplicativo de lógica que é acionado em uma solicitação HTTP ([solicitação](../connectors/connectors-native-reqres.md) ou [Webhook](../connectors/connectors-native-webhook.md)), você pode restringir o acesso para que somente clientes autorizados podem acionar Olá lógica aplicativo. Todas as solicitações para um aplicativo lógico são criptografadas e protegidas por SSL.

### <a name="shared-access-signature"></a>Assinatura de acesso compartilhado

Cada ponto de extremidade de solicitação para um aplicativo de lógica inclui um [assinatura de acesso compartilhado (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) como parte da URL de saudação. Cada URL contém um parâmetro de consulta `sp`, `sv`, e `sig`. As permissões são especificadas por `sp`, e correspondem tooHTTP métodos permitidos, `sv` é Olá versão usada toogenerate, e `sig` é usado tooauthenticate tootrigger de acesso. assinatura de saudação é gerada usando o algoritmo de saudação SHA256 com uma chave de segredo em todos os caminhos de URL hello e propriedades. chave secreta Olá nunca é exposta e publicado e são mantidos criptografados e armazenados como parte do aplicativo de lógica de saudação. Seu aplicativo lógico somente autorizará gatilhos que contém uma assinatura válida criada com a chave secreta hello.

#### <a name="regenerate-access-keys"></a>Regenerar chaves de acesso

Você pode regenerar uma nova chave segura na qualquer momento por meio do portal Olá de API REST ou o Azure. Todas as URLs atuais que foram geradas anteriormente usando a chave antiga Olá são toofire invalidada e não autorizados Olá lógica aplicativo.

1. No portal do Azure de Olá, abra o aplicativo de lógica de Olá deseja tooregenerate uma chave
1. Clique em Olá **chaves de acesso** item de menu no **configurações**
1. Escolha tooregenerate chave hello e processo Olá concluída

Recuperar após a regeneração de URLs são assinados com a nova chave de acesso hello.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Criar URLs de retorno de chamada com uma data de expiração

Se você estiver compartilhando Olá URL com terceiros, você pode gerar URLs com chaves específicas e datas de expiração conforme necessário. Você pode facilmente reverter chaves de, ou garantir acesso toofire um aplicativo é restrito tooa determinado período de tempo. Você pode especificar uma data de validade para uma URL por meio de saudação [lógica aplicativos REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

No corpo do hello, incluir a propriedade de saudação `NotAfter` como uma cadeia de caracteres JSON data, que retorna uma URL de retorno de chamada que só é válida até Olá `NotAfter` data e hora.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>Criar URLs com chave secreta primária ou secundária

Quando você gera ou lista de URLs de retorno de chamada para baseado em solicitação gatilhos, você também pode especificar qual URL de saudação toosign toouse chave.  Você pode gerar uma URL assinada por uma chave específica por meio de saudação [lógica aplicativos REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) da seguinte maneira:

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

No corpo do hello, incluir a propriedade de saudação `KeyType` como `Primary` ou `Secondary`.  Isso retorna uma URL assinada pela chave segura de saudação especificado.

### <a name="restrict-incoming-ip-addresses"></a>Restringir endereços IP de entrada

Além disso toohello assinatura de acesso compartilhado, talvez você queira toorestrict chamar um aplicativo lógico somente de clientes específicos.  Por exemplo, se você gerenciar seu ponto de extremidade por meio do gerenciamento de API do Azure, você pode restringir lógica Olá aplicativo tooonly aceitar solicitação de hello quando a solicitação hello proveniente Olá endereço IP de instância de gerenciamento de API.

Essa configuração pode ser configurada nas configurações de aplicativo hello lógica:

1. No portal do Azure de Olá, abra o aplicativo de lógica de Olá deseja tooadd as restrições de endereço IP
1. Clique em Olá **configuração de controle de acesso** item de menu no **configurações**
1. Especificar lista de saudação do toobe de intervalos de endereço IP aceito pelo gatilho Olá

Um intervalo IP válido assume o formato de saudação `192.168.1.1/255`. Se você desejar Olá lógica aplicativo tooonly incêndio como um aplicativo lógica aninhada, selecione Olá **somente outros aplicativos lógicos** opção. Esta opção grava um recurso de toohello matriz em branco, que significa que somente chamadas de saudação próprio serviço incêndio (pai lógica aplicativos) com êxito.

> [!NOTE]
> Você ainda pode executar um aplicativo de lógica com um gatilho de solicitação por meio da API REST de saudação / gerenciamento `/triggers/{triggerName}/run` independentemente de IP. Esse cenário requer autenticação em relação a saudação API REST do Azure, e todos os eventos apareceria em Olá Log de auditoria do Azure. Defina políticas de controle de acesso de apropriadamente.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Definir intervalos de IP na definição de recurso Olá

Se você estiver usando um [modelo de implantação](logic-apps-create-deploy-template.md) tooautomate suas implantações, as configurações de intervalo IP hello podem ser configuradas no modelo de recurso hello.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Adicionar Azure Active Directory, OAuth, ou outra proteção

tooadd autorização mais protocolos na parte superior de um aplicativo lógico, [gerenciamento do Azure API](https://azure.microsoft.com/services/api-management/) oferece avançados de monitoramento, segurança, política e documentação para qualquer ponto de extremidade com hello recurso tooexpose um aplicativo lógico como uma API. Gerenciamento de API do Azure podem expor um ponto de extremidade público ou privado para o aplicativo lógico hello, o que poderia usar o Active Directory do Azure, certificado, OAuth ou outros padrões de segurança. Quando uma solicitação é recebida, o gerenciamento de API do Azure encaminha aplicativo hello solicitação toohello lógico (executando qualquer transformações necessárias ou restrições em andamento). Você pode usar o intervalo IP entrado Olá Olá lógica aplicativo tooonly configurações permitem que Olá lógica aplicativo toobe disparado do gerenciamento de API.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>Proteger o acesso toomanage ou editar os aplicativos lógicos

Você pode restringir o acesso toomanagement operações em um aplicativo lógico para que somente usuários específicos ou grupos sejam tooperform capaz de operações no recurso de saudação. Aplicativos lógicos usam hello Azure [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md) de recursos e pode ser personalizada com hello mesmas ferramentas.  Há algumas funções internas que você pode atribuir os membros de sua assinatura tooas também:

* **Lógica aplicativo Colaborador** -fornece acesso tooview, editar e atualizar um aplicativo lógico.  Não é possível remover o recurso de saudação ou executar operações de administração.
* **Operador de aplicativo de lógica** - pode exibir o aplicativo de lógica de saudação e histórico de execução e habilitar/desabilitar.  Não é possível editar ou atualizar definição de saudação.

Você também pode usar [bloqueio de recurso do Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent alterar ou excluir aplicativos lógicos. Esse recurso é tooprevent valiosos recursos de produção de alterações ou exclusões.

## <a name="secure-access-toocontents-of-hello-run-history"></a>Acesso seguro toocontents de saudação histórico de execução

Você pode restringir o acesso toocontents de entradas ou saídas em intervalos de endereço IP do anteriores é executado toospecific.  

Todos os dados dentro de uma execução de fluxo de trabalho são criptografados em trânsito e em repouso. Quando um histórico de toorun chamada é feito, o serviço de saudação autentica a solicitação hello e fornece links toohello solicitação e saídas e entradas de resposta. Esse link pode ser protegidas solicitações de forma que só tooview conteúdo de um intervalo de endereço IP designado retornar o conteúdo de saudação. Você pode usar essa funcionalidade para controle de acesso adicional. Você pode até mesmo especificar um endereço IP como `0.0.0.0` para que ninguém possa acessar entradas/saídas. Somente uma pessoa com permissões de administrador pode remover essa restrição, fornecendo a possibilidade de saudação para conteúdo de tooworkflow de acesso 'just-in-time'.

Essa configuração pode ser definida nas configurações de recurso de saudação de saudação portal do Azure:

1. No portal do Azure de Olá, abra o aplicativo de lógica de Olá deseja tooadd as restrições de endereço IP
1. Clique em Olá **configuração de controle de acesso** item de menu no **configurações**
1. Especificar Olá lista de intervalos de endereços IP para acesso toocontent

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Definir intervalos de IP na definição de recurso Olá

Se você estiver usando um [modelo de implantação](logic-apps-create-deploy-template.md) tooautomate suas implantações, as configurações de intervalo IP hello podem ser configuradas no modelo de recurso hello.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Proteger parâmetros e entradas em um fluxo de trabalho

Talvez você queira tooparameterize alguns aspectos de uma definição de fluxo de trabalho para implantação em ambientes. Além disso, alguns parâmetros podem estar seguros parâmetros que você não quiser tooappear ao editar um fluxo de trabalho, como uma ID de cliente e o segredo do cliente para [autenticação do Active Directory do Azure](../connectors/connectors-native-http.md#authentication) de uma ação HTTP.

### <a name="using-parameters-and-secure-parameters"></a>Usar parâmetros e proteger parâmetros

tooaccess Olá valor de um parâmetro de recurso em tempo de execução, hello [linguagem de definição de fluxo de trabalho](http://aka.ms/logicappsdocs) fornece um `@parameters()` operação. Além disso, você pode [especificar parâmetros em um modelo de implantação de recursos de saudação](../azure-resource-manager/resource-group-authoring-templates.md#parameters). Porém, se você especificar o tipo de parâmetro hello como `securestring`, parâmetro hello não será retornado com rest Olá Olá da definição do recurso e não poderão ser acessado exibindo recursos Olá após a implantação.

> [!NOTE]
> Se o parâmetro é usado em cabeçalhos de saudação ou corpo de uma solicitação, o parâmetro hello pode estar visível acessando o histórico de saudação executar e solicitações HTTP de saída. Verifique se tooset suas políticas de acesso ao conteúdo adequadamente.
> Cabeçalhos de autorização nunca são visíveis por meio de entradas ou saídas. Se segredo hello está sendo usado há, segredo Olá não é recuperável.

#### <a name="resource-deployment-template-with-secrets"></a>Modelo de implantação de recursos com segredos

Olá, exemplo a seguir mostra uma implantação que faz referência a um parâmetro seguro de `secret` em tempo de execução. Em um arquivo de parâmetros separados, você pode especificar o valor de ambiente Olá para Olá `secret`, ou use [Azure o Gerenciador de recursos KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve segredos na hora da implantação.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>Proteger o acesso tooservices solicitações de recebimento de um fluxo de trabalho

Há muitos toohelp de maneiras segura de que qualquer aplicativo de lógica de saudação do ponto de extremidade precisa tooaccess.

### <a name="using-authentication-on-outbound-requests"></a>Usar a autenticação em solicitações de saída

Ao trabalhar com um HTTP, HTTP + Swagger (API Open) ou ação de Webhook, você pode adicionar autenticação toohello solicitação. Você pode incluir a autenticação básica, autenticação de certificado ou autenticação do Azure Active Directory. Obter detalhes sobre como tooconfigure essa autenticação pode ser encontrada [neste artigo](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-toologic-app-ip-addresses"></a>Restringir o acesso toologic aplicativo endereços

Todas as chamadas de aplicativos lógicos vêm de um conjunto específico de endereços IP por região. Você pode adicionar filtragem adicional tooonly aceitar as solicitações dos endereços IP de designado. Para obter uma lista desses endereços IP, consulte [limites e configuração do aplicativo lógico](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>Conectividade local

Aplicativos lógicos fornecem integração com vários tooprovide serviços segura e confiável de comunicação no local.

#### <a name="on-premises-data-gateway"></a>Gateway de dados local

Muitos conectores gerenciados para os aplicativos lógicos fornecem conectividade segura entre sistemas de tooon locais, incluindo o sistema de arquivos, SQL, SharePoint, DB2 e muito mais. gateway Olá transmite dados de fontes locais em canais criptografados por meio de saudação do Azure Service Bus. Todo o tráfego originado como proteger o tráfego de saída do agente de gateway de saudação. Saiba mais sobre [como funciona o gateway de dados Olá](logic-apps-gateway-install.md#gateway-cloud-service).

#### <a name="azure-api-management"></a>Gerenciamento de API do Azure

[Gerenciamento de API do Azure](https://azure.microsoft.com/services/api-management/) tem opções de conectividade local, incluindo a integração de rota expressa e VPN site a site para sistemas de tooon locais de proxy e comunicação seguras. Olá lógica de aplicativo Designer, você pode selecionar uma API exposta do gerenciamento de API do Azure dentro de um fluxo de trabalho, fornecendo acesso rápido a sistemas locais tooon rapidamente.

#### <a name="hybrid-connections-from-azure-app-service"></a>Conexões híbridas do Serviço de Aplicativo do Azure

Você pode usar o recurso de conexão de híbrido do hello local para a API do Azure e Web apps toocommunicate local.  Obter detalhes sobre conexões híbridas e como pode ser encontrado tooconfigure [neste artigo](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Próximas etapas
[Criar um modelo de implantação](logic-apps-create-deploy-template.md)  
[Manipulação de exceção](logic-apps-exception-handling.md)  
[Monitorar seus aplicativos lógicos](logic-apps-monitor-your-logic-apps.md)  
[Diagnosticando falhas e problemas nos aplicativos lógicos](logic-apps-diagnosing-failures.md)  
