---
title: "Olá de aaaManaging dispositivos usando o portal do Azure - visualização | Microsoft Docs"
description: "Saiba como toouse Olá dispositivos toomanage portal do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="12667-103">Gerenciamento de dispositivos usando Olá portal do Azure - visualização</span><span class="sxs-lookup"><span data-stu-id="12667-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="12667-104">Atualmente, essa capacidade está em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="12667-104">This capability currently is in public preview.</span></span> <span data-ttu-id="12667-105">Prepare-se toorevert ou remova as alterações.</span><span class="sxs-lookup"><span data-stu-id="12667-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="12667-106">recurso de saudação está disponível em qualquer assinatura do Azure Active Directory (AD do Azure) durante a visualização pública.</span><span class="sxs-lookup"><span data-stu-id="12667-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="12667-107">No entanto, quando o recurso de saudação se torna disponível, alguns aspectos do recurso de saudação podem exigir uma assinatura premium do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="12667-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="12667-108">Com o gerenciamento de dispositivos no Azure AD (Azure Active Directory), você pode garantir que os usuários acessem recursos usando dispositivos que atendam aos padrões de segurança e conformidade.</span><span class="sxs-lookup"><span data-stu-id="12667-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="12667-109">Este tópico:</span><span class="sxs-lookup"><span data-stu-id="12667-109">This topic:</span></span>

