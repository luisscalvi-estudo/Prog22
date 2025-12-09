# Projeto Integrador

## Requisitos

- Node.js (versão >= 18)
- npm ou yarn
- Banco de dados PostgreSQL 

Bibliotecas utilizadas:

Front-end:
- react
- react-dom
- axios
- react-router-dom
- @mui/material
- @mui/icons-material
- @fullcalendar/react
- @fullcalendar/daygrid
- @fullcalendar/interaction

Back-end:
- express
- mysql2
- cors
- dotenv
- bcrypt
- jsonwebtoken

Banco de Dados:

CREATE TABLE usuario (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    senha TEXT NOT NULL
);

CREATE TABLE permissao (
    id BIGINT PRIMARY KEY,
    descricao VARCHAR NOT NULL
);

CREATE TABLE usuario_permissao (
    email VARCHAR NOT NULL,
    id_permissao BIGINT NOT NULL,
    PRIMARY KEY (email, id_permissao),
    FOREIGN KEY (email) REFERENCES usuario (email),
    FOREIGN KEY (id_permissao) REFERENCES permissao (id)
);

CREATE TABLE procedimentos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(150) NOT NULL,
    valor NUMERIC(10,2),
    duracao_minutos INTEGER
);

CREATE TABLE pacientes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(150) NOT NULL,
    telefone VARCHAR(30),
    email VARCHAR(150),
    criado_em TIMESTAMP DEFAULT NOW(),
    cpf VARCHAR(14) UNIQUE
);

CREATE TABLE agendamentos (
    id SERIAL PRIMARY KEY,
    paciente_id INTEGER,
    procedimento_id INTEGER,
    data_hora TIMESTAMP NOT NULL,
    status VARCHAR(50),
    observacoes TEXT,
    usuario_id INTEGER NOT NULL,
    
    FOREIGN KEY (paciente_id) REFERENCES pacientes(id),
    FOREIGN KEY (procedimento_id) REFERENCES procedimentos(id),
    FOREIGN KEY (usuario_id) REFERENCES usuario(id) ON DELETE CASCADE
);

INSERT INTO permissao (id, descricao) VALUES (1, 'VIZUALIZAR_PROCEDIMENTO');
INSERT INTO permissao (id, descricao) VALUES (2, 'VIZUALIZAR_PACIENTE');
INSERT INTO permissao (id, descricao) VALUES (3, 'VIZUALIZAR_DASH');


INSERT INTO usuario_permissao (email, id_permissao) VALUES
('laura@eduarda.com', 1);


INSERT INTO usuario_permissao (email, id_permissao) VALUES
('laura@eduarda.com', 2);

INSERT INTO usuario_permissao (email, id_permissao) VALUES
('laura@eduarda.com', 3);

INSERT INTO pacientes (nome, telefone, email, cpf) VALUES
('Carlos Almeida', '11987654321', 'carlos@gmail.com', '123.456.789-00'),
('Fernanda Costa', '11999998888', 'fernanda@gmail.com', '987.654.321-00'),
('Paula Martins', '11911112222', 'paula@gmail.com', '111.222.333-44');

INSERT INTO procedimentos (nome, valor, duracao_minutos) VALUES
('Limpeza Dental', 150.00, 40),
('Clareamento', 600.00, 90),
('Restauração', 250.00, 50);

INSERT INTO agendamentos (paciente_id, procedimento_id, data_hora, status, observacoes, usuario_id)
VALUES
(1, 1, '2025-12-20 09:00:00', 'AGENDADO', 'Primeira consulta.', 1),
(2, 2, '2025-12-1 14:30:00', 'AGENDADO', NULL, 2),
(3, 3, '2025-01-5 11:00:00', 'CONFIRMADO', 'Paciente já realizou avaliação.', 2),
(1, 1, '2025-12-2 09:00:00', 'concluido', 'Primeira consulta.', 1),
(2, 2, '2025-12-3 14:30:00', 'pago', NULL, 2),
(3, 3, '2025-12-4 11:00:00', 'pago', 'Paciente já realizou avaliação.', 2);





