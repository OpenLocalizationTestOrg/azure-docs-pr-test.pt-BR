---
title: "aaaCustomize sua entrada no página Olá Active Directory do Azure | Microsoft Docs"
description: "Saiba como tooadd uma página toohello sign-in do Azure da identidade visual da empresa"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>Início rápido: Adicionar identidade visual tooyour na página de entrada no AD do Azure
tooavoid confusão, muitas empresas deseja tooapply uma aparência consistente em todos os sites de saudação e serviços que gerenciam. Azure Active Directory (AD do Azure) fornece esse recurso, permitindo-lhe toocustomize Olá aparência Olá entrar página com o logotipo da empresa e esquemas de cores personalizadas. Olá entrar é Olá página que aparece quando você entrar no tooOffice 365 ou outros aplicativos baseados na web que estão usando o AD do Azure como seu provedor de identidade. Você interage com essa página tooenter suas credenciais.

> [!NOTE]
> * Identidade visual da empresa está disponível somente se você atualizar toohello Premium ou edição básica do AD do Azure ou ter uma licença do Office 365. toolearn se um recurso tem suporte por seu tipo de licença, marque Olá [página de informações sobre preços do Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).
> 
> * O Azure Active Directory Premium e edições Basic estão disponíveis para clientes na China usando a instância mundial de saudação do Active Directory do Azure. O Azure Active Directory Premium e edições Basic não têm suporte no momento no serviço do Microsoft Azure Olá operado pela 21Vianet na China. Para obter mais informações, entre em contato conosco em Olá [Fórum do Active Directory do Azure](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="customizing-hello-sign-in-page"></a>Personalizando a página de entrada hello

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

Empresa personalizações de identidade visual exibido na página de entrada hello Azure AD quando os usuários acessam uma URL específica do locatário, como [ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com).

Quando os usuários visitam uma URL genérica, como www.office.com, página de entrada hello não tem marca personalizações porque o sistema de saudação não saber quem é o usuário de saudação da empresa. A identidade visual da empresa aparecerá depois que os usuários inserirem sua ID de usuário ou selecionarem um bloco do usuário.

> [!NOTE]
> * O nome do domínio deve aparecer como "Ativo" no hello **domínios** Olá a parte do portal do Azure no qual você configurou a identidade visual. Para saber mais, confira [Adicionar um nome de domínio personalizado](add-custom-domain.md).
> * Identidade visual da página de entrada não reporta toohello página de entrada para contas da Microsoft pessoais. Se seus funcionários ou parceiros de negócios convidados entram com uma conta pessoal da Microsoft, sua página não reflete Olá identidade visual da sua organização.


### <a name="banner-logo"></a>Logotipo de faixa 

Descrição | Restrições | Recomendações
------- | ------- | ----------
logotipo do banner Olá é exibido na entrada hello e páginas de painel de acesso de saudação.<br>Olá página de entrada, isso mostra depois que a organização saudação do usuário é determinada, geralmente após a saudação de nome de usuário é inserido.  | JPG ou PNG transparente<br>Altura máxima: 36 px<br>Largura máxima: 245 px | Use o logotipo da sua organização aqui.<br>Use uma imagem transparente. Não suponha que o plano de fundo de saudação será branco.<br>Não adicionar preenchimento ao redor de seu logotipo na imagem hello ou seu logotipo aparecerá desproporcionalmente pequeno.

### <a name="username-hint"></a>Dica do nome de usuário   
Descrição | Restrições | Recomendações
------- | ------- | ----------
Isso personaliza o texto de dica de saudação no campo de nome de usuário de saudação. | Texto Unicode too64 caracteres<br>Somente texto sem formatação | É recomendável que você não defina isso se você espera que os usuários convidados fora toosign sua organização no aplicativo tooyour.
            
### <a name="sign-in-page-text"></a>Texto da página de entrada   
Descrição | Restrições | Recomendações
------- | ------- | ----------
Isso aparece na parte inferior de saudação do formulário de entrada hello e pode ser usado toocommunicate obter informações adicionais como Olá phone número tooyour técnico ou uma instrução legal. | Texto Unicode too256 caracteres<br>Apenas texto sem formatação (sem links ou marcas HTML) 

### <a name="sign-in-page-image"></a>Imagem da página de entrada  
Descrição | Restrições | Recomendações
------- | ------- | ----------
Isso aparece no plano de fundo de saudação do hello página de entrada, é ancorado toohello Centro de espaço visível do hello e dimensionar e cortar toofill janela do navegador hello.  <br>Em telas estreitas, como celulares, a imagem não é mostrada.<br>Uma máscara de preta com opacidade 0.55 será aplicada sobre essa imagem pelo nosso código quando Olá página for carregada. | JPG ou PNG<br>Dimensões da imagem: 1920 x 1080 px<br>Tamanho do arquivo: &gt; 300 KB | <br>Use imagens que não possuam um foco forte no assunto. Olá opaco entrar formulário aparece sobre o Centro de saudação desta imagem e pode abranger qualquer parte da imagem Olá dependendo do tamanho de Olá Olá da janela do navegador.<br>Manter o tamanho do arquivo hello menor tempos de carregamento rápido de tooensure possíveis. 

### <a name="background-color"></a>Cor da tela de fundo
Descrição | Restrições | Recomendações
------- | ------- | ----------
Esta cor é usada no lugar da imagem de plano de fundo de saudação em conexões de baixa largura de banda. |   Cor RGB em hexadecimal (exemplo: #FFFFFF | Nós sugerimos usar cor primária de saudação do logotipo do banner hello ou a cor da organização.

### <a name="show-option-tooremain-signed-in"></a>Mostrar opção tooremain conectado
Descrição | Restrições | Recomendações
------- | ------- | ----------
Entrada do Azure AD oferece Olá usuário Olá opção tooremain conectado quando eles feche e reabra o navegador. Use este toohide essa opção.<br>Defina isso muito "não" toohide dessa opção a partir de seus usuários. | &nbsp; | Ela não afeta o tempo de vida da sessão.<br>Alguns recursos do SharePoint Online e o Office 2010 dependem de usuários que estão sendo tooremain toochoose capaz de entrar. Se você definir esse toobe oculta, seus usuários podem ver prompts adicionais e inesperados em toosign.

> [!NOTE]
> Todos os elementos são opcionais. Por exemplo, se você especificar um logotipo de faixa com nenhuma imagem de plano de fundo, a página de entrada hello mostrará sua imagem de fundo do logotipo e Olá Olá para site de destino (por exemplo, Office 365).

## <a name="add-company-branding-tooyour-directory"></a>Adicionar identidade visual tooyour directory da empresa

1. Entrar muito[Olá portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.

   ![Abrir o gerenciamento de usuários](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Em Olá **usuários e grupos** folha, selecione **identidade visual da empresa**.
4. Em Olá **usuários e grupos - identidade visual da empresa** folha, selecione Olá **editar** comando.

    ![Editar identidade visual personalizada](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Modificar Olá elementos você deseja toocustomize. Todos os elementos são opcionais.
6. Clique em **Salvar**.

Pode demorar até tooan horas para que as alterações feitas toohello entrar tooappear identidade visual da página.

## <a name="add-language-specific-company-branding-tooyour-directory"></a>Adicionar marca tooyour directory da empresa de idioma específico

1. Entrar toohello [Centro de administração do AD do Azure](https://aad.portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.

   ![Abrir o gerenciamento de usuários](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Em Olá **usuários e grupos** folha, selecione **identidade visual da empresa**.
4. Em Olá **usuários e grupos - identidade visual da empresa** folha, selecione Olá **Adicionar idioma** comando.

    ![Adicionar elementos de identidade visual específicos do idioma](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Modificar Olá elementos você deseja toocustomize. Todos os elementos são opcionais.
6. Clique em **Salvar**.

Pode demorar até tooan horas para que as alterações feitas toohello entrar tooappear identidade visual da página.

## <a name="next-steps"></a>Próximas etapas
Este guia de início rápido, você aprendeu como tooadd da empresa do diretório de identidade visual tooyour AD do Azure. 

Você pode usar o hello tooconfigure de link a seguir sua marca no AD do Azure de saudação do Azure portal da empresa.

> [!div class="nextstepaction"]
> [Configurar a identidade visual da empresa](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 