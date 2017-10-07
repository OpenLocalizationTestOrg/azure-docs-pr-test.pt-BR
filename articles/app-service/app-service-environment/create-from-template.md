---
title: "aaaCreate um ambiente de serviço de aplicativo do Azure usando um modelo do Gerenciador de recursos"
description: "Explica como toocreate um ambiente de serviço de aplicativo do Azure ILB ou externas usando um modelo do Gerenciador de recursos"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>Criar um ASE usando um modelo do Azure Resource Manager

## <a name="overview"></a>Visão geral
Ambientes do Serviço de Aplicativo do Azure (ASEs) podem ser criados com um ponto de extremidade acessível pela Internet ou um ponto de extremidade em um endereço interno na rede virtual (VNet) do Azure. Quando criado com um ponto de extremidade interno, esse ponto de extremidade é fornecido por um componente do Azure chamado ILB (balanceador de carga interno). Olá ASE em um endereço IP interno é chamada uma ASE ILB. Olá ASE com um ponto de extremidade público é chamada uma ASE externo. 

Uma ASE pode ser criada usando Olá portal do Azure ou um modelo do Gerenciador de recursos do Azure. Este artigo o orienta pelas etapas de hello e a sintaxe necessária toocreate uma ASE externo ou ASE ILB com modelos do Gerenciador de recursos. toolearn como toocreate uma ASE em Olá portal do Azure, consulte [fazer uma ASE externo] [ MakeExternalASE] ou [fazer uma ASE ILB][MakeILBASE].

Quando você cria uma ASE em Olá portal do Azure, você pode criar sua rede virtual no hello ao mesmo tempo ou escolha um toodeploy redes preexistente em. Ao criar um ASE com base em um modelo, você deve começar com: 

* Uma VNet do Resource Manager.
* Uma sub-rede nessa VNet. É recomendável um tamanho de sub-rede ASE de `/25` com o crescimento futuro de tooaccomodate 128 endereços. Depois Olá ASE é criado, você não pode alterar o tamanho de saudação.
* ID do recurso de saudação da sua rede virtual. Você pode obter essas informações de saudação portal do Azure em suas propriedades de rede virtual.
* assinatura de saudação desejado toodeploy em.
* Olá local toodeploy em.

tooautomate sua criação ASE:

1. Crie hello ASE de um modelo. Se você criar um ASE externo, terá concluído após essa etapa. Se você criar uma ASE ILB, há alguns toodo coisas mais.

2. Depois que o ASE ILB for criado, um certificado SSL correspondente ao domínio do ASE ILB será carregado.

