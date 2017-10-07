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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>Cmdlets do Azure Active Directory para definir configurações de grupo

> [!IMPORTANT]
> Este conteúdo se aplica somente tooOffice 365 grupos. Para obter mais informações sobre como definir grupos de segurança do tooallow usuários toocreate, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` conforme descrito em [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0). 

As configurações de Grupos do Office 365 são definidas usando um objeto Settings e um SettingsTemplate. Inicialmente, você não verá quaisquer objetos de configurações em seu diretório, porque o diretório está configurado com as configurações padrão de saudação. toochange as configurações padrão de saudação, você deve criar um novo objeto de configurações usando um modelo de configurações. Modelos de configurações são definidos pela Microsoft. Há vários modelos de configurações diferentes. configurações de grupo tooconfigure Office 365 para seu diretório, use Olá modelo denominado "Group.Unified". configurações de grupo tooconfigure Office 365 em um único grupo, use o modelo de Olá denominado "Group.Unified.Guest". Este modelo é usado toomanage grupo de tooan Office 365 de acesso de convidado. 

Olá cmdlets são parte do módulo de saudação do Azure Active Directory PowerShell V2. Para obter instruções como toodownload e instalar módulo de saudação em seu computador, consulte Olá artigo [versão 2 do Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azuread/). Você pode instalar Olá 2 versão do módulo de saudação do [Galeria do PowerShell Olá](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="retrieve-a-specific-settings-value"></a>Recuperar um valor de configurações específico
Se você souber o nome de saudação do hello configuração deseja tooretrieve, você pode usar o hello abaixo do valor de configurações atuais do cmdlet tooretrieve hello. Neste exemplo, recuperando valor Olá para uma configuração denominada "UsageGuidelinesUrl". Você pode ler que mais sobre configurações de diretório e seus nomes mais abaixo neste artigo.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Criar configurações no nível do diretório Olá
Estas etapas criam as configurações no nível de diretório, que se aplicam a grupos do Office 365 tooall (Unified grupos) no diretório de saudação.

1. Olá DirectorySettings cmdlets, você deve especificar o ID de saudação do hello SettingsTemplate deseja toouse. Se você não souber essa ID, esse cmdlet retorna a lista de saudação de todas as configurações de modelos:
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  Essa chamada do cmdlet retorna todos os modelos disponíveis:
  
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
2. tooadd uma URL de diretriz de uso, primeiro é necessário tooget Olá SettingsTemplate objeto que define o valor de URL da diretriz Olá uso; ou seja, Olá Group.Unified modelo:
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. Em seguida, crie um novo objeto de configurações com base no modelo:
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. Atualize o valor de diretriz do uso de saudação:
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. Finalmente, aplique as configurações de saudação:
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

Após a conclusão bem-sucedida, Olá cmdlet retorna Olá ID do novo objeto de configurações hello:
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
Aqui estão configurações Olá definidas no hello Group.Unified SettingsTemplate.

| **Configuração** | **Descrição** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>Tipo: booliano<li>Padrão: True |Sinalizador de saudação que indica se a criação de grupo unificado é permitida no diretório de saudação. |
|  <ul><li>GroupCreationAllowedGroupId<li>Tipo: String<li>Padrão: “” |GUID do grupo de segurança Olá para qual Olá membros são permitidos grupos unificados do toocreate mesmo quando EnableGroupCreation = = false. |
|  <ul><li>UsageGuidelinesUrl<li>Tipo: String<li>Padrão: “” |Um link toohello diretrizes de uso do grupo. |
|  <ul><li>ClassificationDescriptions<li>Tipo: String<li>Padrão: “” | Uma lista delimitada por vírgulas de descrições de classificação. |
|  <ul><li>DefaultClassification<li>Tipo: String<li>Padrão: “” | classificação de saudação que é toobe usado como classificação padrão de saudação para um grupo se nenhum foi especificado.|
|  <ul><li>PrefixSuffixNamingRequirement<li>Tipo: String<li>Padrão: “” |Ainda não implementado
|  <ul><li>AllowGuestsToBeGroupOwner<li>Tipo: booliano<li>Padrão: False | Booliano que indica se um usuário convidado pode ser um proprietário de grupos. |
|  <ul><li>AllowGuestsToAccessGroups<li>Tipo: booliano<li>Padrão: True | Booleano que indica se um usuário convidado pode ter conteúdo de acesso tooUnified grupos. |
|  <ul><li>GuestUsageGuidelinesUrl<li>Tipo: String<li>Padrão: “” | url de saudação de diretrizes de uso um link toohello convidado. |
|  <ul><li>AllowToAddGuests<li>Tipo: booliano<li>Padrão: True | Um valor booleano que indica se ou não é permitido tooadd clientes por toothis directory.|
|  <ul><li>ClassificationList<li>Tipo: String<li>Padrão: “” |Uma lista delimitada por vírgulas de valores de classificação válido que podem ser aplicadas tooUnified grupos. |
|  <ul><li>EnableGroupCreation<li>Tipo: booliano<li>Padrão: True | Um booliano que indica se usuários não administradores podem criar novos Grupos de Unificação. |


## <a name="read-settings-at-hello-directory-level"></a>Configurações de leitura em nível de diretório Olá
Essas etapas leem as configurações no nível do diretório, que se aplicam a grupos do Office tooall no diretório de saudação.

1. Leia todas as configurações existentes do diretório:
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  Esse cmdlet retorna uma lista de todas as configurações de diretório:
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. Leia todas as configurações para um grupo específico:
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. Leia todos os valores de configurações de diretório de um objeto de configurações de diretório específico, usando o GUID da ID de Configurações:
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  Esse cmdlet retorna Olá nomes e valores neste objeto de configurações para esse grupo específico:
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

## <a name="update-settings-for-a-specific-group"></a>Atualizar as configurações para um grupo específico

1. Procure Olá configurações modelo denominado "Groups.Unified.Guest"
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
2. Recupere o objeto de modelo Olá para o modelo de Groups.Unified.Guest hello:
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Crie um novo objeto de configurações de modelo de saudação:
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Defina o valor de toohello necessárias de configuração de hello:
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Crie nova configuração de saudação para grupo necessário Olá no diretório hello:
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Atualizar as configurações no nível do diretório Olá

Essas etapas atualizar as configurações no nível do diretório, que se aplicam a tooall unificada grupos no diretório de saudação. Estes exemplos pressupõem que já exista um objeto Configurações em seu diretório.

1. Localize o objeto de configurações existente hello:
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Atualize o valor de saudação:
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Atualize a configuração de saudação:
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Remover as configurações no nível do diretório Olá
Essa etapa remove as configurações no nível do diretório, que se aplicam a grupos do Office tooall no diretório de saudação.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Referência de sintaxe de cmdlet
Você pode encontrar mais documentação do PowerShell do Azure Active Directory em [Cmdlets do Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="additional-reading"></a>Leitura adicional

* [Gerenciando acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
