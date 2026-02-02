# Docker Compose Multi-Container Demo

## Services
- **web**: Nginx web server serving a static HTML page
- **web_scaled**: Additional web servers for scaling (internal only)
- **db**: MySQL database

## How to Run
1. Run `docker-compose up -d`
2. Visit http://localhost:8080
3. To scale additional web containers: `docker-compose up -d --scale web_scaled=2`
4. Stop and clean: `docker-compose down`

## Notes
- `volumes` keep data persistent.
- `depends_on` ensures DB starts before the web service.

## Service Interaction Flow
- `web` container serves the website to your browser.
- `web_scaled` containers are additional web servers that share the same code.
- All web containers communicate with the `db` container (MySQL) over Docker’s internal network.
- The database stores persistent data accessed by all web containers.

## Service Interaction Flow Diagram

         +-------------------+
       |     Web (8080)    |
       +-------------------+
                |
                v
       +-------------------+
       |      DB (MySQL)   |
       +-------------------+
                ^
                |
   +-------------------------+
   |   Web_Scaled Containers |
   +-------------------------+

