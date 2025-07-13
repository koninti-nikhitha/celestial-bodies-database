# celestial-bodies-database
PostgreSQL database of celestial bodies for freeCodeCamp certification project.
-- Create the database
-- Note: This is only needed if you're starting from scratch
-- CREATE DATABASE universe;

-- Connect to the universe database
\c universe;

-- Drop existing tables to reset
DROP TABLE IF EXISTS moon, planet, star, galaxy;

-- Create galaxy table
CREATE TABLE galaxy (
  galaxy_id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  type VARCHAR(50),
  age_in_millions_of_years INT,
  has_life BOOLEAN
);

-- Create star table
CREATE TABLE star (
  star_id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  type VARCHAR(50),
  galaxy_id INT REFERENCES galaxy(galaxy_id),
  magnitude DECIMAL,
  is_visible BOOLEAN
);

-- Create planet table
CREATE TABLE planet (
  planet_id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  has_life BOOLEAN,
  planet_type VARCHAR(50),
  star_id INT REFERENCES star(star_id),
  distance_from_star NUMERIC
);

-- Create moon table
CREATE TABLE moon (
  moon_id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  planet_id INT REFERENCES planet(planet_id),
  diameter_km NUMERIC
);

-- Insert into galaxy
INSERT INTO galaxy (name, type, age_in_millions_of_years, has_life) VALUES
('Milky Way', 'Spiral', 13600, TRUE),
('Andromeda', 'Spiral', 10100, FALSE),
('Messier 87', 'Elliptical', 13000, FALSE),
('Whirlpool', 'Spiral', 10000, FALSE),
('Sombrero', 'Spiral', 9800, FALSE),
('Pinwheel', 'Spiral', 14000, FALSE);

-- Insert into star
INSERT INTO star (name, type, galaxy_id, magnitude, is_visible) VALUES
('Sun', 'G-type Main-sequence', 1, -26.74, TRUE),
('Alpha Centauri A', 'G2V', 1, 0.01, TRUE),
('Betelgeuse', 'Red Supergiant', 1, 0.42, TRUE),
('Proxima Centauri', 'M-type', 1, 11.13, FALSE),
('Sirius', 'A1V', 1, -1.46, TRUE),
('Vega', 'A0V', 1, 0.03, TRUE);

-- Insert into planet
INSERT INTO planet (name, has_life, planet_type, star_id, distance_from_star) VALUES
('Earth', TRUE, 'Terrestrial', 1, 1.0),
('Mars', FALSE, 'Terrestrial', 1, 1.52),
('Jupiter', FALSE, 'Gas Giant', 1, 5.2),
('Neptune', FALSE, 'Ice Giant', 1, 30.07),
('Proxima b', MAYBE, 'Terrestrial', 4, 0.05),
('Kepler-452b', FALSE, 'Super Earth', 2, 1.04);

-- Insert into moon
INSERT INTO moon (name, planet_id, diameter_km) VALUES
('Moon', 1, 3474),
('Phobos', 2, 22.4),
('Deimos', 2, 12.4),
('Europa', 3, 3121.6),
('Ganymede', 3, 5268),
('Triton', 4, 2706);

