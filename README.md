# Cyber-Web
Trabalho sobre vulnerabilidades em aplicações web da matéria de Segurança Cibernética na Universidade Federal de São Carlos.

## Abordagem
A abordagem utilizada para a realização do trabalho foi explorar vulnerabilidades no site AltoroMutual (https://demo.testfire.net/index.jsp), que simula um um site de um banco, criado pela WatchFire (agora AppScan Standard) como uma aplicação web 'vulnerable-by-design', ou seja, que possui vulnarabilidades propositalmente para testes.

## Vulnerabilidades exploradas
1. **Cross-Site Scripting (XSS)**
2. **SQL Injection**

# **1. Cross-Site Scripting (XSS)**
A vulnerabilidade de Cross-Site Scripting (XSS) é uma vulnerabilidade de injeção de código que permite que um atacante execute scripts maliciosos em um aplicativo da web. Os atacantes podem usar essa vulnerabilidade para contornar as medidas de segurança do aplicativo da web. Os scripts maliciosos executados pelo navegador da vítima têm acesso a qualquer informação que o usuário tenha acesso. Essa vulnerabilidade pode permitir que um atacante altere a aparência da página, roube informações ou até mesmo controle o navegador da vítima.

*Tipos de XSS*

Existem três tipos de XSS:
1. **Reflected XSS**: O atacante envia um link malicioso para a vítima, que contém um script malicioso. Quando a vítima clica no link, o script é executado no navegador da vítima.
2. **Stored XSS**: O atacante envia um script malicioso para um site, que é armazenado em um banco de dados ou em um servidor. Quando a vítima acessa o site, o script é executado no navegador da vítima.
3. **DOM-based XSS**: O atacante injeta um script malicioso em um site, que não é enviado para o servidor. O script é executado no navegador da vítima.

**Reflected XSS**

O Reflected XSS é o tipo de XSS que foi explorado no site AltoroMutual. O site possui um campo de busca, onde o usuário pode buscar por um termo. O site então retorna uma página com os resultados da busca. O problema é que o site não valida o termo buscado, e simplesmente retorna o termo buscado na página de resultados. Isso permite que um atacante injete um script malicioso no termo buscado, que será executado no navegador da vítima.

#### Explorando a vulnerabilidade
Para explorar a vulnerabilidade, basta inserir um script malicioso no campo de busca. O script será executado na página de resultados. No exemplo abaixo, o script exibe um alerta com a mensagem "XSS":
![image](https://github.com/LuisLourenco1/Cyber-Web/assets/103335009/23c3ed7d-a58e-4161-aa08-c8e3b526f34f)

![image](https://github.com/LuisLourenco1/Cyber-Web/assets/103335009/c6a09f81-a100-4525-b559-26d8f7647f3a)

Outra aplicação desse ataque é redirecionar o usuário para uma página maliciosa. No exemplo abaixo, é inserido o script:

```
<a href="http://sitemalicioso.com"><p>Clique Aqui!</p>
```

Dessa forma, um atacante pode enganar uma vítima enviando a ela o link com essa query:

```
https://demo.testfire.net/search.jsp?query=<a+href%3D"http%3A%2F%2Fsitemalicioso.com"><p>Clique+Aqui%21<%2Fp>
```
![Explorando vulnerabilidade](https://github.com/LuisLourenco1/Cyber-Web/assets/99414301/2b7a0f5c-8fef-4b20-89c5-0ab7b0187b4d)

![image](https://github.com/LuisLourenco1/Cyber-Web/assets/103335009/c03693ca-46b2-4749-ba78-fbcc33648359)

Enganando a vítima para que ela clique no link, e seja redirecionada para o site malicioso.

# **2. SQL Injection**
O SQL Injection é uma vulnerabilidade que permite que um atacante execute comandos SQL maliciosos em um banco de dados. Essa vulnerabilidade pode permitir que um atacante acesse, modifique e exclua dados do banco de dados. Além disso, o atacante pode executar comandos do sistema operacional, como ler e gravar arquivos e executar programas.

#### Explorando a vulnerabilidade
Para explorar a vulnerabilidade, basta inserir um comando SQL malicioso no campo de busca. O site então retorna uma página com os resultados da busca. O problema é que o site não valida o termo buscado, e simplesmente retorna o termo buscado na página de resultados.

Nesse caso, para o campo de login e senha, é possível inserir o comando SQL:
![image](https://github.com/LuisLourenco1/Cyber-Web/assets/103335009/1df7367b-7727-4d35-bf6b-26493bd431d8)

```
'or 1=1--+
```

A query no processo de autenticação do usuário segue o seguinte formato:

```
SELECT * from users WHERE username = 'username' AND password = 'password'
```

- A aspa simples única é utiliza para delimitar o valor do campo
- A condição lógica 1=1 sempre é verdadeira
- O --+ é utilizado para comentar o restante da query, ignorando o valor do campo senha

Dessa forma, a query fica:
![image](https://github.com/LuisLourenco1/Cyber-Web/assets/103335009/98788b6b-9395-4661-90f8-61f7a95877ad)

Após o WHERE essa condição sempre será verdadeira e serão então retornados todos os usuários da tabela, sendo utilizado o primeiro na autentição, que costuma ser o administrador.

![image](https://github.com/LuisLourenco1/Cyber-Web/assets/103335009/3297afec-8323-439c-84b9-4cb1fe37e0ed)

É possível também, sabendo o nome de login de um usuário, é possível fazer login utilizando esse comando no campo de senha:
![image](https://github.com/LuisLourenco1/Cyber-Web/assets/103335009/2b30da36-b675-44f7-82b4-73378e774b72)

![image](https://github.com/LuisLourenco1/Cyber-Web/assets/103335009/ff6e6c6d-27f1-43e3-82ec-5141adb6e5c0)
