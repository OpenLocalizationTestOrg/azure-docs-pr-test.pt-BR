---
title: "B2C de diretório ativo do Azure: Compreendendo políticas personalizadas de pacote de inicializador Olá | Microsoft Docs"
description: "Um tópico sobre as políticas personalizadas do Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>Noções básicas sobre políticas personalizadas de saudação do pacote de inicializador de política personalizada hello Azure AD B2C

Esta seção lista todos os elementos principais de Olá da política de saudação B2C_1A_base que acompanha a saudação **Starter pacote** e que é utilizado para criar suas próprias políticas por meio da herança de saudação do hello *B2C_1A_base_ política de extensões*.

Como tal, ele mais enfoca especialmente Olá já definido de declaração de tipos, transformação de declarações, definições de conteúdo, os provedores de declarações com seus perfis técnica e Olá Jornadas de usuário de núcleo.

> [!IMPORTANT]
> A Microsoft não oferece nenhuma garantia, expressa ou implícita, com respeito toohello informações fornecidas daqui por diante. As alterações podem ser introduzidas a qualquer momento, antes do tempo de GA, no momento da GA, ou depois.

Suas próprias políticas e a saudação B2C_1A_base_extensions política podem substituir essas definições e estender essa política pai fornecendo outros adicionais conforme necessário.

Olá elementos principais de saudação *B2C_1A_base política* são tipos de declaração de transformação de declarações e definições de conteúdo. Esses elementos podem toobe suscetível referenciado em suas próprias políticas, bem como Olá *B2C_1A_base_extensions política*.

## <a name="claims-schemas"></a>Esquemas de declarações

Esses esquemas de declarações são divididos em três seções:

1.  Uma primeira seção lista as declarações de mínimo de saudação que são necessárias para Olá usuário jornadas toowork corretamente.
2.  Uma segunda seção que listas Olá declarações necessárias para parâmetros de cadeia de caracteres de consulta e outros parâmetros especiais toobe passado tooother provedores de declarações, especialmente login.microsoftonline.com para autenticação. **Não modifique essas declarações**.
3.  E finalmente uma terceira seção que lista quaisquer declarações adicionais e opcionais que podem ser coletadas de usuário Olá, armazenado no diretório de saudação e enviadas em tokens durante a entrada. Podem ser adicionadas novas declarações de tipo toobe coletados do usuário hello e/ou enviados no token Olá nesta seção.

> [!IMPORTANT]
> Olá declarações esquema contém restrições em determinados declarações como nomes de usuário e senhas. Olá diretiva de confiança do Framework (TF) trata do AD do Azure como qualquer outro provedor de declarações e todas as suas restrições são modeladas na política de premium Olá. Uma política pode ser modificado tooadd mais restrições ou usar outro provedor de declarações para o armazenamento de credenciais que terá seus próprio restrições.

tipos de declaração disponíveis Olá estão listados abaixo.

### <a name="claims-that-are-required-for-hello-user-journeys"></a>Declarações que são necessárias para viagens de usuário Olá

Olá declarações a seguir é necessário para usuário jornadas toowork corretamente:

