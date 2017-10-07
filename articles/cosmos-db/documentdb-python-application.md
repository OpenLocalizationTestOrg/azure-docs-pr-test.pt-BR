---
title: tutorial do aplicativo web aaaPython bulbo para o banco de dados do Azure Cosmos | Microsoft Docs
description: "Examine um tutorial do banco de dados usando o banco de dados do Azure Cosmos toostore e acessar dados de um aplicativo web do Python bulbo hospedado no Azure. Encontre soluções de desenvolvimento de aplicativo."
keywords: Desenvolvimento de aplicativos, python flask, aplicativo Web python, desenvolvimento Web do python
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Compilar um aplicativo Web do Python Flask usando o Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Este tutorial mostra como toouse o banco de dados do Azure Cosmos toostore e acessar dados de um Python hospedado no Azure do aplicativo web e presume que você tenha alguma experiência anterior com Python e sites do Azure.

Este tutorial de banco de dados aborda:

1. Crie e provisione uma conta do Cosmos DB.
2. Crie um aplicativo Python Flask.
3. Conectando tooand usando o banco de dados do Cosmos de seu aplicativo web.
4. Implantando Olá web aplicativo tooAzure.

Ao seguir este tutorial, você criará um aplicativo simples de votação que permite que você toovote para uma pesquisa.

