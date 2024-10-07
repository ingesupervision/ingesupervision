create database Ingesupervision;
use Ingesupervision
create table Proyecto(
cod_proyecto smallint not null,
nom_proyecto varchar(25) not null,
ini_proyecto date null,
direccion_proyecto varchar(100) not null,
director_proyecto varchar(80) null,
residente_proyecto varchar(80) not null,
constraint pk_proyecto primary key(cod_proyecto));

create table Supervisor(
mprof_supervisor varchar(25) not null,
nom_supervisor varchar(70) not null,
tel_supervisor bigint not null,
constraint pk_supervisor primary key(mprof_supervisor));

create table proyecto_supervisor(
cod_proyecto1 smallint not null,
mprof_supervisor1 varchar(25) not null,
constraint fk_proyecto1 foreign key(cod_proyecto1) references Proyecto(cod_proyecto),
constraint fk_supervisor foreign key(mprof_supervisor1) references Supervisor(mprof_supervisor));

create table Coordinador(
mprof_coord varchar(25) not null,
nom_coord varchar(70) not null,
tel_coord bigint not null,
constraint pk_coordinaror primary key(mprof_coord));

create table Supervisor_Coordinador(
mprof_coord1 varchar(25) not null,
mprof_supervisor2 varchar(25) not null,
constraint fk_coordinador foreign key(mprof_coord1) references Coordinador(mprof_coord),
constraint fk_supervisor2 foreign key(mprof_supervisor2) references Supervisor(mprof_supervisor));

create table Armazon(
numero_ar varchar(10) not null,
diam_ar decimal(4, 2)  not null,
cant_ar smallint not null,
Long_ar decimal(5, 2) not null,
DiamE_ar decimal(4, 2) null,
CantE_ar smallint null,
Observ_ar varchar(500),
constraint pk_armazon primary key(numero_ar));



create table Muestra(
Numero_Mu varchar(5) not null,
FechaVa_Mu date not null,
Fecha_F date not null,
ResTeo_Mu decimal(5,2) not null,
Res7D_Mu decimal(5,2) null,
Res28d_Mu decimal(5,2) not null,
Res56d_Mu decimal(5,2) not null,
Lab_Mu varchar(15) null,
ApNorma_Mu bit null,
constraint pk_muestra primary key(Numero_Mu));

create table Elemento(
cod_elem varchar(20) not null,
tipo_elem varchar(25) not null,
nivel_elem varchar(25) not null,
FechaIni_elem date null,
aprob_elem bit not null,
Ldisenador_elem bit null,
obsev_elem varchar(500) null,
numero_ar1 varchar(10) not null,
constraint pk_elemento primary key(cod_elem),
constraint fk_armazon foreign key(numero_ar1) references Armazon(numero_ar));

create table Elemento_Muestra(
cod_elem1 varchar(20) not null,
numero_mu1 varchar(5) not null,
constraint fk_elemento foreign key(cod_elem1) references Elemento(cod_elem),
constraint fk_muestra foreign key(numero_mu1) references Muestra(Numero_Mu));

create table Informe(
num_info tinyint not null,
fecha_info date not null,
supervisor varchar(25) not null,
coordinador varchar(25) not null,
proyecto smallint not null,
constraint pk_informe primary key(num_info),
constraint fk_supervisor1 foreign key(supervisor) references Supervisor(mprof_supervisor),
constraint fk_coordinador1 foreign key(coordinador) references Coordinador(mprof_coord),
constraint fk_proyecto2 foreign key(proyecto) references Proyecto(cod_proyecto));

create table Informe_elemento(
cod_elem2 varchar(20) not null,
num_info1 tinyint not null,
constraint fk_elemento1 foreign key(cod_elem2) references Elemento(cod_elem),
constraint fk_informe foreign key(num_info1) references Informe(num_info))


select * from Proyecto

insert into Proyecto values(12345,'Cedro_Azul','2023-03-01','Cl 37BSur #27a - 94','Jorge Oquendo','Maria Pulgarin')

select * from Supervisor

insert into Supervisor values('24567-82989407 ANT','Johana Zuluaga', 3018470923);

select * from Coordinador

insert into Coordinador values('49073-84073108 BOG', 'Juan David Lalinde', 3103458720);

select * from Supervisor_Coordinador

insert into Supervisor_Coordinador values('49073-84073108 BOG','24567-82989407 ANT');

select * from Armazon

insert into Armazon values('P05_C_F10',15.87,10,6.25,6.35,24,default);
insert into Armazon values('P05_C_E10',15.87,12,4.50,6.35,18,default);
insert into Armazon values('P05_V_A2',15.87,4,9.60,6.35,50,default);

select * from Muestra

insert into Muestra values('105','2024-08-26','2024-09-17',35,null,96.7,null,'ingeconcreto',1)
insert into Muestra values('110','2024-09-01','2024-09-28',35,null,104,null,'ingeconcreto',null)
insert into Muestra values('86','2024-06-10','2024-07-21',28,null,86.9,99.8,'ingeconcreto',null)

select * from Elemento

insert into Elemento values('Col_P5_F10','Columna','Piso 5',null,1,null,null,'P05_C_F10');
insert into Elemento values('Col_P5_E10','Columna','Piso 5','2024-09-01',0,null,null,'P05_C_E10');
insert into Elemento values('V_P5_A2','Viga','Piso 5','2024-06-10',1,null,'Testigo satisfactorio','P05_V_A2');

select * from Elemento_Muestra

insert into Elemento_Muestra values('Col_P5_F10','105')
insert into Elemento_Muestra values('Col_P5_E10','110')
insert into Elemento_Muestra values('V_P5_A2','86')

select * from Informe

insert into Informe values(54,'2024-10-07','24567-82989407 ANT','49073-84073108 BOG',12345)

select * from Informe_elemento
insert into Informe_elemento values('Col_P5_F10',54)
insert into Informe_elemento values('Col_P5_E10',54)
insert into Informe_elemento values('V_P5_A2',54)


exec sp_help Muestra