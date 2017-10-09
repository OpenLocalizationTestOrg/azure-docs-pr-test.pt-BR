Azure determinará a versão de saudação do Python toouse para seu ambiente virtual com hello prioridade a seguir:

1. versão especificada em runtime.txt na pasta raiz de saudação
2. versão especificada pela configuração de Python na configuração de aplicativo da web hello (Olá **configurações** > **configurações de aplicativo** folha para seu aplicativo web no hello Portal do Azure)
3. Python 2.7 é o padrão de saudação se Olá acima são especificados

Valores válidos para o conteúdo de saudação do 

    \runtime.txt

são:

* python-2.7
* python-3.4

Se versão micro hello (terceiro dígito) for especificado, ele será ignorado.

