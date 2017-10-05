---
title: "Tutorial: configurar o LinkedIn Elevate para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como configurar o Azure Active Directory para provisionar e desprovisionar automaticamente contas de usuário no LinkedIn Elevate."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 526666301aad1e5284c621024649d9cd52c92d18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-elevate-for-automatic-user-provisioning"></a>Tutorial: configurar o LinkedIn Elevate para provisionamento automático de usuário


O objetivo deste tutorial é mostrar as etapas que precisam ser executadas no LinkedIn Elevate e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o LinkedIn Elevate. 

## <a name="prerequisites"></a>Pré-requisitos

O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:

*   Um locatário do Azure Active Directory
*   Um locatário no LinkedIn Elevate 
*   Uma conta de administrador no LinkedIn Elevate com acesso ao Centro de Contas do LinkedIn

> [!NOTE]
> O Azure Active Directory integra-se com o LinkedIn Elevate usando o protocolo [SCIM](http://www.simplecloud.info/).

## <a name="assigning-users-to-linkedin-elevate"></a>Atribuir usuários ao LinkedIn Elevate

O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados. No contexto do provisionamento automático de conta de usuário, somente os usuários e grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados. 

Antes de configurar e habilitar o serviço de provisionamento, você precisará decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao LinkedIn Elevate. Depois de decidir, atribua esses usuários ao LinkedIn Elevate seguindo estas instruções:

[Atribuir um usuário ou um grupo a um aplicativo empresarial](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-elevate"></a>Dicas importantes para atribuir usuários ao LinkedIn Elevate

*   Recomendamos a atribuição de um único usuário do Azure AD ao LinkedIn Elevate para testar a configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um usuário ao LinkedIn Elevate, selecione a função **Usuário** na caixa de diálogo de atribuição. A função de "Acesso Padrão" não funciona para provisionamento.


## <a name="configuring-user-provisioning-to-linkedin-elevate"></a>Como configurar o provisionamento de usuários no LinkedIn Elevate

Esta seção orienta você pela conexão do Azure AD à API de provisionamento de conta de usuário do SCIM do LinkedIn Elevate e também pela configuração do serviço de provisionamento, a fim de criar, atualizar e desabilitar contas de usuário atribuídas no LinkedIn Elevate com base na atribuição de usuário e de grupo do Azure AD.

**Dica:** você também pode optar por habilitar o logon único baseado em SAML para o LinkedIn Elevate seguindo as instruções fornecidas no [Portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-elevate-in-azure-ad"></a>Para configurar o provisionamento de conta de usuário automático para o LinkedIn Elevate no Azure AD:


A primeira etapa é recuperar o token de acesso do LinkedIn. Se você for um administrador corporativo, você poderá provisionar um token de acesso automaticamente. No seu centro de contas, vá para **Configurações &gt; Configurações Globais** e abra o painel **Instalação do SCIM**.

> [!NOTE]
> Se você estiver acessando o centro de contas diretamente em vez de fazê-lo por meio de um link, você poderá alcançá-lo usando as etapas a seguir.

1)  Entre no Centro de Contas.

2)  Selecione **Administrador &gt; Configurações de Administrador**.

3)  Clique em **Integrações Avançadas** na barra lateral esquerda. Você será direcionado para o Centro de Contas.

4)  Clique em **+ Adicionar a nova configuração de SCIM** e siga o procedimento preenchendo cada campo.

> Quando a atribuição automática de licenças não está habilitada, isso significa que somente os dados de usuário estão sincronizados.

![Provisionamento do LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate1.PNG)

> Quando a atribuição automática de licenças estiver habilitada, você precisa anotar o tipo de licença e a instância do aplicativo. Licenças são atribuídas por ordem de chegada, até que todas as licenças tenham sido utilizadas.

![Provisionamento do LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate2.PNG)

5)  Clique em **Gerar token**. Você deve ver o token de acesso ser exibido sob o campo **Token de acesso**.

6)  Salve seu token de acesso para a área de transferência ou o computador antes de sair da página.

7) Em seguida, entre no [Portal do Azure](https://portal.azure.com) e navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.

8) Se você já tiver configurado o LinkedIn Elevate para logon único, pesquise por sua instância do LinkedIn Elevate usando o campo de pesquisa. Caso contrário, selecione **Adicionar** e pesquise por **LinkedIn Elevate** na galeria de aplicativos. Selecione o LinkedIn Elevate nos resultados da pesquisa e adicione-o à lista de aplicativos.

9)  Selecione sua instância do LinkedIn Elevate e selecione a guia **Provisionamento**.

10) Defina o **Modo de Provisionamento** como **Automático**.

![Provisionamento do LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate3.PNG)

11)  Preencha os campos a seguir em **Credenciais de Administrador**:

* Na **URL do Locatário**, digite https://api.linkedin.com.

* No campo **Segredo do Token**, insira o token de acesso gerado na etapa 1 e clique em **Testar Conexão**.

* Você verá uma notificação de êxito no lado do superior direito do seu Portal.

12) Insira o endereço de email de uma pessoa ou grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção abaixo.

13) Clique em **Salvar**. 

14) Na seção **Mapeamentos de Atributo**, examine os atributos de usuário e grupo que serão sincronizados do Azure AD para o LinkedIn Elevate. Observe que os atributos selecionados como propriedades **Correspondentes** serão usados para corresponder as contas de usuário e grupos no LinkedIn Elevate para operações de atualização. Selecione o botão Salvar para confirmar as alterações.

![Provisionamento do LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate4.PNG)

15) Para habilitar o serviço de provisionamento do Azure AD para o LinkedIn Elevate, altere o **Status de Provisionamento** para **Ativado** na seção **Configurações**

16) Clique em **Salvar**. 

Isso iniciará a sincronização inicial de todos os usuários e/ou grupos atribuídos ao LinkedIn Elevate na seção Usuários e Grupos. Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução. Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento em seu aplicativo LinkedIn Elevate.


## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
