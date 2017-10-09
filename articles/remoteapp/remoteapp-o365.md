---
title: aaaUsing Office com o Azure RemoteApp | Microsoft Docs
description: Saiba como o Office e o RemoteApp do Azure funcionam juntos
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Usando o Office com o RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Você tem duas opções para hospedar aplicativos do Office no RemoteApp do Azure: Office 365 ProPlus ou Office 2013 Professional Plus Trial.

**Ei, você sabia que temos um artigo mais novo e melhor que logo substituirá este? Check-out [como toouse sua assinatura do Office 365 com o Azure RemoteApp](remoteapp-officesubscription.md). Ele abrange todas as informações de saudação que é necessário para usar o Office 365 + Azure RemoteApp.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
Você pode criar uma coleção do RemoteApp usando a imagem de modelo Office 365 ProPlus hello. Essa opção permite que você tooextend sua tooRemoteApp de serviço do Office 365. Você deve ter um plano de assinatura existente e os usuários devem ser licenciados para Olá serviço Office 365 ProPlus, de modo autônomo ou por meio de planos de serviço Olá Office 365.

O RemoteApp dá suporte à ativação de computador compartilhado do Office 365. Quando você habilitar a ativação de computador compartilhado e usar Olá [ferramenta de implantação do Office](http://www.microsoft.com/download/details.aspx?id=36778) para instalação, Office 365 ProPlus instalados sem ser ativado. Quando um usuário se autentica em uma coleção que contém o Office 365, Office verifica toosee se usuário Olá tiver sido configurado para o Office 365 ProPlus. Se assim, Office temporariamente ativa o Office 365 ProPlus - essa ativação persiste até que sinais de usuários fora de serviço hello.

toouse a ativação de computador compartilhados do Office 365, você precisa toocreate um [modelo personalizado](remoteapp-create-custom-image.md) e instalação do Office 365 ProPlus, seguindo [estas instruções](https://technet.microsoft.com/library/dn782858.aspx).

Você pode gerenciar licenças do Office 365 de seus usuários a saudação [Portal de administração do Office 365](https://portal.office365.com/). Para obter mais informações sobre os [Planos de serviço do Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Versão de avaliação do Office 2013 Professional Plus
Durante a avaliação de 30 dias do RemoteApp, você pode usar toocreate de imagem de modelo do hello Office 2013 Professional Plus (avaliação) uma coleção do RemoteApp. Você pode atribuir usuários toothis coleta de avaliação usando suas contas de trabalho do Azure Active Directory ou contas da Microsoft. Nenhuma assinatura adicional é necessária.

Isso é pneus de saudação de tookick uma ótima opção e ter uma boa noção do Office no RemoteApp. No entanto, essa opção é destinada somente para avaliação e teste. Coleções do RemoteApp criadas usando a imagem de modelo Olá Office 2013 Professional Plus (avaliação) não podem ser feita a transição tooproduction modo e serão desabilitadas no final de saudação do período de avaliação de saudação.

## <a name="switching-from-trial-tooproduction"></a>Alternar de avaliação tooproduction
Quando você iniciar sua avaliação gratuita de 30 dias, uma anotação em Olá RemoteApp seção do portal de saudação dirá quanto tempo você deixou na avaliação de saudação antes que você precise tooa tootransition paga a conta. Você pode ativar o modo de tooproduction de conta e o comutador usando o link de saudação nesta nota.

Quando você ativa sua conta, isso afetará todas as coleções do RemoteApp Olá em sua conta.

* Coleções que estão executando com hello Windows Server 2012 R2 ou o Office 365 ProPlus imagens de modelo Olá mudará tooproduction perfeitamente. Todos os dados de usuário e configurações, incluindo sessões em andamento, permanecerão intactas.
* Se você carregou imagens de modelo personalizada, as coleções usando essas imagens também mudarão perfeitamente.
* imagem de modelo do Office 2013 Professional Plus (avaliação) Olá destina-se somente para avaliação. Coleções em execução com esta imagem de modelo não podem ser feita a transição tooproduction. Elas serão colocadas no estado “desabilitado”.

Se você não fazer a transição tooproduction modo pela expiração Olá de sua avaliação, coleções do RemoteApp serão desabilitadas. Não se preocupe – suas configurações e dados de usuários são salvos para outro 90 dias, portanto, você ainda pode ativar o modo de tooproduction de serviço e o comutador sem perda de dados.

