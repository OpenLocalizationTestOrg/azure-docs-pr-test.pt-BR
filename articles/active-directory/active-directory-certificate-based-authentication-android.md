---
title: "autenticação baseada em certificado do Active Directory da aaaAzure no Android | Microsoft Docs"
description: "Saiba mais sobre cenários de saudação com suporte e requisitos de saudação para configurar a autenticação baseada em certificado em soluções com dispositivos Android"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 148275fa3da610530c278fcd57e02e907f735d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a>Autenticação baseada em certificado do Azure Active Directory no Android


Autenticação baseada em certificado (CBA) permite que você toobe autenticado pelo Active Directory do Azure com um certificado de cliente em um dispositivo Windows, Android ou iOS ao conectar-se a sua conta do Exchange online para: 

* Aplicativos móveis do Office, como Microsoft Outlook e Microsoft Word   
* Clientes do EAS (Exchange ActiveSync) 

Configurar esse recurso elimina a necessidade de saudação tooenter um nome de usuário e combinação de senha em determinados email e aplicativos do Microsoft Office em seu dispositivo móvel. 

Este tópico fornece requisitos hello e cenários Olá com suporte para configurar CBA em um dispositivo de iOS(Android) para usuários de locatários no Office 365 Enterprise, Business, educação, China, governo dos EUA e Alemanha planos.



Esse recurso está disponível na visualização em planos do governo federal e para defesa governamental dos EUA do Office 365.


## <a name="office-mobile-applications-support"></a>Suporte a aplicativos móveis do Office
| Aplicativos | Suporte |
| --- | --- |
| Aplicativo de Proteção de Informações do Azure |![Verificação][1] |
| Equipes da Microsoft |![Verificação][1] |
| OneNote |![Verificação][1] |
| OneDrive |![Verificação][1] |
| Outlook |![Verificação][1] |
| Aplicativos móveis do Power BI |![Verificação][1] |
| Skype for Business |![Verificação][1] |
| Word/Excel/PowerPoint |![Verificação][1] |
| Yammer |![Verificação][1] |


### <a name="implementation-requirements"></a>Requisitos de implementação

Olá versão de SO do dispositivo deve ser Android 5.0 (pirulito) e acima. 

Um servidor de federação deve ser configurado.  

Para toorevoke um certificado de cliente do Active Directory do Azure, o token do AD FS Olá deve ter Olá declarações a seguir:  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (Olá o número de série do certificado de cliente Olá) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (cadeia de caracteres Olá para o emissor de saudação do certificado de cliente Olá) 

Active Directory do Azure adiciona o token de atualização de toohello essas declarações se eles estão disponíveis no token do AD FS hello (ou qualquer outro token SAML). Quando o token de atualização Olá precisa toobe validado, essas informações são usadas toocheck Olá revogação. 

Como prática recomendada, você deve atualizar páginas de erro do ADFS Olá com instruções sobre como tooget um certificado de usuário.  
Para obter mais detalhes, consulte [Personalizando páginas Olá AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).  

Alguns aplicativos do Office (com autenticação moderna habilitado) enviar '*prompt = logon*' tooAzure AD em sua solicitação. Por padrão, o AD do Azure converte isso em Olá solicitação tooADFS muito '*wauth = usernamepassworduri*' (solicita autenticação do ADFS toodo U/P) e '*wfresh = 0*' (solicita o estado do ADFS tooignore SSO e fazer uma autenticação nova) . Se você quiser que a autenticação baseada em certificado tooenable para esses aplicativos, você precisa comportamento do toomodify saudação padrão do AD do Azure. Apenas o conjunto de saudação '*PromptLoginBehavior*' nas configurações do domínio federado muito '*desabilitado*'. Você pode usar o hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform cmdlet essa tarefa:

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a>Suporte aos clientes do Exchange ActiveSync
Há suporte para determinados aplicativos do Exchange ActiveSync no Android 5.0 (Lollipop) ou superior. toodetermine se seu aplicativo de email oferece suporte a esse recurso, entre em contato com o desenvolvedor do aplicativo. 


## <a name="next-steps"></a>Próximas etapas

Se você quiser tooconfigure a autenticação baseada em certificado em seu ambiente, consulte [Introdução à autenticação baseada em certificado no Android](active-directory-certificate-based-authentication-get-started.md) para obter instruções.

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
