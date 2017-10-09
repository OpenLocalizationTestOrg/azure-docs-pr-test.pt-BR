---
title: "Tutorial: Integração do Azure Active Directory com o NetSuite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a>Tutorial: Configurando o Netsuite para o provisionamento automático de usuário

Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no Netsuite e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooNetsuite.

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory.
*   Uma assinatura habilitada para logon único do Netsuite.
*   Uma conta de usuário no Netsuite com permissões de Administrador de Equipe.

## <a name="assigning-users-toonetsuite"></a>Atribuir usuários tooNetsuite

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, são sincronizados apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure.

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour Netsuite aplicativo. Depois de decidir, você pode atribuir esses aplicativos de Netsuite tooyour usuários, seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a>Dicas importantes para atribuir usuários tooNetsuite

*   É recomendável que um único usuário do AD do Azure é atribuído tooNetsuite tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um usuário tooNetsuite, você deve selecionar uma função de usuário válido. função de "Acesso padrão" Hello não funciona para o provisionamento.

## <a name="enable-user-provisioning"></a>Habilitar o provisionamento de usuário

Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooNetsuite seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no Netsuite com base na atribuição de usuário e grupo no AD do Azure.

> [!TIP] 
> Você também pode escolher tooenabled baseado no SAML SSO para o Netsuite, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="tooconfigure-user-account-provisioning"></a>provisionamento de conta de usuário de tooconfigure:

Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooNetsuite.

1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

2. Se você já tiver configurado o Netsuite para logon único, procure sua instância do Netsuite usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **Netsuite** na Galeria de aplicativo hello. Selecione o Netsuite Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

3. Selecione sua instância do Netsuite, em seguida Olá **provisionamento** guia.

4. Saudação de conjunto **modo de provisionamento** muito**automática**. 

    ![provisionamento](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** seção, forneça Olá definições de configuração a seguir:
   
    a. Em Olá **nome de usuário administrador** caixa de texto, tipo de um Netsuite nome de conta que tem Olá **administrador do sistema** perfil no Netsuite.com atribuído.
   
    b. Em Olá **senha do administrador** caixa de texto, digite a senha Olá para esta conta.
      
6. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour Netsuite aplicativo.

7. Em Olá **Email de notificação** , digite o endereço de email de saudação de uma pessoa ou grupo que deve receber notificações de erros de provisionamento e marque caixa de seleção de saudação.

8. Clique em **Salvar.**

9. Em Olá mapeamentos, selecione **tooNetsuite sincronizar Azure usuários do Active Directory.**

10. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooNetsuite do AD do Azure. Observe que Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Netsuite para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

11. tooenable Olá serviço de provisionamento do AD do Azure para o Netsuite, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação

12. Clique em **Salvar.**

Ele inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooNetsuite em Olá usuários e a seção de grupos. Observe que a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo Netsuite.

Agora você pode criar uma conta de teste. Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooNetsuite.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-netsuite-tutorial.md)