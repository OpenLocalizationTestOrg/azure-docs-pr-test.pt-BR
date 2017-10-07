---
title: "aaaAzure aplicativo do Active Directory e objetos de entidade de serviço | Microsoft Docs"
description: "Uma discussão de relação de saudação entre aplicativos e objetos de entidade de serviço no Active Directory do Azure"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Objetos de entidade de serviço e aplicativo no Azure Active Directory (Azure AD)
Olá, às vezes, o significado do termo hello "aplicativo" pode ser interpretados incorretamente quando usados no contexto de saudação do AD do Azure. Olá objetivo deste artigo é toomake-la mais clara ao enumerar conceituais e concretos aspectos de integração de aplicativos do AD do Azure, com uma ilustração do registro e o consentimento para um [aplicativo multilocatário](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Visão geral
Um aplicativo que foi integrado ao AD do Azure tem implicações que vão além do aspecto de software hello. "Aplicativo" é frequentemente usado como um termo conceitual, referindo-se toonot somente Olá Olá software de aplicativo, mas também seu registro do AD do Azure e função de autenticação/autorização "conversas" em tempo de execução. Por definição, um aplicativo pode funcionar em um [cliente](active-directory-dev-glossary.md#client-application) função (consumindo um recurso), um [servidor recurso](active-directory-dev-glossary.md#resource-server) função (expõe APIs tooclients), ou ambos. protocolo de conversa de saudação é definido por um [fluxo de concessão de autorização do OAuth 2.0](active-directory-dev-glossary.md#authorization-grant), permitindo que Olá cliente/recursos tooaccess e proteger dados do recurso respectivamente. Agora vamos um nível mais profundo e veja como o modelo de aplicativo de saudação do AD do Azure representa um aplicativo em tempo de design e tempo de execução. 

## <a name="application-registration"></a>Registro de aplicativo
Quando você registrar um aplicativo do AD do Azure no hello [portal do Azure][AZURE-Portal], dois objetos são criados no seu locatário do AD do Azure: um objeto de aplicativo e um objeto de entidade de serviço.

#### <a name="application-object"></a>Objeto de aplicativo
Um aplicativo do AD do Azure é definido por um e somente objeto de aplicativo, que reside no locatário de saudação do AD do Azure, onde o aplicativo hello foi registrado, conhecido como o locatário "home" do aplicativo hello. saudação do Azure AD Graph [entidade aplicativos] [ AAD-Graph-App-Entity] define o esquema Olá para propriedades de um objeto de aplicativo. 

#### <a name="service-principal-object"></a>Objeto de entidade de serviço
objeto de entidade de serviço Olá define permissões para uso do aplicativo e política de saudação em um locatário específico, fornecendo a base de saudação para um aplicativo de saudação do toorepresent principal de segurança em tempo de execução. saudação do Azure AD Graph [entidade ServicePrincipal] [ AAD-Graph-Sp-Entity] define o esquema Olá para propriedades do objeto principal um serviço. 

#### <a name="application-and-service-principal-relationship"></a>Relação do aplicativo e a entidade de serviço
Considere a possibilidade de objeto de aplicativo hello como Olá *global* representação do seu aplicativo para uso em todos os locatários e entidade de serviço hello como Olá *local* representação para uso em um determinado locatário. Hello objeto application serve como hello modelo a partir de qual comuns e propriedades padrão são *derivado* para uso na criação de objetos de entidade de serviço correspondentes. Um objeto de aplicativo, portanto, tem uma relação de 1:1 com o aplicativo de software hello e uma relação de 1 com seus objetos principal do serviço correspondente.

Uma entidade de serviço deve ser criada em cada locatário em que o aplicativo hello será usado, permitindo que ele tooestablish uma identidade de entrada e/ou tooresources de acesso está sendo protegido por locatário hello. Um aplicativo de locatário único terá apenas uma entidade de serviço (em seu locatário inicial), geralmente criado e com consentimento para uso durante o registro do aplicativo. Uma aplicativo multilocatária Web API também terá uma entidade de serviço criada em cada locatário em que um usuário de locatário consentiu tooits uso.  

> [!NOTE]
> As alterações feitas tooyour objeto de aplicativo, também são refletidas em seu objeto de entidade de serviço do aplicativo hello inicial locatário apenas (locatário Olá onde ele foi registrado). Para aplicativos de multilocação, objeto de aplicativo toohello alterações não são refletidas nos objetos de entidade de serviço qualquer locatários do consumidor, até que o acesso de saudação é removido por meio de saudação [painel de acesso do aplicativo](https://myapps.microsoft.com) e concedido novamente.
><br>  
> Observe também que os aplicativos nativos são registrados como multilocatários, por padrão.
> 
> 

## <a name="example"></a>Exemplo
Olá, diagrama a seguir ilustra a relação Olá entre o objeto de aplicativo e serviço correspondente, os objetos, no contexto de saudação de um aplicativo de multilocatário de exemplo chamados de um aplicativo **aplicativo HR**. Há três locatários do Azure AD nesse cenário: 

* **Adatum** - Olá locatário usado pela empresa Olá que desenvolveu Olá **aplicativo HR**
* **A Contoso** - Olá locatário usado pelo Olá organização Contoso, que é um consumidor de saudação **aplicativo HR**
* **A Fabrikam** - Olá locatário usado pelo Olá organização Fabrikam, que também consome Olá **aplicativo HR**

![Relação entre um objeto de aplicativo e um objeto de entidade de serviço](./media/active-directory-application-objects/application-objects-relationship.png)

No diagrama anterior de saudação, etapa 1 é processo Olá de criação de aplicativo hello e objetos de serviço no locatário inicial do aplicativo hello.

Na etapa 2, quando os administradores de Contoso e Fabrikam concluir consentimento, um objeto de entidade de serviço é criado no locatário do AD do Azure de sua empresa e permissões atribuídos Olá administrador Olá concedido. Observe também que o aplicativo hello HR pode ser configurado/projetado tooallow consentimento pelos usuários para uso individual.

Na etapa 3, locatários do consumidor de saudação de saudação aplicativo HR (Contoso e Fabrikam) cada tem seu próprio objeto de serviço. Cada uma representa o uso de uma instância do aplicativo hello em tempo de execução, controlado por Olá permissões consentidas pelo administrador do respectivos hello.

## <a name="next-steps"></a>Próximas etapas
Objeto de aplicativo do aplicativo pode ser acessado por meio de saudação do Azure AD Graph API, hello [portal do Azure] [ AZURE-Portal] editor de manifesto do aplicativo, ou [cmdlets do PowerShell do Azure AD](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), conforme representado por seu OData [entidade aplicativos][AAD-Graph-App-Entity].

Objeto de serviço do aplicativo pode ser acessado via hello Azure AD Graph API ou [cmdlets do PowerShell do Azure AD](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), conforme representado por seu OData [entidade ServicePrincipal] [ AAD-Graph-Sp-Entity].

Olá [do Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/) é útil para consultar o aplicativo hello e objetos de serviço.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
