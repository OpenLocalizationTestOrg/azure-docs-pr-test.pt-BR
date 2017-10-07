---
title: "aaaOverview de controle de acesso no repositório Data Lake | Microsoft Docs"
description: Compreenda como o controle de acesso funciona no Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a>Controle de acesso no Azure Data Lake Store

Repositório Azure Data Lake implementa um modelo de controle de acesso que deriva de HDFS, que por sua vez deriva de modelo de controle de acesso do hello POSIX. Este artigo resume Noções básicas de saudação do modelo de controle de acesso de saudação para repositório Data Lake. toolearn mais sobre o modelo de controle de acesso HDFS hello, consulte [HDFS permissões guia](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).

## <a name="access-control-lists-on-files-and-folders"></a>Listas de controle de acesso em arquivos e pastas

Há dois tipos de listas de controle de acesso (ACLs), **ACLs de Acesso** e **ACLs Padrão**.

* **Acessar ACLs**: estes objetos de tooan de acesso de controle. Os arquivos e as pastas têm ACLs de Acesso.

* **Padrão de ACLs**: um "modelo" de ACLs associado com uma pasta que determinam a saudação ACLs de acesso para todos os itens filho que são criados nessa pasta. Os Arquivos não têm ACLs Padrão.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

ACLs de acesso e ACLs padrão têm Olá mesma estrutura.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> Olá alteração ACL padrão em um pai não afeta Olá acesso ACL ou a ACL padrão de itens filho que já existem.
>
>

## <a name="users-and-identities"></a>Usuários e identidades

Todos os arquivos e pastas têm permissões diferentes para estas identidades:

* saudação de usuário do arquivo hello proprietário
* grupo proprietário Olá
* Usuários nomeados
* Grupos nomeados
* Todos os outros usuários

identidades de saudação de usuários e grupos são identidades do Active Directory do Azure (AD do Azure). Portanto, pode ser um "usuário," no contexto de saudação do repositório Data Lake, a menos que indicado o contrário, o significa que um usuário do AD do Azure ou um grupo de segurança do AD do Azure.

## <a name="permissions"></a>Permissões

Olá permissões em um objeto do sistema de arquivos são **leitura**, **gravar**, e **Execute**, e eles podem ser usados em arquivos e pastas, conforme mostrado no Olá a tabela a seguir:

|            |    Arquivo     |   Pasta |
|------------|-------------|----------|
| **Ler (R)** | Pode ler o conteúdo de saudação de um arquivo | Requer **leitura** e **Execute** conteúdo de saudação do toolist da pasta de saudação|
| **Gravar (W)** | Pode escrever ou anexar o arquivo tooa | Requer **gravar** e **Execute** toocreate itens de filho em uma pasta |
| **Executar (X)** | Não significa nada no contexto de saudação do repositório Data Lake | Tootraverse necessário Olá filho itens de uma pasta |

### <a name="short-forms-for-permissions"></a>Formatos abreviados para permissões

**RWX** é usado tooindicate **leitura + escrita + executar**. Um formato numérico mais compacta existe no qual **leitura = 4**, **gravar = 2**, e **Execute = 1**, Olá cuja soma representa as permissões de saudação. Estes são alguns exemplos:

| Formato numérico | Formato curto |      O que significa     |
|--------------|------------|------------------------|
| 7            | RWX        | Ler + Gravar + Executar |
| 5            | R-X        | Ler + Executar         |
| 4            | R--        | Ler                   |
| 0            | ---        | Nenhuma permissão         |


### <a name="permissions-do-not-inherit"></a>Não herdam permissões

No modelo de estilo POSIX Olá que é usado pelo repositório Data Lake, permissões para um item são armazenadas no próprio item hello. Em outras palavras, as permissões para um item não podem ser herdadas Olá itens de pai.

## <a name="common-scenarios-related-toopermissions"></a>Toopermissions relacionados de cenários comuns

