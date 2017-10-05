---
title: "O que são as imagens de modelo do RemoteApp do Azure? | Microsoft Docs"
description: "Saiba mais sobre as imagens de modelo incluídas no RemoteApp do Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cd4e1a16a7c42bd00d9e543d7b62b72e9de3fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-in-the-azure-remoteapp-template-images"></a>O que são as imagens de modelo do RemoteApp do Azure?
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Sua assinatura do RemoteApp do Azure inclui três imagens de modelo:

* Windows Server 2012
* Microsoft Office 365 ProPlus (assinatura do Office 365 necessária)
* Microsoft Office 2013 Professional Plus (somente avaliação)

> [!IMPORTANT]
> Sua assinatura do RemoteApp do Azure concede o acesso ao software nas imagens, com exceção do Office 365 ProPlus, que requer uma assinatura separada, e do Office 2013, que não pode ser usado na produção. Isso significa que você pode compartilhar os programas ou aplicativos nas imagens de modelo com seus usuários. Por exemplo, se você criar uma coleção que usa a imagem do Windows Server 2012 R2, poderá publicar o System Center Endpoint Protection para que os usuários acessem por meio do RemoteApp.
> 
> Confira os [Detalhes de licenciamento do RemoteApp](remoteapp-licensing.md) para obter mais informações. Consulte também [Usando o Office com o RemoteApp do Azure](remoteapp-o365.md) para obter informações de licenciamento do Office.
> 
> 

Leia mais para obter detalhes sobre o que cada imagem contém.

## <a name="windows-server-2012-r2--the-vanilla-image"></a>Windows Server 2012 R2 ("a imagem baunilha")
Essa imagem é baseada no sistema operacional para Data Center Microsoft Windows Server 2012 R2 e tem as seguintes funções e recursos instalados para atender aos requisitos de imagens de modelo RemoteApp do Azure:

* .NET framework 4.5, 3.5.1 e 3.5
* Experiência Desktop
* Serviços de tinta e manuscrito
* Media Foundation
* Host de sessão de área de trabalho remota
* Windows PowerShell 4.0
* Windows PowerShell ISE
* Suporte a WoW64

Esta imagem também tem os seguintes aplicativos instalados:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (assinatura necessária)
O Office 365 é o aplicativo mais solicitado, criamos uma imagem "personalizada" para trabalhar com ele.

Essa imagem é uma extensão da imagem baunilha e tem os seguintes componentes do Microsoft Office 365 ProPlus instalados juntamente com os componentes descritos na imagem do Windows Server 2012 R2:

* Access
* Excel
* Lync
* OneNote
* OneDrive for Business (Observe que o agente de sincronização não é suportado para o uso com o Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Revisores de texto do Microsoft Office

A imagem também inclui Visio Pro e Project Pro.

E os seguintes aplicativos, assim:

* SQL Native client
* Driver ODBC
* Cliente SQL Server Data Mining
* Cliente MasterDataServices
* Microsoft Publisher
* PowerQuery
* PowerMap

Toda a funcionalidade dos aplicativos do Office 365 ProPlus está disponível apenas para os usuários que têm um plano do Office 365 ProPlus. Para obter mais detalhes sobre os planos de assinatura do Office 365, consulte [Planos de serviço do Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx). Ainda tem dúvidas? Confira as informações do [Office 365 + RemoteApp](remoteapp-o365.md) . Verifique também o novo artigo, [Como usar sua assinatura do Office 365 com o RemoteApp do Azure](remoteapp-officesubscription.md).

Observe que você precisa licenciar o Office 365 ProPlus, o Visio Pro e o Project Pro separadamente - cada um deles tem sua própria licença.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus (somente avaliação)
Durante o período de avaliação gratuito, você pode testar o serviço com a imagem do Office 2013.

Essa imagem é uma extensão da imagem baunilha e tem os seguintes componentes do Microsoft Office 2013 ProPlus instalados juntamente com os componentes descritos na imagem do Windows Server 2012 R2:

* Access
* Excel
* Lync
* OneNote
* OneDrive for Business (Observe que o agente de sincronização não é suportado para o uso com o Azure RemoteApp)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Revisores de texto do Microsoft Office

> [!IMPORTANT]
> **Informações legais:** esta imagem não inclui uma licença do Microsoft Office e *não pode ser usada para a produção*. A imagem do Office 2013 Professional Plus é destinada apenas ao uso para avaliação. Se quiser usar os aplicativos do Office no RemoteApp do Azure para produção, você precisará usar a imagem do Office 365 ProPlus. Para obter mais detalhes sobre licenciamento do Office, consulte [Usar o Office 365 com o RemoteApp do Azure](remoteapp-o365.md)
> 
> 

