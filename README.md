# TP-Logico-Ajedrez-

casillero(F,C):- between(1,8,F), between(1,8,C).

% Diagonal descendente desde una casilla inicial 
	diagonalDescendente(FilInicial,ColInicial,Fil,Col):-
	casillero(FilInicial,ColInicial), casillero(Fil,Col),
	between(-8,8,D),
	Fil is FilInicial+D,
	Col is ColInicial+D.

% Diagonal ascendente desde una casilla inicial 
    diagonalAscendente(FilInicial,ColInicial,Fil,Col):-
	
	casillero(FilInicial,ColInicial), casillero(Fil,Col),
	between(-8,8,D),
	Fil is FilInicial+D,
	Col is ColInicial-D.

  

	casilleroSiguienteRey(FilInicial,ColInicial,Fil,Col):-
	
	casillero(FilInicial,ColInicial), casillero(Fil,Col),
	between(-1,1,D),
	Fil is FilInicial+D,
	Col is ColInicial+D.

	casilleroSiguienteTorre(FilInicial,ColInicial,Fil,Col):-
	
	casillero(FilInicial,ColInicial), casillero(Fil,Col),
	between(-8,8,D),
	Fil is FilInicial,
	Col is ColInicial+D.


	casilleroSiguienteTorre(FilInicial,ColInicial,Fil,Col):-
	
	casillero(FilInicial,ColInicial), casillero(Fil,Col),
	between(-8,8,D),
	Fil is FilInicial+D,
	Col is ColInicial.



igualdadCasilleros(F1,C1,F2,C2):-
F1 == F2,
C1 == C2.

amenaza(rey,F1,C1,F2,C2) :-
casilleroSiguienteRey(F1,C1,F2,C2),
not(igualdadCasilleros(F1,C1,F2,C2)).

amenaza(torre,F1,C1,F2,C2) :-
casilleroSiguienteTorre(F1,C1,F2,C2),
not(igualdadCasilleros(F1,C1,F2,C2)).

amenaza(alfil,F1,C1,F2,C2) :-
diagonalAscendente(F1,C1,F2,C2),
not(igualdadCasilleros(F1,C1,F2,C2)).

amenaza(alfil,F1,C1,F2,C2) :-
diagonalDescendente(F1,C1,F2,C2),
not(igualdadCasilleros(F1,C1,F2,C2)).

amenaza(reina,F1,C1,F2,C2) :-
amenaza(alfil,F1,C1,F2,C2).

amenaza(reina,F1,C1,F2,C2) :-
amenaza(torre,F1,C1,F2,C2).



casillerosAmenazados(Ficha,F,C,Casilleros) :-
findall(?,amenaza(Ficha,F,C,?),ListaAmenazados),
length(ListaAmenazados,Casilleros).


puedenEstar(Ficha1,F1,C1,Ficha2,F2,C2) :-
amenaza(Ficha1,_,_,_,_),
amenaza(Ficha2,_,_,_,_),
not(amenaza(Ficha1(F1,C1,F2,C2)),
not(amenaza(Ficha2(F2,C2,F1,C1)),
not(igualdadCasilleros(F1,C1,F2,C2)).






