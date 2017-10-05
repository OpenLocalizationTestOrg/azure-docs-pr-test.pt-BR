---
title: "Adicionar a identidade visual da empresa específica a um idioma à sua página de conexão no Azure Active Directory | Microsoft Docs"
description: "Saiba como adicionar imagens e texto de identidade visual da empresa específicos do idioma a uma página de entrada do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a>Adicionar identidade visual específica a um idioma à sua página de conexão no Azure Active Directory
Para evitar confusão, muitas empresas desejam aplicar uma aparência consistente em todos os sites e serviços que elas gerenciam. O Azure Active Directory fornece esse recurso, permitindo que você personalize a aparência da página de entrada com esquemas de cores e o logotipo da empresa. A página de entrada é a página que aparece quando você entra no Office 365 ou em outros aplicativos baseados na Web que estejam usando o Azure AD como provedor de identidade. Você interage com essa página para inserir suas credenciais.

## <a name="customizing-the-sign-in-page-for-another-language"></a>Personalizando a página de entrada para outro idioma
Você pode adicionar elementos específicos do idioma à sua página de entrada somente se já tiver criado uma página de entrada personalizada, conforme descrito em [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md)(Adicionar a identidade visual da empresa à página de entrada). Você pode configurar uma página de entrada por diretório com um conjunto padrão de elementos personalizáveis. Depois de ter configurado o conjunto padrão de elementos de página, é possível configurar mais versões para diferentes localidades. Você também pode misturar e combinar vários elementos. Por exemplo, você pode:

* Criar uma **Imagem de página de entrada** padrão que funcione para todas as culturas e depois criar versões específicas para o inglês e o francês. Quando você define seus navegadores para um desses dois idiomas, é exibida a imagem específica do idioma, enquanto a ilustração padrão é exibida para todos os outros idiomas.
* Configure logotipos diferentes para sua organização (por exemplo, versões em japonês ou hebraico).

É recomendável manter o número de variações de linguagem baixo, por motivos de desempenho e manutenção.

**Para adicionar identidade visual da empresa ao diretório:**

1. Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.
2. Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.

   ![Abrir o gerenciamento de usuários](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Na folha **Usuários e grupos**, selecione **Identidade visual da empresa**.
4. Na folha **Usuários e grupos - identidade visual da empresa**, selecione o comando **Adicionar idioma**.

    ![Adicionar elementos de identidade visual específicos do idioma](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Modifique os elementos que você deseja personalizar. Todos os elementos são opcionais.
6. Clique em **Salvar**.

Pode demorar até uma hora para que apareçam todas as alterações feitas à identidade visual da página de entrada.

## <a name="next-steps"></a>Próximas etapas
[Adicionar identidade visual da empresa à página de entrada](active-directory-branding-custom-signon-azure-portal.md)
