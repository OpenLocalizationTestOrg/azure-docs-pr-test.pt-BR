---
title: "configurações de grupo aaaConfigure usando cmdlets do Active Directory do Azure | Microsoft Docs"
description: "Como gerenciar as configurações de saudação de grupos usando os cmdlets do Active Directory do Azure"
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
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="37e06-103">Cmdlets do Azure Active Directory para definir configurações de grupo</span><span class="sxs-lookup"><span data-stu-id="37e06-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37e06-104">Este conteúdo se aplica somente tooOffice 365 grupos.</span><span class="sxs-lookup"><span data-stu-id="37e06-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="37e06-105">Para obter mais informações sobre como definir grupos de segurança do tooallow usuários toocreate, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` conforme descrito em [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="37e06-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="37e06-106">As configurações de Grupos do Office 365 são definidas usando um objeto Settings e um SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="37e06-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="37e06-107">Inicialmente, você não verá quaisquer objetos de configurações em seu diretório, porque o diretório está configurado com as configurações padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="37e06-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="37e06-108">toochange as configurações padrão de saudação, você deve criar um novo objeto de configurações usando um modelo de configurações.</span><span class="sxs-lookup"><span data-stu-id="37e06-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="37e06-109">Modelos de configurações são definidos pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="37e06-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="37e06-110">Há vários modelos de configurações diferentes.</span><span class="sxs-lookup"><span data-stu-id="37e06-110">There are several different settings templates.</span></span> <span data-ttu-id="37e06-111">configurações de grupo tooconfigure Office 365 para seu diretório, use Olá modelo denominado "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="37e06-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="37e06-112">configurações de grupo tooconfigure Office 365 em um único grupo, use o modelo de Olá denominado "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="37e06-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="37e06-113">Este modelo é usado toomanage grupo de tooan Office 365 de acesso de convidado.</span><span class="sxs-lookup"><span data-stu-id="37e06-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="37e06-114">Olá cmdlets são parte do módulo de saudação do Azure Active Directory PowerShell V2.</span><span class="sxs-lookup"><span data-stu-id="37e06-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="37e06-115">Para obter instruções como toodownload e instalar módulo de saudação em seu computador, consulte Olá artigo [versão 2 do Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="37e06-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="37e06-116">Você pode instalar Olá 2 versão do módulo de saudação do [Galeria do PowerShell Olá](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="37e06-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="37e06-117">Recuperar um valor de configurações específico</span><span class="sxs-lookup"><span data-stu-id="37e06-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="37e06-118">Se você souber o nome de saudação do hello configuração deseja tooretrieve, você pode usar o hello abaixo do valor de configurações atuais do cmdlet tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="37e06-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="37e06-119">Neste exemplo, recuperando valor Olá para uma configuração denominada "UsageGuidelinesUrl".</span><span class="sxs-lookup"><span data-stu-id="37e06-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="37e06-120">Você pode ler que mais sobre configurações de diretório e seus nomes mais abaixo neste artigo.</span><span class="sxs-lookup"><span data-stu-id="37e06-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="37e06-121">Criar configurações no nível do diretório Olá</span><span class="sxs-lookup"><span data-stu-id="37e06-121">Create settings at hello directory level</span></span>
<span data-ttu-id="37e06-122">Estas etapas criam as configurações no nível de diretório, que se aplicam a grupos do Office 365 tooall (Unified grupos) no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="37e06-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="37e06-123">Olá DirectorySettings cmdlets, você deve especificar o ID de saudação do hello SettingsTemplate deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="37e06-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="37e06-124">Se você não souber essa ID, esse cmdlet retorna a lista de saudação de todas as configurações de modelos:</span><span class="sxs-lookup"><span data-stu-id="37e06-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="37e06-125">Essa chamada do cmdlet retorna todos os modelos disponíveis:</span><span class="sxs-lookup"><span data-stu-id="37e06-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="37e06-126">tooadd uma URL de diretriz de uso, primeiro é necessário tooget Olá SettingsTemplate objeto que define o valor de URL da diretriz Olá uso; ou seja, Olá Group.Unified modelo:</span><span class="sxs-lookup"><span data-stu-id="37e06-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="37e06-127">Em seguida, crie um novo objeto de configurações com base no modelo:</span><span class="sxs-lookup"><span data-stu-id="37e06-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="37e06-128">Atualize o valor de diretriz do uso de saudação:</span><span class="sxs-lookup"><span data-stu-id="37e06-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="37e06-129">Finalmente, aplique as configurações de saudação:</span><span class="sxs-lookup"><span data-stu-id="37e06-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="37e06-130">Após a conclusão bem-sucedida, Olá cmdlet retorna Olá ID do novo objeto de configurações hello:</span><span class="sxs-lookup"><span data-stu-id="37e06-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="37e06-131">Aqui estão configurações Olá definidas no hello Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="37e06-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="37e06-132">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="37e06-132">**Setting**</span></span> | <span data-ttu-id="37e06-133">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="37e06-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="37e06-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="37e06-134">EnableGroupCreation</span></span><li><span data-ttu-id="37e06-135">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="37e06-135">Type: Boolean</span></span><li><span data-ttu-id="37e06-136">Padrão: True</span><span class="sxs-lookup"><span data-stu-id="37e06-136">Default: True</span></span> |<span data-ttu-id="37e06-137">Sinalizador de saudação que indica se a criação de grupo unificado é permitida no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="37e06-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="37e06-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="37e06-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="37e06-139">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="37e06-139">Type: String</span></span><li><span data-ttu-id="37e06-140">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="37e06-140">Default: “”</span></span> |<span data-ttu-id="37e06-141">GUID do grupo de segurança Olá para qual Olá membros são permitidos grupos unificados do toocreate mesmo quando EnableGroupCreation = = false.</span><span class="sxs-lookup"><span data-stu-id="37e06-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="37e06-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="37e06-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="37e06-143">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="37e06-143">Type: String</span></span><li><span data-ttu-id="37e06-144">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="37e06-144">Default: “”</span></span> |<span data-ttu-id="37e06-145">Um link toohello diretrizes de uso do grupo.</span><span class="sxs-lookup"><span data-stu-id="37e06-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="37e06-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="37e06-146">ClassificationDescriptions</span></span><li><span data-ttu-id="37e06-147">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="37e06-147">Type: String</span></span><li><span data-ttu-id="37e06-148">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="37e06-148">Default: “”</span></span> | <span data-ttu-id="37e06-149">Uma lista delimitada por vírgulas de descrições de classificação.</span><span class="sxs-lookup"><span data-stu-id="37e06-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="37e06-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="37e06-150">DefaultClassification</span></span><li><span data-ttu-id="37e06-151">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="37e06-151">Type: String</span></span><li><span data-ttu-id="37e06-152">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="37e06-152">Default: “”</span></span> | <span data-ttu-id="37e06-153">classificação de saudação que é toobe usado como classificação padrão de saudação para um grupo se nenhum foi especificado.</span><span class="sxs-lookup"><span data-stu-id="37e06-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="37e06-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="37e06-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="37e06-155">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="37e06-155">Type: String</span></span><li><span data-ttu-id="37e06-156">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="37e06-156">Default: “”</span></span> |<span data-ttu-id="37e06-157">Ainda não implementado</span><span class="sxs-lookup"><span data-stu-id="37e06-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="37e06-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="37e06-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="37e06-159">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="37e06-159">Type: Boolean</span></span><li><span data-ttu-id="37e06-160">Padrão: False</span><span class="sxs-lookup"><span data-stu-id="37e06-160">Default: False</span></span> | <span data-ttu-id="37e06-161">Booliano que indica se um usuário convidado pode ser um proprietário de grupos.</span><span class="sxs-lookup"><span data-stu-id="37e06-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="37e06-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="37e06-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="37e06-163">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="37e06-163">Type: Boolean</span></span><li><span data-ttu-id="37e06-164">Padrão: True</span><span class="sxs-lookup"><span data-stu-id="37e06-164">Default: True</span></span> | <span data-ttu-id="37e06-165">Booleano que indica se um usuário convidado pode ter conteúdo de acesso tooUnified grupos.</span><span class="sxs-lookup"><span data-stu-id="37e06-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="37e06-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="37e06-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="37e06-167">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="37e06-167">Type: String</span></span><li><span data-ttu-id="37e06-168">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="37e06-168">Default: “”</span></span> | <span data-ttu-id="37e06-169">url de saudação de diretrizes de uso um link toohello convidado.</span><span class="sxs-lookup"><span data-stu-id="37e06-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="37e06-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="37e06-170">AllowToAddGuests</span></span><li><span data-ttu-id="37e06-171">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="37e06-171">Type: Boolean</span></span><li><span data-ttu-id="37e06-172">Padrão: True</span><span class="sxs-lookup"><span data-stu-id="37e06-172">Default: True</span></span> | <span data-ttu-id="37e06-173">Um valor booleano que indica se ou não é permitido tooadd clientes por toothis directory.</span><span class="sxs-lookup"><span data-stu-id="37e06-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="37e06-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="37e06-174">ClassificationList</span></span><li><span data-ttu-id="37e06-175">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="37e06-175">Type: String</span></span><li><span data-ttu-id="37e06-176">Padrão: “”</span><span class="sxs-lookup"><span data-stu-id="37e06-176">Default: “”</span></span> |<span data-ttu-id="37e06-177">Uma lista delimitada por vírgulas de valores de classificação válido que podem ser aplicadas tooUnified grupos.</span><span class="sxs-lookup"><span data-stu-id="37e06-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="37e06-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="37e06-178">EnableGroupCreation</span></span><li><span data-ttu-id="37e06-179">Tipo: booliano</span><span class="sxs-lookup"><span data-stu-id="37e06-179">Type: Boolean</span></span><li><span data-ttu-id="37e06-180">Padrão: True</span><span class="sxs-lookup"><span data-stu-id="37e06-180">Default: True</span></span> | <span data-ttu-id="37e06-181">Um booliano que indica se usuários não administradores podem criar novos Grupos de Unificação.</span><span class="sxs-lookup"><span data-stu-id="37e06-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="37e06-182">Configurações de leitura em nível de diretório Olá</span><span class="sxs-lookup"><span data-stu-id="37e06-182">Read settings at hello directory level</span></span>
<span data-ttu-id="37e06-183">Essas etapas leem as configurações no nível do diretório, que se aplicam a grupos do Office tooall no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="37e06-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="37e06-184">Leia todas as configurações existentes do diretório:</span><span class="sxs-lookup"><span data-stu-id="37e06-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="37e06-185">Esse cmdlet retorna uma lista de todas as configurações de diretório:</span><span class="sxs-lookup"><span data-stu-id="37e06-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="37e06-186">Leia todas as configurações para um grupo específico:</span><span class="sxs-lookup"><span data-stu-id="37e06-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="37e06-187">Leia todos os valores de configurações de diretório de um objeto de configurações de diretório específico, usando o GUID da ID de Configurações:</span><span class="sxs-lookup"><span data-stu-id="37e06-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="37e06-188">Esse cmdlet retorna Olá nomes e valores neste objeto de configurações para esse grupo específico:</span><span class="sxs-lookup"><span data-stu-id="37e06-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="37e06-189">Atualizar as configurações para um grupo específico</span><span class="sxs-lookup"><span data-stu-id="37e06-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="37e06-190">Procure Olá configurações modelo denominado "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="37e06-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="37e06-191">Recupere o objeto de modelo Olá para o modelo de Groups.Unified.Guest hello:</span><span class="sxs-lookup"><span data-stu-id="37e06-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="37e06-192">Crie um novo objeto de configurações de modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="37e06-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="37e06-193">Defina o valor de toohello necessárias de configuração de hello:</span><span class="sxs-lookup"><span data-stu-id="37e06-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="37e06-194">Crie nova configuração de saudação para grupo necessário Olá no diretório hello:</span><span class="sxs-lookup"><span data-stu-id="37e06-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="37e06-195">Atualizar as configurações no nível do diretório Olá</span><span class="sxs-lookup"><span data-stu-id="37e06-195">Update settings at hello directory level</span></span>

<span data-ttu-id="37e06-196">Essas etapas atualizar as configurações no nível do diretório, que se aplicam a tooall unificada grupos no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="37e06-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="37e06-197">Estes exemplos pressupõem que já exista um objeto Configurações em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="37e06-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="37e06-198">Localize o objeto de configurações existente hello:</span><span class="sxs-lookup"><span data-stu-id="37e06-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="37e06-199">Atualize o valor de saudação:</span><span class="sxs-lookup"><span data-stu-id="37e06-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="37e06-200">Atualize a configuração de saudação:</span><span class="sxs-lookup"><span data-stu-id="37e06-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="37e06-201">Remover as configurações no nível do diretório Olá</span><span class="sxs-lookup"><span data-stu-id="37e06-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="37e06-202">Essa etapa remove as configurações no nível do diretório, que se aplicam a grupos do Office tooall no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="37e06-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="37e06-203">Referência de sintaxe de cmdlet</span><span class="sxs-lookup"><span data-stu-id="37e06-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="37e06-204">Você pode encontrar mais documentação do PowerShell do Azure Active Directory em [Cmdlets do Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="37e06-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="37e06-205">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="37e06-205">Additional reading</span></span>

* [<span data-ttu-id="37e06-206">Gerenciando acesso tooresources com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="37e06-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="37e06-207">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="37e06-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
