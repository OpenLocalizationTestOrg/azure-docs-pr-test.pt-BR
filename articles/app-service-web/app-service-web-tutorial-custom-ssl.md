---
title: aaaBind um SSL personalizado existente tooAzure os aplicativos Web de certificado | Microsoft Docs
description: "Saiba tootoobind um aplicativo da web personalizado SSL certificado tooyour, back-end do aplicativo móvel ou aplicativo de API no serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>Associar um tooAzure de certificado SSL de personalizada existente aplicativos Web

Os aplicativos Web do Azure fornecem um serviço de hospedagem na Web altamente escalonável, com aplicação automática de patches. Este tutorial mostra como toobind um SSL personalizado de certificado que você adquirido de uma autoridade de certificação confiável muito[aplicativos Web do Azure](app-service-web-overview.md). Quando você terminar, você será capaz de tooaccess seu aplicativo web no ponto de extremidade HTTPS de saudação do seu domínio DNS personalizado.

![Aplicativo Web com certificado SSL personalizado](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Atualizar o tipo de preço do aplicativo
> * Associar seu tooApp de certificado SSL personalizado serviço
> * Impor HTTPS para seu aplicativo
> * Automatizar a associação de certificado SSL com scripts

> [!NOTE]
> Se você precisar tooget um certificado SSL personalizado, você pode obtê-la no portal do Azure de saudação diretamente e associá-lo tooyour web app. Siga Olá [tutorial de certificados de serviço de aplicativo](web-sites-purchase-ssl-web-site.md).

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

- [Crie um aplicativo do Serviço de Aplicativo](/azure/app-service/)
- [Mapear um nome DNS personalizado, tooyour aplicativo da web](app-service-web-tutorial-custom-domain.md)
- Adquirir um certificado SSL de uma autoridade de certificado confiável

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>Requisitos para o certificado SSL

toouse um certificado no serviço de aplicativo, o certificado de saudação deve atender aos Olá todos os requisitos a seguir:

* Assinado por uma autoridade de certificado confiável
* Exportado como um arquivo PFX protegido por senha
* Conter chave privada com pelo menos 2.048 bits de extensão
* Contém todos os certificados intermediários na cadeia de certificados de saudação

> [!NOTE]
> Os **certificados ECC (Criptografia de Curva Elíptica)** podem funcionar com o Serviço de Aplicativo, mas não são abordados neste artigo. Trabalhar com a autoridade de certificação em certificados ECC Olá as etapas exatas toocreate.

## <a name="prepare-your-web-app"></a>Preparar o aplicativo Web

toobind um SSL personalizado de certificado tooyour web app, seu [plano de serviço de aplicativo](https://azure.microsoft.com/pricing/details/app-service/) deve estar no hello **básica**, **padrão**, ou **Premium** camada. Nesta etapa, você garantir que seu aplicativo web é no hello aceita preço.

### <a name="log-in-tooazure"></a>Faça logon no tooAzure

Olá abrir [portal do Azure](https://portal.azure.com).

### <a name="navigate-tooyour-web-app"></a>Navegue tooyour web app

No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web.

![Selecionar aplicativo Web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

Você descarregou na página de gerenciamento de saudação do seu aplicativo web.  

### <a name="check-hello-pricing-tier"></a>Saudação de verificação de preço

Na navegação do lado esquerdo Olá da página de aplicativo da web, role toohello **configurações** seção e selecione **escalar verticalmente (plano de serviço de aplicativo)**.

![Menu Escalar verticalmente](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

Verificar toomake-se de que seu aplicativo web não está em Olá **livre** ou **compartilhado** camada. A camada atual do seu aplicativo Web é realçada por uma caixa azul escuro.

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

Não há suporte para SSL personalizado Olá **livre** ou **compartilhado** camada. Se for necessário tooscale backup, siga etapas Olá Olá próxima seção. Caso contrário, feche Olá **Escolher tipo de preços** página e ir muito[carregar e associar o certificado SSL](#upload).

### <a name="scale-up-your-app-service-plan"></a>Escalar verticalmente seu Plano do Serviço de Aplicativo

Selecione uma saudação **básica**, **padrão**, ou **Premium** camadas.

Clique em **Selecionar**.

![Escolha um tipo de preço](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

Quando você vir Olá notificação a seguir, a operação de escala de saudação foi concluída.

![Escalar verticalmente a notificação](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>Associar o certificado SSL

Você está pronto tooupload seu aplicativo web de tooyour de certificado SSL.

### <a name="merge-intermediate-certificates"></a>Mesclar certificados intermediários

Se a autoridade de certificação fornece vários certificados na cadeia de certificados hello, você precisa de certificados de saudação toomerge na ordem. 

toodo isso, abra cada certificado que você recebeu em um editor de texto. 

Criar um arquivo para o certificado mesclada hello, chamado _mergedcertificate.crt_. Em um editor de texto, copie o conteúdo de saudação de cada certificado para este arquivo. ordem Olá seus certificados deve ser semelhantes Olá modelo a seguir:

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>Exportar o certificado tooPFX

Exporte o certificado SSL mesclado com chave privada de saudação que sua solicitação de certificado foi gerada com.

Se você gerou a solicitação de certificado usando o OpenSSL, isso significa que você criou um arquivo de chave privada. tooexport tooPFX seu certificado, execute Olá comando a seguir. Substitua os espaços reservados de saudação  _&lt;o arquivo de chave privada >_ e  _&lt;arquivo mesclado de certificado >_.

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

Quando solicitado, defina uma senha de exportação. Você usará essa senha ao carregar o SSL certificado tooApp serviço mais tarde.

Se você usou o IIS ou _Certreq.exe_ toogenerate sua solicitação de certificado, a instalação Olá certificado tooyour computador local e, em seguida, [exportar Olá certificado tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).

### <a name="upload-your-ssl-certificate"></a>Carregar o certificado SSL

tooupload seu certificado SSL, clique em **certificados SSL** de saudação à esquerda de navegação de seu aplicativo web.

Clique em **Carregar Certificado**.

Em **Arquivo de Certificado PFX**, selecione o arquivo PFX. Em **senha do certificado**, digite a senha de saudação que você criou ao exportar o arquivo PFX de saudação.

Clique em **Carregar**.

![Carregar um certificado](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

Quando o serviço de aplicativo terminar de carregar seu certificado, ela aparece no hello **certificados SSL** página.

![Certificado carregado](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>Associar o certificado SSL

Em Olá **associações SSL** seção, clique em **Adicionar associação**.

Em Olá **Adicionar associação de SSL** página, use toosecure de nome de domínio Olá menus suspensos tooselect hello e Olá toouse de certificado.

> [!NOTE]
> Se você carregar seu certificado, mas não vir Olá nomes de domínio em Olá **Hostname** suspenso, tente atualizar a página do navegador hello.
>
>

Em **tipo SSL**, selecione se toouse  **[indicação de nome de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ou SSL com base em IP.

- **SSL baseado em SNI** – várias associações SSL baseadas em SNI podem ser adicionadas. Essa opção permite que vários toosecure de certificados SSL vários domínios em Olá mesmo endereço IP. Navegadores mais modernos (incluindo Internet Explorer, Chrome, Firefox e Opera) dão suporte ao SNI (encontre informações de suporte ao navegador mais abrangentes em [Indicação de Nome de Servidor](http://wikipedia.org/wiki/Server_Name_Indication)).
- **SSL baseado em IP** – apenas uma associação SSL baseada em IP pode ser adicionada. Essa opção permite que apenas um toosecure de certificado SSL para um endereço IP público dedicado. toosecure vários domínios, você deve protegê-los todos usando Olá mesmo certificado SSL. Essa é a opção tradicional Olá para uma associação SSL.

Clique em **Adicionar Associação**.

![Associar Certificado SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

Quando o serviço de aplicativo terminar de carregar seu certificado, ela aparece no hello **associações SSL** seções.

![Certificado associado tooweb aplicativo](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>Remapear um registro para IP SSL

Se você não usar SSL com base em IP em seu aplicativo web, ignorar muito[HTTPS de teste para seu domínio personalizado](#test).

Por padrão, o seu aplicativo Web usa um endereço IP público compartilhado. Quando você associa um certificado ao SSL baseado em IP, o Serviço de Aplicativo cria um novo endereço IP dedicado para o aplicativo Web.

Se você tiver mapeado um aplicativo de web de registro tooyour um, atualize o registro de domínio com esse novo endereço IP dedicado.

Seu aplicativo de web **domínio personalizado** página é atualizada com o endereço IP de novo, dedicado hello. [Copiar esse endereço IP](app-service-web-tutorial-custom-domain.md#info), em seguida, [remapear Olá um registro](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis novo endereço IP.

<a name="test"></a>

## <a name="test-https"></a>Testar HTTPS

Tudo o que tiver saído toodo agora é toomake-se de que o HTTPS funciona para seu domínio personalizado. Em vários navegadores, procurar muito`https://<your.custom.domain>` toosee que serve o seu aplicativo web.

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> Se o seu aplicativo Web retorna erros de validação de certificado, você provavelmente está usando um certificado autoassinado.
>
> Se não for o caso de Olá, você talvez tenha deixado os certificados intermediários, quando você exportar o arquivo PFX do certificado toohello.

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>Impor HTTPS

O Serviço de Aplicativo *não* impõe o HTTPS, de modo que qualquer um ainda pode acessar seu aplicativo Web usando HTTP. tooenforce HTTPS para o aplicativo web, definir uma regra de regravação de saudação _Web. config_ arquivo para seu aplicativo web. Serviço de aplicativo usa esse arquivo, independentemente da estrutura de linguagem de saudação do seu aplicativo web.

> [!NOTE]
> Há um redirecionamento de solicitações específico a um idioma. ASP.NET MVC pode usar Olá [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtro em vez de regra de regravação de saudação em _Web. config_.

Se você é um desenvolvedor do .NET, você deve estar relativamente familiarizado com esse arquivo. Ele é Olá raiz de sua solução.

Como alternativa, se você desenvolve com PHP, Node.js, Python ou Java, há uma chance de termos gerado esse arquivo em seu nome no Serviço de Aplicativo.

Conecte-se o ponto de extremidade do aplicativo da web tooyour FTP seguindo as instruções de saudação em [implantar tooAzure seu aplicativo do serviço de aplicativo usando o FTP/S](app-service-deploy-ftp.md).

Esse arquivo deve estar localizado em _/home/site/wwwroot_. Caso contrário, crie um _Web. config_ arquivo nessa pasta com hello XML a seguir:

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

Existe uma _Web. config_ de arquivo, copie todo Olá `<rule>` elemento em seu _Web. config_do `configuration/system.webServer/rewrite/rules` elemento. Se houver outros `<rule>` elementos no seu _Web. config_, Olá local copiado `<rule>` elemento antes Olá outros `<rule>` elementos.

Essa regra retorna um protocolo HTTPS toohello HTTP 301 (redirecionamento permanente) sempre que o usuário Olá faz com que um aplicativo web de tooyour de solicitação HTTP. Por exemplo, ele redireciona de `http://contoso.com` muito`https://contoso.com`.

Para obter mais informações sobre o módulo de reescrita de URL para IIS hello, consulte Olá [reescrita de URL](http://www.iis.net/downloads/microsoft/url-rewrite) documentação.

## <a name="enforce-https-for-web-apps-on-linux"></a>Impor o HTTPS a aplicativos Web no Linux

O Serviço de Aplicativo no Linux *não* impõe o HTTPS e, portanto, qualquer pessoa ainda pode acessar o aplicativo Web usando o HTTP. tooenforce HTTPS para o aplicativo web, definir uma regra de regravação de saudação _htaccess_ arquivo para seu aplicativo web. 

Conecte-se o ponto de extremidade do aplicativo da web tooyour FTP seguindo as instruções de saudação em [implantar tooAzure seu aplicativo do serviço de aplicativo usando o FTP/S](app-service-deploy-ftp.md).

Em _/home/site/wwwroot_, crie um _htaccess_ arquivo com hello código a seguir:

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

Essa regra retorna um protocolo HTTPS toohello HTTP 301 (redirecionamento permanente) sempre que o usuário Olá faz com que um aplicativo web de tooyour de solicitação HTTP. Por exemplo, ele redireciona de `http://contoso.com` muito`https://contoso.com`.

## <a name="automate-with-scripts"></a>Automatizar com scripts

Você pode automatizar associações SSL para seu aplicativo web com scripts, usando Olá [CLI do Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).

### <a name="azure-cli"></a>CLI do Azure

Olá comando a seguir carrega um arquivo PFX exportado e obtém a impressão digital de saudação.

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

Olá comando a seguir adiciona uma associação de SSL baseado em SNI, usando a impressão digital de saudação do comando anterior hello.

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

Olá comando a seguir carrega um arquivo PFX exportado e adiciona uma associação SSL de SNI.

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Atualizar o tipo de preço do aplicativo
> * Associar seu tooApp de certificado SSL personalizado serviço
> * Impor HTTPS para seu aplicativo
> * Automatizar a associação de certificado SSL com scripts

Avançar toolearn tutorial do próximo toohello como toouse rede de fornecimento de conteúdo do Azure.

> [!div class="nextstepaction"]
> [Adicionar uma tooan de rede de fornecimento de conteúdo (CDN) do serviço de aplicativo do Azure](app-service-web-tutorial-content-delivery-network.md)
