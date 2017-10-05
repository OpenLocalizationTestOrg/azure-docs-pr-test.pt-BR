---
title: "Publicar aplicativos para usuários individuais em uma coleção do Azure RemoteApp (versão prévia) | Microsoft Docs"
description: "Saiba como pode publicar aplicativos para usuários individuais, em vez de depender de grupos no Azure RemoteApp."
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
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a>Publicar aplicativos para usuários individuais em uma coleção do Azure RemoteApp (Visualização)
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Este artigo explica como publicar aplicativos para usuários individuais em uma coleção do Azure RemoteApp. Essa é uma nova funcionalidade no Azure RemoteApp, atualmente em visualização particular, e está disponível somente para usuários pioneiros específicos para fins de avaliação.

Originalmente, o Azure RemoAppte habilitava apenas uma maneira de publicar aplicativos: o administrador publicava os aplicativos a partir da imagem e eles ficavam visíveis para todos os usuários na coleção.

Um cenário comum é incluir vários aplicativos em uma única imagem e implantar uma coleção para reduzir os custos de gerenciamento. Muitas vezes, nem todos os aplicativos são relevantes para todos os usuários. Os administradores preferem publicar aplicativos para usuários individuais, assim, eles não veem aplicativos desnecessários em seu feed de aplicativos.

Isso já é possível no Azure RemoteApp, atualmente como um recurso de visualização limitada. Veja um pequeno resumo sobre a nova funcionalidade:

1. Uma coleção pode ser definida em um destes dois modos:
   
   * o modo de coleção original, em que todos os usuários em uma coleção podem ver todos os aplicativos publicados. Esse é o modo padrão.
   * o novo modo de aplicativo, em que os usuários veem apenas os aplicativos que foram explicitamente atribuídos a eles
2. No momento, o modo de aplicativo só pode ser habilitado por meio de cmdlets do PowerShell do Azure RemoteApp.
   
   * Quando é definido como modo de aplicativo, a atribuição de usuário na coleção não pode ser gerenciada por meio do portal do Azure. A atribuição de usuário deve ser gerenciada por meio de cmdlets do PowerShell.
3. Os usuários verão apenas os aplicativos publicados diretamente para eles. No entanto, ainda é possível que um usuário inicie os outros aplicativos disponíveis na imagem, acessando-os diretamente no sistema operacional.
   
   * Esse recurso não fornece um bloqueio seguro de aplicativos. Ele apenas limita a visibilidade no feed de aplicativos.
   * Se precisar isolar usuários dos aplicativos, será preciso usar coleções separadas para isso.

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a>Como obter os cmdlets do PowerShell do Azure RemoteApp
Para experimentar a nova funcionalidade de visualização, você precisará usar os cmdlets do Azure PowerShell. No momento, não é possível usar o Portal de Gerenciamento do Azure para habilitar o novo modo de publicação de aplicativos.

Primeiro, verifique se você tem o [módulo Azure PowerShell](/powershell/azure/overview) instalado.

Em seguida, inicie o console do PowerShell no modo de administrador e execute este cmdlet:

        Add-AzureAccount

Ele solicitará seu nome de usuário e senha do Azure. Depois de conectado, você poderá executar os cmdlets do RemoteApp do Azure em suas assinaturas do Azure.

## <a name="how-to-check-which-mode-a-collection-is-in"></a>Como verificar o modo no qual uma coleção está
Execute o cmdlet a seguir:

        Get-AzureRemoteAppCollection <collectionName>

![Verificar o modo de coleção](./media/remoteapp-perapp/araacllelvel.png)

A propriedade AclLevel pode ter os seguintes valores:

* Coleção: o modo de publicação original. Todos os usuários veem todos os aplicativos publicados.
* Aplicativo: o novo modo de publicação. Os usuários veem apenas os aplicativos publicados diretamente para eles.

## <a name="how-to-switch-to-application-publishing-mode"></a>Como alternar para o modo de publicação de aplicativos
Execute o cmdlet a seguir:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

O estado de publicação do aplicativo será preservado: inicialmente, todos os usuários verão todos os aplicativos publicados originais.

## <a name="how-to-list-users-who-can-see-a-specific-application"></a>Como listar os usuários que podem ver um aplicativo específico
Execute o cmdlet a seguir:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Isso lista todos os usuários que podem ver o aplicativo.

Observação: você pode ver os aliases de aplicativos (chamados de "alias de aplicativos" na sintaxe acima) executando Get-AzureRemoteAppProgram - CollectionName <collectionName>.

## <a name="how-to-assign-an-application-to-a-user"></a>Como atribuir um aplicativo a um usuário
Execute o cmdlet a seguir:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

Agora, o usuário verá o aplicativo no cliente RemoteApp do Azure e poderá conectar-se a ele.

## <a name="how-to-remove-an-application-from-a-user"></a>Como remover um aplicativo de um usuário
Execute o cmdlet a seguir:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Como fornecer comentários
Agradecemos seus comentários e sugestões sobre este recurso de visualização. Preencha a [pesquisa](http://www.instant.ly/s/FDdrb) para nos informar sobre sua opinião.

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a>Ainda não teve a oportunidade de experimentar o recurso de visualização?
Se você ainda não participou da visualização, use esta [pesquisa](http://www.instant.ly/s/AY83p) para solicitar acesso.

