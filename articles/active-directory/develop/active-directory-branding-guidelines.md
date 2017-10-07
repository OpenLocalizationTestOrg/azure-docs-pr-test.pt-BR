---
title: Diretrizes para aplicativos de aaaBranding | Microsoft Docs
description: Um abrangente guia recursos orientados toodeveloper para Active Directory do Azure
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a>Diretrizes de identidade visual para aplicativos
Este tópico discute Olá marca diretrizes que você deve usar ao desenvolver aplicativos com o Azure Active Directory (AD do Azure). Essas diretrizes ajudarão a orientar seus clientes quando eles querem toouse seu trabalho ou conta de escola, gerenciada no AD do Azure ou sua conta pessoal para tooyour de inscrição e entrar no aplicativo.

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a>Contas pessoais versus contas comerciais ou de estudante da Microsoft
A Microsoft gerencia dois tipos de contas de usuário:

* **Contas pessoais** (anteriormente conhecidas como Windows Live ID). Essas contas representam a relação de saudação entre *individuais* usuários e Microsoft e são usados dispositivos de consumidor tooaccess e serviços da Microsoft. Essas contas são destinadas a uso pessoal.
* **Contas comerciais ou de estudante.** Essas contas são gerenciadas pela Microsoft em nome de organizações que usam o Azure Active Directory. Essas contas são usada toosign tooOffice 365 e outros serviços comerciais da Microsoft.

Microsoft contas corporativa ou escolar normalmente são atribuídos a usuários tooend (funcionários, alunos, funcionários federais) por suas organizações (empresa, escola, órgão do governo). Essas contas são que seja controlado diretamente na nuvem de hello, na plataforma de saudação do AD do Azure ou sincronizado tooAzure AD de um diretório local, como o Windows Server Active Directory. A Microsoft está Olá *custodiante* de trabalho hello ou contas de estudante, mas Olá contas de propriedade e controladas pela organização de saudação.

## <a name="referring-tooazure-ad-accounts-in-your-application"></a>Referindo-se contas tooAzure AD em seu aplicativo
Microsoft não expõe os usuários finais toohello do Azure ou nomes de marca saudação do Active Directory e nem caso.

* Depois que os usuários conectados, você deve usar o nome da organização hello e o logotipo tanto quanto possível. Isso é melhor do que usar termos genéricos como "sua organização".
* Quando os usuários não estiver conectados, você deve consultar contas tootheir como "trabalho ou escolares" e use Olá Microsoft logotipo tooconvey que essas contas são gerenciadas pela Microsoft. Não use termos como "conta comercial", "conta empresarial" ou "conta corporativa", que criam confusão no usuário.

## <a name="user-account-pictogram"></a>Imagem da conta de usuário
Em uma versão anterior dessas diretrizes, recomendamos usar uma imagem de "crachá azul". Com base nos comentários de usuário e de desenvolvedor, agora recomendamos usar saudação do logotipo da Microsoft hello em vez disso. Isso ajudará os usuários a entender o que conta Olá usado com o Office 365 ou outros toosign de serviços do Microsoft business no aplicativo tooyour podem reutilizar.

## <a name="signing-up-and-signing-in-with-azure-ad"></a>Inscrever-se e entrar no Azure AD
Seu aplicativo pode apresentar caminhos separados para se inscrever e entrar e Olá seções a seguir fornece orientação visual para os dois cenários.

**Se seu aplicativo dá suporte a inscrição do usuário final (por exemplo, livre tootrial ou freemium modelo)**: você pode mostrar um **entrar** botão que permite que os usuários tooaccess seu aplicativo com sua conta corporativa ou sua conta pessoal. Azure AD exibirá uma saudação de prompt de consentimento primeira vez que acessarem o seu aplicativo.

