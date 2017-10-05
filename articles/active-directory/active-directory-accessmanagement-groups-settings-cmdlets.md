---
title: "Definir configurações de grupo usando cmdlets do Azure Active Directory | Microsoft Docs"
description: "Como gerenciar as configurações de grupos usando cmdlets do Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 0d89f12955b90c7e1a8301b7c3a1a92e7f62d085
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="2cbf2-103">Cmdlets do Azure Active Directory para definir configurações de grupo</span><span class="sxs-lookup"><span data-stu-id="2cbf2-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cbf2-104">Este conteúdo se aplica apenas a grupos do Office 365.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-104">This content applies only to Office 365 groups.</span></span> <span data-ttu-id="2cbf2-105">Para saber mais sobre como permitir que os usuários criem Grupos de segurança, defina `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` conforme descrito em [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="2cbf2-105">For more information on how to allow users to create Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="2cbf2-106">As configurações de Grupos do Office 365 são definidas usando um objeto Settings e um SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="2cbf2-107">Inicialmente, você não verá objetos Settings no seu diretório, pois o diretório foi configurado com as definições padrão.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span></span> <span data-ttu-id="2cbf2-108">Para alterar as configurações padrão, você deve criar um novo objeto de configurações usando um modelo de configurações.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-108">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="2cbf2-109">Modelos de configurações são definidos pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="2cbf2-110">Há vários modelos de configurações diferentes.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-110">There are several different settings templates.</span></span> <span data-ttu-id="2cbf2-111">Para definir as configuração de grupo do Office 365 para seu diretório, use o modelo chamado "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="2cbf2-111">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span></span> <span data-ttu-id="2cbf2-112">Para definir as configurações de grupo do Office 365 em um único grupo, use o modelo chamado "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="2cbf2-112">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="2cbf2-113">Esse modelo é usado para gerenciar o acesso de convidado a um grupo do Office 365.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-113">This template is used to manage guest access to an Office 365 group.</span></span> 