Estes são alguns toohelp cenários comuns entender quais permissões são necessárias tooperform determinadas operações em uma conta do repositório Data Lake.

### <a name="permissions-needed-tooread-a-file"></a>Permissões necessárias tooread um arquivo

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* Para toobe de arquivo hello ler, Olá chamador necessidades **leitura** permissões.
* Para todos os hello pastas na estrutura de pastas de saudação que contêm o arquivo hello, Olá chamador necessidades **Execute** permissões.

### <a name="permissions-needed-tooappend-tooa-file"></a>Permissões necessárias tooappend tooa arquivo

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* Para toobe do arquivo hello anexados ao, Olá chamador necessidades **gravar** permissões.
* Para todos os hello pastas que contêm o arquivo hello, Olá chamador necessidades **Execute** permissões.

### <a name="permissions-needed-toodelete-a-file"></a>Permissões necessárias toodelete um arquivo

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* Para a pasta pai Olá Olá chamador necessidades **gravar + executar** permissões.
* Para todos os hello outras pastas no caminho do arquivo hello, Olá chamador necessidades **Execute** permissões.



> [!NOTE]
> Grave as permissões no arquivo hello não são necessária toodelete-desde Olá anteriores duas condições forem verdadeiras.
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a>Permissões necessárias tooenumerate uma pasta

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* Para Olá pasta tooenumerate, Olá chamador necessidades **leitura + Execute** permissões.
* Para todos os hello pastas ancestral, Olá chamador necessidades **Execute** permissões.

## <a name="viewing-permissions-in-hello-azure-portal"></a>Exibindo permissões no hello portal do Azure

De saudação **Data Explorer** folha de saudação conta do repositório Data Lake, clique em **acesso** toosee Olá ACLs para um arquivo ou pasta. Clique em **acesso** toosee Olá ACLs para Olá **catálogo** pasta sob Olá **mydatastore** conta.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

Esta folha, seção superior Olá mostra uma visão geral das permissões de saudação que você possui. (Na captura de tela hello, o usuário Olá é Bob.) Depois disso, as permissões de acesso de saudação são mostradas. Depois disso, da saudação **acesso** folha, clique em **exibição simples** toosee Olá exibição simples.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

Clique em **exibição avançada** toosee hello mais exibição avançada, onde os conceitos de saudação de ACLs padrão, a máscara e o superusuário são mostrados.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a>superusuário Olá

Um superusuário tem Olá a maioria dos direitos de todos os usuários Olá Olá repositório Data Lake. Um superusuário:

* Tem permissões de RWX muito**todos os** arquivos e pastas.
* Pode alterar permissões hello em qualquer arquivo ou pasta.
* Pode alterar Olá possui um usuário ou grupo de qualquer arquivo ou pasta proprietário.

No Azure, uma conta do Data Lake Store tem diversas funções do Azure, incluindo:

* Proprietários
* Colaboradores
* Leitores

Todos no hello **proprietários** função para uma conta do repositório Data Lake é automaticamente um superusuário para essa conta. mais, consulte toolearn [controle de acesso baseado em função](../active-directory/role-based-access-control-configure.md).
Se você quiser toocreate uma função de controle de acesso baseado em função (RBAC) personalizado que tenha permissões de superusuário, ele precisa Olá toohave as seguintes permissões:
- Microsoft.DataLakeStore/accounts/Superuser/action
- Microsoft.Authorization/roleAssignments/write


## <a name="hello-owning-user"></a>usuário proprietário Olá

usuário Olá que criou o item de saudação é automaticamente Olá usuário do item de saudação de proprietário. Um usuário proprietário pode:

* Alterar permissões de saudação de um arquivo que é de propriedade.
* Alterar Olá possui o grupo de um arquivo que é de propriedade, como usuário proprietário Olá também é um membro do grupo de destino hello.

