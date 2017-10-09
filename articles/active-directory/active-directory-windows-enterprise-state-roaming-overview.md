---
title: "Visão geral de Roaming de estado aaaEnterprise | Microsoft Docs"
description: "Fornece informações sobre as configurações do Enterprise State Roaming em dispositivos do Windows. Roaming de estado da empresa fornece aos usuários uma experiência unificada em seus dispositivos Windows e reduz o tempo de saudação necessário para configurar um novo dispositivo."
services: active-directory
keywords: "o que é o Enterprise State Roaming, sincronização de empresa, nuvem do windows"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a>Visão geral do Enterprise State Roaming
Com o Windows 10, [do Azure Active Directory (AD do Azure)](active-directory-whatis.md) usuários ganho olá capacidade toosecurely sincronizar suas configurações de usuário e a nuvem de toohello de dados de configurações de aplicativo. Roaming de estado da empresa fornece aos usuários uma experiência unificada em seus dispositivos Windows e reduz o tempo de saudação necessário para configurar um novo dispositivo. Roaming de estado da empresa opera semelhante padrão de toohello [sincronização de configurações de consumidor](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) que foi introduzida no Windows 8. Além disso, o Enterprise State Roaming oferece:

* **Separação dos dados corporativos e do consumidor** – as organizações estão no controle de seus dados, e não há nenhuma combinação de dados corporativos em uma conta de nuvem do consumidor ou de dados do consumidor em uma conta de nuvem da empresa.
* **Segurança aprimorada** – dados são criptografados automaticamente antes de deixar o dispositivo com Windows 10 do usuário hello usando o Azure Rights Management (Azure RMS) e dados permanecem criptografados em repouso na nuvem hello. Todo o conteúdo permanece criptografado em repouso na nuvem hello, exceto Olá namespaces, como nomes de configurações e os nomes de aplicativo do Windows.  
* **Melhor monitoramento e gerenciamento** – fornece visibilidade e controle sobre as configurações em sua organização e em quais dispositivos por meio da integração de portal de saudação do AD do Azure que é sincronizado. 

O Enterprise State Roaming está disponível em várias regiões do Azure. Você pode encontrar hello atualizado lista de regiões disponíveis em Olá [serviços do Azure por região](https://azure.microsoft.com/regions/#services) página no Active Directory do Azure.

| Artigo | Descrição |
| --- | --- |
| [Habilitar o Enterprise State Roaming no Active Directory do Azure](active-directory-windows-enterprise-state-roaming-enable.md) |Roaming de estado da empresa está disponível tooany organização com uma assinatura Premium do Azure Active Directory (AD do Azure). Para obter mais detalhes sobre como tooget uma assinatura do AD do Azure, consulte Olá [produto do AD do Azure](https://azure.microsoft.com/services/active-directory) página. |
| [Perguntas frequentes sobre configurações e roaming de dados](active-directory-windows-enterprise-state-roaming-faqs.md) |Este tópico responde a algumas dúvidas que os administradores de TI podem ter sobre as configurações e a sincronização de dados do aplicativo. |
| [Política de grupo e as configurações do MDM para a sincronização de configurações](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |Windows 10 fornece sincronização de configurações do dispositivo móvel (MDM) gerenciamento política configurações toolimit e política de grupo. |
| [Referência de configurações de roaming do Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |a seguir Olá é uma lista completa de todas as configurações de saudação que será ser movidos e/ou backup no Windows 10. |
| [Solução de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |Este tópico aborda algumas etapas básicas para solução de problemas, além de conter uma lista de problemas conhecidos. |

