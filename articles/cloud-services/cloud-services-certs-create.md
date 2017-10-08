---
title: "certificados de serviços e o gerenciamento de aaaCloud | Microsoft Docs"
description: Saiba como toocreate e usar certificados com o Microsoft Azure
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a>Visão geral sobre certificados para os Serviços de Nuvem do Azure
Certificados são usados no Azure para serviços de nuvem ([certificados de serviço](#what-are-service-certificates)) e para autenticar com a API de gerenciamento da saudação ([certificados de gerenciamento](#what-are-management-certificates) quando usando Olá portal clássico do Azure e não Olá não clássico portal do Azure). Este tópico fornece uma visão geral de ambos os tipos de certificado, como muito[criar](#create) e [implantar](#deploy) -los tooAzure.

Os certificados usados no Azure são certificados x.509 v3, que podem ser assinados por outro certificado confiável ou ser autoassinados. Um certificado autoassinado é assinado por seu próprio criador, portanto não é considerado confiável por padrão. A maioria dos navegadores pode ignorar esse problema. Você só deve usar certificados autoassinados ao desenvolver e testar seus serviços de nuvem. 

Os certificados usados pelo Azure podem conter uma chave particular ou pública. Certificados têm uma impressão digital que fornece um meio tooidentify-los de forma inequívoca. Essa impressão digital é usada em hello Azure [arquivo de configuração](cloud-services-configure-ssl-certificate.md) tooidentify que um serviço de nuvem do certificado deve usar. 

## <a name="what-are-service-certificates"></a>O que são certificados de serviço?
Certificados de serviço são serviços toocloud anexado e habilitar a comunicação segura tooand do serviço de saudação. Por exemplo, se você implantou uma função web, você desejaria toosupply um certificado que pode autenticar um ponto de extremidade HTTPS exposto. Certificados de serviço, definidos em sua definição de serviço, são automaticamente implantado toohello máquina de virtual que está executando uma instância de sua função. 

Você pode carregar clássico de tooAzure de certificados de serviço hello usando portal clássico do Azure portal ou usando o modelo de implantação clássico hello. Os certificados de serviço são associados um serviço de nuvem específico. Implantação de tooa no arquivo de definição de serviço Olá são atribuídos.

Certificados de serviço podem ser gerenciados separadamente de seus serviços e podem ser gerenciados por indivíduos diferentes. Por exemplo, um desenvolvedor pode carregar um pacote de serviço que se refere a tooa certificado que um gerente de TI tem tooAzure carregados anteriormente. Um gerente de TI pode gerenciar e renovar o certificado (alterando a configuração de saudação do serviço de saudação) sem a necessidade de tooupload um novo pacote de serviço. Atualizando sem um novo pacote de serviço é possível porque nome lógico de saudação e nome do repositório local do certificado de saudação está no arquivo de definição de serviço hello e enquanto a impressão digital do certificado Olá é especificado no arquivo de configuração de serviço hello. certificado de saudação tooupdate, é somente necessário tooupload um novo certificado e a impressão digital de saudação de alteração de valor no arquivo de configuração do serviço de saudação.

>[!Note]
>Olá [perguntas frequentes sobre serviços de nuvem](cloud-services-faq.md) artigo tem algumas informações úteis sobre certificados.

## <a name="what-are-management-certificates"></a>O que são certificados de gerenciamento?
Certificados de gerenciamento permitem que você tooauthenticate com o modelo de implantação clássico hello. Muitos programas e ferramentas (como o Visual Studio ou saudação do SDK do Azure) usam esses configuração tooautomate de certificados e a implantação de vários serviços do Azure. Eles não são realmente relacionados toocloud serviços. 

> [!WARNING]
> Portanto, tenha cuidado! Esses tipos de certificados que qualquer pessoa que se autentica com eles toomanage assinatura de saudação que estão associados. 
> 
> 

### <a name="limitations"></a>Limitações
Há um limite de 100 certificados de gerenciamento por assinatura. Também há um limite de 100 certificados de gerenciamento para todas as assinaturas com a ID de usuário de um administrador de serviços específico. Se Olá ID de usuário de administrador da conta Olá já foi usado tooadd 100 certificados de gerenciamento e não há necessidade de mais certificados, você pode adicionar um coadministrador tooadd Olá certificados. 

Antes de adicionar mais de 100 certificados, veja se é possível reutilizar um certificado existente. Uso de coadministradores adiciona complexidade desnecessária potencialmente tooyour certificado gerenciamento processo.

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>Criar um Novo certificado autoassinado
Você pode usar qualquer toocreate disponíveis da ferramenta um certificado autoassinado como aderem configurações toothese:

* Um certificado X.509.
* Contém uma chave privada.
* Criado para troca de chaves (arquivo. pfx).
* Nome da entidade deve corresponder o serviço de nuvem do hello domínio usado tooaccess hello.

    > Não é possível adquirir um certificado SSL para cloudapp.net hello (ou para qualquer relacionadas ao Azure) domínio; nome da entidade do certificado Olá deve corresponder a saudação domínio personalizado nome usado tooaccess seu aplicativo. Por exemplo, **contoso.net** e não **contoso.cloudapp.net**.

* Mínimo de criptografia de 2048 bits.
* **Serviço de certificado somente**: certificado do cliente deve residir no hello *pessoal* repositório de certificados.

Há dois toocreate de maneiras fáceis um certificado no Windows, com hello `makecert.exe` utilitário ou IIS.

### <a name="makecertexe"></a>Makecert.exe
Esse utilitário foi preterido e não está documentado aqui. Para obter mais informações, consulte [este artigo do MSDN](https://msdn.microsoft.com/library/windows/desktop/aa386968).

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> Se desejar que o certificado de saudação toouse com um endereço IP em vez de um domínio, use o endereço IP de saudação no parâmetro de - DnsName hello.


Se você deseja toouse [certificado com o portal de gerenciamento Olá](../azure-api-management-certs.md), exportá-lo tooa **. cer** arquivo:

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>IIS (Serviços de Informações da Internet)
Existem muitas páginas Olá internet que abrangem como toodo isso com o IIS. [Este](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) é um ótimo site que descobri e que acho que explica bem. 

### <a name="java"></a>Java
Você pode usar o Java muito[criar um certificado](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).

### <a name="linux"></a>Linux
[Isso](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artigo descreve como toocreate certificados com o SSH.

## <a name="next-steps"></a>Próximas etapas
[Carregue seu certificado de serviço toohello portal clássico do Azure](cloud-services-configure-ssl-certificate.md) (ou hello [portal do Azure](cloud-services-configure-ssl-certificate-portal.md)).

Carregar um [certificado de gerenciamento de API](../azure-api-management-certs.md) toohello portal clássico do Azure. Olá portal do Azure não usa certificados de gerenciamento para autenticação.

