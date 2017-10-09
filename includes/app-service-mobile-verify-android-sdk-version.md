Por causa de desenvolvimento contínuo, versão do SDK do Android Olá instalado no Android Studio pode não corresponder versão Olá no código de saudação. Olá Android SDK referenciado neste tutorial é Olá 23, da versão mais recente no momento de saudação de gravação. número de versão de Hello pode aumentar como novas versões do hello SDK aparecem e é recomendável usar a versão mais recente da saudação disponível.

Dois sintomas da incompatibilidade de versão são:

- Quando você compilar ou recompilar o projeto hello, você pode receber mensagens de erro do Gradle como "**falha toofind destino Google Inc.:Google APIs:n**".
- Os objetos Android padrão no código que deve ser resolvido com base em instruções `import` podem gerar mensagens de erro.

Se qualquer uma delas for exibida, versão Olá Olá Android SDK instalado no Android Studio pode não corresponder o destino do SDK de saudação do projeto Olá baixado. versão de hello tooverify, fazer Olá as seguintes alterações:

1. No Android Studio, clique em **Ferramentas** > **Android** > **Gerenciador de SDK**. Se você não tiver instalado a versão mais recente de saudação do hello Platform SDK, em seguida, clique em tooinstall-lo. Anote o número de versão hello.
2. Em Olá **Explorador de projeto** guia em **Gradle Scripts**, abra arquivo hello **gradle (modeule: aplicativo)**. Certifique-se de que Olá **compileSdkVersion** e **buildToolsVersion** são definidos toohello versão do SDK mais recente instalado. marcas de saudação podem ter esta aparência:

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. No hello Android Studio Explorador de projeto, nó de projeto de saudação com o botão direito, escolha **propriedades**e na coluna esquerda Olá escolha **Android**. Certifique-se de que Olá **destino de compilação de projeto** está definida toohello mesma versão do SDK Olá **targetSdkVersion**.

No Android Studio, o arquivo de manifesto Olá não é destino de saudação toospecify usado SDK e versão mínima do SDK, ao contrário do caso de Olá com o Eclipse.
