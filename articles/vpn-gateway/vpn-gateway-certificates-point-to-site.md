---
title: 'Gerar e exportar certificados para o Ponto a Site: PowerShell: Azure | Microsoft Docs'
description: "Este artigo contém etapas toocreate um certificado auto-assinado, exportar a chave pública hello e gerar os certificados de cliente usando o PowerShell no Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Gerar e exportar certificados para conexões Ponto a Site utilizando o PowerShell no Windows 10

Conexões ponto a Site usam certificados tooauthenticate. Este artigo mostra como o certificado de raiz toocreate um autoassinado e gerar os certificados de cliente usando o PowerShell no Windows 10. Se você estiver procurando para etapas de configuração de ponto a Site, como como listam certificados de raiz tooupload, selecione um dos artigos de saudação ' Configure ponto a Site' de saudação a seguir:

> [!div class="op_single_selector"]
> * [Criar certificados autoassinados – PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Criar certificados autoassinados - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configurar Ponto a Site – Resource Manager – portal do Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Configurar o Point-to-Site - Gerenciador de recursos - Portal do Azure](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configurar Ponto a Site – Clássico – portal do Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


Você deve executar etapas de saudação neste artigo em um computador executando o Windows 10. Olá cmdlets do PowerShell que você use certificados toogenerate fazem parte do sistema operacional de saudação Windows 10 e não funcionam em outras versões do Windows. computador Olá Windows 10 é apenas os certificados necessários toogenerate hello. Depois que os certificados de saudação são gerados, você pode carregá-los ou instalá-los em qualquer sistema operacional de cliente com suporte. 

Se você não tiver acesso tooa Windows 10 computador, você pode usar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificados. Olá certificados que você gerar usando qualquer método podem ser instalados em qualquer [suporte](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) sistema operacional do cliente.

## <a name="rootcert"></a>Criar um certificado raiz autoassinado

Use Olá New-SelfSignedCertificate cmdlet toocreate um certificado raiz autoassinado. Para obter informações adicionais sobre os parâmetros, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. Em um computador com Windows 10, abra um console do Windows PowerShell com privilégios elevados.
2. Use Olá certificado auto-assinado do exemplo toocreate Olá a seguir. Olá, exemplo a seguir cria um certificado raiz autoassinado chamado 'P2SRootCert' que é instalado automaticamente em 'Certificados de certificados atual'. Você pode exibir certificado Olá abrindo *certmgr.msc*, ou *gerenciar certificados de usuário*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Exportar a chave pública da saudação (. cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

arquivo de exported.cer Olá deve ser carregado tooAzure. Para obter instruções, consulte [Configurar uma conexão ponto a site](vpn-gateway-howto-point-to-site-rm-ps.md#upload). tooadd um certificado de raiz confiável, [nesta seção](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) artigo hello.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Exportar o certificado raiz autoassinado de saudação e toostore de chave pública (opcional)

Talvez você queira tooexport Olá certificado raiz autoassinado e armazená-la com segurança. Se precisar, você pode instalá-lo depois em outro computador e gerar mais certificados de cliente, ou exportar outro arquivo .cer. Olá tooexport raiz certificado autoassinado como um. pfx, certificado de raiz Olá selecione e use Olá mesmas etapas conforme descrito em [exportar um certificado de cliente](#clientexport).

## <a name="clientcert"></a>Gerar um certificado do cliente

Cada computador cliente que se conecta tooa VNet usando ponto a Site deve ter um certificado de cliente instalado. Gere um certificado de cliente de certificado raiz autoassinado de Olá e, em seguida, exportar e instalar o certificado de cliente hello. Se o certificado de cliente Olá não estiver instalado, a autenticação falhará. 

Olá etapas a seguir orientam você durante a geração de um certificado de cliente de um certificado raiz autoassinado. Você pode gerar vários certificados de cliente de saudação mesmo certificado raiz. Quando você gerar os certificados de cliente usando Olá etapas abaixo, o certificado de cliente Olá é instalado automaticamente no computador de saudação que você usou o certificado de saudação toogenerate. Se você quiser tooinstall um certificado de cliente em outro computador cliente, você pode exportar o certificado de saudação.

exemplos de saudação usam Olá New-SelfSignedCertificate cmdlet toogenerate um certificado de cliente que expira dentro de um ano. Para obter informações de parâmetros adicionais, como definir um valor diferente de expiração Olá certificado de cliente, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Exemplo 1

Este exemplo usa Olá declarado '$cert' variável da seção anterior hello. Se você fechar o console do PowerShell Olá depois criando Olá certificado raiz autoassinado, ou são adicional de cliente certificados em uma nova sessão de console do PowerShell, use as etapas de saudação em [exemplo 2](#ex2).

Modifique e execute toogenerate de exemplo hello um certificado de cliente. Se você executar Olá exemplo a seguir sem modificá-lo, o resultado de saudação é um certificado de cliente chamado 'P2SChildCert'.  Se desejar que o certificado do filho Olá tooname algo mais, modifique o valor CN de saudação. Não altere Olá TextExtension ao executar este exemplo. certificado de cliente Olá gerado é instalado automaticamente em 'Certificados - certificados atual' em seu computador.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Exemplo 2

Se você está criando certificados de cliente adicional ou está usando não Olá mesma sessão do PowerShell que você usou toocreate seu certificado raiz autoassinado, Olá use as etapas a seguir:

1. Identifica o certificado raiz autoassinado Olá que está instalado no computador de saudação. Esse cmdlet retorna uma lista de certificados instalados no seu computador.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Localize o nome do assunto de saudação de saudação retornados da lista, em seguida, impressão digital de saudação de cópia que está localizado próximo texto de tooa tooit arquivo. Saudação de exemplo a seguir, há dois certificados. nome CN de saudação é o nome de saudação do certificado raiz autoassinado de saudação do qual você deseja toogenerate um certificado filho. Nesse caso, 'P2SRootCert'.

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Declare uma variável para o certificado de raiz hello usando a impressão digital de saudação da etapa anterior hello. Substitua a impressão digital pela Olá Olá do certificado de raiz do qual você deseja toogenerate um certificado filho.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Por exemplo, usando a impressão digital de saudação para P2SRootCert na etapa anterior Olá, variável Olá tem esta aparência:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Modifique e execute toogenerate de exemplo hello um certificado de cliente. Se você executar Olá exemplo a seguir sem modificá-lo, o resultado de saudação é um certificado de cliente chamado 'P2SChildCert'. Se desejar que o certificado do filho Olá tooname algo mais, modifique o valor CN de saudação. Não altere Olá TextExtension ao executar este exemplo. certificado de cliente Olá gerado é instalado automaticamente em 'Certificados - certificados atual' em seu computador.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Exportar um certificado do cliente   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>Instalar um certificado do cliente exportado

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Próximas etapas

Continue com a configuração de Ponto a Site. 

* Para **Gerenciador de recursos de** etapas do modelo de implantação, consulte [configurar uma conexão de ponto para Site tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Para **clássico** etapas do modelo de implantação, consulte [configurar uma conexão de VPN ponto a Site tooa VNet (clássico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
