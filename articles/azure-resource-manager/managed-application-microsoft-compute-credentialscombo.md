---
title: "elemento de interface do usuário CredentialsCombo de aplicativo gerenciado aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Compute.CredentialsCombo da interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="25ee0-103">Elemento de interface do usuário Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="25ee0-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="25ee0-104">Um grupo de controles com validação interna para chaves públicas SSH e senhas Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="25ee0-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="25ee0-105">Use esse elemento ao [criar um Aplicativo Gerenciado do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="25ee0-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="25ee0-106">Exemplo de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="25ee0-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="25ee0-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="25ee0-108">Schema</span></span>
<span data-ttu-id="25ee0-109">Se `osPlatform` é **Windows**, hello esquema a seguir será usada:</span><span class="sxs-lookup"><span data-stu-id="25ee0-109">If `osPlatform` is **Windows**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="25ee0-110">Se `osPlatform` é **Linux**, hello esquema a seguir será usada:</span><span class="sxs-lookup"><span data-stu-id="25ee0-110">If `osPlatform` is **Linux**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="25ee0-111">Comentários</span><span class="sxs-lookup"><span data-stu-id="25ee0-111">Remarks</span></span>
- <span data-ttu-id="25ee0-112">`osPlatform` deve ser especificada e pode ser **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="25ee0-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="25ee0-113">Se `constraints.required` está definido muito**true**, Olá, em seguida, a senha ou caixas de texto de chave pública de SSH devem conter valores toovalidate com êxito.</span><span class="sxs-lookup"><span data-stu-id="25ee0-113">If `constraints.required` is set too**true**, then hello password or SSH public key text boxes must contain values toovalidate successfully.</span></span> <span data-ttu-id="25ee0-114">valor padrão de saudação é **true**.</span><span class="sxs-lookup"><span data-stu-id="25ee0-114">hello default value is **true**.</span></span>
- <span data-ttu-id="25ee0-115">Se `options.hideConfirmation` está definido muito**true**, em seguida, a segunda caixa de texto Olá para confirmar a senha do usuário hello está oculto.</span><span class="sxs-lookup"><span data-stu-id="25ee0-115">If `options.hideConfirmation` is set too**true**, then hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="25ee0-116">valor padrão de saudação é **false**.</span><span class="sxs-lookup"><span data-stu-id="25ee0-116">hello default value is **false**.</span></span>
- <span data-ttu-id="25ee0-117">Se `options.hidePassword` está definido muito**true**, e a autenticação de senha Olá opção toouse está oculto.</span><span class="sxs-lookup"><span data-stu-id="25ee0-117">If `options.hidePassword` is set too**true**, then hello option toouse password authentication is hidden.</span></span> <span data-ttu-id="25ee0-118">Ele pode ser usado apenas quando `osPlatform` é **Linux**.</span><span class="sxs-lookup"><span data-stu-id="25ee0-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="25ee0-119">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="25ee0-119">The default value is **false**.</span></span>
- <span data-ttu-id="25ee0-120">Restrições adicionais sobre Olá permitidas senhas podem ser implementadas usando Olá `customPasswordRegex` propriedade.</span><span class="sxs-lookup"><span data-stu-id="25ee0-120">Additional constraints on hello allowed passwords can be implemented by using hello `customPasswordRegex` property.</span></span> <span data-ttu-id="25ee0-121">Olá a cadeia de caracteres em `customValidationMessage` é exibida quando uma senha falha a validação personalizada.</span><span class="sxs-lookup"><span data-stu-id="25ee0-121">hello string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="25ee0-122">Olá valor padrão para as duas propriedades é **nulo**.</span><span class="sxs-lookup"><span data-stu-id="25ee0-122">hello default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="25ee0-123">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="25ee0-123">Sample output</span></span>
<span data-ttu-id="25ee0-124">Se `osPlatform` é **Windows**, ou uma senha em vez de uma chave pública SSH fornecido pelo usuário de hello, hello seguinte saída é esperada:</span><span class="sxs-lookup"><span data-stu-id="25ee0-124">If `osPlatform` is **Windows**, or hello user provided a password instead of an SSH public key, then hello following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="25ee0-125">Se o usuário Olá fornecido uma chave pública SSH, em seguida, hello saída a seguir é esperada:</span><span class="sxs-lookup"><span data-stu-id="25ee0-125">If hello user provided an SSH public key, then hello following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="25ee0-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25ee0-126">Next steps</span></span>
* <span data-ttu-id="25ee0-127">Para aplicativos de toomanaged uma introdução, consulte [visão geral de aplicativos gerenciados do Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25ee0-127">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="25ee0-128">Para definições de interface do usuário de toocreating uma introdução, consulte [guia de Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25ee0-128">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="25ee0-129">Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="25ee0-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
