# Pizzas.
Na atividade a seguir, tem objetivo de demonstrar  o bancos de dados de uma pizzaria, conforme o modelo logico que foi usando como base para a montagem de cada etapa do bancos de dados.
Abaixo, vemos o modelo lógico, possuindo os principais dados para o restantes das informações, pizzas, ingredientes, receitas, etc... 

![image](https://github.com/WanderleiJullia/Pizzas.README/assets/144744092/15f43789-5f45-4208-89ee-3a7cc874170a)


## 2º Escreva o script SQL que cria o banco de dados;

``` SQL
Inserir o código aqui

    -- MySQL Workbench Forward Engineering
    
    SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
    SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
    SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='TRADITIONAL,ALLOW_INVALID_DATES';
    
    -- -----------------------------------------------------
    -- Schema mydb
    -- -----------------------------------------------------
    
    -- -----------------------------------------------------
    -- Schema mydb
    -- -----------------------------------------------------
    CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
    -- -----------------------------------------------------
    -- Schema aulasbd
    -- -----------------------------------------------------
    
    -- -----------------------------------------------------
    -- Schema aulasbd
    -- -----------------------------------------------------
    CREATE SCHEMA IF NOT EXISTS `aulasbd` DEFAULT CHARACTER SET utf8 ;
    USE `mydb` ;
    
    -- -----------------------------------------------------
    -- Table `mydb`.`Pizza`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `mydb`.`Pizza` (
      `id_Pizza` INT NOT NULL,
      `Sabor` VARCHAR(90) NULL,
      `Descricao` VARCHAR(100) NULL,
      `Preco` DECIMAL(10,2) NULL,
      `Tamanho` VARCHAR(90) NULL,
      `Material_emba` VARCHAR(70) NULL,
      `Tamanho_emba` VARCHAR(80) NULL,
      `Preco_emba` DECIMAL(9,2) NULL,
      PRIMARY KEY (`id_Pizza`),
      UNIQUE INDEX `id_Pizza_UNIQUE` (`id_Pizza` ASC))
    ENGINE = InnoDB;
    
    
    -- -----------------------------------------------------
    -- Table `mydb`.`Receita`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `mydb`.`Receita` (
      `id_ Receita` INT NOT NULL,
      `Instrucoes` VARCHAR(80) NULL,
      `Autor` VARCHAR(80) NULL,
      `Pizza_id_Pizza` INT NOT NULL,
      PRIMARY KEY (`id_ Receita`, `Pizza_id_Pizza`),
      INDEX `fk_Receita_Pizza_idx` (`Pizza_id_Pizza` ASC),
      CONSTRAINT `fk_Receita_Pizza`
        FOREIGN KEY (`Pizza_id_Pizza`)
        REFERENCES `mydb`.`Pizza` (`id_Pizza`)
        ON DELETE NO ACTION
        ON UPDATE NO ACTION)
    ENGINE = InnoDB;
    
    
    -- -----------------------------------------------------
    -- Table `mydb`.`Pizzaiolo`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `mydb`.`Pizzaiolo` (
      `id_Pizzaiolo` INT NOT NULL,
      `Nome` VARCHAR(45) NULL,
      `Salario` DECIMAL(10,5) NULL,
      PRIMARY KEY (`id_Pizzaiolo`))
    ENGINE = InnoDB;
    
    
    -- -----------------------------------------------------
    -- Table `mydb`.`Ingredientes`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `mydb`.`Ingredientes` (
      `Id_Ingredientes` INT NOT NULL,
      `Ingredientes` VARCHAR(45) NULL,
      PRIMARY KEY (`Id_Ingredientes`))
    ENGINE = InnoDB;
    
    
    -- -----------------------------------------------------
    -- Table `mydb`.`Pizzaiolo_has_Pizza`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `mydb`.`Pizzaiolo_has_Pizza` (
      `Pizzaiolo_id_Pizzaiolo` INT NOT NULL,
      `Pizza_id_Pizza` INT NOT NULL,
      PRIMARY KEY (`Pizzaiolo_id_Pizzaiolo`, `Pizza_id_Pizza`),
      INDEX `fk_Pizzaiolo_has_Pizza_Pizza1_idx` (`Pizza_id_Pizza` ASC),
      INDEX `fk_Pizzaiolo_has_Pizza_Pizzaiolo1_idx` (`Pizzaiolo_id_Pizzaiolo` ASC),
      CONSTRAINT `fk_Pizzaiolo_has_Pizza_Pizzaiolo1`
        FOREIGN KEY (`Pizzaiolo_id_Pizzaiolo`)
        REFERENCES `mydb`.`Pizzaiolo` (`id_Pizzaiolo`)
        ON DELETE NO ACTION
        ON UPDATE NO ACTION,
      CONSTRAINT `fk_Pizzaiolo_has_Pizza_Pizza1`
        FOREIGN KEY (`Pizza_id_Pizza`)
        REFERENCES `mydb`.`Pizza` (`id_Pizza`)
        ON DELETE NO ACTION
        ON UPDATE NO ACTION)
    ENGINE = InnoDB;
    
    
    -- -----------------------------------------------------
    -- Table `mydb`.`Ingredientes_has_Pizza`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `mydb`.`Ingredientes_has_Pizza` (
      `Ingredientes_Id_Ingredientes` INT NOT NULL,
      `Pizza_id_Pizza` INT NOT NULL,
      PRIMARY KEY (`Ingredientes_Id_Ingredientes`, `Pizza_id_Pizza`),
      INDEX `fk_Ingredientes_has_Pizza_Pizza1_idx` (`Pizza_id_Pizza` ASC),
      INDEX `fk_Ingredientes_has_Pizza_Ingredientes1_idx` (`Ingredientes_Id_Ingredientes` ASC),
      CONSTRAINT `fk_Ingredientes_has_Pizza_Ingredientes1`
        FOREIGN KEY (`Ingredientes_Id_Ingredientes`)
        REFERENCES `mydb`.`Ingredientes` (`Id_Ingredientes`)
        ON DELETE NO ACTION
        ON UPDATE NO ACTION,
      CONSTRAINT `fk_Ingredientes_has_Pizza_Pizza1`
        FOREIGN KEY (`Pizza_id_Pizza`)
        REFERENCES `mydb`.`Pizza` (`id_Pizza`)
        ON DELETE NO ACTION
        ON UPDATE NO ACTION)
    ENGINE = InnoDB;
    
    USE `aulasbd` ;
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`cidades`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`cidades` (
      `id` INT(11) NOT NULL,
      `nome` VARCHAR(60) NOT NULL,
      `populacao` INT(11) NULL DEFAULT NULL,
      PRIMARY KEY (`id`))
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`alunos`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`alunos` (
      `id` INT(11) NOT NULL,
      `nome` VARCHAR(60) NOT NULL,
      `data_nasc` DATE NULL DEFAULT NULL,
      `cidade_id` INT(11) NULL DEFAULT NULL,
      PRIMARY KEY (`id`),
      INDEX `cidade_id` (`cidade_id` ASC),
      CONSTRAINT `alunos_ibfk_1`
        FOREIGN KEY (`cidade_id`)
        REFERENCES `aulasbd`.`cidades` (`id`))
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`automoveis`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`automoveis` (
      `Nome_Monta` VARCHAR(200) NULL DEFAULT NULL,
      `Site` VARCHAR(200) NULL DEFAULT NULL,
      `Logotipo` VARCHAR(200) NULL DEFAULT NULL,
      `Placa` VARCHAR(200) NULL DEFAULT NULL,
      `Modelo` VARCHAR(200) NULL DEFAULT NULL,
      `Ano` INT(11) NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`autores`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`autores` (
      `Nome` VARCHAR(80) NULL DEFAULT NULL,
      `Data_nasc` DATE NULL DEFAULT NULL,
      `Nacionalidade` VARCHAR(80) NULL DEFAULT NULL,
      `Email` VARCHAR(50) NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`clientes`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`clientes` (
      `Nome` VARCHAR(50) NULL DEFAULT NULL,
      `CPF` VARCHAR(11) NULL DEFAULT NULL,
      `Email` VARCHAR(50) NULL DEFAULT NULL,
      `TEL` VARCHAR(30) NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`colaboradores`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`colaboradores` (
      `Nome` VARCHAR(150) NULL DEFAULT NULL,
      `ID` INT(11) NULL DEFAULT NULL,
      `CPF` VARCHAR(150) NULL DEFAULT NULL,
      `Cargo` VARCHAR(150) NULL DEFAULT NULL,
      `Salario` FLOAT NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`desenvolvedores`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`desenvolvedores` (
      `Nome` VARCHAR(80) NULL DEFAULT NULL,
      `CPF` VARCHAR(80) NULL DEFAULT NULL,
      `Data_Nasc` DATE NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`diretores`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`diretores` (
      `Nome` VARCHAR(2000) NULL DEFAULT NULL,
      `Data_Nasc` DATE NULL DEFAULT NULL,
      `Nacionalidade` VARCHAR(2000) NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`elenco`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`elenco` (
      `Nome` VARCHAR(2000) NULL DEFAULT NULL,
      `Data_Nasc` DATE NULL DEFAULT NULL,
      `Nacionalidade` VARCHAR(2000) NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`filme`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`filme` (
      `Titulo` VARCHAR(2000) NULL DEFAULT NULL,
      `Duração` INT(11) NULL DEFAULT NULL,
      `Idioma` VARCHAR(2000) NULL DEFAULT NULL,
      `Preço` DECIMAL(10,0) NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`livros`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`livros` (
      `Titulo` VARCHAR(80) NULL DEFAULT NULL,
      `Quan_pag` INT(11) NULL DEFAULT NULL,
      `Acabamento` VARCHAR(80) NULL DEFAULT NULL,
      `Editora` VARCHAR(100) NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`pets`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`pets` (
      `Nome` VARCHAR(50) NULL DEFAULT NULL,
      `Especie` VARCHAR(60) NULL DEFAULT NULL,
      `Nascimento` DATE NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`produtos`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`produtos` (
      `id_produto` INT(11) NOT NULL,
      `nome` VARCHAR(80) NOT NULL,
      `preco` DECIMAL(5,2) NOT NULL,
      `estoque` INT(11) NOT NULL,
      `perecivel` VARCHAR(80) NOT NULL,
      `marca` VARCHAR(60) NULL DEFAULT NULL,
      `nacionalidade` VARCHAR(60) NULL DEFAULT NULL,
      PRIMARY KEY (`id_produto`))
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`projetos`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`projetos` (
      `Nome` VARCHAR(80) NULL DEFAULT NULL,
      `Data_Lan` DATE NULL DEFAULT NULL,
      `Genero` VARCHAR(80) NULL DEFAULT NULL,
      `FaixaEtaria` VARCHAR(80) NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    -- -----------------------------------------------------
    -- Table `aulasbd`.`supermercado`
    -- -----------------------------------------------------
    CREATE TABLE IF NOT EXISTS `aulasbd`.`supermercado` (
      `Nome` VARCHAR(100) NULL DEFAULT NULL,
      `Preço` DECIMAL(10,0) NULL DEFAULT NULL,
      `Quant_Estoq` INT(11) NULL DEFAULT NULL,
      `Nome_Marca` VARCHAR(100) NULL DEFAULT NULL,
      `SAC` VARCHAR(2000) NULL DEFAULT NULL,
      `Nacionalidade` VARCHAR(2000) NULL DEFAULT NULL)
    ENGINE = InnoDB
    DEFAULT CHARACTER SET = utf8;
    
    
    SET SQL_MODE=@OLD_SQL_MODE;
    SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
    SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

``` 

## 3º Inserir dados nas tabelas (Pizza e Embalagem); 

![image](https://github.com/WanderleiJullia/Pizzas.README/assets/144744092/2c53a0d5-a661-453f-99f2-fe21b12f0745)

  ``` SQL
  Inserir o código aqui

    insert into pizza (id_Pizza, Sabor, Descricao, Preco, Tamanho, Material_emba, Tamanho_emba, Preco_emba) values (1,'Queijo', 'Pizza de Queijo', 30.05, 'Pequena', 'Papelao', 'Pequena', 9.60);
    insert into pizza (id_Pizza, Sabor, Descricao, Preco, Tamanho, Material_emba, Tamanho_emba, Preco_emba) values (2,'Frango', 'Pizza de Frango ', 50.90, 'Grande', 'Papelao', 'Grande', 15.80);
    insert into pizza (id_Pizza, Sabor, Descricao, Preco, Tamanho, Material_emba, Tamanho_emba, Preco_emba) values (3,'Atum', 'Pizza de Atum', 48.56, 'Media', 'Papelao', 'Media', 11.20);
    insert into pizza (id_Pizza, Sabor, Descricao, Preco, Tamanho, Material_emba, Tamanho_emba, Preco_emba) values (4,'Calabresa', 'Pizza de Calabresa', 98.80, 'Trem', 'Papelao', 'Big', 30.50);
  ``` 
      
## 4º Inserir dados de Ingredientes; 

![image](https://github.com/WanderleiJullia/Pizzas.README/assets/144744092/36fb3474-1c3c-44a0-8018-be5465610c4a)

``` SQL
Inserir o código aqui
    insert into ingredientes (Id_Ingredientes, Ingredientes) values (1, 'Queijo, Molho de tomate');
    insert into ingredientes (Id_Ingredientes, Ingredientes) values (2, 'Frango, Tomate, Cebola');
    insert into ingredientes (Id_Ingredientes, Ingredientes) values (3, 'Atum, Cebola, Queijo');
    insert into ingredientes (Id_Ingredientes, Ingredientes) values (4, 'Calabresa, Cebola');
``` 

## 5º Inserir dados de Pizzaiolo; 

![image](https://github.com/WanderleiJullia/Pizzas.README/assets/144744092/07cc0304-34aa-43ea-8ff7-55343f6625e9)

``` SQL
Inserir o código aqui 
    insert into pizzaiolo (id_Pizzaiolo, Nome, Salario) values (1, 'Paulo', 1.300);
    insert into pizzaiolo (id_Pizzaiolo, Nome, Salario) values (2, 'Jullia', 1.900);
    insert into pizzaiolo (id_Pizzaiolo, Nome, Salario) values (3, 'Guilherme', 2.000);
    insert into pizzaiolo (id_Pizzaiolo, Nome, Salario) values (4, 'Gustavo', 3.000);
``` 

## 6º Inserir Receita de cada pizza e o autor.

![image](https://github.com/WanderleiJullia/Pizzas.README/assets/144744092/722af6d4-485a-4eab-9c27-4ea45765fbd2)

``` SQL
Inserir o código aqui 
    insert into receita (Instrucoes, Autor, Pizza_id_Pizza) values ('Massa de Pizza, Queijo, Molho de tomate', 'Paulo', 1);
    insert into receita (Instrucoes, Autor, Pizza_id_Pizza) values ('Massa de Pizza, Frango, Milho, Tomate', 'Jullia', 2);
    insert into receita (Instrucoes, Autor, Pizza_id_Pizza) values ('Massa de Pizza, Atum, Queijo', 'Guilherme', 3);
    insert into receita (Instrucoes, Autor, Pizza_id_Pizza) values ('Massa de Pizza, Calabresa, Cebola', 'Gustavo', 4);
``` 

## EXERCICIOS. 

## Crie um relatório com todas as pizzas e os pizzaiolos aptos a produzi-las;

![image](https://github.com/WanderleiJullia/Pizzas.README/assets/144744092/6028e1ba-f3de-4ffd-91b4-f87272458c4e)

``` SQL
Inserir o código aqui  
    select pizza.sabor as Tab_SaborPizza, pizzaiolo.nome as pizzaiolo 
    from pizza 
    join pizzaiolo_has_pizza on Pizza.id_Pizza = pizzaiolo_has_pizza.Pizza_id_Pizza 
    join pizzaiolo on pizzaiolo_has_pizza.Pizzaiolo_id_Pizzaiolo  = Pizzaiolo.id_Pizzaiolo;
```

## Crie um relatório com todas as pizzas e seus ingredientes;

![image](https://github.com/WanderleiJullia/Pizzas.README/assets/144744092/12ddc2b9-e77f-4891-a89a-5ba0b0f314af)

``` SQL
Inserir o código aqui

    select 
    	pizza.sabor as sabor, 
       group_concat( ingredientes.ingredientes_pizza) as ingredientes
    from pizza join ingredientes_has_pizza on pizza.id_pizza =  ingredientes_has_pizza.pizza_id_pizza
    join ingredientes on ingredientes_has_pizza.ingredientes_id_ingredientes = ingredientes.id_ingredientes
    group by pizza.sabor;
``` 

## Crie um relatório com todos os ingredientes e as pizzas onde são utilizados;

![image](https://github.com/WanderleiJullia/Pizzas.README/assets/144744092/cb1e3d6e-4d1a-4d21-967f-e6ea9eb5815d)

```SQL
Inserir o código aqui
    select 
    	ingredientes.ingredientes_pizza as Ingredientes,
        group_concat(pizza.sabor) as Sabor
    from ingredientes join ingredientes_has_pizza on ingredientes.id_ingredientes =  ingredientes_has_pizza.ingredientes_id_ingredientes
    join pizza on ingredientes_has_pizza.pizza_id_pizza = pizza.id_pizza
    GROUP BY ingredientes.ingredientes_pizza;
``` 

## Crie um relatório com os sabores de todas as pizzas, o nome dos pizzaiolos queas fazem e as instruções para produzi-las.

![image](https://github.com/WanderleiJullia/Pizzas.README/assets/144744092/4603198b-05e7-42fa-9a5b-4b906e066d7a)

``` SQL
Inserir o código aqui 
    select 
    	ingredientes.ingredientes_pizza as Ingredientes,
        group_concat(pizza.sabor) as Sabor
    from ingredientes join ingredientes_has_pizza on ingredientes.id_ingredientes =  ingredientes_has_pizza.ingredientes_id_ingredientes
    join pizza on ingredientes_has_pizza.pizza_id_pizza = pizza.id_pizza
    GROUP BY ingredientes.ingredientes_pizza;
``` 

## Jullia Santos Wanderlei

Bancos de Dados 

    