- <span data-ttu-id="12667-110">Pressupõe que você esteja familiarizado com hello [gerenciamento de toodevice de Introdução no Active Directory do Azure](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="12667-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="12667-111">Fornece informações sobre como gerenciar dispositivos usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="12667-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="12667-112">dispositivos toomanage Olá portal do Azure, você precisa tooclick **dispositivos** em Olá **gerenciar** seção Olá Olá **Active Directory do Azure** folha.</span><span class="sxs-lookup"><span data-stu-id="12667-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="12667-114">Definir configurações do dispositivo</span><span class="sxs-lookup"><span data-stu-id="12667-114">Configure device settings</span></span>

<span data-ttu-id="12667-115">toomanage seus dispositivos usando Olá portal do Azure, que precisam toobe registrado ou ingressou tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="12667-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="12667-116">Como administrador, você pode ajustar o processo de saudação de registro e ingresso de dispositivos, definindo configurações de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="12667-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="12667-118">folha de configurações de dispositivo Olá permite tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="12667-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="12667-119">**Os usuários podem ingressar seus dispositivos tooAzure AD** – essa configurações permite que usuários Olá tooselect podem unir dispositivos tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="12667-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="12667-120">saudação padrão é **todos os**.</span><span class="sxs-lookup"><span data-stu-id="12667-120">hello default is **All**.</span></span>

- <span data-ttu-id="12667-121">**Outros administradores locais no AD do Azure associado dispositivos** -você pode selecionar os usuários de saudação são concedidos direitos de administrador local em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12667-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="12667-122">Os usuários adicionados aqui são adicionados toohello *administradores do dispositivo* função no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="12667-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="12667-123">Os administradores globais no Azure AD e os proprietários do dispositivo recebem direitos de administrador local por padrão.</span><span class="sxs-lookup"><span data-stu-id="12667-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="12667-124">Essa opção é um recurso de edição premium disponível por meio de produtos como o Azure AD Premium Olá Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="12667-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="12667-125">**Os usuários podem registrar seus dispositivos com o Azure AD** -você precisa tooconfigure toobe de dispositivos de tooallow essa configuração registrado com o AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="12667-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="12667-126">Se você selecionar **nenhum**, dispositivos não são permitidos tooregister quando eles não são parte do AD do Azure ou híbrido do AD do Azure associado.</span><span class="sxs-lookup"><span data-stu-id="12667-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="12667-127">O registro com o Microsoft Intune ou o MDM (Gerenciamento de Dispositivo Móvel) para o Office 365 exige registro.</span><span class="sxs-lookup"><span data-stu-id="12667-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="12667-128">Se você tiver configurado qualquer um desses serviços, a opção **TODOS** estará selecionada e **NENHUM** não estará disponível.</span><span class="sxs-lookup"><span data-stu-id="12667-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="12667-129">**Exigir que os dispositivos do multi-Factor Auth toojoin** -você pode escolher se os usuários são necessária tooprovide uma autenticação de segundo fator toojoin tooAzure seu dispositivo AD.</span><span class="sxs-lookup"><span data-stu-id="12667-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="12667-130">saudação padrão é **não**.</span><span class="sxs-lookup"><span data-stu-id="12667-130">hello default is **No**.</span></span> <span data-ttu-id="12667-131">É recomendável exigir a autenticação multifator ao registrar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12667-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="12667-132">Antes de habilitar a autenticação multifator para este serviço, você deve garantir que a autenticação multifator está configurada para usuários de saudação que registrem seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="12667-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="12667-133">Para saber mais sobre os diferentes serviços de autenticação multifator do Azure, consulte [Introdução à autenticação multifator do Azure](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="12667-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="12667-134">**Número máximo de dispositivos** -essa configuração permite que você tooselect Olá alto número de dispositivos que um usuário pode ter no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="12667-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="12667-135">Se um usuário atingir essa cota, eles não são ser dispositivos adicionais tooadd capaz de até que um ou mais dos dispositivos existentes Olá são removidos.</span><span class="sxs-lookup"><span data-stu-id="12667-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="12667-136">aspas de dispositivo de saudação é contada para todos os dispositivos que estão unidas do AD do Azure ou AD do Azure registrado atualmente.</span><span class="sxs-lookup"><span data-stu-id="12667-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="12667-137">valor padrão de saudação é **20**.</span><span class="sxs-lookup"><span data-stu-id="12667-137">hello default value is **20**.</span></span>

- <span data-ttu-id="12667-138">**Os usuários podem sincronizar configurações e dados de aplicativo em dispositivos** -por padrão, essa configuração é definida muito**NONE**.</span><span class="sxs-lookup"><span data-stu-id="12667-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="12667-139">Selecionar usuários específicos ou grupos ou todos os permite do usuário Olá configurações e toosync de dados de aplicativo em seus dispositivos Windows 10.</span><span class="sxs-lookup"><span data-stu-id="12667-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="12667-140">Saiba mais sobre como a sincronização funciona no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="12667-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="12667-141">Essa opção é um recurso premium disponível por meio de produtos como o Azure AD Premium Olá Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="12667-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="12667-143">Localizar dispositivos</span><span class="sxs-lookup"><span data-stu-id="12667-143">Locate devices</span></span>

<span data-ttu-id="12667-144">Como administrador, Olá portal do Azure, você tem duas opções toolocate registraram e uniram dispositivos:</span><span class="sxs-lookup"><span data-stu-id="12667-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="12667-145">**Todos os dispositivos** em Olá **gerenciar** seção Olá **dispositivos** folha</span><span class="sxs-lookup"><span data-stu-id="12667-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![Todos os dispositivos](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="12667-147">**Dispositivos** em Olá **gerenciar** seção um **usuário** folha</span><span class="sxs-lookup"><span data-stu-id="12667-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![Todos os dispositivos](./media/device-management-azure-portal/43.png)



<span data-ttu-id="12667-149">Com ambas as opções, você pode ver tooa que:</span><span class="sxs-lookup"><span data-stu-id="12667-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="12667-150">Permite que você toosearch para dispositivos usando o nome de exibição hello como filtro.</span><span class="sxs-lookup"><span data-stu-id="12667-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="12667-151">Fornece visão geral detalhada de dispositivos registrados e associados</span><span class="sxs-lookup"><span data-stu-id="12667-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="12667-152">Permite que você tooperform tarefas comuns de gerenciamento de dispositivo</span><span class="sxs-lookup"><span data-stu-id="12667-152">Enables you tooperform common device management tasks</span></span>
   

![Todos os dispositivos](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="12667-154">Tarefas de gerenciamento de dispositivos</span><span class="sxs-lookup"><span data-stu-id="12667-154">Device management tasks</span></span>

<span data-ttu-id="12667-155">Como administrador, você pode gerenciar Olá registrado ou dispositivos ingressados no.</span><span class="sxs-lookup"><span data-stu-id="12667-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="12667-156">Esta seção fornece informações sobre tarefas comuns de gerenciamento de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12667-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="12667-157">**Gerenciar um dispositivo do Intune** – se você for um administrador do Intune, será possível gerenciar dispositivos marcados como **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="12667-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="12667-158">Um administrador pode ver dispositivos adicionais</span><span class="sxs-lookup"><span data-stu-id="12667-158">An administrator can see additional device</span></span> 

![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="12667-160">**Habilitar/desabilitar um dispositivo do Azure AD**</span><span class="sxs-lookup"><span data-stu-id="12667-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="12667-161">tooenable ou desativar um dispositivo, você precisa toobe um administrador global no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="12667-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="12667-162">Desabilitar um dispositivo impede que um dispositivo acesse seus recursos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12667-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="12667-163">dispositivo de saudação toodisable, você pode clicar em *...*</span><span class="sxs-lookup"><span data-stu-id="12667-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="12667-164">Clique em dispositivo Olá para obter detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="12667-164">click hello device for additional details.</span></span>

 
![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="12667-166">Desativar um dispositivo altera o estado de saudação em Olá **habilitado** coluna muito**não**.</span><span class="sxs-lookup"><span data-stu-id="12667-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![Desabilitar um dispositivo](./media/device-management-azure-portal/32.png)


<span data-ttu-id="12667-168">**Excluir um dispositivo do AD do Azure** -toodelete um dispositivo, você precisa toobe um administrador global no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="12667-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="12667-169">Excluindo um dispositivo:</span><span class="sxs-lookup"><span data-stu-id="12667-169">Deleting a device:</span></span>
 
- <span data-ttu-id="12667-170">Impede que um dispositivo acesse seus recursos do Azure AD</span><span class="sxs-lookup"><span data-stu-id="12667-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="12667-171">Remove todos os detalhes de dispositivo anexado toohello, por exemplo, chaves do BitLocker para dispositivos Windows</span><span class="sxs-lookup"><span data-stu-id="12667-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="12667-172">Representa uma atividade não recuperável e não é recomendável a menos que necessário</span><span class="sxs-lookup"><span data-stu-id="12667-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="12667-173">Se um dispositivo for gerenciado por outra autoridade de gerenciamento (por exemplo, o Microsoft Intune), verifique se esse dispositivo Olá tem foi apagado / desativado antes de excluir o dispositivo Olá no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="12667-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="12667-174">Você pode selecionar “…”</span><span class="sxs-lookup"><span data-stu-id="12667-174">You can either select “…”</span></span> <span data-ttu-id="12667-175">dispositivo de saudação toodelete ou clique no dispositivo Olá para obter detalhes adicionais</span><span class="sxs-lookup"><span data-stu-id="12667-175">toodelete hello device or click on hello device for additional details</span></span>
 
![Excluir um dispositivo](./media/device-management-azure-portal/34.png)


<span data-ttu-id="12667-177">**Exibir ou copiar a ID do dispositivo** -você pode usar o dispositivo ID tooverify Olá ID detalhes do dispositivo no dispositivo de saudação ou usando o PowerShell durante a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="12667-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="12667-178">tooaccess Olá cópia, clique em dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="12667-178">tooaccess hello copy option, click hello device.</span></span>

![Exibir uma ID do dispositivo](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="12667-180">**Exibir ou copiar as chaves do BitLocker** -se você for um administrador, você pode exibir hello cópia BitLocker chaves e toohelp usuários toorecover sua unidade criptografada.</span><span class="sxs-lookup"><span data-stu-id="12667-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="12667-181">Essas chaves só estão disponíveis para dispositivos Windows que são criptografados e têm suas chaves armazenadas no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12667-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="12667-182">Você pode copiar essas chaves ao acessar detalhes do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="12667-182">You can copy these keys when accessing details of hello device.</span></span>
 
![Exibir chaves do BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="12667-184">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="12667-184">Audit logs</span></span>


<span data-ttu-id="12667-185">atividades de dispositivo Olá estão disponíveis por meio de registros de atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="12667-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="12667-186">Isso inclui atividades disparadas pelo serviço de registro de dispositivo de saudação ou por usuário hello:</span><span class="sxs-lookup"><span data-stu-id="12667-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="12667-187">Criação de dispositivo e adicionar usuários/proprietários do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="12667-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="12667-188">Altera as configurações de toodevice</span><span class="sxs-lookup"><span data-stu-id="12667-188">Changes toodevice settings</span></span>

- <span data-ttu-id="12667-189">Operações de dispositivo como excluir ou atualizar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="12667-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="12667-190">O toohello de ponto de entrada dados de auditoria é **logs de auditoria** em Olá **atividade** seção hello **dispositivos* folha.</span><span class="sxs-lookup"><span data-stu-id="12667-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![Logs de auditoria](./media/device-management-azure-portal/61.png)


<span data-ttu-id="12667-192">Um log de auditoria tem um modo de exibição de lista padrão que mostra:</span><span class="sxs-lookup"><span data-stu-id="12667-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="12667-193">Data de saudação e a hora da ocorrência da saudação</span><span class="sxs-lookup"><span data-stu-id="12667-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="12667-194">destinos de saudação</span><span class="sxs-lookup"><span data-stu-id="12667-194">hello targets</span></span>

- <span data-ttu-id="12667-195">Olá iniciador / ator (que) de uma atividade</span><span class="sxs-lookup"><span data-stu-id="12667-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="12667-196">atividade de saudação (o que)</span><span class="sxs-lookup"><span data-stu-id="12667-196">hello activity (what)</span></span>

![Logs de auditoria](./media/device-management-azure-portal/63.png)

<span data-ttu-id="12667-198">Você pode personalizar o modo de exibição de lista Olá clicando **colunas** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="12667-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![Logs de auditoria](./media/device-management-azure-portal/64.png)


<span data-ttu-id="12667-200">toonarrow inativo saudação relatados nível tooa de dados que funciona para você, você pode filtrar os dados de auditoria hello usando Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="12667-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="12667-201">Categoria</span><span class="sxs-lookup"><span data-stu-id="12667-201">Catergory</span></span>
- <span data-ttu-id="12667-202">Tipo de recurso de atividade</span><span class="sxs-lookup"><span data-stu-id="12667-202">Activity resource type</span></span>
- <span data-ttu-id="12667-203">Atividade</span><span class="sxs-lookup"><span data-stu-id="12667-203">Activity</span></span>
- <span data-ttu-id="12667-204">Intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="12667-204">Date range</span></span>
- <span data-ttu-id="12667-205">Destino</span><span class="sxs-lookup"><span data-stu-id="12667-205">Target</span></span>
- <span data-ttu-id="12667-206">Iniciado por (ator)</span><span class="sxs-lookup"><span data-stu-id="12667-206">Initiated By (Actor)</span></span>

<span data-ttu-id="12667-207">Além disso toohello filtros, você pode procurar itens específicos.</span><span class="sxs-lookup"><span data-stu-id="12667-207">In addition toohello filters, you can search for specific entries.</span></span>

![Logs de auditoria](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="12667-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12667-209">Next steps</span></span>

* [<span data-ttu-id="12667-210">Gerenciamento de toodevice de Introdução no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="12667-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



