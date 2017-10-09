---
title: "aaaAzure AD v2 iOS guia de Introdução - instalação | Microsoft Docs"
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
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="c6a50-103">Configurando seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="c6a50-103">Setting up your iOS application</span></span>

<span data-ttu-id="c6a50-104">Esta seção fornece instruções passo a passo sobre como toocreate um novo toodemonstrate de projeto como toointegrate um aplicativo iOS (Swift) com *entrar com a Microsoft* para que ele possa consultar APIs da Web que exigem um token.</span><span class="sxs-lookup"><span data-stu-id="c6a50-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="c6a50-105">Preferir toodownload XCode projeto desse exemplo em vez disso?</span><span class="sxs-lookup"><span data-stu-id="c6a50-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="c6a50-106">[Baixar um projeto](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) e ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes de executar.</span><span class="sxs-lookup"><span data-stu-id="c6a50-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="c6a50-107">Instalar toodownload Carthage e criar MSAL</span><span class="sxs-lookup"><span data-stu-id="c6a50-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="c6a50-108">Gerenciador de pacote Carthage é usado durante o período de visualização de saudação do MSAL – ele se integra com o XCode mantendo a capacidade de saudação de biblioteca do Microsoft toomake alterações toohello.</span><span class="sxs-lookup"><span data-stu-id="c6a50-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="c6a50-109">Baixe e instale a versão mais recente de saudação do Carthage [aqui](https://github.com/Carthage/Carthage/releases "Carthage URL de download")</span><span class="sxs-lookup"><span data-stu-id="c6a50-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="c6a50-110">Criando seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="c6a50-110">Creating your application</span></span>

1.  <span data-ttu-id="c6a50-111">Abra o XCode e selecione `Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="c6a50-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="c6a50-112">Selecione `iOS` > `Single view Application` e clique em *Avançar*</span><span class="sxs-lookup"><span data-stu-id="c6a50-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="c6a50-113">Forneça um nome de produto e clique em *Avançar*</span><span class="sxs-lookup"><span data-stu-id="c6a50-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="c6a50-114">Selecione uma pasta toocreate seu aplicativo e clique em *criar*</span><span class="sxs-lookup"><span data-stu-id="c6a50-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="c6a50-115">Criar hello MSAL Framework</span><span class="sxs-lookup"><span data-stu-id="c6a50-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="c6a50-116">Siga as instruções de saudação abaixo toopull e, em seguida, criar a versão mais recente Olá das bibliotecas MSAL usando Carthage:</span><span class="sxs-lookup"><span data-stu-id="c6a50-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="c6a50-117">Abra Olá bash terminal e acesse a pasta raiz de toohello do aplicativo</span><span class="sxs-lookup"><span data-stu-id="c6a50-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="c6a50-118">Olá abaixo de copiar e colar no hello bash terminal toocreate um arquivo de 'Cartfile':</span><span class="sxs-lookup"><span data-stu-id="c6a50-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="c6a50-119">Copie e cole Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="c6a50-119">Copy and paste hello below.</span></span> <span data-ttu-id="c6a50-120">Este comando busca dependências em uma pasta Carthage/check-outs, e cria a biblioteca MSAL hello:</span><span class="sxs-lookup"><span data-stu-id="c6a50-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="c6a50-121">processo de saudação acima é toodownload usado e compilação Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="c6a50-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="c6a50-122">MSAL lida com a aquisição, cache e atualizar usuário tokens usados tooaccess APIs protegidos pelo Olá v2 do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a50-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="c6a50-123">Adicionar Olá MSAL framework tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="c6a50-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="c6a50-124">No Xcode, abra Olá `General` guia</span><span class="sxs-lookup"><span data-stu-id="c6a50-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="c6a50-125">Vá toohello `Linked Frameworks and Libraries` seção e clique em`+`</span><span class="sxs-lookup"><span data-stu-id="c6a50-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="c6a50-126">Selecione `Add other…`</span><span class="sxs-lookup"><span data-stu-id="c6a50-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="c6a50-127">Selecione: `Carthage` > `Build` > `iOS` > `MSAL.framework` e clique em *Abrir*.</span><span class="sxs-lookup"><span data-stu-id="c6a50-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="c6a50-128">Você deve ver `MSAL.framework` adicionado toohello lista.</span><span class="sxs-lookup"><span data-stu-id="c6a50-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="c6a50-129">Vá muito`Build Phases` guia e, em seguida, clique em `+` ícone, escolha`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="c6a50-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="c6a50-130">Adicionar Olá toohello de conteúdo a seguir *área de script*:</span><span class="sxs-lookup"><span data-stu-id="c6a50-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="c6a50-131">Adicionar Olá seguir muito<code>Input Files</code> clicando <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="c6a50-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="c6a50-132">Criando a interface do usuário de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="c6a50-132">Creating your application’s UI</span></span>
<span data-ttu-id="c6a50-133">Um arquivo Main.storyboard deve ser criado automaticamente como parte do modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="c6a50-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="c6a50-134">Siga as instruções de saudação abaixo toocreate Olá aplicativo da interface do usuário:</span><span class="sxs-lookup"><span data-stu-id="c6a50-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="c6a50-135">CTRL + clique `Main.storyboard` toobring até o menu contextual hello e, em seguida, clique em:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="c6a50-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="c6a50-136">Substituir saudação `<scenes>` nó com o código de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="c6a50-136">Replace hello `<scenes>` node with hello code below:</span></span>

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
