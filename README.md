# Documentação Formulários
## Descritivo funcional

 1. O usuário logado pode criar um formulário;

2. O formulário criado tem um ID único que pode ser acessado através de uma rota desprotegida, sem a necessidade de login, como em rotas de Signup e Login;
    1. Desse modo o formulário se torna facilmente plugável. Alternativamente, poderia ser criado um botão opcional que exige autenticação para acesso do formulário caso necessário.
	2. A autenticação poderia ser feita pela própria Smart ou futuramente por serviços externos (mediante avaliação técnica).

3. O usuário acessa o formulário através de sua url única e preenche de forma obrigatória o seu e-mail, para identificação;
	1. Caso o login para acessar o formulário seja obrigatório o campo de e-mail é preenchido automaticamente.

4. O usuário preenche o formulário, que tem suas respostas validadas e então está pronto para ser enviado.

5. O usuário logado pode acessar todas as respostas de seu formulário em tabela ou planilha;

6. O usuário logado pode acessar gráficos da distribuição de respostas para cada pergunta de seu formulário;

	1. Por exemplo, um gráfico de pizza que mostra a porcentagem total de "Sim" e de "Não", selecionados em uma pergunta do formulário. Cada pergunta do formulário teria um gráfico e, idealmente, cada tipo de pergunta teria um tipo de gráfico mais adequado para si, por exemplo, uma pergunta de texto livro talvez seja melhor representada por um gráfico de barras.

7. O usuário logado pode definir de forma opcional uma data de encerramento para o formulário na sua criação. Ex.: Formulário aceita respostas até 31/08/2023);
	1. O formulário atingindo a data limite passaria de `ATIVO` para `ENCERRADO`.

	2. Alternativamente haveria uma opção de inativar um formulário. O status `INATIVO` é conceitualmente diferente do `ENCERRADO` pois o primeiro considera que o formulário foi descartado indefinidamente, podendo ser revertido, e o segundo considera que o formulário foi concluído.

	3. Outra métrica possível para encerrar um formulário, caso seja da vontade de sue criador, seria o número de respostas. Ex: Formulário atingiu o número máximo de respostas [100].

## Descritivo técnico

### Criação de formulário:
1. Um **Formulário** é composto de uma ou mais **Questões**, cada **Questão** tem um **Tipo de Questão** e pode ter **Opções de Resposta**.

![a](https://i.ibb.co/3rXMQ7Q/Captura-de-tela-2023-08-10-155403.png)

2. Os Tipos de Questões são pré definidos (novos podem ser cadastrados futuramente) e são exibidos no Frontend para serem arrastados ao Formulário.

![a](https://i.ibb.co/dK3VT4G/Captura-de-tela-2023-08-10-160024.png)

3. Após arrastar o Tipo de Questão  para o Formulário devem ser cadastradas as Opções de Resposta caso hajam, título, definir se ela é read-only, required e etc.
2. Todas essas informações serão agrupadas de maneira estruturada em um JSON, enviadas ao Backend e tratadas para serem cadastradas no DB

### Acessando o formulário:
1. O Formulário criado será enviado pela API como um JSON que agrupa as questões e suas especificações e informações gerais do Formulário.
2. No Frontend a lista de questões do Formulário recebido será iterada de modo que para cada item na lista seja exibido um componente do Tipo de Questão adequado. Para cada Tipo de Questão seria feito um componente customizado.

![enter image description here](https://i.ibb.co/TbVFxvw/Captura-de-tela-2023-08-10-160646.png)

![](https://i.ibb.co/rk01WP3/Captura-de-tela-2023-08-10-161547.png)

3. As Questões seriam exibidas respeitando a ordem e a página na qual foram arrastadas na sua criação.

### Respondendo o formulário:

1.  Uma **Resposta** consiste em seu **Usuário**, sua **Questão** e seu valor. O conjunto de Respostas do conjunto de **Questões** de um **Formulário** são a resposta deste Formulário.

![](https://i.ibb.co/kcK9vcK/Captura-de-tela-2023-08-10-161813.png)

2. Antes de uma Resposta ser enviada ela é validada de acordo com o Tipo de Questão e Opções de Resposta, se houver.
3. As Respostas podem ser posteriormente acessadas através de tabela no Frontend, exportadas como planilha ou exibidas em gráficos.

![enter image description here](https://i.ibb.co/FbsjZTM/Captura-de-tela-2023-08-10-161213.png)

### DB Completo
![](https://i.ibb.co/2cZxwZ9/Diagrama-ER-DBMS-nota-o-UML.png)
