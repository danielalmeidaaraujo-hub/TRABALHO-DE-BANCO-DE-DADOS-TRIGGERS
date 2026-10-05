# TRABALHO-DE-BANCO-DE-DADOS-TRIGGERS

CREATE TABLE produtos (
   id INT PRIMARY KEY AUTO_INCREMENT,
   nome VARCHAR(100),
   quantidade INT
);


CREATE TABLE historico_estoque (
   id INT PRIMARY KEY AUTO_INCREMENT,
   produto_id INT,
   quantidade_antiga INT,
   quantidade_nova INT,
   data_alteracao DATETIME
);


INSERT INTO produtos (nome, quantidade)
   VALUES("ALVEJANTE", 200),
         ("SABÃO", 200);


DELIMITER //

CREATE TRIGGER registrar_alteracao_estoque 
  AFTER UPDATE
  ON produtos 
  FOR EACH ROW 
BEGIN 
    INSERT INTO historico_estoque (
        produto_id, 
        quantidade_antiga, 
        quantidade_nova, 
        data_alteracao
    ) VALUES ( 
        NEW.id, 
        OLD.quantidade, 
        NEW.quantidade, 
        NOW() 
    );
END//

DELIMITER ;

UPDATE produtos SET quantidade = 864 WHERE nome = "ALVEJANTE";
UPDATE produtos SET quantidade = 300 WHERE nome = "SABÃO";
 SELECT * FROM produtos;
 SELECT * FROM historico_estoque;