**Se seu aplicativo precisar de permissões que somente os administradores podem conferir, ou se seu aplicativo requer licenciamento organizacional**: você deve separar a aquisição do administrador do logon do usuário. Olá **botão "obter este aplicativo"** será redirecionar toosign admins no e peça-lhes toogrant consentimento em nome dos usuários em sua organização. Isso tem Olá benefício adicional de suprimir os usuários finais consentimento prompts tooyour aplicativo.

## <a name="visual-guidance-for-app-acquisition"></a>Orientação visual para aquisição de aplicativo
O link "obter o aplicativo hello" deve redirecionar conceder acesso ao Olá usuário toohello do Azure AD (Autorizar) página, tooallow tooauthorize de administrador da organização toohave seu aplicativo acessar dados da organização tootheir que são hospedados pela Microsoft. Obter detalhes sobre como toorequest acesso são discutidos em Olá [integrando aplicativos com o Active Directory do Azure](active-directory-integrating-applications.md) artigo.

Depois de administradores de consentimento tooyour aplicativo, eles podem escolher tooadd-experiência dos usuários tootheir Office 365 aplicativo iniciador (acessível de waffle Olá em [https://portal.office.com/myapps](https://portal.office.com/myapps)). Se você quiser tooadvertise esse recurso, você pode usar termos como "Adicionar organização tooyour aplicativo" e mostrar um botão como este:

![Cenários e tipos de aplicativos](./media/active-directory-branding-guidelines/add-to-my-org.png)

No entanto, recomendamos que você escreva um texto explicativo em vez de depender de botões. Por exemplo:

> *Se você já usa o Office 365 ou outros serviços corporativos da Microsoft, você pode simplesmente conceder os dados da organização do tooyour < your_app_name > acesso. Isso permitirá que seus usuários tooaccess < your_app_name > com suas contas de trabalho existente.*
> 
> 

## <a name="visual-guidance-for-sign-in"></a>Orientação visual para logon
Seu aplicativo deve exibir um sinal no botão que redireciona os usuários toohello entrar no ponto de extremidade que corresponde a protocolo toohello usar toointegrate com o Azure AD. Olá seção a seguir fornece detalhes sobre o que deve ser a aparência de botão.

### <a name="pictogram-and-sign-in-with-microsoft"></a>Ícone e “Entrar com a Conta da Microsoft”
Ele 's associação de saudação do logotipo da Microsoft hello e termos de "Sign in with Microsoft" hello que representa com exclusividade o Azure AD entre outros provedores de identidade que pode dar suporte a seu aplicativo. Se você não tiver espaço suficiente para "Sign in with Microsoft", é okey tooshorten ele muito "entrar".

![Cenários e tipos de aplicativos](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![Cenários e tipos de aplicativos](./media/active-directory-branding-guidelines/sign-in-light.png)

Você também pode usar um esquema de cores escuro botões hello.

![Cenários e tipos de aplicativos](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![Cenários e tipos de aplicativos](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a>Regras de identidade visual
**FAZER** use "conta corporativa ou de estudante" em combinação com hello "Sign in with Microsoft" botão tooprovide explicação adicional toohelp os usuários finais reconhecer se ele podem usá-lo. **NÃO USE** outros termos, como "conta comercial", "conta empresarial" ou "conta corporativa".

**NÃO** use "ID do Office 365" ou "ID do Azure". O Office 365 também é nome hello de um consumidor da Microsoft que não usa o Azure AD para autenticação.

**Não** alterar logotipo da Microsoft hello.

**Não** expor as marcas de Azure Active Directory ou de toohello os usuários finais. É okey porém toouse esses termos com desenvolvedores, profissionais de TI e administradores.

## <a name="navigation-dos-and-donts"></a>Regras de navegação
**FAZER** fornecem uma maneira para os usuários toosign out e altere a conta de usuário tooanother. Embora a maioria das pessoas tenha uma única conta pessoal da Microsoft/Facebook/Google/Twitter, as pessoas geralmente são associadas a mais de uma organização. O suporte a vários usuários conectados estará disponível em breve.

