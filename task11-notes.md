# Task 11 — Docker Volume

- Added a named volume "mysql-data" to docker-compose.yml, mounted at /var/lib/mysql in the db service
- Verified volume creation: docker volume ls -> simple-webapp-flask_mysql-data
- Created test data to verify persistence:
  CREATE TABLE test_table (id INT, name VARCHAR(50));
  INSERT INTO test_table VALUES (1, 'persistence-test');
- Destroyed and recreated the mysql-db container to test persistence:
  docker-compose stop db
  docker-compose rm -f db
  docker-compose up -d db
- Reconnected to MySQL after recreation and confirmed data survived:
  SELECT * FROM test_table; -> still returned (1, 'persistence-test')
- Confirmed Docker named volumes persist data independently of container lifecycle.
