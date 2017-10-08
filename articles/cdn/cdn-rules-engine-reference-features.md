---
title: recursos do mecanismo de regras de aaaAzure CDN | Microsoft Docs
description: "Documentação de referência para recursos e condições de correspondência do mecanismo de regras da CDN do Azure."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Recursos do mecanismo de regras da CDN do Azure
Este tópico lista as descrições detalhadas dos recursos disponíveis Olá para o Azure Content Delivery Network (CDN) [mecanismo de regras](cdn-rules-engine.md).

Olá terceira parte de uma regra é o recurso de saudação. Um recurso define o tipo de saudação da ação que será aplicado toohello tipo de solicitação identificado por um conjunto de condições de correspondência.

## <a name="access"></a>Access

Esses recursos são projetados toocontrol toocontent de acesso.


Nome | Finalidade
-----|--------
Negar Acesso | Determina se todas as solicitações são rejeitadas com uma resposta 403 Proibido.
Autenticação de Token | Determina se a autenticação baseada em Token será aplicado tooa solicitação.
Código de Negação de Autenticação de Token | Determina o tipo de saudação da resposta será retornado tooa usuário quando uma solicitação é negada devido a autenticação baseada em tooToken.
Autenticação de Token Ignorar Maiúsculas e Minúsculas da URL | Determina se as comparações de URL feitas por autenticação baseada em token diferenciam maiúsculas de minúsculas.
Parâmetros de Autenticação de Token | Determina se o parâmetro de cadeia de caracteres de consulta de autenticação baseada em Token Olá deve ser renomeado.

### <a name="deny-access"></a>Negar Acesso
**Finalidade**: determina se todas as solicitações são rejeitadas com uma resposta 403 Proibido.

Valor | Result
------|-------
habilitado| Faz com que todas as solicitações que satisfazem toobe critérios correspondentes Olá rejeitada com resposta 403 Proibido.
Desabilitado| Restaura o comportamento padrão de saudação. comportamento padrão de saudação é tooallow Olá origem toodetermine Olá tipo de servidor de resposta será retornado.

**Comportamento Padrão**: Desabilitado

> [!TIP]
   > Um dos usos possíveis para esse recurso é tooassociate com um cabeçalho de solicitação corresponde Referenciadores tooHTTP de acesso de tooblock de condição que estão usando o conteúdo embutido links tooyour.

### <a name="token-auth"></a>Autenticação de Token
**Finalidade:** determina se a autenticação baseada em Token será aplicado tooa solicitação.

Se a autenticação baseada em Token é habilitada, somente solicitações que fornecem um token criptografado e cumprir os requisitos de toohello especificados por esse token serão atendidas.

chave de criptografia de saudação que serão usados valores de tooencrypt e descriptografia de token é determinado pela chave primária e as opções de chave de Backup na página autenticação de Token. Lembre-se de que as chaves de criptografia são específicas da plataforma.

Valor | Result
------|---------
habilitado | Protege Olá solicitado conteúdo com autenticação baseada em Token. Somente as solicitações de clientes que fornecerem um token válido e atenderem aos requisitos serão respeitadas. Transações de FTP são excluídas da Autenticação Baseada em Token.
Desabilitado| Restaura o comportamento padrão de saudação. Olá comportamento padrão é tooallow sua toodetermine de configuração de autenticação baseada em Token, se uma solicitação será protegida.

**Comportamento padrão:** desabilitado.

###<a name="token-auth-denial-code"></a>Código de Negação de Autenticação de Token
**Finalidade:** determina o tipo de saudação da resposta será retornado tooa usuário quando uma solicitação é negada devido a autenticação baseada em tooToken.

códigos de resposta disponíveis Olá estão listados abaixo.

Código de Resposta|Nome da Resposta|Descrição
----------------|-----------|--------
301|Movido Permanentemente|Esse código de status redireciona os usuários não autorizados toohello URL especificado no cabeçalho de localização.
302|Encontrado|Esse código de status redireciona os usuários não autorizados toohello URL especificado no cabeçalho de localização. Esse código de status é o método padrão da indústria Olá da execução de um redirecionamento.
307|Redirecionamento Temporário|Esse código de status redireciona os usuários não autorizados toohello URL especificado no cabeçalho de localização.
401|Não Autorizado|Combinando esse código de status com o cabeçalho de resposta WWW-Authenticate permite tooprompt um usuário para autenticação.
403|Proibido|Este é o saudação padrão 403 Proibido mensagem de status que um usuário não autorizado verão quando tentar tooaccess conteúdo protegido.
404|Arquivo Não Encontrado|Esse código de status indica que o cliente HTTP Olá foi capaz de toocommunicate com o servidor de saudação, mas Olá solicitado conteúdo não foi encontrado.

#### <a name="url-redirection"></a>Redirecionamento de URL

Esse recurso oferece suporte a URL redirecionamento URL tooa definida pelo usuário quando ele é configurado tooreturn um código de status 3xx. Essa URL definida pelo usuário pode ser especificada executando Olá etapas a seguir:

1. Selecione um código de resposta de 3xx para o recurso de código de negação do Token de autenticação de saudação.
2. Selecione "Local" da opção de Nome de Cabeçalho Opcional.
3. Defina a URL do valor de cabeçalho opcional opção toohello desejado.

Se uma URL não está definida para um código de status 3xx, em seguida, hello página de resposta padrão para um código de status 3xx retornará toohello usuário.

O redirecionamento de URL só é aplicável para códigos de resposta 3xx.

A opção de Valor de Cabeçalho Opcional dá suporte a caracteres alfanuméricos, aspas e espaços.

#### <a name="authentication"></a>Autenticação

Esse recurso oferece suporte ao cabeçalho de tooinclude o WWW-Authenticate recurso Olá ao responder a solicitação não autorizada tooan para conteúdo protegido por autenticação baseada em Token. Se o cabeçalho WWW-Authenticate tiver sido definido muito "básico" em sua configuração, usuário não autorizado Olá será solicitado para credenciais de conta.

Olá acima configuração pode ser obtida executando Olá etapas a seguir:

1. Selecione "401" como o código de resposta de saudação do recurso de código de negação do Token de autenticação de saudação.
2. Selecione "WWW-Authenticate" da opção de Nome de Cabeçalho Opcional.
3. Definir a opção de valor de cabeçalho opcional muito "básica".

O cabeçalho WWW-Authenticate só é aplicável a códigos de resposta 401.

### <a name="token-auth-ignore-url-case"></a>Autenticação de Token Ignorar Maiúsculas e Minúsculas da URL
**Finalidade:** determina se as comparações de URL feitas por autenticação baseada em token diferenciam maiúsculas de minúsculas.

Olá parâmetros afetados por esse recurso são:

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

Os valores válidos são:

Valor|Result
---|----
habilitado|Faz com que o nosso servidor de borda tooignore caso ao comparar as URLs para os parâmetros de autenticação baseada em Token.
Desabilitado|Restaura o comportamento padrão de saudação. comportamento padrão de saudação é para comparações de URL para autenticação de Token toobe diferencia maiusculas de minúsculas.

**Comportamento padrão:** desabilitado.
 
### <a name="token-auth-parameter"></a>Parâmetros de Autenticação de Token
**Finalidade:** determina se o parâmetro de cadeia de caracteres de consulta de autenticação baseada em Token Olá deve ser renomeado.

Informações de chave:

- A opção de valor define o nome do parâmetro hello consulta cadeia de caracteres por meio do qual um token pode ser especificado.
- A opção de valor não pode ser definida muito "ec_token".
- Certifique-se de que nome hello definido apenas a opção de valor 
- contém caracteres de URL válidos.

Valor|Result
----|----
habilitado|A opção de valor define o nome do parâmetro hello consulta cadeia de caracteres por meio do qual os tokens devem ser definidos.
Desabilitado|Um token pode ser especificado como um parâmetro de cadeia de caracteres de consulta indefinido na URL de solicitação de saudação.

**Comportamento padrão:** desabilitado. Um token pode ser especificado como um parâmetro de cadeia de caracteres de consulta indefinido na URL de solicitação de saudação.

## <a name="caching"></a>Cache

Esses recursos são projetado toocustomize quando e como o conteúdo é armazenado em cache.

