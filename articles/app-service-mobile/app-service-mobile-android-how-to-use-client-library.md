---
title: "aaaHow toouse hello Azure SDK de aplicativos móveis para Android | Microsoft Docs"
description: "Como toouse Olá SDK de aplicativos móveis do Azure para Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>Como toouse Olá SDK de aplicativos móveis do Azure para Android

Este guia mostra como toouse Olá Android SDK de cliente para cenários comuns de tooimplement de aplicativos móveis, como:

* Consulta de dados (inserir, atualizar e excluir).
* Autenticação.
* Tratamento de erros.
* Personalizando cliente hello.

Este guia se concentra na saudação do cliente SDK do Android.  toolearn mais sobre hello SDKs do lado do servidor para aplicativos móveis, consulte [trabalhar com o back-end .NET SDK] [ 10] ou [como toouse Olá back-end node. js SDK] [ 11].

## <a name="reference-documentation"></a>Documentação de referência

Você pode encontrar hello [referência da API Javadocs] [ 12] para a biblioteca de cliente do Android Olá no GitHub.

## <a name="supported-platforms"></a>Plataformas com suporte

Hello Azure SDK de aplicativos móveis para Android oferece suporte a API níveis 19 a 24 (KitKat por meio de Nougat) para formatos de telefone e tablet.  A autenticação, em particular, utiliza um credenciais de toogather abordagem do framework do web comuns.  A autenticação de fluxo do servidor não funciona com dispositivos de fator de forma pequeno como inspeções.

## <a name="setup-and-prerequisites"></a>Configuração e pré-requisitos

Olá completa [início rápido de aplicativos móveis](app-service-mobile-android-get-started.md) tutorial.  Essa tarefa faz com que todos os pré-requisitos para o desenvolvimento de Aplicativos Móveis do Azure sejam atendidos.  Olá Quickstart também ajuda você a configurar sua conta e criar seu primeiro back-end do aplicativo móvel.

Se você decidir não toocomplete tutorial de início rápido de Olá, conclua Olá tarefas a seguir:

