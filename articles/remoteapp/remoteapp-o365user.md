---
title: "aaaHow toouse Azure RemoteApp com contas de usuário do Office 365 | Microsoft Docs"
description: "Saiba como toouse Azure RemoteApp com minhas contas de usuário do Office 365"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>Como toouse Azure RemoteApp com contas de usuário do Office 365
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Se você tiver uma assinatura do Office 365 têm um Azure Active Directory que armazena os nomes de usuário e senhas usadas tooaccess serviços do Office 365. Por exemplo, quando os usuários ativem o Office 365 ProPlus eles autenticam contra toocheck do AD do Azure para licenças. A maioria dos clientes seriam como toouse Olá mesmo diretório com o Azure RemoteApp.

Se você estiver implantando o Azure RemoteApp, provavelmente estará usando uma assinatura do Azure que está associada a um Azure AD diferente. Em ordem toouse seu diretório do Office 365, você precisará Olá toomove assinatura do Azure no diretório.

Para obter informações sobre como os aplicativos cliente toodeploy Office 365, consulte [como toouse sua assinatura do Office 365 com o Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Fase 1: registrar sua assinatura gratuita do Azure Active Directory do Office 365
Se você estiver usando Olá portal clássico do Azure, use as etapas de saudação em [registrar sua assinatura gratuita do Active Directory do Azure](https://technet.microsoft.com/library/dn832618.aspx) tooget acesso administrativo tooyour AD do Azure por meio do Portal de gerenciamento de saudação. Como resultado de hello desse processo, você deve ser capaz de toolog em Olá portal do Azure e consulte seu diretório – neste momento você não verá mais porque hello assinatura completa do Azure que você está usando com o Azure RemoteApp está em um diretório diferente.

Lembre-se nome hello e a senha da conta de administrador Olá criados nesta etapa – será necessária na fase 2.

Se você estiver usando Olá portal do Azure, confira [como tooregister e ativar um gratuita do Azure Active Directory usando o portal do Office 365](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>Fase 2: Olá alteração AD do Azure associado à sua assinatura do Azure.
Vamos toochange sua assinatura do Azure do seu diretório no diretório do Office 365 hello, trabalhamos na fase 1.

Siga as instruções de saudação descritas em [locatário de Active Directory do Azure Olá alteração no Azure RemoteApp](remoteapp-changetenant.md). Preste atenção especial toohello etapas a seguir:

* Etapa 1: se você implantou o Azure RemoteApp (ARA) nesta assinatura, verifique se removeu todas as contas de usuário do Azure AD de todas as coleções ARA primeiro, antes de tentar qualquer outra coisa. Como alternativa, você pode considerar a exclusão de todas as coleções existentes.
* Etapa 2: Esta é uma etapa crítica. Você precisa toouse uma conta da Microsoft (por exemplo, @outlook.com) como um administrador de serviço na assinatura Olá; isso ocorre porque não é possível temos as contas de usuário de saudação existente do AD do Azure anexado toohello assinatura – se isso for feito, nós não será capaz de toomove-tooa AD do Azure diferente.
* Etapa &#4;: Ao adicionar um diretório existente, Olá sistema solicitará toosign com conta de administrador Olá para aquele diretório. Certifique-se de conta de administrador Olá toouse da fase 1.
* Etapa &#5;: Alterar o diretório pai de saudação do diretório do hello assinatura tooyour Office 365. resultado final de saudação deve ser que em Configurações -> assinaturas sua assinatura lista directory Olá Office 365. 
  ![Altere o diretório de pai de saudação de assinatura de saudação](./media/remoteapp-o365user/settings.png)

Neste momento, sua assinatura do Azure RemoteApp está associada com o Office 365 do Azure AD; Você pode usar contas de usuário do Office 365 existentes Olá com o Azure RemoteApp!