> [!NOTE]
> Olá usuário proprietário *não é possível* alterar Olá possui um usuário de outro arquivo de propriedade. Somente super usuários podem alterar Olá possui um usuário de um arquivo ou pasta.
>
>

## <a name="hello-owning-group"></a>grupo proprietário Olá

Olá POSIX ACLs, cada usuário é associado um "grupo primário". Por exemplo, o usuário "alice" pode pertencer toohello grupo de "financeiro". Alice também pode pertencer a grupos de toomultiple, mas um grupo sempre é designado como o grupo primário. POSIX, quando Alice cria um arquivo, Olá possui o grupo de arquivo é definido grupo primário tooher, que nesse caso é "Finanças".

Quando um novo item do sistema de arquivos é criado, o repositório Data Lake atribui toohello um valor que possui o grupo.

* **Caso 1**: pasta raiz de hello "/". Essa pasta é criada quando uma conta do Data Lake Store é criada. Nesse caso, o grupo proprietário Olá é definido usuário toohello que criou a conta de saudação.
* **Caso 2** (qualquer outro caso): quando um novo item é criado, grupo proprietário Olá é copiado da pasta pai de saudação.

grupo proprietário Olá pode ser alterado por:
* Todos os superusuários.
* saudação do usuário, proprietário, se o usuário proprietário Olá também é um membro do grupo de destino de saudação.

## <a name="access-check-algorithm"></a>Algoritmo de verificação de acesso

Olá ilustração a seguir representa o algoritmo de verificação de acesso Olá para contas do repositório Data Lake.

