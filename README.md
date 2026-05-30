# fom-museum-api (❁´◡`❁)

A web application for [Fields of Mistria](https://fieldsofmistria.wiki.gg/) that helps players track their progress toward completing 
the in-game museum collection. The application uses web scrapers to collect item data and images from the 
wiki for all museum donation items. This data is stored in a SQLite database and served through a FastAPI 
backend, with a React frontend providing an interactive and user-friendly interface.

---

## Project Structure 
```
fom-museum-api/
│
├── app/ # Models and script to populate database + base models to work with API routes
├── data/ # Generated JSON datasets using scrapers
├── frontend/ # Frontend
├── scrapers/ # Scrapers for each wing + image png scraper for each img url stored in JSON
├── static/images # all static images generated and stored here
├── .gitignore
├── database.db # database generated 
├── main.py # API entrypoint
├── README.md
└── requirements.txt # packages txt
```
---

## To run this project

```bash
uvicorn main:app --reload
```
In another terminal, run
```bash
cd frontend
npm run dev
```
Go to this link: http://localhost:5173/  
~ Preview of the webapp:
<img src="repo_img/home.png" alt="description" width="800">
<img src="repo_img/tables.png" alt="description" width="800">

---

## To generate the JSON datasets + img files

```bash
uvicorn main:app --reload
```
Then, follow this link [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
* Generate each wing in ```POST```.
* Refresh each wing in ```POST``` if required.
* The datasets can be found in ```data/``` in the project root.
```bash
python scrapers/img_scraper.py
```
This creates a folder called ```static/``` that contains the image files. It renames the value of 'img_url' in the JSON
files (which are originally stored as URLs) to the location of these image files.
```bash
python -m app.load_data # to generate the database
```
~ This is what the database looks like (screenshot taken from DB Browser for SQLite)
<img src="repo_img/db.png" alt="description" width="800">

---

## Documentation

Swagger UI:  
[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## Endpoints 
| Endpoint               | Description                                          |
|------------------------|------------------------------------------------------|
| `GET /wings`           | List all wings                                       |
| `GET /wings/{wing_id}` | Get a specific wing, and its sets and items          |
| `GET /items/{item_id}` | Mark a specific item as complete/incomplete          |
| `GET /sets/{set_id}`   | Mark a specific set as completed/incomplete          |
| `GET /`                | List all available endpoints for scrapers            |
| `GET /generate/{wing}` | Scrapes data and generates JSON for a specific wing  |


Valid {wing} names for generating JSON:
insects-wing, fish-wing, archaeology-wing, flora-wing

---

## WIP (●'◡'●)
* Frontend for marking an entire set as complete

---
