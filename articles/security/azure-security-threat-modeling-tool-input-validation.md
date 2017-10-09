---
title: "aaaInput validação - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
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
ms.openlocfilehash: 823503881f4bae292ef021834d5e64acf2a0f54a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-input-validation--mitigations"></a>Estrutura de segurança: validação de entrada | Atenuações 
| Produto/Serviço | Artigo |
| --------------- | ------- |
| **Aplicativo Web** | <ul><li>[Desabilite o script XSLT para todas as transformações com uso de folhas de estilo não confiáveis](#disable-xslt)</li><li>[Verifique se cada página que pode ter conteúdo controlável pelo usuário recusa a detecção automática de MIME](#out-sniffing)</li><li>[Proteger ou desabilitar a resolução de entidade XML](#xml-resolution)</li><li>[Aplicativos que usam http.sys executam a verificação de conversão em formato canônico de URL](#app-verification)</li><li>[Verifique se os controles adequados estão em vigor ao aceitar arquivos de usuários](#controls-users)</li><li>[Verifique se os parâmetros de tipo seguro são usados no aplicativo Web para acesso a dados](#typesafe)</li><li>[Usar as classes de associação de modelo separado ou listas de filtro de associação de vulnerabilidade de atribuição em massa de MVC tooprevent](#binding-mvc)</li><li>[Codificar toorendering anterior de saída da web não confiável](#rendering)</li><li>[Execute a validação de entrada e a filtragem em todos os tipos de cadeia de caracteres de propriedades do modelo](#typemodel)</li><li>[A limpeza deve ser aplicada em campos de formulário que aceitam todos os caracteres, como o editor de rich text](#richtext)</li><li>[Não atribua toosinks de elementos DOM que não têm embutidas de codificação](#inbuilt-encode)</li><li>[Validar todos os redirecionamentos de dentro do aplicativo hello serão fechados ou feitos com segurança](#redirect-safe)</li><li>[Implemente a validação de entrada em todos os parâmetros de tipo de cadeia de caracteres aceitos por métodos do Controlador](#string-method)</li><li>[Definir tempo limite de limite superior de expressão regular de processamento DoS tooprevent devido a expressões regulares toobad](#dos-expression)</li><li>[Evite usar Html.Raw nos modos de exibição do Razor](#html-razor)</li></ul> | 
| **Banco de dados** | <ul><li>[Não use consultas dinâmicas em procedimentos armazenados](#stored-proc)</li></ul> |
| **API da Web** | <ul><li>[Verifique se a validação do modelo é feita nos métodos de API Web](#validation-api)</li><li>[Implemente a validação de entrada em todos os parâmetros de tipo de cadeia de caracteres aceitos pelos métodos de API Web](#string-api)</li><li>[Verifique se os parâmetros de tipo seguro são usados na API Web para acesso a dados](#typesafe-api)</li></ul> | 
| **Azure DocumentDB** | <ul><li>[Usar consultas SQL parametrizadas para DocumentDB](#sql-docdb)</li></ul> | 
| **WCF** | <ul><li>[Validação de entrada de WCF por meio de associação de esquema](#schema-binding)</li><li>[Validação de entrada de WCF por meio de Inspetores de Parâmetro](#parameters)</li></ul> |

## <a id="disable-xslt"></a>Desabilite os scripts XSLT para todas as transformações usando folhas de estilo não confiáveis

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Segurança do XSLT](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx), [Propriedade XsltSettings](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx) |
| **Etapas** | XSLT oferece suporte a scripts dentro de folhas de estilo usando Olá `<msxml:script>` elemento. Isso permite que funções personalizadas toobe usado em uma transformação XSLT. Olá script é executado no contexto de saudação do processo de saudação executando Olá transformação. Script XSLT deve ser desabilitada quando em execução tooprevent não confiável do ambiente de código não confiável. *Se o uso do .NET:* script XSLT é desabilitado por padrão; no entanto, você deve garantir que ele não foi explicitamente habilitado por meio de saudação `XsltSettings.EnableScript` propriedade.|

### <a name="example"></a>Exemplo 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Exemplo
Se você estiver usando MSXML 6.0, XSLT de script está desabilitado por padrão. No entanto, você deve garantir que ele não foi explicitamente habilitado por meio da propriedade do objeto XML DOM Olá AllowXsltScript. 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Exemplo
Se você estiver usando MSXML 5 ou anterior, o script XSLT será habilitado por padrão, e você deverá desabilitá-lo explicitamente. Defina Olá XML DOM objeto propriedade AllowXsltScript toofalse. 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting toofalse disables XSLT scripting.
```

## <a id="out-sniffing"></a>Verifique se cada página que pode ter conteúdo controlável pelo usuário recusa a detecção automática de MIME

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Segurança do IE8 parte V - proteção abrangente](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)  |
| **Etapas** | <p>Para cada página que pode conter conteúdo controlável do usuário, você deve usar o hello cabeçalho HTTP `X-Content-Type-Options:nosniff`. toocomply com esse requisito, você pode cabeçalho necessário qualquer conjunto Olá página por página para somente as páginas que podem conter conteúdo usuário controlável ou você pode defini-lo globalmente para todas as páginas no aplicativo hello.</p><p>Cada tipo de arquivo entregue a partir de um servidor da web possui um tipo de [tipo MIME](http://en.wikipedia.org/wiki/Mime_type) (também chamado de um *tipo de conteúdo*) que descreve a natureza de saudação do conteúdo hello (ou seja, imagem, texto, aplicativo, etc.)</p><p>cabeçalho Olá X conteúdo-tipo de opções é um cabeçalho HTTP que permite aos desenvolvedores toospecify que seu conteúdo não deve ser detectados MIME. Esse cabeçalho é projetado toomitigate ataques de detecção de MIME. Foi adicionado suporte para esse cabeçalho no Internet Explorer 8 (IE8)</p><p>Somente os usuários do Internet Explorer 8 (IE8) se beneficiarão de Content-Type-Options. Versões anteriores do Internet Explorer não respeitam atualmente cabeçalho X-conteúdo-opções de tipo de saudação</p><p>Internet Explorer 8 (e posterior) são Olá apenas principais navegadores tooimplement MIME-sniffing recusar o recurso. Se e quando os principais navegadores (Firefox, Safari, Chrome) implementam recursos semelhantes, essa recomendação será atualizado tooinclude sintaxe para esses navegadores</p>|

### <a name="example"></a>Exemplo
cabeçalho necessário de saudação de tooenable globalmente para todas as páginas no aplicativo hello, você pode fazer um dos seguintes hello: 

* Adicionar cabeçalho Olá no arquivo Web. config de saudação se o aplicativo hello é hospedado pelo Internet Information Services (IIS) 7 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* Adicionar cabeçalho Olá Olá aplicativo global\_BeginRequest 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* Implementar o módulo HTTP personalizado 

``` 
public class XContentTypeOptionsModule : IHttpModule 
  {
    #region IHttpModule Members 
    public void Dispose() 
    { 

    } 
    public void Init(HttpApplication context)
    { 
      context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders); 
    } 
    #endregion 
    void context_PreSendRequestHeaders(object sender, EventArgs e) 
      { 
        HttpApplication application = sender as HttpApplication; 
        if (application == null) 
          return; 
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* Você pode habilitar o cabeçalho de saudação necessário apenas para páginas específicas, adicionando-tooindividual respostas: 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <a id="xml-resolution"></a>Proteger ou desabilitar a resolução de entidade XML

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Expansão de Entidade XML](http://capec.mitre.org/data/definitions/197.html), [Ataques de negação de serviço de XML e defesas](http://msdn.microsoft.com/magazine/ee335713.aspx), [Visão geral de segurança do MSXML](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx), [Práticas recomendadas para proteger o código do MSXML](http://msdn.microsoft.com/library/ms759188(VS.85).aspx), [Referência de protocolo NSXMLParserDelegate](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html), [Resolvendo referências externas](https://msdn.microsoft.com/library/5fcwybb2.aspx) |
| **Etapas**| <p>Embora ele ainda não é amplamente usado, há um recurso de XML que permite tooexpand de analisador XML Olá entidades de macro com valores definidos no próprio documento hello ou de fontes externas. Por exemplo, o documento hello pode definir uma entidade "companyname" com valor de hello "Microsoft", para que sempre Olá texto "&companyname;" aparece no documento hello, ele é substituído automaticamente pelo texto de saudação Microsoft. Ou, documento hello pode definir uma entidade "MSFTStock", o que faz referência a um web externo serviço toofetch Olá valor atual de ações da Microsoft.</p><p>Em seguida, a qualquer momento "&MSFTStock;" aparece no documento hello, ele é substituído automaticamente pelo preço de estoque atual de saudação. No entanto, essa funcionalidade pode ser mal utilizada toocreate condições de negação de serviço (DoS). Um invasor pode aninhar uma bomba XML de expansão exponencial que consome toda a memória disponível no sistema de saudação toocreate de várias entidades. </p><p>Como alternativa, ele pode criar uma referência externa que transmite novamente um valor infinito de dados ou que simplesmente trava thread hello. Como resultado, todas as equipes devem desabilitar a resolução de entidade XML interna e/ou externa totalmente se seu aplicativo não usá-lo, ou manualmente limitar a quantidade de saudação de memória e a hora em que o aplicativo hello pode consumir para resolução de entidade se essa funcionalidade é absolutamente necessário. Se a resolução de entidade não for exigida pelo aplicativo, desabilite-a. </p>|

### <a name="example"></a>Exemplo
Código do .NET Framework, você pode usar o hello abordagens a seguir:

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
Observe o valor padrão Olá de `ProhibitDtd` na `XmlReaderSettings` for true, mas em `XmlTextReader` é false. Se você estiver usando XmlReaderSettings, você não precisa tooset ProhibitDtd tootrue explicitamente, mas é recomendável para a mesma segurança que você faça. Também Observe que Olá classe XmlDocument permite que a resolução de entidade por padrão. 

### <a name="example"></a>Exemplo
resolução de entidade toodisable para XmlDocument, use Olá `XmlDocument.Load(XmlReader)` sobrecarga da saudação método Load e definir Olá propriedades adequadas na resolução de toodisable de argumento de XmlReader hello, conforme ilustrado na saudação de código a seguir: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a>Exemplo
Se desabilitar a resolução de entidade não é possível para o seu aplicativo, defina Olá XmlReaderSettings.MaxCharactersFromEntities tooa razoável valor da propriedade de acordo com as necessidades do aplicativo tooyour. Isso limitará o impacto de saudação de possíveis ataques de expansão exponencial. saudação de código a seguir fornece um exemplo dessa abordagem: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a>Exemplo
Se você precisar tooresolve embutido entidades, mas não é necessário para entidades externas tooresolve, defina Olá XmlReaderSettings.XmlResolver propriedade toonull. Por exemplo: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
Observe que no MSXML6, ProhibitDTD é definido tootrue (desabilitar o processamento do DTD) por padrão. Para código do Apple OSX/iOS, há dois analisadores XML que você pode usar: NSXMLParser e libXML2. 

## <a id="app-verification"></a>Os aplicativos que usam http.sys executam a verificação de conversão em formato canônico de URL

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Qualquer aplicativo que usa http.sys deve seguir estas diretrizes:</p><ul><li>Limite Olá toono de comprimento de URL mais de 16.384 caracteres (ASCII ou Unicode). Isso é Olá absoluto tamanho máximo da URL com base na configuração de serviços de informações da Internet (IIS) 6 saudação padrão. Os sites devem se esforçar para ter um comprimento menor do que isso, se possível</li><li>Usar Olá classes do .NET Framework e/s de arquivo (como FileStream) como esses aproveitarão Olá regras de conversão em formato canônico no hello .NET FX</li><li>Criar explicitamente uma lista de permissões de nomes de arquivo conhecidos</li><li>Rejeite explicitamente tipos de arquivo conhecidos que você não fornecerá a rejeições de UrlScan: exe, bat, cmd, com, htw, ida, idq, htr, idc, shtm[l], stm, printer, ini, pol, arquivos files</li><li>Catch Olá exceções a seguir:<ul><li>System.ArgumentException (para nomes de dispositivo)</li><li>System.NotSupportedException (para fluxos de dados)</li><li>System.IO.FileNotFoundException (para nomes com escape inválidos)</li><li>System.IO.DirectoryNotFoundException (para diretórios com escape inválidos)</li></ul></li><li>*Não* chamar tooWin32 arquivo I/O APIs. Em uma URL inválida normalmente retornam um erro de 400 toohello usuário e logon erro real hello.</li></ul>|

## <a id="controls-users"></a>Verifique se os controles adequados estão em vigor ao aceitar arquivos de usuários

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Upload de arquivo irrestrito](https://www.owasp.org/index.php/Unrestricted_File_Upload), [Tabela de assinatura de arquivo](http://www.garykessler.net/library/file_sigs.html) |
| **Etapas** | <p>Arquivos carregados representam um risco significativo tooapplications.</p><p>a primeira etapa Olá em muitos ataques é tooget alguns toobe do código toohello sistema atacado. Em seguida, ataque Olá só precisa toofind executado um código de saudação do tooget de maneira. Usar um upload de arquivo Ajuda invasor Olá realizar a primeira etapa de saudação. consequências de saudação do carregamento de arquivo irrestrito podem variar, incluindo controle de sistema completo, um banco de dados, desfiguração simple e sistemas de tooback a fim de ataques de encaminhamento ou sistema de arquivos sobrecarregados.</p><p>Depende do qual aplicativo hello não com o arquivo hello carregado e especialmente onde ele está armazenado. A validação do lado do servidor de uploads de arquivo está ausente. Os controles de segurança a seguir devem ser implementados para a funcionalidade de Upload de Arquivo:</p><ul><li>Verificação de extensão de arquivo (somente um conjunto válido de tipos de arquivo permitidos deve ser aceito)</li><li>Limite de tamanho máximo de arquivo</li><li>Arquivo não deve ser carregado toowebroot; local de saudação deve ser um diretório no disco não são do sistema</li><li>Convenção de nomenclatura deve ser seguida, de modo que hello nome de arquivo carregado tem algumas aleatoriedade, portanto, como tooprevent arquivo substitui</li><li>Arquivos devem ser verificados antivírus antes de gravar o disco toohello</li><li>Certifique-se de que o nome do arquivo hello e quaisquer outros metadados (por exemplo, o caminho do arquivo) são validados para caracteres mal-intencionado</li><li>Assinatura do arquivo de formato deve ser verificada, tooprevent um usuário carregue um arquivo masqueraded (por exemplo, carregando um arquivo exe, alterando a extensão tootxt)</li></ul>| 

### <a name="example"></a>Exemplo
Para o último ponto relacionadas à validação de assinatura de formato de arquivo hello, consulte classe toohello abaixo para obter detalhes: 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <a id="typesafe"></a>Verifique se os parâmetros de tipo seguro são usados no aplicativo Web para acesso a dados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Se você usar a coleção de parâmetros hello, SQL trata Olá entrada é como um valor literal e, em seguida, em vez disso, como código executável. Olá coleção de parâmetros pode ser restrições de comprimento e tipo de tooenforce usado nos dados de entrada. Valores fora do intervalo de saudação disparar uma exceção. Se não forem usados parâmetros SQL de tipo seguro, os invasores podem ser tooexecute capaz de ataques de injeção que são inseridos na entrada hello filtrada.</p><p>Use parâmetros de tipo de segurança ao construir SQL consultas tooavoid possíveis ataques de injeção SQL que podem ocorrer com a entrada não filtrada. Você pode usar parâmetros de tipo seguro com procedimentos armazenados e instruções SQL dinâmicas. Parâmetros são tratados como valores literais por banco de dados de saudação e não como código executável. Os parâmetros também são verificados quanto ao tipo e ao tamanho.</p>|

### <a name="example"></a>Exemplo 
Olá código a seguir mostra como toouse parâmetros de tipo seguros com hello SqlParameterCollection ao chamar um procedimento armazenado. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Olá precede o exemplo de código, o valor de entrada hello não pode ser mais de 11 caracteres. Se dados saudação não está de acordo com tipo de toohello ou o comprimento definido pelo parâmetro hello, Olá classe SqlParameter gera uma exceção. 

## <a id="binding-mvc"></a>Usar as classes de associação de modelo separado ou listas de filtro de associação de vulnerabilidade de atribuição em massa de MVC tooprevent

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | [Atributos de metadados](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute), [pública chave de segurança e mitigação de vulnerabilidade](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation), [tooMass guia completo atribuição no ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx), [guia de Introdução ao EF com MVC](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost) |
| **Etapas** | <ul><li>**Quando devo procurar vulnerabilidades de overposting? -** As vulnerabilidades de overposting podem ocorrer em qualquer lugar em que você associar classes de modelo da entrada do usuário. Estruturas como MVC podem representar dados de usuário em classes personalizadas do .NET, incluindo POCOs (Plain Old CLR Objects). MVC preenche automaticamente essas classes de modelo com dados de solicitação hello, fornecendo uma representação conveniente para lidar com a entrada do usuário. Quando essas classes incluem propriedades que não devem ser definidas pelo usuário Olá, o aplicativo hello pode ser vulneráveis ataques de lançamento tooover, que permitem o controle de usuário de dados que o aplicativo de hello nunca se destina. Como associação de modelo MVC, tecnologias de acesso de banco de dados como mapeadores de objeto/relacional como Entity Framework geralmente também suportam o uso de dados de banco de dados de toorepresent POCO objetos. Essas classes de modelo de dados fornecem Olá conveniência mesmo em lidar com dados de banco de dados, como o MVC ao lidar com a entrada do usuário. Porque o banco de dados do MVC e hello suporte semelhantes modelos, como os objetos POCO, parece Olá tooreuse fácil mesmo classes para ambas as finalidades. Esta prática falhar, toopreserve separação de preocupações e uma área comum onde propriedades são expostos associação toomodel, habilitar ataques de excesso de lançamento.</li><li>**Por que não devem usar meu classes de modelo de banco de dados não filtrados como ações de MVC toomy parâmetros? -** Associação de modelo MVC porque associará nada nessa classe. Mesmo se Olá dados não aparecem no modo de exibição, que um usuário mal-intencionado pode enviar uma solicitação HTTP com dados incluídos e MVC serão forneceremos associá-lo porque sua ação diz que a classe de banco de dados é forma Olá dos dados, ele deve aceitar entrada do usuário.</li><li>**Por que devo me preocupar Olá forma usada para associação de modelo? -** Associação de modelo usando o ASP.NET MVC com modelos demasiadamente amplas expõe ataques de lançamento tooover um aplicativo. Excesso de lançamento pode permitir que dados de aplicativo invasores toochange além do qual desenvolvedor Olá pretendido, como a substituição de preço Olá para um item ou hello privilégios de segurança para uma conta. Aplicativos devem usar um contrato explícito tooprovide associação de modelos (ou listas de filtros de propriedade permitido específica) da ação específica para que tooallow de entrada não confiável por meio de associação de modelo.</li><li>**Ter modelos de associação separados apenas duplica o código? -** Não, é uma questão de separação de questões. Se você reutilizar os modelos de banco de dados em métodos de ação, você está dizendo qualquer propriedade (ou subpropriedade) em que a classe pode ser definida pelo usuário de saudação em uma solicitação HTTP. Se não desejar for toodo MVC, você precisa de uma lista de filtros ou tooshow de forma uma classe separada MVC que os dados podem vir de usuário de entrada em vez disso.</li><li>**Se os modelos de associação separada para a entrada do usuário, é necessário tooduplicate todos os atributos de anotação meus dados? -** Não necessariamente. Você pode usar MetadataTypeAttribute em Olá banco de dados modelo toolink toohello metadados de classe em uma classe de associação de modelo. Apenas Observe que Olá tipo referenciado pela Olá MetadataTypeAttribute deve ser um subconjunto de saudação fazendo referência ao tipo (ele pode ter menos de propriedades, mas não mais).</li><li>**A movimentação de dados entre modelos de entrada de usuário e modelos de banco de dados é entediante. Posso simplesmente copiar todas as propriedades usando a reflexão? -** Sim. Hello, apenas as propriedades que aparecem em modelos de associação de saudação são Olá que você determinou toobe seguro para a entrada do usuário. Não há nenhum motivo de segurança que impede usando reflexão toocopy em todas as propriedades que existem em comum entre esses dois modelos.</li><li>**Que tal [Bind(Exclude ="â€¦")]. Posso usar isso em vez de ter modelos de associação separados? -** Essa abordagem não é recomendada. Usar [Bind(Exclude ="â€¦")] significa que qualquer nova propriedade é associável por padrão. Quando uma nova propriedade é adicionada, coisas de tookeep de tooremember uma etapa extra é seguro, em vez de ter design Olá ser seguro por padrão. Dependendo de desenvolvedor Olá é arriscado verificar essa lista toda vez que uma propriedade é adicionada.</li><li>**[Bind(Include ="â€¦")] é útil para operações de edição? -** Não. [Bind(Include ="â€¦")] só é adequado para operações de estilo INSERT (adicionar novos dados). Para operações de atualização de estilo (revisar os dados existentes), use outra abordagem, como ter modelos de associação separado ou passar uma lista explícita de propriedades permitidos tooUpdateModel ou TryUpdateModel. Adicionando um [associar (Include = "â..")] atributo em uma operação de edição significa que o MVC será criar uma instância do objeto e definir somente Olá listadas propriedades, deixando todos os outros valores padrão. Quando os dados de saudação são persistentes, substituirá totalmente entidade existente do hello, redefinindo valores hello para os padrões de tootheir propriedades omitido. Por exemplo, se IsAdmin foi omitido um [associar (Include = "â..")] atributo em uma operação de edição, qualquer usuário cujo nome foi editado por meio dessa ação seria tooIsAdmin redefinição = false (qualquer usuário editado perderia status de administrador). Se você quiser tooprevent atualiza as propriedades de toocertain, use um dos Olá outras abordagens acima. Observe que algumas versões das ferramentas do MVC geram classes de controlador com [Bind(Include ="â€¦")] em ações de edição. Isso implica que a remoção de uma propriedade da lista impedirá ataques de excesso de postagem. No entanto, conforme descrito acima, essa abordagem não funciona conforme o esperado e em vez disso redefinirá todos os dados em Olá omitido propriedades tootheir padrão valores.</li><li>**Para operações Create, há alguma restrição ao uso de [Bind(Include ="â€¦")] em vez de modelos de associação separada? -** Sim. Primeiro, essa abordagem não funciona para cenários de Edição, que exigem a manutenção de duas abordagens separadas para atenuar todas as vulnerabilidades de excesso de postagem. Modelos de associação separado e segundo impõem a separação de preocupações entre Olá forma usada para a forma de entrada e hello de usuário usada para a persistência, algo [associar (Include = "â...")] não faz. Observe que, em terceiro lugar, [associar (Include = "â...")] pode lidar somente com propriedades de nível superior; Você não pode permitir que somente partes de subpropriedades (como "Details.Name") no atributo hello. Por fim e talvez o mais importante, usando [associar (Include = "â...")] adiciona uma etapa extra que deve ser lembrada qualquer classe de saudação do tempo é usado para associação de modelo. Se um novo método de ação associa a classe de dados toohello diretamente e esquecer tooinclude um [associar (Include = "â..")] atributo, ele pode ser vulnerável ataques tooover lançamento, portanto Olá [associar (incluir = "â..")] abordagem é menos segura por padrão. Se você usar [associar (Include = "â...")], tome sempre cuidado tooremember toospecify-lo toda vez que suas classes de dados aparecem como parâmetros de método de ação.</li><li>**Para criar operações, o que colocar Olá [associar (Include = "â...")] atributo na própria classe de modelo Olá? Não, essa abordagem evitar Olá necessidade tooremember colocando Olá atributo em cada método de ação? -** Essa abordagem funciona em alguns casos. Usando [associar (Include = "â...")] no próprio tipo de modelo hello (e não em parâmetros de ação usando essa classe), evite Olá necessidade tooremember tooinclude Olá [associar (Include = "â...")] atributo em cada método de ação. Usar o atributo Olá diretamente à classe Olá efetivamente cria uma área de superfície separada dessa classe para fins de associação de modelo. No entanto, essa abordagem só permite uma forma de associação de modelo por classe de modelo. Se um método de ação precisa tooallow a associação de modelo de um campo (por exemplo, um administrador somente ação que atualiza as funções de usuário) e outras ações necessário tooprevent a associação de modelo do campo, essa abordagem não funcionará. Cada classe pode ter apenas uma forma de associação de modelo; Se precisam de ações diferentes formas de associação de modelo diferente, que precisam toorepresent esses separam formas usando ou classes de associação de modelo separado ou separam [associar (Include = "â...")] atributos em métodos de ação de saudação.</li><li>**O que são modelos de associação? São que eles Olá a mesma coisa que exibir modelos? -** Esses são dois conceitos relacionados. termo Olá modelo de associação refere-se a classe de modelo tooa usada em uma ação é a lista de parâmetros (forma Olá passada do método de ação do MVC modelo associação toohello). modelo de exibição de termo Olá refere-se tooa classe de modelo passado de uma exibição de tooa do método de ação. Usando um modelo de exibição específica é uma abordagem comum para transmitir dados de uma exibição de tooa do método de ação. Geralmente, essa forma também é adequada para a associação de modelo e modelo de exibição de termo Olá pode ser usado toorefer Olá mesmo modelo usado em ambos os locais. toobe preciso, esse procedimento fala especificamente sobre associação de modelos, concentrando-se na forma de saudação passada toohello ação, que é o que é importante para fins de atribuição em massa.</li></ul>| 

## <a id="rendering"></a>Codificar toorendering anterior de saída da web não confiável

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, Formulários da Web, MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | [Como tooprevent Cross site scripting no ASP.NET](http://msdn.microsoft.com/library/ms998274.aspx), [scripts intersites](http://cwe.mitre.org/data/definitions/79.html), [XSS (Cross Site Scripting) prevenção Cheat Sheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) |
| **Etapas** | Scripts intersites (frequentemente abreviado como XSS) é um vetor de ataque para serviços online ou qualquer aplicativo/componente que consome a entrada da web hello. Vulnerabilidades XSS podem permitir que um invasor tooexecute script no computador de outro usuário por meio de um aplicativo web vulnerável. Scripts mal-intencionados podem ser usados toosteal cookies e adulterar caso contrário, a máquina da vítima através de JavaScript. O XSS é impedido pela validação da entrada do usuário, garantindo que ele seja bem-formado e codificado antes de ser renderizado em uma página da Web. A validação de entrada e a codificação de saída podem ser feitas usando a Web Protection Library. Para código gerenciado (C\#, VB.net, etc.), use um ou mais apropriado métodos de codificação de saudação biblioteca de proteção da Web (Anti-XSS), dependendo do contexto de saudação onde a entrada do usuário Olá obtém manifestada:| 

### <a name="example"></a>Exemplo

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <a id="typemodel"></a>Execute a validação de entrada e a filtragem em todos os tipos de cadeia de caracteres de propriedades do modelo

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | [Adicionando Validação](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation), [Validando Dados de Modelo em um Aplicativo MVC](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [Princípios Básicos para Aplicativos ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Etapas** | <p>Todos os parâmetros de entrada hello devem ser validados antes de serem usadas em Olá aplicativo tooensure que o aplicativo hello está protegido contra entradas de usuário mal-intencionado. Valide os valores de entrada hello usando validações de expressão regular no lado do servidor com uma estratégia de validação da lista de permissões. Unsanitized entradas de usuário / parâmetros passados toohello métodos podem causar código vulnerabilidades de injeção.</p><p>Para aplicativos Web, os pontos de entrada também podem incluir campos de formulário, QueryStrings, cookies, cabeçalhos HTTP e parâmetros de serviço Web.</p><p>Olá seguintes verificações de validação de entrada devem ser executadas após a associação de modelo:</p><ul><li>Propriedades do modelo Olá devem ser anotadas com a anotação RegularExpression, para aceitar os caracteres permitidos e o comprimento máximo permitido</li><li>os métodos do controlador Olá devem executar ModelState validade</li></ul>|

## <a id="richtext"></a>A limpeza deve ser aplicada em campos de formulário que aceitam todos os caracteres, como o editor de rich text

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Codificar a entrada não segura](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3), [HTML Sanitizer](https://github.com/mganss/HtmlSanitizer) |
| **Etapas** | <p>Identifica todas as marcas de marcação estática que você deseja toouse. Uma prática comum é toorestrict formatação toosafe HTML elementos, como `<b>` (negrito) e `<i>` (itálico).</p><p>Antes de gravar dados hello, codificação HTML-lo. Isso faz com que qualquer script mal-intencionado seguro, levando toobe tratado como texto, não como código executável.</p><ol><li>Desabilitar solicitação ASP.NET validação adicionando Olá Olá ValidateRequest = "false" atributo toohello diretiva @ Page</li><li>Codifique a entrada de cadeia de caracteres de saudação com método de HtmlEncode hello</li><li>Usar StringBuilder e chamada seu tooselectively do método de substituição remover Olá codificação em elementos de saudação HTML que você deseja toopermit</li></ol><p>Olá Olá na página referências desabilita a validação de solicitação do ASP.NET, definindo `ValidateRequest="false"`. Ele hello codifica o HTML de entrada e permite seletivamente Olá `<b>` e `<i>` como alternativa, também pode ser usada uma biblioteca .NET para a limpeza de HTML.</p><p>HtmlSanitizer é uma biblioteca .NET para fragmentos HTML e documentos de construções que podem levar a ataques de tooXSS de limpeza. Ele usa AngleSharp tooparse, manipular e renderizar HTML e CSS. HtmlSanitizer pode ser instalado como um pacote do NuGet e entrada do usuário Olá pode ser passada HTML ou CSS limpeza métodos relevantes, conforme aplicável, no lado do servidor de saudação. Observe que a limpeza como um controle de segurança deve ser considerada apenas como último recurso.</p><p>A validação de entrada e a codificação de saída são consideradas controles de segurança melhores.</p> |

## <a id="inbuilt-encode"></a>Não atribua toosinks de elementos DOM que não têm embutidas de codificação

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Muitas funções de javascript não fazem a codificação por padrão. Ao atribuir elementos tooDOM de entrada não confiáveis por meio de funções, pode resultar em várias execuções de script (XSS) do site.| 

### <a name="example"></a>Exemplo
A seguir estão exemplos não seguros: 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
Não use `innerHtml`; em vez disso, use `innerText`. Da mesma forma, em vez de `$("#elm").html()`, use `$("#elm").text()` 

## <a id="redirect-safe"></a>Validar todos os redirecionamentos de dentro do aplicativo hello serão fechados ou feitos com segurança

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Olá estrutura de autorização do OAuth 2.0 - redirecionadores aberto](http://tools.ietf.org/html/rfc6749#section-10.15) |
| **Etapas** | <p>Exigir tooa fornecido pelo usuário local de redirecionamento de design do aplicativo deve restringir Olá redirecionamento possíveis destinos tooa "seguro" lista predefinida de sites ou domínios. Todos os redirecionamentos no aplicativo hello devem ser fechado/safe.</p><p>toodo isso:</p><ul><li>Identificar todos os redirecionamentos</li><li>Implemente uma atenuação apropriada para cada tipo de redirecionamento. Atenuações apropriadas incluem a confirmação de usuário ou a lista de permissões de redirecionamento. Se um site ou serviço com uma vulnerabilidade de redirecionamento aberto usar provedores de identidade Facebook/OAuth/OpenID, um invasor poderá roubar o token de logon do usuário e representar o usuário. Este é um risco inerente ao usar o OAuth, que está documentada na RFC 6749 "Olá estrutura de autorização OAuth 2.0", seção 10.15 "abrir redireciona" da mesma forma, as credenciais do usuário podem ser comprometidas por ataques de phishing lança usando redirecionamentos abertos</li></ul>|

## <a id="string-method"></a>Implemente a validação de entrada em todos os parâmetros de tipo de cadeia de caracteres aceitos por métodos do Controlador

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | [Validando dados de modelo em um aplicativo MVC](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [Princípios básicos para aplicativos ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Etapas** | Para métodos que aceitam apenas o tipo de dados primitivo e não modelos como argumento, a validação de entrada deve ser feita usando a Expressão Regular. Aqui, Regex.IsMatch deve ser usado com um padrão de regex válido. Se não corresponder a entrada hello Olá Expressão Regular especificada, controle não deve continuar e deve ser exibido um aviso adequado sobre falha de validação.| 

## <a id="dos-expression"></a>Definir tempo limite de limite superior de expressão regular de processamento DoS tooprevent devido a expressões regulares toobad

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, Formulários da Web, MVC5, MVC6  |
| **Atributos**              | N/D  |
| **Referências**              | [Propriedade DefaultRegexMatchTimeout](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| **Etapas** | tooensure ataques de negação de serviço contra mal criado expressões regulares, o que fazer com que um lote de retrocesso, definir tempo limite padrão global de saudação. Se o tempo de processamento de saudação demora mais do que Olá definido pelo limite superior, ele deve gerar uma exceção de tempo limite. Se nada estiver configurado, o tempo limite de saudação seria infinito.| 

### <a name="example"></a>Exemplo
Por exemplo, hello configuração a seguir lançará um RegexMatchTimeoutException, se o processamento de saudação demorar mais de 5 segundos: 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <a id="html-razor"></a>Evite usar Html.Raw nos modos de exibição do Razor

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| Etapa | Páginas da Web do ASP.Net (Razor) executam a codificação HTML automática. Todas as cadeias de caracteres impressas por nuggets de código inserido (blocos @) são codificadas em HTML automaticamente. No entanto, quando o método `HtmlHelper.Raw` é invocado, ele retorna uma marcação que não é codificada em HTML. Se `Html.Raw()` método auxiliar é usado, ignora Olá proteção automática de codificação que fornece Razor.|

### <a name="example"></a>Exemplo
A seguir está um exemplo não seguro: 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
Não use `Html.Raw()` , a menos que você precisa toodisplay marcação. Esse método não executa implicitamente a codificação de saída. Use outros auxiliares do ASP.NET; por exemplo, `@Html.DisplayFor()` 

## <a id="stored-proc"></a>Não use consultas dinâmicas em procedimentos armazenados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Um ataque de injeção de SQL explora vulnerabilidades em comandos arbitrários de toorun de validação de entrada no banco de dados de saudação. Pode ocorrer quando o aplicativo usa a entrada tooconstruct dinâmico tooaccess de instruções SQL Olá banco de dados. Isso também poderá ocorrer se o código usar procedimentos armazenados que sejam cadeias de caracteres passadas que contenham entrada bruta do usuário. Usando Olá ataque de injeção de SQL, invasor Olá pode executar comandos arbitrários no banco de dados de saudação. Todas as instruções SQL (incluindo instruções SQL de saudação em procedimentos armazenados) devem ser parametrizadas. Instruções SQL parametrizadas aceitará caracteres que têm significado especial a tooSQL (como uma aspa simples) sem problemas porque eles são fortemente tipados. |

### <a name="example"></a>Exemplo
A seguir está um exemplo de Procedimento Armazenado dinâmico não seguro: 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a>Exemplo
A seguir é hello mesmo procedimento armazenado com segurança implementado: 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <a id="validation-api"></a>Verifique se a validação do modelo é feita nos métodos de API Web

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | [Validação de modelo na API Web ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Etapas** | Quando um cliente envia a API da web de tooa dados, são obrigatórias toovalidate Olá dados antes de executar qualquer processamento. Para APIs da Web ASP.NET que aceitam modelos como entrada, use as anotações de dados em regras de validação de tooset modelos nas propriedades de saudação do modelo de saudação.|

### <a name="example"></a>Exemplo
saudação de código a seguir demonstra Olá mesmo: 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a>Exemplo
No método de ação de saudação dos controladores da API de hello, validade do modelo de saudação tem toobe explicitamente marcada como mostrado abaixo: 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with hello product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <a id="string-api"></a>Implemente a validação de entrada em todos os parâmetros de tipo de cadeia de caracteres aceitos pelos métodos de API Web

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, MVC 5, MVC 6 |
| **Atributos**              | N/D  |
| **Referências**              | [Validando dados de modelo em um aplicativo MVC](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [Princípios básicos para aplicativos ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Etapas** | Para métodos que aceitam apenas o tipo de dados primitivo e não modelos como argumento, a validação de entrada deve ser feita usando a Expressão Regular. Aqui, Regex.IsMatch deve ser usado com um padrão de regex válido. Se não corresponder a entrada hello Olá Expressão Regular especificada, controle não deve continuar e deve ser exibido um aviso adequado sobre falha de validação.|

## <a id="typesafe-api"></a>Verifique se os parâmetros de tipo seguro são usados na API Web para acesso a dados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Se você usar a coleção de parâmetros hello, SQL trata Olá entrada é como um valor literal e, em seguida, em vez disso, como código executável. Olá coleção de parâmetros pode ser restrições de comprimento e tipo de tooenforce usado nos dados de entrada. Valores fora do intervalo de saudação disparar uma exceção. Se não forem usados parâmetros SQL de tipo seguro, os invasores podem ser tooexecute capaz de ataques de injeção que são inseridos na entrada hello filtrada.</p><p>Use parâmetros de tipo de segurança ao construir SQL consultas tooavoid possíveis ataques de injeção SQL que podem ocorrer com a entrada não filtrada. Você pode usar parâmetros de tipo seguro com procedimentos armazenados e instruções SQL dinâmicas. Parâmetros são tratados como valores literais por banco de dados de saudação e não como código executável. Os parâmetros também são verificados quanto ao tipo e ao tamanho.</p>|

### <a name="example"></a>Exemplo
Olá código a seguir mostra como toouse parâmetros de tipo seguros com hello SqlParameterCollection ao chamar um procedimento armazenado. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Olá precede o exemplo de código, o valor de entrada hello não pode ser mais de 11 caracteres. Se dados saudação não está de acordo com tipo de toohello ou o comprimento definido pelo parâmetro hello, Olá classe SqlParameter gera uma exceção. 

## <a id="sql-docdb"></a>Usar consultas SQL parametrizadas no Cosmos DB

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Azure Document DB | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Anunciando a parametrização de SQL no DocumentDB](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/) |
| **Etapas** | Embora o DocumentDB só dê suporte a consultas somente leitura, a injeção de SQL ainda será possível se as consultas forem construídas concatenando com a entrada do usuário. Talvez seja possível para um usuário toogain acesso toodata que eles não devem estar acessando dentro Olá mesma coleção ao criar consultas SQL mal-intencionadas. Use consultas SQL parametrizadas se as consultas forem construídas com base na entrada do usuário. |

## <a id="schema-binding"></a>Validação de entrada de WCF por meio de associação de esquema

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff647820.aspx) |
| **Etapas** | <p>Ausência de validação de clientes potenciais toodifferent ataques de injeção de tipo.</p><p>Validação de mensagem representa uma linha de defesa na proteção de saudação do seu aplicativo do WCF. Com essa abordagem, você deve validar mensagens usando operações de serviço WCF esquemas tooprotect contra ataques de um cliente mal-intencionado. Valide todas as mensagens recebidas por Olá tooprotect Olá cliente contra ataques por um serviço mal-intencionado. Validação de mensagem torna possível toovalidate mensagens quando as operações de consumir contratos de mensagem ou contratos de dados, que não podem ser feitos usando a validação de parâmetro. Validação de mensagem permite que você toocreate a lógica de validação dentro de esquemas, assim, fornecendo mais flexibilidade e reduzir o tempo de desenvolvimento. Esquemas podem ser reutilizadas em diferentes aplicativos dentro da organização hello, criação de padrões para representação de dados. Além disso, validação de mensagem permite operações tooprotect quando eles consomem tipos de dados mais complexos que envolvem contratos que representa a lógica de negócios.</p><p>validação de mensagem tooperform, você cria um esquema que representa as operações de saudação de seus tipos de dados de serviço e hello consumidas por essas operações. Você criar uma classe .NET que implementa um Inspetor de mensagens do cliente personalizado e dispatcher personalizado Inspetor toovalidate Olá mensagens enviadas/recebidas de/para o serviço de saudação. Em seguida, você deve implementar uma validação de mensagem do ponto de extremidade personalizado comportamento tooenable no cliente hello e serviço hello. Finalmente, você implementa um elemento de configuração personalizada na classe Olá que permite que você tooexpose Olá estendidos comportamento de ponto de extremidade personalizado no arquivo de configuração de saudação do serviço de saudação ou cliente hello"</p>|

## <a id="parameters"></a>Validação de entrada de WCF por meio de Inspetores de Parâmetro

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico, NET Framework 3 |
| **Atributos**              | N/D  |
| **Referências**              | [MSDN](https://msdn.microsoft.com/library/ff647875.aspx) |
| **Etapas** | <p>Validação de entrada e de dados representa um importante de linha de defesa na proteção de saudação do seu aplicativo do WCF. Você deve validar todos os parâmetros expostos no WCF operações tooprotect Olá serviço contra ataques por um cliente mal-intencionado. Por outro lado, você também deve validar todos os valores de retorno recebidos pelo Olá tooprotect Olá cliente contra ataques por um serviço mal-intencionado</p><p>O WCF fornece pontos de extensibilidade diferentes que permitem que você comportamento de tempo de execução toocustomize Olá WCF ao criar extensões personalizadas. Inspetores e inspetores de parâmetro são dois mecanismos de extensibilidade de mensagem usada toogain maior controle sobre dados Olá passando entre um cliente e um serviço. Você deve usar inspetores de parâmetro para validação de entrada e usar inspetores de mensagem somente quando precisar tooinspect Olá toda mensagem que fluem para dentro e fora de um serviço.</p><p>validação de entrada de tooperform, você criará uma classe do .NET e implementar um Inspetor de parâmetro personalizado em parâmetros de toovalidate ordem nas operações em seu serviço. Em seguida, implementar uma validação de tooenable do comportamento de ponto de extremidade personalizado no cliente hello e serviço hello. Por fim, você implementará um elemento de configuração personalizada na classe Olá que permite que você tooexpose Olá estendidos comportamento de ponto de extremidade personalizado no arquivo de configuração de saudação do serviço de saudação ou cliente Olá</p>|
