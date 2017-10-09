---
title: "aaaMicrosoft Azure Storage Explorer 0.8.7 (visualização) | Microsoft Docs"
description: "Notas de versão do Microsoft Azure Storage Explorer 0.8.7 (visualização)"
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
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Gerenciador de Armazenamento do Microsoft Azure 0.8.7 (Visualização)
## <a name="overview"></a>Visão geral
Este artigo contém as notas de versão de saudação para a versão de visualização do Azure Storage Explorer 0.8.7.

[Gerenciador de armazenamento do Microsoft Azure (visualização)](./vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Linux, Windows e macOS.

## <a name="azure-storage-explorer-087-preview"></a>Gerenciador de Armazenamento do Azure 0.8.7 (Visualização)
### <a name="download-azure-storage-explorer-087-preview"></a>Baixar o Gerenciador de Armazenamento do Azure 0.8.7 (Visualização)
- [Armazenamento do Azure Explorer 0.8.7 Preview para Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Gerenciador de Armazenamento do Azure 0.8.7 Visualização para Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Visualização de 0.8.7 do Gerenciador de armazenamento do Azure para Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>Novas atualizações
* Você pode escolher como conflitos tooresolve no início de saudação de uma atualização, baixar ou copiar sessão Olá **atividades** janela.
* Passe o mouse sobre um caminho guia toosee Olá completo saudação do recurso de armazenamento.
* Quando você clica em uma guia, sincronizar com seu local no painel de navegação do lado esquerdo de saudação.

### <a name="fixes"></a>Correções
* Fixo: Storage Explorer agora é um aplicativo confiável no macOS.
* Fixo: Ubuntu 14.04 novamente é suportado.
* Correção: Às vezes hello adicionar interface do usuário da conta pisca ao carregar as assinaturas.
* Correção: Às vezes, nem todos os recursos de armazenamento foram listados no painel de navegação do lado esquerdo da saudação.
* Correção: painel de ação de saudação exibido, às vezes, ações vazias.
* Correção: tamanho da janela Olá Olá fechado pela última vez sessão agora é mantido.
* Correção: Você pode abrir várias guias para Olá mesmo recurso usando o menu de contexto de saudação.

### <a name="known-issues"></a>Problemas conhecidos
* Acesso rápido só funciona com itens baseados em assinatura. Recursos locais ou conectados por meio de chave ou o token SAS de recursos não têm suporte nesta versão.
* Acesso rápido pode levar alguns segundos toonavigate toohello recurso de destino, dependendo de quantos recursos que você tem.
* Ter mais de três grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros.
* Identificadores de pesquisa pesquisar em nós aproximadamente 50.000 - depois disso, o desempenho pode ser afetado ou pode causar exceções sem tratamento.
* Para Olá pela primeira vez usando Olá Gerenciador de armazenamento em macOS, você verá vários prompts solicitando o conjunto de chaves do usuário permissão tooaccess hello. Sugerimos que você selecionar **sempre permitir** para prompt Olá não mostrar novamente

## <a name="previous-releases"></a>Versões anteriores
### <a name="features"></a>Recursos
#### <a name="main-features"></a>Principais recursos
* macOS, Linux e versões do Windows
* Entrar tooview suas contas de armazenamento agrupados por assinatura:
    * Use sua conta Org Account da Microsoft, 2FA, etc.
    * Configurar e gerenciar configurações de proxy
    * Remover contas ao sair
* Conecte-se tooStorage contas usando:
    * Nome e chave da conta
    * Pontos de extremidade personalizados (incluindo o Azure China)
    * URI SAS para contas de armazenamento
* Suporte ao Azure Resource Manager e ao Armazenamento Clássico
* Gerar chaves SAS para contêineres de blob, blobs, filas, tabelas ou compartilhamentos de arquivos
* Conectar contêineres tooblob, filas, tabelas ou compartilhamentos de arquivos com a chave de assinaturas de acesso compartilhado (SAS)
* Gerenciar políticas de acesso armazenado para contêineres de blob, filas, tabelas ou compartilhamentos de arquivos
* Armazenamento de desenvolvimento local com o emulador de armazenamento (somente Windows)
* Criar e excluir tabelas, filas ou contêineres de blob
* Exibição $logs contêineres de blob e tabelas de $metrics
* Procurar específicos blobs, filas, tabelas ou compartilhamentos de arquivos
* Contas de toostorage links diretos ou contêineres, filas, tabelas ou compartilhamentos de arquivos para compartilhar e acessar facilmente seus recursos
* Renomear os contêineres de blob, tabelas, compartilhamentos de arquivos
* Capacidade toomanage e configure as regras CORS
* Copiar facilmente as chaves primária e secundária para contas de armazenamento
* Verificações de MD5 no carregamento e download de integridade de dados e consistência
* Pesquisar para contêineres de blob, tabelas, filas, compartilhamentos de arquivos ou contas de armazenamento de caixa de pesquisa Olá
* Você pode agora fixar usados com mais frequência serviços toohello acesso rápido para facilitar a navegação
* Agora você pode abrir vários editores em guias diferentes. Clique tooopen uma guia temporária; Clique duas vezes tooopen uma guia permanente. Você também pode clicar em Olá guia temporário toomake-uma guia permanente
* Aperfeiçoamentos de desempenho e estabilidade para carregamentos e downloads, especialmente para grandes arquivos em máquinas rápidas
* Podemos reintrodução à pesquisa com escopo definido aprimorada de saudação e o conceito de saudação adicional de escopo. Insira o nó de tooa Olá caminho por meio do ícone de hover hello, clique à direita -> "Pesquisa de aqui", ou manualmente tooscope nesse nó. Depois que o escopo, você pode adicionar um final de toohello do termo de pesquisa de pesquisa de toodeep de caminho hello a partir do nó
* Adicionamos vários temas: luz (padrão), escuro, preto em alto contraste e branco em alto contraste.
* Vá tooEdit -> temas toochange sua preferência de temas
* No Linux, um sistema operacional de 64 bits agora é necessário
* Atualizamos nosso logotipo!
#### <a name="blobs"></a>Blobs
* Exibir blobs e navegar pelos diretórios
* Carregar, baixar, excluir e copiar blobs e pastas
* Abrir e exibir os blobs de texto e imagem de conteúdo Olá
* Exibir e editar propriedades e metadados de blob
* Procure blobs pelo prefixo
* Criar e quebrar concessões para blobs e contêineres de blob
* Arraste ' n Descartar tooupload de arquivos
* Renomear pastas e blobs
* Pastas "virtuais" vazias agora podem ser criadas em contêineres de blob
* Você pode modificar propriedades de Blob e arquivo hello
#### <a name="tables"></a>Tabelas
* Exibir e consultar entidades com o ODATA ou usar consultas complexas de toocreate de construtor de consulta
* Adicionar, editar e excluir entidades
* Importar e exportar o conteúdo da tabela no formato CSV (inclusive exportar resultados de consulta)
* Personalizar a ordem das colunas
* Consultas de toosave de capacidade
#### <a name="queues"></a>Filas
* Inspecionar 32 mensagens mais recentes
* Adicionar, remover, exibir mensagens
* Limpar fila
* Podemos tornam possível que você toodecide se deseja tooencode/decodificar a fila de mensagens
#### <a name="file-shares"></a>Compartilhamentos de arquivos
* Exibir arquivos e navegue pelos diretórios
* Carregar, baixar, excluir e copiar arquivos e diretórios
* Exibir propriedades de arquivo
* Renomear arquivos e diretórios

### <a name="bug-fixes"></a>Correções de bug
* Corrigido: Tela problemas congelamento
* Corrigido: Segurança aprimorada

### <a name="known-issues"></a>Problemas conhecidos
* Pesquisa alças pesquisar em nós aproximadamente 50.000 - depois disso, o desempenho pode ser afetados macOS instalação pode exigir permissões elevadas
* Painel de configurações de conta pode mostrar que você precisa de assinaturas de toofilter credenciais tooreenter
* Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos. Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação
* Pilha do Azure não tem suporte a arquivos, portante, tentar Olá tooexpand **arquivos** nó resulta em erro
* Instalação do Linux 14.04 precisa gcc versão atualizada ou atualizado. Olá etapas a seguir ilustram como tooupgrade:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>Versões anteriores
#### <a name="october-2016-release-version-085"></a>De 2016 de outubro (versão 0.8.5)
* [Baixar para Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Baixar para Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Baixar para Linux](https://go.microsoft.com/fwlink/?LinkId=809308)
