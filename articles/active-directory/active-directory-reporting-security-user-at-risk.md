---
title: "aaaUsers sinalizados para relatório de risco de segurança no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Saiba mais sobre Olá usuários sinalizados para relatório de risco de segurança no portal do Azure Active Directory Olá"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>Usuários sinalizados para relatório de risco de segurança no portal do Azure Active Directory Olá

Relatórios de segurança Olá no hello Azure Active Directory (AD do Azure), você pode obter ideias sobre a probabilidade de saudação de contas de usuário comprometidas em seu ambiente. 

Active Directory do Azure detecta suspeitas ações que são relacionadas tooyour contas de usuário. Para cada ação detectada, um registro chamado *evento de risco* é criado. Para saber mais, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Olá detectados eventos de risco são toocalculate usado:

- **Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário. Para obter mais informações, consulte [Entradas de risco](active-directory-identityprotection.md#risky-sign-ins). 

- **Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida. Para obter mais informações, consulte [Usuários sinalizados para risco](active-directory-identityprotection.md#users-flagged-for-risk).  

Olá portal do Azure, você pode encontrar relata segurança Olá Olá **Active Directory do Azure** folha em Olá **segurança** seção.  

![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Qual licença do AD do Azure precisa de um relatório de segurança de tooaccess?  

Todas as edições do Azure Active Directory fornecem relatórios de usuários sinalizados como risco.  
No entanto, o nível de saudação de granularidade do relatório varia entre as edições hello: 

- Em Olá **edições do Azure Active Directory gratuito e Basic**, você já obter uma lista de usuários sinalizados riscos. 

- Olá **do Azure Active Directory Premium 1** edição estende esse modelo, permitindo que você também tooexamine alguns Olá subjacente eventos de risco que foram detectados para cada relatório. 

- Olá **do Azure Active Directory Premium 2** edition oferece Olá informações mais detalhadas sobre todos os eventos de risco subjacente e permite que as políticas de segurança de tooconfigure respondem automaticamente tooconfigured risco níveis.



## <a name="azure-active-directory-free-and-basic-edition"></a>Edições gratuita e básica do Azure Active Directory

usuários Olá sinalizados para relatório de risco em edições de gratuita e basic do Active Directory do Azure Olá fornece uma lista de contas de usuário que podem ter sido comprometidas. 


![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/03.png)

Seleção de um usuário abre a folha de dados de usuário relacionado hello.
Para usuários que estão em risco, você pode revisar o histórico de entrada do usuário Olá e Redefinir senha hello, se necessário.

![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/46.png)


Essa caixa de diálogo fornece uma opção para:

- Baixar relatório Olá

- Pesquisar usuários

![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Edições premium do Azure Active Directory

usuários Olá sinalizados para relatório de risco em edições de premium Olá Active Directory do Azure oferece:

- Uma [lista de contas de usuário](active-directory-identityprotection.md#users-flagged-for-risk) que podem ter sido comprometidas 

- Informações sobre Olá agregadas [tipos de eventos de risco](active-directory-identity-protection-risk-events.md) que foram detectadas

- Um relatório de saudação toodownload opção

- Uma opção tooconfigure um [política de correção de risco do usuário](active-directory-identityprotection.md#user-risk-security-policy)  


![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/71.png)

Ao selecionar um usuário, você obtém uma exibição detalhada do relatório deste usuário, que lhe habilita a:

- Olá abrir, que exibir todas as entradas

- Redefinir senha do usuário Olá

- Descartar todos os eventos

- Investigue eventos de risco relatado para o usuário hello. 


![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate um evento de risco, selecione uma opção da saudação do hello lista tooopen **detalhes** folha para esse evento de risco. Em hello **detalhes** folha, você tem Olá opção tooeither [Feche manualmente um evento de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reativar um evento de risco fechado manualmente. 


![Entradas de risco](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>Próximas etapas

- Para saber mais sobre o Azure Active Directory Identity Protection, veja [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

