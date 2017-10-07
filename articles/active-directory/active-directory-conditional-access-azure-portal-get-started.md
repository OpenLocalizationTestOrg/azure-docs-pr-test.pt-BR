---
title: aaaGet iniciado com acesso condicional no Active Directory do Azure | Microsoft Docs
description: "Teste o acesso condicional usando uma condição de local."
services: active-directory
keywords: "tooapps de acesso condicional, o acesso condicional com o AD do Azure, proteger o acesso toocompany recursos, políticas de acesso condicional"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>Introdução ao acesso condicional no Azure Active Directory

Acesso condicional é um recurso do Active Directory do Azure que permite que você toodefine condições sob as quais os usuários autorizados podem acessar seus aplicativos. 

Este tópico fornece instruções para testar um acesso condicional com base em uma condição de local em seu ambiente.  


## <a name="scenario-description"></a>Descrição do cenário

Um requisito comum em muitas organizações é tooonly exigir autenticação multifator para acesso tooapps que não é executada da intranet corporativa hello. Com o Azure Active Directory, você pode facilmente atingir essa meta, configurando uma política de acesso condicional com base no local. Este tópico fornece instruções detalhadas sobre como configurar uma política relacionada. Olá aproveita a política [IPs confiáveis](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish entre tentativas de acesso de saudação corporativa da intranet e todos os outros locais.


## <a name="prerequisites"></a>Pré-requisitos

Olá cenário descrito neste tópico pressupõe que você esteja familiarizado com os conceitos de saudação descritos em [acesso condicional do Active Directory do Azure](active-directory-conditional-access-azure-portal.md).

tootest neste cenário, você precisa:

- Criar um usuário de teste 

- Atribuir um usuário de teste do Azure AD Premium licença toohello

- Configurar um aplicativo gerenciado e atribuir seu tooit de usuário de teste

- Configurar IPs confiáveis

Se você precisar de mais detalhes sobre IPs confiáveis, veja [IPs confiáveis](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="policy-configuration-steps"></a>Etapas de configuração de política

**tooconfigure política de acesso condicional, execute:**

1. No hello portal do Azure, na barra de navegação esquerda hello, clique em **Active Directory do Azure**. 

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. Em Olá **Active Directory do Azure** folha em Olá **gerenciar** seção, clique em **acesso condicional**.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. Em Olá **acesso condicional** folha, Olá tooopen **novo** folha, na barra de ferramentas Olá superior hello, clique em **adicionar**.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. Em Olá **novo** folha em Olá **nome** caixa de texto, digite um nome para a política.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. Em Olá **atribuição** seção, clique em **usuários e grupos**.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. Em Olá **usuários e grupos** folha, executar Olá etapas a seguir:

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    a. Clique em **Selecionar usuários e grupos**.

    b. Clique em **Selecionar**.

    c. Em Olá **selecione** folha, selecione seu usuário de teste e, em seguida, clique em **selecione**.

    d. Em Olá **usuários e grupos** folha, clique em **feito**.

7. Em Olá **novo** folha, Olá tooopen **aplicativos de nuvem** folha em Olá **atribuição** seção, clique em **aplicativos de nuvem**.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. Em Olá **aplicativos de nuvem** folha, executar Olá etapas a seguir:

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    a. Clique em **Selecionar aplicativos**.

    b. Clique em **Selecionar**.

    c. Em Olá **selecione** folha, selecione o aplicativo de nuvem e, em seguida, clique em **selecione**.

    d. Em Olá **aplicativos de nuvem** folha, clique em **feito**.

9. Em Olá **novo** folha, Olá tooopen **condições** folha em Olá **atribuição** seção, clique em **condições**.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. Em Olá **condições** folha, Olá tooopen **locais** folha, clique em **locais**.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. Em Olá **locais** folha, executar Olá etapas a seguir:

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    a. Em **Configurar**, clique em **Sim**.

    b. Em **Incluir**, clique em **Todos os locais**.

    c. Clique em **Excluir** e clique em **Todos os IPs confiáveis**.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    d. Clique em **Concluído**.

12. Em Olá **condições** folha, clique em **feito**.

13. Em Olá **novo** folha, Olá tooopen **Grant** folha em Olá **controles** seção, clique em **Grant**.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. Em Olá **Grant** folha, executar Olá etapas a seguir:

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    a. Selecione **Exigir autenticação multifator**.

    b. Clique em **Selecionar**.

15. Em Olá **novo** folha, em **habilitar política**, clique em **em**.

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. Em Olá **novo** folha, clique em **criar**.


## <a name="testing-hello-policy"></a>Política de teste Olá

tootest sua política, você deve acessar o aplicativo de um dispositivo que: 

1. Tenha um endereço IP que esteja dentro de seus IPs Confiáveis configurados 

1. Tenha um endereço IP que não esteja dentro de seus IPs Confiáveis configurados

A autenticação multifator só será necessária durante uma tentativa de conexão feita de um dispositivo que não esteja dentro dos seus IPs Confiáveis configurados. 


## <a name="next-steps"></a>Próximas etapas

Se você quiser toolearn mais sobre o acesso condicional, consulte [acesso condicional do Active Directory do Azure](active-directory-conditional-access-azure-portal.md).

