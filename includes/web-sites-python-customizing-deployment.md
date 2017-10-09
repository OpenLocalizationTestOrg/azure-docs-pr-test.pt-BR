O Azure determinará que o aplicativo usa Python **se estas duas condições forem verdadeiras**:

* arquivo Requirements.txt na pasta raiz de saudação
* qualquer arquivo py na pasta raiz de saudação ou um runtime.txt que especifica o python

Quando esse for o caso de Olá, ele usará um script de implantação específica do Python, que executa a sincronização de saudação padrão de arquivos, bem como as operações de Python adicionais, como:

* Gerenciamento automático do ambiente virtual
* Instalação de pacotes listados em requirements.txt usando o pip
* Criação de saudação apropriado Web. config com base em Olá selecionado versão do Python.
* Coletar arquivos estáticos para aplicativos Django

Você pode controlar determinados aspectos de etapas de implantação padrão de saudação sem ter toocustomize Olá script.

Se você quiser tooskip todas as etapas de implantação específica do Python, você pode criar esse arquivo vazio:

    \.skipPythonDeployment

Para obter mais controle sobre implantação, você pode substituir o script de implantação padrão de saudação criando Olá seguintes arquivos:

    \.deployment
    \deploy.cmd

Você pode usar o hello [interface de linha de comando do Azure] [ Azure command-line interface] toocreate arquivos de saudação.  Use este comando da pasta do projeto:

    azure site deploymentscript --python

Quando esses arquivos não existem, o Azure cria um script de implantação temporária e o executa.  É idêntico toohello criado com o comando Olá acima.

[Azure command-line interface]: http://azure.microsoft.com/downloads/
