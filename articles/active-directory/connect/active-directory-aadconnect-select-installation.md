---
title: "Azure AD Connect: Selecionar o tipo de instalação | Microsoft Docs"
description: "Este tópico o orienta como instalação de saudação tooselect digite toouse para conexão do AD do Azure"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>Selecione quais toouse do tipo de instalação para o Azure AD Connect
O Azure AD Connect oferece dois tipos de instalação para uma nova instalação: Expressa e personalizado. Este tópico Ajuda toodecide qual opção toouse durante a instalação.

## <a name="express"></a>Express
Express é a opção mais comum de saudação e é usado por cerca de 90% de todas as novas instalações. Foi projetado tooprovide uma configuração que funciona para cenários mais comuns de cliente hello.

Ela pressupõe que:

- Você tem uma única floresta local do Active Directory.
- Você tem uma conta de administrador corporativo que você pode usar para a instalação de saudação.
- Há menos de 100.000 objetos em seu Active Directory local.

Você recebe:

- [Sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md) do local tooAzure AD para logon único.
- Uma configuração que sincroniza [usuários, grupos, contatos e computadores com Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).
- Sincronização de todos os objetos qualificados em todos os domínios e em todas as UOs.
- [A atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md) é habilitado toomake-se de que você sempre use a versão mais recente disponível de saudação.

Opções onde ainda é possível usar a Expressa:

- Se você não quiser toosynchronize todas as UOs, você ainda pode usar o Express e na última página de hello, desmarque **iniciar o processo de sincronização hello...** *. Em seguida, execute novamente o Assistente de instalação de saudação e alterar Olá OUs [opções de configuração](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) e habilitar a sincronização agendada.
- Você deseja tooenable um dos recursos de saudação do Azure AD Premium, como write-back de senha. Passam primeiro pelo tooget express saudação inicial a instalação foi concluída. Em seguida, execute novamente o Assistente de instalação hello e alterar Olá [opções de configuração](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).

## <a name="custom"></a>Personalizado
caminho personalizado Olá permite que muitos mais opções do express. Ele deve ser usado em todos os casos em que a configuração de saudação descrita na seção anterior para express não é representativa para sua organização.

Use quando:

- Você não tem a conta de administrador do acesso tooan enterprise no Active Directory.
- Você tem mais de uma floresta ou planejar toosynchronize mais de uma floresta em Olá futuras.
- Você tiver domínios na floresta não pode ser acessada do servidor de conectar hello.
- Planejar toouse federação ou autenticação de passagem de entrada do usuário.
- Você tem mais de 100.000 objetos e precisa toouse um completo do SQL Server.
- Planejar toouse a filtragem baseada em grupo e não apenas domínio ou filtragem baseada em unidade Organizacional.

## <a name="upgrade-from-dirsync"></a>Atualização do DirSync
Se você estiver usando o DirSync, siga etapas Olá [atualizar do DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade sua configuração existente. Há duas opções de atualização diferentes:

- Tooinstall atualização in-loco se conectar em Olá mesmo servidor.
- Paralelo implantação tooinstall conectar em um novo servidor, enquanto o servidor DirSync existente de saudação ainda está operacional.

## <a name="upgrade-from-azure-ad-sync"></a>Atualização do Azure AD Sync
Se você estiver usando sincronização do AD do Azure, você pode seguir Olá [mesmas etapas](active-directory-aadconnect-upgrade-previous-version.md) como quando você atualiza de uma conexão versão tooa mais recente. Há duas opções de atualização diferentes:

- Tooinstall atualização in-loco se conectar em Olá mesmo servidor.
- Migração de giro tooinstall conectar em um novo servidor ao servidor de sincronização do AD do Azure existente Olá ainda está operacional.

## <a name="migrate-from-fim2010-or-mim2016"></a>Migrar do FIM2010 ou MIM2016
Se atualmente você estiver usando o Forefront Identity Manager 2010 ou o Microsoft Identity Manager 2016 com hello conector AD do Azure, sua única opção é uma migração. Execute as etapas de saudação descritas em [movimento migração](active-directory-aadconnect-upgrade-previous-version.md#swing-migration). Nas etapas hello, substitua mencionar do Azure AD Sync FIM2010/MIM2016.

## <a name="next-steps"></a>Próximas etapas
Dependendo da opção de saudação selecionado toouse, use a tabela de saudação do toofind esquerdo toohello conteúdo seu artigo com hello etapas detalhadas.
