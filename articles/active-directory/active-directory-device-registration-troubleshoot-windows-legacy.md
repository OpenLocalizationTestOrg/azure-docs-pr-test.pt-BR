---
title: "aaaTroubleshooting Olá o registro automático de domínio do AD do Azure em computadores ingressados para clientes de nível inferior do Windows | Microsoft Docs"
description: "Solucionando problemas de registro automático de saudação do domínio do AD do Azure em computadores ingressados para clientes de nível inferior do Windows."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD para clientes de nível inferior do Windows 

Este tópico é aplicável toohello somente os clientes a seguir: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Para Windows 10 ou Windows Server 2016, consulte [Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD – Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

Este tópico pressupõe que você tenha configurado o registro automático de dispositivos que ingressaram no domínio conforme descrito em descrito em [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-device-registration-get-started.md).
 
Este tópico fornece orientação sobre como tooresolve possíveis problemas de solução de problemas.  
Toonote algumas coisas para resultados bem-sucedida: 

- O registro desses clientes no Azure AD ocorre por dispositivo/usuário. Por exemplo: se jdoe e jharnett logon toothis dispositivo, um registro separado (DeviceID) é criado para cada um desses usuários na guia de informações de usuário de saudação.  

- O registro desses clientes fora da caixa de saudação é tootry configurado no logon ou Bloquear/desbloquear e pode haver atraso de 5 minutos, isso é disparado usando uma tarefa do Agendador de tarefas. 

- Uma reinstalação do sistema operacional de saudação ou cancelar o registro manual e registrar novamente pode criar um novo registro no AD do Azure e resultará em várias entradas na guia de informações de usuário Olá no hello portal do Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Etapa 1: Recuperar o status de registro de saudação 

**status do registro Olá tooverify:**  

1. Olá abrir o prompt de comando como administrador 

2. Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Este comando exibe uma caixa de diálogo que fornece mais detalhes sobre o status de associação de saudação.

![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>Etapa 2: Avaliar o status de registro de saudação 

Se a associação de saudação não foi bem-sucedida, caixa de diálogo de saudação fornece com detalhes sobre o problema de saudação que ocorreu.

**Olá os problemas mais comuns são:**

- Um AD FS ou Azure AD configurado incorretamente

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- Você não está conectado como um usuário de domínio

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Você atingiu uma cota

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- saudação de serviço não está respondendo 

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

Você também pode encontrar informações de status de Olá no log de eventos de saudação em **aplicativos e serviços Log\Microsoft-ingresso**.
  
**causas mais comuns de saudação para registro com falha são:** 

- O computador não estiver no rede interna da organização hello ou uma VPN sem conexão tooan local controlador de domínio do AD.

- Você está conectado no computador tooyour com uma conta de computador local. 

- Problemas de configuração do serviço: 

  - Olá servidor de Federação foi configurado toosupport **WIAORMULTIAUTHN**. 

  - Não há nenhum objeto de ponto de Conexão de serviço que aponta para o nome de domínio verificado tooyour no AD do Azure na floresta Olá AD qual pertence o computador de saudação.

  - Um usuário atingiu o limite de saudação de dispositivos. Consulte a Introdução ao registro de dispositivos do Azure Active Directory.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, consulte Olá [perguntas frequentes sobre o registro de dispositivo automático](active-directory-device-registration-faq.md) 
