---
title: "diretório de saudação aaaManage para sua assinatura do Office 365 no Azure | Microsoft Docs"
description: "Gerenciar um diretório de assinatura do Office 365 usando o Active Directory do Azure e hello portal clássico do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>Gerenciar o diretório de saudação para sua assinatura do Office 365 no Azure
Este artigo descreve como toomanage um diretório que foi criado para uma assinatura do Office 365, usando Olá portal clássico do Azure. Você deve ser Olá administrador de serviço ou um coadministrador de uma toosign de assinatura do Azure em toohello portal clássico do Azure. Se ainda não tiver uma assinatura do Azure, você poderá se inscrever em uma [avaliação gratuita de 30 dias](https://azure.microsoft.com/trial/get-started-active-directory/) hoje mesmo e implantar sua primeira solução de nuvem em menos de cinco minutos, usando este link. Se toouse Olá trabalho ou escola conta que você use toosign em tooOffice 365.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.

Depois de concluir Olá assinatura do Azure, você pode entrar no toohello portal clássico do Azure e acessar serviços do Azure. Clique em extensão do Active Directory Olá toomanage Olá mesmo diretório que autentica os usuários do Office 365.

Se você já tiver uma assinatura do Azure, Olá processo toomanage um diretório adicional também será simples. Por exemplo, Carlos Lima pode ter uma assinatura do Office 365 para Contoso.com. Ele também tem uma assinatura do Azure na qual se inscreveu usando sua conta da Microsoft, msmith@hotmail.com. Nesse caso, ele gerencia dois diretórios.

| Assinatura | Office 365 | As tabelas |
| --- | --- | --- |
|   Nome de exibição |Contoso |Diretório padrão do Azure AD (Azure Active Directory) |
|   Nome de domínio |contoso.com |msmithhotmail.onmicrosoft.com |

Ele quer que identidades de usuário Olá toomanage no diretório do Contoso Olá enquanto está inscrito no tooAzure usando sua conta da Microsoft, para que ele pode habilitar os recursos do Azure AD como autenticação multifator. Olá diagrama a seguir pode ajudar a processo de saudação tooillustrate.

![Diagrama toomanage dois diretórios independentes](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

Nesse caso, os dois diretórios de saudação são independentes um do outro.

## <a name="toomanage-two-independent-directories"></a>toomanage dois diretórios de independentes
Em ordem de Michael Smith toomanage ambos os diretórios enquanto está inscrito no tooAzure como msmith@hotmail.com, ele deve concluir Olá etapas a seguir:

> [!NOTE]
> Essas etapas só podem ser realizadas quando o usuário está conectado com uma conta da Microsoft. Se o usuário Olá entrar com uma conta corporativa ou escolar, Olá opção muito**usar diretório existente** não está disponível. Uma conta corporativa ou escolar pode ser autenticada apenas por seu diretório base (ou seja, Olá diretório onde hello conta corporativa ou escolar é armazenada e negócios hello ou na escola possui).
>
>

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) como msmith@hotmail.com.
2. Clique em **Novo** > **Serviços de Aplicativos** > **Active Directory** > **Diretório** > **Criação Personalizada**.
3. Clique em usar existentes de diretório e selecione Olá **estou pronto toobe sair agora** caixa de seleção.
4. Entrar toohello portal clássico do Azure como administrador global do Contoso.onmicrosoft.com (por exemplo, msmith@contoso.com).
5. Quando solicitado muito**diretório de Contoso Olá uso com o Azure?**, clique em **continuar**.
6. Clique em **Sair agora**.
7. Entrar toohello portal clássico do Azure como msmith@hotmail.com. diretório de Contoso hello e saudação padrão aparecem no hello extensão do Active Directory.

Depois de concluir essas etapas, msmith@hotmail.com é um administrador global no diretório do Contoso hello.

## <a name="tooadminister-resources-as-hello-global-admin"></a>recursos de tooadminister como Olá administrador global
Agora vamos supor que Jane Doe precise administrar sites e recursos de banco de dados que estão associados Olá assinatura do Azure para msmith@hotmail.com. Antes que ela pode fazer isso, Michael Smith precisa toocomplete estas etapas adicionais:

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) usando a conta de administrador de serviço Olá para Olá assinatura do Azure (neste exemplo, msmith@hotmail.com).
2. Olá assinatura toohello Contoso diretório de transferência: clique em **configurações** > **assinaturas** > selecione assinatura hello > **Editar diretório** > selecione **Contoso (Contoso.com)**. Como parte da transferência hello, qualquer trabalho ou escola contas que são administradores de assinatura de saudação são removidas.
3. Adicionar Jane Doe como coadministrador da assinatura Olá: clique em **configurações** > **administradores** > selecione assinatura hello > **adicionar** > tipo **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a relação Olá entre assinaturas e diretórios, consulte [como uma assinatura está associada um diretório](active-directory-how-subscriptions-associated-directory.md).