![Captura de tela do aplicativo de votação hello criado por este tutorial do banco de dados](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Pré-requisitos do tutorial de banco de dados
Antes de seguir as instruções neste artigo hello, você deve garantir que você tenha a seguinte Olá instalado:

* Uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
 
    OU 

    Uma instalação local do hello [emulador de banco de dados do Azure Cosmos](local-emulator.md).
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).  
* [Ferramentas Python para Visual Studio](https://github.com/Microsoft/PTVS/).  
* [SDK do Microsoft Azure para Python 2.7](https://azure.microsoft.com/downloads/). 
* [Python 2.7.13](https://www.python.org/downloads/windows/). 

> [!IMPORTANT]
> Se você estiver instalando o Python 2.7 para Olá primeira vez, certifique-se de que na tela de Python personalizar 2.7.13 hello, você selecionar **adicionar python.exe tooPath**.
> 
> ![Captura de tela da tela de Python personalizar 2.7.11 hello, em que você precisa tooselect adicionar python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Compilador do Microsoft Visual C++ para Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB
Vamos começar criando uma conta do BD Cosmos. Se você já tiver uma conta ou se você estiver usando hello Azure Cosmos DB emulador para este tutorial, você poderá ignorar muito[etapa 2: criar um novo aplicativo web Python bulbo](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
Percorreremos agora como toocreate um novo aplicativo web Python bulbo da saudação plano de fundo do.

## <a name="step-2-create-a-new-python-flask-web-application"></a>Etapa 2: Criar um novo aplicativo Web Python Flask
1. No Visual Studio, no hello **arquivo** menus, aponte muito**novo**e, em seguida, clique em **projeto**.
   
    Olá **novo projeto** caixa de diálogo é exibida.
2. No painel esquerdo do hello, expanda **modelos** e **Python**e, em seguida, clique em **Web**. 
3. Selecione **bulbo Web projeto** no painel de central hello, em Olá **nome** caixa tipo **tutorial**e, em seguida, clique em **Okey**. Lembre-se de que os nomes de pacote do Python devem ser letras minúsculos, conforme descrito em Olá [guia de estilo para o código Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).
   
    Para esses novos tooPython bulbo, é uma estrutura de desenvolvimento de aplicativos web que ajuda você a criar aplicativos web no Python mais rapidamente.
   
    ![Captura de tela da janela do novo projeto Olá no Visual Studio com Python realçado em Olá Python bulbo Web projeto selecionado no meio de saudação e tutorial de nome de saudação na caixa de nome de saudação à esquerda](./media/documentdb-python-application/image9.png)
4. Em Olá **ferramentas Python para Visual Studio** janela, clique em **instalar em um ambiente virtual**. 
   
    ![Captura de tela do tutorial do banco de dados de saudação - ferramentas Python para a janela do Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. Em Olá **adicionar ambiente Virtual** janela, você pode aceitar os padrões de saudação e usar Python 2.7 ambiente base Olá porque PyDocumentDB não oferece suporte a Python 3. x e, em seguida, clique **criar**. Isso configura o ambiente virtual do Python Olá necessários para seu projeto.
   
    ![Captura de tela do tutorial do banco de dados de saudação - ferramentas Python para a janela do Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    Olá saída janela exibe `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` quando o ambiente de saudação for instalado com êxito.

## <a name="step-3-modify-hello-python-flask-web-application"></a>Etapa 3: Modificar o aplicativo de web hello bulbo Python
### <a name="add-hello-python-flask-packages-tooyour-project"></a>Adicionar Olá Python bulbo pacotes tooyour projeto
Depois de configurar o seu projeto, você precisará tooadd Olá necessário bulbo pacotes tooyour projeto, incluindo pydocumentdb, pacote de Python de saudação do DocumentDB.

1. No Solution Explorer, abra o arquivo de saudação chamado **requirements.txt** e substitua o conteúdo de saudação pelo seguinte hello:
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. Salvar Olá **requirements.txt** arquivo. 
3. No Gerenciador de Soluções, clique com o botão direito do mouse em **env** e clique em **Instalar de requirements.txt**.
   
    ![Captura de tela mostrando env (Python 2.7) selecionado com a instalação do requirements.txt realçado na lista de saudação](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    Após a instalação bem-sucedida, a janela de saída de hello exibe seguinte hello:
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > Em casos raros, talvez você veja uma falha na janela de saída de hello. Se isso acontecer, verifique se o erro de saudação é toocleanup relacionado. Às vezes, a limpeza de saudação falha, mas instalação Olá ainda será bem-sucedida (rolar para cima na tooverify de janela de saída de hello isso). Você pode verificar a instalação por [ambiente virtual do verificando Olá](#verify-the-virtual-environment). Se a falha na instalação de saudação mas Olá verificação for bem-sucedida, é toocontinue Okey.
   > 
   > 

### <a name="verify-hello-virtual-environment"></a>Verifique se o ambiente virtual Olá
Vamos garantir que tudo esteja instalado corretamente.

1. Compile a solução Olá pressionando **Ctrl**+**Shift**+**B**.
2. Quando Olá compilação for bem-sucedida, iniciar o site de saudação pressionando **F5**. Isso inicia o servidor de desenvolvimento do bulbo hello e inicia o navegador da web. Você deve ver Olá página a seguir.
   
    ![Olá vazio Python bulbo desenvolvimento projeto web exibido em um navegador](./media/documentdb-python-application/image12.png)
3. Parar a depuração site Olá pressionando **Shift**+**F5** no Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Criar definições de banco de dados, de coleção e de documentos
Agora vamos criar seu aplicativo de votação adicionando novos arquivos e enviando atualizações para outras pessoas.

1. No Gerenciador de soluções, clique com botão direito Olá **tutorial** de projeto, clique em **adicionar**e, em seguida, clique em **Novo Item**. Selecione **arquivo vazio do Python** e nome hello arquivo **forms.py**.  
2. Adicionar Olá seguir código toohello forms.py arquivo e, em seguida, salve o arquivo hello.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a>Adicionar Olá necessário importações tooviews.py
1. No Gerenciador de soluções, expanda Olá **tutorial** pasta e abra Olá **views.py** arquivo. 
2. Adicionar Olá após a importação instruções toohello superior de saudação **views.py** de arquivo e salve o arquivo hello. Esses importar PythonSDK do banco de dados Cosmos e Olá pacotes bulbo.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>Criar banco de dados, coleção e documento
* Ainda no **views.py**, adicionar Olá seguindo código toohello final do arquivo hello. Isso cuida de criação de banco de dados de saudação usado pelo formulário hello. Não exclua nenhum código existente Olá **views.py**. Basta acrescente essa extremidade toohello.

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a>Ler o banco de dados, a coleção, o documento e enviar o formulário
* Ainda no **views.py**, adicionar Olá seguindo código toohello final do arquivo hello. Isso cuida da configuração de formulário de hello, ler o documento, coleção e banco de dados de saudação. Não exclua nenhum código existente Olá **views.py**. Basta acrescente essa extremidade toohello.

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a>Criar hello arquivos HTML
1. No Solution Explorer, no hello **tutorial** pasta, direito clique Olá **modelos** pasta, clique em **adicionar**e, em seguida, clique em **Novo Item**. 
2. Selecione **página HTML**e, em seguida, na caixa, digite Olá nome **create.html**. 
3. Repita as etapas 1 e 2 toocreate dois outros HTML arquivos: results.html e vote.html.
4. Adicionar Olá código a seguir muito**create.html** em Olá `<body>` elemento. Ele exibe uma mensagem indicando que um banco de dados, uma coleção e um documento novos foram criados.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Adicionar Olá código a seguir muito**results.html** em Olá `<body`> elemento. Ele exibe os resultados de saudação de sondagem de saudação.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. Adicionar Olá código a seguir muito**vote.html** em Olá `<body`> elemento. Exibe a sondagem hello e aceita Olá votos. Sobre como registrar votos hello, controle Olá é passada pela tooviews.py onde podemos reconhecerá Olá voto cast e acrescentar documento hello adequadamente.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. Em Olá **modelos** substituir Olá conteúdo da pasta **index** com os seguintes hello. Isso serve como a saudação inicial da página do seu aplicativo.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a>Adicionar um arquivo de configuração e alterar Olá \_ \_init\_\_py
1. No Gerenciador de soluções, clique com botão direito Olá **tutorial** de projeto, clique em **adicionar**, clique em **Novo Item**, selecione **arquivo vazio do Python**e, em seguida, arquivo de saudação do nome **config.py**. Esse arquivo de configuração é exigido por formulários no flask. Você pode usá-lo tooprovide também uma chave secreta. Essa chave não será necessária neste tutorial.
2. Adicione Olá seguinte tooconfig.py de código, você precisará valores hello tooalter **DOCUMENTDB\_HOST** e **DOCUMENTDB\_chave** na próxima etapa do hello.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. Em Olá [portal do Azure](https://portal.azure.com/), navegar toohello **chaves** folha clicando **procurar**, **contas de banco de dados do Azure Cosmos**, clique duas vezes no nome da saudação de saudação toouse da conta e, em seguida, clique em Olá **chaves** botão Olá **Essentials** área. Em Olá **chaves** folha, Olá cópia **URI** valor e cole-a saudação **config.py** arquivo, como valor Olá Olá **DOCUMENTDB\_HOST**  propriedade. 
4. Em Olá portal do Azure, na Olá **chaves** folha, copiar o valor de saudação do hello **chave primária** ou hello **chave secundária**e cole-a saudação **config.py**  arquivo, como valor Olá Olá **DOCUMENTDB\_chave** propriedade.
5. Em Olá  **\_ \_init\_\_py** de arquivos, adicionar a seguinte linha de saudação. 
   
        app.config.from_object('config')
   
    Assim que o conteúdo do arquivo hello Olá é:
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. Depois de adicionar todos os arquivos de hello, Solution Explorer deve ser assim:
   
    ![Captura de tela da janela do Gerenciador de soluções do Visual Studio Olá](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>Etapa 4: executar o aplicativo localmente
1. Compile a solução Olá pressionando **Ctrl**+**Shift**+**B**.
2. Quando Olá compilação for bem-sucedida, iniciar o site de saudação pressionando **F5**. Você deve ver o seguinte de saudação na tela.
   
    ![Captura de tela de Olá Python + do aplicativo do Azure Cosmos DB votação exibido em um navegador da web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Clique em **criar/limpar Olá votação de banco de dados** banco de dados do toogenerate hello.
   
    ![Captura de tela de Olá Criar página de aplicativo de web hello – detalhes do desenvolvimento](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. Em seguida, clique em **Votar** e selecione sua opção.
   
    ![Captura de tela do aplicativo de web hello com uma pergunta votação apresentado](./media/documentdb-python-application/cosmos-db-vote.png)
5. Para cada voto converter, ele incrementa o contador de apropriada de saudação.
   
    ![Captura de tela de saudação resultados da página de voto Olá mostrado](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Pare a depuração de projeto Olá pressionando Shift + F5.

## <a name="step-5-deploy-hello-web-application-tooazure"></a>Etapa 5: Implantar Olá web aplicativo tooAzure
Agora que você tem um aplicativo completo de saudação funcionando corretamente no banco de dados do Cosmos, vamos toodeploy este tooAzure.

1. Projeto de saudação com o botão direito no Gerenciador de soluções (Verifique se você não tiver ainda executá-lo localmente) e selecione **publicar**.  
   
     ![Captura de tela do tutorial de saudação selecionado no Gerenciador de soluções, com a opção de publicar Olá realçada](./media/documentdb-python-application/image20.png)
2. Em Olá **publicar** caixa de diálogo, selecione **serviço de aplicativo do Microsoft Azure**, selecione **criar novo**e, em seguida, clique em **publicar**.
   
    ![Captura de tela da janela de publicar Web hello com o serviço de aplicativo do Microsoft Azure realçado](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. Em Olá **criar serviço de aplicativo** caixa de diálogo, digite o nome de saudação para seu aplicativo web junto com seus **assinatura**, **grupo de recursos**, e **plano do serviço de aplicativo** , em seguida, clique em **criar**.
   
    ![Captura de tela da janela de janela de aplicativos do Microsoft Azure Web Olá](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. Em poucos segundos, o Visual Studio terminará de publicar seu serviço de aplicativo e iniciará um navegador no qual você poderá ver seu trabalho sendo executado no Azure!

    ![Captura de tela da janela de janela de aplicativos do Microsoft Azure Web Olá](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Solucionar problemas
Se esse for o hello primeiro Python aplicativo executar no seu computador, certifique-se de que seguinte Olá pastas (ou locais de instalação equivalente Olá) são incluídos na sua variável de caminho:

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Se você receber um erro em sua página de voto e você nomeou seu projeto diferente de **tutorial**, certifique-se de que  **\_ \_init\_\_py** referências Olá nome correto do projeto na linha de saudação: `import tutorial.view`.

## <a name="next-steps"></a>Próximas etapas
Parabéns! Apenas ter concluído seu primeiro aplicativo web de Python usando o banco de dados do Cosmos e publicá-la tooAzure.

Atualizamos e aperfeiçoamos este tópico com frequência, de acordo com seus comentários.  Uma vez que você concluiu o tutorial hello, a. usando Olá votação botões na Olá superior e na parte inferior desta página e ser tooinclude-se de que seus comentários sobre quais melhorias você deseja toosee feita. Se você deseja toocontact você diretamente, sinta-se livre tooinclude endereço do seu email em seus comentários.

aplicativo de web do tooadd funcionalidade adicional tooyour, Olá revisão APIs disponíveis no hello [SDK de Python de banco de dados do Azure Cosmos](documentdb-sdk-python.md).

Para obter mais informações sobre o Azure, o Visual Studio e Python, consulte Olá [Central de desenvolvedores de Python](https://azure.microsoft.com/develop/python/). 

Para tutoriais do Python bulbo adicionais, consulte [Olá bulbo Mega-Tutorial, parte i: Olá, mundo!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
