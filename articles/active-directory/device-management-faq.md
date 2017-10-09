---
title: perguntas Frequentes do gerenciamento de dispositivo do Active Directory de aaaAzure | Microsoft Docs
description: Perguntas frequentes sobre o gerenciamento de dispositivos do Azure Active Directory.
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
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="ac72c-103">Perguntas frequentes sobre o gerenciamento de dispositivos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac72c-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="ac72c-104">**P: posso registrar o dispositivo de saudação recentemente. Por que não é possível ver dispositivo Olá em minhas informações de usuário no portal do Azure de saudação?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="ac72c-105">**R:** dispositivos Windows 10 que ingressaram no domínio com o registro automático do dispositivo não aparecem em informações de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ac72c-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="ac72c-106">É necessário toouse PowerShell toosee todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ac72c-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="ac72c-107">Somente hello seguintes dispositivos são listados na informação de usuário hello:</span><span class="sxs-lookup"><span data-stu-id="ac72c-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="ac72c-108">Todos os dispositivos pessoais que não são ingressados pela empresa</span><span class="sxs-lookup"><span data-stu-id="ac72c-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="ac72c-109">Todos os não Windows 10/Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ac72c-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="ac72c-110">Todos os dispositivos não Windows</span><span class="sxs-lookup"><span data-stu-id="ac72c-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="ac72c-111">**P: por que não posso ver todos os dispositivos de saudação registrados no Active Directory do Azure no portal do Azure de saudação?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="ac72c-112">**R:** atualmente, não há nenhuma maneira toosee todos os dispositivos registrados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac72c-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="ac72c-113">Você pode usar o Azure PowerShell toofind todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ac72c-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="ac72c-114">Para obter mais detalhes, consulte Olá [MsolDevice Get](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac72c-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="ac72c-115">**P: como posso saber quais estado do registro de dispositivo saudação do cliente Olá é?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="ac72c-116">**R:** depende do estado do registro de dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="ac72c-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="ac72c-117">Qual dispositivo Olá é</span><span class="sxs-lookup"><span data-stu-id="ac72c-117">What hello device is</span></span>
- <span data-ttu-id="ac72c-118">Como ele foi registrado</span><span class="sxs-lookup"><span data-stu-id="ac72c-118">How it was registered</span></span> 
- <span data-ttu-id="ac72c-119">Todos os detalhes relacionados tooit.</span><span class="sxs-lookup"><span data-stu-id="ac72c-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="ac72c-120">**P: por que é um dispositivo que tenha excluído no hello Azure portal ou usando o Windows PowerShell ainda listados como registrado?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="ac72c-121">**R:** Esse comportamento é intencional.</span><span class="sxs-lookup"><span data-stu-id="ac72c-121">**A:** This is by design.</span></span> <span data-ttu-id="ac72c-122">dispositivo Olá não terá acesso tooresources na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="ac72c-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="ac72c-123">Se você quiser tooremove Olá dispositivo e registrar novamente, uma ação manual deve ser toobe efetuado no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac72c-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="ac72c-124">Para Windows 10 e Windows Server 2016 que estão ingressados pelo domínio do AD local:</span><span class="sxs-lookup"><span data-stu-id="ac72c-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="ac72c-125">Olá abrir o prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="ac72c-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="ac72c-126">Digite `dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="ac72c-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="ac72c-127">Saia e entre em tootrigger Olá tarefa agendada que registra o dispositivo Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="ac72c-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="ac72c-128">Para outras plataformas Windows que estão ingressadas pelo domínio do AD local:</span><span class="sxs-lookup"><span data-stu-id="ac72c-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="ac72c-129">Olá abrir o prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="ac72c-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="ac72c-130">Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="ac72c-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="ac72c-131">Digite `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="ac72c-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="ac72c-132">**P: Por que vejo entradas de dispositivo duplicadas no Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="ac72c-133">**R:**</span><span class="sxs-lookup"><span data-stu-id="ac72c-133">**A:**</span></span>