* [criar um back-end do aplicativo móvel] [ 13] toouse com seu aplicativo do Android.
* No Android Studio, [criar arquivos de atualização Olá Gradle](#gradle-build).
* [Habilitar a permissão de Internet](#enable-internet).

### <a name="gradle-build"></a>Atualizar Olá Gradle criar arquivo

Altere ambos os arquivos **build.gradle** :

1. Adicione este código toohello *projeto* nível **gradle** arquivo hello *buildscript* marca:

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. Adicione este código toohello *aplicativo módulo* nível **gradle** arquivo hello *dependências* marca:

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    Atualmente a versão mais recente da saudação é 3.3.0. Olá suporte para as versões são listadas [na bintray][14].

### <a name="enable-internet"></a>Habilitar a permissão de Internet

tooaccess do Azure, seu aplicativo deve ter permissão de INTERNET Olá habilitada. Se ele ainda não estiver habilitado, adicionar Olá a seguinte linha de código tooyour **AndroidManifest.xml** arquivo:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>Criar uma conexão de cliente

Aplicativos móveis do Azure fornece quatro funções de aplicativo móvel tooyour:

* Acesso a Dados e a Sincronização Offline com um Serviço de Aplicativos Móveis do Azure.
* Chame APIs personalizado escrito com hello SDK de servidor de aplicativos móveis do Azure.
* Autenticação com autenticação e autorização do Serviço de Aplicativo do Azure.
* Envie notificações por push com hubs de notificação.

Cada uma dessas funções primeiro exige que você crie um objeto `MobileServiceClient`.  Apenas um objeto `MobileServiceClient` deve ser criado em seu cliente móvel (ou seja, deve ser um padrão Singleton).  toocreate um `MobileServiceClient` objeto:

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

Olá `<MobileAppUrl>` é uma cadeia de caracteres ou um objeto de URL que aponta o back-end do tooyour móvel.  Se você estiver usando o serviço de aplicativo do Azure toohost seu back-end móvel, em seguida, certifique-se de usar Olá seguro `https://` versão da URL de saudação.

Olá cliente também exige acesso toohello atividade ou contexto - Olá `this` parâmetro no exemplo hello.  Olá MobileServiceClient construção deve acontecer dentro de saudação `onCreate()` método hello atividade referenciada no hello `AndroidManifest.xml` arquivo.

Como prática recomendada, você deve abstrair a comunicação do servidor em sua própria classe (padrão singleton).  Nesse caso, você deve passar hello atividade dentro de saudação construtor tooappropriately Configurar serviço de saudação.  Por exemplo:

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

Agora você pode chamar `AzureServiceAdapter.Initialize(this);` em Olá `onCreate()` método de sua atividade principal.  Usam outros métodos que precisam de cliente de acesso à toohello `AzureServiceAdapter.getInstance();` tooobtain um adaptador de serviço de toohello de referência.

## <a name="data-operations"></a>Operações de dados

núcleo de saudação do hello SDK de aplicativos móveis do Azure é tooprovide acesso toodata armazenado no SQL Azure no back-end de aplicativo móvel hello.  Você pode acessar esses dados usando classes fortemente tipadas (preferido) ou consultas não tipadas (não recomendado).  em massa de saudação desta seção lida com usando classes com rigidez de tipos.

### <a name="define-client-data-classes"></a>Definir as classes de dados do cliente

tooaccess dados de tabelas do SQL Azure, definir classes de dados do cliente que correspondem a tabelas toohello no back-end de aplicativo móvel hello. Exemplos neste tópico presumem uma tabela chamada **MyDataTable**, que tem Olá colunas a seguir:

* ID
* text
* concluído

Olá correspondente com tipo do lado do cliente objeto reside em um arquivo chamado **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

Adicione os métodos getter e setter para cada campo que você adicionar.  Se sua tabela do SQL Azure contém mais colunas, você poderia adicionar classe de toothis de campos correspondente hello.  Por exemplo, se hello DTO (objeto de transferência de dados) tiver uma coluna de prioridade de número inteiro, em seguida, você pode adicionar esse campo, junto com seus métodos getter e setter:

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

toolearn como toocreate outras tabelas no seu back-end de aplicativos móveis, consulte [como: definir um controlador de tabela] [ 15] (back-end .NET) ou [definir tabelas usando um esquema dinâmico] [ 16] (Node. js back-end).

Uma tabela de back-end os aplicativos móveis do Azure define cinco campos especiais, quatro delas são tooclients disponíveis:

* `String id`: Olá ID globalmente exclusiva para registro de saudação.  Como uma prática recomendada, verifique a representação de cadeia de caracteres de Olá Olá id de um [UUID] [ 17] objeto.
* `DateTimeOffset updatedAt`: Olá data/hora da última atualização do hello.  campo de updatedAt de saudação é definido pelo servidor de saudação e nunca deve ser definido por código do cliente.
* `DateTimeOffset createdAt`: data/hora Olá Olá objeto foi criado.  campo de criadona de saudação é definido pelo servidor de saudação e nunca deve ser definido por código do cliente.
* `byte[] version`: Normalmente é representada como uma cadeia de caracteres, versão Olá também é definido pelo servidor de saudação.
* `boolean deleted`: Indica que registro Olá foi excluído, mas ainda não foi limpo.  Não use `deleted` como uma propriedade em sua classe.

Olá `id` campo é obrigatório.  Olá `updatedAt` campo e `version` campo são usados para sincronização offline (para a resolução de conflito e de sincronização incremental respectivamente).  Olá `createdAt` campo é um campo de referência e não é usado pelo cliente de saudação.  Olá nomes são "entre-the-wire" nomes de propriedades de saudação e não ajustáveis.  No entanto, você pode criar um mapeamento entre o objeto e hello nomes de "em-the-wire" usando Olá [gson] [ 3] biblioteca.  Por exemplo:

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a>Criar uma referência de tabela

tooaccess uma tabela, primeiro crie um [MobileServiceTable] [ 8] objeto por chamada hello **getTable** método hello [MobileServiceClient][9].  Esse método tem duas sobrecargas:

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

Em Olá seguindo o código, **mClient** é um objeto de MobileServiceClient de tooyour de referência.  sobrecarga primeiro Olá usada no qual o nome da classe hello e o nome da tabela de saudação serão Olá mesmo, e é hello um usado em Olá início rápido:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

Olá segunda sobrecarga é usada quando o nome da tabela Olá é diferente do nome de classe Olá: Olá primeiro parâmetro é o nome da tabela hello.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>Consultar uma tabela de back-end

Primeiro, obtenha uma referência de tabela.  Em seguida, execute uma consulta na referência de tabela hello.  Uma consulta é qualquer combinação de:

* Uma [cláusula de filtro `.where()`](#filtering).
* Uma [cláusula de ordenação `.orderBy()`](#sorting).
* Uma [cláusula de seleção de campo `.select()`](#selection).
* Um `.skip()` e `.top()` para [resultados paginados](#paging).

cláusulas Olá devem ser apresentadas em Olá anterior ordem.

### <a name="filter"></a> Filtragem de resultados

saudação de forma geral de uma consulta é:

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

Olá, exemplo anterior retorna todos os resultados (o tamanho de página máximo toohello definido pelo servidor de saudação).  Olá `.execute()` método executa a consulta de saudação em Olá back-end.  Olá, consulta é convertida tooan [OData v3] [ 19] consulta antes de back-end do transmissão toohello aplicativos móveis.  Após o recebimento, back-end de aplicativos móveis Olá converte consulta Olá em uma instrução SQL antes de executá-lo na instância do SQL Azure hello.  Desde que a atividade de rede leva algum tempo, Olá `.execute()` método retorna um [ `ListenableFuture<E>` ] [ 18].

### <a name="filtering"></a>Filtrar dados retornados

Olá a execução da consulta a seguir retorna todos os itens de saudação **ToDoItem** tabela onde **completa** é igual a **false**.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** é Olá referência toohello serviço móvel tabela que criamos anteriormente.

Definir um filtro usando Olá **onde** chamada de método na referência de tabela hello. Olá **onde** método é seguido por um **campo** método seguido por um método que especifica um predicado de lógica de saudação. Os possíveis métodos de predicado incluem **eq** (igual),**ne** (diferente), **gt** (maior que), **ge** (maior que ou igual a), **lt** (menor que), **le** (menor que ou igual a). Esses métodos permitem que você compare o número e toospecific valores de campos de cadeia de caracteres.

Você pode filtrar por datas. Olá métodos a seguir permitem que você compare o campo de data inteiro do hello ou partes de data de saudação: **ano**, **mês**, **dia**, **hora**, **minuto**, e **segundo**. Olá, exemplo a seguir adiciona um filtro para itens cujos *data de vencimento* é igual a 2013.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

Olá métodos a seguir suportam filtros complexos em campos de cadeia de caracteres: **startsWith**, **endsWith**, **concat**, **subcadeia de caracteres**, **indexOf**, **substituir**, **toLower**, **toUpper**, **trim**, e  **comprimento**. Olá filtros de exemplo a seguir para linhas de tabela onde hello *texto* coluna começa com "PRI0".

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

Olá métodos operadores a seguir têm suporte em campos de número: **adicionar**, **sub**, **mul**, **div**, **mod**, **andar**, **ceiling**, e **arredondar**. Olá filtros de exemplo a seguir para linhas de tabela onde hello **duração** é um número par.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

É possível combinar predicados com estes métodos lógicos: **and**, **or** e **not**. saudação de exemplo a seguir combina duas Olá anterior exemplos.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

Agrupar e aninhar operadores lógicos:

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

Para obter mais exemplos de filtragem e uma discussão, consulte [explorando riqueza de saudação do modelo de consulta de cliente do Android Olá][20].

### <a name="sorting"></a>Classificar dados retornados

Olá código a seguir retorna todos os itens de uma tabela de **ToDoItems** classificada em ordem crescente por Olá *texto* campo. *mToDoTable* é Olá referência toohello tabela de back-end que você criou anteriormente:

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

Olá primeiro parâmetro da saudação **orderBy** método é um nome de toohello igual de cadeia de caracteres do campo Olá no qual toosort. usa o segundo parâmetro de Olá Olá **QueryOrder** toospecify de enumeração se toosort em ordem crescente ou decrescente.  Se você estiver filtrando usando Olá ***onde*** método, Olá ***onde*** método deve ser chamado antes de saudação ***orderBy*** método.

### <a name="selection"></a>Selecionar colunas específicas

Olá código a seguir ilustra como tooreturn todos os itens de uma tabela de **ToDoItems**, mas exibe apenas Olá **completa** e **texto** campos. **mToDoTable** é Olá referência toohello tabela de back-end que criamos anteriormente.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

função select do Hello parâmetros toohello são nomes de cadeia de caracteres de Olá Olá das colunas da tabela que você deseja tooreturn.  Olá **selecione** método precisa toofollow métodos como **onde** e **orderBy**. Ele pode ser seguido por métodos de paginação como **skip** e **top**.

### <a name="paging"></a>Retornar dados em páginas

Os dados **SEMPRE** retornam em páginas.  número máximo de saudação de registros retornados é definido pelo servidor de saudação.  Se cliente Olá solicitar mais registros, o servidor de saudação retorna o número máximo de saudação de registros.  Por padrão, o tamanho máximo da página de saudação no servidor de saudação é 50 registros.

Olá primeiro exemplo mostra como tooselect Olá primeiros cinco itens de uma tabela. consulta de saudação retorna os itens de saudação de uma tabela de **ToDoItems**. **mToDoTable** é Olá referência toohello tabela de back-end que você criou anteriormente:

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

Aqui está uma consulta que ignora Olá cinco primeiros itens e, em seguida, retorna Olá cinco Avançar:

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

Se você quiser tooget todos os registros em uma tabela, implemente o código tooiterate sobre todas as páginas:

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

Uma solicitação para todos os registros usando esse método cria um mínimo de back-end de aplicativos móveis de toohello duas solicitações.

> [!TIP]
> Escolher tamanho de página direita Olá é um equilíbrio entre o uso de memória enquanto a solicitação hello está ocorrendo, o uso de largura de banda e atraso ao receber dados saudação completamente.  padrão de saudação (50 registros) é adequado para todos os dispositivos.  Se você operar exclusivamente em dispositivos de memória maior, aumente o too500.  Encontramos esse tamanho de página Olá crescentes além 500 registra os resultados em problemas de memória grandes e atrasos inaceitáveis.

### <a name="chaining"></a>Como concatenar métodos de consulta

métodos de saudação usados em consultas de tabelas de back-end podem ser concatenados. Encadeamento consulta métodos permite que você tooselect a colunas específicas de linhas filtradas que são classificadas e paginável. Você pode criar filtros lógicos complexos.  Cada método de consulta retorna um objeto de consulta. série de saudação tooend de métodos e consulta de execução realmente hello, chamada hello **executar** método. Por exemplo:

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

Olá encadeados consulta métodos devem ser ordenados da seguinte maneira:

1. Métodos de filtragem (**where**).
2. Métodos de classificação (**orderBy**).
3. Métodos de seleção (**select**).
4. Métodos de paginação (**skip** e **top**).

## <a name="binding"></a>Interface do usuário toohello dados de ligação

A associação de dados envolve três componentes:

* fonte de dados de saudação
* layout da tela Hello
* adaptador de saudação que ties Olá dois juntos.

Em nosso código de exemplo, retornamos dados saudação da tabela de Mobile aplicativos SQL Azure Olá **ToDoItem** em uma matriz. Essa atividade é um padrão comum para aplicativos de dados.  Consultas de banco de dados geralmente retornam uma coleção de linhas que Olá cliente obtém uma lista ou matriz. Neste exemplo, a matriz de saudação é fonte de dados de saudação.  código de saudação especifica um layout de tela que define o modo de exibição de saudação de dados Olá que aparece no dispositivo de saudação.  Hello dois são associados com um adaptador, o que esse código é uma extensão da saudação **ArrayAdapter&lt;ToDoItem&gt;**  classe.

#### <a name="layout"></a>Definir Olá Layout

layout de saudação é definido por vários trechos de código XML. Dado um layout existente, Olá código a seguir representa Olá **ListView** queremos toopopulate com nossos dados de servidor.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

Em Olá precede o código, Olá *listitem* atributo especifica a id de saudação do layout de saudação para uma linha individual na lista de saudação. Esse código especifica uma caixa de seleção e seu texto associado e é instanciado uma vez para cada item na lista de saudação. Esse layout não exibe Olá **id** campo e um layout mais complexo deve especificar campos adicionais na exibição de saudação. Esse código está em Olá **row_list_to_do.xml** arquivo.

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <a name="adapter"></a>Defina o adaptador de saudação
Como a fonte de dados de saudação do nosso exibição é uma matriz de **ToDoItem**, podemos subclasse nosso adaptador de um **ArrayAdapter&lt;ToDoItem&gt;**  classe. Essa subclasse produz uma exibição para cada **ToDoItem** usando Olá **row_list_to_do** layout.  Em nosso código, definimos Olá seguindo a classe que é uma extensão da saudação **ArrayAdapter&lt;E&gt;**  classe:

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Substituir adaptadores Olá **getView** método. Por exemplo:

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

Criamos uma instância dessa classe em nossa atividade, da seguinte forma:

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

Olá segundo parâmetro toohello ToDoItemAdapter construtor é um layout de toohello de referência. Agora podemos pode instanciar Olá **ListView** e atribuir Olá adaptador toohello **ListView**.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Use Olá adaptador tooBind toohello da interface do usuário

Agora você está pronto toouse associação de dados. Olá código a seguir mostra como tooget itens na tabela de saudação e preenchimentos Olá adaptador local com hello itens devolvido.

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

Chamar adaptador Olá sempre que modificar Olá **ToDoItem** tabela. Como as modificações são feitas de registro em registro, você trata de uma única linha em vez de uma coleção. Quando você insere um item, chame Olá **adicionar** método Olá adaptador ativada; quando a exclusão, chame Olá **remover** método.

Você pode encontrar um exemplo completo em Olá [projeto Quickstart Android][21].

## <a name="inserting"></a>Inserir dados em Olá back-end

Criar uma instância da saudação *ToDoItem* de classe e defina suas propriedades.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

Em seguida, use **Insert ()** tooinsert um objeto:

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

Olá retornou correspondências de entidade inseridos na tabela de back-end hello, ID de saudação incluído e quaisquer outros valores de dados de saudação (como Olá `createdAt`, `updatedAt`, e `version` campos) definido no hello back-end.

As tabelas de Aplicativos Móveis exigem uma coluna de chave primária denominada **id**. Essa coluna deve ser uma cadeia de caracteres. valor padrão de Olá Olá da coluna de ID é um GUID.  Você pode fornecer outros valores exclusivos, como endereços de email ou nomes de usuário. Quando um valor de ID de cadeia de caracteres não for fornecido para um registro inserido, Olá back-end gera um novo GUID.

Valores de ID de cadeia de caracteres fornecem Olá vantagens a seguir:

* IDs podem ser gerados sem fazer um banco de dados de toohello de ida e volta.
* Os registros são toomerge mais fácil de tabelas diferentes ou bancos de dados.
* Os valores de ID integram-se melhor à lógica de um aplicativo.

Valores de ID de cadeia de caracteres são **OBRIGATÓRIOS** para suporte de sincronização offline.  Você não pode alterar uma Id quando ela é armazenada no banco de dados de back-end de saudação.

## <a name="updating"></a>Atualizar dados em um aplicativo móvel

tooupdate dados em uma tabela, passar Olá novo objeto toohello **Update ()** método.

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

Neste exemplo, *item* é uma referência tooa linha hello *ToDoItem* tabela que tenha sido tooit algumas alterações feitas.  saudação de linha com hello mesmo **id** é atualizada.

## <a name="deleting"></a>Excluir dados em um aplicativo móvel

saudação de código a seguir mostra como toodelete dados de uma tabela especificando Olá objeto de dados.

```java
mToDoTable
    .delete(item);
```

Você também pode excluir um item especificando Olá **id** campo de saudação toodelete de linha.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>Pesquisar um item específico por ID

Pesquisar um item com um determinado **id** campo com hello **Lookup ()** método:

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>Como trabalhar com dados não tipados

o modelo de programação sem tipo Hello proporciona controle exato sobre serialização JSON.  Há alguns cenários comuns em que você poderá toouse um modelo de programação sem tipo. Por exemplo, se a tabela de back-end contiver várias colunas e você só precisa de um subconjunto de colunas de saudação do tooreference.  modelo de tipo Hello requer toodefine todas as colunas de saudação definidas no back-end do hello aplicativos móveis em sua classe de dados.  A maioria das chamadas à API para acessar dados de saudação é semelhante toohello digitado chamadas de programação. Olá principal diferença é no modelo sem tipo hello invocar métodos em Olá **MobileServiceJsonTable** objeto, em vez da saudação **MobileServiceTable** objeto.

### <a name="json_instance"></a>Criar uma instância de uma tabela não tipada

Toohello semelhante digitado modelo, você comece obtendo uma referência de tabela, mas nesse caso é um **MobileServicesJsonTable** objeto. Obter referência Olá Olá chamada **getTable** método em uma instância do cliente hello:

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

Depois de criar uma instância do hello **MobileServiceJsonTable**, ele tem praticamente Olá mesma API disponível como com o modelo de programação tipada hello. Em alguns casos, os métodos de saudação levar um parâmetro sem tipo, em vez de um parâmetro de tipo.

### <a name="json_insert"></a>Inserir em uma tabela não tipada
Olá mostrado no código a seguir como toodo uma inserção. Olá, primeira etapa é toocreate uma [JsonObject][1], que faz parte da saudação [gson] [ 3] biblioteca.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

Em seguida, Use **Insert ()** tooinsert Olá sem tipo objeto tabela hello.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Se você precisar tooget Olá ID de objeto Olá inserido, use Olá **getAsJsonPrimitive()** método.

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>Excluir de uma tabela não tipada
Olá código a seguir mostra como toodelete uma instância, Olá nesse caso, a mesma instância de um **JsonObject** que foi criado no antes da saudação *inserir* exemplo. código de saudação é hello igual Olá digitados caso, mas o método hello tem uma assinatura diferente, pois ela faz referência a um **JsonObject**.

```java
mToDoTable
    .delete(insertedItem);
```

Você também pode excluir uma instância diretamente, usando sua ID:

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>Retornar todas as linhas de uma tabela não tipada
Olá mostrado no código a seguir como tooretrieve uma tabela inteira. Como você está usando uma tabela de JSON, você pode recuperar apenas algumas das colunas da tabela Olá seletivamente.

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

Olá a mesmo conjunto de filtragem, filtragem e paginação métodos que estão disponíveis para o modelo de tipo hello estão disponíveis para o modelo sem tipo hello.

## <a name="offline-sync"></a>Implementar a sincronização offline

Olá SDK de cliente de aplicativos móveis do Azure também implementa sincronização offline de dados usando um toostore de banco de dados SQLite uma cópia dos dados do servidor de saudação localmente.  Operações executadas em uma tabela offline não exigem conectividade móvel toowork.  Sincronização offline ajuda a resiliência e desempenho a despesa de saudação de lógica mais complexa para resolução de conflitos.  Olá SDK de cliente de aplicativos móveis do Azure implementa Olá recursos a seguir:

* Sincronização Incremental: somente registros novos e atualizados são baixados, economizando o consumo de largura de banda e de memória.
* Simultaneidade otimista: Operações são consideradas toosucceed.  Resolução de conflitos é adiada até que as atualizações são executadas no servidor de saudação.
* Resolução de conflito: Olá que SDK detecta quando uma alteração conflitante foi feita no servidor de saudação e fornece conecta o usuário de saudação tooalert.
* Exclusão reversível: Registros excluídos são marcadas como excluídos, permitindo que outros dispositivos tooupdate seu cache offline.

### <a name="initialize-offline-sync"></a>Inicializar a sincronização offline

Cada tabela offline deve ser definida no cache offline de saudação antes do uso.  Normalmente, a definição da tabela é feita imediatamente após a criação de saudação do cliente hello:

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>Obter uma referência toohello tabela de Cache Offline

Para uma tabela online, use `.getTable()`.  Para uma tabela offline, use `.getSyncTable()`:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

Todos os Olá métodos que estão disponíveis para tabelas online (incluindo a filtragem, classificação, paginação, inserção de dados, atualização de dados e exclusão de dados) funcionam igualmente bem em tabelas online e offline.

### <a name="synchronize-hello-local-offline-cache"></a>Sincronizar Olá Local Cache Offline

A sincronização é dentro do controle de saudação do seu aplicativo.  Veja um exemplo de método de sincronização:

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

Se um nome de consulta é fornecido toohello `.pull(query, queryname)` método e, em seguida, a sincronização incremental é usado tooreturn somente os registros que foram criados ou alterados desde a recepção de saudação última concluída com êxito.

### <a name="handle-conflicts-during-offline-synchronization"></a>Lidar com conflitos durante a sincronização offline

Se um conflito ocorrer durante uma operação `.push()`, uma `MobileServiceConflictException` será lançada.   item de servidor emitido Olá é inserido na exceção de saudação e pode ser recuperada por `.getItem()` na exceção de saudação.  Ajuste push Olá por chamada hello itens a seguir no objeto de MobileServiceSyncContext hello:

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

Depois que todos os conflitos são marcados como quiser, chame `.push()` novamente tooresolve Olá a todos os conflitos.

## <a name="custom-api"></a>Chamar uma API personalizada

Uma API personalizada permite que você toodefine pontos de extremidade personalizados que expõem a funcionalidade do servidor que não mapeiam tooan inserir, atualizar, excluir ou operação de leitura. Usando uma API personalizada, você pode ter mais controle sobre mensagens, incluindo ler e definir cabeçalhos de mensagens HTTP e definir um formato de corpo de mensagem diferente do JSON.

Em um cliente Android, você chamar hello **invokeApi** método toocall Olá API ponto de extremidade personalizado. Olá exemplo a seguir mostra como toocall um ponto de extremidade de API nomeados **completeAll**, que retorna uma classe de coleção chamada **MarkAllResult**.

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

Olá **invokeApi** método é chamado no cliente de saudação, que envia uma mensagem de solicitação toohello nova API personalizada. resultado de saudação retornado pela API personalizada Olá é exibido em uma caixa de diálogo de mensagem, como erros. Outras versões do **invokeApi** permitem que você enviar um objeto no corpo da solicitação de saudação opcionalmente, especifique o método hello HTTP e enviar parâmetros de consulta com a solicitação de saudação. Versões não tipadas de **invokeApi** também são fornecidas.

## <a name="authentication"></a>Adicionar autenticação tooyour aplicativo

Tutoriais já descrevem detalhadamente como tooadd esses recursos.

O Serviço de Aplicativo oferece suporte à [autenticação de usuários do aplicativo](app-service-mobile-android-get-started-users.md) usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft, Twitter e Azure Active Directory. Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários. Você também pode usar a identidade Olá usuários autenticados tooimplement de regras de autorização em seu back-end.

Dois fluxos de autenticação são suportados: um **server** flow e um **client** flow. fluxo do servidor de saudação fornece experiência de autenticação mais simples de hello, como ele se baseia na interface de web de provedores de identidade hello.  Nenhum SDKs adicionais são necessárias tooimplement autenticação de fluxo do servidor. Autenticação do servidor fluxo não oferece uma integração profunda no dispositivo móvel hello e só é recomendada para uma prova de cenários de conceito.

fluxo de saudação do cliente permite uma integração mais profunda com recursos específicos do dispositivo, como o logon único conforme depende dos SDKs fornecidos pelo provedor de identidade hello.  Por exemplo, você pode integrar Olá Facebook SDK em seu aplicativo móvel.  cliente móvel Olá alterna para o aplicativo do Facebook hello e confirma o logon antes de trocá aplicativo móvel tooyour back.

Quatro etapas são necessárias tooenable autenticação em seu aplicativo:

* Registrar o aplicativo para autenticação com um provedor de identidade.
* Configurar o back-end do Serviço de Aplicativo.
* Restringe os usuários de tooauthenticated de permissões de tabela somente em Olá back-end do serviço de aplicativo.
* Adicione o aplicativo de tooyour de código de autenticação.

Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários. Você também pode usar o hello SID de um usuário autenticado toomodify solicitações.  Para obter mais informações, consulte [Introdução à autenticação] e hello documentação como de SDK do servidor.

### <a name="caching"></a>Autenticação: Fluxo de servidor

Olá código a seguir inicia um processo de logon do fluxo de servidor usando o provedor de saudação do Google.  Configuração adicional é necessária devido aos requisitos de segurança Olá para o provedor de saudação do Google:

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

Além disso, adicione Olá classe principal de atividade do método toohello a seguir:

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

Olá `GOOGLE_LOGIN_REQUEST_CODE` definido na sua principal atividade é usada para Olá `login()` método e dentro de saudação `onActivityResult()` método.  Você pode escolher qualquer número exclusivo, como hello mesmo número é usado em Olá `login()` método e hello `onActivityResult()` método.  Se você abstrair o código de saudação do cliente em um adaptador de serviço (conforme mostrado anteriormente), você deve chamar métodos apropriados Olá no adaptador de saudação do serviço.

Também é necessário um projeto de saudação tooconfigure para customtabs.  Primeiro, especifique uma URL de redirecionamento.  Adicionar Olá trecho de código a seguir muito`AndroidManifest.xml`:

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

Adicionar Olá **redirectUriScheme** toohello `build.gradle` arquivo para seu aplicativo:

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

Finalmente, adicione `com.android.support:customtabs:23.0.1` toohello lista de dependências no hello `build.gradle` arquivo:

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

Obter ID de saudação do hello usuário que fez logon de um **MobileServiceUser** usando Olá **getUserId** método. Para obter um exemplo de como toouse futuros toocall Olá logon assíncrona APIs, consulte [Introdução à autenticação].

> [!WARNING]
> Olá mencionado o esquema de URL diferencia maiusculas de minúsculas.  Certifique-se de que todas as ocorrências de `{url_scheme_of_you_app}` tenham as mesmas maiúsculas ou minúsculas.

### <a name="caching"></a>Armazenar tokens de autenticação em cache

Cache de tokens de autenticação requer toostore Olá ID de usuário e token de autenticação localmente no dispositivo de saudação. Hello próxima inicialização aplicativo hello, você verificará Olá cache, e se esses valores estiverem presentes, você pode ignorar log Olá no procedimento e realimentar cliente Olá com esses dados. No entanto, esses dados são confidenciais e devem ser armazenado criptografados para segurança no caso de telefone Olá for roubado.  Você pode ver um exemplo completo de como os tokens de autenticação toocache em [seção de tokens de autenticação de Cache][7].

Quando você tenta toouse um token expirado, você receberá um *401 não autorizado* resposta. Você pode tratar erros de autenticação usando filtros.  Filtros interceptam solicitações toohello back-end do serviço de aplicativo. Olá filtro código testa resposta Olá para um 401, dispara o processo de entrada hello e recomeça a solicitação Olá que gerou Olá 401.

### <a name="refresh"></a>Usar tokens de atualização

o token de saudação retornado por autorização e autenticação do serviço de aplicativo do Azure tem um tempo de vida definido de uma hora.  Após esse período, você deve autenticar novamente usuário hello.  Se você estiver usando um token de vida longa que você recebeu por meio de autenticação de cliente de fluxo, em seguida, você pode autenticar novamente com a autenticação do serviço de aplicativo do Azure e autorização Olá mesmo token.  Outro token de Serviço de Aplicativo do Azure é gerado com um novo tempo de vida.

Você também pode registrar Olá provedor toouse Tokens de atualização.  Nem sempre um token de atualização está disponível.  É necessário realizar uma configuração adicional:

* Para **Active Directory do Azure**, configure um segredo do cliente para Olá aplicativo do Azure Active Directory.  Especifica o segredo de cliente de Olá em saudação do serviço de aplicativo do Azure ao configurar a autenticação do Active Directory do Azure.  Ao chamar `.login()`, passe `response_type=code id_token` como um parâmetro:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Para **Google**, passar Olá `access_type=offline` como um parâmetro:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Para **Microsoft Account**, selecione Olá `wl.offline_access` escopo.

toorefresh um token, chame `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

Como prática recomendada, crie um filtro que detecta uma resposta 401 do servidor de saudação e tenta token de usuário toorefresh hello.

## <a name="log-in-with-client-flow-authentication"></a>Faça logon com a autenticação de cliente-fluxo

processo geral de saudação para registro em log com autenticação de cliente de fluxo é da seguinte maneira:

* Configure a Autenticação e Autorização do Serviço de Aplicativo do Azure como você faria com autenticação de servidor-fluxo.
* Integre o provedor de autenticação de saudação SDK para autenticação tooproduce um token de acesso.
* Chamar hello `.login()` método da seguinte maneira:

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

Substituir saudação `onSuccess()` método com qualquer código que você deseja toouse em um logon bem-sucedido.  Olá `{provider}` cadeia de caracteres é um provedor válido: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, ou **twitter**.  Se você tiver implementado autenticação personalizada, você também pode usar o marca de provedor de autenticação personalizada hello.

### <a name="adal"></a>Autenticar usuários com hello biblioteca de autenticação do Active Directory (ADAL)

Você pode usar usuários do hello biblioteca de autenticação do Active Directory (ADAL) toosign em seu aplicativo usando o Active Directory do Azure. Usando um logon de fluxo de cliente geralmente é preferível toousing Olá `loginAsync()` métodos como ele fornece uma aparência UX mais nativa e permite a personalização adicional.

1. Configurar seu back-end do aplicativo móvel para entrar no AAD pela seguinte Olá [como tooconfigure aplicativo de serviço de logon do Active Directory] [ 22] tutorial. Torne-se toocomplete Olá opcional de registro de um aplicativo cliente nativo.
2. Instale o ADAL modificando a saudação de tooinclude de arquivo gradle definições a seguir:

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. Adicione Olá aplicativo tooyour de código a seguir, tornando Olá substituições a seguir:

* Substituir **aqui de autoridade de inserção** com o nome de saudação do locatário Olá no qual você provisionou o seu aplicativo. formato de saudação deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com.
* Substituir **inserir recursos-ID aqui** com a ID de cliente Olá para o back-end do aplicativo móvel. Você pode obter a ID do cliente Olá de Olá **avançado** guia **configurações do Active Directory do Azure** no portal de saudação.
* Substituir **aqui INSERT-CLIENT-ID** com a ID de cliente Olá você copiou do aplicativo cliente nativo de saudação.
* Substituir **INSERT-REDIRECT-URI-aqui** com seu site */.auth/login/done* ponto de extremidade, usando o esquema do hello HTTPS. Esse valor deve ser semelhante muito*https://contoso.azurewebsites.net/.auth/login/done*.

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <a name="filters"></a>Ajustar Olá comunicação cliente-servidor

saudação de conexão do cliente é normalmente uma conexão HTTP básica usando Olá subjacente biblioteca HTTP fornecida com hello SDK do Android.  Há várias razões por que você usaria toochange que:

* Você deseja toouse um tempo limite alternativo tooadjust de biblioteca HTTP.
* Você deseja tooprovide uma barra de progresso.
* Você deseja tooadd uma funcionalidade de gerenciamento do cabeçalho personalizado toosupport API.
* Você deseja toointercept uma resposta com falha para que você possa implementar reautenticação.
* Você deseja toolog solicitações de back-end tooan serviço de análise.

### <a name="using-an-alternate-http-library"></a>Usar uma biblioteca HTTP alternativa

Chamar hello `.setAndroidHttpClientFactory()` método imediatamente depois de criar sua referência de cliente.  Por exemplo, tooset Olá conexão timeout too60 segundos (em vez de padrão de saudação 10 segundos):

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a>Implementar um filtro de progresso

Você pode implementar uma interceptação de cada solicitação implementando um `ServiceFilter`.  Por exemplo, o seguinte Olá atualiza uma barra de progresso pré-criados:

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

Você pode anexar este cliente toohello de filtro da seguinte maneira:

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>Personalizar cabeçalhos de solicitações

Use Olá seguinte `ServiceFilter` e anexe o filtro de saudação em Olá mesma maneira que Olá `ProgressFilter`:

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <a name="conversions"></a>Configurar a Serialização Automática

Você pode especificar uma estratégia de conversão que aplica-se a coluna tooevery usando Olá [gson] [ 3] API. biblioteca de cliente do Android Olá usa [gson] [ 3] em segundo plano do hello tooserialize Java objetos tooJSON dados antes de dados saudação são enviados tooAzure do serviço de aplicativo.  Olá, código a seguir usa Olá **setFieldNamingStrategy()** estratégia de saudação do método tooset. Este exemplo exclui caractere inicial da saudação (um "m") e em letras minúsculas, em seguida, Olá próximo caractere, para cada nome de campo. Por exemplo, ele poderia transformar "mId" em "id".  Implementar uma saudação de tooreduce de estratégia de conversão precisa para `SerializedName()` anotações na maioria dos campos.

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

Esse código deve ser executado antes de criar uma referência de cliente móvel usando Olá **MobileServiceClient**.

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[Introdução à autenticação]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
