# -A-virtual-website-to-purchase-and-sell-shares-

This is cs50 finance website

The pseudocode are as below:
#1. steps to implement register route
High level requirement:
1. Display form
2. valid passwords
3. Add user to database
4. Log them in

Detailed requirement:
1. Display forms
2. Ensure username, password and confirmation fields are filled, else apologize
3. Ensure inside form password and confirmation field matches
4. store the hash of password using function generate_password_hash
5. Add the username to database
6. check if username already exist in database as below:
result = db.execute(...)
if not result:
return apology("...")
7. db.execute("INSERT INTO users (username, hash) VALUES(:username, :hash)", username = request.form.get("username"),  hash = hash)
8. once registered store their id in session as follows 
session["user_id"]

Note : label.innerhtml is used to display the message inside the form

#2. Steps to implement quote route

High level requirement
1. Display form
2. Retrieve stock quote
3. Display stock quote

Further breaking down:
quote.html
form for stock look up
form input: symbol the user want to lookup

quote = lookup("AAPL")

returns a dict
name
price
symbol

another template indicating following
ensure the stock is valid
else:another apology

Two curly braces inside .html allow us to reference python values

# 3. Steps to implement buy route

High level requirement:
1. Display form
(a). Get stock
(b). Number of shares
2. Add stock to users portfolio
3. Update cash

Further breaking down:
1. Display form
(a). Ask for symbol
(b). check if valid input

2. Add stock to users portfolio
SELECT cash FROM users WHERE id = 1

Buying more of the same stock
INSERT INTO....

In addition to users table we are going to create another table called portfolio/transcation/history 
New SQL table is for the following:
(a). who bought what at what price and when
(b). use appropriate SQLite types
(c). Define UNIQUE indexes on any fields that should be unique
(d). define (non-UNIQUE) indexes on any fields that we may search

3. Update cash
Note- user cash is stored in user table
How to do that?
UPDATE users SET cash = cash - 50 WHERE id = 1

Error in this route: RuntimeError: (sqlite3.OperationalError) no such table: purchases

#4. Steps to implement index route

High level requirement:
 
Display:
1. HTML table with users portfolio
->stock owned
->shares owned for each stock
->current price of each stock
->Total value of each holding
2. users current cash balance
3. Grand total of cash + stock's total value

For display in index.html
Jinja documentation
{% for stock in stocks %}
<p>{{stock.name}}</p>
{% endfor %}

which variables do we need to pass to index.html?


Note- Yes, so  session is a dictionary, session['user_id'] is an integer, which has no indexes and can't be accessed via bracket notation. Hence, removing [0]['cash'] resolves that particular error, which is correct. The user variable is going to be a list of dictionaries (which represent the rows from the database). Therefore, you'd need to pass user[0]['cash'] to the round() function.
If you're unsure at any time what data types you're working with, it's best just to do a temporary print(type(var)) (where var is the variable in question). It'll save you time compared to simply guessing.

#5. steps to implement sell route

1. Display form
2. Remove stock from users portfolio
DELETE FROM 
log sale as a negative quantity
3. UPDATE cash
stock is sold at its current price

#6. steps to implement history route

1.this depends on our implementation of buy and sell
2. chronology of the users interaction
whether a stock was bought or sold, stock's symbol, the purchase or sale price number of shares bought or sold date and time at which the transaction occured
all these info should be there in table inside database structure which we set up






















