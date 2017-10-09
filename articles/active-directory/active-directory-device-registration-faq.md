---
title: "aaaAzure registro de dispositivo automático do Active Directory perguntas Frequentes | Microsoft Docs"
description: "Perguntas frequentes sobre o registro automático de dispositivo com o Azure Active Directory."
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
ms.openlocfilehash: ba7f113fd3bc310def001a1f44d938b0be71dba8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a>Perguntas frequentes sobre o registro automático de dispositivo do Azure Active Directory

**P: posso registrar o dispositivo de saudação recentemente. Por que não é possível ver dispositivo Olá em minhas informações de usuário no portal do Azure de saudação?**

**R:** dispositivos Windows 10 que ingressaram no domínio com o registro automático do dispositivo não aparecem em informações de saudação do usuário.
É necessário toouse PowerShell toosee todos os dispositivos. 

Somente hello seguintes dispositivos são listados na informação de usuário hello:

- Todos os dispositivos pessoais que não são ingressados pela empresa 
- Todos os não Windows 10/Windows Server 2016 
- Todos os dispositivos não Windows 

---

**P: por que não posso ver todos os dispositivos de saudação registrados no Active Directory do Azure no portal do Azure de saudação?** 

**R:** atualmente, não há nenhuma maneira toosee todos os dispositivos registrados no hello portal do Azure. Você pode usar o Azure PowerShell toofind todos os dispositivos. Para obter mais detalhes, consulte Olá [MsolDevice Get](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.

--- 

**P: como posso saber quais estado do registro de dispositivo saudação do cliente Olá é?**

**R:** depende do estado do registro de dispositivo hello:

- Qual dispositivo Olá é
- Como ele foi registrado 
- Todos os detalhes relacionados tooit. 
 

---

**P: por que é um dispositivo que tenha excluído no hello Azure portal ou usando o Windows PowerShell ainda listados como registrado?**

**R:** Esse comportamento é intencional. dispositivo Olá não terá acesso tooresources na nuvem hello. Se você quiser tooremove Olá dispositivo e registrar novamente, uma ação manual deve ser toobe efetuado no dispositivo de saudação. 

Para Windows 10 e Windows Server 2016 que estão ingressados pelo domínio do AD local:

1.  Olá abrir o prompt de comando como administrador.

2.  Digite `dsregcmd.exe /debug /leave`

3.  Saia e entre em tootrigger Olá tarefa agendada que registra o dispositivo Olá novamente. 

Para outras plataformas Windows que estão ingressadas pelo domínio do AD local:

1.  Olá abrir o prompt de comando como administrador.
2.  Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.
3.  Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.

---

**P: Por que vejo entradas de dispositivo duplicadas no Portal do Azure?**

**R:**

-   Para Windows 10 e Windows Server 2016, caso eles sejam repetidas tentativas toounjoin e una hello mesmo dispositivo, pode haver entradas duplicadas. 

-   Se você tiver usado a adicionar conta corporativa ou escolar, cada usuário do windows que usa adicionar conta corporativa ou escolar criará um novo registro de dispositivo com hello mesmo nome de dispositivo.

-   Outras plataformas do Windows que estão no local usando o registro automático ingressado no domínio do AD criará um novo registro de dispositivo com hello mesmo nome de dispositivo para cada usuário de domínio que faz logon em um dispositivo de saudação. 

-   Uma máquina AADJ foi apagada, reinstalado e Unido novamente com hello mesmo nome, será mostrada como outro registro com hello mesmo nome de dispositivo.

---

**P: por que um usuário ainda pode acessar recursos de um dispositivo que tenha desabilitado no hello portal do Azure?**

**R:** pode levar até horas tooan para um toobe revoke aplicado.

>[!Note] 
>Para dispositivos perdidos, recomendamos apagar Olá dispositivo tooensure que os usuários não poderão acessar o dispositivo hello. Para obter mais detalhes, consulte [Registrar dispositivos para gerenciamento no Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune). 


---

**P: Por que meus usuários veem "Você não pode chegar lá daqui"?**

**R:** se você configurou certa regras de acesso condicional toorequire um estado específico do dispositivo e dispositivo Olá não atendem aos critérios de hello, os usuários estão bloqueados e verá esta mensagem. Avaliar regras hello e certifique-se de que o dispositivo Olá é capaz de toomeet Olá critérios tooavoid essa mensagem.

---


**P: posso ver Olá registro de dispositivo em informações de usuário Olá Olá portal do Azure e pode ver o estado de saudação conforme registrado no cliente de saudação. Estou configurado corretamente para usar o acesso condicional?**

**R:** registro de dispositivo da saudação (deviceID) e o estado em Olá portal do Azure devem corresponder cliente hello e atender a qualquer critério de avaliação de acesso condicional. Para obter mais informações, consulte [Introdução ao registro de dispositivos do Azure Active Directory](active-directory-device-registration.md).

---

**P: por que recebo uma mensagem de "nome de usuário ou senha está incorreta" para um dispositivo tenha apenas Unido tooAzure AD?**

**R:** As razões comuns para esse cenário são:

- Suas credenciais de usuário não são mais válidas.

- O computador está toocommunicate não é possível com o Active Directory do Azure. Verifique se há problemas de conectividade de rede.

- Olá junção do Azure AD pré-requisitos não foram atendidos. Certifique-se de que você tiver seguido as etapas de saudação para [estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Azure Active Directory](active-directory-azureadjoin-overview.md).  

- Logons federados requer o servidor de Federação toosupport um ponto de extremidade do WS-Trust ativo. 

---

**P: por que vejo hello "Opa... Ocorreu um erro!" caixa de diálogo quando tento ingressar em Meu computador?**

**R:** Esse é um resultado da configuração de registro do Azure Active Directory como Intune. Para obter mais detalhes, consulte [Configurar o gerenciamento do dispositivo Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).  

---

**P: por que meu toojoin de tentativa de um computador falhar, embora não recebi qualquer informação de erro?**

**R:** uma causa provável é que esse usuário Olá é registrado no dispositivo toohello usando a conta de administrador interno hello. Crie uma conta local diferente antes de usar a instalação de saudação toocomplete a junção do Azure Active Directory. 

---

**P: onde posso encontrar instruções de instalação de saudação do registro automático do dispositivo?**

**R:** para obter instruções detalhadas, consulte [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md)

---

**P: onde encontrar a solução de problemas informações sobre o registro de dispositivo automático Olá?**

**R:** Para encontrar informações de solução de problemas, consulte:

- [Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD – Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)

- [Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD para clientes de nível inferior do Windows](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

