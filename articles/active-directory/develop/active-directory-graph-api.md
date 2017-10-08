---
title: aaaAzure Active Directory Graph API | Microsoft Docs
description: "Um guia de visão geral e guia de início rápido para Olá Graph API que permite programático acessar tooAzure AD por meio de pontos de extremidade da API REST."
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>Graph API do Active Directory do Azure
> [!IMPORTANT]
> É altamente recomendável que você use [Microsoft Graph](https://graph.microsoft.io/) em vez do Azure AD Graph API tooaccess recursos do Active Directory do Azure. Nossos esforços de desenvolvimento agora estão concentrados no Microsoft Graph e não há planejamento de novas melhorias para a API do Azure AD Graph. Há um número muito limitado de cenários para o qual Azure AD Graph API ainda pode ser apropriada; Para obter mais informações, consulte Olá [Microsoft Graph ou hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) postagem de blog em Olá Centro de desenvolvimento do Office.
> 
> 

Olá API do Graph do Azure Active Directory fornece acesso programático tooAzure AD por meio de pontos de extremidade da API REST. Os aplicativos podem usar tooperform de API do Graph Olá criar, ler, atualizar e excluir operações CRUD () em objetos e dados do diretório. Por exemplo, Olá API do Graph dá suporte a saudação operações comuns para um objeto de usuário a seguir:

* Criar um novo usuário em um diretório
* Obter propriedades detalhadas do usuário, como seus grupos
* Atualizar as propriedades do usuário, como sua localização e o número de telefone, ou alterar sua senha
* Verificar a associação de grupo do usuário para acesso baseado em função
* Desabilitar uma conta de usuário ou excluí-la totalmente

Objetos de toouser adição, você pode executar operações semelhantes em outros objetos, como grupos e aplicativos. Olá toocall API do Graph em um diretório, o aplicativo hello deve ser registrado com o AD do Azure e ser configurado toohello tooallow acessar o diretório. Normalmente, isso é obtido por meio de um fluxo de consentimento do usuário ou administrador.

usando toobegin hello Azure Active Directory Graph API, consulte Olá [guia de início rápido de API do Graph](active-directory-graph-api-quickstart.md), ou o modo de exibição hello [interativa documentação de referência de API do Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="features"></a>Recursos
Olá API do Graph fornece Olá recursos a seguir:

* **Pontos de extremidade do REST API**: Olá API do Graph é um serviço RESTful constituído de pontos de extremidade que é acessadas por meio de solicitações HTTP padrão. Olá API do Graph dá suporte a tipos de conteúdo XML ou JSON Javascript Object Notation () para solicitações e respostas. Para saber mais, consulte [Referência da Graph API REST do AD do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
* **Autenticação com o Azure AD**: cada toohello solicitação API do Graph deve ser autenticada anexando um JSON Web Token (JWT) no cabeçalho de autorização de saudação da solicitação de saudação. Esse token é adquirido, fazendo uma solicitação de tooAzure do AD do ponto de extremidade e fornecer credenciais válidas. Você pode usar o hello fluxo de credenciais de cliente OAuth 2.0 ou tooacquire de fluxo de concessão de códigos de autorização Olá Olá um token toocall gráfico. Para obter mais informações, veja [OAuth 2.0 no AD do Azure](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* **Autorização baseada em função (RBAC)**: grupos de segurança são usado tooperform RBAC em Olá API do Graph. Por exemplo, se você quiser toodetermine se um usuário tem acesso tooa determinado recurso, o aplicativo hello pode chamar hello [verificar associação de grupo (transitiva)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) operação, que retorna true ou false.
* **Consulta diferencial**: se você quiser toocheck para alterações em um diretório entre dois períodos de tempo sem ter que toomake frequentam consultas toohello API do Graph, você pode fazer uma solicitação de consulta diferencial. Este tipo de solicitação retornará somente alterações de saudação feitas entre a solicitação de consulta diferencial anterior hello e solicitação atual hello. Para saber mais, leia [Consulta diferencial da Graph API do AD do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).
* **Extensões de diretório**: se você estiver desenvolvendo um aplicativo que necessite tooread ou gravar propriedades exclusivas para objetos de diretório, você pode registrar e usar valores de extensão usando Olá API do Graph. Por exemplo, se seu aplicativo requer uma propriedade Skype ID para cada usuário, você pode registrar Olá nova propriedade no diretório hello e estará disponível em todos os objetos de usuário. Para obter mais informações, veja [Extensões de esquema do diretório da Graph API do AD do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).
* **Protegido por escopos de permissão**: AAD Graph API expõe os escopos de permissão que habilitar o acesso seguro/consentimento tooAAD dados e dão suporte a uma variedade de tipos de aplicativo do cliente, incluindo:
  
  * com uma interface do usuário que recebem delegado acessar toodata por meio de autorização do usuário Olá conectado (delegado)
  * aqueles que usam controle de acesso baseado em função definido por aplicativo, como clientes de serviço/daemon (funções de aplicativo)
    
    Tanto o delegado e escopos de permissão de função de aplicativo representam um privilégio exposto pelo Olá API do Graph e podem ser solicitados por aplicativos de cliente por meio de permissões de registro de aplicativo [recursos no portal do Azure de saudação](https://portal.azure.com). Clientes podem verificar os escopos de permissão Olá concedidas toothem inspecionando a declaração de escopo ("scp") Olá recebida no token de acesso de saudação para permissões delegadas e declaração de funções hello ("funções") para permissões de função de aplicativo. Saiba mais sobre [Escopos de permissão da API do Graph do Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).

## <a name="scenarios"></a>Cenários
Olá API do Graph habilita muitos cenários de aplicativo. Olá, os seguintes cenários é hello mais comuns:

* **Aplicativo de linha de negócios (único locatário)**: neste cenário, um desenvolvedor corporativo trabalha para uma organização que tem uma assinatura do Office 365. desenvolvedor de saudação está criando um aplicativo web que interage com tarefas de tooperform do AD do Azure como atribuir um usuário de tooa de licença. Esta tarefa exige acesso toohello Graph API, para que o desenvolvedor Olá registra o aplicativo de locatário único Olá no AD do Azure e configura permissões leitura e gravação para Olá API do Graph. Olá, em seguida, o aplicativo é configurado toouse suas próprias credenciais ou aquelas do usuário conectado no momento de saudação tooacquire toocall um token Olá API do Graph.
* **Aplicativo de software como serviço (multilocatário)**: neste cenário, um fornecedor de software independente (ISV) está desenvolvendo um aplicativo Web multilocatário hospedado que fornece recursos de gerenciamento de usuário para outras organizações que usam o AD do Azure. Esses recursos exigem acesso toodirectory objetos, e assim o aplicativo hello precisa Olá toocall API do Graph. Olá developer registra o aplicativo hello no AD do Azure, configura toorequire leitura e permissões de gravação para Olá Graph API e, em seguida, habilita o acesso externo para que outras organizações possam consentir o aplicativo de hello toouse em seu diretório. Quando um usuário em outra organização autentica o aplicativo toohello para Olá a primeira vez, eles verão uma caixa de diálogo de consentimento com permissões Olá Olá aplicativo está solicitando.  Conceder consentimento então oferecerá aplicativo hello aqueles solicitou permissões toohello Graph API no diretório saudação do usuário. Para obter mais informações sobre a estrutura de consentimento hello, consulte [visão geral da estrutura de consentimento do hello](active-directory-integrating-applications.md).

## <a name="see-also"></a>Consulte também
[Guia de início rápido para a Graph API do AD do Azure](active-directory-graph-api-quickstart.md)

[Documentação do REST para a Graph AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Guia do desenvolvedor do Active Directory do Azure](active-directory-developers-guide.md)

