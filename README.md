# URL-Shortner
Introduction
What's a URL Shortener?
URL shortening is a technique to convert a long URL (site or page address) to a shorter version. This shorter version of the URL is usually cleaner and easier to share or remember. When someone accesses the shortened address, the browser redirects to the original (large) url address. It is also called URL redirection or URL redirect.

For example, the large version of this url: http://en.wikipedia.org/wiki/URL_shortening

Can be shortened with bit.do service to this small address, that redirects to the previous longer address: http://bit.do/urlwiki

How does it work?
Essentially, your database has 3 fields: primaryKey, shortCode and targetURL.

Normally the shortCode is simply the primaryKey (which is an int) converted to another base. So for instance base 36 (so 0 through 9, and then 'a' through 'z').

This makes it easy to look up the targetURL in the database, since you can just decode it to base 10 and find the primary key.

You will also have short URLs since the number of URLs you can have is 36^n where n is the number of characters in the shortened URL. So you can see that just with 4 letters you can have a possible of 2,313,441 different URLs. If you use capital letters (a larger base), this gets even larger.

How to use this code?
Make sure you have the latest stable version of Node.js installed
$ sudo npm cache clean -f
$ sudo npm install -g n
$ sudo n stable
Configure your database and jsonwebtoken in config/env. For example config/env/development.js would look like this:
module.exports = {
  mysql: {
    host: 'localhost',
    port: 3306,
    database: 'shortener_dev',
    username: 'root',
    password: '',
  }
};
Fork this repository and clone it
$ git clone https://github.com/<your-user>/node-es6-url-shortener
Navigate into the folder
$ cd node-es6-url-shortener
Install NPM dependencies
$ npm install
Make sure you have a MySQL DB up and running, if you don't, using docker is the easiest way
$ docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -t mysql -d mysql
Login into the container, update the root user and create databases

$ docker exec -it <CONTAINER ID> mysql -uroot
$ ALTER USER root IDENTIFIED WITH mysql_native_password BY 'root';
$ CREATE DATABASE shortener_dev;
$ CREATE DATABASE shortener_dev_dev;
$ CREATE DATABASE shortener_dev_test;
Run the project
$ node index.js
Or use nodemon for live-reload
$ npm start
