
아래와 같이사용한다.
```sql
INSERT INTO cats(name, age)
VALUES('taco', 14)
```


-- Drop the current cats table (if you have one)

`DROP TABLE cats;`
  

-- Create the new cats table: 

1. CREATE TABLE cats (
2.     cat_id INT AUTO_INCREMENT,
3.     name VARCHAR(100),
4.     breed VARCHAR(100),
5.     age INT,
6.     PRIMARY KEY (cat_id)
7. ); 

-- Insert some cats:

1. INSERT INTO cats(name, breed, age) 
2. VALUES ('Ringo', 'Tabby', 4),
3.        ('Cindy', 'Maine Coon', 10),
4.        ('Dumbledore', 'Maine Coon', 11),
5.        ('Egg', 'Persian', 4),
6.        ('Misty', 'Tabby', 13),
7.        ('George Michael', 'Ragdoll', 9),
8.        ('Jackson', 'Sphynx', 7);