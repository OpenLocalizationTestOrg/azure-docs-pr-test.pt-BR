---
title: "Solução de problemas com o registro automático de computadores ingressados no domínio do Azure AD para clientes de nível inferior do Windows | Microsoft Docs"
description: "Solução de problemas com o registro automático de computadores ingressados no domínio do Azure AD para clientes de nível inferior do Windows."
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
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="ce669-103">Solução de problemas com o registro automático de computadores ingressados no domínio do Azure AD para clientes de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="ce669-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="ce669-104">Este tópico é aplicável apenas aos seguintes clientes:</span><span class="sxs-lookup"><span data-stu-id="ce669-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="ce669-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="ce669-105">Windows 7</span></span> 
- <span data-ttu-id="ce669-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ce669-106">Windows 8.1</span></span> 
- <span data-ttu-id="ce669-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="ce669-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="ce669-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ce669-108">Windows Server 2012</span></span> 
- <span data-ttu-id="ce669-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ce669-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="ce669-110">Para o Windows 10 ou o Windows Server 2016, confira [Solução de problemas do registro automático de computadores ingressados no domínio para o Azure AD – Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ce669-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="ce669-111">Este tópico pressupõe que você tenha configurado o registro automático de dispositivos ingressados no domínio conforme descrito em [Como configurar o registro automático de dispositivos ingressados no domínio do Windows com o Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ce669-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="ce669-112">Este tópico fornece orientação para solução de possíveis problemas.</span><span class="sxs-lookup"><span data-stu-id="ce669-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="ce669-113">Para ter resultados bem-sucedidos, fique atento ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="ce669-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="ce669-114">O registro desses clientes no Azure AD ocorre por dispositivo/usuário.</span><span class="sxs-lookup"><span data-stu-id="ce669-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="ce669-115">Por exemplo: se jdoe e jharnett efetuarem logon no dispositivo, um registro separado (DeviceID) será criado para cada um desses usuários na guia Informações do USUÁRIO.</span><span class="sxs-lookup"><span data-stu-id="ce669-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="ce669-116">O registro desses clientes prontos para uso é configurado para ser tentado durante o logon ou durante um bloqueio/desbloqueio, e pode haver atraso de cinco minutos desde o disparo por meio de uma tarefa do Agendador de Tarefas.</span><span class="sxs-lookup"><span data-stu-id="ce669-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="ce669-117">Uma reinstalação do sistema operacional, ou um cancelamento manual do registro seguido por um novo registro, pode criar um novo registro no Azure AD e resultará em várias entradas na guia Informações do USUÁRIO no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce669-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="ce669-118">Etapa 1: Recuperar o status do registro</span><span class="sxs-lookup"><span data-stu-id="ce669-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="ce669-119">**ara verificar o status do registro:**</span><span class="sxs-lookup"><span data-stu-id="ce669-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="ce669-120">Abra o prompt de comando como administrador</span><span class="sxs-lookup"><span data-stu-id="ce669-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="ce669-121">Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="ce669-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="ce669-122">Esse comando exibe uma caixa de diálogo que fornece mais detalhes sobre o status do ingresso.</span><span class="sxs-lookup"><span data-stu-id="ce669-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="ce669-124">Etapa 2: Avaliar o status do registro</span><span class="sxs-lookup"><span data-stu-id="ce669-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="ce669-125">Se o ingresso não tiver sido bem-sucedido, a caixa de diálogo fornecerá detalhes sobre o problema.</span><span class="sxs-lookup"><span data-stu-id="ce669-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="ce669-126">**As tarefas mais comuns são:**</span><span class="sxs-lookup"><span data-stu-id="ce669-126">**The most common issues are:**</span></span>

- <span data-ttu-id="ce669-127">Um AD FS ou Azure AD configurado incorretamente</span><span class="sxs-lookup"><span data-stu-id="ce669-127">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="ce669-129">Você não está conectado como um usuário de domínio</span><span class="sxs-lookup"><span data-stu-id="ce669-129">You are not signed on as a domain user</span></span>

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="ce669-131">Você atingiu uma cota</span><span class="sxs-lookup"><span data-stu-id="ce669-131">A quota has been reached</span></span>

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="ce669-133">O serviço não está respondendo</span><span class="sxs-lookup"><span data-stu-id="ce669-133">The service is not responding</span></span> 

    ![Workplace Join para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="ce669-135">Também é possível encontrar informações de status no log de eventos em **Log de Aplicativos e Serviços\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="ce669-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="ce669-136">**As causas mais comuns para um registro com falha são:**</span><span class="sxs-lookup"><span data-stu-id="ce669-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="ce669-137">O computador não está na rede interna da organização, ou está em uma VPN sem uma conexão com um controlador de domínio do AD local.</span><span class="sxs-lookup"><span data-stu-id="ce669-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="ce669-138">Você está conectado ao computador com uma conta de computador local.</span><span class="sxs-lookup"><span data-stu-id="ce669-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="ce669-139">Problemas de configuração do serviço:</span><span class="sxs-lookup"><span data-stu-id="ce669-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="ce669-140">O servidor de Federação foi configurado para oferecer suporte a **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="ce669-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="ce669-141">Não há nenhum objeto de Ponto de Conexão de Serviço que aponta para o seu nome de domínio verificado no Azure AD na floresta do AD à qual o computador pertence.</span><span class="sxs-lookup"><span data-stu-id="ce669-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="ce669-142">Um usuário atingiu o limite de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ce669-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="ce669-143">Consulte a Introdução ao registro de dispositivos do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ce669-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce669-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce669-144">Next steps</span></span>

<span data-ttu-id="ce669-145">Para saber mais, veja [Perguntas frequentes sobre o registro de dispositivo automático](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="ce669-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
