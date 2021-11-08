*This writeup is not complete*

The intended solution for this challenge was to leak enough info about the database to make a fake query that gets the tokens for every user account, which can be used to login as admin and get the flag. 
It was also possible to leak the true flag pdf link or update the token holder for the flag book instead.

It should be pretty easy to see that the token cookie modifies what response back you get from /mybooks.html.
So the idea here will be to use that to get an info leak.
We can think of the query as some select query that is based on the token.
We can use the UNION keyword to append two select queries and merge their results.
One precondition for union is that the results from the two select clauses have the same number of columns, so we can just guess and check until it works.

Once this works we can use some helpful queries that you can find online to leak the table names and table column names for the users table.

Then we use that to query for the admin user account and get the details. Now there should be a book with those details and we can just set our token equal to the admin token and login.

Flag: `gnsCTF{1m_n0t_4_l1z4rd}`
