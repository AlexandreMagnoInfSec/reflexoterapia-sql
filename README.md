# reflexoterapia-sql
reflexoterapia-sql
1 - insert.sql
2 - select.sql
3 - update_delete.sql
4 - README.md

-- Inserção de Clientes
INSERT INTO Cliente (id_cliente, nome, telefone)
VALUES
(1, 'Maria Oliveira', '12987654321'),
(2, 'João Silva', '12997531245'),
(3, 'Ana Costa', '12999223344');

-- Inserção de Sessões
INSERT INTO Sessao (id_sessao, id_cliente, data_sessao, duracao_min, observacoes)
VALUES
(1, 1, '2025-11-20', 60, 'Cliente ansiosa, tensão nos ombros'),
(2, 2, '2025-11-22', 50, 'Dor lombar e cansaço'),
(3, 3, '2025-11-25', 55, 'Estresse acumulado');

-- Inserção de Pontos Reflexos
INSERT INTO PontoReflexo (id_ponto, nome, localizacao)
VALUES
(1, 'Plexo Solar', 'Centro do pé'),
(2, 'Coluna Vertebral', 'Borda interna do pé'),
(3, 'Coração', 'Região esquerda do pé');

-- Inserção de Avaliações Emocionais
INSERT INTO AvaliacaoEmocional (id_avaliacao, id_sessao, emocao, intensidade)
VALUES
(1, 1, 'Ansiedade', 8),
(2, 2, 'Cansaço', 6),
(3, 3, 'Estresse', 7);

-- Ligação sessão -> ponto reflexo
INSERT INTO Sessao_PontoReflexo (id_sessao, id_ponto)
VALUES
(1, 1),
(1, 2),
(2, 2),
(3, 3);

-- 1. Listar todos os clientes em ordem alfabética
SELECT nome, telefone
FROM Cliente
ORDER BY nome ASC;

-- 2. Buscar sessões com duração maior que 50 minutos
SELECT id_sessao, id_cliente, duracao_min
FROM Sessao
WHERE duracao_min > 50;

-- 3. Ver avaliações emocionais com intensidade alta
SELECT emocao, intensidade
FROM AvaliacaoEmocional
WHERE intensidade >= 7
ORDER BY intensidade DESC;

-- 4. Sessões com seus respectivos clientes (JOIN)
SELECT c.nome AS cliente, s.data_sessao, s.observacoes
FROM Sessao s
JOIN Cliente c ON c.id_cliente = s.id_cliente;

-- 5. Pontos reflexos aplicados em cada sessão (JOIN)
SELECT s.id_sessao, p.nome AS ponto
FROM Sessao_PontoReflexo sp
JOIN Sessao s ON s.id_sessao = sp.id_sessao
JOIN PontoReflexo p ON p.id_ponto = sp.id_ponto;

-- UPDATEs
UPDATE Cliente
SET telefone = '12990001122'
WHERE id_cliente = 1;

UPDATE Sessao
SET duracao_min = 65
WHERE id_sessao = 1;

UPDATE AvaliacaoEmocional
SET intensidade = 5
WHERE id_avaliacao = 2;

-- DELETEs
DELETE FROM Sessao_PontoReflexo
WHERE id_sessao = 2;

DELETE FROM AvaliacaoEmocional
WHERE id_avaliacao = 3;

DELETE FROM Cliente
WHERE id_cliente = 3;

