---
title: "Active Directory perguntas Frequentes dos relatórios de aaaAzure | Microsoft Docs"
description: "Perguntas frequentes sobre relatórios do Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a>Perguntas frequentes sobre relatórios do Azure Active Directory

Este artigo inclui respostas toofrequently perguntas frequentes (FAQs) sobre os relatórios do Active Directory do Azure.  
Para obter mais detalhes, veja [Relatórios do Azure Active Directory](active-directory-reporting-azure-portal.md). 

**P: o que é a retenção de dados Olá para logs de atividade (e entradas de auditoria) Olá portal do Azure?** 

**R:** fornecemos sete dias de dados para nossos clientes livres e alternando tooan 1 do Azure AD Premium ou licença Premium 2, você pode acessar os dados de backup too30 dias. Para obter mais detalhes sobre a retenção, consulte [Políticas de retenção de relatório do Azure Active Directory](active-directory-reporting-retention.md)

--- 

**P: quanto tempo leva até podem ver dados de atividade de saudação depois que concluir minha tarefa?**

**R:** logs de atividade de auditoria tem uma latência de 15 minutos tooan horas. Logs de atividade de entrada tem uma latência de 15 minutos para a maioria dos registros e backup too2 horas para alguns registros.

---

**P: é necessário toobe que uma atividade de saudação do administrador global toosee fizer logon Olá Portal do Azure ou tooget dados por meio de saudação API?**

**R:** Não. Você pode ser um **segurança leitor**, um **Admin de segurança** ou um **Administrador Global** toosee dados no Portal do Azure ou acessá-lo por meio da API de saudação do relatório.

---

**P: posso obter informações de log de atividade do Office 365 por meio de saudação portal do Azure?**

**R:** apesar de atividade do Office 365 e o compartilhamento de logs de atividade do AD do Azure muitos recursos de diretório hello, se você quiser que uma exibição completa de Olá logs de atividade do Office 365, você deve se as informações do log de atividade do Office 365 toohello Centro de administração do Office 365 tooget.

---


**P: qual pelas APIs uso tooget informações sobre os logs de atividade do Office 365?**

**R:** Use Olá APIs de gerenciamento do Office 365 tooaccess Olá [logs de atividade do Office 365 por meio de uma API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).

---

**P: Quantos registros posso baixar do Portal do Azure?**

**R:** você pode baixar os registros de too120K de saudação portal do Azure. Olá registros são classificados por *mais recente* e por padrão, você obter registros Olá K de 120 mais recente. 

---

**P: o número de registros pode consultar por meio de atividades de saudação API?**

**R:** consultar too1 milhões de registros (se você não usar o operador top hello, que classifica registro Olá por mais recente). Se você usar o operador de "top" Olá, você pode consultar os registros too500K. Você pode encontrar exemplos de consultas em como toouse Olá API aqui [aqui](active-directory-reporting-api-getting-started.md).

---

**P: Como obtenho uma licença premium?**

**R:** consulte [guia de Introdução ao Azure Active Directory Premium](active-directory-get-started-premium.md) para uma pergunta de toothis de resposta.

---

**P: Em quanto tempo deverei ver dados de atividades depois de obter uma licença premium?**

**R:** se você já tiver dados de atividades como uma licença gratuita, você pode ver Olá os mesmos dados. Se você não tiver nenhum dado, isso levará um ou dois dias.

---

**P: Eu vejo dados do último mês depois de obter uma licença premium do Azure AD?**

**R:** se você recentemente alternou versão Premium de tooa (incluindo uma versão de avaliação), você pode ver os dados too7 dias inicialmente. Quando se acumulando, você verá too30 dias.

---

**P: há um evento de risco na proteção de identidade, mas não vejo entrada correspondente no hello todas as entradas. Isso é esperado?**

**R:** Sim, o Identity Protection avalia o risco de todos os fluxos de autenticação, sejam eles interativos ou não. No entanto, todos os relatórios somente de logons mostra somente Olá logons interativos.

---

**P: como baixar o relatório de "Usuários sinalizados riscos" hello no portal do Azure?**

**R:** toodownload de opção Olá *usuários sinalizados riscos* relatório será adicionado em breve.

---

**P: como saber por que um logon ou um usuário foi sinalizado arriscados em Olá portal do Azure?**

**R:** clientes de edição Premium podem aprender mais sobre Olá subjacente eventos de risco clicando no usuário hello "Usuários sinalizados riscos" ou clicando no hello "Arriscadas entradas". Os clientes da edição gratuita e Basic obtém usuários em risco de saudação toosee e entradas sem Olá subjacente informações de evento de risco.

---

**P: como os endereços IP são calculados em Olá entradas e o relatório de entradas arriscado?**

**R:** endereços IP são emitidos de forma que não há nenhuma conexão definitiva entre um endereço IP e em que o computador Olá com o endereço estiver localizado fisicamente. Isso é complicado devido a fatores como provedores móveis e VPNs emitir endereços IP de pools centrais geralmente muito distantes de onde o dispositivo de cliente de saudação é realmente usado. Considerando Olá acima, converter o local físico de tooa de endereço IP é um melhor esforço com base em rastreamentos, dados de registro, pesquisa inversa no-break e outras informações. 

---
