---
title: tooIntegrate aaaHow com o Active Directory do Azure | Microsoft Docs
description: "Toobenefits uma guia do e recursos para integração com o Active Directory do Azure."
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 4542965ae4a7756eda9f57e9e895f8044892f20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-azure-active-directory"></a>Integração ao Active Directory do Azure
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

O Active Directory do Azure fornece às organizações gerenciamento de identidades de nível empresarial para aplicativos em nuvem.  Integração do AD do Azure oferece aos usuários uma experiência de entrada simplificada e ajuda a seu aplicativo está de acordo com a política de tooIT.

## <a name="how-toointegrate"></a>Como tooIntegrate
Há várias maneiras para toointegrate seu aplicativo com o Azure AD.  Aproveite o maior ou menor número possível desses cenários, conforme apropriado para seu aplicativo.

### <a name="support-azure-ad-as-a-way-toosign-in-tooyour-application"></a>Suporte do AD do Azure como uma maneira tooSign em tooYour aplicativo
**Reduza a fricção de entrada e reduza os custos de suporte.** Usando AD do Azure toosign tooyour aplicativo, os usuários não terão um tooremember mais de nome e a senha.  Como desenvolvedor, você tem um menos toostore de senha e proteger.  Não ter toohandle esquecido redefinições de senha pode ser uma economia significativa sozinha.  O AD do Azure ativa de entrada para algumas das mais populares aplicativos em nuvem Olá mundo, inclusive o Office 365 e o Microsoft Azure.  Com centenas de milhões usuários milhões de organizações, a probabilidade é o usuário já está conectado tooAzure AD.  Saiba mais sobre [como adicionar suporte ao logon do AD do Azure](active-directory-authentication-scenarios.md).

**Simplifique a inscrição para o aplicativo.**  Durante a inscrição para o aplicativo, o AD do Azure pode enviar informações essenciais sobre um usuário para que você possa preencher previamente o formulário de inscrição ou eliminá-lo completamente.  Os usuários podem inscrever-se para seu aplicativo usando sua conta do Azure AD por meio de um toothose semelhante de experiência de consentimento familiar encontrado na mídia social e aplicativos móveis.  Qualquer usuário pode inscrever-se e entrar no aplicativo tooan que é integrado ao AD do Azure sem a necessidade de envolvimento de TI.  Saiba mais sobre como [inscrever o aplicativo para logon na conta do AD do Azure](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) .

### <a name="browse-for-users-manage-user-provisioning-and-control-access-tooyour-application"></a>Procurar por usuários, gerenciar o provisionamento de usuário e controlar o acesso tooYour aplicativo
**Procurar por usuários no diretório de saudação.**  Usar Olá Graph API toohelp usuários pesquisa e procura de outras pessoas em sua organização ao convidar outras pessoas ou conceder acesso, em vez de exigir que eles tootype endereços de email.  Os usuários podem procurar usando uma interface de estilo do catálogo endereço familiar, incluindo a exibição de detalhes de saudação da hierarquia organizacional hello.  Saiba mais sobre Olá [API do Graph](active-directory-graph-api.md).

**Reutilize grupos do Active Directory e listas de distribuição que seu cliente já está gerenciando.**  AD do Azure contém grupos de saudação que o cliente já está usando para distribuição de email e gerenciamento de acesso.  Usando Olá API do Graph, usar novamente esses grupos em vez de exigir o toocreate de cliente e gerenciar um conjunto separado de grupos em seu aplicativo.  Informações de grupo também podem ser enviadas tooyour aplicativo em tokens de entrada.  Saiba mais sobre Olá [API do Graph](active-directory-graph-api.md).

**Use toocontrol do AD do Azure que tenha acesso tooyour aplicativo.**  Os administradores e os proprietários do aplicativo no AD do Azure podem atribuir acesso tooapplications toospecific usuários e grupos.  Usando Olá API do Graph, você pode ler a essa lista e usá-lo toocontrol provisionamento e cancelamento de provisionamento de recursos e acessar dentro de seu aplicativo.

**Use o AD do Azure para funções com base em controle de acesso.**  Os administradores e os proprietários do aplicativo podem atribuir usuários e grupos tooroles que definem quando você registra seu aplicativo no AD do Azure.  Informações de função enviadas tooyour aplicativo em tokens de entrada e também podem ser lidos usando Olá API do Graph.  Saiba mais sobre [uso do AD do Azure para autorização](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx).

