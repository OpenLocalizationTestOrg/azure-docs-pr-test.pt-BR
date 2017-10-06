---
title: "aaaWhat está em imagens de modelo hello Azure RemoteApp? | Microsoft Docs"
description: "Saiba mais sobre imagens de modelo Olá incluídas com o Azure RemoteApp."
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
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>O que há imagens de modelo hello Azure RemoteApp?
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Sua assinatura do RemoteApp do Azure inclui três imagens de modelo:

* Windows Server 2012
* Microsoft Office 365 ProPlus (assinatura do Office 365 necessária)
* Microsoft Office 2013 Professional Plus (somente avaliação)

> [!IMPORTANT]
> Sua assinatura do Azure RemoteApp concede que acesso toohello software nas imagens hello, com exceção de saudação do Office 365 ProPlus, que requer uma assinatura separada, e Office 2013, que não pode ser usado na produção. Isso significa que você pode compartilhar programas hello ou aplicativos em imagens de modelo Olá com seus usuários. Por exemplo, se você criar uma coleção que usa a imagem do Windows Server 2012 R2 hello, você pode publicar System Center Endpoint Protection para tooaccess de usuários por meio do RemoteApp.
> 
> Check-out Olá [RemoteApp licenciamento detalhes](remoteapp-licensing.md) para obter mais informações. E [usando o Office com o Azure RemoteApp](remoteapp-o365.md) para Olá informações de licenciamento do Office.
> 
> 

Leia mais para obter detalhes sobre o que cada imagem contém.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 ("Olá baunilha imagem")
Esta imagem é baseada no sistema de operacional do Microsoft Windows Server 2012 R2 Datacenter e tem hello seguintes funções e recursos instalados toomeet requisitos de saudação para imagens de modelo do RemoteApp do Azure:

* .NET framework 4.5, 3.5.1 e 3.5
* Experiência Desktop
* Serviços de tinta e manuscrito
* Media Foundation
* Host de sessão de área de trabalho remota
* Windows PowerShell 4.0
* Windows PowerShell ISE
* Suporte a WoW64

Esta imagem tem também Olá aplicativos instalados a seguir:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (assinatura necessária)
O Office 365 é hello mais aplicativo solicitado, criamos uma imagem "custom" você toowork com.

Esta imagem é uma extensão da imagem de baunilha hello e tem hello seguintes componentes do Microsoft Office 365 ProPlus instalado além toohello componentes descritos na imagem do Windows Server 2012 R2 hello:

* Access
* Excel
* Lync
* OneNote
* OneDrive para empresas (Observe que o agente de sincronização Olá não tem suporte para uso com o Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Revisores de texto do Microsoft Office

imagem de saudação também inclui Visio Pro e Pro do projeto.

E Olá aplicativos, bem como a seguir:

* SQL Native client
* Driver ODBC
* Cliente SQL Server Data Mining
* Cliente MasterDataServices
* Microsoft Publisher
* PowerQuery
* PowerMap

Toda a funcionalidade dos aplicativos do Office 365 ProPlus está disponível apenas para os usuários que têm um plano do Office 365 ProPlus. Para obter mais detalhes sobre a assinatura do Office 365 de saudação planos consulte [planos de serviço do Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx). Ainda tem dúvidas? Check-out Olá [Office 365 + RemoteApp](remoteapp-o365.md) informações. Confira também novo artigo de hello, [como toouse sua assinatura do Office 365 com o Azure RemoteApp](remoteapp-officesubscription.md).

Observe que você precisa toolicense Office 365 ProPlus, Visio Pro e projeto Pro separadamente - cada um deles tem sua própria licença.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus (somente avaliação)
Durante o período de avaliação gratuita hello, você pode testar o serviço de saudação com imagem Olá Office 2013.

Esta imagem é uma extensão da imagem de baunilha hello e tem hello seguintes componentes do Microsoft Office 2013 Professional Plus instalado além toohello componentes descritos na imagem do Windows Server 2012 R2 hello:

* Access
* Excel
* Lync
* OneNote
* OneDrive para empresas (Observe que o agente de sincronização Olá não tem suporte para uso com o Azure RemoteApp)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Revisores de texto do Microsoft Office

> [!IMPORTANT]
> **Informações legais:** esta imagem não inclui uma licença do Microsoft Office e *não pode ser usada para a produção*. imagem do Office 2013 Professional Plus Olá destina-se somente para teste. Se você quiser toouse aplicativos do Office no Azure RemoteApp para produção, você precisa imagem Office 365 ProPlus do toouse hello. Para obter mais detalhes sobre licenciamento do Office, consulte [Usar o Office 365 com o RemoteApp do Azure](remoteapp-o365.md)
> 
> 

