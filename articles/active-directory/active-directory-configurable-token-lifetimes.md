---
title: tempos de vida de token de aaaConfigurable no Active Directory do Azure | Microsoft Docs
description: Saiba como tooset tempos de vida para tokens emitidos pelo AD do Azure.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a>Tempos de vida de token configuráveis no Azure Active Directory (Visualização Pública)
Você pode especificar o tempo de vida de saudação de um token emitido pelo Azure Active Directory (AD do Azure). Configure os tempos de vida de token de todos os aplicativos em uma organização, para um aplicativo multilocatário (várias organizações) ou para uma entidade de serviço específica em sua organização.

> [!NOTE]
> Esse recurso está atualmente em Visualização Pública. Prepare-se toorevert ou remova as alterações. recurso de saudação está disponível em qualquer assinatura do Azure Active Directory durante a visualização pública. No entanto, quando o recurso de saudação se torna disponível, alguns aspectos do recurso de saudação podem exigir um [Azure Active Directory Premium](active-directory-get-started-premium.md) assinatura.
>
>

No Azure AD, um objeto de política representa um conjunto de regras aplicadas a todos os aplicativos ou a aplicativos individuais em uma organização. Cada tipo de política tem uma estrutura única, com um conjunto de propriedades que são aplicadas tooobjects toowhich que são atribuídos.

Você pode designar uma política como política padrão de saudação para sua organização. política de saudação é aplicativo tooany aplicada na organização hello, desde que ele não é substituído por uma política com uma prioridade mais alta. Você também pode atribuir uma política toospecific aplicativos. ordem de saudação de prioridade varia de acordo com o tipo de política.


## <a name="token-types"></a>Tipos de token

Configure as políticas de tempo de vida de token para tokens de atualização, tokens de acesso, tokens de sessão e tokens de ID.

### <a name="access-tokens"></a>Tokens de acesso
Tooaccess um recurso protegido de tokens de acesso de uso de clientes. Um token de acesso só pode ser usado para uma combinação específica de usuário, cliente e recurso. Tokens de acesso não podem ser revogados e são válidos até sua expiração. Um ator mal-intencionado que tenha obtido um token de acesso pode usá-lo pela extensão do tempo de vida. Ajustando o tempo de vida de saudação de um acesso de token é uma compensação entre o aprimoramento de desempenho do sistema e crescentes Olá tempo total que Olá cliente mantém acesso depois de desabilitar a conta de usuário de saudação. Melhor desempenho do sistema é obtido reduzindo Olá número de vezes que um cliente precisa tooacquire um token de acesso de novo.

### <a name="refresh-tokens"></a>Tokens de atualização
Quando um cliente adquire um tooaccess de token de acesso um recurso protegido, o cliente Olá recebe um token de atualização e um token de acesso. token de atualização de saudação é novos pares de token de acesso/atualização tooobtain usado quando Olá token de acesso atual expirar. Um token de atualização é a combinação de tooa associada do usuário e do cliente. Um token de atualização pode ser revogado e validade do token de saudação é verificada sempre Olá token é usado.

