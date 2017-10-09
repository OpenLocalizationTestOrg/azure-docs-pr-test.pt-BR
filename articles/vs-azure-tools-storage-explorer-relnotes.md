---
title: "Notas de versão do Gerenciador de armazenamento do Azure (visualização) aaaMicrosoft | Microsoft Docs"
description: "Notas de versão do Gerenciador de Armazenamento do Microsoft Azure (Visualização)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Notas de versão do Gerenciador de Armazenamento do Microsoft Azure (Visualização)

Este artigo contém a versão de hello anotações para o Azure Storage Explorer 0.8.16 (visualização) da versão, bem como notas de versão para versões anteriores.

[Gerenciador de armazenamento do Microsoft Azure (visualização)](./vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Linux, Windows e macOS.

## <a name="version-0816-preview"></a>Versão 0.8.16 (Versão Prévia)
8/21/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>Baixar o Gerenciador de Armazenamento do Azure 0.8.16 (Versão Prévia)
- [Gerenciador de Armazenamento do Azure 0.8.16 (Versão Prévia) para Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Gerenciador de Armazenamento do Azure 0.8.16 (Versão Prévia) para Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Gerenciador de Armazenamento do Azure 0.8.16 (Versão Prévia) para Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>Novo
* Quando você abre um blob, Gerenciador de armazenamento solicitará que você tooupload Olá baixado arquivos se uma mudança for detectada
* Experiência de aprimorada de conexão no Azure Stack
* Desempenho aprimorado de saudação do upload/download de muitas empresas de pequeno arquivos no hello mesmo tempo


### <a name="fixes"></a>Correções
* Para alguns tipos de blob, escolher "substituir" muito durante um conflito de carregamento, às vezes, resultaria em carregamento hello está sendo reiniciado. 
* Na versão 0.8.15, os uploads às vezes paralisavam em 99%.
* Ao carregar o compartilhamento de arquivos de tooa de arquivos, se você escolher o diretório de tooa tooupload que ainda não existe, o carregamento falhará.
* O Gerenciador de Armazenamento estava gerando incorretamente os carimbos de data/hora para assinaturas de acesso compartilhadas e consultas de tabela.


Problemas conhecidos
* Usar uma cadeia de conexão de nome e chave não funciona atualmente. Ele será corrigido na próxima versão do hello. Até lá, você pode usar anexar com o nome e chave.
* Se você tentar tooopen um arquivo com um nome de arquivo inválido do Windows, o download Olá resultará em um arquivo não encontrado o erro.
* Depois de clicar em "Cancelar" em uma tarefa, pode demorar um pouco para toocancel essa tarefa. Essa é uma limitação da biblioteca de nó de armazenamento do Azure hello.
* Depois de concluir o carregamento de um blob, guia Olá que iniciou o carregamento de saudação é atualizado. Isso é uma alteração de comportamento anterior e também causará toobe novamente executada toohello raiz do contêiner Olá em que estão.
* Se você escolher Olá certificado incorreto do PIN/cartão inteligente, em seguida, você precisará toorestart em ordem toohave Gerenciador de armazenamento, esquecer essa decisão.
* Painel de configurações de conta Olá pode mostrar que você precisa de assinaturas de toofilter tooreenter credenciais.
* Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos. Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação.
* Embora o Azure Stack não dê suporte no momento a Compartilhamentos de Arquivos, um nó de Compartilhamentos de Arquivos ainda aparece em uma conta de armazenamento do Azure Stack anexada.
* Para usuários no Ubuntu 14.04, será necessário tooensure GCC está ativo toodate – isso pode ser feito executando Olá comandos a seguir e, em seguida, reinicie seu computador:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Para usuários no Ubuntu 17.04, será necessário tooinstall GConf - isso pode ser feito executando Olá comandos a seguir e, em seguida, reinicie seu computador:

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>Versão 0.8.14 (Visualização)
06/22/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>Baixar o Gerenciador de Armazenamento do Azure 0.8.14 (Visualização)
* [Baixar o Gerenciador de Armazenamento do Azure 0.8.14 (Visualização) para Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Baixar o Gerenciador de Armazenamento do Azure 0.8.14 (Visualização) para Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Baixar o Gerenciador de Armazenamento do Azure 0.8.14 (Visualização) para Linux](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>Novo

* Too1.7.2 de versão elétrons atualizado em vantagem de tootake de ordem de várias atualizações críticas de segurança
* Você agora pode acessar rapidamente o guia de solução de problemas online Olá no menu de ajuda Olá
* [Guia][2] de solução de problemas do Gerenciador de Armazenamento
* [Instruções] [ 3] sobre conexão de assinatura do Azure pilha tooan

### <a name="known-issues"></a>Problemas conhecidos

* Botões da caixa de diálogo de confirmação do hello excluir pasta não se registrar com hello cliques do mouse no Linux. Solução alternativa é a chave do toouse Olá Enter
* Se você escolher Olá certificado PIN/cartão inteligente errado, será necessário toorestart em ordem toohave Gerenciador de armazenamento se esqueça de decisão Olá
* Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros
* Painel de configurações de conta Olá pode mostrar que você precisa ter credenciais de tooreenter em assinaturas de toofilter ordem
* Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos. Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação.
* Embora o Azure Stack não dê suporte no momento a Compartilhamentos de Arquivos, um nó de Compartilhamentos de Arquivos ainda aparece em uma conta de armazenamento do Azure Stack anexada. 
* Ubuntu 14.04 instalação necessidades gcc versão atualizada ou atualizado – tooupgrade etapas estão abaixo:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>Versões anteriores

* [Versão 0.8.13](#version-0813)
* [Versão 0.8.12 / 0.8.11 / 0.8.10](#version-0812--0811--0810)
* [Versão 0.8.9 / 0.8.8](#version-089--088)
* [Versão 0.8.7](#version-087)
* [Versão 0.8.6](#version-086)
* [Versão 0.8.5](#version-085)
* [Versão 0.8.4](#version-084)
* [Versão 0.8.3](#version-083)
* [Versão 0.8.2](#version-082)
* [Versão 0.8.0](#version-080)
* [Versão 0.7.20160509.0](#version-07201605090)
* [Versão 0.7.20160325.0](#version-07201603250)
* [Versão 0.7.20160129.1](#version-07201601291)
* [Versão 0.7.20160105.0](#version-07201601050)
* [Versão 0.7.20151116.0](#version-07201511160)


### <a name="version-0813"></a>Versão 0.8.13
05/12/2017

#### <a name="new"></a>Novo

* [Guia][2] de solução de problemas do Gerenciador de Armazenamento
* [Instruções] [ 3] sobre conexão de assinatura do Azure pilha tooan

#### <a name="fixes"></a>Correções

* Corrigido: o carregamento do arquivo tinha uma chance maior de causar um erro de falta de memória
* Corrigido: agora você pode entrar com PIN/Cartão inteligente
* Corrigido: a opção Abrir no Portal agora funciona com o Azure China, Azure Alemanha, Azure US Government e Azure Stack
* Correção: Durante o carregamento de um contêiner de blob de tooa de pasta, um erro de "Operação ilegal" às vezes, ocorreria
* Corrigido: selecionar tudo foi desabilitado ao gerenciar instantâneos
* Correção: Olá metadados de blob de base Olá podem obter substituídos após exibir propriedades de saudação de seus instantâneos

#### <a name="known-issues"></a>Problemas conhecidos

* Se você escolher Olá certificado PIN/cartão inteligente errado, será necessário toorestart em ordem toohave Gerenciador de armazenamento se esqueça de decisão Olá
* Enquanto aumentados in ou out, nível de zoom Olá momentaneamente pode redefinir o nível padrão de toohello
* Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros
* Painel de configurações de conta Olá pode mostrar que você precisa ter credenciais de tooreenter em assinaturas de toofilter ordem
* Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos. Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação.
* Embora o Azure Stack não dê suporte no momento a Compartilhamentos de Arquivos, um nó de Compartilhamentos de Arquivos ainda aparece em uma conta de armazenamento do Azure Stack anexada. 
* Ubuntu 14.04 instalação necessidades gcc versão atualizada ou atualizado – tooupgrade etapas estão abaixo:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>Versão 0.8.12 / 0.8.11 / 0.8.10
04/07/2017

#### <a name="new"></a>Novo

* Gerenciador de armazenamento agora será fechada automaticamente quando você instala uma atualização de notificação de atualização de saudação
* O acesso rápido in-loco fornece uma experiência aprimorada para trabalhar com seus recursos acessados com frequência
* No editor de contêiner de Blob hello, agora você pode ver um blob concedido pertence à máquina virtual
* Agora você pode recolher painel do lado esquerdo de saudação
* Descoberta agora é executado no Olá a mesma hora como download
* Usar estatísticas no contêiner de Blob, o compartilhamento de arquivos e a tabela editores toosee Olá tamanho do recurso ou seleção de saudação
* Você pode agora entrar tooAzure AAD (Active Directory) com base em contas de pilha do Azure. 
* Você pode agora carregar arquivos em 32 MB as contas de armazenamento tooPremium
* Suporte a acessibilidade aprimorado
* Agora você pode adicionar confiável Base 64 codificados certificados x. 509 SSL pelo vai tooEdit -&gt; certificados SSL -&gt; importar certificados

#### <a name="fixes"></a>Correções

* Correção: depois de atualizar as credenciais da conta, modo de exibição de árvore de saudação seria, às vezes, não atualizar automaticamente
* Corrigido: a geração de um SAS para tabelas e filas do emulador poderia resultar em uma URL inválida
* Corrigido: agora, as contas de armazenamento Premium podem ser expandidas enquanto um proxy está habilitado
* Correção: Olá botão Aplicar em contas Olá página de gerenciamento não funcionará se você tivesse 1 ou 0 contas selecionadas
* Corrigido: o carregamento de blobs que exigem resoluções de conflitos pode falhar – corrigido no 0.8.11 
* Corrigido: o envio de comentários foi interrompido no 0.8.11 – corrigido no 0.8.12 

#### <a name="known-issues"></a>Problemas conhecidos

* Após a atualização too0.8.10, será necessário toorefresh todas as suas credenciais.
* Enquanto aumentados in ou out, nível de zoom Olá momentaneamente pode redefinir o nível padrão de toohello.
* Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros.
* Painel de configurações de conta Olá pode mostrar que você precisa ter credenciais de tooreenter em assinaturas de toofilter de ordem.
* Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos. Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação.
* Embora o Azure Stack não dê suporte no momento a Compartilhamentos de Arquivos, um nó de Compartilhamentos de Arquivos ainda aparece em uma conta de armazenamento do Azure Stack anexada. 
* Ubuntu 14.04 instalação necessidades gcc versão atualizada ou atualizado – tooupgrade etapas estão abaixo:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>Versão 0.8.9 / 0.8.8
02/23/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Novo

* O Gerenciador de armazenamento 0.8.9 baixará automaticamente a versão mais recente Olá para atualizações.
* Hotfix: usando um portal gerado URI SAS tooattach que uma conta de armazenamento pode resultar em um erro.
* Agora você pode criar, gerenciar e promover os instantâneos de blob.
* Agora você pode entrar em contas da China, o Azure Alemanha e o Azure US Government tooAzure.
* Agora você pode alterar o nível de zoom de saudação. Use as opções de Olá Olá Exibir menu tooZoom no zoom e redefinição de Zoom.
* Agora há suporte para caracteres Unicode nos metadados do usuário para blobs e arquivos.
* Aprimoramentos de acessibilidade.
* Notas de versão do Hello próxima versão podem ser exibidas de notificação de atualização de saudação. Você também pode exibir as notas de versão atuais Olá no menu de ajuda de saudação.

#### <a name="fixes"></a>Correções

* Correção: o número de versão Olá é agora exibido corretamente no painel de controle no Windows
* Foram corrigidos: pesquisa não está mais limitado too50, nós 000
* Correção: compartilhamento de arquivos do carregamento tooa girado para sempre se o diretório de destino Olá ainda não existia
* Corrigido: mais estabilidade para downloads e uploads longos

#### <a name="known-issues"></a>Problemas conhecidos

* Enquanto aumentados in ou out, nível de zoom Olá momentaneamente pode redefinir o nível padrão de toohello.
* O Acesso Rápido só funciona com itens baseados em assinatura. Recursos locais ou conectados por meio de chave ou o token SAS de recursos não têm suporte nesta versão.
* Acesso rápido pode levar alguns segundos toonavigate toohello recurso de destino, dependendo de quantos recursos que você tem.
* Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros.

12/16/2016
### <a name="version-087"></a>Versão 0.8.7

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Novo

* Você pode escolher como conflitos tooresolve no início de saudação de uma atualização, baixar ou copiar a sessão na janela de atividades de saudação
* Passe o mouse sobre um caminho guia toosee Olá completo saudação do recurso de armazenamento
* Quando você clica em uma guia, sincronizar com seu local no painel de navegação do lado esquerdo de saudação

#### <a name="fixes"></a>Correções

* Corrigido: agora, o Gerenciador de Armazenamento é um aplicativo confiável no Mac
* Corrigido: o Ubuntu 14.04 tem suporte novamente
* Correção: Às vezes Olá adicionar conta pisca de interface do usuário durante o carregamento de assinaturas
* Correção: Às vezes, nem todos os recursos de armazenamento foram listados no painel de navegação do lado esquerdo de saudação
* Correção: Olá ação painel, às vezes, exibido ações vazias
* Correção: tamanho da janela Olá da sessão Olá fechado pela última vez é agora retido
* Correção: Você pode abrir várias guias para Olá mesmo recurso usando o menu de contexto de saudação

#### <a name="known-issues"></a>Problemas conhecidos

* O Acesso Rápido só funciona com itens baseados em assinatura. Recursos locais ou conectados por meio de chave ou o token SAS de recursos não têm suporte nesta versão
* Acesso rápido pode levar alguns segundos toonavigate toohello recurso de destino, dependendo de quantos recursos
* Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros
* Identificadores de pesquisa pesquisar em nós aproximadamente 50.000 – depois disso, o desempenho pode ser afetado ou pode causar exceções sem tratamento
* Para Olá pela primeira vez usando Olá Gerenciador de armazenamento em macOS, você verá vários prompts pedindo o conjunto de chaves de tooaccess de permissão do usuário. Sugerimos que você selecionar sempre permitir modo prompt Olá não mostra novamente

11/18/2016
### <a name="version-086"></a>Versão 0.8.6

#### <a name="new"></a>Novo

* Você pode agora fixar usados com mais frequência serviços toohello acesso rápido para facilitar a navegação
* Agora você pode abrir vários editores em guias diferentes. Clique tooopen uma guia temporária; Clique duas vezes em tooopen uma guia permanente. Você também pode clicar em Olá guia temporário toomake-uma guia permanente
* Fizemos aperfeiçoamentos de desempenho e estabilidade para carregamentos e downloads, especialmente para grandes arquivos em máquinas rápidas
* Pastas "virtuais" vazias agora podem ser criadas em contêineres de blob
* Introduzimos novamente a pesquisa com escopo com nossa nova pesquisa avançada de subcadeia de caracteres, e agora você tem duas opções de pesquisa: 
    * Global pesquisa - insira apenas um termo de pesquisa na caixa de texto de pesquisa de saudação
    * Pesquisa com escopo definido - clique Olá Lupa ícone próximo tooa nó, em seguida, adicionar um final de toohello do termo de pesquisa do caminho de hello, ou com o botão direito e selecione "Pesquisa de aqui"
* Adicionamos vários temas: luz (padrão), escuro, preto em alto contraste e branco em alto contraste. Vá tooEdit -&gt; toochange temas sua preferência de temas
* Você pode modificar as propriedades do Blob e do arquivo
* Agora, damos suporte mensagens em fila codificadas (base64) e não codificadas
* No Linux, um sistema operacional de 64 bits agora é necessário. Para esta versão, só há suporte para Ubuntu 16.04.1 LTS de 64 bits
* Atualizamos nosso logotipo!

#### <a name="fixes"></a>Correções

* Corrigido: Tela problemas congelamento
* Corrigido: Segurança aprimorada
* Corrigido: às vezes, contas anexadas duplicadas apareciam
* Corrigido: um blob com um tipo de conteúdo indefinido pode gerar uma exceção
* Correção: Olá abrindo o painel de consulta em uma tabela vazia não foi possível
* Corrigido: vários bugs na Pesquisa
* Correção: Maior número de saudação de recursos carregados do too100 50 quando clicar em "Mais carga"
* Corrigido: agora, na primeira execução, se uma conta for conectada, selecionamos todas as assinaturas para essa conta por padrão 

#### <a name="known-issues"></a>Problemas conhecidos

* Esta versão do hello Gerenciador de armazenamento não é executado no Ubuntu 14.04
* tooopen várias guias para Olá mesmo recurso, não é continuamente clique em Olá mesmo recurso. Clique em outro recurso e, em seguida, volte e clique no hello original recurso tooopen-lo novamente em outra guia 
* O Acesso Rápido só funciona com itens baseados em assinatura. Recursos locais ou conectados por meio de chave ou o token SAS de recursos não têm suporte nesta versão
* Acesso rápido pode levar alguns segundos toonavigate toohello recurso de destino, dependendo de quantos recursos
* Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros
* Identificadores de pesquisa pesquisar em nós aproximadamente 50.000 – depois disso, o desempenho pode ser afetado ou pode causar exceções sem tratamento

10/03/2016
### <a name="version-085"></a>Versão 0.8.5

#### <a name="new"></a>Novo

* Pode agora usar SAS gerado pelo Portal chaves tooattach tooStorage contas e recursos

#### <a name="fixes"></a>Correções

* Foram corrigidos: condição de corrida durante a pesquisa às vezes causado nós toobecome não expansível
* Correção: "Usar HTTP" não funciona ao conectar-se tooStorage contas com chave e o nome da conta
* Corrigido: chaves SAS (especialmente as geradas pelo Portal) retornam um erro de "barra à direita"
* Corrigido: problemas de importação de tabela
    * Às vezes, a chave de partição e chave de linha eram invertidas
    * Não é possível tooread "null" chaves de partição

#### <a name="known-issues"></a>Problemas conhecidos

* Identificadores de pesquisa pesquisar em nós aproximadamente 50.000 – depois disso, o desempenho pode ser afetado
* Pilha do Azure atualmente não oferece suporte a arquivos, para que tentar tooexpand arquivos mostrará um erro

09/12/2016
### <a name="version-084"></a>Versão 0.8.4

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Novo

* Gerar contas de toostorage links diretos, contêineres, filas, tabelas ou compartilhamentos de arquivos para compartilhamento e fácil acessam os recursos de tooyour - Windows e o suporte do Mac OS
* Pesquisar para contêineres de blob, tabelas, filas, compartilhamentos de arquivos ou contas de armazenamento de caixa de pesquisa Olá
* Agora você pode agrupar cláusulas no construtor de consultas de tabela Olá
* Renomear e copiar/colar contêineres de blob, compartilhamentos de arquivos, tabelas, blobs, pastas de blob, arquivos e diretórios de contas e contêineres anexadas a SAS
* Agora, ao renomear e copiar contêineres de blob e compartilhamentos de arquivos, as propriedades e metadados são preservados

#### <a name="fixes"></a>Correções

* Corrigido: não é possível editar entidades de tabela se elas contiverem propriedades boolianas ou binárias

#### <a name="known-issues"></a>Problemas conhecidos

* Identificadores de pesquisa pesquisar em nós aproximadamente 50.000 – depois disso, o desempenho pode ser afetado

08/03/2016
### <a name="version-083"></a>Versão 0.8.3

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Novo

* Renomear os contêineres, tabelas, compartilhamentos de arquivos
* Experiência aprimorada do Construtor de consulta
* Consultas de toosave e carga de capacidade
* Direcionar links toostorage contas ou contêineres, filas, tabelas ou arquivos compartilhados para compartilhar e acessar facilmente os recursos (somente Windows - macOS suporte em breve!)
* Capacidade toomanage e configure as regras CORS

#### <a name="fixes"></a>Correções

* Corrigido: as Contas da Microsoft exigem reautenticação a cada 8 a 12 horas

#### <a name="known-issues"></a>Problemas conhecidos

* Às vezes, hello interface do usuário pode parecer congelada - maximizando a janela Olá ajuda a resolver esse problema
* A instalação do macOS pode exigir permissões elevadas
* Painel de configurações de conta pode mostrar que você precisa ter credenciais de tooreenter em assinaturas de toofilter ordem
* Renomeação de compartilhamentos de arquivos, contêineres de blob e tabelas não preserva metadados ou outras propriedades no contêiner de saudação, como a cota de compartilhamento de arquivo, o nível de acesso público ou políticas de acesso
* Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos. Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação
* A cópia ou a renomeação de recursos não funciona em contas anexadas a SAS

07/07/2016
### <a name="version-082"></a>Versão 0.8.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Novo

* As Contas de Armazenamento são agrupadas por assinaturas; armazenamento de desenvolvimento e recursos anexados via chave ou SAS são mostrados sob o nó (Local e Anexado)
* Saia das contas no painel "Configurações de Conta do Azure"
* Configurar tooenable de configurações de proxy e gerenciar entrar
* Criar e quebrar concessões de blob
* Abrir contêineres de blob, filas, tabelas e arquivos com um único clique

#### <a name="fixes"></a>Correções

* Corrigido: mensagens em fila inseridas com bibliotecas .NET ou Java não são corretamente decodificadas com base64
* Corrigido: tabelas $metrics não são exibidas para contas de Armazenamento de Blobs
* Corrigido: o nó tabelas não funciona para o armazenamento local (Desenvolvimento)

#### <a name="known-issues"></a>Problemas conhecidos

* A instalação do macOS pode exigir permissões elevadas

06/15/2016
### <a name="version-080"></a>Versão 0.8.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Novo

* Suporte para compartilhamento de arquivos: exibição, upload, download, cópia de arquivos e diretórios, URIs SAS (criar e conectar)
* Melhor experiência do usuário para conectar-se tooStorage com URIs de SAS ou chaves de conta
* Exportar resultados da consulta de tabela
* Personalização e reordenação da coluna Tabela
* Exibição de contêineres de blob $logs e tabelas $metrics para Contas de Armazenamento com métricas habilitadas
* Comportamento de exportação e importação aprimorado, agora inclui o tipo de valor da propriedade

#### <a name="fixes"></a>Correções

* Corrigido: o upload ou download de blobs grandes pode resultar em uploads/downloads incompletos
* Correção: a edição, adicionando ou importando uma entidade com um valor de cadeia de caracteres numéricos ("1") converterá toodouble
* Correção: Nó de tabela Olá tooexpand não é possível no ambiente de desenvolvimento local Olá

#### <a name="known-issues"></a>Problemas conhecidos

* As tabelas $metrics não são visíveis para contas de Armazenamento de Blobs
* Adicionado por meio de programação de fila de mensagens não pode ser exibida corretamente se mensagens de saudação são codificadas usando a codificação Base64

05/17/2016
### <a name="version-07201605090"></a>Versão 0.7.20160509.0

#### <a name="new"></a>Novo

* Melhor tratamento de erros para falhas de aplicativo

#### <a name="fixes"></a>Correções

* Correção de bug no qual as mensagens da Barra de Informações às vezes não apareciam quando as credenciais de entrada eram exigidas

#### <a name="known-issues"></a>Problemas conhecidos

* Tabelas: Adicionando, editando, ou importar uma entidade que tem uma propriedade com um valor numérico de maneira ambígua, como "1" ou "1.0", e Olá toosend de tentativas de usuário como um `Edm.String`, valor Olá voltará por meio do cliente Olá API como um EDM

03/31/2016

### <a name="version-07201603250"></a>Versão 0.7.20160325.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Novo

* Suporte à tabela: exibição, consulta, exportação, importação e operações CRUD para entidades
* Suporte à fila: exibição, adição, remoção de mensagens da fila
* Gerar URIs SAS para Contas de Armazenamento
* Conectando tooStorage contas com URIs de SAS
* Atualize notificações para atualizações futuras tooStorage Explorer
* Aparência atualizada

#### <a name="fixes"></a>Correções

* Aprimoramento de desempenho e confiabilidade

### <a name="known-issues-amp-mitigations"></a>Problemas &amp; mitigações conhecidos

* O download de arquivos de blob grandes não funciona corretamente – recomendamos usar AzCopy enquanto resolvemos esse problema 
* As credenciais de conta não serão recuperadas nem armazenadas em cache se a pasta base Olá não foi encontrada ou não pode ser gravada
* Se estamos adicionando, editando ou importando uma entidade que tem uma propriedade com um valor numérico de maneira ambígua, como "1" ou "1.0", e o usuário Olá tenta toosend-lo como um `Edm.String`, valor Olá voltará por meio do cliente Olá API como um EDM
* Ao importar arquivos CSV com registros de várias linhas, os dados de saudação podem obter embaralhados ou embaralhados

02/03/2016

### <a name="version-07201601291"></a>Versão 0.7.20160129.1

#### <a name="fixes"></a>Correções

* Desempenho geral aprimorado ao carregar, baixar e copiar blobs

01/14/2016

### <a name="version-07201601050"></a>Versão 0.7.20160105.0

#### <a name="new"></a>Novo

* Suporte a Linux (paridade recursos tooOSX)
* Adicionar contêineres de blob com chave SAS (Assinaturas de Acesso Compartilhado)
* Adicionar Contas de Armazenamento para o Azure China
* Adicionar Contas de Armazenamento com pontos de extremidade personalizados
* Abrir e exibir os blobs de texto e imagem de conteúdo Olá
* Exibir e editar propriedades e metadados de blob

#### <a name="fixes"></a>Correções

* Foram corrigidos: carregar ou baixar um grande número de blobs (500) pode às vezes causar Olá aplicativo toohave uma tela em branca 
* Correção: ao definir o nível de acesso público de contêiner de blob, Olá novo valor não é atualizado até que você defina o foco Olá no contêiner Olá novamente. Além disso, caixa de diálogo Olá sempre padroniza muito "não acessar nenhum public" e não Olá atual valor real.
* Suporte geral aprimorado de teclado/acessibilidade e interface do usuário
* A disposição do texto do histórico de trilha quebra automaticamente quando o texto é longo com espaços em branco
* A caixa de diálogo SAS dá suporte à validação de entrada
* Armazenamento local continua toobe disponível mesmo se as credenciais do usuário tem expirado
* Quando um contêiner de blob aberto é excluído, explorer de blob Olá Olá direita é fechado

#### <a name="known-issues"></a>Problemas conhecidos

* Necessidades de instalação Linux gcc versão atualizada ou atualizado – tooupgrade etapas estão abaixo: 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

11/18/2015
### <a name="version-07201511160"></a>Versão 0.7.20151116.0

#### <a name="new"></a>Novo

* Versões para macOS e Windows
* Entrar tooview suas contas de armazenamento – use sua conta institucional Microsoft Account, 2FA, etc.
* Armazenamento de desenvolvimento local (use o emulador de armazenamento, somente para Windows)
* Suporte ao Azure Resource Manager e ao recurso Clássico
* Criar e excluir blobs, filas ou tabelas
* Procurar blobs, filas ou tabelas específicas
* Explore o conteúdo de saudação de contêineres de blob
* Exibir e navegar pelos diretórios
* Carregar, baixar e excluir blobs e pastas
* Exibir e editar propriedades e metadados de blob
* Gerar as chaves SAS
* Gerenciar e criar SAP (Políticas de Acesso armazenado)
* Procure blobs pelo prefixo
* Arraste ' drop n tooupload de arquivos ou de download

#### <a name="known-issues"></a>Problemas conhecidos

* Ao definir o nível de acesso público de contêiner de blob, valor novo Olá não é atualizado até que você defina o foco Olá no contêiner Olá novamente
* Quando você abre o nível de acesso público do hello diálogo tooset Olá, ele sempre não mostra "Nenhum acesso público" como Olá, valor padrão e não Olá real atual
* Não é possível renomear blobs baixados
* Estado de entradas de log de atividade será às vezes "preso" em uma em andamento quando ocorre um erro e erro Olá não é exibido
* Às vezes, falhas ou ativa completamente durante a tentativa de tooupload em branco ou baixar um grande número de blobs
* Às vezes, cancelar uma operação de cópia não funciona
* Durante a criação de um contêiner (tabela/fila/blob), se um nome inválido de entrada e continuar toocreate outro em um tipo de contêiner diferentes você não pode definir foco no novo tipo de saudação
* Não é possível criar uma nova pasta ou renomear a pasta




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md