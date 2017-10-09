---
title: "relatório de entradas de aaaRisky no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Saiba mais sobre o relatório de entradas arriscados Olá no portal do Azure Active Directory Olá"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Relatório de entradas arriscados no portal do Azure Active Directory Olá

Com os relatórios de segurança Olá no Azure Active Directory (AD do Azure), você pode obter ideias sobre a probabilidade de saudação de contas de usuário comprometidas em seu ambiente. 

O AD do Azure detecta suspeitas ações que são relacionadas tooyour contas de usuário. Para cada ação detectada, um registro chamado *evento de risco* é criado. Para obter mais detalhes, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Olá detectados eventos de risco são toocalculate usado:

- **Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário. Para obter mais detalhes, veja [Entradas arriscadas](active-directory-identityprotection.md#risky-sign-ins). 

- **Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida. Para obter mais detalhes, veja [Usuários sinalizados para riscos](active-directory-identityprotection.md#users-flagged-for-risk).  

Em [Olá portal do Azure](https://portal.azure.com), você pode encontrar relata segurança Olá Olá **Active Directory do Azure** folha em Olá **segurança** seção. 

![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Qual licença do AD do Azure precisa de um relatório de segurança de tooaccess?  

Todas as edições do Azure Active Directory fornecem relatórios de entradas de risco.  
No entanto, o nível de saudação de granularidade do relatório varia entre as edições hello: 

- Em Olá **edições do Azure Active Directory gratuito e Basic**, você já obter uma lista de entradas arriscadas. 

- Olá **do Azure Active Directory Premium 1** edição estende esse modelo, permitindo que você também tooexamine alguns Olá subjacente eventos de risco que foram detectados para cada relatório. 

- Olá **do Azure Active Directory Premium 2** edition fornece com hello mais informações detalhadas sobre todos os eventos de risco subjacente e também permite políticas de segurança tooconfigure respondem automaticamente tooconfigured níveis de risco.



## <a name="azure-active-directory-free-and-basic-edition"></a>Edições gratuita e básica do Azure Active Directory

Hello Azure Active Directory gratuito e edições basic fornecem uma lista de entradas arriscadas que foram detectados para os usuários. O relatório lista:

- **Usuário** - Olá nome de usuário de saudação que foi usado durante a operação de entrada hello
- **IP** -Olá o endereço IP do dispositivo de saudação que foi usado tooconnect tooAzure do Active Directory
- **Local** -local Olá usado tooconnect tooAzure do Active Directory
- **Hora da entrada em** -tempo de saudação quando entrar Olá foi executado
- **Status** -Olá status de entrada hello


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/01.png)

Com base em sua investigação de entrada arriscados hello, você pode fornecer comentários tooAzure do Active Directory na forma de saudação ações a seguir:

- Resolver
- Marcar como falso positivo
- Ignorar
- Reativar

![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Para obter mais detalhes, veja [Fechando eventos de risco manualmente](active-directory-identityprotection.md#closing-risk-events-manually).

Esse relatório fornece uma opção para:

- Recursos de pesquisa
- Baixar dados de relatório de saudação


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Edições premium do Azure Active Directory

relatório de entradas arriscados Olá em edições de premium Olá Active Directory do Azure oferece:

- Informações sobre Olá agregadas [tipos de eventos de risco](active-directory-identity-protection-risk-events.md) que foram detectadas

- Um relatório de saudação toodownload opção


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/456.png)


Ao selecionar um evento de risco, você obtém uma exibição detalhada do relatório deste evento de risco que habilita:

- Uma opção tooconfigure um [política de correção de risco do usuário](active-directory-identityprotection.md#user-risk-security-policy)  

- Examine Olá detecção da linha do tempo para eventos de risco Olá  

- O exame de uma lista de usuários para os quais esse evento de risco foi detectado

- Que você [feche manualmente eventos de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reative um evento de risco fechado manualmente. 


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/457.png)

Ao selecionar um usuário, você obtém uma exibição detalhada do relatório deste usuário, que lhe habilita a:

- Olá abrir, que exibir todas as entradas

- Redefinir senha do usuário Olá

- Descartar todos os eventos

- Investigue eventos de risco relatado para o usuário hello. 


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/324.png)


tooinvestigate um evento de risco, selecione um na lista de saudação.  
Isso abre o hello **detalhes** folha para esse evento de risco. Em hello **detalhes** folha, você tem Olá opção tooeither [Feche manualmente um evento de risco](active-directory-identityprotection.md#closing-risk-events-manually) ou reativar um evento de risco fechado manualmente. 


![Entradas de risco](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Próximas etapas

- Para saber mais sobre o Azure Active Directory Identity Protection, veja [Azure Active Directory Identity Protection](active-directory-identityprotection.md).

