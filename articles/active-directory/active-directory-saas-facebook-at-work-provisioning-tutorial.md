---
title: "Tutorial: configurar o Workplace by Facebook para provisionamento de usuário | Microsoft Docs"
description: "Saiba como contas de usuário de provisionar e provisionar eliminação de tooautomatically do AD do Azure tooWorkplace pelo Facebook."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a>Tutorial: configurar o Workplace by Facebook para provisionamento de usuário

Este tutorial mostra Olá tooautomatically necessárias etapas provisionar e desprovisionar contas de usuário do Azure Active Directory (AD do Azure) tooWorkplace pelo Facebook.

## <a name="prerequisites"></a>Pré-requisitos

tooconfigure integração do AD do Azure com o local de trabalho pelo Facebook, você precisa seguir hello:

- Uma assinatura do AD do Azure
- Uma assinatura do Workplace by Facebook habilitada para SSO (logon único)

etapas de saudação tootest neste tutorial, siga estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma [oferta de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assign-users-tooworkplace-by-facebook"></a>Atribuir usuários tooWorkplace pelo Facebook

O AD do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, são sincronizados apenas Olá usuários e grupos que receberam tooan aplicativo no AD do Azure.

Antes de decidir Configurando e habilitando o Olá provisionamento de serviço, quais usuários e grupos no AD do Azure representam usuários de saudação que precisam acessar tooyour no local de trabalho pelo aplicativo do Facebook. Você pode atribuir essas tooyour de usuários local de trabalho pelo aplicativo do Facebook seguindo Olá instruções [atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

>[!IMPORTANT]
>*   Saudação de teste, configuração de provisionamento, atribuindo um único tooWorkplace de usuário do AD do Azure pelo Facebook. Atribua usuários e grupos adicionais mais tarde.
>*   Quando você atribui um tooWorkplace usuário pelo Facebook, você deve selecionar uma função de usuário válido. função de acesso padrão de saudação não funciona para o provisionamento.

## <a name="enable-automated-user-provisioning"></a>Habilitar o provisionamento automatizado de usuários

Esta seção orienta você por meio de conectar sua conta de usuário do AD do Azure toohello provisionamento API do local de trabalho pelo Facebook. Você também aprenderá como tooconfigure Olá provisionamento serviço toocreate, atualizar e desativar contas de usuário atribuído no local de trabalho pelo Facebook. Isso se baseia na atribuição de usuários e grupos no Azure AD.

>[!Tip]
>Você também pode escolher tooenabled SSO baseado em SAML para o local de trabalho pelo Facebook, por seguindo as instruções de saudação fornecidas no hello [portal do Azure](https://portal.azure.com). O SSO pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>Configurar a conta de usuário provisionamento tooWorkplace pelo Facebook no AD do Azure

Azure AD oferece suporte a saudação capacidade tooautomatically sincronizar detalhes da conta de saudação atribuído tooWorkplace usuários pelo Facebook. A sincronização automática habilita o local de trabalho por precisa tooauthorize usuários para acessar, antes dos dados do Facebook tooget Olá-los de tentativa de toosign em para Olá primeira vez. Ele também desprovisiona os usuários do Workplace by Facebook quando o acesso tiver sido revogado no Azure AD.

1. Em Olá [portal do Azure](https://portal.azure.com), selecione **Active Directory do Azure** > **aplicativos corporativos** > **todos os aplicativos**.

2. Se você já tiver configurado o local de trabalho pelo Facebook para SSO, procure sua instância do local de trabalho pelo Facebook usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **no local de trabalho pelo Facebook** na Galeria de aplicativo hello. Selecione **no local de trabalho pelo Facebook** de saudação resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

3. Selecione sua instância do local de trabalho pelo Facebook e, em seguida, selecione Olá **provisionamento** guia.

4. Definir **modo de provisionamento** muito**automática**. 

    ![Captura de tela das opções de provisionamento do Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** seção, digite Olá **segredo do Token** e hello **URL do locatário** do local de trabalho pelo administrador do Facebook.

6. No portal do Azure de Olá, selecione **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour no local de trabalho pelo aplicativo do Facebook. Se conexão Olá falhar, certifique-se de que o seu local de trabalho por conta do Facebook tem permissões de administrador de equipe.

7. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e marque a caixa de seleção de saudação.

8. Selecione **Salvar**.

9. Em Olá mapeamentos, selecione **tooWorkplace sincronizar do Azure Active Directory Users pelo Facebook**.

10. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooWorkplace pelo Facebook. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usada na área de trabalho pelo Facebook para operações de atualização. Selecione de todas as alterações, toocommit **salvar**.

11. tooenable Olá serviço de provisionamento do Azure AD para o local de trabalho pelo Facebook, no hello **configurações** seção, altere Olá **Status de provisionamento** muito**em**.

12. Selecione **Salvar**.

Para obter mais informações sobre como tooconfigure automático de provisionamento, consulte [Olá Facebook documentação](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).

Agora você pode criar uma conta de teste. Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooWorkplace pelo Facebook.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para aplicativos empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-facebook-at-work-tutorial.md)

