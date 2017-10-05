---
title: "Perguntas frequentes sobre o registro automático de dispositivo do Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 29751239ae2a26cd7b07ddd0d8a8e706d4056b68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="6edcb-103">Perguntas frequentes sobre o registro automático de dispositivo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6edcb-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="6edcb-104">**P: Registrei o dispositivo recentemente. Por que não consigo ver o dispositivo em minhas informações de usuário no Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="6edcb-105">**R:** Dispositivos Windows 10 que ingressaram no domínio com o registro de dispositivo automático não aparecem nas informações de usuário.</span><span class="sxs-lookup"><span data-stu-id="6edcb-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="6edcb-106">Você precisa usar o PowerShell para ver todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="6edcb-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="6edcb-107">Apenas os seguintes dispositivos são listados nas informações de usuário:</span><span class="sxs-lookup"><span data-stu-id="6edcb-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="6edcb-108">Todos os dispositivos pessoais que não são ingressados pela empresa</span><span class="sxs-lookup"><span data-stu-id="6edcb-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="6edcb-109">Todos os não Windows 10/Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6edcb-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="6edcb-110">Todos os dispositivos não Windows</span><span class="sxs-lookup"><span data-stu-id="6edcb-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="6edcb-111">**P: Por que não posso ver todos os dispositivos registrados no Azure Active Directory no Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="6edcb-112">**R:** Atualmente, não há nenhuma maneira de ver todos os dispositivos registrados no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6edcb-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="6edcb-113">Você pode usar o Azure PowerShell para localizar todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="6edcb-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="6edcb-114">Para obter mais detalhes, consulte o cmdlet [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="6edcb-114">For more details, see the [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="6edcb-115">**P: Como saber qual é o estado de registro do dispositivo do cliente?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="6edcb-116">**R:** O estado de registro do dispositivo depende de:</span><span class="sxs-lookup"><span data-stu-id="6edcb-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="6edcb-117">O que é o dispositivo</span><span class="sxs-lookup"><span data-stu-id="6edcb-117">What the device is</span></span>
- <span data-ttu-id="6edcb-118">Como ele foi registrado</span><span class="sxs-lookup"><span data-stu-id="6edcb-118">How it was registered</span></span> 
- <span data-ttu-id="6edcb-119">Todos os detalhes relacionados a ele.</span><span class="sxs-lookup"><span data-stu-id="6edcb-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="6edcb-120">**P: Por que um dispositivo que eu excluí no Portal do Azure ou usando o Windows PowerShell ainda está listado como registrado?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="6edcb-121">**R:** Esse comportamento é intencional.</span><span class="sxs-lookup"><span data-stu-id="6edcb-121">**A:** This is by design.</span></span> <span data-ttu-id="6edcb-122">O dispositivo não terá acesso aos recursos na nuvem.</span><span class="sxs-lookup"><span data-stu-id="6edcb-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="6edcb-123">Se você quiser remover o dispositivo e registre novamente, uma ação manual deve ser a ser executada no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6edcb-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="6edcb-124">Para Windows 10 e Windows Server 2016 que estão ingressados pelo domínio do AD local:</span><span class="sxs-lookup"><span data-stu-id="6edcb-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="6edcb-125">Abra o prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="6edcb-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="6edcb-126">Digite `dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="6edcb-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="6edcb-127">Sair e entrar para disparar a tarefa agendada que registra o dispositivo novamente.</span><span class="sxs-lookup"><span data-stu-id="6edcb-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="6edcb-128">Para outras plataformas Windows que estão ingressadas pelo domínio do AD local:</span><span class="sxs-lookup"><span data-stu-id="6edcb-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="6edcb-129">Abra o prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="6edcb-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="6edcb-130">Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="6edcb-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="6edcb-131">Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="6edcb-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="6edcb-132">**P: Por que vejo entradas de dispositivo duplicadas no Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="6edcb-133">**R:**</span><span class="sxs-lookup"><span data-stu-id="6edcb-133">**A:**</span></span>

-   <span data-ttu-id="6edcb-134">Para Windows 10 e Windows Server 2016, se houver tentativas repetidas de cancelar o ingresso e ingressar novamente o mesmo dispositivo, poderá haver entradas duplicadas.</span><span class="sxs-lookup"><span data-stu-id="6edcb-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="6edcb-135">Se você tiver usado Adicionar Conta Corporativa ou de Estudante, cada usuário do Windows que usar Adicionar Conta Corporativa ou de Estudante criará um novo registro do dispositivo com o mesmo nome do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6edcb-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="6edcb-136">Outras plataformas Windows que são ingressadas pelo domínio do AD local usando o registro automático criarão um novo registro de dispositivo com o mesmo nome do dispositivo para cada usuário de domínio que faça logon no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6edcb-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="6edcb-137">Um computador AADJ que foi apagado, reinstalado e reingressado com o mesmo nome aparecerá como outro registro com o mesmo nome do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6edcb-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="6edcb-138">**P: Por que um usuário ainda pode acessar recursos de um dispositivo que eu desabilitei no Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="6edcb-139">**R:** Pode demorar até uma hora para uma revogação ser aplicada.</span><span class="sxs-lookup"><span data-stu-id="6edcb-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="6edcb-140">Para dispositivos perdidos, recomendamos apagar o dispositivo para garantir que os usuários não possam acessar o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6edcb-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="6edcb-141">Para obter mais detalhes, consulte [Registrar dispositivos para gerenciamento no Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="6edcb-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="6edcb-142">**P: Por que meus usuários veem "Você não pode chegar lá daqui"?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="6edcb-143">**R:** Se você tiver configurado certas regras de acesso condicional para exigir um estado de dispositivo específico e o dispositivo não atender aos critérios, os usuários serão bloqueados e verão esta mensagem.</span><span class="sxs-lookup"><span data-stu-id="6edcb-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="6edcb-144">Avalie as regras e verifique se o dispositivo é capaz de atender aos critérios para evitar esta mensagem.</span><span class="sxs-lookup"><span data-stu-id="6edcb-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="6edcb-145">**P: Posso ver o registro de dispositivo nas informações do usuário no Portal do Azure e posso ver o estado como registrado no cliente. Estou configurado corretamente para usar o acesso condicional?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="6edcb-146">**R:** O registro do dispositivo (deviceID) e o estado no Portal do Azure devem corresponder ao cliente e atender a todos os critérios de avaliação para acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="6edcb-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="6edcb-147">Para obter mais informações, consulte [Introdução ao registro de dispositivos do Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6edcb-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="6edcb-148">**P: Por que recebo uma mensagem de "nome de usuário ou senha está incorreta" para um dispositivo que acabei de ingressar no Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="6edcb-149">**R:** As razões comuns para esse cenário são:</span><span class="sxs-lookup"><span data-stu-id="6edcb-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="6edcb-150">Suas credenciais de usuário não são mais válidas.</span><span class="sxs-lookup"><span data-stu-id="6edcb-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="6edcb-151">O computador não pode se comunicar com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6edcb-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="6edcb-152">Verifique se há problemas de conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="6edcb-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="6edcb-153">Os pré-requisitos de Ingresso no Azure AD não foram atendidos.</span><span class="sxs-lookup"><span data-stu-id="6edcb-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="6edcb-154">Certifique-se de ter seguido as etapas de [Estendendo os recursos de nuvem para dispositivos Windows 10 por meio da Ingresso do Azure Active Directory](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6edcb-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="6edcb-155">Os logons federados requerem que o servidor de federação dê suporte a um ponto de extremidade WS-Trust ativo.</span><span class="sxs-lookup"><span data-stu-id="6edcb-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="6edcb-156">**P: Por que vejo a caixa de diálogo "Ocorreu um erro" quando tento ingressar meu computador?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="6edcb-157">**R:** Esse é um resultado da configuração de registro do Azure Active Directory como Intune.</span><span class="sxs-lookup"><span data-stu-id="6edcb-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="6edcb-158">Para obter mais detalhes, consulte [Configurar o gerenciamento do dispositivo Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="6edcb-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="6edcb-159">**P: Por que minha tentativa de ingressar um computador falhou embora eu não tenha obtido nenhuma informação de erro?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="6edcb-160">**R:** Uma causa provável é que o usuário está conectado ao dispositivo usando a conta de administrador interno.</span><span class="sxs-lookup"><span data-stu-id="6edcb-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="6edcb-161">Crie uma conta local diferente antes de usar o Ingresso do Azure Active Directory para concluir a configuração.</span><span class="sxs-lookup"><span data-stu-id="6edcb-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="6edcb-162">**P: onde posso encontrar instruções para a configuração de registro automático do dispositivo?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="6edcb-163">**R:** Para obter as instruções detalhadas, confira [Como configurar o registro automático de dispositivos ingressados no domínio do Windows com o Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="6edcb-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="6edcb-164">**P: Onde posso encontrar informações de solução de problemas sobre o registro de dispositivo automático?**</span><span class="sxs-lookup"><span data-stu-id="6edcb-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="6edcb-165">**R:** Para encontrar informações de solução de problemas, consulte:</span><span class="sxs-lookup"><span data-stu-id="6edcb-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="6edcb-166">Solução de problemas de registro automático de computadores ingressados no domínio do Azure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6edcb-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="6edcb-167">Solução de problemas com o registro automático de computadores ingressados no domínio do Azure AD para clientes de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="6edcb-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

