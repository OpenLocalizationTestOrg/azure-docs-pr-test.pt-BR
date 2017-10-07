---
title: "Azure AD Connect: instâncias do serviço de sincronização | Microsoft Docs"
description: "Esta página documenta considerações especiais para instâncias do Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect: considerações especiais para instâncias
Conexão do AD do Azure é mais comumente usado com a instância do hello world-wide do AD do Azure e o Office 365. Mas também existem outras instâncias que têm requisitos diferentes para URLs e outras considerações especiais.

## <a name="microsoft-cloud-germany"></a>Microsoft Cloud Alemanha
Olá [Microsoft Cloud Alemanha](http://www.microsoft.de/cloud-deutschland) é uma nuvem soberana operada por um objeto de confiança dados alemão.

| Tooopen de URLs no servidor proxy |
| --- |
| \*.microsoftonline.de |
| \*.windows.net |
| + Listas de revogação de certificados |

Quando você entrar no locatário do AD do Azure tooyour, você deve usar uma conta no domínio de onmicrosoft.de hello.

Recursos atualmente não está presentes na Alemanha do Microsoft Cloud hello:

* O **Azure AD Connect Health** não está disponível.
* As **Atualizações automáticas** não estão disponíveis.
* O **Write-back de senha** está disponível em versão prévia no Azure AD Connect versão 1.1.570.0 e posteriores.
* Outros serviços do Azure AD Premium não estão disponíveis.

## <a name="microsoft-azure-government-cloud"></a>Nuvem do Microsoft Azure Governamental
Olá [nuvem do Microsoft Azure Government](https://azure.microsoft.com/features/gov/) é uma nuvem para o governo dos EUA.

Esta nuvem teve suporte em versões mais antigas do DirSync. Compilação 1.1.180 do Azure AD Connect, Olá próxima geração da nuvem de saudação é suportada. Essa geração está usando pontos de extremidade com base somente nos EUA e tem uma lista de URLs tooopen diferente no servidor proxy.

| Tooopen de URLs no servidor proxy |
| --- |
| \*.microsoftonline.com |
| \*.microsoftonline.us |
| \*.gov.us.microsoftonline.com |
| + Listas de revogação de certificados |

Conexão do AD do Azure não é capaz de tooautomatically detectar que o seu locatário do AD do Azure está localizado na nuvem do governo hello. Em vez disso, você precisa de saudação tootake ações a seguir quando você instala o Azure AD Connect.

1. Inicie a instalação do Azure AD Connect hello.
2. Quando você vir a página primeiro hello, onde você deve tooaccept Olá EULA, não continuar, mas deixar o Assistente de instalação de saudação em execução.
3. Inicie o regedit e alterar a chave de registro de saudação `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valor `2`.
4. Voltar Assistente de instalação toohello do Azure AD Connect, aceite o EULA de saudação e continuar. Durante a instalação, verifique se Olá de toouse **configuração personalizada** caminho de instalação (e não a instalação expressa). Em seguida, continue a instalação do hello como de costume.

Recursos atualmente não está presentes na nuvem do Microsoft Azure Government Olá:

* O **Azure AD Connect Health** não está disponível.
* As **Atualizações automáticas** não estão disponíveis.
* O **Write-back de senha** está disponível em versão prévia no Azure AD Connect versão 1.1.570.0 e posterior.
* Outros serviços do Azure AD Premium não estão disponíveis.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
