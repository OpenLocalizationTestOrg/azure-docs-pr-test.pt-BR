---
title: "Introdução ao iOS no Azure AD v2 – Configuração | Microsoft Docs"
description: Como aplicativos iOS (Swift) podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: d25353a61b2a60bff28aa0679d38110e77d19e64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="f81b4-103">Configurando seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="f81b4-103">Setting up your iOS application</span></span>

<span data-ttu-id="f81b4-104">Esta seção fornece instruções passo a passo sobre como criar um novo projeto para demonstrar como integrar um aplicativo iOS (Swift) com a opção *Entrar com a conta da Microsoft*, de forma que ele possa consultar APIs Web que exigem um token.</span><span class="sxs-lookup"><span data-stu-id="f81b4-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="f81b4-105">Prefere baixar este projeto de exemplo do XCode?</span><span class="sxs-lookup"><span data-stu-id="f81b4-105">Prefer to download this sample's XCode project instead?</span></span> <span data-ttu-id="f81b4-106">[Baixe um projeto](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) e vá para a [Etapa de configuração](#create-an-application-express) para configurar o exemplo de código antes de executá-lo.</span><span class="sxs-lookup"><span data-stu-id="f81b4-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


## <a name="install-carthage-to-download-and-build-msal"></a><span data-ttu-id="f81b4-107">Instale o Carthage para baixar e criar a MSAL</span><span class="sxs-lookup"><span data-stu-id="f81b4-107">Install Carthage to download and build MSAL</span></span>
<span data-ttu-id="f81b4-108">O gerenciador de pacotes Carthage é usado durante o período de versão prévia da MSAL – ele se integra ao XCode enquanto mantém a capacidade da Microsoft de fazer alterações na biblioteca.</span><span class="sxs-lookup"><span data-stu-id="f81b4-108">Carthage package manager is used during the preview period of MSAL – it integrates with XCode while maintaining the ability for Microsoft to make changes to the library.</span></span>

- <span data-ttu-id="f81b4-109">Baixe e instale a versão mais recente do Carthage [aqui](https://github.com/Carthage/Carthage/releases "URL de download do Carthage")</span><span class="sxs-lookup"><span data-stu-id="f81b4-109">Download and install the latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="f81b4-110">Criando seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f81b4-110">Creating your application</span></span>

1.  <span data-ttu-id="f81b4-111">Abra o XCode e selecione `Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="f81b4-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="f81b4-112">Selecione `iOS` > `Single view Application` e clique em *Avançar*</span><span class="sxs-lookup"><span data-stu-id="f81b4-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="f81b4-113">Forneça um nome de produto e clique em *Avançar*</span><span class="sxs-lookup"><span data-stu-id="f81b4-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="f81b4-114">Selecione uma pasta para criar seu aplicativo e clique em *Criar*</span><span class="sxs-lookup"><span data-stu-id="f81b4-114">Select a folder to create your app and click *Create*</span></span>

## <a name="build-the-msal-framework"></a><span data-ttu-id="f81b4-115">Criar a estrutura da MSAL</span><span class="sxs-lookup"><span data-stu-id="f81b4-115">Build the MSAL Framework</span></span>

<span data-ttu-id="f81b4-116">Siga as instruções abaixo para efetuar o pull e, em seguida, criar a versão mais recente das bibliotecas MSAL usando o Carthage:</span><span class="sxs-lookup"><span data-stu-id="f81b4-116">Follow the instructions below to pull and then build the latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="f81b4-117">Abra o terminal de busca e vá até a pasta raiz do aplicativo</span><span class="sxs-lookup"><span data-stu-id="f81b4-117">Open the bash terminal and go to the App’s root folder</span></span>
2.  <span data-ttu-id="f81b4-118">Copiar o que está abaixo e cole no terminal de busca para criar um arquivo “Cartfile”:</span><span class="sxs-lookup"><span data-stu-id="f81b4-118">Copy the below and paste in the bash terminal to create a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="f81b4-119">Copie e cole o que está abaixo.</span><span class="sxs-lookup"><span data-stu-id="f81b4-119">Copy and paste the below.</span></span> <span data-ttu-id="f81b4-120">Este comando busca dependências em uma pasta do Carthage/de check-outs e cria a biblioteca MSAL:</span><span class="sxs-lookup"><span data-stu-id="f81b4-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds the MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="f81b4-121">O processo acima é usado para baixar e criar a MSAL (Biblioteca de Autenticação da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="f81b4-121">The process above is used to download and build the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="f81b4-122">A MSAL manipula a aquisição, o armazenamento em cache e a atualização de tokens de usuário usados para acessar APIs protegidas pelo Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="f81b4-122">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by the Azure Active Directory v2.</span></span>

## <a name="add-the-msal-framework-to-your-application"></a><span data-ttu-id="f81b4-123">Adicionar a estrutura da MSAL ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f81b4-123">Add the MSAL framework to your application</span></span>
1.  <span data-ttu-id="f81b4-124">No Xcode, abra o a guia `General`</span><span class="sxs-lookup"><span data-stu-id="f81b4-124">In Xcode, open the `General` tab</span></span>
2.  <span data-ttu-id="f81b4-125">Vá para a seção `Linked Frameworks and Libraries` e clique em `+`</span><span class="sxs-lookup"><span data-stu-id="f81b4-125">Go to the `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="f81b4-126">Selecione `Add other…`</span><span class="sxs-lookup"><span data-stu-id="f81b4-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="f81b4-127">Selecione: `Carthage` > `Build` > `iOS` > `MSAL.framework` e clique em *Abrir*.</span><span class="sxs-lookup"><span data-stu-id="f81b4-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="f81b4-128">Você deve ver `MSAL.framework` adicionado à lista.</span><span class="sxs-lookup"><span data-stu-id="f81b4-128">You should see `MSAL.framework` added to the list.</span></span>
5.  <span data-ttu-id="f81b4-129">Vá para a guia `Build Phases`, clique no ícone `+` e escolha `New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="f81b4-129">Go to `Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="f81b4-130">Adicione o seguinte conteúdo à *área de script*:</span><span class="sxs-lookup"><span data-stu-id="f81b4-130">Add the following contents to the *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="f81b4-131">Adicione o seguinte a <code>Input Files</code> clicando em <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="f81b4-131">Add the following to <code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="f81b4-132">Criando a interface do usuário de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f81b4-132">Creating your application’s UI</span></span>
<span data-ttu-id="f81b4-133">Um arquivo Main.storyboard deve ser criado automaticamente como parte do modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f81b4-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="f81b4-134">Siga as instruções abaixo para criar a interface do usuário do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="f81b4-134">Follow the instructions below to create the app UI:</span></span>

1.  <span data-ttu-id="f81b4-135">Pressione CTRL e clique em `Main.storyboard` para abrir o menu contextual e, em seguida, clique em: `Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="f81b4-135">Control+click `Main.storyboard` to bring up the contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="f81b4-136">Substitua o nó `<scenes>` pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f81b4-136">Replace the `<scenes>` node with the code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