É importante toomake uma distinção entre os clientes confidenciais e público. Para saber mais sobre os tipos diferentes de clientes, consulte [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a>Tempos de vida de token com tokens de atualização de cliente confidencial
Clientes confidenciais são aplicativos que podem armazenar com segurança uma senha (segredo) do cliente. Eles podem provar que as solicitações são provenientes de aplicativo de cliente hello e não de um ator mal-intencionado. Por exemplo, um aplicativo web é um cliente confidencial porque ele pode armazenar um segredo do cliente no servidor de web hello. Ele não fica exposto. Como esses fluxos são mais seguros, Olá tempos de vida padrão dos tokens de atualização é emitido toothese fluxos `until-revoked`, não pode ser alterado usando a política e não será revogada em redefinições de senha voluntária.

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a>Tempos de vida de token com tokens de atualização de cliente público

Clientes públicos não são capazes de armazenar com segurança a senha (segredo) de um cliente. Por exemplo, um aplicativo do iOS/Android não pode ofuscar um segredo do proprietário do recurso hello, para que ele seja considerado um cliente público. Você pode definir o políticas em recursos tooprevent tokens de atualização de público com mais de um período especificado, obtenha um novo par de tokens de atualização do acesso de clientes. (toodo hello, use propriedade atualizar Token inativo tempo máx.) Você também pode usar políticas tooset um ponto além dos tokens de atualização que Olá não são aceitas. (toodo hello, use propriedade atualizar Token Max Age.) Você pode ajustar o tempo de vida de saudação de um toocontrol de token de atualização e a frequência hello usuário é credenciais de tooreenter necessário, em vez de silenciosamente sendo reautenticado, ao usar um aplicativo de cliente público.

### <a name="id-tokens"></a>Tokens de ID
Tokens de ID são passadas toowebsites e clientes nativos. Os tokens de ID contêm informações de perfil sobre um usuário. Um token de ID é uma combinação específica de tooa associada do usuário e do cliente. Os tokens de ID são considerados válidos até a expiração. Normalmente, um aplicativo web corresponde a um usuário do tempo de vida de sessão no tempo de vida de toohello aplicativo de saudação do token de ID de saudação emitido para usuário hello. Você pode ajustar o tempo de vida de saudação de uma ID token toocontrol frequência aplicativo da web hello expira a sessão do aplicativo hello e frequência requer Olá toobe de usuário autenticado novamente com o Azure AD (silenciosamente ou interativamente).

### <a name="single-sign-on-session-tokens"></a>Tokens de sessão de logon único
Quando um usuário se autentica com o Azure AD e selecionará Olá **Mantenha-me conectado** caixa de seleção, é estabelecida uma sessão de logon único (SSO) com o navegador do usuário hello e o Azure AD. token SSO Hello, na forma de saudação de um cookie representa esta sessão. Observe que esse token de sessão SSO Olá não é aplicativo de recurso/cliente específico de tooa associada. Tokens de sessão de SSO podem ser revogados, e sua validade é verificada sempre que eles são usados.

O Azure AD usa dois tipos de tokens de sessão de SSO: persistente e não persistente. Tokens de sessão persistente são armazenados como cookies persistentes pelo navegador hello. Tokens de sessão não persistentes são armazenados como cookies de sessão. (Cookies de sessão são destruídos quando Olá navegador for fechado).

Tokens de sessão não persistentes têm uma vida útil de 24 horas. Tokens persistentes têm um tempo de vida de 180 dias. Sempre que um token de sessão SSO é usado dentro do período de validade, o período de validade de saudação é estendido outro 24 horas ou 180 dias, dependendo do tipo de token hello. Se o token de sessão de SSO não for usado dentro do período de validade, ele será considerado expirado e não será mais aceito.

Você pode usar um tempo de saudação política tooset após o primeiro token de sessão Olá foi emitido além do qual Olá token de sessão não é aceito. (toodo Olá, use propriedades de sessão Token Max Age.) Você pode ajustar o tempo de vida de saudação de um toocontrol de token de sessão quando e como um usuário é tooreenter necessário credenciais, em vez de sendo autenticado silenciosamente, ao usar um aplicativo web.

### <a name="token-lifetime-policy-properties"></a>Propriedades da política de tempo de vida de token
Uma política de tempo de vida do token é um tipo de objeto de política que contém regras de tempo de vida do token. Use propriedades de saudação do hello política toocontrol especificado tempos de vida de token. Se nenhuma diretiva for definida, o sistema de saudação impõe valor de tempo de vida padrão hello.

### <a name="configurable-token-lifetime-properties"></a>Propriedades de tempo de vida de token configurável
| Propriedade | Cadeia de caracteres de propriedade de política | Afeta | Padrão | Mínimo | Máximo |
| --- | --- | --- | --- | --- | --- |
| Tempo de Vida do Token de Acesso |AccessTokenLifetime |Tokens de acesso, tokens de ID, tokens SAML2 |1 hora |10 minutos |1 dia |
| Tempo Máximo Inativo de Token de Atualização |MaxInactiveTime |Tokens de atualização |14 dias |10 minutos |90 dias |
| Idade Máxima de Token de Atualização de Fator Único |MaxAgeSingleFactor |Tokens de atualização (para quaisquer usuários) |Until-revoked |10 minutos |Until-revoked<sup>1</sup> |
| Idade Máxima de Token de Atualização Multifator |MaxAgeMultiFactor |Tokens de atualização (para quaisquer usuários) |Until-revoked |10 minutos |Until-revoked<sup>1</sup> |
| Idade Máxima de Token de Sessão de Fator Único |MaxAgeSessionSingleFactor<sup>2</sup> |Tokens de sessão (persistentes e não persistentes) |Until-revoked |10 minutos |Until-revoked<sup>1</sup> |
| Idade Máxima de Token de Sessão Multifator |MaxAgeSessionMultiFactor<sup>3</sup> |Tokens de sessão (persistentes e não persistentes) |Until-revoked |10 minutos |Until-revoked<sup>1</sup> |

* <sup>1</sup>é de 365 dias Olá explícita comprimento máximo que pode ser definido para esses atributos.
* <sup>2</sup>se **MaxAgeSessionSingleFactor** não está definida, esse valor tem Olá **MaxAgeSingleFactor** valor. Se nenhum parâmetro for definido, a propriedade de saudação tem valor padrão de saudação (até revogado).
* <sup>3</sup>se **MaxAgeSessionMultiFactor** não está definida, esse valor tem Olá **MaxAgeMultiFactor** valor. Se nenhum parâmetro for definido, a propriedade de saudação tem valor padrão de saudação (até revogado).

### <a name="exceptions"></a>Exceções
| Propriedade | Afeta | Padrão |
| --- | --- | --- |
| Idade Máxima dos Tokens de Atualização (emitidos para usuários federados com informações de revogação insuficientes<sup>1</sup>) |Tokens de atualização (emitidos para usuários federados com informações de revogação insuficientes<sup>1</sup>) |12 horas |
| Tempo Máximo Inativo do Token de Atualização (emitido para clientes confidenciais) |Tokens de atualização (emitido para clientes confidenciais) |90 dias |
| Idade Máxima do Token de Atualização (emitido para clientes confidenciais) |Tokens de atualização (emitido para clientes confidenciais) |Until-revoked |

* <sup>1</sup>usuários federados que têm informações de revogação insuficiente incluem todos os usuários que não possuem hello "LastPasswordChangeTimestamp" atributo sincronizado. Esses usuários recebem esse breve Max Age como AAD é tooverify não é possível quando toorevoke tokens que são vinculados tooan antiga de credenciais (como uma senha que foi alterada) e deve verifique novamente em tooensure com mais frequência do que o usuário hello e tokens associados ainda são válidas. tooimprove essa experiência, locatário administradores devem garantir que eles estão sincronizando Olá atributo "LastPasswordChangeTimestamp" (Isso pode ser definido no objeto de usuário hello usando o Powershell ou por meio do AADSync).

### <a name="policy-evaluation-and-prioritization"></a>Avaliação e priorização de política
Você pode criar e atribuir um aplicativo específico do política tooa de vida útil do token, organização tooyour e tooservice entidades. Várias políticas podem ser aplicadas tooa determinado aplicativo. política de vida útil do token de saudação que entra em vigor segue estas regras:

* Se uma política seja atribuída explicitamente a entidade de serviço toohello, ela será aplicada.
* Se nenhuma política de entidade de serviço toohello atribuído explicitamente uma diretiva atribuídas explicitamente a organização de pai toohello da entidade de serviço Olá é aplicada.
* Se nenhuma política foi atribuída explicitamente toohello entidade de serviço ou organização toohello, política de saudação toohello aplicativo atribuída é aplicada.
* Se nenhuma política foi atribuída toohello principal, Olá organização ou objeto de aplicativo hello, Olá valores padrão do serviço é imposta. (Consulte tabela Olá [propriedades configuráveis vida útil do token](#configurable-token-lifetime-properties).)

Para obter mais informações sobre a relação Olá entre objetos application e service principal, consulte [objetos de aplicativo e serviço principal no Azure Active Directory](active-directory-application-objects.md).

Validade do token é avaliada em tempo de Olá Olá token é usado. política de saudação com prioridade mais alta de saudação no aplicativo hello que está sendo acessado entra em vigor.

> [!NOTE]
> Veja um exemplo de cenários.
>
> Um usuário deseja tooaccess dois aplicativos de web: aplicativo Web A e B. do aplicativo Web
> 
> Fatores:
> * Ambos os aplicativos web estão em Olá mesmo pai de organização.
> * 1 de diretiva de tempo de vida do token com uma sessão Token Max Age de oito horas é definido como padrão da organização do hello pai.
> * Um aplicativo é um aplicativo web de uso normal e não é vinculado tooany políticas.
> * O Aplicativo Web B é usado para processos altamente confidenciais. Essa entidade de serviço é vinculado tooToken 2 de tempo de vida de política, que tem uma sessão Token Max Age de 30 minutos.
>
> Às 12:00, usuário Olá inicia uma nova sessão do navegador e tentativas tooaccess A. do aplicativo Web hello usuário é redirecionado tooAzure AD e será solicitado a toosign no. Isso cria um cookie que tem um token de sessão no navegador de saudação. usuário de saudação é tooWeb redirecionado back um aplicativo com um token de ID que permite Olá usuário tooaccess aplicativo hello.
>
> Às 12:15:00, o usuário de saudação tenta tooaccess B. do aplicativo Web hello navegador redirecionamentos tooAzure AD, que detecta o cookie de sessão hello. Entidade de serviço da Web aplicativo B é vinculado tooToken 2 de tempo de vida de política, mas ele também faz parte da organização do pai hello, com padrão de 1 de diretiva de tempo de vida do Token. 2 de política de tempo de vida do token entra em vigor porque políticas tooservice vinculado entidades têm uma prioridade mais alta que as políticas padrão de organização. o token de sessão Olá foi originalmente lançado em Olá últimos 30 minutos, para que ele seja considerado válido. usuário de saudação é tooWeb redirecionado back aplicativo B com um token de ID que concede acesso eles.
>
> Às 13:00, Olá tentativas tooaccess A. do aplicativo Web hello usuário é redirecionado tooAzure AD. Um aplicativo da Web não está vinculado tooany políticas, mas porque ele está em uma organização com um padrão 1 de diretiva de tempo de vida do Token, essa política entra em vigor. cookie de sessão Olá que foi originalmente lançado em Olá últimas oito horas é detectado. usuário de saudação é tooWeb silenciosamente redirecionado back um aplicativo com um novo token de ID. usuário de saudação não é necessário tooauthenticate.
>
> Imediatamente depois disso, o usuário Olá tenta usuário de saudação do tooaccess B. do aplicativo Web é redirecionado tooAzure AD. Como antes, a Política de tempo de vida de token 2 entra em vigor. Token Olá foi emitido há mais de 30 minutos, o usuário de Olá é tooreenter solicitada suas credenciais de logon. Um token de sessão e um token de ID totalmente novos são emitidos. Olá usuário poderá acessar B. do aplicativo Web
>
>

## <a name="configurable-policy-property-details"></a>Detalhes configuráveis da propriedade da política
### <a name="access-token-lifetime"></a>Tempo de Vida do Token de Acesso
**Cadeia de caracteres:** AccessTokenLifetime

**Afeta:** tokens de acesso, tokens de ID

**Resumo:** essa política controla por quanto tempo tokens de acesso e ID para esse recurso são considerados válidos. Reduzindo a propriedade de vida útil do Token acesso Olá reduz o risco de saudação de um token de acesso ou o token de ID que está sendo usado por um ator mal-intencionado por um longo período de tempo. (Esses tokens não podem ser revogados.) compensação de saudação é que o desempenho é afetado negativamente, como tokens de saudação têm toobe substituída com mais frequência.

### <a name="refresh-token-max-inactive-time"></a>Tempo Máximo Inativo de Token de Atualização
**Cadeia de caracteres:** MaxInactiveTime

**Afeta:** tokens de atualização

**Resumo:** esta política controla quanto tempo um token de atualização pode ser antes que um cliente não poderá mais usá-lo tooretrieve um novo par de tokens de atualização do acesso ao tentar tooaccess esse recurso. Porque um novo token de atualização normalmente é retornado quando um token de atualização é usado, esta política impede o acesso se o cliente Olá tenta tooaccess qualquer recurso usando o token de atualização atual Olá durante a saudação especificado o período de tempo.

Essa política força os usuários que não estão ativos em seu tooretrieve tooreauthenticate do cliente um novo token de atualização.

Olá propriedade atualizar Token inativo tempo máximo deve ser definido tooa menor valor de fator único Token Max Age de saudação Olá multifator atualizar Token Max Age propriedades e.

### <a name="single-factor-refresh-token-max-age"></a>Idade Máxima de Token de Atualização de Fator Único
**Cadeia de caracteres:** MaxAgeSingleFactor

**Afeta:** tokens de atualização

**Resumo:** essa política controla como longa um usuário pode usar um tooget de token de atualização de um novo acesso/atualização par de tokens após eles última autenticados com êxito usando apenas um único fator. Depois que um usuário se autentica e recebe um novo token de atualização, o usuário de Olá pode usar o fluxo do token de atualização Olá para Olá especificado período de tempo. (Isso é verdadeiro contanto que o token de atualização atual Olá não for revogado e ele não estiver em uso por mais de tempo de inatividade hello.) Nesse ponto, o usuário de saudação é forçado tooreauthenticate tooreceive um novo token de atualização.

Reduzindo a idade máxima Olá força tooauthenticate de usuários com mais frequência. Como autenticação de fator único é considerada menos segura do que a autenticação multifator, recomendamos que você defina o valor da propriedade tooa que é igual tooor anterior de saudação propriedade multifator atualizar Token Max Age.

### <a name="multi-factor-refresh-token-max-age"></a>Idade Máxima de Token de Atualização Multifator
**Cadeia de caracteres:** MaxAgeMultiFactor

**Afeta:** tokens de atualização

**Resumo:** essa política controla como longa um usuário pode usar um tooget de token de atualização de um novo acesso/atualização par de tokens após eles última autenticados com êxito por meio de vários fatores. Depois que um usuário se autentica e recebe um novo token de atualização, o usuário de Olá pode usar o fluxo do token de atualização Olá para Olá especificado período de tempo. (Isso é verdadeiro contanto que o token de atualização atual Olá não foi revogado e não é não utilizado por mais de tempo de inatividade hello.) Nesse ponto, os usuários são forçados tooreauthenticate tooreceive um novo token de atualização.

Reduzindo a idade máxima Olá força tooauthenticate de usuários com mais frequência. Como autenticação de fator único é considerada menos segura do que a autenticação multifator, é recomendável que você defina este valor da propriedade tooa que é maior do que a propriedade de fator único atualizar Token Max Age Olá de tooor igual.

### <a name="single-factor-session-token-max-age"></a>Idade Máxima de Token de Sessão de Fator Único
**Cadeia de caracteres:** MaxAgeSessionSingleFactor

**Afeta:** tokens de sessão (persistentes e não persistentes)

**Resumo:** essa política controla quanto tempo um usuário pode usar um tooget de token de sessão uma ID e uma nova sessão de token após eles última autenticados com êxito usando apenas um único fator. Depois que um usuário se autentica e recebe um token de nova sessão, o usuário de saudação pode usar o fluxo do token de sessão Olá para Olá especificado período de tempo. (Isso é verdadeiro, desde que o token da sessão atual Olá não foi revogado e não expirou.) Depois de saudação especificado um período de tempo, usuário Olá é forçado tooreauthenticate tooreceive um token de nova sessão.

Reduzindo a idade máxima Olá força tooauthenticate de usuários com mais frequência. Como autenticação de fator único é considerada menos segura do que a autenticação multifator, é recomendável que você defina este valor da propriedade tooa que é propriedade de sessão Token Max Age multifator tooor menor que Olá igual.

### <a name="multi-factor-session-token-max-age"></a>Idade Máxima de Token de Sessão Multifator
**Cadeia de caracteres:** MaxAgeSessionMultiFactor

**Afeta:** tokens de sessão (persistentes e não persistentes)

**Resumo:** essa política controla quanto tempo um usuário pode usar um tooget de token de sessão uma ID e uma nova sessão de token após Olá a última vez em que eles autenticados com êxito por meio de vários fatores. Depois que um usuário se autentica e recebe um token de nova sessão, o usuário de saudação pode usar o fluxo do token de sessão Olá para Olá especificado período de tempo. (Isso é verdadeiro, desde que o token da sessão atual Olá não foi revogado e não expirou.) Depois de saudação especificado um período de tempo, usuário Olá é forçado tooreauthenticate tooreceive um token de nova sessão.

Reduzindo a idade máxima Olá força tooauthenticate de usuários com mais frequência. Como autenticação de fator único é considerada menos segura do que a autenticação multifator, é recomendável que você defina este valor da propriedade tooa que é maior do que a propriedade de fator único sessão Token Max Age Olá de tooor igual.

## <a name="example-token-lifetime-policies"></a>Exemplo de políticas de tempo de vida do token
Muitos cenários são possíveis no Azure AD quando você cria e gerencia tempos de vida de token para aplicativos, entidades de serviço e sua organização geral. Nesta seção, examinaremos alguns cenários comuns de políticas que ajudarão você a impor novas regras para:

* Tempo de vida do token
* Tempo Máximo Inativos de Token
* Idade Máxima de Token

Exemplos de saudação, você pode aprender como:

* Gerenciar a política padrão de uma organização
* Criar uma política para entrada na Web
* Criar uma política para um aplicativo nativo que chama uma API da Web
* Gerenciar uma política avançada

### <a name="prerequisites"></a>Pré-requisitos
Em Olá exemplos a seguir, você cria, atualizar, vincula e excluir as políticas de aplicativos, as entidades de serviço e sua organização. Se você for novo tooAzure AD, é recomendável que você conheça [como tooget um AD do Azure locatário](active-directory-howto-tenant.md) antes de prosseguir com esses exemplos.  

tooget iniciado, Olá etapas a seguir:

1. Baixar hello mais recente [versão de visualização do Azure AD PowerShell módulo público](https://www.powershellgallery.com/packages/AzureADPreview).
2. Executar Olá `Connect` comando toosign em tooyour conta de administrador do AD do Azure. Execute esse comando sempre que você iniciar uma nova sessão.

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. toosee todas as políticas que foram criadas em sua organização, Olá execução após o comando. Execute este comando após a maioria das operações no hello cenários a seguir. Executando o comando Olá também ajuda você a obter hello * * * * de suas políticas.

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a>Exemplo: Gerenciar a política padrão de uma organização
Neste exemplo, crie uma política que permita aos usuários fazerem logon com menos frequência em toda sua organização. toodo, criar uma política de vida útil do token de fator único atualizar Tokens, que é aplicado em sua organização. política de saudação é aplicado tooevery aplicativo em sua organização e a entidade de serviço tooeach que ainda não tiver uma política definida.

1. Crie uma política de tempo de vida de token.

    1.  Saudação de conjunto de fator único Token de atualização muito "até revogados." token de saudação não expira até que o acesso é revogado. Crie hello após a definição de política:

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  diretiva toocreate hello, executar Olá comando a seguir:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  toosee sua nova política e da política de saudação tooget **ObjectId**, execute hello seguinte comando:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Atualize a política de saudação.

    Você pode decidir que a política de primeiro do hello definido neste exemplo não é como estrita como seu serviço exigir. tooset seu Token de atualização de fator único tooexpire em dois dias, executar Olá seguinte comando:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a>Exemplo: Criar uma política para entrada na Web

Neste exemplo, você deve criar uma política que exige que os usuários tooauthenticate com mais frequência em seu aplicativo web. Essa política define o tempo de vida de saudação de tokens de acesso/ID hello e idade máxima de saudação da entidade de serviço de token toohello sessão de vários fatores de seu aplicativo web.

1. Crie uma política de tempo de vida de token.

    Essa política, para entrar no web, define a vida útil do token acesso ID hello e horas de tootwo Olá máximo de sessões de fator único token de idade.

    1.  diretiva toocreate hello, execute este comando:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee sua nova política e política de saudação tooget **ObjectId**, execute hello seguinte comando:

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  Atribua a entidade de serviço Olá política tooyour. Você também precisa tooget Olá **ObjectId** sua entidade de serviço. 

    1.  toosee entidades de serviço de todas as da sua organização, você pode consultar [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). Ou, no [do Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), entrar tooyour conta AD do Azure.

    2.  Quando você tiver Olá **ObjectId** sua entidade de serviço, execute Olá comando a seguir:

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a>Exemplo: Criar uma política para um aplicativo nativo que chama uma API da Web
Neste exemplo, você deve criar uma política que exige que os usuários tooauthenticate menos frequentemente. política de saudação também aumenta a quantidade de saudação de tempo que um usuário pode ficar inativo antes que o usuário Olá deve autenticar novamente. política de saudação é aplicado toohello web API. Quando o aplicativo nativo Olá solicita Olá web API como um recurso, essa política é aplicada.

1. Crie uma política de tempo de vida de token.

    1.  toocreate uma política estrita para uma API da web, execute Olá comando a seguir:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee sua nova política e política de saudação tooget **ObjectId**, execute hello seguinte comando:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Atribua Olá política tooyour web API. Você também precisa tooget Olá **ObjectId** do seu aplicativo. Olá toofind de maneira melhor seu aplicativo **ObjectId** é hello toouse [portal do Azure](https://portal.azure.com/).

   Quando você tiver Olá **ObjectId** do seu aplicativo, executar Olá comando a seguir:

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a>Exemplo: Gerenciar uma política avançada
Neste exemplo, você deve criar políticas de alguns, toolearn como funciona o sistema de prioridade de saudação. Você também pode aprender como toomanage várias políticas são aplicadas tooseveral objetos.

1. Crie uma política de tempo de vida de token.

    1.  toocreate uma política padrão de organização que define os dias Olá too30 de tempo de vida de Token de atualização de fator único, executados Olá comando a seguir:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  toosee sua nova política e da política de saudação tooget **ObjectId**, execute hello seguinte comando:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Atribua a entidade de serviço Olá política tooa.

    Agora, você tem uma política que se aplica a toda a organização toohello. Você pode deseja toopreserve essa política de 30 dias para uma entidade de serviço específico, mas alterar Olá organização padrão política toohello limite superior de "até revogados."

    1.  toosee entidades de serviço de todas as da sua organização, você pode consultar [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). Ou, no [Graph Explorer do Azure AD](https://graphexplorer.cloudapp.net/), entre usando sua conta do Azure AD.

    2.  Quando você tiver Olá **ObjectId** sua entidade de serviço, execute Olá comando a seguir:

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. Saudação de conjunto `IsOrganizationDefault` sinalizador toofalse:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. Crie uma nova política padrão de organização:

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    Você agora tem a entidade de serviço para Olá original política tooyour vinculado e nova política de saudação é definida como a diretiva de sua organização. É importante tooremember que políticas aplicadas tooservice entidades têm prioridade sobre políticas de padrão da organização.

## <a name="cmdlet-reference"></a>Referência de cmdlet

### <a name="manage-policies"></a>Gerenciar políticas

Você pode usar o hello cmdlets toomanage políticas a seguir.

#### <a name="new-azureadpolicy"></a>New-AzureADPolicy

Cria uma nova política.

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| Parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Definition</code> |Matriz de stringified JSON que contém regras da política de saudação todas as. | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |Cadeia de caracteres do nome da política hello. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |Se true, define a política de saudação como política de padrão da organização hello. Se for false, não fará nada. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |O tipo da política. Para os tempos de vida de token, sempre use "TokenLifetimePolicy". | `-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code> [Opcional] |Define uma ID alternativa para política de saudação. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a>Get-AzureADPolicy
Obtém todas as políticas do Azure AD ou a política especificada.

```PowerShell
Get-AzureADPolicy
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> [Opcional] |**ObjectId (Id)** da política de saudação desejado. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a>Get-AzureADPolicyAppliedObject
Obtém todos os aplicativos e entidades de serviço que são vinculados tooa política.

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** da política de saudação desejado. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a>Set-AzureADPolicy
Atualiza uma política existente.

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** da política de saudação desejado. |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |Cadeia de caracteres do nome da política hello. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;Definition</code> [Opcional] |Matriz de stringified JSON que contém regras da política de saudação todas as. |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;IsOrganizationDefault</code> [Opcional] |Se true, define a política de saudação como política de padrão da organização hello. Se for false, não fará nada. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> [Opcional] |O tipo da política. Para os tempos de vida de token, sempre use "TokenLifetimePolicy". |`-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code> [Opcional] |Define uma ID alternativa para política de saudação. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a>Remove-AzureADPolicy
Olá exclusões especificado política.

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** da política de saudação desejado. | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a>Políticas de aplicativo
Você pode usar o hello cmdlets para políticas de aplicativos a seguir.</br></br>

#### <a name="add-azureadapplicationpolicy"></a>Add-AzureADApplicationPolicy
Saudação de links especificado tooan aplicação da política.

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID (Id) do objeto** do aplicativo hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** da política de saudação. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a>Get-AzureADApplicationPolicy
Obtém a política de saudação tooan aplicativo atribuído.

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID (Id) do objeto** do aplicativo hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a>Remove-AzureADApplicationPolicy
Remove uma política de um aplicativo.

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID (Id) do objeto** do aplicativo hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** da política de saudação. | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a>Políticas de entidade de serviço
Você pode usar o hello cmdlets para políticas de entidade de serviço a seguir.

#### <a name="add-azureadserviceprincipalpolicy"></a>Add-AzureADServicePrincipalPolicy
Links Olá entidade de serviço tooa política especificada.

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID (Id) do objeto** do aplicativo hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** da política de saudação. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a>Get-AzureADServicePrincipalPolicy
Obtém a qualquer entidade de serviço especificado política toohello vinculado.

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID (Id) do objeto** do aplicativo hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a>Remove-AzureADServicePrincipalPolicy
Remove a política de saudação da entidade de serviço especificado do hello.

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| parâmetros | Descrição | Exemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID (Id) do objeto** do aplicativo hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** da política de saudação. | `-PolicyId <ObjectId of Policy>` |
