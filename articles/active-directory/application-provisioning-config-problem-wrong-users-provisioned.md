---
title: "aaaWrong conjunto de usuários estão sendo provisionado tooan AD do Azure Galeria aplicativo | Microsoft Docs"
description: "Saiba como toofind limite por um conjunto diferente de usuários estão sendo provisionadas tooan aplicativo daqueles esperado"
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
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Conjunto de usuários errado estão sendo provisionado tooan AD do Azure Galeria aplicativo

Os usuários que são provisionados toohello aplicativo é orientada principalmente por quais usuários e grupos foram **atribuído** toohello aplicativo.

Usar recursos de saudação abaixo toolearn como toocheck quais usuários e grupos foram atribuído tooan aplicativo no Azure Active Directory.

## <a name="assign-a-user-directly-as-an-administrator"></a>Atribuir um usuário diretamente como administrador

tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.

7.  Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.

8.  Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.

9.  Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.

10. Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.

11. Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**. Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.

12. **Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.

13. Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.

14. **Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.

15. Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.

Se o provisionamento está configurado e já em execução para um aplicativo, novos usuários devem ser provisionados tooan aplicativo em aproximadamente 10 minutos. Verificar Olá **os Logs de auditoria** para obter detalhes.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Atribua um grupo diretamente tooan aplicativo como um administrador

tooassign um ou mais grupos de aplicativo tooan diretamente, siga Olá etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.

7.  Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.

8.  Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.

9.  Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.

10. Tipo de saudação **nome completo do grupo** do grupo de saudação que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.

11. Passe o mouse sobre Olá **grupo** em Olá lista tooreveal um **caixa de seleção**. Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello grupo seu usuário toohello **selecionados** lista.

12. **Opcional:** se você gostaria que muito**adicionar mais de um grupo**, tipo em outro **nome completo do grupo** em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa e clique em tooadd de caixa de seleção Olá esse grupo toohello **selecionados** lista.

13. Quando você terminar de selecionar os grupos, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.

14. **Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect toohello de tooassign uma função grupos selecionados.

15. Clique em Olá **atribuir** grupos selecionados do botão tooassign Olá aplicativo toohello.

Se o provisionamento está configurado e já em execução para um aplicativo, novos usuários contidos no grupo de saudação devem ser provisionado tooan aplicativo em aproximadamente 10 minutos. Verificar Olá **os Logs de auditoria** para obter detalhes.

>[!IMPORTANT]
>Provisionamento de Olá nome do grupo e grupo de detalhes, em membros de toohello de adição, se houver suporte para alguns aplicativos. Você pode habilitar ou desabilitar essa funcionalidade habilitando ou desabilitando Olá **mapeamento** para objetos de grupo mostrados no hello **provisionamento** guia. 
>
>

Se grupos de provisionamento está habilitado, certifique-se de que tooreview Olá atributo mapeamentos tooensure um campo apropriado está sendo usado para hello "correspondência de ID". Isso pode ser o nome de exibição de saudação ou email alias, como hello grupo e seus membros não ser provisionado se a propriedade correspondente hello está vazia ou não preenchidos para um grupo no AD do Azure.

## <a name="next-steps"></a>Próximas etapas
[Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos com o Active Directory do Azure](active-directory-saas-app-provisioning.md)
