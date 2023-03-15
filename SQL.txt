CREATE TABLE films (
    id SERIAL PRIMARY KEY,
    title TEXT NOT NULL,
    original_title TEXT,
    year INTEGER,
    country_id INTEGER REFERENCES countries(id),
    duration INTEGER,
    rating FLOAT,
    description TEXT,
    cover_url TEXT,
    trailer_url TEXT
);

CREATE TABLE person (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    birth_year INTEGER,
    death_year INTEGER
);

CREATE TABLE film_person (
    film_id INTEGER REFERENCES films(id),
    person_id INTEGER REFERENCES person(id),
    role TEXT NOT NULL,
    PRIMARY KEY (film_id, person_id, role)
);

CREATE TABLE genres (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE film_genre (
    film_id INTEGER REFERENCES films(id),
    genre_id INTEGER REFERENCES genres(id),
    PRIMARY KEY (film_id, genre_id)
);

CREATE TABLE countries (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE film_country (
    film_id INTEGER REFERENCES films(id),
    country_id INTEGER REFERENCES countries(id),
    PRIMARY KEY (film_id, country_id)
);

CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT NOT NULL,
    password_hash TEXT NOT NULL
);

CREATE TABLE reviews (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    film_id INTEGER REFERENCES films(id),
    rating INTEGER,
    text TEXT,
    created_at TIMESTAMP
);