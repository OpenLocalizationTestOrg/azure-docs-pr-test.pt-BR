---
title: aaaHow tooCreate uma modelos ILB ASE usando o Azure Resource Manager | Microsoft Docs
description: Saiba como toocreate um interno carregar ASE balanceador usando modelos do Gerenciador de recursos do Azure.
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>Como tooCreate uma modelos ILB ASE usando o Azure Resource Manager

> [!NOTE] 
> Este artigo é sobre Olá v1 do ambiente de serviço de aplicativo. Há uma versão mais recente do hello ambiente de serviço de aplicativo que é mais fácil toouse e é executado na infraestrutura mais avançada. toolearn mais sobre a nova versão de hello começam com hello [Introdução toohello ambiente de serviço de aplicativo](../app-service/app-service-environment/intro.md).
>

## <a name="overview"></a>Visão geral
Ambientes de Serviço de Aplicativo podem ser criados com um endereço interno de rede virtual em vez de um VIP público.  Esse endereço interno é fornecido por um componente do Azure chamado balanceador de carga interno (ILB) do hello.  Uma ASE ILB podem ser criada usando Olá portal do Azure.  Ele também pode ser criado usando a automação por meio de modelos do Azure Resource Manager.  Este artigo orienta pelas etapas de saudação e sintaxe necessária toocreate uma ASE ILB com modelos do Gerenciador de recursos do Azure.

Há três etapas envolvidas na automatização da criação de um ASE ILB:

