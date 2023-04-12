DROP TABLE IF EXISTS users;
DROP TABLE IF EXISTS television_wall_brackets;
DROP TABLE IF EXISTS televisions;
DROP TABLE IF EXISTS remote_controllers;
DROP TABLE IF EXISTS ci_modules;
DROP TABLE IF EXISTS wall_brackets;


CREATE TABLE users (
	id INT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
	name varchar(255) UNIQUE NOT NULL,
	password varchar(255) NOT NULL
);

CREATE TABLE ci_modules (
    id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
	name VARCHAR(255) UNIQUE NOT NULL,
	brand VARCHAR(255),
	price DECIMAL,
	current_stock INT,
	sold INT
);

CREATE TABLE remote_controllers (
    id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
	name VARCHAR(255) UNIQUE NOT NULL,
	brand VARCHAR(255),
	price DECIMAL,
	current_stock INT,
	sold INT,
	compatible_with VARCHAR(255),
	battery_type VARCHAR(255)
);

CREATE TABLE wall_brackets (
    id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
	name VARCHAR(255) UNIQUE NOT NULL,
	brand VARCHAR(255),
	price DECIMAL,
	current_stock INT,
	sold INT,
	adjustable BOOLEAN
);

CREATE TABLE televisions (
	id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
	name VARCHAR(255) UNIQUE NOT NULL,
	brand VARCHAR(255),
	price DECIMAL,
	current_stock INT,
	sold INT,
	type VARCHAR(255),
	available INT,
	refresh_rate DECIMAL,
	screen_type VARCHAR(255),
	ci_id BIGINT,
	rc_id BIGINT,
	CONSTRAINT fk_remote_controllers FOREIGN KEY (rc_id) REFERENCES remote_controllers(id),
	CONSTRAINT fk_ci_modules FOREIGN KEY (ci_id) REFERENCES ci_modules(id)
);

CREATE TABLE television_wall_brackets (
	tv_id BIGINT,
	wall_b_id BIGINT,
	CONSTRAINT fk_televisions FOREIGN KEY (tv_id) REFERENCES televisions(id),
	CONSTRAINT fk_wall_brackets FOREIGN KEY (wall_b_id) REFERENCES wall_brackets(id)
)



