---
title: "Elemento de interface do usuário CredentialsCombo de aplicativo gerenciado do Azure | Microsoft Docs"
description: "Descreve o elemento Microsoft.Compute.CredentialsCombo da interface do usuário para aplicativos gerenciados do Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 254f383ee6f7cb9f7051fa135d85319a22c3c369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="760a3-103">Elemento de interface do usuário Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="760a3-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="760a3-104">Um grupo de controles com validação interna para chaves públicas SSH e senhas Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="760a3-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="760a3-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="760a3-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="760a3-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="760a3-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="760a3-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="760a3-108">Schema</span></span>
<span data-ttu-id="760a3-109">Se `osPlatform` é **Windows**, o seguinte esquema é usado:</span><span class="sxs-lookup"><span data-stu-id="760a3-109">If `osPlatform` is **Windows**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="760a3-110">Se `osPlatform` é **Linux**, o seguinte esquema é usado:</span><span class="sxs-lookup"><span data-stu-id="760a3-110">If `osPlatform` is **Linux**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="760a3-111">Comentários</span><span class="sxs-lookup"><span data-stu-id="760a3-111">Remarks</span></span>
- <span data-ttu-id="760a3-112">`osPlatform` deve ser especificada e pode ser **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="760a3-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="760a3-113">Se `constraints.required` é definido como **true**, as caixas de texto da chave pública SSH ou senha devem conter valores para serem validados com êxito.</span><span class="sxs-lookup"><span data-stu-id="760a3-113">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must contain values to validate successfully.</span></span> <span data-ttu-id="760a3-114">O valor padrão é **true**.</span><span class="sxs-lookup"><span data-stu-id="760a3-114">The default value is **true**.</span></span>
- <span data-ttu-id="760a3-115">Se `options.hideConfirmation` for definido como **true**, a segunda caixa de texto para confirmar a senha do usuário ficará oculta.</span><span class="sxs-lookup"><span data-stu-id="760a3-115">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="760a3-116">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="760a3-116">The default value is **false**.</span></span>
- <span data-ttu-id="760a3-117">Se `options.hidePassword` é definido como **true**, a opção para usar a autenticação de senha fica oculta.</span><span class="sxs-lookup"><span data-stu-id="760a3-117">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span></span> <span data-ttu-id="760a3-118">Ele pode ser usado apenas quando `osPlatform` é **Linux**.</span><span class="sxs-lookup"><span data-stu-id="760a3-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="760a3-119">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="760a3-119">The default value is **false**.</span></span>
- <span data-ttu-id="760a3-120">Outras restrições sobre as senhas permitidas podem ser implementadas usando a propriedade `customPasswordRegex`.</span><span class="sxs-lookup"><span data-stu-id="760a3-120">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span></span> <span data-ttu-id="760a3-121">A cadeia de caracteres em `customValidationMessage` é exibida quando uma senha falha a validação personalizada.</span><span class="sxs-lookup"><span data-stu-id="760a3-121">The string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="760a3-122">O valor padrão para ambas as propriedades é **null**.</span><span class="sxs-lookup"><span data-stu-id="760a3-122">The default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="760a3-123">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="760a3-123">Sample output</span></span>
<span data-ttu-id="760a3-124">Se `osPlatform` é **Windows**, ou o usuário forneceu uma senha em vez de uma chave pública SSH,a seguinte saída é esperada:</span><span class="sxs-lookup"><span data-stu-id="760a3-124">If `osPlatform` is **Windows**, or the user provided a password instead of an SSH public key, then the following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="760a3-125">Se o usuário forneceu uma chave pública SSH, a seguinte saída é esperada:</span><span class="sxs-lookup"><span data-stu-id="760a3-125">If the user provided an SSH public key, then the following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="760a3-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="760a3-126">Next steps</span></span>
* <span data-ttu-id="760a3-127">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="760a3-127">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="760a3-128">Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="760a3-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="760a3-129">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="760a3-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
