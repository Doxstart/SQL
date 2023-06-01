# **Lezione su SQL del 30/05/2023 e 01/06/2023**

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

SELECT *  
FROM customers  
ORDER BY age ASC  
*Posso ordinare la tabella da maniera ascendente*   

SELECT *  
FROM customers  
ORDER BY age DESC  
*Posso ordinare la tabella da maniera discendente*  

SELECT *  
FROM customers  
ORDER BY last_name ASC, first_name  
*Ordino in sequenza, prima per cognome poi per nome*  

SELECT first_name, last_name  
FROM customers  
ORDER BY age  
*Ordina i clienti per età mostrando nome e cognome però senza displayare la età*  

SELECT first_name, last_name, age  
FROM customers  
ORDER BY age  
*Ordina i clienti per età mostrando nome, cognome ed età*

SELECT customer_id, amount  
FROM orders  
ORDER BY amount DESC  
*Ordino le ordini fatte dai clienti in ordine discendente mostrando l'id del cliente e soldi spessi*  

SELECT customer_id, amount  
FROM orders  
ORDER BY amount DESC  
LIMIT 3  
*Individuo i 3 clienti che hanno spesso di più, serve per mostrare i top 3 clienti*  

SELECT COUNT (*)  
FROM customers  
*Funzione di aggregazione, serve per contare tutti i clienti che ho nel database*  

SELECT COUNT (*)  
FROM customers  
WHERE country = 'USA'  
*Stampa la quantità di clienti che sono da USA*  

SELECT DISTINCT country  
FROM customers  
*Query per vedere tutti i paesi senza duplicati grazie al distinct*  

SELECT COUNT (DISTINCT country)  
FROM customers  
*Query per vedere il conteggio totale di paesi dei clienti senza duplicati*  

SELECT MAX (age)  
FROM customers    
*Seleziona il valore massimo di una colonna, in questo caso la età*  

SELECT first_name, MAX (age)  
FROM customers  
*Seleziona e mostra il cliente di maggiore età*  

SELECT AVG (amount)  
FROM orders  
*Calcola la media degli ordini*  

SELECT AVG (amount)  
FROM orders  
WHERE amount <= 300  
*Calcola la media degli ordini dove il risultato sia minore uguale a 300*  

SELECT *  
FROM orders  
ORDER BY amount DESC  
LIMIT 3  
*Seleziona i top 3 ordini che hanno spesso di più in ordine discendente*  

SELECT AVG (amount)  
FROM (  
   $~~~$ SELECT amount  
   $~~~$ FROM orders  
   $~~~$ ORDER BY amount DESC  
   $~~~$ LIMIT 3  
  );
  
  
SELECT amount  
FROM orders  
ORDER BY amount DESC  
LIMIT 3  
*Mostra la media e i top 3 clienti che hanno spesso di più*  

SELECT SUM (amount)  
FROM orders  
*Funzione di aggregazione per sommare le spesse di tutti gli ordini*  

SELECT SUM (amount)  
FROM orders  
WHERE customer_id = 2  
*Somma totale delle spesse fatte dal cliente con id 2*  

SELECT customer_id, SUM (amount)  
FROM orders  
GROUP BY customer_id  
*Mostra la somma dei clienti ordinandole per i suoi id*  

SELECT customer_id, SUM (amount) as total  
FROM orders  
GROUP BY customer_id  
ORDER BY total DESC  
LIMIT 3  
*as total è un alias che mi crea una colonna con il risultato delle somme totali e posso referenziarlo dopo*  

SELECT customer_id, SUM (amount) as total  
FROM orders  
GROUP BY customer_id  
HAVING total >= 700  
ORDER BY total DESC  
LIMIT 3  
*HAVING è un'alternativa al WHERE*    

Mostrare il nome e cognome di tutti i clienti la cui media di spesa è superiore alla media di spessa complessiva di tutti i clienti (ESERCIZIO)  

SELECT *  
FROM orders  
JOIN customers  
WHERE orders.customer_id = customers.customer_id  
*Esempio di Equi Join*  

SELECT *  
FROM orders o   
JOIN customers c  
WHERE o.customer_id = c.customer_id  
*o e c sono alias, posso anche scriverli senza il 'as'*  

SELECT c.customer_id, c.first_name, c.last_name, o.item, o.amount  
FROM orders o  
JOIN customers c  
WHERE o.customer_id = c.customer_id  
*Posso usare gli alias nel SELECT per essere più specifico*  

SELECT c.customer_id, c.first_name, c.last_name, o.item, o.amount  
FROM orders o  
JOIN customers c  
ON o.customer_id = c.customer_id  
*Alternativa a WHERE che è più veloce da esseguire*  

## Esempi DDL

ALTER TABLE shippings  
ADD COLUMN order_id integer  
*aggiungo una nuova colonna 'order_id' nella mia tabella shippings*  

UPDATE shippings  
SET order_id = customer  
*aggiorno la tabella shippings copiando i valori di order_id e incollandoli a customer*  

ALTER TABLE shippings  
DROP COLUMN customer  
*Cancello la colonna customer nella tabella shippings*  

SELECT *  
FROM shippings as s  
  
JOIN orders as o  
ON s.order_id = o.order_id   
  
JOIN customers as c  
ON o.customer_id = c.customer_id  
*Concatenazione di JOIN*  

SELECT c.customer_id, c.first_name, c.last_name, c.country, o.  item, o.amount, s.status  
FROM shippings as s  

JOIN orders as o  
ON s.order_id = o.order_id     

JOIN customers as c  
ON o.customer_id = c.customer_id  

WHERE c.country = 'USA'  
AND s.status = 'Pending'  
*Si deve tenere in conto l'ordine delle query*

LEFT JOIN shippings as s  
ON s.order_id = o.order_id    
*esempio LEFT JOIN*  

ORDER BY s.status NULLS FIRST;  
*Ordina i risultato mettendo come primo tutti i null*  

CREATE TABLE products (  
   $~~~$ product_id integer not null,  
   $~~~$ category varchar(250),  
   $~~~$ model integer not null,  
   $~~~$ name varchar(250) not null,  
   $~~~$ unit_price float not null,  
   $~~~$ is_available boolean not null,  
    
   $~~~$ primary key(product_id),  
   $~~~$ unique(name, model)  
 );  
 *Sintassi per creare tabelle nuove con tutti i campi, dati, tipi, chiavi primarie e secondarie*  

INSERT INTO products  
values(1, null, 'Ihone', 10, 800, true)  
*Inserisco i dati nella tabella appena creata*  

SELECT null, 'Computers', item, 1, amount, true  
FROM orders;  
*Altra maniera di aggiungere dati al mio elenco di prodotti*

INSERT INTO products(product_id, category, name, model, unit_price, is_available)  
SELECT DISTINCT null, 'Computers', item, 1, amount, true  
FROM orders;  
*Serve per importare dati di una tabella all'altra*  

ALTER TABLE orders  
ADD COLUMN product_id integer references products(product_id)  
*References serve per aggiungere la colonna di un'altra tabella in quella che ho bisogno specificandola*  
 