Nome | Finalidade
-----|--------
Parâmetros de Largura de Banda | Determina se os parâmetros de limitação de largura de banda (isto é, ec_rate e ec_prebuf) estarão ativos.
Limitação de Largura de Banda | Limita a largura de banda Olá para resposta Olá fornecida pelos nossos servidores de borda.
Ignorar o Cache | Determina se a solicitação de saudação pode aproveitar nossa tecnologia de cache.
Tratamento de Cabeçalho Cache-Control | Controles Olá geração de cabeçalhos Cache-Control pelo servidor de borda hello quando o recurso de Max-Age externo está ativo.
Cadeia de Caracteres da Consulta da Chave de Cache | Determina se a chave de cache Olá incluir ou excluir parâmetros de cadeia de caracteres de consulta associados a uma solicitação.
Regravação da Chave de Cache | Regrava Olá-chave do cache associado a uma solicitação.
Concluir o Preenchimento do Cache | Determina o que acontece quando uma solicitação resulta em uma perda no cache parcial em um servidor de borda.
Compactar Tipos de Arquivo | Define os formatos de arquivo hello serão compactados no servidor de saudação.
Idade Máxima Interna Padrão | Determina o intervalo de idade máxima saudação padrão para a revalidação do cache servidor servidor tooorigin da borda.
Tratamento do Cabeçalho Expira | Controles Olá geração de expira por um servidor de borda quando Olá externo Max-Age recurso está ativo.
Idade Máxima Externa | Determina o intervalo de idade máxima de saudação de revalidação do cache do navegador tooedge server.
Forçar Idade Máxima Interna | Determina o intervalo de idade máxima de saudação de revalidação do cache servidor servidor tooorigin da borda.
Suporte a H.264 (Download Progressivo de HTTP) | Determina os tipos de saudação de h. 264 formatos que podem ser usado toostream o conteúdo do arquivo.
Respeitar Solicitação Sem Cache | Determina se solicitações sem cache de um HTTP do cliente serão encaminhadas toohello servidor de origem.
Ignorar Ausência de Cache de Origem | Determina se nosso CDN irá ignorar determinadas diretivas atendidas por um servidor de origem.
Ignorar Intervalos Insatisfatórios | Determina a resposta de saudação que será retornada tooclients quando uma solicitação gera um código de status 416 Intervalo solicitado não satisfatório.
Máximo de Estado Obsoleto Interno | Controla quanto tempo ultrapassaram o tempo de expiração normal Olá um ativo em cache pode ser atendido a partir de um servidor de borda quando o servidor de borda de saudação é toorevalidate não é possível Olá ativo em cache no servidor de origem de saudação.
Compartilhamento de Cache Parcial | Determina se uma solicitação pode gerar conteúdo parcialmente em cache.
Pré-validar Conteúdo Armazenado em Cache | Determina se o conteúdo armazenado em cache será qualificado para revalidação antecipada antes que o TTL expire.
Atualizar Arquivos de Cache de Zero Byte. | Determina como a solicitação de cliente HTTP para um ativo de cache de zero byte é tratado por nossos servidores de borda.
Definir Códigos de Status Armazenáveis em Cache | Define o conjunto de saudação de códigos de status que pode resultar em conteúdo armazenado em cache.
Distribuição de Conteúdo Obsoleta em Erro | Determina se expirado conteúdo armazenado em cache será entregue quando ocorre um erro durante a revalidação do cache ou Olá recuperar conteúdo da solicitação do servidor de origem do cliente hello.
Obsoleto Ao Revalidar | Melhora o desempenho permitindo que nossos servidores de borda tooserve solicitante de toohello de cliente obsoleto enquanto revalidação ocorre.
Comentário | o recurso de comentário Hello permite um toobe Observação adicionada dentro de uma regra.

###<a name="bandwidth-parameters"></a>Parâmetros de Largura de Banda
**Finalidade:** determina se os parâmetros de limitação de largura de banda (isto é, ec_rate e ec_prebuf) estarão ativos.

Parâmetros de limitação de largura de banda determinam se Olá taxa de transferência de dados para uma solicitação do cliente poderá ser taxa personalizada tooa limitado.

Valor|Result
--|--
habilitado|Permite que os nossos servidores de borda toohonor de largura de banda solicitações.
Desabilitado|Faz a nossos servidores de borda tooignore de largura de banda parâmetros. Olá solicitou o conteúdo será servido normalmente (ou seja, sem limitação de largura de banda).

**Comportamento padrão:** habilitado.

###<a name="bandwidth-throttling"></a>Limitação de Largura de Banda
**Finalidade:** limitadores Olá largura de banda para resposta Olá fornecida pelos nossos servidores de borda.

Ambos Olá as opções a seguir devem ser definido tooproperly configurar limitação de largura de banda.

Opção|Descrição
--|--
Kbytes por segundo|Defina essa opção toohello largura de banda máxima (Kb por segundo) que pode ser usados toodeliver Olá resposta.
Segundos de Prebuf|Defina essa opção toohello quantos segundos nossos servidores de borda aguardará até que a limitação de largura de banda. Olá finalidade esse período de tempo de largura de banda irrestrito é tooprevent um reprodutor de mídia do apresentando falhas ou problemas devido a limitação de toobandwidth de buffer.

**Comportamento padrão:** desabilitado.

###<a name="bypass-cache"></a>Ignorar o Cache
**Finalidade:** determina se a solicitação de saudação pode aproveitar nossa tecnologia de cache.

Valor|Result
--|--
habilitado|Faz com que todos os toofall de solicitações por meio do servidor de origem toohello, mesmo se o conteúdo de saudação anteriormente foi armazenado em cache nos servidores de borda.
Desabilitado|Faz a servidores de borda ativos toocache acordo com a política de cache de toohello definido em seus cabeçalhos de resposta.

**Comportamento padrão:**

- **HTTP Grande:** Desabilitado

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Tratamento de Cabeçalho Cache-Control
**Finalidade:** controla a geração de saudação de cabeçalhos Cache-Control pelo servidor de borda de saudação quando o recurso de Max-Age externo está ativo.

Olá tooachieve de maneira mais fácil esse tipo de configuração é tooplace Olá Max-Age externo e recursos de tratamento de cabeçalho Cache-Control Olá no hello mesma instrução.

Valor|Result
--|--
Substituir|Garante que Olá seguintes ações ocorrerá:<br/> -Substitui o cabeçalho Cache-Control gerado pelo servidor de origem de saudação. <br/>-Adiciona o cabeçalho Cache-Control produzido pelo Olá resposta de toohello de recurso externo Max-Age.
Passagem|Garante que o cabeçalho Cache-Control produzido pelo recurso de Max-Age externo Olá nunca é adicionado toohello resposta. <br/> Se o servidor de origem Olá produz um cabeçalho Cache-Control, passa por toohello do usuário final. <br/> Se o servidor de origem Olá não produz um cabeçalho Cache-Control e, em seguida, essa opção a causa toonot de cabeçalho de resposta de saudação pode conter um cabeçalho Cache-Control.
Adicionar se Ausente|Se um cabeçalho Cache-Control não foi recebido do servidor de origem hello, essa opção adiciona o cabeçalho Cache-Control produzido pelo recurso de Max-Age externo hello. Essa opção é útil para garantir que um cabeçalho Cache-Control seja atribuído a todos os ativos.
Remover| Essa opção garante que um cabeçalho Cache-Control não está incluído com hello cabeçalho de resposta. Se já tiver sido atribuído a um cabeçalho Cache-Control, em seguida, ele será removido da resposta do cabeçalho hello.

**Comportamento Padrão:** Substituir.

###<a name="cache-key-query-string"></a>Cadeia de Caracteres da Consulta da Chave de Cache
**Finalidade:** determina se a chave de cache incluirá ou excluirá parâmetros de cadeia de caracteres de consulta associados a uma solicitação.

Informações de chave:

- Especifique um ou mais nomes de parâmetro de cadeia de caracteres de consulta. Cada nome de parâmetro deve ser delimitado por um único espaço.
- Este recurso determina se parâmetros de cadeia de caracteres de consulta serão incluídos ou excluídos da chave de cache hello. Informações adicionais são fornecidas para cada opção abaixo.

Tipo|Descrição
--|--
 Incluir|  Indica que cada parâmetro especificado deve ser incluído na chave de cache hello. Uma cache-key exclusiva será gerada para cada solicitação que contém um valor exclusivo para um parâmetro de cadeia de caracteres de consulta definido neste recurso. 
 Incluir Todos  |Indica que uma chave exclusiva de cache será criada para cada ativo de tooan de solicitação que inclui uma cadeia de caracteres de consulta exclusiva. Esse tipo de configuração não é normalmente recomendado porque ele pode levar tooa pequena porcentagem de acertos do cache. Isso aumenta a carga Olá no servidor de origem hello, pois terá tooserve mais solicitações. Essa configuração duplicatas Olá comportamento conhecido como "exclusivo-cache" na página de cache de cadeia de caracteres de consulta do cache. 
 Excluir | Indica que somente Olá especificado parâmetros serão excluídos da chave de cache hello. Todos os outros parâmetros de cadeia de caracteres de consulta serão incluídos na chave de cache hello. 
 Excluir Todos  |Indica que todos os parâmetros de cadeia de caracteres de consulta serão excluídos da chave de cache hello. Essa configuração duplicatas padrão Olá comportamento, que é conhecido como "standard-cache" na página de cache de cadeia de caracteres de consulta do cache. 

alimentação de saudação do mecanismo de regras de HTTP permite que você toocustomize maneira de saudação em que o cache de cadeia de caracteres de consulta é implementado. Por exemplo, você pode especificar que o cache de cadeia de caracteres de consulta seja executado somente em determinados tipos de arquivos ou locais.

