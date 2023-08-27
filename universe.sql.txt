--WORKING AND COMPELETE DATABASE

DROP DATABASE universe;

CREATE DATABASE universe;

\c universe;

CREATE TABLE galaxy (
   galaxy_id SERIAL PRIMARY KEY,
   name VARCHAR(50) UNIQUE,
   description TEXT,
   location_x NUMERIC NOT NULL,
   location_y NUMERIC NOT NULL,
   type TEXT NOT NULL
);

CREATE TABLE class (
  class_id CHAR(1) PRIMARY KEY,
  name VARCHAR(50) UNIQUE NOT NULL,
  temperature  JSONB,
  chromaticity VARCHAR(50) NOT NULL
);

CREATE TABLE star (
  star_id SERIAL PRIMARY KEY,
  name VARCHAR(50) UNIQUE,
  galaxy_id INT REFERENCES galaxy(galaxy_id),
  class_id CHAR(1) REFERENCES class(class_id),
  description TEXT,
  dead BOOLEAN NOT NULL,
  radius_in_km INT
);

CREATE TABLE planet (
  planet_id SERIAL PRIMARY KEY,
  star_id INT REFERENCES star(star_id),
  name VARCHAR(50) UNIQUE,
  description TEXT,
  habitable BOOLEAN,
  dwaf BOOLEAN NOT NULL,
  radius_in_km INT 
);

CREATE TABLE moon (
  moon_id SERIAL PRIMARY KEY,
  name VARCHAR(50) UNIQUE,
  planet_id INT REFERENCES planet(planet_id),
  description TEXT NOT NULL,
  pericentre NUMERIC
);


------insert statements starts here ------
-- Insert more sample data into the 'galaxy' table
INSERT INTO galaxy (name, description, location_x, location_y, type)
VALUES
  ('Milky Way', 'Our home galaxy', 0, 0, 'Spiral'),
  ('Andromeda', 'Neighboring galaxy', 10, 5, 'Spiral'),
  ('Triangulum', 'Spiral galaxy', -8, -6, 'Spiral'),
  ('Messier 87', 'Elliptical galaxy', 25, 30, 'Elliptical'),
  ('Whirlpool', 'Interacting galaxy', -12, 15, 'Spiral'),
  ('Sombrero', 'Spiral galaxy with dust lane', 14, -7, 'Spiral'),
  ('Centaurus A', 'Active galaxy with dust lane', -18, 22, 'Elliptical'),
  ('Cartwheel', 'Ring galaxy', 35, -15, 'Ring'),
  ('Hoag''s Object', 'Ring galaxy with central starburst', 48, 8, 'Ring'),
  ('Pinwheel', 'Spiral galaxy', -30, -28, 'Spiral'),
  ('Starburst', 'Starburst galaxy', 5, -32, 'Irregular'),
  ('Magellanic Clouds', 'Irregular dwarf galaxies', -40, 10, 'Irregular'),
  ('Bode''s Galaxy', 'Spiral galaxy', -20, 40, 'Spiral'),
  ('Sunflower', 'Spiral galaxy', -10, -38, 'Spiral'),
  ('Leo I', 'Dwarf spheroidal galaxy', -42, 18, 'Dwarf');
  -- ... add more rows ...


-- Insert more sample data into the 'class' table
INSERT INTO class (class_id, name, temperature, chromaticity)
VALUES
  ('O', 'O-Type', '[30000, 50000]', 'Blue'),
  ('B', 'B-Type', '[10000, 30000]', 'Blue-White'),
  ('A', 'A-Type', '[7500, 10000]', 'White'),
  ('F', 'F-Type', '[6000, 7500]', 'Yellow-White'),
  ('G', 'G-Type', '[5200, 6000]', 'Yellow'),
  ('K', 'K-Type', '[3700, 5200]', 'Orange'),
  ('M', 'M-Type', '[2400, 3700]', 'Red'),
  ('L', 'L-Type', NULL, 'Brown'),
  ('T', 'T-Type', NULL, 'Methane'),
  ('Y', 'Y-Type', NULL, 'Cool Red'),
  ('W', 'W-Type', NULL, 'White Dwarf'),
  ('S', 'S-Type', NULL, 'Carbon'),
  ('C', 'C-Type', NULL, 'Carbon'),
  ('D', 'D-Type', NULL, 'White Dwarf'),
  ('Q', 'Q-Type', NULL, 'Cool White'),
  ('P', 'P-Type', NULL, 'Warm White');

