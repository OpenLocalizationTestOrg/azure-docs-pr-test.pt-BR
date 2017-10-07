---
title: aaaGet iniciado com a CLI do Azure para o lote | Microsoft Docs
description: "Obter uma introdução rápida toohello comandos de lote em CLI do Azure para gerenciamento de recursos de serviço de lote do Azure"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Gerenciar recursos do Lote com a CLI do Azure

Olá 2.0 do CLI do Azure é a nova experiência de linha de comando do Azure para gerenciar recursos do Azure. Ela pode ser usada em Windows, Linux e macOS. 2.0 do CLI do Azure é otimizado para gerenciar e administrar os recursos do Azure da linha de comando hello. Você pode usar o hello CLI do Azure toomanage suas contas de lote do Azure e os recursos de toomanage como pools, trabalhos e tarefas. Com hello CLI do Azure, você pode gerar um script muitas Olá Olá de mesmas tarefas que você executa com APIs de lote, o portal do Azure e cmdlets do PowerShell do lote.

Este artigo fornece uma visão geral do uso da [CLI do Azure versão 2.0](https://docs.microsoft.com/cli/azure/overview) com o Lote. Consulte [Introdução ao Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) para obter uma visão geral do uso de saudação CLI com o Azure.

A Microsoft recomenda usar Olá última versão do hello CLI do Azure, versão 2.0. Para saber mais sobre a versão 2.0, consulte [CLI do Azure 2.0 agora disponível](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).

## <a name="set-up-hello-azure-cli"></a>Configurar Olá CLI do Azure

Olá tooinstall CLI do Azure, execute as etapas de saudação descritas em [instalação Olá CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli.md).

> [!TIP]
> Recomendamos que você atualize sua instalação de CLI do Azure com frequência tootake vantagem do serviço de atualizações e aprimoramentos.
> 
> 

## <a name="command-help"></a>Ajuda de comando

Você pode exibir o texto de ajuda para cada comando em Olá CLI do Azure, acrescentando `-h` toohello comando. Omita as outras opções. Por exemplo:

* Ajuda de tooget para Olá `az` de comando, digite:`az -h`
* tooget uma lista de todos os comandos de lote no hello CLI, use:`az batch -h`
* tooget ajuda sobre como criar uma conta em lotes, digite:`az batch account create -h`

Em caso de dúvida, use Olá `-h` opção de linha de comando tooget ajuda sobre qualquer comando CLI do Azure.

> [!NOTE]
> Versões anteriores do hello CLI do Azure usado `azure` toopreface um comando CLI. Na versão 2.0, todos os comandos agora são precedidos por `az`. Ser tooupdate-se de que seus scripts toouse Olá nova sintaxe com a versão 2.0.
>
>  

Além disso, consulte a documentação de referência toohello CLI do Azure para obter detalhes sobre [comandos de CLI do Azure para o lote](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Fazer logon e autenticar

Olá toouse CLI do Azure com o lote, você precisa toolog no e autenticar. Há dois toofollow de etapas simples:

1. **Faça logon no Azure.** Fazendo logon no Azure fornece acesso a comandos do Gerenciador de recursos tooAzure, incluindo [serviço de gerenciamento de lote](batch-management-dotnet.md) comandos.  
2. **Faça logon em sua conta do Lote.** Fazer logon no seu dá conta de lote você acessar tooBatch comandos de serviço.   

### <a name="log-in-tooazure"></a>Faça logon no tooAzure

Há alguns toolog de maneiras diferentes para o Azure, descrito detalhadamente na [fazer logon com o Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Fazer logon interativamente](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in). Faça logon interativamente quando você estiver executando os comandos de CLI do Azure da linha de comando hello.
2. [Fazer logon com uma entidade de serviço](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal). Faça logon com uma entidade de serviço quando você estiver executando comandos da CLI do Azure de um script ou aplicativo.

Para fins de saudação deste artigo, mostramos como toolog no Azure interativamente. Tipo [logon az](https://docs.microsoft.com/cli/azure/#login) na linha de comando hello:

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

Olá `az login` comando retorna um token que você pode usar tooauthenticate, conforme mostrado aqui. Execute Olá instruções fornecidas tooopen uma página da web e enviar tooAzure token hello:

![Faça logon no tooAzure](./media/batch-cli-get-started/az-login.png)

exemplos de saudação listados no hello [scripts de shell de exemplo](#sample-shell-scripts) seção também mostra como toostart sua sessão de CLI do Azure fazendo logon interativamente no Azure. Depois de você ter conectado, você pode chamar comandos toowork com recursos de gerenciamento em lote, incluindo contas, chaves, pacotes de aplicativos e cotas do lote.  

### <a name="log-in-tooyour-batch-account"></a>Faça logon no tooyour conta em lotes

toouse Olá CLI do Azure toomanage recursos de lote, como pools, trabalhos e tarefas, você precisa toolog em sua conta de lote e autentica. toolog em toohello serviço de lote, use Olá [logon de conta de lote az](https://docs.microsoft.com/cli/azure/batch/account#login) comando. 

Você tem duas opções para autenticação na sua conta do Lote:

- **Usando a autenticação do Azure AD (Azure Active Directory)** 

    Autenticar com o AD do Azure é o padrão de hello quando você usa Olá CLI do Azure com o lote e recomendado na maioria dos cenários. 
    
    Quando você efetuar logon interativamente, conforme descrito na seção anterior Olá em tooAzure, suas credenciais são armazenadas em cache, para que Olá CLI do Azure pode fazer o logon tooyour usando as mesmas credenciais de conta do lote. Se você efetuar logon em tooAzure usando uma entidade de serviço, essas credenciais também são toolog usado em tooyour conta do lote.

    Uma vantagem do Azure AD é que ele oferece RBAC (controle de acesso baseado em função). Com o RBAC, acesso do usuário depende de sua função atribuída, em vez de estarem ou não possui chaves de conta Olá. Em vez de gerenciar chaves de conta, você pode gerenciar funções RBAC e permitir que o Azure AD lide com autenticação e acesso.  

    Autenticar com o AD do Azure é necessária se você criou sua conta de lote do Azure com o modo de alocação do pool definido too'User assinatura '. 

    toolog em tooyour lote conta usando o Azure AD, chame Olá [logon de conta de lote az](https://docs.microsoft.com/cli/azure/batch/account#login) comando: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Usando a autenticação de Chave compartilhada**

    [Autenticação de chave compartilhada](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) serviço de lote usa tooauthenticate comandos de CLI do Azure para Olá das chaves de acesso à sua conta.

    Se você estiver criando scripts de CLI do Azure tooautomate chamados comandos de lote, você pode usar a autenticação de chave compartilhada ou uma entidade de serviço do AD do Azure. Em alguns cenários, o uso da autenticação de Chave Compartilhada pode ser mais simples do que criar uma entidade de serviço.  

    toolog usando a autenticação de chave compartilhada incluem hello `--shared-key-auth` opção na linha de comando hello:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

exemplos de saudação listados no hello [scripts de shell de exemplo](#sample-shell-scripts) seção mostrará como toolog em sua conta de lote com hello CLI do Azure usando AD do Azure e a chave compartilhada.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Usar modelos CLI do Lote do Azure e o arquivo de transferência (Versão prévia)

Você pode usar o hello CLI do Azure toorun lote trabalhos ponta a ponta sem escrever código. Suporte para arquivos de modelo do lote Criando pools, trabalhos e tarefas com hello CLI do Azure. Você também pode usar arquivos de entrada de trabalho Olá CLI do Azure tooupload toohello conta de armazenamento do Azure associada a saudação conta de lote e baixar arquivos de saída de trabalho dele. Para saber mais, confira [Usar modelos da CLI do Lote do Azure e Transferência de Arquivos (Versão prévia)](batch-cli-templates.md).

## <a name="sample-shell-scripts"></a>Scripts de shell de exemplo

scripts de exemplo Hello listadas na Olá Mostrar tabela a seguir como os comandos toouse CLI do Azure com o serviço de lote hello e tarefas comuns de tooaccomplish de serviço de gerenciamento em lote. Esses scripts de exemplo incluir vários comandos de saudação disponíveis no hello CLI do Azure para o lote. 

| Script | Observações |
|---|---|
| [Criar uma conta do Lote](./scripts/batch-cli-sample-create-account.md) | Cria uma conta do Lote e associa uma conta de armazenamento. |
| [Adicionar um aplicativo](./scripts/batch-cli-sample-add-application.md) | Adiciona um aplicativo e carrega os binários do pacote.|
| [Gerenciar pools do Lote](./scripts/batch-cli-sample-manage-pool.md) | Demonstra como criar, redimensionar e gerenciar pools. |
| [Executar um trabalho e tarefas com o Lote](./scripts/batch-cli-sample-run-job.md) | Demonstra como executar um trabalho e adicionar tarefas. |

## <a name="json-files-for-resource-creation"></a>Arquivos JSON para a criação de recursos

Quando você criar recursos de lote como pools e trabalhos, você pode especificar um arquivo JSON que contém a configuração do recurso novo Olá em vez de passar os parâmetros como opções de linha de comando. Por exemplo:

```azurecli
az batch pool create my_batch_pool.json
```

Embora você possa criar a maioria dos recursos de lote usando apenas as opções de linha de comando, alguns recursos exigem que você especifique um arquivo no formato JSON que contém detalhes do recurso hello. Por exemplo, você deve usar um arquivo JSON se você quiser que os arquivos de recursos de toospecify para uma tarefa inicial.

Olá toosee sintaxe JSON necessário toocreate um recurso, consulte toohello [referência da API REST de lote] [ rest_api] documentação. Cada "adicionar *tipo de recurso*" tópico na referência da API REST de saudação contém scripts de JSON de exemplo para a criação desse recurso. Você pode usar esses scripts JSON de exemplo como modelo para JSON arquivos toouse com hello CLI do Azure. Por exemplo, toosee Olá sintaxe JSON para a criação do pool, consulte muito[adicionar uma conta do pool de tooan][rest_add_pool].

Para um exemplo de script que especifica um arquivo JSON, consulte [Executar um trabalho e tarefas com o Lote](./scripts/batch-cli-sample-run-job.md).

> [!NOTE]
> Se você especificar um arquivo JSON quando você cria um recurso, quaisquer outros parâmetros que você especificou na linha de comando Olá para esse recurso são ignorados.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Consultas eficientes para recursos do Lote

Cada tipo de recurso do Lote dá suporte a um comando `list` que consulta sua conta do Lote e lista os recursos desse tipo. Por exemplo, você pode listar os pools de saudação em suas tarefas de conta e hello em um trabalho:

```azurecli
az batch pool list
az batch task list --job-id job001
```

Quando você consulta o serviço de lote Olá com um `list` operação, você pode especificar um valor de saudação do OData cláusula toolimit dos dados retornados. Como toda a filtragem ocorre no lado do servidor, somente dados Olá que solicitar cruzem durante a transmissão hello. Usar largura de banda de toosave essas cláusulas (e, portanto, o tempo) quando você executa operações de lista.

Olá tabela a seguir descreve as cláusulas de OData Olá suportadas pelo serviço de lote de saudação:

| Cláusula | Descrição |
|---|---|
| `--select-clause [select-clause]` | Retorna um subconjunto de propriedades para cada entidade. |
| `--filter-clause [filter-clause]` | Retorna apenas as entidades que correspondem a saudação especificado expressão do OData. |
| `--expand-clause [expand-clause]` | Obtém informações de entidade de saudação em uma única chamada REST subjacente. Olá expanda cláusula atualmente suporta apenas Olá `stats` propriedade. |

Para obter um exemplo de script que mostra como toouse uma cláusula de OData, consulte [executar um trabalho e tarefas com lotes](./scripts/batch-cli-sample-run-job.md).

Para obter mais informações sobre como executar consultas da lista eficiente com cláusulas de OData, consulte [consultar o serviço de lote do Azure Olá com eficiência](batch-efficient-list-queries.md).

## <a name="troubleshooting-tips"></a>Dicas de solução de problemas

Olá dicas a seguir podem ajudar a quando estiver solucionando problemas de CLI do Azure:

* Use `-h` tooget **texto de Ajuda** para qualquer comando CLI
* Use `-v` e `-vv` toodisplay **detalhado** saída de comando. Olá quando `-vv` sinalizador for incluído, Olá CLI do Azure exibe Olá reais solicitações e respostas REST. Essas opções são úteis para exibir a saída completa do erro.
* Você pode exibir **comando saída como JSON** com hello `--json` opção. Por exemplo, o `az batch pool show pool001 --json` exibe propriedades do pool001 no formato JSON. Você pode copiar e modificar toouse essa saída em um `--json-file` (consulte [arquivos JSON](#json-files) anteriormente neste artigo).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* Olá [Fórum do lote] [ batch_forum] é monitorada por membros da equipe em lotes. Você pode publicar suas perguntas nesse local caso tenha problemas ou queira obter ajuda com uma operação específica.

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre Olá CLI do Azure, consulte Olá [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).
* Para saber mais sobre recursos do Lote, consulte [Visão geral do Lote do Azure para desenvolvedores](batch-api-basics.md).
* Para obter mais informações sobre como usar pools de toocreate modelos, trabalhos e tarefas em lotes sem escrever código, consulte [usar modelos de CLI de lote do Azure e transferência de arquivos (visualização)](batch-cli-templates.md).

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