| Tipo de declarações | Descrição |
|-------------|-------------|
| *UserId* | Nome de Usuário |
| *signInName* | Nome de entrada |
| *tenantId* | Identificador do locatário (ID) do objeto de usuário de saudação no Azure AD B2C Premium |
| *objectId* | Identificador de objeto (ID) do objeto de usuário de saudação no Azure AD B2C Premium |
| *password* | Senha |
| *newPassword* | |
| *reenterPassword* | |
| *passwordPolicies* | Políticas de senha usadas pela força da senha toodetermine B2C do Azure AD Premium, expiração, etc. |
| *sub* | |
| *alternativeSecurityId* | |
| *identityProvider* | |
| *displayName* | |
| *strongAuthenticationPhoneNumber* | O número de telefone do usuário |
| *Verified.strongAuthenticationPhoneNumber* | |
| *email* | Endereço de email que pode ser usado toocontact Olá usuário |
| *signInNamesInfo.emailAddress* | Endereço de email que Olá usuário pode usar toosign em |
| *otherMails* | Endereços de email que podem ser usado toocontact Olá usuário |
| *userPrincipalName* | Nome de usuário conforme armazenado no hello B2C do Azure AD Premium |
| *upnUserName* | Nome de usuário para criar o nome principal do usuário |
| *mailNickName* | Nome de nick de email do usuário conforme armazenado no hello B2C do Azure AD Premium |
| *newUser* | |
| *executed-SelfAsserted-Input* | Declaração que especifica se os atributos foram coletados do usuário Olá |
| *executed-PhoneFactor-Input* | Declaração que especifica se um novo número de telefone foram coletado do usuário Olá |
| *authenticationSource* | Especifica se o usuário Olá foi autenticado no provedor de identidade sociais, login.microsoftonline.com ou conta local |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>Declarações necessárias para parâmetros de cadeia de caracteres de consulta e outros parâmetros especiais

Olá seguintes declarações são necessários toopass nos provedores de declarações de tooother parâmetros especiais (incluindo alguns parâmetros de cadeia de caracteres de consulta):

| Tipo de declarações | Descrição |
|-------------|-------------|
| *nux* | O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local |
| *nca* | O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local |
| *prompt* | O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local |
| *mkt* | O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local |
| *lc* | O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local |
| *grant_type* | O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local |
| *scope* | O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local |
| *client_id* | O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local |
| *objectIdFromSession* | Parâmetro fornecido pelo saudação padrão sessão gerenciamento provedor tooindicate que Olá id de objeto foi recuperado de uma sessão SSO |
| *isActiveMFASession* | Parâmetro fornecido pelo Olá MFA sessão gerenciamento tooindicate que usuário Olá tem uma sessão ativa do MFA |

### <a name="additional-optional-claims-that-can-be-collected"></a>Declarações adicionais (opcional) que podem ser coletadas

seguinte Olá declarações são declarações adicionais que possam ser coletadas dos usuários hello, armazenado no diretório hello e enviadas no token de saudação. Conforme descrito antes, declarações adicionais podem ser adicionadas a lista de toothis.

| Tipo de declarações | Descrição |
|-------------|-------------|
| *givenName* | Nome do usuário (também conhecido como primeiro nome) |
| *surname* | Sobrenome do usuário (também conhecido como nome de família ou último nome) |
| *Extension_picture* | Imagem do usuário do social |

## <a name="claim-transformations"></a>Transformações de declaração

transformações de declaração disponíveis Olá estão listadas abaixo.

| Transformação de declaração | Descrição |
|----------------------|-------------|
| *CreateOtherMailsFromEmail* | |
| *CreateRandomUPNUserName* | |
| *CreateUserPrincipalName* | |
| *CreateSubjectClaimFromObjectID* | |
| *CreateSubjectClaimFromAlternativeSecurityId* | |
| *CreateAlternativeSecurityId* | |

## <a name="content-definitions"></a>Definições de conteúdo

Esta seção descreve as definições de conteúdo Olá já declaradas no hello *B2C_1A_base* política. Essas definições de conteúdo são suscetível toobe referenciado, substituído e/ou estendida conforme necessário em suas próprias políticas, bem como Olá *B2C_1A_base_extensions* política.

| Provedor de declarações | Descrição |
|-----------------|-------------|
| *Facebook* | |
| *Local Account SignIn* | |
| *PhoneFactor* | |
| *Active Directory do Azure* | |
| *Autodeclarado* | |
| *Conta local* | |
| *Gerenciamento da Sessão* | |
| *Mecanismo da política do Trustframework* | |
| *TechnicalProfiles* | |
| *Emissor do token* | |

## <a name="technical-profiles"></a>Perfis técnicos

Esta seção descreve perfis de técnicas Olá já declarados por provedor de declarações no hello *B2C_1A_base* política. Esses perfis técnicas são suscetível toobe mais referenciado, substituída, e/ou estendida conforme necessário em suas próprias políticas, bem como Olá *B2C_1A_base_extensions* política.

