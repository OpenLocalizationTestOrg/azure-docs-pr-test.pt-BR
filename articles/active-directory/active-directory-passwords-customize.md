---
title: 'Personalizando: SSPR do Azure AD | Microsoft Docs'
description: "Opções de personalização para redefinição de senha por autoatendimento do Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>Personalizar a funcionalidade de Autoatendimento de Redefinição de Senha do Azure AD

Profissionais de TI procurando toodeploy redefinição de senha de autoatendimento podem personalizar Olá experiência toomatch seus usuários.

## <a name="customize-hello-contact-your-administrator-link"></a>Personalizar o contato Olá seu link de administrador

Mesmo se SSPR não estiver habilitados usuários ainda um link "Contate o administrador" senha Olá portal de redefinição.  Clicar nesse link emails seus administradores solicitando assistência ao alterar a senha do usuário hello. Este email é enviado toohello destinatários da saudação ordem a seguir:

1. Se hello **administrador de senhas** função é atribuída, os administradores com esta função são notificados
2. Se nenhuma senha os administradores são atribuídos, em seguida, administradores com hello **usuário administrador** devem ser notificados por função
3. Se nenhuma das funções anteriores Olá foram atribuídas, em seguida, **administradores globais** devem ser notificados

Em todos os casos, no máximo 100 destinatários serão notificados.

toofind mais informações sobre funções de administrador diferente hello e como tooassign-los consulte Olá documento [atribuindo funções de administrador no Active Directory do Azure](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>Desabilitar os emails “Contate o administrador”

Se sua organização não deseja que os administradores notificados sobre senha solicitações de redefinição, hello configuração a seguir pode ser habilitada

* Habilite o autoatendimento de redefinição de senha para todos os usuários finais. Essa opção pode ser encontrada em **Redefinição de Senha > Propriedades**.
    * Se você não desejar que os usuários tooreset suas próprias senhas, você pode definir o escopo grupo vazio do access tooan **não recomendamos essa opção**.
* Personalizar Olá tooprovide de link de suporte técnico, uma URL da web ou mailto: endereço que os usuários podem usar tooget assistência. Essa opção pode ser encontrada em **Redefinição de Senha > Personalização > URL ou email de assistência técnica personalizados**.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>Personalizar a página de entrada do AD FS para SSPR

Os administradores do AD FS pode adicionar uma link tootheir página de entrada usando Olá diretrizes encontradas no artigo Olá [adicionar descrição de página de entrada](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).

Usar o comando Olá seguir no servidor ADFS adiciona uma página de logon do link toohello ADFS permitindo que os usuários tooenter Olá senha de autoatendimento redefinição de fluxo de trabalho diretamente.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a>Personalizar Olá entrar e acesso painel aparência

Quando os usuários acessam página de logon hello, você pode personalizar o logotipo de saudação que é exibido junto com toofit de imagem na página de entrada hello sua identidade visual da empresa.

Esses elementos gráficos são mostrados na Olá circunstâncias a seguir:

* Depois que um usuário digita seu nome de usuário
* Quando o usuário acessa uma URL personalizada
    * Por passando Olá página, como "https://login.microsoftonline.com/?whr=contoso.com" de redefinição de senha de toohello do parâmetro de "whr"
    * Por passando hello "username" parâmetro toohello de redefinição de senha página, como "https://login.microsoftonline.com/?username=admin@contoso.com"

### <a name="graphics-details"></a>Detalhes de elementos gráficos

Olá configurações a seguir permitem características de visuais Olá toochange da página de entrada hello e pode ser encontradas em **Active Directory do Azure**, **identidade visual da empresa**, **Editar da empresa identidade Visual**

* A imagem da página de conexão deve ser um arquivo PNG ou JPG com 1420x1200 pixels e, no máximo, 500 KB. É recomendável toobe cerca de 200 KB para obter melhores resultados.
* Cor de plano de fundo da página de logon é usado quando em conexões de alta latência e deve estar no formato hexadecimal do hello RGB.
* A imagem da faixa deve ser um arquivo PNG ou JPG com 60x280 pixels e, no máximo, 10 KB.
* Logotipo quadrado (tema normal e escuro) em PNG ou JPG com 240x240 (redimensionável) e, no máximo, 10 KB.

### <a name="sign-in-text-options"></a>Opções do texto de conexão

Olá, as configurações a seguir permitem que você organização tooyour relevantes do tooadd texto toohello na página de entrada. Essas configurações podem ser encontradas em **Azure Active Directory**, **Identidade visual da empresa**, **Editar identidade visual da empresa**

* **Dica de nome de usuário** substitui o texto de exemplo de hello someone@example.com com algo mais apropriado para seus usuários, recomendado padrão esquerdo toobe ao oferecer suporte a usuários internos e externos
* O **texto da página de conexão** tem, no máximo, 256 caracteres. Esse texto é exibido em qualquer lugar seu logon de usuários online e em Olá experiência de junção do Azure AD no Windows 10. Use este texto para termos de uso, instruções e dicas para os usuários. **Qualquer pessoa pode ver sua página de conexão; portanto, não forneça informações confidenciais aqui.**

### <a name="keep-me-signed-in-disabled"></a>Opção “Manter-me conectado desabilitado”

opção Hello "Mantenha-me conectado desabilitado" permite que os usuários tooremain conectado quando eles feche e reabra a janela do navegador. Essa opção não afeta o tempo de vida da sessão. Essa configuração é encontrada em **Azure Active Directory > Identidade visual da empresa > Editar identidade visual da empresa**.

Alguns recursos do SharePoint Online e o Office 2010 têm uma dependência em usuários, sendo possível toocheck essa caixa. Se você ocultar essa opção, os usuários poderão receber prompts de conexão adicionais e inesperados.

### <a name="directory-name"></a>Nome do diretório

Você pode alterar o atributo de nome de saudação em **Active Directory do Azure > propriedades** tooshow um nome de organização amigável visto no portal de saudação e automatizado de comunicações. Esta opção é mais visível na forma de saudação de emails automatizados em formulários de saudação que siga

* Nome amigável em email “Microsoft em nome da demonstração da CONTOSO”
* Linha do assunto em email “Código de verificação de email da conta de demonstração da CONTOSO”

## <a name="next-steps"></a>Próximas etapas

Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD 
* [**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD
* [**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha
* [**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui
* [**Política** ](active-directory-passwords-policy.md) - Como entender e definir políticas de senha do Azure AD
* [**Write-back de senha** ](active-directory-passwords-writeback.md) - Como o write-back de senha opera com o seu diretório local
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona
* [**Perguntas frequentes**](active-directory-passwords-faq.md): como? Por quê? O quê? Onde? Quem? Quando? -Respostas tooquestions você sempre quis tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR

