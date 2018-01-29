---
title: "Proteger ativos da CDN do Azure com autenticação de token | Microsoft Docs"
description: "Aprenda a usar autenticação de token para proteger o acesso aos ativos da CDN do Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/17/2017
ms.author: mezha
ms.openlocfilehash: f6d008a92677d28d0184e64637dcb2e093299519
ms.sourcegitcommit: 4ea06f52af0a8799561125497f2c2d28db7818e7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="securing-azure-content-delivery-network-assets-with-token-authentication"></a>Proteger ativos da Rede de Distribuição de Conteúdo do Azure com autenticação de token

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Visão geral

A autenticação de token é um mecanismo que permite que você impeça que a CDN (Rede de Distribuição de Conteúdo) do Azure forneça ativos a clientes não autorizados. A autenticação de token normalmente é feita para evitar "hotlinking" de conteúdo, em que um site diferente, como um quadro de mensagens, usa seus ativos sem sua permissão. O hotlinking pode ter um impacto sobre os custos de fornecimento de conteúdo. Ao habilitar a autenticação de token na CDN, as solicitações são autenticadas pelo servidor de borda da CDN antes que a CDN entregue o conteúdo. 

## <a name="how-it-works"></a>Como ele funciona

A autenticação de token verifica que as solicitações são geradas por um site confiável, exigindo que as solicitações contenham um valor de token com informações codificadas sobre o solicitante. O conteúdo será fornecido a um solicitante somente se as informações codificadas atenderem aos requisitos; caso contrário, as solicitações serão negadas. Você pode configurar os requisitos usando um ou mais dos seguintes parâmetros:

