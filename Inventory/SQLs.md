```sql
# neue Gastnutzer  
SELECT YEAR(u.created_at) AS year, MONTH(u.created_at) AS month, COUNT(DISTINCT u.id) AS count  
FROM users as u  
    INNER JOIN notification_devices as nd ON u.id = nd.user_id  
WHERE  
    nd.type = 'bikemanager'  
    AND u.created_at >= '2023-01-01'  
    AND u.created_at <= '2023-12-31'  
    AND u.is_guest = 1  
GROUP BY year, month  
ORDER BY year, month;  
    # AND users.email like '%@%';  
  
# neue Bikes mit Vertrag  
SELECT YEAR(d.created_at) AS year, MONTH(d.created_at) AS month, COUNT(DISTINCT d.id) AS count  
FROM devices as d  
    INNER JOIN contracts AS c ON c.id = d.contract_id  
    INNER JOIN customers AS c2 ON c2.id = d.customer_id  
    INNER JOIN users AS u ON u.id = c2.user_id  
    INNER JOIN notification_devices nd on u.id = nd.user_id  
WHERE  
    nd.type = 'bikemanager'  
    AND d.legacy_id IS NULL  
    AND d.object_type = 'FAHRRAD'  
    AND d.created_at >= '2023-01-01'  
    AND d.created_at <= '2023-12-31'  
    # AND u.is_guest = 1  
GROUP BY year, month  
ORDER BY year, month;  
  
# neue Bikes ohne Vertrag  
SELECT YEAR(d.created_at) AS year, MONTH(d.created_at) AS month, COUNT(DISTINCT d.id) AS count  
FROM devices as d  
    LEFT JOIN contracts AS c ON c.id = d.contract_id  
    INNER JOIN customers AS c2 ON c2.id = d.customer_id  
    INNER JOIN users AS u ON u.id = c2.user_id  
    INNER JOIN notification_devices nd on u.id = nd.user_id  
WHERE  
    nd.type = 'bikemanager'  
    AND d.legacy_id IS NULL  
    AND d.object_type = 'FAHRRAD'  
    AND c.id IS NULL  
    AND d.created_at >= '2023-01-01'  
    AND d.created_at <= '2023-12-31'  
    # AND u.is_guest = 1  
GROUP BY year, month  
ORDER BY year, month;  
  
SELECT DISTINCT u.email, d.id, d.name  
FROM devices as d  
    LEFT JOIN contracts AS c ON c.id = d.contract_id  
    INNER JOIN customers AS c2 ON c2.id = d.customer_id  
    INNER JOIN users AS u ON u.id = c2.user_id  
    INNER JOIN notification_devices nd on u.id = nd.user_id  
WHERE  
    nd.type = 'bikemanager'  
    AND d.legacy_id IS NULL  
    AND d.object_type = 'FAHRRAD'  
    AND c.id IS NULL  
    AND d.created_at >= '2023-03-01'  
    AND d.created_at <= '2023-03-31';
```