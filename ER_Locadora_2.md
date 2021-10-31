|Esquema de Relação - Locadora de Veículos|
|-|
|CLIENTE (CPF) <br> CLIENTE (CPF) IS PRIMARY KEY|
|FUNCIONARIO (CPF, Tipo) <br> FUNCIONARIO (CPF) IS PRIMARY KEY|
|ATENDENTE (CPF, Taxa_Comissao) <br> ATENDENTE (CPF) IS PRIMARY KEY <br> ATENDENTE (CPF) REFERENCES FUNCIONARIO (CPF)|
|MECANICO (CPF) <br> MECANICO (CPF) IS PRIMARY KEY <br> MECANICO (CPF) REFERENCES FUNCIONARIO (CPF)|
|MODELO (Nome, Marca Taxa_Seg, Num_Lugares) <br> MODELO (Nome, Marca) IS PRIMARY KEY|
|VEICULO (Renavam, Placa, Custo_Loc, Preco_Vend, Preco_Comp, Data_Comp, Nome_Mod, Marca_Mod) <br> VEICULO (Renavam) IS PRIMARY KEY <br> VEICULO (Nome_Mod, Marca_Mod) REFERENCES MODELO (Nome, Marca)|
|ACESSORIO_INCLUSO (Renavam, Tipo) <br> ACESSORIO_INCLUSO (Renavam, Tipo) IS PRIMARY KEY <br> ACESSORIO_INCLUSO (Renavam) REFERENCES VEICULO (Renavam)|
|PLANO (Id, Tipo, Perc_Decrescimo) <br> PLANO (Id) IS PRIMARY KEY|
|DIAS_PLANO (Id_Plano, Dia) <br> DIAS_PLANO (Id_Plano, Dia) IS PRIMARY KEY <br> DIAS_PLANO (Id_Plano) REFERENCES PLANO (Id)|
|LOCACAO (Renavam, Data_Loc, Data_Dev_Estimada, Data_Dev_Real, Valor_Pago, CPF_Cliente, CPF_Atendente, Id_Plano) <br> LOCACAO (Renavam, Data_Loc) IS PRIMARY KEY <br> LOCACAO (Renavam) REFERENCES VEICULO (Renavam) <br> LOCACAO (CPF_Cliente) REFERENCES CLIENTE (CPF) <br> LOCACAO (CPF_Atendente) REFERENCES ATENDENTE (CPF) <br> LOCACAO (Id_Plano) REFERENCES PLANO (Id)|
|ACESSORIO_EXTRA (Id, Acrescimo, Tipo) <br> ACESSORIO_EXTRA (Id) IS PRIMARY KEY|
|INCLUIDO_EM (Id_aces, Renavam, Data_Loc) <br> INCLUIDO_EM (Id_aces, Renavam, Data_Loc) IS PRIMARY KEY <br> INCLUIDO_EM (Id_aces) REFERENCES ACESSORIO_EXTRA (Id) <br> INCLUIDO_EM (Renavam, Data_Loc) REFERENCES LOCACAO (Renavam, Data_Loc)|
|MANUTENCAO (Renavam, Data_Ini, Estado, Tipo, Custo, Data_Ter_Prevista, Data_Ter_Real, CPF_Mecanico) <br> MANUTENCAO (Renavam, Data_Ini) IS PRIMARY KEY <br> MANUTENCAO (Renavam) REFERENCES VEICULO (Renavam) <br> MANUTENCAO (CPF_Mecanico) REFERENCES MECANICO (CPF)|
|PECA (Num_Serie, Fabricante, Custo, Tipo, Renavam_Usada, Data_Ini_Usada) <br> PECA (Num_Serie) IS PRIMARY KEY <br> PECA (Renavam_Usada) REFERENCES VEICULO (RENAVAM) <br> PECA (Data_Ini_Usada) REFERENCES MANUTENCAO (Data_Ini)|
|MOTIVO (Id, Descricao) <br> MOTIVO (Id) IS PRIMARY KEY|
|DEVIDO_A (Renavam, Data_Ini, Id_Motivo) <br> DEVIDO_A (Renavam, Data_Ini, Id_Motivo) IS PRIMARY KEY <br> DEVIDO_A (Renavam) REFERENCES VEICULO (RENAVAM) <br> DEVIDO_A (Data_Ini) REFERENCES MANUTENCAO (Data_Ini) <br> DEVIDO_A (Id_Motivo) REFERENCES MOTIVO (Id)|
