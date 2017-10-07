---
title: "relatórios de atividade de aaaFind em Olá portal do Azure | Microsoft Docs"
description: "Saiba como os relatórios de toofind atividade do Active Directory do Azure no hello portal do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>Localizar relatórios de atividade no hello portal do Azure

Se você estiver movendo de saudação toohello de portal clássico do Azure portal do Azure, você obtém uma nova aparência em logs de atividades do Azure Active Directory (AD do Azure). Em uma recente [postagem de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), explicaremos como você pode ver os logs de atividades no contexto de saudação do recurso Olá você está trabalhando em Olá portal do Azure. Neste artigo, descreveremos como toofind relatórios que você usou no portal clássico do Azure no portal do Azure de saudação do hello.

## <a name="whats-new"></a>Novidades

Relatórios no portal clássico do Azure de saudação são separados em categorias:

1.  Relatórios de segurança
2.  Relatórios de atividades
3.  Relatórios de aplicativo integrados

### <a name="activity-and-integrated-app-reports"></a>Relatórios do aplicativo integrado e de atividade

Para o contexto de acordo com relatórios no hello portal do Azure, os relatórios existentes são mesclados em uma única exibição. Uma única API subjacente fornece Olá dados toohello exibição.

toosee essa exibição em Olá **Active Directory do Azure** folha, em **atividade**, selecione **logs de auditoria**.

![Logs de auditoria](./media/active-directory-reporting-migration/482.png "Logs de auditoria")

Olá relatórios a seguir é consolidado nesta exibição:

-   Relatório de auditoria
-   Atividade de redefinição de senha
-   Atividade de registro de redefinição de senha
-   Atividade dos grupos de autoatendimento
-   Alterações de nome do grupo do Office365
-   Atividade de provisionamento de conta
-   Status de substituição de senha
-   Erros de provisionamento de conta


Olá relatório de uso do aplicativo foi aprimorada e está incluído no hello **entradas** exibição. toosee essa exibição em Olá **Active Directory do Azure** folha, em **atividade**, selecione **entradas**.

![Exibição de entradas](./media/active-directory-reporting-migration/483.png "Exibição de entradas")

Olá **entradas** exibição inclui todas as entradas do usuário. Você pode usar essas informações de uso de aplicativo de tooget informações. Você também pode exibir informações de uso do aplicativo no hello **aplicativos empresariais** visão geral, em Olá **gerenciar** seção.

![Aplicativos empresariais](./media/active-directory-reporting-migration/484.png "Aplicativos empresariais")

## <a name="access-a-specific-report"></a>Acessar uma porta específica

Embora Olá portal do Azure oferece uma única exibição, você também pode examinar relatórios específicos.

### <a name="audit-logs"></a>Logs de auditoria

Comentários de toocustomer de resposta, no Olá portal do Azure, você pode usar avançada filtragem tooaccess Olá de dados desejado. É um filtro que você pode usar um *categoria de atividade*, que lista os tipos diferentes de saudação da atividade de logs no AD do Azure. toonarrow resulta toowhat que você está procurando, você pode selecionar uma categoria.

Por exemplo, se você estiver interessado apenas em redefinições de senha de serviço tooself relacionados de atividades, você pode escolher Olá **gerenciamento de senha de autoatendimento** categoria. categorias de saudação que você ver se baseiam em recursos Olá que você está trabalhando no.  

![Opções de categoria na página de Logs de auditoria de filtro Olá](./media/active-directory-reporting-migration/06.png "opções de categoria na página de Logs de auditoria de filtro de saudação")

As categorias de atividades incluem:

- Diretório principal
- Gerenciamento de senhas de auto-atendimento
- Gerenciamento de grupos de autoatendimento
- Provisionamento de conta de usuário

### <a name="application-usage"></a>Uso do aplicativo

tooview detalhes sobre o uso do aplicativo para todos os aplicativos ou para um único aplicativo, em **atividade**, selecione **entradas**. resultados de saudação toonarrow, você pode filtrar no nome de usuário ou nome do aplicativo.

![Página Filtrar Eventos de Entrada](./media/active-directory-reporting-migration/07.png "Página Filtrar Eventos de Entrada")

### <a name="security-reports"></a>Relatórios de segurança

#### <a name="azure-ad-anomalous-activity-reports"></a>Relatórios de atividades anômalas do Azure AD