### <a name="get-access-toousers-profile-calendar-email-contacts-files-and-more"></a>Obter o perfil do acesso tooUser, calendário, Email, contatos, arquivos e muito mais
**AD do Azure é um servidor de autorização Olá para o Office 365 e outros serviços comerciais da Microsoft.**  Se você der suporte do AD do Azure para o logon no aplicativo tooyour ou suporte vinculando as atual usuário contas tooAzure AD contas de usuário usando o OAuth 2.0, você pode solicitar a leitura e perfil do usuário do acesso de gravação tooa, calendário, email, contatos, arquivos e outras informações.  Você perfeitamente pode gravar o calendário de eventos do toouser e ler ou gravar arquivos tootheir OneDrive.  Saiba mais sobre [acessando Olá APIs do Office 365](https://msdn.microsoft.com/office/office365/howto/platform-development-overview).

### <a name="promote-your-application-in-hello-azure-and-office-365-marketplaces"></a>Promover o aplicativo hello Azure e Office 365 mercados
**Promova o seu aplicativo toohello milhões de organizações que já estão usando o AD do Azure.**  Usuários que pesquisam e procuram por itens nesses Marketplaces já estão usando um ou mais serviços de nuvem, tornando-os clientes qualificados do serviço de nuvem.  Saiba mais sobre a promoção de seu aplicativo em [hello Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/).

**Quando os usuários se inscreverem no aplicativo, este será exibido no painel de acesso do AD do Azure e no lançador de aplicativo do Office 365 desses usuários.**  Os usuários serão tooquickly capaz e facilmente retorno tooyour aplicativo mais tarde, melhorando o envolvimento do usuário.  Saiba mais sobre Olá [painel de acesso do AD do Azure](../active-directory-saas-access-panel-introduction.md).

### <a name="secure-device-to-service-and-service-to-service-communication"></a>Comunicação segura de dispositivo a serviço e entre serviços
**Usando o Azure AD para o gerenciamento de identidade de dispositivos e serviços reduz o código de saudação necessário toowrite e permite o acesso de toomanage IT.**  Dispositivos e serviços podem obter tokens do AD do Azure usando o OAuth e usar esses tokens tooaccess APIs da web.  Usando o AD do Azure, você pode evitar escrever código de autenticação complexo.  Como identidades Olá Olá serviços e dispositivos são armazenadas no AD do Azure, IT poderá gerenciar chaves e a revogação em um local em vez de ter toodo isso separadamente em seu aplicativo.

## <a name="benefits-of-integration"></a>Vantagens da integração
Integração com o AD do Azure vem com os benefícios que não exigem um código adicional toowrite.

### <a name="integration-with-enterprise-identity-management"></a>Integração com o gerenciamento de identidades corporativas
**Ajude seu aplicativo a manter-se em conformidade com as políticas de TI.**  As organizações integram seus sistemas de gerenciamento de identidade corporativa com o Azure AD, portanto, quando uma pessoa deixa uma organização, ele automaticamente perderá acesso tooyour aplicativo sem tootake necessário IT etapas adicionais.  IT poderá gerenciar quem pode acessar o aplicativo e determinar quais políticas de acesso necessárias - exemplo multi-factor Authentication - reduzindo toocomply de código de toowrite sua necessidade com políticas corporativas complexas.  AD do Azure fornece aos administradores um log de auditoria detalhada do que conectado tooyour aplicativo forma IT pode controlar o uso.

**O AD do Azure estende a nuvem de toohello do Active Directory para que seu aplicativo pode integrar com o AD.**  Muitas empresas Olá, mundo usam o Active Directory como sua entrada principal e o sistema de gerenciamento de identidade e exigem toowork seus aplicativos com o AD.  A integração com o AD do Azure integra seu aplicativo ao Active Directory.

### <a name="advanced-security-features"></a>Recursos avançados de segurança
**Multi-Factor Authentication.**  O AD do Azure fornece Multi-Factor Authentication nativa.  Os administradores de TI podem exigir autenticação multifator tooaccess seu aplicativo, para que você não tem toocode esse suporte por conta própria.  Saiba mais sobre [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/).

**Detecção de entrada anormal.**  O AD do Azure processa mais de um bilhão entradas por dia durante o uso de máquina atividades suspeitas de toodetect de algoritmos de aprendizado e notificar os administradores de TI de possíveis problemas.  Com o suporte à entrada do AD do Azure, seu aplicativo obtém o benefício de saudação dessa proteção. Saiba mais sobre a [visualização do relatório de acesso do Azure Active Directory](../active-directory-view-access-usage-reports.md).

**Acesso condicional.**  Além de autenticação de fator de toomulti, os administradores podem exigir condições específicas ser atendidos antes que os usuários podem entrar no aplicativo tooyour.  As condições que podem ser definidas incluem intervalo de endereços IP hello de dispositivos cliente, a associação em grupos especificados e o estado de saudação do dispositivo hello está sendo usado para o acesso.  Saiba mais sobre o [acesso condicional ao Azure Active Directory](../active-directory-conditional-access.md).

### <a name="easy-development"></a>Desenvolvimento fácil
**Protocolos padrão da indústria.**  A Microsoft está confirmada toosupporting padrões da indústria.  O AD do Azure oferece suporte a protocolos de autenticação SAML 2.0, OpenID Connect 1.0, OAuth 2.0 e WS-Federation 1.2 hello.  Olá Graph API é compatível com o OData 4.0.  Se seu aplicativo já oferece suporte a protocolos de OpenID Connect 1.0 ou Olá SAML 2.0 para logon federado em, adicionando suporte para o Azure AD pode ser simples.  Saiba mais sobre [protocolos de autenticação com suporte no AD do Azure](active-directory-authentication-protocols.md).

**Bibliotecas de software livre.**  Microsoft fornece bibliotecas de código-fonte aberto com suporte total para populares de desenvolvimento toospeed plataformas e idiomas.  código-fonte Olá é licenciado sob Apache 2.0 e você é livre toofork e contribuir toohello back projetos.  Saiba mais sobre as [bibliotecas de autenticação do AD do Azure](active-directory-authentication-libraries.md).

### <a name="worldwide-presence-and-high-availability"></a>Presença mundial e alta disponibilidade
**O AD do Azure é implantado em data centers ao redor Olá, mundo e é gerenciado e monitorado em torno de relógio hello.**  AD do Azure é o sistema de gerenciamento de identidade Olá para o Microsoft Azure e o Office 365 e é implantado em data 28 centers em torno de Olá, mundo.  Dados do diretório são garantidos toobe replicada tooat pelo menos três datacenters.  Balanceadores de carga global Verifique usuários acessam a cópia mais próxima de saudação do AD do Azure que contém seus dados e roteará solicita automaticamente tooother datacenters se for detectado um problema.

## <a name="next-steps"></a>Próximas etapas
[Introdução à escrita de código](active-directory-developers-guide.md#get-started).

[Conectar usuários usando o AD do Azure](active-directory-authentication-scenarios.md)

