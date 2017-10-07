---
title: "de aaaHow tooremove um usuário acessar o aplicativo tooan | Microsoft Docs"
description: "Entender como tooremove um usuário acessar o aplicativo tooan"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 17017bddb73aad5a0ef3a411ac91bf0423f0b600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooremove-a-users-access-tooan-application"></a>Como tooremove um usuário acessar o aplicativo tooan

Este artigo ajuda você toounderstand como tooremove um usuário acessar o aplicativo tooan.

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Desejo tooremove aplicativos de tooan de atribuição de um usuário específico ou do grupo

tooremove um usuário ou grupo atribuição tooan aplicativo, execute as etapas de saudação listadas no hello [remover uma atribuição de usuário ou grupo de um aplicativo de empresa no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artigo.

. # # desejo toodisable todos os aplicativos de tooan de acesso para cada usuário

toodisable todos os usuário entradas tooan de aplicativos, siga etapas de saudação listadas Olá [desabilitar entradas do usuário para um aplicativo de empresa no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artigo.

## <a name="i-want-toodelete-an-application-entirely"></a>Desejo toodelete um aplicativo totalmente

muito**excluir um aplicativo**, siga as instruções de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja toodelete.

7.  Depois que o aplicativo hello carrega, clique em **excluir** ícone do aplicativo de superior hello **visão geral** folha.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Desejo toodisable todos os aplicativos do usuário futuras consentimento operações tooany

Desabilitando o consentimento do usuário para seu diretório de todo a impedir que usuários finais de consentimento tooany aplicativo. Os administradores ainda podem consentir em nome dos usuários. toolearn mais sobre o aplicativo de consentimento e por que você pode ou não poderá toodo, leitura [usuário conhecimento e consentimento do administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

muito**desabilitar todas as operações de consentimento do usuário futuras em seu diretório inteiro**, siga as instruções de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Configurações de usuário**.

6.  Desabilitar todas as operações de consentimento do usuário futuro por configuração Olá **usuários podem permitir que aplicativos tooaccess seus dados** alternar muito**não** e clique em Olá **salvar** botão.


# <a name="next-steps"></a>Próximas etapas
[Gerenciando acesso tooapps](active-directory-managing-access-to-apps.md)