Segurança de atividade anormal do AD do Azure relatórios de saudação portal clássico do Azure foram consolidado tooprovide você com um modo de exibição central. Essa exibição mostra todos os eventos de risco relacionado à segurança que o Azure AD pode detectar e relatar.

Olá a tabela a seguir lista os relatórios de segurança de atividade anormal de saudação do AD do Azure e tipos de eventos de risco correspondentes no hello portal do Azure.

| Relatório de atividades anômalas do Azure AD |  Tipo de evento de risco do Identity Protection|
| :--- | :--- |
| Usuários com credenciais vazadas | Credenciais vazadas |
| Atividades de entrada irregulares | Viagem impossível tooatypical locais |
| Entradas de dispositivos possivelmente infectados | Entradas de dispositivos infectados|
| Entradas de fontes desconhecidas | Entradas de endereços IP anônimos |
| Entradas de endereços IP com atividade suspeita | Entradas de endereços IP com atividade suspeita |
| - | Entradas de locais desconhecidos |

Olá, segurança de atividade anormal do AD do Azure a seguir relata não são incluídos como eventos de risco em Olá portal do Azure:

* Entradas após várias falhas
* Entradas de várias geografias

Esses relatórios ainda estão disponíveis no portal clássico do Azure de hello, mas eles serão substituídos em algum momento futuro de saudação.

Para saber mais, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).  


#### <a name="detected-risk-events"></a>Eventos de risco detectados

No hello portal do Azure, você pode acessar relatórios sobre eventos de risco detectados em Olá **Active Directory do Azure** folha, em **segurança**. Eventos de risco detectados são rastreados em Olá relatórios a seguir:   

- Usuários em risco
- Entradas de risco

![Relatórios de segurança](./media/active-directory-reporting-migration/04.png "Relatórios de segurança")

Para saber mais sobre relatórios de segurança, veja:

- [Usuários no relatório de riscos de segurança no portal do Azure Active Directory Olá](active-directory-reporting-security-user-at-risk.md)
- [Relatório de entradas arriscado no portal do Azure Active Directory Olá](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>Relatórios de atividade no hello portal clássico do Azure versus Olá portal do Azure

tabela Olá nesta seção lista os relatórios existentes em Olá portal clássico do Azure. Ele também descreve como você pode obter Olá as mesmas informações no hello portal do Azure.

tooview todos os dados na saudação de auditoria **Active Directory do Azure** folha, em **atividade**, ir muito**logs de auditoria**.

![Logs de auditoria](./media/active-directory-reporting-migration/61.png "Logs de auditoria")

| portal clássico do Azure                 | toofind em Olá portal do Azure                                                         |
| ---                                  | ---                                                                        |
| Logs de auditoria                           | Para **Categoria da Atividade**, selecione **Diretório Principal**.                       |
| Atividade de redefinição de senha              | Para **Categoria da Atividade**, selecione **Gerenciamento de Senhas de Autoatendimento**. |
| Atividade de registro de redefinição de senha | Para **Categoria da Atividade**, selecione **Gerenciamento de Senhas de Autoatendimento**.     |
| Atividade dos grupos de autoatendimento         | Para **Categoria da Atividade**, selecione **Gerenciamento de Grupos de Autoatendimento**.        |
| Atividade de provisionamento de conta        | Para **Categoria da Atividade**, selecione **Provisionamento do Usuário da Conta**.         |
| Status de substituição de senha             | Para **Categoria da Atividade**, selecione **Substituição Automática de Senha do Aplicativo**.      |
| Erros de provisionamento de conta          | Para **Categoria da Atividade**, selecione **Provisionamento do Usuário da Conta**.        |
| Alterações de nome do grupo do Office365         | Para **Categoria da Atividade**, selecione **Gerenciamento de Senhas de Autoatendimento**. Para **Tipo de Recurso de Atividade**, selecione **Grupo**. Para **Origem da Atividade**, selecione **Grupos do O365**.|

Olá tooview **uso do aplicativo** relatório, no hello **Active Directory do Azure** folha, em **gerenciar**, selecione **aplicativos empresariais**e, em seguida, selecione **entradas**.


![Relatório de Entradas de aplicativos empresariais](./media/active-directory-reporting-migration/199.png "Relatório de Entradas de aplicativos empresariais")

## <a name="next-steps"></a>Próximas etapas

Para obter uma visão geral de emissão de relatórios, consulte Olá [reporting do Active Directory do Azure](active-directory-reporting-azure-portal.md).
