---
title: aaaAzure AD Connect na Alemanha Microsoft Cloud
description: "O Azure AD Connect integrará seus diretórios locais com o Azure Active Directory.  Isso permite que você tooprovide uma identidade comum para aplicativos do Office 365, Azure e SaaS integrada ao AD do Azure."
keywords: "Introdução tooAzure AD Connect, visão geral do Azure AD Connect, o que é o Azure AD Connect, instalar o active directory, Alemanha, preto floresta"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Azure AD Connect na Microsoft Cloud Alemanha - Visualização Pública
## <a name="introduction"></a>Introdução
O Azure AD Connect fornece sincronização entre o Active Directory local e o Azure Active Directory.
Atualmente, muitos dos cenários de saudação em [Microsoft Cloud Alemanha](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) deve ser feito por operador hello. Ao usar o Microsoft Cloud Alemanha, você deve estar ciente do seguinte hello:

* Olá que URLs a seguir devem ser abertas em um servidor proxy para sincronização toooccur com êxito:
  
  * *.microsoftonline.de
  * *.windows.net
  * * Listas de Revogação de Certificados
* Quando você entrar no diretório do AD do Azure tooyour, você deve usar uma conta no domínio de onmicrosoft.de hello.
* Olá recursos a seguir não está disponível:
  * Azure AD Connect Health
  * Atualizações automáticas
 
## <a name="download"></a>Baixar
Você pode baixar o Azure AD Connect da folha de conexão do AD do Azure hello dentro do portal de saudação.  Use as instruções de saudação abaixo folha do toolocate hello Azure AD Connect.

### <a name="hello-azure-ad-connect-blade"></a>saudação do Azure AD Connect-folha
Depois de ter entrado no toohello portal do Azure, Olá a seguir:

1. Vá tooBrowse
2. Selecione Azure Active Directory
3. Em seguida, selecione Azure AD Connect

Você verá a seguinte hello:

![Folha do Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

Hello tabela a seguir descreve os recursos de saudação mostrados na folha de saudação.

| Title | Descrição |
| --- | --- |
| STATUS DA SINCRONIZAÇÃO |Informa se a sincronização está habilitada ou desabilitada. |
| ÚLTIMA SINCRONIZAÇÃO |Olá a última vez em que uma sincronização bem-sucedida foi concluída. |
| DOMÍNIOS FEDERADOS |Mostra o número de saudação de domínios federados configurado no momento. |

## <a name="installation"></a>Instalação
tooinstall do Azure AD Connect, você pode usar a documentação de saudação [aqui](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Recursos avançados e informações adicionais
Para obter informações adicionais e orientação sobre as configurações personalizadas ou configurações avançadas, comece em [Integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).  Esta página fornece informações e links tooadditional orientação.

