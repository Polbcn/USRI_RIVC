
DEF ACT 1, M_IN(19)=1 GOSUB *parar_carton,S ' Definimos interripcion cinta carton
DEF ACT 2, M_IN(20)=1 GOSUB *parar_plastico,S ' Definimos interripcion cinta plastico
DEF ACT 3, M_IN(21)=1 GOSUB *parar_manzana,S ' Definimos interripcion cinta manzanas
DEF PLT 1, P1, P2, P3, P4,6, 3, 2 ' palet 1
DEF PLT 2, P5, P6, P7, P8, 7, 2, 2 ' palet 2
'movemos las cajas de carton y plastico en las cintas a la vez
ACT 1= 1
ACT 2= 1
M_OUT(29) = 1
M_OUT(30) = 1
WAIT M_IN(19) = 1 ' NOS ASEGURAMOS A QUE LLEGUE LA CAJA DE CARTON
WAIT M_IN(20) = 1 ' NOS ASEGURAMOS A QUE LLEGUE LA CAJA DE PLASTICO
' colocamos caja carton en caja de caja plastico
HOPEN 1
MOV PCARTONLAT ' nos movemos en separacion lateral de la caja de carton
MVS PCARTON ' introducimos la pinza en la caja de carton
HCLOSE 1
DLY 1
MOV PPLAST, -20
MVS PPLAST
'COLOCACION MANZANAS
ACT 3=1
M_OUT(31) = 1 ' movimiento inicial cinta manzanas
WAIT M_IN(21) = 1

'COLUMNA 1 (PLT 1)
FOR M1=1 TO 6
WAIT M_IN(21) = 1
GOTO *pick
ACT 3=1
M_OUT(31) = 1
PPLACE = (PLT 1, M1)
GOTO *place
NEXT

'COLUMNA 2 (PLT 2)
FOR M1=1 TO 7
WAIT M_IN(21) = 1
GOTO *pick
ACT 3=1
M_OUT(31) = 1
PPLACE = (PLT 1, M1)
GOTO *place
NEXT

'COLUMNA 3 (PLT 1)
FOR M1=7 TO 12
WAIT M_IN(21) = 1
GOTO *pick
ACT 3=1
M_OUT(31) = 1
PPLACE = (PLT 1, M1)
GOTO *place
NEXT

'COLUMNA 4 (PLT 2)
FOR M1=8 TO 14
WAIT M_IN(21) = 1
GOTO *pick
ACT 3=1
M_OUT(31) = 1
PPLACE = (PLT 1, M1)
GOTO *place
NEXT

'COLUMNA 5 (PLT 1)
FOR M1=13 TO 18
WAIT M_IN(21) = 1
GOTO *pick
ACT 3=1
M_OUT(31) = 1
PPLACE = (PLT 1, M1)
GOTO *place
NEXT

'MUEVO EL CONJUNTO CAJA PLASTICO, CON CARTON LLENO DE MANZANAS HACIA LA SIGUIENTE ESTACION
M_OUT(30) = 1
WAIT M_IN(20) = 0 ' CUANDO YA NO LA DETECTO, VUELVO A EMPEZAR EL CICLO DE ESTA ESTACION
END

*pick ' Subrutina PICK
OVRD 100
MOV PCINTA, 20
OVRD 20
MVS PCINTA
HCLOSE 1
DLY 1
MVS PCINTA, 20
OVRD 100
RETURN

*place
OVRD 100
MOV PPLACE, 20
OVRD 20
MVS PPLACE
HOPEN 1
DLY 1
MVS PPLACE, 20
OVRD 100
RETURN


*parar_carton
M_OUT(29)=0 ' parar cinta
ACT 1=0 ' inhabilitar interrupcion
RETURN ' continuacion del programa

*parar_plastico
M_OUT(30)=0 ' parar cinta
ACT 2=0 ' inhabilitar interrupcion
RETURN ' continuacion del programa

*parar_manzana
M_OUT(31)=0 ' parar cinta
ACT 3=0 ' inhabilitar interrupcion
RETURN 0 ' continuacion del programa