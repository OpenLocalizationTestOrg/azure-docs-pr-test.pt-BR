---
title: 'Gerar e exportar certificados para o Ponto a Site: MakeCert : Azure | Microsoft Docs'
description: "Este artigo contém etapas toocreate um certificado auto-assinado, exportar a chave pública hello e gerar os certificados de cliente usando MakeCert."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>Gerar e exportar certificados para conexões Ponto a Site usando o MakeCert

Conexões ponto a Site usam certificados tooauthenticate. Este artigo mostra como o certificado de raiz toocreate um autoassinado e gerar os certificados de cliente usando MakeCert. Se você estiver procurando para etapas de configuração de ponto a Site, como como listam certificados de raiz tooupload, selecione um dos artigos de saudação ' Configure ponto a Site' de saudação a seguir:

> [!div class="op_single_selector"]
> * [Criar certificados autoassinados – PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Criar certificados autoassinados - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configurar Ponto a Site – Resource Manager – portal do Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Configurar o Point-to-Site - Gerenciador de recursos - Portal do Azure](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configurar Ponto a Site – Clássico – portal do Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

Enquanto é recomendável usar Olá [etapas do PowerShell do Windows 10](vpn-gateway-certificates-point-to-site.md) toocreate os certificados, fornecemos essas instruções MakeCert como um método opcional. certificados de saudação geradas usando qualquer método que podem ser instalados em [qualquer sistema operacional de cliente com suporte](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq). No entanto, o MakeCert tem Olá limitação a seguir:

* O MakeCert foi preterido. Isso significa que essa ferramenta pode ser removida a qualquer momento. Todos os certificados que você já tiver gerado usando MakeCert não serão afetados quando o MakeCert não estiver mais disponível. MakeCert somente os certificados de saudação toogenerate usado, não é um mecanismo de validação.

## <a name="rootcert"></a>Criar um certificado raiz autoassinado

Olá, as etapas a seguir mostra como toocreate um autoassinado certificado usando MakeCert. Essas etapas não são específicas do modelo de implantação. Elas são válidas tanto para o Gerenciador de Recursos quanto para o clássico.

1. Baixe e instale o [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).
2. Após a instalação, normalmente você pode encontrar o utilitário makecert.exe de saudação nesse caminho: ' C:\Program Files (x86) \Windows Kits\10\bin\<arch >'. Embora, é possível que eles foram instalados tooanother local. Abra um prompt de comando como administrador e navegue local toohello de saudação utilitário MakeCert. Você pode usar o hello exemplo a seguir, ajustando para a localização correta hello:

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. Crie e instale um certificado no repositório de certificados pessoal da saudação em seu computador. Olá exemplo a seguir cria um correspondente *. cer* arquivo que você carregue tooAzure ao configurar P2S. Substitua 'P2SRootCert' e 'P2SRootCert.cer' com nome hello que você deseja toouse certificado hello. Olá certificado está localizado em 'Certificados - certificados atual'.

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>Exportar a chave pública da saudação (. cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

arquivo de exported.cer Olá deve ser carregado tooAzure. Para obter instruções, consulte [Configurar uma conexão ponto a site](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile). tooadd um certificado de raiz confiável, consulte [nesta seção](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) artigo hello.

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>Exportar o certificado autoassinado hello e toostore chave privada (opcional)

Talvez você queira tooexport Olá certificado raiz autoassinado e armazená-la com segurança. Se precisar, você pode instalá-lo depois em outro computador e gerar mais certificados de cliente, ou exportar outro arquivo .cer. Olá tooexport raiz certificado autoassinado como um. pfx, certificado de raiz Olá selecione e use Olá mesmas etapas conforme descrito em [exportar um certificado de cliente](#clientexport).

## <a name="create-and-install-client-certificates"></a>Criar e instalar certificados de cliente

Não instalar o certificado autoassinado Olá diretamente no computador do cliente hello. É necessário toogenerate um certificado do cliente do certificado autoassinado hello. Em seguida, exportar e instalar o computador de cliente do hello cliente certificado toohello. Olá, as etapas a seguir não é específicas do modelo de implantação. Elas são válidas tanto para o Gerenciador de Recursos quanto para o clássico.

### <a name="clientcert"></a>Gerar um certificado do cliente

Cada computador cliente que se conecta tooa VNet usando ponto a Site deve ter um certificado de cliente instalado. Gere um certificado de cliente de certificado raiz autoassinado de Olá e, em seguida, exportar e instalar o certificado de cliente hello. Se o certificado de cliente Olá não estiver instalado, a autenticação falhará. 

Olá etapas a seguir orientam você durante a geração de um certificado de cliente de um certificado raiz autoassinado. Você pode gerar vários certificados de cliente de saudação mesmo certificado raiz. Quando você gerar os certificados de cliente usando Olá etapas abaixo, o certificado de cliente Olá é instalado automaticamente no computador de saudação que você usou o certificado de saudação toogenerate. Se você quiser tooinstall um certificado de cliente em outro computador cliente, você pode exportar o certificado de saudação.
 
1. Em Olá mesmo computador que você usou Olá toocreate certificado autoassinado, abra um prompt de comando como administrador.
2. Modifique e execute toogenerate de exemplo hello um certificado de cliente.
  * Alterar *"P2SRootCert"* toohello nome da saudação auto-assinado que estão gerando o certificado do cliente de saudação do. Verifique se está usando o nome de Olá Olá do certificado de raiz, que é qualquer hello ' CN =' valor foi especificado quando você criou Olá auto-assinado.
  * Alterar *P2SChildCert* toohello nome toogenerate um toobe de certificado de cliente.

  Se você executar Olá exemplo a seguir sem modificá-lo, o resultado de saudação é um certificado de cliente chamado P2SChildcert no repositório de certificados pessoais que foi gerado a partir do certificado raiz P2SRootCert.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>Exportar um certificado do cliente

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>Instalar um certificado do cliente exportado

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Próximas etapas

Continue com a configuração de Ponto a Site. 

* Para **Gerenciador de recursos de** etapas do modelo de implantação, consulte [configurar uma conexão de ponto para Site tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Para **clássico** etapas do modelo de implantação, consulte [configurar uma conexão de VPN ponto a Site tooa VNet (clássico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
