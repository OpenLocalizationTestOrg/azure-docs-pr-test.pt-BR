---
title: "aaaPreview Office 365 grupos de expiração no Active Directory do Azure | Microsoft Docs"
description: "Como os grupos de tooset a expiração para o Office 365 no Active Directory do Azure (visualização)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>Como configurar o vencimento de grupos do Office 365 (visualização)

Agora você pode gerenciar o ciclo de vida de saudação de grupos do Office 365, definindo a validade de todos os grupos Office 365 que você selecionar. Quando este expiração estiver definida, os proprietários desses grupos são frequentes toorenew seus grupos se eles ainda terão que grupos de saudação. Os grupos do Office 365 que não forem renovados, serão excluídos. Qualquer grupo que foi excluído do Office 365 pode ser restaurado dentro de 30 dias por proprietários do grupo de saudação ou administrador hello.  


> [!NOTE]
> Você pode definir o vencimento de grupos somente do Office 365.
>
> Atribuir um vencimento para grupos do O365 requer que uma licença Premium do Azure AD esteja atribuída para:
>   - administrador de saudação que configura as configurações de expiração de saudação do locatário Olá
>   - Todos os membros de grupos de saudação selecionados para esta configuração

## <a name="set-office-365-groups-expiration"></a>Como configurar o vencimento de grupos do Office 365

1. Olá abrir [Centro de administração do AD do Azure](https://aad.portal.azure.com) com uma conta que seja um administrador global no seu locatário do AD do Azure.

2. Abra o Azure AD e selecione **Usuários e grupos**.

3. Selecione **configurações de grupo** e, em seguida, selecione **validade** tooopen as configurações de expiração de saudação.
  
  ![Folha Vencimento](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. Em Olá **validade** folha, você pode:

  * Definir o tempo de vida de grupo Olá em dias. Você pode selecionar um dos Olá predefinição valores ou um valor personalizado (deve ser 31 dias ou mais). 
  * Especifique um endereço de email onde as notificações de expiração e renovação Olá devem ser enviadas quando um grupo não tem nenhum proprietário. 
  * Selecione quais grupos do Office 365 expirarão. Você pode habilitar a expiração para **todos os** grupos do Office 365, você pode selecionar entre grupos de saudação Office 365 ou selecionar **nenhum** para desabilitar a validade de todos os grupos.
  * Salve as configurações quando terminar selecionando **Salvar**.

Para obter instruções sobre como toodownload e instale Olá expiração de tooconfigure de módulo do Microsoft PowerShell para grupos do Office 365 por meio do PowerShell, consulte [Azure V2 PowerShell módulo do Active Directory - versão de visualização pública 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).

Notificações de email como esta são enviadas proprietários de grupo toohello Office 365 30 dias, 15 dias e tooexpiration anteriores de 1 dia do grupo de saudação.

![Notificação de email de vencimento](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

o proprietário do grupo Hello, em seguida, pode selecionar **renovar grupo** toorenew Olá grupo do Office 365, ou pode selecionar **vá toogroup** toosee membros de saudação e outros detalhes sobre Olá grupo.

Quando um grupo de expira, o grupo de saudação é excluído um dia após a data de expiração de saudação. Uma notificação por email, como este é enviada proprietários do grupo toohello Office 365 informando sobre expiração hello e exclusão subsequente de seus grupos do Office 365.

![Notificação de email de exclusão do grupo](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

Olá grupo pode ser restaurado selecionando **restauração grupo** ou usando cmdlets do PowerShell, conforme descrito em [restauração um Office 365 excluído o grupo no Active Directory do Azure] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-portal).
    
Se você estiver restaurando de grupo de saudação contiver documentos, sites do SharePoint ou outros objetos persistentes, pode levar até too24 horas toofully restauração Olá grupo e seu conteúdo.

> [!NOTE]
> * Ao implantar as configurações de expiração hello, pode haver alguns grupos que são mais antigos que a janela de expiração de saudação. Esses grupos não são ser imediatamente excluídos, mas são definir too30 dias até a expiração. email de notificação de renovação primeiro Olá é enviado dentro de um dia. Por exemplo, um grupo foi criado 400 dias atrás e intervalo de expiração de saudação é definido too180 dias. Quando você aplica as configurações de expiração, um grupo tem 30 dias antes de ser excluído, a menos que renova o proprietário de saudação.
> * Quando um grupo dinâmico é excluído e restaurado, ele é visto como um novo grupo e regra de toohello acordo populado novamente. Esse processo pode levar até too24 horas.

## <a name="next-steps"></a>Próximas etapas
Esses artigos fornecem mais informações sobre os grupos do Azure AD.

* [Consultar grupos existentes](active-directory-groups-view-azure-portal.md)
* [Gerenciar configurações de um grupo](active-directory-groups-settings-azure-portal.md)
* [Gerenciar membros de um grupo](active-directory-groups-members-azure-portal.md)
* [Gerenciar associações de um grupo](active-directory-groups-membership-azure-portal.md)
* [Gerenciar regras dinâmicas para usuários em um grupo](active-directory-groups-dynamic-membership-azure-portal.md)