### <a name="technical-profiles-for-facebook"></a>Perfis técnicos para o Facebook

| Perfil técnico | Descrição |
|-------------------|-------------|
| *OAUTH do Facebook* | |

### <a name="technical-profiles-for-local-account-signin"></a>Perfis técnicos para entrada de conta Local

| Perfil técnico | Descrição |
|-------------------|-------------|
| *Login-NonInteractive* | |

### <a name="technical-profiles-for-phone-factor"></a>Perfis técnicos de Phone Factor

| Perfil técnico | Descrição |
|-------------------|-------------|
| *PhoneFactor-Input* | |
| *PhoneFactor-InputOrVerify* | |
| *PhoneFactor-Verify* | |

### <a name="technical-profiles-for-azure-active-directory"></a>Perfis técnicos para Azure Active Directory

| Perfil técnico | Descrição |
|-------------------|-------------|
| *AAD-Common* | Perfil técnico incluído por Olá outros perfis técnicos AAD xxx |
| *AAD-UserWriteUsingAlternativeSecurityId* | Perfil técnico para logons sociais |
| *AAD-UserReadUsingAlternativeSecurityId* | Perfil técnico para logons sociais |
| *AAD-UserReadUsingAlternativeSecurityId-NoError* | Perfil técnico para logons sociais |
| *AAD-UserWritePasswordUsingLogonEmail* | Perfil técnico para contas locais |
| *AAD-UserReadUsingEmailAddress* | Perfil técnico para contas locais |
| *AAD-UserWriteProfileUsingObjectId* | Perfil técnico para atualizar o registro de usuário usando o objectId |
| *AAD-UserWritePhoneNumberUsingObjectId* | Perfil técnico para atualizar o registro de usuário usando o objectId |
| *AAD-UserWritePasswordUsingObjectId* | Perfil técnico para atualizar o registro de usuário usando o objectId |
| *AAD-UserReadUsingObjectId* | Perfil técnica é usada tooread dados após a autenticação do usuário |

### <a name="technical-profiles-for-self-asserted"></a>Perfis técnicos para autodeclarados

| Perfil técnico | Descrição |
|-------------------|-------------|
| *SelfAsserted-Social* | |
| *SelfAsserted-ProfileUpdate* | |

### <a name="technical-profiles-for-local-account"></a>Perfis técnicos para conta local

| Perfil técnico | Descrição |
|-------------------|-------------|
| *LocalAccountSignUpWithLogonEmail* | |

### <a name="technical-profiles-for-session-management"></a>Perfis técnicos de gerenciamento de sessão

| Perfil técnico | Descrição |
|-------------------|-------------|
| *SM-Noop* | |
| *SM-AAD* | |
| *SM-SocialSignup* | Nome do perfil está sendo usado toodisambiguate AAD sessão entre o sinal de backup e entrar |
| *SM-SocialLogin* | |
| *SM-MFA* | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Perfis técnicos para TechnicalProfiles do mecanismo da política do Trustframework

No momento, não há perfis de técnicos são definidos para Olá **TechnicalProfiles de mecanismo de política Trustframework** provedor de declarações.

### <a name="technical-profiles-for-token-issuer"></a>Perfis técnicos de emissor do Token

| Perfil técnico | Descrição |
|-------------------|-------------|
| *JwtIssuer* | |

## <a name="user-journeys"></a>Percursos do usuário

Esta seção descreve Jornadas de usuário Olá já declaradas no hello *B2C_1A_base* política. Esses Jornadas de usuário são suscetível toobe mais referenciado, substituída, e/ou estendida conforme necessário em suas próprias políticas, bem como Olá *B2C_1A_base_extensions* política.

| Percurso do usuário | Descrição |
|--------------|-------------|
| *SignUp* | |
| *SignIn* | |
| *SignUpOrSignIn* | |
| *EditProfile* | |
| *PasswordReset* | |
