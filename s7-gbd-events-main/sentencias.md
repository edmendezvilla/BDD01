 1.-El numero total de facturas realizadas por cada cliente.
          nombre_cliente | direccion | nro_facturas
SELECT c.full_name AS nombre_cliente, c.address AS direccion, 
       (SELECT COUNT(*) FROM invoice WHERE client_id = c.id) AS nro_facturas
FROM client c;
<img src="![alt text](image-1.png)" 

2.-Listar nombre y correo de los clientes junto a su compra mas cara realizada.
          nombres |  correo   | total_mas_alto
SELECT c.full_name AS nombres, c.email AS correo, MAX(i.total) AS total_mas_alto
FROM client c
JOIN invoice i ON c.id = i.client_id
GROUP BY c.full_name, c.email;
<img src="![alt text](image.png)" 

3.-Listar las facturas donde sus totales sean mayores al promedio de las facturas
          fecha_factura | total
SELECT fecha_factura, total
FROM invoice
WHERE total > (SELECT AVG(total) FROM invoice);
<img src="![alt text](image-2.png)" 

4.- DB EVENT

Crear dos ejemplo con la base de datos event. Uno con subconsulta en SELECT y otro con subconsulta  en WHERESELECT
    c.title AS conference_title,
    (
        SELECT string_agg(m.first_name || ' ' || m.last_name, ', ')
        FROM registrations r
        JOIN members m ON r.member_id = m.member_id
        WHERE r.conference_id = c.event_id
    ) AS member_names
FROM
    conferences c;

<img src="![alt text](image-3.png)" 

WHERE
SELECT
    c.title AS conference_title,
    c.speaker,
    c.date
FROM
    conferences c
WHERE
    EXISTS (
        SELECT 1
        FROM registrations r
        WHERE r.conference_id = c.event_id
    );


<img src="![alt text](image-4.png)"

