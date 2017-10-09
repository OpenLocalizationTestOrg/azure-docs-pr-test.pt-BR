---
title: "aaaSigning substituição de chave no AD do Azure | Microsoft Docs"
description: "Este artigo aborda Olá práticas recomendadas de substituição de chave de assinatura do Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Substituição de chave de assinatura no Azure Active Directory
Este tópico discute o que você precisa tooknow sobre as chaves públicas hello são usadas em tokens de segurança do Azure Active Directory (AD do Azure) toosign. É importante toonote que essas chaves são substituídas em uma base periódica e, em caso de emergência, poderia ser acumulados imediatamente. Todos os aplicativos que usam o AD do Azure devem ser capaz de tooprogrammatically identificador Olá substituição de chave processo ou estabelecer um processo de substituição manual periódica. Continuar a ler toounderstand como as chaves de saudação funcionam, como tooassess Olá impacto do aplicativo de tooyour de substituição hello e tooupdate seu aplicativo ou estabelecer uma sobreposição da chave de substituição manual periódica processo toohandle, se necessário.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Visão geral das chaves de assinatura no Azure AD
AD do Azure usa criptografia de chave pública criada na indústria padrões tooestablish confiança entre ele mesmo e Olá aplicativos que o utilizam. Em termos práticos, isso funciona em Olá seguinte caminho: AD do Azure usa uma chave de assinatura que consiste em um par de chaves público e privado. Quando um usuário entra no aplicativo tooan que usa o AD do Azure para autenticação, o AD do Azure cria um token de segurança que contém informações sobre o usuário hello. Esse token é assinado pelo AD do Azure usando sua chave privada antes de serem enviado back toohello aplicativo. tooverify Olá token seja válido e realmente originado do AD do Azure, o aplicativo hello deve validar a assinatura do token hello usando a chave pública do hello exposto pelo AD do Azure que está contido no locatário Olá [documentodedescobertadeOpenIDConnect](http://openid.net/specs/openid-connect-discovery-1_0.html) ou SAML/WS-Fed [documento de metadados de Federação](active-directory-federation-metadata.md).

Para fins de segurança do AD do Azure assinatura acumula chave periodicamente e, no caso de saudação de uma emergência, poderia ser acumulados imediatamente. Qualquer aplicativo que se integra ao AD do Azure deve ser preparado toohandle um evento de substituição de chave não importa a frequência, isso pode ocorrer. Se não, e seu aplicativo tenta toouse uma assinatura de saudação tooverify chave expiradas em um token, a solicitação de entrada hello falhará.

Sempre há mais de uma chave válida disponível no documento de descoberta de OpenID Connect hello e documento de metadados de Federação hello. Seu aplicativo deve estar preparado toouse qualquer uma das chaves de saudação especificado no documento hello, porque uma chave pode ser substituída em breve, outra pode ser seu substituição e assim por diante.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>Como tooassess se seu aplicativo será afetado e quais toodo sobre ele
Como o seu aplicativo lida com a substituição de chave depende de variáveis como tipo de saudação do aplicativo ou o protocolo de identidade e a biblioteca foi usado. seções de saudação abaixo avaliam se tipos mais comuns de saudação de aplicativos são afetados pela substituição de chave hello e fornecem orientação sobre como tooupdate Olá substituição automática do aplicativo toosupport ou atualizar manualmente a chave de saudação.

* [Aplicativos cliente nativos que acessam recursos](#nativeclient)
* [Aplicativos/APIs Web que acessam recursos](#webclient)
* [Aplicativos/APIs Web que protegem recursos e criam usando os Serviços de Aplicativo do Azure](#appservices)
* [Aplicativos/APIs Web que protegem recursos usando .NET OWIN OpenID Connect, WS-Fed ou o middleware WindowsAzureActiveDirectoryBearerAuthentication](#owin)
* [Aplicativos/APIs Web protegendo recursos usando .NET Core OpenID Connect ou o middleware JwtBearerAuthentication](#owincore)
* [Aplicativos/APIs Web que protegem recursos usando o módulo passport-azure-ad do Node.js](#passport)
* [Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2015 ou o Visual Studio 2017](#vs2015)
* [Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2013](#vs2013)
* [APIs Web que protegem recursos e que foram criados com o Visual Studio 2013](#vs2013_webapi)
* [Aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2012](#vs2012)
* [Aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2010, 2008 ou usando o Windows Identity Foundation](#vs2010)
* [Aplicativos da Web / APIs de proteção de recursos usando qualquer outras bibliotecas de ou implementar manualmente qualquer Olá protocolos suportados](#other)

Esta diretriz **não** é aplicável:

* Aplicativos adicionados da Galeria de aplicativo do Azure AD (incluindo personalizada) têm diretrizes separado com relação toosigning chaves. [Mais informações.](../active-directory-sso-certs.md)
* Local aplicativos publicados por meio do proxy de aplicativo não tem tooworry sobre chaves de assinatura.

### <a name="nativeclient"></a>Aplicativos cliente nativos que acessam recursos
Aplicativos que só acessam recursos (ou seja, Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft) geralmente apenas obter um token e passá-lo pelo proprietário do recurso toohello. Considerando que eles não estão protegendo todos os recursos, eles não inspecionam token hello e, portanto, não é necessário tooensure que está assinado corretamente.

Aplicativos cliente nativo, se o desktop ou mobile, entram nessa categoria e, portanto, não são afetados por substituição hello.

### <a name="webclient"></a>Aplicativos/APIs Web que acessam recursos
Aplicativos que só acessam recursos (ou seja, Microsoft Graph, KeyVault, API do Outlook e outras APIs Microsoft) geralmente apenas obter um token e passá-lo pelo proprietário do recurso toohello. Considerando que eles não estão protegendo todos os recursos, eles não inspecionam token hello e, portanto, não é necessário tooensure que está assinado corretamente.

Aplicativos da Web e APIs que estão usando o fluxo de saudação somente de aplicativo web (as credenciais do cliente / certificado do cliente), se enquadram nessa categoria e, portanto, não são afetadas por substituição hello.

### <a name="appservices"></a>Aplicativos/APIs Web que protegem recursos e criam usando os Serviços de Aplicativo do Azure
Autenticação dos serviços de aplicativo do Azure funcionalidade de autorização (EasyAuth) já tem substituição de chave Olá lógica necessária toohandle automaticamente.

### <a name="owin"></a>Aplicativos/APIs Web que protegem recursos usando .NET OWIN OpenID Connect, WS-Fed ou o middleware WindowsAzureActiveDirectoryBearerAuthentication
Se seu aplicativo estiver usando Olá .NET OWIN OpenID Connect, WS-Fed ou middleware WindowsAzureActiveDirectoryBearerAuthentication, ela já tem substituição de chave Olá lógica necessária toohandle automaticamente.

Você pode confirmar que o aplicativo está usando qualquer um desses procurando qualquer Olá trechos de código em seu aplicativo Startup.cs ou Startup.Auth.cs a seguir

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>Aplicativos/APIs Web protegendo recursos usando .NET Core OpenID Connect ou o middleware JwtBearerAuthentication
Se seu aplicativo estiver usando Olá .NET Core OWIN OpenID Connect ou middleware JwtBearerAuthentication, ela já tem substituição de chave Olá lógica necessária toohandle automaticamente.

Você pode confirmar que o aplicativo está usando qualquer um desses procurando qualquer Olá trechos de código em seu aplicativo Startup.cs ou Startup.Auth.cs a seguir

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>Aplicativos/APIs Web que protegem recursos usando o módulo passport-azure-ad do Node.js
Se seu aplicativo estiver usando o módulo de passport ad Node. js hello, ela já tem substituição de chave Olá lógica necessária toohandle automaticamente.

Você pode confirmar que seu aplicativo passport-ad pesquisando Olá seguindo o trecho de código em app.js seu aplicativo

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2015 ou o Visual Studio 2017
Se seu aplicativo foi criado usando um modelo de aplicativo da web no Visual Studio 2015 ou Visual Studio de 2017 e selecionado **contas de trabalho e escolares** de saudação **alterar autenticação** menu, ele já tem a substituição de chave Olá lógica necessária toohandle automaticamente. Esta lógica, inserida no middleware OWIN OpenID Connect hello, recupera e armazena em cache chaves de saudação do documento de descoberta de OpenID Connect hello e atualiza periodicamente.

Se você adicionou a solução de autenticação tooyour manualmente, seu aplicativo pode não ter lógica de substituição de chave necessária hello. Você precisará toowrite-lo por conta própria ou Olá siga as etapas em [aplicativos Web APIs usando quaisquer outras bibliotecas de ou implementar manualmente qualquer Olá suporte protocolos.](#other).

### <a name="vs2013"></a>Aplicativos/APIs Web que protegem recursos e que foram criados com o Visual Studio 2013
Se seu aplicativo foi criado usando um modelo de aplicativo da web no Visual Studio 2013 e você tiver selecionado **contas organizacionais** de saudação **alterar autenticação** menu, ele já tem Olá necessário toohandle lógica de substituição de chave automaticamente. Esta lógica armazena o identificador exclusivo da sua organização e hello assinar informações chave em duas tabelas de banco de dados associados ao projeto de saudação. Você pode encontrar a cadeia de caracteres de conexão de saudação para banco de dados de saudação no arquivo de Web. config do projeto de saudação.

Se você adicionou a solução de autenticação tooyour manualmente, seu aplicativo pode não ter lógica de substituição de chave necessária hello. Você precisará toowrite-lo por conta própria ou Olá siga as etapas em [aplicativos Web APIs usando quaisquer outras bibliotecas de ou implementar manualmente qualquer Olá suporte protocolos.](#other).

Olá, as etapas a seguir o ajudará a verificar se a lógica de saudação está funcionando corretamente em seu aplicativo.

1. No Visual Studio 2013, Olá solução aberta e, em seguida, clique em Olá **Server Explorer** guia na janela direita hello.
2. Expanda **Conexões de Dados**, **DefaultConnection** e **Tabelas**. Localizar Olá **IssuingAuthorityKeys** de tabela, clique duas vezes e, em seguida, clique em **Mostrar dados da tabela**.
3. Em Olá **IssuingAuthorityKeys** da tabela, haverá pelo menos uma linha, que corresponde a toohello o valor de impressão digital da chave de saudação. Exclua todas as linhas na tabela de saudação.
4. Saudação de atalho **locatários** de tabela e, em seguida, clique em **Mostrar dados da tabela**.
5. Em Olá **locatários** da tabela, haverá pelo menos uma linha, que corresponde a tooa identificador do locatário de diretório exclusivo. Exclua todas as linhas na tabela de saudação. Se você não excluir linhas de saudação em ambos os Olá **locatários** tabela e **IssuingAuthorityKeys** tabela, você obterá um erro em tempo de execução.
6. Compilar e executar o aplicativo hello. Depois de fazer logon na conta de tooyour, você pode interromper o aplicativo hello.
7. Retornar toohello **Server Explorer** e examinar valores Olá Olá **IssuingAuthorityKeys** e **locatários** tabela. Você observará que eles foram repopulados automaticamente com informações apropriadas de saudação do documento de metadados de Federação hello.

### <a name="vs2013"></a>APIs Web que protegem recursos e que foram criados com o Visual Studio 2013
Se você criou um aplicativo de API da web no Visual Studio 2013 usando o modelo de API da Web hello e, em seguida, selecionado **contas organizacionais** de saudação **alterar autenticação** menu, você já tiver Olá lógica necessária em seu aplicativo.

Se você configurou manualmente a autenticação, siga as instruções de saudação abaixo toolearn como tooconfigure tooautomatically sua API da Web atualizar suas informações de chave.

Olá trecho de código a seguir demonstra como tooget Olá últimas chaves de documento de metadados de Federação Olá e, em seguida, usar Olá [manipulador de Token de JWT](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate token de saudação. trecho de código Olá pressupõe que você usará seus próprio cache de mecanismo para persistir Olá chave toovalidate futuro tokens do AD do Azure, se estiver em um banco de dados, arquivo de configuração ou em outro lugar.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>Aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2012
Se seu aplicativo foi compilado no Visual Studio 2012, você provavelmente usou hello identidade e tooconfigure da ferramenta de acesso a seu aplicativo. Também é provável que você está usando Olá [do registro de nome de emissor Validando (VINR)](https://msdn.microsoft.com/library/dn205067.aspx). Olá VINR é responsável por manter informações sobre provedores de identidade confiável (AD do Azure) e chaves Olá usado toovalidate tokens emitidos por eles. Olá VINR também torna fácil tooautomatically atualização Olá informações de chave armazenadas em um arquivo Web. config baixando hello mais recente federação documento de metadados associado ao diretório, verificando se a configuração hello está desatualizada com hello mais recente documento e atualização Olá toouse Olá nova chave de aplicativo conforme necessário.

Se você criou seu aplicativo usando qualquer um dos exemplos de código hello ou documentação passo a passo fornecida pela Microsoft, a lógica de substituição de chave Olá já está incluída em seu projeto. Você observará que o código de saudação abaixo já existe em seu projeto. Se seu aplicativo ainda não tiver esta lógica, siga as etapas de saudação abaixo tooadd-lo e tooverify que ele está funcionando corretamente.

1. Em **Solution Explorer**, adicione uma referência toohello **System. IdentityModel** assembly para o projeto apropriado do hello.
2. Olá abrir **Global.asax.cs** de arquivo e adicione o seguinte hello usando diretivas:
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. Adicionar Olá após o método toohello **Global.asax.cs** arquivo:
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Invocar Olá **Refreshvalidationsettings** método hello **Application_Start ()** método **Global.asax.cs** conforme mostrado:
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

Depois de seguir essas etapas, Web. config do seu aplicativo será atualizada com informações mais recentes de saudação do documento de metadados de Federação hello, incluindo chaves mais recentes hello. Essa atualização ocorrerá sempre que recicla o pool de aplicativos no IIS; Por padrão o IIS é definido toorecycle aplicativos cada 29 horas.

Siga as próximas etapas, Olá tooverify Olá lógica de substituição de chave está funcionando.

1. Depois de ter verificado que seu aplicativo está usando código Olá acima, abra Olá **Web. config** de arquivo e navegue toohello  **<issuerNameRegistry>**  bloco, especificamente procurando Olá algumas linhas a seguir:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. Em Olá  **<add thumbprint=””>**  definir, alterar o valor de impressão digital de hello, substituindo qualquer caractere por um diferente. Salvar Olá **Web. config** arquivo.
3. Criar um aplicativo hello e, em seguida, executá-lo. Se você pode concluir o processo de entrada hello, seu aplicativo estará atualizando com êxito chave Olá Baixando informações necessárias de saudação do documento de metadados de Federação do diretório. Se você estiver tendo problemas para entrar, certifique-se de alterações de saudação em seu aplicativo estão corretas, lendo Olá [tooYour adicionar logon usando o aplicativo Web Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) tópico, ou baixe e inspecione Olá exemplo de código a seguir: [ Aplicativo de nuvem multilocatário para Active Directory do Azure](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### <a name="vs2010"></a>Os aplicativos Web que protegem recursos e que foram criados com o Visual Studio 2008 ou 2010 e o Windows Identity Foundation (WIF) v1.0 para .NET 3.5
Se você criou um aplicativo no WIF v 1.0, não há nenhuma atualização do mecanismo fornecido tooautomatically toouse de configuração do aplicativo uma nova chave.

* *A maneira mais fácil* usar Olá FedUtil ferramentas incluídas no hello WIF SDK, que pode recuperar o documento de metadados mais recente hello e atualizar sua configuração.
* Atualize seu too.NET aplicativo 4.5, que inclui a versão mais recente de saudação do WIF localizado no namespace do sistema de saudação. Você pode usar Olá [do registro de nome de emissor Validando (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform as atualizações automáticas de configuração do aplicativo hello.
* Execute a substituição de um manual conforme as instruções de saudação final Olá deste documento orientação.

Instruções toouse Olá FedUtil tooupdate sua configuração:

1. Verifique se você tem Olá WIF v 1.0 SDK instalado no computador de desenvolvimento para Visual Studio 2008 ou 2010. Você pode [baixá-lo daqui](https://www.microsoft.com/en-us/download/details.aspx?id=4451) se ainda não estiver instalado.
2. No Visual Studio, abra a solução Olá e, em seguida, clique com botão direito Olá aplicável e selecione **atualizar metadados de Federação**. Se essa opção não estiver disponível, FedUtil e/ou Olá WIF v 1.0 SDK não foi instalado.
3. No prompt de saudação, selecione **atualização** toobegin atualizar seus metadados de Federação. Se você tiver um ambiente de servidor toohello de acesso onde o aplicativo hello está hospedado, opcionalmente, você pode usar do FedUtil [Agendador de atualização automática de metadados](https://msdn.microsoft.com/library/ee517272.aspx).
4. Clique em **concluir** toocomplete processo de atualização de saudação.

### <a name="other"></a>Aplicativos da Web / APIs de proteção de recursos usando qualquer outras bibliotecas de ou implementar manualmente qualquer Olá protocolos suportados
Se você estiver usando alguma outra biblioteca ou implementado manualmente qualquer um dos protocolos Olá com suporte, você precisará de biblioteca de saudação tooreview ou tooensure sua implementação que Olá chave está sendo recuperado do documento de descoberta de OpenID Connect hello ou hello documento de metadados de Federação. Toocheck unidirecional para isso é toodo uma pesquisa em seu código ou o código da biblioteca de saudação para todas as chamadas de documento de descoberta de OpenID tooeither hello ou documento de metadados de Federação hello.

Se eles chave é armazenada em ou codificado no seu aplicativo, você pode manualmente recupere chave hello e ele adequadamente ao executar a substituição de um manual conforme as instruções de saudação final Olá deste documento Guia de atualização. **Ele é incentivado fortemente que você aperfeiçoe a substituição automática do aplicativo toosupport** usando qualquer um dos Olá abordagens da estrutura de tópicos neste interrupções futuras do artigo tooavoid e sobrecarga de AD do Azure aumenta o ritmo da substituição ou possui um substituição de emergência fora de banda.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>Como tootest toodetermine seu aplicativo se serão afetado
Você pode validar se o aplicativo oferece suporte a substituição da chave automática baixando scripts hello e seguindo as instruções de saudação do [este repositório GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>Como tooperform uma substituição manual se seu aplicativo não oferece suporte a substituição automática
Se seu aplicativo **não** suporte a substituição automática, será necessário tooestablish chaves de um processo que periodicamente de assinatura de monitores AD do Azure e executa a substituição de um manual adequadamente. [Esse repositório GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contém scripts e instruções sobre como toodo isso.