- País: permitir ou negar as solicitações originadas em países especificados pelo seu [código de país](https://msdn.microsoft.com/library/mt761717.aspx).
- URL: permitir somente solicitações que correspondam ao ativo ou ao caminho especificado.
- Host: permitir ou negar as solicitações que usem os hosts especificados no cabeçalho da solicitação.
- Referenciador: permitir ou negar a solicitação de referenciador especificado.
- Endereço IP: permitir somente solicitações originadas de determinado endereço IP ou sub-rede IP.
- Protocolo: permitir ou negar solicitações com base no protocolo usado para solicitar o conteúdo.
- Tempo de expiração: atribua um período de data e hora para garantir que um link só permaneça válido por um período limitado.

Para obter mais informações, consulte os exemplos de configuração detalhados para cada parâmetro em [Configuração de autenticação de token](#setting-up-token-authentication).

## <a name="reference-architecture"></a>Arquitetura de referência

O diagrama de fluxo de trabalho a seguir descreve como a CDN usa autenticação de token para trabalhar com seu aplicativo Web.

![Fluxo de trabalho de autenticação de token da CDN](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>Lógica de validação de token no ponto de extremidade da CDN
    
O fluxograma a seguir descreve como a CDN do Azure valida a solicitação do cliente quando a autenticação de token é configurada no ponto de extremidade da CDN.

![Lógica de validação de token da CDN](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>Configurar autenticação de token

1. No [portal do Azure](https://portal.azure.com), navegue até seu perfil da CDN e clique em **Gerenciar** para inicializar o portal suplementar.

    ![Botão Gerenciar perfil da CDN](./media/cdn-token-auth/cdn-manage-btn.png)

2. Passe o mouse sobre **HTTP Grande** e clique em **Token de Autenticação** no submenu. Então você pode configurar os parâmetros de criptografia e a chave de criptografia da seguinte maneira:

    1. Crie uma ou mais chaves de criptografia. Uma chave de criptografia diferencia maiúsculas de minúsculas e pode conter qualquer combinação de caracteres alfanuméricos. Todos os outros tipos de caracteres, incluindo espaços, não são permitidos. O comprimento máximo é de 250 caracteres. Para garantir que as chaves de criptografia sejam aleatórias, é recomendável criá-las usando a [ferramenta OpenSSL](https://www.openssl.org/). 

       A ferramenta OpenSSL tem a seguinte sintaxe:

       ```rand -hex <key length>```

       Por exemplo:

       ```OpenSSL> rand -hex 32``` 

       Para evitar tempo de inatividade, crie uma chave primária e uma de backup. Uma chave de backup fornece acesso ininterrupto ao seu conteúdo quando sua chave primária está sendo atualizada.
    
    2. Insira uma chave de criptografia exclusiva na caixa **Chave Primária** e, opcionalmente, insira uma chave de backup na caixa **Chave de Backup**.

    3. Selecione a versão mínima de criptografia para cada chave de sua lista de **versão Mínima De Criptografia** e, em seguida, clique em **Atualização**:
       - **V2**: Indica que a chave pode ser usada para gerar tokens da versão 2.0 e 3.0. Use esta opção somente se estiver em transição de uma chave de criptografia legado versão 2.0 para uma chave de versão 3.0.
       - **V3**: (Recomendado) Indica que a chave pode ser usada somente para gerar tokens da versão 3.0.

    ![Chave de configuração de autenticação de token da CDN](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    4. Use a ferramenta de criptografia para configurar os parâmetros de criptografia e gerar um token. Com a ferramenta de criptografia, você pode permitir ou negar as solicitações com base no horário de expiração, no país, no referenciador, no protocolo e no IP do cliente (em qualquer combinação). Embora não haja nenhum limite para o número e a combinação de parâmetros que podem ser combinados para formar um token, o comprimento total de um token é limitado a 512 caracteres. 

       ![Ferramenta de criptografia da CDN](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

       Insira valores para um ou mais dos seguintes parâmetros de criptografia na seção da **Ferramenta de Criptografia**: 

       > [!div class="mx-tdCol2BreakAll"] 
       > <table>
       > <tr>
       >   <th>Nome do parâmetro</th> 
       >   <th>Descrição</th>
       > </tr>
       > <tr>
       >    <td><b>ec_expire</b></td>
       >    <td>Atribui um horário de expiração a um token, após o qual o token expira. Solicitações enviadas depois do horário expiração são negadas. Esse parâmetro usa um carimbo de data/hora Unix que se baseia no número de segundos desde a época Unix padrão de `1/1/1970 00:00:00 GMT`. (Você pode usar ferramentas online para converter entre hora padrão e hora Unix.)> 
       >    Por exemplo, se você quiser que o token expire em `12/31/2016 12:00:00 GMT`, use o valor de carimbo de data/hora Unix, `1483185600`. 
       > </tr>
       > <tr>
       >    <td><b>ec_url_allow</b></td> 
       >    <td>Permite personalizar tokens para determinado ativo ou caminho. Restringe o acesso às solicitações cuja URL começa com um caminho relativo específico. URLs diferenciam maiúsculas de minúsculas. Insira vários caminhos separando cada um com uma vírgula; não adicione espaços. Dependendo dos seus requisitos, você pode definir um valor diferente para fornecer um nível de acesso diferente.> 
       >    Por exemplo, para a URL `http://www.mydomain.com/pictures/city/strasbourg.png`, estas solicitações são permitidas para os seguintes valores de entrada: 
       >    <ul>
       >       <li>Valor de entrada `/`: todas as solicitações são permitidas.</li>
       >       <li>Valor de entrada `/pictures`, as seguintes solicitações são permitidas: <ul>
       >          <li>`http://www.mydomain.com/pictures.png`</li>
       >          <li>`http://www.mydomain.com/pictures/city/strasbourg.png`</li>
       >          <li>`http://www.mydomain.com/picturesnew/city/strasbourgh.png`</li>
       >       </ul></li>
       >       <li>Valor de entrada `/pictures/`: somente as solicitações que contêm o caminho `/pictures/` são permitidas. Por exemplo: `http://www.mydomain.com/pictures/city/strasbourg.png`.</li>
       >       <li>Valor de entrada `/pictures/city/strasbourg.png`: somente as solicitações para esse caminho e ativos específicos são permitidas.</li>
       >    </ul>
       > </tr>
       > <tr>
       >    <td><b>ec_country_allow</b></td> 
       >    <td>Permite somente solicitações originadas de um ou mais países especificados. Solicitações originadas em todos os outros países são negadas. Use um [código de país ISO 3166](https://msdn.microsoft.com/library/mt761717.aspx) de duas letras para cada país e separe cada um deles com uma vírgula; não adicione espaço. Por exemplo, se você quiser permitir o acesso apenas dos Estados Unidos e da França, insira `US,FR`.</td>
       > </tr>
       > <tr>
       >    <td><b>ec_country_deny</b></td> 
       >    <td>Nega solicitações originadas de um ou mais países especificados. Solicitações originadas em todos os outros países são permitidas. A implementação é a mesma que a do parâmetro <b>ec_country_allow</b>. Se houver um código de país nos parâmetros <b>ec_country_allow</b> e <b>ec_country_deny</b>, o parâmetro <b>ec_country_allow</b> terá precedência.</td>
       > </tr>
       > <tr>
       >    <td><b>ec_ref_allow</b></td>
       >    <td>Permite apenas solicitações do referenciador especificado. Um referenciador identifica a URL da página da Web vinculada ao recurso que está sendo solicitado. Não inclua o protocolo no valor do parâmetro.>    
       >    Os seguintes tipos de entrada são permitidos:
       >    <ul>
       >       <li>Um nome de host ou um nome de host e um caminho.</li>
       >       <li>Vários referenciadores. Para adicionar vários referenciadores, separe cada um com uma vírgula; não adicione espaço. Se você especificar um valor de referenciador, mas as informações do referenciador não forem enviadas na solicitação devido à configuração do navegador, essas solicitações serão negadas por padrão.</li> 
       >       <li>Solicitações com informações do referenciador ausentes ou em branco. Por padrão, o parâmetro <b>ec_ref_allow</b> bloqueia esses tipos de solicitações. Para permitir essas solicitações, insira o texto "ausente" ou insira um valor em branco (usando uma vírgula no fim).</li> 
       >       <li>Subdomínios. Para permitir subdomínios, digite um asterisco (\*). Por exemplo, para permitir todos os subdomínios de `contoso.com`, digite `*.contoso.com`.</li>
       >    </ul>     
       >    Por exemplo, para permitir o acesso para solicitações de `www.contoso.com`, todos os subdomínios em `contoso2.com` e solicitações com referenciadores em branco ou ausentes, insira `www.contoso.com,*.contoso.com,missing`.</td>
       > </tr>
       > <tr> 
       >    <td><b>ec_ref_deny</b></td>
       >    <td>Nega solicitações do referenciador especificado. A implementação é a mesma que a do parâmetro <b>ec_ref_allow</b>. Se houver uma referência presente nos parâmetros <b>ec_ref_allow</b> e <b>ec_ref_deny</b>, o parâmetro <b>ec_ref_allow</b> terá precedência.</td>
       > </tr>
       > <tr> 
       >    <td><b>ec_proto_allow</b></td> 
       >    <td>Permite apenas solicitações do protocolo especificado. Os valores válidos são `http`, `https` ou `http,https`.</td>
       > </tr>
       > <tr>
       >    <td><b>ec_proto_deny</b></td>
       >    <td>Nega solicitações do protocolo especificado. A implementação é a mesma que a do parâmetro <b>ec_proto_allow</b>. Se houver um protocolo presente nos parâmetros <b>ec_proto_allow</b> e <b>ec_proto_deny</b>, o parâmetro <b>ec_proto_allow</b> terá precedência.</td>
       > </tr>
       > <tr>
       >    <td><b>ec_clientip</b></td>
       >    <td>Restringe o acesso ao endereço IP do solicitante especificado. Há suporte para IPV4 e IPV6. Você pode especificar um único endereço IP de solicitação ou endereços IP associados a uma sub-rede específica. Por exemplo, `11.22.33.0/22` permite as solicitações de endereços IP 11.22.32.1 a 11.22.35.254.</td>
       > </tr>
       > </table>

    5. Depois de terminar de inserir valores de parâmetro de criptografia, selecione uma chave para criptografar (se você tiver criado uma chave principal e uma chave de backup) da lista **Chave a Criptografar**.
    
    6. Selecione uma versão de criptografia da lista **Versão Criptografia**: **V2** para a versão 2 ou **V3** para a versão 3 (recomendado). 

    7. Clique em **Criptografar** para gerar o token.

    Depois que o token é gerado, ele será exibido na caixa **Tokens Gerados**. Para usar o token, acrescente-o como uma cadeia de consulta ao final do arquivo no caminho da sua URL. Por exemplo: `http://www.domain.com/content.mov?a4fbc3710fd3449a7c99986b`.
        
    8. Como opção, teste seu token com a ferramenta de descriptografia para que você possa exibir os parâmetros do token. Cole o valor do token na caixa **Token a Descriptografar**. Selecione a de chave de criptografia para usar na lista **Chave a Descriptografar** e, em seguida, clique em **Descriptografar**.

    Depois que o token for descriptografado, seus parâmetros são exibidos na caixa **Parâmetros Originais**.

    9. Opcionalmente, personalize o tipo de código de resposta retornado quando uma solicitação é negada. Selecione **Habilitado**, em seguida, selecione o código de resposta da lista **Código de Resposta**. **Nome do Cabeçalho** é definido automaticamente como **Local**. Clique em **Salvar** para implementar o novo código de resposta. Para determinados códigos de resposta, você também deve inserir o URL da sua página de erro na caixa **Valor do Cabeçalho**. O código de resposta **403** (Proibido) é selecionado por padrão. 

3. Em **HTTP Grande**, clique em **Mecanismo de Regras**. Você usa o mecanismo de regras para definir os caminhos para aplicar o recurso, habilitar o recurso de autenticação de token e habilitar funcionalidades adicionais relacionadas à autenticação de token. Para obter mais informações, consulte [Referência do mecanismo de regras](cdn-rules-engine-reference.md).

    1. Selecione uma regra existente ou crie uma nova regra para definir o ativo ou o caminho ao qual você deseja aplicar a autenticação de token. 
    2. Para habilitar a autenticação de token em uma regra, selecione **[Autenticação de Token](cdn-rules-engine-reference-features.md#token-auth)** na lista **Recursos** e, em seguida, selecione **Habilitado**. Clique em **Atualização** se você estiver atualizando uma regra ou em **Adicionar** se você estiver criando uma regra.
        
    ![Exemplo de habilitação de autenticação de token do mecanismo de regras da CDN](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. O mecanismo de regras, você também pode habilitar recursos adicionais relacionados à autenticação de token. Para habilitar qualquer um dos recursos a seguir, selecione-o na lista **Recursos** e, em seguida, selecione **Habilitado**.
    
    - **[Código de negação de autenticação de token](cdn-rules-engine-reference-features.md#token-auth-denial-code)**: determina o tipo de resposta retornado para um usuário quando uma solicitação é negada. As regras definidas aqui substituem o código de resposta definido na seção **Tratamento de Negação Personalizado** na página de autenticação baseada em token.
    - **[Token de autenticação ignorar URL caso](cdn-rules-engine-reference-features.md#token-auth-ignore-url-case)**: determina se a URL usada para validar o token diferencia Maiúsculas de minúsculas.
    - **[Parâmetro de autenticação de token](cdn-rules-engine-reference-features.md#token-auth-parameter)**: renomeia o parâmetro de cadeia de caracteres de consulta de autenticação de token que aparece na URL solicitada. 
        
    ![Exemplo de configurações de autenticação de token do mecanismo de regras da CDN](./media/cdn-token-auth/cdn-rules-engine2.png)

5. Você pode personalizar seu token acessando o código-fonte no [GitHub](https://github.com/VerizonDigital/ectoken).
Os idiomas disponíveis incluem:
    
   - C
   - C#
   - PHP
   - Perl
   - Java
   - Python 

## <a name="azure-cdn-features-and-provider-pricing"></a>Preços de provedor e recursos da Azure CDN

Para informações sobre os recursos, consulte [Visão Geral da CDN](cdn-overview.md). Para obter informações sobre preços, consulte [preços de Rede de Distribuição de Conteúdo](https://azure.microsoft.com/pricing/details/cdn/).
