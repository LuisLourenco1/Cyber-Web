# Cyber-Web
Trabalho sobre vulnerabilidades em aplicações web da matéria de Segurança Cibernética na Universidade Federal de São Carlos.

## Abordagem
A abordagem utilizada para a realização do trabalho foi explorar vulnerabilidades no site AltoroMutual (https://demo.testfire.net/index.jsp), que simula um um site de um banco, criado pela WatchFire (agora AppScan Standard) como uma aplicação web 'vulnerable-by-design', ou seja, que possui vulnarabilidades propositalmente para testes.

## Vulnerabilidades exploradas
1. Cross-Site Scripting (XSS)
2. SQL Injection
3. 

# **1. Cross-Site Scripting (XSS)**
A vulnerabilidade de Cross-Site Scripting (XSS) é uma vulnerabilidade de injeção de código que permite que um atacante execute scripts maliciosos em um aplicativo da web. Os atacantes podem usar essa vulnerabilidade para contornar as medidas de segurança do aplicativo da web. Os scripts maliciosos executados pelo navegador da vítima têm acesso a qualquer informação que o usuário tenha acesso. Essa vulnerabilidade pode permitir que um atacante altere a aparência da página, roube informações ou até mesmo controle o navegador da vítima.

## Tipos de XSS
Existem três tipos de XSS:
1. **Reflected XSS**: O atacante envia um link malicioso para a vítima, que contém um script malicioso. Quando a vítima clica no link, o script é executado no navegador da vítima.
2. **Stored XSS**: O atacante envia um script malicioso para um site, que é armazenado em um banco de dados ou em um servidor. Quando a vítima acessa o site, o script é executado no navegador da vítima.
3. **DOM-based XSS**: O atacante injeta um script malicioso em um site, que não é enviado para o servidor. O script é executado no navegador da vítima.

## Reflected XSS
O Reflected XSS é o tipo de XSS que foi explorado no site AltoroMutual. O site possui um campo de busca, onde o usuário pode buscar por um termo. O site então retorna uma página com os resultados da busca. O problema é que o site não valida o termo buscado, e simplesmente retorna o termo buscado na página de resultados. Isso permite que um atacante injete um script malicioso no termo buscado, que será executado no navegador da vítima.

## Explorando a vulnerabilidade
Para explorar a vulnerabilidade, basta inserir um script malicioso no campo de busca. O script será executado na página de resultados. No exemplo abaixo, o script exibe um alerta com a mensagem "XSS":

Outra aplicação desse ataque é redirecionar o usuário para uma página maliciosa. No exemplo abaixo, é inserido o script:

```
<a href="http://sitemalicioso.com"><p>Clique Aqui!</p>
```

Dessa forma, um atacante pode enganar uma vítima enviando a ela o link com essa query:

```
https://demo.testfire.net/search.jsp?query=<a+href%3D"http%3A%2F%2Fsitemalicioso.com"><p>Clique+Aqui%21<%2Fp>
```

Enganando a vítima para que ela clique no link, e seja redirecionada para o site malicioso.

# **2. **
