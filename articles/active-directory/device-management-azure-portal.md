---
title: "Gerenciar dispositivos usando o portal do Azure – versão prévia | Microsoft Docs"
description: Saiba como usar o portal do Azure para gerenciar dispositivos.
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
ms.openlocfilehash: 4b46e1627a229b0649d9ccd2550cd28fda9849f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-devices-using-the-azure-portal---preview"></a><span data-ttu-id="e2646-103">Gerenciar dispositivos usando o portal do Azure – versão prévia</span><span class="sxs-lookup"><span data-stu-id="e2646-103">Managing devices using the Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="e2646-104">Atualmente, essa capacidade está em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="e2646-104">This capability currently is in public preview.</span></span> <span data-ttu-id="e2646-105">Esteja preparado para reverter ou remover quaisquer alterações.</span><span class="sxs-lookup"><span data-stu-id="e2646-105">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="e2646-106">O recurso está disponível em qualquer assinatura do Azure AD (Azure Active Directory) durante a visualização pública.</span><span class="sxs-lookup"><span data-stu-id="e2646-106">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="e2646-107">No entanto, quando o recurso for disponibilizado para todos, alguns aspectos dele poderão exigir uma assinatura do Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="e2646-107">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="e2646-108">Com o gerenciamento de dispositivos no Azure AD (Azure Active Directory), você pode garantir que os usuários acessem recursos usando dispositivos que atendam aos padrões de segurança e conformidade.</span><span class="sxs-lookup"><span data-stu-id="e2646-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="e2646-109">Este tópico:</span><span class="sxs-lookup"><span data-stu-id="e2646-109">This topic:</span></span>

