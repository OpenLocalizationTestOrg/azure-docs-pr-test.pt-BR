---
title: "aaaPublish aplicativos tooindividual os usuários em uma coleção do RemoteApp do Azure (visualização) | Microsoft Docs"
description: "Saiba como você pode publicar os usuários tooindividual de aplicativos, em vez de dependendo grupos no Azure RemoteApp."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>Publicar aplicativos tooindividual os usuários em uma coleção do RemoteApp do Azure (visualização)
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Este artigo explica como toopublish aplicativos tooindividual os usuários em uma coleção do RemoteApp do Azure. Isso é uma nova funcionalidade no Azure RemoteApp, atualmente na visualização privada e pioneiros disponível tooselect apenas para fins de avaliação.

Originalmente o Azure RemoteApp habilitado apenas uma maneira de publicação de aplicativos: administrador Olá seria publicar aplicativos de imagem de saudação e estariam visíveis tooall usuários na coleção de saudação.

Um cenário comum é tooinclude muitos aplicativos em uma única imagem e implantar uma coleção em custos de gerenciamento de tooreduce de ordem. Muitas vezes, nem todos os aplicativos são usuários relevantes tooall – os administradores prefere toopublish usuários de tooindividual de aplicativos para que eles não verão os aplicativos desnecessários em seus aplicativos de feed.

Isso já é possível no Azure RemoteApp, atualmente como um recurso de visualização limitada. Aqui está um resumo da nova funcionalidade de saudação:

1. Uma coleção pode ser definida em um destes dois modos:
   
   * Olá original modo de coleta onde todos os usuários em uma coleção podem ver todos os aplicativos publicados. Este é o modo de padrão de saudação.
   * novo modo de aplicativo Hello, onde os usuários veem somente os aplicativos que foram explicitamente atribuídas toothem
2. No momento de saudação o modo de aplicativo hello só pode ser habilitado usando cmdlets do PowerShell do Azure RemoteApp.
   
   * Ao definir o modo de tooapplication, atribuição de usuário na coleção de saudação não pode ser gerenciado por meio de Olá portal do Azure. Atribuição do usuário tem toobe gerenciada por meio de cmdlets do PowerShell.
3. Os usuários verão apenas aplicativos Olá publicados diretamente toothem. No entanto, talvez ainda seja possível para um usuário toolaunch Olá outros aplicativos disponíveis na imagem de saudação acessando-los diretamente no sistema operacional de saudação.
   
   * Este recurso não fornece um bloqueio seguro de aplicativos; ela apenas limita a visibilidade no aplicativo hello feed.
   * Se você precisar tooisolate usuários de aplicativos, você precisará coleções separadas toouse para fazer isso.

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>Como tooget cmdlets do PowerShell do Azure RemoteApp
tootry Olá nova visualização funcionalidade, você precisará toouse cmdlets do PowerShell do Azure. No momento não é toouse possíveis Olá Azure Management portal tooenable Olá nova publicação modo de aplicativo.

Primeiro, verifique se você tem Olá [módulo Azure PowerShell](/powershell/azure/overview) instalado.

Em seguida, inicie o console do PowerShell Olá no modo de administrador e execute hello cmdlet a seguir:

        Add-AzureAccount

Ele solicitará seu nome de usuário e senha do Azure. Depois de conectado, será capaz de toorun cmdlets do Azure RemoteApp em relação a suas assinaturas do Azure.

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>Como toocheck modo no qual uma coleção está em
Execute Olá cmdlet a seguir:

        Get-AzureRemoteAppCollection <collectionName>

![Verificar o modo de coleta de saudação](./media/remoteapp-perapp/araacllelvel.png)

Olá AclLevel propriedade pode ter Olá valores a seguir:

* Coleta: Olá publicação modo original. Todos os usuários veem todos os aplicativos publicados.
* Aplicativo: Olá nova publicação modo. Os usuários veem somente Olá aplicativos publicados diretamente toothem.

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>Como o modo de publicação de tooapplication tooswitch
Execute Olá cmdlet a seguir:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

Estado de publicação de aplicativo será preservado: inicialmente todos os usuários verão todos os aplicativos publicados original de saudação.

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>Como os usuários toolist quem podem ver um aplicativo específico
Execute Olá cmdlet a seguir:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Lista todos os usuários que podem ver o aplicativo hello.

Observação: Você pode ver aliases de aplicativo hello (chamados "alias do aplicativo" na sintaxe de saudação acima) executando Get-AzureRemoteAppProgram - CollectionName <collectionName>.

## <a name="how-tooassign-an-application-tooa-user"></a>Como tooassign um usuário do aplicativo tooa
Execute Olá cmdlet a seguir:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

usuário Hello agora verá saudação do aplicativo no cliente do Azure RemoteApp hello e será capaz de tooconnect tooit.

## <a name="how-tooremove-an-application-from-a-user"></a>Como tooremove um aplicativo de um usuário
Execute Olá cmdlet a seguir:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Como fornecer comentários
Agradecemos seus comentários e sugestões sobre este recurso de visualização. Por favor, preencha Olá [pesquisa](http://www.instant.ly/s/FDdrb) toolet no que você acha.

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>Ainda não teve um recurso de visualização chance tootry Olá?
Se você não participou de visualização Olá ainda, use isso [pesquisa](http://www.instant.ly/s/AY83p) toorequest acesso.

