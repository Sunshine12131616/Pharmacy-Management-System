# Pharmacy-Management-System
Database


CREATE TABLE Supplier(
    supplier_id NUMBER PRIMARY KEY,
    supplier_name VARCHAR2(100),
    phone VARCHAR2(20),
    address VARCHAR2(100)
);


CREATE TABLE Medicine(
    medicine_id NUMBER PRIMARY KEY,
    medicine_name VARCHAR2(100),
    category VARCHAR2(50),
    price NUMBER(10,2),
    stock NUMBER,
    supplier_id NUMBER
);


CREATE TABLE Customer(
    customer_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(100),
    phone VARCHAR2(20),
    address VARCHAR2(100)
);


CREATE TABLE Employee(
    employee_id NUMBER PRIMARY KEY,
    employee_name VARCHAR2(100),
    position VARCHAR2(50),
    salary NUMBER(10,2),
    phone VARCHAR2(20)
);


CREATE TABLE Sales(
    sale_id NUMBER PRIMARY KEY,
    sale_date DATE,
    total_amount NUMBER(10,2),
    employee_id NUMBER
);


CREATE TABLE Purchase_Details(
    customer_id NUMBER,
    medicine_id NUMBER,
    sale_id NUMBER,
    quantity NUMBER,
    purchase_date DATE
);



ALTER TABLE Medicine
ADD CONSTRAINT fk_medicine_supplier
FOREIGN KEY (supplier_id)
REFERENCES Supplier(supplier_id);


ALTER TABLE Sales
ADD CONSTRAINT fk_sales_employee
FOREIGN KEY (employee_id)
REFERENCES Employee(employee_id);


ALTER TABLE Purchase_Details
ADD CONSTRAINT fk_purchase_customer
FOREIGN KEY (customer_id)
REFERENCES Customer(customer_id);


ALTER TABLE Purchase_Details
ADD CONSTRAINT fk_purchase_medicine
FOREIGN KEY (medicine_id)
REFERENCES Medicine(medicine_id);


ALTER TABLE Purchase_Details
ADD CONSTRAINT fk_purchase_sale
FOREIGN KEY (sale_id)
REFERENCES Sales(sale_id);




INSERT INTO Supplier VALUES
(1, 'ABC Pharma', '01711111111', 'Dhaka');

INSERT INTO Supplier VALUES
(2, 'Square Pharma', '01822222222', 'Rajshahi');

INSERT INTO Supplier VALUES
(3, 'Beximco Pharma', '01933333333', 'Chittagong');

INSERT INTO Supplier VALUES
(4, 'Renata Pharma', '01644444444', 'Khulna');




INSERT INTO Medicine VALUES
(101, 'Napa', 'Tablet', 2.50, 500, 1);

INSERT INTO Medicine VALUES
(102, 'Seclo', 'Capsule', 8.00, 300, 2);

INSERT INTO Medicine VALUES
(103, 'Ace', 'Tablet', 5.00, 450, 3);

INSERT INTO Medicine VALUES
(104, 'DP Rose', 'Syrup', 120.00, 80, 4);

INSERT INTO Medicine VALUES
(105, 'Fexo', 'Tablet', 6.50, 250, 2);

INSERT INTO Medicine VALUES
(106, 'Omidon', 'Tablet', 3.50, 600, 1);



INSERT INTO Customer VALUES
(201, 'Rayhan', '01911111111', 'Dhaka');

INSERT INTO Customer VALUES
(202, 'Fardin', '01888888888', 'Madaripur');

INSERT INTO Customer VALUES
(203, 'Hasibur', '01755555555', 'Dhaka');

INSERT INTO Customer VALUES
(204, 'Shihab', '01666666666', 'Chittagong');




INSERT INTO Employee VALUES
(301, 'Ankan', 'Cashier', 25000, '01777777777');

INSERT INTO Employee VALUES
(302, 'Rafi', 'Manager', 45000, '01877777777');

INSERT INTO Employee VALUES
(303, 'Mim', 'Pharmacist', 35000, '01977777777');

INSERT INTO Employee VALUES
(304, 'Priya', 'Cashier', 28000, '01677777777');



