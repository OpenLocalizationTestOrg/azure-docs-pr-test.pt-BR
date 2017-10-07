---
title: "aaaAzure Active Directory PoC guia estratégico ingredientes | Microsoft Docs"
description: "Explorar e implementar rapidamente os cenários de Identidade e Gerenciamento de Acesso"
services: active-directory
keywords: azure active directory, cartilha, prova de conceito, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a>Ingredientes do guia estratégico de prova de conceito do Azure Active Directory 

## <a name="theme"></a>Tema
AD do Azure fornece soluções de identidade e acesso de várias áreas da empresa hello. Classificamos cenários Olá Olá áreas a seguir: 

* [Muitos aplicativos, uma identidade](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [Aumentar sua segurança](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [Dimensionar com autoatendimento](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

Definir um tema tooframe Olá PoC ajuda esforços de saudação toofocus que reflete os desejos com as metas de negócios, que são muitas vezes, os gatilhos de Olá de interesse de saudação em uma verificação de conceito em primeiro lugar de saudação. 

## <a name="environment"></a>Ambiente

É toodetermine importante detalhes de saudação do ambiente Olá onde você fornecerá Olá PoC. Idealmente, você pode criar após ele depois Olá que POC é concluída. ambiente de destino Olá é crucial, e você deve encontrar o equilíbrio correto de saudação entre tornar a ele como real possível e sobrecarga de saudação de restrições ou considerações adicionais. saudação de ambientes típicos para PoCs é:
* **Produção:** cenários Olá serão implementados em seu ambiente em tempo real e já implantado os serviços do Microsoft Cloud (produção AD, Office 365, solução SSO/locatário do AD do Azure). 
* **Ambiente UAT (Teste de Aceitação do Usuário)/de desenvolvimento:** você tem uma infraestrutura de teste (AD paralelo e eventualmente a solução SSO/locatário do Azure AD) que tem dados de teste que se assemelham à produção. Normalmente, o ambiente de teste Olá é compartilhado entre vários projetos na empresa hello.

A maioria dos cenários deste guia são aditivos por natureza. Como resultado, ele podem ser implantados em locatário de produção de hello sem afetar os usuários fora da saudação PoC. Ao longo deste documento, mencionaremos quais cenários teriam efeito em todo o locatário. Nesses casos, convém tooconsider um ambiente de não produção. 


## <a name="target-users"></a>Usuários de destino

É importante toodetermine Olá destino conjunto de usuários que usará cenários hello, especialmente quando o ambiente de saudação for produção ou teste. Olá categorias de usuários de destino para PoC são:
* **Os usuários do piloto:** funções de trabalho de usuários reais no ambiente de saudação que vai usar solução Olá com conta Olá usam para seu tooday dia
* **Usuários de teste:** criadas no ambiente de saudação de contas de teste 

A maioria dos cenários neste guia pode ser exercida por usuários piloto. Ao longo deste documento, mencionaremos considerações do usuário de destino, se necessário.


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]