1. Primeiro ASE base de saudação é criado em uma rede virtual usando um endereço de Balanceador de carga interno, em vez de um VIP público.  Como parte dessa etapa, é atribuído um nome de domínio de raiz toohello ILB ASE.
2. Uma vez carregado Olá que ILB ASE é criado, um certificado SSL.  
3. Olá carregado certificado SSL está explicitamente atribuído toohello ASE ILB como seu certificado SSL "padrão".  Esse certificado SSL será usado para tooapps de tráfego do SSL em Olá ILB ASE quando Olá aplicativos são resolvidos através dos Olá comuns raiz domínio atribuído toohello ASE (por exemplo, https://someapp.mycustomrootcomain.com)

## <a name="creating-hello-base-ilb-ase"></a>Criando Olá Base ILB ASE
Um modelo do Azure Resource Manager de exemplo e seu arquivo de parâmetros associado estão disponíveis no GitHub [aqui][quickstartilbasecreate].

A maioria dos parâmetros Olá Olá *azuredeploy.parameters.json* arquivo é comuns toocreating ambos os ASs ILB, bem como ASs associado VIP público tooa.  lista de Olá abaixo chamadas de parâmetros de Observação especial, ou que são exclusivos, ao criar uma ASE ILB:

* *interalLoadBalancingMode*: na maioria dos casos, defina este too3, o que significa que os tráfegos HTTP/HTTPS nas portas 80/443, e portas de canal de dados do controle Olá ouviu tooby serviço Olá FTP Olá ASE, serão associada tooan ILB alocado rede virtual endereço interno.  Se essa propriedade for definida em vez disso, too2, Olá somente serviço FTP relacionada portas (canais de controle e de dados) serão associadas endereço tooan ILB, enquanto Olá tráfego HTTP/HTTPS permanecerá no VIP público hello.
* *dnsSuffix*: esse parâmetro define o domínio raiz da saudação padrão que será atribuído ASE toohello.  Variação pública de saudação do serviço de aplicativo do Azure, domínio raiz da saudação padrão para todos os aplicativos web é *azurewebsites.net*.  No entanto como uma ASE ILB é a rede virtual do cliente interno tooa, domínio de raiz padrão do serviço do sentido toouse Olá público não faz.  Em vez disso, um ASE ILB deve ter um domínio de raiz padrão que faça sentido para uso dentro da rede virtual interna da empresa.  Por exemplo, uma corporação Contoso hipotético pode usar um domínio de raiz padrão do *interna do contoso.com* para aplicativos que são tooonly pretendido ser resolvido e acessível na rede virtual da Contoso. 
* *ipSslAddressCount*: esse parâmetro é automaticamente padronizada tooa valor 0 Olá *azuredeploy.json* o arquivo porque o ILB ASs ter apenas um único endereço ILB.  Não há nenhum endereço IP SSL explícito para uma ASE ILB e, portanto, Olá pool de endereços IP SSL para um ASE ILB deve ser definido toozero, caso contrário, ocorrerá um erro de provisionamento. 

Uma vez Olá *azuredeploy.parameters.json* arquivo tiver sido preenchido para uma ASE ILB, Olá ASE ILB, em seguida, podem ser criado usando Olá trecho de código do Powershell a seguir.  Altere Olá toomatch de caminhos de arquivo onde os arquivos de modelo do Azure Resource Manager Olá estão localizados no seu computador.  Lembre-se também toosupply seus próprios valores para o nome da implantação do Azure Resource Manager hello e nome do grupo de recursos.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Depois de saudação do Azure Resource Manager modelo é enviado levará algumas horas para Olá ASE ILB toobe criado.  Depois de concluir a criação de hello, Olá ILB ASE aparecerão no portal de saudação UX na lista de saudação de ambientes de serviço de aplicativo para a assinatura de saudação que disparou a implantação de saudação.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>Carregar e configurar hello "Padrão" certificado de SSL
Uma vez Olá que ILB ASE é criado, um certificado SSL deve ser associado à saudação ASE como padrão"hello" uso de certificados SSL para estabelecer tooapps de conexões SSL.  Continuando com o exemplo de Contoso Corporation hipotético Olá, se saudação do ASE padrão DNS sufixo é *interna do contoso.com*, em seguida, uma conexão muito*https://some-random-app.internal-contoso.com*requer um certificado SSL válido para **.internal contoso.com*. 

Há uma variedade de maneiras tooobtain um certificado SSL válido, incluindo CAs internas, adquirir um certificado de um emissor externo e usar um certificado autoassinado.  Independentemente de fonte de saudação do certificado SSL hello, hello seguintes atributos de certificado necessário toobe configurado corretamente:

* *Entidade*: este atributo deve ser definido muito **sua raiz-domínio here.com*
* *Nome alternativo da entidade*: este atributo deve incluir tanto **sua raiz-domínio here.com*, e **.scm.your-raiz-domínio-here.com*.  motivo da segunda entrada de Olá Olá é que toohello de conexões SSL site SCM/Kudu associado a cada aplicativo será feita usando um endereço de formulário de saudação *your-app-name.scm.your-root-domain-here.com*.

Com um certificado SSL válido em mãos, são necessárias mais duas etapas preparatórias.  certificado SSL Olá precisa toobe convertidos/salvo como um arquivo. pfx.  Lembre-se de arquivo hello. pfx precisa tooinclude todos os intermediário e certificados de raiz e também precisa toobe protegido com uma senha.

Em seguida, arquivo.pfx resultante da saudação precisa toobe convertido em uma cadeia de caracteres base64 porque o certificado SSL hello será carregado usando um modelo do Gerenciador de recursos do Azure.  Desde que o Azure Resource Manager modelos são arquivos de texto, arquivo. pfx de saudação precisa toobe convertido em uma cadeia de caracteres base64 que ela possa ser incluída como um parâmetro de modelo de saudação.

trecho de código do Powershell Olá abaixo mostra um exemplo de como gerar um certificado autoassinado, exportar Olá certificado como um arquivo. pfx, converter o arquivo. pfx de saudação em base64 de cadeia de caracteres codificada e, em seguida, salvar Olá base64 codificada arquivo separado do tooa de cadeia de caracteres.  Olá código do Powershell para codificação base64 foi adaptada Olá [Blog de Scripts do Powershell][examplebase64encoding].

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

Depois que o certificado SSL da saudação foi gerado com êxito e a cadeia de caracteres codificada de base64 tooa convertido, Olá exemplo de modelo do Azure Resource Manager no GitHub para [Configurando certificado SSL padrão Olá] [ configuringDefaultSSLCertificate] pode ser usado.

Olá parâmetros em Olá *azuredeploy.parameters.json* arquivo estão listadas abaixo:

* *appServiceEnvironmentName*: nome de saudação do hello ASE ILB que está sendo configurado.
* *existingAseLocation*: cadeia de caracteres de texto contendo Olá região do Azure onde hello ASE ILB foi implantado.  Por exemplo: "Centro-Sul dos EUA".
* *pfxBlobString*: Olá based64 codificado a representação de cadeia de caracteres do arquivo. pfx de saudação.  Usando o trecho de código Olá mostrado anteriormente, copie string hello contido em "exportedcert.pfx.b64" e colá-lo em como valor Olá Olá *pfxBlobString* atributo.
* *senha*: arquivo. pfx do hello senha usada toosecure hello.
* *certificateThumbprint*: Olá a impressão digital do certificado.  Se você recuperar esse valor do Powershell (por exemplo, *$certificate. Impressão digital* de saudação trecho de código anterior), você pode usar o valor de saudação como-é.  No entanto se você copiar o valor de saudação do diálogo de certificado do Windows hello, lembre-se toostrip out espaços estranhos hello.  Olá *certificateThumbprint* deve ser algo como: AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *certificateName*: um identificador de cadeia de caracteres amigável de sua escolha usado tooidentity certificado de saudação.  nome de saudação é usado como parte do identificador exclusivo de Gerenciador de recursos do Azure Olá para Olá *Microsoft.Web/certificates* entidade que representa o certificado SSL de saudação.  nome da saudação **deve** terminar com hello sufixo a seguir: \_yourASENameHere_InternalLoadBalancingASE.  Esse sufixo é usado pelo portal hello como um indicador que Olá certificado é usado para proteger uma ASE ILB habilitado.

Um exemplo abreviado de *azuredeploy.parameters.json* é mostrado abaixo:

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Uma vez Olá *azuredeploy.parameters.json* arquivo tiver sido preenchido, certificado SSL saudação padrão pode ser configurado usando Olá trecho de código do Powershell a seguir.  Altere Olá toomatch de caminhos de arquivo onde os arquivos de modelo do Azure Resource Manager Olá estão localizados no seu computador.  Lembre-se também toosupply seus próprios valores para o nome da implantação do Azure Resource Manager hello e nome do grupo de recursos.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Depois de saudação do Azure Resource Manager modelo é enviado levará aproximadamente quarenta minutos minutos por alteração de saudação do ASE tooapply front-end.  Por exemplo, com um padrão ASE dimensionado usando dois front-ends, o modelo de saudação levará em torno de uma hora e toocomplete de vinte minutos.  Durante a execução do modelo de saudação Olá ASE não será capaz de tooscaled.  

Após a conclusão do modelo hello, aplicativos em Olá ASE ILB podem ser acessados via HTTPS e conexões Olá serão protegidos usando o certificado SSL saudação padrão.  certificado SSL do saudação padrão será usado quando os aplicativos em Olá ASE ILB são endereçados usando uma combinação do nome do aplicativo hello mais Olá nome do host padrão.  Por exemplo *https://mycustomapp.internal-contoso.com* usaria o certificado SSL saudação padrão para **.internal contoso.com*.

No entanto, assim como os aplicativos em execução no serviço de multilocatário pública hello, os desenvolvedores podem também configurar nomes de host personalizados para aplicativos individuais e, em seguida, configurar associações de certificado SSL de SNI exclusivas para aplicativos individuais.  

## <a name="getting-started"></a>Introdução
tooget iniciado com ambientes de serviço de aplicativo, consulte [Introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)

Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

