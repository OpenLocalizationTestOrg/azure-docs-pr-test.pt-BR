---
title: aaaAuthenticate com o Active Directory local em seu aplicativo do Azure | Microsoft Docs
description: "Saiba mais sobre as diferentes opções de saudação para aplicativos de linha de negócios no tooauthenticate do serviço de aplicativo do Azure com o Active Directory no local"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Autenticar com o Active Directory local em seu aplicativo do Azure
Este artigo mostra como tooauthenticate com local AD (Active Directory) em [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md). Um aplicativo do Azure está hospedado na nuvem hello, mas há maneiras tooauthenticate AD usuários locais com segurança. 

## <a name="authenticate-through-azure-active-directory"></a>Autenticar por meio do Azure Active Directory
Um locatário do Azure Active Directory pode ser sincronizado com o diretório com um AD local. Essa abordagem permite que os usuários do AD acessar seu aplicativo do hello internet e autenticar usando suas credenciais locais. Além disso, o Serviço de Aplicativo do Azure fornece uma [solução completa para esse método](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Com alguns cliques, você poderá habilitar a autenticação com um locatário sincronizado com diretório para seu aplicativo do Azure. Essa abordagem tem Olá vantagens a seguir:

* Não exige um código de autenticação em seu aplicativo. Permitem serviço de aplicativo hello autenticação para você e gastar tempo na funcionalidade em seu aplicativo.
* [O Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) permite acessar dados de toodirectory de seu aplicativo do Azure.
* Fornece o SSO muito[todos os aplicativos suportados pelo Active Directory do Azure](/marketplace/active-directory/), incluindo o Office 365, Dynamics CRM Online, Microsoft Intune e milhares de aplicativos em nuvem não são da Microsoft. 
* O Azure Active Directory oferece suporte ao controle de acesso baseado em função. Você pode usar o padrão de saudação [Authorize(Roles="X")] com o código de tooyour alterações mínimas.

toosee como toowrite um aplicativo de linha de negócios do Azure que se autentica com o Active Directory do Azure, consulte [criar um aplicativo de linha de negócios do Azure com a autenticação do Active Directory do Azure](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Autenticação por meio de um STS local
Se você tiver um local seguro serviço de token (STS) como os serviços de Federação do Active Directory (AD FS), você pode usar essa autenticação toofederate para seu aplicativo do Azure. Essa abordagem é mais adequada quando a política da empresa proíbe o armazenamento dos dados do AD no Azure. No entanto, observe o seguinte hello:

* A topologia do STS deve ser implantada no local, com sobrecarga de gerenciamento e de custo.
* Os administradores do AD FS podem configurar [terceira relações de confiança de terceiros e regras de declaração](http://technet.microsoft.com/library/dd807108.aspx), que pode limitar as opções do desenvolvedor hello. Em Olá outro lado, é possível toomanage e personalizar [declarações](http://technet.microsoft.com/library/ee913571.aspx) em uma base por aplicativo.
* Acessar o local de tooon dados do AD requerem uma solução separada por meio do firewall corporativo hello.

toosee como toowrite um aplicativo de linha de negócios do Azure que se autentica com um STS local, consulte [criar um aplicativo de linha de negócios do Azure com autenticação do AD FS](web-sites-dotnet-lob-application-adfs.md).

