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
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="9d8bf-103">Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos de nível inferior</span><span class="sxs-lookup"><span data-stu-id="9d8bf-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="9d8bf-104">Este tópico é aplicável toohello somente dispositivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d8bf-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="9d8bf-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="9d8bf-105">Windows 7</span></span> 
- <span data-ttu-id="9d8bf-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="9d8bf-106">Windows 8.1</span></span> 
- <span data-ttu-id="9d8bf-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="9d8bf-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="9d8bf-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="9d8bf-108">Windows Server 2012</span></span> 
- <span data-ttu-id="9d8bf-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9d8bf-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="9d8bf-110">Para Windows 10 ou Windows Server 2016, confira [Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="9d8bf-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="9d8bf-111">Este tópico pressupõe que você tenha [dispositivos ingressados no configurado híbrida do Active Directory do Azure](device-management-hybrid-azuread-joined-devices-setup.md) Olá toosupport os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="9d8bf-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="9d8bf-112">Acesso condicional com base em dispositivo</span><span class="sxs-lookup"><span data-stu-id="9d8bf-112">Device-based conditional access</span></span>

- [<span data-ttu-id="9d8bf-113">Roaming corporativo de configurações</span><span class="sxs-lookup"><span data-stu-id="9d8bf-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="9d8bf-114">Configurar o Hello for Business</span><span class="sxs-lookup"><span data-stu-id="9d8bf-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="9d8bf-115">Este tópico fornece orientação sobre como tooresolve possíveis problemas de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="9d8bf-116">**O que você deve saber:**</span><span class="sxs-lookup"><span data-stu-id="9d8bf-116">**What you should know:**</span></span> 

- <span data-ttu-id="9d8bf-117">número máximo de saudação de dispositivos por usuário é centrada no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="9d8bf-118">Por exemplo, se *jdoe* e *jharnett* tooa entrar no dispositivo, um registro separado (DeviceID) é criado para cada um deles Olá **usuário** guia informações.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="9d8bf-119">Olá registro inicial / join de dispositivos é configurado tooperform uma tentativa de logon ou de bloqueio / desbloqueio.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="9d8bf-120">Pode haver um atraso de cinco minutos disparado por uma tarefa do agendador de tarefas.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="9d8bf-121">A reinstalação do sistema operacional de saudação ou manual cancela o registro e registrar novamente podem criar um novo registro no AD do Azure e resulta em várias entradas na guia de informações de usuário Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="9d8bf-122">Etapa 1: Recuperar o status de registro de saudação</span><span class="sxs-lookup"><span data-stu-id="9d8bf-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="9d8bf-123">**status do registro Olá tooverify:**</span><span class="sxs-lookup"><span data-stu-id="9d8bf-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="9d8bf-124">Olá abrir o prompt de comando como administrador</span><span class="sxs-lookup"><span data-stu-id="9d8bf-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="9d8bf-125">Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="9d8bf-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="9d8bf-126">Este comando exibe uma caixa de diálogo que fornece mais detalhes sobre o status de associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="9d8bf-128">Etapa 2: Avaliar o status de junção Olá híbrido do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9d8bf-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="9d8bf-129">Se ingresso no AD do Azure Olá híbrida não foi bem-sucedida, caixa de diálogo de saudação fornece detalhes sobre Olá problema ocorrido.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="9d8bf-130">**Olá os problemas mais comuns são:**</span><span class="sxs-lookup"><span data-stu-id="9d8bf-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="9d8bf-131">Um AD FS ou Azure AD configurado incorretamente</span><span class="sxs-lookup"><span data-stu-id="9d8bf-131">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="9d8bf-133">Você não está conectado como um usuário de domínio</span><span class="sxs-lookup"><span data-stu-id="9d8bf-133">You are not signed on as a domain user</span></span>

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="9d8bf-135">Você atingiu uma cota</span><span class="sxs-lookup"><span data-stu-id="9d8bf-135">A quota has been reached</span></span>

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="9d8bf-137">saudação de serviço não está respondendo</span><span class="sxs-lookup"><span data-stu-id="9d8bf-137">hello service is not responding</span></span> 

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="9d8bf-139">Você também pode encontrar informações de status de Olá no log de eventos de saudação em **aplicativos e serviços Log\Microsoft-ingresso**.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="9d8bf-140">**causas mais comuns de saudação para uma associação de AD do Azure híbrido com falha são:**</span><span class="sxs-lookup"><span data-stu-id="9d8bf-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="9d8bf-141">O computador não estiver no rede interna da organização hello ou uma VPN sem conexão tooan local controlador de domínio do AD.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="9d8bf-142">Você está conectado no computador tooyour com uma conta de computador local.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="9d8bf-143">Problemas de configuração do serviço:</span><span class="sxs-lookup"><span data-stu-id="9d8bf-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="9d8bf-144">Olá servidor de Federação foi configurado toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="9d8bf-145">Não há nenhum objeto de ponto de Conexão de serviço que aponta para o nome de domínio verificado tooyour no AD do Azure na floresta Olá AD qual pertence o computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="9d8bf-146">Um usuário atingiu o limite de saudação de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9d8bf-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9d8bf-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d8bf-147">Next steps</span></span>

<span data-ttu-id="9d8bf-148">Para perguntas, consulte Olá [perguntas frequentes sobre o gerenciamento de dispositivos](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="9d8bf-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