Se desejar que a cadeia de consulta de saudação tooduplicate comportamento conhecido como "no-cache" na página de cache de cadeia de caracteres de consulta do cache, você precisará toocreate uma regra que contém uma condição de correspondência de curinga de consulta de URL e um recurso de desvio de Cache. Olá condição de correspondência de curinga de consulta de URL deve ser definido tooan asterisco (*).

#### <a name="sample-scenarios"></a>Cenários de Exemplo

O exemplo de uso para esse recurso é fornecido abaixo. Um exemplo de solicitação e saudação padrão a chave de cache são fornecidas abaixo.

- **Solicitação de exemplo:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01
- **Default cache-key:** /800001/Origin/folder/asset.htm

##### <a name="include"></a>Incluir

Configuração de exemplo:

- **Tipo:** Incluir
- **Parâmetro(s):** idioma

Esse tipo de configuração geraria Olá chave de cache de parâmetro de cadeia de caracteres de consulta a seguir:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>Incluir Todos

Configuração de exemplo:

- **Tipo:** Incluir Todos

Esse tipo de configuração geraria Olá chave de cache de parâmetro de cadeia de caracteres de consulta a seguir:

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>Excluir

Configuração de exemplo:

- **Tipo:** Excluir
- **Parâmetros:** sessionid userid

Esse tipo de configuração geraria Olá chave de cache de parâmetro de cadeia de caracteres de consulta a seguir:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>Excluir Todos

Configuração de exemplo:

- **Tipo:** Excluir Todos

Esse tipo de configuração geraria Olá chave de cache de parâmetro de cadeia de caracteres de consulta a seguir:

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>Regravação da Chave de Cache
**Finalidade:** regravações Olá associado a uma solicitação de chave de cache.

Uma chave de cache é o caminho relativo de saudação que identifica um ativo para fins de saudação do armazenamento em cache. Em outras palavras, nossos servidores irá verificar se há uma versão em cache de um ativo de acordo com o caminho tooits conforme definido pela chave de cache.

Configure esse recurso definindo ambos Olá as opções a seguir:

Opção|Descrição
--|--
Caminho Original| Defina Olá caminho relativo toohello tipos de solicitações cuja chave de cache será recriado. Um caminho relativo pode ser definido selecionando um caminho de origem de base e, em seguida, definindo uma expressão regular padrão.
Novo Caminho|Defina caminho relativo Olá Olá novo-chave de cache. Um caminho relativo pode ser definido selecionando um caminho de origem de base e, em seguida, definindo uma expressão regular padrão. Esse caminho relativo pode ser construído dinamicamente por meio do uso de saudação de variáveis de HTTP
**Comportamento padrão:** chave de cache da solicitação é determinado pelo URI de solicitação de saudação.

###<a name="complete-cache-fill"></a>Concluir o Preenchimento do Cache
**Finalidade:** determina o que acontece quando uma solicitação resulta em uma perda no cache parcial em um servidor de borda.

Um erro de cache parcial descreve o status de cache de saudação para um ativo que não foi completamente baixado tooan servidor de borda. Se um ativo é apenas parcialmente em cache em um servidor de borda, em seguida, hello próxima solicitação para esse ativo será encaminhada novamente toohello servidor de origem.
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
Um erro de cache parcial normalmente ocorre depois que um usuário anula um download ou para ativos que são solicitados somente usando solicitações de intervalo HTTP. Esse recurso é mais útil para grandes ativos em que os usuários não normalmente baixarão do início toofinish (por exemplo, vídeos). Como resultado, esse recurso é habilitado por padrão na plataforma HTTP grande hello. Isso é desabilitado em todas as outras plataformas.

Configuração do tooleave saudação padrão para a plataforma de HTTP grande Olá, é recomendável porque ele irá reduzir a carga de saudação em seu servidor de origem do cliente e aumentar a velocidade de saudação em que os clientes baixam seu conteúdo.

Devido a maneira de toohello no cache de quais configurações são controladas, esse recurso não pode ser associado com hello seguintes condições de correspondência: Cname de borda, Literal de cabeçalho de solicitação, curinga de cabeçalho de solicitação, Literal de consulta de URL e curinga de consulta da URL.

Valor|Result
--|--
habilitado|Restaura o comportamento padrão de saudação. comportamento padrão de saudação é tooforce Olá borda server tooinitiate uma busca em segundo plano do ativo de saudação do servidor de origem de saudação. Após o qual ativo hello serão no cache local do servidor de borda hello.
Desabilitado|Impede que um servidor de borda realizar uma busca em segundo plano para ativo hello. Isso significa que essa solicitação Avançar Olá para esse ativo dessa região fará com que um toorequest de servidor de borda do servidor de origem do cliente hello.

**Comportamento padrão:** habilitado.

###<a name="compress-file-types"></a>Compactar Tipos de Arquivo
**Finalidade:** define os formatos de arquivo hello serão compactados no servidor de saudação.

Um formato de arquivo pode ser especificado usando o tipo de mídia da Internet (ou seja, Content-Type). Tipo de mídia da Internet é metadados independente de plataforma que permite que o formato de arquivo de saudação nossos servidores tooidentify de um determinado ativo. Uma lista dos tipos comuns de mídia da Internet é fornecida abaixo.

Tipo de Mídia da Internet|Descrição
--|--
texto/sem formatação|Arquivos de texto sem formatação
texto/html| Arquivos HTML
texto/css|Folhas de Estilo em Cascata (CSS)
aplicativo/x-javascript|JavaScript
aplicativo/javascript|JavaScript
Informações de chave:

- Especifique vários tipos de mídia da Internet delimitando cada um deles com um único espaço. 
- Esse recurso compactará apenas ativos cujo tamanho seja menor que 1 MB. Ativos maiores não serão compactados por nossos servidores.
- Determinados tipos de conteúdo, como imagens, vídeos e ativos de mídia de áudio (por exemplo, JPG, MP3, MP4 etc.) já são compactados. A compactação adicional nesses tipos de ativos não reduzirá significativamente o tamanho do arquivo. Portanto, é recomendável que você não habilite a compactação nesses tipos de ativos.
- Não há suporte para caracteres curinga, como asteriscos.
- Antes de adicionar esta regra de tooa de recurso, verifique tooset-se de que a opção de compactação desabilitado na página de compactação para Olá plataforma toowhich que essa regra será aplicada.

###<a name="default-internal-max-age"></a>Idade Máxima Interna Padrão
**Finalidade:** determina Olá max-age o intervalo padrão para revalidação do cache servidor servidor tooorigin da borda. Em outras palavras, quantidade Olá de tempo que decorrerá antes de um servidor de borda irá verificar se um ativo de cache corresponde ativo Olá armazenado no servidor de origem de saudação.

Informações de chave:

- Esta ação ocorrerá somente para respostas de um servidor de origem que não atribuiu uma indicação de max-age no cabeçalho Cache-Control ou Expires.
- Essa ação não ocorrerá para ativos que não são considerados armazenáveis em cache.
- Essa ação não afeta revalidações de exame de cache do navegador tooedge server. Esses tipos de revalidações de exame são determinados pelo controle de Cache ou expira enviadas toohello navegador, que pode ser personalizada com o recurso externo Max-Age.
- resultados Olá essa ação não tem um efeito observável em cabeçalhos de resposta de saudação e conteúdo de saudação retornado de servidores de borda para o seu conteúdo, mas pode ter um efeito na quantidade de saudação do tráfego de revalidação enviado do servidor de origem de tooyour de servidores de borda.
- Configure este recurso da seguinte forma:
    - Selecionando o código de status de saudação para o qual um padrão de max-age interno pode ser aplicada.
    - Especificando um valor inteiro e, em seguida, selecionando Olá unidade de tempo desejado (ou seja, segundos, minutos, horas, etc.). Esse valor define o intervalo de idade máxima saudação padrão interno.

- Unidade de tempo de saudação configuração muito "Desativado" atribuirá um intervalo de idade máxima interna padrão de 7 dias para solicitações que não tem sido atribuídas uma indicação de idade máxima em seu Cache-Control ou o cabeçalho Expires.
- Devido a maneira de toohello no cache de quais configurações são controladas, esse recurso não pode ser associado com hello correspondência condições a seguir: 
    - Edge 
    - Cname
    - Literal de Cabeçalho de Solicitação
    - Curinga de Cabeçalho de Solicitação
    - Método de Solicitação
    - Literal da Consulta da URL
    - Curinga da consulta da URL

**Valor Padrão:** 7 dias

###<a name="expires-header-treatment"></a>Tratamento do Cabeçalho Expira
**Finalidade:** controla a geração de saudação do expira por um servidor de borda quando o recurso de Max-Age externo está ativo.

Olá tooachieve de maneira mais fácil esse tipo de configuração é tooplace Olá Max-Age externo e recursos de tratamento de cabeçalho expira Olá no hello mesma instrução.

Valor|Result
--|--
Substituir|Garante que Olá seguintes ações ocorrerá:<br/>-Substitui o cabeçalho Expires gerado pelo servidor de origem de saudação.<br/>-Adiciona o cabeçalho Expires produzido pela resposta de toohello de recurso Olá Max-Age externo.
Passagem|Garante que o cabeçalho Expires produzido pelo recurso de Max-Age externo Olá nunca é adicionado toohello resposta. <br/> Se o servidor de origem Olá produz um cabeçalho de expiração, ele é transmitido toohello do usuário final. <br/>Se o servidor de origem Olá não produz um cabeçalho de expiração e, em seguida, essa opção a causa toonot de cabeçalho de resposta de saudação pode conter um cabeçalho de expiração.
Adicionar se Ausente| Se um cabeçalho de expiração não foi recebido do servidor de origem hello, essa opção adiciona o cabeçalho Expires produzido pelo recurso de Max-Age externo hello. Essa opção é útil para garantir que um cabeçalho Expires seja atribuído a todos os ativos.
Remover| Garante que um cabeçalho de expiração não está incluído com hello cabeçalho de resposta. Se já tiver sido atribuído a um cabeçalho de expiração, em seguida, ele será removido da resposta do cabeçalho hello.

**Comportamento Padrão:** Substituir

###<a name="external-max-age"></a>Idade Máxima Externa
**Finalidade:** intervalo de idade máxima de saudação determina para a revalidação do cache do navegador tooedge server. Em outras palavras, a quantidade de saudação de tempo que decorrerá antes de um navegador pode verificar para uma nova versão de um ativo de um servidor de borda.

Habilitar esse recurso irá gerar o Cache-controle: max-age e expira os cabeçalhos dos nossos servidores de borda e enviá-los toohello HTTP cliente. Por padrão, esses cabeçalhos substituirá os criados pelo servidor de origem de saudação. No entanto, o tratamento do cabeçalho Cache-Control e os recursos de tratamento de cabeçalho expira podem ser usado tooalter esse comportamento.

Informações de chave:

- Essa ação não afeta revalidações exame do cache de servidor edge servidor tooorigin. Esses tipos de revalidações de exame são determinados pelos cabeçalhos Cache-controle/Expires recebidos do servidor de origem Olá e podem ser personalizados com o padrão interno Max-Age e os recursos de Max-Age Force interno.
- Configure esse recurso, especificando um valor inteiro e selecione a unidade de tempo desejado hello (ou seja, segundos, minutos, horas, etc.).
- Definir esse valor negativo do recurso tooa faz com que o nosso toosend de servidores de borda um Cache-controle: não-cache e uma hora de expiração que está definida no hello passado com cada navegador toohello de resposta. Embora um cliente HTTP não armazenará em cache resposta hello, essa configuração não afetará a resposta do nossos servidores de borda capacidade toocache saudação do servidor de origem de saudação.
- Unidade de tempo de saudação configuração muito "Desativado" desabilitará esse recurso. Os cabeçalhos Cache-controle/expira em cache com a resposta de saudação do servidor de origem Olá passará por meio do navegador de toohello.

**Comportamento padrão:** desativado

###<a name="force-internal-max-age"></a>Forçar Idade Máxima Interna
**Finalidade:** intervalo de idade máxima de saudação determina para a revalidação do cache servidor servidor tooorigin da borda. Em outras palavras, quantidade de saudação de tempo que decorrerá antes de um servidor de borda pode verificar se um ativo de cache corresponde ativo Olá armazenado no servidor de origem de saudação.

Informações de chave:

- Esse recurso substituirá o intervalo de idade máxima de saudação definido em Cache-Control ou Expires cabeçalhos gerados a partir de um servidor de origem.
- Esse recurso não afeta revalidações de exame de cache do navegador tooedge server. Esses tipos de revalidações de exame são determinados pelo controle de Cache ou expira enviadas toohello navegador.
- Este recurso não tem um efeito observável em resposta Olá entregue por um solicitante de toohello do servidor de borda. No entanto, ele pode ter um efeito na quantidade de saudação do tráfego de revalidação enviado do nosso servidor de origem de toohello de servidores de borda.
- Configure este recurso da seguinte forma:
    - Selecionando o código de status de saudação para o qual um max-age interno será aplicada.
    - Especificando um valor inteiro e selecionando Olá unidade de tempo desejado (ou seja, segundos, minutos, horas, etc.). Esse valor define o intervalo de idade máxima da solicitação hello.

- Unidade de tempo de saudação configuração muito "Off" desabilita esse recurso. Um intervalo de idade máxima interno não será atribuído toorequested ativos. Se o cabeçalho original Olá não contém instruções de cache, em seguida, ativo Olá será armazenada na cache toohello a configuração ativa no recurso padrão interno Max-Age de acordo com.
- Devido a maneira de toohello no cache de quais configurações são controladas, esse recurso não pode ser associado com hello correspondência condições a seguir: 
    - Edge 
    - Cname
    - Literal de Cabeçalho de Solicitação
    - Curinga de Cabeçalho de Solicitação
    - Método de Solicitação
    - Literal da Consulta da URL
    - Curinga da consulta da URL

**Comportamento padrão:** desativado

###<a name="h264-support-http-progressive-download"></a>Suporte a H.264 (Download Progressivo de HTTP)
**Finalidade:** tipos de saudação determina de h. 264 formatos que podem ser usado toostream o conteúdo do arquivo.

Informações de chave:

- Defina um conjunto de extensões de nome de arquivo H.264 permitidas delimitadas por espaço na opção de Extensões de Arquivo. A opção de extensões de arquivo substituirá o comportamento padrão de saudação. Mantenha o suporte a MP4 e F4V incluindo as extensões de nome de arquivo ao definir esta opção. 
- Verifique se tooinclude um período quando especificar cada extensão de nome de arquivo (por exemplo,. F4V. mp4).

**Comportamento padrão:** o Download Progressivo de HTTP dá suporte à mídia MP4 e F4V por padrão.

###<a name="honor-no-cache-request"></a>Respeitar solicitação no-cache
**Finalidade:** determina se solicitações sem cache de um HTTP do cliente serão encaminhadas toohello servidor de origem.

Uma solicitação de cache não ocorre quando o cliente Olá HTTP envia um Cache-controle: não-cache e/ou Pragma:no-cabeçalho de cache na solicitação de saudação HTTP.

Valor|Result
--|--
habilitado|Permite que solicitações de sem cache de um cliente HTTP servidor de origem toobe toohello encaminhada e servidor de origem Olá retornará cabeçalhos de resposta hello e corpo Olá por meio do servidor de borda de saudação toohello back HTTP cliente.
Desabilitado|Restaura o comportamento padrão de saudação. comportamento padrão de saudação é tooprevent solicitações de cache não sejam encaminhadas toohello servidor de origem.

Para todo o tráfego de produção, é altamente recomendável tooleave esse recurso em seu estado padrão desativado. Caso contrário, não serão possível blindar a servidores de origem dos usuários finais que podem disparar inadvertidamente a muitas solicitações de cache não durante a atualização de páginas da web ou de saudação muitos players de mídia populares são codificados toosend um cabeçalho de cache não com cada solicitação de vídeo. No entanto, esse recurso pode ser útil tooapply preparação de não produção de toocertain ou diretórios, de teste toobe de conteúdo nova ordem tooallow extraída sob demanda do servidor de origem de saudação.

status de cache de saudação que serão relatados para uma solicitação que é permitida com o servidor de origem tooan toobe encaminhado devido toothis recurso é TCP_Client_Refresh_Miss. O relatório de status do Cache, que está disponível no módulo de relatório de núcleo hello, fornece informações estatísticas por status de cache. Isso permite que você tootrack número de saudação e a porcentagem de solicitações que estão sendo encaminhadas tooan o servidor de origem devido toothis recurso.

**Comportamento padrão:** desabilitado.

###<a name="ignore-origin-no-cache"></a>Ignorar no-cache de origem
**Finalidade:** determina se a nossa CDN ignora Olá diretivas atendidas a partir de um servidor de origem a seguir:

- Cache-Control: privado
- Cache-Control: no-store
- Cache-Control: no-cache
- Pragma: no-cache

Informações de chave:

- Configure esse recurso definindo uma lista delimitada por espaço dos códigos de status para o qual Olá acima diretivas será ignorada.
- Olá conjunto de códigos de status válido para esse recurso são: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 e 505.
- Desabilite esse recurso definindo-o valor em branco tooa.
- Devido a maneira de toohello no cache de quais configurações são controladas, esse recurso não pode ser associado com hello correspondência condições a seguir: 
    - Edge 
    - Cname
    - Literal de Cabeçalho de Solicitação
    - Curinga de Cabeçalho de Solicitação
    - Método de Solicitação
    - Literal da Consulta da URL
    - Curinga da consulta da URL

**Comportamento padrão:** o comportamento padrão é toohonor Olá acima diretivas.