3. Olá carregado certificado SSL está atribuído toohello ASE ILB como seu certificado SSL "padrão".  Esse certificado é usado para tooapps de tráfego do SSL em Olá ILB ASE quando eles usam o domínio raiz comum Olá que é atribuído toohello ASE (por exemplo, https://someapp.mycustomrootcomain.com).


## <a name="create-hello-ase"></a>Criar hello ASE
Um modelo do Resource Manager que cria um ASE e seu arquivo de parâmetros associado está disponível [no exemplo][quickstartasev2create] no GitHub.

Se você quiser toomake uma ASE ILB, use esses modelo do Gerenciador de recursos [exemplos][quickstartilbasecreate]. Eles atendem toothat caso de uso. A maioria dos parâmetros Olá Olá *azuredeploy.parameters.json* arquivo são comuns criação toohello de ASs ILB e ASs externos. Olá lista a seguir chama parâmetros de Observação especial ou que são exclusivos, quando você cria uma ASE ILB:

* *interalLoadBalancingMode*: na maioria dos casos, defina este too3, o que significa que os tráfegos HTTP/HTTPS nas portas 80/443, e portas de canal de dados do controle Olá ouviu tooby serviço Olá FTP Olá ASE, será rede virtual alocada pelo ILB tooan associada endereço interno. Se essa propriedade for definida too2, somente Olá FTP relacionados ao serviço portas (canais de controle e de dados) são endereços ILB tooan associado. Olá tráfego HTTP/HTTPS permanece no VIP público hello.
* *dnsSuffix*: esse parâmetro define o domínio raiz da saudação padrão que é atribuído toohello ASE. Variação pública de saudação do serviço de aplicativo do Azure, domínio raiz da saudação padrão para todos os aplicativos web é *azurewebsites.net*. Como uma ASE ILB é a rede virtual do cliente interno tooa, domínio de raiz padrão do serviço do sentido toouse Olá público não faz. Em vez disso, um ASE ILB deve ter um domínio de raiz padrão que faça sentido para uso dentro da rede virtual interna da empresa. Por exemplo, a Contoso Corporation pode usar um domínio de raiz padrão do *interna do contoso.com* para aplicativos que são toobe pretendido acessível apenas dentro de rede virtual da Contoso e pode ser resolvido. 
* *ipSslAddressCount*: esse parâmetro é automaticamente padronizada tooa valor 0 Olá *azuredeploy.json* o arquivo porque o ILB ASs ter apenas um único endereço ILB. Não há nenhum endereço IP SSL explícito para um ASE ILB. Portanto, Olá pool de endereços IP SSL para um ASE ILB deve ser definido toozero. Caso contrário, ocorrerá um erro de provisionamento. 

Depois de saudação *azuredeploy.parameters.json* arquivo é preenchido, criar hello ASE usando o trecho de código do PowerShell hello. Alterar Olá caminhos toomatch Olá Gerenciador de recursos de arquivo de modelo locais de arquivos em seu computador. Lembre-se de toosupply seus próprios valores para nome de implantação do Gerenciador de recursos de saudação e o nome do grupo de recursos de saudação:

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Leva aproximadamente uma hora para Olá ASE toobe criado. Em seguida, Olá ASE mostra no portal de saudação na lista de saudação do ASs para assinatura de saudação que disparou a implantação de saudação.

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>Carregar e configurar o certificado SSL hello "padrão"
Um certificado SSL deve ser associado a saudação ASE como hello "padrão" certificado SSL usado tooestablish SSL conexões tooapps. Se o sufixo DNS de padrão de saudação do ASE é *interna do contoso.com*, toohttps://some-random-app.internal-contoso.com uma conexão requer um certificado SSL válido para **.internal contoso.com* . 

Obtenha um certificado SSL válido, usando autoridades de certificação internas, adquirindo um certificado de um emissor externo ou usando um certificado autoassinado. Independentemente de fonte de saudação do certificado SSL hello, Olá seguintes atributos do certificado deve ser configurado corretamente:

* **Entidade**: este atributo deve ser definido muito **sua raiz-domínio here.com*.
* **Nome Alternativo da Entidade**: Esse atributo deve incluir **.seu-dominio-raiz-aqui.com* e **.scm.seu-dominio-raiz-aqui.com*. SSL conexões toohello site SCM/Kudu associado a cada aplicativo usar um endereço de formulário Olá *your-app-name.scm.your-root-domain-here.com*.

Com um certificado SSL válido em mãos, são necessárias mais duas etapas preparatórias. Certificado SSL da saudação de Convert/Salvar como um arquivo. pfx. Lembre-se de arquivo hello. pfx deve incluir todos os intermediário e raiz certificados. Proteja-o com uma senha.

arquivo. pfx de saudação precisa toobe convertido em uma cadeia de caracteres base64, pois o certificado SSL de saudação é carregado por meio de um modelo do Gerenciador de recursos. Como modelos do Gerenciador de recursos são arquivos de texto, o arquivo. pfx de saudação deve ser convertido em uma cadeia de caracteres base64. Dessa forma pode ser incluído como um parâmetro de modelo de saudação.

Use Olá PowerShell trecho de código a seguir:

* Criar um certificado autoassinado.
* Exporte certificado hello como um arquivo. pfx.
* Converta o arquivo. pfx de saudação em uma cadeia de caracteres codificada em base64.
* Salve arquivo separado do tooa Olá cadeia de caracteres codificada em base64. 

Esse código do PowerShell para codificação base64 foi adaptado Olá [PowerShell scripts blog][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Após certificado SSL da saudação é gerado com êxito e convertido tooa cadeia de caracteres codificada em base64, use o modelo de Gerenciador de recursos do exemplo hello [certificado SSL configurar saudação padrão] [ quickstartconfiguressl] no GitHub. 

Olá parâmetros em Olá *azuredeploy.parameters.json* arquivo estão listados aqui:

* *appServiceEnvironmentName*: nome de saudação do hello ASE ILB que está sendo configurado.
* *existingAseLocation*: cadeia de caracteres de texto contendo Olá região do Azure onde hello ASE ILB foi implantado.  Por exemplo, "Centro-Sul dos EUA".
* *pfxBlobString*: Olá representação de cadeia de caracteres codificada based64 do arquivo. pfx de saudação. Use o trecho de código Olá mostrado anteriormente e copie a cadeia de caracteres de saudação contida em "exportedcert.pfx.b64". Cole-o como valor de saudação do hello *pfxBlobString* atributo.
* *senha*: arquivo. pfx do hello senha usada toosecure hello.
* *certificateThumbprint*: Olá a impressão digital do certificado. Se você recuperar esse valor do PowerShell (por exemplo, *$certificate. Impressão digital* de saudação trecho de código anterior), você pode usar o valor hello como está. Se você copiar o valor de saudação da caixa de diálogo do certificado de Windows hello, lembre-se toostrip out espaços estranhos hello. Olá *certificateThumbprint* deve ser algo como AF3143EB61D43F6727842115BB7F17BBCECAECAE.
* *certificateName*: um identificador de cadeia de caracteres amigável de sua escolha usado tooidentity certificado de saudação. nome de saudação é usado como parte do identificador de Gerenciador de recursos exclusivo Olá para Olá *Microsoft.Web/certificates* entidade que representa o certificado SSL de saudação. nome da saudação *deve* terminar com hello sufixo a seguir: \_yourASENameHere_InternalLoadBalancingASE. Olá portal do Azure usa esse sufixo como um indicador que Olá certificado é usado toosecure uma ASE ILB habilitado.

Um exemplo abreviado de *azuredeploy.parameters.json* é mostrado aqui:

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

Depois de saudação *azuredeploy.parameters.json* arquivo é preenchido, configure o certificado SSL saudação padrão usando o trecho de código do PowerShell hello. Alterar Olá toomatch de caminhos de arquivo onde os arquivos de modelo do Gerenciador de recursos de saudação estão localizados em seu computador. Lembre-se de toosupply seus próprios valores para nome de implantação do Gerenciador de recursos de saudação e o nome do grupo de recursos de saudação:

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Leva cerca de 40 minutos por alteração de saudação do ASE front-end tooapply. Por exemplo, para uma ASE tamanho padrão que usa dois front-ends, modelo Olá leva em torno de uma hora e toocomplete de 20 minutos. Durante a execução, o modelo de Olá Olá ASE não pode ser dimensionados.  

Após a conclusão do modelo hello, aplicativos em Olá ASE ILB podem ser acessados via HTTPS. Olá conexões são protegidas usando o certificado SSL saudação padrão. certificado SSL saudação padrão é usado quando aplicativos Olá ASE ILB são endereçados usando uma combinação do nome do aplicativo hello além do nome de host padrão hello. Por exemplo, https://mycustomapp.internal-contoso.com usa o certificado SSL saudação padrão para **.internal contoso.com*.

No entanto, assim como os aplicativos que são executados no serviço de multilocatário pública hello, os desenvolvedores podem configurar os nomes de host personalizados para aplicativos individuais. Eles também podem configurar associações de certificado SSL SNI exclusivas para aplicativos individuais.

## <a name="app-service-environment-v1"></a>Ambiente do Serviço de Aplicativo v1 ##
O Ambiente do Serviço de Aplicativo tem duas versões: ASEv1 e ASEv2. Olá informações anteriores foi baseado em ASEv2. Este mostra seção Olá diferenças entre ASEv1 e ASEv2.

Em ASEv1, você gerencia todos os recursos de saudação manualmente. Isso inclui front-ends hello, funcionários e endereços IP usados para SSL baseado em IP. Antes de você pode dimensionar seu plano de serviço de aplicativo, você deve expandir pool do trabalhador Olá que você deseja toohost-lo.

O ASEv1 usa um modelo de preço diferente do ASEv2. No ASEv1, você paga por cada núcleo alocado. Isso inclui os núcleos que são usados para front-ends ou funções de trabalho que não hospedam nenhuma carga de trabalho. Em ASEv1, tamanho de máximo escala saudação padrão de uma ASE é 55 total de hosts. Isso inclui funções de trabalho e front-ends. Um tooASEv1 de vantagem é que ele pode ser implantado em uma rede virtual clássica e uma rede virtual do Gerenciador de recursos. toolearn mais sobre ASEv1, consulte [introdução do ambiente de serviço de aplicativo v1][ASEv1Intro].

toocreate um ASEv1 usando um modelo do Gerenciador de recursos, consulte [criar um v1 ASE ILB com um modelo do Gerenciador de recursos][ILBASEv1Template].


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
