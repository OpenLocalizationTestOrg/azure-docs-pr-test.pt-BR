---
title: "aaaAdd tooyour um usuário coleção do RemoteApp do Azure | Microsoft Docs"
description: "Saiba como tooadd usuários tooyour coleção do RemoteApp do Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>Como tooadd tooyour um usuário coleção do RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Antes dos usuários podem ver e usar seus aplicativos no Azure RemoteApp, você tem toogrant tooyour coleção a eles acesso. Isso faz parte de fácil Olá: em Olá **acesso de usuário** guia, insira informações de conta de saudação do usuário Olá e, em seguida, clique em marca de seleção de saudação.

Quais informações da conta são necessárias? Isso depende Olá tipo de coleção criado por você (nuvem ou híbrida) e se você estiver usando Office 365 ProPlus nessa coleção.

## <a name="supported-user-identities"></a>Identidades de usuário com suporte
tipos de coleção diferente de saudação (nuvem versus híbrido) suportam o uso de diferentes identidades de usuário para acesso tooapplications.  

Para uma coleção híbrida do RemoteApp, você precisa tooset backup de uma infraestrutura de domínio do Active Directory local e um locatário do Active Directory do Azure com a integração de diretório (e opcionalmente o logon único). Além disso, você precisa toocreate alguns objetos do Active Directory no diretório local de saudação.  

Para uma coleção de nuvem do RemoteApp, qualquer usuário que tenha o Active Directory do Azure suporta identidades pode ser concedido usuário acesso tooRemoteApp tooinclude Accounts da Microsoft.  Consulte a tabela de saudação abaixo.

Os usuários do Office 365 são usuários do Active Directory do Azure. Se eles tiverem o Active Directory do Azure híbrido, as contas sincronizadas do diretório, eles poderão receber acesso de usuário em uma implantação híbrida do RemoteApp.   

Você pode usar essa tabela como uma referência rápida para o qual há suporte para em sua coleção e quais são os requisitos de Active Directory Olá identidade.

| Contas de usuário | Nuvem | Híbrido |
| --- | --- | --- |
| Conta da Microsoft |Sim |Não |
| Active Directory do Azure (Azure AD) | | |
| Somente nuvem do Azure AD |Sim |Não |
| ADsync com sincronização de senha |Sim |Sim |
| ADsync sem sincronização de senha |Sim |Não |
| ADsync com o AD FS |Sim |sim |
| [Provedores de identidade de terceiros com suporte do Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (por exemplo, Ping) |Sim |Sim |
| Multi-Factor Authentication |Sim |Sim |

Verifique [obter mais informações](remoteapp-ad.md) sobre a configuração do Active Directory para o RemoteApp.

> [!NOTE]
> os usuários do Active Directory do Azure Olá devem ser do locatário Olá associado à sua assinatura. (Você pode exibir e modificar sua assinatura do hello **configurações** no portal de saudação. Consulte [locatário de Active Directory do Azure Olá alteração usado pelo RemoteApp](remoteapp-changetenant.md) para obter mais informações.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Informações de conta de usuário do Office 365 ProPlus
Se você estiver usando a imagem de modelo Olá Office 365 ProPlus em sua coleção *ou* se você tiver criado uma imagem personalizada que usa o Office 365, são permitidos apenas os usuários tooadd do Active Directory do Azure que têm assinaturas do Office 365 para Olá domínio padrão da sua assinatura. Consulte [Usando o Office 365 com o Azure RemoteApp](remoteapp-o365.md) para obter mais informações.

