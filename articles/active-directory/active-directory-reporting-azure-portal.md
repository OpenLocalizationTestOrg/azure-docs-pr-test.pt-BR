---
title: "relatório de Active Directory aaaAzure | Microsoft Docs"
description: "Fornece uma visão geral sobre a emissão de relatórios do Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Relatórios do Azure Active Directory

Com os relatórios do Azure Active Directory, você pode ter uma ideia de como o seu ambiente está funcionando.  
dados saudação fornecido permite que você:

- Determinar como os aplicativos e serviços estão sendo utilizados pelos usuários
- Detectar possíveis riscos que afetam a integridade de saudação do seu ambiente
- Solucionar problemas que impedem a conclusão dos trabalhos pelos usuários  

arquitetura de relatórios Olá se baseia em dois pilares principais:

- Relatórios de segurança
- Relatórios de atividades

![Relatórios](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>Relatórios de segurança

Olá relatórios de segurança no Active Directory do Azure ajudam você tooprotect identidades da organização.  
Há dois tipos de relatórios de segurança no Azure Active Directory:

- **Usuários sinalizados riscos** - da saudação [usuários sinalizados para relatório de risco de segurança](active-directory-reporting-security-user-at-risk.md), obter uma visão geral das contas de usuário que possa ter sido comprometido.

- **Entradas arriscadas** - com hello [relatório de segurança de entrada arriscados](active-directory-reporting-security-risky-sign-ins.md), obterá um indicador para tentativas de logon que podem ter sido realizadas por alguém que é não Olá legítimo proprietário de uma conta de usuário. 

**Qual licença do AD do Azure precisa de um relatório de segurança de tooaccess?**  
Todas as edições do Azure Active Directory fornecem relatórios de usuários sinalizados como risco e de entradas de risco.  
No entanto, o nível de saudação de granularidade do relatório varia entre as edições hello: 

- Em Olá **edições do Azure Active Directory gratuito e Basic**, você já obter uma lista de usuários sinalizados para riscos e entradas arriscadas. 

- Olá **do Azure Active Directory Premium 1** edição estende esse modelo, permitindo que você também tooexamine alguns Olá subjacente eventos de risco que foram detectados para cada relatório. 

- Olá **do Azure Active Directory Premium 2** edition fornece com hello mais informações detalhadas sobre Olá subjacente eventos de risco e ele também permite políticas de segurança tooconfigure respondem automaticamente tooconfigured níveis de risco.


## <a name="activity-reports"></a>Relatórios de atividades

Há dois tipos de relatórios de atividade no Azure Active Directory:

- **Logs de auditoria** - Olá [relatório de atividade de logs de auditoria](active-directory-reporting-activity-audit-logs.md) fornece toohello acesse o histórico de todas as tarefas executadas em seu locatário.

- **Entradas** - com hello [relatório de atividade de entradas](active-directory-reporting-activity-sign-ins.md), você pode determinar, quem executou tarefas Olá relatadas pelo relatório de logs de auditoria de saudação.



Olá **relatório dos logs de auditoria** fornece registros de atividades de sistema para fins de conformidade.
Entre outros, Olá fornecidos dados permite que você tooaddress os cenários comuns, como:

- Alguém em meu locatário tem o grupo de administradores de tooan de acesso. Quem deu o acesso? 

- Desejo tooknow lista de saudação de usuários de assinatura em um aplicativo específico desde recentemente incorporada Olá aplicativo e deseja tooknow se ela está bem

- Desejo tooknow senha quantas redefinições estão ocorrendo em meu locatário


**Qual licença do AD do Azure precisa de relatório de logs de auditoria do tooaccess Olá?**  
relatório de logs de auditoria de saudação está disponível para os recursos para os quais você possui licenças. Se você tiver uma licença para um recurso específico, você também tem acesso toohello informações de log para ele de auditoria.

Para obter mais detalhes, consulte **compara recursos disponíveis de edições de gratuito, Basic e Premium Olá** na [recursos do Active Directory do Azure](https://www.microsoft.com/cloud-platform/azure-active-directory-features).   



Olá **relatório de atividade de entradas** tootoofind habilita responde tooquestions como:

- O que é Olá entrar padrão de um usuário?
- Quantos usuários entraram em uma semana?
- Qual é o status de saudação destas entradas?


**Qual licença do AD do Azure é que você precisa tooaccess Olá relatório de atividade de entradas?**  
tooaccess Olá relatório de atividade de entradas, seu locatário deve ter uma licença Azure AD Premium associada a ele.


## <a name="programmatic-access"></a>Acesso Programático

Na interface do usuário toohello adição, relatórios do Active Directory do Azure também fornece a você [acesso programático](active-directory-reporting-api-getting-started-azure-portal.md) toohello dados de relatório. dados Olá desses relatórios podem ser muito útil tooyour aplicativos, como sistemas SIEM, auditoria e ferramentas de business intelligence. Olá AD do Azure reporting que APIs fornecem dados de toohello acesso programático por meio de um conjunto de APIs com base em REST. Você pode chamar essas APIs de várias ferramentas e linguagens de programação. 


## <a name="next-steps"></a>Próximas etapas

Se você quiser tooknow mais sobre Olá vários tipos de relatório no Azure Active Directory, consulte:

- [Usuários sinalizados como risco](active-directory-reporting-security-user-at-risk.md)
- [Relatório de entradas de risco](active-directory-reporting-security-risky-sign-ins.md)
- [Relatório de trilhas de auditoria](active-directory-reporting-activity-audit-logs.md)
- [Relatório de logs de entrada](active-directory-reporting-activity-sign-ins.md)

Se você quiser tooknow mais sobre como acessar Olá Olá usando Olá API de relatórios de dados de relatórios, consulte: 

- [Guia de Introdução ao Olá do Active Directory do Azure API de relatório](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png