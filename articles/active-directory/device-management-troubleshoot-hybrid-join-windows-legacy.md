---
title: "aaaTroubleshooting híbrida do Active Directory do Azure associado a dispositivos de nível inferior | Microsoft Docs"
description: "Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos de nível inferior."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos de nível inferior 

Este tópico é aplicável toohello somente dispositivos a seguir: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Para Windows 10 ou Windows Server 2016, confira [Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016](device-management-troubleshoot-hybrid-join-windows-current.md).

Este tópico pressupõe que você tenha [dispositivos ingressados no configurado híbrida do Active Directory do Azure](device-management-hybrid-azuread-joined-devices-setup.md) Olá toosupport os seguintes cenários:

- Acesso condicional com base em dispositivo

- [Roaming corporativo de configurações](active-directory-windows-enterprise-state-roaming-overview.md)

- [Configurar o Hello for Business](active-directory-azureadjoin-passport-deployment.md) 





Este tópico fornece orientação sobre como tooresolve possíveis problemas de solução de problemas.  

**O que você deve saber:** 

- número máximo de saudação de dispositivos por usuário é centrada no dispositivo. Por exemplo, se *jdoe* e *jharnett* tooa entrar no dispositivo, um registro separado (DeviceID) é criado para cada um deles Olá **usuário** guia informações.  

- Olá registro inicial / join de dispositivos é configurado tooperform uma tentativa de logon ou de bloqueio / desbloqueio. Pode haver um atraso de cinco minutos disparado por uma tarefa do agendador de tarefas. 

- A reinstalação do sistema operacional de saudação ou manual cancela o registro e registrar novamente podem criar um novo registro no AD do Azure e resulta em várias entradas na guia de informações de usuário Olá no hello portal do Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Etapa 1: Recuperar o status de registro de saudação 

**status do registro Olá tooverify:**  

1. Olá abrir o prompt de comando como administrador 

2. Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Este comando exibe uma caixa de diálogo que fornece mais detalhes sobre o status de associação de saudação.

![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>Etapa 2: Avaliar o status de junção Olá híbrido do AD do Azure 

Se ingresso no AD do Azure Olá híbrida não foi bem-sucedida, caixa de diálogo de saudação fornece detalhes sobre Olá problema ocorrido.

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
  
**causas mais comuns de saudação para uma associação de AD do Azure híbrido com falha são:** 

- O computador não estiver no rede interna da organização hello ou uma VPN sem conexão tooan local controlador de domínio do AD.

- Você está conectado no computador tooyour com uma conta de computador local. 

- Problemas de configuração do serviço: 

  - Olá servidor de Federação foi configurado toosupport **WIAORMULTIAUTHN**. 

  - Não há nenhum objeto de ponto de Conexão de serviço que aponta para o nome de domínio verificado tooyour no AD do Azure na floresta Olá AD qual pertence o computador de saudação.

  - Um usuário atingiu o limite de saudação de dispositivos. 

## <a name="next-steps"></a>Próximas etapas

Para perguntas, consulte Olá [perguntas frequentes sobre o gerenciamento de dispositivos](device-management-faq.md)  