<span data-ttu-id="2cbf2-114">Os cmdlets fazem parte do Módulo do Azure Active Directory PowerShell V2.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-114">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="2cbf2-115">Para obter instruções de como baixar e instalar o módulo no seu computador, confira o artigo [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/) (PowerShell Versão 2 do Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2cbf2-115">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="2cbf2-116">Você pode instalar a versão 2 do módulo da [galeria do PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="2cbf2-116">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="2cbf2-117">Recuperar um valor de configurações específico</span><span class="sxs-lookup"><span data-stu-id="2cbf2-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="2cbf2-118">Se você souber o nome da configuração que deseja recuperar, será possível usar o cmdlet abaixo para recuperar o valor atual das configurações.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-118">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span></span> <span data-ttu-id="2cbf2-119">Neste exemplo, recuperaremos o valor de uma configuração chamada "UsageGuidelinesUrl".</span><span class="sxs-lookup"><span data-stu-id="2cbf2-119">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="2cbf2-120">Você pode ler que mais sobre configurações de diretório e seus nomes mais abaixo neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="2cbf2-121">Criar configurações no nível do diretório</span><span class="sxs-lookup"><span data-stu-id="2cbf2-121">Create settings at the directory level</span></span>
<span data-ttu-id="2cbf2-122">Estas etapas criam configurações no nível do diretório, que se aplicam a todos os grupos do Office 365 (Grupos unificados) no diretório.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-122">These steps create settings at directory level, which apply to all Office 365 groups (Unified groups) in the directory.</span></span>

1. <span data-ttu-id="2cbf2-123">Nos cmdlets DirectorySettings, você precisa especificar a ID de SettingsTemplate que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-123">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="2cbf2-124">Se você não souber essa ID, esse cmdlet retornará a lista com todos os modelos de configurações:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-124">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="2cbf2-125">Essa chamada do cmdlet retorna todos os modelos disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="2cbf2-126">Para adicionar uma URL de diretrizes de uso, primeiro você precisa obter o objeto SettingsTemplate que define o valor de URL da diretriz de uso; ou seja, o modelo de Group.Unified:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-126">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="2cbf2-127">Em seguida, crie um novo objeto de configurações com base no modelo:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="2cbf2-128">Então, atualize o valor de diretriz de uso:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-128">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="2cbf2-129">Por fim, aplique as configurações:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-129">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="2cbf2-130">Após a conclusão bem-sucedida, o cmdlet retornará a ID do novo objeto de configuração:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-130">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="2cbf2-131">Aqui estão as configurações definidas no Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-131">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="2cbf2-132">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="2cbf2-132">**Setting**</span></span> | <span data-ttu-id="2cbf2-133">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="2cbf2-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="2cbf2-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-134">EnableGroupCreation</span></span><li><span data-ttu-id="2cbf2-135">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="2cbf2-135">Type: Boolean</span></span><li><span data-ttu-id="2cbf2-136">Padrão: True</span><span class="sxs-lookup"><span data-stu-id="2cbf2-136">Default: True</span></span> |<span data-ttu-id="2cbf2-137">O sinalizador que indica se é permitida a criação de Grupo Unificado no diretório.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-137">The flag indicating whether Unified Group creation is allowed in the directory.</span></span> |
|  <ul><li><span data-ttu-id="2cbf2-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="2cbf2-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="2cbf2-139">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="2cbf2-139">Type: String</span></span><li><span data-ttu-id="2cbf2-140">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="2cbf2-140">Default: “”</span></span> |<span data-ttu-id="2cbf2-141">O GUID do grupo de segurança para o qual os membros têm permissão para criar Grupos Unificados, mesmo quando EnableGroupCreation = = false.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-141">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="2cbf2-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="2cbf2-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="2cbf2-143">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="2cbf2-143">Type: String</span></span><li><span data-ttu-id="2cbf2-144">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="2cbf2-144">Default: “”</span></span> |<span data-ttu-id="2cbf2-145">Um link para as Diretrizes de Uso do Grupo.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-145">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="2cbf2-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="2cbf2-146">ClassificationDescriptions</span></span><li><span data-ttu-id="2cbf2-147">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="2cbf2-147">Type: String</span></span><li><span data-ttu-id="2cbf2-148">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="2cbf2-148">Default: “”</span></span> | <span data-ttu-id="2cbf2-149">Uma lista delimitada por vírgulas de descrições de classificação.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="2cbf2-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="2cbf2-150">DefaultClassification</span></span><li><span data-ttu-id="2cbf2-151">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="2cbf2-151">Type: String</span></span><li><span data-ttu-id="2cbf2-152">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="2cbf2-152">Default: “”</span></span> | <span data-ttu-id="2cbf2-153">A classificação que deve ser usada como a classificação padrão para um grupo, se nenhuma for especificada.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-153">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="2cbf2-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="2cbf2-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="2cbf2-155">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="2cbf2-155">Type: String</span></span><li><span data-ttu-id="2cbf2-156">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="2cbf2-156">Default: “”</span></span> |<span data-ttu-id="2cbf2-157">Ainda não implementado</span><span class="sxs-lookup"><span data-stu-id="2cbf2-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="2cbf2-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="2cbf2-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="2cbf2-159">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="2cbf2-159">Type: Boolean</span></span><li><span data-ttu-id="2cbf2-160">Padrão: False</span><span class="sxs-lookup"><span data-stu-id="2cbf2-160">Default: False</span></span> | <span data-ttu-id="2cbf2-161">Booliano que indica se um usuário convidado pode ser um proprietário de grupos.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="2cbf2-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="2cbf2-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="2cbf2-163">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="2cbf2-163">Type: Boolean</span></span><li><span data-ttu-id="2cbf2-164">Padrão: True</span><span class="sxs-lookup"><span data-stu-id="2cbf2-164">Default: True</span></span> | <span data-ttu-id="2cbf2-165">Booliano que indica se um usuário convidado pode ter acesso ao conteúdo de Grupos Unificados.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-165">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="2cbf2-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="2cbf2-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="2cbf2-167">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="2cbf2-167">Type: String</span></span><li><span data-ttu-id="2cbf2-168">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="2cbf2-168">Default: “”</span></span> | <span data-ttu-id="2cbf2-169">A url de um link para as diretrizes de uso do convidado.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-169">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="2cbf2-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="2cbf2-170">AllowToAddGuests</span></span><li><span data-ttu-id="2cbf2-171">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="2cbf2-171">Type: Boolean</span></span><li><span data-ttu-id="2cbf2-172">Padrão: True</span><span class="sxs-lookup"><span data-stu-id="2cbf2-172">Default: True</span></span> | <span data-ttu-id="2cbf2-173">Um booliano que indica se há permissão para adicionar convidados a este diretório.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-173">A boolean indicating whether or not is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="2cbf2-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="2cbf2-174">ClassificationList</span></span><li><span data-ttu-id="2cbf2-175">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="2cbf2-175">Type: String</span></span><li><span data-ttu-id="2cbf2-176">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="2cbf2-176">Default: “”</span></span> |<span data-ttu-id="2cbf2-177">Uma lista delimitada por vírgulas de valores de classificação válidos que podem ser aplicados a Grupos Unificados.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-177">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span></span> |
|  <ul><li><span data-ttu-id="2cbf2-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="2cbf2-178">EnableGroupCreation</span></span><li><span data-ttu-id="2cbf2-179">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="2cbf2-179">Type: Boolean</span></span><li><span data-ttu-id="2cbf2-180">Padrão: True</span><span class="sxs-lookup"><span data-stu-id="2cbf2-180">Default: True</span></span> | <span data-ttu-id="2cbf2-181">Um booliano que indica se usuários não administradores podem criar novos Grupos de Unificação.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="2cbf2-182">Ler configurações no nível do diretório</span><span class="sxs-lookup"><span data-stu-id="2cbf2-182">Read settings at the directory level</span></span>
<span data-ttu-id="2cbf2-183">Estas etapas leem configurações no nível do diretório, que se aplicam a todos os grupos do Office no diretório.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-183">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="2cbf2-184">Leia todas as configurações existentes do diretório:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="2cbf2-185">Esse cmdlet retorna uma lista de todas as configurações de diretório:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="2cbf2-186">Leia todas as configurações para um grupo específico:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="2cbf2-187">Leia todos os valores de configurações de diretório de um objeto de configurações de diretório específico, usando o GUID da ID de Configurações:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="2cbf2-188">Esse cmdlet retorna os nomes e valores nesse objeto de configurações para esse grupo específico:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-188">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="2cbf2-189">Atualizar as configurações para um grupo específico</span><span class="sxs-lookup"><span data-stu-id="2cbf2-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="2cbf2-190">Procurar o modelo de configurações denominado "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="2cbf2-190">Search for the settings template named "Groups.Unified.Guest"</span></span>
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. <span data-ttu-id="2cbf2-191">Recupere o objeto de modelo para o modelo Groups.Unified.Guest:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-191">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="2cbf2-192">Crie um novo objeto de configurações do modelo:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-192">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="2cbf2-193">Defina a configuração com o valor necessário:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-193">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="2cbf2-194">Crie a nova configuração para o grupo exigido no diretório:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-194">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="2cbf2-195">Atualizar configurações no nível do diretório</span><span class="sxs-lookup"><span data-stu-id="2cbf2-195">Update settings at the directory level</span></span>

<span data-ttu-id="2cbf2-196">Estas etapas atualizam as configurações no nível do diretório, que se aplicam a todos os grupos Unificados no diretório.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-196">These steps update settings at directory level, which apply to all Unified groups in the directory.</span></span> <span data-ttu-id="2cbf2-197">Estes exemplos pressupõem que já exista um objeto Configurações em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="2cbf2-198">Encontre o objeto Configurações existente:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-198">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="2cbf2-199">Atualize o valor:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-199">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="2cbf2-200">Atualize a configuração:</span><span class="sxs-lookup"><span data-stu-id="2cbf2-200">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="2cbf2-201">Remover configurações no nível do diretório</span><span class="sxs-lookup"><span data-stu-id="2cbf2-201">Remove settings at the directory level</span></span>
<span data-ttu-id="2cbf2-202">Esta etapa remove configurações no nível do diretório, que se aplicam a todos os grupos do Office no diretório.</span><span class="sxs-lookup"><span data-stu-id="2cbf2-202">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="2cbf2-203">Referência de sintaxe de cmdlet</span><span class="sxs-lookup"><span data-stu-id="2cbf2-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="2cbf2-204">Você pode encontrar mais documentação do PowerShell do Azure Active Directory em [Cmdlets do Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="2cbf2-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="2cbf2-205">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="2cbf2-205">Additional reading</span></span>

* [<span data-ttu-id="2cbf2-206">Gerenciamento de acesso a recursos com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2cbf2-206">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="2cbf2-207">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2cbf2-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