INSERT INTO Sales VALUES
(401, TO_DATE('23-07-2026','DD-MM-YYYY'), 18.50, 301);

INSERT INTO Sales VALUES
(402, TO_DATE('24-07-2026','DD-MM-YYYY'), 120.00, 303);

INSERT INTO Sales VALUES
(403, TO_DATE('25-07-2026','DD-MM-YYYY'), 32.50, 301);

INSERT INTO Sales VALUES
(404, TO_DATE('26-07-2026','DD-MM-YYYY'), 16.00, 304);



INSERT INTO Purchase_Details VALUES
(201, 101, 401, 3,
 TO_DATE('23-07-2026','DD-MM-YYYY'));

INSERT INTO Purchase_Details VALUES
(202, 104, 402, 1,
 TO_DATE('24-07-2026','DD-MM-YYYY'));

INSERT INTO Purchase_Details VALUES
(203, 105, 403, 5,
 TO_DATE('25-07-2026','DD-MM-YYYY'));

INSERT INTO Purchase_Details VALUES
(204, 102, 404, 2,
 TO_DATE('26-07-2026','DD-MM-YYYY'));




COMMIT;


SELECT * FROM Supplier;

SELECT * FROM Medicine;

SELECT * FROM Customer;

SELECT * FROM Employee;

SELECT * FROM Sales;

SELECT * FROM Purchase_Details;




--  Price greater than 3 AND stock greater than 400 

SELECT *
FROM Medicine
WHERE price > 3
AND stock > 400;


-- Category is Tablet OR Capsule 

SELECT *
FROM Medicine
WHERE category = 'Tablet'
OR category = 'Capsule';


--Medicines except Napa 

SELECT *
FROM Medicine
WHERE NOT medicine_name = 'Napa';


-- Medicines with price greater than 5

SELECT medicine_name, price
FROM Medicine
WHERE price > 5;


-- Medicines with stock less than 400 

SELECT medicine_name, stock
FROM Medicine
WHERE stock < 400;






-- Show supplier names and customer names together 

SELECT supplier_name AS name
FROM Supplier
UNION
SELECT customer_name AS name
FROM Customer;


 -- Find names existing in both tables

SELECT supplier_name AS name
FROM Supplier
INTERSECT
SELECT customer_name AS name
FROM Customer;


--Find customers whose names are not in supplier names

SELECT customer_name AS name
FROM Customer
MINUS
SELECT supplier_name AS name
FROM Supplier;



SELECT medicine_name,
       price,
       stock,
       category
FROM Medicine
WHERE (price > 2 AND stock > 300)
OR category = 'Capsule';



SELECT medicine_name, price
FROM Medicine
WHERE NOT price > 5;



ALTER TABLE Medicine
ADD expiry_date DATE;




ALTER TABLE Medicine
RENAME COLUMN category TO medicine_category;



ALTER TABLE Medicine
DROP COLUMN expiry_date;




SELECT medicine_name, stock
FROM Medicine
WHERE stock < 300;



SELECT medicine_name, price, stock
FROM Medicine
WHERE price > 3
AND stock > 400;


SELECT medicine_name, medicine_category
FROM Medicine
WHERE medicine_category = 'Tablet'
OR medicine_category = 'Capsule';


SELECT medicine_name, price
FROM Medicine
WHERE NOT medicine_name = 'Napa';


SELECT medicine_name,
       price,
       stock,
       medicine_category
FROM Medicine
WHERE (price > 2 AND stock > 300)
OR medicine_category = 'Capsule';


SELECT medicine_name, price
FROM Medicine
WHERE NOT price > 5;



SELECT supplier_name FROM Supplier;


SELECT supplier_name AS person_name
FROM Supplier UNION
SELECT customer_name
FROM Customer;


SELECT supplier_name AS person_name
FROM Supplier UNION ALL
SELECT customer_name
FROM Customer;

SELECT supplier_name AS person_name
FROM Supplier INTERSECT
SELECT customer_name
FROM Customer;


SELECT customer_name AS person_name
FROM Customer MINUS
SELECT supplier_name
FROM Supplier;


SELECT
    employee_id,
    employee_name,
    position,
    salary
FROM Employee
WHERE salary > 25000
AND NOT position = 'Cashier';


