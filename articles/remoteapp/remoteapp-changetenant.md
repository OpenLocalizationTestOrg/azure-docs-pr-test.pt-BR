---
title: "locatário do aaaChange hello Azure Active Directory no Azure RemoteApp | Microsoft Docs"
description: "Saiba como o locatário de Active Directory do Azure Olá toochange associado com o Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>Alterar o locatário do Active Directory do Azure Olá no Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O Azure RemoteApp usa o acesso do usuário tooallow do Azure Active Directory (AD do Azure). locatário Olá somente do AD do Azure que você pode usar no Azure RemoteApp é hello associado Olá assinatura do Azure. Você pode exibir a assinatura Olá associado no hello **configurações** página no portal de saudação. Examinar Olá **diretório** coluna Olá **assinaturas** guia.

> [!NOTE]
> Para essa alteração toosucceed, primeiro remova todos os usuários do locatário existente do Active Directory do Azure saudação de todas as coleções do RemoteApp do Azure. toodo isso, vá toohello Portal do Azure, vá toohello **Azure RemoteApp** guia e abra cada coleção do RemoteApp do Azure. Vá toohello **usuários** guia e remover usuários que pertencem a tooyour locatário de Active Directory do Azure atual. Repita para todas as coleções de RemoteApp do Azure existentes. Sem isso, não será capaz de toocreate ou coleções de patch.
> 
> 

Se você quiser toouse um locatário diferente, use essas etapas toochange Olá associada a sua assinatura:

1. No portal de hello, remova qualquer toowhich de usuários do AD do Azure você concedeu acesso tooAzure coleções do RemoteApp. (Consulte a observação de saudação acima para obter etapas sobre como toodo isso.)
2. Defina uma conta da Microsoft (anteriormente chamada de um Live ID) como administrador de serviço hello. (Não sabe se você já está Olá administrador de serviço? É possível descobrir isso clicando em **Configurações -> Administradores**.) Veja como você pode alterar isso:
   
   1. Clique em usuário Olá no canto superior direito da saudação e, em seguida, clique em **Exibir minha fatura**.
   2. Clique na assinatura de saudação. Em seguida, na página de novo hello, role para baixo e clique em **editar detalhes da assinatura** de saudação à direita. (Classificação de saudação metade inferior direita, se isso ajuda a encontrá-lo.)
   3. Tipo de conta da Microsoft hello para usuário Olá que deve ser o administrador de serviço hello.
3. Agora, saia do portal hello e entre novamente com hello conta da Microsoft especificada na etapa anterior hello.
4. Clique em **Novo -> Serviços de Aplicativos -> Active Directory -> Diretório -> Criação Personalizada**.
5. Em **Diretório**, escolha **Usar diretório existente**. Vamos toohave toosign fora do portal de saudação agora, preferir **estou pronto toobe sair agora**.
6. Entrar novamente no hello portal como um administrador global do diretório Olá deseja tooadd. (Se você ainda não era o administrador global, você será após uma rodada de entrada e saída).
7. Você será solicitado quando você entrar se você quiser toouse seu locatário do AD existente com sua assinatura. Clique em **Continuar** e em **Sair agora**.
8. Entrar novamente e voltar muito**Configurações -> assinaturas**. Selecione sua assinatura e clique em **Editar Diretório**. Selecione o locatário de saudação do AD do Azure que você deseja toouse.

Agora você pode usar o hello novo AD do Azure locatário toocontrol acesso toohello acesso de usuário de assinatura e tooconfigure do Azure no Azure RemoteApp.

