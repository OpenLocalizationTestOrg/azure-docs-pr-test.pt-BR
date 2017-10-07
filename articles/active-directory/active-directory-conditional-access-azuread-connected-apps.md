---
title: Acesso condicional para aplicativos SaaS de aaaAzure | Microsoft Docs
description: "Acesso condicional no AD do Azure permite que você tooconfigure autenticação multifator por aplicativo regras de acesso e o acesso de tooblock de capacidade de saudação para usuários não em uma rede confiável. "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Introdução ao Acesso Condicional ao Azure Active Directory
O Acesso Condicional ao Azure Active Directory para aplicativos [SaaS](https://azure.microsoft.com/overview/what-is-saas/) e aplicativos conectados ao Azure AD permite que você configure o acesso condicional com base em grupo, localização e sensibilidade de aplicativo. 

Com acesso condicional com base na confidencialidade do aplicativo, você pode definir regras de acesso de autenticação multifator (MFA) por aplicativo. MFA por aplicativo fornece acesso de tooblock de capacidade de saudação para usuários que não estão em uma rede confiável. Você pode aplicar MFA regras tooall usuários recebem toohello aplicativo ou apenas para os usuários especificados grupos de segurança.  Os usuários podem ser excluídos do requisito de MFA de saudação se eles estiverem acessando o aplicativo hello de um endereço IP que está dentro da rede da organização hello.

Esses recursos estarão disponíveis toocustomers que tiver adquirido uma licença Azure Active Directory Premium.

## <a name="scenario-prerequisites"></a>Pré-requisitos do cenário
* Licença do Azure Active Directory Premium
* Um locatário do Azure Active Directory federado ou gerenciado
* Locatários federados exigem que a autenticação multifator esteja habilitada.

## <a name="configure-per-application-access-rules"></a>Configurar regras de acesso por aplicativo
Esta seção descreve como acessar tooconfigure por aplicativo regras.

1. Entrar toohello portal clássico do Azure usando uma conta que seja um administrador global do AD do Azure.
2. No painel esquerdo do hello, selecione **do Active Directory**.
3. Na guia de diretório hello, selecione seu diretório.
4. Selecione Olá **aplicativos** guia.
5. Aplicativo hello selecione Olá regra será definido para.
6. Selecione Olá **configurar** guia.
7. Role para baixo toohello seção de regras de acesso. Selecione a regra de acesso desejado hello.
8. Especifique usuários Olá Olá regra será aplicada.
9. Habilitar política de saudação selecionando **ativado toobe**.

## <a name="understanding-access-rules"></a>Noções básicas de regras de acesso
Esta seção fornece uma descrição detalhada das regras de acesso de saudação com suporte no hello acesso condicional de aplicativo do Azure.

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a>Especificar usuários de Olá Olá acesso regras se aplicam a
Por padrão Olá política se aplicará tooall os usuários que têm acesso toohello aplicativo. No entanto, você também pode restringir Olá toousers de política que são membros de saudação especificado grupos de segurança. Olá **adicionar grupo** botão é usado tooselect um ou mais grupos de caixa de diálogo de seleção de grupo Olá que Olá regra de acesso serão aplicada a. Essa caixa de diálogo também pode ser usado tooremove selecionada de grupos. Quando as regras de saudação tooGroups tooapply selecionado, as regras de acesso de saudação só serão impostas para usuários que pertencem a tooone de saudação especificada grupos de segurança.

Grupos de segurança podem também ser excluídos explicitamente da política de saudação selecionando Olá **exceto** opção e especificando um ou mais grupos. Os usuários que são membros de um grupo em Olá **exceto** lista não será o requisito de autenticação multifator toohello assunto, mesmo se eles são membros de um grupo de regra de acesso que Olá se aplica.
regra de acesso de saudação mostrada abaixo exigirá todos os usuários de autenticação de multifatores toouse do grupo de gerentes Olá ao acessar o aplicativo hello.

![Configurando regras de acesso condicional com MFA](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>Regras de acesso condicional com MFA
Se um usuário tiver sido configurado usando o recurso de autenticação multifator por usuário hello, essa configuração no usuário hello serão combinadas com as regras de autenticação multifator de saudação do aplicativo hello. Isso significa que um usuário que tenha sido configurado para a autenticação multifator por usuário será necessário tooperform a autenticação multifator mesmo se ele tiver sido isentado das regras de autenticação multifator do aplicativo hello. Saiba mais sobre autenticação multifator e configurações por usuário.

### <a name="access-rule-options"></a>Opções de regra de acesso
Olá, as opções a seguir têm suporte:

* **Exigir autenticação multifator**: usuários Olá aplicam regras de acesso toowhom Olá, será necessário toocomplete a autenticação multifator antes de acessar o aplicativo hello que Olá política aplica-se a.
* **Exigir autenticação multifator quando não estiver no trabalho**: um usuário que vêm de um endereço IP confiável não será necessário tooperform a autenticação multifator. Olá confiável intervalos de endereços IP podem ser configurados na página de configurações de autenticação multifator hello.
* **Bloquear o acesso quando não estiver no trabalho**: um usuário que não vem de um endereço IP confiável será bloqueado. Olá confiável intervalos de endereços IP podem ser configurados na página de configurações de autenticação multifator hello.

### <a name="setting-rule-status"></a>Status da regra de configuração
Status da regra de acesso permite ativar ou desativar a regras de saudação. Quando hello regras de acesso estiverem desativadas, o requisito de autenticação multifator Olá não é imposto.

### <a name="access-rule-evaluation"></a>Avaliação da regra de acesso
Regras de acesso são avaliadas quando um usuário acessa um aplicativo federado que usa OAuth 2.0, OpenID Connect, SAML ou WS-Federation. Além disso, as regras de acesso são avaliadas quando hello OAuth 2.0 e OpenID Connect usam um tooacquire de token de atualização de um token de acesso. Se a avaliação da política falhar quando um token de atualização é usado, Olá erro **invalid_grant** será retornado, isso indica que o usuário de saudação precisa toore-autenticar toohello cliente.

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a>Configurar a autenticação de vários fatores de tooprovide de serviços de Federação
Para locatários federados, MFA pode ser executada pelo Active Directory do Azure ou por saudação do servidor AD FS local.

Por padrão, a MFA ocorrerá em uma página hospedada pelo Active Directory do Azure. Olá tooconfigure MFA local, **– SupportsMFA** propriedade deve ser definida muito**true** no Active Directory do Azure, usando o módulo de saudação do AD do Azure para Windows PowerShell.

Olá, exemplo a seguir mostra como tooenable local MFA usando Olá [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) no locatário do hello contoso.com:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

Em adição toosetting esse sinalizador, Olá locatário federado do AD FS instância deve ser configurado tooperform a autenticação multifator. Siga as instruções de saudação de [implantação local do Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>Artigos relacionados
* [Protegendo o acesso tooOffice 365 e outros aplicativos conectados tooAzure do Active Directory](active-directory-conditional-access.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)

