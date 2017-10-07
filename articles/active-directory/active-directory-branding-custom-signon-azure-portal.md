---
title: "aaaCustomize sua entrada no página Olá Active Directory do Azure | Microsoft Docs"
description: "Saiba como tooadd uma página toohello sign-in do Azure da identidade visual da empresa"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Adicionar identidade visual tooyour página de entrada de saudação do Active Directory do Azure
tooavoid confusão, muitas empresas deseja tooapply uma aparência consistente em todos os sites de saudação e serviços que gerenciam. O Azure Active Directory fornece esse recurso, permitindo-lhe toocustomize Olá aparência Olá entrar página com o logotipo da empresa e esquemas de cores personalizadas. Olá entrar é Olá página que aparece quando você entrar no tooOffice 365 ou outros aplicativos baseados na web que estão usando o AD do Azure como seu provedor de identidade. Você interage com essa página tooenter suas credenciais.

Se você quiser tooshow a marca da empresa, cores e outros elementos personalizáveis nesta página, consulte Olá diferença de saudação toounderstand imagens entre duas experiências de saudação a seguir.

Olá seguinte captura de tela mostra e exemplo de hello Office 365 na página de entrada em um computador desktop **antes de** uma personalização:

![Página de entrada do Office 365 antes da personalização](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

Olá seguinte captura de tela mostra e exemplo de hello Office 365 na página de entrada em um computador desktop **depois** uma personalização:

![Página de entrada do Office 365 após a personalização](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>Personalizando a página de entrada hello
Normalmente, se você precisar de acesso baseado em navegador tooyour nuvem aplicativos e serviços que sua empresa assina, você usa página de entrada hello.

Se você aplicou alterações tooyour na página de entrada, pode levar a hora de tooan para Olá alterações tooappear.

Uma página de entrada com marca só aparece quando você visita um serviço com uma URL específica do locatário, como https://outlook.com/**contoso**.com ou https://mail.**contoso**.com.

Quando você visita um serviço com URLs específicas sem locatário (por exemplo, https://mail.office365.com), uma página de entrada sem marca é exibida. Nesse caso, sua identidade visual aparecerá assim que você inserir sua ID de usuário ou que tiver selecionado um bloco de usuário.

> [!NOTE]
> * O nome do domínio deve aparecer como "Ativo" no hello **domínios** Olá a parte do portal do Azure no qual você configurou a identidade visual. Para obter mais informações, confira [Adicionar nomes de domínio personalizados](active-directory-domains-add-azure-portal.md).
> * Identidade visual da página de entrada não reporta o sinal do consumidor toohello na página do Microsoft. Se você entrar com uma conta da Microsoft, você pode ver a lista marcada de blocos do usuário renderizados pelo AD do Azure, mas Olá identidade visual da sua organização não se aplica toohello página de logon da conta de Microsoft.
>
>

Na página entrar, Olá **Mantenha-me conectado** caixa de seleção permite que um tooremain do usuário conectado ao fechar e reabrir o navegador.

   ![Mantenha-me conectado](./media/active-directory-branding-custom-signon-azure-portal/01.png)

Ela não afeta o tempo de vida da sessão. Você pode ocultar Olá a caixa de seleção na página de entrada do Active Directory do Azure de saudação.
Se a caixa de seleção de saudação é exibida depende de configuração de saudação do **Mantenha-me conectado desabilitado**.

   ![Mantenha-me conectado](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide Olá caixa de seleção, defina essa configuração muito**Sim**.

> [!NOTE]
> Alguns recursos do SharePoint Online e o Office 2010 dependem usuários sendo capaz de toocheck nesta caixa. Se você configurar toohidden essa configuração, os usuários podem ver prompts adicionais e inesperados em toosign.
>
>

**diretório de tooyour identidade visual da empresa de tooadd:**

1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.

   ![Abrir o gerenciamento de usuários](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Em Olá **usuários e grupos** folha, selecione **identidade visual da empresa**.
4. Em Olá **usuários e grupos - identidade visual da empresa** folha, selecione Olá **editar** comando.

    ![Editar identidade visual personalizada](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Modificar Olá elementos você deseja toocustomize. Todos os elementos são opcionais.
6. Clique em **Salvar**.

Pode demorar até tooan horas para que as alterações feitas toohello entrar tooappear identidade visual da página.

## <a name="next-steps"></a>Próximas etapas
[Adicionar identidade visual da empresa específica a um idioma](active-directory-branding-localize-azure-portal.md)
