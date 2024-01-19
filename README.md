[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/AYE28mim)




Database inlamningsuppgift

-----------------------------------


show databases;

create database inlamningsuppgift;

use inlamningsuppgift;

show tables;

Create table if not exists allLibraryCatalogue
(
id bigint primary key auto_increment not null,
title varchar (255) not null unique,
mediaType varchar (100) not null,
author varchar (255) not null,
stocks bigint null,
maxDaysOfRent int
);

create table if not exists USERS
(
id bigint primary key auto_increment not null,
name varchar (255) not null,
email varchar (255) not null unique,
password varchar (255) null);

create table if not exists Log(
id int primary key auto_increment,
activityDate TIMESTAMP not null default CURRENT_TIMESTAMP,
usersId int null,
message text);

create table if not exists usersRent
(
id bigint auto_increment not null,
usersId bigint null,
name varchar(255),
allLibraryCatalogueId bigint null,
title varchar(255),
mediaType varchar(100),
dateBorrowed date default current_date,
dateToBeReturned date default current_date,
primary key (id),
foreign key (usersId) references users(id),
foreign key (allLibraryCatalogueId) references allLibraryCatalogue(id)
);

INSERT INTO allLibraryCatalogue
    (title, mediaType, author, stocks, maxDaysOfRent)
VALUES
    ("The Gifts of Imperfection", "Book", "Brené Brown", 10, 30),
    ("You Are a Badass", "Book", "Jen Sincero", 10, 30),
    ("The Power of Now", "Book", "Eckhart Tolle", 10, 30),
    ("Love Yourself Like Your Life Depends on It", "Book", "Kamal Ravikant", 4, 30),
    ("Radical Self-Love", "Book", "Gala Darling", 4, 30),
    ("Little Fires Everywhere", "Book", "Celeste Ng", 2, 30),
    ("Gone Girl", "Book", "Gillian Flynn", 3, 30),
    ("Big Little Lies", "Book", "Liane Moriarty", 3, 30),
    ("The Girl on the Train", "Book", "Paula Hawkins", 3, 30),
    ("The Great Gatsby", "Book", "F. Scott Fitzgerald", 3, 30),
    ("The Audacity of Hope", "Book", "Barack Obama", 2, 30),
    ("1984", "Book", "George Orwell", 2, 30),
    ("The Road to Wigan Pier", "Book", "George Orwell", 2, 30),
    ("The Federalist Papers", "Book", "Alexander Hamilton, James Madison, John Jay", 2, 30),
    ("The Prince", "Book", "Niccolò Machiavelli", 2, 30),
    ("Meditations", "Book", "Marcus Aurelius", 1, 30),
    ("Sophie's World", "Book", "Jostein Gaarder", 2, 30),
    ("Being and Time", "Book", "Martin Heidegger", 1, 30),
    ("Thus Spoke Zarathustra", "Book", "Friedrich Nietzsche", 1, 30),
    ("The Republic", "Book", "Plato", 4, 30),
    ("Inception", "DVD", "Christopher Nolan", 5, 10),
    ("The Shawshank Redemption", "DVD", "Frank Darabont", 5, 10),
    ("The Dark Knight", "DVD", "Christopher Nolan", 5, 10),
    ("The Godfather", "DVD", "Francis Ford Coppola", 5, 10),
    ("Titanic", "DVD", "James Cameron", 5, 10),
    ("Becoming", "Audio Book", "Michelle Obama", 5, 10),
    ("The Hitchhiker's Guide to the Galaxy", "Audio Book", "Douglas Adams", 5, 10),
    ("Educated", "Audio Book", "Tara Westover", 5, 10),
    ("The Girl with the Dragon Tattoo", "Audio Book", "Stieg Larsson", 5, 10),
    ("Sapiens: A Brief History of Humankind", "Audio Book", "Yuval Noah Harari", 5, 10),
    ("The Legend of Zelda: Breath of the Wild", "Video Game", "Nintendo", 5, 10),
    ("Red Dead Redemption 2", "Video Game", "Rockstar Games", 5, 10),
    ("Fortnite", "Video Game", "Epic Games", 5, 10),
    ("Minecraft", "Video Game", "Mojang", 5, 10),
    ("FIFA 22", "Video Game", "EA Sports", 5, 10);

update allLibraryCatalogue set stocks = 2 where title = "Gone girl";
insert into Users (name, email, password) VALUES
("Greg", "greg.heffley@gritacademy.se", "12345678"),
("Mariam", "mariam.svensson@gritacademy.se", "12345678"),
("Nobita", "nobi.nobita@gritacademy.se", "12345678"),
("Josh", "joshua.farris@gritacademy.se", "12345678");

insert into Users (name, email, password) VALUES
("Suneo", "suneo.takahashi@gritacademy.se", "12345678");



-- logInpage

select name, password from users;

-- Look after the book from the title or author, allLibraryCatalogue

select id, title, mediaType, author, stocks from allLibraryCatalogue where title like "%19%" or author like "%19";

-- borrowing the book
-- if its book, then user has 30 days rent


insert into usersRent
(usersId, name, allLibraryCatalogueId, title, mediaType, dateBorrowed, dateToBeReturned)
select
u.id, u.name, a.id, a.title, a.mediaType, current_date, date_add(Current_date, interval 30 day)
from users u join allLibraryCatalogue a on u.id = 1 and a.id = 19;

-- if mediaType != "book", insert into (dateReminder 10 days) // CHANGE THE INTERVAL

insert into usersRent
(usersId, name, allLibraryCatalogueId, title, mediaType, dateBorrowed, dateToBeReturned)
select
u.id, u.name, a.id, a.title, a.mediaType, current_date, date_add(Current_date, interval 10 day)
from users u join allLibraryCatalogue a on u.id = 1 and a.id = 29;

-- if stocks is == 0 --
-- Sorry the item is currently rent out, please come back again.

-- user can change their profile
-- for name
UPDATE users SET name = "Josh" where name = "Brian";
-- for password
UPDATE users SET password = "newPassword394" where name = "Brian";
--for email
UPDATE email set email = "brian.mccanon@gritacademy.se" where name = "Brian";