###<a name="ignore-unsatisfiable-ranges"></a>Ignorar Intervalos Insatisfatórios 
**Finalidade:** determina a resposta de saudação que será retornada tooclients quando uma solicitação gera um código de status 416 Intervalo solicitado não satisfatório.

Por padrão, esse código de status é retornado quando Olá especificado a solicitação de intervalo de bytes não pode ser atendida por um servidor de borda e um campo de cabeçalho de solicitação de intervalo se não foi especificado.

Valor|Result
-|-
habilitado|Impede que nossos servidores de borda da solicitação de intervalo de bytes inválido tooan responde com um código de status 416 Intervalo solicitado não satisfatório. Em vez disso, nossos servidores entregará ativo solicitada hello e retornar uma resposta 200 Okey ao cliente hello.
Desabilitado|Restaura o comportamento padrão de saudação. comportamento padrão de saudação é toohonor o código de status 416 Intervalo solicitado não satisfatório.

**Comportamento padrão:** desabilitado.

###<a name="internal-max-stale"></a>Máximo de Estado Obsoleto Interno
**Finalidade:** controla quanto últimos saudação normal de validade um ativo em cache pode ser atendido a partir de um servidor de borda quando o servidor de borda Olá Olá toorevalidate não é possível em cache ativo no servidor de origem de saudação.

Normalmente, quando max-age tempo um ativo expira, o servidor de borda de saudação enviará um servidor de origem de toohello de solicitação de revalidação. Olá servidor de origem será, em seguida, responder com uma 304 não modificado para dar o servidor de borda Olá uma nova concessão ativo em cache Olá or else com 200 Okey para fornecer o servidor de borda de saudação com uma versão atualizada do ativo de saudação em cache.

Se o servidor de borda de saudação tooestablish não é possível uma conexão com o servidor de origem Olá durante a tentativa de tal a revalidação, esse recurso interno máximo obsoleta controla se e para Olá quanto tempo, servidor de borda pode continuar ativos do tooserve Olá agora obsoleta.

Observe que esse intervalo de tempo inicia quando max-age Olá ativo expira, não quando hello revalidação falha ocorre. Portanto, período máximo de saudação durante os quais um ativo possa ser atendido sem revalidação bem-sucedida é Olá tempo especificado pela combinação de saudação de max-age mais max obsoleta. Por exemplo, se um ativo foi armazenado em cache às 9:00, com uma duração de máximo de 30 minutos e obsoleta uma máximo de 15 minutos, e tente a revalidação falhou em 9:44 resultaria em uma usuário final recebimento Olá obsoletas em cache ativo, enquanto uma tentativa com falha revalidação às 9:46 resultaria em Olá ao usuário final receber um tempo limite de Gateway 504.

Qualquer valor configurado para esse recurso foi substituído pelo Cache-controle: precisa-revalidar ou armazenar em Cache-controle: proxy-revalidar cabeçalhos recebidos do servidor de origem de saudação. Se qualquer um desses cabeçalhos é recebida do servidor de origem hello quando inicialmente armazenado em cache um ativo, o servidor de borda Olá não fornecerá um ativo em cache desatualizado. Nesse caso, se o servidor de borda Olá for toorevalidate não é possível com origem hello quando o intervalo de idade máxima do ativo Olá tiver expirado, o servidor de borda Olá retornará um tempo limite de Gateway 504.

Informações de chave:

- Configure este recurso da seguinte forma:
    - Selecionando o código de status de saudação para o qual um obsoleto máximo será aplicado.
    - Especificando um valor inteiro e, em seguida, selecionando Olá unidade de tempo desejado (ou seja, segundos, minutos, horas, etc.). Esse valor define Olá interno máximo obsoleta que será aplicada.

- Unidade de tempo de saudação configuração muito "Desativado" desabilitará esse recurso. Um ativo em cache não será servido além de seu tempo de expiração normal.
- Devido a maneira de toohello no cache de quais configurações são controladas, esse recurso não pode ser associado com hello correspondência condições a seguir: 
    - Edge 
    - Cname
    - Literal de Cabeçalho de Solicitação
    - Curinga de Cabeçalho de Solicitação
    - Método de Solicitação
    - Literal da Consulta da URL
    - Curinga da consulta da URL

**Comportamento Padrão:** 2 minutos

###<a name="partial-cache-sharing"></a>Compartilhamento de Cache Parcial
**Finalidade:** determina se uma solicitação pode gerar conteúdo parcialmente em cache.

Esse cache parcial, em seguida, pode ser usado toofulfill novas solicitações para esse conteúdo até Olá solicitado totalmente armazenada em cache o conteúdo.

Valor|Result
-|-
Habilitado|As solicitações podem gerar conteúdo parcialmente em cache.
Desabilitado|Solicitações só podem gerar um totalmente armazenada em cache conteúdo da solicitação de versão de hello.

**Comportamento padrão:** desabilitado.

###<a name="prevalidate-cached-content"></a>Pré-validar Conteúdo Armazenado em Cache
**Finalidade:** determina se o conteúdo armazenado em cache será qualificado para revalidação antecipada antes que o TTL expire.

Defina Olá tempo de expiração toohello anterior de saudação solicitado TTL do conteúdo durante o qual ele estará qualificado para a revalidação antecipada.

Informações de chave:

- Selecionando "Desativado", como a unidade de tempo de saudação requer o lugar de tootake revalidação após o vencimento TTL do conteúdo armazenado em cache de saudação. O tempo não deve ser especificado e será ignorado.

**Comportamento padrão:** desativado. Revalidação só pode ocorrer depois de saudação TTL do conteúdo armazenado em cache tenha expirado.

###<a name="refresh-zero-byte-cache-files"></a>Atualizar Arquivos de Cache de Zero Byte
**Finalidade:** determina como a solicitação de cliente HTTP para um ativo de cache de zero byte é tratado por nossos servidores de borda.

Os valores válidos são:

Valor|Result
--|--
habilitado|Faz com que ativo borda server toore busca saudação do servidor de origem de saudação.
Desabilitado|Restaura o comportamento padrão de saudação. comportamento padrão de saudação é tooserve os ativos de cache válido na solicitação.
Este recurso não é necessário para o armazenamento em cache e o fornecimento de conteúdo corretos, mas pode ser útil como solução alternativa. Por exemplo, os geradores de conteúdo dinâmicos em servidores de origem inadvertidamente podem resultar em respostas de 0 bytes enviadas toohello os servidores de borda. Esses tipos de respostas normalmente são armazenados em cache por nossos servidores de borda. Se você souber que uma resposta de 0 byte nunca é uma resposta válida 

para esse tipo de conteúdo, em seguida, esse recurso pode impedir esses tipos de recursos servidos tooyour clientes.

**Comportamento padrão:** desabilitado.

###<a name="set-cacheable-status-codes"></a>Definir Códigos de Status Armazenáveis em Cache
**Finalidade:** define Olá conjunto de códigos de status que pode resultar em conteúdo armazenado em cache.

Por padrão, o cache é habilitado apenas para respostas 200 OK.

Defina um conjunto delimitada por espaço de códigos de status de saudação desejado.

Informações de chave:

- Habilite também o recurso de Ignorar No-Cache de Origem. Se esse recurso não estiver habilitado, respostas não 200 OK não poderão ser armazenadas em cache.
- Olá conjunto de códigos de status válido para esse recurso são: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 e 505.
- Esse recurso não pode ser usado toodisable cache para respostas que geram um código de status Okey 200.

**Comportamento padrão:** o armazenamento em cache só está habilitado para respostas que geram um código de status 200 OK.
###<a name="stale-content-delivery-on-error"></a>Distribuição de Conteúdo Obsoleta em Erro
**Finalidade:** 

Determina se expirado conteúdo armazenado em cache será entregue quando ocorre um erro durante a revalidação do cache ou Olá recuperar conteúdo da solicitação do servidor de origem do cliente hello.

Valor|Result
-|-
habilitado|Conteúdo obsoleto será servido toohello solicitante, quando ocorre um erro durante a um servidor de origem de tooan de conexão.
Desabilitado|Erro do servidor de origem Hello será encaminhado toohello solicitante.

**Comportamento Padrão:** Desabilitado

###<a name="stale-while-revalidate"></a>Obsoleto Ao Revalidar
**Finalidade:** melhora o desempenho permitindo que nossos servidores de borda tooserve toohello conteúdo obsoleto solicitante enquanto revalidação ocorre.

Informações de chave:

- comportamento de Olá desse recurso varia de acordo unidade de tempo selecionado toohello.
    - **Unidade de tempo:** especificar um período de tempo e selecione um tempo unidade (por exemplo, segundos, minutos, horas, etc.) tooallow obsoletos fornecimento de conteúdo. Esse tipo de instalação permite Olá CDN tooextend Olá período de tempo que pode entregar conteúdo antes de solicitar a validação de acordo com a seguinte fórmula de toohello:**TTL** + **enquanto revalidar hora obsoletos** 
    - **Desativar:** selecione "Desativado" revalidação toorequire antes de uma solicitação para conteúdo obsoleto pode ser atendido.
        - Não especifique um período de tempo, pois ele é inaplicável e será ignorado.

**Comportamento padrão:** desativado. Revalidação deve ocorrer antes do hello solicitado conteúdo possa ser atendido.

###<a name="comment"></a>Comentário
**Finalidade:** permite que um toobe Observação adicionada dentro de uma regra.

Um uso para esse recurso é tooprovide obter informações adicionais sobre o uso geral de saudação de uma regra ou por um determinado coincidem com a condição ou recurso foi adicionado toohello regra.

Informações de chave:

- Um máximo de 150 caracteres pode ser especificado.
- Verifique se tooonly use caracteres alfanuméricos.
- Esse recurso não afetam o comportamento de saudação da regra de saudação. É destinada apenas tooprovide uma área onde você pode fornecer informações para referência futura ou que pode ajudar a regra de saudação de solução de problemas.
 
## <a name="headers"></a>Cabeçalhos

Esses recursos são projetado tooadd, modificar ou excluir os cabeçalhos de resposta ou solicitação de saudação.

Nome | Finalidade
-----|--------
Cabeçalho de Resposta de Idade | Determina se um cabeçalho de resposta de idade será incluído na resposta de saudação enviada toohello solicitante.
Depurar Cabeçalhos de Resposta do Cache | Determina se uma resposta pode incluir o cabeçalho de resposta de X-EC-Debug Olá que fornece informações sobre a política de cache Olá para ativo solicitada hello.
Modificar Cabeçalho de Solicitação do Cliente | Substitui, acrescenta ou exclui um cabeçalho de uma solicitação.
Modificar Cabeçalho de Resposta do Cliente | Substitui, acrescenta ou exclui um cabeçalho de uma resposta.
Definir Cabeçalho Personalizado da IP do Cliente | Permite que endereço IP de saudação do cliente solicitante Olá toobe toohello adicionado solicitação como um cabeçalho de solicitação personalizado.

###<a name="age-response-header"></a>Cabeçalho de Resposta de Idade
**Finalidade**: determina se um cabeçalho de resposta de idade será incluído no hello resposta enviada toohello solicitante.
Valor|Result
--|--
habilitado | cabeçalho de resposta de idade Hello será incluído na resposta de saudação enviada toohello solicitante.
Desabilitado | cabeçalho de resposta de idade Hello será excluído da resposta de saudação enviada toohello solicitante.

**Comportamento Padrão**: Desabilitado.

###<a name="debug-cache-response-headers"></a>Depurar Cabeçalhos de Resposta do Cache
**Finalidade:** determina se uma resposta pode incluir o cabeçalho de resposta X-EC-Debug que fornece informações sobre a política de cache Olá para ativo solicitada hello.

Depurar a resposta do cache cabeçalhos serão incluídos na resposta hello quando ambas das seguintes Olá forem verdadeiras:

- Olá depurar recurso de cabeçalhos de resposta do Cache foi habilitado na solicitação de saudação desejado.
- Olá acima solicitação define o conjunto de saudação de cabeçalhos de resposta do cache de depuração que será incluído na resposta de saudação.

Resposta do cache cabeçalhos podem ser solicitados, incluindo Olá cabeçalho a seguir e Olá diretivas desejadas na solicitação de saudação de depuração:

X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_

**Exemplo:**

X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

Valor|Result
-|-
Habilitado|Solicitações para cabeçalhos de resposta do cache de depuração retornarão uma resposta que inclui o cabeçalho X-EC-Debug.
Desabilitado|O cabeçalho de resposta X-EC-Debug será excluído da resposta de saudação.

**Comportamento padrão:** desabilitado.

###<a name="modify-client-response-header"></a>Modificar Cabeçalho de Resposta do Cliente
**Finalidade:** cada solicitação contém um conjunto de [cabeçalhos de solicitação]() que a descrevem. Este recurso pode:

- Acrescentar ou substituir o valor de saudação atribuído tooa cabeçalho de solicitação. Se não existir um cabeçalho de solicitação especificado hello, em seguida, esse recurso será adicionada toohello solicitação.
- Exclua um cabeçalho de solicitação da solicitação de saudação.

Solicitações que são encaminhadas tooan servidor de origem refletirá as alterações de saudação feitas por esse recurso.

Uma das seguintes ações de saudação pode ser executada em um cabeçalho de solicitação:

Opção|Descrição|Exemplo
-|-|-
Acrescentar|Olá especificado valor será adicionado paraextremidade do valor de cabeçalho de solicitação existente hello.|**Valor de cabeçalho de solicitação (cliente):**Valor1 <br/> **Valor de cabeçalho de solicitação (Mecanismo de Regras de HTTP):** Valor2 <br/>**Novo valor de cabeçalho de solicitação:** Value1Value2
Substituir|solicitação Olá valor de cabeçalho será conjunto toohello o valor especificado.|**Valor de cabeçalho de solicitação (cliente):**Valor1 <br/>**Valor de cabeçalho de solicitação (Mecanismo de Regras de HTTP):** Valor2 <br/>**Novo valor de cabeçalho de solicitação:** Value2 <br/>
Exclusão|Exclui o cabeçalho de solicitação especificado hello.|**Valor de cabeçalho de solicitação (cliente):**Valor1 <br/> **Modificar configuração do cabeçalho de solicitação de cliente:** cabeçalho de solicitação de saudação de exclusão em questão. <br/>**Resultado:** Olá especificado de cabeçalho de solicitação não será encaminhado toohello servidor de origem.

Informações de chave:

- Certifique-se de que o valor de saudação especificado na opção de nome é uma correspondência exata para o cabeçalho de solicitação desejado hello.
- Caso não é levado em conta para finalidade de saudação de identificação de um cabeçalho. Por exemplo, qualquer Olá variações do nome do cabeçalho Cache-Control a seguir pode ser usado tooidentify-lo:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Verifique se tooonly usar caracteres alfanuméricos, traços ou sublinhados ao especificar um nome de cabeçalho.
- Excluir um cabeçalho impedirão de ser encaminhadas ao servidor de origem tooan por nossos servidores de borda.
- Olá cabeçalhos a seguir são reservados e não podem ser modificados por esse recurso:
    - encaminhado
    - host
    - via
    - Aviso
    - x-forwarded-for
    - Todos os nomes de cabeçalho que começam com "x-ec" são reservados.

###<a name="modify-client-response-header"></a>Modificar Cabeçalho de Resposta do Cliente
Cada resposta contém um conjunto de [cabeçalhos de resposta]() que o descrevem. Este recurso pode:

- Acrescentar ou substituir o valor de saudação atribuído tooa cabeçalho de resposta. Se não existir um cabeçalho de solicitação especificado hello, em seguida, esse recurso será adicionada toohello resposta.
- Exclua um cabeçalho de resposta da resposta de saudação.

Por padrão, os valores de cabeçalho de resposta são definidos por um servidor de origem e por nossos servidores de borda.

Uma das seguintes ações de saudação pode ser executada em um cabeçalho de resposta:

Opção|Descrição|Exemplo
-|-|-
Acrescentar|Olá especificado valor será adicionado paraextremidade do valor de cabeçalho de solicitação existente hello.|**Valor de cabeçalho de resposta (Cliente):**Valor1 <br/> **Valor de cabeçalho de resposta (Mecanismo de Regras de HTTP):** Valor2 <br/>**Novo valor de cabeçalho de resposta:** Value1Value2
Substituir|solicitação Olá valor de cabeçalho será conjunto toohello o valor especificado.|**Valor de cabeçalho de resposta (Cliente):**Valor1 <br/>**Valor de cabeçalho de resposta (Mecanismo de Regras de HTTP):** Valor2 <br/>**Novo valor de cabeçalho de resposta:** Value2 <br/>
Exclusão|Exclui o cabeçalho de solicitação especificado hello.|**Valor de cabeçalho (cliente) da solicitação:** Value1 <br/> **Modificar configuração do cabeçalho de solicitação de cliente:** cabeçalho de resposta de saudação de exclusão em questão. <br/>**Resultado:** Olá especificado de cabeçalho de resposta não será encaminhado toohello solicitante.

Informações de chave:

- Certifique-se de que o valor de saudação especificado na opção de nome é uma correspondência exata para o cabeçalho de resposta desejado de saudação. 
- Caso não é levado em conta para finalidade de saudação de identificação de um cabeçalho. Por exemplo, qualquer Olá variações do nome do cabeçalho Cache-Control a seguir pode ser usado tooidentify-lo:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Excluir um cabeçalho impedirão de ser encaminhadas toohello solicitante.
- Olá cabeçalhos a seguir são reservados e não podem ser modificados por esse recurso:
    - accept-encoding
    - age
    - connection
    - content-encoding
    - content-length
    - content-range
    - data
    - server
    - trailer
    - transfer-encoding
    - atualizar
    - vary
    - via
    - Aviso
    - Todos os nomes de cabeçalho que começam com "x-ec" são reservados.

