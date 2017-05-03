Respostas do Exercicio no arquivo "RespostaDas Perguntas.rtf"
Banco da Dados utilizado = MYSQL;
Visual Studio Enterprise 2017

Configurações de Conexão do banco de Dados:
Hostname:localhost
Port:3306
username:root
password=7431
nome do Banco: PedidoDrLavaTudo;

Script para gerar o Banco de Dados.

DROP DATABASE PedidoDrLavaTudo;
CREATE DATABASE PedidoDrLavaTudo;
USE PedidoDrLavaTudo;


CREATE TABLE IF NOT EXISTS CLIENTE
(
IdCliente int AUTO_INCREMENT PRIMARY KEY,
Nome VARCHAR(100),
INDEX(IdCliente)
);

CREATE TABLE IF NOT EXISTS FUNCIONARIO
(
IdFuncionario int AUTO_INCREMENT PRIMARY KEY,
Nome VARCHAR(100) NOT NULL,
DataContratacao datetime NOT NULL,
TipoFuncionario int NOT NULL,
INDEX(IdFuncionario)
);
set optimizer_switch='derived_merge=off';
CREATE TABLE IF NOT EXISTS PEDIDO
(
IdPedido int AUTO_INCREMENT PRIMARY KEY,
IdCliente int NOT NULL,
Situacao int NOT NULL,
Total decimal,
CONSTRAINT FK_Pedido_Cliente FOREIGN KEY(IdCliente)
REFERENCES CLIENTE(IdCliente),
INDEX(IdPedido)
);
set optimizer_switch='derived_merge=off';
CREATE TABLE IF NOT EXISTS PAGAMENTO
(
IdPagamento int AUTO_INCREMENT PRIMARY KEY,
IdPedido int NOT NULL,
TotalPagamento decimal,
TipoPagamento int NOT NULL,
DataPagamento datetime not null,
CONSTRAINT FK_Pagamento_Pedido FOREIGN KEY(IdPedido)
REFERENCES PEDIDO(IdPedido),
INDEX(IdPagamento)
);
set optimizer_switch='derived_merge=off';
CREATE TABLE IF NOT EXISTS TECNICO
(
IdTecnico INT AUTO_INCREMENT PRIMARY KEY,
IdFuncionario INT NOT NULL,
CONSTRAINT FK_Tecnico_Funcionario FOREIGN KEY(IdFuncionario)
REFERENCES FUNCIONARIO(IdFuncionario),
INDEX(IdTecnico)
);
set optimizer_switch='derived_merge=off';
CREATE TABLE IF NOT EXISTS ATENDENTE
(
IdAtendente INT AUTO_INCREMENT PRIMARY KEY,
IdFuncionario INT NOT NULL,
ValorComissao decimal,
CONSTRAINT FK_Atendente_Funcionario FOREIGN KEY(IdFuncionario)
REFERENCES FUNCIONARIO(IdFuncionario),
INDEX(IdAtendente)
);
set optimizer_switch='derived_merge=off';

CREATE TABLE IF NOT EXISTS AGENDAMENTO
(
IdAgendamento INT AUTO_INCREMENT PRIMARY KEY,
IdPedido int NOT NULL,
IdTecnico int NOT NULL,
DataAgendamento datetime NOT NULL,
CONSTRAINT FK_Agendamento_Pedido FOREIGN KEY(IdPedido)
REFERENCES PEDIDO(IdPedido),
CONSTRAINT FK_Agendamento_Tecnico FOREIGN KEY(IdTecnico)
REFERENCES TECNICO(IdTecnico),
INDEX(IdAgendamento)
);

set optimizer_switch='derived_merge=off';
CREATE TABLE IF NOT EXISTS SERVICO
(
IdServico INT AUTO_INCREMENT PRIMARY KEY,
IdAgendamento int NOT NULL,
IDSDESCRICAOSERVICO VARCHAR(100) NOT NULL,
Tempo int NOT NULL,
CONSTRAINT FK_Servico_Agendamento FOREIGN KEY(IdAgendamento)
REFERENCES AGENDAMENTO(IdAgendamento),
INDEX(IdServico)
);

set optimizer_switch='derived_merge=off';
CREATE TABLE IF NOT EXISTS DESCRICAOSERVICO
(
IdServico INT AUTO_INCREMENT PRIMARY KEY,
DescricaoServico VARCHAR(100) NOT NULL,
Tempo int NOT NULL,
INDEX(IdServico)
);

set optimizer_switch='derived_merge=off';

INSERT INTO `pedidodrlavatudo`.`descricaoservico` (`IdServico`, `DescricaoServico`, `Tempo`) VALUES ('1', 'Limpeza de sofá de 3 lugares', '35');
INSERT INTO `pedidodrlavatudo`.`descricaoservico` (`IdServico`, `DescricaoServico`, `Tempo`) VALUES ('2', 'Impermeabilização de sofá de 3 lugares', '25');
INSERT INTO `pedidodrlavatudo`.`descricaoservico` (`IdServico`, `DescricaoServico`, `Tempo`) VALUES ('3', 'Limpeza de 1 cadeira', '7');
INSERT INTO `pedidodrlavatudo`.`descricaoservico` (`IdServico`, `DescricaoServico`, `Tempo`) VALUES ('4', ' Impermeabilização de 1 cadeira', '3');
INSERT INTO `pedidodrlavatudo`.`descricaoservico` (`IdServico`, `DescricaoServico`, `Tempo`) VALUES ('5', 'Limpeza de 2 cadeiras','12');
INSERT INTO `pedidodrlavatudo`.`descricaoservico` (`IdServico`, `DescricaoServico`, `Tempo`) VALUES ('6', 'Impermeabilização de 2 cadeiras', '5');
INSERT INTO `pedidodrlavatudo`.`descricaoservico` (`IdServico`, `DescricaoServico`, `Tempo`) VALUES ('7', 'Limpeza de 1 m2 de carpete', '4');







