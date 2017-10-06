---
title: "algoritmo de hash de assinatura aaaChange da terceira parte confiável do Office 365 | Microsoft Docs"
description: "Esta página fornece diretrizes para alterar o algoritmo SHA para confiança de federação com o Office 365"
keywords: "SHA1, SHA256, O365, federação, aadconnect, adfs, ad fs, alterar o sha, confiança de federação, objeto de confiança de terceira parte confiável"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a>Alterar o algoritmo de hash de assinatura para o objeto de confiança de terceira parte confiável Office 365
## <a name="overview"></a>Visão geral
Os serviços de Federação do Active Directory (AD FS) assina seu tooensure Active Directory do Azure tooMicrosoft de tokens que não pode ser violados. Essa assinatura pode ser baseada em SHA1 ou em SHA256. Active Directory do Azure agora oferece suporte a tokens assinados com um algoritmo SHA256 e é recomendável definir tooSHA256 de algoritmo de assinatura de token Olá para o nível mais alto de saudação de segurança. Este artigo descreve etapas Olá necessário toohello de algoritmo de assinatura de token do tooset hello mais seguras nível SHA256.

>[!NOTE]
>A Microsoft recomenda o uso de SHA256 como algoritmo de saudação para assinar tokens como SHA1 ainda é uma opção com suporte, mas é mais seguro do que SHA1.

## <a name="change-hello-token-signing-algorithm"></a>Alterar o algoritmo de assinatura de token Olá
Depois que você configurou o algoritmo de assinatura de saudação com uma saudação dois processos abaixo, o AD FS assina os tokens de saudação para o Office 365 terceira parte confiável com SHA256. Você não precisa toomake as alterações de configuração adicional, e essa alteração não tem nenhum impacto em sua capacidade tooaccess Office 365 ou outros aplicativos do AD do Azure.

### <a name="ad-fs-management-console"></a>Console de gerenciamento do AD FS
1. Abra o console de gerenciamento do hello AD FS no servidor do hello primário AD FS.
2. Expanda o nó do hello AD FS e clique em **terceira parte confiável**.
3. Clique com o botão direito do mouse no Office 365/objeto de confiança de terceira parte confiável e selecione **Propriedades**.
4. Selecione Olá **avançado** guia e o algoritmo de hash seguro Olá selecione SHA256.
5. Clique em **OK**.

![Algoritmo de assinatura SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a>Cmdlets do PowerShell do AD FS
1. Em qualquer servidor do AD FS, abra o PowerShell com privilégios de administrador.
2. Algoritmo de hash seguro conjunto hello usando Olá **Set-AdfsRelyingPartyTrust** cmdlet.
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a>Leia também
* [Reparar a confiança do Office 365 com o Azure AD Connect](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

