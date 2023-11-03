Essa abstração funciona de modo semelhante ao controle de Exceptions no backend.

**Como usar:**
- injete o service `MensagensErros` no arquivo onde deseja capturar um erro.
- perceba a existência do método `disparaErro` nesse service. Esse método recebe um argumento obrigatório (`tipoErro`) e três opcionais (`tituloErro`, `mensagem`, `erro`). **Use-o quando notar que naquele ponto do código uma mensagem de erro deveria ser exibida para o usuário.**
- ao passar apenas o argumento `tipoErro`, uma mensagem pré-definida será exibida para o tipo de erro em questão.
- use o Enum de `assets/js/enum/CodigoErroEnum` para deixar a chamada do método `disparaErro` mais clara.
- caso queira especificar uma mensagem mais detalhada para o seu caso, você pode passar os parâmetros opcionais. Recomendado validar com alguém de UX antes.
- para adicionar um tipo de erro não tratado ao service `MensagensErros`, basta seguir o padrão e atualizar também o enum `CodigoErroEnum`.

**Observação:** com exceção dos erros do Keycloak, não há Interceptor para capturar e tratar erros automaticamente. Um tratamento sempre deve existir dentro dos `.catch` das requisições ou em pontos onde a possibilidade de erro for detectada. Fica a critério do desenvolvedor decidir quando usar ou um _Toaster_ com uma mensagem informando o que ocorreu ou a página de erro completa do módulo `MensagensErros`.

### disparaErro(tipoErro, tituloErro?, mensagem?, erro?)

| Argumento             | Descrição | Tipo | Obrigatório                |
| ----------------- | ----------- | ------------------- | ------------------- |
| `tipoErro` | Deve ser um dos tipos listados no enum `codigoErroEnum`, que por sua vez são códigos de erros HTTP.            | `int` | Sim
| `tituloErro` | Mensagem para informar o usuário o que aconteceu. | `string` | Não
| `mensagem` | Mensagem para sugerir alguma ação ao usuário. | `string` | Não
| `erro` | Título do código do erro HTTP, como `NÃO ENCONTRADO`, `ACESSO NEGADO`, etc. | `string` | Não