###<a name="set-client-ip-custom-header"></a>Definir Cabeçalho Personalizado da IP do Cliente
**Finalidade:** adiciona um cabeçalho personalizado que identifica o cliente solicitante Olá pelo endereço IP do toohello solicitação.

A opção de nome de cabeçalho define o nome de saudação do cabeçalho de solicitação personalizado Olá onde o endereço IP do cliente hello será armazenado.

Esse recurso permite que um cliente toofind do servidor de origem endereços de IP do cliente por meio de um cabeçalho de solicitação personalizado. Se a solicitação de saudação é servida do cache, o servidor de origem Olá não será informado de endereço IP do cliente Olá. Portanto, é recomendável que esse recurso seja usado com ADN ou ativos que não serão ser armazenado em cache.

Verifique se que esse nome de cabeçalho especificado Olá não coincide com qualquer um dos seguintes hello:

- Nomes de cabeçalho de solicitação padrão. Uma lista de nomes de cabeçalho padrão pode ser encontrada em [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).
- Nomes de cabeçalho reservados:
    - forwarded-for
    - host
    - vary
    - via
    - Aviso
    - x-forwarded-for
    - Todos os nomes de cabeçalho que começam com "x-ec" são reservados.
 
## <a name="logs"></a>Logs

Esses recursos são dados de saudação toocustomize projetado armazenados em arquivos de log não processados.

Nome | Finalidade
-----|--------
Campo de Log Personalizado 1 | Determina o formato de saudação e o conteúdo de saudação que será atribuído o campo de log personalizado toohello em um arquivo de log não processados.
Cadeia de Caracteres de Consulta de Log | Determina se uma cadeia de caracteres de consulta será armazenada junto com a URL de saudação nos logs de acesso.

###<a name="custom-log-field-1"></a>Campo de Log Personalizado 1
**Finalidade:** determina o formato de saudação e o conteúdo de saudação que será atribuído o campo de log personalizado toohello em um arquivo de log não processados.

Olá principal objetivo por trás de campo personalizado é tooallow toodetermine quais valores de cabeçalho de solicitação e resposta serão armazenados nos arquivos de log.

Por padrão, o campo de log personalizado Olá é chamado "x-ec_custom-1". No entanto, o nome hello desse campo pode ser personalizado do [página de configurações de Log Raw]().

saudação de formatação que você deve usar os cabeçalhos de solicitação e resposta toospecify está definida abaixo.

Tipo de Cabeçalho|Formatar|Exemplos
-|-|-
Cabeçalho da Solicitação|%{[RequestHeader]()}[i]() | %{Accept-Encoding}i <br/> {Referer}i <br/> %{Authorization}i
Cabeçalho de Resposta|%{[ResponseHeader]()}[o]()| %{Age}o <br/> %{Content-Type}o <br/> %{Cookie}o

Informações de chave:

- Um campo de log personalizado pode conter qualquer combinação de campos de cabeçalho e texto sem formatação.
- Caracteres válidos para esse campo incluem o seguinte Olá: alfanuméricos (ou seja, 0-9, a-z e A-Z), traços, dois-pontos, ponto e vírgula, apóstrofos, vírgulas, pontos, sublinhados, sinais de igual, parênteses, colchetes e espaços. Olá símbolo de porcentagem e as chaves são permitidas apenas quando usado toospecify um campo de cabeçalho.
- ortografia Olá para cada campo de cabeçalho especificado deve corresponder ao nome de cabeçalho de solicitação/resposta desejada de hello.
- Se você quiser toospecify vários cabeçalhos, ele é recomendável que você use um separador tooindicate cada cabeçalho. Por exemplo, você poderia usar uma abreviação para cada cabeçalho. A sintaxe de exemplo é fornecida abaixo.
    - AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o 

**Valor Padrão:** -

###<a name="log-query-string"></a>Cadeia de Caracteres de Consulta de Log
**Finalidade:** determina se uma cadeia de caracteres de consulta será armazenada junto com a URL de saudação nos logs de acesso.

Valor|Result
-|-
habilitado|Permite o armazenamento de saudação de cadeias de caracteres de consulta durante a gravação de URLs em um log de acesso. Se uma URL não contiver uma cadeia de caracteres de consulta, essa opção não terá efeito.
Desabilitado|Restaura o comportamento padrão de saudação. comportamento padrão de saudação é tooignore cadeias de caracteres de consulta durante a gravação de URLs em um log de acesso.

**Comportamento padrão:** desabilitado.

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>Origem

Esses recursos são toocontrol projetado como Olá CDN se comunica com um servidor de origem.

Nome | Finalidade
-----|--------
Máximo de Solicitações Keep-Alive | Define o número máximo de saudação de solicitações para uma conexão Keep-Alive antes de ser fechado.
Cabeçalhos Especiais de Proxy | Define o conjunto de saudação de cabeçalhos de solicitação de CDN específico que será encaminhado de um servidor de origem de tooan de servidor de borda.


###<a name="maximum-keep-alive-requests"></a>Máximo de Solicitações Keep-Alive
**Finalidade:** define o número máximo de saudação de solicitações para uma conexão Keep-Alive antes de ser fechado.

Olá máximo valor do número de solicitações tooa baixa de configuração não é recomendado e pode resultar em degradação do desempenho.

Informações de chave:

- Especifique esse valor como um inteiro.
- Não incluir vírgulas ou pontos Olá especificado valor.

**Valor padrão:** 10.000 solicitações

###<a name="proxy-special-headers"></a>Cabeçalhos Especiais de Proxy
**Finalidade:** define o conjunto de saudação do [cabeçalhos de solicitação específica de CDN]() que será encaminhado de um servidor de origem de tooan de servidor de borda.

Informações de chave:

- Cada cabeçalho de solicitação de CDN específica definido neste recurso será encaminhado tooan servidor de origem.
- Impedir que um cabeçalho de solicitação específico CDN encaminhamento tooan servidor de origem, removendo-o da lista.

**Comportamento padrão:** todos os [cabeçalhos de solicitação específica de CDN]() serão encaminhados toohello servidor de origem.

## <a name="specialty"></a>Especialidade

Esses recursos fornecem funcionalidade avançada que deve ser usada somente por usuários avançados.

Nome | Finalidade
-----|--------
Métodos HTTP Armazenáveis em Cache | Determina o conjunto de saudação de métodos HTTP adicionais que podem ser armazenados em cache na rede.
Tamanho do Corpo da Solicitação Armazenável em Cache | Define o limite de saudação para determinar se uma resposta POST pode ser armazenados em cache.

###<a name="cacheable-http-methods"></a>Métodos HTTP Armazenáveis em Cache
**Finalidade:** determina o conjunto de saudação de métodos HTTP adicionais que podem ser armazenados em cache na rede.

Informações de chave:

- Esse recurso pressupõe que respostas GET devam ser sempre armazenadas em cache. Como resultado, Olá método HTTP GET não deve ser incluída ao configurar esse recurso.
- Esse recurso suporta apenas o método HTTP POST de saudação. Habilite o cache de resposta POST definindo esse recurso para: POST 
- Por padrão, somente as solicitações cujo corpo for menor do que 14 Kb serão armazenadas. Use o recurso de tamanho de corpo de solicitação armazenável em cache para definir o tamanho do corpo da solicitação máxima hello.

**Comportamento padrão:** apenas respostas GET serão armazenadas em cache.

###<a name="cacheable-request-body-size"></a>Tamanho do Corpo da Solicitação Armazenável em Cache

**Finalidade:** define o limite de saudação para determinar se uma resposta POST pode ser armazenados em cache.

Esse limite é determinado pela especificação de um tamanho máximo de corpo de solicitação. Solicitações que contiverem um corpo de solicitação maior não serão armazenadas.

Informações de chave:

- Esse recurso só é aplicável quando respostas POST são qualificadas para o cache. Use Olá armazenável recurso de métodos HTTP para habilitar o cache de solicitação POST.
- corpo da solicitação Olá é levado em consideração para:
    - x-www-form-urlencoded values
    - Garantindo um cache-key exclusivo
- Definir um tamanho de corpo de solicitação máximo grande pode afetar o desempenho de entrega de dados.
    - **Valor Recomendado:** 14 Kb
    - **Valor Mínimo:** 1 Kb

**Comportamento Padrão:** 14 Kb
 
## <a name="url"></a>URL

Esses recursos permitem que uma solicitação toobe redirecionado ou reescrita tooa outra URL.

Nome | Finalidade
-----|--------
Seguir Redirecionamentos | Determina se solicitações podem ser redirecionadas toohello hostname definido no cabeçalho de local de saudação retornado por um servidor de origem do cliente.
Redirecionamento de URL | Redireciona solicitações por meio do cabeçalho de local de saudação.
Regravação de URL  | Regrava Olá URL da solicitação.

###<a name="follow-redirects"></a>Seguir Redirecionamentos
**Finalidade:** determina se solicitações podem ser o nome de host redirecionado toohello definido no cabeçalho de local retornado por um servidor de origem do cliente.