SELECT
    employee_id,
    employee_name,
    position,
    salary
FROM Employee
WHERE position = 'Manager'
   OR (position = 'Pharmacist' AND salary > 30000)
   OR (position = 'Cashier' AND salary >= 28000);

  
   SELECT supplier_name AS person_name,
       'SUPPLIER' AS person_type
FROM Supplier
UNION
SELECT customer_name AS person_name,
       'CUSTOMER' AS person_type
FROM Customer;


SELECT
    medicine_name,
    price,
    'EXPENSIVE' AS status
FROM Medicine
WHERE price >= 5

UNION ALL

SELECT
    medicine_name,
    price,
    'HIGH STOCK' AS status
FROM Medicine
WHERE stock >= 500;


SELECT
    s.sale_id,
    s.sale_date,
    s.total_amount,
    e.employee_name,
    e.position
FROM Sales s
JOIN Employee e
ON s.employee_id = e.employee_id
WHERE s.total_amount > 20
AND e.position <> 'Cashier';



SELECT
    medicine_id,
    medicine_name,
    price,
    stock,
    'RESTOCK REQUIRED' AS stock_status
FROM Medicine
WHERE stock < 300
AND price > 5;



SELECT medicine_name, price
FROM Medicine
WHERE medicine_name LIKE '%o%'
AND price > 3;


SELECT customer_id, customer_name, address
FROM Customer
WHERE customer_name LIKE 'R%'
AND address = 'Dhaka';



SELECT customer_id, customer_name, phone
FROM Customer
WHERE phone IN (
    SELECT phone
    FROM Customer
    GROUP BY phone
    HAVING COUNT(*) = 1
);


SELECT medicine_name, supplier_id
FROM Medicine
WHERE supplier_id IN (
    SELECT supplier_id
    FROM Supplier
    WHERE address IN (
        SELECT address
        FROM Supplier
        GROUP BY address
        HAVING COUNT(*) = 1
    )
);



SELECT c.customer_id, c.customer_name
FROM Customer c
WHERE EXISTS (
    SELECT 1
    FROM Purchase_Details p
    WHERE p.customer_id = c.customer_id
    AND p.quantity >= 3
);


SELECT c.customer_id, c.customer_name
FROM Customer c
WHERE EXISTS (
    SELECT 1
    FROM Purchase_Details p
    JOIN Medicine m
        ON p.medicine_id = m.medicine_id
    WHERE p.customer_id = c.customer_id
    AND m.price > 5
);


SELECT c.customer_id, c.customer_name
FROM Customer c
WHERE EXISTS (
    SELECT 1
    FROM Purchase_Details p
    WHERE p.customer_id = c.customer_id
);


SELECT medicine_name, stock
FROM Medicine
WHERE stock > ALL (
    SELECT stock
    FROM Medicine
    WHERE stock < 100
);

SET SERVEROUTPUT ON;

DECLARE
    v_med_name   VARCHAR2(100) := 'Napa';
    v_price      NUMBER(10,2)  := 2.50;
    v_stock      NUMBER        := 500;
BEGIN
    DBMS_OUTPUT.PUT_LINE('=== Pharmacy Management System ===');
    DBMS_OUTPUT.PUT_LINE('Medicine Name : ' || v_med_name);
    DBMS_OUTPUT.PUT_LINE('Price         : ' || v_price || ' BDT');
    DBMS_OUTPUT.PUT_LINE('Current Stock : ' || v_stock);
END;
/

DECLARE
    v_name    Medicine.medicine_name%TYPE;
    v_price   Medicine.price%TYPE;
    v_stock   Medicine.stock%TYPE;
BEGIN
    SELECT medicine_name, price, stock
    INTO   v_name, v_price, v_stock
    FROM   Medicine
    WHERE  medicine_id = 101;

    DBMS_OUTPUT.PUT_LINE('Medicine : ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Price    : ' || v_price);
    DBMS_OUTPUT.PUT_LINE('Stock    : ' || v_stock);
END;
/

SET SERVEROUTPUT ON;

DECLARE
    v_med   Medicine%ROWTYPE;
