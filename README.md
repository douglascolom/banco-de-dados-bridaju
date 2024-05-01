# banco-de-dados-bridaju

Meu primeiro projeto de banco de dados pensado para atender um comércio

create schema bridaju;

use bridaju;

create table if not exists fornecedor (
	idfornecedor int auto_increment not null primary key,
	nomefornecedor varchar(50) not null,
	cnpj char(14) not null,
	contato varchar(60) not null,
 
	constraint uniquecnpj unique (cnpj),
    constraint unique_id_fornecedor unique (idfornecedor)
);

alter table suprimento add column codigo varchar(50);

create table if not  exists suprimento (
	idsuprimento int auto_increment not null primary key,
    nomesuprimento varchar(50) not null,
    codigo varchar(50),
    
    constraint unique_id_suprimentos unique (idsuprimento)

);


create table if not exists produto (
	idproduto int auto_increment not null primary key,
    nomeproduto varchar (50) not null,
    setor varchar(20),
    codigo varchar (25),
    
    constraint unique_id_produto unique (idproduto)
    
);

create table if not exists cliente (
	idcliente  int auto_increment not null primary key,
    nomecliente varchar(50),
    cpf char(11) not null,
    contato char (11),
    cidade varchar (40),
    rua varchar (50),
    numero varchar (20),
    cep char (8),
    
	constraint unique_id_cliente unique (idcliente)   

);


create table if not exists cupom (
	idcupom int auto_increment not null primary key,
    sujeito int,
    pedidocupom int,
    data date not null,
    valor double not null,
    posição enum('ENTRADA','SAIDA'),
    
    constraint fk_pedidocupom foreign key (pedidocupom) references pedido(idpedido),
    constraint fk_clientecupom foreign key (sujeito) references cliente(idcliente),
	constraint fk_fornecedorcupom foreign key (sujeito) references fornecedor(idfornecedor),
    constraint unique_id_cupom unique (idcupom)

);


create table if not exists pedido (
	idpedido int not null primary key auto_increment,
    itens int,
    itens2 int,
    quantidade int,
    
    constraint fk_itens foreign key (itens) references produto(idproduto),
	constraint fk_itens2 foreign key (itens2) references suprimento(idsuprimento)
 
);

create table if not exists receita (
	recproduto int not null,
    recsuprimento int not null,
    quantidade float not null,
    
    constraint fk_recproduto foreign key (recproduto) references produto(idproduto),
    constraint fk_recsuprimento foreign key (recsuprimento) references suprimento(idsuprimento)

);


create table if not exists mercado (
	fornecedormercado int not null,
    suprimentomercado int not null,
    
    constraint fk_mecfornecedor foreign key (fornecedormercado) references fornecedor(idfornecedor),
    constraint fk_mecsuprimento	foreign key (suprimentomercado) references suprimento(idsuprimento)

);

