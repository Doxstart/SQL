# **Lezione su SQL del 30/05/2023**

[sito web] : (https://www.programiz.com/sql/online-compiler/)

**SQL = Structured Query Language**  
**DQL = Data Query Language**  
**DML = Data Manipulation Language**  
**DDL = Data Definition Language**  

SELECT  
*Serve per scegliere la colonna o colonne*  
FROM  
*Serve per scegliere la tabella*  
WHERE  
*Serve per filtrare i dati di una riga*

## **Esempi SQL**

SELECT first_name, last_name *Posso scegliere tra 2 o più campi per richiamarli*  
FROM customers  

SELECT * *Asterisco sceglie tutti i campi*  
FROM customers   

SELECT country  *Scegliere la nazionalità*  
FROM customers  

SELECT *
FROM customers  
WHERE age >= 25   
*Serve per fare una richiesta dove la età sia maggiore e uguale a 25*  

SELECT *
FROM customers  
WHERE last_name = 'Doe'    
*Serve per selezionare il cognome dando il dato specifico*  

SELECT *  
FROM customers  
WHERE last_name like 'Doe'    
*like e come l'uguale, ci sono database che prendono anche "ilike"*  

SELECT *  
FROM customers  
WHERE last_name like '%oe%'  
*le percentuali (%) sevono per cercare dei caratteri specifici dentro la tabella*  

SELECT *  
FROM customers  
WHERE age >= 25  
AND country = 'USA'   
*AND è un booleano che serve per aggiungere un altra richiesta con più parametri*

SELECT *  
FROM customers  
WHERE age >= 25  
-- AND country = 'USA'  
*(--) serve per discriminare campi nella ricerca*  

SELECT *  
FROM customers  
WHERE age >= 25  
OR country = 'USA'    
*OR è un altro booleano per aggiungere parametri alla ricerca*  

SELECT *  
FROM customers  
WHERE NOT (age >= 25 OR country = 'USA')    
*Un'altra sintassi per discriminare campi*  

SELECT *  
FROM customers  
WHERE NOT country = 'USA';    
*(;) Serve per dichiarare la fine di una query*  

SELECT *  
FROM customers  
WHERE NOT country = 'USA';  

select * from orders  
*Comincia una nuova query dopo il (;)* 

--SELECT *  
--FROM customers  
--WHERE NOT country = 'USA';  
*(--) Serve per commentare le mie query*

select * from orders  
*Dichiarare che campi voglio discriminare*     

SELECT distinct item  
FROM orders  
WHERE amount > 300  
*distinct serve per discriminare i risultati ripetuti, può solo essere inserito nel SELECT*  

SELECT * FROM customers WHERE customer_id = 3  
select * from customers where customer_id = 3  
*Posso scrivere in maiuscolo o minuscolo, è lo stesso, posso anche concatenare i query in una sola riga*  

SELECT *   
FROM orders  
WHERE amount > 350;  

SELECT *   
FROM customers   
WHERE customer_id IN (3, 4, 1)  
*Posso esseguire 2 query insieme, IN mi serve per selezionare vari dati dalla tabella richiesta*  

SELECT *   
FROM customers   
WHERE customer_id IN (  
	$~~~$ SELECT customer_id  
  	$~~~$ FROM orders  
  	$~~~$ WHERE amount > 350  
);  
*Faccio una sottoquery*

SELECT item, amount  
FROM Orders WHERE customer_id IN (  
	$~~~$ SELECT customer_id  
  	$~~~$ FROM Customers  
  	$~~~$ WHERE country = 'UK'  
)  
*Query che serve per mostrare gli acquisti con rispettivi prezzi che hanno fatto clienti del Regno Unito*  

## Esempi DML  

INSERT ...   
*Serve per inserire dei valori*

INTO customers  
*Serve per selezionare la tabella*  

INSERT INTO customers  
VALUES(6, 'Walter', 'Paganini', 30, 'IT')  
*Inserisco i dati nella mia tabella specificata*

<span style="color: red">Error: UNIQUE constraint failed: Customers.customer_id</span>  
*Mi da errore perchè non posso assegnare valori nuovi a un id che non è vuoto*  

DELETE FROM customers  
*Con questo cancello la tabella intera*  

WHERE customer_id = 7  
*Cancello l'intera riga specificata dall'id*  

WHERE first_name = 'Walter'   
*Cancello l'intera riga specificata dall nome*  

INSERT INTO customers (customer_id, first_name, last_name, age, country)   
VALUES(7, 'Pierpaolo', 'Passolini', null, 'IT')  
*Posso lasciare una cella o dato vuoto con null*  

SELECT 3 + 5  
8  
*Posso fare calcoli con select, e gli stampa come se fosse un console.log*  

SELECT 5 = null  
5 = null  
*sintassi inutile*

SELECT null = null  
null = null  
*null è un valore sconosciuto, quindi non lo posso confrontare con un altro*  

SELECT null is null  
1  
*faccio il confronto con is e mi da 1 che in booleano è true*

SELECT 5 is null  
0  
*lo confronto è mi torna 0, cioè false*  

SELECT *  
FROM customers  
WHERE customer_id is null  
*Query per selezionare le colonne dove l'id è null o sconosciuto*  

SELECT *  
FROM customers  
WHERE customer_id is not null  
*Query per selezionare le colonne che non sono sconosciute o null*    

DELETE FROM customers  
WHERE customer_id is null  
*Cancello la riga intera dove l'id era null o vuota*  

UPDATE customers  
SET age = 24, first_name = 'Carlo'  
WHERE customer_id = 6  
*Sintassi per aggiornare/aggiungere i dati in una riga con i valori specificati*  

UPDATE Customers  
SET first_name = first_name || ' Giovanni'   
WHERE customer_id = 6  
*Posso concatenare string con (||) ed aggiungere un secondo nome alla cella specificata*  