-   <span data-ttu-id="ac72c-134">Para Windows 10 e Windows Server 2016, caso eles sejam repetidas tentativas toounjoin e una hello mesmo dispositivo, pode haver entradas duplicadas.</span><span class="sxs-lookup"><span data-stu-id="ac72c-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="ac72c-135">Se você tiver usado a adicionar conta corporativa ou escolar, cada usuário do windows que usa adicionar conta corporativa ou escolar criará um novo registro de dispositivo com hello mesmo nome de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac72c-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="ac72c-136">Outras plataformas do Windows que estão no local usando o registro automático ingressado no domínio do AD criará um novo registro de dispositivo com hello mesmo nome de dispositivo para cada usuário de domínio que faz logon em um dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac72c-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="ac72c-137">Uma máquina AADJ foi apagada, reinstalado e Unido novamente com hello mesmo nome, será mostrada como outro registro com hello mesmo nome de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac72c-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="ac72c-138">**P: por que um usuário ainda pode acessar recursos de um dispositivo que tenha desabilitado no hello portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="ac72c-139">**R:** pode levar até horas tooan para um toobe revoke aplicado.</span><span class="sxs-lookup"><span data-stu-id="ac72c-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="ac72c-140">Para dispositivos perdidos, recomendamos apagar Olá dispositivo tooensure que os usuários não poderão acessar o dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ac72c-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="ac72c-141">Para obter mais detalhes, consulte [Registrar dispositivos para gerenciamento no Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="ac72c-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="ac72c-142">**P: Por que meus usuários veem "Você não pode chegar lá daqui"?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="ac72c-143">**R:** se você configurou certa regras de acesso condicional toorequire um estado específico do dispositivo e dispositivo Olá não atendem aos critérios de hello, os usuários estão bloqueados e verá esta mensagem.</span><span class="sxs-lookup"><span data-stu-id="ac72c-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="ac72c-144">Avaliar regras hello e certifique-se de que o dispositivo Olá é capaz de toomeet Olá critérios tooavoid essa mensagem.</span><span class="sxs-lookup"><span data-stu-id="ac72c-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="ac72c-145">**P: posso ver Olá registro de dispositivo em informações de usuário Olá Olá portal do Azure e pode ver o estado de saudação conforme registrado no cliente de saudação. Estou configurado corretamente para usar o acesso condicional?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="ac72c-146">**R:** registro de dispositivo da saudação (deviceID) e o estado em Olá portal do Azure devem corresponder cliente hello e atender a qualquer critério de avaliação de acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="ac72c-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="ac72c-147">Para obter mais informações, consulte [Introdução ao registro de dispositivos do Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ac72c-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="ac72c-148">**P: por que recebo uma mensagem de "nome de usuário ou senha está incorreta" para um dispositivo tenha apenas Unido tooAzure AD?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="ac72c-149">**R:** As razões comuns para esse cenário são:</span><span class="sxs-lookup"><span data-stu-id="ac72c-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="ac72c-150">Suas credenciais de usuário não são mais válidas.</span><span class="sxs-lookup"><span data-stu-id="ac72c-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="ac72c-151">O computador está toocommunicate não é possível com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac72c-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="ac72c-152">Verifique se há problemas de conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="ac72c-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="ac72c-153">Olá junção do Azure AD pré-requisitos não foram atendidos.</span><span class="sxs-lookup"><span data-stu-id="ac72c-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="ac72c-154">Certifique-se de que você tiver seguido as etapas de saudação para [estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Azure Active Directory](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac72c-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="ac72c-155">Logons federados requer o servidor de Federação toosupport um ponto de extremidade do WS-Trust ativo.</span><span class="sxs-lookup"><span data-stu-id="ac72c-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="ac72c-156">**P: por que vejo hello "Opa... Ocorreu um erro!" caixa de diálogo quando tento ingressar em Meu computador?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="ac72c-157">**R:** Esse é um resultado da configuração de registro do Azure Active Directory como Intune.</span><span class="sxs-lookup"><span data-stu-id="ac72c-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="ac72c-158">Para obter mais detalhes, consulte [Configurar o gerenciamento do dispositivo Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="ac72c-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="ac72c-159">**P: por que meu toojoin de tentativa de um computador falhar, embora não recebi qualquer informação de erro?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="ac72c-160">**R:** uma causa provável é que esse usuário Olá é registrado no dispositivo toohello usando a conta de administrador interno hello.</span><span class="sxs-lookup"><span data-stu-id="ac72c-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="ac72c-161">Crie uma conta local diferente antes de usar a instalação de saudação toocomplete a junção do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac72c-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="ac72c-162">**P: onde posso encontrar instruções de instalação de saudação do registro automático do dispositivo?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="ac72c-163">**R:** para obter instruções detalhadas, consulte [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="ac72c-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="ac72c-164">**P: onde encontrar a solução de problemas informações sobre o registro de dispositivo automático Olá?**</span><span class="sxs-lookup"><span data-stu-id="ac72c-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="ac72c-165">**R:** Para encontrar informações de solução de problemas, consulte:</span><span class="sxs-lookup"><span data-stu-id="ac72c-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="ac72c-166">Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ac72c-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="ac72c-167">Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD para clientes de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="ac72c-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

