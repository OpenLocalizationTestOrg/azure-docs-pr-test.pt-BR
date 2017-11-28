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
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="fc09a-103">Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD para clientes de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="fc09a-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="fc09a-104">Este tópico é aplicável toohello somente os clientes a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc09a-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="fc09a-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="fc09a-105">Windows 7</span></span> 
- <span data-ttu-id="fc09a-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="fc09a-106">Windows 8.1</span></span> 
- <span data-ttu-id="fc09a-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="fc09a-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="fc09a-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fc09a-108">Windows Server 2012</span></span> 
- <span data-ttu-id="fc09a-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fc09a-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="fc09a-110">Para Windows 10 ou Windows Server 2016, consulte [Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD – Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="fc09a-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="fc09a-111">Este tópico pressupõe que você tenha configurado o registro automático de dispositivos que ingressaram no domínio conforme descrito em descrito em [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fc09a-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="fc09a-112">Este tópico fornece orientação sobre como tooresolve possíveis problemas de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="fc09a-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="fc09a-113">Toonote algumas coisas para resultados bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="fc09a-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="fc09a-114">O registro desses clientes no Azure AD ocorre por dispositivo/usuário.</span><span class="sxs-lookup"><span data-stu-id="fc09a-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="fc09a-115">Por exemplo: se jdoe e jharnett logon toothis dispositivo, um registro separado (DeviceID) é criado para cada um desses usuários na guia de informações de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc09a-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="fc09a-116">O registro desses clientes fora da caixa de saudação é tootry configurado no logon ou Bloquear/desbloquear e pode haver atraso de 5 minutos, isso é disparado usando uma tarefa do Agendador de tarefas.</span><span class="sxs-lookup"><span data-stu-id="fc09a-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="fc09a-117">Uma reinstalação do sistema operacional de saudação ou cancelar o registro manual e registrar novamente pode criar um novo registro no AD do Azure e resultará em várias entradas na guia de informações de usuário Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc09a-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="fc09a-118">Etapa 1: Recuperar o status de registro de saudação</span><span class="sxs-lookup"><span data-stu-id="fc09a-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="fc09a-119">**status do registro Olá tooverify:**</span><span class="sxs-lookup"><span data-stu-id="fc09a-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="fc09a-120">Olá abrir o prompt de comando como administrador</span><span class="sxs-lookup"><span data-stu-id="fc09a-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="fc09a-121">Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="fc09a-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="fc09a-122">Este comando exibe uma caixa de diálogo que fornece mais detalhes sobre o status de associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc09a-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="fc09a-124">Etapa 2: Avaliar o status de registro de saudação</span><span class="sxs-lookup"><span data-stu-id="fc09a-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="fc09a-125">Se a associação de saudação não foi bem-sucedida, caixa de diálogo de saudação fornece com detalhes sobre o problema de saudação que ocorreu.</span><span class="sxs-lookup"><span data-stu-id="fc09a-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="fc09a-126">**Olá os problemas mais comuns são:**</span><span class="sxs-lookup"><span data-stu-id="fc09a-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="fc09a-127">Um AD FS ou Azure AD configurado incorretamente</span><span class="sxs-lookup"><span data-stu-id="fc09a-127">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="fc09a-129">Você não está conectado como um usuário de domínio</span><span class="sxs-lookup"><span data-stu-id="fc09a-129">You are not signed on as a domain user</span></span>

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="fc09a-131">Você atingiu uma cota</span><span class="sxs-lookup"><span data-stu-id="fc09a-131">A quota has been reached</span></span>

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="fc09a-133">saudação de serviço não está respondendo</span><span class="sxs-lookup"><span data-stu-id="fc09a-133">hello service is not responding</span></span> 

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="fc09a-135">Você também pode encontrar informações de status de Olá no log de eventos de saudação em **aplicativos e serviços Log\Microsoft-ingresso**.</span><span class="sxs-lookup"><span data-stu-id="fc09a-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="fc09a-136">**causas mais comuns de saudação para registro com falha são:**</span><span class="sxs-lookup"><span data-stu-id="fc09a-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="fc09a-137">O computador não estiver no rede interna da organização hello ou uma VPN sem conexão tooan local controlador de domínio do AD.</span><span class="sxs-lookup"><span data-stu-id="fc09a-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="fc09a-138">Você está conectado no computador tooyour com uma conta de computador local.</span><span class="sxs-lookup"><span data-stu-id="fc09a-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="fc09a-139">Problemas de configuração do serviço:</span><span class="sxs-lookup"><span data-stu-id="fc09a-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="fc09a-140">Olá servidor de Federação foi configurado toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="fc09a-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="fc09a-141">Não há nenhum objeto de ponto de Conexão de serviço que aponta para o nome de domínio verificado tooyour no AD do Azure na floresta Olá AD qual pertence o computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc09a-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="fc09a-142">Um usuário atingiu o limite de saudação de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="fc09a-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="fc09a-143">Consulte a Introdução ao registro de dispositivos do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc09a-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc09a-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc09a-144">Next steps</span></span>

<span data-ttu-id="fc09a-145">Para obter mais informações, consulte Olá [perguntas frequentes sobre o registro de dispositivo automático](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="fc09a-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
