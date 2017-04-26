# MVC - Teoria

O Zend framework 1 trabalha com o conceito de MVC tradicional, onde as camadas são controller, view e model;

A camada de controle é obrigatória, logo você sempre terá ao menos um controller;
As outras camadas são opcionais, por exemplo, você pode retornar um JSON diretamente do controller sem a necessidade de criar uma view; Ou processar o negócio direto no controller;

Abaixo a imagem que demonstra o fluxo da requisição:

![Zend Framework Dispatch Process](/zend dispatch process.png)