- <span data-ttu-id="e2646-110">Assuma que você está familiarizado com a [Introdução ao gerenciamento de dispositivos no Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="e2646-110">Assumes that you are familiar with the [introduction to device management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="e2646-111">Fornece informações sobre como gerenciar dispositivos usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e2646-111">Provides you with information about managing your devices using the Azure portal</span></span>


<span data-ttu-id="e2646-112">Para gerenciar dispositivos no portal do Azure, é necessário clicar em **Dispositivos** na seção **Gerenciar** da folha **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2646-112">To manage devices in the Azure portal, you need to click **Devices** in the **Manage** section of the the **Azure Active Directory** blade.</span></span>

![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="e2646-114">Definir configurações do dispositivo</span><span class="sxs-lookup"><span data-stu-id="e2646-114">Configure device settings</span></span>

<span data-ttu-id="e2646-115">Para gerenciar seus dispositivos usando o portal do Azure, eles precisam ser registrados ou associados ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-115">To manage your devices using the Azure portal, they need to be either registered or joined to Azure AD.</span></span> <span data-ttu-id="e2646-116">Como administrador, você pode ajustar o processo de registro e ingresso de dispositivos definindo as configurações do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2646-116">As an administrator, you can fine-tune the process of registering and joining devices by configuring the device settings.</span></span>

![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="e2646-118">A folha de configurações do dispositivo permite que você configure:</span><span class="sxs-lookup"><span data-stu-id="e2646-118">The device settings blade enables you to configure:</span></span>

- <span data-ttu-id="e2646-119">**Os usuários podem associar seus dispositivos ao Azure AD** – essas configurações permitem que você selecione os usuários que podem associar dispositivos ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-119">**Users may join devices to Azure AD** - This settings enables you to select the users who can join devices to Azure AD.</span></span> <span data-ttu-id="e2646-120">O padrão é **Todos**.</span><span class="sxs-lookup"><span data-stu-id="e2646-120">The default is **All**.</span></span>

- <span data-ttu-id="e2646-121">**Outros administradores locais nos dispositivos associados ao Azure AD** – você pode selecionar os usuários que têm direitos de administrador local em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2646-121">**Additional local administrators on Azure AD joined devices** - You can select the users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="e2646-122">Os usuários adicionados aqui são adicionados à função *Administradores do dispositivo* no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-122">Users added here are added to the *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="e2646-123">Os administradores globais no Azure AD e os proprietários do dispositivo recebem direitos de administrador local por padrão.</span><span class="sxs-lookup"><span data-stu-id="e2646-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="e2646-124">Essa opção é uma funcionalidade Premium Edition disponível por meio de produtos como o Azure AD Premium ou o EMS (Enterprise Mobility Suite).</span><span class="sxs-lookup"><span data-stu-id="e2646-124">This option is a premium edition capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="e2646-125">**Os usuários podem registrar seus dispositivos com o Azure AD** – você precisa definir essa configuração para permitir que dispositivos sejam registrados com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-125">**Users may register their devices with Azure AD** - You need to configure this setting to allow devices to be registered with Azure AD.</span></span> <span data-ttu-id="e2646-126">Se você selecionar **Nenhum**, os dispositivos não terão permissão para registro quando eles não forem associados ao Azure AD ou não forem associados ao Azure AD híbrido.</span><span class="sxs-lookup"><span data-stu-id="e2646-126">If you select **None**, devices are not allowed to register when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="e2646-127">O registro com o Microsoft Intune ou o MDM (Gerenciamento de Dispositivo Móvel) para o Office 365 exige registro.</span><span class="sxs-lookup"><span data-stu-id="e2646-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="e2646-128">Se você tiver configurado qualquer um desses serviços, a opção **TODOS** estará selecionada e **NENHUM** não estará disponível.</span><span class="sxs-lookup"><span data-stu-id="e2646-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="e2646-129">**Exigir autenticação multifator para associar dispositivos** – é possível definir se os usuários devem precisar fornecer um segundo fator de autenticação para associar seu dispositivo ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-129">**Require Multi-Factor Auth to join devices** - You can choose whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="e2646-130">O padrão é **Não**.</span><span class="sxs-lookup"><span data-stu-id="e2646-130">The default is **No**.</span></span> <span data-ttu-id="e2646-131">É recomendável exigir a autenticação multifator ao registrar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2646-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="e2646-132">Antes de habilitar a autenticação multifator para este serviço, você deve garantir que a autenticação multifator esteja configurada para os usuários que registram seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e2646-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for the users that register their devices.</span></span> <span data-ttu-id="e2646-133">Para saber mais sobre os diferentes serviços de autenticação multifator do Azure, consulte [Introdução à autenticação multifator do Azure](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e2646-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="e2646-134">**Número máximo de dispositivos** – essa configuração permite selecionar o número máximo de dispositivos que um usuário pode ter no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-134">**Maximum number of devices** - This setting enables you to select the maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="e2646-135">Se um usuário atingir esta cota, ele não poderá adicionar mais dispositivos até que um ou mais dos seus dispositivos existentes sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="e2646-135">If a user reaches this quota, they are not be able to add additional devices until one or more of the existing devices are removed.</span></span> <span data-ttu-id="e2646-136">A cotação de dispositivo é contada para todos os dispositivos que estão associados ao Azure AD ou registrados no Azure AD atualmente.</span><span class="sxs-lookup"><span data-stu-id="e2646-136">The device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="e2646-137">O valor padrão é **20**.</span><span class="sxs-lookup"><span data-stu-id="e2646-137">The default value is **20**.</span></span>

- <span data-ttu-id="e2646-138">**Os usuários podem sincronizar configurações e dados de aplicativo em dispositivos** – por padrão, essa configuração é definida como **NENHUM**.</span><span class="sxs-lookup"><span data-stu-id="e2646-138">**Users may sync settings and app data across devices** - By default, this setting is set to **NONE**.</span></span> <span data-ttu-id="e2646-139">Selecionar usuários específicos ou grupos ou TODOS permite que as configurações do usuário e os dados de aplicativo sejam sincronizados em seus dispositivos Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e2646-139">Selecting specific users or groups or ALL allows the user’s settings and app data to sync across their Windows 10 devices.</span></span> <span data-ttu-id="e2646-140">Saiba mais sobre como a sincronização funciona no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e2646-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="e2646-141">Essa opção é uma funcionalidade premium disponível por meio de produtos como o Azure AD Premium ou o EMS (Enterprise Mobility Suite).</span><span class="sxs-lookup"><span data-stu-id="e2646-141">This option is a premium capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span>
 
    ![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="e2646-143">Localizar dispositivos</span><span class="sxs-lookup"><span data-stu-id="e2646-143">Locate devices</span></span>

<span data-ttu-id="e2646-144">Como administrador, no portal do Azure, você tem duas opções para localizar dispositivos registrados e associados:</span><span class="sxs-lookup"><span data-stu-id="e2646-144">As an administrator, in the Azure portal, you have two options to locate registered and joined devices:</span></span>

- <span data-ttu-id="e2646-145">**Todos os dispositivos** na seção **Gerenciar** da folha **Dispositivos**</span><span class="sxs-lookup"><span data-stu-id="e2646-145">**All devices** in the **Manage** section of the **Devices** blade</span></span>  

    ![Todos os dispositivos](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="e2646-147">**Dispositivos** na seção **Gerenciar** de uma folha **Usuário**</span><span class="sxs-lookup"><span data-stu-id="e2646-147">**Devices** in the **Manage** section of a **User** blade</span></span>
 
    ![Todos os dispositivos](./media/device-management-azure-portal/43.png)



<span data-ttu-id="e2646-149">Com as duas opções, você pode obter uma exibição que:</span><span class="sxs-lookup"><span data-stu-id="e2646-149">With both options, you can get to a view that:</span></span>


- <span data-ttu-id="e2646-150">Permite pesquisar dispositivos usando o nome de exibição como filtro.</span><span class="sxs-lookup"><span data-stu-id="e2646-150">Enables you to search for devices using the display name as filter.</span></span>

- <span data-ttu-id="e2646-151">Fornece visão geral detalhada de dispositivos registrados e associados</span><span class="sxs-lookup"><span data-stu-id="e2646-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="e2646-152">Permite que você execute tarefas comuns de gerenciamento de dispositivo</span><span class="sxs-lookup"><span data-stu-id="e2646-152">Enables you to perform common device management tasks</span></span>
   

![Todos os dispositivos](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="e2646-154">Tarefas de gerenciamento de dispositivos</span><span class="sxs-lookup"><span data-stu-id="e2646-154">Device management tasks</span></span>

<span data-ttu-id="e2646-155">Como administrador, você pode gerenciar os dispositivos registrados ou associados.</span><span class="sxs-lookup"><span data-stu-id="e2646-155">As an administrator, you can manage the registered or joined devices.</span></span> <span data-ttu-id="e2646-156">Esta seção fornece informações sobre tarefas comuns de gerenciamento de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2646-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="e2646-157">**Gerenciar um dispositivo do Intune** – se você for um administrador do Intune, será possível gerenciar dispositivos marcados como **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="e2646-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="e2646-158">Um administrador pode ver dispositivos adicionais</span><span class="sxs-lookup"><span data-stu-id="e2646-158">An administrator can see additional device</span></span> 

![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="e2646-160">**Habilitar/desabilitar um dispositivo do Azure AD**</span><span class="sxs-lookup"><span data-stu-id="e2646-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="e2646-161">Para habilitar ou desabilitar um dispositivo, você precisa ser um administrador global no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-161">To enable or disable a device, you need to be a global administrator in Azure  AD.</span></span> <span data-ttu-id="e2646-162">Desabilitar um dispositivo impede que um dispositivo acesse seus recursos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="e2646-163">Para desabilitar o dispositivo, você pode clicar em *...*</span><span class="sxs-lookup"><span data-stu-id="e2646-163">To disable the device, you can either click *…*</span></span> <span data-ttu-id="e2646-164">clique no dispositivo para detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="e2646-164">click the device for additional details.</span></span>

 
![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="e2646-166">Desabilitar um dispositivo altera o estado na coluna **HABILITADO** para **Não**.</span><span class="sxs-lookup"><span data-stu-id="e2646-166">Disabling a device changes the state in the **ENABLED** column to **No**.</span></span>

![Desabilitar um dispositivo](./media/device-management-azure-portal/32.png)


<span data-ttu-id="e2646-168">**Excluir um dispositivo Azure AD** – para excluir um dispositivo, você precisa ser um administrador global no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-168">**Delete an Azure AD device** - To delete a device, you need to be a global administrator in Azure AD.</span></span>  
<span data-ttu-id="e2646-169">Excluindo um dispositivo:</span><span class="sxs-lookup"><span data-stu-id="e2646-169">Deleting a device:</span></span>
 
- <span data-ttu-id="e2646-170">Impede que um dispositivo acesse seus recursos do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2646-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="e2646-171">Remove todos os detalhes que estão relacionados ao dispositivo, por exemplo, chaves do BitLocker para dispositivos Windows</span><span class="sxs-lookup"><span data-stu-id="e2646-171">Removes all details that are attached to the device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="e2646-172">Representa uma atividade não recuperável e não é recomendável a menos que necessário</span><span class="sxs-lookup"><span data-stu-id="e2646-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="e2646-173">Se um dispositivo for gerenciado por outra autoridade de gerenciamento (por exemplo, o Microsoft Intune), certifique-se de que o dispositivo foi apagado/desativado antes de excluir o dispositivo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that the device has been wiped / retired before deleting the device in Azure AD.</span></span>

<span data-ttu-id="e2646-174">Você pode selecionar “…”</span><span class="sxs-lookup"><span data-stu-id="e2646-174">You can either select “…”</span></span> <span data-ttu-id="e2646-175">para excluir o dispositivo ou clicar no dispositivo para obter detalhes adicionais</span><span class="sxs-lookup"><span data-stu-id="e2646-175">to delete the device or click on the device for additional details</span></span>
 
![Excluir um dispositivo](./media/device-management-azure-portal/34.png)


<span data-ttu-id="e2646-177">**Exibir ou copiar a ID do dispositivo** – você pode usar uma ID de dispositivo para verificar os detalhes de ID de dispositivo no dispositivo ou usar o PowerShell durante a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="e2646-177">**View or copy device ID** - You can use a device ID to verify the device ID details on the device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="e2646-178">Para acessar a opção de cópia, clique no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2646-178">To access the copy option, click the device.</span></span>

![Exibir uma ID do dispositivo](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="e2646-180">**Exibir ou copiar as chaves do BitLocker** – se você for um administrador, será possível exibir e copiar as chaves do BitLocker para ajudar os usuários a recuperar sua unidade criptografada.</span><span class="sxs-lookup"><span data-stu-id="e2646-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy the BitLocker keys to help users to recover their encrypted drive.</span></span> <span data-ttu-id="e2646-181">Essas chaves só estão disponíveis para dispositivos Windows que são criptografados e têm suas chaves armazenadas no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2646-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="e2646-182">Você pode copiar essas chaves ao acessar detalhes do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2646-182">You can copy these keys when accessing details of the device.</span></span>
 
![Exibir chaves do BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="e2646-184">Logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="e2646-184">Audit logs</span></span>


<span data-ttu-id="e2646-185">As atividades de dispositivo estão disponíveis por meio dos logs de atividade.</span><span class="sxs-lookup"><span data-stu-id="e2646-185">The device activities are available through the activity logs.</span></span> <span data-ttu-id="e2646-186">Isso inclui atividades acionadas pelo serviço de registro do dispositivo ou pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="e2646-186">This includes activities triggered by the device registration service or by the user:</span></span>

- <span data-ttu-id="e2646-187">Criação de dispositivo e adição de usuários/proprietários no dispositivo</span><span class="sxs-lookup"><span data-stu-id="e2646-187">Device creation and adding owners/users on the device</span></span>

- <span data-ttu-id="e2646-188">Alterações nas configurações do dispositivo</span><span class="sxs-lookup"><span data-stu-id="e2646-188">Changes to device settings</span></span>

- <span data-ttu-id="e2646-189">Operações de dispositivo como excluir ou atualizar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="e2646-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="e2646-190">O ponto de entrada para os dados de auditoria é **Logs de auditoria**, na seção **Atividade** da folha **Dispositivos*.</span><span class="sxs-lookup"><span data-stu-id="e2646-190">Your entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices* blade.</span></span>

![Logs de auditoria](./media/device-management-azure-portal/61.png)


<span data-ttu-id="e2646-192">Um log de auditoria tem um modo de exibição de lista padrão que mostra:</span><span class="sxs-lookup"><span data-stu-id="e2646-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="e2646-193">a data e a hora da ocorrência</span><span class="sxs-lookup"><span data-stu-id="e2646-193">the date and time of the occurrence</span></span>

- <span data-ttu-id="e2646-194">os destinos</span><span class="sxs-lookup"><span data-stu-id="e2646-194">the targets</span></span>

- <span data-ttu-id="e2646-195">o iniciador/ator (quem) de uma atividade</span><span class="sxs-lookup"><span data-stu-id="e2646-195">the initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="e2646-196">a atividade (o quê)</span><span class="sxs-lookup"><span data-stu-id="e2646-196">the activity (what)</span></span>

![Logs de auditoria](./media/device-management-azure-portal/63.png)

<span data-ttu-id="e2646-198">Você pode personalizar o modo de exibição de lista clicando em **Colunas** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="e2646-198">You can customize the list view by clicking **Columns** in the toolbar.</span></span>
 
![Logs de auditoria](./media/device-management-azure-portal/64.png)


<span data-ttu-id="e2646-200">Para restringir os dados relatados a um nível que funciona para você, filtre os dados de auditoria usando os seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="e2646-200">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="e2646-201">Categoria</span><span class="sxs-lookup"><span data-stu-id="e2646-201">Catergory</span></span>
- <span data-ttu-id="e2646-202">Tipo de recurso de atividade</span><span class="sxs-lookup"><span data-stu-id="e2646-202">Activity resource type</span></span>
- <span data-ttu-id="e2646-203">Atividade</span><span class="sxs-lookup"><span data-stu-id="e2646-203">Activity</span></span>
- <span data-ttu-id="e2646-204">Intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="e2646-204">Date range</span></span>
- <span data-ttu-id="e2646-205">Destino</span><span class="sxs-lookup"><span data-stu-id="e2646-205">Target</span></span>
- <span data-ttu-id="e2646-206">Iniciado por (ator)</span><span class="sxs-lookup"><span data-stu-id="e2646-206">Initiated By (Actor)</span></span>

<span data-ttu-id="e2646-207">Além dos filtros, você pode pesquisar itens específicos.</span><span class="sxs-lookup"><span data-stu-id="e2646-207">In addition to the filters, you can search for specific entries.</span></span>

![Logs de auditoria](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="e2646-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2646-209">Next steps</span></span>

* [<span data-ttu-id="e2646-210">Introdução ao gerenciamento de dispositivos no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2646-210">Introduction to device management in Azure Active Directory</span></span>](device-management-introduction.md)



