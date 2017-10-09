script de implantação de saudação vai ignorar a criação de um ambiente virtual Olá no Azure se detectar um ambiente virtual compatível já existe.  Isso pode acelerar consideravelmente a implantação.  Pacotes que já estão instalados serão ignorados pelo pip.

Em determinadas situações, convém excluir tooforce ambiente virtual.  Você vai querer toodo isso se você decidir tooinclude um ambiente virtual como parte do seu repositório.  Também convém toodo isso se precisar tooget rid de determinados pacotes ou testar alterações toorequirements.txt.

Há alguns Olá toomanage de opções ambiente virtual no Azure existente:

### <a name="option-1-use-ftp"></a>Opção 1: usar o FTP
Com um cliente FTP, conecte-se o servidor toohello e você será toodelete capaz de pasta de env de saudação.  Observe que alguns clientes FTP (como navegadores da web) podem ser somente leitura e não permitem toodelete pastas, portanto, será toouse de toomake-se de que um cliente FTP com esse recurso.  nome do host Olá FTP e usuário são exibidas na folha do seu aplicativo web em hello [Portal do Azure](https://portal.azure.com).

### <a name="option-2-toggle-runtime"></a>Opção 2: alternar o tempo de execução
Aqui está uma alternativa que aproveita o fato de saudação que o script de implantação Olá vai excluir a pasta de env hello quando ele não corresponde a versão desejada de saudação do Python.  Isso efetivamente excluir o ambiente existente do hello e criar um novo.

1. Opção tooa outra versão do Python (via runtime.txt ou hello **configurações de aplicativo** folha em Olá Portal do Azure)
2. use git push e faça algumas mudanças (ignore quaisquer eventuais erros de instalação de pip)
3. Alternar tooinitial back versão do Python
4. use git push e faça algumas mudanças novamente

### <a name="option-3-customize-deployment-script"></a>Opção 3: personalizar o script de implantação
Se você personalizou o script de implantação hello, você pode alterar Olá código em tooforce Deploy-pasta de env Olá toodelete.