![Algoritmo de ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a>Olá e máscara "permissões efetivas"

Olá **máscara** é um RWX valor que é usado toolimit acesso **usuários nomeados**, Olá **grupo proprietário**, e **grupos nomeados** quando estiver algoritmo de verificação de acesso de execução hello. Aqui estão os principais conceitos Olá para máscara hello.

* máscara de saudação cria "permissões efetivas". Ou seja, modifica as permissões de saudação em tempo de saudação de verificação de acesso.
* máscara de saudação pode ser editada diretamente pelo proprietário do arquivo hello e quaisquer super usuários.
* máscara de saudação pode remover a permissão efetiva do permissões toocreate Olá. máscara de saudação *não é possível* adicionar permissão efetiva do toohello de permissões.

Vejamos alguns exemplos. Saudação de exemplo a seguir, máscara de saudação é definida muito**RWX**, que significa que essa máscara Olá não remova as permissões. permissões efetivas Olá Olá usuário, grupo de proprietário e denominado grupo nomeado não são alteradas durante a verificação de acesso de saudação.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

Saudação de exemplo a seguir, máscara de saudação é definida muito**R-X**. Isso significa que ele **desativa permissões de gravação da saudação** para **usuário nomeado**, **grupo proprietário**, e **denominado grupo** em tempo de saudação do access seleção.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

Para referência, aqui é onde a máscara de saudação para um arquivo ou pasta aparece na Olá portal do Azure.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> Para obter uma nova conta do repositório Data Lake, máscara Olá Olá acesso ACL e ACL padrão da raiz de saudação ("/") de pasta padrão é tooRWX.
>
>

## <a name="permissions-on-new-files-and-folders"></a>Permissões em novos arquivos e pastas

Quando um novo arquivo ou pasta é criada em uma pasta existente, a saudação padrão ACL na pasta pai de saudação determina:

- ACL Padrão e ACL de Acesso de uma pasta filho.
- ACL de Acesso de um arquivo filho (os arquivos não têm uma ACL Padrão).

### <a name="hello-access-acl-of-a-child-file-or-folder"></a>Olá acesso ACL de um filho de arquivo ou pasta

Quando um arquivo filho ou uma pasta é criada, padrão ACL do pai da saudação é copiada como Olá Olá filho arquivo ou pasta de acesso ACL. Além disso, se **outros** usuário tem permissões de RWX na ACL padrão de saudação pai, ele será removido da ACL de acesso do item do hello filho.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

Na maioria dos cenários, as informações anteriores Olá são que tudo o que você precisa tooknow sobre como acesso ACL de um item filho é determinada. No entanto, se você estiver familiarizado com os sistemas POSIX e quiser toounderstand detalhada como essa transformação é obtida, consulte a seção Olá [função do Umask na criação de saudação acesso ACL para novos arquivos e pastas](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) posteriormente neste artigo.


### <a name="a-child-folders-default-acl"></a>ACL Padrão de uma pasta filho

Quando uma pasta filho é criada em uma pasta pai, padrão ACL da pasta do pai de saudação é copiada sobre como está a ACL de padrão da pasta do toohello filho.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a>Tópicos avançados para compreender as ACLs no Data Lake Store

A seguir estão alguns toohelp tópicos avançados que você entender como as ACLs são determinadas por pastas ou arquivos de repositório Data Lake.

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a>Função do umask na criação de saudação acesso ACL para novos arquivos e pastas

Em um sistema compatível com o POSIX, conceito geral Olá é que umask é um valor de 9 bits na pasta pai Olá que usou permissão Olá tootransform **usuário proprietário**, **grupo proprietário**, e  **outros** em Olá acesso ACL de um novo arquivo filho ou uma pasta. bits de saudação de um umask identificam quais tooturn bits desativado na ACL de acesso do item do hello filho. Assim, ele é usado tooselectively impedir a propagação de saudação de permissões para **usuário proprietário**, **grupo proprietário**, e **outros**.

Em um sistema HDFS, Olá umask costuma ser uma opção de configuração de todo o site é controlada por administradores. O Data Lake Store usa uma **umask de toda a conta** que não pode ser alterada. Olá a seguinte tabela mostra Olá sem máscara para repositório Data Lake.

| Grupo de usuários  | Configuração | Efeito na ACL de Acesso de um novo item filho |
|------------ |---------|---------------------------------------|
| usuário proprietário | ---     | Sem efeito                             |
| grupo proprietário| ---     | Sem efeito                             |
| outro       | RWX     | Remover Ler + Gravar + Executar         |

Olá ilustração a seguir mostra essa umask em ação. efeito de saudação é tooremove **leitura + escrita + executar** para **outros** usuário. Porque Olá umask não especificou o bits para **usuário proprietário** e **grupo proprietário**, essas permissões não são transformadas.

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a>bit Autoadesivas Olá

bit Autoadesivas Olá é um recurso mais avançado de um sistema de arquivos POSIX. No contexto de saudação do repositório Data Lake, é improvável que esse bit Autoadesivas hello serão necessários.

Olá tabela a seguir mostra como bit Autoadesivas Olá funciona no repositório Data Lake.

| Grupo de usuários         | Arquivo    | Pasta |
|--------------------|---------|-------------------------|
| Sticky bit **DESATIVADO** | Sem efeito   | Sem efeito.           |
| Sticky bit **ATIVADO**  | Sem efeito   | Impede que qualquer pessoa exceto **super usuários** e hello **usuário proprietário** de um item filho de excluir ou renomear o item filho.               |

bit Autoadesivas Olá não é mostrada em Olá portal do Azure.

## <a name="common-questions-about-acls-in-data-lake-store"></a>Perguntas comuns sobre ACLs no Data Lake Store

Aqui estão algumas perguntas que surgem com frequência sobre ACLs no Data Lake Store.

### <a name="do-i-have-tooenable-support-for-acls"></a>É necessário o suporte para ACLs tooenable?

Não. O controle de acesso via ACLs está sempre ativado para uma conta do Data Lake Store.

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a>Quais permissões são necessárias toorecursively excluir uma pasta e seu conteúdo?

* a pasta pai Olá deve ter **gravar + executar** permissões.
* Olá toobe pasta excluída e requer que todas as pastas dentro dele, **leitura + escrita + executar** permissões.

> [!NOTE]
> Não é necessário gravar permissões toodelete arquivos em pastas. Além disso, Olá pasta raiz "/" pode **nunca** ser excluído.
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a>Quem é o proprietário de saudação de um arquivo ou pasta?

Criador de saudação de um arquivo ou pasta se torna o proprietário de saudação.

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a>Qual grupo está definido como Olá possui o grupo de um arquivo ou pasta no momento da criação?

grupo proprietário Olá é copiado da saudação possui o grupo da pasta pai de saudação sob o qual Olá novo arquivo ou pasta é criada.

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a>Estou Olá possui um usuário de um arquivo, mas não tenho permissões de RWX Olá que necessário. O que devo fazer?

usuário proprietário Olá pode alterar permissões Olá Olá arquivo toogive se qualquer RWX permissões precisam.

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a>Quando vejo as ACLs no hello portal do Azure, consulte nomes de usuário, mas por meio de APIs, vejo que os GUIDs, por quê?

Entradas no hello ACLs são armazenadas como GUIDs que correspondem a toousers no AD do Azure. Olá APIs retornar Olá GUIDs como está. Olá portal do Azure tenta toomake ACLs mais fácil toouse por conversão Olá GUIDs em nomes amigáveis, quando possível.

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a>Por que às vezes, vejo GUIDs Olá ACLs ao usar o hello portal do Azure?

Um GUID é mostrado ao usuário Olá não existe no AD do Azure mais. Normalmente, isso ocorre quando o usuário Olá saiu da empresa de saudação ou se sua conta foi excluída no AD do Azure.

### <a name="does-data-lake-store-support-inheritance-of-acls"></a>O Data Lake Store dá suporte à herança de ACLs?

Não.

### <a name="what-is-hello-difference-between-mask-and-umask"></a>Qual é a diferença de saudação entre máscara e umask?

| mask | umask|
|------|------|
| Olá **máscara** propriedade está disponível em cada arquivo e pasta. | Olá **umask** é uma propriedade de saudação conta do repositório Data Lake. Portanto, há apenas um único umask em Olá repositório Data Lake.    |
| propriedade de máscara de saudação em um arquivo ou pasta pode ser alterada por Olá possui um usuário ou grupo de um arquivo ou um superusuário proprietário. | propriedade de umask Olá não pode ser modificada por qualquer usuário, até mesmo um superusuário. É um valor constante, inalterável.|
| propriedade de máscara de saudação é usada durante o algoritmo de verificação de acesso de saudação em tempo de execução toodetermine se um usuário tem tooperform direita Olá em operação em um arquivo ou pasta. função Hello máscara Olá é toocreate "permissões efetivas" em tempo de saudação de verificação de acesso. | Olá umask não é usado em todos os durante a verificação de acesso. Olá umask é usado toodetermine Olá acesso ACL de novos itens filho de uma pasta. |
| máscara de saudação é um valor RWX de 3 bits que se aplica a toonamed usuário, grupo nomeado e usuário proprietário no tempo de saudação de verificação de acesso.| Olá, umask é um valor de 9 bits que se aplica a toohello possui um usuário, grupo, proprietário e **outros** de um novo filho.|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a>Onde posso saber mais sobre o modelo de controle de acesso do POSIX?

* [Listas de controle de acesso POSIX no Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [Guia de permissão do HDFS](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [PERGUNTAS FREQUENTES SOBRE O POSIX](http://www.opengroup.org/austin/papers/posix_faq.html)

* [POSIX 1003.1 2008](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [POSIX 1003.1 2013](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [POSIX 1003.1 2016](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [POSIX ACL no Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs)

* [ACL usando listas de controle de acesso no Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a>Consulte também

* [Visão geral do Repositório Azure Data Lake](data-lake-store-overview.md)
