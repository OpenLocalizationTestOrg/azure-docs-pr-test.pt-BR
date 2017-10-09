---
title: "Tutorial: Integração do Azure Active Directory com o Workplace by Facebook| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o local de trabalho pelo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Tutorial: configurar o Workplace by Facebook para o provisionamento de usuário

Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no local de trabalho pelo Facebook e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooWorkplace pelo Facebook.

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o local de trabalho pelo Facebook, você precisa Olá itens a seguir:

- Uma assinatura do AD do Azure
- Uma assinatura do Workplace by Facebook habilitada para logon único

> [!NOTE]
> Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.

tootest Olá etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-tooworkplace-by-facebook"></a>Atribuir usuários tooWorkplace pelo Facebook

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooyour no local de trabalho pelo aplicativo do Facebook. Depois de decidir, você pode atribuir essas tooyour de usuários local de trabalho pelo aplicativo do Facebook, seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>Dicas importantes para atribuir usuários tooWorkplace pelo Facebook

*   É recomendável que um único usuário do AD do Azure é atribuído tooWorkplace pelo Facebook tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir tooWorkplace um usuário pelo Facebook, você deve selecionar uma função de usuário válido. função de "Acesso padrão" Hello não funciona para o provisionamento.

## <a name="enable-user-provisioning"></a>Habilitar o provisionamento de usuário

Esta seção orienta você conectar seu AD do Azure tooWorkplace pela API de provisionamento de conta de usuário do Facebook e configurando Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no local de trabalho pelo Facebook com base no usuário e grupo atribuição no AD do Azure.

>[!Tip]
>Você também pode escolher tooenabled baseado no SAML SSO para o local de trabalho pelo Facebook, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>conta de usuário tooconfigure provisionamento tooWorkplace pelo Facebook no AD do Azure:

Olá o objetivo desta seção é toooutline como tooenable provisionamento de usuário do Active Directory contas tooWorkplace pelo Facebook.

Azure AD oferece suporte a saudação capacidade tooautomatically sincronizar detalhes da conta de saudação atribuído tooWorkplace usuários pelo Facebook. A sincronização automática habilita o local de trabalho por precisa tooauthorize usuários para acessar, antes dos dados do Facebook tooget Olá-los de tentativa de toosign em para Olá primeira vez. Ele também desprovisiona os usuários do Workplace by Facebook quando o acesso tiver sido revogado no Azure AD.

1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure** > **aplicativos corporativos** > **detodososaplicativos** seção.

2. Se você já tiver configurado o local de trabalho pelo Facebook para logon único, procure sua instância do local de trabalho pelo Facebook usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **no local de trabalho pelo Facebook** na Galeria de aplicativo hello. Selecione o local de trabalho pelo Facebook Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

3. Selecione sua instância do local de trabalho pelo Facebook e selecione Olá **provisionamento** guia.

4. Saudação de conjunto **modo de provisionamento** muito**automática**. 

    ![provisionamento](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** seção, digite Olá segredo do Token e Olá URL do locatário da área de trabalho pelo administrador do Facebook.

6. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour no local de trabalho pelo aplicativo do Facebook. Se a conexão de saudação falhar, certifique-se de que seu local de trabalho por conta do Facebook tem permissões de administrador de equipe.

7. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.

8. Clique em **Salvar.**

9. Em Olá mapeamentos, selecione **tooWorkplace sincronizar do Azure Active Directory Users pelo Facebook.**

10. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooWorkplace pelo Facebook. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usada na área de trabalho pelo Facebook para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

11. tooenable Olá serviço de provisionamento do AD do Azure para o local de trabalho pelo Facebook, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção

12. Clique em **Salvar.**

Para obter mais informações sobre como tooconfigure automático de provisionamento, consulte [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

Agora você pode criar uma conta de teste. Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooWorkplace pelo Facebook.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-workplacebyfacebook-tutorial.md)