Informações de chave:

- Solicitações só podem ser redirecionado tooedge CNAMEs que correspondem a toohello mesma plataforma.

Valor|Result
-|-
Habilitado|As solicitações podem ser redirecionadas.
Desabilitado|As solicitações não serão redirecionadas.

**Comportamento padrão:** desabilitado.
###<a name="url-redirect"></a>Redirecionamento de URL
**Finalidade:** redireciona as solicitações por meio do cabeçalho Local.

configuração de saudação desse recurso requer a definição Olá as opções a seguir:

Opção|Descrição
-|-
Código|Selecione o código de resposta de Olá que será retornado toohello solicitante.
Origem e Padrão| Essas configurações definem um padrão URI de solicitação que identifica o tipo de saudação de solicitações que podem ser redirecionadas. Somente solicitações cuja URL atende Olá critérios a seguir serão redirecionadas: <br/> <br/> **Origem** (ou ponto de acesso a conteúdo): selecione um caminho relativo que identifique um servidor de origem. Isso é a seção de "/XXXX/" hello e seu nome de ponto de extremidade. <br/> **Origem (padrão):** deve ser definido um padrão que identifica solicitações pelo caminho relativo. Esse padrão de expressão regular deve definir um caminho que começa diretamente depois Olá selecionado anteriormente o ponto de acesso ao conteúdo (veja acima). <br/> -Certifique-se de que os critérios URI de solicitação hello (ou seja, fonte e padrão) definido acima não entra em conflito com qualquer condição de correspondência definidas para esse recurso. <br/> -Verifique se toospecify um padrão. Usando um valor em branco como padrão Olá corresponderá apenas a pasta de raiz de toohello de solicitações do servidor de origem selecionado hello (por exemplo, http://cdn.mydomain.com/).
Destino| Definir URL Olá Olá toowhich acima solicitações será redirecionado. <br/> Construa dinamicamente esta URL usando: <br/> - Um padrão de expressão regular <br/>- Variáveis HTTP <br/> Substituir valores hello capturados no padrão de origem Olá no padrão de destino hello usando $ _n_  onde  _n_  identifica um valor por ordem de saudação em que ele foi capturado. Por exemplo, $1 representa o primeiro valor de saudação capturado no padrão de origem hello, enquanto $2 representa o valor de segundo hello. <br/> 
É altamente recomendável toouse uma URL absoluta. uso de saudação de uma URL relativa pode redirecionar um caminho inválido de tooan CDN URLs.

**Cenário de exemplo**

Neste exemplo, demonstraremos como tooredirect uma borda CNAME URL que resolve toothis base URL CDN: http://marketing.azureedge.net/brochures

Qualificando solicitações serão redirecionadas toothis borda base URL CNAME: http://cdn.mydomain.com/resources

O redirecionamento de URL pode ser obtido por meio de hello a seguinte configuração:![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**Pontos principais:**

- recurso de redirecionamento de URL de saudação define Olá URLs serão redirecionados de solicitação. Como resultado, as condições de correspondência adicionais não são necessárias. Embora a condição de correspondência de saudação foi definida como "Sempre", somente solicitações que toohello ponto será redirecionada a pasta de origem de cliente "marketing" hello "folhetos". 
- Todas as solicitações correspondentes serão redirecionadas toohello borda que CNAME URL definido na opção de destino. 
    - Cenário de exemplo 1: 
        - Solicitação de exemplo (URL da CDN): http://marketing.azureedge.net/brochures/widgets.pdf 
        - URL da solicitação (depois do redirecionamento): http://cdn.mydomain.com/resources/widgets.pdf  
    - Cenário de exemplo 2: 
        - Exemplo de solicitação (URL de CNAME de borda): http://marketing.mydomain.com/brochures/widgets.pdf 
        - URL da solicitação (depois do redirecionamento): http://cdn.mydomain.com/resources/widgets.pdf Cenário de exemplo
    - Cenário de exemplo 3: 
        - Solicitação de Exemplo (URL de CNAME de borda): http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - URL da solicitação (depois do redirecionamento): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- variável de solicitação de esquema (% {esquema}) Olá foi utilizado na opção de destino. Isso garante que o esquema da solicitação que Olá permanecerá inalterada depois que o redirecionamento.
- segmentos de URL Olá que foram capturados da solicitação de saudação são acrescentadas toohello nova URL por meio de "$1".
 
###<a name="url-rewrite"></a>Regravação de URL
**Finalidade:** regrava Olá URL de solicitação.

Informações de chave:

- configuração de saudação desse recurso requer a definição Olá as opções a seguir:

Opção|Descrição
-|-
 Origem e Padrão | Essas configurações definem um padrão URI de solicitação que identifica o tipo de saudação de solicitações que podem ser reconfigurados. Serão regravadas somente solicitações cuja URL atende Olá critérios a seguir: <br/>     - **Origem (ou ponto de acesso de conteúdo):** selecione um caminho relativo que identifique um servidor de origem. Isso é a seção de "/XXXX/" hello e seu nome de ponto de extremidade. <br/> - **Origem (padrão):** deve ser definido um padrão que identifica solicitações pelo caminho relativo. Esse padrão de expressão regular deve definir um caminho que começa diretamente depois Olá selecionado anteriormente o ponto de acesso ao conteúdo (veja acima). <br/> Certifique-se de que Olá solicitação URI critérios (ou seja, fonte e padrão) definidos acima não entrem em conflito com qualquer uma das condições de correspondência Olá definidas para esse recurso. Verifique se toospecify um padrão. Usando um valor em branco como padrão Olá corresponderá apenas a pasta de raiz de toohello de solicitações do servidor de origem selecionado hello (por exemplo, http://cdn.mydomain.com/). 
 Destino  |Definir a URL relativa Olá Olá toowhich acima solicitações será regravado por: <br/>    1. Selecionando um ponto de acesso ao conteúdo que identifica um servidor de origem. <br/>    2. Definindo um caminho relativo usando: <br/>        - Um padrão de expressão regular <br/>        - Variáveis HTTP <br/> <br/> Substituir valores hello capturados no padrão de origem Olá no padrão de destino hello usando $ _n_  onde  _n_  identifica um valor por ordem de saudação em que ele foi capturado. Por exemplo, $1 representa o primeiro valor de saudação capturado no padrão de origem hello, enquanto $2 representa o valor de segundo hello. 
 Esse recurso permite que nossos servidores de borda toorewrite Olá URL sem executar um redirecionamento tradicional. Isso significa que solicitante Olá receberá Olá mesma resposta de código como se tivesse sido solicitada Olá reescrita de URL.

**Cenário de exemplo 1**

Neste exemplo, demonstraremos como tooredirect uma borda CNAME URL que resolve toothis base URL CDN: http://marketing.azureedge.net/brochures/

Qualificando solicitações serão redirecionadas toothis borda base URL CNAME: http://MyOrigin.azureedge.net/resources/

O redirecionamento de URL pode ser obtido por meio de hello a seguinte configuração:![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**Cenário de exemplo 2**

Neste exemplo, demonstraremos como tooredirect uma borda CNAME URL de letras maiusculas toolowercase usando expressões regulares.

O redirecionamento de URL pode ser obtido por meio de hello a seguinte configuração:![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**Pontos principais:**

- recurso de reescrita de URL Olá define Olá URLs serão regravados de solicitação. Como resultado, as condições de correspondência adicionais não são necessárias. Embora a condição de correspondência de saudação foi definida como "Sempre", somente solicitações que toohello ponto será regravada pasta de origem de cliente "marketing" hello "folhetos".

- segmentos de URL Olá que foram capturados da solicitação de saudação são acrescentadas toohello nova URL por meio de "$1".



###<a name="compatibility"></a>Compatibilidade

Esse recurso inclui corresponde aos critérios que devem ser atendidos para que possa ser aplicado tooa solicitação. Em ordem tooprevent Configurando conflitantes critérios de correspondência, esse recurso é incompatível com hello correspondência condições a seguir:

- Número AS
- Origem CDN
- Endereço IP do Cliente
- Origem do Cliente
- Esquema de Solicitação
- Diretório do Caminho da URL
- Extensão do Caminho da URL
- Nome do Arquivo do Caminho da URL
- Literal do Caminho da URL
- Regex do Caminho da URL
- Curinga do Caminho da URL
- Literal da Consulta da URL
- Parâmetro da Consulta da URL
- Regex da consulta da URL
- Curinga da consulta da URL


## <a name="next-steps"></a>Próximas etapas
* [Referência do Mecanismo de Regras](cdn-rules-engine-reference.md)
* [Expressões Condicionais do Mecanismo de Regras](cdn-rules-engine-reference-conditional-expressions.md)
* [Condições de Correspondência do Mecanismo de Regras](cdn-rules-engine-reference-match-conditions.md)
* [Substituindo o comportamento HTTP padrão usando o mecanismo de regras de saudação](cdn-rules-engine.md)
* [Visão geral da CDN do Azure](cdn-overview.md)