BEGIN
    SELECT * 
    INTO v_med
    FROM Medicine
    WHERE medicine_id = 102;

    DBMS_OUTPUT.PUT_LINE('ID       : ' || v_med.medicine_id);
    DBMS_OUTPUT.PUT_LINE('Name     : ' || v_med.medicine_name);
    DBMS_OUTPUT.PUT_LINE('Category : ' || v_med.medicine_category);   -- এখানে ঠিক করা হয়েছে
    DBMS_OUTPUT.PUT_LINE('Price    : ' || v_med.price);
    DBMS_OUTPUT.PUT_LINE('Stock    : ' || v_med.stock);
    DBMS_OUTPUT.PUT_LINE('Supplier : ' || v_med.supplier_id);
END;
/

 ---------if/ELSE

SET SERVEROUTPUT ON;

DECLARE
    v_stock    NUMBER;
    v_status   VARCHAR2(50);
BEGIN
    SELECT stock INTO v_stock
    FROM Medicine
    WHERE medicine_id = 104;   -- DP Rose

    IF v_stock > 300 THEN
        v_status := 'Sufficient Stock';
    ELSIF v_stock BETWEEN 100 AND 300 THEN
        v_status := 'Medium Stock - Reorder Soon';
    ELSE
        v_status := 'Critical Stock - Order Immediately';
    END IF;

    DBMS_OUTPUT.PUT_LINE('Stock Status of DP Rose: ' || v_status);
END;
/


SET SERVEROUTPUT ON;

DECLARE
    TYPE med_name_tab IS TABLE OF VARCHAR2(100) INDEX BY PLS_INTEGER;
    v_names   med_name_tab;
    i         NUMBER := 1;
BEGIN
    FOR rec IN (SELECT medicine_name FROM Medicine ORDER BY medicine_id) LOOP
        v_names(i) := rec.medicine_name;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('=== All Medicines (Associative Array) ===');
    FOR j IN 1..v_names.COUNT LOOP
        DBMS_OUTPUT.PUT_LINE(j || '. ' || v_names(j));
    END LOOP;
END;
/

SET SERVEROUTPUT ON;

DECLARE
    TYPE med_varray IS VARRAY(10) OF VARCHAR2(100);
    v_meds   med_varray := med_varray('Napa', 'Seclo', 'Ace', 'DP Rose', 'Fexo', 'Omidon');
BEGIN
    DBMS_OUTPUT.PUT_LINE('=== Medicines using VARRAY ===');
    FOR i IN 1..v_meds.COUNT LOOP
        DBMS_OUTPUT.PUT_LINE(i || '. ' || v_meds(i));
    END LOOP;
END;
/
 ---loop
SET SERVEROUTPUT ON;

DECLARE
    i NUMBER := 1;
BEGIN
    LOOP
        DBMS_OUTPUT.PUT_LINE('Checking Medicine ID: ' || (100 + i));
        i := i + 1;
        EXIT WHEN i > 6;
    END LOOP;
END;
/
-----while

SET SERVEROUTPUT ON;

DECLARE
    i NUMBER := 1;
BEGIN
    WHILE i <= 6 LOOP
        DBMS_OUTPUT.PUT_LINE('Processing Medicine ' || i);
        i := i + 1;
    END LOOP;
END;
/

SET SERVEROUTPUT ON;

BEGIN
    FOR i IN 101..106 LOOP
        DBMS_OUTPUT.PUT_LINE('Medicine ID: ' || i);
    END LOOP;
END;
/
----new  medicine add 
SET SERVEROUTPUT ON;

DECLARE
    v_price   NUMBER;
BEGIN
    -- Intentionally wrong ID
    SELECT price INTO v_price
    FROM Medicine
    WHERE medicine_id = 999;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: Medicine not found!');
    WHEN ZERO_DIVIDE THEN
        DBMS_OUTPUT.PUT_LINE('Cannot divide by zero');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected Error: ' || SQLERRM);
END;
/

CREATE OR REPLACE PROCEDURE add_medicine (
    p_id         IN NUMBER,
    p_name       IN VARCHAR2,
    p_category   IN VARCHAR2,
    p_price      IN NUMBER,
    p_stock      IN NUMBER,
    p_supplier   IN NUMBER
)
IS
BEGIN
    INSERT INTO Medicine (medicine_id, medicine_name, medicine_category, price, stock, supplier_id)
    VALUES (p_id, p_name, p_category, p_price, p_stock, p_supplier);

    DBMS_OUTPUT.PUT_LINE('Medicine added successfully: ' || p_name);
EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        DBMS_OUTPUT.PUT_LINE('Error: Medicine ID already exists!');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/

-- Execute
EXEC add_medicine(107, 'Histacin', 'Tablet', 4.00, 350, 1);

----stock value calculate

CREATE OR REPLACE FUNCTION get_stock_value (p_med_id IN NUMBER)
RETURN NUMBER
IS
    v_value   NUMBER;
BEGIN
    SELECT price * stock
    INTO   v_value
    FROM   Medicine
    WHERE  medicine_id = p_med_id;

    RETURN v_value;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        RETURN 0;
END;
/

-- Use
SELECT medicine_name, get_stock_value(medicine_id) AS total_value
FROM Medicine;


---display all medicine(cursor use)
SET SERVEROUTPUT ON;

DECLARE
    CURSOR c_med IS
        SELECT medicine_id, medicine_name, medicine_category, price, stock
        FROM Medicine
        ORDER BY medicine_id;

    v_id        Medicine.medicine_id%TYPE;
    v_name      Medicine.medicine_name%TYPE;
    v_category  Medicine.medicine_category%TYPE;
    v_price     Medicine.price%TYPE;
    v_stock     Medicine.stock%TYPE;
BEGIN
    OPEN c_med;
    LOOP
        FETCH c_med INTO v_id, v_name, v_category, v_price, v_stock;
        EXIT WHEN c_med%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE(
            'ID: ' || v_id || 
            ' | Name: ' || v_name || 
            ' | Category: ' || v_category || 
            ' | Price: ' || v_price || 
            ' | Stock: ' || v_stock
        );
    END LOOP;
    CLOSE c_med;
END;
/



---- low stock alert
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE check_low_stock (p_threshold IN NUMBER DEFAULT 100)
IS
BEGIN
    DBMS_OUTPUT.PUT_LINE('=== Low Stock Alert (Threshold: ' || p_threshold || ') ===');
    
    FOR rec IN (
        SELECT medicine_name, stock
        FROM Medicine
        WHERE stock < p_threshold
    ) LOOP
        DBMS_OUTPUT.PUT_LINE(rec.medicine_name || ' → Only ' || rec.stock || ' left');
    END LOOP;
END;
/

EXEC check_low_stock(200);


---cus purchase His

SET SERVEROUTPUT ON;

DECLARE
    CURSOR c_purchase IS
        SELECT c.customer_name, m.medicine_name, pd.quantity, pd.purchase_date
        FROM Purchase_Details pd
        JOIN Customer c ON pd.customer_id = c.customer_id
        JOIN Medicine m ON pd.medicine_id = m.medicine_id
        ORDER BY pd.purchase_date;
BEGIN
    DBMS_OUTPUT.PUT_LINE('=== Customer Purchase History ===');
    FOR rec IN c_purchase LOOP
        DBMS_OUTPUT.PUT_LINE(
            rec.customer_name || ' bought ' || 
            rec.quantity || ' × ' || rec.medicine_name || 
            ' on ' || TO_CHAR(rec.purchase_date, 'DD-MM-YYYY')
        );
    END LOOP;
END;
/


---em total sale
CREATE OR REPLACE FUNCTION total_sales_by_employee (p_emp_id IN NUMBER)
RETURN NUMBER
IS
    v_total   NUMBER := 0;
BEGIN
    SELECT NVL(SUM(total_amount), 0)
    INTO   v_total
    FROM   Sales
    WHERE  employee_id = p_emp_id;

    RETURN v_total;
END;
/

-- Test
SET SERVEROUTPUT ON;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Ankan Total Sales : ' || total_sales_by_employee(301) || ' BDT');
    DBMS_OUTPUT.PUT_LINE('Mim Total Sales   : ' || total_sales_by_employee(303) || ' BDT');
    DBMS_OUTPUT.PUT_LINE('Priya Total Sales : ' || total_sales_by_employee(304) || ' BDT');
END;
/
