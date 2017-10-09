---
title: "configurações de política e MDM aaaGroup | Microsoft Docs"
description: "Fornece informações sobre as configurações de política de grupo e do MDM (gerenciamento de dispositivos móveis) que devem ser usadas em dispositivos corporativos. Essas políticas são aplicadas toohello todo dispositivo de usuário."
services: active-directory
keywords: "quais são as configurações da Política e do MDM para o Enterprise State Roaming, Enterprise State Roaming, nuvem do windows"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a>Configurações de Política de Grupo e do MDM
Use esses diretiva de grupo e as configurações de gerenciamento (MDM) do dispositivo móvel somente em dispositivos corporativos como essas políticas são aplicadas toohello todo dispositivo de usuário. Aplicando uma sincronização de configurações de toodisable da política MDM para um pessoal, dispositivos de propriedade do usuário serão afetar negativamente o uso de saudação do dispositivo. Além disso, outras contas de usuário no dispositivo Olá também serão afetadas pela política de saudação.

Empresas que desejam toomanage móvel para dispositivos pessoais de (não gerenciados) pode usar Olá tooenable portal do Azure ou desabilitar o roaming, em vez de usar a política de grupo ou o MDM.
Olá tabelas a seguir descreve as configurações de política de saudação disponíveis.

## <a name="mdm-settings"></a>Configurações do MDM
configurações de política MDM Olá aplicam tooboth Windows 10 e Windows 10 Mobile.  Há suporte do Windows Mobile 10 somente para roaming baseado em conta da Microsoft por meio da conta do OneDrive do usuário.  Consulte muito seção "Dispositivos e pontos de extremidade" para obter detalhes sobre quais dispositivos têm suporte do AD do Azure com base em sincronização.

| Nome | Descrição |
| --- | --- |
| Permitir Conexão da Conta da Microsoft |Permite que usuários tooauthenticate usando uma conta da Microsoft no dispositivo Olá |
| Permitir Sincronizar Configurações |Permite que os usuários tooroam Windows as configurações e dados de aplicativo. Desabilitar essa política desabilitará a sincronização, bem como os backups em dispositivos móveis |

## <a name="group-policy-settings"></a>Configurações de Política de Grupo
configurações de política de grupo Olá se aplicam a dispositivos tooWindows 10 tooan ingressado no domínio de Active Directory. tabela Olá também inclui configurações herdadas que seria exibido toomanage configurações de sincronização, mas que não funcionam para Enterprise estado móvel para Windows 10, que são observadas com 'não use' na descrição de saudação.

| Nome | Descrição |
| --- | --- |
| Contas: Bloquear Contas da Microsoft |Essa configuração de política impede que os usuários adicionem novas contas da Microsoft a este computador |
| Não sincronizar |Impede que os usuários tooroam Windows as configurações e dados de aplicativo |
| Não sincronizar personalização |Desabilita a sincronização do grupo de temas Olá |
| Não sincronizar configurações do navegador |Desabilita a sincronização de grupo do Internet Explorer Olá |
| Não sincronizar senhas |Desabilita a sincronização do grupo Senhas |
| Não sincronizar outras configurações do Windows |Desabilita a sincronização do grupo Outras configurações do Windows |
| Não sincronizar personalização da área de trabalho |Não use; não tem nenhum efeito |
| Não sincronizar em conexões limitadas |Desabilita o roaming em conexões limitadas, como o 3G do celular |
| Não sincronizar aplicativos |Não use; não tem nenhum efeito |
| Não sincronizar configurações do aplicativo |Desabilita o roaming de dados do aplicativo |
| Não sincronizar configurações iniciais |Não use; não tem nenhum efeito |

## <a name="related-topics"></a>Tópicos relacionados
* [Visão geral do Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Habilitar o enterprise state roaming no Active Directory do Azure](active-directory-windows-enterprise-state-roaming-enable.md)
* [Perguntas frequentes sobre configurações e roaming de dados](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Referência de configurações de roaming do Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Solução de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