-- Insert more sample data into the 'star' table
INSERT INTO star (name, galaxy_id, class_id, description, dead, radius_in_km)
VALUES
  ('Sun', 1, 'G', 'Our star', FALSE, 696340),
  ('Sirius', 1, 'A', 'Brightest star', FALSE, 16738000),
  ('Alpha Centauri A', 1, 'G', 'Closest star system', FALSE, 14417000),
  ('Betelgeuse', 1, 'M', 'Red supergiant', FALSE, 887000000),
  ('Vega', 1, 'A', 'Fifth-brightest star', FALSE, 2360000),
  ('Proxima Centauri', 1, 'M', 'Closest known star', FALSE, 201120),
  ('Canopus', 1, 'F', 'Second-brightest star', FALSE, 7100000),
  ('Rigel', 1, 'B', 'Blue supergiant', FALSE, 9500000),
  ('Arcturus', 1, 'K', 'Orange giant', FALSE, 25600000),
  ('Antares', 1, 'M', 'Red supergiant', FALSE, 883000000),
  ('Aldebaran', 1, 'K', 'Orange giant', FALSE, 44000000),
  ('Polaris', 1, 'F', 'North Star', FALSE, 9000000),
  ('Deneb', 1, 'A', 'Luminous star', FALSE, 2030000),
  ('Bellatrix', 1, 'B', 'Blue giant', FALSE, 3700000),
  ('Achernar', 1, 'B', 'Blue main-sequence', FALSE, 10900000);

-- Insert more sample data into the 'planet' table
INSERT INTO planet (star_id, name, description, habitable, dwaf, radius_in_km)
VALUES
  (1, 'Earth', 'Our home planet', TRUE, FALSE, 6371),
  (2, 'Mars', 'The red planet', FALSE, FALSE, 3389),
  (3, 'Jupiter', 'Largest planet', FALSE, FALSE, 69911),
  (4, 'Neptune', 'Ice giant', FALSE, FALSE, 24622),
  (5, 'Saturn', 'Ringed planet', FALSE, FALSE, 58232),
  (6, 'Mercury', 'Closest to the Sun', FALSE, TRUE, 2439),
  (7, 'Venus', 'Sister planet to Earth', FALSE, FALSE, 6052),
  (8, 'Uranus', 'Ice giant', FALSE, FALSE, 25362),
  (9, 'Pluto', 'Dwarf planet', FALSE, TRUE, 1188),
  (10, 'Kepler-186f', 'Exoplanet', TRUE, FALSE, 6371),
  (11, 'HD 209458 b', 'Hot Jupiter', FALSE, FALSE, 71492),
  (12, 'Gliese 581 c', 'Exoplanet', TRUE, FALSE, 6371),
  (13, 'TRAPPIST-1e', 'Exoplanet', TRUE, FALSE, 6371),
  (14, 'HD 40307 g', 'Exoplanet', TRUE, FALSE, 6371),
  (15, 'WASP-39b', 'Exoplanet', FALSE, FALSE, 74752);

-- Insert more sample data into the 'moon' table
INSERT INTO moon (name, planet_id, description, pericentre)
VALUES
  ('Moon', 1, 'Earth''s natural satellite', 363300),
  ('Phobos', 2, 'Mars''s moon', 9378),
  ('Ganymede', 3, 'Largest moon in the Solar System', 1069200),
  ('Triton', 4, 'Neptune''s moon', 354759),
  ('Titan', 5, 'Saturn''s moon', 1221870),
  ('Io', 3, 'Jupiter''s moon', 420000),
  ('Europa', 3, 'Jupiter''s moon', 664862),
  ('Callisto', 3, 'Jupiter''s moon', 1882700),
  ('Phoebe', 5, 'Saturn''s moon', 12952000),
  ('Charon', 9, 'Pluto''s moon', 19571),
  ('Luna', 7, 'Venus''s moon', 50000),
  ('Miranda', 12, 'Uranus''s moon', 129390),
  ('Enceladus', 5, 'Saturn''s moon', 238042),
  ('Oberon', 12, 'Uranus''s moon', 582600),
  ('Deimos', 2, 'Mars''s moon', 23463),
  ('Moon2', 1, 'Earth''s natural satellite', 363301),
  ('Phobos2', 3, 'Mars''s moon', 9379),
  ('Ganymede2', 4, 'Largest moon in the Solar System', 1069201),
  ('Triton2', 5, 'Neptune''s moon', 354760),
  ('Titan2', 1, 'Saturn''s moon', 1221871),
  ('Io2', 6, 'Jupiter''s moon', 420001),
  ('Europa2', 7, 'Jupiter''s moon', 664863),
  ('Callisto2', 8, 'Jupiter''s moon', 1882701),
  ('Phoebe2', 9, 'Saturn''s moon', 12952001),
  ('Charon2', 10, 'Pluto''s moon', 19572),
  ('Luna2', 11, 'Venus''s moon', 50001),
  ('Miranda2', 12, 'Uranus''s moon', 129391),
  ('Enceladus2', 13, 'Saturn''s moon', 238043),
  ('Oberon2', 14, 'Uranus''s moon', 582601),
  ('Deimos2', 15, 'Mars''s moon', 23464);