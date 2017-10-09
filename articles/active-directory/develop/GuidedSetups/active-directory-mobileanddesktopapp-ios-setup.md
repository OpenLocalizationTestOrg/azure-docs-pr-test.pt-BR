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
## <a name="setting-up-your-ios-application"></a>Configurando seu aplicativo iOS

Esta seção fornece instruções passo a passo sobre como toocreate um novo toodemonstrate de projeto como toointegrate um aplicativo iOS (Swift) com *entrar com a Microsoft* para que ele possa consultar APIs da Web que exigem um token.

> Preferir toodownload XCode projeto desse exemplo em vez disso? [Baixar um projeto](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) e ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes de executar.


## <a name="install-carthage-toodownload-and-build-msal"></a>Instalar toodownload Carthage e criar MSAL
Gerenciador de pacote Carthage é usado durante o período de visualização de saudação do MSAL – ele se integra com o XCode mantendo a capacidade de saudação de biblioteca do Microsoft toomake alterações toohello.

- Baixe e instale a versão mais recente de saudação do Carthage [aqui](https://github.com/Carthage/Carthage/releases "Carthage URL de download")

## <a name="creating-your-application"></a>Criando seu aplicativo

1.  Abra o XCode e selecione `Create a new Xcode project`
2.  Selecione `iOS` > `Single view Application` e clique em *Avançar*
3.  Forneça um nome de produto e clique em *Avançar*
4.  Selecione uma pasta toocreate seu aplicativo e clique em *criar*

## <a name="build-hello-msal-framework"></a>Criar hello MSAL Framework

Siga as instruções de saudação abaixo toopull e, em seguida, criar a versão mais recente Olá das bibliotecas MSAL usando Carthage:

1.  Abra Olá bash terminal e acesse a pasta raiz de toohello do aplicativo
2.  Olá abaixo de copiar e colar no hello bash terminal toocreate um arquivo de 'Cartfile':

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Copie e cole Olá abaixo. Este comando busca dependências em uma pasta Carthage/check-outs, e cria a biblioteca MSAL hello:
</li>
</ol>

```bash
carthage update
```

> processo de saudação acima é toodownload usado e compilação Olá biblioteca de autenticação da Microsoft (MSAL). MSAL lida com a aquisição, cache e atualizar usuário tokens usados tooaccess APIs protegidos pelo Olá v2 do Active Directory do Azure.

## <a name="add-hello-msal-framework-tooyour-application"></a>Adicionar Olá MSAL framework tooyour aplicativo
1.  No Xcode, abra Olá `General` guia
2.  Vá toohello `Linked Frameworks and Libraries` seção e clique em`+`
3.  Selecione `Add other…`
4.  Selecione: `Carthage` > `Build` > `iOS` > `MSAL.framework` e clique em *Abrir*. Você deve ver `MSAL.framework` adicionado toohello lista.
5.  Vá muito`Build Phases` guia e, em seguida, clique em `+` ícone, escolha`New Run Script Phase`
6.  Adicionar Olá toohello de conteúdo a seguir *área de script*:

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Adicionar Olá seguir muito<code>Input Files</code> clicando <code>+</code>:
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a>Criando a interface do usuário de seu aplicativo
Um arquivo Main.storyboard deve ser criado automaticamente como parte do modelo de projeto. Siga as instruções de saudação abaixo toocreate Olá aplicativo da interface do usuário:

1.  CTRL + clique `Main.storyboard` toobring até o menu contextual hello e, em seguida, clique em:`Open As` > `Source Code`
2.  Substituir saudação `<scenes>` nó com o código de saudação abaixo:

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
