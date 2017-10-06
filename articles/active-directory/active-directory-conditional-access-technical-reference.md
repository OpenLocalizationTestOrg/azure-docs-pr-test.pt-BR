---
title: "Referência técnica do acesso condicional do Active Directory de aaaAzure | Microsoft Docs"
description: "Com controle de acesso condicional, o Active Directory do Azure verifica condições específicas hello, que você escolhe ao autenticar usuário hello e antes de permitir acesso toohello aplicativo. Quando essas condições forem atendidas, o usuário de Olá é autenticado e acesso toohello aplicativo autorizado."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Referência técnica do acesso condicional ao Azure Active Directory

## <a name="services-enabled-with-conditional-access"></a>Serviços habilitados com acesso condicional

Regras de acesso condicional têm suporte em vários tipos de aplicativos do AD do Azure. Essa lista inclui:


* Aplicativos registrados com hello Proxy de aplicativo do Azure
* Aplicativo Remoto do Azure
* Aplicativos de linha de negócios e de multilocação desenvolvidos registrados no AD do Azure
* Dynamics CRM
* Aplicativos federados da Galeria de aplicativo do AD do Azure Olá
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint Online (inclui o OneDrive for Business)
* Microsoft Power BI 
* Aplicativos de SSO de senha da Galeria de aplicativo hello AD do Azure
* Visual Studio Team Services
* Equipes da Microsoft









## <a name="enable-access-rules"></a>Habilitar regras de acesso
Cada regra pode ser habilitada ou desabilitada com base no aplicativo. Quando as regras são **ON** serão habilitadas e aplicadas a usuários que acessam o aplicativo hello. Quando eles são **OFF** não serão usados e assinará não usuários de saudação do impacto na experiência.

## <a name="applying-rules-toospecific-users"></a>Usuários de toospecific aplicando regras
As regras podem ser aplicadas toospecific conjuntos de usuários com base no grupo de segurança, definindo **aplicar a**. **Aplicar a** pode ser definido muito**todos os usuários** ou **grupos**. Quando definido muito**todos os usuários** Olá regras se aplicarão tooany usuário com aplicativos de toohello de acesso. Olá **grupos** opção permite específicas de segurança e toobe de grupos de distribuição selecionado, as regras serão aplicadas apenas para esses grupos.

Ao implantar uma regra, é comum toofirst aplicá-lo um conjunto limitado de usuários, que são membros de grupos um piloto. Depois que a regra de saudação completa pode ser aplicada muito**todos os usuários**. Isso fará com que a regra Olá toobe imposta para todos os usuários na organização hello.

Selecione grupos também podem ser isentos da política usando Olá **exceto** opção. Todos os membros desses grupos estarão isentos mesmo que apareçam em um grupo incluído.

## <a name="at-work-networks"></a>Redes "No trabalho"
As regras de acesso condicional que usam uma rede "no trabalho", dependem de intervalos de endereços IP confiáveis que foram configurados no AD do Azure, ou o uso de hello "dentro da rede corporativa" declarações do AD FS. Essas regras incluem:

* Exigir autenticação multifator quando não está no trabalho
* Bloquear acesso quando não estiver no trabalho

Opções para especificar redes "no trabalho"

1. Configurar intervalos de endereços IP confiáveis em hello [página de configuração de autenticação multifator](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Política de acesso condicional usará os intervalos de saudação configurado em cada solicitação e o token de emissão tooevaluate as regras de autenticação. 
2. Configurar o uso de saudação dentro de declaração da rede corporativa, essa opção pode ser usada com diretórios federados, usando o AD FS. toolearn mais sobre hello dentro de declarações de rede corporativa, consulte [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Regras com base na confidencialidade do aplicativo
Regras são configuradas por aplicativo permitindo Olá alto valor serviços toobe protegida sem afetar o acesso tooother serviços. Regras de acesso condicional podem ser configuradas em Olá **configurar** guia do aplicativo hello. 

Regras oferecidas atualmente:

* **Exigir autenticação multifator**
  
  * Todos os usuários que essa política é aplicada toowill ser tooauthenticate necessária por meio de pelo menos uma vez a autenticação multifator.
* **Exigir autenticação multifator quando não está no trabalho**
  
  * Se essa política é aplicada, todos os usuários serão autenticação de multifator toohave necessária executada pelo menos uma vez se acessam o serviço de saudação de um local remoto inativo. Se eles mudam de local de tooremote um trabalho, eles serão tooperform necessária a autenticação multifator ao acessar o serviço de saudação.
* **Bloquear acesso quando não estiver no trabalho** 
  
  * Quando os usuários mudam de local remoto do trabalho tooa, eles serão bloqueados se hello, "Bloquear acesso quando não estiver no trabalho" política é aplicada toothem.  Eles terão o acesso permitido novamente quando estiverem em um local de trabalho.

## <a name="related-topics"></a>Tópicos relacionados
* [Protegendo o acesso tooOffice 365 e outros aplicativos conectados tooAzure do Active Directory](active-directory-conditional-access.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)

