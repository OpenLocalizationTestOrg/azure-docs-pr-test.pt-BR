---
title: "aaaCommunication segurança - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
description: "reduções de ameaças expostas em Olá, ferramenta de modelagem de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 667829c75123f4dbe0b383fdaf8cd899802f9b16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-communication-security--mitigations"></a>Estrutura de segurança: Segurança de comunicações | Atenuações 
| Produto/serviço | Artigo |
| --------------- | ------- |
| **Hub de Eventos do Azure** | <ul><li>[Comunicação segura tooEvent Hub usando SSL/TLS](#comm-ssltls)</li></ul> |
| **Dynamics CRM** | <ul><li>[Verifique a conta de serviço, privilégios e verificar se Olá personalizado serviços ou páginas ASP.NET respeitam a segurança do CRM](#priv-aspnet)</li></ul> |
| **Azure Data Factory** | <ul><li>[Usar o gateway de gerenciamento de dados durante a conexão local SQL Server tooAzure fábrica de dados](#sqlserver-factory)</li></ul> |
| **Identity Server** | <ul><li>[Verifique se todos os tooIdentity de tráfego servidor pela conexão HTTPS](#identity-https)</li></ul> |
| **Aplicativo Web** | <ul><li>[Verifique se os certificados x. 509 usado tooauthenticate conexões de SSL, TLS e DTLS](#x509-ssltls)</li><li>[Configurar um certificado SSL para um domínio personalizado no Serviço de Aplicativo do Azure](#ssl-appservice)</li><li>[Forçar tooAzure todo o tráfego do serviço de aplicativo pela conexão HTTPS](#appservice-https)</li><li>[Habilitar HSTS (Segurança de Transporte Estrito HTTP)](#http-hsts)</li></ul> |
| **Banco de dados** | <ul><li>[Garantir a validação de certificado e a criptografia da conexão do SQL Server](#sqlserver-validation)</li><li>[Forçar o servidor de tooSQL de comunicação criptografados](#encrypted-sqlserver)</li></ul> |
| **Armazenamento do Azure** | <ul><li>[Certifique-se de que tooAzure comunicação que armazenamento é HTTPS](#comm-storage)</li><li>[Validar o hash MD5 depois de baixar o blob se o HTTPS não puder ser habilitado](#md5-https)</li><li>[Tooensure de cliente compatível do SMB 3.0 de uso de criptografia de dados tooAzure compartilhamentos de arquivos em trânsito](#smb-shares)</li></ul> |
| **Cliente móvel** | <ul><li>[Implementar a anexação de certificado](#cert-pinning)</li></ul> |
| **WCF** | <ul><li>[Habilitar HTTPS - proteger o canal de transporte](#https-transport)</li><li>[WCF: TooEncryptAndSign nível de proteção mensagem de conjunto de segurança](#message-protection)</li><li>[WCF: Use uma conta menos privilegiada toorun seu serviço WCF](#least-account-wcf)</li></ul> |
| **API da Web** | <ul><li>[Forçar todos os tráfego tooWeb APIs pela conexão HTTPS](#webapi-https)</li></ul> |
| **Cache Redis do Azure** | <ul><li>[Certifique-se de que tooAzure comunicação que cache Redis é sobre SSL](#redis-ssl)</li></ul> |
| **Gateway de Campo de IoT** | <ul><li>[Proteger a comunicação do dispositivo tooField Gateway](#device-field)</li></ul> |
| **Gateway de Nuvem IoT** | <ul><li>[Proteger dispositivos tooCloud comunicação Gateway usando o SSL/TLS](#device-cloud)</li></ul> |

## <a id="comm-ssltls"></a>Comunicação segura tooEvent Hub usando SSL/TLS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Hub de Eventos do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Visão geral do modelo de autenticação e segurança dos Hubs de Eventos](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Etapas** | Proteger conexões de AMQP ou HTTP tooEvent Hub usando SSL/TLS |

## <a id="priv-aspnet"></a>Verifique a conta de serviço, privilégios e verificar se Olá personalizado serviços ou páginas ASP.NET respeitam a segurança do CRM

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Verifique a conta de serviço, privilégios e verificar se Olá personalizado serviços ou páginas ASP.NET respeitam a segurança do CRM |

## <a id="sqlserver-factory"></a>Usar o gateway de gerenciamento de dados durante a conexão local SQL Server tooAzure fábrica de dados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Fábrica de dados do Azure | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Tipos de serviços vinculados - no Azure e localmente |
| **Referências**              |[Movendo dados entre o armazenamento local e o Azure Data Factory](https://azure.microsoft.com/documentation/articles/data-factory-move-data-between-onprem-and-cloud/#create-gateway), [Gateway de Gerenciamento de Dados](https://azure.microsoft.com/documentation/articles/data-factory-data-management-gateway/) |
| **Etapas** | <p>a ferramenta de Gateway de gerenciamento de dados (DMG) Olá é necessário tooconnect toodata fontes que são protegidos por trás de um firewall ou a rede corporativa.</p><ol><li>Bloquear o computador Olá isola a ferramenta DMG Olá e impede que programas mau funcionamento danifique ou espionagem no computador de origem de dados de saudação. Por exemplo, instalando das atualizações mais recentes, habilitando o mínimo necessário de portas, provisionando contas controladas, habilitando a auditoria, habilitando a criptografia de disco, etc.</li><li>Chave do Gateway de dados deve ser girado em intervalos frequentes ou sempre que a senha da conta de serviço do hello DMG renova</li><li>O tráfego de dados pelo serviço de vinculação deve ser criptografado.</li></ol> |

## <a id="identity-https"></a>Verifique se todos os tooIdentity de tráfego servidor pela conexão HTTPS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Servidor de Identidade | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [IdentityServer3 - chaves, assinaturas e criptografia](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html), [IdentityServer3 - implantação](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Etapas** | Por padrão, IdentityServer requer que todos os toocome de conexões de entrada via HTTPS. É absolutamente obrigatório que a comunicação com IdentityServer seja feita apenas transportes protegidos. Em alguns cenários de implantação, como o de descarregamento de SSL, esse requisito pode ser relaxado. Consulte a página de implantação de servidor de identidade Olá em referências de saudação para obter mais informações. |

## <a id="x509-ssltls"></a>Verifique se os certificados x. 509 usado tooauthenticate conexões de SSL, TLS e DTLS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Aplicativos que usam SSL, TLS e DTLS totalmente devem verificar certificados x. 509 de saudação de entidades de saudação que se conectam ao. Isso inclui a verificação de certificados Olá para:</p><ul><li>Nome de domínio</li><li>Datas de validade (datas de início e vencimento)</li><li>Status de revogação</li><li>Uso (por exemplo, autenticação de servidor para servidores de autenticação de cliente para clientes)</li><li>Cadeia de confiança Certificados devem se encadear autoridade de certificação tooa raiz (CA) confiável pela plataforma de saudação ou explicitamente configurada pelo administrador de saudação</li><li>O comprimento da chave pública do certificado deve ser maior que 2.048 bits</li><li>Algoritmo de hash deve ser SHA256 e superior |

## <a id="ssl-appservice"></a>Configurar um certificado SSL para um domínio personalizado no Serviço de Aplicativo do Azure

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Tipo de ambiente - Azure |
| **Referências**              | [Habilitar HTTPS para um aplicativo no Serviço de Aplicativo do Azure](https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/) |
| **Etapas** | Por padrão, o Azure já habilita HTTPS para todos os aplicativos com um certificado curinga para hello *. domínio azurewebsites.net. No entanto, assim como todos os domínios curinga, ele não é tão seguro quanto usar um domínio personalizado com seu próprio certificado. [Consulte este artigo](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/). É recomendável tooenable SSL para o qual aplicativo hello implantado será acessado por meio de domínio personalizado do hello|

## <a id="appservice-https"></a>Forçar tooAzure todo o tráfego do serviço de aplicativo pela conexão HTTPS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Tipo de ambiente - Azure |
| **Referências**              | [Impor o HTTPS no Serviço de Aplicativo do Azure]https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/#4-enforce-https-on-your-app |
| **Etapas** | <p>Embora o Azure permite já HTTPS para serviços de aplicativo do Azure com um certificado curinga para domínio hello *. azurewebsites.net, ele não impõem HTTPS. Os visitantes ainda podem acessar o aplicativo hello usando HTTP, que pode comprometer a segurança do aplicativo hello e, portanto, o HTTPS tem toobe imposta explicitamente. Aplicativos ASP.NET MVC devem usar Olá [RequireHttps filtro](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) que força uma toobe de solicitação HTTP não segura reenviada via HTTPS.</p><p>Como alternativa, Olá URL Rewrite module, que é incluído com o serviço de aplicativo do Azure pode ser usado tooenforce HTTPS. Módulo de reescrita de URL permite que os desenvolvedores toodefine regras de solicitações de tooincoming aplicada antes Olá solicitações são passadas tooyour aplicativo. Regras de reescrita de URL são definidas em um arquivo Web. config armazenado na raiz de saudação do aplicativo hello</p>|

### <a name="example"></a>Exemplo
Hello, exemplo a seguir contém uma regra de regravação de URL básica que força toouse de todo o tráfego HTTPS
```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
Essa regra funciona, retornando um código de status HTTP de 301 (redirecionamento permanente) quando o usuário Olá solicita uma página usando HTTP. Olá 301 redirecionamentos Olá solicitação toohello mesma URL que o visitante Olá solicitada, mas substitui Olá HTTP parte da solicitação de saudação com HTTPS. Por exemplo, HTTP://contoso.com seria tooHTTPS://contoso.com redirecionado. 

## <a id="http-hsts"></a>Habilitar HSTS (Segurança de Transporte Estrito HTTP)

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Folha de dados do OWASP sobre Segurança de Transporte Estrito HTTP](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) |
| **Etapas** | <p>Segurança de transporte estrito HTTP (HSTS) é um aprimoramento de segurança de aceitação do que é especificado por um aplicativo web por meio do uso de saudação de um cabeçalho de resposta especial. Depois que um navegador com suporte recebe esse cabeçalho navegador impedirá todas as comunicações sejam enviadas pela domínio especificado do HTTP toohello e enviará, em vez disso, todas as comunicações via HTTPS. Ele também impede cliques via HTTPS em prompts de navegadores.</p><p>tooimplement HSTS, Olá cabeçalho de resposta a seguir tem toobe configurado para um site globalmente, no código ou na configuração. Transporte segurança Strict: max-age = 300; includeSubDomains HSTS endereços Olá ameaças a seguir:</p><ul><li>Usuário indicadores ou tipos http://example.com e manualmente é invasor do assunto tooa man-in-the-middle: HSTS redireciona automaticamente tooHTTPS de solicitações HTTP para o domínio de destino Olá</li><li>Aplicativo que é pretendido toobe puramente HTTPS inadvertidamente contém links HTTP ou serve conteúdo por HTTP da Web: HSTS redireciona automaticamente tooHTTPS de solicitações HTTP para o domínio de destino Olá</li><li>Um invasor man-in-the-middle tentativas toointercept tráfego de um usuário vítima usando um certificado inválido e espera usuário Olá aceitará certificado incorreto Olá: HSTS não permite uma mensagem de certificado inválido de saudação do usuário toooverride</li></ul>|

## <a id="sqlserver-validation"></a>Garantir a validação de certificado e a criptografia da conexão do SQL Server

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | SQL Azure  |
| **Atributos**              | Versão do SQL - V12 |
| **Referências**              | [Práticas recomendadas para escrever cadeias de caracteres de conexão seguras para o banco de dados SQL](http://social.technet.microsoft.com/wiki/contents/articles/2951.windows-azure-sql-database-connection-security.aspx#best) |
| **Etapas** | <p>Todas as comunicações entre o banco de dados SQL e um aplicativo cliente são criptografadas usando Secure Sockets Layer (SSL) o tempo todo. O banco de dados SQL não oferece suporte a conexões não criptografadas. certificados de toovalidate com código de aplicativo ou as ferramentas, explicitamente solicitar uma conexão criptografada e não confiar em certificados de saudação do servidor. Se o código ou as ferramentas do aplicativo não solicitam uma conexão criptografada, eles continuarão receberão conexões criptografadas.</p><p>No entanto, eles não podem validar certificados de saudação do servidor e, portanto, ficarão suscetíveis muito ataques "man no meio Olá". toovalidate certificados com o código do aplicativo ADO.NET, defina `Encrypt=True` e `TrustServerCertificate=False` na cadeia de conexão de banco de dados de saudação. certificados de toovalidate por meio do SQL Server Management Studio, abra a caixa de diálogo de tooServer de conectar-se de hello. Clique em criptografar conexão na guia de propriedades de Conexão de saudação</p>|

## <a id="encrypted-sqlserver"></a>Forçar o servidor de tooSQL de comunicação criptografados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | OnPrem |
| **Atributos**              | Versão do SQL - MsSQL2016, Versão do SQL - MsSQL2012, Versão do SQL - MsSQL2014 |
| **Referências**              | [Habilitar conexões criptografadas toohello mecanismo de banco de dados](https://msdn.microsoft.com/library/ms191192)  |
| **Etapas** | Habilitar o SSL criptografia aumenta a segurança de saudação dos dados transmitidos pelas redes entre instâncias do SQL Server e aplicativos. |

## <a id="comm-storage"></a>Certifique-se de que tooAzure comunicação que armazenamento é HTTPS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Criptografia no nível do transporte do Armazenamento do Azure – usando HTTPS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_encryption-in-transit) |
| **Etapas** | tooensure segurança de saudação do armazenamento do Azure dados em trânsito, sempre use o protocolo HTTPS de saudação ao chamar hello APIs REST ou acessar objetos no armazenamento. Além disso, assinaturas de acesso compartilhado, que pode ser usado toodelegate acessar objetos de armazenamento tooAzure, incluem uma opção toospecify que Olá somente pode ser usado o protocolo HTTPS ao usar assinaturas de acesso compartilhado, garantindo que qualquer pessoa enviando links com tokens SAS será Use protocolo correto hello.|

## <a id="md5-https"></a>Validar o hash MD5 depois de baixar o blob se o HTTPS não puder ser habilitado

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | StorageType - Blob |
| **Referências**              | [Visão geral da MD5 do Blob do Azure](https://blogs.msdn.microsoft.com/windowsazurestorage/2011/02/17/windows-azure-blob-md5-overview/) |
| **Etapas** | <p>Serviço de Blob do Windows Azure fornece integridade de dados de tooensure de mecanismos tanto nas camadas de transporte e o aplicativo hello. Se por algum motivo, você precisa toouse HTTP em vez de HTTPS e você estiver trabalhando com blobs de bloco, você pode usar a verificação MD5 toohelp verificar a integridade de saudação de blobs Olá que estão sendo transferidos</p><p>Isso ajudará na proteção contra erros na camada de rede/transporte, mas não necessariamente contra ataques de intermediários. Se você puder usar HTTPS, que fornece segurança em nível de transporte, o uso da verificação MD5 será redundante e desnecessário.</p>|

## <a id="smb-shares"></a>Usar tooAzure de criptografia de dados em trânsito do SMB 3.0 cliente compatível tooensure que compartilhamentos de arquivos

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvel | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Tipo de armazenamento - Arquivo |
| **Referências**              | [Armazenamento de Arquivos do Azure](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/#comment-2529238931), [Suporte do Armazenamento de Arquivos do Azure para SMB em clientes Windows](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/#_mount-the-file-share) |
| **Etapas** | Armazenamento de arquivo do Azure dá suporte a HTTPS ao usar a API REST de saudação, mas é mais comumente usado como um compartilhamento de arquivos SMB anexado tooa VM. SMB 2.1 não oferece suporte a criptografia, portanto conexões só são permitidos no hello mesmo região no Azure. No entanto, SMB 3.0 oferece suporte à criptografia e pode ser usado com o Windows Server 2012 R2, Windows 8, Windows 8.1 e Windows 10, permitindo entre regiões acessar e até mesmo acesso na área de trabalho de saudação. |

## <a id="cert-pinning"></a>Implementar a anexação de certificado

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Armazenamento do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, Windows Phone |
| **Atributos**              | N/D  |
| **Referências**              | [Anexação de chave pública e certificado](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#.Net) |
| **Etapas** | <p>A anexação de certificado protege contra ataques MITM (Man-In-The-Middle). Fixando é o processo de saudação de associar um host com seus X509 esperado certificado ou chave pública. Depois que um certificado ou chave pública é conhecida ou Vista para um host, Olá certificado ou chave pública é toohello associado ou 'fixo' host. </p><p>Assim, quando um adversário tenta toodo ataque MITM SSL, durante a chave de saudação do handshake SSL do servidor de um invasor será diferente da saudação fixado chave do certificado e solicitação hello será descartada, evitando assim que o certificado MITM fixação pode ser obtida com implementação do ServicePointManager `ServerCertificateValidationCallback` delegate.</p>|

### <a name="example"></a>Exemplo
```C#
using System;
using System.Net;
using System.Net.Security;
using System.Security.Cryptography;

namespace CertificatePinningExample
{
    class CertificatePinningExample
    {
        /* Note: In this example, we're hardcoding a hello certificate's public key and algorithm for 
           demonstration purposes. In a real-world application, this should be stored in a secure
           configuration area that can be updated as needed. */

        private static readonly string PINNED_ALGORITHM = "RSA";

        private static readonly string PINNED_PUBLIC_KEY = "3082010A0282010100B0E75B7CBE56D31658EF79B3A1" +
            "294D506A88DFCDD603F6EF15E7F5BCBDF32291EC50B2B82BA158E905FE6A83EE044A48258B07FAC3D6356AF09B2" +
            "3EDAB15D00507B70DB08DB9A20C7D1201417B3071A346D663A241061C151B6EC5B5B4ECCCDCDBEA24F051962809" +
            "FEC499BF2D093C06E3BDA7D0BB83CDC1C2C6660B8ECB2EA30A685ADE2DC83C88314010FFC7F4F0F895EDDBE5C02" +
            "ABF78E50B708E0A0EB984A9AA536BCE61A0C31DB95425C6FEE5A564B158EE7C4F0693C439AE010EF83CA8155750" +
            "09B17537C29F86071E5DD8CA50EBD8A409494F479B07574D83EDCE6F68A8F7D40447471D05BC3F5EAD7862FA748" +
            "EA3C92A60A128344B1CEF7A0B0D94E50203010001";


        public static void Main(string[] args)
        {
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://azure.microsoft.com");
            request.ServerCertificateValidationCallback = (sender, certificate, chain, sslPolicyErrors) =>
            {
                if (certificate == null || sslPolicyErrors != SslPolicyErrors.None)
                {
                    // Error getting certificate or hello certificate failed basic validation
                    return false;
                }

                var targetKeyAlgorithm = new Oid(certificate.GetKeyAlgorithm()).FriendlyName;
                var targetPublicKey = certificate.GetPublicKeyString();
                
                if (targetKeyAlgorithm == PINNED_ALGORITHM &&
                    targetPublicKey == PINNED_PUBLIC_KEY)
                {
                    // Success, hello certificate matches hello pinned value.
                    return true;
                }
                // Reject, either hello key or hello algorithm does not match hello expected value.
                return false;
            };

            try
            {
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine($"Success, HTTP status code: {response.StatusCode}");
            }
            catch(Exception ex)
            {
                Console.WriteLine($"Failure, {ex.Message}");
            }
            Console.WriteLine("Press any key tooend.");
            Console.ReadKey();
        }
    }
}
```

## <a id="https-transport"></a>Habilitar HTTPS - proteger o canal de transporte

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Etapas** | configuração de aplicativo Hello deve garantir que o HTTPS é usado para todas as informações de toosensitive de acesso.<ul><li>**EXPLICAÇÃO:** se um aplicativo lida com informações confidenciais e não usar a criptografia de nível de mensagem, ele só deve ter permissão toocommunicate por um canal criptografado de transporte.</li><li>**RECOMENDAÇÕES:** verifique se o transporte HTTP está desabilitado e habilite o transporte HTTPS em vez disso. Por exemplo, substitua Olá `<httpTransport/>` com `<httpsTransport/>` marca. Não confie em um tooguarantee (firewall) de configuração de rede que o aplicativo hello só pode ser acessado por um canal seguro. Do ponto de vista filosóficas aplicativo hello não deve depender rede Olá para sua segurança.</li></ul><p>Do ponto de vista prático, Olá responsáveis para proteger a rede de saudação não sempre controlam os requisitos de segurança de saudação do aplicativo hello como sua evolução.</p>|

## <a id="message-protection"></a>WCF: TooEncryptAndSign nível de proteção mensagem de conjunto de segurança

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff650862.aspx) |
| **Etapas** | <ul><li>**EXPLICAÇÃO:** quando o nível de proteção está definido muito "none" ele desativará a proteção da mensagem. A confidencialidade e a integridade dos dados só são conquistadas com o nível apropriado de configuração.</li><li>**RECOMENDAÇÕES:**<ul><li>`Mode=None` - desabilita a proteção de mensagem</li><li>Quando `Mode=Sign` -sinais mas não criptografa a mensagem de saudação; deve ser usados quando a integridade dos dados é importante</li><li>Quando `Mode=EncryptAndSign` -sinais e criptografa a mensagem de saudação</li></ul></li></ul><p>Considere a desativação da criptografia e assinar apenas uma mensagem quando você precisa apenas a integridade de saudação do toovalidate das informações de saudação sem preocupações de confidencialidade. Isso pode ser útil para operações ou contratos de serviço no qual você precisa do remetente original toovalidate hello, mas não há dados confidenciais são transmitidos. Ao reduzir o nível de proteção hello, tenha cuidado que essa mensagem de saudação não contém qualquer informação de identificação pessoal (PII).</p>|

### <a name="example"></a>Exemplo
Configurar o serviço de saudação e mensagem de saudação do hello operação tooonly sinal é mostrado no hello exemplos a seguir. Exemplo de contrato de serviço de `ProtectionLevel.Sign`: Olá seguir está um exemplo do uso de ProtectionLevel.Sign no nível do contrato de serviço hello: 
```
[ServiceContract(Protection Level=ProtectionLevel.Sign] 
public interface IService 
  { 
  string GetData(int value); 
  } 
```

### <a name="example"></a>Exemplo
Exemplo de contrato de operação de `ProtectionLevel.Sign` (para um controle Granular): Olá seguir está um exemplo de como usar `ProtectionLevel.Sign` no hello OperationContract nível:

```
[OperationContract(ProtectionLevel=ProtectionLevel.Sign] 
string GetData(int value);
``` 

## <a id="least-account-wcf"></a>WCF: Use uma conta menos privilegiada toorun seu serviço WCF

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff648826.aspx ) |
| **Etapas** | <ul><li>**EXPLICAÇÃO:** não execute serviços do WCF usando contas de administrador ou com privilégios altos. Se os serviços forem comprometidos, isso pode ter um impacto alto.</li><li>**RECOMENDAÇÕES:** usar um toohost conta menos privilegiada o WCF serviço porque ele reduzir a superfície de ataque do seu aplicativo e reduzir o dano potencial Olá se estão sendo atacado. Se a conta de serviço de saudação requer direitos de acesso adicionais nos recursos de infraestrutura, como MSMQ, hello permissões apropriadas do log de eventos, contadores de desempenho e sistema de arquivos hello, devem ser dadas recursos toothese para que o serviço do WCF Olá pode ser executado com êxito.</li></ul><p>Se seu serviço precisar de recursos específicos de tooaccess em nome do chamador original hello, use representação e a identidade do chamador do delegação tooflow Olá para uma verificação de autorização de downstream. Em um cenário de desenvolvimento, use a conta de serviço de rede local hello, que é uma conta interna especial que tem menos privilégios. Em um cenário de produção, crie uma conta de serviço de domínio personalizada com privilégios mínimos.</p>|

## <a id="webapi-https"></a>Forçar todos os tráfego tooWeb APIs pela conexão HTTPS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | [Impondo o SSL em um controlador de API da Web](http://www.asp.net/web-api/overview/security/working-with-ssl-in-web-api) |
| **Etapas** | Se um aplicativo tiver um HTTPS e uma associação HTTP, os clientes ainda podem usar o site de saudação tooaccess HTTP. tooprevent isso, use um tooensure de filtro de ação que solicita tooprotected APIs são sempre em HTTPS.|

### <a name="example"></a>Exemplo 
Olá código a seguir mostra um filtro de autenticação de API da Web que verifica o SSL: 
```C#
public class RequireHttpsAttribute : AuthorizationFilterAttribute
{
    public override void OnAuthorization(HttpActionContext actionContext)
    {
        if (actionContext.Request.RequestUri.Scheme != Uri.UriSchemeHttps)
        {
            actionContext.Response = new HttpResponseMessage(System.Net.HttpStatusCode.Forbidden)
            {
                ReasonPhrase = "HTTPS Required"
            };
        }
        else
        {
            base.OnAuthorization(actionContext);
        }
    }
}
```
Adicione esse filtro tooany API da Web que exigem SSL: 
```C#
public class ValuesController : ApiController
{
    [RequireHttps]
    public HttpResponseMessage Get() { ... }
}
```
 
## <a id="redis-ssl"></a>Certifique-se de que tooAzure comunicação que cache Redis é sobre SSL

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Cache Redis do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Suporte a SSL do Redis do Azure](https://azure.microsoft.com/documentation/articles/cache-faq/#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis) |
| **Etapas** | Redis servidor não dá suporte a SSL imediato saudação, mas não de Cache Redis do Azure. Se você estiver se conectando tooAzure Redis Cache e o cliente oferece suporte a SSL, como Stackexchange, você deve usar SSL. Por padrão, a porta não SSL está desabilitada para novas instâncias do Cache Redis do Azure. Certifique-se de padrões seguros Olá não são alterados a menos que haja uma dependência no suporte a SSL para clientes redis. |

Observe que o Redis é projetado toobe acessado por clientes confiáveis em ambientes confiáveis. Isso significa que geralmente não é uma boa ideia Olá tooexpose Redis diretamente instância toohello internet ou, em geral, tooan ambiente em que os clientes não confiáveis podem acessar diretamente Olá a porta TCP Redis ou soquete do UNIX. 

## <a id="device-field"></a>Proteger a comunicação do dispositivo tooField Gateway

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Campo de IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Para dispositivos com base em IP, protocolo de comunicação de saudação normalmente pode ser encapsulado em um SSL/TLS canal tooprotect de dados em trânsito. Para outros protocolos que não oferecem suporte a SSL/TLS investigar se há versões seguras do protocolo de saudação que fornecem segurança na camada de transporte ou mensagem. |

## <a id="device-cloud"></a>Proteger dispositivos tooCloud comunicação Gateway usando o SSL/TLS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Nuvem IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Escolha seu protocolo de comunicação](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#messaging) |
| **Etapas** | Proteja os protocolos HTTP/AMQP ou MQTT usando SSL/TLS. |
