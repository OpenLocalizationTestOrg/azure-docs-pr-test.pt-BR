---
title: "Sincronização do Azure AD Connect: alterar senha da conta Olá AD DS | Microsoft Docs"
description: "Este documento de tópico descreve como tooupdate do Azure AD Connect após a senha de saudação da conta de saudação AD DS é alterada."
services: active-directory
keywords: Conta do AD DS, conta do Active Directory, senha
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>Alterar a senha da conta Olá AD DS
conta do Hello AD DS refere-se a conta de usuário toohello usada pelo Azure AD Connect toocommunicate com o Active Directory no local. Se você alterar a senha Olá Olá conta AD DS, você deve atualizar o serviço de sincronização se conectar do Azure AD com hello nova senha. Caso contrário, Olá que sincronização não poderá sincronizar corretamente com hello Active Directory local e você encontrará Olá os erros a seguir:

* Em Olá operação do Gerenciador de serviço de sincronização, nenhuma importação ou exportação com local AD falha com **credenciais de início não** erro.

* No Visualizador de eventos do Windows, o log de eventos do aplicativo hello contém um erro com **evento ID 6000** e mensagem **'Agente de gerenciamento hello "contoso.com" com falha toorun porque as credenciais de saudação eram inválidas'** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>Como tooupdate Olá o serviço de sincronização com a nova senha para a conta do AD DS
Olá tooupdate serviço de sincronização com a nova senha hello:

1. Inicie Olá Synchronization Service Manager (serviço de sincronização inicial →).
</br>![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Vá toohello **conectores** guia.

3. Selecione Olá **conector AD** que corresponde a conta do toohello AD DS para que sua senha foi alterada.

4. Em **Ações**, selecione **Propriedades**.

5. Na caixa de diálogo pop-up hello, selecione **conectar-se a floresta do diretório tooActive**:

6. Insira Olá nova senha da conta de saudação AD DS no hello **senha** caixa de texto.

7. Clique em **Okey** toosave Olá nova senha e a caixa de diálogo pop-up Olá fechar.

8. Reinicialização hello Azure AD conectar serviço de sincronização no Gerenciador de controle de serviço do Windows. Isso é tooensure que qualquer senha antiga de toohello de referência é removida do cache de memória de saudação.

## <a name="next-steps"></a>Próximas etapas
**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)

* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
