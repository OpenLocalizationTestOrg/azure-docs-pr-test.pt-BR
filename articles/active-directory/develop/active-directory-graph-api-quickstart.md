---
title: "aaaQuickstart de saudação do Azure AD Graph API | Microsoft Docs"
description: "Olá API do Graph do Azure Active Directory fornece acesso programático tooAzure AD por meio de pontos de extremidade de API de REST do OData. Os aplicativos podem usar tooperform de API do Graph Olá criar, ler, atualizar e excluir operações CRUD () em objetos e dados do diretório."
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Início rápido para hello Azure AD Graph API
Olá API do Graph do Azure Active Directory (AD) fornece acesso programático tooAzure AD por meio de pontos de extremidade de API de REST do OData. Os aplicativos podem usar tooperform de API do Graph Olá criar, ler, atualizar e excluir operações CRUD () em objetos e dados do diretório. Por exemplo, você pode usar para a API do Graph Olá toocreate um novo usuário, exibição ou atualizar as propriedades do usuário, alterar a senha do usuário, verificar a associação de grupo de acesso baseado em função, desabilitar ou excluir Olá usuário. Para obter mais informações sobre recursos da API do Graph hello e cenários de aplicativo, consulte [API do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) e [pré-requisitos do Azure AD Graph API](https://msdn.microsoft.com/library/hh974476.aspx). 

> [!IMPORTANT]
> É altamente recomendável que você use [Microsoft Graph](https://developer.microsoft.com/graph) em vez do Azure AD Graph API tooaccess recursos do Active Directory do Azure. Nossos esforços de desenvolvimento agora estão concentrados no Microsoft Graph e não há planejamento de novas melhorias para a API do Azure AD Graph. Há um número muito limitado de cenários para o qual Azure AD Graph API ainda pode ser apropriada; Para obter mais informações, consulte Olá [Microsoft Graph ou hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) postagem de blog em Olá Centro de desenvolvimento do Office.
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>Como tooconstruct uma URL de API do Graph
Na API do Graph, os dados de diretório tooaccess e objetos (em outras palavras, recursos ou entidades) em relação ao qual você deseja que as operações CRUD tooperform, você pode usar URLs com base no protocolo OData (Open Data) do hello. Olá URLs usadas na Graph API consistem em quatro partes principais: serviço raiz, identificador do locatário, caminho de recurso e opções de cadeia de caracteres de consulta: `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`. Veja exemplo hello de saudação URL a seguir: `https://graph.windows.net/contoso.com/groups?api-version=1.6`.

* **Raiz do serviço**: no Azure AD Graph API, raiz de serviço Olá é sempre https://graph.windows.net.
* **Identificador do locatário**: Esta seção pode ser um nome de domínio (registrado) verificado, no hello anterior como exemplo, contoso.com. Ele também pode ser um locatário objeto ID ou hello "myorganization" ou "me" alias. Para obter mais informações, consulte [endereçamento de entidades e operações Olá Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview)).
* **Caminho do recurso**: Esta seção de URL identifica o recurso de saudação toobe interagir com (usuários, grupos, um usuário específico ou um grupo específico, etc.) O exemplo hello acima, é tooaddress de nível superior "grupos" hello esse conjunto de recursos. Você também pode abordar uma entidade específica, por exemplo "users/{objectId}" ou "users/userPrincipalName".
* **Parâmetros de consulta**: um ponto de interrogação (?) separa a seção do caminho de recurso Olá da seção de parâmetros de consulta hello. parâmetro de consulta "api-version" Hello é necessário em todas as solicitações no hello API do Graph. Olá Graph API também dá suporte a saudação seguindo as opções de consulta OData: **$filter**, **$orderby**, **$expand**, **$top**e **$format**. Olá, as opções de consulta a seguir não têm suporte: **$count**, **$inlinecount**, e **$skip**. Para saber mais, confira [Suporte a consultas, filtros e opções de paginação na API do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options).

## <a name="graph-api-versions"></a>Versões da Graph API
Você pode especificar versão Olá para uma solicitação de API do Graph no parâmetro de consulta "api-version" hello. Para a versão 1.5 e posterior, você usa um valor numérico de versão; api-version=1.6. Para versões anteriores, você use uma cadeia de caracteres de data que segue toohello formato AAAA-MM-DD; Por exemplo, api-version = 2013-11-08. Recursos de visualização, use a cadeia de caracteres do hello "beta"; Por exemplo, api-version = beta. Para obter mais informações sobre as diferenças entre as versões da Graph API, consulte [Controle de versão da Graph API do AD do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning).

## <a name="graph-api-metadata"></a>Metadados da Graph API
Olá tooreturn arquivo de metadados de API do Graph, adicionar segmento hello "$metadata" após Olá identificador do locatário na URL. por exemplo hello, hello seguindo a URL retorna metadados para uma empresa de demonstração: `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`. Você pode inserir esta URL na barra de endereços de saudação do web navegador toosee Olá metadados. Olá documento de metadados CSDL retornado descreve Olá entidades e tipos complexos, suas propriedades e funções hello e ações expostas pela versão de saudação do Graph API solicitada. A omissão de parâmetro de versão de api de saudação retorna metadados para a versão mais recente do hello.

## <a name="common-queries"></a>Consultas comuns
[Consultas do Azure AD Graph API Common](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) lista as consultas comuns que podem ser usadas com hello Azure AD Graph, incluindo consultas que podem ser usados tooaccess recursos de nível superior em suas operações de diretório e consultas tooperform em seu diretório.

Por exemplo, `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` retorna informações de empresa para o diretório contoso.com.

Ou `https://graph.windows.net/contoso.com/users?api-version=1.6` lista todos os objetos de usuário no hello diretório contoso.com.

## <a name="using-hello-graph-explorer"></a>Usando o Gerenciador de gráficos de saudação
Você pode usar o hello Gerenciador de gráficos para Olá dados do diretório do Azure AD Graph API tooquery Olá conforme você criar seu aplicativo.

Olá, a seguir é Olá saída seria ver se fosse toonavigate toohello Gerenciador de gráficos, entrar e digite `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` toodisplay todos Olá usuários Olá assinado no diretório do usuário:

![Gerenciador de a Graph API do AD do Azure](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**Saudação de carga Gerenciador de gráficos**: Olá tooload ferramenta, navegue até muito[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/). Clique em **Login** e entrar com sua toorun de credenciais de conta do AD do Azure Olá Gerenciador de gráficos em seu locatário. Se você executar o Gerenciador de gráficos em seu próprio locatário, você ou o administrador precisa tooconsent durante o logon. Se tiver uma assinatura do Office 365, você automaticamente terá um locatário do AD do Azure. credenciais de saudação usar toosign no tooOffice 365 são, na verdade, contas do AD do Azure e você pode usar essas credenciais com o Gerenciador de gráficos.

**Executar uma consulta**: toorun uma consulta, digite sua consulta na caixa de texto de solicitação hello e clique em **obter** ou clique em Olá **insira** chave. Olá resultados são exibidos na caixa de resposta de saudação. Por exemplo, `https://graph.windows.net/myorganization/groups?api-version=1.6` lista todos os objetos de grupo no diretório Olá assinado do usuário.

Saudação de Observação recursos e limitações do hello Gerenciador de gráficos a seguir:

* Funcionalidade de preenchimento automático em conjuntos de recursos. toosee essa funcionalidade, clique em Olá solicitar a caixa de texto (onde o URL da empresa Olá aparece). Você pode selecionar um recurso definido na lista suspensa hello.
* Dá suporte a hello "me" e "myorganization" alias de endereço. Por exemplo, você pode usar `https://graph.windows.net/me?api-version=1.6` tooreturn objeto de usuário de saudação do usuário conectado hello ou `https://graph.windows.net/myorganization/users?api-version=1.6` tooreturn todos os usuários no diretório atual hello.
* Uma seção de cabeçalhos de resposta. Esta seção pode ser usada toohelp solucionar problemas que ocorrem durante a execução de consultas.
* Um visualizador JSON para resposta de saudação com recursos de expandir e recolher.
* Não há suporte para a exibição de uma foto em miniatura.

## <a name="using-fiddler-toowrite-toohello-directory"></a>Usando o Fiddler toowrite toohello directory
Para fins de saudação deste guia de início rápido, você pode usar o hello Fiddler Web Debugger toopractice executando '' as operações de gravação em relação a seu diretório do AD do Azure. Para obter mais informações e tooinstall Fiddler, consulte [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler).

No exemplo hello abaixo, você pode usar o Fiddler Web Debugger toocreate um novo grupo de segurança 'MyTestGroup' em seu diretório do AD do Azure.

**Obter um token de acesso**: tooaccess do Azure AD Graph, os clientes são toosuccessfully necessário autenticar tooAzure AD primeiro. Para obter mais informações, consulte [Cenários de autenticação para o Azure AD](active-directory-authentication-scenarios.md).

**Compor e executar uma consulta**: Olá concluir as etapas a seguir:

1. Abra o Fiddler Web depurador e alterne toohello **criador** guia.
2. Selecione como você deseja toocreate um novo grupo de segurança, **Post** como Olá método HTTP a partir do menu suspenso de saudação. Para obter mais informações sobre operações e permissões em um objeto de grupo, consulte [grupo](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity) em Olá [referência de API REST do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
3. Em Olá campo próximo muito**Post**, digite seguinte hello como Olá URL da solicitação: `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`.
   
   > [!NOTE]
   > Você deve substituir mytenantdomain pelo nome de domínio de saudação do seu próprio diretório do AD do Azure.
   > 
   > 
4. No campo de saudação diretamente abaixo do menu suspenso Post, digite o seguinte de saudação:
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > Substituir o &lt;o token de acesso&gt; com token de acesso de saudação do seu diretório do AD do Azure.
   > 
   > 
5. Em Olá **corpo da solicitação** , digite o seguinte hello:
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    Para saber mais sobre como criar grupos, confira [Criar um grupo](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup).

Para obter mais informações sobre entidades do AD do Azure e tipos que são expostos pelo Graph e informações sobre operações de saudação que podem ser executadas com o Graph, consulte [referência de API REST do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre Olá [API do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* Saiba mais sobre [Escopos de Permissão da API do Graph do Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

