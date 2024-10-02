Start with Babi khan


گام اول . بالا آوردن خود دیتابیس mesle postgres= ok

version: '3.8'

services:
  db:
    image: postgres:15-alpine  # Use the version you prefer
    container_name: postgres_db
    environment:
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
      POSTGRES_DB: mydatabase
    ports:
      - "5432:5432"  # Map PostgreSQL port
    volumes:
      - db_data:/var/lib/postgresql/data  # Persist data

volumes:
  db_data:



گام دوم . کانفرم کردن گام قبلی که آیا میتوانم بهش وصل بشم = ok با dbeaver ???

docker exec -it postgres-db psql -U myuser -d mydb

گام سوم . دامی دیتا چطور دیتا توش بریزم 
ساخت فایل init.sql
:
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

INSERT INTO users (name, email) VALUES
    ('Alice', 'alice@example.com'),
    ('Bob', 'bob@example.com'),
    ('Charlie', 'charlie@example.com');


گام چهارم کانفرم دامی دیتا = ok :

docker-compose up
docker exec -it postgres-db psql -U myuser -d mydb
SELECT * FROM users;


گام پنجم بکاپ از دامی دیتا = ok 
back up from database  :docker exec -t c19936495cb4  pg_dump -U myuser mydb > /file-bakcup.sql
با پسوند بک آپ: docker exec -t <container_name> pg_dump -U <your_username> -F c <your_database_name> > /path/to/backup/file.backup
docker-compose exec db pg_dump -U myuser mydb > /home/root/backups/mydb_backup.sql

گام ششم چطور کل دیتابیس رو پاک کنم = ok
To delete a specific database inside PostgreSQL, use the DROP DATABASE command inside the PostgreSQL container:
DROP DATABASE mydb;

To delete all data, stop the containers and remove the associated Docker volumes.:
docker-compose down
docker volume rm my_project_postgres_data
docler volume ls

To completely remove the PostgreSQL service, use docker-compose down --volumes:

گام هفتم چطور بکاپم رو ری استور کنم = ok
docker exec -i postgres-db psql -U myuser -d mydb < /home/root/backups/mydb_backup.sql

گام هشتم کانفرم ری استور

گام اضافه: 
Automate Backup with a Script = ok

گام اضافه ، کانفرم

https://dbeaver.io/download/
نرم افزار وصل شدن به دیتابیس های مختلف

$ pass data in python ???

1. Using $ in f-strings (formatted string literals):
Python supports f-strings (introduced in Python 3.6) for string formatting. The dollar sign can appear inside a string, but it doesn't have a special meaning in Python's f-strings.

Example:

python

amount = 100
formatted = f"The total is ${amount}"
print(formatted)
Output:

swift

The total is $100

2. Using string.Template for String Substitution:
Python’s string module provides the Template class, which uses $ for string substitutions.

Example:

python
Copy code
from string import Template

template = Template('Hello, $name!')
result = template.substitute(name='John')
print(result)
Output:

Copy code
Hello, John!
These are the primary ways you might encounter the dollar sign in Python code!